# Speak Chain – iPhone kurulumu

Bu klasör, iPhone'da ana ekrana eklenebilen bir web uygulamasıdır. Kurulum üç adımdan oluşur: dosyaları ücretsiz bir adreste yayınlamak, iPhone'da ana ekrana eklemek ve Claude API anahtarını girmek.

## Klasördekiler

| Dosya | Ne işe yarar |
|---|---|
| `index.html` | Uygulamanın kendisi |
| `manifest.webmanifest` | Ana ekran adı, ikonu ve tam ekran görünümü |
| `sw.js` | Uygulamanın internet yokken de açılmasını sağlar (konuşma için yine internet gerekir) |
| `icons/` | Ana ekran ikonları |

## 1. Dosyaları yayınla

Uygulamanın bir `https://` adresinden açılması gerekiyor. İki kolay yol:

### A) GitHub Pages (kalıcı, ücretsiz)
1. github.com'da hesap aç ve **New repository** ile yeni bir depo oluştur (örneğin `speak-chain`). Ücretsiz hesapta Pages için deponun **Public** olması gerekir. API anahtarın kodda olmadığı için bu bir sorun değil.
2. Depoda **Add file > Upload files** ile bu klasördeki tüm dosyaları sürükle (`icons` klasörü dahil, yapı aynı kalmalı). **Commit changes** de.
3. **Settings > Pages** bölümünde *Source* olarak **Deploy from a branch**, branch olarak **main** ve klasör olarak **/(root)** seç, kaydet.
4. Bir iki dakika sonra adresin görünür: `https://kullaniciadin.github.io/speak-chain/`

### B) Netlify Drop (en hızlısı)
1. Bilgisayarda app.netlify.com/drop adresine git.
2. Bu klasörü olduğu gibi sayfaya sürükle. Sana bir adres verir.
3. Kalıcı olması için ücretsiz Netlify hesabı açıp siteyi hesabına bağla.

## 2. iPhone'da ana ekrana ekle
1. Adresi **Safari** ile aç (Chrome'da ana ekrana ekleme farklı çalışır).
2. Paylaş butonuna bas, **Ana Ekrana Ekle**'yi seç.
3. Uygulamayı ana ekrandaki ikondan aç. İlk konuşmada mikrofon ve konuşma tanıma izni isteyecek, izin ver.

## 3. Claude API anahtarı
1. console.anthropic.com adresinde hesap aç. API kullanımı Claude aboneliğinden ayrıdır ve kullandıkça ücretlendirilir, bu yüzden hesaba kredi yüklemen gerekir.
2. **API Keys** bölümünden yeni bir anahtar oluştur (`sk-ant-...`).
3. Console'da bir **harcama limiti** belirle. Anahtar telefonda saklandığı için bu iyi bir güvenlik önlemi.
4. Uygulamada **Ayarlar**'a anahtarı yapıştır ve **Kaydet ve test et**'e bas. "Bağlantı çalışıyor" yazmalı.

Model adları varsayılan olarak `claude-sonnet-5-5` (konuşma ve analiz) ve `claude-haiku-5-5` (hızlı işler). Test "Model bulunamadı" derse console'daki güncel model adını Ayarlar'a yaz.

## Bilmen gerekenler
- **Veriler yalnızca bu telefonda.** Konuşmalar, zincir ve hata defteri telefonun tarayıcı deposunda tutuluyor. Ayarlar'dan ara sıra **Yedeği indir** ile yedek al. Telefon değiştirirsen **Yedekten geri yükle** ile taşırsın.
- **API anahtarı paylaşılmaz.** Sayfanın adresi herkese açık olsa da anahtar yalnızca senin telefonunda saklanıyor. Başkası açarsa kendi anahtarı olmadan kullanamaz.
- **Ses tanıma Safari'nin özelliği.** İnternet bağlantısı gerektirir ve sessiz kaldığında kendiliğinden durabilir. Uygulama bunu fark edip dinlemeyi yeniden başlatmaya çalışır. Uzun bir sessizlikten sonra cevabını kendisi gönderir.
- **İzin tekrarları.** Bazı iOS sürümlerinde ana ekrandan açılan web uygulamaları mikrofon iznini her açılışta yeniden sorabilir.
- **Daha doğal ses için:** iPhone Ayarlar > Erişilebilirlik > Seslendirilen İçerik > Sesler > İngilizce bölümünden "Gelişmiş" (Enhanced) bir ses indir, sonra uygulamanın Ayarlar sayfasından onu seç.
- **Güncelleme:** Dosyaları değiştirip tekrar yüklediğinde, uygulamayı internete bağlıyken açınca yeni sürüm gelir. Gerekirse uygulamayı kapatıp yeniden aç.
- Claude içindeki önceki sürümdeki kayıtlar bu uygulamaya taşınmaz.
