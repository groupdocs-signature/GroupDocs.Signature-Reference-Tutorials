---
"date": "2025-05-08"
"description": "GroupDocs.Signature for Java ile şifreleme kullanarak görüntü meta verilerini nasıl güvence altına alacağınızı öğrenin. Adım adım kılavuzla veri bütünlüğünü ve gerçekliğini sağlayın."
"title": "GroupDocs.Signature ile Java'da Görüntü Meta Veri İmzalama ve Şifrelemeyi Uygulama"
"url": "/tr/java/metadata-signatures/groupdocs-signature-java-image-metadata-encryption/"
"weight": 1
type: docs
---
# GroupDocs.Signature Kullanarak Java'da Şifreleme ile Görüntü Meta Veri İmzalama İşlemini Uygulama

## giriiş

Günümüzün dijital dünyasında, belge meta verilerindeki hassas bilgilerin güvenliğini sağlamak son derece önemlidir. İster gizli iş sözleşmeleri ister kişisel kimlik fotoğrafları olsun, görüntü meta verilerinin bütünlüğünü ve gerçekliğini korumak, yetkisiz erişim ve tahrifatları önlemeye yardımcı olur. **Java için GroupDocs.Signature** Görüntü meta verilerini güvenli bir şekilde imzalamak ve şifrelemek için sağlam bir çözüm sağlar.

Bu eğitim, GroupDocs.Signature'ın güçlü özelliklerini kullanarak Java'da şifrelemeyle görüntü meta verisi imzalamayı nasıl uygulayacağınız konusunda size rehberlik eder. Bu adımları izleyerek, bu işlevselliği Java uygulamalarınıza etkili bir şekilde entegre edeceksiniz.

**Öğrenecekleriniz:**
- GroupDocs.Signature for Java kullanarak belge meta verilerini imzalama
- Şifreleme ile özel nesne imzalarının uygulanması
- Simetrik anahtar şifrelemesini kullanarak güvenli bir ortam oluşturma

## Ön koşullar

Başlamadan önce aşağıdaki ön koşulların sağlandığından emin olun:

### Gerekli Kütüphaneler ve Bağımlılıklar:
- **Java için GroupDocs.Signature**: 23.12 veya üzeri bir sürüme sahip olduğunuzdan emin olun.

### Ortam Kurulum Gereksinimleri:
- Makinenize Java Development Kit'i (JDK) yükleyin.
- IntelliJ IDEA, Eclipse veya NetBeans gibi Entegre Geliştirme Ortamı (IDE) kullanın.

### Bilgi Ön Koşulları:
- Java programlamanın temel bilgisi.
- Bağımlılık yönetimi için Maven veya Gradle'a aşinalık.

## Java için GroupDocs.Signature Kurulumu

GroupDocs.Signature'ı projenizde kullanmak için gerekli bağımlılıkları aşağıdaki gibi ekleyin:

### Maven Kullanımı
Bunu şuna ekle: `pom.xml` dosya:
```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

### Gradle Kullanımı
Bunu da ekleyin `build.gradle` dosya:
```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

### Doğrudan İndirme
Alternatif olarak, en son sürümü şu adresten indirin: [Java sürümleri için GroupDocs.Signature](https://releases.groupdocs.com/signature/java/).

#### Lisans Edinme Adımları
- **Ücretsiz Deneme**: Özellikleri keşfetmek için deneme sürümüyle başlayın.
- **Geçici Lisans**:Gerekirse kapsamlı testlere başvurun.
- **Satın almak**: Üretim amaçlı kullanım için lisans satın alın [GrupDokümanları](https://purchase.groupdocs.com/buy).

## Temel Başlatma ve Kurulum

GroupDocs.Signature'ı Java uygulamanızda şu şekilde başlatabilirsiniz:

```java
import com.groupdocs.signature.Signature;

public class InitializeSignature {
    public static void main(String[] args) {
        // Belgeye giden yol
        String filePath = "path/to/your/document.jpg";
        
        // İmzanın yeni bir örneğini oluşturun
        Signature signature = new Signature(filePath);

        System.out.println("GroupDocs.Signature initialized successfully.");
    }
}
```

## Uygulama Kılavuzu

### Özellik: Özel Nesne ile Meta Veri İmzası

#### Genel Bakış
Bu özellik, özel bir nesne kullanarak görüntü meta verilerinin imzalanmasına ve ek güvenlik için şifrelenmesine olanak tanır ve yalnızca yetkili tarafların meta verilere erişebilmesini veya bunları değiştirebilmesini sağlar.

#### Adım Adım Uygulama

##### 1. Belge İmza Veri Sınıfınızı Tanımlayın
Meta veri bilgilerinizi tutacak bir sınıf oluşturun:

```java
import java.math.BigDecimal;
import java.util.Date;

class DocumentSignatureData {
    private String ID;
    private String Author;
    private Date Signed = new Date();
    private BigDecimal DataFactor = new BigDecimal(0.01);

    public String getID() { return ID; }
    public void setID(String value) { ID = value; }

    @FormatAttribute(propertyName = "SignID")
    public final String getAuthor() { return Author; }
    public final void setAuthor(String value) { Author = value; }

    @FormatAttribute(propertyName = "SAuth")
    public final Date getSigned() { return Signed; }
    public final void setSigned(Date value) { Signed = value; }

    @FormatAttribute(propertyName = "SDate", propertyFormat = "yyyy-MM-dd")
    public final BigDecimal getDataFactor() { return DataFactor; }
    public final void setDataFactor(BigDecimal value) { DataFactor = value; }
}
```

##### 2. İmza Mantığını Uygulayın
İşte şifreleme kullanarak meta verileri imzalama yöntemi:

```java
import com.groupdocs.signature.Signature;
import com.groupdocs.signature.domain.extensions.encryption.IDataEncryption;
import com.groupdocs.signature.domain.extensions.encryption.SymmetricAlgorithmType;
import com.groupdocs.signature.domain.extensions.encryption.SymmetricEncryption;
import com.groupdocs.signature.domain.signatures.metadata.ImageMetadataSignature;
import com.groupdocs.signature.exception.GroupDocsSignatureException;
import com.groupdocs.signature.options.sign.MetadataSignOptions;

import java.io.File;
import java.nio.file.Paths;
import java.util.UUID;

public class SignMetadataWithCustomObject {
    // Yer tutucularla dosya yollarını başlatın
    String filePath = "YOUR_DOCUMENT_DIRECTORY/SampleImage.jpg";
    String outputFilePath = new File("YOUR_OUTPUT_DIRECTORY", 
                                       "SignedImageWithCustomMetadata/SampleImage_signed.jpg").getPath();

    public void run() throws Exception {
        Signature signature = new Signature(filePath);

        // Şifreleme için anahtar ve parolayı ayarlayın
        String key = "1234567890";
        String salt = "1234567890";
        IDataEncryption encryption = new SymmetricEncryption(
            SymmetricAlgorithmType.Rijndael, key, salt);

        MetadataSignOptions options = new MetadataSignOptions();
        DocumentSignatureData documentSignature = new DocumentSignatureData();
        
        // Özel meta veri özelliklerini ayarlayın
        documentSignature.setID(UUID.randomUUID().toString());
        documentSignature.setAuthor(System.getenv("USERNAME"));
        documentSignature.setSigned(new Date());
        documentSignature.setDataFactor(new BigDecimal("11.22"));

        ImageMetadataSignature mdDocument = new ImageMetadataSignature(41996, documentSignature);
        mdDocument.setDataEncryption(encryption);

        // Seçeneklere meta veri imzaları ekleyin
        options.getSignatures().add(mdDocument);

        signature.sign(outputFilePath, options);
    }
}
```

#### Anahtar Yapılandırma Seçenekleri
- **Simetrik Şifreleme**: Şifreleme için Rijndael algoritmasını kullanır.
- **Meta Veri SignOptions**: İmzalama sürecini yapılandırır ve hangi meta verilerin imzalanacağını belirtir.

##### Sorun Giderme İpuçları
- Dosya yollarınızın doğru ve erişilebilir olduğundan emin olun.
- Ortam değişkeninin şu şekilde olduğunu kontrol edin: `USERNAME` düzgün bir şekilde ayarlanmıştır.
- GroupDocs.Signature kütüphane sürümünün kod bağımlılıklarınızla eşleştiğini doğrulayın.

### Özellik: Şifrelemeli Meta Veri İmzası

#### Genel Bakış
Bu özellik, görüntü dosyalarındaki hassas bilgileri korumak için meta veri imzalarının şifrelenmesine odaklanır.

#### Adım Adım Uygulama
##### 1. Şifreleme Mantığını Uygulayın
İşte şifreleme kullanarak meta verileri imzalama yöntemi:
```java
import com.groupdocs.signature.Signature;
import com.groupdocs.signature.domain.extensions.encryption.IDataEncryption;
import com.groupdocs.signature.domain.extensions.encryption.SymmetricAlgorithmType;
import com.groupdocs.signature.domain.extensions.encryption.SymmetricEncryption;
import com.groupdocs.signature.exception.GroupDocsSignatureException;
import com.groupdocs.signature.options.sign.MetadataSignOptions;

import java.io.File;
import java.nio.file.Paths;
import java.util.UUID;

public class SignMetadataWithEncryption {
    // Yer tutucularla dosya yollarını başlatın
    String filePath = "YOUR_DOCUMENT_DIRECTORY/SampleImage.jpg";
    String outputFilePath = new File("YOUR_OUTPUT_DIRECTORY", 
                                       "SignedImageWithEncryption/SampleImage_signed.jpg").getPath();

    public void run() throws Exception {
        Signature signature = new Signature(filePath);

        // Şifreleme için anahtar ve parolayı ayarlayın
        String key = "1234567890";
        String salt = "1234567890";
        IDataEncryption encryption = new SymmetricEncryption(
            SymmetricAlgorithmType.Rijndael, key, salt);

        MetadataSignOptions options = new MetadataSignOptions();
        DocumentSignatureData documentSignature = new DocumentSignatureData();
        
        // Özel meta veri özelliklerini ayarlayın
        documentSignature.setID(UUID.randomUUID().toString());
        documentSignature.setAuthor(System.getenv("USERNAME"));
        documentSignature.setSigned(new Date());
        documentSignature.setDataFactor(new BigDecimal("11.22"));

        ImageMetadataSignature mdDocument = new ImageMetadataSignature(41996, documentSignature);
        mdDocument.setDataEncryption(encryption);

        // Seçeneklere meta veri imzaları ekleyin
        options.getSignatures().add(mdDocument);

        signature.sign(outputFilePath, options);
    }
}
```