---
"date": "2025-05-08"
"description": "Pelajari cara menandatangani lembar kerja Excel dengan kode QR dan menyimpannya dalam berbagai format menggunakan GroupDocs.Signature untuk Java. Amankan dokumen Anda secara efisien."
"title": "Menandatangani & Menyimpan Spreadsheet Excel dengan Kode QR di Java Menggunakan GroupDocs.Signature"
"url": "/id/java/qr-code-signatures/sign-save-spreadsheets-java-qr-codes-groupdocs-signature/"
"weight": 1
type: docs
---
# Menandatangani & Menyimpan Spreadsheet Excel dengan Kode QR di Java Menggunakan GroupDocs.Signature

## Perkenalan

Di era digital saat ini, memastikan keaslian dokumen menjadi semakin penting. Baik Anda menangani kontrak, perjanjian, maupun spreadsheet keuangan, menandatangani dokumen dengan aman dapat menghemat waktu dan mencegah penipuan. **GroupDocs.Signature untuk Java** adalah pustaka canggih yang menyederhanakan tanda tangan elektronik dalam berbagai format dokumen. Tutorial ini akan memandu Anda menggunakan GroupDocs.Signature untuk menandatangani lembar kerja Excel dengan kode QR dan menyimpannya dalam berbagai format.

### Apa yang Akan Anda Pelajari:
- Cara menandatangani spreadsheet menggunakan tanda tangan kode QR.
- Simpan dokumen yang ditandatangani dalam berbagai format keluaran seperti PDF, XLSX, dll.
- Optimalkan kinerja aplikasi Java Anda saat menangani tanda tangan dokumen.

Di akhir tutorial ini, Anda akan memiliki pemahaman yang mendalam tentang cara mengintegrasikan dan memanfaatkan GroupDocs.Signature untuk tugas penandatanganan di aplikasi Java Anda. Mari kita mulai menyiapkan alat-alat yang diperlukan sebelum mulai mengimplementasikan fitur-fitur ini!

## Prasyarat

Sebelum melanjutkan dengan panduan ini, pastikan Anda memiliki hal berikut:
- **Kit Pengembangan Java (JDK)** terinstal di komputer Anda.
- Pengetahuan dasar tentang pemrograman Java dan keakraban dengan sistem pembangunan Maven atau Gradle.
- IDE seperti IntelliJ IDEA, Eclipse, atau NetBeans.

Selain itu, Anda perlu menyiapkan GroupDocs.Signature untuk Java di proyek Anda. Proses penyiapannya mudah dan dapat dilakukan menggunakan dependensi Maven atau Gradle seperti yang ditunjukkan di bawah ini:

## Menyiapkan GroupDocs.Signature untuk Java

Untuk memulainya, tambahkan dependensi GroupDocs.Signature ke berkas build proyek Anda.

### Pakar
```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

### Gradle
```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

Atau, Anda dapat mengunduh perpustakaan langsung dari [GroupDocs.Signature untuk rilis Java](https://releases.groupdocs.com/signature/java/).

#### Akuisisi Lisensi
Untuk memanfaatkan sepenuhnya fitur GroupDocs.Signature:
- **Uji Coba Gratis**: Mulailah dengan uji coba gratis untuk menjelajahi fungsionalitas dasar.
- **Lisensi Sementara**: Dapatkan lisensi sementara untuk akses penuh selama evaluasi.
- **Pembelian**:Untuk penggunaan jangka panjang, pertimbangkan untuk membeli lisensi komersial.

### Inisialisasi dan Pengaturan Dasar
Inisialisasi `Signature` kelas dengan meneruskan jalur berkas dokumen Anda seperti yang ditunjukkan di bawah ini:
```java
import com.groupdocs.signature.Signature;

// Inisialisasi dengan jalur dokumen Anda
Signature signature = new Signature("YOUR_DOCUMENT_DIRECTORY/SampleSpreadsheet.xlsx");
```

## Panduan Implementasi
Di bagian ini, kita akan membahas langkah-langkah untuk menandatangani spreadsheet dan menyimpannya menggunakan GroupDocs.Signature.

### Menandatangani Spreadsheet dengan Kode QR
#### Ringkasan
Fitur ini memungkinkan Anda menambahkan tanda tangan kode QR ke lembar kerja Excel Anda. Fitur ini sangat berguna untuk menambahkan pengenal elektronik aman yang dapat dipindai dengan mudah.
##### Langkah 1: Tentukan Jalur File
Mulailah dengan menentukan jalur untuk file input dan output:
```java
String filePath = "YOUR_DOCUMENT_DIRECTORY/SampleSpreadsheet.xlsx";
String outputFilePath = "YOUR_OUTPUT_DIRECTORY/signedDocument.pdf";
```
##### Langkah 2: Inisialisasi Objek Tanda Tangan
Membuat sebuah `Signature` objek dengan jalur berkas dokumen Anda.
```java
Signature signature = new Signature(filePath);
```
##### Langkah 3: Buat Opsi Tanda Tangan Kode QR
Konfigurasikan opsi penandatanganan kode QR. Tentukan properti seperti teks, jenis, dan posisi kode QR:
```java
import com.groupdocs.signature.options.sign.QrCodeSignOptions;
import com.groupdocs.signature.domain.qrcodes.QrCodeTypes;

QrCodeSignOptions signOptions = new QrCodeSignOptions("JohnSmith");
signOptions.setEncodeType(QrCodeTypes.QR);
signOptions.setLeft(100); // Koordinat X
signOptions.setTop(100);  // Koordinat Y
```
##### Langkah 4: Konfigurasikan Opsi Penyimpanan
Tentukan bagaimana Anda ingin dokumen yang ditandatangani disimpan, termasuk formatnya:
```java
import com.groupdocs.signature.options.saveoptions.SpreadsheetSaveOptions;
import com.groupdocs.signature.domain.enums.SpreadsheetSaveFileFormat;

SpreadsheetSaveOptions saveOptions = new SpreadsheetSaveOptions();
saveOptions.setFileFormat(SpreadsheetSaveFileFormat.Pdf);
saveOptions.setOverwriteExistingFiles(true);
```
##### Langkah 5: Tandatangani dan Simpan Dokumen
Terakhir, gunakan `sign` metode untuk menerapkan tanda tangan kode QR Anda dan menyimpan dokumen:
```java
try {
    signature.sign(outputFilePath, signOptions, saveOptions);
} catch (Exception e) {
    e.printStackTrace();
}
```
### Menyimpan Dokumen dalam Format File Output yang Berbeda
#### Ringkasan
GroupDocs.Signature memungkinkan Anda menyimpan dokumen yang ditandatangani ke dalam berbagai format seperti PDF, XLSX, dan DOCX.
##### Langkah 1: Tentukan Jalur Output
Tentukan jalur dan format file keluaran yang Anda inginkan:
```java
String outputPath = "YOUR_OUTPUT_DIRECTORY/signedDocument.pdf"; // Ubah format sesuai kebutuhan
```
##### Langkah 2: Siapkan Opsi Penyimpanan
Konfigurasi `SpreadsheetSaveOptions` untuk menentukan bagaimana Anda ingin dokumen disimpan:
```java
SpreadsheetSaveOptions saveOptions = new SpreadsheetSaveOptions();
saveOptions.setFileFormat(SpreadsheetSaveFileFormat.Pdf); // Dapat diubah untuk format yang berbeda
saveOptions.setOverwriteExistingFiles(true);
```
##### Langkah 3: Terapkan Operasi Penandatanganan
Gunakan opsi ini dalam operasi penandatanganan. Pastikan `signature` objek diinisialisasi dengan benar:
```java
// Contoh penggunaan (dengan asumsi objek tanda tangan ada)
signature.sign(outputPath, signOptions, saveOptions);
```
## Aplikasi Praktis
Berikut adalah beberapa skenario dunia nyata di mana fungsi ini dapat bermanfaat:
- **Dokumen Hukum**:Tanda tangani kontrak secara aman dengan kode QR untuk verifikasi yang mudah.
- **Laporan Keuangan**:Tambahkan tanda tangan ke lembar kerja yang berisi data keuangan sensitif.
- **Manajemen Inventaris**:Gunakan kode QR pada lembar inventaris untuk pelacakan dan autentikasi yang efisien.

## Pertimbangan Kinerja
Saat bekerja dengan penandatanganan dokumen, pertimbangkan kiat berikut:
- Optimalkan manajemen memori Java Anda dengan membuat profil penggunaan sumber daya selama operasi tanda tangan.
- GroupDocs.Signature dioptimalkan untuk kinerja, tetapi pastikan Anda menjalankannya di lingkungan yang sesuai untuk menangani dokumen besar secara efisien.

## Kesimpulan
Sekarang, Anda seharusnya sudah terbiasa menggunakan GroupDocs.Signature untuk menandatangani dan menyimpan lembar kerja Excel dengan kode QR. Alat canggih ini dapat meningkatkan keamanan dan keaslian dokumen digital Anda secara signifikan. Sebagai langkah selanjutnya, jelajahi fitur tambahan seperti tanda tangan teks atau tanda tangan stempel untuk lebih mengamankan dokumen Anda.

**Ajakan Bertindak**:Coba terapkan solusi ini dalam proyek Anda hari ini!

## Bagian FAQ
1. **Format apa yang didukung GroupDocs.Signature?**
   - Mendukung PDF, XLSX, DOCX, dan banyak lagi.
2. **Bagaimana saya dapat memecahkan masalah tanda tangan?**
   - Periksa pesan pengecualian untuk mencari petunjuk; pastikan semua jalur berkas benar.
3. **Apakah mungkin untuk menandatangani beberapa halaman dalam satu dokumen?**
   - Ya, tentukan nomor halaman dalam opsi penandatanganan Anda.
4. **Bisakah GroupDocs.Signature digunakan dalam aplikasi web?**
   - Tentu saja, sangat cocok untuk aplikasi Java sisi server.
5. **Bagaimana cara mendapatkan dukungan jika diperlukan?**
   - Gunakan [Forum Dukungan GroupDocs](https://forum.groupdocs.com/c/signature) untuk bantuan.

## Sumber daya
- **Dokumentasi**:Panduan lengkap dan referensi API dapat ditemukan di [Dokumentasi GroupDocs](https://docs.groupdocs.com/signature/java/).
- **Referensi API**:Informasi lebih lengkap tersedia di [Halaman Referensi API](https://reference.groupdocs.com/signature/java/).
- **Unduh**: Akses versi terbaru di [Rilis GroupDocs](https://releases.groupdocs.com/signature/java/).
- **Pembelian dan Lisensi**:Pelajari lebih lanjut tentang opsi lisensi di [Pembelian GroupDocs](https://purchase.groupdocs.com/buy) dan dapatkan uji coba gratis melalui [Uji Coba Gratis GroupDocs](http://www.groupdocs.com/pricing)