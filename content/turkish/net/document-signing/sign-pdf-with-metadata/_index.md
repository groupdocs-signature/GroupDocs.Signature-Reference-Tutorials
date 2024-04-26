---
title: PDF'yi Meta Verilerle İmzalayın
linktitle: PDF'yi Meta Verilerle İmzalayın
second_title: GroupDocs.Signature .NET API'si
description: GroupDocs.Signature for .NET'i kullanarak PDF belgelerini meta verilerle nasıl imzalayacağınızı öğrenin. Belge izlenebilirliğini ve orijinalliğini kolayca geliştirin.
type: docs
weight: 11
url: /tr/net/document-signing/sign-pdf-with-metadata/
---
## giriiş
Bu öğreticide, GroupDocs.Signature for .NET'i kullanarak meta veriler içeren bir PDF belgesinin nasıl imzalanacağını öğreneceğiz. PDF'ye meta veriler eklemek, belge hakkında yazarlık, oluşturulma tarihi, belge kimliği ve daha fazlası gibi ek bilgiler sağlayabilir.
## Önkoşullar
Başlamadan önce aşağıdakilere sahip olduğunuzdan emin olun:
1.  GroupDocs.Signature for .NET: Şu adresten indirebilirsiniz:[Burada](https://releases.groupdocs.com/signature/net/).
2. PDF Belgesi: İmzalamaya hazır örnek bir PDF dosyası hazırlayın.
3. Temel C# Programlama Bilgisi: Kod örneklerini anlamak için C# sözdizimine aşina olmak gerekir.
## Ad Alanlarını İçe Aktar
Öncelikle gerekli sınıflara ve yöntemlere erişmek için gerekli ad alanlarını içe aktardığınızdan emin olun:
```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## 1. Adım: PDF Belgesini Yükleyin
İmzalamak istediğiniz PDF belgesini yükleyin:
```csharp
string filePath = "sample.pdf";
```
## Adım 2: Çıktı Dosyası Yolunu Belirtin
İmzalı PDF'nin meta verilerle kaydedileceği çıktı dosyası yolunu tanımlayın:
```csharp
string outputFilePath = Path.Combine("Your Document Directory", "SignPdfWithMetadata", "SignedWithMetadata.pdf");
```
## 3. Adım: İmza Örneği Oluşturun
PDF belgesinin yolunu sağlayarak bir İmza örneğini başlatın:
```csharp
using (Signature signature = new Signature(filePath))
{
    // İmzayla ilgili kod buraya gelecek
}
```
## Adım 4: Meta Veri Seçeneklerini Tanımlayın
MetadataSignOptions oluşturun ve meta veri alanlarını ilgili değerleriyle ekleyin:
```csharp
MetadataSignOptions options = new MetadataSignOptions();
options
    .Add(new PdfMetadataSignature("Author", "Mr.Sherlock Holmes")) // Dize değeri
    .Add(new PdfMetadataSignature("CreatedOn", DateTime.Now))       // TarihSaat değerleri
    .Add(new PdfMetadataSignature("DocumentId", 123456))            // Tamsayı değeri
    .Add(new PdfMetadataSignature("SignatureId", 123.456D))         // Çift değer
    .Add(new PdfMetadataSignature("Amount", 123.456M))              // Ondalık değer
    .Add(new PdfMetadataSignature("Total", 123.456F));              // Kayan değer
```
## Adım 5: Belgeyi İmzalayın
PDF belgesini belirtilen meta veri seçenekleriyle imzalayın ve imzalanan belgeyi kaydedin:
```csharp
SignResult result = signature.Sign(outputFilePath, options);
Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).\nFile saved at {outputFilePath}.");
```

## Çözüm
Bu öğreticide, GroupDocs.Signature for .NET'i kullanarak meta veriler içeren bir PDF belgesinin nasıl imzalanacağını ele aldık. Adım adım kılavuzu izleyerek PDF dosyalarınıza yazarlık, oluşturulma tarihi ve daha fazlası gibi meta veri bilgilerini kolayca ekleyerek bunların kullanışlılığını ve izlenebilirliğini artırabilirsiniz.
## SSS'ler
### PDF belgelerime özel meta veri alanları ekleyebilir miyim?
Evet, GroupDocs.Signature for .NET'i kullanarak alan adını ve buna karşılık gelen değeri belirterek özel meta veri alanları ekleyebilirsiniz.
### GroupDocs.Signature for .NET, .NET Framework'ün tüm sürümleriyle uyumlu mu?
GroupDocs.Signature for .NET, .NET Framework'ün çeşitli sürümleriyle uyumlu olduğundan esneklik ve entegrasyon kolaylığı sağlar.
### GroupDocs.Signature, PDF dışında diğer belge formatlarının imzalanmasını destekliyor mu?
Evet, GroupDocs.Signature, aralarında Word, Excel, PowerPoint ve daha fazlasının da bulunduğu çok çeşitli belge formatlarını destekler.
### GroupDocs.Signature for .NET'i kullanarak birden fazla belgeyi toplu olarak imzalayabilir miyim?
Evet, bir dosya listesini yineleyerek ve imza sürecini programlı olarak uygulayarak birden çok belgeyi toplu olarak imzalayabilirsiniz.
### GroupDocs.Signature kullanıcıları için teknik destek mevcut mu?
 Evet, GroupDocs forumları aracılığıyla özel teknik destek sağlamaktadır. Destek forumuna erişebilirsiniz[Burada](https://forum.groupdocs.com/c/signature/13).