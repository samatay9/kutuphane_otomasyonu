# 📚 Kütüphane Yönetim Sistemi (LibrarySimple)

Modern ve kapsamlı bir kütüphane yönetim sistemi. Windows Forms tabanlı, .NET Framework 4.7.2 ile geliştirilmiş profesyonel bir uygulama.

## 🎯 Özellikler

### 👥 Kullanıcı Yönetimi
- **6 Farklı Rol**: Admin, Kütüphaneci, Muhasebeci, Üye, Öğrenci, Öğretmen
- **Güvenli Kimlik Doğrulama**: SHA-256 şifre hashleme
- **İki Faktörlü Doğrulama (2FA)**: TOTP/Google Authenticator desteği
- **E-posta Doğrulama**: Kayıt sırasında e-posta doğrulama kodu
- **TC Kimlik Doğrulama**: Algoritma tabanlı TC Kimlik validasyonu

### 📖 Kitap Yönetimi
- Kitap ekleme, düzenleme, silme
- Google Books API entegrasyonu
- Çoklu kategori desteği
- Otomatik kategori tahmini
- Görsel kitap kartları
- Gelişmiş arama ve filtreleme

### 🔄 Ödünç/İade Sistemi
- Rol bazlı ödünç süreleri (14-30 gün)
- Rol bazlı kitap limitleri (5-7 kitap)
- Otomatik ceza hesaplama
- Rezervasyon sistemi
- Masa rezervasyonu

### 💰 Finansal Sistem
- Bakiye yönetimi
- IBAN ile ödeme
- Stripe kredi kartı entegrasyonu
- Ceza ödeme sistemi
- Finansal raporlar (Excel/CSV export)
- Gelir-gider grafikleri

### 🔔 Bildirim Sistemi
- Kullanıcı bazlı bildirimler
- Toplu bildirim gönderimi
- Okundu/Okunmadı takibi
- Badge sistemi
- Otomatik bildirimler

### 📊 Raporlama ve İstatistikler
- Kitap raporları
- Üye raporları
- Ödünç raporları
- Finansal raporlar
- İstatistik grafikleri
- Excel/CSV export

### 🎉 Etkinlik Yönetimi
- Etkinlik oluşturma
- Katılımcı kayıt sistemi
- E-posta bildirimleri

### 🎫 Destek Sistemi
- Destek talebi oluşturma
- Talep yanıtlama
- Durum takibi
- Kategori bazlı organizasyon

### ☁️ Yedekleme
- Google Drive entegrasyonu
- Otomatik yedekleme
- Manuel yedekleme

### 📧 Entegrasyonlar
- **SMTP Mail**: E-posta gönderimi
- **VatanSMS**: SMS gönderimi
- **Stripe**: Ödeme işlemleri
- **Google Books API**: Kitap bilgisi çekme
- **Google Drive**: Yedekleme

## 🛠️ Teknolojiler

- **.NET Framework**: 4.7.2
- **UI Framework**: Windows Forms
- **Veritabanı**: SQL Server (LocalDB)
- **UI Kütüphaneleri**:
  - Guna.UI2.WinForms (2.0.4.7)
  - MaterialSkin.2 (2.3.1)
- **Diğer Kütüphaneler**:
  - Microsoft.Extensions.Caching.Memory (10.0.1)
  - Newtonsoft.Json (13.0.3)
  - Google.Apis.Auth (1.68.0)
  - Google.Apis.Drive.v3 (1.68.0.3197)
  - Otp.NET (1.3.0)
  - QRCoder (1.6.0)
  - Stripe.net (43.20.0)
  - EPPlus (7.5.2)

## 📋 Gereksinimler

- Windows 10 veya üzeri
- .NET Framework 4.7.2 veya üzeri
- SQL Server LocalDB veya SQL Server Express
- Visual Studio 2019 veya üzeri (geliştirme için)
- Minimum 4 GB RAM
- 500 MB disk alanı

## 🚀 Hızlı Başlangıç

1. **Projeyi klonlayın veya indirin**
2. **Veritabanını oluşturun** (SQL/create_db.sql dosyasını çalıştırın)
3. **Visual Studio'da açın** (LibrarySimple.sln)
4. **NuGet paketlerini geri yükleyin**
5. **Projeyi derleyin ve çalıştırın**

Detaylı kurulum için [KURULUM.md](KURULUM.md) dosyasına bakın.

## 📖 Dokümantasyon

- **[KURULUM.md](KURULUM.md)**: Detaylı kurulum rehberi
- **[GELISTIRICI_DOKUMANTASYONU.md](GELISTIRICI_DOKUMANTASYONU.md)**: Geliştirici rehberi
- **[PROJE_OZELLIKLERI.txt](PROJE_OZELLIKLERI.txt)**: Tüm özellikler listesi
- **[LibrarySimple.Tests/README.md](LibrarySimple.Tests/README.md)**: Test dokümantasyonu

## 🧪 Testler

Proje 134 unit test içermektedir. Testleri çalıştırmak için:

```bash
dotnet test LibrarySimple.Tests/LibrarySimple.Tests.csproj
```

## 📁 Proje Yapısı

```
LibrarySimple/
├── Forms/              # Windows Forms formları
├── Models/             # Veri modelleri
├── Services/           # Servis sınıfları
├── SQL/               # SQL script'leri
├── Properties/        # Proje özellikleri
├── LibrarySimple.Tests/ # Unit testler
└── Images/            # Resim dosyaları
```

## 🔐 Güvenlik

- SHA-256 şifre hashleme
- TOTP 2FA desteği
- SQL Injection koruması (parametreli sorgular)
- Sistem logları (IP, tarih, kullanıcı)
- Rol bazlı yetkilendirme

## 📊 Performans

- Connection pooling (Min: 10, Max: 200)
- Memory cache sistemi
- Async/await desteği
- NOLOCK hint'leri (read-only sorgular)
- Image caching
- Lazy loading

## 🎨 Tasarım

- Modern UI (Guna.UI2, MaterialSkin)
- Gradient arka planlar
- Shadow decoration
- Rounded corners
- Hover efektleri
- Smooth animasyonlar

## 📝 Lisans

Bu proje eğitim amaçlı geliştirilmiştir.

## 👨‍💻 Geliştirici

Proje, kütüphane yönetimi için kapsamlı bir çözüm sunmak amacıyla geliştirilmiştir.

## 🤝 Katkıda Bulunma

1. Fork edin
2. Feature branch oluşturun (`git checkout -b feature/AmazingFeature`)
3. Commit edin (`git commit -m 'Add some AmazingFeature'`)
4. Push edin (`git push origin feature/AmazingFeature`)
5. Pull Request açın

## 📞 Destek

Sorularınız için issue açabilir veya dokümantasyonu inceleyebilirsiniz.

## 🔄 Güncellemeler

- **v1.0**: İlk sürüm
  - Temel kütüphane yönetimi
  - Kullanıcı yönetimi
  - Ödünç/İade sistemi
  - Finansal sistem
  - Bildirim sistemi

## 📌 Notlar

- Veritabanı yedeği almayı unutmayın!
- Production ortamında connection string'i güvenli bir şekilde saklayın
- API key'leri veritabanında saklanmaktadır (güvenlik için şifreleme önerilir)

---

**Not**: Bu sistem Windows Forms tabanlı bir masaüstü uygulamasıdır. Web versiyonu bulunmamaktadır.

