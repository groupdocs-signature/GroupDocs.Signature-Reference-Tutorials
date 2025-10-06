---
"date": "2025-05-08"
"description": "Pelajari cara menerapkan serialisasi kode QR khusus dengan enkripsi dalam PDF menggunakan GroupDocs.Signature untuk Java. Amankan dokumen Anda secara efisien."
"title": "Implementasi Serialisasi & Enkripsi Kode QR Kustom dalam PDF menggunakan GroupDocs.Signature untuk Java"
"url": "/id/java/qr-code-signatures/groupdocs-signature-java-custom-qr-code-serialization/"
"weight": 1
type: docs
---
# Cara Menerapkan Serialisasi dan Enkripsi Kode QR Kustom dalam PDF Menggunakan GroupDocs.Signature untuk Java

## Perkenalan

Di era digital, penandatanganan dokumen yang aman sangat penting untuk menjaga integritas dan keaslian data. Gunakan GroupDocs.Signature for Java—pustaka canggih yang dirancang untuk menyederhanakan penambahan tanda tangan ke dokumen. Tutorial ini akan memandu Anda menerapkan serialisasi kode QR khusus dengan enkripsi dalam PDF menggunakan GroupDocs.Signature for Java.

**Apa yang Akan Anda Pelajari:**
- Cara mengatur dan mengonfigurasi GroupDocs.Signature untuk Java
- Menerapkan serialisasi khusus untuk tanda tangan kode QR
- Mengenkripsi data serial dalam kode QR
- Menerapkan fitur-fitur ini untuk mengamankan dokumen Anda

Sebelum kita mulai penerapannya, mari pastikan Anda memiliki semua yang diperlukan untuk mengikutinya.

### Prasyarat

Untuk menggunakan tutorial ini secara efektif, pastikan Anda memenuhi prasyarat berikut:

1. **Pustaka dan Dependensi yang Diperlukan:**
   - GroupDocs.Signature untuk Java versi 23.12 atau lebih tinggi
   - Maven atau Gradle untuk manajemen ketergantungan (opsional)

2. **Persyaratan Pengaturan Lingkungan:**
   - Java Development Kit (JDK) terinstal di mesin Anda
   - Pemahaman dasar tentang pemrograman Java

3. **Prasyarat Pengetahuan:**
   - Keakraban dengan Java dan konsep pemrograman berorientasi objek
   - Pengetahuan dasar tentang bekerja dengan PDF di Java

## Menyiapkan GroupDocs.Signature untuk Java

Untuk memulai, Anda perlu menyiapkan pustaka GroupDocs.Signature di lingkungan proyek Anda.

### Instalasi Maven

Jika Anda menggunakan Maven, tambahkan dependensi berikut ke `pom.xml` mengajukan:

```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

### Instalasi Gradle

Untuk pengguna Gradle, sertakan baris ini di `build.gradle` mengajukan:

```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

### Unduh Langsung

Atau, Anda dapat mengunduh versi terbaru langsung dari [GroupDocs.Signature untuk rilis Java](https://releases.groupdocs.com/signature/java/).

#### Langkah-Langkah Perolehan Lisensi
- **Uji Coba Gratis:** Mulailah dengan mengunduh versi uji coba untuk menguji fitur-fiturnya.
- **Lisensi Sementara:** Anda dapat meminta lisensi sementara jika diperlukan, yang memungkinkan Anda mengevaluasi produk tanpa batasan apa pun.
- **Pembelian:** Untuk penggunaan jangka panjang, pertimbangkan untuk membeli lisensi penuh.

Setelah terinstal, inisialisasi GroupDocs.Signature di proyek Anda:

```java
import com.groupdocs.signature.Signature;

public class SetupGroupDocs {
    public static void main(String[] args) {
        Signature signature = new Signature("YOUR_DOCUMENT_DIRECTORY/sample.pdf");
        // Kode Anda di sini...
    }
}
```

## Panduan Implementasi

Sekarang, mari selami penerapan serialisasi dan enkripsi kode QR khusus dengan GroupDocs.Signature untuk Java.

### Kelas Serialisasi Kustom untuk Tanda Tangan Kode QR

#### Ringkasan

Fitur ini melibatkan pembuatan kelas yang menangani serialisasi metadata menjadi tanda tangan kode QR. `DocumentSignatureData` kelas menyimpan atribut seperti ID, penulis, tanggal penandatanganan, dan faktor data.

```java
import com.groupdocs.signature.domain.extensions.serialization.FormatAttribute;
import java.math.BigDecimal;
import java.util.Date;

class DocumentSignatureData {
    @FormatAttribute(propertyName = "SignID")
    public String ID;

    public void setID(String value) { 
        this.ID = value; 
    }

    @FormatAttribute(propertyName = "SAuth")
    public String author;

    public void setAuthor(String value) {
        this.author = value;
    }

    @FormatAttribute(propertyName = "SDate", propertyFormat = "yyyy-MM-dd")
    public Date signed = new Date();

    public void setSigned(Date value) {
        this.signed = value;
    }

    @FormatAttribute(propertyName = "SDFact", propertyFormat = "N2")
    public BigDecimal dataFactor = new BigDecimal(0.01);

    public void setDataFactor(BigDecimal value) {
        this.dataFactor = value;
    }
}
```

#### Penjelasan
- **Atribut:** Itu `@FormatAttribute` anotasi menentukan bagaimana setiap atribut diserialkan ke dalam kode QR.
  - **PENGENAL**Pengidentifikasi unik untuk tanda tangan.
  - **Pengarang**: Orang yang menandatangani dokumen tersebut.
  - **Tanggal Ditandatangani**: Cap waktu saat dokumen ditandatangani.
  - **Faktor Data**: Data numerik tambahan yang dikaitkan dengan tanda tangan.

### Tanda Tangan Kode QR dengan Serialisasi dan Enkripsi Data Kustom

#### Ringkasan

Bagian ini memperagakan cara menandatangani dokumen menggunakan kode QR yang menyertakan data serialisasi dan enkripsi khusus.

```java
import com.groupdocs.signature.Signature;
import com.groupdocs.signature.domain.Padding;
import com.groupdocs.signature.domain.enums.HorizontalAlignment;
import com.groupdocs.signature.domain.enums.VerticalAlignment;
import com.groupdocs.signature.domain.extensions.encryption.IDataEncryption;
import com.groupdocs.signature.domain.qrcodes.QrCodeTypes;
import com.groupdocs.signature.exception.GroupDocsSignatureException;
import com.groupdocs.signature.options.sign.QrCodeSignOptions;
import java.io.File;
import java.math.BigDecimal;
import java.util.Date;
import java.util.UUID;

class SignWithQRCodeCustomSerialization {
    String filePath = "YOUR_DOCUMENT_DIRECTORY/sample.pdf"; 
    String outputFilePath = new File("YOUR_OUTPUT_DIRECTORY", "SignedQRCodeCustomSerialization.pdf").getPath();

    public void signDocument() throws Exception {
        Signature signature = new Signature(filePath);

        // Terapkan logika enkripsi khusus Anda di sini
        IDataEncryption encryption = new CustomXOREncryption();

        DocumentSignatureData documentSignature = new DocumentSignatureData();
        documentSignature.setID(UUID.randomUUID().toString());
        documentSignature.setAuthor(System.getenv("USERNAME")); 
        documentSignature.setSigned(new Date());
        documentSignature.setDataFactor(new BigDecimal("11.22"));

        QrCodeSignOptions options = new QrCodeSignOptions();
        options.setData(documentSignature);
        options.setEncodeType(QrCodeTypes.QR);
        options.setDataEncryption(encryption);

        // Konfigurasikan penyelarasan dan tampilan
        options.setHeight(100);
        options.setWidth(100);
        options.setVerticalAlignment(VerticalAlignment.Bottom);
        options.setHorizontalAlignment(HorizontalAlignment.Right);
        
        Padding padding = new Padding();
        padding.setRight(10);
        padding.setBottom(10);
        options.setMargin(padding);

        signature.sign(outputFilePath, options);
    }
}
```

#### Penjelasan
- **Enkripsi Kustom:** Terapkan logika enkripsi Anda sendiri di `CustomXOREncryption` atau menggunakan metode lain yang menerapkan `IDataEncryption`.
- **Opsi Tanda Tangan:** Konfigurasikan tampilan dan penyelarasan kode QR dengan opsi seperti tinggi, lebar, bantalan, dll.
- **Proses Penandatanganan:** Itu `signature.sign()` metode menerapkan tanda tangan kode QR ke dokumen.

### Tips Pemecahan Masalah

- Pastikan semua dependensi dikonfigurasikan dengan benar di alat build Anda (Maven/Gradle).
- Verifikasi bahwa jalur berkas untuk dokumen masukan dan keluaran akurat.
- Pastikan logika enkripsi khusus Anda diterapkan dan terintegrasi dengan benar.

## Aplikasi Praktis

Berikut adalah beberapa aplikasi nyata dari fitur ini:

1. **Penandatanganan Dokumen Hukum:** Tandatangani kontrak secara aman dengan metadata yang tertanam dalam kode QR untuk memastikan keaslian.
2. **Pemrosesan Faktur:** Secara otomatis menambahkan tanda tangan terenkripsi ke faktur untuk menambah keamanan dan keterlacakan.
3. **Pelacakan Logistik:** Gunakan dokumen yang ditandatangani untuk pelacakan pengiriman, tanamkan pengenal unik dan stempel waktu dalam kode QR.
4. **Sertifikasi Akademik:** Sematkan informasi siswa dengan aman ke dalam sertifikat digital menggunakan tanda tangan kode QR