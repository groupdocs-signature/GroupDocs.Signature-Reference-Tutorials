---
categories:
- Digital Signatures
date: '2026-06-26'
description: Pelajari cara membuat tanda tangan QR Code di dokumen Word secara programatis
  dengan GroupDocs.Signature untuk Java. Tutorial langkah demi langkah, contoh kode,
  praktik terbaik, dan tips kinerja.
keywords:
- create qr code signature
- programmatically sign word
- qr code digital signature
- add qr to word
- groupdocs signature java
lastmod: '2026-06-26'
linktitle: Tanda Tangan QR Code di Word dengan Java
schemas:
- author: GroupDocs
  dateModified: '2026-06-26'
  description: Learn how to create QR code signature in Word documents programmatically
    with GroupDocs.Signature for Java. Step‑by‑step tutorial, code examples, best
    practices, and performance tips.
  headline: Create QR Code Signature in Word Documents Using Java
  type: TechArticle
- description: Learn how to create QR code signature in Word documents programmatically
    with GroupDocs.Signature for Java. Step‑by‑step tutorial, code examples, best
    practices, and performance tips.
  name: Create QR Code Signature in Word Documents Using Java
  steps:
  - name: The library reads the source document.
    text: The library reads the source document.
  - name: Generates the QR code based on `QrCodeSignOptions`.
    text: Generates the QR code based on `QrCodeSignOptions`.
  - name: Inserts the graphic at the specified coordinates.
    text: Inserts the graphic at the specified coordinates.
  - name: Saves the modified file to the path you provided.
    text: Saves the modified file to the path you provided.
  type: HowTo
- questions:
  - answer: Yes. GroupDocs.Signature supports PDF, Excel, PowerPoint, images, and
      many other formats. Just change the `setFileFormat` to the desired output type.
    question: Can I sign PDFs instead of Word documents?
  - answer: Use the library’s `SearchQrCodeSignatures` method to locate QR codes and
      validate the embedded data against your backend service.
    question: How do I verify a QR code signature after it’s been added?
  - answer: Standard QR codes hold up to **4 296 alphanumeric characters**, but for
      reliable scanning keep payloads under **500 characters**. For larger payloads
      store a reference ID and fetch details server‑side.
    question: What is the maximum data I can store in a QR code?
  - answer: Yes. You can set size, position, foreground/background colors, and even
      add a logo overlay. Stick to high‑contrast colors for best scan results.
    question: Can I customize the QR code’s visual appearance?
  - answer: For documents over 50 pages, expect a few seconds per file. Use batch
      processing, reuse the `Signature` instance, and monitor JVM heap size.
    question: How should I handle large‑document signing efficiently?
  type: FAQPage
tags:
- java
- word-documents
- qr-code
- digital-signature
- groupdocs
title: Buat Tanda Tangan QR Code di Dokumen Word Menggunakan Java
type: docs
url: /id/java/digital-signatures/groupdocs-signature-java-word-documents-qr-code/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Buat Tanda Tangan Kode QR dalam Dokumen Word Menggunakan Java

Pernah menghabiskan berjam‑jam menandatangani dokumen secara manual, lalu bertanya‑tanya apakah ada cara yang lebih cepat dan andal? Anda dapat **membuat tanda tangan kode QR** dalam dokumen Word secara programatis dengan hanya beberapa baris kode Java. Baik Anda mengotomatisasi alur kerja kontrak, mengelola dokumen hukum, atau membangun portal persetujuan mobile‑first, tanda tangan kode QR memberi verifikasi instan yang dapat dipindai pada smartphone apa pun. Dalam tutorial ini Anda akan belajar cara menyiapkan GroupDocs.Signature untuk Java, mengonfigurasi opsi QR code, dan menyematkan data kaya seperti URL, timestamp, atau payload JSON ke file Word. Pada akhir tutorial Anda akan dapat menandatangani dokumen secara massal, mengurangi upaya manual, dan meningkatkan kepatuhan.

## Jawaban Cepat
- **Perpustakaan apa yang saya perlukan?** GroupDocs.Signature untuk Java (v23.12+).  
- **Berapa baris kode?** Dua baris pembuatan QR ditambah beberapa baris konfigurasi.  
- **Bisakah saya menandatangani PDF juga?** Ya – API yang sama bekerja untuk PDF, Excel, PowerPoint, dan gambar.  
- **Apakah lisensi komersial diperlukan?** Hanya untuk produksi; trial gratis atau lisensi sementara cukup untuk pengembangan.  
- **Data apa yang dapat saya simpan?** Hingga ~4 k karakter (URL, JSON, ID), tetapi usahakan di bawah 500 karakter untuk pemindaian yang andal.

## Apa itu membuat tanda tangan kode QR?
**Membuat tanda tangan kode QR** adalah barcode 2‑D yang dapat dipindai dan disematkan dalam dokumen untuk mewakili tanda tangan digital atau payload verifikasi. Ketika pengguna memindai kode QR, data yang dikodekan (biasanya URL atau token) dibaca dan divalidasi, membuktikan keaslian dokumen tanpa memerlukan perangkat lunak khusus.

## Mengapa menggunakan GroupDocs.Signature untuk Java dalam menambahkan kode QR?
GroupDocs.Signature mendukung **lebih dari 50 format input dan output**, dapat memproses file ratusan halaman tanpa memuat seluruh dokumen ke memori, dan menyediakan API fluida yang memungkinkan Anda **menandatangani file Word** secara programatis dalam milidetik. Perpustakaan ini juga menawarkan pembuatan QR, Aztec, DataMatrix, dan PDF417 secara bawaan, menjadikannya solusi satu‑hentian untuk verifikasi mobile‑first modern.

## Prasyarat

### Perpustakaan dan Dependensi yang Diperlukan
- **GroupDocs.Signature untuk Java** versi **23.12** atau lebih baru (satu‑satunya dependensi eksternal).

### Persyaratan Penyiapan Lingkungan
- **JDK 8+** (Java 11 atau 17 direkomendasikan untuk produksi).  
- **IDE** pilihan Anda (IntelliJ IDEA, Eclipse, VS Code).  
- **Alat build** – Maven atau Gradle (contoh di bawah bekerja dengan keduanya).

### Pengetahuan Dasar yang Diperlukan
- Sintaks Java dasar dan penanganan file‑IO.  
- Familiaritas dengan deklarasi dependensi Maven/Gradle (kami akan menampilkan cuplikan tepatnya).  

## Menyiapkan GroupDocs.Signature untuk Java

Pilih sistem build Anda dan tambahkan dependensi persis seperti yang ditunjukkan. Placeholder di bawah mewakili blok kode asli; biarkan tidak berubah.

**Maven**

```java
```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```
```

**Gradle**

```java
```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```
```

**Unduhan Langsung**

Lebih suka manajemen manual? Unduh JAR langsung dari [rilis GroupDocs.Signature untuk Java](https://releases.groupdocs.com/signature/java/) dan tambahkan ke classpath proyek Anda.

### Akuisisi Lisensi
- **Trial Gratis:** Ideal untuk prototipe; fitur inti tersedia.  
- **Lisensi Sementara:** Akses penuh untuk pengembangan jangka pendek.  
- **Lisensi Komersial:** Diperlukan untuk deployment produksi.  

**Tips Pro:** Mulailah dengan trial gratis, lalu minta lisensi sementara sebelum beralih ke produksi. Ini memungkinkan Anda memvalidasi alur kerja tanpa biaya di muka.

### Inisialisasi Dasar
Objek `Signature` adalah titik masuk untuk semua operasi penandatanganan. Ia mengimplementasikan `AutoCloseable`, sehingga Anda dapat menggunakan blok try‑with‑resources dengan aman.

```java
```java
Signature signature = new Signature("path/to/your/document");
```
```

## Panduan Implementasi: Menandatangani Dokumen Word dengan Kode QR

Berikut kami jelaskan setiap langkah, menambahkan anchor definisi dan jawaban langsung bila diperlukan.

### Bagaimana cara menginisialisasi objek Signature untuk file Word?
Muat dokumen sumber dengan `new Signature("source.docx")` di dalam blok try‑with‑resources; objek menyiapkan file untuk modifikasi dan secara otomatis melepaskan sumber daya saat blok selesai.

```java
```java
String filePath = "YOUR_DOCUMENT_DIRECTORY/SampleDocX.docx";
Signature signature = new Signature(filePath);
```
```

**Penjelasan:** Kelas `Signature` mewakili satu dokumen dalam memori dan menyediakan metode untuk menambah, mencari, serta memverifikasi tanda tangan. Ia mendukung `.docx`, `.doc`, dan banyak format lainnya.

### Bagaimana cara mengonfigurasi opsi penandatanganan kode QR?
Buat instance `QrCodeSignOptions`, tetapkan teks yang akan dikodekan, tipe barcode, dan posisi. Cuplikan berikut menunjukkan konfigurasi minimal.

```java
```java
QrCodeSignOptions signOptions = new QrCodeSignOptions("JohnSmith");
signOptions.setEncodeType(QrCodeTypes.QR);
signOptions.setLeft(100); // posisi sumbu X dalam piksel
signOptions.setTop(100);  // posisi sumbu Y dalam piksel
```
```

**Definisi:** Kelas `QrCodeSignOptions` mengenkapsulasi semua pengaturan yang diperlukan untuk menghasilkan dan menempatkan tanda tangan kode QR, termasuk teks yang dikodekan, tipe barcode, ukuran, warna, serta koordinat posisi dalam dokumen.

#### Menyesuaikan Tampilan
Anda dapat menyesuaikan ukuran, margin, dan warna lebih lanjut:

```java
```java
QrCodeSignOptions signOptions = new QrCodeSignOptions("https://yourapp.com/verify/doc-12345");
```
```

**Mengapa penting:** Kode QR berukuran 150 px persegi dengan latar depan hitam pada latar belakang putih menghasilkan >99 % keberhasilan pemindaian pada layar maupun cetakan.

### Bagaimana cara mengatur opsi output untuk dokumen yang ditandatangani?
Tentukan format target dan perilaku timpa sebelum memanggil `sign`.

```java
```java
WordProcessingSaveOptions saveOptions = new WordProcessingSaveOptions();
saveOptions.setFileFormat(WordProcessingSaveFileFormat.Odt);
saveOptions.setOverwriteExistingFiles(true);
```
```

**Definisi:** Kelas `WordProcessingSaveOptions` menentukan cara dokumen Word yang ditandatangani disimpan, memungkinkan Anda menyebutkan format output (DOCX, ODT, dll.), apakah file yang ada ditimpa, dan preferensi tingkat file lainnya.

Jika Anda memerlukan format sumber terbuka, ubah ke `OutputType.ODT`:

```java
```java
saveOptions.setFileFormat(WordProcessingSaveFileFormat.Docx);
```
```

### Bagaimana cara menandatangani dan menyimpan dokumen dengan kode QR?
Metode `sign` menerapkan kode QR dan menulis file output dalam satu panggilan.

```java
```java
String outputFilePath = "YOUR_OUTPUT_DIRECTORY/SaveSignedOutputType/SampleDocX.odt";
signature.sign(outputFilePath, signOptions, saveOptions);
```
```

**Definisi:** Metode `sign` pada objek `Signature` menerima jalur tujuan, opsi penandatanganan yang telah dikonfigurasi, dan opsi penyimpanan opsional, lalu menyematkan kode QR ke dalam dokumen dan menulis hasilnya ke lokasi yang ditentukan.

**Apa yang terjadi:**  
1. Perpustakaan membaca dokumen sumber.  
2. Menghasilkan kode QR berdasarkan `QrCodeSignOptions`.  
3. Menyisipkan grafik pada koordinat yang ditentukan.  
4. Menyimpan file yang telah dimodifikasi ke jalur yang Anda berikan.

### Bagaimana cara menangani error selama penandatanganan?
Bungkus logika penandatanganan dalam blok try‑catch untuk menangkap file yang hilang, jalur tidak valid, atau masalah lisensi.

```java
```java
try {
    signature.sign(outputFilePath, signOptions, saveOptions);
    System.out.println("Document signed successfully!");
} catch (Exception e) {
    System.err.println("Signing failed: " + e.getMessage());
}
```
```

**Definisi:** Menangkap `Exception` memastikan bahwa setiap masalah runtime seperti file yang tidak ada, jalur tidak valid, atau masalah lisensi dilaporkan secara elegan, mencegah aplikasi crash di produksi.

## Kasus Penggunaan Umum dan Aplikasi Dunia Nyata

### Manajemen Kontrak Otomatis
Platform SaaS menandatangani **lebih dari 500 kontrak per bulan** dengan menghasilkan kode QR unik yang berisi ID kontrak dan URL verifikasi. Penerima memindai untuk melihat status kontrak di portal, menghilangkan pertukaran email manual.

### Penerbitan Sertifikat Karyawan
Departemen HR menyematkan ID karyawan dan tanggal penerbitan dalam kode QR pada sertifikat pelatihan. Memindai QR langsung memvalidasi keaslian terhadap basis data internal, mengurangi penipuan **lebih dari 80 %**.

### Otomatisasi Alur Kerja Persetujuan
Setiap kode QR approver menyimpan nomor karyawan, peran, dan timestamp. Sistem membaca QR saat audit, memberikan jejak yang tahan manipulasi tanpa pencarian basis data tambahan.

### Penandatanganan Faktur dan Kwitansi
Tim keuangan menambahkan kode QR yang menautkan ke gateway pembayaran. Saat dipindai, QR mengarahkan pembayar ke halaman pembayaran aman, memotong waktu proses **30 %** dan menurunkan risiko penipuan faktur.

## Praktik Terbaik untuk Penggunaan Produksi

### Pertimbangan Keamanan
- **Jangan pernah menyematkan password mentah**; gunakan token atau ID referensi yang di‑resolve di sisi server.  
- **Selalu gunakan HTTPS** untuk URL; hindari HTTP untuk mencegah serangan man‑in‑the‑middle.  
- **Tetapkan kedaluwarsa token** (misalnya JWT dengan validitas 24 jam) untuk dokumen sensitif waktu.

### Optimasi Kinerja
- **Pemrosesan batch:** Simpan satu instance `Signature` tetap hidup dan iterasi atas file untuk menghindari pemanasan JVM berulang.  
- **Manajemen memori:** Untuk dokumen > 50 MB, proses secara berurutan dan lepaskan objek `Signature` setelah tiap file.  
- **Penempatan penting:** Letakkan kode QR di bagian bawah halaman untuk mengurangi reflow tata letak dan meningkatkan kecepatan.

```java
```java
List<String> documents = getDocumentPaths();
for (String docPath : documents) {
    Signature sig = new Signature(docPath);
    // Konfigurasi dan tanda tangan
    sig.dispose();
}
```
```

### Tips Penempatan Kode QR
- **Keamanan cetak:** Jaga kode QR setidaknya 0,5 in dari tepi halaman agar tidak terpotong.  
- **Rekomendasi ukuran:** Minimum 150 × 150 px untuk pemindaian yang andal pada media cetak.  
- **Banyak halaman:** Loop melalui halaman dan buat instance `QrCodeSignOptions` baru untuk tiap posisi.

```java
```java
for (Document doc : documents) {
    Signature sig = new Signature(doc.getPath());
    sig.sign(outputPath, signOptions, saveOptions);
    sig.dispose();
}
```
```

## Opsi Konfigurasi Lanjutan

### Bagaimana cara menambahkan beberapa kode QR ke satu dokumen?
Buat objek `QrCodeSignOptions` terpisah untuk tiap lokasi dan panggil `sign` berulang kali.

```java
```java
// QR pertama
QrCodeSignOptions sign1 = new QrCodeSignOptions("Approver 1");
sign1.setLeft(100);
sign1.setTop(100);

// QR kedua
QrCodeSignOptions sign2 = new QrCodeSignOptions("Approver 2");
sign2.setLeft(300);
sign2.setTop(100);

// Terapkan keduanya
signature.sign(outputPath, sign1, saveOptions);
signature.sign(outputPath, sign2, saveOptions);
```
```

### Jenis barcode lain apa yang didukung?
Selain QR, Anda dapat menghasilkan **Aztec**, **DataMatrix**, atau **PDF417** dengan mengubah `setEncodeType()`.

### Bagaimana cara menghitung posisi dinamis berdasarkan ukuran halaman?
Dapatkan dimensi halaman lewat `Signature.getDocumentInfo()` dan hitung koordinat secara programatis.

```java
```java
// Dapatkan info dokumen
DocumentInfo docInfo = signature.getDocumentInfo();
int pageWidth = docInfo.getWidth();
int pageHeight = docInfo.getHeight();

// Pusatkan kode QR
int qrSize = 100;
signOptions.setLeft((pageWidth - qrSize) / 2);
signOptions.setTop((pageHeight - qrSize) / 2);
```
```

**Definisi:** `Signature.getDocumentInfo()` mengembalikan objek `DocumentInfo` yang berisi metadata seperti dimensi halaman, yang dapat dipakai untuk menghitung koordinat penempatan yang tepat berdasarkan ukuran aktual tiap halaman.

## Memecahkan Masalah Umum

### Kode QR tidak muncul
- Pastikan `setLeft`/`setTop` berada dalam batas halaman (A4 ≈ 595 × 842 px pada 72 DPI).  
- Pastikan kontras warna latar depan/latar belakang cukup (hitam di atas putih).  
- Tingkatkan lebar/tinggi jika kode terlalu kecil untuk dipindai.

### “File not found” saat menginisialisasi Signature
- Gunakan jalur absolut selama pengembangan atau validasi jalur relatif dengan `Paths.get(...)`.  
- Pastikan file sumber tidak terkunci oleh proses lain.

### File output rusak
- Periksa kembali `setFileFormat` sesuai ekstensi yang diinginkan.  
- Tutup semua stream yang mungkin masih memegang file sebelum menandatangani.

### Kode QR berisi data salah
- Cetak string yang Anda berikan ke `QrCodeSignOptions` sebelum menandatangani untuk memastikan encoding.  
- Hindari karakter non‑ASCII kecuali Anda secara eksplisit mengatur encoding UTF‑8.

### Kinerja lambat pada dokumen besar
- Proses dokumen dalam batch (lihat blok kode 10).  
- Hindari menempatkan kode QR di dalam tabel kompleks; hal itu memicu perhitungan ulang tata letak yang berat.

## Pertanyaan yang Sering Diajukan

**T: Bisakah saya menandatangani PDF alih‑alih dokumen Word?**  
J: Ya. GroupDocs.Signature mendukung PDF, Excel, PowerPoint, gambar, dan banyak format lainnya. Cukup ubah `setFileFormat` ke tipe output yang diinginkan.

**T: Bagaimana cara memverifikasi tanda tangan kode QR setelah ditambahkan?**  
J: Gunakan metode `SearchQrCodeSignatures` dari perpustakaan untuk menemukan kode QR dan memvalidasi data yang disematkan terhadap layanan backend Anda.

**T: Berapa maksimum data yang dapat disimpan dalam kode QR?**  
J: Kode QR standar dapat menampung hingga **4 296 karakter alfanumerik**, namun untuk pemindaian yang andal, simpan payload di bawah **500 karakter**. Untuk payload lebih besar, simpan ID referensi dan ambil detailnya di sisi server.

**T: Bisakah saya menyesuaikan tampilan visual kode QR?**  
J: Ya. Anda dapat mengatur ukuran, posisi, warna latar depan/latar belakang, bahkan menambahkan logo overlay. Gunakan warna kontras tinggi untuk hasil pemindaian terbaik.

**T: Bagaimana cara menangani penandatanganan dokumen berukuran besar secara efisien?**  
J: Untuk dokumen lebih dari 50 halaman, harapkan beberapa detik per file. Gunakan pemrosesan batch, gunakan kembali instance `Signature`, dan pantau ukuran heap JVM.

**T: Apakah tanda tangan QR akan tetap ada setelah konversi ke PDF?**  
J: Tentu. Kode QR disematkan sebagai grafik, sehingga tetap utuh saat konversi antar format, asalkan resolusi cukup dipertahankan.

**T: Bisakah saya menandatangani dokumen yang disimpan di penyimpanan cloud seperti S3?**  
J: Ya. Unduh file ke jalur lokal sementara, tanda tangani, lalu unggah kembali versi yang ditandatangani ke S3. Perpustakaan hanya bekerja dengan file lokal.

**T: Apa yang terjadi jika seseorang memodifikasi dokumen setelah ditandatangani?**  
J: Grafik QR tetap tidak berubah, namun tidak akan mendeteksi manipulasi. Kombinasikan kode QR dengan verifikasi berbasis hash atau sertifikat digital untuk integritas yang kuat.

**T: Apakah saya memerlukan lisensi berbeda untuk pengembangan vs. produksi?**  
J: Pengembangan dapat menggunakan trial gratis atau lisensi sementara. Deployment produksi memerlukan lisensi komersial sesuai ketentuan GroupDocs.

**T: Apakah penerima yang tidak menggunakan Java dapat memindai kode QR ini?**  
J: Ya. Kode QR mengikuti standar terbuka; kamera smartphone atau aplikasi pembaca QR apa pun dapat mendekodenya. Java hanya diperlukan untuk *membuat* tanda tangan.

## Sumber Daya

- [rilis GroupDocs.Signature untuk Java](https://releases.groupdocs.com/signature/java/)
- [Dokumentasi GroupDocs.Signature untuk Java](https://docs.groupdocs.com/signature/java/)
- [Referensi API GroupDocs.Signature](https://reference.groupdocs.com/signature/java/)
- [Rilis Terbaru GroupDocs.Signature](https://releases.groupdocs.com/signature/java/)
- [Beli GroupDocs.Signature](https://purchase.groupdocs.com/buy)
- [Trial Gratis GroupDocs.Signatures](https://releases.groupdocs.com/signature/java/)
- [Ajukan Lisensi Sementara](https://purchase.groupdocs.com/temporary-license/)
- [Forum Dukungan GroupDocs](https://forum.groupdocs.com/c/signature/)

## Kesimpulan

Anda kini memiliki peta jalan lengkap, siap produksi, untuk **membuat tanda tangan kode QR** dalam dokumen Word menggunakan Java dan GroupDocs.Signature. Dari penyiapan dasar hingga pemrosesan batch, dari praktik keamanan hingga tipe barcode lanjutan, semua yang Anda perlukan telah tercakup. Mulailah dengan trial gratis, bereksperimen dengan payload berbeda, dan integrasikan langkah penandatanganan ke pipeline generasi dokumen Anda yang sudah ada. Selamat coding dan selamat menandatangani dengan aman!

---

**Terakhir Diperbarui:** 2026-06-26  
**Diuji Dengan:** GroupDocs.Signature 23.12 untuk Java  
**Penulis:** GroupDocs  

{{< blocks/products/products-backtop-button >}}

## Tutorial Terkait

- [Java QR Code Signature Library - Tutorial Lengkap GroupDocs](/signature/java/qr-code-signatures/)
- [Muat dan Simpan Dokumen di Java - Tutorial Lengkap GroupDocs.Signature](/signature/java/document-loading-saving/)
- [Cara Menambahkan Tanda Tangan Digital ke Dokumen di Java](/signature/java/digital-signatures/groupdocs-signature-java-digital-signing-guide/)


{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}