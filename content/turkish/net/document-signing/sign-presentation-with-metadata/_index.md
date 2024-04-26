---
title: Sunumu Meta Verilerle İmzalayın
linktitle: Sunumu Meta Verilerle İmzalayın
second_title: GroupDocs.Signature .NET API'si
description: GroupDocs.Signature for .NET'i kullanarak sunum dosyalarını meta verilerle nasıl imzalayacağınızı öğrenin. Belge bütünlüğünü geliştirin ve değerli bilgiler ekleyin.
type: docs
weight: 12
url: /tr/net/document-signing/sign-presentation-with-metadata/
---
## giriiş
Bu öğreticide, GroupDocs.Signature for .NET kitaplığını kullanarak meta veriler içeren bir sunum dosyasının (PPTX) nasıl imzalanacağını öğreneceğiz. Sunumların meta verilerle imzalanması, belgeye yazarın adı, oluşturulma tarihi, belge kimliği, imza kimliği ve çeşitli sayısal değerler gibi değerli bilgiler ekler.
## Önkoşullar
Başlamadan önce aşağıdakilere sahip olduğunuzdan emin olun:
1.  GroupDocs.Signature for .NET Kitaplığı: Kitaplığı şu adresten indirip yükleyin:[Burada](https://releases.groupdocs.com/signature/net/).
2. Geliştirme Ortamı: Bir .NET geliştirme ortamı kurduğunuzdan emin olun.
3. Sunum Dosyası: Örnek bir sunum dosyasını (PPTX formatında) imzaya hazır bulundurun.
4. Temel C# Anlayışı: C# programlama diline aşina olmak faydalı olacaktır.

## Ad Alanlarını İçe Aktar
Koda dalmadan önce gerekli ad alanlarını içe aktaralım:
```csharp
using System;
using System.IO;
    using GroupDocs.Signature;
    using GroupDocs.Signature.Domain;
    using GroupDocs.Signature.Options;
```
## Adım 1: Sunum Dosyasını Yükleyin
```csharp
string filePath = "sample.pptx";
```
 Yer değiştirmek`"sample.pptx"` sunum dosyanızın yolu ile birlikte.
## Adım 2: Çıktı Dosyası Yolunu Belirtin
```csharp
string outputFilePath = Path.Combine("Your Document Directory", "SignPresentationWithMetadata", "SignedWithMetadata.pptx");
```
İmzalı sunum dosyasını dosya adıyla birlikte kaydetmek istediğiniz dizini belirtin.
## 3. Adım: İmza Nesnesini Başlatın
```csharp
using (Signature signature = new Signature(filePath))
```
Sunum dosyasının yolunu sağlayarak bir İmza nesnesini başlatın.
## 4. Adım: Meta Veri İmzalama Seçeneklerini Tanımlayın
```csharp
MetadataSignOptions options = new MetadataSignOptions();
```
Meta veri imzalama seçeneklerini tanımlamak için bir MetadataSignOptions örneği oluşturun.
## Adım 5: Meta Veri İmzaları Oluşturun
```csharp
PresentationMetadataSignature[] signatures = new PresentationMetadataSignature[]
{
    new PresentationMetadataSignature("Author", "Mr.Scherlock Holmes"),
    new PresentationMetadataSignature("CreatedOn", DateTime.Now),
    new PresentationMetadataSignature("DocumentId", 123456),
    new PresentationMetadataSignature("SignatureId", 123.456D),
    new PresentationMetadataSignature("Amount", 123.456M),
    new PresentationMetadataSignature("Total", 123.456F)
};
```
Her biri bir meta veri imzasını temsil eden bir dizi SunumMetadataSignature nesnesi oluşturun. Dize, DateTime, tamsayı, double, ondalık ve kayan nokta dahil olmak üzere çeşitli meta veri türleri ekleyebilirsiniz.
## Adım 6: Seçeneklere İmza Ekleme
```csharp
options.Signatures.AddRange(signatures);
```
Oluşturulan meta veri imzalarını MetadataSignOptions nesnesine ekleyin.
## Adım 7: Belgeyi İmzalayın
```csharp
SignResult result = signature.Sign(outputFilePath, options);
```
Belirtilen seçenekleri kullanarak sunum dosyasını meta verilerle imzalayın ve imzalanan dosyayı çıkış yoluna kaydedin.
## Adım 8: Sonucu Görüntüleyin
```csharp
Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).\nFile saved at {outputFilePath}.");
```
Uygulanan imza sayısı ve imzalı dosyanın kaydedildiği yol ile birlikte bir başarı mesajı görüntüleyin.

## Çözüm
Bu öğreticide, GroupDocs.Signature for .NET kitaplığını kullanarak meta veriler içeren bir sunum dosyasının nasıl imzalanacağını öğrendik. Meta veri imzalarının eklenmesi belgenin bütünlüğünü artırır ve içeriği hakkında değerli bilgiler sağlar.

## SSS'ler
### GroupDocs.Signature for .NET'i kullanarak PPTX dışındaki diğer belge formatlarını meta verilerle imzalayabilir miyim?
Evet, GroupDocs.Signature, meta verilerle imzalamak için Word, Excel, PDF ve daha fazlası dahil olmak üzere çeşitli belge formatlarını destekler.
### GroupDocs.Signature for .NET, .NET Core ile uyumlu mu?
Evet, kitaplık hem .NET Framework hem de .NET Core ile uyumludur.
### Meta veri imzalarının görünümünü özelleştirebilir miyim?
Evet, meta veri imzalarının görünümünü, konumunu ve diğer özelliklerini gereksinimlerinize göre özelleştirebilirsiniz.
### GroupDocs.Signature for .NET imzalı belgeler için şifreleme sağlıyor mu?
Evet, GroupDocs.Signature imzalı belgeleri yetkisiz erişime karşı korumak için şifreleme seçenekleri sunar.
### Satın almadan önce test edebileceğiniz bir deneme sürümü var mı?
 Evet, GroupDocs.Signature for .NET'in ücretsiz deneme sürümünden şu adresten yararlanabilirsiniz:[Burada](https://releases.groupdocs.com/).