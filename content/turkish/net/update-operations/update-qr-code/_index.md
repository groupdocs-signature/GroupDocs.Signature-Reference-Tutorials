---
"description": "GroupDocs.Signature for .NET ile çeşitli belge formatlarındaki QR kod imzalarını dinamik olarak nasıl güncelleyeceğinizi öğrenin. Modern belge yönetimi çözümleri için kapsamlı geliştirici kılavuzu."
"linktitle": "QR Kodunu Güncelle"
"second_title": "GroupDocs.Signature .NET API"
"title": "Belgelerdeki QR Kod İmzalarını Güncelleyin"
"url": "/tr/net/update-operations/update-qr-code/"
"weight": 12
---

## giriiş
Günümüzün dijital odaklı iş ortamında, QR kodları belge yönetimi ve kimlik doğrulama sistemlerinde vazgeçilmez bir unsur haline gelmiştir. Basit URL'lerden karmaşık yapılandırılmış verilere kadar bilgileri kodlamak ve erişmek için kullanışlı bir yol sunarlar. GroupDocs.Signature for .NET, geliştiricilerin gelişmiş elektronik imza özelliklerini uygulamalarına entegre etmelerini sağlayan kapsamlı bir araç seti sunar; bu özellikler arasında, belgelerdeki mevcut QR kod imzalarını güncelleme olanağı da yer alır.

Bu eğitim, özellikle .NET için GroupDocs.Signature kullanarak belgelerdeki QR kod imzalarını güncellemeye odaklanmaktadır. Mevcut QR kodlarının konumunu, boyutunu veya kodlanmış verilerini değiştirmeniz gerekip gerekmediğini açıklayan bu kılavuz, size adım adım açıklayıcı kod örnekleri ve açıklamalarla süreci adım adım anlatacaktır.

## Ön koşullar
GroupDocs.Signature for .NET ile QR kod imza güncellemelerine başlamadan önce aşağıdaki ön koşulların mevcut olduğundan emin olun:

1. Geliştirme Ortamı: Visual Studio 2017 veya sonraki sürümleri gibi çalışan bir .NET geliştirme ortamı.
2. GroupDocs.Signature Kütüphanesi: GroupDocs.Signature for .NET kütüphanesini şu adresten indirin ve yükleyin: [indirme sayfası](https://releases.groupdocs.com/signature/net/).
3. Lisans (İsteğe bağlı): Üretim amaçlı kullanım için geçerli bir lisansa ihtiyacınız olacak. Test amaçlı olarak, [geçici lisans](https://purchase.groupdocs.com/temporary-license/).
4. Örnek Belge: Güncellemek istediğiniz QR kod imzalarını içeren belge.
5. Temel C# Bilgisi: C# programlama kavramlarına aşinalık.

## Ad Alanlarını İçe Aktar
GroupDocs.Signature işlevine erişmek için gerekli ad alanlarını içe aktararak başlayın:

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

QR kod imzalarının güncellenme sürecini anlaşılır ve yönetilebilir adımlara bölelim:

## Adım 1: Belge Yollarını Ayarlayın
Öncelikle kaynak belgenizin yollarını ve güncellenen belgenin nereye kaydedileceğini tanımlayın:

```csharp
// QR kod imzalarıyla kaynak belgeye giden yol
string filePath = "sample_multiple_signatures.docx";

// Çıktı için dosya adını al
string fileName = Path.GetFileName(filePath);

// Çıktı dizinini ve dosya yolunu tanımlayın
string outputDirectory = Path.Combine("Your Document Directory", "UpdateQRCode");
string outputFilePath = Path.Combine(outputDirectory, fileName);

// Çıktı dizininin mevcut olduğundan emin olun
Directory.CreateDirectory(outputDirectory);
```

## Adım 2: Kaynak Belgeyi Kopyalayın
Güncelleme işlemi belgeyi doğrudan değiştirdiğinden, orijinal belgeyi korumak için bir kopyasını oluşturun:

```csharp
// Orijinal belgenin bir kopyasını oluşturun
File.Copy(filePath, outputFilePath, true);
```

## Adım 3: İmza Örneğini Başlatın
Bir örneğini oluşturun `Signature` belgeyle çalışmak için sınıf:

```csharp
// İmza örneğini çıktı dosyası yoluyla başlatın
using (Signature signature = new Signature(outputFilePath))
{
    // İmza işlemleri burada gerçekleştirilecektir
}
```

## Adım 4: QR Kod Arama Seçeneklerini Yapılandırın
Belgedeki mevcut QR kod imzalarını bulmak için arama seçeneklerini ayarlayın:

```csharp
// QR kod imzaları için arama seçeneklerini yapılandırın
QrCodeSearchOptions options = new QrCodeSearchOptions();

// Gerekirse arama seçeneklerini özelleştirebilirsiniz
// options.AllPages = true; // Tüm sayfalarda ara
// options.PageNumber = 1; // Belirli bir sayfada arama yap
// options.EncodeType = QrCodeTypes.QR; // Belirli QR kod türünü ara
```

## Adım 5: QR Kod İmzalarını Arayın
Belgedeki QR kod imzalarını bulmak için yapılandırılmış arama seçeneklerini kullanın:

```csharp
// QR kod imzalarını arayın
List<QrCodeSignature> signatures = signature.Search<QrCodeSignature>(options);
```

## Adım 6: QR Kod İmza Özelliklerini Güncelleyin
QR kod imzaları bulunursa, özelliklerini gerektiği gibi güncelleyin:

```csharp
// İmzaların bulunup bulunmadığını kontrol edin
if (signatures.Count > 0)
{
    // İlk QR kod imzasını alın
    QrCodeSignature qrCodeSignature = signatures[0];
    
    // Pozisyonu güncelle
    qrCodeSignature.Left = 200;
    qrCodeSignature.Top = 250;
    
    // Güncelleme boyutu
    qrCodeSignature.Width = 200;
    qrCodeSignature.Height = 200;
    
    // Gerekirse QR kod verilerini de güncelleyebilirsiniz
    // qrCodeSignature.Text = "Güncellenen QR Kod Verileri";
    
    // Güncellemeleri uygula
    bool result = signature.Update(qrCodeSignature);
    
    // Sonucu kontrol edin
    if (result)
    {
        Console.WriteLine($"QR Code signature was successfully updated in the document '{fileName}'.");
        Console.WriteLine($"New position: {qrCodeSignature.Left}x{qrCodeSignature.Top}");
        Console.WriteLine($"New size: {qrCodeSignature.Width}x{qrCodeSignature.Height}");
    }
    else
    {
        Console.WriteLine($"Failed to update QR Code signature in the document!");
    }
}
else
{
    Console.WriteLine("No QR Code signatures found in the document.");
}
```

## Tam Örnek
İşte bir belgedeki QR kod imzasının nasıl güncelleneceğini gösteren eksiksiz, işlevsel bir örnek:

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;

namespace UpdateQRCodeSignatureExample
{
    class Program
    {
        static void Main(string[] args)
        {
            // Belge yolu
            string filePath = "sample_multiple_signatures.docx";
            
            // Çıkış yolunu tanımla
            string fileName = Path.GetFileName(filePath);
            string outputDirectory = Path.Combine(Environment.CurrentDirectory, "UpdateQRCode");
            string outputFilePath = Path.Combine(outputDirectory, fileName);
            
            // Çıktı dizininin mevcut olduğundan emin olun
            Directory.CreateDirectory(outputDirectory);
            
            // Orijinal belgenin bir kopyasını oluşturun
            File.Copy(filePath, outputFilePath, true);
            
            // İmza örneğini başlat
            using (Signature signature = new Signature(outputFilePath))
            {
                // Arama seçeneklerini yapılandırın
                QrCodeSearchOptions options = new QrCodeSearchOptions();
                
                // QR kod imzalarını arayın
                List<QrCodeSignature> signatures = signature.Search<QrCodeSignature>(options);
                
                // İmzaların bulunup bulunmadığını kontrol edin
                if (signatures.Count > 0)
                {
                    // İlk imzayı alın
                    QrCodeSignature qrCodeSignature = signatures[0];
                    
                    // Pozisyonu ve boyutu güncelle
                    qrCodeSignature.Left = 200;
                    qrCodeSignature.Top = 250;
                    qrCodeSignature.Width = 200;
                    qrCodeSignature.Height = 200;
                    
                    // Güncellemeleri uygula
                    bool result = signature.Update(qrCodeSignature);
                    
                    // Sonucu kontrol et
                    if (result)
                    {
                        Console.WriteLine($"QR Code signature was successfully updated in document '{fileName}'.");
                        Console.WriteLine($"New position: {qrCodeSignature.Left}x{qrCodeSignature.Top}");
                        Console.WriteLine($"New size: {qrCodeSignature.Width}x{qrCodeSignature.Height}");
                        Console.WriteLine($"Output file path: {outputFilePath}");
                    }
                    else
                    {
                        Console.WriteLine("Failed to update QR Code signature!");
                    }
                }
                else
                {
                    Console.WriteLine("No QR Code signatures found in the document.");
                }
            }
            
            Console.WriteLine("\nPress any key to exit...");
            Console.ReadKey();
        }
    }
}
```

## Gelişmiş QR Kod İmza Özelleştirmesi
GroupDocs.Signature, QR kod imzalarını temel konum ve boyutun ötesinde özelleştirmek için ek seçenekler sunar:

### Kodlanmış Verilerin Güncellenmesi
QR kodunda kodlanmış gerçek verileri güncelleyebilirsiniz:

```csharp
// Kodlanmış verileri güncelle
qrCodeSignature.Text = "https://www.güncellenmiş-websitesi.com";
```

### Görünüm Özelliklerini Ayarlama
QR kodunun görsel özelliklerini özelleştirin:

```csharp
// Ön plan rengini ayarla (QR kod rengi)
qrCodeSignature.ForeColor = System.Drawing.Color.Blue;

// Arka plan rengini ayarla
qrCodeSignature.BackgroundColor = System.Drawing.Color.LightYellow;

// Şeffaflığı ayarlayın
qrCodeSignature.Opacity = 0.8;
```

### Sınır Ekleme
QR kodunu özel kenarlıklarla geliştirin:

```csharp
qrCodeSignature.Border.Color = System.Drawing.Color.Red;
qrCodeSignature.Border.DashStyle = System.Drawing.Drawing2D.DashStyle.Dash;
qrCodeSignature.Border.Weight = 2;
qrCodeSignature.Border.Visible = true;
```

### QR Kodunu Döndürme
QR kod imzasını belirli bir açıyla döndürün:

```csharp
qrCodeSignature.Angle = 30; // 30 derece döndür
```

## Farklı Belge Biçimleriyle Çalışma
GroupDocs.Signature, çeşitli belge formatlarındaki QR kod imzalarının güncellenmesini destekler:

- PDF belgeleri
- Microsoft Word belgeleri (DOC, DOCX)
- Microsoft Excel elektronik tabloları (XLS, XLSX)
- Microsoft PowerPoint sunumları (PPT, PPTX)
- OpenDocument biçimleri
- Görüntü biçimleri

Aynı kod, bu formatlarda minimum ayarlamalarla kullanılabilir.

## Çözüm
GroupDocs.Signature for .NET, belgelerdeki QR kod imzalarını güncellemek için güçlü ve esnek bir çözüm sunar. Geliştiriciler, bu eğitimde özetlenen adımları izleyerek .NET uygulamalarında QR kod imza güncelleme işlevini verimli bir şekilde uygulayabilir, belge yönetimi ve kimlik doğrulama yeteneklerini geliştirebilirler.

GroupDocs.Signature, kapsamlı özellik seti ve sezgisel API'siyle geliştiricilerin, belge bütünlüğünü ve erişilebilirliğini garanti altına alırken modern iş uygulamalarının gereksinimlerini karşılayan gelişmiş belge imzalama çözümleri oluşturmasını sağlar.

## SSS
### Tek bir belge içerisinde birden fazla QR kod imzasını güncelleyebilir miyim?
Evet, GroupDocs.Signature aynı belge içinde birden fazla QR kod imzasını güncellemenize olanak tanır. İmzaları aradıktan sonra, ortaya çıkan listede gezinebilir ve her QR kod imzasını ayrı ayrı güncelleyebilirsiniz.

### GroupDocs.Signature farklı QR kod türlerini destekliyor mu?
Evet, GroupDocs.Signature standart QR, Mikro QR ve diğerleri dahil olmak üzere çeşitli QR kod türlerini destekler. QR kod türünü şu şekilde belirtebilirsiniz: `EncodeType` mülk.

### GroupDocs.Signature for .NET için deneme sürümü mevcut mu?
Evet, ücretsiz deneme sürümünü şu adresten indirebilirsiniz: [GroupDocs web sitesi](https://releases.groupdocs.com/signature/net/) Satın alma işlemi yapmadan önce kütüphanenin özelliklerini değerlendirmek.

### QR kod hata düzeltme seviyesini programlı olarak değiştirebilir miyim?
Evet, yeni QR kodları eklerken hata düzeltme düzeyini değiştirebilirsiniz, ancak mevcut QR kodları için bu özelliğin güncellenmesi tüm belge biçimlerinde desteklenmeyebilir.

### GroupDocs.Signature for .NET için ek desteği nerede bulabilirim?
Aşağıdaki kaynaklardan kapsamlı destek alabilirsiniz:
- [API Belgeleri](https://docs.groupdocs.com/signature/net/)
- [API Referansı](https://reference.groupdocs.com/signature/net/)
- [GitHub Örnekleri](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
- [Destek Forumu](https://forum.groupdocs.com/c/signature/13)
- [Blog](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)