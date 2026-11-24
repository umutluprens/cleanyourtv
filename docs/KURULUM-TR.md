# Snug TV hazır APK: ADB'siz kurulum (Türkçe)

Bu sayfa, bu fork'un GitHub Releases sayfasındaki hazır APK'yı bilgisayar ve ADB kullanmadan bir Android TV veya Google TV'ye kurmayı anlatır. Tek APK tüm bu cihazlar için aynıdır.

Snug TV'deki ana ekran, Gathin ve katkıcılarının geliştirdiği [CleanYourTV](https://github.com/Gathin23/cleanyourtv) başlatıcısıdır. Snug TV onun **gayriresmi bir fork'udur**: kodun neredeyse tamamı CleanYourTV'nin, bu fork onu tek APK olarak paketler ve birkaç ayarını değiştirir. Adı İngilizcede "sıcak, rahat" anlamına gelir. Uygulama TV'de **Snug TV** adıyla görünür. Paket adı `io.github.umutluprens.tvhome`, yani asıl projenin uygulamasından (`com.gathin.tvhome`) ayrı bir uygulamadır ve onun üstüne değil yanına kurulur. Erişilebilirlik ayarlarındaki yardımcının adı **Snug TV ana ekranı**'dır (TV İngilizceyse **Snug TV Home**).

## Önce bilmen gerekenler

- APK ana ekranın görünümünü değiştirir: reklam ve öneri satırları gider, uygulamaların sade bir kutu düzeninde durur.
- Gerçek hızlanma ve RAM kazancı **sağlamaz**. Stok ana ekran (Google TV'de launcherx) arka planda çalışmaya devam eder. Örnek ölçüm, Google TV Streamer: launcherx yaklaşık 240 MB, Snug TV yaklaşık 167 MB. Gerçek hızlanma için ADB ile gereksiz uygulamaları kapatmak gerekir (bkz. ana README).
- Her şey geri alınabilir. Sistem dosyalarına dokunulmaz, root gerekmez.

## 1. APK'yı indir

Releases sayfasından `snug-tv-<sürüm>.apk` dosyasını ve yanındaki `.sha256` dosyasını indir. İstersen bilgisayarda doğrula:

```
shasum -a 256 snug-tv-<sürüm>.apk     # macOS
sha256sum snug-tv-<sürüm>.apk         # Linux
certutil -hashfile snug-tv-<sürüm>.apk SHA256   # Windows
```

Çıkan değer `.sha256` dosyasındakiyle aynı olmalı.

## 2. APK'yı TV'ye aktar

Aşağıdakilerden biri yeterli:

- **USB bellek:** APK'yı belleğe kopyala, TV'ye tak, TV'deki bir dosya yöneticisiyle (ör. File Commander, X-plore) aç.
- **Telefondan "Send files to TV":** Uygulamayı hem telefona hem TV'ye kur (Play Store'da ücretsiz), ikisi aynı Wi-Fi'da olsun, telefondan APK'yı gönder, TV'de açıp kur.
- **Downloader (AFTVnews):** TV'de Downloader'ı Play Store'dan kur, Releases sayfasındaki APK bağlantısını adres çubuğuna yaz, indirince kur de.

## 3. Bilinmeyen kaynaklara izin ver

APK'yı açan uygulamaya (dosya yöneticisi, Send files to TV veya Downloader) kurulum izni vermen gerekir. Kurulum sırasında TV genellikle doğrudan o ekrana götürür. Elle açmak için yol cihaza göre değişir, en yaygınları:

- Ayarlar > Uygulamalar > Güvenlik ve kısıtlamalar > Bilinmeyen kaynaklar > ilgili uygulamayı aç
- Google TV: Ayarlar > Gizlilik (veya Uygulamalar) > Güvenlik ve kısıtlamalar > Bilinmeyen kaynaklar

Kurulum bitince bu izni tekrar kapatabilirsin.

## 4. Ana ekran olarak ayarla

### Klasik Android TV (Sony, Philips, Mi Box, çoğu Android TV)

1. Kumandada Home tuşuna bas.
2. Hangi ana ekranın kullanılacağı sorulursa **Snug TV**'yi seç, sonra **Her zaman**'a bas.
3. Soru gelmezse: Ayarlar > Uygulamalar > Varsayılan uygulamalar > Ana ekran uygulaması (menü adı markaya göre değişir) > Snug TV.
4. Stok ana ekran yine de geri geliyorsa aşağıdaki Google TV adımındaki erişilebilirlik ayarını da aç.

### Google TV (Google TV Streamer, Chromecast with Google TV, Google TV'li televizyonlar)

Google TV ana ekran seçtirmez. Bunun yerine uygulamanın erişilebilirlik yardımcısı Home tuşunu ve stok ana ekranı Snug TV'ye yönlendirir:

1. Ayarlar > Sistem > Erişilebilirlik (bazı cihazlarda doğrudan Ayarlar > Erişilebilirlik).
2. **Snug TV ana ekranı**'nı bul ve aç. Listedeki **Snug TV giriş tuşu** başka bir yardımcıdır, ana ekran için onu açma. Android "cihazın tam kontrolü" diye bir uyarı gösterir. Bu, Home tuşunu izleyebilmek için gereken standart erişilebilirlik uyarısıdır. Onayla.
3. Home tuşuna bas: Google TV ana ekranı bir an görünür, sonra Snug TV gelir. ADB'siz kurulumda bu kısa geçiş normaldir. Yeniden başlatınca da aynısı olur.

## Bilinen sınırlar

- **Vestel tabanlı TV'ler (tvlauncher):** Denenen bir cihazda varsayılan ana ekran ayarı, tvlauncher ADB ile kapatılana kadar tutmadı. ADB'siz çözüm yukarıdaki erişilebilirlik ayarı (Snug TV ana ekranı).
- **Bazı Çin pazarı TCL yazılımları** üçüncü parti ana ekranı hiç kabul etmez.
- **Kumandadaki uygulama tuşları** (YouTube, Netflix vb.) bu APK'da yeniden atanmaz. Bu sürüm, basılı tutulan ses tuşunun tekrar etmesi için tuş filtrelemeyi kapalı tutar (`key_filter=false`). Google TV'de bu tuşları stok ana ekran karşılamaya devam eder.
- Stok ana ekran zaten açıkken Home'a basılırsa (ör. yeniden başlatmadan hemen sonra) birkaç saniye stok ekranda kalabilir. Başka bir uygulama açılıp kapanınca veya tekrar Home'a basınca düzelir.
- **Sesli arama (Google TV):** "YouTube'da ... aç" gibi isteklerin sonuçları Google TV'nin kendi ekranında açılır, Snug TV bu ekranı kapatmaz. Oradan bir uygulama açıp Home'a basınca Snug TV'ye dönersin. "Müzik aç" gibi istekler uygulamayı (ör. Spotify) doğrudan açar.
- `restore_key_services` açık gelir ama ADB ile izin verilmeden bir işe yaramaz. Zararı da yoktur.

## Geri alma

1. Ayarlar > Erişilebilirlik > **Snug TV ana ekranı**'nı kapat (açtıysan).
2. Klasik Android TV'de: Ayarlar > Uygulamalar > Varsayılan uygulamalar > Ana ekran uygulaması > stok ana ekranı seç.
3. Ayarlar > Uygulamalar > **Snug TV** > Kaldır.

Home tuşu hemen eski ana ekrana döner. Başka hiçbir şey değişmemiş olur.

## Güncelleme

Yeni sürümü aynı yoldan kurman yeterli, ayarların ve kutu sıralaman korunur. Bu fork'un APK'ları hep aynı anahtarla imzalanır. Asıl projenin uygulaması (`com.gathin.tvhome`) TV'de kuruluysa ona dokunulmaz, ikisi yan yana durabilir. Ana ekran tuşunu hangisinin karşılayacağını erişilebilirlik ayarlarında hangi yardımcıyı açtığın belirler, ikisini birden açma. Not: 3.5-umut.2 ve öncesi **CleanYourTV** adıyla ve `com.gathin.tvhome` paket adıyla geliyordu. 3.5-umut.3'e (Snug TV) geçerken önce erişilebilirlikte **CleanYourTV ana ekranı**'nı kapat, sonra eski uygulamayı kaldır. Kutu sıralaması bir kez sıfırlanır.

## Emeği geçenler

Snug TV, Gathin ve katkıcılarının geliştirdiği CleanYourTV'ye dayanır ve aynı MIT lisansıyla dağıtılır (bkz. `LICENSE`). Upstream proje bilerek hazır APK yayınlamaz, cihaza göre ayarlanmış kurulumu ADB ile yapar. Bu fork'taki hazır APK, ADB kullanamayanlar için ortak varsayılanlarla derlenmiş bir paketlemedir. Sorunlar için önce bu fork'a yaz, upstream'e değil.
