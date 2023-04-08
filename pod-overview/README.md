# 🎯 POD NEDİR ? 

<p align ="center">
<img src = "https://github.com/rasitesdmr/kubernetes/blob/master/pod-overview/images/pod1.png">


* Pod , Kuberbetes dünyasının temel bir kavramıdır. En küçük ve basit birimi temsil eder. 

* Bir pod bir veya birden fazla konteynerin bir arada çalıştığı ve aynı ağ ve depolama alanını paylaştığı mantıksal bir grup olarak düşünülebilir.

* Genellikle , bir pod içindeki konteynerler birlikte çalışan ve birbirleriyle sıkı bir şekilde entegre olan uygulama bileşenleridir.

* Bu konteynerler, birbirleriyle ve diğer pod'larla iletişim kurarak uygulamanın genel işleyişini sağlar.

* Pod'lar kubernetes'in ölçeklendirme ve yönetim kabiliyetlerini sağlayan temel yapı taşlarıdır.

* Kubernetes, pod'ları otomatik olarak dağıtabilir, yeniden başlatabilir ve ölçeklendirebilir.

* Ayrıca , pod'lar kısa ömürlü olabilir ve dinamik bir şekilde oluşturulup silinebilir, bu sayede uygulamanın kaynak tüketimini ve performansını optimize edebiliriz.

## 📌 AYNI POD İÇİNDEKİ KONTEYNERLER ARASINDA Kİ İLETİŞİM NASIL SAĞLANIR ?

<p align ="center">
<img src = "https://github.com/rasitesdmr/kubernetes/blob/master/pod-overview/images/pod2.png">
</p>

* İlk olarak , aynı pod'da çalışan iki konteyneriniz varsa , birbileriyle nasıl konuşur ?

* Bu , localhost ve port numaraları aracılığıyla gerçekleşir. Tıpkı kendi dizüstü bilgisayarınızda birden fazla sunucu çalıştıdığınızda olduğu gibi.

* Pod içindeki konteynerler aynı ağ ad alanında (network namespace) bulunurlar , ağ kaynaklarını (networking resources) paylaşırlar.

## 📌 PEKİ AĞ AD ALANI (NETWORK NAMESPACES) NEDİR ?

<p align ="center">
<img src = "https://github.com/rasitesdmr/kubernetes/blob/master/pod-overview/images/pod3.png">
</p>

* Ağ arabirimlerinin (bir ağdaki iki ekipman parçası arasındaki bağlantılar) ve yönlendirme tablolarının (ağ paketlerinin nereye gönderileceğine ilişkin talimatlar) bir koleksiyonudur.

* Ad alanları faydalıdır çünkü aynı sanal makinede çakışma veya parazit olmadan birçok ağ ad alanına sahip olabilirsiniz.

* Tüm podlarınızın aynı ad alanında 3000 numaralı bağlantı noktasını dinleyen kapsayıcıları çalıştırmasını istemezsiniz . Hepsi çakışır!

* Kubernetes'teki her pod üzerinde çalışan gizli bir konteyner vardır.

* Bu konteynerin 1 numaralı görevi pod üzerindeki diğer tüm konteynerlerin ölmesi durumunda isim alanını açık tutmaktır. Buna duraklatma konteyneri (pause container) denir.

* Böylece her pod kendi ağ isim alanına sahip olur. 

* Aynı poddaki konteynerler aynı ağ isim alanındadır. Bu nedenle kapsayıcılar arasında localhost üzerinden konuşabilirsiniz ve aynı podda birden fazla kapsayıcınız olduğunda bağlantı noktası çakışmalarına dikkat etmeniz gerekir.

* Görsel olarak özetlemem gerekirse : 

<p align ="center">
<img src = "https://github.com/rasitesdmr/kubernetes/blob/master/pod-overview/images/pod4.png">
</p>

<p align ="center">
<img src = "https://github.com/rasitesdmr/kubernetes/blob/master/pod-overview/images/pod5.png">
</p>

<p align ="center">
<img src = "https://github.com/rasitesdmr/kubernetes/blob/master/pod-overview/images/pod6.png">
</p>

## 📌 AYNI DÜĞÜM (NODE) ÜZERİNDEKİ PODLAR ARASINDA İLETİŞİM NASIL SAĞLANIR ?

<p align ="center">
<img src = "https://github.com/rasitesdmr/kubernetes/blob/master/pod-overview/images/pod7.png">
</p>

* Bir düğümdeki (node) her podun kendi ağ ad alanı vardır. Her podun kendi IP adresi vardır.

* Ve her pod, ağ isteklerini iletmek için eth0 adı verilen tamamen normal bir ethernet cihazına sahip olduğunu düşünür. Ancak Kubernetes numara yapıyor - bu sadece sanal bir ethernet bağlantısı.

* Her pod'un eth0 cihazı aslında node'daki sanal bir ethernet cihazına bağlıdır.

* Sanal ethernet cihazı, pod'un ağını node'a bağlayan bir tüneldir. Bu bağlantının iki tarafı vardır - pod tarafında eth0 olarak adlandırılır ve düğüm tarafında vethX olarak adlandırılır.

* Neden X ? Düğümdeki her pod için bir vethX bağlantısı vardır. (Yani veth1, veth2, veth3, vb.)

* Bir pod başka bir düğümün IP adresine istekte bulunduğunda, bu isteği kendi eth0 arayüzü üzerinden yapar. Bu, düğümün ilgili sanal vethX arayüzüne tünel oluşturur.

* Peki o zaman istek diğer pod'a nasıl ulaşır? 

* Düğüm bir ağ köprüsü kullanır.

## 📌 AĞ KÖPRÜSÜ (NETWORK BRIDGE) NEDİR ?

* Bir ağ köprüsü iki ağı birbirine bağlar.

* Bir istek köprüye ulaştığında, köprü bağlı tüm cihazlara (yani pod'lara) orijinal isteği işlemek için doğru IP adresine sahip olup olmadıklarını sorar.

* Her podun kendi IP adresine sahip olduğunu ve kendi IP adresini bildiğini unutmayın

* Cihazlardan biri biliyorsa, köprü bu bilgiyi depolar ve ayrıca ağ talebinin tamamlanması için verileri orijinal geri iletir.

* Kubernetes'te bu köprüye cbr0 adı verilir. 

* Bir düğüm üzerindeki her pod köprünün bir parçasıdır ve köprü aynı düğüm üzerindeki tüm podları birbirine bağlar.

* Görsel olarak özetlemem gerekirse : 

<p align ="center">
<img src = "https://github.com/rasitesdmr/kubernetes/blob/master/pod-overview/images/pod8.png">
</p>

<p align ="center">
<img src = "https://github.com/rasitesdmr/kubernetes/blob/master/pod-overview/images/pod9.png">
</p>

<p align ="center">
<img src = "https://github.com/rasitesdmr/kubernetes/blob/master/pod-overview/images/pod10.png">
</p>

<p align ="center">
<img src = "https://github.com/rasitesdmr/kubernetes/blob/master/pod-overview/images/pod11.png">
</p>

<p align ="center">
<img src = "https://github.com/rasitesdmr/kubernetes/blob/master/pod-overview/images/pod12.png">
</p>

<p align ="center">
<img src = "https://github.com/rasitesdmr/kubernetes/blob/master/pod-overview/images/pod13.png">
</p>