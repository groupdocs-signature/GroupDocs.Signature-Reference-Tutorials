---
title: Belgeden Dijital İmzayı Sil
linktitle: Belgeden Dijital İmzayı Sil
second_title: GroupDocs.Signature .NET API'si
description: GroupDocs.Signature for .NET'i kullanarak belgelerden dijital imzaları nasıl sileceğinizi öğrenin. Verimli yönetim için adım adım kılavuzumuzu izleyin.
type: docs
weight: 13
url: /tr/net/delete-operations/delete-digital-signature/
---
## giriiş
Dijital belgeler dünyasında özgünlüğün ve güvenliğin sağlanması çok önemlidir. Dijital imzalar, elektronik belgelerin bütünlüğünün doğrulanmasında çok önemli bir rol oynamaktadır. GroupDocs.Signature for .NET, .NET uygulamaları içindeki dijital imzaları verimli bir şekilde yönetmek için güçlü araçlar sunar.
## Önkoşullar
Belgelerden dijital imzaları silmek için GroupDocs.Signature for .NET'i kullanmaya başlamadan önce aşağıdakilere sahip olduğunuzdan emin olun:
1. Visual Studio: Sisteminize Visual Studio IDE'yi yükleyin.
2.  GroupDocs.Signature for .NET: GroupDocs.Signature for .NET'i şu adresten indirip yükleyin:[indirme sayfası](https://releases.groupdocs.com/signature/net/).
3. Örnek Belge: Test için dijital imzalar içeren örnek bir belge hazırlayın.

## Ad Alanlarını İçe Aktar
Başlamak için .NET projenize gerekli ad alanlarını içe aktardığınızdan emin olun:
```csharp
using System;
using System.IO;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
```
## 1. Adım: Dosya Yollarını Tanımlayın
Kaynak belge ve çıktı belgesi için dosya yollarını tanımlayarak başlayın:
```csharp
string filePath = "sample.pdf"_SIGNED_DIGITAL;
string fileName = Path.GetFileName(filePath);
string outputFilePath = Path.Combine("Your Document Directory", "DeleteDigital", fileName);
```
## Adım 2: Kaynak Belgeyi Kopyalayın
 Beri`Delete` yöntem aynı belgeyle çalışıyorsa kaynak dosyayı yeni bir konuma kopyalamak gerekir:
```csharp
File.Copy(filePath, outputFilePath, true);
```
## 3. Adım: İmza Nesnesini Başlatın
 Bir başlat`Signature` çıktı dosyası yoluna sahip nesne:
```csharp
using (Signature signature = new Signature(outputFilePath))
{
    // Kodunuz buraya gelecek
}
```
## Adım 4: Dijital İmzaları Arayın
Belgede elektronik dijital imzaları arayın:
```csharp
List<DigitalSignature> signatures = signature.Search<DigitalSignature>(SignatureType.Digital);
```
## Adım 5: Dijital İmzayı Sil
Dijital imza bulunursa bulunan ilk imzayı silin:
```csharp
if (signatures.Count > 0)
{
    DigitalSignature digitalSignature = signatures[0];
    bool result = signature.Delete(digitalSignature);
    if (result)
    {
        Console.WriteLine($"Digital signature #{digitalSignature.Thumbprint} from {digitalSignature.SignTime.ToShortDateString()} was deleted from document ['{fileName}'].");
    }
    else
    {
        Helper.WriteError($"Signature was not deleted from the document! Signature# {digitalSignature.Thumbprint} was not found!");
    }
}
```

## Çözüm
.NET uygulamalarındaki dijital imzaları yönetmek GroupDocs.Signature ile zahmetsiz hale gelir. Yukarıda özetlenen basit adımları izleyerek dijital imzaları belgelerinizden sorunsuz bir şekilde silebilir, veri bütünlüğünü ve güvenliğini sağlayabilirsiniz.
## SSS'ler
### Tek bir belgeden birden fazla dijital imzayı silebilir miyim?
Evet, bulunan tüm dijital imzaları yineleyecek şekilde kodu değiştirebilir ve bunları uygun şekilde silebilirsiniz.
### GroupDocs.Signature dijitalin yanı sıra diğer imza türlerini de destekliyor mu?
Evet, GroupDocs.Signature elektronik, dijital ve el yazısı imzalar dahil olmak üzere çeşitli imza türlerini destekler.
### GroupDocs.Signature kurumsal düzeyde belge yönetimi için uygun mu?
Kesinlikle GroupDocs.Signature, güçlü özellikler ve ölçeklenebilirlik sunarak hem bireysel geliştiricilerin hem de kurumsal düzeydeki uygulamaların ihtiyaçlarını karşılamak üzere tasarlanmıştır.
### Dijital imzaların silinme sürecini özelleştirebilir miyim?
Evet, GroupDocs.Signature, imza silme sürecini özel gereksinimlerinize göre özelleştirmek için çok çeşitli seçenekler ve ayarlar sağlar.
### GroupDocs.Signature'ı test etmek için kullanılabilecek bir deneme sürümü var mı?
 Evet, ücretsiz deneme sürümünü şuradan indirebilirsiniz:[sürümler sayfası](https://releases.groupdocs.com/).