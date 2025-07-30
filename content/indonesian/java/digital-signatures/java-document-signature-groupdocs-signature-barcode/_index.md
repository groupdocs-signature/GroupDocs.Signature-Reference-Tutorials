---
"date": "2025-05-08"
"description": "Pelajari cara menandatangani, memverifikasi, mencari, memperbarui, dan menghapus tanda tangan kode batang dalam dokumen menggunakan GroupDocs.Signature untuk Java. Tingkatkan efisiensi alur kerja dokumen Anda."
"title": "Panduan Tanda Tangan Barcode GroupDocs.Signature untuk Dokumen Master di Java"
"url": "/id/java/digital-signatures/java-document-signature-groupdocs-signature-barcode/"
"weight": 1
---

# Menguasai Tanda Tangan Dokumen di Java dengan GroupDocs.Signature

**Sederhanakan alur kerja dokumen digital Anda dengan menandatangani, memverifikasi, mencari, memperbarui, dan menghapus tanda tangan kode batang menggunakan GroupDocs.Signature untuk Java.**

Di dunia interaksi digital yang serba cepat, pengelolaan dokumen yang efisien sangatlah penting. Baik dalam menangani kontrak maupun dokumen penting lainnya, kemampuan untuk menandatangani, memverifikasi, mencari, memperbarui, dan menghapus tanda tangan dokumen akan meningkatkan produktivitas dan keamanan secara signifikan. Panduan komprehensif ini memandu Anda dalam penggunaan GroupDocs.Signature untuk Java—pustaka canggih yang menyederhanakan tugas-tugas ini dengan tanda tangan kode batang.

**Apa yang Akan Anda Pelajari:**
- Cara menandatangani dokumen menggunakan tanda tangan kode batang.
- Teknik untuk memverifikasi keaslian dokumen yang ditandatangani.
- Metode untuk mencari, memperbarui, dan menghapus tanda tangan kode batang yang ada di dokumen Anda.
- Aplikasi praktis dan tips pengoptimalan kinerja.

Sebelum masuk ke detail implementasi, pastikan Anda memiliki semua yang dibutuhkan untuk memulai.

## Prasyarat

Untuk mengikuti tutorial ini, Anda memerlukan:
- **Kit Pengembangan Java (JDK):** Pastikan JDK 8 atau yang lebih baru terinstal di sistem Anda.
- **Lingkungan Pengembangan Terpadu (IDE):** Kami merekomendasikan penggunaan IntelliJ IDEA atau Eclipse untuk pengembangan Java.
- **Pustaka GroupDocs.Signature:** Pustaka ini penting untuk menandatangani dan memverifikasi dokumen.

### Pustaka dan Ketergantungan yang Diperlukan

Anda dapat menambahkan GroupDocs.Signature ke proyek Anda menggunakan Maven, Gradle, atau dengan mengunduh JAR secara langsung:

**Pakar**
```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

**Gradle**
```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

Bagi mereka yang lebih suka mengunduh langsung, versi terbaru dapat ditemukan di [GroupDocs.Signature untuk rilis Java](https://releases.groupdocs.com/signature/java/).

### Akuisisi Lisensi

Untuk menjelajahi kemampuan GroupDocs.Signature secara menyeluruh, pertimbangkan untuk mendapatkan lisensi sementara atau berlangganan. Anda dapat memulai dengan uji coba gratis untuk menguji fitur-fiturnya:

- **Uji Coba Gratis:** Kunjungi [Halaman unduhan GroupDocs](https://releases.groupdocs.com/signature/java/) untuk langkah pertama Anda.
- **Lisensi Sementara:** Dapatkan melalui [Halaman lisensi sementara GroupDocs](https://purchase.groupdocs.com/temporary-license/).
- **Opsi Pembelian:** Untuk penggunaan jangka panjang, kunjungi [Opsi pembelian GroupDocs](https://purchase.groupdocs.com/buy).

### Pengaturan Lingkungan

Pastikan Anda memiliki proyek Java yang siap di IDE pilihan Anda. Konfigurasikan jalur build atau `pom.xml` (untuk Maven) atau `build.gradle` (untuk Gradle) dengan dependensi GroupDocs.Signature. Setelah disiapkan, inisialisasi pustaka dalam proyek Anda dengan membuat instance `Signature`.

## Menyiapkan GroupDocs.Signature untuk Java

GroupDocs.Signature menyederhanakan proses penandatanganan dan verifikasi dokumen menggunakan berbagai jenis tanda tangan, termasuk kode batang. Mulailah dengan mengimpor kelas-kelas yang diperlukan:

```java
import com.groupdocs.signature.Signature;
```

### Inisialisasi Dasar

Untuk menginisialisasi GroupDocs.Signature di aplikasi Java Anda, buat `Signature` objek dengan jalur ke dokumen target Anda:

```java
Signature signature = new Signature("path/to/your/document.pdf");
```

Dengan pengaturan ini, Anda siap menerapkan berbagai fungsi yang ditawarkan oleh GroupDocs.Signature.

## Panduan Implementasi

### Tanda Tangani Dokumen dengan Tanda Tangan Kode Batang

**Ringkasan:** Fitur ini memungkinkan Anda menambahkan tanda tangan kode batang ke dokumen apa pun. Kode batang dapat menyertakan teks seperti nama atau nomor identifikasi untuk keamanan tambahan dan kemudahan verifikasi.

#### Implementasi Langkah demi Langkah:
1. **Tentukan Jalur:**
   Tentukan jalur untuk dokumen masukan dan keluaran Anda:
   
   ```java
   String filePath = "YOUR_DOCUMENT_DIRECTORY/sample.docx";
   String outputFilePath = "YOUR_OUTPUT_DIRECTORY/signed_sample.docx";
   ```

2. **Buat Objek Tanda Tangan:**
   Inisialisasi a `Signature` objek dengan jalur dokumen Anda:

   ```java
   Signature signature = new Signature(filePath);
   ```

3. **Tetapkan Opsi Kode Batang:**
   Konfigurasikan opsi tanda kode batang, termasuk teks, jenis, perataan, ukuran, dan warna:

   ```java
   BarcodeSignOptions signOptions = new BarcodeSignOptions("John Smith", BarcodeTypes.Code128);
   signOptions.setVerticalAlignment(VerticalAlignment.Top);
   signOptions.setHorizontalAlignment(HorizontalAlignment.Center);
   signOptions.setWidth(100);
   signOptions.setHeight(40);
   signOptions.setMargin(new java.awt.Rectangle(20, 20, 0, 0));
   signOptions.setForeColor(Color.RED);

   SignatureFont signatureFont = new SignatureFont();
   signatureFont.setSize(12);
   signatureFont.setFamilyName("Comic Sans MS");
   signOptions.setFont(signatureFont);
   ```

4. **Tandatangani Dokumen:**
   Terapkan tanda tangan kode batang yang telah dikonfigurasikan ke dokumen:

   ```java
   signature.sign(outputFilePath, signOptions);
   ```

### Verifikasi Dokumen untuk Tanda Tangan Kode Batang

**Ringkasan:** Pastikan integritas dan keaslian dokumen yang ditandatangani dengan memverifikasi tanda tangan kode batangnya.

#### Implementasi Langkah demi Langkah:
1. **Verifikasi Pengaturan:**
   Muat dokumen yang telah Anda tandatangani ke dalam `Signature` obyek:

   ```java
   Signature signature = new Signature("YOUR_OUTPUT_DIRECTORY/signed_sample.docx");
   ```

2. **Konfigurasikan Opsi Verifikasi:**
   Tetapkan opsi verifikasi agar cocok dengan tanda tangan kode batang tertentu:

   ```java
   BarcodeVerifyOptions verifyOptions = new BarcodeVerifyOptions();
   verifyOptions.setAllPages(false); // Verifikasi hanya halaman pertama
   verifyOptions.setPageNumber(1);
   verifyOptions.setEncodeType(BarcodeTypes.Code128);
   verifyOptions.setText("John Smith");
   ```

3. **Lakukan Verifikasi:**
   Jalankan proses verifikasi dan periksa apakah tanda tangannya valid:

   ```java
   boolean isValid = signature.verify(verifyOptions) != null;
   ```

### Cari Dokumen untuk Tanda Tangan Barcode

**Ringkasan:** Temukan tanda tangan kode batang dengan cepat dalam dokumen untuk mengonfirmasi keberadaannya atau mengumpulkan informasi.

#### Implementasi Langkah demi Langkah:
1. **Inisialisasi Pencarian:**
   Muat dokumen Anda ke dalam `Signature` kelas:

   ```java
   Signature signature = new Signature("YOUR_OUTPUT_DIRECTORY/signed_sample.docx");
   ```

2. **Tetapkan Opsi Pencarian:**
   Tentukan opsi untuk mencari tanda tangan kode batang di semua halaman dokumen:

   ```java
   BarcodeSearchOptions searchOptions = new BarcodeSearchOptions();
   searchOptions.setAllPages(true);
   ```

3. **Jalankan Pencarian:**
   Ambil daftar tanda tangan kode batang yang ditemukan:

   ```java
   java.util.List<BarcodeSignature> signatures = signature.search(BarcodeSignature.class, searchOptions);
   ```

### Perbarui Tanda Tangan Kode Batang Dokumen

**Ringkasan:** Ubah tanda tangan kode batang yang ada di dokumen Anda untuk mencerminkan perubahan atau pembaruan.

#### Implementasi Langkah demi Langkah:
1. **Persiapan untuk Pembaruan:**
   Asumsikan Anda memiliki daftar tanda tangan yang diambil dari operasi pencarian sebelumnya:

   ```java
   List<BarcodeSignature> signaturesToUpdate = new ArrayList<>();
   ```

2. **Ubah Properti Tanda Tangan:**
   Sesuaikan properti seperti posisi dan ukuran untuk memperbarui tanda tangan:

   ```java
   if (!signaturesToUpdate.isEmpty()) {
       BarcodeSignature bcSignature = signaturesToUpdate.get(0);
       bcSignature.setLeft(bcSignature.getLeft() + 100);
       bcSignature.setTop(bcSignature.getTop() + 100);
       bcSignature.setWidth(200);
       bcSignature.setHeight(50);
   }
   ```

3. **Terapkan Pembaruan:**
   Simpan perubahan pada dokumen Anda:

   ```java
   ByteArrayOutputStream outputStream = new ByteArrayOutputStream();
   signature.update(outputStream, signaturesToUpdate);
   ```

### Hapus Tanda Tangan Kode Batang Dokumen

**Ringkasan:** Hapus tanda tangan kode batang yang tidak diperlukan atau kedaluwarsa dari suatu dokumen.

#### Implementasi Langkah demi Langkah:
1. **Persiapan untuk Penghapusan:**
   Asumsikan Anda memiliki daftar tanda tangan yang diambil dari operasi pencarian sebelumnya:

   ```java
   List<BarcodeSignature> signaturesToDelete = new ArrayList<>();
   ```

2. **Hapus Tanda Tangan:**
   Hapus tanda tangan kode batang yang ditentukan dari dokumen Anda:

   ```java
   signature.delete(signaturesToDelete);
   ```