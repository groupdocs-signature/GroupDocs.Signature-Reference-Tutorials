---
title: GroupDocs.Signature Kullanarak Belgeleri QR Koduyla İmzalama
linktitle: QR Kod ile İmzalama
second_title: GroupDocs.Signature .NET API'si
description: GroupDocs.Signature for .NET ile belgelerinize QR kodu imzalarını nasıl ekleyeceğinizi öğrenin. Güvenliği ve kimlik doğrulamayı zahmetsizce geliştirin.
type: docs
weight: 15
url: /tr/net/advanced-signature-techniques/sign-with-qr-code/
---
## giriiş
Bu öğreticide, GroupDocs.Signature for .NET'i kullanarak belgeleri QR koduyla imzalama sürecini anlatacağız. GroupDocs.Signature for .NET, geliştiricilerin dijital belgelere program aracılığıyla çeşitli imza türleri eklemesine olanak tanıyan güçlü bir API'dir. Belgeleri QR kodlarıyla imzalamak, belgelerinize ek bir güvenlik ve kimlik doğrulama katmanı sağlayabilir.
## Önkoşullar
Başlamadan önce aşağıdaki önkoşulların kurulu olduğundan emin olun:
1.  GroupDocs.Signature for .NET: Kitaplığı şu adresten indirebilirsiniz:[İnternet sitesi](https://releases.groupdocs.com/signature/net/).
2. Geliştirme Ortamı: Makinenizde bir .NET geliştirme ortamının kurulu olduğundan emin olun.
3. Örnek Belge: QR koduyla imzalamak istediğiniz örnek belgeyi (örn. PDF) hazırlayın.

## Gerekli Ad Alanlarını İçe Aktarma
Koda dalmadan önce gerekli ad alanlarını içe aktaralım:
```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

## 1. Adım: Dosya Yollarını Tanımlayın
```csharp
string filePath = "sample.pdf";
string fileName = Path.GetFileName(filePath);
string outputFilePath = Path.Combine("Your Document Directory", "SignWithQRCode", fileName);
```
 Değiştirildiğinden emin olun`"Your Document Directory"` imzalı belgeyi kaydetmek istediğiniz dizinin yolu ile birlikte.
## Adım 2: İmza Nesnesini Başlatın
```csharp
using (Signature signature = new Signature(filePath))
{
    //İmzalama kodu buraya gelecek
}
```
 Bir başlat`Signature` İmzalamak istediğiniz belgenin yolunu içeren nesne.
## 3. Adım: QRCodeSignOptions'ı oluşturun
```csharp
QrCodeSignOptions options = new QrCodeSignOptions("JohnSmith")
{
    EncodeType = QrCodeTypes.QR,
    Left = 50,
    Top = 150,
    Width = 200,
    Height = 200
};
```
 Oluşturmak`QrCodeSignOptions` QR kod imzası için istenen ayarlara sahip nesneyi seçin. Kodlanacak metin, QR kodunun konumu ve boyutları gibi parametreleri özelleştirebilirsiniz.
## 4. Adım: Belgeyi İmzalayın
```csharp
SignResult result = signature.Sign(outputFilePath, options);
```
 Kullan`Sign` yöntemi`Signature` Belgeyi belirtilen seçeneklerle imzalamak için nesne. Bu yöntem bir döndürür`SignResult` İmzalama işlemiyle ilgili bilgileri içeren nesne.
## Adım 5: Sonucu Görüntüleyin
```csharp
Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).\nFile saved at {outputFilePath}.");
```
İmzalama işleminin başarısını ve imzalanan belgenin kaydedildiği konumu belirten bir mesaj görüntüler.

## Çözüm
Bu öğreticide, GroupDocs.Signature for .NET'i kullanarak belgeleri QR koduyla nasıl imzalayacağımızı öğrendik. Bu basit adımları izleyerek dijital belgelerinize QR kodu imzaları ekleyerek güvenliği ve kimlik doğrulamayı artırabilirsiniz.

## SSS'ler
### QR kodunun görünümünü özelleştirebilir miyim?
Evet, QR kodunun boyutu, konumu ve kodlama türü gibi çeşitli parametreleri gereksinimlerinize göre özelleştirebilirsiniz.
### QR kodlarıyla imzalama için hangi belge biçimleri desteklenir?
GroupDocs.Signature for .NET, PDF, Word, Excel, PowerPoint ve daha fazlasını içeren çok çeşitli belge formatlarını destekler.
### Toplu işlemde birden fazla belgeyi imzalamak mümkün mü?
Kesinlikle, birden fazla belgeyi aynı anda imzalamak ve iş akışınızı kolaylaştırmak için GroupDocs.Signature for .NET'i kullanabilirsiniz.
### QR koduyla imzalanmış bir belgenin orijinalliğini doğrulayabilir miyim?
Evet, GroupDocs.Signature for .NET, imzalanan belgelerin bütünlüğünü ve orijinalliğini sağlamak için doğrulama mekanizmaları sağlar.
### Satın almadan önce işlevselliği test etmek için deneme sürümü mevcut mu?
 Evet, ücretsiz deneme sürümünü şuradan indirebilirsiniz:[İnternet sitesi](https://releases.groupdocs.com/) GroupDocs.Signature for .NET'in özelliklerini ve yeteneklerini değerlendirmek.