---
"description": "GroupDocs.Signature for .NET kullanarak belgelerde birden fazla imza türünü nasıl arayacağınızı öğrenin. Gelişmiş belge güvenliği için kod örnekleri içeren kapsamlı kılavuz."
"linktitle": "Çoklu İmzaları Ara"
"second_title": "GroupDocs.Signature .NET API"
"title": "Belgelerde Çoklu İmza Türlerini Arama"
"url": "/tr/net/signature-searching/search-for-multiple-signatures/"
"weight": 14
type: docs
---
## giriiş

Modern belge yönetim sistemlerinde, tek bir belge içinde birden fazla imza türünü arama ve doğrulama yeteneği giderek daha önemli hale geliyor. Kuruluşlar, belge güvenliğini artırmak ve doğrulama süreçlerini kolaylaştırmak için genellikle dijital imzalar, metin imzaları, barkodlar, QR kodları ve daha fazlası gibi çeşitli imza türleri kullanır. GroupDocs.Signature for .NET, geliştiricilerin çeşitli belge formatlarında kapsamlı imza arama işlevselliği uygulamasına olanak tanıyan güçlü bir çerçeve sunar.

Bu eğitim, .NET için GroupDocs.Signature kullanarak belgeler içinde birden fazla imza türünü arama sürecinde size rehberlik edecek, ayrıntılı açıklamalar ve pratik kod örnekleri sunacaktır.

## Ön koşullar

Çoklu imza arama işlevselliğini uygulamaya başlamadan önce aşağıdaki ön koşullara sahip olduğunuzdan emin olun:

1. Geliştirme Ortamı: Sisteminizde yüklü Visual Studio veya tercih ettiğiniz herhangi bir .NET geliştirme ortamı.
  
2. GroupDocs.Signature for .NET: GroupDocs.Signature for .NET kitaplığını şu adresten indirin ve yükleyin: [Burada](https://releases.groupdocs.com/signature/net/).

3. Temel C# Bilgisi: C# programlama dili ve .NET framework kavramlarına aşinalık.

4. Örnek Belgeler: Test amaçlı çeşitli imza türlerini içeren test belgeleri hazırlayın.

## Ad Alanlarını İçe Aktar

GroupDocs.Signature işlevine erişmek için gerekli ad alanlarını içe aktararak başlayın:

```csharp
using System;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

Şimdi, birden fazla imza türünü arama sürecini anlaşılır ve yönetilebilir adımlara bölelim:

## Adım 1: Belgeyi Yükleyin

Öncelikle aramak istediğiniz imzaları içeren belgeyi yükleyin:

```csharp
string filePath = "sample_multiple_signatures.docx";
using (Signature signature = new Signature(filePath))
{
    // Çoklu imzalı arama kodu buraya eklenecek
}
```

## Adım 2: Farklı İmza Türleri için Arama Seçeneklerini Tanımlayın

Aramak istediğiniz her imza türü için arama seçenekleri oluşturun:

```csharp
// Metin imzaları için arama seçeneklerini tanımlayın
TextSearchOptions textOptions = new TextSearchOptions
{
    AllPages = true,  // Tüm sayfalarda ara
    Text = "Signature",  // İsteğe bağlı: Bulunacak metin
    MatchType = TextMatchType.Contains  // Eşleşen kriterler
};

// Dijital imzalar için arama seçeneklerini tanımlayın
DigitalSearchOptions digitalOptions = new DigitalSearchOptions
{
    AllPages = true
};

// Barkod imzaları için arama seçeneklerini tanımlayın
BarcodeSearchOptions barcodeOptions = new BarcodeSearchOptions
{
    AllPages = true,
    Text = "123456",  // İsteğe bağlı: eşleşen barkod metni
    MatchType = TextMatchType.Exact  // Eşleşen kriterler
};

// QR kod imzaları için arama seçeneklerini tanımlayın
QrCodeSearchOptions qrCodeOptions = new QrCodeSearchOptions
{
    AllPages = true,
    Text = "John",  // İsteğe bağlı: Eşleşecek QR kod metni
    MatchType = TextMatchType.Contains  // Eşleşen kriterler
};

// Meta veri imzaları için arama seçeneklerini tanımlayın
MetadataSearchOptions metadataOptions = new MetadataSearchOptions();
```

## Adım 3: Bir Koleksiyona Seçenekler Ekleyin

Tüm arama seçeneklerini bir koleksiyona ekleyin:

```csharp
// Tüm arama seçeneklerini tutacak bir liste oluşturun
List<SearchOptions> searchOptions = new List<SearchOptions>
{
    textOptions,
    digitalOptions,
    barcodeOptions,
    qrCodeOptions,
    metadataOptions
};
```

## Adım 4: Aramayı Gerçekleştirin ve Sonuçları İşleyin

Birleştirilmiş arama seçeneklerini kullanarak aramayı gerçekleştirin ve sonuçları işleyin:

```csharp
// Tanımlanan seçenekleri kullanarak tüm imza türlerini arayın
SearchResult result = signature.Search(searchOptions);

// İmzaların bulunup bulunmadığını kontrol edin
if (result.Signatures.Count > 0)
{
    Console.WriteLine($"\nSource document ['{filePath}'] contains {result.Signatures.Count} signature(s):");
    
    // Bulunan imzaları yineleyin
    foreach (var foundSignature in result.Signatures)
    {
        Console.WriteLine($"Signature found: Type: {foundSignature.SignatureType}, Page: {foundSignature.PageNumber}, ID: {foundSignature.SignatureId}");
        
        // İşleme özgü imza türleri
        if (foundSignature is TextSignature textSignature)
        {
            Console.WriteLine($"Text: '{textSignature.Text}'");
        }
        else if (foundSignature is BarcodeSignature barcodeSignature)
        {
            Console.WriteLine($"Barcode Type: {barcodeSignature.EncodeType.TypeName}, Text: '{barcodeSignature.Text}'");
        }
        else if (foundSignature is QrCodeSignature qrCodeSignature)
        {
            Console.WriteLine($"QR Code Type: {qrCodeSignature.EncodeType.TypeName}, Text: '{qrCodeSignature.Text}'");
        }
        else if (foundSignature is DigitalSignature digitalSignature)
        {
            Console.WriteLine($"Certificate: {digitalSignature.Certificate?.SubjectName}, Valid: {digitalSignature.IsValid}");
        }
        else if (foundSignature is MetadataSignature metadataSignature)
        {
            Console.WriteLine($"Metadata: Name: {metadataSignature.Name}, Value: {metadataSignature.Value}");
        }
    }
}
else
{
    Console.WriteLine("No signatures were found in the document.");
}
```

## Tam Örnek

İşte bir belgede birden fazla imza türünü aramayı gösteren eksiksiz, çalışan bir örnek:

```csharp
using System;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;

namespace MultiSignatureSearch
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
                try
                {
                    // Metin imzaları için arama seçeneklerini tanımlayın
                    TextSearchOptions textOptions = new TextSearchOptions
                    {
                        AllPages = true,
                        MatchType = TextMatchType.Contains
                    };

                    // Dijital imzalar için arama seçeneklerini tanımlayın
                    DigitalSearchOptions digitalOptions = new DigitalSearchOptions
                    {
                        AllPages = true
                    };

                    // Barkod imzaları için arama seçeneklerini tanımlayın
                    BarcodeSearchOptions barcodeOptions = new BarcodeSearchOptions
                    {
                        AllPages = true
                    };

                    // QR kod imzaları için arama seçeneklerini tanımlayın
                    QrCodeSearchOptions qrCodeOptions = new QrCodeSearchOptions
                    {
                        AllPages = true
                    };

                    // Meta veri imzaları için arama seçeneklerini tanımlayın
                    MetadataSearchOptions metadataOptions = new MetadataSearchOptions();

                    // Tüm arama seçeneklerini tutacak bir liste oluşturun
                    List<SearchOptions> searchOptions = new List<SearchOptions>
                    {
                        textOptions,
                        digitalOptions,
                        barcodeOptions,
                        qrCodeOptions,
                        metadataOptions
                    };

                    // Tüm imza türlerini arayın
                    SearchResult result = signature.Search(searchOptions);

                    // İmzaların bulunup bulunmadığını kontrol edin
                    if (result.Signatures.Count > 0)
                    {
                        Console.WriteLine($"\nSource document ['{filePath}'] contains {result.Signatures.Count} signature(s):");
                        
                        // İmza türüne göre işlem sonuçları
                        foreach (var foundSignature in result.Signatures)
                        {
                            Console.WriteLine($"Signature found: Type: {foundSignature.SignatureType}, Page: {foundSignature.PageNumber}");
                            
                            // İşleme özgü imza türleri
                            switch (foundSignature.SignatureType)
                            {
                                case SignatureType.Text:
                                    var textSignature = foundSignature as TextSignature;
                                    Console.WriteLine($"Text: '{textSignature.Text}'");
                                    break;
                                    
                                case SignatureType.Barcode:
                                    var barcodeSignature = foundSignature as BarcodeSignature;
                                    Console.WriteLine($"Barcode Type: {barcodeSignature.EncodeType.TypeName}, Text: '{barcodeSignature.Text}'");
                                    break;
                                    
                                case SignatureType.QrCode:
                                    var qrCodeSignature = foundSignature as QrCodeSignature;
                                    Console.WriteLine($"QR Code Type: {qrCodeSignature.EncodeType.TypeName}, Text: '{qrCodeSignature.Text}'");
                                    break;
                                    
                                case SignatureType.Digital:
                                    var digitalSignature = foundSignature as DigitalSignature;
                                    Console.WriteLine($"Certificate: {digitalSignature.Certificate?.SubjectName}, Valid: {digitalSignature.IsValid}");
                                    break;
                                    
                                case SignatureType.Metadata:
                                    var metadataSignature = foundSignature as MetadataSignature;
                                    Console.WriteLine($"Metadata: Name: {metadataSignature.Name}, Value: {metadataSignature.Value}");
                                    break;
                            }
                            
                            Console.WriteLine(); // İmzalar arasına satır sonu ekle
                        }
                    }
                    else
                    {
                        Console.WriteLine("No signatures were found in the document.");
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

## Gelişmiş Çoklu İmza Arama Teknikleri

### Arama Sonuçlarını Filtreleme

Arama sonuçlarını daraltmak için gelişmiş filtrelemeyi uygulayabilirsiniz:

```csharp
// Sonuçları sayfa numarasına göre filtrele
var signaturesOnFirstPage = result.Signatures.FindAll(s => s.PageNumber == 1);

// Sonuçları imza türüne göre filtrele
var digitalSignatures = result.Signatures.FindAll(s => s.SignatureType == SignatureType.Digital);
var qrCodeSignatures = result.Signatures.FindAll(s => s.SignatureType == SignatureType.QrCode);

// Belirli içerik barındıran metin imzalarını filtrele
var approvalSignatures = result.Signatures
    .FindAll(s => s is TextSignature && ((TextSignature)s).Text.Contains("Approved"));
```

### Birden Fazla İmzanın Doğrulanması

Farklı imza türleri için doğrulama mantığını uygulayın:

```csharp
bool ValidateAllSignatures(SearchResult result)
{
    bool isDocumentValid = true;
    
    // Belgenin geçerli bir dijital imzaya sahip olup olmadığını kontrol edin
    bool hasValidDigitalSignature = result.Signatures
        .Any(s => s is DigitalSignature && ((DigitalSignature)s).IsValid);
    
    if (!hasValidDigitalSignature)
    {
        Console.WriteLine("Warning: Document does not contain a valid digital signature");
        isDocumentValid = false;
    }
    
    // Belgenin gerekli QR koduna sahip olup olmadığını kontrol edin
    bool hasRequiredQRCode = result.Signatures
        .Any(s => s is QrCodeSignature && ((QrCodeSignature)s).Text.Contains("Auth-Code"));
    
    if (!hasRequiredQRCode)
    {
        Console.WriteLine("Warning: Document does not contain the required authentication QR code");
        isDocumentValid = false;
    }
    
    return isDocumentValid;
}
```

### Özel İşleme ile Arama

Arama işlemleri için özel işlem mantığını tanımlayabilirsiniz:

```csharp
// Özel işlemeyle arama seçenekleri oluşturun
TextSearchOptions textOptions = new TextSearchOptions
{
    AllPages = true,
    
    // Bir temsilci kullanarak özel işlemeyi tanımlayın
    ProcessCompleted = (signature) =>
    {
        // Özel doğrulama mantığı - yalnızca belirtilen sayfalardaki imzaları kabul et
        TextSignature textSignature = signature as TextSignature;
        return textSignature != null && (textSignature.PageNumber == 1 || textSignature.PageNumber == 2);
    }
};
```

## Çözüm

Bu kapsamlı kılavuzda, .NET için GroupDocs.Signature kullanarak belgelerde birden fazla imza türünü nasıl arayacağınızı inceledik. Farklı imza türleri için arama seçenekleri ayarlamaktan sonuçları işleyip doğrulamaya kadar, artık .NET uygulamalarınızda güçlü imza arama işlevselliğini uygulamak için gereken bilgiye sahipsiniz.

Birden fazla imza türünü aynı anda arama olanağı, belge doğrulama süreçlerini iyileştirir, güvenlik önlemlerini güçlendirir ve belge doğrulama iş akışlarını kolaylaştırır. GroupDocs.Signature, farklı belge formatlarında çeşitli imza türleriyle çalışmak için güçlü ve esnek bir çerçeve sunarak belge işleme uygulamaları için mükemmel bir seçimdir.

## SSS

### Şifreyle korunan belgelerde imzaları arayabilir miyim?

Evet, GroupDocs.Signature parola korumalı belgelerde imza aramayı destekler. Parolayı, belgeyi başlatırken sağlayabilirsiniz. `Signature` nesne:

```csharp
LoadOptions loadOptions = new LoadOptions { Password = "your_password" };
using (Signature signature = new Signature(filePath, loadOptions))
{
    // İmzaları arayın
}
```

### İmza araması için hangi belge biçimleri destekleniyor?

GroupDocs.Signature, PDF, Microsoft Office belgeleri (Word, Excel, PowerPoint), OpenOffice biçimleri, resimler ve daha fazlası dahil olmak üzere çok çeşitli belge biçimlerini destekler.

### Aramayı bir belgedeki belirli sayfalarla sınırlayabilir miyim?

Evet, her arama seçeneği türünün hangi sayfalarda arama yapacağınızı belirtmenize olanak tanıyan özellikleri vardır:

```csharp
TextSearchOptions options = new TextSearchOptions
{
    AllPages = false,  // Tüm sayfaları aramayın
    PageNumber = 1,    // Sadece 1. sayfada ara
    
    // Veya birden fazla sayfa belirtin
    PagesSetup = new PagesSetup { Pages = new List<int> { 1, 3, 5 } }
};
```

### Büyük belgelerde arama yaparken performansı nasıl optimize edebilirim?

Büyük belgeler için performansı şu şekilde optimize edebilirsiniz:

1. Aramayı belirli sayfalarla veya sayfa aralıklarıyla sınırlama
2. Potansiyel eşleşme sayısını azaltmak için daha spesifik arama ölçütleri kullanma
3. Sonuç görüntülemenizde sayfalandırmayı uygulama
4. Eşzamanlı sonuçlara ihtiyacınız yoksa, bir seferde bir imza türünü arayın

### GroupDocs.Signature'ı özel imza türlerini destekleyecek şekilde genişletebilir miyim?

GroupDocs.Signature, yaygın imza türleri için yerleşik destek sağlarken işlevselliğini şu şekilde genişletebilirsiniz:

1. Özel arama seçenekleri sınıfları türetilerek oluşturuluyor `SearchOptions`
2. Özel işleme mantığını kullanarak uygulama `ProcessCompleted` temsilci
3. Birden fazla imza aramasını gelişmiş iş mantığıyla birleştiren sarmalayıcı sınıflar geliştirme

## Ayrıca bakınız

* [API Referansı](https://reference.groupdocs.com/signature/net/)
* [GitHub'daki Kod Örnekleri](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
* [Ürün Dokümantasyonu](https://docs.groupdocs.com/signature/net/)
* [Ürün Sayfası](https://products.groupdocs.com/signature/net/)
* [En Son Sürümü İndirin](https://releases.groupdocs.com/signature/net/)
* [Blog Yazıları](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
* [Ücretsiz Destek Forumu](https://forum.groupdocs.com/c/signature/13)
* [Geçici Lisans](https://purchase.groupdocs.com/temporary-license/)