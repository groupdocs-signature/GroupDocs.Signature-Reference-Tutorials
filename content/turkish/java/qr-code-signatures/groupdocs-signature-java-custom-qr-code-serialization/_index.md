---
"date": "2025-05-08"
"description": "GroupDocs.Signature for Java kullanarak PDF'lerde şifrelemeyle özel QR kod serileştirmenin nasıl uygulanacağını öğrenin. Belgelerinizi etkili bir şekilde güvence altına alın."
"title": "GroupDocs.Signature for Java kullanarak PDF'lerde Özel QR Kodu Serileştirme ve Şifrelemeyi Uygulayın"
"url": "/tr/java/qr-code-signatures/groupdocs-signature-java-custom-qr-code-serialization/"
"weight": 1
type: docs
---
# GroupDocs.Signature for Java Kullanarak PDF'lerde Özel QR Kodu Serileştirme ve Şifreleme Nasıl Uygulanır?

## giriiş

Dijital çağda, veri bütünlüğünü ve gerçekliğini korumak için güvenli belge imzalama olmazsa olmazdır. İşte bu noktada, belgelere imza eklemeyi kolaylaştırmak için tasarlanmış güçlü bir kütüphane olan GroupDocs.Signature for Java devreye girer. Bu eğitim, GroupDocs.Signature for Java kullanarak PDF'lerde şifrelemeli özel QR kod serileştirmesini uygulama konusunda size rehberlik edecektir.

**Öğrenecekleriniz:**
- GroupDocs.Signature for Java nasıl kurulur ve yapılandırılır
- QR kod imzaları için özel serileştirmenin uygulanması
- QR kodunda serileştirilmiş verilerin şifrelenmesi
- Belgelerinizi güvence altına almak için bu özellikleri kullanın

Uygulamaya geçmeden önce, takip etmeniz gereken her şeye sahip olduğunuzdan emin olalım.

### Ön koşullar

Bu eğitimi etkili bir şekilde kullanabilmek için aşağıdaki ön koşulları karşıladığınızdan emin olun:

1. **Gerekli Kütüphaneler ve Bağımlılıklar:**
   - Java sürüm 23.12 veya üzeri için GroupDocs.Signature
   - Bağımlılık yönetimi için Maven veya Gradle (isteğe bağlı)

2. **Ortam Kurulum Gereksinimleri:**
   - Makinenize Java Geliştirme Kiti (JDK) yüklendi
   - Java programlamanın temel bir anlayışı

3. **Bilgi Ön Koşulları:**
   - Java ve nesne yönelimli programlama kavramlarına aşinalık
   - Java'da PDF'lerle çalışma konusunda temel bilgiler

## Java için GroupDocs.Signature Kurulumu

Başlamak için proje ortamınızda GroupDocs.Signature kütüphanesini kurmanız gerekir.

### Maven Kurulumu

Maven kullanıyorsanız, aşağıdaki bağımlılığı ekleyin `pom.xml` dosya:

```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

### Gradle Kurulumu

Gradle kullanıcıları için bu satırı ekleyin `build.gradle` dosya:

```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

### Doğrudan İndirme

Alternatif olarak, en son sürümü doğrudan şu adresten indirebilirsiniz: [Java sürümleri için GroupDocs.Signature](https://releases.groupdocs.com/signature/java/).

#### Lisans Edinme Adımları
- **Ücretsiz Deneme:** Özelliklerini test etmek için öncelikle deneme sürümünü indirin.
- **Geçici Lisans:** İhtiyaç duymanız halinde geçici lisans talebinde bulunarak, ürünü herhangi bir kısıtlama olmadan değerlendirebilirsiniz.
- **Satın almak:** Uzun süreli kullanım için tam lisans satın almayı düşünebilirsiniz.

Kurulum tamamlandıktan sonra projenizde GroupDocs.Signature'ı başlatın:

```java
import com.groupdocs.signature.Signature;

public class SetupGroupDocs {
    public static void main(String[] args) {
        Signature signature = new Signature("YOUR_DOCUMENT_DIRECTORY/sample.pdf");
        // Kodunuz burada...
    }
}
```

## Uygulama Kılavuzu

Şimdi, GroupDocs.Signature for Java ile özel QR kod serileştirme ve şifrelemeyi uygulamaya geçelim.

### QR Kod İmzaları için Özel Serileştirme Sınıfı

#### Genel Bakış

Bu özellik, meta verilerin QR kod imzasına serileştirilmesini işleyen bir sınıfın oluşturulmasını içerir. `DocumentSignatureData` sınıf, kimlik, yazar, imza tarihi ve veri faktörü gibi nitelikleri depolar.

```java
import com.groupdocs.signature.domain.extensions.serialization.FormatAttribute;
import java.math.BigDecimal;
import java.util.Date;

class DocumentSignatureData {
    @FormatAttribute(propertyName = "SignID")
    public String ID;

    public void setID(String value) { 
        this.ID = value; 
    }

    @FormatAttribute(propertyName = "SAuth")
    public String author;

    public void setAuthor(String value) {
        this.author = value;
    }

    @FormatAttribute(propertyName = "SDate", propertyFormat = "yyyy-MM-dd")
    public Date signed = new Date();

    public void setSigned(Date value) {
        this.signed = value;
    }

    @FormatAttribute(propertyName = "SDFact", propertyFormat = "N2")
    public BigDecimal dataFactor = new BigDecimal(0.01);

    public void setDataFactor(BigDecimal value) {
        this.dataFactor = value;
    }
}
```

#### Açıklama
- **Nitelikler:** The `@FormatAttribute` Açıklamalar, her bir niteliğin QR koduna nasıl serileştirileceğini belirtir.
  - **İD**İmza için benzersiz bir tanımlayıcı.
  - **Yazar**: Belgeyi imzalayan kişi.
  - **İmza Tarihi**: Belgenin imzalandığı zaman damgası.
  - **Veri Faktörü**: İmza ile ilişkili ek sayısal veriler.

### Özel Veri Serileştirme ve Şifreleme ile QR Kod İmzası

#### Genel Bakış

Bu bölüm, özel serileştirilmiş veriler ve şifreleme içeren bir QR kodu kullanarak bir belgenin nasıl imzalanacağını göstermektedir.

```java
import com.groupdocs.signature.Signature;
import com.groupdocs.signature.domain.Padding;
import com.groupdocs.signature.domain.enums.HorizontalAlignment;
import com.groupdocs.signature.domain.enums.VerticalAlignment;
import com.groupdocs.signature.domain.extensions.encryption.IDataEncryption;
import com.groupdocs.signature.domain.qrcodes.QrCodeTypes;
import com.groupdocs.signature.exception.GroupDocsSignatureException;
import com.groupdocs.signature.options.sign.QrCodeSignOptions;
import java.io.File;
import java.math.BigDecimal;
import java.util.Date;
import java.util.UUID;

class SignWithQRCodeCustomSerialization {
    String filePath = "YOUR_DOCUMENT_DIRECTORY/sample.pdf"; 
    String outputFilePath = new File("YOUR_OUTPUT_DIRECTORY", "SignedQRCodeCustomSerialization.pdf").getPath();

    public void signDocument() throws Exception {
        Signature signature = new Signature(filePath);

        // Özel şifreleme mantığınızı buraya uygulayın
        IDataEncryption encryption = new CustomXOREncryption();

        DocumentSignatureData documentSignature = new DocumentSignatureData();
        documentSignature.setID(UUID.randomUUID().toString());
        documentSignature.setAuthor(System.getenv("USERNAME")); 
        documentSignature.setSigned(new Date());
        documentSignature.setDataFactor(new BigDecimal("11.22"));

        QrCodeSignOptions options = new QrCodeSignOptions();
        options.setData(documentSignature);
        options.setEncodeType(QrCodeTypes.QR);
        options.setDataEncryption(encryption);

        // Hizalamayı ve görünümü yapılandırın
        options.setHeight(100);
        options.setWidth(100);
        options.setVerticalAlignment(VerticalAlignment.Bottom);
        options.setHorizontalAlignment(HorizontalAlignment.Right);
        
        Padding padding = new Padding();
        padding.setRight(10);
        padding.setBottom(10);
        options.setMargin(padding);

        signature.sign(outputFilePath, options);
    }
}
```

#### Açıklama
- **Özel Şifreleme:** Kendi şifreleme mantığınızı uygulayın `CustomXOREncryption` veya uygulayan başka bir yöntemi kullanın `IDataEncryption`.
- **İmza Seçenekleri:** QR kodunun görünümünü ve hizalamasını yükseklik, genişlik, dolgu vb. seçeneklerle yapılandırın.
- **İmzalama Süreci:** The `signature.sign()` yöntem QR kod imzasını belgeye uygular.

### Sorun Giderme İpuçları

- Tüm bağımlılıkların yapı aracınızda (Maven/Gradle) doğru şekilde yapılandırıldığından emin olun.
- Giriş ve çıkış belgelerinin dosya yollarının doğru olduğunu doğrulayın.
- Özel şifreleme mantığınızın düzgün bir şekilde uygulandığını ve entegre edildiğini onaylayın.

## Pratik Uygulamalar

Bu özelliğin gerçek dünyadaki bazı uygulamaları şunlardır:

1. **Yasal Belge İmzalama:** Gerçekliği garanti altına almak için QR kodlarına gömülü meta verilerle sözleşmeleri güvenli bir şekilde imzalayın.
2. **Fatura İşleme:** Ek güvenlik ve izlenebilirlik için faturalara otomatik olarak şifreli imzalar ekleyin.
3. **Lojistik Takibi:** Gönderi takibi için imzalı belgeleri kullanın, QR kodlarına benzersiz tanımlayıcılar ve zaman damgaları yerleştirin.
4. **Akademik Sertifikalar:** QR kod imzası kullanarak öğrenci bilgilerini dijital sertifikalara güvenli bir şekilde yerleştirin