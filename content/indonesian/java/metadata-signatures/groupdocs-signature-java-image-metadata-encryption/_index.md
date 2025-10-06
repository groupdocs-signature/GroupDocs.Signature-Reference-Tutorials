---
"date": "2025-05-08"
"description": "Pelajari cara mengamankan metadata gambar menggunakan enkripsi dengan GroupDocs.Signature untuk Java. Pastikan integritas dan keaslian data dengan panduan langkah demi langkah."
"title": "Implementasi Penandatanganan dan Enkripsi Metadata Gambar di Java dengan GroupDocs.Signature"
"url": "/id/java/metadata-signatures/groupdocs-signature-java-image-metadata-encryption/"
"weight": 1
type: docs
---
# Implementasi Penandatanganan Metadata Gambar dengan Enkripsi di Java Menggunakan GroupDocs.Signature

## Perkenalan

Dalam lanskap digital saat ini, mengamankan informasi sensitif dalam metadata dokumen sangatlah penting. Baik untuk kontrak bisnis rahasia maupun foto identitas pribadi, menjaga integritas dan keaslian metadata gambar membantu mencegah akses dan manipulasi tanpa izin. **GroupDocs.Signature untuk Java** menyediakan solusi kuat untuk menandatangani dan mengenkripsi metadata gambar dengan aman.

Tutorial ini memandu Anda dalam mengimplementasikan penandatanganan metadata gambar dengan enkripsi di Java menggunakan fitur-fitur canggih GroupDocs.Signature. Dengan mengikuti langkah-langkah ini, Anda akan mengintegrasikan fungsionalitas ini ke dalam aplikasi Java Anda secara efektif.

**Apa yang Akan Anda Pelajari:**
- Menandatangani metadata dokumen menggunakan GroupDocs.Signature untuk Java
- Menerapkan tanda tangan objek kustom dengan enkripsi
- Menyiapkan lingkungan yang aman menggunakan enkripsi kunci simetris

## Prasyarat

Sebelum memulai, pastikan prasyarat berikut terpenuhi:

### Pustaka dan Dependensi yang Diperlukan:
- **GroupDocs.Signature untuk Java**: Pastikan Anda memiliki versi 23.12 atau yang lebih baru.

### Persyaratan Pengaturan Lingkungan:
- Instal Java Development Kit (JDK) di komputer Anda.
- Gunakan Lingkungan Pengembangan Terpadu (IDE) seperti IntelliJ IDEA, Eclipse, atau NetBeans.

### Prasyarat Pengetahuan:
- Pemahaman dasar tentang pemrograman Java.
- Keakraban dengan Maven atau Gradle untuk manajemen ketergantungan.

## Menyiapkan GroupDocs.Signature untuk Java

Untuk menggunakan GroupDocs.Signature dalam proyek Anda, sertakan dependensi yang diperlukan sebagai berikut:

### Menggunakan Maven
Tambahkan ini ke Anda `pom.xml` mengajukan:
```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

### Menggunakan Gradle
Sertakan ini di dalam `build.gradle` mengajukan:
```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

### Unduh Langsung
Atau, unduh versi terbaru dari [GroupDocs.Signature untuk rilis Java](https://releases.groupdocs.com/signature/java/).

#### Langkah-Langkah Perolehan Lisensi
- **Uji Coba Gratis**:Mulailah dengan uji coba untuk menjelajahi fitur-fitur.
- **Lisensi Sementara**:Lakukan pengujian ekstensif jika diperlukan.
- **Pembelian**: Dapatkan lisensi untuk penggunaan produksi dari [GroupDocs](https://purchase.groupdocs.com/buy).

## Inisialisasi dan Pengaturan Dasar

Berikut cara menginisialisasi GroupDocs.Signature di aplikasi Java Anda:

```java
import com.groupdocs.signature.Signature;

public class InitializeSignature {
    public static void main(String[] args) {
        // Jalur menuju dokumen
        String filePath = "path/to/your/document.jpg";
        
        // Buat contoh baru Signature
        Signature signature = new Signature(filePath);

        System.out.println("GroupDocs.Signature initialized successfully.");
    }
}
```

## Panduan Implementasi

### Fitur: Tanda Tangan Metadata dengan Objek Kustom

#### Ringkasan
Fitur ini memungkinkan penandatanganan metadata gambar menggunakan objek khusus dan mengenkripsinya untuk keamanan tambahan, memastikan bahwa hanya pihak berwenang yang dapat mengakses atau mengubah metadata.

#### Implementasi Langkah demi Langkah

##### 1. Tentukan Kelas Data Tanda Tangan Dokumen Anda
Buat kelas untuk menyimpan informasi metadata Anda:

```java
import java.math.BigDecimal;
import java.util.Date;

class DocumentSignatureData {
    private String ID;
    private String Author;
    private Date Signed = new Date();
    private BigDecimal DataFactor = new BigDecimal(0.01);

    public String getID() { return ID; }
    public void setID(String value) { ID = value; }

    @FormatAttribute(propertyName = "SignID")
    public final String getAuthor() { return Author; }
    public final void setAuthor(String value) { Author = value; }

    @FormatAttribute(propertyName = "SAuth")
    public final Date getSigned() { return Signed; }
    public final void setSigned(Date value) { Signed = value; }

    @FormatAttribute(propertyName = "SDate", propertyFormat = "yyyy-MM-dd")
    public final BigDecimal getDataFactor() { return DataFactor; }
    public final void setDataFactor(BigDecimal value) { DataFactor = value; }
}
```

##### 2. Terapkan Logika Tanda Tangan
Berikut cara menandatangani metadata menggunakan enkripsi:

```java
import com.groupdocs.signature.Signature;
import com.groupdocs.signature.domain.extensions.encryption.IDataEncryption;
import com.groupdocs.signature.domain.extensions.encryption.SymmetricAlgorithmType;
import com.groupdocs.signature.domain.extensions.encryption.SymmetricEncryption;
import com.groupdocs.signature.domain.signatures.metadata.ImageMetadataSignature;
import com.groupdocs.signature.exception.GroupDocsSignatureException;
import com.groupdocs.signature.options.sign.MetadataSignOptions;

import java.io.File;
import java.nio.file.Paths;
import java.util.UUID;

public class SignMetadataWithCustomObject {
    // Inisialisasi jalur file dengan placeholder
    String filePath = "YOUR_DOCUMENT_DIRECTORY/SampleImage.jpg";
    String outputFilePath = new File("YOUR_OUTPUT_DIRECTORY", 
                                       "SignedImageWithCustomMetadata/SampleImage_signed.jpg").getPath();

    public void run() throws Exception {
        Signature signature = new Signature(filePath);

        // Siapkan kunci dan frasa sandi untuk enkripsi
        String key = "1234567890";
        String salt = "1234567890";
        IDataEncryption encryption = new SymmetricEncryption(
            SymmetricAlgorithmType.Rijndael, key, salt);

        MetadataSignOptions options = new MetadataSignOptions();
        DocumentSignatureData documentSignature = new DocumentSignatureData();
        
        // Tetapkan properti metadata khusus
        documentSignature.setID(UUID.randomUUID().toString());
        documentSignature.setAuthor(System.getenv("USERNAME"));
        documentSignature.setSigned(new Date());
        documentSignature.setDataFactor(new BigDecimal("11.22"));

        ImageMetadataSignature mdDocument = new ImageMetadataSignature(41996, documentSignature);
        mdDocument.setDataEncryption(encryption);

        // Tambahkan tanda tangan metadata ke opsi
        options.getSignatures().add(mdDocument);

        signature.sign(outputFilePath, options);
    }
}
```

#### Opsi Konfigurasi Utama
- **Enkripsi Simetris**: Menggunakan algoritma Rijndael untuk enkripsi.
- **Metadata SignOptions**: Mengonfigurasi proses penandatanganan dan menentukan metadata mana yang akan ditandatangani.

##### Tips Pemecahan Masalah
- Pastikan jalur berkas Anda benar dan dapat diakses.
- Periksa apakah variabel lingkungan `USERNAME` diatur dengan benar.
- Verifikasi bahwa versi pustaka GroupDocs.Signature cocok dengan dependensi kode Anda.

### Fitur: Tanda Tangan Metadata dengan Enkripsi

#### Ringkasan
Fitur ini berfokus pada enkripsi tanda tangan metadata untuk melindungi informasi sensitif dalam berkas gambar.

#### Implementasi Langkah demi Langkah
##### 1. Terapkan Logika Enkripsi
Berikut cara menandatangani metadata menggunakan enkripsi:
```java
import com.groupdocs.signature.Signature;
import com.groupdocs.signature.domain.extensions.encryption.IDataEncryption;
import com.groupdocs.signature.domain.extensions.encryption.SymmetricAlgorithmType;
import com.groupdocs.signature.domain.extensions.encryption.SymmetricEncryption;
import com.groupdocs.signature.exception.GroupDocsSignatureException;
import com.groupdocs.signature.options.sign.MetadataSignOptions;

import java.io.File;
import java.nio.file.Paths;
import java.util.UUID;

public class SignMetadataWithEncryption {
    // Inisialisasi jalur file dengan placeholder
    String filePath = "YOUR_DOCUMENT_DIRECTORY/SampleImage.jpg";
    String outputFilePath = new File("YOUR_OUTPUT_DIRECTORY", 
                                       "SignedImageWithEncryption/SampleImage_signed.jpg").getPath();

    public void run() throws Exception {
        Signature signature = new Signature(filePath);

        // Siapkan kunci dan frasa sandi untuk enkripsi
        String key = "1234567890";
        String salt = "1234567890";
        IDataEncryption encryption = new SymmetricEncryption(
            SymmetricAlgorithmType.Rijndael, key, salt);

        MetadataSignOptions options = new MetadataSignOptions();
        DocumentSignatureData documentSignature = new DocumentSignatureData();
        
        // Tetapkan properti metadata khusus
        documentSignature.setID(UUID.randomUUID().toString());
        documentSignature.setAuthor(System.getenv("USERNAME"));
        documentSignature.setSigned(new Date());
        documentSignature.setDataFactor(new BigDecimal("11.22"));

        ImageMetadataSignature mdDocument = new ImageMetadataSignature(41996, documentSignature);
        mdDocument.setDataEncryption(encryption);

        // Tambahkan tanda tangan metadata ke opsi
        options.getSignatures().add(mdDocument);

        signature.sign(outputFilePath, options);
    }
}
```