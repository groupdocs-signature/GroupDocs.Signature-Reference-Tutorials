---
"description": "Bu kapsamlı adım adım kılavuz ve kod örnekleriyle GroupDocs.Signature for .NET kullanarak belgelerde QR kodlarını nasıl etkili bir şekilde arayacağınızı öğrenin."
"linktitle": "QR Kodlarını Ara"
"second_title": "GroupDocs.Signature .NET API"
"title": "Belgelerde QR Kod İmzalarını Arayın"
"url": "/tr/net/signature-searching/search-for-qr-codes/"
"weight": 15
type: docs
---
## giriiş

Günümüzün dijital belge ekosisteminde QR kod imzaları, bilgi yerleştirme, kimlik doğrulama ve belge güvenliğini artırma konusunda paha biçilmez bir araç haline gelmiştir. GroupDocs.Signature for .NET, geliştiricilere çeşitli belge biçimlerinden QR kodlarını arama ve çıkarma konusunda güçlü bir API sunarak, .NET uygulamalarında gelişmiş belge analizi ve doğrulama yetenekleri sağlar.

Bu kapsamlı eğitim, GroupDocs.Signature for .NET kullanarak QR kod arama işlevselliğini uygulama sürecinde size rehberlik edecek, net açıklamalar, adım adım talimatlar ve kendi uygulamalarınıza entegre edebileceğiniz pratik kod örnekleri sağlayacaktır.

## Ön koşullar

QR kod imzası aramasına başlamadan önce aşağıdaki ön koşullara sahip olduğunuzdan emin olun:

1. GroupDocs.Signature for .NET SDK: SDK'yı şu adresten indirin ve yükleyin: [indirme sayfası](https://releases.groupdocs.com/signature/net/).

2. Geliştirme Ortamı: .NET Framework veya .NET Core yüklü Visual Studio gibi bir .NET geliştirme ortamı kurun.

3. Temel Bilgi: C# programlama ve .NET geliştirme kavramlarına aşinalık.

4. Örnek Belgeler: Doğrulama ve test için QR kodları içeren test belgeleri hazırlayın.

## Ad Alanlarını İçe Aktar

GroupDocs.Signature işlevine erişmek için gerekli ad alanlarını içe aktararak başlayın:

```csharp
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
using System;
using System.Collections.Generic;
```

Şimdi QR kodlarını arama sürecini anlaşılır ve takip etmesi kolay adımlara ayıralım:

## Adım 1: Belge Yolunu Tanımlayın

Öncelikle aramak istediğiniz QR kodlarını içeren belgenin yolunu belirtin:

```csharp
string filePath = "sample_multiple_signatures.docx";
```

## Adım 2: İmza Nesnesini Başlatın

Bir örneğini oluşturun `Signature` belge yolunu geçirerek sınıf:

```csharp
using (Signature signature = new Signature(filePath))
{
    // QR kod arama kodu buraya eklenecek
}
```

## Adım 3: QR Kod İmzalarını Arayın

Kullanın `Search` Belgedeki QR kodlarını bulmak için uygun imza türüne sahip yöntem:

```csharp
// Belge içinde QR kod imzalarını arayın
List<QrCodeSignature> signatures = signature.Search<QrCodeSignature>(SignatureType.QrCode);
```

## 4. Adım: Sonuçları İşleyin ve Görüntüleyin

Bulunan QR kod imzalarını inceleyin ve özelliklerine erişin:

```csharp
// Bulunan QR kodları hakkında bilgi görüntüle
Console.WriteLine($"\nSource document contains {signatures.Count} QR code signature(s):");

foreach (var qrCodeSignature in signatures)
{
    Console.WriteLine($"QR Code found at page {qrCodeSignature.PageNumber} with type {qrCodeSignature.EncodeType.TypeName}");
    Console.WriteLine($"Content: {qrCodeSignature.Text}");
    Console.WriteLine($"Location: X={qrCodeSignature.Left}, Y={qrCodeSignature.Top}, Width={qrCodeSignature.Width}, Height={qrCodeSignature.Height}");
    Console.WriteLine();
}
```

## Tam Örnek

İşte bir belgede QR kodlarını aramanın tüm sürecini gösteren kapsamlı bir çalışma örneği:

```csharp
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
using System;
using System.Collections.Generic;

namespace QrCodeSignatureSearch
{
    class Program
    {
        static void Main(string[] args)
        {
            // Belge yolu - dosya yolunuzla güncelleyin
            string filePath = "sample_multiple_signatures.docx";
            
            // İmza örneğini başlat
            using (Signature signature = new Signature(filePath))
            {
                try
                {
                    // Belgede QR kod imzalarını arayın
                    List<QrCodeSignature> signatures = signature.Search<QrCodeSignature>(SignatureType.QrCode);
                    
                    // Arama sonuçlarını görüntüle
                    Console.WriteLine($"\nSource document ['{filePath}'] contains {signatures.Count} QR code signature(s):");
                    
                    foreach (var qrCodeSignature in signatures)
                    {
                        Console.WriteLine($"QR Code found at page {qrCodeSignature.PageNumber} with type {qrCodeSignature.EncodeType.TypeName}");
                        Console.WriteLine($"Content: {qrCodeSignature.Text}");
                        Console.WriteLine($"Location: X={qrCodeSignature.Left}, Y={qrCodeSignature.Top}, Width={qrCodeSignature.Width}, Height={qrCodeSignature.Height}");
                        Console.WriteLine();
                    }
                }
                catch (Exception ex)
                {
                    Console.WriteLine($"Error occurred: {ex.Message}");
                }
            }
            
            Console.WriteLine("Press any key to exit...");
            Console.ReadKey();
        }
    }
}
```

## Gelişmiş QR Kod Arama Teknikleri

### Belirli Kriterlerle Arama

Daha hedefli aramalar için şunları kullanabilirsiniz: `QrCodeSearchOptions` arama kriterlerinizi özelleştirmek için:

```csharp
// Belirli kriterlerle QR kod arama seçenekleri oluşturun
QrCodeSearchOptions options = new QrCodeSearchOptions
{
    // Yalnızca belirli sayfalarda arama yapın
    AllPages = false,
    PageNumber = 1,
    PagesSetup = new PagesSetup { Pages = new List<int> { 1, 3, 5 } },
    
    // QR kod içeriğine göre filtrele
    Text = "Invoice",
    MatchType = TextMatchType.Contains,
    
    // Belirli QR kod türlerine göre filtreleyin
    EncodeType = QrCodeTypes.QR,
    
    // İçinde arama yapılacak belirli bir alanı tanımlayın
    Rectangle = new Rectangle(100, 100, 400, 400)
};

// Belirli seçeneklerle arama yapın
List<QrCodeSignature> filteredSignatures = signature.Search<QrCodeSignature>(options);
```

### QR Kod Verilerinin İşlenmesi

Uygulama gereksinimlerinize göre QR kod verileri için özel işleme uygulayabilirsiniz:

```csharp
foreach (var qrCode in signatures)
{
    // İçeriğe dayalı QR kod verilerini çıkarın ve işleyin
    string qrContent = qrCode.Text;
    
    if (qrContent.StartsWith("URL:"))
    {
        // İşlem URL verileri
        string url = qrContent.Substring(4);
        Console.WriteLine($"Found URL in QR code: {url}");
    }
    else if (qrContent.StartsWith("CONTACT:"))
    {
        // İşlem iletişim bilgileri
        string contact = qrContent.Substring(8);
        Console.WriteLine($"Found contact information in QR code: {contact}");
    }
    else if (qrContent.StartsWith("INVOICE:"))
    {
        // Fatura bilgilerini işle
        string invoiceData = qrContent.Substring(8);
        Console.WriteLine($"Found invoice information in QR code: {invoiceData}");
        
        // Fatura verilerini ayrıştırın ve doğrulayın
        if (ValidateInvoiceData(invoiceData))
        {
            Console.WriteLine("Invoice data is valid!");
        }
        else
        {
            Console.WriteLine("Warning: Invalid invoice data detected!");
        }
    }
}

// Örnek doğrulama yöntemi
static bool ValidateInvoiceData(string data)
{
    // Doğrulama mantığınızı uygulayın
    return !string.IsNullOrEmpty(data) && data.Contains("ID") && data.Contains("Amount");
}
```

### Güvenlik Doğrulamasının Uygulanması

QR kodları genellikle kimlik doğrulama amacıyla kullanılır. Temel güvenlik doğrulamasını şu şekilde uygulayabilirsiniz:

```csharp
// Belgenin geçerli bir kimlik doğrulama QR kodu içerip içermediğini kontrol edin
bool hasValidAuthQrCode = false;

foreach (var qrCode in signatures)
{
    if (qrCode.Text.StartsWith("AUTH:"))
    {
        string authCode = qrCode.Text.Substring(5);
        
        // Kimlik doğrulama kodunu doğrulayın (örneğin, bir veritabanına veya önceden tanımlanmış bir listeye göre)
        if (VerifyAuthCode(authCode))
        {
            hasValidAuthQrCode = true;
            Console.WriteLine("Document contains valid authentication QR code!");
            break;
        }
    }
}

if (!hasValidAuthQrCode)
{
    Console.WriteLine("Warning: Document does not contain a valid authentication QR code!");
}

// Örnek doğrulama yöntemi
static bool VerifyAuthCode(string code)
{
    // Doğrulama mantığınızı uygulayın
    // Bu, bir veritabanı araması, API çağrısı veya önceden tanımlanmış değerlere karşı bir karşılaştırma olabilir
    return code == "A7B82C3D" || code == "X9Y8Z7W6";
}
```

### QR Kod Görüntülerinin Çıkarılması

Daha ileri işleme veya görüntüleme için belgelerden QR kod görüntülerini çıkarabilirsiniz:

```csharp
// QR kod görüntülerini diske kaydedin
foreach (var qrCode in signatures)
{
    if (qrCode.Content != null)
    {
        // Sayfa numarasına ve konuma göre benzersiz bir dosya adı oluşturun
        string outputPath = $"QrCode_P{qrCode.PageNumber}_X{qrCode.Left}_Y{qrCode.Top}.png";
        
        // Görüntü verilerini kaydedin
        File.WriteAllBytes(outputPath, qrCode.Content);
        Console.WriteLine($"Saved QR code image to {outputPath}");
    }
}
```

## Çözüm

Bu kapsamlı kılavuzda, .NET için GroupDocs.Signature kullanarak belgelerde QR kodu imzalarını nasıl arayacağınızı inceledik. Temel aramadan gelişmiş tekniklere kadar, artık .NET uygulamalarınızda güçlü QR kodu işleme yöntemlerini uygulamak için gereken bilgiye sahipsiniz. GroupDocs.Signature API, farklı belge formatlarında QR kodları da dahil olmak üzere çeşitli imza türleriyle çalışmak için güçlü ve esnek bir çerçeve sunar.

Bu yetenekleri kullanarak belge doğrulama süreçlerini geliştirebilir, kimlik doğrulama sistemleri uygulayabilir ve QR kodlarına gömülü değerli bilgileri .NET uygulamalarınızda çıkarabilirsiniz.

## SSS

### GroupDocs.Signature hangi QR kod formatlarını destekliyor?

GroupDocs.Signature, standart QR Kodu, Mikro QR Kodu ve diğer yaygın QR kodu standartları dahil olmak üzere çeşitli QR kodu formatlarını destekler. Belirli formata şu adresten erişilebilir: `EncodeType` mülkiyeti `QrCodeSignature` nesne.

### Şifreyle korunan belgelerde QR kodlarını arayabilir miyim?

Evet, GroupDocs.Signature, başlatılırken parolayı sağlayarak parola korumalı belgelerde QR kodlarını aramayı destekler. `Signature` nesne:

```csharp
LoadOptions loadOptions = new LoadOptions { Password = "your_password" };
using (Signature signature = new Signature(filePath, loadOptions))
{
    // QR kodlarını arayın
}
```

### QR kodlarını içeriklerine göre nasıl filtreleyebilirim?

QR kodlarını içeriklerine göre filtreleyebilirsiniz. `Text` Ve `MatchType` özellikleri `QrCodeSearchOptions`:

```csharp
QrCodeSearchOptions options = new QrCodeSearchOptions
{
    Text = "Invoice",
    MatchType = TextMatchType.Contains // Diğer seçenekler: Tam, Başlangıç, Bitiş
};
```

### GroupDocs.Signature hasarlı veya kısmen görünen QR kodlarını tespit edebilir mi?

GroupDocs.Signature, kısmen görünür QR kodlarını algılama yeteneğine sahiptir, ancak ağır hasarlı QR kodları tanınmayabilir. Algılama doğruluğu, belgedeki QR kodunun kalitesine ve görünürlüğüne bağlıdır.

### QR kod araması için hangi belge biçimleri destekleniyor?

GroupDocs.Signature, PDF, Microsoft Office belgeleri (Word, Excel, PowerPoint), resimler (JPEG, PNG, TIFF) ve daha birçok belge biçimini içeren QR kod aramasını destekler.

## Ayrıca bakınız

* [API Referansı](https://reference.groupdocs.com/signature/net/)
* [GitHub'daki Kod Örnekleri](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
* [Ürün Dokümantasyonu](https://docs.groupdocs.com/signature/net/)
* [Ürün Sayfası](https://products.groupdocs.com/signature/net/)
* [En Son Sürümü İndirin](https://releases.groupdocs.com/signature/net/)
* [Blog Yazıları](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
* [Ücretsiz Destek Forumu](https://forum.groupdocs.com/c/signature/13)
* [Geçici Lisans](https://purchase.groupdocs.com/temporary-license/)