---
"description": "GroupDocs.Signature for .NET kullanarak görsellere meta verileri nasıl imzalayıp yerleştireceğinizi öğrenin. Görsel özgünlüğünü ve izlenebilirliğini artırmak için yazar bilgileri, zaman damgaları ve özel veriler ekleyin."
"linktitle": "Meta Verili İmza Resmi"
"second_title": "GroupDocs.Signature .NET API"
"title": "C# .NET'te Meta Verilerle Görüntüleri İmzalama"
"url": "/tr/net/document-signing/sign-image-with-metadata/"
"weight": 10
type: docs
---
## giriiş

Dijital görüntü imzalarının meta verilerle imzalanması, özgünlük, mülkiyet ve izlenebilirlik sağlamak için giderek daha önemli hale geliyor. GroupDocs.Signature for .NET, çeşitli görüntü formatlarına meta veri imzaları eklemek için güçlü ve kullanımı kolay bir çözüm sunar. Bu eğitim, C# kullanarak görüntüleri meta verilerle imzalama sürecinin tamamında size rehberlik eder.

Meta veri imzaları, yazar bilgileri, oluşturma zaman damgaları, benzersiz tanımlayıcılar ve daha fazlası gibi değerli bilgileri doğrudan görüntü dosyalarına yerleştirmenize olanak tanır. Bu bilgiler, görüntü dosyasının bir parçası haline gelerek, görüntü gerçekliğini izlemek ve doğrulamak için güvenilir bir yöntem sunar.

## Ön koşullar

Bu eğitime başlamadan önce aşağıdakilere sahip olduğunuzdan emin olun:

1. [.NET için GroupDocs.Signature](https://releases.groupdocs.com/signature/net/) - Kütüphaneyi indirin ve kurun
2. Geliştirme Ortamı - Visual Studio veya .NET desteği olan herhangi bir uyumlu IDE
3. Resim Dosyası - Desteklenen bir formatta (PNG, JPG, TIFF, vb.) örnek bir resim dosyası
4. Temel C# Programlama Bilgisi - C# programlama kavramlarına aşinalık

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

Kaynak görüntünüz için yolları ve imzalı çıktının nereye kaydedileceğini tanımlayın:

```csharp
// Kaynak görüntü dosyanızın yolunu belirtin
string filePath = "sample.png";

// İmzalanmış görüntü için çıktı dizinini ve dosya adını tanımlayın
string outputDirectory = "Your Document Directory";
string outputFilePath = Path.Combine(outputDirectory, "SignImageWithMetadata", "SignedWithMetadata.png");

// Çıktı dizininin mevcut olduğundan emin olun
Directory.CreateDirectory(Path.GetDirectoryName(outputFilePath));
```

## Adım 2: İmza Nesnesini Başlatın

Kaynak görüntü dosyanızla Signature sınıfının bir örneğini oluşturun:

```csharp
using (Signature signature = new Signature(filePath))
{
    // Kodun geri kalanı buraya gelecek
}
```

## Adım 3: Meta Veri İmzalarını Oluşturun ve Yapılandırın

Ardından, görüntüye yerleştirmek istediğiniz meta verileri tanımlayın. GroupDocs.Signature, meta veriler için çeşitli veri türlerini destekler:

```csharp
// Meta veri kimliğini başlat (görüntü biçimine özgü)
ushort imgsMetadataId = 41996;

// Meta veri seçenekleri nesnesi oluştur
MetadataSignOptions options = new MetadataSignOptions();

// Çeşitli meta veri imzası türleri ekleyin
options
    .Add(new ImageMetadataSignature(imgsMetadataId++, "Mr.Sherlock Holmes"))  // Dize değeri
    .Add(new ImageMetadataSignature(imgsMetadataId++, DateTime.Now))          // Tarih Saat değeri
    .Add(new ImageMetadataSignature(imgsMetadataId++, 123456))                // Tam sayı değeri
    .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456D))              // Çift değer
    .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456M))              // Ondalık değer
    .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456F));             // Kayan nokta değeri
```

## Adım 4: Görseli Meta Verilerle İmzalayın

Meta veri imzalarını görüntüye uygulayın ve sonucu kaydedin:

```csharp
// Belgeyi imzalayın ve çıktı dosyası yoluna kaydedin
SignResult result = signature.Sign(outputFilePath, options);

// Başarı mesajını görüntüle
Console.WriteLine($"\nSource image signed successfully with {result.Succeeded.Count} metadata signature(s).");
Console.WriteLine($"Signed image saved at: {outputFilePath}");
```

## Tam Örnek

İşte tüm adımları bir araya getiren tam kod örneği:

```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;

namespace SignImageWithMetadataExample
{
    class Program
    {
        static void Main(string[] args)
        {
            // Dosya yollarını belirtin
            string filePath = "sample.png";            
            string outputFilePath = Path.Combine("Your Document Directory", "SignImageWithMetadata", "SignedWithMetadata.png");
            
            // Çıktı dizininin mevcut olduğundan emin olun
            Directory.CreateDirectory(Path.GetDirectoryName(outputFilePath));

            // Resmi meta verilerle imzalayın
            using (Signature signature = new Signature(filePath))
            {
                // Meta veri kimliğini başlat (görüntü biçimine özgü)
                ushort imgsMetadataId = 41996;
                
                // Meta veri seçenekleri oluşturun
                MetadataSignOptions options = new MetadataSignOptions();
                
                // Farklı türde meta veri imzaları ekleyin
                options
                    .Add(new ImageMetadataSignature(imgsMetadataId++, "Mr.Sherlock Holmes")) // Dize değeri
                    .Add(new ImageMetadataSignature(imgsMetadataId++, DateTime.Now))          // Tarih Saat değeri
                    .Add(new ImageMetadataSignature(imgsMetadataId++, 123456))                // Tam sayı değeri
                    .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456D))              // Çift değer
                    .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456M))              // Ondalık değer
                    .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456F));             // Kayan nokta değeri
                
                // Belgeyi imzalayın ve dosyaya kaydedin
                SignResult result = signature.Sign(outputFilePath, options);
                
                // Sonuçları görüntüle
                Console.WriteLine($"\nSource image signed successfully with {result.Succeeded.Count} signature(s).");
                Console.WriteLine($"File saved at {outputFilePath}.");
            }
        }
    }
}
```

## Gelişmiş Meta Veri İmzalama Teknikleri

### Özel Meta Verilerle Çalışma

Ayrıca belirli kimliklere sahip özel meta veri alanları da oluşturabilirsiniz:

```csharp
// Belirli bir kimliğe sahip özel meta veriler oluşturun
options.Add(new ImageMetadataSignature(42000, "CustomValue"));
```

### Meta Veri İmzalarını Doğrulama

İmzalamanın ardından meta veri imzalarını doğrulamak isteyebilirsiniz:

```csharp
// Doğrulama seçenekleri oluşturun
MetadataSearchOptions searchOptions = new MetadataSearchOptions();

// Meta veri imzalarını arayın
SearchResult result = signature.Search(searchOptions);

// Bulunan imzaları görüntüle
Console.WriteLine($"Found {result.Signatures.Count} metadata signatures:");
foreach(var metadataSignature in result.Signatures)
{
    Console.WriteLine($"- {metadataSignature.Name}: {metadataSignature.Value}");
}
```

## Çözüm

Bu eğitimde, .NET için GroupDocs.Signature kullanarak görselleri meta verilerle nasıl imzalayacağınızı öğrendiniz. Görsellere meta veri eklemek, görsellerin özgünlüğünü artırmak, kritik bilgiler eklemek ve belge yönetimi iş akışlarını iyileştirmek için mükemmel bir yol sağlar. Bu süreç basit ve güçlüdür ve özel gereksinimlerinize göre özelleştirme olanağı sunar.

Görüntü dosyasına yerleştirilen meta veriler, telif hakkı koruması, görüntü kaynağını izleme, açıklayıcı bilgiler ekleme ve dijital gözetim zinciri oluşturma gibi çeşitli amaçlarla kullanılabilir. Meta veri imzalarını uygulayarak, görüntülerinizin yaşam döngüsü boyunca bütünlüğünü ve özgünlüğünü koruyabilirsiniz.

## SSS

### Mevcut imzalı görsellere meta veri ekleyebilir miyim?

Evet, meta veri imzaları içeren görsellere ek meta veri ekleyebilirsiniz. Mevcut meta veriler korunacak ve buna göre yeni meta veriler eklenecektir.

### Meta veri imzalama için hangi görüntü biçimleri destekleniyor?

GroupDocs.Signature for .NET, PNG, JPEG, TIFF, BMP, GIF ve daha fazlası dahil olmak üzere çeşitli görüntü biçimleri için meta veri imzalamayı destekler. Tam liste için bkz. [resmi belgeler](https://docs.groupdocs.com/signature/net/).

### Görsellerdeki meta verileri şifrelemek mümkün müdür?

Evet, GroupDocs.Signature, gelişmiş güvenlik için meta verileri şifreleme seçenekleri sunar. Hassas meta veri bilgilerini korumak için kütüphane tarafından sağlanan şifreleme seçeneklerini kullanabilirsiniz.

### İmzalı görsellerin gerçekliğini programatik olarak doğrulayabilir miyim?

Kesinlikle. Meta veri imzalarını doğrulamak ve imzalı görsellerin gerçekliğini teyit etmek için GroupDocs.Signature'daki doğrulama yöntemlerini kullanabilirsiniz.

### Görselleri meta verilerle imzalarken dosya boyutu sınırlaması var mı?

Kütüphanenin kendisi tarafından belirli bir dosya boyutu sınırlaması getirilmemiştir, ancak çok büyük dosyalar daha fazla işlem süresi ve bellek gerektirebilir. Çok büyük görsellerle çalışırken sistem kaynaklarını göz önünde bulundurmanız önerilir.

### Test amaçlı geçici lisansı nasıl alabilirim?

Bir tane edinebilirsiniz [geçici lisans](https://purchase.groupdocs.com/temporary-license/) Satın alma işlemi yapmadan önce GroupDocs.Signature'ı test etmek için.

### Daha fazla kaynak ve desteği nerede bulabilirim?

- [API Referansı](https://reference.groupdocs.com/signature/net/)
- [İndirmeler](https://releases.groupdocs.com/signature/net/)
- [Örnekler](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
- [Belgeleme](https://docs.groupdocs.com/signature/net/)
- [Ürün Sayfası](https://products.groupdocs.com/signature/net/)
- [Blog](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
- [Destek Forumu](https://forum.groupdocs.com/c/signature/13)