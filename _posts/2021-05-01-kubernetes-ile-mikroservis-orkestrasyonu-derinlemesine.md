---
layout: post
title: "Kubernetes ile Mikroservis Orkestrasyonu Derinlemesine"
date: 2021-05-01 12:00:00 +0300
categories: [Kubernetes, Microservices, Orchestration, DevOps]
---


Mikroservis mimarileri, modern yazılım geliştirmenin temel taşlarından biri haline gelmiştir. Uygulamaları küçük, bağımsız ve birbiriyle iletişim kuran servisler halinde bölmek, geliştirme hızını, esnektiği ve ölçeklenebilirliği artırır. Ancak, yüzlerce veya binlerce mikroservisi yönetmek, dağıtmak ve ölçeklendirmek karmaşık bir operasyonel zorluktur. İşte bu noktada Kubernetes devreye girer. Kubernetes, konteynerize edilmiş iş yüklerini ve servisleri otomatikleştirmek, dağıtmak, ölçeklendirmek ve yönetmek için açık kaynaklı bir platformdur. Bu makalede, Kubernetes'in temel bileşenlerini, dağıtım stratejilerini, servis keşfini, yük dengelemeyi ve otomatik ölçeklendirme mekanizmalarını derinlemesine inceleyeceğiz.

**Kubernetes Nedir?**

Kubernetes (genellikle K8s olarak kısaltılır), Google tarafından geliştirilen ve Linux Vakfı'na bağışlanan açık kaynaklı bir konteyner orkestrasyon platformudur. Konteynerize edilmiş uygulamaların (Docker gibi) dağıtımını, yönetimini ve ölçeklendirmesini otomatikleştirmek için tasarlanmıştır. Kubernetes, altyapı karmaşıklığını soyutlayarak geliştiricilerin ve operasyon ekiplerinin uygulama dağıtımına odaklanmasını sağlar.

**Kubernetes'in Temel Bileşenleri**

Bir Kubernetes kümesi (cluster), genellikle bir veya daha fazla ana düğüm (master node) ve bir veya daha fazla çalışan düğümden (worker node) oluşur.

**Ana Düğüm (Master Node) Bileşenleri:**

1.  **kube-apiserver:** Kubernetes API'sini sunar. Tüm yönetim istekleri bu bileşen üzerinden geçer. Kümenin ön yüzüdür.
2.  **etcd:** Küme yapılandırma verilerini, durum bilgilerini ve meta verileri saklayan dağıtık bir anahtar-değer deposudur.
3.  **kube-scheduler:** Yeni oluşturulan Pod'ları (konteyner grupları) uygun çalışan düğümlere atar.
4.  **kube-controller-manager:** Çeşitli kontrolörleri çalıştırır (Node Controller, Replication Controller, Endpoints Controller, Service Account Controller). Bu kontrolörler, kümenin istenen durumunu korumakla sorumludur.
5.  **cloud-controller-manager (isteğe bağlı):** Bulut sağlayıcılarına özgü kontrolörleri çalıştırır (örneğin, bulut yük dengeleyicileri, disk provizyonu).

**Çalışan Düğüm (Worker Node) Bileşenleri:**

1.  **kubelet:** Her çalışan düğümde çalışan bir ajandır. Ana düğümden gelen Pod spesifikasyonlarını alır ve konteynerleri çalıştırır.
2.  **kube-proxy:** Her düğümde çalışan bir ağ proxy'sidir. Kubernetes servisleri için ağ kurallarını yönetir ve Pod'lar arası iletişimi sağlar.
3.  **Container Runtime:** Konteynerleri çalıştıran yazılımdır (örneğin, Docker, containerd, CRI-O).

**Dağıtım Stratejileri**

Kubernetes, mikroservislerin güvenli ve kesintisiz bir şekilde dağıtılması için çeşitli stratejileri destekler:

1.  **Rolling Update (Kademeli Güncelleme):** Yeni sürüm Pod'ları yavaş yavaş eski sürüm Pod'ların yerini alır. Bu, kesinti süresini minimize eder ve hatalı dağıtımlarda geri alma (rollback) imkanı sunar.
2.  **Recreate (Yeniden Oluşturma):** Tüm eski Pod'lar durdurulur, ardından yeni Pod'lar başlatılır. Kesinti süresi daha uzundur.
3.  **Blue/Green Deployment:** Yeni sürüm (Green) mevcut sürümden (Blue) tamamen ayrı bir ortamda dağıtılır. Testler tamamlandıktan sonra trafik yeni sürüme yönlendirilir. Hatalı durumlarda hızlı geri dönüş imkanı sunar.
4.  **Canary Deployment:** Yeni sürüm, trafiğin küçük bir yüzdesine (örneğin, %5) dağıtılır. Performans ve hata oranları izlenir. Her şey yolundaysa, trafik kademeli olarak artırılır.
5.  **A/B Testing:** Kullanıcıların farklı gruplarına farklı uygulama sürümleri sunularak kullanıcı davranışları analiz edilir.

**Servis Keşfi (Service Discovery)**

Mikroservis mimarilerinde, servislerin birbirini bulması kritik öneme sahiptir. Kubernetes, yerleşik DNS tabanlı servis keşfi sunar:

*   Her servis için otomatik olarak bir DNS adı oluşturulur.
*   Pod'lar, bu DNS adlarını kullanarak diğer servislere erişebilir.
*   `kube-proxy`, servis adlarını Pod IP adreslerine çevirerek yük dengelemeyi sağlar.

**Yük Dengeleme (Load Balancing)**

Kubernetes, gelen trafiği Pod'lar arasında dağıtmak için çeşitli yük dengeleme mekanizmaları sunar:

*   **ClusterIP:** Küme içindeki servisler için dahili bir IP adresi sağlar.
*   **NodePort:** Her çalışan düğümde belirli bir portu açarak servisi dışarıya açar.
*   **LoadBalancer:** Bulut sağlayıcısının yük dengeleyicisini kullanarak servisi dışarıya açar.
*   **Ingress:** HTTP/HTTPS trafiğini küme içindeki servislere yönlendiren bir API nesnesidir. Daha gelişmiş yönlendirme kuralları ve SSL sonlandırma sağlar.

**Otomatik Ölçeklendirme (Auto-Scaling)**

Kubernetes, uygulama ve altyapı kaynaklarını otomatik olarak ölçeklendirme yeteneği sunar:

1.  **Horizontal Pod Autoscaler (HPA):** CPU kullanımı, bellek kullanımı veya özel metrikler gibi ölçütlere göre Pod sayısını otomatik olarak artırır veya azaltır.
2.  **Vertical Pod Autoscaler (VPA):** Pod'ların CPU ve bellek kaynak gereksinimlerini otomatik olarak ayarlar.
3.  **Cluster Autoscaler:** Kümedeki çalışan düğüm sayısını, Pod'ların kaynak ihtiyaçlarına göre otomatik olarak artırır veya azaltır.

**Sonuç**

Kubernetes, mikroservis mimarilerinin karmaşıklığını yönetmek için güçlü ve kapsamlı bir platformdur. Temel bileşenleri, esnek dağıtım stratejileri, otomatik servis keşfi, gelişmiş yük dengeleme ve akıllı otomatik ölçeklendirme mekanizmaları sayesinde, geliştiriciler ve operasyon ekipleri, yüksek performanslı, hataya dayanıklı ve ölçeklenebilir uygulamaları kolayca dağıtabilir ve yönetebilirler. Kubernetes, bulut tabanlı ve konteynerize edilmiş uygulamaların geleceğinde kilit bir rol oynamaya devam edecektir.