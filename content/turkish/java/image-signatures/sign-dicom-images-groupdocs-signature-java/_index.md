---
"date": "2025-05-08"
"description": "GroupDocs.Signature for Java kullanarak DICOM görüntülerini güvenli bir şekilde nasıl imzalayacağınızı öğrenin. QR kodları ve meta verileri yerleştirerek belge güvenliğini artırın."
"title": "GroupDocs.Signature for Java Kullanarak DICOM Görüntülerini QR Kodları ve Meta Verilerle İmzalama"
"url": "/tr/java/image-signatures/sign-dicom-images-groupdocs-signature-java/"
"weight": 1
---

# GroupDocs.Signature for Java Kullanarak DICOM Görüntülerini QR Kodları ve Meta Verilerle Nasıl İmzalayabilirsiniz?

## giriiş

Hızla gelişen dijital sağlık sektöründe, hasta verilerinin güvenli bir şekilde yönetilmesi büyük önem taşımaktadır. Bu eğitim, GroupDocs.Signature for Java kullanarak Dijital Görüntüleme ve Tıpta İletişim (DICOM) görüntülerini QR kodları ve meta verilerle imzalamak için sağlam bir çözüm uygulamanıza rehberlik edecektir. Bu özellikler, hayati bilgileri doğrudan tıbbi görüntülere yerleştirerek özgünlüğü garanti eder, izlenebilirliği artırır ve uyumluluğu korur.

### Öğrenecekleriniz:
- GroupDocs.Signature for Java'yı projenize nasıl entegre edersiniz?
- DICOM görüntülerinin QR kodlarla imzalanması işlemi.
- Belge güvenliğini artırmak için XMP meta verilerinin eklenmesi.
- DICOM dosyalarındaki imzaların alınması, doğrulanması ve aranması.
- İmzalanmış DICOM görüntülerinin önizlemelerinin oluşturulması.

Hadi başlayalım! Başlamadan önce, sorunsuz bir şekilde takip edebilmeniz için gereken her şeye sahip olduğunuzdan emin olalım.

## Ön koşullar

GroupDocs.Signature özelliklerini etkili bir şekilde uygulamak için aşağıdaki ön koşulları karşıladığınızdan emin olun:

### Gerekli Kitaplıklar ve Bağımlılıklar
- **Java için GroupDocs.Signature**: Bu kütüphanenin 23.12 veya daha sonraki sürümüne ihtiyacınız olacak.

### Ortam Kurulum Gereksinimleri
- **Java Geliştirme Kiti (JDK)**: Sisteminizde JDK'nın kurulu olduğundan emin olun.
- **IDE**: IntelliJ IDEA veya Eclipse gibi Entegre Geliştirme Ortamı kullanın.

### Bilgi Ön Koşulları
Temel bir anlayış:
- Java programlama ve nesne yönelimli prensipler.
- Bağımlılık yönetimi için Maven veya Gradle derleme araçları.

## Java için GroupDocs.Signature Kurulumu

GroupDocs.Signature'ı kullanmaya başlamak için, projenize bir bağımlılık olarak eklemeniz gerekir. Bunu farklı derleme araçlarını kullanarak nasıl yapabileceğiniz aşağıda açıklanmıştır:

### Maven
Aşağıdaki parçacığı ekleyin `pom.xml` dosya:
```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

### Gradle
Bunu da ekleyin `build.gradle` dosya:
```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

### Doğrudan İndirme
Alternatif olarak, en son sürümü şu adresten indirebilirsiniz: [Java sürümleri için GroupDocs.Signature](https://releases.groupdocs.com/signature/java/).

#### Lisans Edinme Adımları
1. **Ücretsiz Deneme**: Sınırlı süreli ücretsiz denemeyle özellikleri deneyin.
2. **Geçici Lisans**Tüm yetenekleri keşfetmek için geçici bir lisans edinin.
3. **Satın almak**: Uzun süreli erişime ihtiyacınız varsa abonelik satın alın.

#### Temel Başlatma ve Kurulum

GroupDocs.Signature'ı başlatmak için bir örnek oluşturun `Signature` sınıf:
```java
import com.groupdocs.signature.Signature;

// İmza nesnesini DICOM dosyanızın yoluyla başlatın
Signature signature = new Signature(filePath);
```

## Uygulama Kılavuzu

### DICOM Görüntüsünün QR Kodu ve Meta Verilerle İmzalanması

#### Genel Bakış
Bu özellik, DICOM görüntülerini QR koduyla imzalamanıza ve XMP meta verilerini eklemenize olanak tanıyarak belge güvenliğini artırır.

#### Adım 1: QR Kod İmzalama Seçeneklerini Ayarlayın
```java
import com.groupdocs.signature.domain.Padding;
import com.groupdocs.signature.domain.enums.HorizontalAlignment;
import com.groupdocs.signature.domain.enums.VerticalAlignment;
import com.groupdocs.signature.domain.signatures.QrCodeSignOptions;

Padding padding = new Padding();
padding.setRight(5);
padding.setLeft(5);

QrCodeSignOptions options = new QrCodeSignOptions("Patient #36363393. R: No-Issues");
options.setAllPages(true);
options.setWidth(100);
options.setHeight(100);
options.setVerticalAlignment(VerticalAlignment.Bottom);
options.setHorizontalAlignment(HorizontalAlignment.Right);
options.setMargin(padding);
```
Burada QR kodunun DICOM görüntüsündeki görünümünü ve konumunu yapılandırıyoruz.

#### Adım 2: XMP Meta Verilerini Ekleyin
```java
import com.groupdocs.signature.options.saveoptions.imagessaveoptions.DicomSaveOptions;
import com.groupdocs.signature.options.saveoptions.imagessaveoptions.DicomXmpEntry;
import com.groupdocs.signature.options.saveoptions.imagessaveoptions.DicomXmpType;

DicomSaveOptions dicomSaveOptions = new DicomSaveOptions();
List<DicomXmpEntry> xmpEntries = new ArrayList<>();
xmpEntries.add(new DicomXmpEntry(DicomXmpType.PatientName, "Patient #4"));
dicomSaveOptions.setXmpEntries(xmpEntries);
```
Bu kod parçası DICOM dosyasına meta veri ekleyerek ek hasta bilgilerini yerleştirir.

#### Adım 3: Belgeyi İmzalayın
```java
String outputFilePath = YOUR_OUTPUT_DIRECTORY + "/SignDicomImageAdvanced/" + fileName;
signature.sign(outputFilePath, options, dicomSaveOptions);
```
The `sign` yöntemi QR kodunu ve meta veriyi DICOM dosyanıza yazar ve belirtilen konuma kaydeder.

### İmzalanmış DICOM Görüntü Bilgilerinin Alınması

#### Genel Bakış
Doğrulama veya denetim amacıyla imzalı bir DICOM görüntüsünden XMP meta verilerini çıkarın.
```java
import com.groupdocs.signature.domain.IDocumentInfo;
import com.groupdocs.signature.domain.signatures.MetadataSignature;

IDocumentInfo documentInfo = signature.getDocumentInfo();
for (MetadataSignature item : documentInfo.getMetadataSignatures()) {
    System.out.println(item.toString());
}
```
Bu kod, DICOM dosyasıyla ilişkili tüm meta veri imzalarını alır ve yazdırır.

### İmzalanmış DICOM'un Doğrulanması

#### Genel Bakış
İmzalanmış DICOM görüntüsünün gerçekliğini teyit etmek için QR kod imzasının mevcut olduğunu doğrulayın.
```java
import com.groupdocs.signature.domain.VerificationResult;
import com.groupdocs.signature.options.verify.QrCodeVerifyOptions;
import com.groupdocs.signature.domain.enums.TextMatchType;

QrCodeVerifyOptions verifyOptions = new QrCodeVerifyOptions();
verifyOptions.setAllPages(true);
verifyOptions.setText("Patient #36363393");
verifyOptions.setMatchType(TextMatchType.Contains);

VerificationResult result = signature.verify(verifyOptions);
if (result.isValid()) {
    System.out.println(filePath + " has successfully verified signatures!");
} else {
    System.out.println(filePath + " failed verification process.");
}
```
Bu doğrulama adımı, QR kodunun beklenen kriterlere uymasını sağlayarak belge bütünlüğünü teyit eder.

### İmzalı DICOM'da İmza Arama

#### Genel Bakış
İmzalanmış bir DICOM görüntüsündeki tüm QR kod imzalarını bulun ve inceleyin veya denetleyin.
```java
import com.groupdocs.signature.domain.signatures.QrCodeSignature;
import java.util.List;

List<QrCodeSignature> signatures = signature.search(QrCodeSignature.class);
for (QrCodeSignature qrCodeSignature : signatures) {
    System.out.println("QRCode signature found at page " +
        qrCodeSignature.getPageNumber() + ": " +
        qrCodeSignature.getEncodeType().getTypeName() + ": " +
        qrCodeSignature.getText());
}
```
Bu özellik, belgedeki tüm QR kod imzalarını tarayarak kapsamlı görünürlük sağlamak için kullanışlıdır.

### İmzalanmış DICOM'un Önizlemesi Oluşturuluyor

#### Genel Bakış
İmzalı DICOM görüntüsünün her sayfası için önizlemeler oluşturun; böylece tüm dosyayı açmadan hızlı görsel incelemeye olanak tanıyın.
```java
import com.groupdocs.signature.options.PreviewOptions;
import java.io.File;
import java.io.FileOutputStream;
import java.nio.file.Paths;

PreviewOptions previewOption = new PreviewOptions(pageNumber -> {
    try {
        String pageFilePath = YOUR_OUTPUT_DIRECTORY + "/SignDicomImageAdvanced/image-" + pageNumber + ".jpg";
        return new FileOutputStream(Paths.get(pageFilePath).toFile());
    } catch (Exception e) {
        throw new RuntimeException(e.getMessage());
    }
});

signature.generatePreview(previewOption);
```
Bu kod parçası, her sayfa için hızlı doğrulama veya paylaşım için yararlı olabilecek resim önizlemeleri oluşturur.

## Pratik Uygulamalar

GroupDocs.Signature for Java, gerçek dünyada birçok uygulama sunmaktadır:
- **Tıbbi Görüntüleme**: QR kodları ve meta verilerle hasta DICOM görüntülerini güvenli bir şekilde imzalayın ve yönetin.
- **Yasal Belge Yönetimi**: Yasal işlemlerde belge gerçekliğini ve uyumluluğunu artırın.
- **Finansal Hizmetler**: Hassas finansal belgelerde güvenli elektronik imzaları uygulayın.