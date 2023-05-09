# 🎯 CONTROL PLANE (MASTER NODE) NEDİR ?

<p align ="center">
<img src = "cont4">
</p>

* Kubernetes cluster'ın iki bölümü vardır. Bunlar control plane (master node) ve worker node bölümleridir. Bu yazıda control plane bölümüne değinilecektir.

* Bu iki bölümün görsel olarak özeti şu şekildedir : 

<p align ="center">
<img src = "cont1">
</p>

<p align ="center">
<img src = "cont2">
</p>

* Aslında bunu Worker Node kısmında anlatmam gerekir di ama kubelet terimini bilmeden de master node kısmını anlatmak istemedim.

## 📌 KUBELET NEDİR ?

<p align ="center">
<img src = "cont3">
</p>

* Kubelet, Kubernetes sisteminin önemli bir bileşenidir.

* Kubelet, her bir Kubernetes düğümünde (işlemci ve belleğe sahip bir fiziksel veya sanal makine gibi) çalışan bir ajan görevi görür.

* Kubelet'in temel işlevi, o düğümde çalışacak konteynerlerin sağlığını ve durumunu yönetmektir.

* Bu, düğüme atanmış olan Kubernetes API sunucusundan alınan PodSpec'leri (podların özelliklerini ve yapılandırmasını tanımlayan JSON nesneleri) ile yapılır. API sunucusu birazdan göreceğiz.

* Kubelet, belirli aralıklarla API sunucusundan PodSpec'leri alır ve düğüm üzerindeki konteynerlerin durumunu kontrol eder.

* Eğer konteynerler beklenen durumda değilse, Kubelet eksik veya hatalı konteynerleri düzelterek beklenen duruma getirir.

* Kubelet ayrıca, düğümdeki kaynak kullanımını rapor eder ve bu bilgileri Kubernetes API sunucusu ile paylaşır.

* Bu sayede, Kubernetes kümesi kaynak yönetimi ve planlama kararları alabilir.

* Kubelet'in çalışma şekli kısaca şöyledir:

    1-) API sunucusundan düğüm için PodSpec'leri alır.

    2-) Alınan PodSpec'lerle düğümde çalışan konteynerlerin durumunu karşılaştırır.

    3-) Eksik veya hatalı konteynerleri düzeltecek şekilde, gerekli düzeltmeleri yapar.

    4-) Düğümdeki kaynak kullanımını rapor eder ve bu bilgileri API sunucusuyla paylaşır.

* Kubelet, Kubernetes kümesinin sağlıklı ve düzgün çalışması için kritik bir bileşendir ve konteynerlerin yönetimine ve düğümdeki kaynakların izlenmesine yardımcı olur.

## 📌 MASTER NODE NEDİR ?

<p align ="center">
<img src = "cont5">
</p>

* Kontrol düzlemi (Control plane) bir Kubernetes kümesinin güç merkezidir.

* Kümedeki (Cluster) her bileşenin (component) istenen durumda tutulmasını sağlar. 

* Dahili küme olayları, harici sistemler ve üçüncü taraf uygulamalar hakkında veri alır, ardından verileri işler ve yanıt olarak kararlar alır ve yürütür.

* Kontrol düzlemi (control plane), kapsayıcılı uygulamaları tutan işçi düğümleri (worker node) yönetir ve bakımını yapar.

* Kontrol düzlemine neden ihtiyaç duyduğunuzu anlamak için, kontrol düzleminin her bir parçasının kümenizin uygun şekilde yönetilmesine nasıl katkıda bulunduğunu derinlemesine incelemeniz gerekir.

* Şimdi gelelim kontrol düzleminin önemli parçalarına.

## 📌 kubectl NEDİR ?

* Kubernetes'te, kubectl komut satırı aracı (Command Line Interface - CLI), kullanıcıların Kubernetes kümesi ile iletişim kurmalarına ve yönetmelerine yardımcı olan önemli bir araçtır. 

* kubectl, kümeye özel komutlar göndererek ve Kubernetes API'si ile etkileşim kurarak çalışır.

* Kullanıcılar, bu aracı kullanarak Kubernetes kaynaklarını (ör. podlar, hizmetler, düğümler) oluşturmak, güncellemek, silmek ve incelemek için işlemler gerçekleştirebilir.

## 📌 Kube Apiserver ?

* API sunucusu, kontrol düzleminin işçi düğümleri (worker node) ve harici sistemlerle etkileşim kurmak için kullandığı arayüzdür.

* REST uç noktaları aracılığıyla veri paylaşarak Kubernetes API'sini ortaya çıkarır.

* Komut satırı arayüzü, web kullanıcı arayüzü, kullanıcılar ve hizmetler API sunucusu aracılığıyla küme (cluster) ile iletişim kurar.

## 📌 Etcd ?

* Etcd, tüm küme verilerini dağıtılmış bir şekilde kalıcı olarak depolamak için kullanılan güvenilir bir anahtar-değer veri deposudur. 

* Cloud Native Computing Foundation (CNCF) ekosisteminde ayrı bir açık kaynak hizmeti olmasına rağmen, Kubernetes'te, sakladığı bilgilerin son derece hassas olması nedeniyle yalnızca Kube-apiserver aracılığıyla erişilebilir.

* İşçi düğümleri (worker node) tarafından kullanılan yapılandırmayı ve kümeyi yönetmek için kullanılan diğer verileri tutar.

## 📌 Kube Scheduler ?

* Adından da anlaşılacağı gibi, Kube-scheduler işçi düğümlere(worker node) yeni podlar tahsis eder.

* Ayrıca, kaynakları ve iş yükünü işçi düğümler(worker node) arasında dağıtır. 

* Düğümlerin iş yüklerini ne kadar iyi idare ettiklerini izler ve mevcut kaynakları düğümlerle eşleştirir.

* Daha sonra yeni oluşturulan kapsayıcıları (containers) küme düğümlerine (cluster node) planlar.

## 📌 Kube Controller Manager ?

* Kontrol düzlemi, kümenin durumunu izleyen ve kümenin mevcut durumunu istenen durumla eşleşecek şekilde değiştirmeye çalışan denetleyici süreçleri adı verilen dört kontrol döngüsüne sahiptir.

* Kube-controller-manager bir kümedeki denetleyici süreçlerini çalıştırır ve yönetir.

* Bunları yönetmenin karmaşıklığını azaltmak için denetleyiciler tek bir işlemde çalıştırılır:

* Düğüm denetleyicisi (node controller) düğümleri yönetir. Kapanan herhangi bir düğümü yeniden başlatır.

* İş denetleyicisi (job controller) açma-kapama görevlerini fark eder ve bu görevleri çalıştırmak için podlar oluşturur.

* Uç noktalar denetleyicisi (endpoints controller), podları harici olarak açığa çıkarmak için uç nokta nesnelerini oluşturur.

* Hizmet hesabı denetleyicisi (service account controller) ve belirteç denetleyicisi (token controller), yeni oluşturulan bir ad alanıyla etkileşim kurmak için bir hesaba ve API erişim belirtecine ihtiyacınız olduğundan, yeni ad alanlarına erişimi yetkilendirmek için varsayılan hesaplar ve API erişim belirteçleri oluşturur.

## 📌 Cloud Controller Manager ?

* Cloud-controller-manager, kümeyi altta yatan bulut altyapısının API'sine bağlayan ayrı bir bileşendir. 

* Yalnızca Amazon Web Services, Azure veya Google Cloud Platform gibi bulut sağlayıcısına özgü denetleyicileri çalıştırır.

* Bu şekilde, bulut sağlayıcınızla etkileşime giren bileşenler, yalnızca kümenizle etkileşime giren bileşenlerden ayrı tutulur.

* Cloud-controller-manager, karmaşıklığı azaltmak için tek bir işlemde birleştirilen üç denetleyici işleminden oluşur:

* Düğüm denetleyicisi (node controller), varsayılan olarak her beş saniyede bir kontrol ederek bulut sağlayıcısındaki düğümlerin durumunu ve sağlığını izler. Bir düğüm yanıt vermeyi durdurursa, düğüm denetleyicisi düğümün silinip silinmediğini de kontrol eder.

* Rota denetleyicisi (route controller) bulut sağlayıcısında rotalar oluşturur.

* Hizmet denetleyicisi (service controller), bulut altyapısında yük dengeleyicileri oluşturur, günceller ve siler.


