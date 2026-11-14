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
