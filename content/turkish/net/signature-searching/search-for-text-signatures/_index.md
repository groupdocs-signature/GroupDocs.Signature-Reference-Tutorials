---
"description": ".NET için GroupDocs.Signature'ı kullanarak belgelerdeki metin imzalarını nasıl etkili bir şekilde arayacağınızı kapsamlı adım adım kılavuzumuz ve kod örneklerimizle öğrenin."
"linktitle": "Metin İmzalarını Ara"
"second_title": "GroupDocs.Signature .NET API"
"title": "Belgelerde Metin İmzalarını Ara"
"url": "/tr/net/signature-searching/search-for-text-signatures/"
"weight": 16
type: docs
---
## giriiş

Metin imzaları, belge yazarlığını, onayını veya doğrulamasını göstermenin yaygın bir yöntemidir. Dijital belge yönetiminde, metin imzalarını programatik olarak arama ve çıkarma yeteneği, belge doğrulama, iş akışı otomasyonu ve uyumluluk doğrulaması için çok önemlidir. GroupDocs.Signature for .NET, .NET uygulamalarınızda metin imzası arama işlevini uygulamak için kapsamlı bir çözüm sunar ve çeşitli belge biçimlerini ve gelişmiş arama özelliklerini destekler.

Bu eğitim, .NET için GroupDocs.Signature kullanarak belgelerde metin imzalarını arama sürecinde size rehberlik edecek, ayrıntılı açıklamalar, adım adım talimatlar ve pratik kod örnekleri sağlayacaktır.

## Ön koşullar

Metin imzası aramasına başlamadan önce aşağıdaki ön koşullara sahip olduğunuzdan emin olun:

1. .NET için GroupDocs.Signature Kitaplığı: Kitaplığı şu adresten indirin ve yükleyin: [sürümler sayfası](https://releases.groupdocs.com/signature/net/).

2. Geliştirme Ortamı: Visual Studio veya .NET desteği olan herhangi bir uyumlu IDE gibi uygun bir geliştirme ortamı kurun.

3. Örnek Belgeler: Doğrulama ve test için metin imzaları içeren test belgeleri hazırlayın.

4. Temel C# Bilgisi: C# programlama dili ve .NET framework kavramlarına aşinalık.

## Ad Alanlarını İçe Aktar

GroupDocs.Signature işlevine erişmek için gerekli ad alanlarını içe aktararak başlayın:

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

Şimdi, metin imzalarını arama sürecini açık ve yönetilebilir adımlara bölelim:

## Adım 1: Belgeyi Yükleyin

İlk olarak, belge yolunu tanımlayın ve bir belge başlatın. `Signature` nesne:

```csharp
string filePath = "sample_multiple_signatures.docx";
string fileName = Path.GetFileName(filePath);

using (Signature signature = new Signature(filePath))
{
    // Metin imzası arama kodu buraya eklenecek
}
```

## Adım 2: Arama Seçeneklerini Yapılandırın

Oluştur ve yapılandır `TextSearchOptions` metin imzalarının nasıl aranacağını belirtmek için:

```csharp
// Metin arama seçeneklerini yapılandırın
TextSearchOptions options = new TextSearchOptions
{
    // Tüm sayfalarda ara
    AllPages = true,
    
    // İsteğe bağlı: Eşleşecek metni belirtin
    // Metin = "Onaylandı",
    
    // İsteğe bağlı: eşleşme türünü belirtin
    // Eşleşme Türü = TextMatchType.Contains
};
```

## Adım 3: Metin İmzası Araması Gerçekleştirin

Yapılandırılan seçenekleri kullanarak arama işlemini gerçekleştirin:

```csharp
// Metin imzalarını arayın
List<TextSignature> signatures = signature.Search<TextSignature>(options);
```

## 4. Adım: Sonuçları İşleyin ve Görüntüleyin

Bulunan metin imzalarını inceleyin ve ayrıntılarını görüntüleyin:

```csharp
// Arama sonuçlarını görüntüle
Console.WriteLine($"\nSource document '{fileName}' contains {signatures.Count} text signature(s):");

foreach (TextSignature textSignature in signatures)
{
    Console.WriteLine($"Text signature found at page {textSignature.PageNumber} with text '{textSignature.Text}'");
    Console.WriteLine($"Location: X={textSignature.Left}, Y={textSignature.Top}, Width={textSignature.Width}, Height={textSignature.Height}");
    Console.WriteLine($"Signature type: {textSignature.SignatureImplementation}");
    Console.WriteLine();
}
```

## Tam Örnek

İşte bir belgede metin imzalarının nasıl aranacağını gösteren eksiksiz bir çalışma örneği:

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;

namespace TextSignatureSearch
{
    class Program
    {
        static void Main(string[] args)
        {
            // Belge yolu - dosya yolunuzla güncelleyin
            string filePath = "sample_multiple_signatures.docx";
            string fileName = Path.GetFileName(filePath);
            
            // İmza örneğini başlat
            using (Signature signature = new Signature(filePath))
            {
                try
                {
                    // Metin arama seçeneklerini yapılandırın
                    TextSearchOptions options = new TextSearchOptions
                    {
                        // Tüm sayfalarda ara
                        AllPages = true
                    };
                    
                    // Metin imzalarını arayın
                    List<TextSignature> signatures = signature.Search<TextSignature>(options);
                    
                    // Arama sonuçlarını görüntüle
                    Console.WriteLine($"\nSource document '{fileName}' contains {signatures.Count} text signature(s):");
                    
                    foreach (TextSignature textSignature in signatures)
                    {
                        Console.WriteLine($"Text signature found at page {textSignature.PageNumber} with text '{textSignature.Text}'");
                        Console.WriteLine($"Location: X={textSignature.Left}, Y={textSignature.Top}, Width={textSignature.Width}, Height={textSignature.Height}");
                        Console.WriteLine($"Signature type: {textSignature.SignatureImplementation}");
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

## Gelişmiş Metin İmza Arama Teknikleri

### Belirli Metin Kriterleriyle Arama

Daha hedefli aramalar için özelleştirebilirsiniz `TextSearchOptions` belirli metin içeriğine göre filtrelemek için:

```csharp
// Belirli metin ölçütleriyle arama seçenekleri oluşturun
TextSearchOptions options = new TextSearchOptions
{
    // Tüm sayfalarda ara
    AllPages = true,
    
    // Belirli bir metni arayın
    Text = "Approved",
    
    // Eşleşme türünü belirtin (İçerir, Tam, Başlangıç, Bitiş)
    MatchType = TextMatchType.Contains,
    
    // Büyük/küçük harfe duyarlı arama
    MatchCase = true
};
```

### Belirli Belge Alanlarında Arama

Aramayı belgenin belirli alanlarıyla sınırlayabilirsiniz:

```csharp
// Belirli bir belge alanı için arama seçenekleri oluşturun
TextSearchOptions options = new TextSearchOptions
{
    // Yalnızca belirli sayfalarda arama yapın
    AllPages = false,
    PageNumber = 1,
    
    // Veya birden fazla sayfa belirtin
    PagesSetup = new PagesSetup { Pages = new List<int> { 1, 3, 5 } },
    
    // İçinde arama yapılacak belirli bir alanı tanımlayın
    Rectangle = new Rectangle(100, 100, 400, 200)
};
```

### Gelişmiş Metin Filtreleme

Daha karmaşık arama gereksinimleri için özel filtreleme mantığını uygulayın:

```csharp
// Özel işlemeyle arama seçenekleri oluşturun
TextSearchOptions options = new TextSearchOptions
{
    AllPages = true,
    
    // Bir temsilci kullanarak özel işlemeyi tanımlayın
    ProcessCompleted = (TextSignature signature) =>
    {
        // Özel doğrulama mantığı
        bool isValid = signature.Text.Length > 5 && 
                      (signature.Text.Contains("Approved") || signature.Text.Contains("Verified"));
        
        return isValid;
    }
};
```

### Farklı Metin Stilleri Arama

Metin imzalarını filtrelemek için yazı tipi ve stil özelliklerini kullanın:

```csharp
// Belirli metin görünümünü hedefleyen arama seçenekleri oluşturun
TextSearchOptions options = new TextSearchOptions
{
    // Yazı tipi adına göre filtrele
    FontName = "Arial",
    
    // Yazı tipi boyutu aralığına göre filtrele
    MinFontSize = 10,
    MaxFontSize = 14,
    
    // Yazı tipi rengine göre filtrele
    ForeColor = System.Drawing.Color.Blue
};
```

### İmza Meta Verilerini Çıkarma

Metin imzalarıyla ilişkili meta verileri çıkarın ve işleyin:

```csharp
foreach (TextSignature signature in signatures)
{
    // İmza meta verilerine erişim
    if (signature.Metadata != null && signature.Metadata.Count > 0)
    {
        Console.WriteLine("Signature Metadata:");
        
        foreach (var item in signature.Metadata)
        {
            Console.WriteLine($"  {item.Key}: {item.Value}");
        }
    }
    
    // İmza oluşturma ve değiştirme tarihlerini kontrol edin
    if (signature.CreatedOn.HasValue)
    {
        Console.WriteLine($"Created on: {signature.CreatedOn.Value}");
    }
    
    if (signature.ModifiedOn.HasValue)
    {
        Console.WriteLine($"Modified on: {signature.ModifiedOn.Value}");
    }
}
```

## Çözüm

Bu kapsamlı kılavuzda, .NET için GroupDocs.Signature kullanarak belgelerde metin imzalarının nasıl aranacağını inceledik. Temel arama işlemlerinden gelişmiş tekniklere kadar, artık .NET uygulamalarınızda güçlü metin imzası işlevselliğini uygulamak için gereken bilgiye sahipsiniz.

GroupDocs.Signature, metin imzalarıyla çalışmak için güçlü ve esnek bir çerçeve sunarak, gelişmiş belge doğrulama sistemleri, otomatik iş akışı çözümleri ve uyumluluk doğrulama araçları oluşturmanıza olanak tanır.

## SSS

### Şifreyle korunan belgelerde metin imzalarını arayabilir miyim?

Evet, GroupDocs.Signature, parola korumalı belgelerde metin imzalarının aranmasını destekler. Başlatma sırasında parolayı girebilirsiniz. `Signature` nesne:

```csharp
LoadOptions loadOptions = new LoadOptions { Password = "your_password" };
using (Signature signature = new Signature(filePath, loadOptions))
{
    // Metin imzalarını arayın
}
```

### Metin imzası araması için hangi belge biçimleri destekleniyor?

GroupDocs.Signature, PDF, Microsoft Office belgeleri (Word, Excel, PowerPoint), OpenOffice biçimleri, resimler ve daha fazlası dahil olmak üzere çok çeşitli belge biçimlerini destekler.

### Kalın veya italik gibi belirli biçimlendirmelere sahip metin imzalarını arayabilir miyim?

Evet, belirli biçimlendirmeye sahip metin imzalarını kullanarak arayabilirsiniz. `FontBold` Ve `FontItalic` özellikleri `TextSearchOptions`:

```csharp
TextSearchOptions options = new TextSearchOptions
{
    FontBold = true,
    FontItalic = true
};
```

### Büyük belgelerde arama performansını nasıl artırabilirim?

Büyük belgeler için arama performansını şu şekilde optimize edebilirsiniz:

1. Tüm belgeyi aramak yerine aramayı belirli sayfalarla sınırlama
2. Eşleşme sayısını azaltmak için daha spesifik arama ölçütleri kullanma
3. Arama alanını kullanarak bir arama alanı belirtme `Rectangle` İmzaların genellikle nerede bulunduğunu biliyorsanız mülk
4. Uygulamanızda arama sonuçlarını toplu olarak işlemek için sayfalandırmayı uygulama

### Bir metin imzasının elektronik olarak eklenip eklenmediğini veya orijinal belge içeriğinin bir parçası olup olmadığını tespit edebilir miyim?

GroupDocs.Signature, belgelerdeki farklı metin öğesi türleri arasında ayrım yapabilir. `SignatureImplementation` mülkiyeti `TextSignature` Metnin resmi bir imza mı yoksa normal bir belge içeriği mi olduğunu belirtir. Ancak kesin tespit, metnin belgeye başlangıçta nasıl eklendiğine bağlı olabilir.

## Ayrıca bakınız

* [API Referansı](https://reference.groupdocs.com/signature/net/)
* [GitHub'daki Kod Örnekleri](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
* [Ürün Dokümantasyonu](https://docs.groupdocs.com/signature/net/)
* [Ürün Sayfası](https://products.groupdocs.com/signature/net/)
* [En Son Sürümü İndirin](https://releases.groupdocs.com/signature/net/)
* [Blog Yazıları](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
* [Ücretsiz Destek Forumu](https://forum.groupdocs.com/c/signature/13)
* [Geçici Lisans](https://purchase.groupdocs.com/temporary-license/)