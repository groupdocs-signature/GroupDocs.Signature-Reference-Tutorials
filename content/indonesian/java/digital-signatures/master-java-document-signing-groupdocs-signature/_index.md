---
categories:
- Java Development
- Document Management
date: '2026-08-25'
description: Pelajari cara menambahkan barcode ke dokumen PDF dengan Java menggunakan
  GroupDocs.Signature. Panduan langkah demi langkah ini menunjukkan cara menambahkan
  barcode GS1DotCode, mengekstrak gambar, dan menghindari jebakan umum.
keywords:
- how to add barcode
- groupdocs signature java
- pdf document barcode
lastmod: '2026-08-25'
linktitle: Tambahkan Barcode ke PDF Java
og_description: Pelajari cara menambahkan barcode ke PDF dengan Java menggunakan GroupDocs.Signature.
  Tutorial langkah demi langkah, contoh kode, dan tips pemecahan masalah untuk barcode
  GS1DotCode.
og_image_alt: Guide showing Java code to embed GS1DotCode barcode into a PDF using
  GroupDocs.Signature
og_title: Cara menambahkan barcode ke PDF dengan Java – Panduan Lengkap
schemas:
- author: GroupDocs
  dateModified: '2026-08-25'
  description: Learn how to add barcode to PDF documents in Java using GroupDocs.Signature.
    This step‑by‑step guide shows how to add GS1DotCode barcodes, extract images,
    and avoid common pitfalls.
  headline: How to Add Barcode to PDF in Java
  type: TechArticle
- description: Learn how to add barcode to PDF documents in Java using GroupDocs.Signature.
    This step‑by‑step guide shows how to add GS1DotCode barcodes, extract images,
    and avoid common pitfalls.
  name: How to Add Barcode to PDF in Java
  steps:
  - name: Validate GS1 payloads before encoding.
    text: Validate GS1 payloads before encoding.
  - name: Choose barcode dimensions that balance scan reliability with layout constraints.
    text: Choose barcode dimensions that balance scan reliability with layout constraints.
  - name: Combine barcode signatures with cryptographic signatures for full security
      coverage.
    text: Combine barcode signatures with cryptographic signatures for full security
      coverage.
  type: HowTo
- questions:
  - answer: GS1DotCode is a compact 2‑D dot matrix that stores up to **3,116 characters**
      in a smaller footprint than QR codes, making it ideal for tiny labels and high‑speed
      printing.
    question: What is GS1DotCode and why is it different from QR codes?
  - answer: The free trial is limited to evaluation and adds a watermark to output
      files. Production use requires a purchased or temporary 30‑day license.
    question: Can I use a free trial for production deployments?
  - answer: Set `setPageNumber(pageIndex)` on the `BarcodeSignOptions` object, then
      adjust `setLeft()` and `setTop()` to place it precisely.
    question: How do I position the barcode on a specific page?
  - answer: 'Yes. Provide the password when constructing the `Signature` object: `new
      Signature("file.pdf", "password")`.'
    question: Does GroupDocs.Signature support password‑protected PDFs?
  - answer: Aim for at least **108 pt × 108 pt** (1.5 in × 1.5 in). Larger sizes improve
      readability, especially on low‑resolution printers.
    question: What is the minimum barcode size for reliable scanning?
  type: FAQPage
tags:
- java
- pdf-signing
- barcodes
- groupdocs
- document-security
title: Cara Menambahkan Barcode ke PDF dengan Java
type: docs
url: /id/java/digital-signatures/master-java-document-signing-groupdocs-signature/
weight: 1
---

# Cara menambahkan barcode ke PDF di Java

## Pendahuluan

Pernahkah Anda berjuang dengan keaslian dokumen dalam aplikasi Java Anda? Anda tidak sendirian. Baik Anda sedang membangun sistem inventaris, mengelola kontrak, atau menangani dokumen rantai pasokan, ada kemungkinan besar Anda memerlukan cara yang andal untuk menandatangani dan memverifikasi PDF secara otomatis.

Tanda tangan digital tradisional memang bagus, tetapi terkadang Anda memerlukan sesuatu yang lebih khusus—seperti tanda tangan barcode yang bekerja mulus dengan sistem pemindaian dan alur kerja otomatis. Di sinilah barcode GS1DotCode berguna.

**Apa yang akan Anda pelajari:**
- Cara menandatangani dokumen PDF dengan barcode GS1DotCode di Java
- Cara mengekstrak dan menyimpan gambar tanda tangan barcode
- Kapan (dan mengapa) menggunakan tanda tangan barcode dibandingkan metode tradisional
- Kesalahan umum dan cara menghindarinya

Pada akhir panduan ini, Anda akan memiliki solusi siap pakai yang dapat Anda integrasikan ke dalam proyek Java mana pun.

## Jawaban Cepat
- **Perpustakaan apa yang menambahkan barcode ke PDF di Java?** GroupDocs.Signature for Java.
- **Format barcode apa yang didukung?** GS1DotCode, matriks titik 2‑D yang kompak.
- **Apakah saya memerlukan lisensi berbayar?** Versi percobaan gratis dapat digunakan untuk pengujian; produksi memerlukan lisensi komersial.
- **Bisakah saya mengekstrak barcode sebagai gambar?** Ya, menggunakan API `BarcodeSignature`.
- **Versi Java apa yang diperlukan?** JDK 8 atau lebih tinggi.

## Apa itu cara menambahkan barcode?

*Cara menambahkan barcode* mengacu pada proses menyematkan grafik barcode yang dapat dibaca mesin ke dalam file PDF secara programatis sehingga barcode menjadi bagian dari aliran konten dokumen. Ini melibatkan pembuatan gambar barcode, penempatannya pada halaman, dan menyimpan PDF yang telah dimodifikasi, memastikan barcode tetap dapat dicari dan dicetak.

## Mengapa memilih barcode GS1DotCode?

GS1DotCode dirancang untuk situasi di mana ruang terbatas. Tidak seperti barcode linear yang memanjang secara horizontal, DotCode membuat matriks titik 2‑D yang memuat banyak informasi dalam area kecil. Ini membuatnya sempurna untuk:

- **Label produk kecil** di mana setiap milimeter penting  
- **Pencetakan berkecepatan tinggi** pada jalur produksi (format ini dirancang untuk itu)  
- **Pelacakan rantai pasokan** di mana Anda perlu mengkodekan struktur data yang kompleks  

Format ini dapat menangani hingga **3.116 karakter** dalam ruang yang kompak dan dapat dibaca dengan andal bahkan pada kecepatan tinggi atau dengan kerusakan parsial. Jika Anda bekerja di bidang ritel atau logistik, mitra Anda kemungkinan sudah menggunakan standar GS1—sehingga Anda berbicara dalam bahasa yang sama.

> **Tip pro:** Gunakan GS1DotCode ketika Anda perlu menyematkan lebih dari 20 karakter pada label yang lebih kecil dari 1 inci × 1 inci.

## Prasyarat

Sebelum Anda mulai menulis kode, pastikan lingkungan Anda memenuhi persyaratan berikut.

### Perpustakaan dan dependensi yang diperlukan
- **GroupDocs.Signature for Java** 23.12 atau lebih baru (mendukung **30+** format dokumen)
- Maven atau Gradle untuk manajemen dependensi

### Penyiapan lingkungan
- **JDK 8** atau yang lebih baru terpasang dan dikonfigurasi di `PATH` Anda
- Sebuah IDE seperti IntelliJ IDEA, Eclipse, atau NetBeans
- File PDF contoh untuk bereksperimen (PDF apa pun yang tidak dilindungi dapat digunakan)

### Prasyarat pengetahuan
- Sintaks Java dasar (variabel, metode, objek)
- Familiaritas dengan deklarasi dependensi Maven atau Gradle
- Pemahaman tentang I/O file di Java (misalnya, `FileInputStream`)

Jika ada item yang belum ada, berhentilah sejenak dan instal sekarang; langkah-langkah selanjutnya mengasumsikan semuanya sudah ada.

## Menyiapkan GroupDocs.Signature untuk Java

### Maven
Jika Anda menggunakan Maven, tambahkan dependensi berikut ke `pom.xml` Anda:

```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

Maven akan mengunduh perpustakaan dan semua dependensi transitif yang diperlukan secara otomatis.

### Gradle
Untuk pengguna Gradle, sisipkan baris ini ke dalam file `build.gradle` Anda:

```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

Gradle menyelesaikan paket dengan cara yang sama tanpa intervensi manual.

### Unduhan langsung
Jika Anda lebih suka manajemen manual, unduh file JAR dari halaman rilis resmi: [GroupDocs.Signature for Java releases](https://releases.groupdocs.com/signature/java/). Letakkan JAR di classpath proyek Anda.

**Tip pro:** Maven atau Gradle mempermudah peningkatan di masa depan—cukup naikkan nomor versi.

### Akuisisi lisensi
GroupDocs menawarkan tiga opsi lisensi:

- **Percobaan gratis** – tanpa kartu kredit, watermark diterapkan pada output
- **Lisensi sementara** – evaluasi penuh fitur selama 30 hari
- **Lisensi komersial** – menghapus batas percobaan dan memberikan hak produksi

Setelah memperoleh file lisensi, letakkan di folder resources proyek Anda dan muat sebelum objek `Signature` apa pun dibuat.

`License.setLicense` memuat file lisensi GroupDocs, memungkinkan operasi penuh fitur tanpa batas percobaan.

Jalankan potongan kode berikut untuk memverifikasi perpustakaan dimuat dengan benar:

```java
import com.groupdocs.signature.Signature;

public class InitializeGroupDocs {
    public static void main(String[] args) {
        // Create an instance of Signature
        Signature signature = new Signature("path/to/your/document.pdf");
        
        System.out.println("Initialization successful!");
    }
}
```

Jika Anda melihat “Initialization successful!” maka penyiapan selesai. Jika tidak, periksa kembali classpath dan jalur lisensi.

## Panduan Implementasi

Kami akan membahas dua fitur inti: (1) menandatangani PDF dengan barcode GS1DotCode dan (2) mengekstrak barcode tersebut sebagai file gambar.

### Fitur 1: menandatangani dokumen dengan barcode GS1DotCode

#### Cara menandatangani PDF dengan barcode GS1DotCode di Java?

Muat PDF target dengan `new Signature("source.pdf")`, konfigurasikan objek `BarcodeSignOptions` yang berisi data berformat GS1, dan panggil `sign()` untuk menghasilkan PDF baru yang menyematkan barcode. Operasi ini menulis barcode langsung ke dalam aliran konten PDF, mempertahankannya melalui pencetakan dan pemindaian ulang.

Proses ini melibatkan tiga langkah singkat: membuat instance `Signature`, menyiapkan `BarcodeSignOptions`, dan memanggil `sign()`. Kode di bawah ini menunjukkan setiap langkah.

##### 1. inisialisasi objek signature
The `Signature` class is the entry point for all document‑processing operations in GroupDocs.Signature.

```java
import com.groupdocs.signature.Signature;

String sourceFilePath = "YOUR_DOCUMENT_DIRECTORY/document.pdf";
final Signature signature = new Signature(sourceFilePath);
```

> **Mengapa ini penting:** Objek `Signature` mengabstraksi penanganan file, men‑stream PDF besar secara efisien tanpa memuat seluruh file ke memori.

##### 2. konfigurasikan opsi barcode
`BarcodeSignOptions` lets you specify the barcode type, encoded data, position, and dimensions.

```java
import com.groupdocs.signature.domain.signatures.BarcodeSignature;
import com.groupdocs.signature.options.sign.BarcodeSignOptions;
import com.groupdocs.signature.domain.barcodes.BarcodeTypes;

BarcodeSignOptions gs1DotCodeOptions = new BarcodeSignOptions("(01)04912345123459(15)970331(30)128(10)ABC123", BarcodeTypes.GS1DotCode);
gs1DotCodeOptions.setLeft(100); // Set barcode position
gs1DotCodeOptions.setTop(100);
gs1DotCodeOptions.setHeight(150);
gs1DotCodeOptions.setWidth(200);
```

> **Poin penting:**  
> - String yang dikodekan mengikuti GS1 Application Identifiers (AIs) seperti `(01)` untuk GTIN, `(15)` untuk tanggal kedaluwarsa, dll.  
> - `setLeft()` dan `setTop()` menggunakan poin (72 pts = 1 in).  
> - Ukuran minimum yang direkomendasikan untuk pemindaian yang andal adalah **108 pt × 108 pt** (1,5 in × 1,5 in).

##### 3. tandatangani dokumen
Add the configured options to a list (you can combine multiple signature types) and call `sign()`.

```java
import java.util.ArrayList;
import java.util.List;

List<com.groupdocs.signature.options.sign.SignOptions> listOptions = new ArrayList<>();
listOptions.add(gs1DotCodeOptions);
signature.sign("YOUR_OUTPUT_DIRECTORY/signed_document_with_gs1dotcode.pdf", listOptions);
```

> **Catatan kinerja:** Menggunakan kembali satu instance `Signature` untuk operasi batch mengurangi overhead pembuatan objek dan meningkatkan throughput.

### Fitur 2: menyimpan konten tanda tangan barcode ke file

#### Cara mengekstrak gambar barcode dari PDF yang ditandatangani di Java?

`BarcodeSignature` mewakili objek tanda tangan barcode yang diekstrak dari dokumen yang ditandatangani, memberikan akses ke data dan konten gambar.

Buat instance `BarcodeSignature` (atau dapatkan melalui `search()`), baca data gambar yang di‑encode Base64 melalui `getContent()`, dekode, dan tulis byte ke file PNG. Ini menghasilkan gambar mandiri yang dapat Anda tampilkan di UI atau kirim ke printer label.

##### 1. simulasi pembuatan tanda tangan barcode
In real scenarios you would obtain the `BarcodeSignature` from a search result; here we instantiate it manually for illustration.

```java
import com.groupdocs.signature.domain.signatures.BarcodeSignature;
import java.io.FileOutputStream;

String base64String = "SampleBase64EncodedData";
BarcodeSignature barcodeSignature = new BarcodeSignature(base64String);
```

##### 2. simpan konten ke file
Decode the Base64 string and write the resulting bytes to disk using a try‑with‑resources block.

```java
int imageNumber = 1;
String formatExtension = ".png";  // Assume PNG format

try (FileOutputStream outputStream = new FileOutputStream("YOUR_OUTPUT_DIRECTORY/barcode_image" + imageNumber + formatExtension)) {
    byte[] byteArray = barcodeSignature.getContent();
    if (byteArray != null) {
        outputStream.write(byteArray);
    }
}
```

> **Catatan:** `getContent()` mungkin mengembalikan `null` jika tanda tangan dibuat tanpa menyematkan gambar. Selalu periksa `null` sebelum menulis.

## Masalah umum dan solusi

### Masalah: barcode tidak dapat dipindai
**Gejala:** Barcode terlihat baik di penampil PDF tetapi pemindai mengembalikan kesalahan.

**Solusi:**  
- Tingkatkan ukuran barcode setidaknya **108 pt × 108 pt**.  
- Pastikan resolusi printer **≥ 300 dpi**.  
- Verifikasi string data GS1 mengikuti sintaks AI yang benar; tanda kurung yang hilang dapat merusak pemindai.

### Masalah: OutOfMemoryError pada PDF besar
**Gejala:** Memproses dokumen lebih besar dari **50 MB** memicu kegagalan heap‑space.

**Solusi:**  
- Jalankan JVM dengan heap yang lebih besar, misalnya `-Xmx2g`.  
- Proses dokumen dalam batch yang lebih kecil.  
- Secara eksplisit buang objek `Signature`: `signature.dispose()` setelah setiap file.

### Masalah: barcode muncul buram
**Gejala:** Barcode yang dihasilkan terlihat piksel pada PDF output.

**Solusi:**  
- Gunakan dimensi yang lebih besar; perpustakaan merender grafik vektor bila memungkinkan, tetapi memperkecil setelah pembuatan menimbulkan artefak.  
- Hindari konversi raster‑ke‑vektor; biarkan GroupDocs menangani rendering langsung dari definisi vektor.

### Masalah: pengecualian lisensi
**Gejala:** Kesalahan seperti “License not found” atau “Trial limitations exceeded”.

**Solusi:**  
- Letakkan file lisensi di root classpath (`src/main/resources`).  
- Panggil `License.setLicense("GroupDocs.Signature.lic")` **sebelum** instansiasi `Signature` apa pun.  
- Untuk lisensi sementara, konfirmasi tanggal kedaluwarsa (30 hari sejak penerbitan).

## Kapan menggunakan pendekatan ini

### Kasus penggunaan yang baik
- **Pelacakan rantai pasokan** – menyematkan ID produk, nomor batch, dan tanggal kedaluwarsa langsung pada dokumen pengiriman.  
- **Pencetakan label otomatis** – menghasilkan barcode secara langsung untuk setiap faktur PDF.  
- **Industri yang diatur** – standar GS1 wajib di banyak lingkungan ritel dan perawatan kesehatan.  

### Kapan mempertimbangkan alternatif
- Jika Anda hanya memerlukan integritas kriptografis, tanda tangan digital PKI standar lebih tepat.  
- Untuk anotasi visual sederhana, tanda tangan teks atau stempel gambar mungkin sudah cukup.  
- Ketika ukuran dokumen menjadi kendala kritis, hindari menambahkan gambar barcode resolusi tinggi; sebaliknya, gunakan QR code yang dapat lebih kecil untuk kepadatan data yang sebanding.

## Praktik keamanan terbaik

### Validasi data
Sanitasi data yang diberikan pengguna sebelum mengenkodenya ke dalam barcode. String GS1 yang tidak tepat dapat menyebabkan kesalahan pemindaian di hilir atau, dalam kasus terburuk, memicu overflow buffer pada firmware pemindai lama.

### Kontrol akses
Terapkan kontrol akses berbasis peran (RBAC) sehingga hanya pengguna yang berwenang yang dapat memanggil API penandatanganan. Simpan file lisensi dengan aman dan batasi izin sistem file.

### Pencatatan audit
Log setiap operasi penandatanganan dengan detail seperti ID pengguna, timestamp, jalur file sumber, dan payload GS1 yang tepat. Contoh potongan kode pencatatan:

```java
// Simple logging example (use a proper logging framework in production)
System.out.println("Document signed by: " + userId + " at " + new Date());
System.out.println("Barcode data: " + barcodeData);
```

### Deteksi manipulasi
Gabungkan tanda tangan barcode dengan tanda tangan digital kriptografis. Barcode menyediakan data yang dapat dibaca mesin, sementara tanda tangan digital menjamin integritas dan non‑repudiasi.

## Aplikasi praktis

### 1. manajemen rantai pasokan
Setiap slip pengemasan menerima barcode GS1DotCode yang mengkodekan GTIN, batch, dan tujuan pengiriman. Pemindai di setiap titik pemeriksaan secara otomatis memperbarui sistem ERP, mengurangi kesalahan entri manual sebesar **98 %**.

### 2. kontrol inventaris
Saat barang tiba, PDF penerimaan ditandatangani dengan barcode yang berisi nomor PO dan kuantitas item. Staf gudang memindai barcode, dan basis data inventaris diperbarui secara real time.

### 3. titik penjualan ritel
Faktur yang dicetak dengan barcode memungkinkan kasir memproses pengembalian dengan memindai faktur alih‑alih memasukkan ID transaksi secara manual, mengurangi waktu checkout rata‑rata sebesar **30 detik** per pengembalian.

### 4. dokumentasi perawatan kesehatan
Resep yang ditandatangani dengan barcode GS1DotCode menyematkan ID pasien, kode obat, dan instruksi dosis. Apotek memindai barcode, menghilangkan kesalahan transkripsi yang menyebabkan kejadian obat berbahaya.

## Pertimbangan kinerja

### Manajemen memori
GroupDocs.Signature streams PDF data, but you should still close resources promptly:

```java
try (Signature signature = new Signature(sourceFilePath)) {
    // Do your signing operations here
} // Signature automatically disposed here
```

Menggunakan try‑with‑resources menjamin objek `Signature` melepaskan handle file bahkan jika terjadi pengecualian.

### Tips pemrosesan batch
- Gunakan kembali instance `BarcodeSignOptions` yang sama ketika payload identik di banyak dokumen.  
- Paralelkan penandatanganan dengan `ExecutorService` untuk beban kerja CPU‑bound; server 8‑core tipikal dapat menandatangani **≈ 150 PDF per menit** ketika setiap file di bawah 5 MB.  
- Batasi panggilan validasi lisensi eksternal untuk menghindari pembatasan laju.

### Optimisasi format file
- Pilih PDF/A‑1b untuk arsip; ia mengompresi aliran dan mengurangi ukuran file hingga **40 %**.  
- Jaga dimensi barcode tidak lebih besar dari yang diperlukan; barcode 1,5 in × 1,5 in menambah kira‑kira **15 KB** pada PDF 2 MB.

## Kesimpulan

Anda kini memiliki alur kerja lengkap dan siap produksi untuk menambahkan tanda tangan barcode GS1DotCode ke file PDF di Java, mengekstrak barcode tersebut sebagai gambar, dan mengintegrasikan proses ke dalam pipeline manajemen dokumen yang lebih besar. Ingat untuk:

1. Validasi payload GS1 sebelum mengenkode.  
2. Pilih dimensi barcode yang menyeimbangkan keandalan pemindaian dengan batasan tata letak.  
3. Gabungkan tanda tangan barcode dengan tanda tangan kriptografis untuk cakupan keamanan penuh.

Langkah selanjutnya: jelajahi tipe tanda tangan lain yang ditawarkan oleh GroupDocs.Signature—QR code, stempel teks, dan sertifikat digital—semua memiliki antarmuka API yang konsisten.

---

## Pertanyaan yang sering diajukan

**T: Apa itu GS1DotCode dan mengapa berbeda dari QR code?**  
J: GS1DotCode adalah matriks titik 2‑D yang kompak yang menyimpan hingga **3.116 karakter** dalam jejak yang lebih kecil dibanding QR code, menjadikannya ideal untuk label kecil dan pencetakan berkecepatan tinggi.

**T: Bisakah saya menggunakan percobaan gratis untuk penerapan produksi?**  
J: Versi percobaan gratis terbatas untuk evaluasi dan menambahkan watermark pada file output. Penggunaan produksi memerlukan lisensi berbayar atau lisensi sementara 30 hari.

**T: Bagaimana cara menempatkan barcode pada halaman tertentu?**  
J: Atur `setPageNumber(pageIndex)` pada objek `BarcodeSignOptions`, lalu sesuaikan `setLeft()` dan `setTop()` untuk menempatkannya secara tepat.

**T: Apakah GroupDocs.Signature mendukung PDF yang dilindungi kata sandi?**  
J: Ya. Berikan kata sandi saat membuat objek `Signature`: `new Signature("file.pdf", "password")`.

**T: Bagaimana saya dapat memverifikasi bahwa tanda tangan barcode telah ditambahkan dengan benar?**  
`Signature.search()` mencari tanda tangan dalam dokumen, mengembalikan koleksi objek tanda tangan yang cocok. Gunakan `Signature.search()` dengan `BarcodeSearchOptions`. Objek `BarcodeSignature` yang dikembalikan berisi data yang di‑encode dan konten gambar untuk verifikasi.

**T: Apa ukuran barcode minimum untuk pemindaian yang andal?**  
J: Targetkan setidaknya **108 pt × 108 pt** (1,5 in × 1,5 in). Ukuran yang lebih besar meningkatkan keterbacaan, terutama pada printer beresolusi rendah.

**T: Bisakah saya menandatangani beberapa PDF secara bersamaan?**  
J: Ya. Buat thread pool dan buat objek `Signature` terpisah per thread; perpustakaan ini thread‑safe ketika setiap thread bekerja pada dokumen masing‑masing.

**T: Apakah ada batas berapa banyak barcode yang dapat saya sematkan dalam satu PDF?**  
J: Tidak ada batas keras, tetapi setiap barcode menambah kira‑kira **15 KB** data. Untuk PDF lebih besar dari **100 MB**, pertimbangkan pemrosesan batch untuk mengelola penggunaan memori.

**T: Apakah perpustakaan ini bekerja pada platform non‑Windows?**  
J: GroupDocs.Signature for Java bersifat platform‑agnostic dan berjalan pada OS apa pun dengan JRE yang kompatibel, termasuk Linux dan macOS.

**Terakhir Diperbarui:** 2026-08-25  
**Diuji Dengan:** GroupDocs.Signature 23.12 untuk Java  
**Penulis:** GroupDocs

## Tutorial Terkait

- [Cara Memverifikasi Tanda Tangan Barcode di Java Menggunakan GroupDocs.Signature](/signature/java/barcode-signatures/verify-barcode-signatures-groupdocs-signature-java/)
- [Buat Tanda Tangan Barcode Java – Perbarui Barcode PDF](/signature/java/barcode-signatures/java-groupdocs-signature-barcode-initialize-update/)
- [Tambahkan QR Code ke PDF Java - Panduan Lengkap dengan GroupDocs.Signature](/signature/java/qr-code-signatures/qr-code-signatures-java-groupdocs/)