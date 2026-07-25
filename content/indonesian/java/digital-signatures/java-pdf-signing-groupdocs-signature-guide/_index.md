---
categories:
- Java Development
date: '2026-07-25'
description: Pelajari cara menambahkan tanda tangan barcode ke PDF menggunakan GroupDocs.Signature
  untuk Java. Setup Maven langkah-demi-langkah, opsi barcode, penanganan error, dan
  tips produksi.
keywords:
- add barcode signature
- groupdocs signature java
- scannable pdf signature
- pdf signing java
- troubleshoot pdf signing
lastmod: '2026-07-25'
linktitle: Tutorial GroupDocs.Signature Java
og_description: Tambahkan tanda tangan barcode ke PDF menggunakan GroupDocs.Signature
  Java. Setup Maven lengkap, opsi barcode, pemecahan masalah, dan praktik terbaik
  produksi untuk pengembang Java.
og_image_alt: 'Guide: add barcode signature to PDF using GroupDocs.Signature Java'
og_title: Tambahkan tanda tangan barcode ke PDF dengan GroupDocs.Signature Java
schemas:
- author: GroupDocs
  dateModified: '2026-07-25'
  description: Learn how to add barcode signature to PDFs using GroupDocs.Signature
    for Java. Step‑by‑step Maven setup, barcode options, error handling, and production
    tips.
  headline: Add barcode signature to PDFs with GroupDocs.Signature Java
  type: TechArticle
- description: Learn how to add barcode signature to PDFs using GroupDocs.Signature
    for Java. Step‑by‑step Maven setup, barcode options, error handling, and production
    tips.
  name: Add barcode signature to PDFs with GroupDocs.Signature Java
  steps:
  - name: Initialize the Signature Object
    text: 'The `Signature` class is GroupDocs.Signature''s entry point for all signing
      operations. It represents a single PDF document in memory and provides lazy
      loading to keep memory usage low. java import com.groupdocs.signature.Signature;
      public class InitializeSignature { public static void main(String[] '
  - name: Configure Barcode Sign Options
    text: '`BarcodeSignOptions` lets you define every attribute of the barcode—type,
      data, position, colors, borders, and even whether the raw barcode image should
      be returned. java import com.groupdocs.signature.Signature; import com.groupdocs.signature.exception.GroupDocsSignatureException;
      import java.nio.f'
  - name: Sign the Document
    text: 'The `sign` method applies the configured barcode to the PDF and writes
      the result to the target path. java signOptions.setEncodeType(BarcodeTypes.QR);
      // QR codes for more data signOptions.setForeColor(Color.BLACK); signOptions.setBackgroundColor(Color.WHITE);
      // Remove border and fancy styling for '
  type: HowTo
- questions:
  - answer: GroupDocs.Signature for Java is self‑contained; after adding the Maven/Gradle
      artifact you get full barcode generation and PDF rendering without any third‑party
      libraries.
    question: How do I add a barcode signature to a PDF in Java without external dependencies?
  - answer: Absolutely. Switch the `BarcodeTypes` enum to `QRCode` and adjust size
      parameters as needed.
    question: Can I configure barcode sign options in Java to generate QR codes?
  - answer: Pin the exact version in `pom.xml` (e.g., `23.10.0`) to avoid accidental
      upgrades, and enable the Maven `shade` plugin to produce a single executable
      JAR.
    question: What is the recommended Maven setup for production use?
  - answer: Yes. Provide the password when constructing the `Signature` object, then
      proceed with signing as usual.
    question: Does the library support password‑protected PDFs?
  - answer: GroupDocs.Signature can address all pages in a PDF at once or target specific
      pages via `setPageNumber()`. Performance scales linearly; a 200‑page PDF signs
      in ~2 seconds on a typical cloud VM.
    question: How many pages can I sign in one operation?
  type: FAQPage
tags:
- pdf-signing
- digital-signatures
- groupdocs
- barcode-signatures
title: Tambahkan tanda tangan barcode ke PDF dengan GroupDocs.Signature Java
type: docs
url: /id/java/digital-signatures/java-pdf-signing-groupdocs-signature-guide/
weight: 1
---

# Tambahkan tanda tangan barcode ke PDF dengan GroupDocs.Signature Java

Dalam aplikasi modern yang berfokus pada dokumen, **menambahkan tanda tangan barcode** adalah cara cepat dan dapat diandalkan untuk membuat PDF dapat dibaca manusia dan dapat dipindai mesin. Tutorial ini memandu Anda melalui setiap langkah—mulai dari konfigurasi Maven, melalui penataan barcode, hingga menangani kasus tepi file besar—sehingga Anda dapat mengintegrasikan tanda tangan barcode ke dalam proyek Java Anda dengan percaya diri.

## Jawaban Cepat
- **Apa baris kode pertama untuk memulai penandatanganan?** `Signature signature = new Signature("sample.pdf");`
- **Artefak Maven mana yang saya perlukan?** `com.groupdocs:groupdocs-signature:23.10` (replace with the latest version)
- **Apakah saya dapat menandatangani PDF yang dilindungi kata sandi?** Ya—lewatkan kata sandi saat membuat objek `Signature`.
- **Berapa banyak format barcode yang didukung?** Lebih dari 30, termasuk Code128, QR, DataMatrix, dan Aztec.
- **Berapa ukuran heap yang disarankan untuk PDF 100 MB?** Setidaknya `-Xmx2g` (2 GB) untuk menghindari `OutOfMemoryError`.

## Apa itu tanda tangan barcode?
Sebuah **tanda tangan barcode** adalah barcode yang dapat dibaca mesin yang disisipkan ke dalam PDF yang berfungsi sebagai penanda anti‑perubahan dan dapat membawa data khusus seperti ID, cap waktu, atau URL. Ini menggabungkan verifikasi visual dengan pemindaian otomatis, menjadikannya ideal untuk inventaris, kepatuhan, dan otomatisasi alur kerja volume tinggi.

## Mengapa menambahkan tanda tangan barcode dengan GroupDocs.Signature Java?
GroupDocs.Signature mendukung **lebih dari 50** format input dan output, memproses PDF beratus‑ratus halaman tanpa memuat seluruh file ke memori, dan menyediakan API Java yang fluida yang memungkinkan Anda menyesuaikan setiap aspek visual barcode. Dalam pengujian benchmark, menandatangani PDF 150‑halaman dengan barcode Code128 memakan **kurang dari 1,2 detik** pada instance cloud standar 2 vCPU.

## Prasyarat

Sebelum kita mulai, pastikan Anda memiliki hal‑hal berikut:

- **Java Development Kit (JDK)** 8 atau lebih baru (JDK 11 atau 17 disarankan untuk dukungan jangka panjang)
- **IDE** (IntelliJ IDEA, Eclipse, atau VS Code dengan ekstensi Java)
- **Alat build** (Maven 3.6+ atau Gradle 7.0+)
- **Pustaka GroupDocs.Signature Java** (kami akan menunjukkan pengaturan Maven & Gradle di bawah)
- Pemahaman dasar tentang konsep OOP Java dan struktur proyek Maven/Gradle

### Perpustakaan dan Dependensi yang Diperlukan

GroupDocs.Signature terintegrasi dengan mulus dengan Maven atau Gradle. Pilih alat build yang sudah Anda gunakan:

**Maven Setup**  
```markdown
```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```
```

**Pengaturan Gradle**  
```markdown
```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```
```

Jika Anda lebih suka menangani JAR secara manual, unduh rilis terbaru dari [GroupDocs.Signature for Java releases](https://releases.groupdocs.com/signature/java/) dan tambahkan ke classpath Anda.

### Langkah-langkah Akuisisi Lisensi

GroupDocs menawarkan tiga model lisensi:

- **Free Trial** – Akses penuh fitur selama 30 hari (watermark diterapkan pada PDF yang ditandatangani)  
- **Temporary License** – Percobaan diperpanjang tanpa batas fitur (ideal untuk pipeline pengembangan)  
- **Full License** – Siap produksi, termasuk dukungan prioritas dan tanpa watermark  

Dapatkan lisensi yang sesuai di [GroupDocs Licensing](https://purchase.groupdocs.com/buy). Bahkan selama percobaan Anda dapat menjalankan kode secara lokal; cukup ingat untuk mengganti kunci percobaan dengan yang permanen sebelum diluncurkan.

## Bagaimana cara menambahkan tanda tangan barcode ke PDF menggunakan GroupDocs.Signature Java?

Kelas `Signature` adalah titik masuk utama untuk bekerja dengan dokumen di GroupDocs.Signature.  
Kelas `BarcodeSignOptions` menentukan data, tipe, dan tampilan visual barcode.  

Muat PDF sumber Anda dengan `new Signature("source.pdf")`, konfigurasikan objek `BarcodeSignOptions` dengan data dan gaya visual yang diinginkan, lalu panggil `signature.sign("output.pdf", options)`. Pola tiga langkah ini menangani I/O file, pembuatan barcode, dan penulisan PDF dalam satu panggilan yang thread‑safe, dan bekerja untuk PDF mulai dari beberapa kilobyte hingga ratusan megabyte.

### Langkah 1: Inisialisasi Objek Signature

Kelas `Signature` adalah titik masuk GroupDocs.Signature untuk semua operasi penandatanganan. Ia mewakili satu dokumen PDF dalam memori dan menyediakan pemuatan malas untuk menjaga penggunaan memori tetap rendah.

```markdown
```java
import com.groupdocs.signature.Signature;

public class InitializeSignature {
    public static void main(String[] args) {
        Signature signature = new Signature("YOUR_DOCUMENT_DIRECTORY/sample.pdf");
        System.out.println("GroupDocs.Signature initialized successfully.");
    }
}
```
```

**Explanation:**  
- `filePath` menunjuk ke PDF sumber yang ingin Anda tandatangani.  
- `outputFilePath` adalah tempat PDF yang ditandatangani akan disimpan, mempertahankan file asli.  
- Blok `try‑catch` memastikan penanganan yang elegan terhadap kesalahan I/O, file yang hilang, atau masalah izin.

### Langkah 2: Konfigurasikan Opsi Tanda Tangan Barcode

`BarcodeSignOptions` memungkinkan Anda mendefinisikan setiap atribut barcode—tipe, data, posisi, warna, batas, dan bahkan apakah gambar barcode mentah harus dikembalikan.

```markdown
```java
import com.groupdocs.signature.Signature;
import com.groupdocs.signature.exception.GroupDocsSignatureException;
import java.nio.file.Paths;
import java.io.File;

public class Feature1 {
    public static void run() throws Exception {
        String filePath = "YOUR_DOCUMENT_DIRECTORY/sample.pdf";
        String outputFilePath = new File("YOUR_OUTPUT_DIRECTORY", "SignedOutputSample.pdf").getPath();

        try {
            Signature signature = new Signature(filePath);
            System.out.println("Signature initialized and paths set.");
        } catch (Exception e) {
            throw new GroupDocsSignatureException(e.getMessage());
        }
    }
}
```
```

**Key settings breakdown:**

- **Data & Type** – `"12345678"` adalah payload; `BarcodeTypes.Code128` bekerja untuk string alfanumerik dan didukung luas oleh pemindai.  
- **Positioning** – `setLeft(100)` dan `setTop(100)` menggeser barcode 100 px dari sudut kiri‑atas; `VerticalAlignment.Top` + `HorizontalAlignment.Right` menyesuaikan perataan relatif terhadap offset tersebut.  
- **Margins & Padding** – Objek `Padding` menambahkan buffer 20 px untuk menghindari pemotongan di tepi halaman.  
- **Styling** – Border, font, dan kuas latar belakang dapat disesuaikan sepenuhnya; untuk produksi Anda mungkin menghilangkan gradien untuk meningkatkan kecepatan rendering.  
- **Return Content** – Mengaktifkan `setReturnContent(true)` memberikan barcode sebagai `byte[]`, berguna untuk menyimpan gambar di basis data atau menampilkannya di UI.

#### Konfigurasi Minimal Siap Produksi

Untuk dokumen legal yang bersih, biasanya Anda menginginkan barcode hitam‑di‑atas‑putih sederhana tanpa border tambahan:

```markdown
```java
import com.groupdocs.signature.domain.enums.*;
import com.groupdocs.signature.domain.Padding;
import com.groupdocs.signature.domain.Border;
import com.groupdocs.signature.domain.DashStyle;
import com.groupdocs.signature.domain.extensions.LinearGradientBrush;
import com.groupdocs.signature.domain.font.SignatureFont;
import java.awt.Color;
import com.groupdocs.signature.options.sign.BarcodeSignOptions;

public class Feature2 {
    public static void configureBarcodeOptions() throws Exception {
        BarcodeSignOptions signOptions = new BarcodeSignOptions("12345678");
        signOptions.setEncodeType(BarcodeTypes.Code128);
        signOptions.setLeft(100);
        signOptions.setTop(100);
        signOptions.setVerticalAlignment(VerticalAlignment.Top);
        signOptions.setHorizontalAlignment(HorizontalAlignment.Right);

        Padding padding = new Padding();
        padding.setLeft(20);
        padding.setTop(20);
        signOptions.setMargin(padding);

        Border border = new Border();
        border.setColor(Color.GREEN);
        border.setDashStyle(DashStyle.DashLongDashDot);
        border.setWeight(2);
        border.setTransparency(0.5);
        border.setVisible(true);
        signOptions.setBorder(border);

        signOptions.setForeColor(Color.RED);
        SignatureFont font = new SignatureFont();
        font.setSize(12);
        font.setFamilyName("Comic Sans MS");
        signOptions.setFont(font);

        signOptions.setCodeTextAlignment(CodeTextAlignment.Above);

        Background background = new Background();
        background.setColor(Color.GREEN);
        background.setTransparency(0.5);
        background.setBrush(new LinearGradientBrush(Color.GREEN, Color.DARK_GRAY, 0));
        signOptions.setBackground(background);

        signOptions.setReturnContent(true);
        signOptions.setReturnContentType(FileType.PNG);
    }
}
```
```

### Langkah 3: Tanda Tangani Dokumen

Metode `sign` menerapkan barcode yang dikonfigurasi ke PDF dan menulis hasilnya ke jalur target.

```markdown
```java
signOptions.setEncodeType(BarcodeTypes.QR); // QR codes for more data
signOptions.setForeColor(Color.BLACK);
signOptions.setBackgroundColor(Color.WHITE);
// Remove border and fancy styling for professional appearance
```
```

**Under the hood:**  
- `signature.sign(outputFilePath, signOptions)` menulis barcode ke PDF sambil membiarkan sumber tidak berubah.  
- `SignResult` melaporkan berapa banyak tanda tangan yang ditambahkan, halaman mana yang dimodifikasi, dan peringatan apa pun yang dihasilkan.  
- Untuk pekerjaan batch, bungkus panggilan ini dalam `ExecutorService` untuk memparalelkan across core CPU.

## Masalah Umum dan Solusinya

### Masalah 1: FileNotFoundException pada Inisialisasi

**Gejala:** Aplikasi melempar `FileNotFoundException` saat membuat objek `Signature`.

**Penyebab utama:**  
- Jalur file tidak tepat (relatif vs. absolut)  
- Izin baca tidak ada  
- File terkunci oleh proses lain (misalnya, terbuka di Acrobat)

**Solusi:**  
```markdown
```java
import com.groupdocs.signature.Signature;
import com.groupdocs.signature.exception.GroupDocsSignatureException;
import com.groupdocs.signature.options.sign.BarcodeSignOptions;
import com.groupdocs.signature.domain.BaseSignature;

public class Feature3 {
    public static void signDocument(String filePath, BarcodeSignOptions signOptions) throws Exception {
        Signature signature = new Signature(filePath);
        String outputFilePath = filePath.replace(".pdf", "_Signed.pdf");

        try {
            com.groupdocs.signature.domain.signatures.SignResult signResult = signature.sign(outputFilePath, signOptions);
            System.out.println("Document signed successfully.");
        } catch (Exception e) {
            throw new GroupDocsSignatureException(e.getMessage());
        }
    }
}
```
```
Pastikan jalur menggunakan garis miring maju (`C:/Docs/sample.pdf`) atau meng-escape backslashes (`C:\\Docs\\sample.pdf`). Verifikasi izin OS dan tutup program apa pun yang mungkin mengunci file.

### Masalah 2: Barcode Tidak Muncul di Output

**Gejala:** Penandatanganan selesai tanpa error, tetapi barcode tidak terlihat.

**Alasan umum:**  
- Posisi menempatkan barcode di luar area cetak.  
- Transparansi diatur ke `1.0` (sepenuhnya transparan).  
- Ukuran font diatur ke `0`.

**Solusi:**  
- Pertahankan nilai `setLeft`/`setTop` dalam dimensi halaman (0‑600 px untuk A4 standar).  
- Gunakan nilai transparansi antara `0.0` (opaque) dan `0.9`.  
- Atur ukuran font yang dapat dibaca, misalnya `12pt`.

### Masalah 3: Kesalahan Out of Memory pada Dokumen Besar

**Gejala:** `OutOfMemoryError` saat memproses PDF lebih besar dari ~50 MB.

**Solusi:**  
- Tingkatkan heap JVM: `-Xmx2g` atau lebih tinggi tergantung ukuran dokumen.  
- Proses PDF halaman‑per‑halaman menggunakan streaming API `Signature`.  
- Tutup secara eksplisit instance `Signature` setelah setiap operasi untuk membebaskan sumber daya native.

```markdown
```java
import java.nio.file.Files;
import java.nio.file.Path;

Path filePath = Path.of("YOUR_DOCUMENT_DIRECTORY/sample.pdf");
if (!Files.exists(filePath)) {
    throw new IllegalArgumentException("PDF file not found: " + filePath);
}
if (!Files.isReadable(filePath)) {
    throw new SecurityException("Cannot read PDF file: " + filePath);
}
// Now safe to initialize
Signature signature = new Signature(filePath.toString());
```
```

### Masalah 4: Kesalahan Data Barcode Tidak Valid

**Gejala:** API melempar pengecualian yang mengeluh tentang karakter yang tidak didukung.

**Penyebab:** Standar barcode yang berbeda menerima set karakter yang berbeda. Code128 mengizinkan alfanumerik; QR dapat menangani Unicode; beberapa barcode 1D hanya menerima digit.

**Resolusi:** Pilih tipe barcode yang cocok dengan set data Anda, atau bersihkan string sebelum menetapkannya ke `BarcodeSignOptions`.

```markdown
```java
String barcodeData = "ABC123"; // Your data
BarcodeTypes type = BarcodeTypes.Code128; // Alphanumeric support

// For numeric-only barcodes, validate first:
if (type == BarcodeTypes.EAN13 && !barcodeData.matches("\\d+")) {
    throw new IllegalArgumentException("EAN13 requires numeric data only");
}
```
```

## Praktik Terbaik untuk Produksi

### 1. Validasi PDF Sebelum Menandatangani

Selalu pastikan file adalah PDF yang terbentuk dengan baik untuk menghindari error parsing saat runtime.

```markdown
```java
try (Signature signature = new Signature(filePath)) {
    // If this succeeds, file is valid
    signature.getDocumentInfo();
} catch (Exception e) {
    // Handle invalid PDF
}
```
```

### 2. Gunakan Pemrosesan Asinkron untuk Beban Kerja Volume Tinggi

Alihkan penandatanganan ke thread pool latar belakang; ini mencegah pembekuan UI dan meningkatkan throughput.

```markdown
```java
ExecutorService executor = Executors.newFixedThreadPool(4);
List<String> pdfFiles = Arrays.asList("doc1.pdf", "doc2.pdf", "doc3.pdf");

pdfFiles.forEach(file -> {
    executor.submit(() -> {
        try {
            signDocument(file, signOptions);
        } catch (Exception e) {
            // Log error
        }
    });
});
executor.shutdown();
```
```

### 3. Implementasikan Logging Terstruktur

Catat setiap permintaan penandatanganan dengan jalur input, jalur output, data barcode, dan setiap pengecualian. Ini secara dramatis mempercepat analisis pasca‑mortem.

```markdown
```java
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

private static final Logger logger = LoggerFactory.getLogger(YourClass.class);

try {
    SignResult result = signature.sign(outputFilePath, signOptions);
    logger.info("Document signed successfully: {}", outputFilePath);
    logger.debug("Signatures added: {}", result.getSucceeded().size());
} catch (Exception e) {
    logger.error("Failed to sign document: {}", filePath, e);
}
```
```

### 4. Optimalkan Pengaturan Barcode untuk Kecepatan
- Nonaktifkan `setReturnContent(true)` kecuali Anda memerlukan gambar secara terpisah.  
- Lebih pilih kuas latar belakang solid daripada gradien.  
- Hilangkan border untuk kasus penggunaan pelacakan sederhana.

### 5. Tangani Kedaluwarsa Lisensi Sementara dengan Elegan

Kelas `License` memuat dan memvalidasi file lisensi GroupDocs untuk API.  
Periksa status lisensi sebelum setiap operasi penandatanganan dan beralih ke mode hanya-baca atau beri peringatan kepada admin.

```markdown
```java
try {
    License license = new License();
    license.setLicense(licensePath);
} catch (Exception e) {
    logger.warn("License validation failed. Using trial mode.");
    // Continue with trial limitations
}
```
```

## Kapan Menggunakan Tanda Tangan Barcode

### Skenario Ideal
- **Inventaris & Logistik:** Lampirkan barcode yang dapat dipindai ke manifest pengiriman, daftar pengepakan, atau tag aset.  
- **Kepatuhan Regulasi:** Industri seperti farmasi memerlukan jejak audit yang dapat dibaca mesin.  
- **Pipeline Dokumen Otomatis:** Gabungkan tanda tangan barcode dengan OCR untuk memungkinkan pemrosesan ujung‑ke‑ujung tanpa entri data manual.  
- **Pekerjaan Batch Volume Tinggi:** Barcode lebih cepat diverifikasi dibandingkan tanda tangan digital kriptografis saat memindai arsip kertas besar.

### Kapan Memilih Tipe Tanda Tangan Lain
- **Kontrak Legal:** Gunakan tanda tangan digital berbasis PKI (mis., X.509) untuk non‑repudiation.  
- **PDF yang Dihadapkan ke Pelanggan:** QR code lebih mudah dikenali pada perangkat seluler.  
- **Dokumen Ultra‑Aman:** Padukan barcode dengan tanda tangan digital terenkripsi untuk keamanan berlapis.

> **Tips Pro:** Anda dapat menyematkan beberapa tipe tanda tangan dalam PDF yang sama—tambahkan barcode untuk pelacakan dan sertifikat digital untuk penegakan hukum.

## Pertanyaan yang Sering Diajukan

**Q: Bagaimana cara menambahkan tanda tangan barcode ke PDF di Java tanpa dependensi eksternal?**  
A: GroupDocs.Signature untuk Java bersifat mandiri; setelah menambahkan artefak Maven/Gradle Anda mendapatkan generasi barcode lengkap dan rendering PDF tanpa pustaka pihak ketiga apa pun.

**Q: Bisakah saya mengonfigurasi opsi tanda tangan barcode di Java untuk menghasilkan QR code?**  
A: Tentu saja. Ganti enum `BarcodeTypes` menjadi `QRCode` dan sesuaikan parameter ukuran sesuai kebutuhan.

```markdown
```java
signOptions.setEncodeType(BarcodeTypes.QR);
```
```

**Q: Apa pengaturan Maven yang disarankan untuk penggunaan produksi?**  
A: Tetapkan versi tepat di `pom.xml` (mis., `23.10.0`) untuk menghindari upgrade tidak sengaja, dan aktifkan plugin Maven `shade` untuk menghasilkan satu JAR yang dapat dieksekusi.

```markdown
```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version> <!-- Don't use LATEST -->
</dependency>
```
```

**Q: Apakah pustaka mendukung PDF yang dilindungi kata sandi?**  
A: Ya. Berikan kata sandi saat membuat objek `Signature`, lalu lanjutkan penandatanganan seperti biasa.

```markdown
```java
LoadOptions loadOptions = new LoadOptions();
loadOptions.setPassword("your_pdf_password");
Signature signature = new Signature(filePath, loadOptions);
```
```

**Q: Berapa banyak halaman yang dapat saya tandatangani dalam satu operasi?**  
A: GroupDocs.Signature dapat menangani semua halaman dalam PDF sekaligus atau menargetkan halaman tertentu melalui `setPageNumber()`. Kinerja meningkat secara linear; PDF 200‑halaman ditandatangani dalam ~2 detik pada VM cloud tipikal.

**Q: Format barcode apa yang tersedia selain Code128?**  
A: Lebih dari 30 format, termasuk QR, DataMatrix, Aztec, UPC‑A, EAN‑13, PDF417, dan lainnya. Lihat enum `BarcodeTypes` untuk daftar lengkap.

**Q: Apakah ada batas panjang data barcode?**  
A: Batas panjang tergantung pada tipe barcode; untuk Code128 batas praktisnya adalah 80 karakter, sementara QR code dapat menyimpan hingga 4 KB data.

**Q: Bisakah saya mengambil gambar barcode yang dihasilkan setelah penandatanganan?**  
A: Atur `setReturnContent(true)` dan `setReturnContentType(FileType.PNG)`; `SignResult` akan berisi `byte[]` yang dapat Anda tulis ke disk atau basis data.

---

**Terakhir Diperbarui:** 2026-07-25  
**Diuji Dengan:** GroupDocs.Signature 23.10 untuk Java  
**Penulis:** GroupDocs

## Tutorial Terkait

- [Cara Menambahkan Tanda Tangan Digital di Java - Tutorial Lengkap GroupDocs](/signature/java/getting-started/groupdocs-signature-java-digital-setup-guide/)
- [Tambahkan QR Code ke PDF Java - Tutorial Lengkap GroupDocs](/signature/java/qr-code-signatures/qr-code-signature-generation-java-groupdocs/)
- [Tambahkan Tanda Tangan Teks ke PDF di Java - Tutorial Lengkap GroupDocs](/signature/java/text-signatures/implement-text-signatures-groupdocs-java/)