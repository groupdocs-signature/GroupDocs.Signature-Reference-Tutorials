---
title: GroupDocs.Signature kullanarak Stamp ile imzalama
linktitle: Damgayla İmzalama
second_title: GroupDocs.Signature .NET API'si
description: GroupDocs.Signature for .NET ile .NET belgelerinize damga imzalarını nasıl kolayca ekleyeceğinizi öğrenin. Belge güvenliğini geliştirin.
weight: 16
url: /tr/net/advanced-signature-techniques/sign-with-stamp/
---

# GroupDocs.Signature kullanarak Stamp ile imzalama

## giriiş
Bu öğreticide, GroupDocs.Signature for .NET'i kullanarak bir belgeyi damgayla imzalama sürecinde size yol göstereceğiz. Bu adım adım talimatları izleyerek belgelerinize kolaylıkla damga imzası ekleyebilirsiniz.
## Önkoşullar
Başlamadan önce aşağıdaki önkoşullara sahip olduğunuzdan emin olun:
1.  GroupDocs.Signature for .NET SDK: SDK'yı şu adresten indirip yükleyin:[İnternet sitesi](https://releases.groupdocs.com/signature/net/).
2. Geliştirme Ortamı: .NET geliştirme için uygun bir geliştirme ortamına sahip olduğunuzdan emin olun.
3. İmzalanacak Belge: Damgayla imzalamak istediğiniz belgeyi (örneğin PDF) hazırlayın.

## Ad Alanlarını İçe Aktarma
Gerekli ad alanlarını projenize aktararak başlayın:
```csharp
using System;
using System.IO;
using System.Drawing;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## 1. Adım: Belgeyi Yükleyin
```csharp
string filePath = "sample.pdf";
using (Signature signature = new Signature(filePath))
{
    // Kodunuz buraya gelecek
}
```
## Adım 2: Damga İşareti Seçeneklerini Ayarlayın
```csharp
StampSignOptions options = new StampSignOptions()
{
    Left = 50,
    Top = 150,                    
    Width = 200,
    Height = 200
};
```
## 3. Adım: Damga Görünümünü Yapılandırma
```csharp
StampLine outerLine = new StampLine();
outerLine.Text = " * European Union ";
outerLine.TextRepeatType = StampTextRepeatType.FullTextRepeat;
outerLine.Font.Size = 12;
outerLine.Height = 22;
outerLine.TextBottomIntent = 6;
outerLine.TextColor = Color.WhiteSmoke;
outerLine.BackgroundColor = Color.DarkSlateBlue;
options.OuterLines.Add(outerLine);
StampLine innerLine = new StampLine();
innerLine.Text = "John Smith";
innerLine.TextColor = Color.MediumVioletRed;
innerLine.Font.Size = 20;
innerLine.Font.Bold = true;
innerLine.Height = 40;
options.InnerLines.Add(innerLine);
```
## 4. Adım: Belgeyi İmzalayın
```csharp
string outputFilePath = Path.Combine("Your Document Directory", "SignWithStamp", fileName);
SignResult result = signature.Sign(outputFilePath, options);
Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).\nFile saved at {outputFilePath}.");
```

## Çözüm
GroupDocs.Signature for .NET kullanarak belgelerinize damga imzaları eklemek, bu eğitimde gösterildiği gibi basit bir işlemdir. Sağlanan adımlarla belgelerinizin güvenliğini ve orijinalliğini kolayca artırabilirsiniz.
## SSS'ler
### Damga imzasının görünümünü özelleştirebilir miyim?
Evet, metin, yazı tipi, renk ve damga imzasının konumu gibi çeşitli hususları gereksinimlerinize göre özelleştirebilirsiniz.
### GroupDocs.Signature birden fazla belge biçiminin imzalanmasını destekliyor mu?
Evet, GroupDocs.Signature, PDF, Microsoft Word, Excel, PowerPoint ve daha fazlasını içeren çok çeşitli belge formatlarını destekler.
### GroupDocs.Signature'ın deneme sürümü mevcut mu?
 Evet, ücretsiz deneme sürümüne şuradan erişebilirsiniz:[İnternet sitesi](https://releases.groupdocs.com/).
### Tek bir belgeye birden fazla imza ekleyebilir miyim?
Kesinlikle GroupDocs.Signature, tek bir belgeye damgalar, metinler, resimler ve dijital imzalar dahil olmak üzere birden fazla imza eklemenize olanak tanır.
### Uygulama sırasında herhangi bir sorunla karşılaşırsam nereden destek alabilirim?
 GroupDocs.Signature topluluk forumunda destek ve yardım bulabilirsiniz.[Burada](https://forum.groupdocs.com/c/signature/13).