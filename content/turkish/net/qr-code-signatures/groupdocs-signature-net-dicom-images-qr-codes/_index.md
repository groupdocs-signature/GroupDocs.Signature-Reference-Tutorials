---
"date": "2025-05-07"
"description": "GroupDocs.Signature for .NET kullanarak DICOM görüntülerini QR kodlarıyla nasıl imzalayacağınızı öğrenin. Bu kılavuz, tıbbi görüntülemede QR kod imzalarının kurulumunu, uygulanmasını ve doğrulanmasını ele almaktadır."
"title": "GroupDocs.Signature for .NET Kullanarak DICOM Görüntülerini QR Kodlarıyla Nasıl İmzalayabilirsiniz? Kapsamlı Bir Kılavuz"
"url": "/tr/net/qr-code-signatures/groupdocs-signature-net-dicom-images-qr-codes/"
"weight": 1
type: docs
---
# .NET için GroupDocs.Signature Kullanarak DICOM Görüntülerini QR Kodlarıyla Nasıl İmzalayabilirsiniz: Kapsamlı Bir Kılavuz

DICOM dosyalarınızı doğrulamak için güvenli bir yöntem mi arıyorsunuz? Bu ayrıntılı kılavuz, DICOM görüntülerine QR kod imzalarını entegre etmek için GroupDocs.Signature for .NET'i nasıl kullanacağınızı gösterecektir. Sağlık profesyonelleri, geliştiriciler ve dijital tıbbi belgelerle çalışan herkes için ideal olan bu eğitim, kurulumdan uygulamaya kadar her şeyi kapsar.

## Öğrenecekleriniz:
- GroupDocs.Signature for .NET ile geliştirme ortamınızı kurma.
- QR kodları kullanılarak DICOM görüntülerinin imzalanmasına ilişkin adım adım talimatlar.
- DICOM dosyalarında QR kod imzalarını doğrulama ve arama yöntemleri.
- İmzalanmış belgelerin inceleme amaçlı önizlemelerini oluşturma teknikleri.
- Performansı optimize etmek ve kaynakları etkili bir şekilde yönetmek için en iyi uygulamalar.

Ön koşullarla başlayalım!

## Ön koşullar

GroupDocs.Signature for .NET'i kullanmak için ortamınızın hazır olduğundan emin olun. İhtiyacınız olanlar şunlardır:

### Gerekli Kitaplıklar ve Sürümler
- **.NET için GroupDocs.Signature**.NET framework'ünüzle uyumluluğu sağlayın.

### Ortam Kurulum Gereksinimleri
- Windows veya Linux üzerinde bir geliştirme ortamı.
- Visual Studio veya başka bir .NET uyumlu IDE yüklü.

### Bilgi Ön Koşulları
- C# programlamanın temel bilgisi.
- .NET uygulamalarında dosya G/Ç'ye aşinalık.

## .NET için GroupDocs.Signature Kurulumu

GroupDocs.Signature kütüphanesini tercih ettiğiniz yöntemi kullanarak yükleyin:

**.NET CLI'yi kullanarak:**
```bash
dotnet add package GroupDocs.Signature
```

**Paket Yöneticisi:**
```powershell
Install-Package GroupDocs.Signature
```

**NuGet Paket Yöneticisi Kullanıcı Arayüzü:**
- "GroupDocs.Signature" ifadesini arayın ve en son sürümü yükleyin.

### Lisans Edinimi

Yetenekleri keşfetmek için ücretsiz deneme sürümüyle başlayın. Uzun süreli kullanım için, geçici veya tam lisans satın almayı düşünün. [GrupDokümanları](https://purchase.groupdocs.com/buy).

Kurulum tamamlandıktan sonra kütüphaneyi başlatın:

```csharp
using GroupDocs.Signature;
// İmza nesnesini DICOM dosya yolunuzla başlatın.
Signature signature = new Signature("YOUR_DOCUMENT_DIRECTORY\\sample.dicom");
```

## Uygulama Kılavuzu

### DICOM Görüntüsünü QR Koduyla İmzalayın

#### Genel Bakış
Tıbbi belgelerin gerçekliğini ve izlenebilirliğini sağlamak için QR kod imzaları ekleyin.

**Adım 1: İmza Nesnesini Başlatın**

```csharp
string filePath = "YOUR_DOCUMENT_DIRECTORY\\sample.dicom";
using (Signature signature = new Signature(filePath))
{
    // İmzalama işlemlerine devam edin...
}
```

**Adım 2: QR Kod İmza Seçenekleri Oluşturun**

Metin, boyut ve hizalama gibi özellikleri yapılandırın.

```csharp
QrCodeSignOptions options = new QrCodeSignOptions("Patient #36363393. R: No-Issues")
{
    AllPages = true,
    Width = 100,
    Height = 100,
    VerticalAlignment = VerticalAlignment.Bottom,
    HorizontalAlignment = HorizontalAlignment.Right,
    Margin = new Padding() { Right = 5, Left = 5 }
};
```

**Adım 3: XMP Meta Verilerini Ekleyin**

Belgeyi ek meta verilerle geliştirin.

```csharp
DicomSaveOptions dicomSaveOptions = new DicomSaveOptions()
{
    XmpEntries = new List<DicomXmpEntry>() { new DicomXmpEntry(DicomXmpType.PatientName, "Patient #4") }
};
```

**Adım 4: Belgeyi İmzalayın**

İmzalamayı gerçekleştirin ve kaydedin.

```csharp
SignResult signResult = signature.Sign("YOUR_OUTPUT_DIRECTORY\\SignedDicom", options, dicomSaveOptions);
```

### Belge Bilgilerini Al

Veri bütünlüğünü sağlamak için imzalı DICOM dosyalarından meta verileri alın.

**Genel bakış:**
Doğrulama için belge bilgilerine ve XMP meta veri imzalarına erişin.

**Adım 1: Belge Bilgilerini Alın**

```csharp
using (Signature signature = new Signature("YOUR_DOCUMENT_DIRECTORY\\sample_signed.dicom"))
{
    IDocumentInfo signedDocumentInfo = signature.GetDocumentInfo();
}
```

**Adım 2: XMP Verilerini Yineleyin ve Yazdırın**

Meta veri ayrıntılarını görüntüle.

```csharp
foreach (var item in signedDocumentInfo.MetadataSignatures)
{
    Console.WriteLine(item.ToString());
}
```

### DICOM İmzalarını Doğrulayın

DICOM görüntülerindeki QR kod imzalarının gerçekliğini doğrulayın.

**Genel bakış:**
İmzaların doğru ve gerçek olduğundan emin olun.

**Adım 1: QR Kod Doğrulama Seçeneklerini Oluşturun**

QR kodlarındaki belirli metinle eşleşen seçenekleri ayarlayın.

```csharp
QrCodeVerifyOptions options = new QrCodeVerifyOptions()
{
    AllPages = true,
    Text = "Patient #36363393",
    MatchType = TextMatchType.Contains
};
```

**Adım 2: İmzaları Doğrulayın**

İmzaların kriterlere uygun olup olmadığını kontrol edin.

```csharp
VerificationResult result = signature.Verify(options);

if (result.IsValid)
{
    Console.WriteLine($"DICOM {filePath} has {result.Succeeded.Count} successfully verified signatures!");
}
```

### DICOM'da İmzaları Ara

İmzalanmış DICOM görüntülerinde QR kod imzalarını bulun.

**Genel bakış:**
Belgelerin gerçekliğini yönetmek için tüm QR kod imzalarını etkin bir şekilde bulun.

**Adım 1: QR Kod İmzalarını Arayın**

```csharp
List<QrCodeSignature> signatures = signature.Search<QrCodeSignature>(SignatureType.QrCode);
```

**Adım 2: İmza Ayrıntılarını Yineleyin ve Yazdırın**

Bulunan her imzanın ayrıntılarını inceleyin.

```csharp
foreach (var QrCodeSignature in signatures)
{
    Console.WriteLine($"QRCode signature found at page {QrCodeSignature.PageNumber} with type {QrCodeSignature.EncodeType.TypeName} and text {QrCodeSignature.Text}");
}
```

### İmzalanmış DICOM'un Önizlemesini Oluştur

Doğrulama için görsel önizlemeler oluşturun.

**Genel bakış:**
Özel bir yazılıma ihtiyaç duymadan içeriği doğrulamak için görüntü önizlemeleri oluşturun.

**Adım 1: Akış Yöntemlerini Tanımlayın**

Önizleme oluşturma sırasında dosya akışı yönetimi için yöntemler ayarlayın.

```csharp
Stream CreatePageStream(PreviewPageData pageData)
{
    string imageFilePath = Path.Combine("YOUR_OUTPUT_DIRECTORY", "SignDicomImageAdvanced", $"preview-{pageData.PageNumber}.jpg");
    var folder = Path.GetDirectoryName(imageFilePath);
    if (!Directory.Exists(folder))
    {
        Directory.CreateDirectory(folder);
    }
    return new FileStream(imageFilePath, FileMode.Create);
}

void ReleasePageStream(PreviewPageData pageData, Stream pageStream)
{
    pageStream.Dispose();
}
```

**Adım 2: Önizlemeler Oluşturun**

Önizleme oluşturma sürecini yürütün.

```csharp
using (Signature signature = new Signature("YOUR_DOCUMENT_DIRECTORY\\sample_signed.dicom"))
{
    PreviewOptions previewOption = new PreviewOptions(CreatePageStream, ReleasePageStream)
    {
        PreviewFormat = PreviewOptions.PreviewFormats.PNG,
    };

    signature.GeneratePreview(previewOption);
}
```

## Pratik Uygulamalar

1. **Tıbbi Kayıt Yönetimi**: Uyumluluk için QR kod imzalarını kullanarak hasta kayıtlarını doğrulayın.
2. **Sağlık Sistemlerinde Denetim İzleri**: Belge değişikliklerini takip edin ve QR kodlarıyla gerçekliğini doğrulayın.
3. **Güvenli Veri Paylaşımı**:Dijital imzalar yerleştirerek tıbbi görüntülerin güvenli bir şekilde paylaşılmasını sağlayın.
4. **Uyumluluk Doğrulaması**: Yasal gereklilikleri karşılamak için DICOM dosya bütünlüğünü düzenli olarak doğrulayın.
5. **EHR Sistemleriyle Entegrasyon**: İmzalı DICOM dosyalarını sorunsuz bir şekilde Elektronik Sağlık Kayıtları (EHR) sistemlerine entegre ederek işlemleri kolaylaştırın.