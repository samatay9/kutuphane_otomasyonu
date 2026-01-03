# 📦 Kurulum Rehberi

Bu dokümantasyon, Kütüphane Yönetim Sistemi'ni kurmak için gerekli adımları içermektedir.

## 📋 İçindekiler

1. [Gereksinimler](#gereksinimler)
2. [Adım Adım Kurulum](#adım-adım-kurulum)
3. [Veritabanı Kurulumu](#veritabanı-kurulumu)
4. [Yapılandırma](#yapılandırma)
5. [İlk Kullanıcı Oluşturma](#ilk-kullanıcı-oluşturma)
6. [Sorun Giderme](#sorun-giderme)

---

## 🔧 Gereksinimler

### Sistem Gereksinimleri

- **İşletim Sistemi**: Windows 10 veya üzeri
- **RAM**: Minimum 4 GB (Önerilen: 8 GB)
- **Disk Alanı**: Minimum 500 MB
- **.NET Framework**: 4.7.2 veya üzeri
- **SQL Server**: LocalDB veya SQL Server Express

### Yazılım Gereksinimleri

- **Visual Studio**: 2019 veya üzeri (geliştirme için)
- **SQL Server Management Studio (SSMS)**: Veritabanı yönetimi için (opsiyonel)

---

## 🚀 Adım Adım Kurulum

### 1. Projeyi İndirin

Projeyi GitHub'dan klonlayın veya ZIP olarak indirin:

```bash
git clone [repository-url]
```

veya

Proje ZIP dosyasını indirip çıkarın.

### 2. .NET Framework Kontrolü

.NET Framework 4.7.2 veya üzeri yüklü olduğundan emin olun:

1. Windows tuşu + R
2. `appwiz.cpl` yazın ve Enter'a basın
3. "Microsoft .NET Framework 4.7.2" veya üzeri sürümün yüklü olduğunu kontrol edin

Eğer yüklü değilse: [.NET Framework İndirme](https://dotnet.microsoft.com/download/dotnet-framework)

### 3. SQL Server LocalDB Kurulumu

SQL Server LocalDB yüklü değilse:

1. [SQL Server Express İndirme](https://www.microsoft.com/tr-tr/sql-server/sql-server-downloads)
2. "Download" butonuna tıklayın
3. "Express" sürümünü seçin
4. Kurulum sırasında "LocalDB" seçeneğini işaretleyin

Kontrol etmek için:

```cmd
sqllocaldb info
```

### 4. Visual Studio'da Projeyi Açın

1. Visual Studio'yu açın
2. `File > Open > Project/Solution`
3. `LibrarySimple.sln` dosyasını seçin
4. Visual Studio projeyi yükleyecektir

### 5. NuGet Paketlerini Geri Yükleyin

Visual Studio otomatik olarak NuGet paketlerini geri yükleyecektir. Eğer yüklemediyse:

1. `Solution Explorer`'da projeye sağ tıklayın
2. `Restore NuGet Packages` seçeneğini seçin

veya

```bash
dotnet restore
```

### 6. Projeyi Derleyin

1. `Build > Build Solution` (Ctrl+Shift+B)
2. Hata olmadığından emin olun

---

## 🗄️ Veritabanı Kurulumu

### Yöntem 1: SQL Script ile (Önerilen)

1. **SQL Server Management Studio (SSMS)** veya **Visual Studio SQL Server Object Explorer**'ı açın
2. LocalDB'ye bağlanın:
   - Server name: `(localdb)\MSSQLLocalDB`
   - Authentication: Windows Authentication
3. `SQL/create_db.sql` dosyasını açın
4. Tüm script'i çalıştırın (F5)

### Yöntem 2: Visual Studio SQL Server Object Explorer

1. Visual Studio'da `View > SQL Server Object Explorer`
2. `(localdb)\MSSQLLocalDB` genişletin
3. `Databases` üzerine sağ tıklayın > `Add New Database`
4. Database name: `libraryDb2`
5. `SQL/create_db.sql` dosyasını açın ve çalıştırın

### Veritabanı Bağlantı String'i

Varsayılan bağlantı string'i `Program.cs` dosyasında tanımlıdır:

```csharp
Server=(localdb)\MSSQLLocalDB;Database=libraryDb2;Trusted_Connection=True;
```

Farklı bir SQL Server kullanıyorsanız, `Program.cs` dosyasındaki `ConnectionString` değişkenini güncelleyin.

---

## ⚙️ Yapılandırma

### 1. Connection String Ayarlama

`Program.cs` dosyasını açın ve connection string'i düzenleyin:

```csharp
public static string ConnectionString = @"Server=(localdb)\MSSQLLocalDB;Database=libraryDb2;Trusted_Connection=True;" +
    "Connection Timeout=30;" +
    "Pooling=true;" +
    "Min Pool Size=10;" +
    "Max Pool Size=200;" +
    "Connection Lifetime=1800;" +
    "MultipleActiveResultSets=true;" +
    "Enlist=true;" +
    "Application Name=LibrarySimple;";
```

**SQL Server Express için örnek:**
```csharp
Server=localhost\SQLEXPRESS;Database=libraryDb2;Trusted_Connection=True;
```

**SQL Server için örnek:**
```csharp
Server=localhost;Database=libraryDb2;User Id=sa;Password=YourPassword;
```

### 2. İlk Çalıştırma

1. Projeyi çalıştırın (F5)
2. Uygulama açıldığında veritabanı tabloları otomatik oluşturulacaktır
3. İlk kullanıcıyı oluşturmak için kayıt formunu kullanın

---

## 👤 İlk Kullanıcı Oluşturma

### Yöntem 1: Kayıt Formu ile

1. Uygulamayı çalıştırın
2. Login formunda "Hesabınız yok mu? Hemen kayıt olun" linkine tıklayın
3. Kayıt formunu doldurun:
   - Kullanıcı adı
   - Şifre
   - E-posta
   - TC Kimlik (opsiyonel)
   - Telefon (opsiyonel)
   - Adres (opsiyonel)
4. E-posta doğrulama kodu girin
5. Kayıt olun

**Not**: İlk kayıt olan kullanıcı otomatik olarak "Member" rolüne atanır.

### Yöntem 2: SQL ile Admin Kullanıcı Oluşturma

1. SSMS'de veritabanına bağlanın
2. Aşağıdaki SQL script'ini çalıştırın:

```sql
-- Admin rolünü oluştur (eğer yoksa)
IF NOT EXISTS (SELECT 1 FROM Roles WHERE RoleName = 'Admin')
BEGIN
    INSERT INTO Roles (RoleName) VALUES ('Admin');
END

-- Admin kullanıcı oluştur
-- Şifre: admin123 (SHA-256 hash)
INSERT INTO Users (Username, PasswordHash, FullName, RoleId)
VALUES (
    'admin',
    '240be518fabd2724ddb6f04eeb1da5967448d7e831c08c8fa822809f74c720a9', -- admin123
    'Sistem Yöneticisi',
    (SELECT RoleId FROM Roles WHERE RoleName = 'Admin')
);
```

**Güvenlik Uyarısı**: İlk girişten sonra şifrenizi değiştirin!

### Şifre Hash'i Oluşturma

Yeni bir şifre hash'i oluşturmak için:

1. Uygulamayı çalıştırın
2. Kayıt formunda şifre girin
3. `DataAccess.HashPassword()` metodunu kullanarak hash oluşturun

veya

C# kodunda:

```csharp
using System.Security.Cryptography;
using System.Text;

string password = "yourpassword";
using (SHA256 sha256Hash = SHA256.Create())
{
    byte[] bytes = sha256Hash.ComputeHash(Encoding.UTF8.GetBytes(password));
    StringBuilder builder = new StringBuilder();
    for (int i = 0; i < bytes.Length; i++)
    {
        builder.Append(bytes[i].ToString("x2"));
    }
    string hash = builder.ToString();
    Console.WriteLine(hash);
}
```

---

## 🔧 Ek Yapılandırmalar

### SMTP Mail Ayarları

1. Uygulamayı çalıştırın ve Admin olarak giriş yapın
2. `Admin Panel > Ayarlar > Mail Ayarları` sekmesine gidin
3. SMTP bilgilerini girin:
   - SMTP Host
   - SMTP Port
   - Kullanıcı Adı
   - Şifre
   - Gönderen E-posta
   - SSL/TLS ayarları
4. "Test Mail Gönder" butonu ile test edin
5. Ayarları kaydedin

### SMS Ayarları (VatanSMS)

1. [VatanSMS](https://www.vatansms.com/) hesabı oluşturun
2. API Key ve Secret alın
3. Admin Panel > Ayarlar > SMS Ayarları
4. API bilgilerini girin
5. "Test SMS Gönder" butonu ile test edin

### Stripe Ödeme Ayarları

1. [Stripe](https://stripe.com/) hesabı oluşturun
2. API Key'leri alın (Test ve Live)
3. Admin Panel > Ayarlar > Stripe Ayarları
4. API Key'leri girin

### Google Drive Yedekleme

1. [Google Cloud Console](https://console.cloud.google.com/) hesabı oluşturun
2. Service Account oluşturun
3. JSON key dosyasını indirin
4. Admin Panel > Ayarlar > Yedekleme Ayarları
5. JSON dosya yolunu ve klasör ID'sini girin

---

## 🐛 Sorun Giderme

### Veritabanı Bağlantı Hatası

**Hata**: "Cannot open database 'libraryDb2'"

**Çözüm**:
1. LocalDB'nin çalıştığından emin olun:
   ```cmd
   sqllocaldb start MSSQLLocalDB
   ```
2. Veritabanının oluşturulduğunu kontrol edin
3. Connection string'i kontrol edin

### NuGet Paket Hataları

**Hata**: "Package restore failed"

**Çözüm**:
1. Visual Studio'yu yönetici olarak çalıştırın
2. `Tools > NuGet Package Manager > Package Manager Console`
3. Şu komutu çalıştırın:
   ```powershell
   Update-Package -reinstall
   ```

### Guna.UI2 Tasarımcı Hatası

**Hata**: "The designer cannot be loaded"

**Çözüm**:
1. Projeyi temizleyin: `Build > Clean Solution`
2. Projeyi yeniden derleyin: `Build > Rebuild Solution`
3. Visual Studio'yu yeniden başlatın

### Resim Yolu Hataları

**Hata**: "Image not found"

**Çözüm**:
1. `Images/Books/` klasörünün var olduğundan emin olun
2. Resim yollarının göreli olduğunu kontrol edin
3. `SQL/fix_image_paths.sql` script'ini çalıştırın

### E-posta Gönderim Hatası

**Hata**: "SMTP connection failed"

**Çözüm**:
1. SMTP ayarlarını kontrol edin
2. Firewall'un SMTP portunu engellemediğinden emin olun
3. SSL/TLS ayarlarını kontrol edin
4. Test mail göndererek doğrulayın

### SMS Gönderim Hatası

**Hata**: "SMS API error"

**Çözüm**:
1. VatanSMS API Key ve Secret'ı kontrol edin
2. VatanSMS hesabında bakiye olduğundan emin olun
3. Telefon numarası formatını kontrol edin (5XXXXXXXXX)
4. Gönderen başlığının kayıtlı olduğundan emin olun

---

## ✅ Kurulum Kontrol Listesi

- [ ] .NET Framework 4.7.2 yüklü
- [ ] SQL Server LocalDB yüklü ve çalışıyor
- [ ] Visual Studio 2019+ yüklü
- [ ] Proje başarıyla derlendi
- [ ] Veritabanı oluşturuldu
- [ ] İlk kullanıcı oluşturuldu
- [ ] SMTP ayarları yapılandırıldı (opsiyonel)
- [ ] SMS ayarları yapılandırıldı (opsiyonel)
- [ ] Stripe ayarları yapılandırıldı (opsiyonel)
- [ ] Google Drive yedekleme ayarları yapılandırıldı (opsiyonel)

---

## 📞 Destek

Kurulum sırasında sorun yaşarsanız:

1. Bu dokümantasyonu tekrar okuyun
2. Sorun giderme bölümüne bakın
3. GitHub'da issue açın
4. Geliştirici dokümantasyonunu inceleyin

---

**Not**: Production ortamında kurulum yapmadan önce mutlaka yedek alın!

