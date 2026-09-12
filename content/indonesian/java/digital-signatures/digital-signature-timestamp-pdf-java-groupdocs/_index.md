---
date: '2026-09-05'
description: Pelajari cara menandatangani PDF dengan Java menggunakan GroupDocs.Signature,
  menambahkan digital signature dan timestamp. Panduan langkah demi langkah dengan
  contoh kode dan praktik terbaik.
keywords:
- how to sign pdf
- add digital signature pdf
- digital signature pdf java
- sign pdf java
- groupdocs signature java
lastmod: '2026-09-05'
linktitle: Tambahkan digital signature ke PDF Java
og_description: Pelajari cara menandatangani PDF dengan Java menggunakan GroupDocs.Signature,
  menambahkan digital signature dan trusted timestamp dalam beberapa baris kode. Ikuti
  instruksi langkah demi langkah, praktik terbaik, dan tips pemecahan masalah.
og_image_alt: Guide showing Java code to add digital signature and timestamp to PDF
  with GroupDocs.Signature
og_title: Cara menandatangani PDF dengan Java menggunakan GroupDocs.Signature
schemas:
- author: GroupDocs
  dateModified: '2026-09-05'
  description: Learn how to sign PDF with Java using GroupDocs.Signature, add digital
    signature and timestamp. Step-by-step guide with code examples and best practices.
  headline: How to sign PDF with Java and timestamp
  type: TechArticle
- description: Learn how to sign PDF with Java using GroupDocs.Signature, add digital
    signature and timestamp. Step-by-step guide with code examples and best practices.
  name: How to sign PDF with Java and timestamp
  steps:
  - name: import required classes
    text: The following imports give you access to signature configuration, positioning,
      and timestamp functionality.
  - name: define your file paths
    text: Set up paths for the input PDF, the certificate (PFX), and the output location.
      Keep the certificate file secure; it contains your private key.
  - name: initialize the Signature object
    text: '`Signature` is the entry point for all signing actions. Creating it loads
      the PDF into memory and prepares the API for further operations.'
  - name: configure signature properties and timestamp
    text: '`DigitalSignature` is the cryptographic seal that will be embedded in the
      PDF. You can also attach a timestamp from a trusted authority. * **ContactInfo**
      – e.g., `john.doe@company.com` * **Location** – e.g., `New York Office` * **Reason**
      – e.g., `Contract Approval` We use FreeTSA (a free timestamp'
  - name: configure digital sign options
    text: '`SignOptions` aggregates the certificate, visual appearance, and placement
      settings for the digital signature.'
  - name: sign and save the document
    text: '`SignResult` provides the outcome of the signing operation, including success
      status and any warnings.'
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
- pdf signing
- digital signatures
- java security
- groupdocs
- java pdf signature
title: Cara menandatangani PDF dengan Java dan timestamp
---

# Cara menandatangani PDF dengan Java dan timestamp

Ketika Anda perlu melindungi kontrak, faktur, atau dokumen penting apa pun dari manipulasi, **cara menandatangani PDF** secara aman menjadi prioritas utama. Dalam panduan ini Anda akan menemukan cara menambahkan tanda tangan digital dan timestamp tepercaya ke PDF menggunakan GroupDocs.Signature untuk Java. Pendekatan ini bekerja secara offline, mendukung file hingga 500 MB, dan hanya memerlukan beberapa baris kode.

## Jawaban Cepat
- **Library apa yang menyederhanakan penandatanganan PDF di Java?** GroupDocs.Signature untuk Java.  
- **Apakah saya memerlukan koneksi internet?** Hanya untuk otoritas timestamp; penandatanganan kriptografis berjalan secara lokal.  
- **Bisakah saya menggunakan sertifikat self‑signed untuk pengujian?** Ya, buat satu dengan `keytool`.  
- **Apakah ada batas ukuran?** Library dapat menandatangani PDF hingga 500 MB tanpa memuat seluruh file ke memori.  
- **Berapa banyak format yang didukung GroupDocs?** Lebih dari 50 format input dan output, termasuk DOCX, XLSX, PPTX, HTML, dan gambar.

## Cara menandatangani PDF dengan Java?

Muat PDF, konfigurasikan `DigitalSignature` dengan sertifikat Anda, secara opsional lampirkan timestamp dari TSA yang mematuhi RFC 3161, dan panggil `sign()`. Objek `Signature` menulis file yang ditandatangani ke disk, mengembalikan `SignResult` yang memberi tahu apakah operasi berhasil dan menampilkan peringatan apa pun. Alur end‑to‑end ini hanya memerlukan beberapa baris kode Java dan secara otomatis menangani hashing, validasi sertifikat, serta pengambilan timestamp.

## Mengapa tanda tangan digital penting (dan mengapa Anda membutuhkan timestamp)

Tanda tangan digital menjamin **keaslian** (siapa yang menandatangani) dan **integritas** (dokumen tidak berubah). Menambahkan timestamp membuktikan tanda tangan ada pada waktu tertentu, melindungi Anda bahkan jika sertifikat penandatangan kemudian kedaluwarsa atau dicabut. Bersama-sama keduanya memberikan non‑repudiation—kritikal untuk alur kerja hukum, keuangan, dan regulasi.

## Menyiapkan GroupDocs.Signature untuk Java

### Metode Integrasi

Pilih alat build yang Anda sukai:

**Untuk pengguna Maven**  
Tambahkan dependensi ke `pom.xml` Anda:

Koordinat Maven berikut akan mengambil rilis stabil terbaru dari GroupDocs.Signature untuk Java.

```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

**Untuk pengguna Gradle**  
Tambahkan baris ke `build.gradle` Anda:

Gradle akan mengunduh library dari Maven Central.

```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

**Unduhan langsung (jika Anda lebih suka)**  
Kunjungi [GroupDocs.Signature for Java releases](https://releases.groupdocs.com/signature/java/) dan unduh file JAR. Tambahkan ke classpath proyek Anda secara manual. Lihat [GroupDocs.Signature Documentation](https://docs.groupdocs.com/signature/java/) untuk referensi API lengkap. Untuk build terbaru, lihat [Latest Version & Releases](https://releases.groupdocs.com/signature/java/).

*Tip Pro:* Maven atau Gradle mengotomatisasi pembaruan versi dan dependensi transitif, menghemat waktu Anda ketika patch keamanan baru dirilis.

### Mengatur lisensi Anda

GroupDocs menawarkan tiga opsi lisensi:

1. **Uji coba gratis** – evaluasi semua fitur tanpa watermark. [Download Trial Version](https://releases.groupdocs.com/signature/java/)  
2. **Lisensi sementara** – kunci akses penuh selama 30 hari untuk pengembangan.  
3. **Lisensi komersial** – siap produksi, penggunaan tak terbatas. [Buy License](https://purchase.groupdocs.com/buy)

Jika Anda memiliki pertanyaan, komunitas aktif di [GroupDocs Forum](https://forum.groupdocs.com/c/signature/).

### Inisialisasi Dasar

`Signature` adalah objek tingkat atas GroupDocs.Signature yang mewakili satu file PDF dalam memori. Setelah Anda membuat instance, semua operasi baca/tulis mengalir melalui objek ini.

```java
import com.groupdocs.signature.Signature;

String filePath = "YOUR_DOCUMENT_DIRECTORY/sample.pdf";
final Signature signature = new Signature(filePath);
```

## Cara menambahkan tanda tangan digital ke PDF Java: langkah‑demi‑langkah

Prosesnya linear: impor kelas, tentukan jalur file, buat objek `Signature`, konfigurasikan `DigitalSignature` dengan timestamp opsional, definisikan `SignOptions`, lalu tandatangani dan simpan.

### Langkah 1: impor kelas yang diperlukan

Impor berikut memberi Anda akses ke konfigurasi tanda tangan, penempatan, dan fungsionalitas timestamp.

```java
import com.groupdocs.signature.Signature;
import com.groupdocs.signature.domain.enums.HorizontalAlignment;
import com.groupdocs.signature.domain.enums.VerticalAlignment;
import com.groupdocs.signature.domain.signatures.PdfDigitalSignature;
import com.groupdocs.signature.domain.structs.TimeStamp;
import com.groupdocs.signature.options.sign.DigitalSignOptions;
```

### Langkah 2: definisikan jalur file Anda

Siapkan jalur untuk PDF input, sertifikat (PFX), dan lokasi output. Jaga file sertifikat tetap aman; ia berisi kunci pribadi Anda.

```java
String filePath = "YOUR_DOCUMENT_DIRECTORY/sample.pdf";
String certificatePath = "YOUR_DOCUMENT_DIRECTORY/certificate.pfx";
String outputFilePath = "YOUR_OUTPUT_DIRECTORY/digitallySignedTimeStamp.pdf";
```

### Langkah 3: inisialisasi objek Signature

`Signature` adalah titik masuk untuk semua tindakan penandatanganan. Membuatnya memuat PDF ke memori dan menyiapkan API untuk operasi selanjutnya.

```java
final Signature signature = new Signature(filePath);
```

### Langkah 4: konfigurasikan properti tanda tangan dan timestamp

`DigitalSignature` adalah segel kriptografis yang akan disematkan dalam PDF. Anda juga dapat melampirkan timestamp dari otoritas tepercaya.

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

Kami menggunakan FreeTSA (otoritas timestamp gratis) untuk demonstrasi. Dalam produksi, pilih TSA komersial untuk jaminan uptime dan status hukum.

### Langkah 5: konfigurasikan opsi tanda tangan digital

`SignOptions` menggabungkan sertifikat, tampilan visual, dan pengaturan penempatan untuk tanda tangan digital.

```java
DigitalSignOptions options = new DigitalSignOptions(certificatePath);
options.setPassword("YourCertificatePassword"); // Certificate password
options.setSignature(pdfDigitalSignature); // Attach the PdfDigitalSignature object

// Specify signature alignment (where it appears on the page)
options.setVerticalAlignment(VerticalAlignment.Bottom);
options.setHorizontalAlignment(HorizontalAlignment.Right);
```

### Langkah 6: tandatangani dan simpan dokumen

`SignResult` memberikan hasil operasi penandatanganan, termasuk status keberhasilan dan peringatan apa pun.

```java
try {
    SignResult signResult = signature.sign(outputFilePath, options);
    System.out.println("Document signed successfully!");
    System.out.println("Output: " + outputFilePath);
} catch (Exception e) {
    throw new RuntimeException("Error during signing process: " + e.getMessage());
}
```

## Kesalahan umum yang harus dihindari

### 1. masalah sertifikat
**Masalah:** error “Invalid certificate”.  
**Solusi:** Verifikasi kata sandi dengan `keytool -list -v -keystore your.pfx`.

```bash
keytool -list -v -keystore certificate.pfx -storetype PKCS12
```

### 2. timeout layanan timestamp
**Masalah:** timeout jaringan saat menghubungi TSA.  
**Solusi:** Uji konektivitas (`curl -I https://freetsa.org/tsr`), tambahkan logika retry, atau konfigurasikan TSA cadangan.

```java
new File(outputFilePath).getParentFile().mkdirs();
```

### 3. masalah izin file
**Masalah:** “Access denied” saat menyimpan.  
**Solusi:** Pastikan direktori output ada dan aplikasi memiliki izin menulis.

```bash
keytool -genkeypair -alias mykey -keyalg RSA -keysize 2048 -storetype PKCS12 -keystore certificate.pfx -validity 365
```

### 4. masalah memori dengan PDF besar
**Masalah:** `OutOfMemoryError` untuk file besar.  
**Solusi:** Tingkatkan heap JVM (`-Xmx4g`) atau proses file secara batch.

### 5. penempatan tanda tangan yang salah
**Masalah:** Tanda tangan menutupi konten yang ada.  
**Solusi:** Uji pengaturan alignment terlebih dahulu; untuk penempatan pixel‑perfect, gunakan opsi berbasis koordinat.

## Tips manajemen sertifikat

### Mendapatkan sertifikat untuk pengembangan
Buat sertifikat self‑signed dengan `keytool` Java untuk keperluan pengujian.

```java
   String certPassword = System.getenv("CERT_PASSWORD");
   ```

### Praktik terbaik sertifikat
1. **Jangan pernah menuliskan password secara hard‑code** – gunakan variabel lingkungan.  
2. **Rotasi sertifikat** sebelum kedaluwarsa.  
3. **Simpan kunci pribadi** di perangkat keras aman (HSM) untuk aplikasi dengan keamanan tinggi.  
4. **Cadangkan sertifikat** di lokasi yang terlindungi.  
5. **Validasi sertifikat** sebelum menandatangani untuk mendeteksi yang kedaluwarsa atau dicabut.

## Praktik keamanan terbaik

### 1. lindungi kunci pribadi
Simpan sertifikat di luar direktori proyek, gunakan konfigurasi spesifik lingkungan, dan pertimbangkan HSM untuk penerapan perusahaan.

### 2. validasi PDF input
Periksa kerusakan, tanda tangan yang ada, batas ukuran, dan kepatuhan konten sebelum menandatangani.

### 3. terapkan pencatatan audit
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

### 4. gunakan otoritas timestamp tepercaya
Jangan pernah mengandalkan waktu sistem lokal; selalu minta timestamp dari TSA yang mematuhi RFC 3161.

### 5. terapkan penanganan error
Tangkap pengecualian tanpa mengungkap detail sensitif.

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

## Kasus penggunaan dunia nyata dan aplikasi

1. **Sistem manajemen kontrak** – karyawan menandatangani NDA dan perjanjian secara elektronik; timestamp membuktikan tepat kapan setiap kontrak diterima.  
2. **Pemrosesan dokumen keuangan** – menandatangani faktur dan purchase order secara batch, menyediakan jejak audit yang tidak dapat diubah untuk regulator.  
3. **Verifikasi kredensial pendidikan** – universitas mengeluarkan transkrip yang tidak dapat dimanipulasi dan dapat divalidasi secara instan melalui tautan QR‑code.  
4. **Manajemen lisensi perangkat lunak** – menghasilkan sertifikat lisensi dengan tanda tangan digital dan timestamp untuk mencegah pemalsuan.  
5. **Kepatuhan regulasi (FDA 21 CFR Part 11, dll.)** – perusahaan perangkat medis menandatangani SOP dan laporan validasi; timestamp memenuhi persyaratan non‑repudiation.

## Pertimbangan kinerja dan optimasi

### Manajemen memori
Proses PDF besar secara batch, tutup objek `Signature` dengan cepat, dan tingkatkan ukuran heap bila diperlukan.

### Optimasi jaringan untuk timestamp
Gunakan pooling koneksi HTTP, terapkan retry dengan backoff eksponensial, dan cache timestamp untuk penandatanganan berurutan yang cepat.

### Praktik terbaik pemrosesan batch

```java
// Pseudo‑code: process a list of PDFs in parallel, limiting to 5 concurrent TSA calls
```  
*Hindari memunculkan terlalu banyak thread; 5‑10 penandatanganan bersamaan menyeimbangkan throughput dan beban TSA.*

### Optimasi I/O disk
Gunakan SSD untuk file sementara, minimalkan siklus baca/tulis, dan bersihkan artefak sementara setelah setiap proses penandatanganan.

## Panduan pemecahan masalah

### Error: “Invalid certificate password”
**Solusi:** Verifikasi kata sandi dengan `keytool -list -keystore your.pfx`.

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

### Error: “Timestamp authority not responding”
**Solusi:** Uji URL TSA, periksa aturan firewall, dan tambahkan logika TSA cadangan.

```bash
keytool -list -v -keystore certificate.pfx -storetype PKCS12
```

### Error: “PDF is already signed”
**Solusi:** Deteksi tanda tangan yang ada terlebih dahulu; tambahkan counter‑signature atau tandatangani salinan baru.

### Error: “Access denied” when saving
**Solusi:** Pastikan direktori output ada, aplikasi memiliki hak menulis, dan tidak ada proses lain yang mengunci file.

```java
TimeStamp timeStamp;
try {
    timeStamp = new TimeStamp("https://freetsa.org/tsr", "", "");
} catch (Exception e) {
    // Fallback to alternative TSA
    timeStamp = new TimeStamp("https://alternate-tsa.com/tsr", "", "");
}
```

### Error: OutOfMemoryError
**Solusi:** Tingkatkan heap JVM, proses PDF dalam batch lebih kecil, atau beralih ke API streaming untuk file sangat besar.

## Kesimpulan dan langkah selanjutnya

Anda kini tahu **cara menandatangani PDF** dengan Java, menambahkan timestamp tepercaya, dan menghindari kesalahan umum. Selanjutnya Anda dapat:

1. Menambahkan beberapa bidang tanda tangan untuk perjanjian multi‑pihak.  
2. Memverifikasi tanda tangan secara programatik dengan GroupDocs.Signature.  
3. Menyesuaikan tampilan visual tanda tangan (gambar, teks, penempatan).  
4. Membangun layanan penandatanganan batch yang kuat dengan antrian dan pemantauan.

## Pertanyaan yang sering diajukan

**Q: Apa perbedaan antara tanda tangan digital dan tanda tangan elektronik?**  
A: Tanda tangan digital menggunakan algoritma kriptografis untuk memverifikasi identitas dan mendeteksi manipulasi, sementara tanda tangan elektronik dapat sesederhana nama yang diketik.

**Q: Apakah saya memerlukan koneksi internet untuk menandatangani PDF?**  
A: Hanya untuk layanan timestamp; penandatanganan kriptografis itu sendiri berjalan secara lokal.

**Q: Apakah PDF yang ditandatangani dapat diedit kemudian?**  
A: Setiap modifikasi akan memutus tanda tangan, dan pembaca PDF akan menampilkan peringatan bahwa dokumen telah diubah.

**Q: Bagaimana cara memverifikasi PDF yang ditandatangani?**  
A: Sebagian besar pembaca PDF memverifikasi secara otomatis; secara programatik, gunakan API verifikasi GroupDocs.Signature untuk memeriksa status, detail penandatangan, dan keabsahan timestamp.

**Q: Apa yang terjadi jika sertifikat saya kedaluwarsa setelah saya menandatangani dokumen?**  
A: Timestamp yang disematkan membuktikan tanda tangan dibuat saat sertifikat masih berlaku, menjaga keabsahan hukum.

**Q: Bisakah saya menggunakan ini dengan penyimpanan cloud (S3, Azure Blob, dll.)?**  
A: Ya—unduh PDF ke lokasi sementara, tandatangani, lalu unggah versi yang ditandatangani kembali ke cloud.

**Q: Apakah ada batas ukuran file?**  
A: Library menangani PDF hingga 500 MB tanpa memuat seluruh file ke memori; file yang lebih besar mungkin memerlukan streaming.

**Q: Berapa biaya GroupDocs.Signature untuk penggunaan komersial?**  
A: Harga bervariasi tergantung tipe deployment; hubungi tim penjualan GroupDocs untuk tarif terbaru. Uji coba gratis dan lisensi sementara tersedia untuk evaluasi.

**Q: Apakah ini bekerja di server Linux?**  
A: Tentu saja. GroupDocs.Signature untuk Java bersifat platform‑independen dan berjalan di OS apa pun dengan JRE.

**Terakhir Diperbarui:** 2026-09-05  
**Diuji Dengan:** GroupDocs.Signature 23.9 untuk Java  
**Penulis:** GroupDocs

## Tutorial terkait

- [Cara Memverifikasi Sertifikat Digital di Java - Panduan Lengkap dengan Contoh Kode](/signature/java/digital-signatures/java-certificate-verification-groupdocs-signature/)
- [Cara Menandatangani PDF secara Programatik di Java dengan GroupDocs.Signature](/signature/java/digital-signatures/sign-pdfs-groupdocs-signature-java/)
- [Menambahkan Tanda Tangan Gambar ke PDF Java dengan GroupDocs](/signature/java/image-signatures/sign-pdf-image-signature-groupdocs-java/)

```java
File outputFile = new File(outputFilePath);
outputFile.getParentFile().mkdirs(); // Create directories if needed

if (!outputFile.canWrite() && outputFile.exists()) {
    throw new IOException("Cannot write to " + outputFilePath);
}
```