---
categories:
- Document Signing
- Healthcare Integration
date: '2026-05-16'
description: Java için GroupDocs.Signature kullanarak data matrix PDF oluşturmayı
  ve QR code PDF eklemeyi öğrenin. Sağlık belgeleri imzalama için adım adım rehber.
keywords:
- create data matrix pdf
- add qr code pdf
- HIBC barcode Java
lastmod: '2026-05-16'
linktitle: Java için HIBC PDF İmzalama Rehberi
schemas:
- author: GroupDocs
  dateModified: '2026-05-16'
  description: Learn how to create data matrix PDF and add QR code PDF using GroupDocs.Signature
    for Java. Step‑by‑step guide for healthcare document signing.
  headline: Create Data Matrix PDF with HIBC Barcode in Java
  type: TechArticle
- description: Learn how to create data matrix PDF and add QR code PDF using GroupDocs.Signature
    for Java. Step‑by‑step guide for healthcare document signing.
  name: Create Data Matrix PDF with HIBC Barcode in Java
  steps:
  - name: '**Import the required classes** – these give you access to the signature
      engine and Data Matrix options.'
    text: '**Import the required classes** – these give you access to the signature
      engine and Data Matrix options.'
  - name: '**Instantiate the `Signature` object** with absolute paths for source and
      destination files.'
    text: '**Instantiate the `Signature` object** with absolute paths for source and
      destination files.'
  - name: '**Configure the Data Matrix options** – set the HIBC string, choose `QrCodeTypes.HIBCLICDataMatrix`,
      and define placement coordinates. `QrCodeTypes` enumerates the supported barcode
      formats for HIBC signatures.'
    text: '**Configure the Data Matrix options** – set the HIBC string, choose `QrCodeTypes.HIBCLICDataMatrix`,
      and define placement coordinates. `QrCodeTypes` enumerates the supported barcode
      formats for HIBC signatures.'
  - name: '**Apply the signature** to the PDF.'
    text: '**Apply the signature** to the PDF.'
  - name: '**Dispose of resources** to free file handles and avoid memory leaks.'
    text: '**Dispose of resources** to free file handles and avoid memory leaks.'
  - name: '**Import QR‑specific classes**'
    text: '**Import QR‑specific classes**'
  - name: '**Create and configure QR options** – note the use of `QrCodeTypes.HIBCLICQR`.'
    text: '**Create and configure QR options** – note the use of `QrCodeTypes.HIBCLICQR`.'
  - name: '**Sign the document**'
    text: '**Sign the document**'
  type: HowTo
- questions:
  - answer: Yes, it also supports DOCX, XLSX, PPTX, PNG, JPEG, and TIFF with the same
      barcode‑signing API.
    question: Can GroupDocs.Signature sign file types other than PDF?
  - answer: Verify that your HIBC string follows the exact HIBCC syntax, use the online
      validator, and ensure you’re using the correct `QrCodeTypes` constant for the
      chosen format.
    question: How do I troubleshoot “Invalid barcode content” errors?
  - answer: QR ≈ 4,296 alphanumeric characters, Aztec ≈ 3,832 numeric / 3,067 alphanumeric,
      Data Matrix ≈ 3,116 numeric / 2,335 alphanumeric. Keep codes under 200 characters
      for optimal scan reliability.
    question: What is the maximum data capacity for each HIBC format?
  - answer: Absolutely. Create separate `QrCodeSignOptions` objects with different
      positions and call `signature.sign()` for each. Just ensure they don’t overlap.
    question: Is it possible to embed multiple barcode types in one PDF?
  - answer: No. After the JAR is on the classpath and the license is activated, all
      operations are performed locally.
    question: Do I need an internet connection for signing at runtime?
  type: FAQPage
tags:
- java
- pdf-signing
- hibc
- healthcare
- barcode
- pharmaceutical
title: Java'da HIBC Barkodu ile Data Matrix PDF Oluşturma
type: docs
url: /tr/java/barcode-signatures/sign-pdfs-hibc-lic-codes-groupdocs-java/
weight: 1
---

# HIBC Barkodlu Data Matrix PDF Oluşturma Java'da

İlaç veya sağlık hizmetleri lojistik yazılımı geliştiriyorsanız, muhtemelen kağıt‑tabanlı izleme, kayıp imzalar ve denetim kabuslarıyla karşılaştınız. **Data Matrix PDF Oluşturma**, bir HIBC LIC barkodu gömerek bu sorunları, baskı, tarama ve düzenleyici inceleme sonrası hayatta kalabilen bir müdahale‑kanıtlı, makine‑okunabilir iz sağlayarak çözer. Bu öğreticide, GroupDocs.Signature for Java kullanarak **QR kod PDF ekleme** desteğini ve ayrıca Aztec ve Data Matrix formatlarını nasıl ekleyeceğinizi tam olarak göreceksiniz.

## Hızlı Yanıtlar
- **Java'da HIBC barkodlarını işleyen kütüphane hangisidir?** GroupDocs.Signature for Java.  
- **En kompakt barkod formatı hangisidir?** Data Matrix – küçük etiketler için idealdir.  
- **Aynı PDF'ye hem QR hem de Data Matrix ekleyebilir miyim?** Evet, sadece ayrı `QrCodeSignOptions` oluşturun.  
- **Çalışma zamanında internet bağlantısına ihtiyacım var mı?** Hayır, kütüphane kurulum sonrası tamamen çevrim dışı çalışır.  
- **Hangi Java sürümü önerilir?** Java 11+ üretim‑düzeyi performans için.

## HIBC barkodlu PDF imzalama nedir?
`Signature` sınıfı GroupDocs.Signature for Java içinde bir PDF belgesini temsil eder ve HIBC barkodlarını dijital imzalar olarak gömmek için yöntemler sağlar. Bir PDF'yi HIBC barkodu ile imzalayarak, tedarik zincirinin herhangi bir noktasında taranabilen doğrulanabilir, müdahale‑kanıtlı bir kayıt oluşturursunuz.

## Data Matrix ve QR kodlarını birlikte neden kullanmalısınız?
GroupDocs.Signature **50+ giriş ve çıkış formatını** destekler ve tüm dosyayı belleğe yüklemeden çok sayfalı PDF'leri işleyebilir. Yoğun, küçük alan etiketleri için Data Matrix ve daha geniş belgeler için QR kullanmak, okunabilirlik, veri kapasitesi (QR için 4.296 karaktere kadar) ve baskı‑alan verimliliği açısından en iyi dengeyi sağlar.

## Önkoşullar
- **JDK 11 veya üzeri** (Java 8 çalışır ancak optimal performans için Java 11+ önerilir).  
- **IDE** (IntelliJ IDEA, Eclipse veya Java uzantılarına sahip VS Code gibi).  
- **Maven veya Gradle** bağımlılık yönetimi için (aşağıdaki örnekler).  
- **Örnek PDF** (ör. `sample.pdf`) uygulamayı test etmek için.  
- **Geçerli GroupDocs.Signature lisansı** (geliştirme için ücretsiz deneme, üretim için ücretli lisans).

## GroupDocs.Signature for Java Kurulumu

### Maven Yapılandırması
Add the dependency to your `pom.xml`:

```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

### Gradle Yapılandırması
For Gradle projects, add this to your `build.gradle`:

```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

### Doğrudan İndirme Seçeneği
JAR dosyasını doğrudan [GroupDocs.Signature for Java releases](https://releases.groupdocs.com/signature/java/) adresinden indirebilir ve projenizin sınıf yoluna manuel olarak ekleyebilirsiniz. Bu yaklaşım sınırlı ağ ortamlarında iyi çalışır.

### Lisans Alma
GroupDocs'tan su işaretlerini kaldırmak ve tüm özelliklerin kilidini açmak için ücretsiz deneme veya geçici lisans isteyin. Üretim dağıtımları satın alınmış bir lisans gerektirir.

### Temel Başlatma
`Signature` sınıfı tüm imzalama işlemleri için giriş noktasıdır. PDF'yi yükler, barkodu uygular ve imzalı dosyayı yazar.

```java
import com.groupdocs.signature.Signature;

class InitializeSignature {
    public static void main(String[] args) {
        Signature signature = new Signature("sample.pdf");
        // Proceed with signing operations...
    }
}
```

## HIBC barkodlu Data Matrix PDF nasıl oluşturulur?
Kaynak PDF'nizi yükleyin, Data Matrix formatı için bir `QrCodeSignOptions` nesnesi yapılandırın ve `sign()` metodunu çağırın – bu, uyumlu bir HIBC Data Matrix barkodu gömmek için ihtiyacınız olan tek şeydir. Aşağıdaki adımlar gerekli tam kodu size gösterir. `QrCodeSignOptions`, barkod imzasının tür, içerik, boyut ve konum gibi ayarlarını tanımlar.

1. **Gerekli sınıfları içe aktarın** – bunlar imza motoruna ve Data Matrix seçeneklerine erişim sağlar.  

```java
import com.groupdocs.signature.Signature;
import com.groupdocs.signature.options.sign.QrCodeSignOptions;
import com.groupdocs.signature.domain.qrcodes.QrCodeTypes;
```

2. **`Signature` nesnesini örnekleyin** kaynak ve hedef dosyalar için mutlak yollarla.  

```java
String sourceFilePath = "YOUR_DOCUMENT_DIRECTORY";
String destinFilePath = "YOUR_OUTPUT_DIRECTORY/SignWithHIBCLICQR.pdf";

final Signature signature = new Signature(sourceFilePath);
```

3. **Data Matrix seçeneklerini yapılandırın** – HIBC dizesini ayarlayın, `QrCodeTypes.HIBCLICDataMatrix` seçin ve yerleştirme koordinatlarını tanımlayın. `QrCodeTypes`, HIBC imzaları için desteklenen barkod formatlarını listeler.  

```java
QrCodeSignOptions hibcLic_QR = new QrCodeSignOptions("A123PROD30917/75#422011907#GP293", QrCodeTypes.HIBCLICQR);
hibcLic_QR.setLeft(1); // Set the position from left
hibcLic_QR.setTop(1);   // Set the position from top
hibcLic_QR.setReturnContent(true); // Return content after signing
hibcLic_QR.setReturnContentType(FileType.PNG); // Specify return content type as PNG
```

4. **İmzayı PDF'ye uygulayın**.  

```java
signature.sign(destinFilePath, hibcLic_QR);
```

5. **Kaynakları serbest bırakın** dosya tutucularını serbest bırakmak ve bellek sızıntılarını önlemek için.  

```java
finally {
    if (signature != null) signature.dispose();
}
```

### Tam Çalışan Örnek
İşte tek bir blokta tam akış (yer tutucular, önceki snippet'lerden yapıştıracağınız tam kodu temsil eder):

```java
import com.groupdocs.signature.Signature;
import com.groupdocs.signature.options.sign.QrCodeSignOptions;
import com.groupdocs.signature.domain.qrcodes.QrCodeTypes;

public class HibcQrSigning {
    public static void main(String[] args) {
        String sourceFilePath = "sample.pdf";
        String destinFilePath = "output/SignWithHIBCLICQR.pdf";
        
        Signature signature = null;
        try {
            signature = new Signature(sourceFilePath);
            
            QrCodeSignOptions hibcLic_QR = new QrCodeSignOptions(
                "A123PROD30917/75#422011907#GP293", 
                QrCodeTypes.HIBCLICQR
            );
            hibcLic_QR.setLeft(1);
            hibcLic_QR.setTop(1);
            hibcLic_QR.setReturnContent(true);
            hibcLic_QR.setReturnContentType(FileType.PNG);
            
            signature.sign(destinFilePath, hibcLic_QR);
            System.out.println("PDF signed successfully with HIBC QR code");
            
        } catch (Exception e) {
            System.err.println("Error signing PDF: " + e.getMessage());
            e.printStackTrace();
        } finally {
            if (signature != null) signature.dispose();
        }
    }
}
```

#### Doğrudan cevap (40–70 kelime)
Bir **Data Matrix PDF oluşturmak** için, `Signature`'ı kaynak PDF'nizle örnekleyin, `QrCodeSignOptions`'ı `QrCodeTypes.HIBCLICDataMatrix` olarak ayarlayın ve doğru biçimlendirilmiş bir HIBC dizesi sağlayın, ardından `signature.sign(outputPath, options)` metodunu çağırın. Kütüphane imzalı PDF'yi hedefe yazar, düzeni korur ve barkodu müdahale‑kanıtlı bir imza olarak gömer.

## GroupDocs.Signature kullanarak QR kod PDF nasıl eklenir?
PDF'yi yükleyin, QR formatı için `QrCodeSignOptions` yapılandırın ve `sign()` metodunu çağırın. Bu iki satırlık desen herhangi bir PDF boyutu için çalışır ve QR görüntüsünü optimal okunabilirlik için otomatik ölçeklendirir. `QrCodeSignOptions`, QR barkod imzasını içeriği ve görsel özellikleriyle yapılandırır. Kodu, ayarladığınız koordinatlara göre konumlandırır, mevcut içerikle çakışmadığından ve baskı sonrası taranabilir olduğundan emin olur.

1. **QR‑özel sınıfları içe aktarın**  

```java
QrCodeSignOptions hibcLic_AZ = new QrCodeSignOptions("A123PROD30917/75#422011907#GP293", QrCodeTypes.HIBCLICAztec);
hibcLic_AZ.setLeft(1); // Set the position from left
hibcLic_AZ.setTop(200); // Set the position from top
hibcLic_AZ.setReturnContent(true); // Return content after signing
hibcLic_AZ.setReturnContentType(FileType.PNG); // Specify return content type as PNG
```

2. **QR seçeneklerini oluşturun ve yapılandırın** – `QrCodeTypes.HIBCLICQR` kullanımına dikkat edin.  

```java
signature.sign(destinFilePath, hibcLic_AZ);
```

3. **Belgeyi imzalayın**  

```java
QrCodeSignOptions hibcLic_DM = new QrCodeSignOptions("A123PROD30917/75#422011907#GP293", QrCodeTypes.HIBCLICDataMatrix);
hibcLic_DM.setLeft(1); // Set the position from left
hibcLic_DM.setTop(400); // Set the position from top
hibcLic_DM.setReturnContent(true); // Return content after signing
hibcLic_DM.setReturnContentType(FileType.PNG); // Specify return content type as PNG
```

> **Doğrudan cevap:** `QrCodeSignOptions` içinde `QrCodeTypes.HIBCLICQR` kullanın, HIBC içerik dizesini ayarlayın, kodu `setLeft()` ve `setTop()` ile konumlandırın, ardından `signature.sign(outputPath, options)` metodunu çağırın. QR barkodu anında gömülür, akıllı telefon veya tarayıcı ile yakalamaya hazır.

## Kaçınılması Gereken Yaygın Hatalar

### 1. Kaynakların Serbest Bırakılmasını Unutma
**Yanlış:**  

```java
Signature signature = new Signature("sample.pdf");
signature.sign(destinFilePath, options);
// Oops, no dispose() call
```  

**Düzeltme:** `Signature` kullanımını try‑with‑resources bloğu içinde sarın veya finally bloğunda `close()` metodunu açıkça çağırın.

### 2. Yanlış HIBC Format Dizesi Kullanma
**Yanlış:** “12345” gibi genel dizeler kullanmak.  
**Düzeltme:** HIBCC standardını izleyin (ör. `A123PROD30917/75#422011907#GP293`). [HIBCC online validator](https://www.hibcc.org/) ile doğrulayın.

### 3. Dosya Yollarını Sabit Kodlama
**Yanlış:**  
```java
String sourceFilePath = "C:/Users/John/Documents/test.pdf";
```  

**Düzeltme:** Yolları bir yapılandırma dosyasında veya ortam değişkeninde saklayın ve çalışma zamanında okuyun.

### 4. Barkod Konum Çakışmalarını Görmezden Gelme
Barkodları mevcut metin veya imzalardan uzakta konumlandırın. PDF koordinatlarını (orijin alt‑sol) kullanın ve basılmış bir örnekle test edin.

### 5. Gerçek Tarayıcılarla Test Etmemek
İmzalı PDF'yi yazdırın ve iş akışınızda kullanılan aynı donanımla tarayın. Farklı baskı kalitelerinde okunabilirliği doğrulayın.

## Sağlıkta Pratik Uygulamalar

| Senaryo | Önerilen Barkod | Neden Uygun |
|----------|--------------------|--------------|
| **İlaç dağıtımı** | QR Kodu | Yüksek veri kapasitesi, akıllı telefonlar tarafından yaygın olarak taranır. |
| **Envanter yönetimi** | Data Matrix | Küçük alan, yoğun raf etiketleri için idealdir. |
| **Regülasyon uyumu (FDA 21 CFR Part 11)** | QR + Data Matrix | Çift format yedeklilik ve denetlenebilirlik sağlar. |
| **Medikal cihaz takibi** | Aztec Kodu | Kompakt boyut sınırlı alanlı ambalajlarda çalışır. |

## Performans Düşünceleri ve En İyi Uygulamalar

### Toplu İşleme Deseni
```java
List<String> filesToSign = getFileList();
for (String filePath : filesToSign) {
    Signature signature = null;
    try {
        signature = new Signature(filePath);
        // Sign and save
    } finally {
        if (signature != null) signature.dispose();
    }
}
```

- Her dosya için yeni bir `Signature` örneği oluşturun, böylece bellek kullanımı düşük kalır.  
- Paralel işleme için sabit bir iş parçacığı havuzu (`Executors.newFixedThreadPool(Runtime.getRuntime().availableProcessors() - 1)`) kullanın, ancak her `Signature` tam PDF'yi bellekte tuttuğu için yığın boyutunu izleyin.

### Kütüphaneleri Güncel Tutun
GroupDocs sürümleri işlem hızını **%20**'ye kadar artırır ve yeni HIBC uyumluluk özellikleri ekler. Üç aylık bağımlılık kontrolleri planlayın.

### Şablonları Önbellekleme
Bir PDF şablonunu bir kez yükleyin, her barkod varyantı için klonlayın ve klonları imzalayın. Bu, I/O'yu azaltır ve yüksek hacimli iş akışlarını hızlandırır.

## Sıkça Sorulan Sorular

**S: GroupDocs.Signature PDF dışındaki dosya türlerini imzalayabilir mi?**  
C: Evet, aynı barkod‑imzalama API'siyle DOCX, XLSX, PPTX, PNG, JPEG ve TIFF formatlarını da destekler.

**S: “Geçersiz barkod içeriği” hatalarını nasıl gideririm?**  
C: HIBC dizenizin tam HIBCC sözdizimini izlediğini doğrulayın, çevrimiçi doğrulayıcıyı kullanın ve seçilen format için doğru `QrCodeTypes` sabitini kullandığınızdan emin olun.

**S: Her HIBC formatı için maksimum veri kapasitesi nedir?**  
C: QR ≈ 4.296 alfanümerik karakter, Aztec ≈ 3.832 sayısal / 3.067 alfanümerik, Data Matrix ≈ 3.116 sayısal / 2.335 alfanümerik. Optimum tarama güvenilirliği için kodları 200 karakterin altında tutun.

**S: Tek bir PDF'ye birden fazla barkod türü gömmek mümkün mü?**  
C: Kesinlikle. Farklı konumlarla ayrı `QrCodeSignOptions` nesneleri oluşturun ve her biri için `signature.sign()` metodunu çağırın. Çakışmadıklarından emin olun.

**S: Çalışma zamanında imzalama için internet bağlantısına ihtiyacım var mı?**  
C: Hayır. JAR sınıf yolunda ve lisans etkinleştirildikten sonra tüm işlemler yerel olarak gerçekleştirilir.

## Ek Kaynaklar

- [GroupDocs.Signature for Java Dokümantasyonu](https://docs.groupdocs.com/signature/java/)  
- [API Referans Kılavuzu](https://reference.groupdocs.com/signature/java/)  
- [En Son Sürüm İndirmeleri](https://releases.groupdocs.com/signature/java/)  
- [Lisans Satın Al](https://purchase.groupdocs.com/buy)  
- [Ücretsiz Deneme Al](https://releases.groupdocs.com/signature/java/)  
- [Geçici Lisans İste](https://purchase.groupdocs.com/temporary-license/)  
- [GroupDocs Forum](https://forum.groupdocs.com/c/signature/)

---

**Son Güncelleme:** 2026-05-16  
**Test Edilen Versiyon:** GroupDocs.Signature 23.12 for Java  
**Yazar:** GroupDocs  

```java
signature.sign(destinFilePath, hibcLic_DM);
```

## İlgili Eğitimler

- [Create Barcode Signature PDF in Java – GroupDocs Guide](/signature/java/barcode-signatures/create-sign-pdfs-groupdocs-barcode-java/)
- [Create Barcode Signature in Java – Update PDF Barcodes](/signature/java/barcode-signatures/java-groupdocs-signature-barcode-initialize-update/)
- [How to read QR code PDF using Java and GroupDocs.Signature](/signature/java/barcode-signatures/java-pdf-barcode-search-groupdocs-signature-api/)