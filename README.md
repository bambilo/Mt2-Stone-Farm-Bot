# Metin2 Stone-Farm Bot

Python tabanlı, görüntü işleme (Image Processing) teknikleri kullanarak **Metin2** oyununda Metin taşlarını otomatik olarak tespit eden, kesen ve farm sürecini yöneten bir otomasyon botudur.

> **Not:** Bot, ekran görüntülerini sürekli analiz ederek çalıştığı için yüksek CPU kullanımı gerektirir. Düşük donanımlı sistemlerde performans düşebilir veya bot beklenen verimlilikte çalışmayabilir.

---

# Özellikler

* 🤖 Otomatik hesap girişi
* 🗺️ Belirlenen haritaya otomatik ışınlanma
* 🔍 Kamera döndürerek Metin taşı arama
* ⚔️ Taşı otomatik hedefleme ve kırma
* 🎁 Düşen eşyaları toplama
* ❤️ Ölüm, takılma ve bağlantı kopması kontrolleri
* 🖥️ Aynı anda birden fazla oyun istemcisini yönetebilme (Multi-Client)
* 🧩 Modüler yapılandırma sistemi

---

# Çalışma Mantığı

Bot aşağıdaki adımları sırasıyla gerçekleştirir:

### 1. Giriş

Kayıtlı hesabınıza otomatik giriş yapar.

### 2. Işınlanma

Belirlenen farm haritasına ışınlanır.

### 3. Metin Taşı Arama

Karakter bulunduğu noktada kamerayı döndürerek çevredeki Metin taşlarını görüntü işleme ile tespit eder.

### 4. Saldırı ve Toplama

Bulunan Metin taşını hedef alır, kırar ve düşen eşyaları toplar.

### 5. Durum Kontrolü

Bot çalışma boyunca sürekli olarak;

* Karakter öldü mü?
* Karakter sıkıştı mı?
* Oyun bağlantısı koptu mu?

kontrollerini yaparak gerekli işlemleri uygular.

---

# Önemli Notlar

## Sunucu Koruma Sistemleri

Rubinum gibi bazı sunucu altyapıları, istemciye gönderilen sentetik klavye ve fare girdilerini engellemektedir. Bu tür korumalara sahip sunucularda bot çalışmayabilir.

---

## Sunucu Uyumluluğu

Bot, ağırlıklı olarak **Rubinum altyapısı** için geliştirilmiştir.

Çalışabilmesi için istemcide aşağıdaki özelliklerin bulunması önerilir:

* Hesap bilgilerinin kayıtlı olması
* Işınlanma yüzüğünün bulunması
* Farm yapılacak haritanın uygun yapıda olması

Her PvP sunucusunda doğrudan çalışacağı garanti edilmez.

---

## Arama Sınırı

Bot, gelişmiş bir yol bulma (Pathfinding) algoritmasına sahip değildir.

Sadece bulunduğu konumdan kamerayı döndürerek Metin taşı araması yapmaktadır.

---

## Çözünürlük

Önerilen oyun çözünürlüğü:

```
1024 x 768
```

### 800×600

Arayüz elemanları üst üste geldiği için nesne tespiti hatalı olabilir.

### Daha yüksek çözünürlükler

Görüntü işleme süresi uzayacağı için performans düşebilir.

---

## Binek / At

Botun stabil çalışabilmesi için karakterinizin **ata veya bineğe binmiş** olması gerekmektedir.

---

## Multi-Client

Bot aynı anda birden fazla oyun istemcisini yönetebilir.

Her istemci için ayrı yapılandırma dosyası kullanılmaktadır.

---

## İşletim Sistemi

Projede yalnızca **Windows** üzerinde çalışan bazı kütüphaneler kullanılmıştır.

Linux ve macOS desteği bulunmamaktadır.

---

## Geliştirme Durumu

Proje halen geliştirilmektedir.

Mevcut sürümde bazı ayarlar sabit (hardcoded) tanımlanmıştır ve yapılandırma süreci tamamen otomatik değildir.

---

# Yapılandırma (Configuration)

Botun doğru şekilde çalışabilmesi için proje içerisindeki üç temel yapılandırma dizininin anlaşılması gerekir.

```
clients/
maps/
relatives/
```

---

# 1. relatives

Bu dizin, farklı ekran çözünürlükleri için oyun arayüzündeki elemanların göreceli konumlarını hesaplar.

## Hesaplama Mantığı

```python
def get_relative(top_left, new_top_left, def_pos):
    dif = (def_pos[0] - top_left[0], def_pos[1] - top_left[1])
    pos = (new_top_left[0] + dif[0], new_top_left[1] + dif[1])
    return pos
```

### Parametreler

| Parametre      | Açıklama                                                          |
| -------------- | ----------------------------------------------------------------- |
| `top_left`     | Varsayılan konfigürasyondaki oyun penceresinin sol üst koordinatı |
| `new_top_left` | Mevcut istemcinizin sol üst koordinatı                            |
| `def_pos`      | Hesaplanacak UI elemanının varsayılan koordinatı                  |

---

## Yeni Bir relatives Konfigürasyonu Oluşturma

Farklı çözünürlük kullanıyorsanız aşağıdaki adımları izleyin.

### 1. Ekran Görüntüleri Alın

* Giriş ekranı
* Oyun içi (Metin taşı seçiliyken HP barı açık)
* Karakter ölü ekranı

---

### 2. Koordinatları Belirleyin

Paint.NET veya benzeri bir uygulama kullanarak aşağıdaki koordinatları tespit edin.

| Alan               | Açıklama                          |
| ------------------ | --------------------------------- |
| `top-left`         | Oyun penceresinin sol üst pikseli |
| `window-size`      | İstemci pencere boyutu            |
| `stone-bar-close`  | Hedef HP barındaki kapatma butonu |
| `mini-map`         | Minimap kapatma butonu            |
| `hp`               | HP yazısının başlangıç noktası    |
| `hp-rectangle`     | HP OCR alanı                      |
| `revive-here`      | "Burada Yeniden Doğ" butonu       |
| `revive-rectangle` | Ölüm ekranı OCR alanı             |
| `account1-12`      | Giriş ekranındaki hesap butonları |
| `channel1-8`       | Kanal seçim butonları             |
| `next`             | Sonraki sayfa                     |
| `ork`              | Ork Vadisi                        |
| `red-forest`       | Kızıl Orman                       |
| `area1-8`          | Harita seçim alanları             |

---

# 2. maps

Haritaya özel yapılandırmaları içerir.

| Ayar               | Açıklama                                         |
| ------------------ | ------------------------------------------------ |
| `name`             | Harita adı (clients ile eşleşmelidir)            |
| `stone-sample`     | Aranacak Metin taşının örnek görselleri          |
| `object-detection` | Kullanılacak nesne tespit yöntemi                |
| `hl`               | En iyi eşleşmenin yüksek veya düşük skor mantığı |
| `threshold`        | Eşleşme doğrulama eşiği                          |
| `navigation`       | Haritaya ışınlanırken izlenecek menü adımları    |

> **Not:** Mevcut sürümde taşın kaplaması yerine isminin ekran görüntüsü kullanılmaktadır.

`actions.py` içerisindeki:

```python
loc[1] + 80
```

değeri, hedefleme sırasında kullanılan görsel ofsettir.

Kaplama (texture) üzerinden tespit yapmak isterseniz bu değeri **0** olarak değiştirmeniz gerekir.

---

# 3. clients

Her oyun istemcisi için ayrı bir yapılandırma dosyası bulunur.

## account

İstemciye ait bilgiler.

* enabled
* id
* channel
* username
* map

---

## position

Karakter seçme ekranındaki karakter konumu.

---

## navigation

İstemciye ait navigasyon ayarları.

### task-bar

Windows görev çubuğundaki istemci sırası.

> Görev çubuğunda pencere birleştirme özelliği kapalı olmalıdır.

### top-left

Oyun penceresinin sol üst koordinatı.

### ring

Işınlanma yüzüğünün bulunduğu kısayol.

Örnek:

```
1
2
F1
F2
```

### skills

Yakılacak karakter becerileri.

Örneğin:

* Hava Kılıcı
* Öfke
* Aura
* Büyülü Silah

### horse-skills

Karakter takıldığında kullanılacak binek becerileri.

---

# Kurulum

## Gereksinimler

* Python 3.7 veya üzeri
* Windows İşletim Sistemi

---

## Gerekli Kütüphaneler

Aşağıdaki komutu çalıştırarak gerekli Python paketlerini yükleyebilirsiniz.

```bash
pip install pillow opencv-python pyautogui numpy keyboard imutils pytesseract
```

---

# Desteklenen Platform

| Platform | Destek |
| -------- | ------ |
| Windows  | ✅      |
| Linux    | ❌      |
| macOS    | ❌      |

---

# Uyarı

Bu proje eğitim ve araştırma amacıyla geliştirilmiştir.

Oyunun kullanım şartlarını ihlal edebilecek otomasyon yazılımlarının kullanımı hesap yaptırımlarına neden olabilir. Projeyi kullanmadan önce ilgili sunucunun kurallarını incelemeniz tavsiye edilir.
