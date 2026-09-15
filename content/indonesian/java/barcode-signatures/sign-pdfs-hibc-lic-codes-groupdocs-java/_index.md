---
categories:
- Document Signing
- Healthcare Integration
date: '2026-09-15'
description: Pelajari cara menandatangani PDF dengan barcode menggunakan GroupDocs.Signature
  untuk Java. Panduan langkah demi langkah menambahkan Data Matrix dan QR code dalam
  dokumen kesehatan.
keywords:
- sign pdf with barcode
- add qr code pdf
- hibc barcode java
- pdf signing java
- healthcare barcode signing
lastmod: '2026-09-15'
linktitle: Panduan Penandatanganan PDF HIBC Java
og_description: Tandatangani PDF dengan barcode menggunakan GroupDocs.Signature untuk
  Java. Pelajari cara menyisipkan Data Matrix dan QR code dalam dokumen kesehatan
  dalam beberapa langkah.
og_image_alt: 'Developer tutorial: sign PDF with HIBC barcode using GroupDocs.Signature
  for Java'
og_title: Tandatangani PDF dengan barcode menggunakan HIBC di Java – Panduan GroupDocs
schemas:
- author: GroupDocs
  dateModified: '2026-09-15'
  description: Learn how to sign PDF with barcode using GroupDocs.Signature for Java.
    Step‑by‑step guide for adding Data Matrix and QR codes in healthcare documents.
  headline: Sign PDF with barcode using HIBC in Java
  type: TechArticle
- description: Learn how to sign PDF with barcode using GroupDocs.Signature for Java.
    Step‑by‑step guide for adding Data Matrix and QR codes in healthcare documents.
  name: Sign PDF with barcode using HIBC in Java
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
- sign pdf
- barcode
- java
- healthcare
- groupdocs
title: Cara menandatangani PDF dengan barcode menggunakan HIBC di Java
type: docs
url: /id/java/barcode-signatures/sign-pdfs-hibc-lic-codes-groupdocs-java/
weight: 1
---

# Tandatangani PDF dengan barcode menggunakan HIBC di Java

Jika Anda membangun perangkat lunak logistik farmasi atau perawatan kesehatan, Anda mungkin telah menghadapi masalah pelacakan berbasis kertas, tanda tangan yang hilang, dan mimpi buruk audit. **Menandatangani PDF dengan barcode**—terutama Data Matrix HIBC atau kode QR—menciptakan jejak yang tahan manipulasi dan dapat dibaca mesin yang bertahan melalui pencetakan, pemindaian, dan tinjauan regulasi. Dalam tutorial ini Anda akan melihat secara tepat cara menambahkan barcode Data Matrix dan QR ke PDF menggunakan GroupDocs.Signature untuk Java.

## Jawaban Cepat
- **Perpustakaan apa yang menangani barcode HIBC di Java?** GroupDocs.Signature untuk Java.  
- **Format barcode apa yang paling kompak?** Data Matrix – ideal untuk label kecil.  
- **Bisakah saya menambahkan QR dan Data Matrix ke PDF yang sama?** Ya, cukup buat `QrCodeSignOptions` terpisah.  
- **Apakah saya memerlukan koneksi internet saat runtime?** Tidak, perpustakaan berfungsi sepenuhnya offline setelah instalasi.  
- **Versi Java apa yang direkomendasikan?** Java 11+ untuk kinerja produksi.

## Apa itu penandatanganan PDF dengan barcode HIBC?
`Signature` adalah kelas inti GroupDocs.Signature yang mewakili dokumen PDF dan memungkinkan penyisipan tanda tangan digital. Kelas `Signature` dalam GroupDocs.Signature untuk Java menyediakan metode untuk menyematkan barcode HIBC sebagai tanda tangan digital. Dengan menandatangani PDF menggunakan barcode HIBC, Anda membuat catatan yang dapat diverifikasi dan tahan manipulasi yang dapat dipindai pada titik mana pun dalam rantai pasokan.

## Mengapa menggunakan Data Matrix dan kode QR bersama-sama?
Data Matrix menawarkan jejak terkecil sambil dapat menampung hingga 2.335 karakter alfanumerik, menjadikannya sempurna untuk area label yang padat. Kode QR, di sisi lain, mendukung hingga 4.296 karakter dan dapat dibaca secara universal oleh smartphone. Menggabungkan keduanya memberi Anda keseimbangan terbaik antara efisiensi ruang dan kapasitas data, memastikan setiap pemangku kepentingan—dari pemindai gudang hingga aplikasi seluler—dapat membaca informasi yang mereka butuhkan.

## Prasyarat
- **JDK 11 atau lebih tinggi** (Java 8 dapat digunakan tetapi Java 11+ direkomendasikan untuk kinerja optimal).  
- **IDE** seperti IntelliJ IDEA, Eclipse, atau VS Code dengan ekstensi Java.  
- **Maven atau Gradle** untuk manajemen dependensi (contoh di bawah).  
- **PDF contoh** (misalnya `sample.pdf`) untuk menguji implementasi.  
- **Lisensi GroupDocs.Signature yang valid** (percobaan gratis untuk pengembangan, lisensi berbayar untuk produksi).

## Menyiapkan GroupDocs.Signature untuk Java

### Konfigurasi Maven
Tambahkan dependensi ke `pom.xml` Anda:

```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

### Konfigurasi Gradle
Untuk proyek Gradle, tambahkan ini ke `build.gradle` Anda:

```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

### Opsi unduhan langsung
Anda juga dapat mengunduh file JAR secara langsung dari [rilisan GroupDocs.Signature untuk Java](https://releases.groupdocs.com/signature/java/) dan menambahkannya ke classpath proyek Anda secara manual. Pendekatan ini bekerja dengan baik di lingkungan jaringan terbatas.

### Mendapatkan lisensi
Minta percobaan gratis atau lisensi sementara dari GroupDocs untuk menghapus watermark dan membuka semua fitur. Penyebaran produksi memerlukan lisensi yang dibeli.

### Inisialisasi dasar
`Signature` adalah titik masuk untuk semua operasi penandatanganan. Ia memuat PDF, menerapkan barcode, dan menulis file yang ditandatangani.

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
Instansiasi `Signature` dengan PDF sumber Anda, atur `QrCodeSignOptions` ke format **Data Matrix**, berikan string HIBC yang diformat dengan benar, dan panggil `sign()`. Perpustakaan menulis PDF yang ditandatangani ke tujuan, mempertahankan tata letak dan menyematkan barcode sebagai tanda tangan yang tahan manipulasi.

`QrCodeSignOptions` menentukan jenis barcode, konten, ukuran, dan penempatan untuk sebuah tanda tangan.

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

3. **Konfigurasikan opsi Data Matrix** – atur string HIBC, pilih `QrCodeTypes.HIBCLICDataMatrix`, dan tentukan koordinat penempatan. `QrCodeTypes` mengenumerasi format barcode yang didukung untuk tanda tangan HIBC.  

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
Untuk **membuat PDF Data Matrix**, instansiasi `Signature` dengan PDF sumber Anda, atur `QrCodeSignOptions` ke `QrCodeTypes.HIBCLICDataMatrix` dan berikan string HIBC yang diformat dengan benar, kemudian panggil `signature.sign(outputPath, options)`. Perpustakaan menulis PDF yang ditandatangani ke tujuan, mempertahankan tata letak dan menyematkan barcode sebagai tanda tangan yang tahan manipulasi.

## Cara menambahkan QR code PDF menggunakan GroupDocs.Signature?
Muat PDF, konfigurasikan `QrCodeSignOptions` untuk format QR, dan panggil `sign()`. Perpustakaan memperbesar gambar QR untuk keterbacaan dan menempatkannya berdasarkan koordinat yang Anda tentukan, menghindari tumpang tindih dengan konten yang ada. Ini memastikan barcode tetap dapat dipindai setelah pencetakan dan mematuhi standar HIBC.

`QrCodeSignOptions` mendefinisikan konten, ukuran, dan posisi barcode QR.

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

> **Jawaban langsung:** Gunakan `QrCodeTypes.HIBCLICQR` dalam `QrCodeSignOptions`, atur string konten HIBC, posisikan kode dengan `setLeft()` dan `setTop()`, kemudian panggil `signature.sign(outputPath, options)`. Barcode QR disematkan secara instan, siap untuk penangkapan oleh smartphone atau pemindai.

## Kesalahan umum yang harus dihindari

### 1. Lupa membebaskan sumber daya
**Salah:**  
```java
Signature signature = new Signature("sample.pdf");
signature.sign(destinFilePath, options);
// Oops, no dispose() call
```  
**Perbaikan:** Bungkus penggunaan `Signature` dalam blok try‑with‑resources atau panggil `close()` secara eksplisit dalam klausa finally.

### 2. Menggunakan string format HIBC yang tidak tepat
**Salah:** Menggunakan string umum seperti “12345”.  
**Perbaikan:** Ikuti standar HIBCC (misalnya, `A123PROD30917/75#422011907#GP293`). Validasi dengan [validator online HIBCC](https://www.hibcc.org/).

### 3. Menghard‑code jalur file
**Salah:**  
```java
String sourceFilePath = "C:/Users/John/Documents/test.pdf";
```  
**Perbaikan:** Simpan jalur dalam file konfigurasi atau variabel lingkungan dan baca mereka saat runtime.

### 4. Mengabaikan konflik posisi barcode
Tempatkan barcode jauh dari teks atau tanda tangan yang ada. Gunakan koordinat PDF (asalnya di kiri‑bawah) dan uji dengan contoh cetakan.

### 5. Tidak menguji dengan pemindai nyata
Cetak PDF yang ditandatangani dan pindai dengan perangkat keras yang tepat yang digunakan dalam alur kerja Anda. Verifikasi keterbacaan pada kualitas cetak yang berbeda.

## Aplikasi praktis dalam perawatan kesehatan

| Skenario | Barcode yang direkomendasikan | Mengapa cocok |
|----------|------------------------------|--------------|
| **Distribusi farmasi** | QR Code | Kapasitas data tinggi, banyak dipindai oleh smartphone. |
| **Manajemen inventaris** | Data Matrix | Jejak kecil, ideal untuk label rak yang padat. |
| **Kepatuhan regulasi (FDA 21 CFR Part 11)** | QR + Data Matrix | Format ganda memberikan redundansi dan auditabilitas. |
| **Pelacakan perangkat medis** | Aztec Code | Ukuran kompak bekerja pada kemasan dengan ruang terbatas. |

## Pertimbangan kinerja dan praktik terbaik

### Pola pemrosesan batch
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

### Jaga perpustakaan tetap diperbarui
Rilis GroupDocs meningkatkan kecepatan pemrosesan hingga **20 %** dan menambahkan fitur kepatuhan HIBC baru. Jadwalkan pemeriksaan dependensi setiap kuartal.

### Menyimpan templat dalam cache
Muat templat PDF sekali, kloning untuk setiap varian barcode, dan tandatangani klon tersebut. Ini mengurangi I/O dan mempercepat alur kerja volume tinggi.

## Pertanyaan yang sering diajukan

**Q: Bisakah GroupDocs.Signature menandatangani tipe file selain PDF?**  
A: Ya, ia juga mendukung DOCX, XLSX, PPTX, PNG, JPEG, dan TIFF dengan API penandatanganan barcode yang sama.

**Q: Bagaimana cara mengatasi error “Invalid barcode content”?**  
A: Verifikasi bahwa string HIBC Anda mengikuti sintaks HIBCC yang tepat, gunakan validator online, dan pastikan Anda menggunakan konstanta `QrCodeTypes` yang benar untuk format yang dipilih.

**Q: Berapa kapasitas data maksimum untuk setiap format HIBC?**  
A: QR ≈ 4.296 karakter alfanumerik, Aztec ≈ 3.832 numerik / 3.067 alfanumerik, Data Matrix ≈ 3.116 numerik / 2.335 alfanumerik. Jaga kode di bawah 200 karakter untuk keandalan pemindaian optimal.

**Q: Apakah memungkinkan menyematkan beberapa jenis barcode dalam satu PDF?**  
A: Tentu saja. Buat objek `QrCodeSignOptions` terpisah dengan posisi berbeda dan panggil `signature.sign()` untuk masing‑masing. Pastikan mereka tidak tumpang tindih.

**Q: Apakah saya memerlukan koneksi internet untuk menandatangani saat runtime?**  
A: Tidak. Setelah JAR berada di classpath dan lisensi diaktifkan, semua operasi dilakukan secara lokal.

## Sumber daya tambahan

- [Dokumentasi GroupDocs.Signature untuk Java](https://docs.groupdocs.com/signature/java/)  
- [Panduan Referensi API](https://reference.groupdocs.com/signature/java/)  
- [Unduhan Rilis Terbaru](https://releases.groupdocs.com/signature/java/)  
- [Beli Lisensi](https://purchase.groupdocs.com/buy)  
- [Dapatkan Percobaan Gratis](https://releases.groupdocs.com/signature/java/)  
- [Minta Lisensi Sementara](https://purchase.groupdocs.com/temporary-license/)  
- [Forum GroupDocs](https://forum.groupdocs.com/c/signature/)  

---

**Terakhir Diperbarui:** 2026-09-15  
**Diuji Dengan:** GroupDocs.Signature 23.12 untuk Java  
**Penulis:** GroupDocs  

## Tutorial terkait

- [Buat Tanda Tangan Barcode PDF di Java – Panduan GroupDocs](/signature/java/barcode-signatures/create-sign-pdfs-groupdocs-barcode-java/)
- [Buat Tanda Tangan Barcode di Java – Perbarui Barcode PDF](/signature/java/barcode-signatures/java-groupdocs-signature-barcode-initialize-update/)
- [Cara membaca PDF kode QR menggunakan Java dan GroupDocs.Signature](/signature/java/barcode-signatures/java-pdf-barcode-search-groupdocs-signature-api/)

```java
signature.sign(destinFilePath, hibcLic_DM);
```

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}