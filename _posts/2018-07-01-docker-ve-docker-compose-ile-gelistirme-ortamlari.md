---
layout: post
title: "Docker ve Docker Compose ile Geliştirme Ortamları"
date: 2018-07-01 12:00:00 +0300
categories: [Docker, DevOps, Containerization]
---

# Docker ve Docker Compose ile Geliştirme Ortamları

Modern yazılım geliştirme süreçlerinde, uygulamaların farklı ortamlarda (geliştirme, test, üretim) tutarlı bir şekilde çalışmasını sağlamak büyük bir zorluktur. "Benim makinemde çalışıyor" sendromu, geliştiricilerin ve operasyon ekiplerinin karşılaştığı yaygın bir sorundur. Docker ve Docker Compose, bu sorunu çözmek için konteynerizasyon teknolojisini kullanarak taşınabilir, izole ve tutarlı geliştirme ortamları oluşturmayı sağlar. Bu makalede, Docker konteynerizasyonunun temellerini, Docker Compose ile çoklu servis uygulamalarını yönetmeyi ve bu araçların geliştirme süreçlerine nasıl entegre edildiğini detaylandıracağız.

**Docker Nedir? Konteynerizasyonun Temelleri**

Docker, uygulamaları ve tüm bağımlılıklarını (kütüphaneler, çalışma zamanı, sistem araçları, kod vb.) izole edilmiş, hafif ve taşınabilir birimler olan "konteynerler" içinde paketlemeye olanak tanıyan açık kaynaklı bir platformdur.

*   **Konteyner vs. Sanal Makine (VM):** Sanal makineler, her biri kendi işletim sistemine sahip tam bir donanım sanallaştırması sağlarken, konteynerler ana işletim sisteminin çekirdeğini paylaşır ve sadece uygulama katmanını izole eder. Bu, konteynerleri çok daha hafif, hızlı ve kaynak dostu yapar.
*   **Docker Image (İmaj):** Bir uygulamanın çalışması için gerekli tüm kod, çalışma zamanı, kütüphaneler ve bağımlılıkları içeren salt okunur bir şablondur. Dockerfile adı verilen bir metin dosyası ile tanımlanır.
*   **Docker Container (Konteyner):** Bir Docker imajının çalıştırılabilir bir örneğidir. İzole bir ortamda çalışır ve ana sistemden bağımsızdır.

**Docker'ın Avantajları:**

1.  **Tutarlılık:** Uygulamalar, geliştirme ortamından üretime kadar her yerde aynı şekilde çalışır.
2.  **İzolasyon:** Konteynerler birbirinden ve ana sistemden izole edilmiştir, bu da bağımlılık çakışmalarını önler.
3.  **Taşınabilirlik:** Konteyner imajları, Docker'ın kurulu olduğu herhangi bir sistemde çalıştırılabilir.
4.  **Hızlı Dağıtım:** Konteynerler hızlıca başlatılabilir ve durdurulabilir.
5.  **Kaynak Verimliliği:** Sanal makinelere göre daha az kaynak tüketir.

**Docker Compose: Çoklu Servis Uygulamalarını Yönetme**

Modern uygulamalar genellikle birden fazla servisten oluşur (örneğin, bir web uygulaması, bir veri tabanı, bir önbellek servisi). Docker Compose, bu çoklu konteyner uygulamalarını tek bir YAML dosyası kullanarak tanımlamanıza, yapılandırmanıza ve çalıştırmanıza olanak tanıyan bir araçtır.

*   **`docker-compose.yml` Dosyası:** Bu dosya, uygulamanın servislerini, ağlarını ve depolama birimlerini tanımlar. Her servis için kullanılacak Docker imajı, port eşleştirmeleri, ortam değişkenleri ve bağımlılıklar belirtilir.
*   **Tek Komutla Yönetim:** `docker-compose up` komutuyla tüm servisler tek seferde başlatılır, `docker-compose down` ile durdurulur ve kaldırılır.

**Docker Compose'un Avantajları:**

1.  **Kolay Kurulum:** Karmaşık çoklu servis ortamlarını tek bir dosya ile kolayca kurar.
2.  **Tutarlı Geliştirme Ortamı:** Tüm ekip üyeleri aynı geliştirme ortamını kullanır.
3.  **Hızlı Geliştirme Döngüsü:** Servisler arasında hızlıca geçiş yapma ve değişiklikleri test etme imkanı.
4.  **Versiyon Kontrolü:** `docker-compose.yml` dosyası Git gibi versiyon kontrol sistemlerinde saklanabilir.

**Geliştirme Süreçlerine Entegrasyon**

Docker ve Docker Compose, geliştirme süreçlerine aşağıdaki şekillerde entegre edilebilir:

1.  **Yerel Geliştirme Ortamı:** Geliştiriciler, uygulamalarını ve bağımlılıklarını (veri tabanı, mesaj kuyruğu vb.) kendi makinelerinde Docker konteynerleri içinde çalıştırabilir. Bu, "benim makinemde çalışıyor" sorununu ortadan kaldırır.
2.  **Bağımlılık Yönetimi:** Uygulamanın ihtiyaç duyduğu tüm dış servisler (PostgreSQL, Redis, Kafka) Docker Compose ile kolayca ayağa kaldırılabilir.
3.  **Test Ortamları:** Entegrasyon testleri ve uçtan uca (end-to-end) testler, Docker Compose ile oluşturulan izole ortamlarda çalıştırılabilir. Bu, testlerin tutarlı ve tekrarlanabilir olmasını sağlar.
4.  **CI/CD Boru Hatları:** Docker imajları, CI (Sürekli Entegrasyon) sürecinde oluşturulur ve test edilir. CD (Sürekli Dağıtım) sürecinde ise bu imajlar üretim ortamına dağıtılır.
5.  **Mikroservis Geliştirme:** Her mikroservis kendi konteynerinde çalışabilir ve Docker Compose ile tüm mikroservisler bir arada yönetilebilir.

**Örnek Senaryo: Web Uygulaması + Veri Tabanı**

Bir Python/Django web uygulaması ve PostgreSQL veri tabanından oluşan bir sistem için `docker-compose.yml` dosyası şu şekilde olabilir:

```yaml
version: '3.8'
services:
  web:
    build: .
    command: python manage.py runserver 0.0.0.0:8000
    volumes:
      - .:/code
    ports:
      - "8000:8000"
    depends_on:
      - db
    environment:
      - DATABASE_URL=postgresql://user:password@db:5432/mydatabase
  db:
    image: postgres:13
    environment:
      - POSTGRES_DB=mydatabase
      - POSTGRES_USER=user
      - POSTGRES_PASSWORD=password
    volumes:
      - pgdata:/var/lib/postgresql/data
volumes:
  pgdata:
```

Bu dosya ile `docker-compose up` komutu çalıştırıldığında, hem web uygulaması hem de PostgreSQL veri tabanı konteynerleri ayağa kalkar ve birbirleriyle iletişim kurabilir.

**Sonuç**

Docker ve Docker Compose, modern yazılım geliştirme süreçlerinde vazgeçilmez araçlar haline gelmiştir. Konteynerizasyonun sağladığı tutarlılık, izolasyon ve taşınabilirlik avantajları, geliştirme ortamlarının kurulumunu ve yönetimini basitleştirir. Docker Compose ise çoklu servis uygulamalarını tek bir dosya ile yönetme kolaylığı sunar. Bu araçların etkin kullanımı, geliştirici verimliliğini artırır, "benim makinemde çalışıyor" sorununu ortadan kaldırır ve yazılımın farklı ortamlarda güvenilir bir şekilde çalışmasını sağlar.