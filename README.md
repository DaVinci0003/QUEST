# PixelQuest - GitHub Üzerinden APK Üretme Rehberi

Bu klasör, telefonunuza **APK olarak kurabileceğiniz** eksiksiz bir Android uygulama projesidir. GitHub üzerinden tek tıkla otomatik olarak APK dosyası (`app-debug.apk`) üretebilirsiniz.

## Adım Adım APK Üretme (GitHub Actions ile):

1. **GitHub'da Yeni Bir Repozitoru (Repository) Oluşturun:**
   - [GitHub.com](https://github.com) adresine gidin ve yeni bir public/private repo açın (Örn: `pixelquest`).

2. **Bu Dosyaları Yükleyin:**
   - İndirdiğiniz bu ZIP dosyasının içindeki tüm dosyaları (`www/`, `.github/`, `config.xml`, `package.json`) doğrudan repozitorunuze yükleyin (Commit edin).
   - *Not: `index.html` dosyası mutlaka `www/` klasörünün içinde olmalıdır.*

3. **APK Derlemesini Bekleyin:**
   - Repozitorunuzde üst menüden **Actions** sekmesine tıklayın.
   - GitHub Actions otomatik olarak **"Build Android APK"** işlemini başlatacaktır (yaklaşık 2-3 dakika sürer).

4. **APK İndirin:**
   - İşlem yeşil tik (başarılı) olduğunda üzerine tıklayın.
   - Sayfanın en altında **Artifacts** kısmında `app-debug` dosyasını göreceksiniz.
   - `app-debug.zip` dosyasını bilgisayarınıza indirin, zip'i açın ve içindeki `app-debug.apk` dosyasını telefonunuza atarak doğrudan yükleyin!
