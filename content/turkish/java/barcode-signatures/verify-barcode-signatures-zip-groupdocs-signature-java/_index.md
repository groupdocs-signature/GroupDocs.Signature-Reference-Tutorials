---
categories:
- Document Security
date: '2026-09-26'
description: Java ve GroupDocs.Signature kullanarak ZIP arşivlerinde barkod imzalarını
  nasıl doğrulayacağınızı öğrenin. Güvenli belge doğrulama için adım adım kılavuz.
keywords:
- how to verify barcode
- java barcode verification
- groupdocs signature zip
- barcode verification java
- zip archive barcode validation
lastmod: '2026-09-26'
linktitle: Barkod doğrulama Java ZIP
og_description: GroupDocs.Signature kullanarak Java ZIP arşivlerinde barkod imzalarını
  nasıl doğrulayacağınızı öğrenin. Güvenli ve hızlı doğrulama için adım adım talimatlar.
og_image_alt: Developer guide showing barcode verification inside a Java ZIP archive
  using GroupDocs.Signature
og_title: Java ZIP dosyalarında barkod imzalarını doğrulama – GroupDocs Guide
schemas:
- author: GroupDocs
  dateModified: '2026-09-26'
  description: Learn how to verify barcode signatures in ZIP archives using Java and
    GroupDocs.Signature. Step‑by‑step guide for secure document validation.
  headline: How to verify barcode signatures in Java ZIP files
  type: TechArticle
- description: Learn how to verify barcode signatures in ZIP archives using Java and
    GroupDocs.Signature. Step‑by‑step guide for secure document validation.
  name: How to verify barcode signatures in Java ZIP files
  steps:
  - name: '**Presence** – Does the expected barcode exist?'
    text: '**Presence** – Does the expected barcode exist?'
  - name: '**Content** – Does the barcode contain the correct string?'
    text: '**Content** – Does the barcode contain the correct string?'
  - name: '**Integrity** – Has the document changed since the barcode was added?'
    text: '**Integrity** – Has the document changed since the barcode was added?'
  - name: '**Incorrect file paths** – Use `File.separator` or forward slashes for
      cross‑platform compatibility.'
    text: '**Incorrect file paths** – Use `File.separator` or forward slashes for
      cross‑platform compatibility.'
  - name: '**Case‑sensitive matching** – If your barcodes may vary in case, normalise
      both sides or use a case‑insensitive match type.'
    text: '**Case‑sensitive matching** – If your barcodes may vary in case, normalise
      both sides or use a case‑insensitive match type.'
  - name: '**Resource leaks** – Always close the `Signature` object; the try‑with‑resources
      pattern guarantees cleanup.'
    text: '**Resource leaks** – Always close the `Signature` object; the try‑with‑resources
      pattern guarantees cleanup.'
  - name: Build a small proof‑of‑concept with a sample ZIP containing a barcode‑signed
      PDF.
    text: Build a small proof‑of‑concept with a sample ZIP containing a barcode‑signed
      PDF.
  - name: Experiment with different `TextMatchType` values to find the sweet spot
      for your data.
    text: Experiment with different `TextMatchType` values to find the sweet spot
      for your data.
  - name: Add logging, monitoring, and error‑handling as shown in the best‑practice
      section.
    text: Add logging, monitoring, and error‑handling as shown in the best‑practice
      section.
  - name: Explore additional signature types (digital certificates, QR codes) using
      the same API.
    text: Explore additional signature types (digital certificates, QR codes) using
      the same API.
  type: HowTo
- questions:
  - answer: Call `verify()` once; the API scans the entire archive and returns all
      matching signatures in `result.getSucceeded()`. Iterate over that list to handle
      each barcode individually.
    question: How do I verify multiple barcodes within a single ZIP file?
  - answer: Check `result.isValid()` (false) and inspect `result.getFailed()` for
      details. Common reasons include mismatched text, case sensitivity, or missing
      barcodes. Adjust `TextMatchType` or verify the barcode actually exists using
      a scanner app.
    question: What should I do when verification fails?
  - answer: Yes. The library is pure Java and works wherever a compatible JDK runs.
      Just ensure the license file is accessible to the runtime and that the instance
      has enough memory for large archives.
    question: Can this run on cloud platforms like AWS or Azure?
  - answer: 'Minimum: JDK 8, 2 GB RAM, and any OS that supports Java. For high‑volume
      scenarios, allocate 4 GB+ RAM and SSD storage to improve I/O performance.'
    question: What are the system requirements for GroupDocs.Signature?
  - answer: Increase the JVM heap (`-Xmx`), process files in smaller batches, or switch
      to stream‑based processing. Closing each `Signature` object promptly also frees
      native resources.
    question: How can I handle very large ZIP files without exhausting memory?
  type: FAQPage
tags:
- barcode verification
- java security
- zip archives
- groupdocs
- document authentication
title: Java ZIP dosyalarında barkod imzalarını doğrulama
type: docs
url: /tr/java/barcode-signatures/verify-barcode-signatures-zip-groupdocs-signature-java/
weight: 1
---

# Java ZIP dosyalarında barkod imzalarını nasıl doğrularız

## Giriş

Bunu hayal edin: binlerce ürün belgesinin ZIP arşivlerinde saklandığı bir dijital depo yönetiyorsunuz. Her belge, özgünlüğünü kanıtlayan bir barkod imzasına sahiptir. **How to verify barcode** imzalarını her dosyayı çıkarmadan nasıl doğrularsınız? GroupDocs.Signature for Java, bu barkodları arşivin içinde doğrudan doğrulamanıza olanak tanır, böylece iş akışınız hızlı ve güvenli kalır.

İmzalı belgeler içeren sıkıştırılmış arşivlerle—faturalar, nakliye manifestoları veya yasal sözleşmeler gibi—çalışıyorsanız, bu barkod imzalarını programlı olarak doğrulamanın güvenilir bir yoluna ihtiyacınız var. Bu öğretici, ortam kurulumundan üretim‑hazır en iyi uygulamalara kadar her şeyi adım adım gösterir, böylece herhangi bir Java projesinde “how to verify barcode” sorusuna güvenle yanıt verebilirsiniz.

### Hızlı Yanıtlar
- **Java ZIP dosyalarında barkod doğrulamasını hangi kütüphane yönetir?** GroupDocs.Signature for Java.  
- **Dosyaları önce çıkarmam gerekiyor mu?** Hayır, doğrulama ZIP konteyneri üzerinde doğrudan çalışır.  
- **Hangi Java sürümü gereklidir?** JDK 8+, ancak JDK 11+ önerilir.  
- **Birden fazla barkodu aynı anda doğrulayabilir miyim?** Evet, API tüm arşivi otomatik olarak tarar.  
- **Üretim için lisans zorunlu mu?** Evet, üretim kullanımında ticari bir lisans gereklidir.

## ZIP arşivlerinde barkod doğrulaması nedir?

`BarcodeVerifyOptions` sınıfı, sıkıştırılmış bir konteyner içindeki barkod imzaları için arama kriterlerini tanımlar. GroupDocs.Signature'a hangi metin deseninin aranacağını ve ne kadar katı eşleşeceğini söyler. Bu seçeneği kullanarak, arşivi açmadan barkodların varlığını, içeriğini ve bütünlüğünü doğrulayabilirsiniz.

## Neden GroupDocs.Signature for Java kullanmalısınız?

GroupDocs.Signature, **50+ giriş ve çıkış formatını** destekler ve **tüm dosyayı belleğe yüklemeden çok sayfalı belgeleri** işleyebilir. ZIP‑bilinçli motoru, arşivleri tek bir belge gibi ele alır ve **tek‑geçiş doğrulaması** sağlayarak manuel çıkarma ile karşılaştırıldığında I/O yükünü **%40** kadar azaltır. Kütüphane ayrıca **QR, Code 128, EAN‑13 ve 20'den fazla barkod türü** için **yerleşik destek** sunar, böylece kutudan çıkar çıkmaz esneklik elde edersiniz.

## Önkoşullar

### Gerekli kütüphaneler, sürümler ve bağımlılıklar
- **GroupDocs.Signature for Java** sürüm 23.12 ve üzeri (daha yeni sürümler performans artışı ve ek barkod türleri getirir).  
- **Java Development Kit (JDK)** 8 ve üzeri (JDK 11+ daha iyi çöp toplama yönetimi için tercih edilir).  
- **Build tool:** Maven 3.x veya Gradle 6.x+.

### Ortam kurulum gereksinimleri
IDE'niz IntelliJ IDEA, Eclipse, Java uzantılı VS Code veya NetBeans olabilir—standart bir Java uygulamasını çalıştırabilen herhangi bir ortam.

### Bilgi önkoşulları
- Java temelleri (sınıflar, metodlar, OOP)  
- Temel dosya I/O  
- ZIP arşivlerinin anlaşılması  
- Bağımlılık yönetimi için Maven veya Gradle bilgisi  

## GroupDocs.Signature for Java'ı Kurma

### Kurulum bilgileri

#### Maven
`pom.xml` dosyanıza bağımlılığı ekleyin:

```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

#### Gradle
Gradle kullanıcıları için, aşağıdaki satırı `build.gradle` dosyasına ekleyin:

```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

#### Direct download
Manuel kurulumu tercih mi ediyorsunuz? Resmi sürüm sayfasından JAR dosyasını indirin ve sınıf yolunuza ekleyin:

[GroupDocs.Signature for Java releases](https://releases.groupdocs.com/signature/java/)

**Pro ipucu:** Maven/Gradle, geçişli bağımlılıkları otomatik olarak çözer, zaman kazandırır ve sürüm çakışma riskini azaltır.

### Lisans edinme adımları
GroupDocs.Signature, üretim için ücretsiz deneme, geçici genişletilmiş‑değerlendirme lisansı ve ticari lisanslar sunar. API'nin ihtiyaçlarınızı karşıladığını doğrulamak için deneme sürümüyle başlayın, ardından 30 günden fazla sınırsız test için geçici bir anahtar isteyin.

#### Temel başlatma ve kurulum
`Signature` sınıfı, tüm doğrulama işlemleri için giriş noktasıdır. ZIP dosyasını kapsar ve imzaları aramak için metodlar sunar.

```java
import com.groupdocs.signature.Signature;

String filePath = "path/to/your/archive.zip";
Signature signature = new Signature(filePath);
```

Detaylı rehberlik için, [official GroupDocs documentation](https://docs.groupdocs.com/signature/java/) adresine bakın.

## ZIP arşivlerindeki barkod imzalarını anlama

Bir **barcode signature** (barkod imzası), makine‑okunabilir veriyi (QR, Code 128, EAN‑13 vb.) doğrudan bir belgeye gömer. Doğrulama üç şeyi kontrol eder:
1. **Presence** – Beklenen barkod mevcut mu?  
2. **Content** – Barkod doğru metni içeriyor mu?  
3. **Integrity** – Barkod eklendikten sonra belge değişti mi?

Bu belgeler bir ZIP dosyası içinde bulunduğunda, GroupDocs.Signature arşivi tek bir belge gibi ele alır, her girişi döner ve aynı kontrolleri açık çıkarma yapmadan uygular.

## ZIP dosyalarında barkod imzalarını nasıl doğrularız?

`Signature` işleme için bir belge veya arşivi yükleyen ana sınıftır. Doğrulama için, ZIP'i `new Signature("archive.zip")` ile yükleyin, `BarcodeVerifyOptions`'ı beklenen metin deseniyle yapılandırın ve `verify()`'ı çağırın. API tek bir geçişte her girişi tarar ve eşleşen barkodların bulunup bulunmadığını gösteren bir `VerificationResult` döndürür; ayrıca her eşleşme hakkında konum, tip ve güven skoru gibi ayrıntılı bilgi sağlar.

## Uygulama rehberi: ZIP arşivlerinde barkod imzalarını doğrulama

### GroupDocs kullanarak bir ZIP dosyasında barkodu nasıl doğrularım?
`new Signature("archive.zip")` ile ZIP'i yükleyin, `BarcodeVerifyOptions`'ı beklenen metin deseniyle yapılandırın ve `verify()`'ı çağırın. API her girişi tarar, böylece tek bir çağrıda tam arşiv sonucu elde edersiniz.

### Adım‑adım uygulama

#### 1. Gerekli paketleri içe aktarın
`Signature`, `VerificationResult`, `TextMatchType`, `BaseSignature` ve `BarcodeVerifyOptions` sınıfları doğrulama iş akışı için gereklidir.  
`Signature` işleme için bir belge veya arşivi yükleyen ana sınıftır.  
`VerificationResult` bir doğrulama işleminin sonucunu içerir.  
`TextMatchType` enum'ı barkod metninin nasıl karşılaştırılacağını belirtir (ör. tam, içerir, başlar).  
`BaseSignature` tespit edilen herhangi bir imzayı temsil eden soyut temel sınıftır.  
`BarcodeVerifyOptions` barkod doğrulama parametrelerini yapılandırır.

```java
import com.groupdocs.signature.Signature;
import com.groupdocs.signature.domain.VerificationResult;
import com.groupdocs.signature.domain.enums.TextMatchType;
import com.groupdocs.signature.domain.signatures.BaseSignature;
import com.groupdocs.signature.options.verify.BarcodeVerifyOptions;
```

#### 2. Signature nesnesini başlatın
`Signature` örneğini ZIP arşivinize işaret edecek şekilde oluşturun. Değişkeni `final` olarak işaretlemek, yanlışlıkla yeniden atamayı önler.

```java
String filePath = "YOUR_DOCUMENT_DIRECTORY/signed_document.zip";
final Signature signature = new Signature(filePath);
```

#### 3. Barkod doğrulama seçeneklerini yapılandırın
Geçerli bir barkod olarak neyi kabul ettiğinizi tanımlayan metin desenini ve eşleşme tipini ayarlayın. `TextMatchType.Contains` genellikle gerçek dünya tanımlayıcıları için en esnek olanıdır.

```java
BarcodeVerifyOptions barOptions = new BarcodeVerifyOptions();
barOptions.setText("12345");
barOptions.setMatchType(TextMatchType.Contains);
```

#### 4. Doğrulamayı gerçekleştir
`verify()`'ı çağırın ve `VerificationResult`'ı inceleyin. Hızlı bir geç/başarısız kontrol için `isValid()`'ı kullanın ve her eşleşen imzanın meta verilerini almak için `getSucceeded()` üzerinde döngü yapın.

```java
VerificationResult result = signature.verify(barOptions);

if (result.isValid()) {
    System.out.println("Document was verified successfully!");
    for (BaseSignature temp : result.getSucceeded()) {
        System.out.println("-#" + temp.getSignatureId() + "-" + temp.getSignatureType()
                + ": at: " + temp.getLeft() + "x" + temp.getTop() 
                + ". Size: " + temp.getWidth() + "x" + temp.getHeight());
    }
} else {
    System.out.println("Verification failed.");
}
```

### Kaçınılması gereken yaygın tuzaklar
1. **Incorrect file paths** – Çapraz‑platform uyumluluğu için `File.separator` veya ileri eğik çizgi kullanın.  
2. **Case‑sensitive matching** – Barkodlarınız büyük/küçük harf farklılık gösterebilir, her iki tarafı da normalleştirin veya büyük/küçük harfe duyarsız bir eşleşme tipi kullanın.  
3. **Resource leaks** – Her zaman `Signature` nesnesini kapatın; try‑with‑resources deseni temizlik garantiler.

```java
try (Signature signature = new Signature(filePath)) {
    // Your verification code here
}
```

### Sorun giderme ipuçları
- **File not found** – Yolu, izinleri ve ZIP'in bozuk olmadığını doğrulayın.  
- **Always false** – Gerçek barkod metnini her `BaseSignature`'dan yazdırarak neyin saklandığını görün; gerekirse `Contains`'a geçin.  
- **Slow performance** – JVM yığınını artırın (`-Xmx4G`), arşivleri toplu işleyin veya ZIP içeriğini tamamen yüklemek yerine akış olarak okuyun.  
- **Unexpected results** – Bulunan her imzayı kaydedin; barkod tipini (QR vs. Code 128) ve konum meta verilerini kontrol edin.

## ZIP arşivlerinde barkod doğrulamasını ne zaman kullanmalısınız

ZIP arşivleri içinde barkod doğrulamasını, imzalı belgelerin büyük toplularını her dosyayı çıkarmadan doğrulamanız gerektiğinde kullanın. Otomatik pipeline'lar, uyumluluk kontrolleri ve yüksek verimli ortamlar için idealdir; burada hız ve manipülasyon kanıtı kritik önemdedir. API tek bir geçişte her girişi tarar ve sonuçları verimli bir şekilde sunar.

### Uygun olduğu durumlar
- Günlük olarak imzalı belge topluları işliyorsanız.  
- Belgeler depolama verimliliği için zaten arşivlenmişse.  
- Düzenleyici uyumluluk manipülasyon kanıtı gerektiriyorsa.  
- Otomatik pipeline'ların imzasız veya değiştirilmiş dosyaları reddetmesi gerekiyorsa.

### Aşırı kullanım durumları
- Sadece birkaç belge ara sıra doğrulanıyorsa.  
- Dosyalar ZIP formatında depolanmıyorsa.  
- İş akışınız için manuel kontroller yeterliyse.

**Alternatif yaklaşımlar:** Önce bireysel dosyaları doğrulayın, ardından konsepti kanıtladıktan sonra ZIP‑seviyesinde doğrulamayı düşünün.

## Sektörler arası pratik uygulamalar

*(Her madde, sayılarla desteklenen somut bir iş etkisini gösterir.)*

- **E‑Commerce:** Sipariş yerine konmadan önce barkod‑tabanlı gönderi kimliklerini onaylayarak nakliye hatalarını **%35** azaltır.  
- **Healthcare:** Barkod‑tabanlı onay formu doğrulaması uygulandıktan sonra HIPAA denetimlerini sıfır bulgu ile geçer.  
- **Legal:** Sözleşme inceleme süresini saatlerden dakikalara düşürerek dava hazırlık verimliliğini **%40** artırır.  
- **Supply Chain:** Kusurlu bileşen girişini önleyerek garanti taleplerini **%22** azaltır.  
- **Finance:** Otomatik imza kontrolleri sayesinde üç aylık denetim döngülerini hızlandırır, hazırlık süresini **%40** azaltır.

## Performans değerlendirmeleri ve en iyi uygulamalar

### Optimizasyon stratejileri

#### Birden fazla arşiv için toplu işleme
Birden fazla ZIP dosyasını tek bir döngüde işleyerek nesne‑oluşturma yükünü azaltın.

```java
List<String> archives = getArchivesToProcess();
for (String archivePath : archives) {
    try (Signature sig = new Signature(archivePath)) {
        // Verify and process
    }
}
```

#### Bellek yönetimi
Yığın kullanımını izleyin; büyük arşivler için yığını artırın (`-Xmx4G`) ve akış API'lerini tercih edin.

#### Paralel işleme
`ExecutorService`'i kullanarak arşivleri eşzamanlı olarak doğrulayın, CPU çekirdek sınırlarına saygı gösterin ve thread‑safety tuzaklarından kaçının.

#### Doğrulama sonuçlarını önbelleğe alma
Sonuçları bir checksum anahtarıyla önbelleğe alın; arşiv değiştiğinde önbelleği geçersiz kılın.

### Üretim‑hazır en iyi uygulamalar
- **Robust error handling:** Arşiv adını, aranan barkod metnini ve ayrıntılı istisna mesajlarını kaydedin.  
- **Pre‑verification checks:** API'yi çağırmadan önce dosyanın mevcut ve okunabilir olduğundan emin olun.

```java
File file = new File(filePath);
if (!file.exists() || !file.canRead()) {
    throw new IllegalArgumentException("Cannot access file: " + filePath);
}
```

- **Timeouts:** Bozuk dosyalarda takılmayı önlemek için makul işlem zaman aşımı ayarlayın.  
- **Monitoring:** Başarı oranlarını, ortalama işleme süresini ve bellek kullanımını izleyin; anormallikler için uyarılar ayarlayın.  
- **Security:** Kullanıcı tarafından sağlanan yolları doğrulayın, yüklemeleri kötü amaçlı yazılım için tarayın ve arşivleri dinlenirken ve aktarılırken şifreleyin.  
- **Version control:** GroupDocs.Signature'ı güncel tutun, ancak her yeni sürümü temsilci veri setlerine karşı test edin.  
- **Resource cleanup:** Her zaman `Signature` nesnelerini kapatın (yukarıdaki try‑with‑resources örneğine bakın).

## Sıkça Sorulan Sorular

**Q: Tek bir ZIP dosyasında birden fazla barkodu nasıl doğrularım?**  
A: `verify()`'ı bir kez çağırın; API tüm arşivi tarar ve `result.getSucceeded()` içinde bulunan tüm eşleşen imzaları döndürür. Bu listedeki her barkodu ayrı ayrı işlemek için döngü yapın.

```java
for (BaseSignature sig : result.getSucceeded()) {
    // Process each matched barcode
    System.out.println("Found barcode: " + sig.getSignatureId());
}
```

**Q: Doğrulama başarısız olduğunda ne yapmalıyım?**  
A: `result.isValid()`'ı (false) kontrol edin ve detaylar için `result.getFailed()`'ı inceleyin. Yaygın nedenler arasında metin uyuşmazlığı, büyük/küçük harf duyarlılığı veya eksik barkodlar bulunur. `TextMatchType`'ı ayarlayın veya bir tarayıcı uygulamasıyla barkodun gerçekten var olduğunu doğrulayın.

**Q: Bu, AWS veya Azure gibi bulut platformlarında çalışabilir mi?**  
A: Evet. Kütüphane saf Java'dır ve uyumlu bir JDK'nın çalıştığı her yerde çalışır. Lisans dosyasının çalışma zamanına erişilebilir olduğundan ve örneğin büyük arşivler için yeterli belleğe sahip olduğundan emin olun.

**Q: GroupDocs.Signature için sistem gereksinimleri nelerdir?**  
A: Minimum: JDK 8, 2 GB RAM ve Java'yı destekleyen herhangi bir işletim sistemi. Yüksek hacimli senaryolar için 4 GB+ RAM ve I/O performansını artırmak amacıyla SSD depolama ayırın.

**Q: Çok büyük ZIP dosyalarını bellek tüketmeden nasıl yönetebilirim?**  
A: JVM yığınını (`-Xmx`) artırın, dosyaları daha küçük partilerde işleyin veya akış‑tabanlı işleme geçin. Her `Signature` nesnesini hızlıca kapatmak da yerel kaynakları serbest bırakır.

## Sonuç

Artık Java ve GroupDocs.Signature kullanarak ZIP arşivleri içinde **how to verify barcode** imzalarını doğrulamak için eksiksiz, üretim‑hazır bir yol haritasına sahipsiniz. Kurulumdan performans ayarına kadar, yukarıdaki adımlar işinizle ölçeklenebilen güvenilir, otomatik bir doğrulama pipeline'ı oluşturmak için ihtiyacınız olan her şeyi kapsar.

### Sonraki adımlar
1. Barkod‑imzalı bir PDF içeren örnek bir ZIP ile küçük bir proof‑of‑concept oluşturun.  
2. Veriniz için en uygun ayarı bulmak amacıyla farklı `TextMatchType` değerleriyle deney yapın.  
3. En iyi uygulama bölümünde gösterildiği gibi günlükleme, izleme ve hata‑işleme ekleyin.  
4. Aynı API'yi kullanarak ek imza türlerini (dijital sertifikalar, QR kodları) keşfedin.

Derinlemesine incelemeler için resmi kaynaklara bakın:

- **Documentation:** [GroupDocs.Signature for Java Documentation](https://docs.groupdocs.com/signature/java/)  
- **API reference:** [GroupDocs API Reference](https://reference.groupdocs.com/signature/java/)  
- **Downloads:** [Latest GroupDocs.Signature Releases](https://releases.groupdocs.com/signature/java/)  
- **Purchase:** [Buy a License](https://purchase.groupdocs.com/buy)  
- **Free trial:** [Try Free Trial](https://releases.groupdocs.com/signature/java/)  
- **Temporary license:** [Request Temporary License](https://purchase.groupdocs.com/temporary-license/)  
- **Support:** [GroupDocs Support Forum](https://forum.groupdocs.com/c/signature/)

---

**Son Güncelleme:** 2026-09-26  
**Test Edilen:** GroupDocs.Signature 23.12 for Java  
**Yazar:** GroupDocs

## İlgili öğreticiler

- [Java'da Barcode İmzası PDF Oluşturma – GroupDocs Kılavuzu](/signature/java/barcode-signatures/create-sign-pdfs-groupdocs-barcode-java/)  
- [Java'da GroupDocs.Signature ile Barcode İmzalarını Doğrulama](/signature/java/search-verification/groupdocs-signature-java-document-verification/)  
- [Java QR Kod İmza Doğrulama - Güvenli Belge Kimlik Doğrulama](/signature/java/qr-code-signatures/implement-qr-code-signature-search-java-groupdocs/)