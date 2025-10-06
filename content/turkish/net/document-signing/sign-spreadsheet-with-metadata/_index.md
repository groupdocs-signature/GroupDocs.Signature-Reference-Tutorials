---
"description": "GroupDocs.Signature for .NET kullanarak meta veri imzalarını yerleştirerek Excel elektronik tablolarınızı koruyun ve geliştirin. Belge izlenebilirliğini ve özgünlüğünü artırmak için yazar bilgileri, zaman damgaları ve özel veriler ekleyin."
"linktitle": "Meta Verili İmza Elektronik Tablosu"
"second_title": "GroupDocs.Signature .NET API"
"title": "C# .NET'te Excel Elektronik Tablolarına Meta Veri İmzaları Ekleme"
"url": "/tr/net/document-signing/sign-spreadsheet-with-metadata/"
"weight": 13
type: docs
---
## giriiş

Excel elektronik tabloları genellikle kritik iş verileri, finansal bilgiler ve önemli hesaplamalar içerir. Bunların gerçekliğini sağlamak, kaynaklarını takip etmek ve bütünlüklerini korumak birçok profesyonel ortamda hayati önem taşır. Elektronik tablo güvenliğini ve izlenebilirliğini artırmanın etkili bir yolu, meta veri imzaları yerleştirmektir.

Bu kapsamlı eğitim, .NET için GroupDocs.Signature kullanarak Excel elektronik tablolarını meta verilerle imzalama sürecinde size rehberlik edecektir. Meta veri imzaları ekleyerek, yazar bilgileri, oluşturma zaman damgaları, belge tanımlayıcıları ve diğer özel özellikler gibi değerli bilgileri doğrudan elektronik tablo dosya yapısına yerleştirebilirsiniz.

## Ön koşullar

Bu eğitime başlamadan önce aşağıdakilere sahip olduğunuzdan emin olun:

1. [.NET için GroupDocs.Signature](https://releases.groupdocs.com/signature/net/) - Kütüphaneyi indirin ve kurun
2. Geliştirme Ortamı - Visual Studio veya herhangi bir .NET uyumlu IDE
3. Excel Elektronik Tablosu - Örnek bir elektronik tablo dosyası (XLSX, XLS, vb.)
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

Kaynak elektronik tablonuz için yolları ve imzalı çıktının nereye kaydedileceğini tanımlayın:

```csharp
// Excel dosyanızın yolunu belirtin
string filePath = "sample.xlsx";

// İmzalanmış elektronik tablonun çıktı dizinini ve dosya adını tanımlayın
string outputDirectory = "Your Document Directory";
string outputFilePath = Path.Combine(outputDirectory, "SignSpreadsheetWithMetadata", "SignedWithMetadata.xlsx");

// Çıktı dizininin mevcut olduğundan emin olun
Directory.CreateDirectory(Path.GetDirectoryName(outputFilePath));
```

## Adım 2: İmza Nesnesini Başlatın

Kaynak elektronik tablo dosyanızla Signature sınıfının bir örneğini oluşturun:

```csharp
using (Signature signature = new Signature(filePath))
{
    // Kodun geri kalanı buraya gelecek
}
```

## Adım 3: Meta Veri İmzalarını Oluşturun ve Yapılandırın

Ardından meta veri seçeneklerini tanımlayın ve bir dizi elektronik tablo meta veri imzası oluşturun:

```csharp
// Meta veri seçenekleri nesnesi oluştur
MetadataSignOptions options = new MetadataSignOptions();

// Farklı veri türlerine sahip bir dizi elektronik tablo meta veri imzası oluşturun
SpreadsheetMetadataSignature[] signatures = new SpreadsheetMetadataSignature[]
{
    new SpreadsheetMetadataSignature("Author", "Mr.Sherlock Holmes"), // Dize değeri
    new SpreadsheetMetadataSignature("CreatedOn", DateTime.Now),      // DateTime değeri
    new SpreadsheetMetadataSignature("DocumentId", 123456),           // Tam sayı değeri
    new SpreadsheetMetadataSignature("SignatureId", 123.456D),        // Çift değer
    new SpreadsheetMetadataSignature("Amount", 123.456M),             // Ondalık değer
    new SpreadsheetMetadataSignature("Total", 123.456F)               // Kayan nokta değeri
};

// İmza koleksiyonunu seçeneklere ekle
options.Signatures.AddRange(signatures);
```

## Adım 4: E-Tabloyu Meta Verilerle İmzalayın

Meta veri imzalarını elektronik tabloya uygulayın ve sonucu kaydedin:

```csharp
// Belgeyi imzalayın ve çıktı dosyası yoluna kaydedin
SignResult result = signature.Sign(outputFilePath, options);

// Başarı mesajını görüntüle
Console.WriteLine($"\nSource spreadsheet signed successfully with {result.Succeeded.Count} metadata signature(s).");
Console.WriteLine($"Signed spreadsheet saved at: {outputFilePath}");
```

## Tam Örnek

İşte tüm adımları bir araya getiren tam kod örneği:

```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;

namespace SignSpreadsheetWithMetadataExample
{
    class Program
    {
        static void Main(string[] args)
        {
            // Dosya yollarını belirtin
            string filePath = "sample.xlsx";
            string outputFilePath = Path.Combine("Your Document Directory", "SignSpreadsheetWithMetadata", "SignedWithMetadata.xlsx");
            
            // Çıktı dizininin mevcut olduğundan emin olun
            Directory.CreateDirectory(Path.GetDirectoryName(outputFilePath));

            // E-tabloyu meta verilerle imzalayın
            using (Signature signature = new Signature(filePath))
            {
                // Meta veri seçenekleri nesnesi oluştur
                MetadataSignOptions options = new MetadataSignOptions();
                
                // Farklı veri türlerine sahip bir dizi elektronik tablo meta veri imzası oluşturun
                SpreadsheetMetadataSignature[] signatures = new SpreadsheetMetadataSignature[]
                {
                    new SpreadsheetMetadataSignature("Author", "Mr.Sherlock Holmes"), // Dize değeri
                    new SpreadsheetMetadataSignature("CreatedOn", DateTime.Now),      // DateTime değeri
                    new SpreadsheetMetadataSignature("DocumentId", 123456),           // Tam sayı değeri
                    new SpreadsheetMetadataSignature("SignatureId", 123.456D),        // Çift değer
                    new SpreadsheetMetadataSignature("Amount", 123.456M),             // Ondalık değer
                    new SpreadsheetMetadataSignature("Total", 123.456F)               // Kayan nokta değeri
                };
                
                // İmza koleksiyonunu seçeneklere ekle
                options.Signatures.AddRange(signatures);
                
                // Belgeyi imzalayın ve dosyaya kaydedin
                SignResult result = signature.Sign(outputFilePath, options);
                
                // Sonuçları görüntüle
                Console.WriteLine($"\nSource spreadsheet signed successfully with {result.Succeeded.Count} signature(s).");
                Console.WriteLine($"File saved at {outputFilePath}.");
            }
        }
    }
}
```

## Gelişmiş Elektronik Tablo Meta Veri Teknikleri

### Özel ve Yerleşik Elektronik Tablo Özellikleriyle Çalışma

Excel elektronik tablolarının, dosya özellikleri iletişim kutusu aracılığıyla erişilebilen hem yerleşik hem de özel özellikleri vardır. GroupDocs.Signature, her ikisiyle de çalışmanıza olanak tanır:

```csharp
// Yerleşik özellikler ekleyin
signatures = new SpreadsheetMetadataSignature[]
{
    new SpreadsheetMetadataSignature("Company", "Sherlock Holmes Consulting"),
    new SpreadsheetMetadataSignature("Category", "Financial"),
    new SpreadsheetMetadataSignature("Keywords", "budget,forecast,analysis"),
    new SpreadsheetMetadataSignature("Comments", "This spreadsheet contains confidential information"),
    new SpreadsheetMetadataSignature("Manager", "John Watson")
};
options.Signatures.AddRange(signatures);

// Özel özellikler ekleyin
options.Signatures.Add(new SpreadsheetMetadataSignature("Department", "Finance"));
options.Signatures.Add(new SpreadsheetMetadataSignature("SecurityLevel", "Confidential"));
```

### İmzalı Elektronik Tablolarda Meta Veri Arama

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

### Mevcut Meta Verileri Güncelleme

Aynı özellik adlarını kullanarak elektronik tablolardaki mevcut meta verileri güncelleyebilirsiniz:

```csharp
// Mevcut meta verileri güncelle
options.Signatures.Add(new SpreadsheetMetadataSignature("Author", "Updated Author Name"));
```

## Çözüm

Bu kapsamlı eğitimde, .NET için GroupDocs.Signature kullanarak Excel elektronik tablolarını meta verilerle nasıl imzalayacağınızı öğrendiniz. Meta verilerin elektronik tablo dosyalarına yerleştirilmesi, belge izlenebilirliğini artırır, değerli bir bağlam sağlar ve özgünlüğün sağlanmasına yardımcı olur.

Elektronik tablolardaki meta veri imzaları, belge kaynağının, yazarın ve sürüm takibinin önemli olduğu iş ortamlarında özellikle kullanışlıdır. Gömülü meta veriler, yazar, oluşturma zamanı, belge tanımlayıcıları ve kuruluşunuzun ihtiyaçlarına uygun özel özellikler hakkında bilgiler içerebilir.

GroupDocs.Signature ile meta veri imzalarını uygulayarak Excel elektronik tablolarınızın bütünlüğünü korumasını ve yaşam döngüsü boyunca doğrulanabilir bilgiler sağlamasını sağlayabilirsiniz.

## SSS

### Zaten bazı özellikleri tanımlanmış olan elektronik tablolara meta veri ekleyebilir miyim?

Evet, elektronik tablolara yeni meta veriler ekleyebilir veya mevcut meta verileri güncelleyebilirsiniz. GroupDocs.Signature, yeni özellikler ekleyerek veya mevcut olanları aynı adlarla güncelleyerek entegrasyonu gerçekleştirecektir.

### Meta veri imzalama için hangi elektronik tablo biçimleri destekleniyor?

GroupDocs.Signature for .NET, XLSX, XLS, XLSM, ODS ve daha fazlası dahil olmak üzere çeşitli elektronik tablo biçimleri için meta veri imzalamayı destekler. Tam liste için bkz. [resmi belgeler](https://docs.groupdocs.com/signature/net/).

### E-tablolardaki meta veri imzaları kullanıcılar tarafından görülebilir mi?

Meta veri imzaları elektronik tablo içeriğinde görünmez. Ancak, Excel veya diğer uyumlu uygulamalardaki belge özellikleri panelinden görüntülenebilirler.

### Meta veri ekledikten sonra bir elektronik tablonun değiştirilip değiştirilmediğini programatik olarak doğrulayabilir miyim?

Evet, GroupDocs.Signature, meta verilerdeki değişiklikler de dahil olmak üzere, bir belgenin imzalandıktan sonra değiştirilip değiştirilmediğini tespit etmeye yardımcı olabilecek doğrulama yetenekleri sağlar.

### Meta veri eklemek elektronik tablo işlevselliğini etkiler mi?

Meta veri eklemenin dosya boyutu üzerinde minimum etkisi vardır ve elektronik tablo işlevselliği üzerinde hiçbir etkisi yoktur. Bu, hesaplamaları, formülleri veya diğer Excel özelliklerini etkilemeden belge özelliklerini geliştirmenin kolay bir yoludur.

### Daha fazla kaynak ve desteği nerede bulabilirim?

- [API Referansı](https://reference.groupdocs.com/signature/net/)
- [İndirmeler](https://releases.groupdocs.com/signature/net/)
- [Örnekler](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
- [Belgeleme](https://docs.groupdocs.com/signature/net/)
- [Ürün Sayfası](https://products.groupdocs.com/signature/net/)
- [Blog](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
- [Destek Forumu](https://forum.groupdocs.com/c/signature/13)
- [Geçici Lisans](https://purchase.groupdocs.com/temporary-license/)