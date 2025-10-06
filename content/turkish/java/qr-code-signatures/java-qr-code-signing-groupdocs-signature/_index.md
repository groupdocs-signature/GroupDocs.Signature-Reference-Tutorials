---
"date": "2025-05-08"
"description": "GroupDocs.Signature kullanarak Java QR kod imzalamayı nasıl uygulayacağınızı öğrenin. Belge güvenliğini artırın, imzalama seçeneklerini yapılandırın ve Java uygulamalarınızda özel şifreleme uygulayın."
"title": "Java QR Kod İmzalama Kılavuzu - Belgelerinizi GroupDocs.Signature ile Güvence Altına Alın"
"url": "/tr/java/qr-code-signatures/java-qr-code-signing-groupdocs-signature/"
"weight": 1
type: docs
---
# GroupDocs.Signature for Java ile Java QR Kod İmzalamanın Uygulanması

## giriiş

Java uygulamalarınıza QR kodları yerleştirerek dijital belgelerinizin güvenliğini artırın. GroupDocs.Signature for Java'dan yararlanarak belgelerinizin gerçekliğini ve izlenebilirliğini etkili bir şekilde sağlayabilirsiniz. Bu kılavuz, özel veri imzaları oluşturma, QR kodu imzalama seçeneklerini yapılandırma ve belgelerinizi güçlü şifrelemeyle koruma konularında size yol gösterecektir.

**Öğrenecekleriniz:**
- GroupDocs.Signature kullanılarak özel bir veri imza sınıfı nasıl oluşturulur?
- Java uygulamalarında QR kod imzalama seçeneklerini yapılandırma
- Belgeleri QR kodlarıyla imzalama ve özel şifreleme uygulama

Ön koşullara bir göz atalım ve bu işlevselliği projelerinize entegre etmeye başlayalım!

## Ön koşullar

Başlamadan önce, geliştirme ortamınızda gerekli kütüphaneleri ve bağımlılıkları kurduğunuzdan emin olun.

### Gerekli Kitaplıklar ve Sürümler

GroupDocs.Signature for Java'yı uygulamak için aşağıdaki bağımlılığı ekleyin:

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
implementation 'com.groupdocs:groupdocs-signation:23.12'
```

Ayrıca en son sürümü doğrudan şu adresten indirebilirsiniz: [Java sürümleri için GroupDocs.Signature](https://releases.groupdocs.com/signature/java/).

### Ortam Kurulum Gereksinimleri

- Çalışan bir Java Geliştirme Kiti'nin (JDK) yüklü olduğundan emin olun.
- IntelliJ IDEA veya Eclipse gibi Entegre Geliştirme Ortamınızı (IDE) kurun.

### Bilgi Ön Koşulları

- Java programlama ve nesne yönelimli kavramların temel düzeyde anlaşılması.
- Maven veya Gradle kullanarak bağımlılıkları yönetme konusunda bilgi sahibi olmak.

## Java için GroupDocs.Signature Kurulumu

Başlamak için, yukarıdaki kurulum talimatlarını izleyerek GroupDocs.Signature'ı projenize kurun ve yapı yapılandırmanıza ekleyin.

### Lisans Edinme Adımları

GroupDocs farklı lisanslama seçenekleri sunmaktadır:
- **Ücretsiz Deneme**: Tüm özellikleri sınırlama olmaksızın test edin.
- **Geçici Lisans**: Değerlendirme amaçlı lisans alın.
- **Satın almak**:Ticari kullanım için tam lisans satın alın.

İndirdikten sonra GroupDocs.Signature'ı şu şekilde başlatın:

```java
import com.groupdocs.signature.Signature;

class InitializeGroupDocs {
    public static void main(String[] args) {
        Signature signature = new Signature("path/to/your/document");
        // Artık imza nesnesini kullanarak belgelerle çalışmaya başlayabilirsiniz.
    }
}
```

## Uygulama Kılavuzu

Uygulama sürecini yönetilebilir bölümlere ayıralım ve temel özelliklere odaklanalım.

### Özel Veri İmza Sınıfı

#### Genel Bakış
Kimlik, yazar, imzalama tarihi ve ek faktörler gibi imza verilerini depolamak için özel bir sınıf oluşturun. Bu, imzalarınızda gerekli tüm meta verilerin kapsüllenmesini sağlar.

#### Adım Adım Uygulama

**DocumentSignatureData Sınıfını Tanımlayın**

```java
import com.groupdocs.signature.domain.extensions.serialization.FormatAttribute;
import java.util.Date;
import java.math.BigDecimal;

class DocumentSignatureData {
    @FormatAttribute(propertyName = "SignID")
    public String ID; // İmza için benzersiz tanımlayıcı
    
    public String getID() { return ID; }
    public void setID(String value) { ID = value; }
    
    @FormatAttribute(propertyName = "SAuth")
    public final String Author; // Belgenin yazarı
    
    public final String getAuthor() { return Author; }
    public final void setAuthor(String value) { Author = value; }
    
    @FormatAttribute(propertyName = "SDate", propertyFormat = "yyyy-MM-dd")
    public final Date Signed = new Date(); // İmza tarihi ve saati
    
    public final Date getSigned() { return Signed; }
    public final void setSigned(Date value) { Signed = value; }
    
    @FormatAttribute(propertyName = "SDFact", propertyFormat = "N2")
    public final BigDecimal DataFactor = new BigDecimal(0.01); // İmza için ek veri faktörü
    
    public final BigDecimal getDataFactor() { return DataFactor; }
    public final void setDataFactor(BigDecimal value) { DataFactor = value; }
}
```

**Açıklama:**
- **BiçimÖzniteliği**: Serileştirmeyi özelleştirmek için özellikleri açıklar.
- **Özellikler**: Benzersiz kimlik, yazar adı, imzalama tarihi ve veri faktörü gibi temel ayrıntıları yakalayın.

### QR Kod İmza Seçenekleri Yapılandırması

#### Genel Bakış
QR kodlarınızın belgelerde nasıl görüneceğini (boyut, hizalama ve dolgu dahil) tanımlamak için QR kod imzalama seçeneklerini yapılandırın.

#### Adım Adım Uygulama

**QrCodeSignOptionsConfig Sınıfını Tanımlayın**

```java
import com.groupdocs.signature.domain.enums.HorizontalAlignment;
import com.groupdocs.signature.domain.enums.VerticalAlignment;
import com.groupdocs.signature.domain.qrcodes.QrCodeTypes;
import com.groupdocs.signature.domain.Padding;
import com.groupdocs.signature.options.sign.QrCodeSignOptions;

class QrCodeSignOptionsConfig {
    public static QrCodeSignOptions setupQrCodeSignOptions(DocumentSignatureData documentSignature) {
        QrCodeSignOptions options = new QrCodeSignOptions();
        
        // Özel veri nesnesini QR koduna dönüştürün
        options.setData(documentSignature);
        
        // QR kod türünü belirtin
        options.setEncodeType(QrCodeTypes.QR);
        
        // Hizalama için dolguyu yapılandırın
        Padding padding = new Padding();
        padding.setRight(10); // Piksel cinsinden sağ dolgu
        padding.setBottom(10); // Piksel cinsinden alt dolgu
        options.setMargin(padding);
        
        // QR kodunun boyutunu ve konumunu tanımlayın
        options.setHeight(100);
        options.setWidth(100);
        options.setVerticalAlignment(VerticalAlignment.Bottom);
        options.setHorizontalAlignment(HorizontalAlignment.Right);
        
        return options;
    }
}
```

**Açıklama:**
- **QrCodeSignOptions**: QR kodunun boyutu ve konumu dahil olmak üzere nasıl görüntüleneceğini yönetir.
- **Dolgu**Belge içindeki hizalamayı ayarlar.

### QR Kod ve Özel Şifreleme ile Belge İmzalama

#### Genel Bakış
Belgeleri güvenli bir şekilde imzalamak için QR kodlarını ve özel şifrelemeyi birleştirin. Bu, veri bütünlüğünü ve gizliliğini sağlar.

#### Adım Adım Uygulama

**QR Koduyla Belge İmzala**

```java
import com.groupdocs.signature.Signature;
import com.groupdocs.signature.domain.extensions.encryption.IDataEncryption;
import com.groupdocs.signature.exception.GroupDocsSignatureException;

import java.util.UUID;

class SignDocumentWithQRCode {
    public static void signDocument(String filePath, String outputFilePath) throws Exception {
        try {
            Signature signature = new Signature(filePath);

            // Özel XOR şifreleme stratejisi
            IDataEncryption encryption = new CustomXOREncryption();

            // Özel belge imza veri nesnesini yapılandırın
            DocumentSignatureData documentSignature = new DocumentSignatureData();
            documentSignature.setID(UUID.randomUUID().toString());
            documentSignature.setAuthor(System.getenv("USERNAME"));
            documentSignature.setSigned(new Date());
            documentSignature.setDataFactor(new BigDecimal("11.22"));

            // QR Kod seçeneklerini ayarlayın
            QrCodeSignOptions options = QrCodeSignOptionsConfig.setupQrCodeSignOptions(documentSignature);

            // QR kodundaki verilere şifreleme uygulayın
            options.setDataEncryption(encryption);

            // Belgeyi imzalayın ve kaydedin
            signature.sign(outputFilePath, options);
        } catch (Exception e) {
            throw new GroupDocsSignatureException(e.getMessage());
        }
    }
}
```

**Açıklama:**
- **CustomXOREncryption**: QR kod verilerini güvence altına almak için özel bir şifreleme stratejisi uygular.
- **UUID**: Her imza için benzersiz bir tanımlayıcı üretir.