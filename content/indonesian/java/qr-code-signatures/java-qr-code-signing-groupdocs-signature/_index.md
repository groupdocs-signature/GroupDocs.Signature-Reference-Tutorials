---
"date": "2025-05-08"
"description": "Pelajari cara menerapkan penandatanganan kode QR Java menggunakan GroupDocs.Signature. Tingkatkan keamanan dokumen, konfigurasikan opsi penandatanganan, dan terapkan enkripsi khusus di aplikasi Java Anda."
"title": "Panduan Penandatanganan Kode QR Java&#58; Amankan Dokumen Anda dengan GroupDocs.Signature"
"url": "/id/java/qr-code-signatures/java-qr-code-signing-groupdocs-signature/"
"weight": 1
type: docs
---
# Menerapkan Penandatanganan Kode QR Java dengan GroupDocs.Signature untuk Java

## Perkenalan

Tingkatkan keamanan dokumen digital Anda dengan menyematkan kode QR ke dalam aplikasi Java Anda. Memanfaatkan GroupDocs.Signature untuk Java memungkinkan Anda memastikan keaslian dan keterlacakan dokumen secara efektif. Panduan ini akan memandu Anda dalam membuat tanda tangan data khusus, mengonfigurasi opsi penandatanganan kode QR, dan mengamankan dokumen Anda dengan enkripsi yang kuat.

**Apa yang Akan Anda Pelajari:**
- Cara membuat kelas tanda tangan data kustom menggunakan GroupDocs.Signature
- Mengonfigurasi opsi tanda kode QR di aplikasi Java
- Menandatangani dokumen dengan kode QR dan menerapkan enkripsi khusus

Mari selami prasyaratnya dan mulai mengintegrasikan fungsionalitas ini ke dalam proyek Anda!

## Prasyarat

Sebelum memulai, pastikan Anda telah menyiapkan pustaka dan dependensi yang diperlukan di lingkungan pengembangan Anda.

### Pustaka dan Versi yang Diperlukan

Untuk mengimplementasikan GroupDocs.Signature untuk Java, sertakan dependensi berikut:

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
implementation 'com.groupdocs:groupdocs-signation:23.12'
```

Anda juga dapat mengunduh versi terbaru langsung dari [GroupDocs.Signature untuk rilis Java](https://releases.groupdocs.com/signature/java/).

### Persyaratan Pengaturan Lingkungan

- Pastikan Anda telah menginstal Java Development Kit (JDK) yang berfungsi.
- Siapkan Lingkungan Pengembangan Terpadu (IDE) Anda, seperti IntelliJ IDEA atau Eclipse.

### Prasyarat Pengetahuan

- Pemahaman dasar tentang pemrograman Java dan konsep berorientasi objek.
- Kemampuan menangani dependensi menggunakan Maven atau Gradle.

## Menyiapkan GroupDocs.Signature untuk Java

Untuk memulai, atur GroupDocs.Signature di proyek Anda dengan mengikuti petunjuk instalasi di atas untuk memasukkannya ke dalam konfigurasi build Anda.

### Langkah-Langkah Perolehan Lisensi

GroupDocs menawarkan berbagai pilihan lisensi:
- **Uji Coba Gratis**:Uji semua fitur tanpa batasan.
- **Lisensi Sementara**: Dapatkan lisensi untuk tujuan evaluasi.
- **Pembelian**: Dapatkan lisensi penuh untuk penggunaan komersial.

Setelah mengunduh, inisialisasi GroupDocs.Signature seperti ini:

```java
import com.groupdocs.signature.Signature;

class InitializeGroupDocs {
    public static void main(String[] args) {
        Signature signature = new Signature("path/to/your/document");
        // Anda sekarang dapat mulai menggunakan objek tanda tangan untuk bekerja dengan dokumen.
    }
}
```

## Panduan Implementasi

Mari kita uraikan proses implementasi ke dalam beberapa bagian yang dapat dikelola, dengan fokus pada fitur-fitur utama.

### Kelas Tanda Tangan Data Kustom

#### Ringkasan
Buat kelas khusus untuk menyimpan data tanda tangan seperti ID, penulis, tanggal penandatanganan, dan faktor lainnya. Ini memastikan Anda memiliki semua metadata yang diperlukan yang terenkapsulasi dalam tanda tangan Anda.

#### Implementasi Langkah demi Langkah

**Tentukan Kelas DocumentSignatureData**

```java
import com.groupdocs.signature.domain.extensions.serialization.FormatAttribute;
import java.util.Date;
import java.math.BigDecimal;

class DocumentSignatureData {
    @FormatAttribute(propertyName = "SignID")
    public String ID; // Pengidentifikasi unik untuk tanda tangan
    
    public String getID() { return ID; }
    public void setID(String value) { ID = value; }
    
    @FormatAttribute(propertyName = "SAuth")
    public final String Author; // Penulis dokumen
    
    public final String getAuthor() { return Author; }
    public final void setAuthor(String value) { Author = value; }
    
    @FormatAttribute(propertyName = "SDate", propertyFormat = "yyyy-MM-dd")
    public final Date Signed = new Date(); // Tanggal dan waktu penandatanganan
    
    public final Date getSigned() { return Signed; }
    public final void setSigned(Date value) { Signed = value; }
    
    @FormatAttribute(propertyName = "SDFact", propertyFormat = "N2")
    public final BigDecimal DataFactor = new BigDecimal(0.01); // Faktor data tambahan untuk tanda tangan
    
    public final BigDecimal getDataFactor() { return DataFactor; }
    public final void setDataFactor(BigDecimal value) { DataFactor = value; }
}
```

**Penjelasan:**
- **Atribut Format**: Memberi anotasi pada properti untuk menyesuaikan serialisasi.
- **Properti**: Menangkap rincian penting seperti ID unik, nama penulis, tanggal penandatanganan, dan faktor data.

### Konfigurasi Opsi Tanda Kode QR

#### Ringkasan
Konfigurasikan opsi tanda kode QR untuk menentukan bagaimana kode QR Anda akan muncul pada dokumen, termasuk ukuran, perataan, dan bantalan.

#### Implementasi Langkah demi Langkah

**Tentukan Kelas QrCodeSignOptionsConfig**

```java
import com.groupdocs.signature.domain.enums.HorizontalAlignment;
import com.groupdocs.signature.domain.enums.VerticalAlignment;
import com.groupdocs.signature.domain.qrcodes.QrCodeTypes;
import com.groupdocs.signature.domain.Padding;
import com.groupdocs.signature.options.sign.QrCodeSignOptions;

class QrCodeSignOptionsConfig {
    public static QrCodeSignOptions setupQrCodeSignOptions(DocumentSignatureData documentSignature) {
        QrCodeSignOptions options = new QrCodeSignOptions();
        
        // Serialisasikan objek data kustom ke dalam kode QR
        options.setData(documentSignature);
        
        // Tentukan jenis kode QR
        options.setEncodeType(QrCodeTypes.QR);
        
        // Konfigurasikan bantalan untuk penyelarasan
        Padding padding = new Padding();
        padding.setRight(10); // Padding kanan dalam piksel
        padding.setBottom(10); // Padding bawah dalam piksel
        options.setMargin(padding);
        
        // Tentukan ukuran dan posisi kode QR
        options.setHeight(100);
        options.setWidth(100);
        options.setVerticalAlignment(VerticalAlignment.Bottom);
        options.setHorizontalAlignment(HorizontalAlignment.Right);
        
        return options;
    }
}
```

**Penjelasan:**
- **Opsi Tanda QrCode**: Mengelola bagaimana kode QR ditampilkan, termasuk ukuran dan posisinya.
- **Lapisan**Menyesuaikan perataan dalam dokumen.

### Penandatanganan Dokumen dengan Kode QR dan Enkripsi Kustom

#### Ringkasan
Gabungkan kode QR dan enkripsi khusus untuk menandatangani dokumen dengan aman. Ini menjamin integritas dan kerahasiaan data.

#### Implementasi Langkah demi Langkah

**Tandatangani Dokumen dengan Kode QR**

```java
import com.groupdocs.signature.Signature;
import com.groupdocs.signature.domain.extensions.encryption.IDataEncryption;
import com.groupdocs.signature.exception.GroupDocsSignatureException;

import java.util.UUID;

class SignDocumentWithQRCode {
    public static void signDocument(String filePath, String outputFilePath) throws Exception {
        try {
            Signature signature = new Signature(filePath);

            // Strategi enkripsi XOR khusus
            IDataEncryption encryption = new CustomXOREncryption();

            // Konfigurasikan objek data tanda tangan dokumen kustom
            DocumentSignatureData documentSignature = new DocumentSignatureData();
            documentSignature.setID(UUID.randomUUID().toString());
            documentSignature.setAuthor(System.getenv("USERNAME"));
            documentSignature.setSigned(new Date());
            documentSignature.setDataFactor(new BigDecimal("11.22"));

            // Siapkan opsi Kode QR
            QrCodeSignOptions options = QrCodeSignOptionsConfig.setupQrCodeSignOptions(documentSignature);

            // Terapkan enkripsi pada data dalam kode QR
            options.setDataEncryption(encryption);

            // Tanda tangani dan simpan dokumennya
            signature.sign(outputFilePath, options);
        } catch (Exception e) {
            throw new GroupDocsSignatureException(e.getMessage());
        }
    }
}
```

**Penjelasan:**
- **Enkripsi XORE Kustom**: Menerapkan strategi enkripsi khusus untuk mengamankan data kode QR.
- **UUID**: Menghasilkan pengenal unik untuk setiap tanda tangan.