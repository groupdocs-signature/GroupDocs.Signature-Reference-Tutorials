---
"date": "2025-05-08"
"description": "Pelajari cara mengamankan PDF menggunakan enkripsi kode QR dan tanda tangan digital dengan GroupDocs.Signature untuk Java. Tingkatkan keamanan dokumen Anda secara efektif."
"title": "Menerapkan Penandatanganan PDF Aman dengan Enkripsi Kode QR di Java Menggunakan GroupDocs.Signature"
"url": "/id/java/qr-code-signatures/secure-pdf-signing-qr-code-groupdocs-java/"
"weight": 1
---

# Cara Menerapkan Penandatanganan PDF Aman dengan Enkripsi Kode QR di Java Menggunakan GroupDocs.Signature

Di era digital saat ini, mengamankan informasi sensitif dalam dokumen sangatlah penting. Maraknya ancaman siber telah menjadikan enkripsi data sebagai bagian penting dari manajemen dokumen. Tutorial ini memandu Anda dalam menerapkan penandatanganan PDF yang aman menggunakan enkripsi kode QR dengan GroupDocs.Signature untuk Java. Di akhir artikel ini, Anda akan siap untuk mengintegrasikan fitur keamanan yang tangguh ke dalam aplikasi Anda.

## Apa yang Akan Anda Pelajari:
- Memahami enkripsi data simetris di Java
- Membuat kelas tanda tangan khusus
- Mengonfigurasi tanda tangan kode QR dengan data dan penyelarasan khusus
- Mengintegrasikan GroupDocs.Signature untuk penandatanganan PDF yang aman

Siap untuk memulai? Ayo mulai!

## Prasyarat
Sebelum kita mulai, pastikan Anda memiliki hal berikut:
- **Kit Pengembangan Java (JDK):** Versi 8 atau lebih tinggi.
- **Maven atau Gradle:** Untuk manajemen ketergantungan. Pilih berdasarkan pengaturan proyek Anda.
- **Pengetahuan Pemrograman Java:** Pemahaman dasar tentang pemrograman berorientasi objek di Java.

## Menyiapkan GroupDocs.Signature untuk Java
Untuk mulai menggunakan GroupDocs.Signature, Anda perlu menambahkannya sebagai dependensi ke proyek Anda. Pustaka ini menawarkan alat canggih untuk mengelola tanda tangan digital dan enkripsi dokumen.

### Pengaturan Maven
Tambahkan dependensi berikut ke `pom.xml` mengajukan:
```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

### Pengaturan Gradle
Untuk pengguna Gradle, sertakan ini di `build.gradle` mengajukan:
```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

### Unduh Langsung
Atau, unduh versi terbaru dari [GroupDocs.Signature untuk rilis Java](https://releases.groupdocs.com/signature/java/).

### Akuisisi Lisensi
Anda dapat memulai dengan uji coba gratis GroupDocs.Signature untuk mengevaluasi fitur-fiturnya. Untuk penggunaan jangka panjang, pertimbangkan untuk membeli lisensi atau mengajukan lisensi sementara melalui situs web mereka.

## Panduan Implementasi
Panduan ini dibagi menjadi beberapa bagian utama yang mencakup enkripsi data, pembuatan tanda tangan khusus, dan konfigurasi tanda tangan kode QR.

### Enkripsi Data dengan Algoritma Simetris
Mengenkripsi data Anda memastikan keamanannya selama transmisi dan penyimpanan. Berikut cara mengatur enkripsi simetris menggunakan GroupDocs.Signature:

#### Menyiapkan Enkripsi Simetris
1. **Impor Paket yang Diperlukan:**
   ```java
   import com.groupdocs.signature.domain.extensions.encryption.IDataEncryption;
   import com.groupdocs.signature.domain.extensions.encryption.SymmetricAlgorithmType;
   import com.groupdocs.signature.domain.extensions.encryption.SymmetricEncryption;
   ```
2. **Inisialisasi Objek Enkripsi:**
   Gunakan kunci aman dan garam untuk enkripsi. Ganti `"YOUR_SECURE_KEY"` dengan kunci Anda sendiri.
   ```java
   String key = "YOUR_SECURE_KEY";
   String salt = "YOUR_SECURE_SALT";

   IDataEncryption encryption = new SymmetricEncryption(
       SymmetricAlgorithmType.Rijndael, 
       key, 
       salt
   );
   ```
   - **TipeAlgoritmaSimetris.Rijndael:** Ini menentukan jenis algoritma simetris yang akan digunakan.
   - **Kunci dan Garam:** Pastikan ini unik dan aman untuk aplikasi Anda.

### Kelas Tanda Tangan Data Kustom
Membuat kelas khusus memungkinkan Anda mengelola properti tanda tangan secara efektif. Berikut caranya:

#### Mendefinisikan `DocumentSignatureData` Kelas
```java
class DocumentSignatureData {
    private String ID;
    private String Author;
    private Date Signed = new Date();
    private BigDecimal DataFactor = new BigDecimal(0.01);

    public String getID() { return ID; }
    public void setID(String value) { ID = value; }

    public final String getAuthor() { return Author; }
    public final void setAuthor(String value) { Author = value; }

    public final Date getSigned() { return Signed; }
    public final void setSigned(Date value) { Signed = value; }

    public final BigDecimal getDataFactor() { return DataFactor; }
    public final void setDataFactor(BigDecimal value) { DataFactor = value; }
}
```
- **ID, Penulis, Tanda Tangan:** Bidang ini menyimpan metadata tanda tangan.
- **Faktor Data:** Menyimpan nilai numerik yang relevan dengan logika aplikasi Anda.

### Opsi Tanda Tangan Kode QR
Kode QR menawarkan cara yang ringkas untuk menyematkan informasi. Konfigurasikan kode QR dengan data dan enkripsi khusus:

#### Menyiapkan Tanda Tangan Kode QR
1. **Inisialisasi `Signature` Obyek:**
   ```java
   import com.groupdocs.signature.Signature;
   
   Signature signature = new Signature("YOUR_DOCUMENT_DIRECTORY");
   ```
2. **Konfigurasikan Opsi Kode QR:**
   ```java
   import com.groupdocs.signature.domain.qrcodes.QrCodeTypes;
   import com.groupdocs.signature.options.sign.QrCodeSignOptions;
   import java.util.UUID;

   DocumentSignatureData documentSignature = new DocumentSignatureData();
   documentSignature.setID(UUID.randomUUID().toString());
   documentSignature.setAuthor(System.getenv("USERNAME"));
   documentSignature.setDataFactor(new BigDecimal("11.22"));

   QrCodeSignOptions options = new QrCodeSignOptions();
   options.setData(documentSignature);
   options.setEncodeType(QrCodeTypes.QR);
   options.setDataEncryption(encryption); // Gunakan objek enkripsi
   options.setHeight(100);
   options.setWidth(100);
   options.setVerticalAlignment(com.groupdocs.signature.domain.enums.VerticalAlignment.Bottom);
   options.setHorizontalAlignment(com.groupdocs.signature.domain.enums.HorizontalAlignment.Right);

   import com.groupdocs.signature.domain.Padding;
   Padding padding = new Padding();
   padding.setRight(10);
   padding.setBottom(10);
   options.setMargin(padding);
   ```
   - **Jenis Pengkodean:** Menentukan format kode QR.
   - **Penjajaran dan Margin:** Sesuaikan bagaimana kode QR muncul pada dokumen.

### Contoh Penggunaan
Untuk menandatangani dokumen dengan opsi yang Anda konfigurasikan:
```java
signature.sign("YOUR_OUTPUT_DIRECTORY/QRCodeEncryptedObject.pdf\