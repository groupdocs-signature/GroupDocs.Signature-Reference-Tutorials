---
title: Resim İmzasını Sil
linktitle: Resim İmzasını Sil
second_title: GroupDocs.Signature .NET API'si
description: GroupDocs.Signature for .NET'i kullanarak belgelerdeki resim imzalarını nasıl sileceğinizi öğrenin. Etkin imza yönetimi için adım adım kılavuzumuzu izleyin.
type: docs
weight: 14
url: /tr/net/delete-operations/delete-image-signature/
---
## giriiş
Bu öğreticide, GroupDocs.Signature for .NET kullanarak belgelerdeki görüntü imzalarının nasıl silineceğini inceleyeceğiz. GroupDocs.Signature, geliştiricilerin çeşitli belge formatlarındaki dijital imzalar, damgalar ve form alanlarıyla çalışmasına olanak tanıyan güçlü bir kitaplıktır.
## Önkoşullar
Başlamadan önce aşağıdakilere sahip olduğunuzdan emin olun:
### 1. .NET için GroupDocs.Signature
 GroupDocs.Signature for .NET'i şu adresten indirip yükleyin:[İnternet sitesi](https://releases.groupdocs.com/signature/net/). Belgelerde sağlanan kurulum talimatlarını izleyin.
### 2. .NET Çerçevesi
Makinenizde .NET Framework'ün kurulu olduğundan emin olun.
## Ad Alanlarını İçe Aktar
Projenize gerekli ad alanlarını ekleyin:
```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
Görüntü imzalarını silme işlemini birden çok adıma ayıralım:
## 1. Adım: Dosya Yollarını Tanımlayın
İlk olarak, imzayı sildikten sonra giriş belgesi ve çıktı belgesinin yollarını belirtin:
```csharp
string filePath = "sample_multiple_signatures.docx";
string fileName = Path.GetFileName(filePath);
string outputFilePath = Path.Combine("Your Document Directory", "DeleteImage", fileName);
```
## Adım 2: Kaynak Dosyayı Kopyalayın
 Beri`Delete`yöntem aynı belgeyle çalıştığından kaynak dosyayı başka bir konuma kopyalamak önemlidir:
```csharp
File.Copy(filePath, outputFilePath, true);
```
## 3. Adım: İmza Nesnesini Başlatın
 Bir örneğini oluşturun`Signature` sınıfını seçin ve çıktı belgesinin yolunu belirtin:
```csharp
using (Signature signature = new Signature(outputFilePath))
{
    // Kod buraya gelecek
}
```
## 4. Adım: Görüntü İmzalarını Arayın
Arama seçeneklerini tanımlayın ve belgedeki resim imzalarını arayın:
```csharp
ImageSearchOptions options = new ImageSearchOptions();
List<ImageSignature> signatures = signature.Search<ImageSignature>(options);
```
## Adım 5: Görüntü İmzasını Sil
Resim imzaları bulunursa ilkini silin:
```csharp
if (signatures.Count > 0)
{
    ImageSignature imageSignature = signatures[0];
    bool result = signature.Delete(imageSignature);
    if (result)
    {
        Console.WriteLine($"Image signature at location {imageSignature.Left}x{imageSignature.Top} and Size {imageSignature.Size} was deleted from document ['{fileName}'].");
    }
    else
    {
        Helper.WriteError($"Signature was not deleted from the document! Signature at location {imageSignature.Left}x{imageSignature.Top} and Size {imageSignature.Size} was not found!");
    }
}
```
## Çözüm
Bu öğreticide, GroupDocs.Signature for .NET kullanarak belgelerdeki görüntü imzalarının nasıl silineceğini öğrendik. Geliştiriciler adım adım kılavuzu izleyerek uygulamaları içindeki dijital imzaları verimli bir şekilde yönetebilirler.
## SSS'ler
### Bir belgeden birden çok resim imzasını silebilir miyim?
 Evet, birden fazla resim imzasını silmek için kodu değiştirebilirsiniz.`signatures` liste.
### GroupDocs.Signature, DOCX'in yanı sıra diğer belge formatlarını da destekliyor mu?
Evet, GroupDocs.Signature, aralarında PDF, PPT, XLS ve daha fazlasının da bulunduğu çok çeşitli belge formatlarını destekler.
### GroupDocs.Signature for .NET'in deneme sürümü mevcut mu?
 Evet, ücretsiz deneme sürümünü şuradan indirebilirsiniz:[İnternet sitesi](https://releases.groupdocs.com/).
### GroupDocs.Signature için nasıl destek alabilirim?
 Ziyaret edebilirsiniz[GroupDocs.Signature forumu](https://forum.groupdocs.com/c/signature/13) yardım ve destek için.
### GroupDocs.Signature için geçici bir lisans satın alabilir miyim?
 Evet, geçici lisansı şu adresten satın alabilirsiniz:[satın alma sayfası](https://purchase.groupdocs.com/temporary-license/).