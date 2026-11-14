# Zihin Sarayı · İngilizce

Ön büro ekibi için İngilizce eğitim uygulaması: A1 dersleri, Zeytin Otel hikâyesi, otel İngilizcesi, hafıza sarayı ve 64 hazır sınav, 8 Otel İngilizcesi dersi, 21 otel bölümü.
Öğretmen not verir, mesajlaşır, ödev ve kendi sınavını verir. Veriler Firebase Realtime Database'te ekip koduyla tutulur (Turno ile aynı yapı).

- Uygulama: https://backpacker-dotcom.github.io/zihin-sarayi/
- `index.html` uygulamanın kendisidir; bu dosya güncellenince herkes bir sonraki açılışta yeni sürümü görür.

## İlk kurulum (yönetici, bir kez)

Zihin Sarayı için **ayrı bir Firebase projesi** önerilir (Turno'nun açık kurallarından etkilenmemesi için).

1. console.firebase.google.com → **Proje ekle** (ör. `zihin-sarayi`). Analytics gerekmez.
2. **Authentication** → Get started → Sign-in method → **Email/Password** → Enable → Save.
3. **Realtime Database** → Veritabanı oluştur → konum *europe-west1* → kilitli modda başlat.
4. **Rules** sekmesine `database.rules.json` dosyasının içeriğini yapıştır → **Publish**.
   (Uygulamadaki kurulum ekranında "Kuralları kopyala" düğmesi de aynı metni verir.)
5. ⚙ **Proje ayarları** → Genel → **Web API Key** değerini kopyala.
6. Uygulamayı aç → **Ekip kur** → veritabanı adresi + Web API anahtarı → yönetici hesabın (e-posta önerilir) → Ekibi kur.
7. Panel › Kullanıcılar'dan ekibi ekle; her kişinin giriş bilgisini WhatsApp'tan gönder.

## Güvenlik

- Şifreler Firebase Authentication'da tutulur; uygulama veritabanında şifre ya da şifre karması yoktur.
- Her istek sunucu tarafında `database.rules.json` kurallarıyla denetlenir:
  - Öğrenci yalnızca kendi sonuçlarını, notlarını, mesajlarını, karnelerini ve özel sorularını okuyabilir.
  - Not verme, ödev, sınav hazırlama, içerik düzenleme ve kullanıcı yönetimi yalnızca öğretmen ve yöneticidedir.
  - Öğretmen yalnızca öğrenci hesabı açıp değiştirebilir; öğretmen atamak, ayarlar ve kullanıcı silmek yöneticidedir.
  - Gönderilmiş sınav sonuçları ve mesajlar sonradan değiştirilemez ya da silinemez.
  - Pasifleştirilen kişi ekip verisine anında erişimini kaybeder.
- Sayfa yalnızca Firebase, Google giriş servisleri ve FormSubmit ile konuşabilir (Content-Security-Policy).
- "Ortak bilgisayar" seçeneğiyle girilen oturum, tarayıcı kapanınca ve 30 dakika hareketsizlikte kapanır.
- Otomatik sınav puanları öğrencinin cihazında hesaplanır; resmî değerlendirme için öğretmen notu esas alınmalıdır.

## Yarış, ilan panosu ve çıktılar (3.1)

- **Yarış sekmesi:** Günün yarışması (herkese aynı 10 soru, tek hak, süre yok), Üç Can oyunu, haftalık XP ligi, ekip hedefi, 18 rozet.
- **İlan panosu:** Panel › 📌 İlan sekmesinden sınav sonucu, başarı sıralaması, karne listesi ya da lig tablosu yayınlanır; herkes Yarış sekmesinde görür. Her ilan A4 yazdırılır / PDF yapılır.
- **Yarışmalar (3.2):** Panel › 🏁 Yarışma sekmesinden öğretmen ya da yönetici kendi yarışmasını kurar (hazır bir sınavdan ya da kendi yazdığı sorulardan); tek hak, isteğe bağlı son gün, ödül ve gizli sıralama; bitince sonuç tek dokunuşla ilan panosuna asılır.
- **Ödevler:** kişiye ayrı ayrı gönderme, öğrencinin yazılı cevap teslimi, ödev kâğıdı (cevap anahtarıyla) ve ödev çizelgesi çıktısı.
- **Sınav sonuçları:** öğrenci ve öğretmen için sonuç belgesi çıktısı.

> 3.1 ve 3.2 ile `database.rules.json` güncellendi. Firebase › Realtime Database › Rules sekmesine yeni dosyayı yapıştırıp **Publish** etmek gerekir.

## Yöneticinin gizliliği (3.3)

Yöneticinin (owner) kendi sınav sonuçları, ilerlemesi, günün yarışması ve oyun puanları yalnızca kendisinin okuyabildiği `me/<uid>` dalında tutulur; öğretmen ve öğrenciler bunları göremez, ligde ve sıralamalarda görünmez.
