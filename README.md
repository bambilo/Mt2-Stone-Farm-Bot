
🗡️ Metin2 Stone Farm Bot
Bu proje, görüntü işleme teknikleri kullanarak Metin2 oyununda otomatik Metin taşı kesimi ve farm yapan Python tabanlı bir otomasyon botudur.

⚠️ Önemli Performans Uyarısı: Bot, ekran üzerindeki görüntüleri işlemek ve nesneleri tespit etmek için yüksek CPU gücüne ihtiyaç duyar. Düşük donanımlı bilgisayarlarda yavaş çalışabilir veya düzgün çalışmayabilir.

🛠️ Nasıl Çalışır?
Hesabınıza otomatik olarak giriş yapar (Login).

Doğru haritaya ışınlanır.

Kamerayı döndürerek etrafta Metin taşı arar.

Metin taşını bulup keser ve düşen eşyaları (drop) toplar.

Karakterin ölüp ölmediğini, takılıp takılmadığını veya oyundan atılıp atılmadığını (kick) kontrol eder.

📌 Bilinmesi Gerekenler & Sınırlamalar
PVP Sunucu Uyumluluğu: Rubinum gibi bazı sunucular bu tür komut dizilerinin (script) oyuna girdi göndermesini engellemiştir. Bot her PVP / Resmi sunucuda çalışmayabilir (İlk olarak Rubinum için geliştirilmiştir).

Gereksinimler: Oyuna giriş bilgilerini kaydedebilen bir istemci (client), istediğiniz haritaya ışınlayan bir ışınlanma yüzüğü ve taş kesimi için özel bir harita gereklidir. Bot, haritada rastgele gezerek taş arayacak kadar gelişmiş değildir.

Çözünürlük: Önerilen oyun çözünürlüğü 1024x768'dir. 800x600 çözünürlükte arayüz elemanları üst üste binebilir; daha yüksek çözünürlükler ise görüntü işleme süresini artırır.

At / Binek: Botun sorunsuz çalışması için karakterinizin bir ata/bineğe sahip olması ve üzerine binmiş olması gerekir.

Çoklu İstemci (Multi-Client): Bot, aynı anda birden fazla oyun istemcisini yönetebilir.

İşletim Sistemi: Bot içerisinde kullanılan bazı kütüphaneler sadece Windows üzerinde çalışır.

Geliştirme Durumu: Proje modülerliği düşük ve bazı ayarları kod içerisinde sabitleşmiş (hardcoded) durumdadır.

⚙️ Yapılandırma (Configuration)
Botu doğru şekilde konfigüre etmek için 3 ana klasörün mantığını anlamak gerekir: clients, maps ve relatives.

1. relatives (Göreceli Konumlar)
Bu dosya, belirli ekran çözünürlükleri için piksel koordinatlarını içerir. Bot, varsayılan bir ekran konumunu referans alarak sizin ekranınızdaki minimap, can barı gibi elemanların yerini hesaplar.

Göreceli Konum Hesaplama Mantığı (bmath.py):

Python
def get_relative(top_left, new_top_left, def_pos):
    dif = (def_pos[0] - top_left[0], def_pos[1] - top_left[1])
    pos = (new_top_left[0] + dif[0], new_top_left[1] + dif[1])
    return pos
top_left: Konfigürasyondaki referans istemcinin sol üst konumu.

new_top_left: Sizin gerçek istemcinizin sol üst konumu.

def_pos: Bulunmak istenen elemanın referans konumu.

Kendi Çözünürlüğünüz İçin Konfigürasyon Oluşturma:
Görsel düzenleme programı (örneğin Paint.NET) kullanarak ekran görüntülerinizden şu koordinatları alıp eklemelisiniz:

top-left: Oyun pencerelisinin en sol üst piksel noktası.

window-size: İstemcinin pencere boyutu.

stone-bar-close: Hedef can barındaki kapatma (X) butonu.

mini-map: Minimap kapatma butonu.

hp & hp-rectangle: Taşın kalan canını okumak için oluşturulan dikdörtgen alanı.

revive-here & revive-rectangle: Karakter öldüğünde "Burada Yeniden Doğ" butonunun konumu ve alanı.

account1-12: Giriş ekranındaki kayıtlı hesap konumları.

channel1-8: Kanal (CH) seçim butonları.

2. maps (Harita Ayarları)
name: Haritanın adı.

stone-sample: Aranacak Metin taşının görsellerinin bulunduğu dizin path'i (icons klasöründeki gibi taşın isminin ekran görüntüsü olması önerilir).

hl & threshold: Görüntü eşleştirme (Object Detection) hassasiyet değerleri.

navigation: İlgili haritaya gitmek için menüde yapılması gereken tıklama sırası.

3. clients (İstemci Ayarları)
Her farklı istemci (client) için ayrı bir konfigürasyon dosyası kullanılır:

account: Giriş yapılacak id, channel, map ve username bilgileri.

navigation: Windows görev çubuğundaki yer (task-bar), pencere konumu (top-left) ve ışınlanma yüzüğünün kısayol tuşu (ring -> 1, 2, f1 vb.).

skills: Hava Kılıcı, Öfke veya Şaman kutsamaları gibi otomatik basılacak yetenekler.

horse-skills: Karakter takıldığında kurtulmak için kullanılacak binek yetenekleri.

🚀 Çalıştırma ve Kurulum
Gereksinimler
Sisteminizde Python 3.7 veya üzeri bir sürüm yüklü olmalıdır.

Komut satırını (CMD) açarak gerekli kütüphaneleri yükleyin:

Bash
pip install pillow cv2 opencv-python pyautogui numpy keyboard imutils pytesseract
Botu Başlatma
Kullanmak istediğiniz oyun istemcilerini giriş ekranında (Login screen) açık tutun.

Komut satırına şu komutu yazarak botu başlatın:

Bash
python main.py
Bot çalışmaya başladıktan sonra klavye ve farenize dokunmayın.

Botu durdurmak için CMD penceresine gelip Ctrl + C kombinasyonunu kullanın.

Döngü Sayısı: Bot varsayılan olarak 5000 döngü boyunca çalışır. Süresiz çalıştırmak için main.py içindeki while loop < max_loops: satırını while True: olarak değiştirebilirsiniz.

🛠️ Ek Araçlar (Scripts)
Proje içerisinde yardımcı iki adet ek Python dosyası bulunmaktadır:

cords.py: Ekranda tıkladığınız herhangi bir noktanın piksel koordinatlarını terminale yazdırır (Konfigürasyon hazırlarken koordinat bulmak için kullanılır).

xp.py: Otomatik olarak Boşluk (Space) tuşuna basan ve her 10 saniyede bir Cesaret Pelerini (2 tuşu) kullanan basit bir XP / Slot farm botudur.

Tuşu değiştirmek için: binput.press_button('2')

Pelerin basma sıklığını değiştirmek için: sleep(10)

İstemciyi öne getirmek için görev çubuğu konumu: task_bar = (1291, 1062)
