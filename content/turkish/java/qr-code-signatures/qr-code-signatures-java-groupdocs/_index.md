---
"date": "2025-05-08"
"description": "GroupDocs.Signature ile Java'da QR kod imzalarını uygulayıp doğrulayarak belge güvenliğini nasıl artıracağınızı öğrenin. Güvenli bir imzalama süreci için bu adım adım kılavuzu izleyin."
"title": "Belgelerinizi Güvence Altına Alın ve GroupDocs.Signature Kullanarak Java'da QR Kod İmzalarını Uygulayın"
"url": "/tr/java/qr-code-signatures/qr-code-signatures-java-groupdocs/"
"weight": 1
type: docs
---
# Belgelerinizi Güvence Altına Alın: GroupDocs.Signature Kullanarak Java'da QR Kod İmzalarını Uygulayın

Günümüzün dijital dünyasında, sözleşmeler, faturalar veya hassas kişisel bilgiler gibi belgelerin güvenliğini sağlamak hayati önem taşımaktadır. Belge güvenliğini artırmak ve doğrulama süreçlerini basitleştirmek için yenilikçi bir yaklaşım, QR kod imzalarını kullanmaktır. Bu eğitim, GroupDocs.Signature kullanarak Java'da belgeleriniz için QR kod imzalarını uygulama ve doğrulama konusunda size rehberlik edecektir.

## Ne Öğreneceksiniz
- QR Kodları kullanarak belgeler nasıl imzalanır?
- İmzalanmış belgelerin QR Kodları ile doğrulanması
- Bir belge içinde mevcut QR Kod imzalarını arama
- Belgelerinizdeki QR Kod imzalarını güncelleme ve silme

Ortamınızı kuralım ve başlayalım!

### Ön koşullar
Başlamadan önce aşağıdaki ön koşullara sahip olduğunuzdan emin olun:

#### Gerekli Kitaplıklar ve Bağımlılıklar
Java için GroupDocs.Signature'a ihtiyacınız olacak. Maven veya Gradle üzerinden ekleyebilir veya doğrudan indirebilirsiniz.

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

**Doğrudan İndirme**
En son sürümü şu adresten indirin: [Java sürümleri için GroupDocs.Signature](https://releases.groupdocs.com/signature/java/).

#### Ortam Kurulum Gereksinimleri
- Java Development Kit (JDK) 8 veya üzeri sürümünün yüklü olduğundan emin olun.
- IntelliJ IDEA, Eclipse veya NetBeans gibi bir IDE kullanın.

#### Bilgi Ön Koşulları
Java programlama ve belge işleme konusunda temel bir anlayışa sahip olmak faydalıdır.

## Java için GroupDocs.Signature Kurulumu
GroupDocs.Signature'ı projenizde kullanmak için şu adımları izleyin:
1. **Kurulum**: Kurulumunuza bağlı olarak Maven, Gradle veya doğrudan indirme arasında seçim yapın.
2. **Lisans Edinimi**:
   - Ücretsiz deneme sürümüyle başlayın [GroupDocs web sitesi](https://releases.groupdocs.com/signature/java/).
   - Uzun süreli test ve geliştirme için geçici bir lisans almayı düşünün. [Burada](https://purchase.groupdocs.com/temporary-license/).
3. **Temel Başlatma**: 
    GroupDocs.Signature'ı başlatma yöntemi şöyledir:

    ```java
    Signature signature = new Signature("YOUR_DOCUMENT_PATH");
    ```

Bu sizi QR Kod imzalarını uygulamaya hazırlar.

## Uygulama Kılavuzu

### QR Kod İmzasıyla Belgeyi İmzalayın
#### Genel Bakış
QR Kodu kullanarak bir belgeyi imzalamak, dijital imzanızı temsil eden benzersiz bir kodun yerleştirilmesini içerir. Bu işlem, belgeyi güvence altına alır ve daha sonra orijinalliğinin kolayca doğrulanmasını sağlar.

##### Adım 1: İmzalama Seçeneklerinizi Ayarlayın
```java
import com.groupdocs.signature.Signature;
import com.groupdocs.signature.domain.enums.HorizontalAlignment;
import com.groupdocs.signature.domain.enums.VerticalAlignment;
import com.groupdocs.signature.options.sign.QrCodeSignOptions;

Signature signature = new Signature("YOUR_DOCUMENT_PATH");
QrCodeSignOptions signOptions = new QrCodeSignOptions("John Smith", com.groupdocs.signature.domain.qrcodes.QrCodeTypes.QR);

signOptions.setVerticalAlignment(VerticalAlignment.Top);
signOptions.setHorizontalAlignment(HorizontalAlignment.Center);
signOptions.setWidth(100);
signOptions.setHeight(40);
```
**Açıklama**: `QrCodeSignOptions` Belirli bir metin ve hizalama ile bir QR Kodu oluşturmak üzere yapılandırılmıştır. Genişlik ve yüksekliği gerektiği gibi ayarlayın.

##### Adım 2: İmza Görünümünü Özelleştirin
```java
import java.awt.Color;

signOptions.setForeColor(Color.RED); // QR kod rengini ayarla
com.groupdocs.signature.domain.SignatureFont signatureFont = new com.groupdocs.signature.domain.SignatureFont();
signatureFont.setSize(12);
signatureFont.setFamilyName("Comic Sans MS");
signOptions.setFont(signatureFont);
```
**Açıklama**: Yazı tipi ve renginin özelleştirilmesi görsel tanımlamayı kolaylaştırır.

##### Adım 3: Belgeyi İmzalayın
```java
import java.util.ArrayList;
import java.util.List;

List<String> signatureIds = new ArrayList<>();
List<com.groupdocs.signature.domain.BaseSignature> signedSignatures = signature.sign("YOUR_OUTPUT_PATH", signOptions).getSucceeded();

for (com.groupdocs.signature.domain.BaseSignature temp : signedSignatures) {
    signatureIds.add(temp.getSignatureId());
}
```
**Açıklama**: Bu adım belgeyi imzalar ve imza kimliklerini gelecekte referans olması için saklar.

### Belgeyi QR Kod İmzasıyla Doğrulayın
#### Genel Bakış
Doğrulama, bir belgenin yasal olarak imzalandığını garanti eder. Bir belgedeki QR Kod imzasını nasıl doğrulayabileceğiniz aşağıda açıklanmıştır.

##### Adım 1: Doğrulama Seçeneklerini Ayarlayın
```java
import com.groupdocs.signature.Signature;
import com.groupdocs.signature.options.verify.QrCodeVerifyOptions;

Signature signature2 = new Signature("YOUR_OUTPUT_PATH");
QrCodeVerifyOptions verifyOptions = new QrCodeVerifyOptions();

verifyOptions.setEncodeType(QrCodeTypes.QR);
verifyOptions.setText("John Smith"); // Doğrulanacak metin
verifyOptions.setAllPages(false); 
verifyOptions.setPageNumber(1);
```
**Açıklama**:Doğrulama seçenekleri, hangi QR Kod türünü ve metnini arayacağınızı belirleyerek imzanın beklentilerinizle uyumlu olmasını sağlar.

##### Adım 2: Doğrulamayı Gerçekleştirin
```java
boolean isValid = signature2.verify(verifyOptions).isValid();
System.out.println("Is Signature Valid? " + isValid);
```
**Açıklama**: Bu, belgenin kriterlerinizle eşleşen geçerli bir QR Kodu içerip içermediğini kontrol eder.

### QR Kod İmzası için Belgeyi Ara
#### Genel Bakış
Bazen bir belgedeki mevcut imzaları bulmak gerekebilir. GroupDocs.Signature kullanarak bunları nasıl arayabileceğinizi aşağıda bulabilirsiniz.

##### Adım 1: Arama Seçeneklerini Yapılandırın
```java
import com.groupdocs.signature.domain.signatures.QrCodeSignature;
import com.groupdocs.signature.options.search.QrCodeSearchOptions;

Signature signature2 = new Signature("YOUR_OUTPUT_PATH");
QrCodeSearchOptions searchOptions = new QrCodeSearchOptions();
searchOptions.setAllPages(true);
```
**Açıklama**: Bu, aracın tüm sayfaları QR Kod imzaları için taramasını sağlar.

##### Adım 2: Aramayı Çalıştırın
```java
List<QrCodeSignature> signatures = signature2.search(QrCodeSignature.class, searchOptions);

for (QrCodeSignature qrSignature : signatures) {
    System.out.println("Found Signature ID: " + qrSignature.getSignatureId());
}
```
**Açıklama**: Bu, belgede bulunan tüm QR Kod imzalarını alır.

### Belge QR Kod İmzasını Güncelle
#### Genel Bakış
Bir imzayı güncellemek, konum veya boyut gibi özelliklerini değiştirmeyi içerir. İşte nasıl yapılacağı:

##### Adım 1: Güncelleme için İmzaları Hazırlayın
```java
import com.groupdocs.signature.domain.signatures.QrCodeSignature;
import java.io.ByteArrayOutputStream;

Signature signature2 = new Signature("YOUR_OUTPUT_PATH");
List<QrCodeSignature> signaturesToUpdate = new ArrayList<>();

// 'İmzalar'ın aramadan elde edilen QrCodeSignature nesnelerinin bir listesi olduğunu varsayalım
for (QrCodeSignature qrSignature : signatures) {
    qrSignature.setLeft(qrSignature.getLeft() + 100);
    qrSignature.setTop(qrSignature.getTop() + 100);
    qrSignature.setWidth(200);
    qrSignature.setHeight(50);
    signaturesToUpdate.add(qrSignature);
}
```
**Açıklama**: Bu, her imzanın konumunu ve boyutunu ayarlar.

##### Adım 2: Belgeyi Güncelleyin
```java
ByteArrayOutputStream outputStream = new ByteArrayOutputStream();
signature2.update(outputStream, signaturesToUpdate);
```
**Açıklama**: Belge, değiştirilen QR Kod imzalarıyla güncellendi.

### Belge QR-Kod İmzasını Kimliğe Göre Sil
#### Genel Bakış
Artık ihtiyaç duyulmayan veya yanlışlıkla eklenen bir imzayı silmek gerekebilir. Benzersiz kimliğini kullanarak nasıl kaldırabileceğinizi aşağıda bulabilirsiniz.

##### Adım 1: Silinecek İmzaları Belirleyin
```java
import com.groupdocs.signature.domain.SignatureCollection;
import java.util.Arrays;

SignatureCollection signaturesToDelete = signature2.search(QrCodeSignature.class);
Arrays.stream(signaturesToDelete).forEach(signature -> {
    if (signature.getSignatureId().equals("YOUR_SIGNATURE_ID")) {
        signature.delete();
    }
});
```
**Açıklama**: Bu, QR Kod imzasını benzersiz kimliğine göre bulur ve siler.

## Çözüm
Bu kılavuz, Java'da GroupDocs.Signature ile QR kod imzalarını kullanarak belgelerinizi nasıl güvence altına alacağınızı adım adım açıklamaktadır. Bu adımları izleyerek belgelerinizin güvenli bir şekilde imzalanmasını sağlayabilir ve orijinalliğini kolayca doğrulayabilirsiniz.