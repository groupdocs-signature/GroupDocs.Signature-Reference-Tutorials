---
title: .NET için GroupDocs.Signature kullanarak Metin ile İmzalama
linktitle: Metinle İmzalama
second_title: GroupDocs.Signature .NET API'si
description: GroupDocs.Signature for .NET'i kullanarak belgeleri metinle nasıl imzalayacağınızı öğrenin. Program aracılığıyla metin imzaları eklemek için adım adım kılavuz.
weight: 17
url: /tr/net/advanced-signature-techniques/sign-with-text/
---
## giriiş
Dijital çağda, belgeleri elektronik olarak imzalamak standart bir uygulama haline gelerek zamandan ve kaynaklardan tasarruf sağlar. GroupDocs.Signature for .NET, program aracılığıyla çeşitli belge formatlarına metin imzaları eklemek için kapsamlı bir çözüm sunar. Bu öğreticide, GroupDocs.Signature for .NET'i kullanarak metin içeren bir belgeyi imzalama sürecinde size yol göstereceğiz.
## Önkoşullar
Eğiticiye dalmadan önce aşağıdaki önkoşullara sahip olduğunuzdan emin olun:
1.  GroupDocs.Signature for .NET: GroupDocs.Signature for .NET kitaplığının yüklü olduğundan emin olun. Şuradan indirebilirsiniz[Burada](https://releases.groupdocs.com/signature/net/).
2. Geliştirme Ortamı: .NET geliştirme için ayarlanmış bir çalışma ortamına sahip olun.
3. Belge: Metinle imzalamak istediğiniz belgeyi (örn. PDF, Word) hazırlayın.

## Ad Alanlarını İçe Aktar
GroupDocs.Signature işlevlerini kullanmak için öncelikle gerekli ad alanlarını .NET projenize aktarmanız gerekir.
```csharp
using System;
using System.IO;
using System.Drawing;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

Metin içeren bir belgeyi imzalama sürecini birden çok adıma ayıralım:
## 1. Adım: Belgeyi Yükleyin
İmzalamak istediğiniz belgeyi metinle yükleyin.
```csharp
string filePath = "sample.pdf"; // Belgenin yolu
string fileName = Path.GetFileName(filePath);
```
## Adım 2: Çıktı Dosyası Yolunu Ayarlayın
İmzalanan belgenin kaydedileceği çıktı dosyası yolunu tanımlayın.
```csharp
string outputFilePath = Path.Combine("Your Document Directory", "SignWithText", fileName);
```
## 3. Adım: İmza Seçenekleri Oluşturun
Metin içeriği, konum, boyut, renk ve yazı tipi dahil olmak üzere metin imzası seçeneklerini ayarlayın.
```csharp
TextSignOptions options = new TextSignOptions("John Smith")
{
    Left = 50, // İmza konumunu ayarla
    Top = 200,
    Width = 100, // İmza dikdörtgenini ayarla
    Height = 30,
    ForeColor = Color.Red, // Metin rengini ayarla
    Font = new SignatureFont { Size = 14, FamilyName = "Comic Sans MS" } // Yazı tipini ayarla
};
```
## Adım 4: Belgeyi İmzalayın
Belgeyi belirtilen seçeneklerle imzalamak ve imzalanan belgeyi çıktı dosyası yoluna kaydetmek için GroupDocs.Signature'ı kullanın.
```csharp
using (Signature signature = new Signature(filePath))
{
    SignResult result = signature.Sign(outputFilePath, options); // Belgeyi imzala
    Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).\nFile saved at {outputFilePath}.");
}
```

## Çözüm
Bu öğreticide, GroupDocs.Signature for .NET kullanarak metin içeren bir belgenin nasıl imzalanacağını öğrendik. Bu adımları izleyerek, belgelerinize programlı bir şekilde metin imzalarını verimli bir şekilde ekleyerek güvenliği ve orijinalliği artırabilirsiniz.
## SSS'ler
### Metin imzasının görünümünü özelleştirebilir miyim?
Evet, metin imzasının rengi, yazı tipi, boyutu ve konumu gibi çeşitli parametreleri tercihlerinize göre özelleştirebilirsiniz.
### GroupDocs.Signature birden fazla belge formatıyla uyumlu mu?
Evet, GroupDocs.Signature, PDF, Word, Excel, PowerPoint ve daha fazlası dahil olmak üzere çeşitli belge formatlarını destekler.
### Tek bir belgeye birden fazla metin imzası ekleyebilir miyim?
Kesinlikle, bir belgeye her biri kendi özelleştirme seçeneklerine sahip birden fazla metin imzası ekleyebilirsiniz.
### GroupDocs.Signature, imzalama sonrasında belgenin bütünlüğünü sağlıyor mu?
Evet, GroupDocs.Signature, belge bütünlüğünü sağlamak ve imzalama sonrasında kurcalamayı önlemek için güçlü şifreleme algoritmaları kullanır.
### Satın almadan önce test edebileceğiniz bir deneme sürümü var mı?
 Evet, ücretsiz deneme sürümünü şuradan indirebilirsiniz:[Burada](https://releases.groupdocs.com/) Bir satın alma işlemi yapmadan önce özellikleri keşfetmek için.