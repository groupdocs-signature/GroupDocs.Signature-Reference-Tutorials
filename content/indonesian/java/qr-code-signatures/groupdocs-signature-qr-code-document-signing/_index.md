---
"date": "2025-05-08"
"description": "Pelajari cara menggunakan GroupDocs.Signature untuk Java untuk menandatangani dokumen secara aman menggunakan kode QR yang mengodekan data HIBC. Sederhanakan proses manajemen dokumen Anda hari ini."
"title": "Penandatanganan Dokumen Master dengan Kode QR Menggunakan GroupDocs.Signature untuk Java&#58; Panduan Lengkap"
"url": "/id/java/qr-code-signatures/groupdocs-signature-qr-code-document-signing/"
"weight": 1
type: docs
---
# Penandatanganan Dokumen Master dengan Kode QR Menggunakan GroupDocs.Signature untuk Java

## Perkenalan

Di era digital, pengelolaan dan pengamanan data farmasi yang efisien sangat penting untuk kepatuhan dan efisiensi operasional. Mengintegrasikan informasi produk yang komprehensif ke dalam dokumen bisa menjadi tantangan tersendiri. Tutorial ini menunjukkan cara menggunakan **GroupDocs.Signature untuk Java** untuk mengkodekan data Kode Batang Industri Kesehatan (HIBC) dalam kode QR dan menandatangani dokumen dengan mudah.

### Apa yang Akan Anda Pelajari:
- Siapkan GroupDocs.Signature untuk Java.
- Buat contoh HIBCLICPrimaryData, HIBCLICSecondaryAdditionalData, dan bentuk gabungannya.
- Tandatangani dokumen menggunakan kode QR yang mengkodekan informasi produk terperinci.
- Mengoptimalkan kinerja sambil mengelola sumber daya secara efektif.

## Prasyarat

### Pustaka dan Ketergantungan yang Diperlukan
Untuk menggunakan GroupDocs.Signature untuk Java, pastikan Anda memiliki:
- **Kit Pengembangan Java (JDK)**: Versi 8 atau lebih tinggi.
- **Pakar** atau **Gradle**: Untuk manajemen ketergantungan.

### Persyaratan Pengaturan Lingkungan
Pastikan lingkungan pengembangan Anda dikonfigurasi untuk menggunakan Maven atau Gradle, menyederhanakan manajemen ketergantungan dan pembangunan proyek.

### Prasyarat Pengetahuan
Kemampuan dalam pemrograman Java akan membantu dalam memahami potongan kode dan detail implementasi.

## Menyiapkan GroupDocs.Signature untuk Java

### Informasi Instalasi

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

**Unduh Langsung**: Unduh versi terbaru dari [GroupDocs.Signature untuk rilis Java](https://releases.groupdocs.com/signature/java/).

### Langkah-Langkah Perolehan Lisensi
1. **Uji Coba Gratis**: Mulailah dengan mengunduh uji coba untuk menguji fungsionalitas dasar.
2. **Lisensi Sementara**:Dapatkan ini untuk akses penuh tanpa batasan selama periode evaluasi Anda.
3. **Pembelian**:Pertimbangkan untuk membeli lisensi untuk proyek jangka panjang.

#### Inisialisasi dan Pengaturan Dasar
Setelah terinstal, inisialisasi `Signature` objek dengan jalur file dokumen yang ingin Anda tandatangani:
```java
String filePath = "Sample.pdf";
Signature signature = new Signature(filePath);
```

## Panduan Implementasi

### Buat Data Primer HIBC LIC
**Ringkasan**:Bagian ini menunjukkan cara membuat dan mengonfigurasi instance `HIBCLICPrimaryData`, yang menyimpan informasi produk penting.

#### Langkah 1: Inisialisasi Objek Data Primer
```java
HIBCLICPrimaryData primaryData = new HIBCLICPrimaryData();
```

#### Langkah 2: Tetapkan Properti Esensial
- **Nomor Produk atau Katalog**: Pengidentifikasi unik untuk produk.
- **Kode Identifikasi Pelabel**: Mengidentifikasi produsen.
- **ID Satuan Ukur**: Menentukan unit pengukuran.

```java
primaryData.setProductOrCatalogNumber("12345");
primaryData.setLabelerIdentificationCode("A999");
primaryData.setUnitOfMeasureID(1);
```

### Buat Data Tambahan Sekunder HIBC LIC
**Ringkasan**:Bagian ini mencakup pembuatan dan konfigurasi instance `HIBCLICSecondaryAdditionalData`, yang mencakup rincian tambahan seperti tanggal kedaluwarsa dan nomor lot.

#### Langkah 1: Inisialisasi Objek Data Sekunder
```java
HIBCLICSecondaryAdditionalData secondaryData = new HIBCLICSecondaryAdditionalData();
```

#### Langkah 2: Tetapkan Properti Tambahan
- **Tanggal Kedaluwarsa**: Gunakan tanggal saat ini untuk demonstrasi.
- **Jumlah, Nomor Lot, Nomor Seri**:Tentukan spesifikasi produk.
- **Tanggal Pembuatan dan Karakter Tautan**: Menetapkan rincian manufaktur.

```java
secondaryData.setExpiryDate(new Date());
secondaryData.setExpiryDateFormat(HIBCLICDateFormat.MMDDYY);
secondaryData.setQuantity(30);
secondaryData.setLotNumber("LOT123");
secondaryData.setSerialNumber("SERIAL123");
secondaryData.setDateOfManufacture(new Date());
secondaryData.setLinkCharacter('S');
```

### Gabungkan Data Primer dan Sekunder HIBC LIC
**Ringkasan**:Pelajari cara menggabungkan data primer dan sekunder menjadi satu `HIBCLICCombinedData` objek untuk pemrosesan yang efisien.

#### Langkah 1: Inisialisasi Objek Data Gabungan
```java
HIBCLICCombinedData combinedData = new HIBCLICCombinedData();
```

#### Langkah 2: Tetapkan Data Primer dan Sekunder
- Hubungkan kedua kumpulan data untuk membentuk struktur data yang lengkap.

```java
combinedData.setPrimaryData(primaryData);
combinedData.setSecondaryAdditionalData(secondaryData);
```

### Tanda Tangani Dokumen dengan Kode QR yang Berisi Data Gabungan HIBC LIC
**Ringkasan**:Bagian terakhir ini menunjukkan cara menandatangani dokumen menggunakan kode QR yang mengkodekan gabungan data HIBC.

#### Langkah 1: Tentukan Jalur File
```java
String filePath = "YOUR_DOCUMENT_DIRECTORY/Sample.pdf";
String outputFilePath = "YOUR_OUTPUT_DIRECTORY/SignWithQRCodeHIBCLICCombinedData/" + fileName;
```

#### Langkah 2: Siapkan Opsi Tanda Tangan Kode QR
- **Jenis Enkode**: Menggunakan `QrCodeTypes.HIBCLICQR` untuk menentukan jenis pengkodean.
- **Penugasan Data**: : Melewati data gabungan untuk dimasukkan dalam kode QR.

```java
Signature signature = new Signature(filePath);
try {
    QrCodeSignOptions options = new QrCodeSignOptions();
    options.setEncodeType(QrCodeTypes.HIBCLICQR);
    options.setData(combinedData);

    // Tanda tangani dan simpan dokumen
    signature.sign(outputFilePath, options);
} finally {
    if (signature != null) signature.dispose();
}
```

## Aplikasi Praktis
1. **Kepatuhan Farmasi**Sederhanakan kepatuhan terhadap standar peraturan menggunakan integrasi ini.
2. **Manajemen Rantai Pasokan**: Meningkatkan keterlacakan produk farmasi melalui kode QR dalam dokumen.
3. **Integrasi Sistem Layanan Kesehatan**:Menanamkan data produk yang komprehensif dalam catatan perawatan kesehatan untuk keselamatan pasien yang lebih baik.

## Pertimbangan Kinerja
- **Optimalkan Penggunaan Sumber Daya**: Pastikan manajemen memori yang efisien dengan membuang `Signature` objek pasca operasi.
- **Praktik Terbaik**: Perbarui secara berkala ke versi GroupDocs.Signature terbaru untuk peningkatan kinerja dan perbaikan bug.

## Kesimpulan
Dengan mengikuti panduan ini, Anda telah mempelajari cara membuat objek data primer dan sekunder HIBC LIC, menggabungkannya menjadi satu entitas, dan menandatangani dokumen dengan kode QR menggunakan GroupDocs.Signature untuk Java. Keterampilan ini meningkatkan keamanan dokumen dan memastikan kepatuhan dalam industri farmasi.

### Langkah Selanjutnya
- Jelajahi fungsionalitas tambahan GroupDocs.Signature.
- Integrasikan solusi ini dalam sistem Anda yang sudah ada untuk mengotomatiskan proses penandatanganan dokumen.

## Bagian FAQ
1. **Apa itu data HIBC?**
   - Data Kode Batang Industri Kesehatan (HIBC) mencakup informasi produk penting yang digunakan dalam industri perawatan kesehatan dan farmasi.
2. **Dapatkah saya menggunakan GroupDocs.Signature untuk jenis kode batang lainnya?**
   - Ya, GroupDocs.Signature mendukung berbagai format kode batang selain kode QR.
3. **Bagaimana jika format dokumen saya bukan PDF?**
   - GroupDocs.Signature mendukung berbagai format dokumen, termasuk Word dan Excel.
4. **Bagaimana cara menangani pengecualian selama penandatanganan?**
   - Terapkan blok try-catch untuk mengelola pengecualian secara efektif dan memastikan pembersihan sumber daya.
5. **Apakah ada batasan jumlah kode QR per dokumen?**
   - Tidak ada batasan yang melekat; namun, pertimbangkan implikasi kinerja saat menambahkan banyak kode.

## Sumber daya
- **Dokumentasi**: [GroupDocs.Signature untuk Dokumen Java](https://docs.groupdocs.com/signature/java/)
- **Referensi API**: [Referensi API GroupDocs](https://reference.groupdocs.com/signature/java/)
- **Unduh**: [GroupDocs.Rilis Terbaru](https://releases.groupdocs.com/signature/java/)
- **Pembelian**: [Beli Lisensi](https://purchase.groupdocs.com/buy)
- **Uji Coba Gratis**: [Coba Gratis](https://releases.groupdocs.com/signature/java/)
- **Lisensi Sementara**: [Daftar di sini](https://purchase.groupdocs.com/temporary-license/)