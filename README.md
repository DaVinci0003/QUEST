# PixelQuest - GitHub Üzerinden APK Üretme Rehberi

Bu klasör, telefonunuza **APK olarak kurabileceğiniz** eksiksiz bir Android uygulama projesidir. GitHub üzerinden tek tıkla otomatik olarak APK dosyası (`app-debug.apk`) üretebilirsiniz.

## Adım Adım APK Üretme (GitHub Actions ile):

1. **GitHub'da Yeni Bir Repozitoru (Repository) Oluşturun:**
   - [GitHub.com](https://github.com) adresine gidin ve yeni bir public/private repo açın (Örn: `pixelquest`).

2. **Bu Dosyaları Yükleyin:**
   - İndirdiğiniz bu ZIP dosyasının içindeki `www/` klasörünü, `config.xml` ve `package.json` dosyalarını doğrudan repozitorunuze yükleyin (Commit edin).

3. **Workflow Dosyasını Oluşturun (GitHub Üzerinden):**
   - GitHub'da repozitorunuzde **"Add file" -> "Create new file"** butonuna tıklayın.
   - Dosya adı olarak tam olarak şunu yazın: `.github/workflows/build-apk.yml` (GitHub bu klasör yapısını otomatik oluşturacaktır).
   - Aşağıdaki Workflow kodunu kopyalayıp yapıştırın ve **"Commit changes"** butonuna basın.

### Workflow Kodu (Kopyalayıp GitHub'a yapıştırın):
```yaml
name: Build Android APK

on:
  push:
    branches: [ main, master ]
  workflow_dispatch:

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout Code
        uses: actions/checkout@v3

      - name: Set up Node.js
        uses: actions/setup-node@v3
        with:
          node-version: '18'

      - name: Install Cordova
        run: npm install -g cordova

      - name: Set up JDK 17
        uses: actions/setup-java@v3
        with:
          distribution: 'temurin'
          java-version: '17'

      - name: Create Cordova Project
        run: |
          cordova create myapp com.pixelquest.app PixelQuest
          cd myapp
          cordova platform add android
          rm -rf www/*
          cp -r ../www/* www/
          cordova build android --debug

      - name: Upload APK Artifact
        uses: actions/upload-artifact@v3
        with:
          name: app-debug
          path: myapp/platforms/android/app/build/outputs/apk/debug/app-debug.apk
```

4. **APK Derlemesini Bekleyin:**
   - Repozitorunuzde üst menüden **Actions** sekmesine tıklayın.
   - GitHub Actions otomatik olarak **"Build Android APK"** işlemini başlatacaktır (yaklaşık 2-3 dakika sürer).

5. **APK İndirin:**
   - İşlem tamamlandığında üzerine tıklayın, en alttaki **Artifacts** kısmından `app-debug` zip'ini indirin, açın ve içindeki `app-debug.apk` dosyasını telefonunuza yükleyin!
