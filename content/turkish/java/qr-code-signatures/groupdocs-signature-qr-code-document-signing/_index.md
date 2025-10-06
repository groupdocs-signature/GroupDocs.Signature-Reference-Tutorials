---
"date": "2025-05-08"
"description": "HIBC verilerini kodlayan QR kodlarıyla belgeleri güvenli bir şekilde imzalamak için GroupDocs.Signature for Java'yı nasıl kullanacağınızı öğrenin. Belge yönetimi süreçlerinizi bugünden itibaren hızlandırın."
"title": "GroupDocs.Signature for Java Kullanarak QR Kodlarıyla Ana Belge İmzalama - Kapsamlı Bir Kılavuz"
"url": "/tr/java/qr-code-signatures/groupdocs-signature-qr-code-document-signing/"
"weight": 1
type: docs
---
# Java için GroupDocs.Signature Kullanarak QR Kodlarıyla Ana Belge İmzalama

## giriiş

Dijital çağda, ilaç verilerinin verimli bir şekilde yönetilmesi ve güvence altına alınması, uyumluluk ve operasyonel verimlilik açısından hayati önem taşımaktadır. Kapsamlı ürün bilgilerinin belgelere entegre edilmesi zor olabilir. Bu eğitim, **Java için GroupDocs.Signature** Sağlık Endüstrisi Barkod (HIBC) verilerini QR kodlarına kodlamak ve belgeleri sorunsuz bir şekilde imzalamak.

### Öğrenecekleriniz:
- Java için GroupDocs.Signature'ı ayarlayın.
- HIBCLICPrimaryData, HIBCLICSecondaryAdditionalData örneklerini ve bunların birleştirilmiş formlarını oluşturun.
- Ayrıntılı ürün bilgilerini kodlayan QR kodlarını kullanarak belgeleri imzalayın.
- Kaynakları etkili bir şekilde yönetirken performansı optimize edin.

## Ön koşullar

### Gerekli Kitaplıklar ve Bağımlılıklar
GroupDocs.Signature for Java'yı kullanmak için şunlara sahip olduğunuzdan emin olun:
- **Java Geliştirme Kiti (JDK)**: Sürüm 8 veya üzeri.
- **Maven** veya **Gradle**: Bağımlılık yönetimi için.

### Ortam Kurulum Gereksinimleri
Geliştirme ortamınızın Maven veya Gradle kullanacak şekilde yapılandırıldığından emin olun; bu, bağımlılığı ve proje oluşturma yönetimini basitleştirir.

### Bilgi Ön Koşulları
Java programlamaya aşinalık, kod parçacıklarını ve uygulama ayrıntılarını anlamanıza yardımcı olacaktır.

## Java için GroupDocs.Signature Kurulumu

### Kurulum Bilgileri

**Maven**
```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

**Gradle**
```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

**Doğrudan İndirme**: En son sürümü şu adresten indirin: [Java sürümleri için GroupDocs.Signature](https://releases.groupdocs.com/signature/java/).

### Lisans Edinme Adımları
1. **Ücretsiz Deneme**:Temel işlevleri test etmek için öncelikle deneme sürümünü indirin.
2. **Geçici Lisans**: Değerlendirme süreniz boyunca hiçbir sınırlama olmadan tam erişim için bunu edinin.
3. **Satın almak**: Uzun vadeli projeler için lisans satın almayı düşünün.

#### Temel Başlatma ve Kurulum
Kurulduktan sonra, başlatın `Signature` İmzalamak istediğiniz belgenin dosya yolunu içeren nesne:
```java
String filePath = "Sample.pdf";
Signature signature = new Signature(filePath);
```

## Uygulama Kılavuzu

### HIBC LIC Birincil Verilerini Oluşturun
**Genel Bakış**: Bu bölüm, bir örneğin nasıl oluşturulacağını ve yapılandırılacağını gösterir. `HIBCLICPrimaryData`, temel ürün bilgilerinin yer aldığı.

#### Adım 1: Birincil Veri Nesnesini Başlatın
```java
HIBCLICPrimaryData primaryData = new HIBCLICPrimaryData();
```

#### Adım 2: Temel Özellikleri Ayarlayın
- **Ürün veya Katalog Numarası**: Ürüne ait benzersiz tanımlayıcı.
- **Etiketleyici Tanımlama Kodu**: Üreticiyi tanımlar.
- **Ölçü Birimi Kimliği**: Ölçüm birimlerini belirtir.

```java
primaryData.setProductOrCatalogNumber("12345");
primaryData.setLabelerIdentificationCode("A999");
primaryData.setUnitOfMeasureID(1);
```

### HIBC LIC İkincil Ek Verilerini Oluşturun
**Genel Bakış**: Bu bölüm, bir örneğin oluşturulmasını ve yapılandırılmasını kapsar `HIBCLICSecondaryAdditionalData`Son kullanma tarihi ve parti numarası gibi ek ayrıntıları da içerir.

#### Adım 1: İkincil Veri Nesnesini Başlatın
```java
HIBCLICSecondaryAdditionalData secondaryData = new HIBCLICSecondaryAdditionalData();
```

#### Adım 2: Ek Özellikleri Ayarlayın
- **Son kullanma tarihi**: Gösterim için güncel tarihi kullanın.
- **Miktar, Parti Numarası, Seri Numarası**: Ürün özelliklerini tanımlayın.
- **Üretim Tarihi ve Bağlantı Karakteri**: Üretim detaylarını belirleyin.

```java
secondaryData.setExpiryDate(new Date());
secondaryData.setExpiryDateFormat(HIBCLICDateFormat.MMDDYY);
secondaryData.setQuantity(30);
secondaryData.setLotNumber("LOT123");
secondaryData.setSerialNumber("SERIAL123");
secondaryData.setDateOfManufacture(new Date());
secondaryData.setLinkCharacter('S');
```

### HIBC LIC Birincil ve İkincil Verilerini Birleştirin
**Genel Bakış**: Birincil ve ikincil verileri tek bir veride nasıl birleştireceğinizi öğrenin `HIBCLICCombinedData` akıcı işleme için nesne.

#### Adım 1: Birleşik Veri Nesnesini Başlatın
```java
HIBCLICCombinedData combinedData = new HIBCLICCombinedData();
```

#### Adım 2: Birincil ve İkincil Verileri Ayarlayın
- Her iki veri setini birbirine bağlayarak eksiksiz bir veri yapısı oluşturun.

```java
combinedData.setPrimaryData(primaryData);
combinedData.setSecondaryAdditionalData(secondaryData);
```

### HIBC LIC Birleşik Verilerini İçeren QR Koduyla Belgeyi İmzalayın
**Genel Bakış**: Bu son bölüm, birleştirilmiş HIBC verilerini kodlayan bir QR kodu kullanarak bir belgenin nasıl imzalanacağını göstermektedir.

#### Adım 1: Dosya Yollarını Tanımlayın
```java
String filePath = "YOUR_DOCUMENT_DIRECTORY/Sample.pdf";
String outputFilePath = "YOUR_OUTPUT_DIRECTORY/SignWithQRCodeHIBCLICCombinedData/" + fileName;
```

#### Adım 2: QR Kod İmzalama Seçeneklerini Ayarlayın
- **Kodlama Türü**: Kullanmak `QrCodeTypes.HIBCLICQR` kodlama türünü belirtmek için.
- **Veri Atama**: QR koduna dahil edilmek üzere birleştirilmiş verileri iletin.

```java
Signature signature = new Signature(filePath);
try {
    QrCodeSignOptions options = new QrCodeSignOptions();
    options.setEncodeType(QrCodeTypes.HIBCLICQR);
    options.setData(combinedData);

    // Belgeyi imzala ve kaydet
    signature.sign(outputFilePath, options);
} finally {
    if (signature != null) signature.dispose();
}
```

## Pratik Uygulamalar
1. **İlaç Uyumluluğu**Bu entegrasyonu kullanarak düzenleyici standartlara uyumluluğu kolaylaştırın.
2. **Tedarik zinciri yönetimi**: Belgelerdeki QR kodlar aracılığıyla farmasötik ürünlerin izlenebilirliğini artırın.
3. **Sağlık Sistemleri Entegrasyonu**:Daha iyi hasta güvenliği için kapsamlı ürün verilerini sağlık kayıtlarına yerleştirin.

## Performans Hususları
- **Kaynak Kullanımını Optimize Edin**: Bellek yönetimini verimli bir şekilde sağlamak için şunları yapın: `Signature` nesne operasyon sonrası.
- **En İyi Uygulamalar**: Performans iyileştirmeleri ve hata düzeltmeleri için düzenli olarak en son GroupDocs.Signature sürümüne güncelleyin.

## Çözüm
Bu kılavuzu izleyerek, HIBC LIC birincil ve ikincil veri nesnelerini nasıl oluşturacağınızı, bunları tek bir varlıkta nasıl birleştireceğinizi ve GroupDocs.Signature for Java kullanarak belgeleri QR kodlarıyla nasıl imzalayacağınızı öğrendiniz. Bu beceriler, belge güvenliğini artırır ve ilaç endüstrisinde uyumluluğu sağlar.

### Sonraki Adımlar
- GroupDocs.Signature'ın ek işlevlerini keşfedin.
- Belge imzalama süreçlerini otomatikleştirmek için bu çözümü mevcut sistemlerinize entegre edin.

## SSS Bölümü
1. **HIBC verisi nedir?**
   - Sağlık Endüstrisi Barkodu (HIBC) verileri, sağlık ve ilaç endüstrilerinde kullanılan temel ürün bilgilerini içerir.
2. **GroupDocs.Signature'ı diğer barkod türleri için kullanabilir miyim?**
   - Evet, GroupDocs.Signature QR kodlarının ötesinde çeşitli barkod formatlarını destekler.
3. **Belgemin formatı PDF değilse ne olacak?**
   - GroupDocs.Signature, Word ve Excel dahil olmak üzere birden fazla belge biçimini destekler.
4. **İmzalama sırasında istisnaları nasıl yönetirim?**
   - İstisnaları etkili bir şekilde yönetmek ve kaynak temizliğini sağlamak için try-catch bloklarını uygulayın.
5. **Belge başına QR kod sayısında bir sınırlama var mı?**
   - Doğal bir sınır yoktur; ancak çok sayıda kod eklerken performans etkilerini göz önünde bulundurun.

## Kaynaklar
- **Belgeleme**: [Java Belgeleri için GroupDocs.Signature](https://docs.groupdocs.com/signature/java/)
- **API Referansı**: [GroupDocs API Referansı](https://reference.groupdocs.com/signature/java/)
- **İndirmek**: [En Son GroupDocs.Sürümleri](https://releases.groupdocs.com/signature/java/)
- **Satın almak**: [Lisans Satın Al](https://purchase.groupdocs.com/buy)
- **Ücretsiz Deneme**: [Ücretsiz Deneyin](https://releases.groupdocs.com/signature/java/)
- **Geçici Lisans**: [Buraya Başvurun](https://purchase.groupdocs.com/temporary-license/)