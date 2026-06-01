# Mesai Takip - Capacitor Android Build

Bu proje HTML uygulamasını tam offline çalışan Android APK/AAB'ye dönüştürür.

## 📁 Dosya Yapısı

```
├── www/
│   ├── index.html        # Ana uygulama (internet gerekmez)
│   └── icons/            # Uygulama ikonları
├── capacitor.config.json # Capacitor ayarları
├── package.json
└── .github/
    └── workflows/
        └── build.yml     # Otomatik AAB build
```

## 🔑 GitHub Secrets Kurulumu (Bir kerelik)

Repo → Settings → Secrets and variables → Actions → New repository secret:

### 1. Keystore oluşturun (bilgisayarda):
```bash
keytool -genkey -v -keystore mesai-takip.jks \
  -keyalg RSA -keysize 2048 -validity 10000 \
  -alias mesai-takip
```

### 2. Base64'e çevirin:
```bash
# Linux/Mac:
base64 -w 0 mesai-takip.jks

# Windows (PowerShell):
[Convert]::ToBase64String([IO.File]::ReadAllBytes("mesai-takip.jks"))
```

### 3. Şu 4 secret'ı ekleyin:
| Secret Adı | Değer |
|---|---|
| `SIGNING_KEY` | Base64 çıktısı |
| `KEY_ALIAS` | mesai-takip |
| `KEY_STORE_PASSWORD` | Keystore şifresi |
| `KEY_PASSWORD` | Key şifresi |

## 🚀 Build Alma

1. Bu dosyaları GitHub'a yükleyin
2. Secrets'ları ekleyin
3. Actions → Build Android AAB → Run workflow
4. Tamamlanınca Artifacts kısmından AAB'yi indirin
5. Play Store'a yükleyin ✅
