   1. Projenin Amacı ve Kapsamı

Bu çalışma, bir havalimanının en kritik operasyonel noktaları olan Güvenlik Kontrolü ve Pasaport Kontrol istasyonlarındaki yolcu akışını ve oluşan tıkanıklıkları (darboğazları) incelemektedir. Projede SimPy kütüphanesi kullanılarak Kesikli Olay Simülasyonu (Discrete-Event Simulation) modeli kurulmuş ve Streamlit ile dinamik bir Karar Destek Sistemi arayüzü tasarlanmıştır.

   2. Model Yapısı ve Varsayımlar

Yolcu Geliş Süreci: Yolcuların havalimanına varışları arasındaki süre, kuyruk teorisine uygun olarak Üstel Dağılım (random.expovariate) ile modellenmiştir.
Öncelikli Kaynak Yönetimi (Priority Resource): VIP yolcular, havayolu sadakat programları ve business bilet politikalarına uygun olarak sistemde önceliğe (priority=0) sahiptir ve standart yolcuların önüne geçerler.
Stokastik İşlem Süreleri: Güvenlik ve pasaport süreçlerindeki kalabalık ve insan faktörü, uniform (düzgün) rastgele dağılımlarla simüle edilmiştir. Vize problemi olan yolcuların pasaport işlem sürelerine ek gecikme maliyeti yüklenmiştir.

   3. Güncelleme: Mevsimsellik Katmanı (Seasonality)
   
Gerçek hayat senaryolarına tam uyum sağlamak adına modele "Dönemsel Yoğunluk" parametresi entegre edilmiştir. Havalimanı yolcu talebi statik değildir; bayramlar, resmi tatiller ve yaz sezonlarında ekstrem yoğunluklar yaşanır. Modelde bu durum şu çarpanlarla işletilmiştir:
Bayram Tatili (Aşırı Yoğun): Yolcu geliş aralığı frekansı yüzde 70 sıklaşır (Çarpan: 0.3). Sistem parametreleri aynı kalsa bile yolcu yığılması en yüksek seviyeye ulaşır.
Yaz Tatili (Yoğun): Yolcu geliş frekansı yüzde 40 sıklaşır (Çarpan: 0.6).
Normal Sezon: Standart akış parametreleri uygulanır (Çarpan: 1.0).
Düşük Sezon (Sakin): Yolcu gelişleri yüzde 50 seyrelir (Çarpan: 1.5).

   4. Elde Edilen Metrikler ve Görselleştirme
   
Simülasyon çalıştırıldığında anlık olarak şu çıktılar üretilir ve analiz edilir:
Toplam Yolcu Sayısı: Sistemden başarıyla geçen toplam yolcu hacmi.
Ortalama İşlem Süresi: Bir yolcunun havalimanına girişinden pasaporttan çıkışına kadar harcadığı ortalama süre (Darboğazın ana göstergesi).
Kritik Darboğaz Tespiti: Güvenlik ve Pasaport istasyonlarının ortalama bekleme süreleri kıyaslanarak sistemin en zayıf halkası (Birincil Darboğaz) otomatik olarak belirlenir.
Kutu Grafiği (Box Plot Analizi): VIP ve Standart yolcuların toplam süre dağılımları kıyaslanarak PriorityResource yapısının performansı doğrulanır.

  Havalimanı Güvenlik ve Pasaport Kontrolü Darboğaz Analiz Sistemi

Bu proje, bir havalimanının en kritik operasyonel süreçleri olan Güvenlik Kontrolü ve Pasaport Kontrol istasyonlarındaki yolcu akışını simüle eden ve kaynak yetersizliklerini (darboğazları) tespit eden bir Kesikli Olay Simülasyonu (Discrete-Event Simulation) modelidir.
Sistem, SimPy kütüphanesi ile modellenmiş ve teknik olmayan karar vericilerin bile senaryo analizleri yapabilmesi için Streamlit ile interaktif bir web arayüzüne dönüştürülmüştür.

 Öne Çıkan Özellikler

Dinamik Mevsimsellik (Seasonality):** Havalimanı yolcu talebinin statik olmamasından yola çıkılarak; Bayram Tatili, Yaz Sezonu, Normal Sezon ve Düşük Sezon gibi dönemsel yoğunluk çarpanları sisteme entegre edilmiştir.
Öncelikli Kaynak Yönetimi (PriorityResource):** VIP yolcuların sistemde öncelik hakkına sahip olması ve kuyrukların önüne geçmesi simüle edilmiştir.
Stokastik Gecikme Modelleri:** Vize sorunu yaşayan yolcuların pasaport kontrol süreçlerine getirdiği ek rastgele gecikmeler ve operasyonel riskler modellenmiştir.
Anlık Karar Destek Metrikleri:** Simülasyon sonucunda birincil darboğaz noktası otomatik olarak algılanır, ortalama bekleme süreleri hesaplanır ve grafiksel olarak raporlanır.

 Kurulum ve Çalıştırma
Projeyi yerelde çalıştırmak için aşağıdaki adımları sırayla takip edebilirsiniz:

1. Gerekli Kütüphanelerin Kurulumu:
   ```bash
   pip install simpy streamlit pandas plotly

Uygulamayı Başlatma:

Proje klasörünün içinde terminali açarak aşağıdaki komutu çalıştırın:
streamlit run app.py

Giriş Parametreleri (Girdi Modülleri)

Uygulamanın sol panelinden (Sidebar) aşağıdaki 7 temel parametre dinamik olarak değiştirilebilir:
Parametre                       Açıklama
Güvenlik Görevlisi Sayısı      Güvenlik istasyonunda hizmet veren personel miktarı.
Pasaport Memuru Sayısı         Pasaport bankolarında görevli memur miktarı.
Baz Yolcu Geliş Aralığı (Dk)   Yolcuların havalimanına varışları arasındaki temel süre.
Simülasyon Dönemi              Mevsimsellik çarpanını belirler (Örn: Bayram Tatilinde gelişler yüzde 70 sıklaşır).
VIP Yolcu Olasılığı (%)        Gelen yolcuların yüzde kaçının öncelikli olacağı.
Vize Sorunu Olasılığı (%)      Pasaportta ek gecikme yaşayacak yolcu oranı.
Simülasyon Süresi (Dk)         Simülasyonun toplamda ne kadar süre (dakika) çalışacağı.

  Çıktılar ve Analiz Grafikleri

Kritik Darboğaz Göstergesi: Güvenlik ve pasaport istasyonlarının ortalama gecikme sürelerini kıyaslayarak sistemin en zayıf halkasını (Birincil Darboğaz) dinamik olarak ilan eder.
Yolcu Tipi Bazlı Bekleme Süreleri (Box Plot): VIP ve Standart yolcuların toplam sistem sürelerini dağılım olarak göstererek öncelik mekanizmasının doğruluğunu test eder.
İstasyon Ortalama Tıkanıklık Süreleri (Bar Chart): Hangi birimde ortalama kaç dakika kaybedildiğini görselleştirerek havalimanı yönetimine net kaynak tavsiyeleri sunar.

Hazırlayan : Alperen Gülsoy
Ders sorumlusu : Doktor Öğretim Üyesi HÜSEYİN YANIK

