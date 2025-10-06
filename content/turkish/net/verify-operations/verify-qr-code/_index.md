---
"description": "GroupDocs.Signature for .NET kullanarak belgelerdeki QR kodlarını nasıl doğrulayacağınızı öğrenin. Belge kimlik doğrulaması için kod örnekleri ve en iyi uygulamaları içeren kapsamlı kılavuz."
"linktitle": "QR Kodunu Doğrula"
"second_title": "GroupDocs.Signature .NET API"
"title": "Belgelerdeki QR Kodunu Doğrulayın"
"url": "/tr/net/verify-operations/verify-qr-code/"
"weight": 12
type: docs
---
## giriiş

Belge güvenliği, modern iş operasyonlarının kritik bir unsurudur. QR kodları, belgelerin içine gerçekliğini doğrulayabilen bilgileri yerleştirmek için giderek daha popüler bir yöntem haline gelmiştir. GroupDocs.Signature for .NET, çeşitli formatlardaki belgelere yerleştirilmiş QR kodlarını doğrulamak için güçlü ve esnek bir çözüm sunar.

Bu kapsamlı eğitim, .NET uygulamalarınızda QR kod doğrulamasını uygulama sürecinde size rehberlik edecek ve belgelerinizin bütünlüğünü ve orijinalliğini korumasını sağlayacaktır.

## Ön koşullar

QR kod doğrulama işlevini uygulamadan önce aşağıdaki ön koşullara sahip olduğunuzdan emin olun:

1. GroupDocs.Signature for .NET: Kitaplığı şu adresten indirin ve yükleyin: [indirme sayfası](https://releases.groupdocs.com/signature/net/).
2. Geliştirme Ortamı: Visual Studio veya uyumlu herhangi bir .NET geliştirme ortamı.
3. Test Belgesi: Doğrulama amaçlı QR kod imzalarını içeren belge.
4. Temel Bilgi: C# programlama ve .NET framework kavramlarına aşinalık.

## Ad Alanlarını İçe Aktar

GroupDocs.Signature işlevine erişmek için gerekli ad alanlarını içe aktararak başlayın:

```csharp
using System;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

## Adım Adım QR Kod Doğrulama Süreci

Belgelerinizdeki QR kodlarını doğrulamak için şu detaylı adımları izleyin:

### Adım 1: Belge Yolunu Belirleyin

```csharp
// QR kod imzalarını içeren belgenin yolunu sağlayın
string filePath = "sample_multiple_signatures.docx";
```

Örnek yolu, belgenizin gerçek yoluyla değiştirdiğinizden emin olun.

### Adım 2: İmza Nesnesini Başlatın

```csharp
// Belge yolunu ileterek bir İmza örneği oluşturun
using (Signature signature = new Signature(filePath))
{
    // Doğrulama kodu burada uygulanacaktır
}
```

Signature sınıfı, GroupDocs.Signature API'sindeki tüm işlemler için ana giriş noktasıdır.

### Adım 3: QR Kod Doğrulama Seçeneklerini Yapılandırın

```csharp
// QR kod doğrulama seçeneklerini tanımlayın
QrCodeVerifyOptions options = new QrCodeVerifyOptions()
{
    AllPages = true, // Belgenin tüm sayfalarını kontrol edin
    Text = "John",   // QR kodunda doğrulanacak metin
    MatchType = TextMatchType.Contains // Metin eşleştirme kriterlerini belirtin
};
```

Doğrulama seçenekleri, doğrulama süreci için belirli kriterleri tanımlamanıza olanak tanır:
- `AllPages`: Tüm belge sayfalarını kontrol etmek için doğru olarak ayarlayın (varsayılan davranış)
- `Text`: QR kodunda eşleşecek metin içeriği
- `MatchType`: Metin eşleştirme yöntemi (İçerir, Tam, Başlar, vb.)

### Adım 4: Doğrulama İşlemini Gerçekleştirin

```csharp
// Doğrulamayı gerçekleştirin
VerificationResult result = signature.Verify(options);
```

Bu, belirttiğiniz seçeneklere göre doğrulama işlemini gerçekleştirir.

### Adım 5: İşlem Doğrulama Sonuçları

```csharp
// Doğrulama sonucunu kontrol edin ve buna göre işlem yapın
if (result.IsValid)
{
    Console.WriteLine($"Document {filePath} contains valid QR code signature!");
    
    // Başarılı imzalar hakkında bilgi görüntüle
    foreach (QrCodeSignature signature in result.Succeeded)
    {
        Console.WriteLine($"Found valid QR Code signature with text: {signature.Text}");
        Console.WriteLine($"QR Code type: {signature.EncodeType.TypeName}");
        Console.WriteLine($"Location: Page {signature.PageNumber}, {signature.Left}x{signature.Top}");
    }
}
else
{
    Console.WriteLine($"Document {filePath} failed verification process.");
    Console.WriteLine($"Number of failed signatures: {result.Failed.Count}");
}
```

Doğrulama sonucunun doğru bir şekilde işlenmesi, uygulamanızın doğrulama sonucuna göre uygun eylemleri gerçekleştirmesini sağlar.

## Tam Örnek

İşte QR kod doğrulamasını gösteren eksiksiz, çalışan bir örnek:

```csharp
using System;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;

namespace GroupDocs.Signature.Examples
{
    class Program
    {
        static void Main(string[] args)
        {
            // Belge yolu
            string filePath = "sample_multiple_signatures.docx";
            
            // İmza örneğini başlat
            using (Signature signature = new Signature(filePath))
            {
                // Kurulum doğrulama seçenekleri
                QrCodeVerifyOptions options = new QrCodeVerifyOptions()
                {
                    AllPages = true,
                    Text = "John",
                    MatchType = TextMatchType.Contains
                };
                
                // Belge imzalarını doğrulayın
                VerificationResult result = signature.Verify(options);
                
                // İşlem doğrulama sonuçları
                if (result.IsValid)
                {
                    Console.WriteLine($"Document {filePath} contains valid QR code signature!");
                    
                    foreach (QrCodeSignature qrSignature in result.Succeeded)
                    {
                        Console.WriteLine($"Found valid QR Code with text: {qrSignature.Text}");
                    }
                }
                else
                {
                    Console.WriteLine($"Document {filePath} failed verification process.");
                }
            }
        }
    }
}
```

## Gelişmiş Doğrulama Seçenekleri

GroupDocs.Signature, daha karmaşık doğrulama senaryoları için ek seçenekler sunar:

### Belirli QR Kod Türlerini Doğrulama

```csharp
QrCodeVerifyOptions options = new QrCodeVerifyOptions()
{
    EncodeType = QrCodeTypes.QR,  // Yalnızca standart QR kodlarını doğrulayın
    Text = "Confidential",
    MatchType = TextMatchType.Exact
};
```

### Belirli Sayfalarda Doğrulama

```csharp
QrCodeVerifyOptions options = new QrCodeVerifyOptions()
{
    AllPages = false,
    PageNumber = 2,  // Yalnızca 2. sayfada doğrulayın
    Text = "Approved"
};
```

### Doğrulama İçin Düzenli İfadelerin Kullanımı

```csharp
QrCodeVerifyOptions options = new QrCodeVerifyOptions()
{
    Text = "INV-\\d{6}",  // Fatura numaralarını eşleştirin (örneğin, INV-123456)
    MatchType = TextMatchType.Regex
};
```

## QR Kod Doğrulaması için En İyi Uygulamalar

1. Girişleri her zaman doğrulayın: İşleme başlamadan önce belge yollarının ve doğrulama kriterlerinin geçerli olduğundan emin olun.
2. Hata işlemeyi uygulayın: Doğrulama sırasında olası istisnaları işlemek için try-catch bloklarını kullanın.
3. Performansı göz önünde bulundurun: Büyük belgeler için tüm belgeyi doğrulamak yerine belirli sayfaları doğrulamayı düşünün.
4. Doğrulama sonuçlarını kaydedin: Denetim amacıyla doğrulama süreçlerinin kayıtlarını tutun.
5. Çeşitli belge formatlarıyla test edin: Doğrulamanızın tüm gerekli belge formatlarında çalıştığından emin olun.

## Çözüm

Belgelerdeki QR kodlarını doğrulamak, belgenin gerçekliğini ve bütünlüğünü sağlamanın önemli bir parçasıdır. GroupDocs.Signature for .NET, .NET uygulamalarınızda QR kod doğrulamasını uygulamak için kapsamlı ve kullanıcı dostu bir API sağlar.

Bu eğitimi takip ederek şunları öğrendiniz:
- Doğrulama sürecini yapılandırın ve başlatın
- Çeşitli doğrulama kriterlerini belirtin
- Doğrulama sonuçlarını işleyin ve yorumlayın
- Gelişmiş doğrulama seçeneklerini uygulayın

Bu bilgi, belge yönetim sistemlerinizin güvenliğini ve güvenilirliğini artırmanıza olanak tanır.

## SSS

### GroupDocs.Signature tek bir belgedeki birden fazla QR kodunu doğrulayabilir mi?
Evet, GroupDocs.Signature tek bir belgedeki birden fazla QR kodunu doğrulayabilir. Doğrulama sonuçları, eşleşen tüm QR kodlarını içerecektir.

### QR kod doğrulaması için hangi belge formatları destekleniyor?
GroupDocs.Signature, PDF, Word (DOC, DOCX), Excel (XLS, XLSX), PowerPoint (PPT, PPTX), resimler ve daha fazlası dahil olmak üzere çok çeşitli belge biçimlerini destekler.

### Belirli bir şifreleme veya biçimlendirme ile QR kodlarını doğrulayabilir miyim?
Evet, GroupDocs.Signature, QR kodlarını belirli kodlama türleri ve içerik biçimlendirme desenleriyle doğrulamak için seçenekler sunar.

### Üçüncü parti uygulamalar tarafından oluşturulan QR kodlarının doğrulanması mümkün müdür?
Evet, GroupDocs.Signature, standart QR kod formatlarını takip ettikleri sürece çoğu uygulama tarafından oluşturulan standart QR kodlarını doğrulayabilir.

### Metin yerine ikili veri içeren QR kodlarını nasıl işlerim?
GroupDocs.Signature, ikili verilerle QR kodlarını doğrulamak için seçenekler sunar `BinaryData` Doğrulama seçeneklerinin özelliği.

### İlgili Kaynaklar
* [GroupDocs.Signature API Referansı](https://reference.groupdocs.com/signature/net/)
* [GroupDocs.Signature İndirmeleri](https://releases.groupdocs.com/signature/net/)
* [GitHub'daki Kod Örnekleri](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
* [Belgeleme](https://docs.groupdocs.com/signature/net/)
* [Ürün Sayfası](https://products.groupdocs.com/signature/net/)
* [Blog Yazıları](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
* [Destek Forumu](https://forum.groupdocs.com/c/signature/13)
* [Geçici Lisans](https://purchase.groupdocs.com/temporary-license/)