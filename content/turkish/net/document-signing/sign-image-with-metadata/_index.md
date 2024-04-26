---
title: Görüntüyü Meta Verilerle İmzala
linktitle: Görüntüyü Meta Verilerle İmzala
second_title: GroupDocs.Signature .NET API'si
description: GroupDocs.Signature kullanarak görüntüleri .NET'te meta verilerle nasıl imzalayacağınızı öğrenin. Kolay, verimli ve özelleştirilebilir meta veri imzalama çözümü.
type: docs
weight: 10
url: /tr/net/document-signing/sign-image-with-metadata/
---
## giriiş
GroupDocs.Signature for .NET, geliştiricilerin görüntüleri meta verilerle verimli bir şekilde imzalamasına olanak tanır. Bu eğitim, süreç boyunca size adım adım yol gösterir.
## Önkoşullar
Başlamadan önce aşağıdakilere sahip olduğunuzdan emin olun:
1. .NET için GroupDocs.Signature: .NET projenize GroupDocs.Signature paketini yükleyin. Şuradan indirebilirsiniz[Burada](https://releases.groupdocs.com/signature/net/).   
2. İmaj Dosyası: Meta verilerle imzalamak istediğiniz resim dosyasını hazırlayın.

## Ad Alanlarını İçe Aktar
Gerekli ad alanlarını C# kodunuza aktardığınızdan emin olun:
```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## 1. Adım: Görüntü Dosyasını Yükleyin
İlk olarak, görüntü dosyanızın yolunu ve imzalı görüntünün çıktı dizinini meta verilerle birlikte belirtin:
```csharp
string filePath = "sample.png";            
string outputFilePath = Path.Combine("Your Document Directory", "SignImageWithMetadata", "SignedWithMetadata.png");
```
## 2. Adım: Meta Veri İmzaları Oluşturun
Daha sonra farklı meta veri imzaları oluşturun ve bunları seçenekler imza koleksiyonuna ekleyin:
```csharp
using (Signature signature = new Signature(filePath))
{
    ushort imgsMetadataId = 41996;
    MetadataSignOptions options = new MetadataSignOptions();
    options
        .Add(new ImageMetadataSignature(imgsMetadataId++, "Mr.Scherlock Holmes")) // Dize değeri
        .Add(new ImageMetadataSignature(imgsMetadataId++, DateTime.Now))          // Tarih Saat değeri
        .Add(new ImageMetadataSignature(imgsMetadataId++, 123456))                // Tamsayı değeri
        .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456D))              // Çift değer
        .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456M))              // Ondalık değer
        .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456F));             // Kayan değer
    
    // belgeyi dosyaya imzala
    SignResult result = signature.Sign(outputFilePath, options);
    Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).\nFile saved at {outputFilePath}.");
}
```

## Çözüm
Bu öğreticide, GroupDocs.Signature for .NET'i kullanarak meta verilerle bir görüntüyü nasıl imzalayacağınızı öğrendiniz. Bu adımları izleyerek meta veri imzalarını .NET uygulamalarınıza kolayca dahil edebilirsiniz.

## SSS'ler
### GroupDocs.Signature for .NET'i kullanarak birden fazla görüntüyü meta verilerle imzalayabilir miyim?
Evet, her görüntü dosyasını yineleyerek ve meta veri imzalarını uygulayarak birden fazla görüntüyü meta verilerle imzalayabilirsiniz.
### GroupDocs.Signature for .NET'in deneme sürümü mevcut mu?
 Evet, deneme sürümünü şuradan indirebilirsiniz:[Burada](https://releases.groupdocs.com/).
### GroupDocs.Signature for .NET, görsellerin yanı sıra diğer dosya formatlarını da destekliyor mu?
Evet, GroupDocs.Signature, PDF, Word, Excel ve daha fazlası dahil olmak üzere çeşitli dosya formatlarını destekler.
### Meta veri imzasının görünümünü özelleştirebilir miyim?
Evet, meta veri imzasının yazı tipi boyutu, rengi ve konumu gibi görünümünü özelleştirebilirsiniz.
### .NET için GroupDocs.Signature desteğini nereden alabilirim?
 GroupDocs.Signature forumundan destek alabilirsiniz[Burada](https://forum.groupdocs.com/c/signature/13).