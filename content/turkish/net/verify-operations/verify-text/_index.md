---
"description": "GroupDocs.Signature ile .NET uygulamalarında metin imzası doğrulamasını öğrenin. Tam kod örnekleri ve en iyi uygulamalarla adım adım uygulama kılavuzu."
"linktitle": "Metni Doğrula"
"second_title": "GroupDocs.Signature .NET API"
"title": "Belgelerdeki Metin İmzalarını Doğrulayın"
"url": "/tr/net/verify-operations/verify-text/"
"weight": 13
type: docs
---
## giriiş

Metin imzaları, genellikle dijital veya elektronik imzalardan daha basit olsa da, belge yönetimi ve doğrulamasında önemli bir rol oynar. Filigranlar, alt bilgi metinleri veya belirli içerik kalıpları olsun, metin imzalarının varlığını ve bütünlüğünü doğrulamak, belge doğrulama süreçlerinin önemli bir parçasıdır.

GroupDocs.Signature for .NET, çok çeşitli formatlardaki belgelerdeki metin imzalarını doğrulamak için güçlü bir API sağlar. Bu kapsamlı eğitim, .NET uygulamalarınızda metin doğrulama işlevini uygulayarak belgelerinizin bütünlüğünü ve orijinalliğini korumanızı sağlayacaktır.

## Ön koşullar

Metin doğrulama işlevini uygulamadan önce aşağıdaki ön koşulların mevcut olduğundan emin olun:

1. GroupDocs.Signature for .NET: Kitaplığı şu adresten indirin ve yükleyin: [indirme sayfası](https://releases.groupdocs.com/signature/net/).
2. .NET Geliştirme Ortamı: Visual Studio veya uyumlu herhangi bir .NET geliştirme ortamı.
3. Temel Bilgi: C# programlama ve .NET framework kavramlarına aşinalık.
4. Test Belgesi: Doğrulama amaçlı metin imzaları içeren belge.

## Gerekli Ad Alanlarını İçe Aktar

GroupDocs.Signature işlevine erişmek için gerekli ad alanlarını içe aktararak başlayın:

```csharp
using System;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

Metin doğrulama sürecini anlaşılır ve yönetilebilir adımlara bölelim:

## Adım 1: Belge Yolunu Belirleyin

```csharp
// Metin imzalarını içeren belgenin yolu
string filePath = "sample_multiple_signatures.docx";
```

Örnek yolu, metin imzalarını içeren belgenizin gerçek yoluyla değiştirdiğinizden emin olun.

## Adım 2: İmza Nesnesini Başlatın

```csharp
// Belge yolunu geçirerek Signature sınıfının bir örneğini oluşturun
using (Signature signature = new Signature(filePath))
{
    // Doğrulama kodu burada uygulanacaktır
}
```

Signature sınıfı, GroupDocs.Signature API'sindeki tüm işlemler için ana giriş noktasıdır.

## Adım 3: Metin Doğrulama Seçeneklerini Yapılandırın

```csharp
// Metin doğrulama seçeneklerini tanımlayın
TextVerifyOptions options = new TextVerifyOptions()
{
    AllPages = true,                               // Belgenin tüm sayfalarını kontrol edin
    SignatureImplementation = TextSignatureImplementation.Native,
    Text = "signature",                            // Doğrulanması gereken metin
    MatchType = TextMatchType.Contains             // Eşleşen kriterleri belirtin
};
```

Doğrulama seçenekleri, doğrulama süreci için belirli kriterleri tanımlamanıza olanak tanır:
- `AllPages`: Tüm belge sayfalarını kontrol etmek için doğru olarak ayarlayın
- `SignatureImplementation`: Metnin nasıl uygulanacağını belirtin (Yerel veya Etiket)
- `Text`: Belge içinde eşleşecek metin içeriği
- `MatchType`: Metin eşleştirme yöntemi (İçerir, Tam, Başlar, vb.)

## Adım 4: Doğrulama İşlemini Gerçekleştirin

```csharp
// Doğrulamayı gerçekleştirin
VerificationResult result = signature.Verify(options);
```

Bu, belirttiğiniz seçeneklere göre doğrulama işlemini gerçekleştirir.

## Adım 5: İşlem Doğrulama Sonuçları

```csharp
// Doğrulama sonucunu kontrol edin ve buna göre işlem yapın
if (result.IsValid)
{
    Console.WriteLine($"Document {filePath} contains valid text signatures!");
    
    // Başarılı imzalar hakkında bilgi görüntüle
    foreach (TextSignature textSignature in result.Succeeded)
    {
        Console.WriteLine($"\nFound valid text signature:");
        Console.WriteLine($"Text: {textSignature.Text}");
        Console.WriteLine($"Location: Page {textSignature.PageNumber}, {textSignature.Left}x{textSignature.Top}");
    }
}
else
{
    Console.WriteLine($"Document {filePath} failed verification process.");
    Console.WriteLine($"Number of failed signatures: {result.Failed.Count}");
}
```

Bu kod doğrulamanın başarılı olup olmadığını kontrol eder ve doğrulanan metin imzaları hakkında ayrıntılı bilgi sağlar.

## Tam Örnek

İşte metin imzası doğrulamasını gösteren tam bir çalışma örneği:

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
            
            try
            {
                // İmza örneğini başlat
                using (Signature signature = new Signature(filePath))
                {
                    // Kurulum doğrulama seçenekleri
                    TextVerifyOptions options = new TextVerifyOptions()
                    {
                        AllPages = true,
                        SignatureImplementation = TextSignatureImplementation.Native,
                        Text = "signature",
                        MatchType = TextMatchType.Contains
                    };
                    
                    // Belge imzalarını doğrulayın
                    VerificationResult result = signature.Verify(options);
                    
                    // İşlem doğrulama sonuçları
                    if(result.IsValid)
                    {
                        Console.WriteLine($"\nDocument {filePath} was verified successfully!");
                        foreach (TextSignature item in result.Succeeded)
                        {
                            Console.WriteLine($"\nValid signature is found with text: {item.Text}");
                            Console.WriteLine($"Location: Page {item.PageNumber}, position {item.Left}x{item.Top}");
                        }
                    }
                    else
                    {
                        Console.WriteLine($"\nDocument {filePath} failed verification process.");
                    }
                }
            }
            catch (Exception ex)
            {
                Console.WriteLine($"Error: {ex.Message}");
            }
        }
    }
}
```

## Gelişmiş Doğrulama Senaryoları

GroupDocs.Signature, daha karmaşık doğrulama senaryoları için ek seçenekler sunar:

### Doğrulama İçin Düzenli İfadelerin Kullanımı

Daha esnek desen eşleştirmesi için düzenli ifadeleri kullanabilirsiniz:

```csharp
TextVerifyOptions options = new TextVerifyOptions()
{
    Text = "Invoice\\s+#\\d{5,6}",  // "Fatura #12345" gibi kalıpları eşleştirin
    MatchType = TextMatchType.Regex
};
```

### Belirli Belge Alanlarındaki Metni Doğrulama

Doğrulamayı belgenin belirli alanlarıyla sınırlayabilirsiniz:

```csharp
TextVerifyOptions options = new TextVerifyOptions()
{
    AllPages = false,
    PageNumber = 1,  // Sadece ilk sayfada doğrulayın
    
    // Arama yapılacak alanı tanımlayın (nokta cinsinden koordinatlar)
    PagesSetup = new PagesSetup() 
    { 
        FirstPage = true,
        LastPage = false,
        OddPages = false,
        EvenPages = false 
    },
    
    // Dikdörtgen alanı milimetre cinsinden
    Rectangle = new Rectangle(10, 10, 100, 30),
    
    Text = "Confidential"
};
```

### Birden Fazla Metin Desenini Aynı Anda Doğrulama

Farklı metin desenlerini kontrol etmek için birden fazla doğrulama seçeneği oluşturabilirsiniz:

```csharp
// Doğrulama seçeneklerinin bir listesini oluşturun
List<VerifyOptions> listOptions = new List<VerifyOptions>();

// İlk metin doğrulamasını ekle
listOptions.Add(new TextVerifyOptions()
{
    Text = "Confidential",
    MatchType = TextMatchType.Exact
});

// İkinci metin doğrulamasını ekle
listOptions.Add(new TextVerifyOptions()
{
    Text = "Do not copy",
    MatchType = TextMatchType.Contains
});

// Birden fazla seçenekle doğrulayın
VerificationResult result = signature.Verify(listOptions);
```

### Belirli Görünüme Sahip Metni Doğrulama

Ayrıca metni belirli biçimlendirme özelliklerine göre de doğrulayabilirsiniz:

```csharp
TextVerifyOptions options = new TextVerifyOptions()
{
    Text = "APPROVED",
    MatchType = TextMatchType.Exact,
    
    // Belirli görünüm özelliklerini doğrulayın
    ForegroundColorRGB = System.Drawing.Color.Green,
    Font = new SignatureFont() { FontFamily = "Arial", FontSize = 12, Bold = true }
};
```

## Metin Doğrulaması için En İyi Uygulamalar

1. Uygun Eşleşme Türlerini Seçin: Doğrulama gereksinimlerinize göre doğru eşleşme türünü (İçerir, Tam, Düzenli İfade) seçin.
2. Performans İçin Optimize Edin: Büyük belgeler için, tüm belgeyi doğrulamak yerine belirli sayfaları doğrulamayı düşünün.
3. Hata Yönetimi: Beklenmeyen senaryoları zarif bir şekilde yönetmek için uygun hata yönetimini uygulayın.
4. Büyük/Küçük Harf Duyarlılığını Göz Önünde Bulundurun: Özellikle kritik doğrulamalarda, metin eşleştirmede büyük/küçük harf duyarlılığına dikkat edin.
5. Kapsamlı Test: Uyumluluğu sağlamak için çeşitli belge biçimleri ve metin desenleriyle test doğrulaması yapın.

## Yaygın Sorunların Giderilmesi

### Metin Algılanamadı
- Metin biçimlendirmesinin veya kodlamasının algılamayı etkileyip etkilemediğini kontrol edin
- Metnin belgede normal metin olarak (görüntü olarak değil) mevcut olduğundan emin olun
- Farklı eşleştirme ölçütlerini deneyin (Tam yerine İçerir)

### Performans Sorunları
- Belirli sayfaları veya alanları hedefleyerek doğrulamayı optimize edin
- Yanlış pozitifleri azaltmak için daha spesifik metin kalıpları kullanın

### Doğrulama Hataları
- Boşlukların, özel karakterlerin veya biçimlendirmenin eşleşmeyi etkileyip etkilemediğini kontrol edin
- Metnin taranmış bir görüntünün parçası olmadığını doğrulayın (bunun için OCR gerekir)
- Metin eklendikten sonra belgenin değiştirilmediğinden emin olun

## Çözüm

Metin doğrulama, tek başına veya diğer doğrulama yöntemleriyle birlikte kullanılabilen, belge kimlik doğrulamaya yönelik çok yönlü ve pratik bir yaklaşımdır. GroupDocs.Signature for .NET, .NET uygulamalarınızda güçlü metin doğrulama işlevselliğini uygulamak için kapsamlı ve kullanımı kolay bir API sağlar.

Bu adım adım kılavuzu izleyerek şunları öğrendiniz:
- Metin doğrulama sürecini yapılandırın ve başlatın
- Çeşitli doğrulama kriterlerini belirtin
- Doğrulama sonuçlarını işleyin ve yorumlayın
- Gelişmiş doğrulama senaryolarını uygulayın

Bu yetenekler, çeşitli belge formatlarındaki metinlerin doğruluğunu doğrulayabilen güvenli ve güvenilir belge işleme sistemleri oluşturmanıza olanak tanır.

## SSS

### GroupDocs.Signature taranan belgelerdeki metni doğrulayabilir mi?
GroupDocs.Signature, öncelikle dijital metin doğrulaması için tasarlanmıştır. Taranan belgelerde, taranan görüntüleri metne dönüştürmek için öncelikle OCR (Optik Karakter Tanıma) teknolojisini kullanmanız gerekir.

### Metin doğrulaması için hangi belge biçimleri destekleniyor?
GroupDocs.Signature, PDF, Word belgeleri (DOC, DOCX), Excel elektronik tabloları (XLS, XLSX), PowerPoint sunumları (PPT, PPTX), resimler ve daha fazlası dahil olmak üzere çok çeşitli belge biçimlerini destekler.

### Biçimlendirilmiş metni (kalın, italik, belirli yazı tipleri) doğrulayabilir miyim?
Evet, GroupDocs.Signature, yazı tipi ailesi, boyut, stil (kalın, italik) ve renk dahil olmak üzere belirli biçimlendirme özelliklerine sahip metni doğrulamak için seçenekler sunar.

### Şifreyle korunan belgelerdeki metinleri doğrulamak mümkün müdür?
Evet, GroupDocs.Signature, doğrulama için korumalı belgeleri açarken belge parolalarını belirtme seçenekleri sunar.

### Filigranları ve arka plan metinlerini doğrulayabilir miyim?
Evet, GroupDocs.Signature, belgede nasıl uygulandığına bağlı olarak filigranlar ve arka plan metni dahil olmak üzere çeşitli metin imzası türlerini doğrulayabilir.

### İlgili Kaynaklar
* [GroupDocs.Signature API Referansı](https://reference.groupdocs.com/signature/net/)
* [GroupDocs.Signature İndirmeleri](https://releases.groupdocs.com/signature/net/)
* [GitHub'daki Kod Örnekleri](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
* [Belgeleme](https://docs.groupdocs.com/signature/net/)
* [Ürün Sayfası](https://products.groupdocs.com/signature/net/)
* [Blog Yazıları](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
* [Destek Forumu](https://forum.groupdocs.com/c/signature/13)
* [Geçici Lisans](https://purchase.groupdocs.com/temporary-license/)