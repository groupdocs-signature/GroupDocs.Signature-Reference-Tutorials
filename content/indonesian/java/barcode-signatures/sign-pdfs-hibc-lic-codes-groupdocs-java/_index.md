---
categories:
- Document Signing
- Healthcare Integration
date: '2026-05-16'
description: Pelajari cara membuat PDF Data Matrix dan menambahkan QR code PDF menggunakan
  GroupDocs.Signature untuk Java. Panduan langkah demi langkah untuk penandatanganan
  dokumen layanan kesehatan.
keywords:
- create data matrix pdf
- add qr code pdf
- HIBC barcode Java
lastmod: '2026-05-16'
linktitle: Panduan Penandatanganan PDF HIBC dengan Java
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
title: Buat PDF Data Matrix dengan Barcode HIBC di Java
type: docs
url: /id/java/barcode-signatures/sign-pdfs-hibc-lic-codes-groupdocs-java/
weight: 1
---

# Buat PDF Data Matrix dengan Barcode HIBC di Java

Jika Anda membangun perangkat lunak logistik farmasi atau perawatan kesehatan, Anda mungkin telah menemui masalah pelacakan berbasis kertas, tanda tangan yang hilang, dan mimpi buruk audit. **Membuat PDF Data Matrix** yang menyematkan barcode HIBC LIC menyelesaikan masalah tersebut dengan memberikan jejak yang tahan gangguan, dapat dibaca mesin, yang bertahan melalui pencetakan, pemindaian, dan tinjauan regulasi. Dalam tutorial ini Anda akan melihat secara tepat cara **menambahkan PDF kode QR** serta format Aztec dan Data Matrix, menggunakan GroupDocs.Signature untuk Java.

## Jawaban Cepat
- **Perpustakaan apa yang menangani barcode HIBC di Java?** GroupDocs.Signature for Java.  
- **Format barcode mana yang paling kompak?** Data Matrix – ideal untuk label kecil.  
- **Bisakah saya menambahkan QR dan Data Matrix ke PDF yang sama?** Ya, cukup buat `QrCodeSignOptions` terpisah.  
- **Apakah saya membutuhkan koneksi internet saat runtime?** Tidak, perpustakaan berfungsi sepenuhnya offline setelah instalasi.  
- **Versi Java apa yang direkomendasikan?** Java 11+ untuk kinerja produksi.

## Apa itu penandatanganan PDF barcode HIBC?
Kelas `Signature` dalam GroupDocs.Signature untuk Java mewakili dokumen PDF dan menyediakan metode untuk menyematkan barcode HIBC sebagai tanda tangan digital. Dengan menandatangani PDF dengan barcode HIBC Anda membuat catatan yang dapat diverifikasi, tahan gangguan, yang dapat dipindai pada titik mana pun dalam rantai pasokan.

## Mengapa menggunakan Data Matrix dan kode QR bersama-sama?
GroupDocs.Signature mendukung **lebih dari 50 format input dan output** dan dapat memproses PDF beratus‑ratus halaman tanpa memuat seluruh file ke memori. Menggunakan Data Matrix untuk label padat berukuran kecil dan QR untuk dokumen yang lebih luas memberi Anda keseimbangan terbaik antara keterbacaan, kapasitas data (hingga 4.296 karakter untuk QR), dan efisiensi ruang cetak.

## Prasyarat
- **JDK 11 atau lebih tinggi** (Java 8 berfungsi tetapi Java 11+ direkomendasikan untuk kinerja optimal).  
- **IDE** seperti IntelliJ IDEA, Eclipse, atau VS Code dengan ekstensi Java.  
- **Maven atau Gradle** untuk manajemen dependensi (contoh di bawah).  
- **PDF contoh** (mis., `sample.pdf`) untuk menguji implementasi.  
- **Lisensi GroupDocs.Signature yang valid** (percobaan gratis untuk pengembangan, lisensi berbayar untuk produksi).

## Menyiapkan GroupDocs.Signature untuk Java

### Konfigurasi Maven
Add the dependency to your `pom.xml`:

```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

### Konfigurasi Gradle
For Gradle projects, add this to your `build.gradle`:

```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

### Opsi Unduhan Langsung
Anda juga dapat mengunduh file JAR secara langsung dari [GroupDocs.Signature for Java releases](https://releases.groupdocs.com/signature/java/) dan menambahkannya ke classpath proyek Anda secara manual. Pendekatan ini bekerja dengan baik di lingkungan jaringan terbatas.

### Mendapatkan Lisensi
Minta percobaan gratis atau lisensi sementara dari GroupDocs untuk menghapus watermark dan membuka semua fitur. Penyebaran produksi memerlukan lisensi yang dibeli.

### Inisialisasi Dasar
Kelas `Signature` adalah titik masuk untuk semua operasi penandatanganan. Ia memuat PDF, menerapkan barcode, dan menulis file yang ditandatangani.

```java
import com.groupdocs.signature.Signature;

class InitializeSignature {
    public static void main(String[] args) {
        Signature signature = new Signature("sample.pdf");
        // Proceed with signing operations...
    }
}
```

## Cara membuat PDF Data Matrix dengan barcode HIBC?
Muat PDF sumber Anda, konfigurasikan objek `QrCodeSignOptions` untuk format Data Matrix, dan panggil `sign()` – itu semua yang Anda perlukan untuk menyematkan barcode HIBC Data Matrix yang sesuai. Langkah‑langkah berikut memandu Anda melalui kode yang tepat. `QrCodeSignOptions` mendefinisikan pengaturan untuk tanda tangan barcode, seperti tipe, konten, ukuran, dan posisi.

1. **Impor kelas yang diperlukan** – ini memberi Anda akses ke mesin tanda tangan dan opsi Data Matrix.  

```java
import com.groupdocs.signature.Signature;
import com.groupdocs.signature.options.sign.QrCodeSignOptions;
import com.groupdocs.signature.domain.qrcodes.QrCodeTypes;
```

2. **Instansiasi objek `Signature`** dengan jalur absolut untuk file sumber dan tujuan.  

```java
String sourceFilePath = "YOUR_DOCUMENT_DIRECTORY";
String destinFilePath = "YOUR_OUTPUT_DIRECTORY/SignWithHIBCLICQR.pdf";

final Signature signature = new Signature(sourceFilePath);
```

3. **Konfigurasikan opsi Data Matrix** – tetapkan string HIBC, pilih `QrCodeTypes.HIBCLICDataMatrix`, dan definisikan koordinat penempatan. `QrCodeTypes` mengenumerasi format barcode yang didukung untuk tanda tangan HIBC.  

```java
QrCodeSignOptions hibcLic_QR = new QrCodeSignOptions("A123PROD30917/75#422011907#GP293", QrCodeTypes.HIBCLICQR);
hibcLic_QR.setLeft(1); // Set the position from left
hibcLic_QR.setTop(1);   // Set the position from top
hibcLic_QR.setReturnContent(true); // Return content after signing
hibcLic_QR.setReturnContentType(FileType.PNG); // Specify return content type as PNG
```

4. **Terapkan tanda tangan** ke PDF.  

```java
signature.sign(destinFilePath, hibcLic_QR);
```

5. **Bebaskan sumber daya** untuk melepaskan handle file dan menghindari kebocoran memori.  

```java
finally {
    if (signature != null) signature.dispose();
}
```

### Contoh kerja lengkap
Berikut alur lengkap dalam satu blok (placeholder mewakili kode tepat yang akan Anda tempel dari cuplikan sebelumnya):

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

#### Jawaban langsung (40–70 kata)
Untuk **membuat PDF Data Matrix**, instansiasi `Signature` dengan PDF sumber Anda, atur `QrCodeSignOptions` ke `QrCodeTypes.HIBCLICDataMatrix` dan berikan string HIBC yang diformat dengan benar, lalu panggil `signature.sign(outputPath, options)`. Perpustakaan menulis PDF yang ditandatangani ke tujuan, mempertahankan tata letak dan menyematkan barcode sebagai tanda tangan tahan gangguan.

## Cara menambahkan PDF kode QR menggunakan GroupDocs.Signature?
Muat PDF, konfigurasikan `QrCodeSignOptions` untuk format QR, dan panggil `sign()`. Pola dua baris ini bekerja untuk ukuran PDF apa pun dan secara otomatis menyesuaikan ukuran gambar QR untuk keterbacaan optimal. `QrCodeSignOptions` mengonfigurasi tanda tangan barcode QR, termasuk konten dan properti visualnya. Ia menempatkan kode berdasarkan koordinat yang Anda tetapkan, memastikan tidak menimpa konten yang ada dan tetap dapat dipindai setelah pencetakan.

1. **Impor kelas khusus QR**  

```java
QrCodeSignOptions hibcLic_AZ = new QrCodeSignOptions("A123PROD30917/75#422011907#GP293", QrCodeTypes.HIBCLICAztec);
hibcLic_AZ.setLeft(1); // Set the position from left
hibcLic_AZ.setTop(200); // Set the position from top
hibcLic_AZ.setReturnContent(true); // Return content after signing
hibcLic_AZ.setReturnContentType(FileType.PNG); // Specify return content type as PNG
```

2. **Buat dan konfigurasikan opsi QR** – perhatikan penggunaan `QrCodeTypes.HIBCLICQR`.  

```java
signature.sign(destinFilePath, hibcLic_AZ);
```

3. **Tandatangani dokumen**  

```java
QrCodeSignOptions hibcLic_DM = new QrCodeSignOptions("A123PROD30917/75#422011907#GP293", QrCodeTypes.HIBCLICDataMatrix);
hibcLic_DM.setLeft(1); // Set the position from left
hibcLic_DM.setTop(400); // Set the position from top
hibcLic_DM.setReturnContent(true); // Return content after signing
hibcLic_DM.setReturnContentType(FileType.PNG); // Specify return content type as PNG
```

> **Jawaban langsung:** Gunakan `QrCodeTypes.HIBCLICQR` dalam `QrCodeSignOptions`, tetapkan string konten HIBC, posisikan kode dengan `setLeft()` dan `setTop()`, lalu panggil `signature.sign(outputPath, options)`. Barcode QR disematkan secara instan, siap untuk penangkapan oleh smartphone atau pemindai.

## Kesalahan Umum yang Harus Dihindari

### 1. Lupa Membebaskan Sumber Daya
**Salah:**  
```java
Signature signature = new Signature("sample.pdf");
signature.sign(destinFilePath, options);
// Oops, no dispose() call
```  

**Perbaikan:** Bungkus penggunaan `Signature` dalam blok try‑with‑resources atau panggil `close()` secara eksplisit dalam klausa finally.

### 2. Menggunakan String Format HIBC yang Salah
**Salah:** Menggunakan string generik seperti “12345”.  
**Perbaikan:** Ikuti standar HIBCC (mis., `A123PROD30917/75#422011907#GP293`). Validasi dengan [HIBCC online validator](https://www.hibcc.org/).

### 3. Menyandikan Jalur File Secara Hard‑code
**Salah:**  
```java
String sourceFilePath = "C:/Users/John/Documents/test.pdf";
```  

**Perbaikan:** Simpan jalur dalam file konfigurasi atau variabel lingkungan dan baca pada runtime.

### 4. Mengabaikan Konflik Posisi Barcode
Tempatkan barcode jauh dari teks atau tanda tangan yang ada. Gunakan koordinat PDF (asal di kiri‑bawah) dan uji dengan contoh cetak.

### 5. Tidak Menguji dengan Pemindai Nyata
Cetak PDF yang ditandatangani dan pindai dengan perangkat keras yang tepat digunakan dalam alur kerja Anda. Verifikasi keterbacaan pada kualitas cetak yang berbeda.

## Aplikasi Praktis di Kesehatan

| Skenario | Barcode yang Direkomendasikan | Mengapa cocok |
|----------|------------------------------|---------------|
| **Distribusi farmasi** | QR Code | Kapasitas data tinggi, banyak dipindai oleh smartphone. |
| **Manajemen inventaris** | Data Matrix | Jejak kecil, ideal untuk label rak yang padat. |
| **Kepatuhan regulasi (FDA 21 CFR Part 11)** | QR + Data Matrix | Format ganda memberikan redundansi dan auditabilitas. |
| **Pelacakan perangkat medis** | Aztec Code | Ukuran kompak bekerja pada kemasan dengan ruang terbatas. |

## Pertimbangan Kinerja dan Praktik Terbaik

### Pola Pemrosesan Batch
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

- Buat instance `Signature` baru per file untuk menjaga penggunaan memori tetap rendah.  
- Gunakan thread pool tetap (`Executors.newFixedThreadPool(Runtime.getRuntime().availableProcessors() - 1)`) untuk pemrosesan paralel, tetapi pantau ukuran heap karena setiap `Signature` menyimpan seluruh PDF di memori.  

### Jaga Perpustakaan Tetap Terbaru
Rilis GroupDocs meningkatkan kecepatan pemrosesan hingga **20 %** dan menambahkan fitur kepatuhan HIBC baru. Jadwalkan pemeriksaan dependensi setiap kuartal.

### Caching Template
Muat template PDF sekali, kloning untuk setiap varian barcode, dan tanda tangani klon tersebut. Ini mengurangi I/O dan mempercepat alur kerja volume tinggi.

## Pertanyaan yang Sering Diajukan

**T: Bisakah GroupDocs.Signature menandatangani tipe file selain PDF?**  
J: Ya, juga mendukung DOCX, XLSX, PPTX, PNG, JPEG, dan TIFF dengan API penandatanganan barcode yang sama.

**T: Bagaimana cara mengatasi error “Invalid barcode content”?**  
J: Verifikasi bahwa string HIBC Anda mengikuti sintaks HIBCC yang tepat, gunakan validator online, dan pastikan Anda menggunakan konstanta `QrCodeTypes` yang benar untuk format yang dipilih.

**T: Apa kapasitas data maksimum untuk setiap format HIBC?**  
J: QR ≈ 4.296 karakter alfanumerik, Aztec ≈ 3.832 numerik / 3.067 alfanumerik, Data Matrix ≈ 3.116 numerik / 2.335 alfanumerik. Jaga kode di bawah 200 karakter untuk keandalan pemindaian optimal.

**T: Apakah memungkinkan menyematkan beberapa tipe barcode dalam satu PDF?**  
J: Tentu saja. Buat objek `QrCodeSignOptions` terpisah dengan posisi berbeda dan panggil `signature.sign()` untuk masing‑masing. Pastikan tidak saling tumpang tindih.

**T: Apakah saya membutuhkan koneksi internet untuk menandatangani pada runtime?**  
J: Tidak. Setelah JAR berada di classpath dan lisensi diaktifkan, semua operasi dilakukan secara lokal.

## Sumber Daya Tambahan

- [GroupDocs.Signature for Java Documentation](https://docs.groupdocs.com/signature/java/)  
- [API Reference Guide](https://reference.groupdocs.com/signature/java/)  
- [Latest Release Downloads](https://releases.groupdocs.com/signature/java/)  
- [Purchase License](https://purchase.groupdocs.com/buy)  
- [Get Free Trial](https://releases.groupdocs.com/signature/java/)  
- [Request Temporary License](https://purchase.groupdocs.com/temporary-license/)  
- [GroupDocs Forum](https://forum.groupdocs.com/c/signature/)

---

**Terakhir Diperbarui:** 2026-05-16  
**Diuji Dengan:** GroupDocs.Signature 23.12 untuk Java  
**Penulis:** GroupDocs  

```java
signature.sign(destinFilePath, hibcLic_DM);
```

## Tutorial Terkait

- [Create Barcode Signature PDF in Java – GroupDocs Guide](/signature/java/barcode-signatures/create-sign-pdfs-groupdocs-barcode-java/)
- [Create Barcode Signature in Java – Update PDF Barcodes](/signature/java/barcode-signatures/java-groupdocs-signature-barcode-initialize-update/)
- [How to read QR code PDF using Java and GroupDocs.Signature](/signature/java/barcode-signatures/java-pdf-barcode-search-groupdocs-signature-api/)