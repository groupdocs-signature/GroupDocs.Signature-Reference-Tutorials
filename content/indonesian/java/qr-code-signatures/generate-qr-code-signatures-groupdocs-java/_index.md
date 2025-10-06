---
"date": "2025-05-08"
"description": "Pelajari cara membuat tanda tangan kode QR yang aman dan dinamis di Java menggunakan GroupDocs.Signature. Sederhanakan penandatanganan dokumen dengan mudah."
"title": "Hasilkan Tanda Tangan Kode QR dengan GroupDocs.Signature untuk Java&#58; Panduan Lengkap"
"url": "/id/java/qr-code-signatures/generate-qr-code-signatures-groupdocs-java/"
"weight": 1
type: docs
---
# Hasilkan Tanda Tangan Kode QR dengan GroupDocs.Signature untuk Java

## Perkenalan

Di era digital saat ini, pengamanan dokumen sangatlah penting. Baik Anda menangani kontrak, faktur, atau perjanjian, memastikan tanda tangan yang akurat dan aman bisa menjadi tantangan tersendiri. **GroupDocs.Signature untuk Java** menawarkan solusi tangguh untuk menyederhanakan penambahan tanda tangan digital ke dokumen Anda.

Tutorial ini akan memandu Anda membuat tanda tangan Kode QR menggunakan GroupDocs.Signature untuk Java, yang akan meningkatkan keamanan dan fleksibilitas dalam menyematkan data tambahan ke dalam dokumen Anda. Dengan mengikuti tutorial ini, Anda akan mempelajari:

- Menyiapkan dan mengonfigurasi GroupDocs.Signature untuk Java.
- Teknik untuk menghasilkan tanda tangan kode QR dengan pengaturan penyelarasan yang tepat.
- Mengonfigurasi opsi pratinjau tanda tangan untuk tampilan komprehensif dokumen yang ditandatangani.
- Menghasilkan aliran tanda tangan untuk memastikan penanganan berkas yang lancar.

Mari kita bahas lebih lanjut tentang penerapan fungsi-fungsi ini di aplikasi Java Anda. Pertama, mari kita bahas beberapa prasyarat agar Anda dapat memulai dengan lancar.

## Prasyarat

Sebelum menggunakan GroupDocs.Signature untuk Java, pastikan Anda memenuhi persyaratan berikut:

- **Perpustakaan & Ketergantungan**Instal pustaka yang diperlukan. Gunakan Maven atau Gradle untuk mengelola dependensi.
  
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

- **Pengaturan Lingkungan**Pastikan Anda memiliki lingkungan pengembangan Java dengan JDK dan IDE seperti IntelliJ IDEA atau Eclipse.

- **Prasyarat Pengetahuan**:Keakraban dengan konsep pemrograman Java sangat penting, begitu pula pemahaman tentang tanda tangan digital.

Selanjutnya, kami akan memandu Anda dalam menyiapkan GroupDocs.Signature untuk Java di lingkungan proyek Anda.

## Menyiapkan GroupDocs.Signature untuk Java

Untuk mulai menggunakan GroupDocs.Signature untuk Java, ikuti langkah-langkah berikut:

1. **Tambahkan Ketergantungan**: Gunakan Maven atau Gradle untuk menyertakan dependensi seperti yang ditunjukkan di atas.
2. **Akuisisi Lisensi**:
   - Mulailah dengan versi uji coba gratis dengan mengunduhnya dari [Rilis GroupDocs](https://releases.groupdocs.com/signature/java/).
   - Untuk penggunaan jangka panjang, pertimbangkan untuk membeli lisensi atau mengajukan lisensi sementara melalui [halaman pembelian](https://purchase.groupdocs.com/buy).
3. **Inisialisasi Dasar**:
   Inisialisasi pustaka di aplikasi Java Anda untuk mulai menggunakan fitur-fiturnya.

   ```java
   import com.groupdocs.signature.Signature;
   
   // Inisialisasi objek Tanda Tangan
   Signature signature = new Signature("sample.pdf");
   ```

Setelah GroupDocs.Signature untuk Java dikonfigurasi, Anda siap membuat tanda tangan Kode QR. Mari kita bahas detailnya.

## Panduan Implementasi

### Membuat Tanda Tangan Kode QR

Pembuatan tanda tangan kode QR melibatkan beberapa langkah penting. Setiap langkah membantu menyesuaikan cara data disematkan dan ditampilkan dalam dokumen Anda.

#### Ringkasan
Tanda tangan Kode QR bersifat serbaguna; memungkinkan Anda untuk menyematkan informasi kompleks seperti alamat, URL, atau data biner langsung ke dalam dokumen Anda. Mari kita lihat cara membuat tanda tangan ini dengan pengaturan penyelarasan khusus menggunakan GroupDocs.Signature untuk Java.

#### Implementasi Langkah demi Langkah

##### 1. Konfigurasikan Opsi Kode QR
Mulailah dengan menyiapkan `QrCodeSignOptions` Objek. Di sinilah Anda menentukan jenis kode QR dan data yang harus dikandungnya.

```java
import com.groupdocs.signature.domain.enums.HorizontalAlignment;
import com.groupdocs.signature.domain.enums.VerticalAlignment;
import com.groupdocs.signature.domain.extensions.serialization.Address;
import com.groupdocs.signature.domain.qrcodes.QrCodeTypes;
import com.groupdocs.signature.options.sign.QrCodeSignOptions;

QrCodeSignOptions signOptions = new QrCodeSignOptions();
signOptions.setEncodeType(QrCodeTypes.QR);

// Menyiapkan data dengan objek Alamat
Address address = new Address();
address.setStreet("221B Baker Street");
address.setCity("London");
address.setState("NW");
address.setZIP("NW16XE");
address.setCountry("England");

signOptions.setData(address);
```
**Penjelasan**:Di sini, kami mengatur jenis kode QR ke standar `QR` dan isi dengan informasi alamat. Enkapsulasi data ini memastikan detail penting mudah diakses dalam dokumen Anda.

##### 2. Sejajarkan Kode QR
Sesuaikan pengaturan perataan untuk mengontrol tempat kode QR muncul di halaman dokumen.

```java
signOptions.setHorizontalAlignment(HorizontalAlignment.Left);
signOptions.setVerticalAlignment(VerticalAlignment.Center);
signOptions.setWidth(100);
signOptions.setHeight(100);
```
**Penjelasan**: Opsi penyelarasan (`HorizontalAlignment` Dan `VerticalAlignment`) memungkinkan Anda memposisikan kode QR secara tepat. Langkah ini memastikan kode QR terlihat menarik secara estetika sekaligus ditempatkan secara strategis untuk pemindaian optimal.

##### 3. Atur Margin
Tentukan margin di sekitar kode QR untuk memastikan kode tidak menyentuh tepian dokumen, yang penting untuk keandalan pemindaian.

```java
signOptions.setMargin(new Padding(10));
```
**Penjelasan**:Margin diatur di sini menggunakan `Padding`, memastikan adanya ruang antara kode QR dan tepi dokumen, meningkatkan kemampuan pemindaian.

### Mengonfigurasi Opsi Pratinjau Tanda Tangan

Dengan mengatur opsi pratinjau, Anda dapat memvisualisasikan tampilan tanda tangan sebelum menyelesaikannya. Berikut caranya:

#### Ringkasan
Pengaturan pratinjau sangat penting untuk memverifikasi tampilan tanda tangan Anda dalam dokumen.

#### Implementasi Langkah demi Langkah

##### 1. Buat dan Konfigurasikan PreviewOptions
Memanfaatkan `PreviewSignatureOptions` untuk menentukan bagaimana tanda tangan akan dipratinjau.

```java
import com.groupdocs.signature.options.PreviewSignatureOptions;
import com.groupdocs.signature.options.preview.PreviewFormats;
import java.util.UUID;

PreviewSignatureOptions previewOption = new PreviewSignatureOptions(signOptions);
previewOption.setSignatureId(UUID.randomUUID().toString());
previewOption.setPreviewFormat(PreviewFormats.JPEG);
```
**Penjelasan**: Itu `PreviewSignatureOptions` Objek dikonfigurasi untuk menghasilkan pratinjau JPEG dari kode QR. Pengidentifikasi unik untuk setiap tanda tangan (`UUID`) memastikan bahwa Anda dapat melacak dan mengelola beberapa tanda tangan secara efisien.

### Menghasilkan Aliran Tanda Tangan

Membuat aliran memastikan dokumen Anda yang telah ditandatangani disimpan atau dikirimkan dengan benar.

#### Ringkasan
Pembuatan aliran berkas memungkinkan penanganan dokumen yang ditandatangani secara lancar, memastikan dokumen disimpan dengan benar di direktori yang ditentukan.

#### Implementasi Langkah demi Langkah

##### 1. Tentukan Direktori Output dan Hasilkan Stream
Pastikan direktori keluaran ada sebelum membuat aliran untuk menghindari kesalahan selama penulisan berkas.

```java
import java.io.FileOutputStream;
import java.io.OutputStream;
import java.nio.file.Files;
import java.nio.file.Path;
import java.nio.file.Paths;

public OutputStream generateSignatureStream(PreviewSignatureOptions previewOptions) {
    try {
        Path path = Paths.get("YOUR_OUTPUT_DIRECTORY");
        if (!Files.exists(path)) {
            Files.createDirectories(path);
        }
        
        // Buat aliran keluaran untuk menyimpan dokumen yang ditandatangani
        return new FileOutputStream(path.resolve("signedDocument.pdf"));
    } catch (Exception e) {
        e.printStackTrace();
        return null;
    }
}
```
**Penjelasan**Metode ini memeriksa keberadaan direktori yang ditentukan dan membuatnya jika perlu, lalu mengembalikan aliran keluaran berkas untuk menyimpan dokumen Anda. Penanganan direktori memastikan bahwa dokumen yang ditandatangani disimpan secara terorganisir.

## Kesimpulan

Dengan mengikuti panduan ini, Anda telah mempelajari cara membuat tanda tangan kode QR menggunakan GroupDocs.Signature untuk Java, yang meningkatkan keamanan dan fleksibilitas dalam menyematkan data tambahan di dalam dokumen Anda. Dengan langkah-langkah ini, Anda dapat dengan yakin mengimplementasikan fungsionalitas tanda tangan digital di aplikasi Java Anda.

Untuk eksplorasi lebih lanjut, pertimbangkan untuk bereksperimen dengan berbagai jenis tanda tangan atau menjelajahi fitur lain yang ditawarkan oleh GroupDocs.Signature untuk Java.