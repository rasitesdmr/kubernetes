# 🎯 POD NEDİR ? 

<p align ="center">
<img src = "https://github.com/rasitesdmr/kubernetes/blob/master/pod-overview/images/prod1.png">


* Pod , Kuberbetes dünyasının temel bir kavramıdır. En küçük ve basit birimi temsil eder. 

* Bir pod bir veya birden fazla konteynerin bir arada çalıştığı ve aynı ağ ve depolama alanını paylaştığı mantıksal bir grup olarak düşünülebilir.

* Genellikle , bir pod içindeki konteynerler birlikte çalışan ve birbirleriyle sıkı bir şekilde entegre olan uygulama bileşenleridir.

* Bu konteynerler, birbirleriyle ve diğer pod'larla iletişim kurarak uygulamanın genel işleyişini sağlar.

* Pod'lar kubernetes'in ölçeklendirme ve yönetim kabiliyetlerini sağlayan temel yapı taşlarıdır.

* Kubernetes, pod'ları otomatik olarak dağıtabilir, yeniden başlatabilir ve ölçeklendirebilir.

* Ayrıca , pod'lar kısa ömürlü olabilir ve dinamik bir şekilde oluşturulup silinebilir, bu sayede uygulamanın kaynak tüketimini ve performansını optimize edebiliriz.

## 📌 AYNI POD İÇİNDEKİ KONTEYNERLER ARASINDA Kİ İLETİŞİM NASIL SAĞLANIR ?

<p align ="center">
<img src = "https://github.com/rasitesdmr/kubernetes/blob/master/pod-overview/images/prod2.png">
</p>

* İlk olarak , aynı pod'da çalışan iki konteyneriniz varsa , birbileriyle nasıl konuşur ?

* Bu , localhost ve port numaraları aracılığıyla gerçekleşir. Tıpkı kendi dizüstü bilgisayarınızda birden fazla sunucu çalıştıdığınızda olduğu gibi.

* Pod içindeki konteynerler aynı ağ ad alanında (network namespace) bulunurlar , ağ kaynaklarını (networking resources) paylaşırlar.

## 📌 PEKİ AĞ AD ALANI (NETWORK NAMESPACES) NEDİR ?

<p align ="center">
<img src = "prod3">
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
<img src = "prod4">
</p>

<p align ="center">
<img src = "prod5">
</p>

<p align ="center">
<img src = "prod6">
</p>