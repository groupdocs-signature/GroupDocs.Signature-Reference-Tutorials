---
categories:
- Java Development
date: '2026-06-11'
description: Pelajari cara menandatangani PDF dengan Java menggunakan GroupDocs.Signature,
  menambahkan digital signature dan timestamp. Panduan langkah demi langkah dengan
  contoh kode dan praktik terbaik.
keywords:
- how to sign pdf
- add digital signature pdf
- timestamp pdf signature
- java pdf signature library
- groupdocs signature java
lastmod: '2026-06-11'
linktitle: Tambahkan Digital Signature ke PDF Java
schemas:
- author: GroupDocs
  dateModified: '2026-06-11'
  description: Learn how to sign PDF with Java using GroupDocs.Signature, add digital
    signature and timestamp. Step-by-step guide with code examples and best practices.
  headline: 'How to Sign PDF with Java: Add Digital Signature and Timestamp'
  type: TechArticle
- description: Learn how to sign PDF with Java using GroupDocs.Signature, add digital
    signature and timestamp. Step-by-step guide with code examples and best practices.
  name: 'How to Sign PDF with Java: Add Digital Signature and Timestamp'
  steps:
  - name: Import Required Classes
    text: The following imports give you access to signature configuration, positioning,
      and timestamp functionality.
  - name: Define Your File Paths
    text: Set up paths for your input PDF, certificate, and where you want the signed
      PDF saved. Keep the certificate file secure; it contains your private key.
  - name: Initialize the Signature Object
    text: Create a `Signature` instance pointing to the PDF you want to sign. This
      loads the PDF into memory and prepares it for signing.
  - name: Configure Signature Properties and Timestamp
    text: The `DigitalSignature` class represents the cryptographic seal that will
      be embedded in the PDF. You can also attach a timestamp from a trusted authority.
      * **ContactInfo** – e.g., `john.doe@company.com` * **Location** – e.g., `New
      York Office` * **Reason** – e.g., `Contract Approval` We use FreeTSA
  - name: Configure Digital Sign Options
    text: The `SignOptions` class ties together the certificate, signature properties,
      and visual placement. Alignment enums control where the signature appears.
  - name: Sign and Save the Document
    text: Execute the signing process and write the signed PDF to disk. The returned
      `SignResult` object tells you whether the operation succeeded and lists any
      warnings.
  type: HowTo
- questions:
  - answer: A digital signature uses cryptographic algorithms to verify identity and
      detect tampering, while an electronic signature can be as simple as a typed
      name.
    question: What's the difference between a digital signature and an electronic
      signature?
  - answer: Only for the timestamp service; the cryptographic signing itself runs
      locally.
    question: Do I need internet connectivity to sign PDFs?
  - answer: Any modification breaks the signature, and PDF viewers will display a
      warning indicating the document has been altered.
    question: Can signed PDFs be edited later?
  - answer: Most PDF readers verify automatically; programmatically, use GroupDocs.Signature's
      verification API to check status, signer details, and timestamp validity.
    question: How do I verify a signed PDF?
  - answer: The embedded timestamp proves the signature was created while the certificate
      was still valid, preserving legal standing.
    question: What happens if my certificate expires after I've signed documents?
  type: FAQPage
tags:
- pdf-signing
- digital-signatures
- java-security
- groupdocs
title: 'Cara Menandatangani PDF dengan Java: Tambahkan Digital Signature dan Timestamp'
type: docs
url: /id/java/digital-signatures/digital-signature-timestamp-pdf-java-groupdocs/
weight: 1
---

# Cara Menandatangani PDF dengan Java dan Timestamp

Pernah mengirim dokumen penting dan khawatir apakah seseorang dapat mengubahnya nanti? Anda tidak sendirian. Baik Anda sedang membangun sistem manajemen dokumen perusahaan, membuat platform penandatanganan kontrak, atau hanya perlu mengamankan file PDF secara programatis, **how to sign PDF** dengan timestamp tepercaya adalah jawabannya. Menambahkan tanda tangan digital tidak hanya membuktikan siapa yang menandatangani file tetapi juga membuat catatan tidak dapat diubah tentang *tepat* kapan penandatanganan terjadi.

## Jawaban Cepat
- **Library apa yang menyederhanakan penandatanganan PDF di Java?** GroupDocs.Signature for Java.  
- **Apakah saya memerlukan koneksi internet?** Hanya untuk otoritas timestamp; penandatanganan itu sendiri offline.  
- **Bisakah saya menggunakan sertifikat self‑signed untuk pengujian?** Ya, buat satu dengan `keytool`.  
- **Apakah ada batas ukuran?** Library dapat menandatangani PDF hingga 500 MB tanpa memuat seluruh file ke memori.  
- **Berapa banyak format yang didukung GroupDocs?** Lebih dari 50 format input dan output, termasuk DOCX, XLSX, PPTX, HTML, dan gambar.

## Mengapa Tanda Tangan Digital Penting (Dan Mengapa Anda Membutuhkan Timestamp)

Muat PDF Anda, terapkan segel kriptografis, dan sematkan timestamp tepercaya—proses dua langkah ini menjamin otentikasi, integritas, dan non‑repudiation. Timestamp membuktikan tanda tangan ada pada momen tertentu, bahkan jika sertifikat penandatangan kemudian kedaluwarsa atau dicabut.

## Cara Menandatangani PDF dengan Java?

Muat PDF Anda dengan `new Signature("input.pdf")`, konfigurasikan objek `DigitalSignature`, lampirkan timestamp dari otoritas tepercaya, dan panggil `sign()`—seluruh operasi selesai dalam beberapa baris kode. GroupDocs.Signature menangani parsing sertifikat, perhitungan hash, dan pengambilan timestamp secara otomatis, sehingga Anda dapat fokus pada logika bisnis daripada kriptografi.

## Menyiapkan GroupDocs.Signature untuk Java

### Metode Integrasi

Pilih alat build yang Anda gunakan:

**Untuk Pengguna Maven:**  
Tambahkan dependensi ini ke `pom.xml` Anda:
```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

**Untuk Pengguna Gradle:**  
Tambahkan ini ke `build.gradle` Anda:
```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

**Unduhan Langsung (Jika Anda Lebih Suka):**  
Head over to [GroupDocs.Signature for Java releases](https://releases.groupdocs.com/signature/java/) and download the JAR file. Add it to your project's classpath manually. See the [GroupDocs.Signature Documentation](https://docs.groupdocs.com/signature/java/) for detailed API reference. For the most recent build, see the [Latest Version & Releases](https://releases.groupdocs.com/signature/java/).

Tip pro: Gunakan Maven atau Gradle jika memungkinkan—ini membuat manajemen dependensi dan pembaruan jauh lebih mudah di kemudian hari.

### Mengatur Lisensi Anda

GroupDocs menawarkan beberapa opsi di sini, tergantung pada tahap proyek Anda:

1. **Free Trial** – Sempurna untuk evaluasi. [Download Trial Version](https://releases.groupdocs.com/signature/java/) dan coba semua fitur.  
2. **Temporary License** – Membutuhkan akses penuh untuk pengembangan tanpa watermark trial? Dapatkan lisensi sementara 30‑hari.  
3. **Commercial License** – Untuk penggunaan produksi, [Buy License](https://purchase.groupdocs.com/buy). Harga bervariasi tergantung tipe penyebaran.

Butuh bantuan? Kunjungi [GroupDocs Forum](https://forum.groupdocs.com/c/signature/).

### Inisialisasi Dasar

Kelas `Signature` adalah objek tingkat‑atas GroupDocs.Signature yang mewakili satu file PDF dalam memori. Setelah diinstansiasi, semua operasi baca dan tulis mengalir melalui objek ini.

```java
import com.groupdocs.signature.Signature;

String filePath = "YOUR_DOCUMENT_DIRECTORY/sample.pdf";
final Signature signature = new Signature(filePath);
```

Sederhana, kan? Anda cukup menunjukannya ke file PDF Anda, dan Anda siap. Objek `Signature` adalah antarmuka utama Anda untuk semua operasi penandatanganan.

## Cara Menambahkan Tanda Tangan Digital ke PDF Java: Langkah‑per‑Langkah

Muat PDF Anda, konfigurasikan detail tanda tangan, lampirkan timestamp, dan simpan dokumen yang ditandatangani—semua dalam alur yang jelas dan linear.

### Langkah 1: Impor Kelas yang Diperlukan

Impor berikut memberi Anda akses ke konfigurasi tanda tangan, penempatan, dan fungsionalitas timestamp.

```java
import com.groupdocs.signature.Signature;
import com.groupdocs.signature.domain.enums.HorizontalAlignment;
import com.groupdocs.signature.domain.enums.VerticalAlignment;
import com.groupdocs.signature.domain.signatures.PdfDigitalSignature;
import com.groupdocs.signature.domain.structs.TimeStamp;
import com.groupdocs.signature.options.sign.DigitalSignOptions;
```

### Langkah 2: Tentukan Jalur File Anda

Atur jalur untuk PDF input Anda, sertifikat, dan tempat Anda ingin menyimpan PDF yang ditandatangani. Jaga file sertifikat tetap aman; ia berisi kunci pribadi Anda.

```java
String filePath = "YOUR_DOCUMENT_DIRECTORY/sample.pdf";
String certificatePath = "YOUR_DOCUMENT_DIRECTORY/certificate.pfx";
String outputFilePath = "YOUR_OUTPUT_DIRECTORY/digitallySignedTimeStamp.pdf";
```

### Langkah 3: Inisialisasi Objek Signature

Buat instance `Signature` yang menunjuk ke PDF yang ingin Anda tandatangani. Ini memuat PDF ke memori dan menyiapkannya untuk penandatanganan.

```java
final Signature signature = new Signature(filePath);
```

### Langkah 4: Konfigurasikan Properti Tanda Tangan dan Timestamp

Kelas `DigitalSignature` mewakili segel kriptografis yang akan disematkan dalam PDF. Anda juga dapat melampirkan timestamp dari otoritas tepercaya.

```java
PdfDigitalSignature pdfDigitalSignature = new PdfDigitalSignature();
pdfDigitalSignature.setContactInfo("Contact Information");
pdfDigitalSignature.setLocation("Location Info");
pdfDigitalSignature.setReason("Signing Reason");

// Configure the TimeStamp with URL, User Id, and Password
TimeStamp timeStamp = new TimeStamp("https://freetsa.org/tsr", "User Id", "Password");
pdfDigitalSignature.setTimeStamp(timeStamp);
```

* **ContactInfo** – misalnya, `john.doe@company.com`  
* **Location** – misalnya, `New York Office`  
* **Reason** – misalnya, `Contract Approval`  

Kami menggunakan FreeTSA (otoritas timestamp gratis) untuk demonstrasi. Dalam produksi, pilih TSA komersial untuk jaminan waktu aktif dan kepatuhan hukum.

### Langkah 5: Konfigurasikan Opsi Tanda Tangan Digital

Kelas `SignOptions` menggabungkan sertifikat, properti tanda tangan, dan penempatan visual. Enum alignment mengontrol di mana tanda tangan muncul.

```java
DigitalSignOptions options = new DigitalSignOptions(certificatePath);
options.setPassword("YourCertificatePassword"); // Certificate password
options.setSignature(pdfDigitalSignature); // Attach the PdfDigitalSignature object

// Specify signature alignment (where it appears on the page)
options.setVerticalAlignment(VerticalAlignment.Bottom);
options.setHorizontalAlignment(HorizontalAlignment.Right);
```

### Langkah 6: Tanda Tangani dan Simpan Dokumen

Jalankan proses penandatanganan dan tulis PDF yang ditandatangani ke disk. Objek `SignResult` yang dikembalikan memberi tahu Anda apakah operasi berhasil dan menampilkan peringatan apa pun.

```java
try {
    SignResult signResult = signature.sign(outputFilePath, options);
    System.out.println("Document signed successfully!");
    System.out.println("Output: " + outputFilePath);
} catch (Exception e) {
    throw new RuntimeException("Error during signing process: " + e.getMessage());
}
```

## Kesalahan Umum yang Harus Dihindari

### 1. Masalah Sertifikat

**Problem:** Kesalahan “Invalid certificate”.  
**Fix:** Verifikasi kata sandi dengan `keytool -list -v -keystore your.pfx`.

```bash
keytool -list -v -keystore certificate.pfx -storetype PKCS12
```

### 2. Timeout Layanan Timestamp

**Problem:** Timeout jaringan saat menghubungi TSA.  
**Fix:** Uji konektivitas (`curl -I https://freetsa.org/tsr`), tambahkan logika retry, atau konfigurasikan TSA cadangan.

```java
new File(outputFilePath).getParentFile().mkdirs();
```

### 3. Masalah Izin File

**Problem:** “Access denied” saat menyimpan.  
**Fix:** Pastikan direktori output ada dan aplikasi memiliki izin menulis.

```bash
keytool -genkeypair -alias mykey -keyalg RSA -keysize 2048 -storetype PKCS12 -keystore certificate.pfx -validity 365
```

### 4. Masalah Memori dengan PDF Besar

**Problem:** `OutOfMemoryError` untuk file besar.  
**Fix:** Tingkatkan heap JVM (`-Xmx4g`) atau proses file secara batch.

### 5. Penempatan Tanda Tangan Salah

**Problem:** Tanda tangan menutupi konten yang ada.  
**Fix:** Uji pengaturan alignment terlebih dahulu; untuk penempatan pixel‑perfect, gunakan opsi berbasis koordinat.

## Tips Manajemen Sertifikat

### Mendapatkan Sertifikat untuk Pengembangan

Buat sertifikat self‑signed dengan `keytool` Java untuk keperluan pengujian.

```java
   String certPassword = System.getenv("CERT_PASSWORD");
   ```

### Praktik Terbaik Sertifikat

1. **Jangan pernah menuliskan password secara hard‑code** – gunakan variabel lingkungan.  
2. **Rotasi sertifikat** sebelum kedaluwarsa.  
3. **Simpan kunci pribadi** di perangkat keras aman (HSM) untuk aplikasi keamanan tinggi.  
4. **Cadangkan sertifikat** di lokasi yang terlindungi.  
5. **Validasi sertifikat** sebelum menandatangani untuk menangkap yang kedaluwarsa atau dicabut.

## Praktik Keamanan Terbaik

### 1. Lindungi Kunci Pribadi
Simpan sertifikat di luar direktori proyek, gunakan konfigurasi spesifik lingkungan, dan pertimbangkan HSM untuk penyebaran perusahaan.

### 2. Validasi PDF Masukan
Periksa kerusakan, tanda tangan yang ada, batas ukuran, dan kepatuhan konten sebelum menandatangani.

### 3. Implementasikan Logging Audit
Catat setiap operasi penandatanganan dengan timestamp, pengguna, nama dokumen, dan status.

```java
try {
    SignResult result = signature.sign(outputFilePath, options);
    logger.info("Document signed: " + filePath + " by " + signerEmail);
} catch (Exception e) {
    logger.error("Signing failed: " + filePath + " - " + e.getMessage());
    // Handle appropriately
}
```

### 4. Gunakan Otoritas Timestamp Tepercaya
Jangan pernah mengandalkan waktu sistem lokal; selalu minta timestamp dari TSA yang sesuai RFC 3161.

### 5. Implementasikan Penanganan Kesalahan
Tangkap pengecualian tanpa mengungkapkan detail sensitif.

```java
try {
    signature.sign(outputFilePath, options);
} catch (Exception e) {
    // Log detailed error internally
    logger.error("Signing error: " + e.getMessage(), e);
    // Return generic error to client
    throw new ApplicationException("Unable to sign document. Please try again.");
}
```

## Kasus Penggunaan dan Aplikasi di Dunia Nyata

### 1. Sistem Manajemen Kontrak
Karyawan menandatangani NDA dan perjanjian secara elektronik; timestamp membuktikan tepat kapan setiap kontrak diterima.

### 2. Pemrosesan Dokumen Keuangan
Tandatangani batch faktur dan purchase order, menyediakan jejak audit tidak dapat diubah untuk regulator.

### 3. Verifikasi Kredensial Pendidikan
Universitas mengeluarkan transkrip yang tidak dapat diubah yang dapat divalidasi secara instan melalui tautan QR‑code.

### 4. Manajemen Lisensi Perangkat Lunak
Hasilkan sertifikat lisensi dengan tanda tangan digital dan timestamp untuk mencegah pemalsuan.

### 5. Kepatuhan Regulasi (FDA 21 CFR Part 11, dll.)
Perusahaan perangkat medis menandatangani SOP dan laporan validasi; timestamp memenuhi persyaratan non‑repudiation.

## Pertimbangan Kinerja dan Optimasi

### Manajemen Memori
Proses PDF besar secara batch, tutup objek `Signature` dengan cepat, dan tingkatkan ukuran heap bila diperlukan.

### Optimasi Jaringan untuk Timestamp
Gunakan pool koneksi HTTP, implementasikan retry dengan backoff eksponensial, dan cache timestamp untuk penandatanganan berurutan yang cepat.

### Praktik Terbaik Pemrosesan Batch
```java
// Pseudo‑code: process a list of PDFs in parallel, limiting to 5 concurrent TSA calls
```
*Hindari membuat terlalu banyak thread; 5‑10 penandatanganan bersamaan menyeimbangkan throughput dan beban TSA.*

### Optimasi I/O Disk
Gunakan SSD untuk file sementara, minimalkan siklus baca/tulis, dan bersihkan artefak sementara setelah setiap proses penandatanganan.

## Panduan Pemecahan Masalah

### Kesalahan: “Invalid Certificate Password”
**Solution:** Verifikasi kata sandi dengan `keytool -list -keystore your.pfx`.

```java
ExecutorService executor = Executors.newFixedThreadPool(5);
List<Future<SignResult>> futures = new ArrayList<>();

for (String pdfPath : pdfPaths) {
    futures.add(executor.submit(() -> {
        try (Signature sig = new Signature(pdfPath)) {
            return sig.sign(outputPath, options);
        }
    }));
}

// Wait for all to complete
for (Future<SignResult> future : futures) {
    SignResult result = future.get();
    // Process result
}

executor.shutdown();
```

### Kesalahan: “Timestamp Authority Not Responding”
**Solution:** Uji URL TSA, periksa aturan firewall, dan tambahkan logika TSA cadangan.

```bash
keytool -list -v -keystore certificate.pfx -storetype PKCS12
```

### Kesalahan: “PDF is Already Signed”
Solusi: Deteksi tanda tangan yang ada terlebih dahulu; tambahkan counter‑signature atau tandatangani salinan baru.

### Kesalahan: “Access Denied” Saat Menyimpan
Solusi: Pastikan direktori output ada, aplikasi memiliki hak menulis, dan tidak ada proses lain yang mengunci file.

```java
TimeStamp timeStamp;
try {
    timeStamp = new TimeStamp("https://freetsa.org/tsr", "", "");
} catch (Exception e) {
    // Fallback to alternative TSA
    timeStamp = new TimeStamp("https://alternate-tsa.com/tsr", "", "");
}
```

### Kesalahan: OutOfMemoryError
Solusi: Tingkatkan heap JVM, proses PDF dalam batch lebih kecil, atau beralih ke API streaming untuk file sangat besar.

## Kesimpulan dan Langkah Selanjutnya

Anda telah mempelajari **how to sign PDF** dengan Java, menambahkan timestamp tepercaya, dan menangani kesulitan umum. Selanjutnya, jelajahi:

1. Menambahkan beberapa bidang tanda tangan untuk perjanjian multi‑pihak.  
2. Memverifikasi tanda tangan secara programatis dengan GroupDocs.Signature.  
3. Menyesuaikan tampilan tanda tangan (gambar, teks, penempatan).  
4. Membangun layanan penandatanganan batch yang kuat dengan antrian dan pemantauan.

## Pertanyaan yang Sering Diajukan

**Q: Apa perbedaan antara tanda tangan digital dan tanda tangan elektronik?**  
A: Tanda tangan digital menggunakan algoritma kriptografis untuk memverifikasi identitas dan mendeteksi manipulasi, sementara tanda tangan elektronik dapat sesederhana nama yang diketik.

**Q: Apakah saya memerlukan koneksi internet untuk menandatangani PDF?**  
A: Hanya untuk layanan timestamp; penandatanganan kriptografis itu sendiri berjalan secara lokal.

**Q: Dapatkah PDF yang ditandatangani diedit kemudian?**  
A: Setiap modifikasi akan memutus tanda tangan, dan penampil PDF akan menampilkan peringatan bahwa dokumen telah diubah.

**Q: Bagaimana cara memverifikasi PDF yang ditandatangani?**  
A: Sebagian besar pembaca PDF memverifikasi secara otomatis; secara programatis, gunakan API verifikasi GroupDocs.Signature untuk memeriksa status, detail penandatangan, dan keabsahan timestamp.

**Q: Apa yang terjadi jika sertifikat saya kedaluwarsa setelah saya menandatangani dokumen?**  
A: Timestamp yang disematkan membuktikan tanda tangan dibuat saat sertifikat masih berlaku, menjaga keabsahan hukum.

**Q: Bisakah saya menggunakan ini dengan penyimpanan cloud (S3, Azure Blob, dll.)?**  
A: Ya—unduh PDF ke lokasi sementara, tandatangani, lalu unggah versi yang ditandatangani kembali ke cloud.

**Q: Apakah ada batas ukuran file?**  
A: Library menangani PDF hingga 500 MB tanpa memuat seluruh file ke memori; file yang lebih besar mungkin memerlukan streaming.

**Q: Berapa biaya GroupDocs.Signature untuk penggunaan komersial?**  
A: Harga bervariasi tergantung tipe penyebaran; hubungi penjualan GroupDocs untuk tarif terbaru. Versi trial dan lisensi sementara tersedia untuk evaluasi.

**Q: Apakah ini bekerja di server Linux?**  
A: Tentu saja. GroupDocs.Signature untuk Java bersifat platform‑independen dan berjalan di OS apa pun dengan JRE.

**Last Updated:** 2026-06-11  
**Tested With:** GroupDocs.Signature 23.9 for Java  
**Author:** GroupDocs

```java
File outputFile = new File(outputFilePath);
outputFile.getParentFile().mkdirs(); // Create directories if needed

if (!outputFile.canWrite() && outputFile.exists()) {
    throw new IOException("Cannot write to " + outputFilePath);
}
```

## Tutorial Terkait

- [Cara Memverifikasi Sertifikat Digital di Java - Panduan Lengkap dengan Contoh Kode](/signature/java/digital-signatures/java-certificate-verification-groupdocs-signature/)
- [Cara Menandatangani PDF secara Programatis di Java dengan GroupDocs.Signature](/signature/java/digital-signatures/sign-pdfs-groupdocs-signature-java/)
- [Menambahkan Tanda Tangan Gambar ke PDF Java dengan GroupDocs](/signature/java/image-signatures/sign-pdf-image-signature-groupdocs-java/)