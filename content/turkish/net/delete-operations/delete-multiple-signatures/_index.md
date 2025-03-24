---
title: Belgeden Birden Çok İmzayı Sil
linktitle: Belgeden Birden Çok İmzayı Sil
second_title: GroupDocs.Signature .NET API'si
description: GroupDocs.Signature for .NET'i kullanarak belgelerdeki birden çok imzayı zahmetsizce silin. Belge yönetimi iş akışınızı kolaylaştırın.
weight: 15
url: /tr/net/delete-operations/delete-multiple-signatures/
---

# Belgeden Birden Çok İmzayı Sil

## giriiş
Dijital dünyada belge yönetimi genellikle çeşitli imzaların işlenmesini içerir. Bir belgeden birden fazla imzanın programlı olarak silinmesi iş akışlarını kolaylaştırabilir ve verimliliği artırabilir. GroupDocs.Signature for .NET ile bu görev kusursuz ve basit hale gelir. Bu eğitim, bir belgeden birden fazla imzayı adım adım silme sürecinde size rehberlik edecektir.
## Önkoşullar
Eğiticiye dalmadan önce aşağıdaki önkoşullara sahip olduğunuzdan emin olun:
- C# programlama dilinin temel anlayışı.
- .NET kitaplığı için GroupDocs.Signature yüklendi.
- Test için birden fazla imza içeren örnek belge.

## Ad Alanlarını İçe Aktar
GroupDocs.Signature for .NET'in işlevselliğine erişmek için gerekli ad alanlarını içe aktararak başlayın:
```csharp
using System;
using System.IO;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## Adım 1: Belge Yolunu ve Dosya Adını Tanımlayın
Birden fazla imza içeren belgenin dosya yolunu ayarlayın. Uygun dosya yoluna ve dosya adına sahip olduğunuzdan emin olun:
```csharp
string filePath = "sample_multiple_signatures.docx";
string fileName = Path.GetFileName(filePath);
```
## Adım 2: Belgeyi İşlenmek üzere Kopyalayın
Orijinal belgede değişiklik yapılmasını önlemek için işlenmek üzere bir kopya oluşturun:
```csharp
string outputFilePath = Path.Combine("Your Document Directory", "DeleteMultiple", fileName);
File.Copy(filePath, outputFilePath, true);
```
## 3. Adım: İmza Nesnesini Başlatın
Çıkış dosyası yolunu kullanarak bir İmza nesnesi örneği oluşturun:
```csharp
using (Signature signature = new Signature(outputFilePath))
{
    // İmza işleme kodu buraya gelecek
}
```
## 4. Adım: Arama Seçeneklerini Tanımlayın
Belgedeki imzaları tanımlamak için çeşitli arama seçeneklerini tanımlayın. Seçenekler arasında metin araması, görsel arama, barkod araması ve QR kodu araması bulunur:
```csharp
TextSearchOptions textSearchOptions = new TextSearchOptions();
ImageSearchOptions imageSearchOptions = new ImageSearchOptions();
BarcodeSearchOptions barcodeOptions = new BarcodeSearchOptions();
QrCodeSearchOptions qrCodeOptions = new QrCodeSearchOptions();
// Listeye seçenekler ekleyin
List<SearchOptions> listOptions = new List<SearchOptions>();
listOptions.Add(textSearchOptions);
listOptions.Add(imageSearchOptions);
listOptions.Add(barcodeOptions);
listOptions.Add(qrCodeOptions);
```
## Adım 5: İmzaları Arayın
Tanımlanan arama seçeneklerine göre belgedeki tüm imzaları bulmak için bir arama işlemi yürütün:
```csharp
SearchResult result = signature.Search(listOptions);
```
## Adım 6: İmzaları Sil
İmza bulunursa bunları silmeye devam edin:
```csharp
if (result.Signatures.Count > 0)
{
    // Tüm imzaları silmeyi dene
    DeleteResult deleteResult = signature.Delete(result.Signatures);
    //Silme işleminin başarılı olup olmadığını kontrol edin
    if(deleteResult.Succeeded.Count == result.Signatures.Count)
    {
        Console.WriteLine("\nAll signatures were successfully deleted!");                        
    }
    else
    {
        Console.WriteLine($"Successfully deleted signatures : {deleteResult.Succeeded.Count}");
        Helper.WriteError($"Not deleted signatures : {deleteResult.Failed.Count}");
    }
    // Silinen imzalarla ilgili bilgileri görüntüle
    Console.WriteLine("\nList of deleted signatures:");
    int number = 1;
    foreach(BaseSignature temp in deleteResult.Succeeded)
    {
        Console.WriteLine($"Signature #{number++}: Type: {temp.SignatureType} Id:{temp.SignatureId}, Location: {temp.Left}x{temp.Top}. Size: {temp.Width}x{temp.Height}");
    }
}
else
{
    Helper.WriteError("No one signature was found.");
}
```

## Çözüm
Bir belgeden birden fazla imzayı programlı olarak silmek, belge yönetiminde çok önemli bir görevdir. GroupDocs.Signature for .NET ile bu süreç verimli ve güvenilir hale gelir. Bu öğreticide özetlenen adımları izleyerek imza silme işlevini .NET uygulamalarınıza kolayca entegre edebilirsiniz.
## SSS'ler
### GroupDocs.Signature for .NET çeşitli belge formatlarını işleyebilir mi?
Evet, GroupDocs.Signature for .NET, DOCX, PDF, PPTX, XLSX ve daha fazlası dahil olmak üzere çok çeşitli belge formatlarını destekler.
### İmza tespiti için arama seçeneklerini özelleştirmek mümkün mü?
Kesinlikle, metin arama, görsel arama, barkod arama ve QR kod arama gibi arama seçeneklerini özel gereksinimlerinizi karşılayacak şekilde özelleştirebilirsiniz.
### GroupDocs.Signature for .NET hata işleme mekanizmaları sağlıyor mu?
Evet, kitaplık, belge işleme görevlerinin sorunsuz yürütülmesini sağlamak için güçlü hata işleme yetenekleri sunar.
### GroupDocs.Signature for .NET'i diğer üçüncü taraf kitaplıklarla entegre edebilir miyim?
Kesinlikle, GroupDocs.Signature for .NET, esneklik ve genişletilebilirlik sağlayarak diğer .NET kitaplıklarıyla sorunsuz bir şekilde entegre olacak şekilde tasarlanmıştır.
### GroupDocs.Signature for .NET için ek desteği ve kaynakları nerede bulabilirim?
 GroupDocs'u ziyaret edebilirsiniz[forum](https://forum.groupdocs.com/c/signature/13) İmzayla ilgili tartışmalara adanmıştır ve topluluktan ve uzmanlardan yardım istemektedir.