---
title: Çoklu İmza Ara
linktitle: Çoklu İmza Ara
second_title: GroupDocs.Signature .NET API'si
description: Verimli belge güvenliği ve bütünlüğü için GroupDocs.Signature'ı kullanarak .NET belgelerinde birden çok imzayı nasıl arayacağınızı öğrenin.
type: docs
weight: 14
url: /tr/net/signature-searching/search-for-multiple-signatures/
---
## giriiş
GroupDocs.Signature for .NET, geliştiricilerin .NET uygulamalarını kullanarak popüler belge formatlarındaki çeşitli imza türlerini eklemesine, aramasına ve kaldırmasına olanak tanıyan güçlü bir kitaplıktır. Bu öğreticide, GroupDocs.Signature for .NET'i kullanarak bir belge içinde birden çok imzayı aramaya odaklanacağız.
## Önkoşullar
Başlamadan önce aşağıdaki önkoşullara sahip olduğunuzdan emin olun:
- Sisteminizde Visual Studio yüklü.
- C# programlama dilinin temel anlayışı.
- Projenizde yüklü olan .NET kitaplığı için GroupDocs.Signature. Şuradan indirebilirsiniz[Burada](https://releases.groupdocs.com/signature/net/).

## Ad Alanlarını İçe Aktar
Öncelikle GroupDocs.Signature for .NET tarafından sağlanan sınıflara ve yöntemlere erişmek için gerekli ad alanlarını içe aktarmanız gerekir.
```csharp
using System;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## 1. Adım: Belgeyi Yükleyin
Belgeyi birden fazla imza aramak istediğiniz yere yükleyin. Doğru dosya yolunu sağladığınızdan emin olun.
```csharp
string filePath = "sample_multiple_signatures.docx";
using (Signature signature = new Signature(filePath))
{
    // Kodunuz buraya gelecek
}
```
## 2. Adım: Arama Seçeneklerini Tanımlayın
Metin, dijital, barkod, QR kodu ve meta veriler gibi çeşitli imza türleri için arama seçeneklerini tanımlayın. Eşleşecek metin, eşleme türü gibi arama kriterlerini belirtebilir ve tüm sayfalarda arama yapabilirsiniz.
```csharp
// Arama seçeneklerini tanımlayın
TextSearchOptions textOptions = new TextSearchOptions()
{
    AllPages = true
};
DigitalSearchOptions digitalOptions = new DigitalSearchOptions()
{
    AllPages = true
};
BarcodeSearchOptions barcodeOptions = new BarcodeSearchOptions()
{
    AllPages = true,
    Text = "123456",
    MatchType = TextMatchType.Exact
};
QrCodeSearchOptions qrCodeOptions = new QrCodeSearchOptions()
{
    AllPages = true,
    Text = "John",
    MatchType = TextMatchType.Contains
};
MetadataSearchOptions metadataOptions = new MetadataSearchOptions();
```
## 3. Adım: Arama Seçeneklerini Listeye Ekleme
Tanımlanan arama seçeneklerini bir listeye ekleyin.
```csharp
// Listeye seçenekler ekleyin
List<SearchOptions> listOptions = new List<SearchOptions>();
listOptions.Add(textOptions);
listOptions.Add(barcodeOptions);
listOptions.Add(qrCodeOptions);
listOptions.Add(metadataOptions);
listOptions.Add(digitalOptions);
```
## 4. Adım: İmzaları Arayın
Tanımlanan arama seçeneklerini kullanarak belgedeki imzaları arayın.
```csharp
// Belgedeki imzaları arayın
SearchResult result = signature.Search(listOptions);
if (result.Signatures.Count > 0)
{
    Console.WriteLine($"\nSource document ['{filePath}'] contains following signatures.");
    foreach (var resSignature in result.Signatures)
    {
        Console.WriteLine($"Signature found at page {resSignature.PageNumber} with type {resSignature.SignatureType} and Id#: {resSignature.SignatureId}");
    }
}
else
{
    Helper.WriteError("No one signature was found.");
}
```

## Çözüm
Bu öğreticide, GroupDocs.Signature for .NET'i kullanarak bir belgede birden çok imzayı nasıl arayacağımızı öğrendik. Verilen adımları izleyerek, belgelerinizdeki çeşitli imza türlerini etkili bir şekilde bulabilir, belge güvenliğini ve bütünlüğünü artırabilirsiniz.
## SSS'ler
### Farklı belge formatlarındaki imzaları arayabilir miyim?
Evet, GroupDocs.Signature for .NET, Word, PDF, Excel ve daha fazlasını içeren çok çeşitli belge formatlarını destekler.
### İmzalar için arama kriterlerini özelleştirmek mümkün mü?
Kesinlikle, arama kriterlerini tam metin eşleşmelerini belirlemek veya tüm sayfalarda arama yapmak gibi gereksinimlerinize göre uyarlayabilirsiniz.
### GroupDocs.Signature for .NET dijital imzalar için destek sunuyor mu?
Evet, dijital imzaların yanı sıra metin, barkod ve QR kod imzaları gibi diğer türleri de arayabilirsiniz.
### İmza arama işlevini .NET uygulamalarıma kolayca entegre edebilir miyim?
Evet, GroupDocs.Signature for .NET, entegrasyon sürecini kolaylaştıran basit bir API sağlar.
### Nerede ek destek veya yardım bulabilirim?
 GroupDocs.Signature forumunu ziyaret edebilirsiniz.[Burada](https://forum.groupdocs.com/c/signature/13) Herhangi bir sorunuz veya yardımınız için.