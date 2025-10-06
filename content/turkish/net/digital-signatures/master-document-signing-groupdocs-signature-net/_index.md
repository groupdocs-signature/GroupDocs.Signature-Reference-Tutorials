---
"date": "2025-05-07"
"description": "GroupDocs.Signature for .NET'i kullanarak belgelerdeki metin imzalarını nasıl etkili bir şekilde imzalayacağınızı, doğrulayacağınızı, arayacağınızı, güncelleyeceğinizi ve sileceğinizi öğrenin. Dijital imzalama sürecinizi bugün hızlandırın."
"title": "GroupDocs.Signature for .NET ile Ana Belge İmzalama ve Doğrulama"
"url": "/tr/net/digital-signatures/master-document-signing-groupdocs-signature-net/"
"weight": 1
type: docs
---
# GroupDocs.Signature for .NET ile Ana Belge İmzalama ve Doğrulama

## GroupDocs.Signature for .NET ile Belge İmzalama ve Doğrulamada Ustalaşma

Günümüzün dijital dünyasında, sözleşmeleri, anlaşmaları veya her türlü yasal belgeyi yönetmek için verimli belge imzalama çözümleri hayati önem taşımaktadır. Bu sürecin otomatikleştirilmesi zamandan tasarruf sağlar ve hataları azaltır. **.NET için GroupDocs.Signature** Uygulamalarınızda metin imzası yönetimini kolaylaştırmak için sağlam bir çözüm sunar. Bu kapsamlı kılavuz, metin imzalarını imzalama, doğrulama, arama, güncelleme ve silme gibi GroupDocs.Signature for .NET özelliklerini ayrıntılı olarak ele alacaktır.

## Ne Öğreneceksiniz

- Özelleştirilebilir metin imzalarıyla belgeler nasıl imzalanır?
- İmzalanmış belgeleri etkili bir şekilde doğrulama teknikleri
- Belgelerde mevcut metin imzalarını arama yöntemleri
- Gerektiğinde metin imzalarını güncelleme ve silme adımları
- Performansı ve bellek yönetimini optimize etmek için en iyi uygulamalar

Öncelikle ön koşulları gözden geçirelim.

## Ön koşullar

Başlamadan önce, geliştirme ortamınızın gerekli araçlarla kurulduğundan emin olun:

### Gerekli Kitaplıklar ve Bağımlılıklar

- **.NET için GroupDocs.Signature**: Bu kütüphane uygulamalarınıza imza işlevleri eklemenizi sağlar.
- **.NET Framework 4.6.1 veya üzeri** (veya .NET Core 2.x+)

### Ortam Kurulum Gereksinimleri

Gerekli paketleri indirmek için Visual Studio gibi bir C# geliştirme ortamına ve internet bağlantısına ihtiyacınız olacak.

### Bilgi Ön Koşulları

Temel C# programlama kavramlarına aşina olmanız önerilir. GroupDocs.Signature for .NET'i yeni kullanmaya başladıysanız endişelenmeyin; bu kılavuz size her adımda yol gösterecektir.

## .NET için GroupDocs.Signature Kurulumu

Başlamak için projenize GroupDocs.Signature kitaplığını yüklemeniz gerekir. İşte yapmanız gerekenler:

### .NET CLI aracılığıyla kurulum
```bash
dotnet add package GroupDocs.Signature
```

### Paket Yöneticisi Konsolu
```powershell
Install-Package GroupDocs.Signature
```

### NuGet Paket Yöneticisi Kullanıcı Arayüzü
1. Projenizi Visual Studio’da açın.
2. Şuraya git: **Aletler** > **NuGet Paket Yöneticisi** > **Çözüm için NuGet Paketlerini Yönetin**.
3. "GroupDocs.Signature" ifadesini arayın ve en son sürümü yükleyin.

#### Lisans Edinme Adımları
- **Ücretsiz Deneme**: Ücretsiz deneme sürümüne başlamak için şuradan indirin: [GroupDocs Ücretsiz Denemeleri](https://releases.groupdocs.com/signature/net/).
- **Geçici Lisans**: Tam özellikleri değerlendirmek için geçici bir lisans edinin [Geçici Lisans](https://purchase.groupdocs.com/temporary-license/).
- **Satın almak**: Devamlı kullanım için, şu adresten bir lisans satın alın: [GroupDocs Satın Alma Sayfası](https://purchase.groupdocs.com/buy).

#### Temel Başlatma ve Kurulum

Kurulumdan sonra projenizde GroupDocs.Signature'ı aşağıdaki şekilde başlatın:

```csharp
using GroupDocs.Signature;

// İmza örneğini belge yoluyla başlatın.
Signature signature = new Signature("path/to/your/document.pdf");
```

Artık kurulumunuz tamamlandığına göre, GroupDocs.Signature'ı çeşitli işlevler için nasıl kullanacağınızı inceleyelim.

## Uygulama Kılavuzu

### Belgeyi Metin İmzasıyla İmzala

Bu özellik, bir belgeye metin imzaları eklemenize olanak tanır. Bunu ayrıntılı olarak açıklayalım:

#### Genel Bakış
Yazı tipi boyutu, renk, hizalama vb. gibi çeşitli seçenekleri kullanarak metin imzanızın görünümünü ve konumunu özelleştirebilirsiniz.

#### Adım Adım Uygulama

**Adım 1**: Dosya yolunu ve çıktı konumunu tanımlayın.
```csharp
string filePath = "YOUR_DOCUMENT_DIRECTORY"; // Orijinal belgeye giden yol
string outputFilePath = Path.Combine("YOUR_OUTPUT_DIRECTORY", "SignedDocument.docx");
```

**Adım 2**: Kullanarak bir metin imzası oluşturun `TextSignOptions`.
```csharp
using (Signature signature = new Signature(filePath))
{
    TextSignOptions signOptions = new TextSignOptions("John Smith")
    {
        VerticalAlignment = GroupDocs.Signature.Options.VerticalAlignment.Top,
        HorizontalAlignment = GroupDocs.Signature.Options.HorizontalAlignment.Center,
        Width = 100,
        Height = 40,
        Margin = new Padding(20),
        ForeColor = Color.Red,
        Font = new SignatureFont { Size = 12, FamilyName = "Comic Sans MS" }
    };
```

**Adım 3**: Belgeyi imzalayın ve sonuçları çıktı olarak alın.
```csharp
    SignResult signResult = signature.Sign(outputFilePath, signOptions);
    foreach (BaseSignature temp in signResult.Succeeded)
    {
        Console.WriteLine($"Signed Text Signature: Id:{temp.SignatureId}, Location: {temp.Left}x{temp.Top}. Size: {temp.Width}x{temp.Height}");
    }
}
```

#### Anahtar Yapılandırma Seçenekleri
- **Dikey Hizalama ve Yatay Hizalama**İmzanın sayfada nerede görüneceğini kontrol edin.
- **Yazı tipi**: Metin imzanız için yazı tipi boyutunu ve stilini özelleştirin.

### Belgeyi Metin İmzası için Doğrulayın

Doğrulama, bir belgenin amaçlandığı gibi imzalandığını garanti eder. Uygulama yöntemi şu şekildedir:

#### Genel Bakış
Belgelerinizdeki mevcut metin imzalarını doğrulayarak bunların gerçekliğini ve bütünlüğünü teyit edin.

#### Adım Adım Uygulama

**Adım 1**: İmzalanan belgenin dosya yolunu belirtin.
```csharp
string filePath = "YOUR_OUTPUT_DIRECTORY"; // İmzalanan belgeye giden yol
```

**Adım 2**: Doğrulama seçeneklerini kullanarak oluşturun `TextVerifyOptions`.
```csharp
using (Signature signature = new Signature(filePath))
{
    TextVerifyOptions verifyOptions = new TextVerifyOptions()
    {
        AllPages = false,
        PageNumber = 1,
        Text = "John Smith",
        MatchType = GroupDocs.Signature.Options.TextMatchType.Exact
    };
```

**Adım 3**: Belgeyi doğrulayın.
```csharp
    VerificationResult verifyResult = signature.Verify(verifyOptions);
    if (verifyResult.IsValid)
    {
        Console.WriteLine("Document was verified successfully!");
    }
    else
    {
        Console.WriteLine("Document failed verification process.");
    }
}
```

#### Sorun Giderme İpuçları
- Sağlayın `Text` özellik, belgede yer alanla birebir örtüşüyor.
- Bunu kontrol et `PageNumber` İmzanın bulunduğu doğru sayfaya karşılık gelir.

### Metin İmzası için Belgeyi Ara

Bu özelliği kullanarak belgelerinizdeki metin imzalarını etkili bir şekilde bulun.

#### Genel Bakış
Belirli metin imzalarını bulmak için bir belgenin tüm sayfalarında veya seçili sayfalarında arama yapın.

#### Adım Adım Uygulama

**Adım 1**: Dosya yolunu tanımlayın.
```csharp
string filePath = "YOUR_OUTPUT_DIRECTORY"; // İmzalanan belgeye giden yol
```

**Adım 2**: Kullanmak `TextSearchOptions` Arama için.
```csharp
using (Signature signature = new Signature(filePath))
{
    TextSearchOptions searchOptions = new TextSearchOptions()
    {
        AllPages = true,
        MatchType = GroupDocs.Signature.Options.TextMatchType.Exact,
        Text = "John Smith"
    };
```

**Adım 3**: Aramayı gerçekleştirin.
```csharp
    List<TextSignature> signatures = signature.Search<TextSignature>(searchOptions);
    foreach (TextSignature textSignature in signatures)
    {
        if (textSignature != null)
        {
            Console.WriteLine($"Found Text signature at page {textSignature.PageNumber} with type [{textSignature.SignatureImplementation}] and text '{textSignature.Text}'. Location: {textSignature.Left}-{textSignature.Top}. Size is {textSignature.Width}x{textSignature.Height}.");
        }
    }
}
```

### Belge Metin İmzasını Güncelle

Gerektiğinde belgedeki mevcut metin imzalarını değiştirin.

#### Genel Bakış
Mevcut metin imzalarının boyut ve konum gibi özelliklerini ayarlayın.

#### Adım Adım Uygulama

**Adım 1**: Dosya yolunu ve imza kimliklerini belirtin.
```csharp
string filePath = "YOUR_OUTPUT_DIRECTORY"; // İmzalanan belgeye giden yol
List<string> signatureIds = new List<string>(); // Bu listenin geçerli imza kimlikleriyle doldurulduğunu varsayalım
```

**Adım 2**: Yaratmak `TextSignature` güncellemeler için nesneler.
```csharp
using (Signature signature = new Signature(filePath))
{
    foreach (var item in signatureIds)
    {
        TextSignature temp = new TextSignature(item)
        {
            Width = 150,
            Height = 50,
            HorizontalAlignment = GroupDocs.Signature.Options.HorizontalAlignment.Right
        };
```

**Adım 3**: Belgeyi güncelleyin.
```csharp
        SignResult signResult = signature.UpdateSignatures(temp);
        if (signResult.Succeeded.Count > 0)
        {
            Console.WriteLine($"Updated Text Signature: Id:{temp.SignatureId}");
        }
    }
}
```

#### Anahtar Yapılandırma Seçenekleri
- **Genişlik ve Yükseklik**: İmzanın boyutunu ayarlayın.
- **Yatay Hizalama**: Güncellenen imzanın sayfada nerede görüneceğini kontrol edin.

## Çözüm

Bu kılavuzu izleyerek, GroupDocs.Signature for .NET kullanarak belgelerdeki metin imzalarını nasıl imzalayacağınızı, doğrulayacağınızı, arayacağınızı, güncelleyeceğinizi ve sileceğinizi öğrendiniz. Bu özellikler, uygulamalarınızdaki dijital imzalama süreçlerini otomatikleştirmek için olmazsa olmazdır. Daha ayrıntılı bilgi ve gelişmiş seçenekler için bkz. [resmi belgeler](https://docs.groupdocs.com/signature/net/).