---
layout: post
title: "Elasticsearch hızlı başlangıç"
date: 2015-09-17 12:00:00 +0300
categories: [Elasticsearch, Big data]
---
Geçen yazımızda, Elastic’e hızlı bir giriş yapmış, daha doğrusu kısa bir özet sunmuştuk. Şimdi ise, yavaş yavaş bir şeyler yapmaya başlayalım istiyorum. Bunun için, en çok ilgimi çeken bazı Elasticsearch pluginlerini incelemeye ne dersiniz?

Elasticsearch, desteklediği pluginlerle sadece bir veri deposu ve arama motoru olmaktan çıkıp, analitik özellikleri, güvenlik, içerikle ilgili ek özellikler gibi çeşitli boyutlar elde ediyor. Eldeki makineyi modifiye edip yeni aksesuarlarla zenginleştirelim.

## Elasticsearch kurulum
Bu aşamayı aslında atlayabiliriz, fakat sistemsel boyutu olan mimari çözümlerde ayağımızın yere bastığını böyle mi gösteriyoruz ne? Eğer aylık kiralama ücreti ödemeye hazırsanız, Found adlı bulut servis sağlayıcı üzerinden hosted Elastic hizmeti almak mümkündür. Hatta Found’un Elastic tarafından satın alındığını belirtelim.

Bence en kolay kurulum Digital Ocean’ın Elasticsearch paketiyle yapılıyor. Kolaylık olması açısından bağlantı adresini buraya yazıyorum: <a href="https://www.digitalocean.com/community/tutorials/how-to-install-elasticsearch-logstash-and-kibana-4-on-ubuntu-14-04">Digital Ocean &amp; Elastic</a>. Burada ayda 5 USD’ye minimum özellikte sunucu kiralama yapabileceğinizi hatırlatalım.

Burada gençlere kısaca seslenmek isterim. Gençler, Elasticsearch’ü öğrenin. Bakın gelecekte MS SQL, .NET filan bugünün DOS’u, Windows’u gibi olacak. O nedenle yeni yaklaşımlara sürekli açık olun. İşte elinizin altında böyle bir açık kaynak imkan varken gidip en büyük sermayenizi, yani zamanınızı, geleceği olmayan 3 katmanlı mimarilere harcamayın. Big data mimarilerine çalışın. Açık kaynak çalışın ve know how sizin ve herkesin olsun. Elastic ile başlangıç yapabilirsiniz.

Şimdi konuya dönelim. Elastic search’un kurulum kılavuzunu okudunuz mu? Çok güzel, eğer İngilizce sorun teşkil ediyorsa, Chrome tarayıcının Türkçe tercüme özelliğiyle devam edebilirsiniz. Burada yine de önemli bazı adımları belirtmekte fayda var.

Elastic ile bir düğümlü bir küme (tek nodlu cluster) oluşturun. Bu küme sonra büyüyecek. Fakat tüm geliştirme çalışmalarınızı, veri kaynaklarına bağlantıları, geliştirmeleri bu nodda yapacaksınız.

Elastic’i herhangi bir yere, okulunuza, işyerinize, bitirme projenize ve benzeri yerlerde kullanırken minimum üç düğümlü bir küme haline getirmek öneriliyor. Dolayısıyla küme yönetimi konusunu ele alacağız.

Log analizi gibi bir amaçla kullanmak isterseniz, logları toplamanız lazım. Bu amaçla çeşitli log toplama araçlarını inceleyeceğiz. Log toplama işi, envai çeşit sistemde üretilen logların kaydedilip işlenerek merkezi noktalara aktarılmasından ibaret olduğundan, elastic’e işleyeceği verileri sunmayı sağlayan bir adım. Büyük veri işinden biraz farklı bir iş olsa da, veri toplama önemli bir deneyim. Dolayısıyla log toplama ajanlarını yazmak ve geliştirmek, bu işi yeterince iyi yapıyorsanız tam zamanlı işiniz bile olabilir.

Log analizi, bir dönem 5651 yasasıyla beraber pazarlanmaya başlanan, yasal gereksinimleri karşılamak amaçlı bir olguydu. Ama artık 5651 olmadan da, ciddi kuruluşların loglarını kolayca analiz edecekleri yapılara ihtiyaçları var. Çünkü log analizi, bunun adına makine verisi işleme de diyebiliriz, doğru yapıldığında, ciddi anlamda iç görü sağlayan bir yaklaşımdır. Elastic burada açık kaynak olduğundan, cebinizden yüklü lisans maliyeti çıkmadan da bu işleri yapmaya başlayabilirsiniz. Geleceği olan bir platform, sadece bugün X ürünü daha iyi diye düşünmeyin, gelecekte açık kaynak ve hızlı gelişen yaklaşımlar kazanacak. Bugün Elastic’in rakipleri hala konvansiyonel veri ambarı yaklaşımıyla, ETL ile giderken, siz veri gölünüzü biriktirmeye başladınız bile.

Bugünlük bu kadar, ama söz, ilk fırsatta devam edeceğiz. Elastic’le ilgili sorun yaşarsanız veya makaleyi anlamadıysanız iletişime geçebilirsiniz.
