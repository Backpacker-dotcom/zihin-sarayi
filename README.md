# Zihin Sarayı · İngilizce

Ön büro ekibi için İngilizce eğitim uygulaması: A1 dersleri, Zeytin Otel hikâyesi, otel İngilizcesi, hafıza sarayı ve 64 hazır sınav, 8 Otel İngilizcesi dersi, 21 otel bölümü.
Öğretmen not verir, mesajlaşır, ödev ve kendi sınavını verir. Veriler Firebase Realtime Database'te ekip koduyla tutulur (Turno ile aynı yapı).

- Uygulama: https://backpacker-dotcom.github.io/zihin-sarayi/
- `index.html` uygulamanın kendisidir; bu dosya güncellenince herkes bir sonraki açılışta yeni sürümü görür.

## İlk kurulum (yönetici, bir kez)

1. Uygulamayı aç → **Ekip kur**.
2. **Veritabanı adresi:** Turno'da kullandığın Firebase Realtime Database adresi (`https://…firebasedatabase.app`). Turno'daki kurallar `teams/*` altına yazmaya izin verdiği için yeni proje gerekmez.
3. **Ekip kodu:** otomatik üretilir; Turno'nunkinden farklı ve tahmin edilemez kalsın.
4. Kendi kullanıcı adın ve şifren; öğretmen hesabı (İrem Yıldız) aynı ekranda açılır.
5. Panel › Kullanıcılar'dan ekibi ekle; her kişi için giriş bilgisini WhatsApp'tan gönder.

## Güvenlik notu

Şifreler veritabanında düz metin değil, karma (hash) olarak tutulur. Ancak Turno'daki gibi veriye erişim ekip koduna dayanır:
bağlantıyı bilen ve teknik bilgisi olan biri verileri okuyabilir. Ekip bağlantısını yalnızca ekip içinde paylaşın.
