---
"date": "2025-05-08"
"description": "Pelajari cara meningkatkan keamanan dokumen dengan menerapkan dan memverifikasi tanda tangan kode QR di Java menggunakan GroupDocs.Signature. Ikuti panduan langkah demi langkah ini untuk proses penandatanganan yang aman."
"title": "Amankan Dokumen Anda&#58; Terapkan Tanda Tangan Kode QR di Java Menggunakan GroupDocs.Signature"
"url": "/id/java/qr-code-signatures/qr-code-signatures-java-groupdocs/"
"weight": 1
type: docs
---
# Amankan Dokumen Anda: Terapkan Tanda Tangan Kode QR di Java Menggunakan GroupDocs.Signature

Di era digital saat ini, memastikan keamanan dokumen seperti kontrak, faktur, atau informasi pribadi yang sensitif sangatlah penting. Salah satu pendekatan inovatif untuk meningkatkan keamanan dokumen dan menyederhanakan proses verifikasi adalah dengan menggunakan tanda tangan kode QR. Tutorial ini akan memandu Anda dalam mengimplementasikan dan memverifikasi tanda tangan kode QR untuk dokumen Anda di Java menggunakan GroupDocs.Signature.

## Apa yang Akan Anda Pelajari
- Cara menandatangani dokumen menggunakan Kode QR
- Memverifikasi dokumen yang ditandatangani dengan Kode QR
- Mencari tanda tangan Kode QR yang ada dalam dokumen
- Memperbarui dan menghapus tanda tangan Kode QR dari dokumen Anda

Mari atur lingkungan Anda dan mulai!

### Prasyarat
Sebelum memulai, pastikan Anda memiliki prasyarat berikut:

#### Pustaka dan Ketergantungan yang Diperlukan
Anda memerlukan GroupDocs.Signature untuk Java. Anda dapat menyertakannya melalui Maven atau Gradle, atau mengunduhnya langsung.

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

**Unduh Langsung**
Unduh versi terbaru dari [GroupDocs.Signature untuk rilis Java](https://releases.groupdocs.com/signature/java/).

#### Persyaratan Pengaturan Lingkungan
- Pastikan Anda telah menginstal Java Development Kit (JDK) 8 atau yang lebih tinggi.
- Gunakan IDE seperti IntelliJ IDEA, Eclipse, atau NetBeans.

#### Prasyarat Pengetahuan
Pemahaman dasar tentang pemrograman Java dan pemrosesan dokumen akan bermanfaat.

## Menyiapkan GroupDocs.Signature untuk Java
Untuk menggunakan GroupDocs.Signature di proyek Anda, ikuti langkah-langkah berikut:
1. **Instalasi**: Pilih antara Maven, Gradle, atau unduhan langsung berdasarkan pengaturan Anda.
2. **Akuisisi Lisensi**:
   - Mulailah dengan uji coba gratis yang tersedia di [Situs web GroupDocs](https://releases.groupdocs.com/signature/java/).
   - Pertimbangkan untuk mendapatkan lisensi sementara untuk pengujian dan pengembangan yang diperpanjang dari [Di Sini](https://purchase.groupdocs.com/temporary-license/).
3. **Inisialisasi Dasar**: 
    Berikut cara menginisialisasi GroupDocs.Signature:

    ```java
    Signature signature = new Signature("YOUR_DOCUMENT_PATH");
    ```

Ini mempersiapkan Anda untuk menerapkan tanda tangan Kode QR.

## Panduan Implementasi

### Tanda Tangani Dokumen dengan Tanda Tangan Kode QR
#### Ringkasan
Menandatangani dokumen menggunakan Kode QR melibatkan penyematan kode unik yang mewakili tanda tangan digital Anda. Proses ini mengamankan dokumen dan memudahkan verifikasi keasliannya nanti.

##### Langkah 1: Siapkan Opsi Penandatanganan Anda
```java
import com.groupdocs.signature.Signature;
import com.groupdocs.signature.domain.enums.HorizontalAlignment;
import com.groupdocs.signature.domain.enums.VerticalAlignment;
import com.groupdocs.signature.options.sign.QrCodeSignOptions;

Signature signature = new Signature("YOUR_DOCUMENT_PATH");
QrCodeSignOptions signOptions = new QrCodeSignOptions("John Smith", com.groupdocs.signature.domain.qrcodes.QrCodeTypes.QR);

signOptions.setVerticalAlignment(VerticalAlignment.Top);
signOptions.setHorizontalAlignment(HorizontalAlignment.Center);
signOptions.setWidth(100);
signOptions.setHeight(40);
```
**Penjelasan**: `QrCodeSignOptions` dikonfigurasi untuk membuat Kode QR dengan teks dan perataan tertentu. Sesuaikan lebar dan tinggi sesuai kebutuhan.

##### Langkah 2: Sesuaikan Tampilan Tanda Tangan
```java
import java.awt.Color;

signOptions.setForeColor(Color.RED); // Tetapkan warna kode QR
com.groupdocs.signature.domain.SignatureFont signatureFont = new com.groupdocs.signature.domain.SignatureFont();
signatureFont.setSize(12);
signatureFont.setFamilyName("Comic Sans MS");
signOptions.setFont(signatureFont);
```
**Penjelasan**: Menyesuaikan font dan warna meningkatkan identifikasi visual.

##### Langkah 3: Tandatangani Dokumen
```java
import java.util.ArrayList;
import java.util.List;

List<String> signatureIds = new ArrayList<>();
List<com.groupdocs.signature.domain.BaseSignature> signedSignatures = signature.sign("YOUR_OUTPUT_PATH", signOptions).getSucceeded();

for (com.groupdocs.signature.domain.BaseSignature temp : signedSignatures) {
    signatureIds.add(temp.getSignatureId());
}
```
**Penjelasan**: Langkah ini menandatangani dokumen dan menyimpan ID tanda tangan untuk referensi di masa mendatang.

### Verifikasi Dokumen dengan Tanda Tangan Kode QR
#### Ringkasan
Verifikasi memastikan bahwa dokumen telah ditandatangani secara sah. Berikut cara memverifikasi tanda tangan Kode QR dalam dokumen.

##### Langkah 1: Siapkan Opsi Verifikasi
```java
import com.groupdocs.signature.Signature;
import com.groupdocs.signature.options.verify.QrCodeVerifyOptions;

Signature signature2 = new Signature("YOUR_OUTPUT_PATH");
QrCodeVerifyOptions verifyOptions = new QrCodeVerifyOptions();

verifyOptions.setEncodeType(QrCodeTypes.QR);
verifyOptions.setText("John Smith"); // Teks untuk verifikasi
verifyOptions.setAllPages(false); 
verifyOptions.setPageNumber(1);
```
**Penjelasan**Pilihan verifikasi menentukan jenis dan teks Kode QR yang dicari, memastikan tanda tangan sesuai dengan harapan Anda.

##### Langkah 2: Lakukan Verifikasi
```java
boolean isValid = signature2.verify(verifyOptions).isValid();
System.out.println("Is Signature Valid? " + isValid);
```
**Penjelasan**: Ini memeriksa apakah dokumen berisi Kode QR valid yang sesuai dengan kriteria Anda.

### Cari Dokumen untuk Tanda Tangan Kode QR
#### Ringkasan
Menemukan tanda tangan yang ada dalam dokumen terkadang diperlukan. Berikut cara mencarinya menggunakan GroupDocs.Signature.

##### Langkah 1: Konfigurasikan Opsi Pencarian
```java
import com.groupdocs.signature.domain.signatures.QrCodeSignature;
import com.groupdocs.signature.options.search.QrCodeSearchOptions;

Signature signature2 = new Signature("YOUR_OUTPUT_PATH");
QrCodeSearchOptions searchOptions = new QrCodeSearchOptions();
searchOptions.setAllPages(true);
```
**Penjelasan**: Ini menyiapkan alat untuk memindai semua halaman untuk tanda tangan Kode QR.

##### Langkah 2: Jalankan Pencarian
```java
List<QrCodeSignature> signatures = signature2.search(QrCodeSignature.class, searchOptions);

for (QrCodeSignature qrSignature : signatures) {
    System.out.println("Found Signature ID: " + qrSignature.getSignatureId());
}
```
**Penjelasan**: Ini mengambil semua tanda tangan Kode QR yang ditemukan dalam dokumen.

### Perbarui Tanda Tangan Kode QR Dokumen
#### Ringkasan
Memperbarui tanda tangan melibatkan perubahan propertinya, seperti posisi atau ukuran. Berikut cara melakukannya:

##### Langkah 1: Siapkan Tanda Tangan untuk Pembaruan
```java
import com.groupdocs.signature.domain.signatures.QrCodeSignature;
import java.io.ByteArrayOutputStream;

Signature signature2 = new Signature("YOUR_OUTPUT_PATH");
List<QrCodeSignature> signaturesToUpdate = new ArrayList<>();

// Dengan asumsi 'tanda tangan' adalah daftar objek QrCodeSignature yang diperoleh dari pencarian
for (QrCodeSignature qrSignature : signatures) {
    qrSignature.setLeft(qrSignature.getLeft() + 100);
    qrSignature.setTop(qrSignature.getTop() + 100);
    qrSignature.setWidth(200);
    qrSignature.setHeight(50);
    signaturesToUpdate.add(qrSignature);
}
```
**Penjelasan**: Ini menyesuaikan posisi dan ukuran setiap tanda tangan.

##### Langkah 2: Perbarui Dokumen
```java
ByteArrayOutputStream outputStream = new ByteArrayOutputStream();
signature2.update(outputStream, signaturesToUpdate);
```
**Penjelasan**:Dokumen diperbarui dengan tanda tangan Kode QR yang dimodifikasi.

### Hapus Tanda Tangan Kode QR Dokumen berdasarkan ID
#### Ringkasan
Menghapus tanda tangan mungkin diperlukan jika tidak lagi diperlukan atau ditambahkan karena kesalahan. Berikut cara menghapusnya menggunakan ID uniknya.

##### Langkah 1: Identifikasi Tanda Tangan yang Akan Dihapus
```java
import com.groupdocs.signature.domain.SignatureCollection;
import java.util.Arrays;

SignatureCollection signaturesToDelete = signature2.search(QrCodeSignature.class);
Arrays.stream(signaturesToDelete).forEach(signature -> {
    if (signature.getSignatureId().equals("YOUR_SIGNATURE_ID")) {
        signature.delete();
    }
});
```
**Penjelasan**: Ini menemukan dan menghapus tanda tangan Kode QR berdasarkan ID uniknya.

## Kesimpulan
Panduan ini memandu Anda mengamankan dokumen menggunakan tanda tangan kode QR di Java dengan GroupDocs.Signature. Dengan mengikuti langkah-langkah ini, Anda dapat memastikan dokumen Anda ditandatangani dengan aman dan memverifikasi keasliannya dengan mudah.