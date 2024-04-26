---
title: İmzayı kimliğe göre sil
linktitle: İmzayı kimliğe göre sil
second_title: GroupDocs.Signature .NET API'si
description: GroupDocs.Signature kitaplığını kullanarak .NET belgelerinde kimliğe göre imzayı nasıl sileceğinizi öğrenin. Kolay adım adım kılavuz.
type: docs
weight: 11
url: /tr/net/delete-operations/delete-signature-by-id/
---
## giriiş
Bu öğreticide, GroupDocs.Signature for .NET kullanarak bir imzanın kimliğine göre nasıl silineceğini inceleyeceğiz. GroupDocs.Signature for .NET, geliştiricilerin .NET uygulamalarını kullanarak çeşitli belge formatlarındaki dijital imzaları eklemesine, kaldırmasına veya doğrulamasına olanak tanıyan güçlü bir kitaplıktır.
## Önkoşullar
Başlamadan önce aşağıdaki önkoşullara sahip olduğunuzdan emin olun:
1.  GroupDocs.Signature for .NET Kitaplığı: Kitaplığı şu adresten indirip yükleyin:[Burada](https://releases.groupdocs.com/signature/net/).
2. .NET Framework: Sisteminizde .NET Framework'ün kurulu olduğundan emin olun.
3. İmzalı Belge: Silmek istediğiniz imzanın bulunduğu bir belge (örn. DOCX, PDF) hazırlayın.

## Ad Alanlarını İçe Aktar
```csharp
using System;
using System.IO;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## 1. Adım: Dosya Yollarını Tanımlayın
Öncelikle imzayı içeren belgenin dosya yolunu ve değiştirilen belgenin kaydedileceği çıktı dosyası yolunu belirtin.
```csharp
string filePath = "sample_multiple_signatures.docx";
string fileName = Path.GetFileName(filePath);
string outputFilePath = Path.Combine("Your Document Directory", "DeleteById", fileName);
```
## Adım 2: Belgeyi Kopyalayın
 Beri`Delete` yöntemi belgeyi yerinde değiştirirse, orijinal belgenin bir kopyasını oluşturmak en iyisidir.
```csharp
File.Copy(filePath, outputFilePath, true);
```
## 3. Adım: İmzayı kimliğe göre silin
 Başlat`Signature` belge dosya yolunu içeren nesneyi kullanın ve`Delete` İmzayı kimliğine göre kaldırma yöntemi.
```csharp
using (Signature signature = new Signature(outputFilePath))
{
    string id = @"eff64a14-dad9-47b0-88e5-2ee4e3604e71";
    bool result = signature.Delete(id);
    if (result)
    {
        Console.WriteLine($"Signature with Id# '{id}' was deleted from document ['{fileName}'].");
    }
    else
    {
        Helper.WriteError($"Signature was not deleted from the document! Signature with id# '{id}' was not found!");
    }
}
```

## Çözüm
Bu öğreticide, GroupDocs.Signature for .NET kullanarak bir imzanın kimliğine göre nasıl silineceğini öğrendik. Bu kitaplık, çeşitli belge formatlarındaki dijital imzaları programlı olarak yönetmenin kullanışlı bir yolunu sağlar.
## SSS'ler
### Birden fazla imzayı aynı anda silebilir miyim?
 Evet, kimliklerini yineleyerek ve çağrı yaparak birden fazla imzayı silebilirsiniz.`Delete` Her kimlik için yöntem.
### GroupDocs.Signature for .NET tüm belge formatlarıyla uyumlu mu?
GroupDocs.Signature for .NET, PDF, DOCX, XLSX ve daha fazlasını içeren çok çeşitli belge formatlarını destekler.
### İmzanın görünümünü özelleştirebilir miyim?
Evet, konumu, boyutu, yazı tipi ve rengi de dahil olmak üzere imzanın görünümünü özelleştirebilirsiniz.
### Deneme sürümü mevcut mu?
 Evet, ücretsiz deneme sürümünü şuradan indirebilirsiniz:[Burada](https://releases.groupdocs.com/).
### GroupDocs.Signature for .NET için nerede yardım veya destek bulabilirim?
 Destek forumunu ziyaret edebilirsiniz[Burada](https://forum.groupdocs.com/c/signature/13) yardım için.