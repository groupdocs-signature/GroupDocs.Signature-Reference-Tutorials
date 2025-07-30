---
"date": "2025-05-08"
"description": "GroupDocs.Signature for Java ile QR kod şifrelemesi ve dijital imzalar kullanarak PDF'leri nasıl güvence altına alacağınızı öğrenin. Belge güvenliğinizi etkili bir şekilde artırın."
"title": "GroupDocs.Signature Kullanarak Java'da QR Kod Şifrelemesiyle Güvenli PDF İmzalamayı Uygulama"
"url": "/tr/java/qr-code-signatures/secure-pdf-signing-qr-code-groupdocs-java/"
"weight": 1
---

# GroupDocs.Signature Kullanarak Java'da QR Kod Şifrelemesiyle Güvenli PDF İmzalama Nasıl Uygulanır?

Günümüzün dijital çağında, belgelerdeki hassas bilgilerin güvenliği son derece önemlidir. Siber tehditlerin artışı, veri şifrelemesini belge yönetiminin vazgeçilmez bir parçası haline getirmiştir. Bu eğitim, GroupDocs.Signature for Java ile QR kod şifrelemesi kullanarak güvenli PDF imzalamayı uygulama konusunda size rehberlik edecektir. Bu makalenin sonunda, güçlü güvenlik özelliklerini uygulamalarınıza entegre edebilecek donanıma sahip olacaksınız.

## Öğrenecekleriniz:
- Java'da simetrik veri şifrelemesini anlama
- Özel bir imza sınıfı oluşturma
- QR kod imzalarını özel veriler ve hizalama ile yapılandırma
- Güvenli PDF imzalama için GroupDocs.Signature'ı entegre etme

Dalmaya hazır mısınız? Hadi başlayalım!

## Ön koşullar
Başlamadan önce aşağıdakilere sahip olduğunuzdan emin olun:
- **Java Geliştirme Kiti (JDK):** Sürüm 8 veya üzeri.
- **Maven veya Gradle:** Bağımlılık yönetimi için. Proje kurulumunuza göre seçim yapın.
- **Java Programlama Bilgisi:** Java'da nesne yönelimli programlamanın temel anlayışı.

## Java için GroupDocs.Signature Kurulumu
GroupDocs.Signature'ı kullanmaya başlamak için projenize bağımlılık olarak eklemeniz gerekir. Bu kütüphane, dijital imzaları ve belge şifrelemesini yönetmek için güçlü araçlar sunar.

### Maven Kurulumu
Aşağıdaki bağımlılığı ekleyin `pom.xml` dosya:
```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

### Gradle Kurulumu
Gradle kullanıcıları için bunu ekleyin `build.gradle` dosya:
```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

### Doğrudan İndirme
Alternatif olarak, en son sürümü şu adresten indirin: [Java sürümleri için GroupDocs.Signature](https://releases.groupdocs.com/signature/java/).

### Lisans Edinimi
Özelliklerini değerlendirmek için GroupDocs.Signature'ın ücretsiz deneme sürümünü kullanabilirsiniz. Uzun süreli kullanım için lisans satın almayı veya web siteleri üzerinden geçici lisans başvurusunda bulunmayı düşünebilirsiniz.

## Uygulama Kılavuzu
Bu kılavuz, veri şifreleme, özel imza oluşturma ve QR kod imza yapılandırmasını kapsayan temel bölümlere ayrılmıştır.

### Simetrik Algoritma ile Veri Şifreleme
Verilerinizi şifrelemek, aktarım ve depolama sırasında güvenli kalmalarını sağlar. GroupDocs.Signature kullanarak simetrik şifrelemeyi nasıl kuracağınız aşağıda açıklanmıştır:

#### Simetrik Şifrelemeyi Ayarlama
1. **Gerekli Paketleri İthal Edin:**
   ```java
   import com.groupdocs.signature.domain.extensions.encryption.IDataEncryption;
   import com.groupdocs.signature.domain.extensions.encryption.SymmetricAlgorithmType;
   import com.groupdocs.signature.domain.extensions.encryption.SymmetricEncryption;
   ```
2. **Şifreleme Nesnesini Başlatın:**
   Şifreleme için güvenli bir anahtar ve tuz kullanın. Değiştirin `"YOUR_SECURE_KEY"` kendi anahtarlarınızla.
   ```java
   String key = "YOUR_SECURE_KEY";
   String salt = "YOUR_SECURE_SALT";

   IDataEncryption encryption = new SymmetricEncryption(
       SymmetricAlgorithmType.Rijndael, 
       key, 
       salt
   );
   ```
   - **SimetrikAlgoritmaTürü.Rijndael:** Bu, kullanılacak simetrik algoritmanın türünü belirtir.
   - **Anahtar ve Tuz:** Bunların uygulamanız için benzersiz ve güvenli olduğundan emin olun.

### Özel Veri İmza Sınıfı
Özel bir sınıf oluşturmak, imza özelliklerini etkili bir şekilde yönetmenizi sağlar. İşte nasıl:

#### Tanımlama `DocumentSignatureData` Sınıf
```java
class DocumentSignatureData {
    private String ID;
    private String Author;
    private Date Signed = new Date();
    private BigDecimal DataFactor = new BigDecimal(0.01);

    public String getID() { return ID; }
    public void setID(String value) { ID = value; }

    public final String getAuthor() { return Author; }
    public final void setAuthor(String value) { Author = value; }

    public final Date getSigned() { return Signed; }
    public final void setSigned(Date value) { Signed = value; }

    public final BigDecimal getDataFactor() { return DataFactor; }
    public final void setDataFactor(BigDecimal value) { DataFactor = value; }
}
```
- **Kimlik, Yazar, İmza:** Bu alanlar imzanın meta verilerini depolar.
- **VeriFaktörü:** Uygulamanızın mantığıyla ilgili sayısal bir değer tutar.

### QR Kod İmza Seçenekleri
QR kodları, bilgileri yerleştirmenin kompakt bir yolunu sunar. Bunları özel veriler ve şifrelemeyle yapılandırın:

#### QR Kod İmzalarının Ayarlanması
1. **Başlat `Signature` Nesne:**
   ```java
   import com.groupdocs.signature.Signature;
   
   Signature signature = new Signature("YOUR_DOCUMENT_DIRECTORY");
   ```
2. **QR Kod Seçeneklerini Yapılandırın:**
   ```java
   import com.groupdocs.signature.domain.qrcodes.QrCodeTypes;
   import com.groupdocs.signature.options.sign.QrCodeSignOptions;
   import java.util.UUID;

   DocumentSignatureData documentSignature = new DocumentSignatureData();
   documentSignature.setID(UUID.randomUUID().toString());
   documentSignature.setAuthor(System.getenv("USERNAME"));
   documentSignature.setDataFactor(new BigDecimal("11.22"));

   QrCodeSignOptions options = new QrCodeSignOptions();
   options.setData(documentSignature);
   options.setEncodeType(QrCodeTypes.QR);
   options.setDataEncryption(encryption); // Şifreleme nesnesini kullan
   options.setHeight(100);
   options.setWidth(100);
   options.setVerticalAlignment(com.groupdocs.signature.domain.enums.VerticalAlignment.Bottom);
   options.setHorizontalAlignment(com.groupdocs.signature.domain.enums.HorizontalAlignment.Right);

   import com.groupdocs.signature.domain.Padding;
   Padding padding = new Padding();
   padding.setRight(10);
   padding.setBottom(10);
   options.setMargin(padding);
   ```
   - **Kodlama Türü:** QR kod formatını belirtir.
   - **Hizalama ve Kenar Boşluğu:** QR kodunun belgede nasıl görüneceğini özelleştirin.

### Örnek Kullanım
Yapılandırdığınız seçeneklerle bir belgeyi imzalamak için:
```java
signature.sign("YOUR_OUTPUT_DIRECTORY/QRCodeEncryptedObject.pdf\