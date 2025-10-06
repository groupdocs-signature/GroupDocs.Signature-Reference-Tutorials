---
"description": "Adım adım geliştirici kılavuzumuzla GroupDocs.Signature for .NET'i kullanarak belgelerinizden QR kod imzalarını kolayca nasıl sileceğinizi öğrenin."
"linktitle": "Belgeden QR Kod İmzasını Sil"
"second_title": "GroupDocs.Signature .NET API"
"title": ".NET'te Belgelerden QR Kod İmzaları Nasıl Kaldırılır?"
"url": "/tr/net/delete-operations/delete-qr-code-signature/"
"weight": 16
type: docs
---
# Belgelerinizden QR Kod İmzalarını Nasıl Silersiniz?

## giriiş

Bir belgeden QR kod imzasını programatik olarak kaldırmanız gerekti mi? İster güncelliğini yitirmiş bilgileri temizliyor olun, ister belgeleri yeniden dağıtıma hazırlıyor olun, belge imzalarını etkili bir şekilde yönetebilmek .NET geliştiricileri için hayati önem taşıyan bir beceridir.

Bu kullanıcı dostu kılavuzda, GroupDocs.Signature for .NET kullanarak belgelerden QR kod imzalarını nasıl sileceğinizi adım adım anlatacağız. Bu güçlü kütüphane, imza yönetimini kolaylaştırarak belge işleme zorluklarıyla boğuşmak yerine harika uygulamalar geliştirmeye odaklanmanızı sağlar.

## Başlamadan Önce İhtiyacınız Olanlar

Koda dalmadan önce her şeyin hazır olduğundan emin olalım:

- GroupDocs.Signature for .NET: Projenizde kütüphanenin yüklü olması gerekir. Doğrudan şu adresten indirebilirsiniz: [GroupDocs sürüm sayfası](https://releases.groupdocs.com/signature/net/).
- QR kodlu bir belge: Pratik yapmak için, kaldırmak istediğiniz en az bir QR kod imzası içeren bir belge hazırlayın.
- Temel C# bilgisi: Örneklerimizi takip edebilmek için C# temellerine hakim olmanız gerekir.

Bu ön koşulları yerine getirdiğinizde, QR kodlarını kaldırmaya hazırsınız!

## Projenizi Doğru Ad Alanlarıyla Kurma

Öncelikle kodumuzun düzgün çalışması için gerekli ad alanlarını içe aktaralım:

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

Bu içe aktarımlar bize GroupDocs.Signature kütüphanesinden ihtiyaç duyduğumuz tüm işlevlere ve dosya işleme için bazı temel .NET sınıflarına erişim olanağı sağlar.

## Adım 1: Dosyalarınız Nerede? Belge Yollarını Ayarlama

Öncelikle belgelerimizin nerede bulunduğunu ve değiştirilmiş halini nereye kaydetmek istediğimizi tanımlayalım:

```csharp
// Belgeler dizinine giden yol.
string filePath = "sample_multiple_signatures.docx";
string fileName = Path.GetFileName(filePath);

// Değiştirilen belge için çıktı dosyası yolunu tanımlayın.
string outputFilePath = Path.Combine("Your Document Directory", "DeleteQRCode", fileName);

// Delete metodu aynı Document ile çalıştığı için kaynak dosyayı kopyalayın.
File.Copy(filePath, outputFilePath, true);
```

Orijinal belgemizin bir kopyasını oluşturduğumuzu unutmayın. Bu önemlidir çünkü imza silme işlemi dosyayı doğrudan değiştirecektir ve orijinal belgelerimizi her zaman korumak isteriz.

## Adım 2: Üzerinde Çalışılacak Bir İmza Nesnesi Oluşturma

Şimdi belgemize bağlanan bir Signature nesnesi oluşturacağız:

```csharp
using (Signature signature = new Signature(outputFilePath))
{
    // QR kod imzalarını aramak için seçenekler oluşturun.
    QrCodeSearchOptions options = new QrCodeSearchOptions();
    
    // Belgede QR kod imzalarını arayın.
    List<QrCodeSignature> signatures = signature.Search<QrCodeSignature>(options);
```

Bu kod, Signature nesnesini belgemizle başlatır ve ardından içinde bulunan tüm QR kod imzalarını arar. Arama, bulunan tüm QR kod imzalarının bir listesini döndürür.

## Adım 3: Silinecek QR Kodları Var mı?

Herhangi bir şeyi silmeye çalışmadan önce, gerçekten QR kodlarının mevcut olup olmadığını kontrol etmeliyiz:

```csharp
    if (signatures.Count > 0)
    {
        // Belgede bulunan ilk QR kod imzasını alın.
        QrCodeSignature qrCodeSignature = signatures[0];
```

Bu basit kontrol, belgede en az bir QR kod imzası varsa işlem yapmamızı sağlar. Bu örnekte, bulunan ilk QR kodunu hedefliyoruz, ancak gerekirse birden fazla imzayı işleyecek şekilde bunu kolayca değiştirebilirsiniz.

## Adım 4: QR Kodunu Belgenizden Kaldırma

Şimdi asıl olaya gelelim: QR kodunu silmek:

```csharp
        // QR kod imzasını belgeden silin.
        bool result = signature.Delete(qrCodeSignature);
        
        if (result)
        {
            Console.WriteLine($"Signature with QR-Code '{qrCodeSignature.Text}' and encode type '{qrCodeSignature.EncodeType.TypeName}' was deleted from document ['{fileName}'].");
        }
        else
        {
            Console.WriteLine($"Signature was not deleted from the document! Signature with QR-Code '{qrCodeSignature.Text}' and encode type '{qrCodeSignature.EncodeType.TypeName}' was not found!");
        }
    }
}
```

Kod, imzayı siler ve işlemin başarılı olup olmadığına dair geri bildirim sağlar. Bu geri bildirim, hata ayıklama ve kodunuzun beklendiği gibi çalıştığını doğrulama açısından çok önemlidir.

## Neler Başardık?

Tebrikler! GroupDocs.Signature for .NET kullanarak belgelerden QR kod imzalarını nasıl kaldıracağınızı öğrendiniz. Bu beceri, uygulamalarınızda belge yönetimi için sayısız olanak sunar.

Artık sadece birkaç satır kodla, güncelliğini yitirmiş veya gereksiz QR kod imzalarını kaldırarak belgelerinizi programatik olarak temizleyebilir, belgelerinizin her zaman yalnızca ilgili bilgileri içermesini sağlayabilirsiniz.

## Aklınıza Gelebilecek Yaygın Sorular

### Birden fazla QR kodunu aynı anda silebilir miyim?

Kesinlikle! Sadece bulunan ilk imzayı silmek yerine, tüm imza listesini tarayıp her birini şu şekilde silebilirsiniz:

```csharp
foreach(var qrSignature in signatures)
{
    signature.Delete(qrSignature);
}
```

### GroupDocs.Signature ile başka hangi imza türlerini yönetebilirim?

GroupDocs.Signature, aşağıdakiler de dahil olmak üzere çeşitli imza türlerini destekleyen inanılmaz derecede çok yönlüdür:
- Metin imzaları
- Görüntü imzaları
- Barkod imzaları
- Dijital imzalar
- Ve daha niceleri!

### Bu tüm belge biçimlerimle çalışacak mı?

GroupDocs.Signature'ın aşağıdakiler de dahil olmak üzere çok çeşitli belge formatlarıyla çalıştığını bilmek sizi memnun edecektir:
- PDF belgeleri
- Microsoft Word belgeleri
- Excel elektronik tabloları
- PowerPoint sunumları
- Ve diğerleri

### Tüm QR kodlarını silmek yerine belirli QR kodlarını arayabilir miyim?

Evet! `QrCodeSearchOptions` class, aramanızı filtrelemek için çeşitli özellikler sunar. Örneğin, belirli metinler içeren veya belirli biçimlerle kodlanmış QR kodlarını arayabilirsiniz.

### GroupDocs.Signature'ı satın almadan önce denemenin bir yolu var mı?

Evet, ücretsiz deneme sürümünü şu adresten indirebilirsiniz: [GroupDocs web sitesi](https://releases.groupdocs.com/) taahhütte bulunmadan önce bunu kendi özel kullanım durumlarınızla test etmeniz gerekir.