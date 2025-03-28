---
title: Belgeden QR Kod İmzasını Sil
linktitle: Belgeden QR Kod İmzasını Sil
second_title: GroupDocs.Signature .NET API'si
description: GroupDocs.Signature for .NET'i kullanarak belgelerden QR kodu imzalarını nasıl sileceğinizi öğrenin. Etkin imza yönetimi için adım adım kılavuzumuzu izleyin.
weight: 16
url: /tr/net/delete-operations/delete-qr-code-signature/
---

# Belgeden QR Kod İmzasını Sil

## giriiş
Bu öğreticide, GroupDocs.Signature for .NET'i kullanarak bir belgeden QR kod imzasını kaldırma sürecinde size yol göstereceğiz. QR kodu imzalarını etkili bir şekilde silmek için bu adım adım talimatları izleyin.
## Önkoşullar
Başlamadan önce aşağıdaki önkoşullara sahip olduğunuzdan emin olun:
-  .NET için GroupDocs.Signature: .NET projenizde GroupDocs.Signature kitaplığının yüklü olduğundan emin olun. Şuradan indirebilirsiniz[Burada](https://releases.groupdocs.com/signature/net/).
- QR Kod İmzalı Belge: Silmek istediğiniz QR kod imzalarını içeren bir belge hazırlayın.
- Temel C# Bilgisi: C# programlama dilinin temellerine aşina olun.

## Ad Alanlarını İçe Aktarma
Koda dalmadan önce gerekli ad alanlarını C# dosyanıza aktarın:
```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## 1. Adım: Dosya Yollarını Tanımlayın
```csharp
// Belgeler dizininin yolu.
string filePath = "sample_multiple_signatures.docx";
string fileName = Path.GetFileName(filePath);
// Değiştirilen belge için çıktı dosyası yolunu tanımlayın.
string outputFilePath = Path.Combine("Your Document Directory", "DeleteQRCode", fileName);
// Sil yöntemi aynı Belgeyle çalıştığından kaynak dosyayı kopyalayın.
File.Copy(filePath, outputFilePath, true);
```
## Adım 2: İmza Nesnesini Başlatın
```csharp
using (Signature signature = new Signature(outputFilePath))
{
    // QR kodu imzalarını aramak için seçenekler oluşturun.
    QrCodeSearchOptions options = new QrCodeSearchOptions();
    // Belgede QR kodu imzalarını arayın.
    List<QrCodeSignature> signatures = signature.Search<QrCodeSignature>(options);
```
## 3. Adım: QR Kod İmzasının Varlığını Kontrol Edin
```csharp
    if (signatures.Count > 0)
    {
        // Belgede bulunan ilk QR kod imzasını alın.
        QrCodeSignature qrCodeSignature = signatures[0];
```
## Adım 4: QR Kod İmzasını Sil
```csharp
        // Belgeden QR kod imzasını silin.
        bool result = signature.Delete(qrCodeSignature);
        if (result)
        {
            Console.WriteLine($"Signature with QR-Code '{qrCodeSignature.Text}' and encode type '{qrCodeSignature.EncodeType.TypeName}' was deleted from document ['{fileName}'].");
        }
        else
        {
            Helper.WriteError($"Signature was not deleted from the document! Signature with Barcode '{qrCodeSignature.Text}' and encode type '{qrCodeSignature.EncodeType.TypeName}' was not found!");
        }
    }
}
```
Tebrikler! GroupDocs.Signature for .NET'i kullanarak QR kod imzasını belgeden başarıyla kaldırdınız.

## Çözüm
Bu eğitimde, GroupDocs.Signature for .NET kullanarak bir belgeden QR kod imzasının nasıl silineceğini öğrendik. Sağlanan adımları izleyerek .NET uygulamalarınızdaki imzaları verimli bir şekilde yönetebilir ve değiştirebilirsiniz.
## SSS'ler
### Bir belgeden birden fazla QR kodu imzasını silebilir miyim?
Evet, tüm QR kodu imzalarını yineleyecek şekilde kodu değiştirebilir ve bunları uygun şekilde silebilirsiniz.
### GroupDocs.Signature, QR kodlarının yanı sıra diğer imza türlerini de destekliyor mu?
Evet, GroupDocs.Signature metin, resim, barkod ve daha fazlası gibi çeşitli imza türlerini destekler.
### GroupDocs.Signature tüm belge formatlarıyla uyumlu mu?
GroupDocs.Signature, PDF, Microsoft Word, Excel, PowerPoint ve daha fazlasını içeren çok çeşitli belge formatlarını destekler.
### İmzalara ilişkin arama seçeneklerini özelleştirebilir miyim?
Evet, belgedeki belirli imzaları bulmak için arama seçeneklerini gereksinimlerinize göre uyarlayabilirsiniz.
### GroupDocs.Signature'ın deneme sürümü mevcut mu?
 Evet, GroupDocs.Signature'ın ücretsiz deneme sürümüne şuradan erişebilirsiniz:[Burada](https://releases.groupdocs.com/).