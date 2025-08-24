---
layout: post
title: "AWS Üzerinde Lambda ve Amplify ile Sunucusuz Uygulamalar"
date: 2022-05-01 12:00:00 +0300
categories: [AWS, Serverless, Lambda, Amplify, Cloud]
---


Modern web ve mobil uygulama geliştirme, geleneksel sunucu yönetimi yükünden kurtulmayı ve daha hızlı, ölçeklenebilir ve maliyet etkin çözümler üretmeyi hedeflemektedir. Sunucusuz (serverless) mimariler, bu hedeflere ulaşmada kilit bir rol oynamaktadır. Amazon Web Services (AWS), Lambda ve Amplify gibi hizmetleriyle geliştiricilere güçlü bir sunucusuz uygulama geliştirme platformu sunar. Bu makalede, AWS Lambda ile sunucusuz fonksiyonlar oluşturmayı, AWS Amplify ile frontend ve backend entegrasyonunu ve bu yaklaşımın maliyet optimizasyonu avantajlarını detaylandıracağız.

**Sunucusuz Mimari Nedir?**

Sunucusuz mimari, geliştiricilerin sunucu provizyonu, ölçeklendirme ve bakımı gibi altyapı yönetim görevleriyle uğraşmadan kod yazmasına ve dağıtmasına olanak tanıyan bir bulut yürütme modelidir. Bulut sağlayıcısı (bu durumda AWS), kodun çalıştırılması için gerekli tüm altyapıyı otomatik olarak yönetir. Geliştiriciler sadece kodlarını yazar ve olaylara (HTTP isteği, veri tabanı değişikliği, dosya yükleme vb.) tepki veren fonksiyonlar olarak dağıtır.

**AWS Lambda: Sunucusuz Fonksiyonların Kalbi**

AWS Lambda, sunucusuz mimarinin temel taşıdır. Geliştiricilerin kodlarını (Python, Node.js, Java, Go, C# vb.) küçük, bağımsız fonksiyonlar olarak dağıtmasına olanak tanır. Lambda fonksiyonları, belirli olaylar tarafından tetiklenir ve yalnızca çalıştıkları süre boyunca ücretlendirilir.

**Lambda'nın Avantajları:**

*   **Maliyet Etkinliği:** Sadece kullanılan kaynaklar ve yürütme süresi için ödeme yapılır. Boşta duran sunucular için maliyet oluşmaz.
*   **Otomatik Ölçeklendirme:** Gelen isteklere göre otomatik olarak ölçeklenir, manuel müdahaleye gerek kalmaz.
*   **Yönetim Kolaylığı:** Sunucu provizyonu, yama yönetimi, işletim sistemi güncellemeleri gibi altyapı görevleri AWS tarafından yönetilir.
*   **Hızlı Dağıtım:** Kod değişiklikleri hızlıca dağıtılabilir.

**AWS Amplify: Frontend ve Backend Entegrasyonu**

AWS Amplify, web ve mobil uygulamalar için hızlı ve kolay bir şekilde ölçeklenebilir backend'ler oluşturmayı ve mevcut AWS hizmetleriyle entegre etmeyi sağlayan bir geliştirme platformudur. Frontend geliştiricilerin, kimlik doğrulama, veri depolama, API'ler, dosya depolama ve barındırma gibi backend özelliklerini kolayca uygulamalarına olanak tanır.

**Amplify'ın Temel Bileşenleri:**

1.  **Amplify CLI:** Backend kaynaklarını (Lambda fonksiyonları, API Gateway, DynamoDB, Cognito vb.) yapılandırmak ve dağıtmak için komut satırı aracı.
2.  **Amplify Libraries:** Frontend uygulamalarından (React, Angular, Vue, iOS, Android, Flutter) AWS backend hizmetleriyle etkileşim kurmak için kullanılan JavaScript/TypeScript kütüphaneleri.
3.  **Amplify UI Components:** Kimlik doğrulama akışları gibi yaygın UI desenleri için önceden oluşturulmuş React, Vue, Angular bileşenleri.
4.  **Amplify Hosting:** Statik web siteleri ve sunucu tarafı render (SSR) uygulamaları için tam yönetilen bir barındırma hizmeti. Otomatik CI/CD entegrasyonu sunar.

**Lambda ve Amplify ile Sunucusuz Uygulama Mimarisi**

Tipik bir Lambda ve Amplify tabanlı sunucusuz uygulama mimarisi şu şekilde olabilir:

*   **Frontend:** React, Vue veya Angular gibi bir framework ile geliştirilir ve Amplify Hosting üzerinde barındırılır. Amplify Libraries, frontend'in backend servisleriyle iletişim kurmasını sağlar.
*   **Kimlik Doğrulama:** AWS Cognito, kullanıcı kaydı, girişi ve yetkilendirmesi için kullanılır. Amplify, Cognito ile entegrasyonu basitleştirir.
*   **API Katmanı:** AWS API Gateway, frontend'den gelen HTTP isteklerini alır ve Lambda fonksiyonlarına yönlendirir. Amplify CLI, API Gateway ve Lambda entegrasyonunu otomatik olarak yapılandırır.
*   **Backend Mantığı:** AWS Lambda fonksiyonları, API isteklerini işler, veri tabanıyla etkileşime girer ve iş mantığını yürütür.
*   **Veri Tabanı:** AWS DynamoDB (NoSQL) veya Aurora Serverless (ilişkisel) gibi sunucusuz veri tabanları kullanılır.
*   **Dosya Depolama:** AWS S3, kullanıcı tarafından yüklenen dosyalar veya statik içerikler için kullanılır.

**Maliyet Optimizasyonu**

Lambda ve Amplify ile sunucusuz mimari, maliyet optimizasyonu açısından önemli avantajlar sunar:

*   **Kullandıkça Öde Modeli:** Sadece kodunuz çalıştığında ödeme yaparsınız. Boşta duran sunucular için maliyet oluşmaz.
*   **Otomatik Ölçeklendirme:** Kaynaklar, talebe göre otomatik olarak artırılıp azaltıldığı için gereksiz kapasite için ödeme yapmaktan kaçınılır.
*   **Yönetim Yükünün Azalması:** Altyapı yönetimi AWS tarafından yapıldığı için operasyonel maliyetler düşer.
*   **Ücretsiz Katman (Free Tier):** AWS, Lambda, S3, DynamoDB gibi birçok hizmet için cömert bir ücretsiz katman sunar, bu da başlangıç maliyetlerini düşürür.

**Sonuç**

AWS Lambda ve Amplify, modern web ve mobil uygulamalar için güçlü, ölçeklenebilir ve maliyet etkin sunucusuz çözümler oluşturmak isteyen geliştiriciler için vazgeçilmez araçlardır. Lambda'nın olay tabanlı, kullandıkça öde modeli ve Amplify'ın frontend-backend entegrasyonunu basitleştiren yetenekleri sayesinde, geliştiriciler altyapı karmaşıklığıyla uğraşmak yerine yenilikçi özelliklere ve üstün bir kullanıcı deneyimine odaklanabilirler. Bu sunucusuz yaklaşım, geliştirme hızını artırırken, operasyonel maliyetleri düşürerek işletmelere önemli rekabet avantajları sağlar.