---
"date": "2025-05-08"
"description": "Pelajari cara menandatangani citra DICOM dengan aman menggunakan GroupDocs.Signature untuk Java. Tingkatkan keamanan dokumen dengan menyematkan kode QR dan metadata."
"title": "Menandatangani Gambar DICOM dengan Kode QR dan Metadata Menggunakan GroupDocs.Signature untuk Java"
"url": "/id/java/image-signatures/sign-dicom-images-groupdocs-signature-java/"
"weight": 1
type: docs
---
# Cara Menandatangani Gambar DICOM dengan Kode QR dan Metadata Menggunakan GroupDocs.Signature untuk Java

## Perkenalan

Dalam lanskap layanan kesehatan digital yang berkembang pesat, pengelolaan data pasien yang aman sangatlah penting. Tutorial ini memandu Anda dalam menerapkan solusi yang andal menggunakan GroupDocs.Signature untuk Java untuk menandatangani citra Digital Imaging and Communications in Medicine (DICOM) dengan kode QR dan metadata. Fitur-fitur ini memastikan keaslian, meningkatkan ketertelusuran, dan menjaga kepatuhan dengan menyematkan informasi penting langsung ke dalam citra medis.

### Apa yang Akan Anda Pelajari:
- Cara mengintegrasikan GroupDocs.Signature untuk Java ke dalam proyek Anda.
- Proses penandatanganan gambar DICOM dengan kode QR.
- Menambahkan metadata XMP untuk meningkatkan keamanan dokumen.
- Mengambil, memverifikasi, dan mencari tanda tangan dalam file DICOM.
- Membuat pratinjau gambar DICOM yang ditandatangani.

Mari kita mulai! Sebelum kita mulai, pastikan Anda memiliki semua yang dibutuhkan untuk mengikuti dengan lancar.

## Prasyarat

Untuk menerapkan fitur GroupDocs.Signature secara efektif, pastikan Anda memenuhi prasyarat berikut:

### Pustaka dan Ketergantungan yang Diperlukan
- **GroupDocs.Signature untuk Java**Anda memerlukan versi 23.12 atau yang lebih baru dari pustaka ini.

### Persyaratan Pengaturan Lingkungan
- **Kit Pengembangan Java (JDK)**: Pastikan JDK terinstal pada sistem Anda.
- **IDE**: Gunakan Lingkungan Pengembangan Terpadu seperti IntelliJ IDEA atau Eclipse.

### Prasyarat Pengetahuan
Pemahaman dasar tentang:
- Pemrograman Java dan prinsip berorientasi objek.
- Alat pembangun Maven atau Gradle untuk manajemen ketergantungan.

## Menyiapkan GroupDocs.Signature untuk Java

Untuk memulai GroupDocs.Signature, Anda perlu menambahkannya sebagai dependensi dalam proyek Anda. Berikut cara melakukannya menggunakan berbagai alat build:

### Pakar
Tambahkan cuplikan berikut ke `pom.xml` mengajukan:
```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

### Gradle
Sertakan ini di dalam `build.gradle` mengajukan:
```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

### Unduh Langsung
Atau, Anda dapat mengunduh versi terbaru dari [GroupDocs.Signature untuk rilis Java](https://releases.groupdocs.com/signature/java/).

#### Langkah-Langkah Perolehan Lisensi
1. **Uji Coba Gratis**: Uji coba fitur-fiturnya dengan uji coba gratis waktu terbatas.
2. **Lisensi Sementara**Dapatkan lisensi sementara untuk mengeksplorasi kemampuan penuh.
3. **Pembelian**:Beli langganan jika Anda memerlukan akses jangka panjang.

#### Inisialisasi dan Pengaturan Dasar

Untuk menginisialisasi GroupDocs.Signature, buatlah sebuah instance dari `Signature` kelas:
```java
import com.groupdocs.signature.Signature;

// Inisialisasi objek tanda tangan dengan jalur ke file DICOM Anda
Signature signature = new Signature(filePath);
```

## Panduan Implementasi

### Menandatangani Gambar DICOM dengan Kode QR dan Metadata

#### Ringkasan
Fitur ini memungkinkan Anda menandatangani gambar DICOM dengan kode QR dan menambahkan metadata XMP, sehingga meningkatkan keamanan dokumen.

#### Langkah 1: Siapkan Opsi Tanda Tangan Kode QR
```java
import com.groupdocs.signature.domain.Padding;
import com.groupdocs.signature.domain.enums.HorizontalAlignment;
import com.groupdocs.signature.domain.enums.VerticalAlignment;
import com.groupdocs.signature.domain.signatures.QrCodeSignOptions;

Padding padding = new Padding();
padding.setRight(5);
padding.setLeft(5);

QrCodeSignOptions options = new QrCodeSignOptions("Patient #36363393. R: No-Issues");
options.setAllPages(true);
options.setWidth(100);
options.setHeight(100);
options.setVerticalAlignment(VerticalAlignment.Bottom);
options.setHorizontalAlignment(HorizontalAlignment.Right);
options.setMargin(padding);
```
Di sini, kami mengonfigurasikan tampilan dan posisi kode QR pada gambar DICOM.

#### Langkah 2: Tambahkan Metadata XMP
```java
import com.groupdocs.signature.options.saveoptions.imagessaveoptions.DicomSaveOptions;
import com.groupdocs.signature.options.saveoptions.imagessaveoptions.DicomXmpEntry;
import com.groupdocs.signature.options.saveoptions.imagessaveoptions.DicomXmpType;

DicomSaveOptions dicomSaveOptions = new DicomSaveOptions();
List<DicomXmpEntry> xmpEntries = new ArrayList<>();
xmpEntries.add(new DicomXmpEntry(DicomXmpType.PatientName, "Patient #4"));
dicomSaveOptions.setXmpEntries(xmpEntries);
```
Cuplikan ini menambahkan metadata ke berkas DICOM, yang menyematkan informasi pasien tambahan.

#### Langkah 3: Tandatangani Dokumen
```java
String outputFilePath = YOUR_OUTPUT_DIRECTORY + "/SignDicomImageAdvanced/" + fileName;
signature.sign(outputFilePath, options, dicomSaveOptions);
```
Itu `sign` metode menulis kode QR dan metadata ke dalam file DICOM Anda, menyimpannya ke lokasi yang ditentukan.

### Mengambil Info Gambar DICOM yang Ditandatangani

#### Ringkasan
Ekstrak metadata XMP dari citra DICOM yang ditandatangani untuk tujuan verifikasi atau audit.
```java
import com.groupdocs.signature.domain.IDocumentInfo;
import com.groupdocs.signature.domain.signatures.MetadataSignature;

IDocumentInfo documentInfo = signature.getDocumentInfo();
for (MetadataSignature item : documentInfo.getMetadataSignatures()) {
    System.out.println(item.toString());
}
```
Kode ini mengambil dan mencetak semua tanda tangan metadata yang terkait dengan berkas DICOM.

### Memverifikasi DICOM yang Ditandatangani

#### Ringkasan
Verifikasi bahwa tanda tangan kode QR ada dalam gambar DICOM yang ditandatangani untuk mengonfirmasi keasliannya.
```java
import com.groupdocs.signature.domain.VerificationResult;
import com.groupdocs.signature.options.verify.QrCodeVerifyOptions;
import com.groupdocs.signature.domain.enums.TextMatchType;

QrCodeVerifyOptions verifyOptions = new QrCodeVerifyOptions();
verifyOptions.setAllPages(true);
verifyOptions.setText("Patient #36363393");
verifyOptions.setMatchType(TextMatchType.Contains);

VerificationResult result = signature.verify(verifyOptions);
if (result.isValid()) {
    System.out.println(filePath + " has successfully verified signatures!");
} else {
    System.out.println(filePath + " failed verification process.");
}
```
Langkah verifikasi ini memastikan bahwa kode QR sesuai dengan kriteria yang diharapkan, mengonfirmasi integritas dokumen.

### Mencari Tanda Tangan di DICOM yang Ditandatangani

#### Ringkasan
Temukan semua tanda tangan kode QR dalam gambar DICOM yang ditandatangani untuk meninjau atau mengauditnya.
```java
import com.groupdocs.signature.domain.signatures.QrCodeSignature;
import java.util.List;

List<QrCodeSignature> signatures = signature.search(QrCodeSignature.class);
for (QrCodeSignature qrCodeSignature : signatures) {
    System.out.println("QRCode signature found at page " +
        qrCodeSignature.getPageNumber() + ": " +
        qrCodeSignature.getEncodeType().getTypeName() + ": " +
        qrCodeSignature.getText());
}
```
Fitur ini berguna untuk memindai semua tanda tangan kode QR dalam dokumen, memberikan visibilitas yang komprehensif.

### Membuat Pratinjau DICOM yang Ditandatangani

#### Ringkasan
Buat pratinjau untuk setiap halaman gambar DICOM yang ditandatangani, memungkinkan pemeriksaan visual cepat tanpa membuka seluruh berkas.
```java
import com.groupdocs.signature.options.PreviewOptions;
import java.io.File;
import java.io.FileOutputStream;
import java.nio.file.Paths;

PreviewOptions previewOption = new PreviewOptions(pageNumber -> {
    try {
        String pageFilePath = YOUR_OUTPUT_DIRECTORY + "/SignDicomImageAdvanced/image-" + pageNumber + ".jpg";
        return new FileOutputStream(Paths.get(pageFilePath).toFile());
    } catch (Exception e) {
        throw new RuntimeException(e.getMessage());
    }
});

signature.generatePreview(previewOption);
```
Cuplikan ini menghasilkan pratinjau gambar untuk setiap halaman, yang dapat berguna untuk verifikasi atau berbagi cepat.

## Aplikasi Praktis

GroupDocs.Signature untuk Java menawarkan beberapa aplikasi dunia nyata:
- **Pencitraan Medis**:Tanda tangani dan kelola gambar DICOM pasien secara aman dengan kode QR dan metadata.
- **Manajemen Dokumen Hukum**: Meningkatkan keaslian dan kepatuhan dokumen dalam proses hukum.
- **Layanan Keuangan**:Terapkan tanda tangan elektronik yang aman pada dokumen keuangan yang sensitif.