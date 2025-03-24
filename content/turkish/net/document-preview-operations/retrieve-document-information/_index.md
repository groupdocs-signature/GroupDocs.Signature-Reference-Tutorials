---
title: Belge Bilgilerini Al
linktitle: Belge Bilgilerini Al
second_title: GroupDocs.Signature .NET API'si
description: GroupDocs.Signature ile .NET'te belge yönetimini geliştirin. Belge bilgilerini adım adım alın. Çeşitli formatları destekler.
weight: 11
url: /tr/net/document-preview-operations/retrieve-document-information/
---
## giriiş
Dijital dokümantasyon alanında özgünlüğün ve bütünlüğün sağlanması çok önemlidir. GroupDocs.Signature for .NET, .NET ortamında belge imzalarını yönetmek için sağlam bir çözüm sağlar. Bu öğreticide, GroupDocs.Signature for .NET'i kullanarak belge bilgilerini alma sürecini ayrıntılı olarak ele alıyoruz ve kapsamlı bir anlayış için her adımı parçalara ayırıyoruz.
## Önkoşullar
Eğiticiye dalmadan önce aşağıdaki önkoşulların mevcut olduğundan emin olun:
1.  Kurulum: GroupDocs.Signature for .NET'i şuradan indirerek yükleyin:[Burada](https://releases.groupdocs.com/signature/net/).
2. .NET Ortamı: .NET çerçevesi hakkında çalışma bilgisine sahip olun.
3. Belge: Test amacıyla örnek bir belge hazırlayın (örneğin, "sample_multiple_signatures.docx").

## Ad Alanlarını İçe Aktarma
Belge imzası alma işlemine devam etmeden önce gerekli ad alanlarını içe aktarın:
```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
```

## Adım 1: Belge Dosya Yolunu Ayarlayın:
Bilgi almak istediğiniz belgenin dosya yolunu tanımlayın.
```csharp
string filePath = "sample_multiple_signatures.docx";
```
## Adım 2: İmza Nesnesini Örneklendirin:
 Bir örneğini oluşturun`Signature` belge dosya yolunu ileterek sınıf.
```csharp
using (Signature signature = new Signature(filePath))
{

}
```
## Adım 3: Belge Bilgilerini Alın:
 Kullanın`GetDocumentInfo()` Belge hakkında kapsamlı bilgi alma yöntemi.
```csharp
IDocumentInfo documentInfo = signature.GetDocumentInfo();
```
## Adım 4: Belge Özelliklerini Görüntüleyin:
Belgenin format, uzantı, boyut, sayfa sayısı vb. gibi çeşitli özelliklerinin çıktısını alın.
```csharp
Console.WriteLine($"Document properties {Path.GetFileName(filePath)}:");
Console.WriteLine($" - format : {documentInfo.FileType.FileFormat}");
Console.WriteLine($" - extension : {documentInfo.FileType.Extension}");
Console.WriteLine($" - size : {documentInfo.Size}");
Console.WriteLine($" - page count : {documentInfo.PageCount}");
Console.WriteLine($" - Form Fields count : {documentInfo.FormFields.Count}");
Console.WriteLine($" - Text signatures count : {documentInfo.TextSignatures.Count}");
Console.WriteLine($" - Image signatures count : {documentInfo.ImageSignatures.Count}");
Console.WriteLine($" - Digital signatures count : {documentInfo.DigitalSignatures.Count}");
Console.WriteLine($" - Barcode signatures count : {documentInfo.BarcodeSignatures.Count}");
Console.WriteLine($" - QrCode signatures count : {documentInfo.QrCodeSignatures.Count}");
Console.WriteLine($" - FormField signatures count : {documentInfo.FormFieldSignatures.Count}");
foreach (PageInfo pageInfo in documentInfo.Pages)
{
   Console.WriteLine($" - page-{pageInfo.PageNumber} Width {pageInfo.Width}, Height {pageInfo.Height}");
}
```


## Çözüm
GroupDocs.Signature for .NET, belge imzalarını .NET çerçevesinde sorunsuz bir şekilde yönetmek için güçlü bir araç paketi sunar. Bu kılavuzda özetlenen adımları izleyerek, belgelerinizle ilgili kapsamlı bilgileri verimli bir şekilde alabilir ve gelişmiş belge yönetimi özelliklerini kolaylaştırabilirsiniz.

## SSS'ler
### GroupDocs.Signature for .NET birden çok belge biçimini işleyebilir mi?
Evet, GroupDocs.Signature, DOCX, PDF, PNG ve JPEG dahil ancak bunlarla sınırlı olmamak üzere çok çeşitli belge formatlarını destekler.
### GroupDocs.Signature for .NET'in deneme sürümü mevcut mu?
 Evet, deneme sürümüne şuradan ulaşabilirsiniz:[Burada](https://releases.groupdocs.com/).
### GroupDocs.Signature for .NET dijital imzalar için destek sağlıyor mu?
GroupDocs.Signature kesinlikle dijital imzalar için güçlü bir destek sunarak belgenin orijinalliğini ve bütünlüğünü garanti eder.
### GroupDocs.Signature for .NET için ek belgeleri ve desteği nerede bulabilirim?
 Kapsamlı belgelere başvurabilirsiniz[Burada](https://tutorials.groupdocs.com/signature/net/) ve destek için GroupDocs forumunu ziyaret edin[Burada](https://forum.groupdocs.com/c/signature/13).
### GroupDocs.Signature for .NET için geçici lisanslar alınabilir mi?
 Evet, geçici lisanslar satın alınabilir[Burada](https://purchase.groupdocs.com/temporary-license/).