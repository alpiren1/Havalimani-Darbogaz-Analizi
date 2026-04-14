  Projenin Amacı 
Hava alanı yöneticilerinin;

"Hangi saatlerde kapasite artırılmalı?" 
"Güvenlik mi yoksa pasaport gişesi mi daha büyük bir darboğaz (bottleneck) oluşturuyor?" 
"VIP önceliği ve vize sorunları sistemin toplam hızını nasıl etkiliyor?"
gibi sorulara veriye dayalı cevaplar bulmasını sağlamaktır.

  Teknik Özellikler ve Teorik Temel

Uygulama, yöneylem araştırması prensiplerine ve Kuyruk Teorisi (Queuing Theory) temellerine dayanmaktadır.
M/M/c Modeli: Yolcu gelişleri (Poisson), hizmet süreleri (Erlang/Normal) ve çoklu servis noktaları modellenmiştir.
Stokastik Modelleme: Veriler statik bir dosyadan okunmaz; random.expovariate ve random.normalvariate kullanılarak çalışma anında dinamik olarak üretilir.
Öncelik Yönetimi: PriorityResource kullanılarak VIP yolcuların kuyrukta öne geçmesi sağlanmıştır.

  Kurulum ve Çalıştırma

Projeyi yerel makinenizde çalıştırmak için aşağıdaki adımları izleyebilirsinz;
1: Depoyu klonlayın: git clone https://github.com/kullanici-adiniz/havalimani-simulasyonu.git
cd havalimani-simulasyonu
2: Gerekli kütüphaneleri yükleyin: 
a) pip install -r requirements.txt
b) streamlit run app.py

Analiz Kriterleri

Sistem verimliliği şu metriklerle anlık olarak takip edilebilir:
Ortalama Bekleme Süresi: Yolcuların kuyrukta geçirdiği sürelerin ortalaması.
Darboğaz Tespiti: Hangi birimin sistemi daha fazla yavaşlattığının görsel analizi.
Maksimum Bekleme Süresi: En kötü senaryo performans gözlemi.

Kullanılan Teknolojiler

Python: Ana mantık ve simülasyon motoru
SimPy: Olay tabanlı simülasyon kütüphanesi
Streamlit: Dashboard ve web arayüzü
Plotly & Pandas: İstatistiksel veri analizi ve interaktif grafikler

Hazırlayan : Alperen Gülsoy
Ders sorumlusu : Doktor Öğretim Üyesi HÜSEYİN YANIK

