# 🎯 <font size="5" color="bf4040" face="verdana"> POD NEDİR ? </font>

<img src = "pod2">

* Pod , Kuberbetes dünyasının temel bir kavramıdır. En küçük ve basit birimi temsil eder. 

* Bir pod bir veya birden fazla konteynerin bir arada çalıştığı ve aynı ağ ve depolama alanını paylaştığı mantıksal bir grup olarak düşünülebilir.

* Genellikle , bir pod içindeki konteynerler birlikte çalışan ve birbirleriyle sıkı bir şekilde entegre olan uygulama bileşenleridir.

* Bu konteynerler, birbirleriyle ve diğer pod'larla iletişim kurarak uygulamanın genel işleyişini sağlar.

* Pod'lar kubernetes'in ölçeklendirme ve yönetim kabiliyetlerini sağlayan temel yapı taşlarıdır.

* Kubernetes, pod'ları otomatik olarak dağıtabilir, yeniden başlatabilir ve ölçeklendirebilir.

* Ayrıca , pod'lar kısa ömürlü olabilir ve dinamik bir şekilde oluşturulup silinebilir, bu sayede uygulamanın kaynak tüketimini ve performansını optimize edebiliriz.

## 📌 <font size="4" color="bf4040" face="verdana"> AYNI POD İÇİNDEKİ KONTEYNERLER ARASINDA Kİ İLETİŞİM NASIL SAĞLANIR ? </font>

<img src = "pod1">

* İlk olarak , aynı pod'da çalışan iki konteyneriniz varsa , birbileriyle nasıl konuşur ?

* Bu , localhost ve port numaraları aracılığıyla gerçekleşir. Tıpkı kendi dizüstü bilgisayarınızda birden fazla sunucu çalıştıdığınızda olduğu gibi.

* Pod içindeki konteynerler aynı ağ ad alanında (network namespace) bulunurlar , ağ kaynaklarını (networking resources) paylaşırlar.

## 📌 <font size="4" color="bf4040" face="verdana"> PEKİ AĞ AD ALANI (NETWORK NAMESPACES) NEDİR ? </font>