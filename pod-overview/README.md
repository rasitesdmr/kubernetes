# 🎯 POD NEDİR ? 

<img src = "https://github.com/rasitesdmr/kubernetes/blob/master/pod-overview/images/pod2.png">

* Pod , Kuberbetes dünyasının temel bir kavramıdır. En küçük ve basit birimi temsil eder. 

* Bir pod bir veya birden fazla konteynerin bir arada çalıştığı ve aynı ağ ve depolama alanını paylaştığı mantıksal bir grup olarak düşünülebilir.

* Genellikle , bir pod içindeki konteynerler birlikte çalışan ve birbirleriyle sıkı bir şekilde entegre olan uygulama bileşenleridir.

* Bu konteynerler, birbirleriyle ve diğer pod'larla iletişim kurarak uygulamanın genel işleyişini sağlar.

* Pod'lar kubernetes'in ölçeklendirme ve yönetim kabiliyetlerini sağlayan temel yapı taşlarıdır.

* Kubernetes, pod'ları otomatik olarak dağıtabilir, yeniden başlatabilir ve ölçeklendirebilir.

* Ayrıca , pod'lar kısa ömürlü olabilir ve dinamik bir şekilde oluşturulup silinebilir, bu sayede uygulamanın kaynak tüketimini ve performansını optimize edebiliriz.

## 📌 AYNI POD İÇİNDEKİ KONTEYNERLER ARASINDA Kİ İLETİŞİM NASIL SAĞLANIR ?

<img src = "https://github.com/rasitesdmr/kubernetes/blob/master/pod-overview/images/pod1.png">

* İlk olarak , aynı pod'da çalışan iki konteyneriniz varsa , birbileriyle nasıl konuşur ?

* Bu , localhost ve port numaraları aracılığıyla gerçekleşir. Tıpkı kendi dizüstü bilgisayarınızda birden fazla sunucu çalıştıdığınızda olduğu gibi.

* Pod içindeki konteynerler aynı ağ ad alanında (network namespace) bulunurlar , ağ kaynaklarını (networking resources) paylaşırlar.

## 📌 PEKİ AĞ AD ALANI (NETWORK NAMESPACES) NEDİR ?