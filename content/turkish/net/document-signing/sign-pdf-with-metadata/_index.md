---
"description": "GroupDocs.Signature for .NET kullanarak PDF belgelerine meta veri imzaları entegre edin. PDF'lerin özgünlüğünü ve izlenebilirliğini artırmak için yazar bilgilerini, zaman damgalarını ve özel verileri nasıl yerleştireceğinizi öğrenin."
"linktitle": "PDF'yi Meta Verilerle İmzala"
"second_title": "GroupDocs.Signature .NET API"
"title": "C# .NET'te PDF Belgelerine Meta Veri İmzaları Ekleme"
"url": "/tr/net/document-signing/sign-pdf-with-metadata/"
"weight": 11
type: docs
---
## giriiş

PDF (Taşınabilir Belge Biçimi) belgeleri, tutarlılıkları ve platform bağımsızlıkları nedeniyle sektörler arasında yaygın olarak kullanılmaktadır. Bu belgelerin gerçekliğini ve izlenebilirliğini sağlamak birçok profesyonel ortamda hayati önem taşır. Bunu başarmanın etkili bir yolu, meta verileri PDF dosyalarının kendilerine yerleştirmektir.

Bu kapsamlı eğitimde, .NET için GroupDocs.Signature kullanarak PDF belgelerini meta verilerle nasıl imzalayacağınızı inceleyeceğiz. Meta veri imzaları, belgenin görünümünü gözle görülür şekilde değiştirmeden yazar bilgileri, oluşturma zaman damgaları, belge tanımlayıcıları ve özel değerler gibi ek bilgileri belgeye yerleştirmenize olanak tanır.

## Ön koşullar

Başlamadan önce aşağıdakilerin mevcut olduğundan emin olun:

1. [.NET için GroupDocs.Signature](https://releases.groupdocs.com/signature/net/) - Kütüphaneyi indirin ve kurun
2. Geliştirme Ortamı - Visual Studio veya herhangi bir .NET uyumlu IDE
3. PDF Belgesi - İmzalama için örnek bir PDF dosyası
4. Temel C# Bilgisi - C# programlama diline aşinalık

## Ad Alanlarını İçe Aktar

GroupDocs.Signature işlevine erişmek için gerekli ad alanlarını içe aktararak başlayın:

```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

## Adım 1: Dosya Yollarını Ayarlayın

Öncelikle PDF belgenizin yolunu tanımlayın ve imzalı çıktıyı nereye kaydetmek istediğinizi belirtin:

```csharp
// PDF belgenizin yolunu belirtin
string filePath = "sample.pdf";

// Çıktı dizinini ve dosya yolunu tanımlayın
string outputDirectory = "Your Document Directory";
string outputFilePath = Path.Combine(outputDirectory, "SignPdfWithMetadata", "SignedWithMetadata.pdf");

// Çıktı dizininin mevcut olduğundan emin olun
Directory.CreateDirectory(Path.GetDirectoryName(outputFilePath));
```

## Adım 2: İmza Nesnesini Başlatın

Kaynak PDF belgenizle Signature sınıfının bir örneğini oluşturun:

```csharp
using (Signature signature = new Signature(filePath))
{
    // İmzalama kodu buraya gelecek
}
```

## Adım 3: Meta Veri Seçeneklerini Tanımlayın

Çeşitli meta veri imzası türlerini ekleyerek meta veri seçeneklerini oluşturun ve yapılandırın:

```csharp
// Meta veri seçenekleri nesnesi oluştur
MetadataSignOptions options = new MetadataSignOptions();

// Akıcı arayüzü kullanarak çeşitli meta veri türleri ekleyin
options
    .Add(new PdfMetadataSignature("Author", "Mr.Sherlock Holmes")) // Dize değeri
    .Add(new PdfMetadataSignature("CreatedOn", DateTime.Now))       // DateTime değeri
    .Add(new PdfMetadataSignature("DocumentId", 123456))            // Tam sayı değeri
    .Add(new PdfMetadataSignature("SignatureId", 123.456D))         // Çift değer
    .Add(new PdfMetadataSignature("Amount", 123.456M))              // Ondalık değer
    .Add(new PdfMetadataSignature("Total", 123.456F));              // Kayan nokta değeri
```

## Adım 4: PDF'yi Meta Verilerle İmzalayın

Meta veri imzalarını PDF belgesine uygulayın ve sonucu kaydedin:

```csharp
// Belgeyi imzalayın ve çıktı yoluna kaydedin
SignResult result = signature.Sign(outputFilePath, options);

// Başarı mesajını görüntüle
Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} metadata signature(s).");
Console.WriteLine($"Signed document saved at: {outputFilePath}");
```

## Tam Örnek

İşte tüm adımları bir araya getiren tam kod örneği:

```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;

namespace SignPdfWithMetadataExample
{
    class Program
    {
        static void Main(string[] args)
        {
            // Dosya yollarını belirtin
            string filePath = "sample.pdf";
            string outputFilePath = Path.Combine("Your Document Directory", "SignPdfWithMetadata", "SignedWithMetadata.pdf");
            
            // Çıktı dizininin mevcut olduğundan emin olun
            Directory.CreateDirectory(Path.GetDirectoryName(outputFilePath));

            // PDF'yi meta verilerle imzalayın
            using (Signature signature = new Signature(filePath))
            {
                // Meta veri seçenekleri nesnesi oluştur
                MetadataSignOptions options = new MetadataSignOptions();
                
                // Farklı türde meta veri imzaları ekleyin
                options
                    .Add(new PdfMetadataSignature("Author", "Mr.Sherlock Holmes")) // Dize değeri
                    .Add(new PdfMetadataSignature("CreatedOn", DateTime.Now))       // DateTime değeri
                    .Add(new PdfMetadataSignature("DocumentId", 123456))            // Tam sayı değeri
                    .Add(new PdfMetadataSignature("SignatureId", 123.456D))         // Çift değer
                    .Add(new PdfMetadataSignature("Amount", 123.456M))              // Ondalık değer
                    .Add(new PdfMetadataSignature("Total", 123.456F));              // Kayan nokta değeri
                
                // Belgeyi imzalayın ve dosyaya kaydedin
                SignResult result = signature.Sign(outputFilePath, options);
                
                // Sonuçları görüntüle
                Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).");
                Console.WriteLine($"File saved at {outputFilePath}.");
            }
        }
    }
}
```

## Gelişmiş PDF Meta Veri İşlemleri

### Ad Alanı Desteğiyle Özel Meta Veri Ekleme

PDF belgeleri XML ad alanı desteğiyle özel meta verileri destekler:

```csharp
// Ad alanıyla özel meta veri ekleyin
options.Add(new PdfMetadataSignature("CustomProperty", "Custom Value")
{
    NamespaceUri = "http://your-namespace.com/schema"
});
```

### İmzalanmış PDF'lerde Meta Veri Arama

İmzalamanın ardından meta verileri doğrulamak veya çıkarmak isteyebilirsiniz:

```csharp
// Meta veriler için arama seçenekleri oluşturun
MetadataSearchOptions searchOptions = new MetadataSearchOptions();

// Meta veri imzalarını arayın
SearchResult searchResult = signature.Search(searchOptions);

// Bulunan imzaları görüntüle
Console.WriteLine($"Found {searchResult.Signatures.Count} metadata signatures:");
foreach (var foundSignature in searchResult.Signatures)
{
    MetadataSignature metadataSignature = foundSignature as MetadataSignature;
    if (metadataSignature != null)
    {
        Console.WriteLine($"- {metadataSignature.Name}: {metadataSignature.Value} ({metadataSignature.Value.GetType().Name})");
    }
}
```

### Standart PDF Meta Verileri ile Çalışma

PDF belgelerinde erişilebilen ve değiştirilebilen standart meta veri alanları bulunur:

```csharp
// Standart PDF meta veri alanlarını ayarlayın
options
    .Add(new PdfMetadataSignature("Title", "Important Contract"))
    .Add(new PdfMetadataSignature("Subject", "Legal Agreement"))
    .Add(new PdfMetadataSignature("Keywords", "contract, agreement, legal, binding"))
    .Add(new PdfMetadataSignature("Creator", "Legal Department"))
    .Add(new PdfMetadataSignature("Producer", "GroupDocs.Signature"));
```

## Çözüm

Bu eğitimde, .NET için GroupDocs.Signature kullanarak PDF belgelerini meta verilerle nasıl imzalayacağınızı öğrendiniz. PDF dosyalarına meta veri eklemek, belge özgünlüğünü artırmak, önemli bilgiler eklemek ve belge yönetimi iş akışlarını iyileştirmek için mükemmel bir yol sağlar.

PDF'lerdeki meta veri imzaları, belge izlenebilirliği ve özgünlük doğrulamasının önemli olduğu iş ortamlarında özellikle değerlidir. Gömülü meta veriler, belgenin kaynağı, yazarı, oluşturulma zamanı, sürümü ve kuruluşunuzun iş akışıyla ilgili özel özellikler hakkında bilgiler içerebilir.

GroupDocs.Signature ile meta veri imzalarını uygulayarak PDF belgelerinizin bütünlüğünü korumasını ve yaşam döngüsü boyunca doğrulanabilir bilgiler sağlamasını sağlayabilirsiniz.

## SSS

### PDF belgesindeki mevcut meta verileri değiştirebilir miyim?

Evet, PDF belgelerindeki mevcut meta verileri değiştirebilirsiniz. Mevcut meta verilerle aynı adlara sahip yeni meta veri imzaları uyguladığınızda, değerler buna göre güncellenecektir.

### PDF belgelerindeki meta veri imzaları son kullanıcı tarafından görülebilir mi?

Meta veri imzaları belge içeriğinde görünmez. Ancak, Adobe Acrobat gibi PDF okuyucularındaki belge özellikleri panelinden veya meta verileri görüntülemek için özel araçlar kullanılarak görüntülenebilirler.

### PDF'lerdeki meta verileri şifreleyebilir veya koruyabilir miyim?

GroupDocs.Signature, şifreleme de dahil olmak üzere belgeleri güvence altına almak için seçenekler sunar. Meta verileri de dahil olmak üzere tüm PDF'yi korumak için belge düzeyinde şifreleme uygulayabilirsiniz.

### Bir PDF'e ekleyebileceğim meta veri miktarında bir sınır var mı?

PDF spesifikasyonunda katı bir sınırlama bulunmamakla birlikte, aşırı miktarda meta veri eklemek dosya boyutunu artırabilir. Meta verilere yalnızca ilgili ve gerekli bilgilerin eklenmesi önerilir.

### Meta veri ekledikten sonra bir PDF'in kurcalanıp kurcalanmadığını programatik olarak doğrulayabilir miyim?

Evet, GroupDocs.Signature, meta verilerdeki değişiklikler de dahil olmak üzere, bir belgenin imzalandıktan sonra değiştirilip değiştirilmediğini tespit etmeye yardımcı olabilecek doğrulama yetenekleri sağlar.

### Daha fazla kaynak ve desteği nerede bulabilirim?

- [API Referansı](https://reference.groupdocs.com/signature/net/)
- [İndirmeler](https://releases.groupdocs.com/signature/net/)
- [Örnekler](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
- [Belgeleme](https://docs.groupdocs.com/signature/net/)
- [Ürün Sayfası](https://products.groupdocs.com/signature/net/)
- [Blog](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
- [Destek Forumu](https://forum.groupdocs.com/c/signature/13)
- [Geçici Lisans](https://purchase.groupdocs.com/temporary-license/)