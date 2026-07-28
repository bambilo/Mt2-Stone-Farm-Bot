<div align="center">

# 🗡️ Metin2 Stone Farm Bot

**Python ve Bilgisayarlı Görü (Computer Vision) kullanılarak geliştirilmiş otomatik Metin Taş kesim otomasyonu.**

[![Python Version](https://img.shields.io/badge/python-3.7+-blue.svg)](https://www.python.org/)
[![Platform](https://img.shields.io/badge/platform-Windows-lightgrey.svg)](https://www.microsoft.com/windows)
[![OpenCV](https://img.shields.io/badge/OpenCV-4.x-green.svg)](https://opencv.org/)
[![Status](https://img.shields.io/badge/status-Archive-orange.svg)](#)

[Özellikler](#-özellikler) • [Gereksinimler](#-gereksinimler) • [Kurulum](#-kurulum--çalıştırma) • [Yapılandırma](#-yapılandırma-configuration) • [Sınırlamalar](#-bilinen-sınırlamalar)

---

</div>

> **⚠️ Donanım Uyarısı:** Bot, ekran üzerindeki görüntüleri anlık işlemek için yüksek CPU gücü tüketir. Düşük donanımlı sistemlerde gecikmeler yaşanabilir.

<br/>

## 🎯 Özellikler

* 🔐 **Otomatik Oturum:** Hesap bilgilerini kullanarak karakter seçimi ve oyuna giriş yapar.
* 🗺️ **Harita Gezinimi:** Belirlenen rotaları izleyerek hedef haritaya ışınlanır.
* 👁️ **Nesne Tespiti:** Ekrandaki Metin Taşlarını görüntü işleme teknikleriyle algılar.
* ⚔️ **Savaş & Toplama:** Taşa odaklanıp kesim gerçekleştirir ve düşen ganimetleri (*drop*) toplar.
* 🛡️ **Güvenlik Kontrolleri:** Karakterin ölme, takılma veya oyundan düşme (*kick*) durumlarını otomatik tespit eder.
* 🖥️ **Multi-Client:** Aynı anda birden fazla oyun penceresini paralel olarak yönetebilir.

<br/>

## 💻 Gereksinimler & Bağımlılıklar

* **İşletim Sistemi:** Windows *(Sadece Windows API kütüphaneleri desteklenmektedir)*
* **Python:** v3.7 veya üzeri
* **Önerilen Ekran Çözünürlüğü:** `1024x768` *(800x600 çözünürlükte arayüz elemanları çakışabilir)*

🚀 Kurulum & Çalıştırma
Oyun istemcilerini Login (Giriş) ekranında hazır tutun.

Terminal/Komut satırını açarak projeyi başlatın:
python main.py

Bot çalışmaya başladığında klavye ve fare müdahalesinde bulunmayın.

Durdurmak için: Terminal penceresine geçip Ctrl + C kombinasyonunu kullanın.

⚙️ Yapılandırma (Configuration)
Botun doğru çalışabilmesi için 3 temel konfigürasyon dizini kullanılır:

• relatives/ : Ekran çözünürlüğünüze göre UI elemanlarının (minimap, hp bar vb.) pikselsel konum bağıntıları.
• maps/ : Hedef harita bilgileri, gezinme tıklamaları ve tanınacak taş görselleri (icons/).
• clients/ : Giriş yapılacak hesap ID'leri, kanal (CH), kısayol tuşları ve skill ayarları.

🔍 Göreceli Konum Hesaplama Mantığı:
Bot, bmath.py içerisindeki algoritma ile referans alınan ekran koordinatlarından sizin ekranınızdaki elemanların yerini türetir:

def get_relative(top_left, new_top_left, def_pos):
dif = (def_pos[0] - top_left[0], def_pos[1] - top_left[1])
pos = (new_top_left[0] + dif[0], new_top_left[1] + dif[1])
return pos

• top_left: Referans konfigürasyondaki sol üst piksel.
• new_top_left: Oyununuzun aktif pencere sol üst pikseli.
• def_pos: Aranacak buton/arayüz elemanının referans koordinatı.

🛠️ Ek Araçlar
Proje dizininde yer alan yardımcı scriptler:

• 📍 cords.py: Ekranda tıklandığı noktanın piksel koordinatlarını terminale yazdırır (Konfigürasyon hazırlığı için).
• ⚡ xp.py: Otomatik olarak Space (Saldırı) ve belirli aralıklarla Cesaret Pelerini basan hafif farm script'i.

⚠️ Bilinen Sınırlamalar
• PVP Sunucu Korumaları: Rubinum gibi bazı sunucularda kullanılan anti-cheat/input engelleme sistemleri botun komut göndermesini engelleyebilir.
• Geliştirme Durumu: Kod mimarisinde bazı değerler sabitleşmiş (hardcoded) durumdadır ve modülerlik kısıtlıdır.




