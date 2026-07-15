---
date: '2026-07-15'
description: Pelajari cara menambahkan barcode PDF Java menggunakan GroupDocs.Signature
  – panduan langkah demi langkah untuk menandatangani, memverifikasi, mencari, memperbarui,
  dan menghapus tanda tangan barcode pada dokumen Java.
keywords:
- add barcode pdf java
- groupdocs barcode signature
- java document signing
lastmod: '2026-07-15'
linktitle: Panduan Tanda Tangan Barcode Java
og_description: Pelajari cara menambahkan barcode PDF Java menggunakan GroupDocs.Signature
  – panduan langkah demi langkah untuk menandatangani, memverifikasi, mencari, memperbarui,
  dan menghapus tanda tangan barcode pada dokumen Java.
og_image_alt: Guide showing how to add barcode PDF Java using GroupDocs.Signature
og_title: Tambahkan Barcode PDF Java – Tanda Tangan & Verifikasi dengan GroupDocs
schemas:
- author: GroupDocs
  dateModified: '2026-07-15'
  description: Learn how to add barcode PDF Java using GroupDocs.Signature – step‑by‑step
    guide to sign, verify, search, update and delete barcode signatures in Java documents.
  headline: Add Barcode PDF Java – Sign & Verify with GroupDocs
  type: TechArticle
- description: Learn how to add barcode PDF Java using GroupDocs.Signature – step‑by‑step
    guide to sign, verify, search, update and delete barcode signatures in Java documents.
  name: Add Barcode PDF Java – Sign & Verify with GroupDocs
  steps:
  - name: Case mismatch (e.g., “John Smith” vs. “john smith”).
    text: Case mismatch (e.g., “John Smith” vs. “john smith”).
  - name: Extra whitespace in the encoded text.
    text: Extra whitespace in the encoded text.
  - name: Wrong barcode type specified in the verification options.
    text: Wrong barcode type specified in the verification options.
  - name: Searching the wrong page number.
    text: Searching the wrong page number.
  - name: '**Reuse Signature Instances** – Create a single `Signature` object per
      document and reuse it for multiple operations.'
    text: '**Reuse Signature Instances** – Create a single `Signature` object per
      document and reuse it for multiple operations.'
  - name: '**Search Specific Pages Only** – Limit the page range to where barcodes
      are expected.'
    text: '**Search Specific Pages Only** – Limit the page range to where barcodes
      are expected.'
  - name: '**Choose the Simplest Barcode Type** – Simpler barcodes generate faster;
      only use QR or Data Matrix when you truly need the extra capacity.'
    text: '**Choose the Simplest Barcode Type** – Simpler barcodes generate faster;
      only use QR or Data Matrix when you truly need the extra capacity.'
  - name: '**Never Encode Sensitive Personal Data** – Barcodes are easily readable;
      avoid PII such as SSNs or passwords.'
    text: '**Never Encode Sensitive Personal Data** – Barcodes are easily readable;
      avoid PII such as SSNs or passwords.'
  - name: '**Validate Server‑Side** – Never trust client‑side verification alone;
      always re‑verify on a trusted backend.'
    text: '**Validate Server‑Side** – Never trust client‑side verification alone;
      always re‑verify on a trusted backend.'
  - name: '**Add Timestamps** – Include a timestamp in the barcode payload to prevent
      replay attacks.'
    text: '**Add Timestamps** – Include a timestamp in the barcode payload to prevent
      replay attacks.'
  type: HowTo
- questions:
  - answer: Yes – the library is fully compatible with JDK 8, 11, and 17.
    question: Can I use GroupDocs.Signature with Java 17?
  - answer: When you use Code128 or QR with sufficient size and contrast, the barcode
      remains scannable after printing and scanning.
    question: Does the barcode survive a print‑scan cycle?
  - answer: There is no hard limit; however, for optimal performance keep the total
      count below **200** per document.
    question: How many barcodes can a single document contain?
  - answer: A temporary license removes evaluation watermarks; a full license is mandatory
      for any production deployment.
    question: Is a license required for development builds?
  - answer: Yes – provide the password when creating the `Signature` object; the API
      will unlock the file internally.
    question: Can I sign password‑protected PDFs?
  type: FAQPage
tags:
- barcode signature
- groupdocs
- java
- pdf
- document signing
title: Tambahkan Barcode PDF Java – Tanda Tangan & Verifikasi dengan GroupDocs
type: docs
url: /id/java/digital-signatures/java-document-signature-groupdocs-signature-barcode/
weight: 1
---

# Tambahkan Barcode PDF Java – Tanda & Verifikasi dengan GroupDocs

Jika Anda membutuhkan cara cepat dan visual untuk menandai dokumen dalam alur kerja internal, menambahkan barcode ke PDF dengan Java adalah solusi yang sempurna. Dengan **GroupDocs.Signature**, Anda dapat menyematkan, memverifikasi, mencari, memperbarui, dan menghapus tanda barcode tanpa beban tanda digital berbasis PKI penuh. Tutorial ini memandu Anda melalui setiap langkah, mulai dari penyiapan lingkungan hingga praktik terbaik siap produksi.

## Jawaban Cepat
- **Library apa yang menambahkan barcode ke PDF dalam Java?** GroupDocs.Signature untuk Java.  
- **Bisakah saya menandatangani PDF, Word, dan gambar?** Ya – API mendukung 30+ format.  
- **Apakah saya memerlukan lisensi untuk pengembangan?** Lisensi sementara 30‑hari gratis; lisensi penuh diperlukan untuk produksi.  
- **Berapa baris kode yang diperlukan untuk menandatangani PDF?** Hanya dua baris: buat objek `Signature` dan panggil `sign`.  
- **Apakah verifikasi barcode sensitif terhadap huruf besar/kecil?** Ya – teks harus cocok persis, termasuk huruf besar/kecil dan spasi.

## Apa itu add barcode pdf java?
`add barcode pdf java` mengacu pada proses menggunakan kode Java untuk menyematkan barcode (seperti Code128, QR, atau Data Matrix) ke dalam file PDF. Teknik ini menyediakan tag yang dapat dibaca mesin yang dapat dipindai atau diverifikasi secara programatis, memungkinkan pelacakan dokumen yang cepat dalam sistem internal.

## Mengapa menggunakan tanda barcode alih-alih tanda digital penuh?
Tanda barcode **30‑50 % lebih cepat** untuk dibuat dan diverifikasi dibandingkan tanda digital berbasis PKI, dan mereka berfungsi dengan andal setelah siklus cetak‑scan. Mereka juga tidak memerlukan manajemen sertifikat, menjadikannya ideal untuk alur kerja internal bervolume tinggi di mana bukti kriptografis tidak wajib.

## Prasyarat

- **Java Development Kit (JDK) 8+** – Java 11 atau 17 disarankan untuk kinerja yang lebih baik.  
- **IDE** – IntelliJ IDEA atau Eclipse (contoh menggunakan sintaks IntelliJ).  
- **Alat Build** – Maven atau Gradle untuk manajemen dependensi.  

### Menambahkan GroupDocs.Signature ke Proyek Anda

Cara termudah untuk memulai adalah menambahkan pustaka melalui alat build Anda. Berikut caranya:

**Pengguna Maven** – Tambahkan ini ke `pom.xml`:

```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

**Pengguna Gradle** – Tambahkan ini ke `build.gradle`:

```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

**Unduhan JAR Langsung** – Jika Anda lebih suka penyiapan manual, dapatkan JAR dari [GroupDocs.Signature releases](https://releases.groupdocs.com/signature/java/) dan tambahkan ke classpath Anda.

### Mengatur Lisensi Anda

GroupDocs.Signature tidak gratis untuk penggunaan produksi, tetapi Anda memiliki opsi fleksibel:

- **Uji Coba Gratis** – Unduh dari [halaman unduhan GroupDocs](https://releases.groupdocs.com/signature/java/) untuk menguji fitur (watermark evaluasi ditambahkan).  
- **Lisensi Sementara** – Dapatkan akses penuh selama 30 hari melalui [halaman lisensi sementara GroupDocs](https://purchase.groupdocs.com/temporary-license/) – sempurna untuk proof of concept.  
- **Lisensi Penuh** – Untuk penerapan produksi, lihat [opsi pembelian GroupDocs](https://purchase.groupdocs.com/buy).  

**Tips Pro:** Mulailah dengan lisensi sementara untuk pengembangan; ini menghapus watermark setelah Anda beralih ke kunci permanen.

### Pemeriksaan Lingkungan Cepat

Setelah Anda menambahkan dependensi, jalankan tes sederhana:

```java
import com.groupdocs.signature.Signature;

public class SignatureTest {
    public static void main(String[] args) {
        try {
            Signature signature = new Signature("test.pdf");
            System.out.println("GroupDocs.Signature initialized successfully!");
            signature.dispose();
        } catch (Exception e) {
            System.err.println("Setup issue: " + e.getMessage());
        }
    }
}
```

Jika program berjalan tanpa error, lingkungan Anda siap. Jika Anda mengalami masalah, periksa versi JDK dan versi pustaka yang tepat yang Anda tambahkan.

## Kapan Menggunakan Tanda Barcode

Tanda barcode bersinar dalam skenario tertentu:

- **Alur Kerja Dokumen Internal** – Lacak faktur, pesanan pembelian, atau memo melalui rantai persetujuan.  
- **Pemrosesan Volume Tinggi** – Tanda ribuan dokumen dengan cepat; pembuatan barcode hingga **2× lebih cepat** dibandingkan tanda digital penuh.  
- **Jembatan Cetak‑Scan** – Barcode bertahan setelah siklus cetak‑scan, menjadikannya ideal untuk proses hybrid kertas‑digital.  
- **Integrasi Sistem Legacy** – Pemindai barcode yang ada dapat membaca tag tanpa perangkat lunak tambahan.  
- **Jejak Audit** – Sematkan ID transaksi atau timestamp yang dapat diverifikasi auditor secara instan.

Hindari tanda barcode untuk kontrak hukum, dokumen keamanan tinggi, atau pertukaran dengan mitra eksternal di mana tanda digital berbasis PKI diperlukan.

## Menyiapkan GroupDocs.Signature untuk Java

### Definisi Kelas Inti

Kelas `Signature` adalah titik masuk untuk semua operasi penandatanganan, verifikasi, pencarian, pembaruan, dan penghapusan di GroupDocs.Signature.

```java
import com.groupdocs.signature.Signature;
```

### Inisialisasi Dasar

Buat objek `Signature` yang menunjuk ke file target:

```java
Signature signature = new Signature("path/to/your/document.pdf");
```

**Catatan penting**

- Jalur dapat bersifat absolut atau relatif; gunakan `System.getProperty("user.home")` untuk kompatibilitas lintas‑platform.  
- GroupDocs mendukung **lebih dari 30 format input dan output**, termasuk PDF, DOCX, XLSX, PPTX, dan PNG.  
- Selalu lepaskan sumber daya dengan `signature.dispose()` atau blok try‑with‑resources:

```java
try (Signature signature = new Signature("path/to/your/document.pdf")) {
    // Your signing operations here
} catch (Exception e) {
    System.err.println("Error working with document: " + e.getMessage());
}
```

Sekarang Anda siap menambahkan barcode.

## Bagaimana cara menambahkan barcode ke PDF dalam Java?

Muat PDF sumber dengan `new Signature("input.pdf")`, konfigurasikan objek `BarcodeSignature` (misalnya Code128 dengan teks “John Smith”), dan panggil `sign` untuk menghasilkan file yang ditandatangani – semuanya dalam tiga baris kode yang singkat. Pendekatan ini memungkinkan Anda menyematkan tag yang dapat dibaca mesin sambil mempertahankan tata letak dokumen asli, dan berfungsi untuk semua format yang didukung, tidak hanya PDF.

### Implementasi Langkah‑per‑Langkah

#### 1. Tentukan Jalur File

Tetapkan lokasi untuk file sumber dan output:

```java
String filePath = "YOUR_DOCUMENT_DIRECTORY/sample.docx";
String outputFilePath = "YOUR_OUTPUT_DIRECTORY/signed_sample.docx";
```

#### 2. Buat Penangani Signature

Inisialisasi penangani dengan dokumen sumber:

```java
Signature signature = new Signature(filePath);
```

#### 3. Konfigurasikan Opsi Barcode

Objek `BarcodeSignature` mendefinisikan properti visual dan data dari barcode yang akan disematkan. Atur tipe barcode, teks yang dikodekan, posisi, ukuran, warna, dan font yang dapat dibaca manusia secara opsional:

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

> **Tips Pro:** Jika string yang dikodekan melebihi 20 karakter, tingkatkan lebar barcode untuk menghindari kesalahan pemindaian.

#### 4. Terapkan Signature

Jalankan operasi penandatanganan dan hasilkan file output:

```java
signature.sign(outputFilePath, signOptions);
```

#### 5. Contoh Dunia Nyata

Dalam sistem persetujuan faktur, Anda dapat menyematkan ID karyawan approver dan timestamp:

```java
String invoiceId = "INV-2025-0042";
String approver = "john.smith@company.com";
String timestamp = LocalDateTime.now().toString();

// Combine into barcode data
String barcodeData = invoiceId + "|" + approver + "|" + timestamp;

BarcodeSignOptions signOptions = new BarcodeSignOptions(barcodeData, BarcodeTypes.QR);
signOptions.setVerticalAlignment(VerticalAlignment.Bottom);
signOptions.setHorizontalAlignment(HorizontalAlignment.Right);

signature.sign(outputFilePath, signOptions);
```

PDF yang dihasilkan kini membawa barcode yang dapat dipindai yang mengkodekan semua metadata persetujuan yang diperlukan.

## Bagaimana saya dapat memverifikasi tanda barcode dalam dokumen Java?

Metode `Signature.verify` memeriksa dokumen untuk tanda barcode yang cocok berdasarkan opsi yang diberikan, mengembalikan boolean yang menunjukkan apakah barcode yang diharapkan ada. Verifikasi berguna untuk alur kerja otomatis di mana Anda perlu memastikan bahwa dokumen telah diproses oleh pihak yang tepat sebelum tindakan selanjutnya.

### Langkah‑Langkah Verifikasi

#### 1. Muat Dokumen yang Ditandatangani

```java
Signature signature = new Signature("YOUR_OUTPUT_DIRECTORY/signed_sample.docx");
```

#### 2. Tetapkan Kriteria Verifikasi

Tentukan teks tepat, format barcode, dan nomor halaman yang Anda harapkan:

```java
BarcodeVerifyOptions verifyOptions = new BarcodeVerifyOptions();
verifyOptions.setAllPages(false); // Only check the first page
verifyOptions.setPageNumber(1);
verifyOptions.setEncodeType(BarcodeTypes.Code128);
verifyOptions.setText("John Smith");
```

#### 3. Jalankan Verifikasi

Jalankan pemeriksaan dan tangani hasilnya:

```java
boolean isValid = signature.verify(verifyOptions) != null;

if (isValid) {
    System.out.println("Document signature verified successfully!");
} else {
    System.out.println("Warning: Signature verification failed!");
}
```

**Pola umum:** Untuk sekadar mengonfirmasi bahwa *setiap* barcode dari tipe tertentu ada, hapus filter `setText`:

```java
BarcodeVerifyOptions flexibleOptions = new BarcodeVerifyOptions();
flexibleOptions.setAllPages(true);
flexibleOptions.setEncodeType(BarcodeTypes.Code128);
// No setText() call = accept any text with this barcode type

boolean hasAnySignature = signature.verify(flexibleOptions) != null;
```

Atau verifikasi hanya format barcode tanpa memperhatikan kontennya:

```java
BarcodeVerifyOptions formatOnly = new BarcodeVerifyOptions();
formatOnly.setEncodeType(BarcodeTypes.QR);
// Confirms a QR code exists, regardless of content
```

> **Peringatan:** Verifikasi sensitif terhadap huruf besar/kecil dan spasi; selalu pangkas dan normalisasi data sebelum menandatangani.

## Bagaimana cara mencari tanda barcode di dalam dokumen?

Metode `Signature.search` memindai dokumen untuk tanda barcode yang cocok dengan `BarcodeSearchOptions` yang diberikan, mengembalikan koleksi yang mencakup lokasi setiap barcode, nomor halaman, dan nilai yang dikodekan. Kemampuan ini memungkinkan ekstraksi metadata secara massal tanpa membuka setiap file secara manual.

### Alur Kerja Pencarian

#### 1. Inisialisasi Pencarian

```java
Signature signature = new Signature("YOUR_OUTPUT_DIRECTORY/signed_sample.docx");
```

#### 2. Konfigurasikan Parameter Pencarian

Tentukan rentang halaman, tipe barcode, atau filter teks:

```java
BarcodeSearchOptions searchOptions = new BarcodeSearchOptions();
searchOptions.setAllPages(true); // Search the entire document
```

Opsional mempersempit pencarian untuk meningkatkan kinerja:

```java
BarcodeSearchOptions narrowSearch = new BarcodeSearchOptions();
narrowSearch.setAllPages(false);
narrowSearch.setPageNumber(1); // Only search page 1
narrowSearch.setEncodeType(BarcodeTypes.Code128); // Only find Code128 barcodes
```

#### 3. Eksekusi Pencarian

```java
java.util.List<BarcodeSignature> signatures = signature.search(BarcodeSignature.class, searchOptions);

System.out.println("Found " + signatures.size() + " barcode signature(s)");

for (BarcodeSignature bcSignature : signatures) {
    System.out.println("Barcode Type: " + bcSignature.getEncodeType().getTypeName());
    System.out.println("Text: " + bcSignature.getText());
    System.out.println("Position: (" + bcSignature.getLeft() + ", " + bcSignature.getTop() + ")");
    System.out.println("Size: " + bcSignature.getWidth() + "x" + bcSignature.getHeight());
    System.out.println("---");
}
```

#### 4. Contoh Ekstraksi Data

Ambil data persetujuan dari setiap barcode pada batch faktur:

```java
List<BarcodeSignature> foundSignatures = signature.search(BarcodeSignature.class, searchOptions);

for (BarcodeSignature sig : foundSignatures) {
    String barcodeData = sig.getText();
    
    // Parse your custom format (remember our invoice example?)
    String[] parts = barcodeData.split("\\|");
    if (parts.length == 3) {
        String invoiceId = parts[0];
        String approver = parts[1];
        String timestamp = parts[2];
        
        System.out.println("Invoice " + invoiceId + " approved by " + approver + " at " + timestamp);
    }
}
```

> **Tips Kinerja:** Untuk dokumen lebih dari 100 halaman, selalu batasi pencarian ke halaman yang memang berisi barcode; ini dapat mengurangi waktu proses hingga **70 %**.

## Bagaimana saya dapat memperbarui tanda barcode yang ada?

Metode `Signature.update` memodifikasi atribut visual dari tanda barcode yang ada—seperti posisi, ukuran, atau warna—sementara mempertahankan data yang dikodekan asli. Ini berguna ketika perubahan tata letak diperlukan setelah dokumen sudah ditandatangani.

### Prosedur Pembaruan

#### 1. Temukan Signature yang Akan Diperbarui

```java
Signature signature = new Signature("YOUR_OUTPUT_DIRECTORY/signed_sample.docx");

BarcodeSearchOptions searchOptions = new BarcodeSearchOptions();
searchOptions.setAllPages(true);

List<BarcodeSignature> signatures = signature.search(BarcodeSignature.class, searchOptions);
```

#### 2. Modifikasi Properti yang Diinginkan

```java
List<BarcodeSignature> signaturesToUpdate = new ArrayList<>();

if (!signatures.isEmpty()) {
    BarcodeSignature bcSignature = signatures.get(0); // Update the first found signature
    
    // Move it 100px right and 100px down
    bcSignature.setLeft(bcSignature.getLeft() + 100);
    bcSignature.setTop(bcSignature.getTop() + 100);
    
    // Make it bigger
    bcSignature.setWidth(200);
    bcSignature.setHeight(50);
    
    signaturesToUpdate.add(bcSignature);
}
```

Anda dapat mengubah beberapa atribut sekaligus:

```java
bcSignature.setLeft(50);
bcSignature.setTop(50);
bcSignature.setWidth(150);
bcSignature.setHeight(45);
// Note: You can't change the encoded text or barcode type with update
// For that, you'd need to delete and re-sign
```

#### 3. Simpan Perubahan

```java
ByteArrayOutputStream outputStream = new ByteArrayOutputStream();
signature.update(outputStream, signaturesToUpdate);

// If you want to save to a file instead:
// signature.update("path/to/updated_document.docx", signaturesToUpdate);
```

#### 4. Skenario Dunia Nyata

Pindahkan semua signature untuk menghindari tumpang tindih dengan logo perusahaan yang baru ditambahkan:

```java
List<BarcodeSignature> allSignatures = signature.search(BarcodeSignature.class, searchOptions);
List<BarcodeSignature> toUpdate = new ArrayList<>();

for (BarcodeSignature sig : allSignatures) {
    // Move all signatures down by 50px to clear space for new logo
    if (sig.getTop() < 100) {
        sig.setTop(sig.getTop() + 50);
        toUpdate.add(sig);
    }
}

if (!toUpdate.isEmpty()) {
    signature.update(outputStream, toUpdate);
    System.out.println("Repositioned " + toUpdate.size() + " signature(s)");
}
```

> **Batasan:** Mengubah teks yang dikodekan memerlukan penghapusan dan penyisipan signature baru.

## Bagaimana cara menghapus tanda barcode dari dokumen?

Metode `Signature.delete` secara permanen menghapus tanda barcode yang dipilih dari dokumen, menghapus baik elemen visual maupun data yang dikodekan. Gunakan operasi ini saat membersihkan signature uji atau ketika barcode tidak lagi relevan.

### Langkah‑Langkah Penghapusan

#### 1. Temukan Signature

```java
Signature signature = new Signature("YOUR_OUTPUT_DIRECTORY/signed_sample.docx");

BarcodeSearchOptions searchOptions = new BarcodeSearchOptions();
searchOptions.setAllPages(true);

List<BarcodeSignature> signatures = signature.search(BarcodeSignature.class, searchOptions);
```

#### 2. Hapus Signature yang Dipilih

```java
List<BarcodeSignature> signaturesToDelete = new ArrayList<>();

// Delete all Code128 signatures (for example)
for (BarcodeSignature sig : signatures) {
    if (sig.getEncodeType().equals(BarcodeTypes.Code128)) {
        signaturesToDelete.add(sig);
    }
}

if (!signaturesToDelete.isEmpty()) {
    boolean result = signature.delete(signaturesToDelete);
    
    if (result) {
        System.out.println("Successfully deleted " + signaturesToDelete.size() + " signature(s)");
    } else {
        System.err.println("Failed to delete signatures");
    }
}
```

#### 3. Contoh Penghapusan Bersyarat

Hapus hanya barcode yang lebih lama dari timestamp tertentu (asumsi timestamp merupakan bagian dari teks yang dikodekan):

```java
LocalDateTime cutoffDate = LocalDateTime.now().minusDays(30);
List<BarcodeSignature> outdatedSignatures = new ArrayList<>();

for (BarcodeSignature sig : signatures) {
    try {
        String text = sig.getText();
        // Assuming format like "data|timestamp"
        String[] parts = text.split("\\|");
        if (parts.length > 1) {
            LocalDateTime sigDate = LocalDateTime.parse(parts[1]);
            if (sigDate.isBefore(cutoffDate)) {
                outdatedSignatures.add(sig);
            }
        }
    } catch (Exception e) {
        // Skip signatures that don't match our format
        continue;
    }
}

if (!outdatedSignatures.isEmpty()) {
    signature.delete(outdatedSignatures);
    System.out.println("Removed " + outdatedSignatures.size() + " outdated signature(s)");
}
```

> **Perhatian:** Penghapusan tidak dapat dibatalkan; selalu operasikan pada salinan file produksi saat pengujian.

#### 4. Pola Penghapusan Batch

Bersihkan signature uji sebelum rilis:

```java
// Remove all signatures containing "TEST" in their text
List<BarcodeSignature> testSignatures = signatures.stream()
    .filter(sig -> sig.getText().toUpperCase().contains("TEST"))
    .collect(Collectors.toList());

if (!testSignatures.isEmpty()) {
    signature.delete(testSignatures);
    System.out.println("Cleaned up " + testSignatures.size() + " test signature(s)");
}
```

## Jenis Barcode: Panduan Praktis

Memilih barcode yang tepat memengaruhi keandalan pemindaian, kapasitas data, dan kompatibilitas printer.

### Code128 (Pilihan Paling Umum)

- **Kapan digunakan:** Data alfanumerik, kepadatan tinggi, dokumen tercetak.  
- **Keunggulan:** Kompak, bekerja dengan pemindai standar, mencetak jelas pada ukuran kecil.  
- **Kekurangan:** Terbatas pada ASCII, kurang tahan error dibandingkan kode 2‑D.  

```java
BarcodeSignOptions code128 = new BarcodeSignOptions("INV-2025-042", BarcodeTypes.Code128);
```

### QR Code (Terbaik untuk Mobile)

- **Kapan digunakan:** Pemindaian mobile, payload data besar (URL, JSON, dll.), dokumen yang mungkin rusak.  
- **Keunggulan:** Hingga 4 000 karakter, koreksi error bawaan, ramah smartphone.  
- **Kekurangan:** Jejak visual lebih besar, memerlukan resolusi lebih tinggi untuk ukuran kecil.  

```java
String jsonData = "{\"invoice\":\"INV-042\",\"amount\":1500.00,\"approver\":\"john@company.com\"}";
BarcodeSignOptions qrCode = new BarcodeSignOptions(jsonData, BarcodeTypes.QR);
```

### Code39 (Andalan Lama)

- **Kapan digunakan:** Lingkungan pemindai legacy, kebutuhan teks yang dapat dibaca manusia.  
- **Keunggulan:** Dukungan legacy luas, format sederhana, tidak memerlukan checksum.  
- **Kekurangan:** Kepadatan data rendah, set karakter terbatas, memakan lebih banyak ruang.  

### Data Matrix (Kekuatan Kompak)

- **Kapan digunakan:** Ruang sangat terbatas, menandai barang kecil, data kepadatan tinggi.  
- **Keunggulan:** Sangat kompak, koreksi error kuat, bekerja pada permukaan melengkung.  
- **Kekurangan:** Memerlukan pencetakan berkualitas tinggi, dukungan pemindai kurang umum.  

#### Perbandingan Cepat

| Tipe Barcode | Kapasitas Data | Terbaik Untuk | Ukuran Tipikal |
|--------------|----------------|---------------|----------------|
| Code128      | ~100 chars     | General‑purpose tagging | Small |
| QR Code      | ~4 000 chars   | Mobile scanning, rich data | Medium |
| Code39       | ~43 chars      | Legacy hardware | Large |
| Data Matrix  | ~3 000 chars   | Tiny spaces, industrial tags | Very small |

## Masalah Umum & Solusi

### Masalah: “Barcode Tidak Ditemukan Saat Verifikasi”

**Gejala:** Verifikasi mengembalikan `false` meskipun barcode terlihat.

**Penyebab umum**
1. Ketidaksesuaian huruf besar/kecil (misalnya “John Smith” vs. “john smith”).  
2. Spasi ekstra dalam teks yang dikodekan.  
3. Tipe barcode yang salah ditentukan dalam opsi verifikasi.  
4. Mencari pada nomor halaman yang salah.

**Solusi:** Normalisasi teks sebelum menandatangani dan verifikasi, serta pastikan `setEncodeType` cocok dengan tipe asli.

```java
// Always normalize your data
String signatureText = originalText.trim().toLowerCase();

// When signing:
BarcodeSignOptions signOptions = new BarcodeSignOptions(signatureText, BarcodeTypes.Code128);

// When verifying:
BarcodeVerifyOptions verifyOptions = new BarcodeVerifyOptions();
verifyOptions.setText(signatureText); // Use the same normalized text
verifyOptions.setEncodeType(BarcodeTypes.Code128);
```

### Masalah: “Barcode Tampak Kabur atau Tidak Dapat Dibaca”

**Gejala:** Barcode yang dicetak tidak dapat dipindai.

**Penyebab**
- Ukuran barcode terlalu kecil untuk data yang dikodekan.  
- Pengaturan printer beresolusi rendah.  
- Kontras yang tidak cukup antara warna barcode dan latar belakang.

**Solusi:** Tingkatkan lebar/tinggi barcode, gunakan warna kontras tinggi (hitam pada putih), dan atur DPI printer minimal 300 dpi.

```java
// Increase size for longer strings
int dataLength = barcodeText.length();
int minWidth = Math.max(100, dataLength * 10); // 10px per character minimum

BarcodeSignOptions signOptions = new BarcodeSignOptions(barcodeText, BarcodeTypes.Code128);
signOptions.setWidth(minWidth);
signOptions.setHeight(60); // Taller = easier to scan

// Use high-contrast colors
signOptions.setForeColor(Color.BLACK); // Black on white is most reliable
signOptions.setBackColor(Color.WHITE);
```

### Masalah: “OutOfMemoryError dengan Dokumen Besar”

**Gejala:** Aplikasi crash saat memproses PDF dengan ratusan halaman.

**Penyebab:** Pustaka memuat seluruh dokumen ke memori.

**Solusi:** Aktifkan mode streaming dan proses halaman secara bertahap.

```java
// Process pages in batches instead of all at once
BarcodeSearchOptions searchOptions = new BarcodeSearchOptions();
searchOptions.setAllPages(false);

List<BarcodeSignature> allSignatures = new ArrayList<>();

for (int page = 1; page <= totalPages; page++) {
    searchOptions.setPageNumber(page);
    List<BarcodeSignature> pageSignatures = signature.search(BarcodeSignature.class, searchOptions);
    allSignatures.addAll(pageSignatures);
    
    // Process and clear as you go
    if (page % 10 == 0) {
        System.gc(); // Suggest garbage collection every 10 pages
    }
}
```

### Masalah: “Posisi Signature Tidak Konsisten Antara Tipe Dokumen”

**Gejala:** Barcode muncul di lokasi berbeda saat menandatangani PDF vs. dokumen Word.

**Penyebab:** PDF menggunakan asal kiri‑bawah, sementara Word menggunakan asal kiri‑atas.

**Solusi:** Deteksi tipe dokumen dan terapkan transformasi koordinat yang sesuai.

```java
// Use relative positioning instead of absolute
signOptions.setVerticalAlignment(VerticalAlignment.Bottom);
signOptions.setHorizontalAlignment(HorizontalAlignment.Right);

// Then use margins for fine-tuning
Padding margin = new Padding();
margin.setRight(50); // 50px from right edge
margin.setBottom(50); // 50px from bottom
signOptions.setMargin(margin);

// This works consistently across PDF, DOCX, XLSX, etc.
```

### Masalah: “Signature yang Diperbarui Kehilangan Format”

**Gejala:** Setelah memanggil `update`, warna atau font barcode berubah secara tak terduga.

**Penyebab:** Tidak semua properti visual dipertahankan selama operasi pembaruan.

**Solusi:** Terapkan kembali pengaturan visual setelah pemanggilan `update`.

```java
// When updating, explicitly set all visual properties
bcSignature.setLeft(newLeft);
bcSignature.setTop(newTop);
bcSignature.setWidth(originalWidth); // Don't forget these!
bcSignature.setHeight(originalHeight);
// Note: Color and font can't be updated - you'd need to delete and re-sign
```

## Praktik Terbaik untuk Produksi

### Optimasi Kinerja

- **Gunakan Kembali Instance Signature** – Buat satu objek `Signature` per dokumen dan gunakan kembali untuk beberapa operasi.

```java
// Bad - Creates new instance each time
public void processDocument(String path) {
    Signature sig1 = new Signature(path);
    sig1.search(/* ... */);
    
    Signature sig2 = new Signature(path); // Unnecessary reload
    sig2.verify(/* ... */);
}

// Good - Reuse the same instance
public void processDocument(String path) {
    try (Signature signature = new Signature(path)) {
        signature.search(/* ... */);
        signature.verify(/* ... */);
        signature.update(/* ... */);
    }
}
```

- **Cari Hanya Halaman Tertentu** – Batasi rentang halaman ke tempat barcode diharapkan.

```java
// Slow for 100+ page documents
BarcodeSearchOptions slowSearch = new BarcodeSearchOptions();
slowSearch.setAllPages(true);

// Fast - only check where signatures actually are
BarcodeSearchOptions fastSearch = new BarcodeSearchOptions();
fastSearch.setAllPages(false);
fastSearch.setPageNumber(1); // Only check cover page
```

- **Pilih Tipe Barcode Paling Sederhana** – Barcode yang lebih sederhana menghasilkan lebih cepat; gunakan QR atau Data Matrix hanya ketika Anda benar-benar membutuhkan kapasitas tambahan.

```java
// Overkill for simple IDs
BarcodeSignOptions slow = new BarcodeSignOptions("12345", BarcodeTypes.QR);

// Faster and more appropriate
BarcodeSignOptions fast = new BarcodeSignOptions("12345", BarcodeTypes.Code128);
```

### Pertimbangan Keamanan

- **Jangan Pernah Mengkodekan Data Pribadi Sensitif** – Barcode mudah dibaca; hindari PII seperti SSN atau kata sandi.

```java
// Bad - exposes sensitive data
String barcodeData = "SSN:123-45-6789|Password:hunter2";

// Good - use reference IDs
String barcodeData = "USER-REF-7721X"; // Look up sensitive data server-side
```

- **Validasi di Server‑Side** – Jangan pernah mempercayai verifikasi sisi klien saja; selalu verifikasi kembali di backend yang terpercaya.

```java
// Client scans barcode and extracts "APPROVED-BY-ADMIN"
// Always verify server-side:
public boolean verifyApproval(String documentId, String scannedData) {
    // Load document from secure storage
    Signature signature = new Signature(getSecureDocument(documentId));
    
    BarcodeVerifyOptions verifyOptions = new BarcodeVerifyOptions();
    verifyOptions.setText(scannedData);
    
    boolean isValid = signature.verify(verifyOptions) != null;
    
    // Also check against your database
    boolean isInDatabase = checkApprovalDatabase(documentId, scannedData);
    
    return isValid && isInDatabase;
}
```

- **Tambahkan Timestamp** – Sertakan timestamp dalam payload barcode untuk mencegah serangan replay.

```java
import java.time.LocalDateTime;
import java.time.temporal.ChronoUnit;

String timestamp = LocalDateTime.now().truncatedTo(ChronoUnit.SECONDS).toString();
String barcodeData = "APPROVAL|" + userId + "|" + timestamp;

// When verifying, check the timestamp isn't too old
public boolean isSignatureRecent(String barcodeData, int maxAgeHours) {
    String[] parts = barcodeData.split("\\|");
    if (parts.length < 3) return false;
    
    LocalDateTime signatureTime = LocalDateTime.parse(parts[2]);
    LocalDateTime now = LocalDateTime.now();
    
    long hoursSince = ChronoUnit.HOURS.between(signatureTime, now);
    return hoursSince <= maxAgeHours;
}
```

### Pola Penanganan Kesalahan

- **Selalu Gunakan Try‑With‑Resources** untuk memastikan objek `Signature` dibuang.

```java
try (Signature signature = new Signature(documentPath)) {
    // Your operations here
    signature.sign(outputPath, signOptions);
} catch (Exception e) {
    logger.error("Failed to sign document: " + documentPath, e);
    throw new DocumentSigningException("Could not process document", e);
}
```

- **Validasi Akses File** sebelum mencoba menandatangani.

```java
public void signDocument(String inputPath, String outputPath) {
    File inputFile = new File(inputPath);
    
    if (!inputFile.exists()) {
        throw new IllegalArgumentException("Input file not found: " + inputPath);
    }
    
    if (!inputFile.canRead()) {
        throw new SecurityException("Cannot read input file: " + inputPath);
    }
    
    File outputDir = new File(outputPath).getParentFile();
    if (outputDir != null && !outputDir.exists()) {
        outputDir.mkdirs();
    }
    
    try (Signature signature = new Signature(inputPath)) {
        signature.sign(outputPath, signOptions);
    }
}
```

- **Sinkronkan Akses** jika beberapa thread mungkin bekerja pada file yang sama.

```java
import java.util.concurrent.locks.ReentrantLock;
import java.util.concurrent.ConcurrentHashMap;

public class SignatureManager {
    private final ConcurrentHashMap<String, ReentrantLock> documentLocks = new ConcurrentHashMap<>();
    
    public void signDocument(String documentPath, BarcodeSignOptions options) {
        ReentrantLock lock = documentLocks.computeIfAbsent(documentPath, k -> new ReentrantLock());
        
        lock.lock();
        try (Signature signature = new Signature(documentPath)) {
            signature.sign(documentPath + ".signed", options);
        } finally {
            lock.unlock();
        }
    }
}
```

### Menguji Implementasi Anda

**Templat Unit Test**

```java
import org.junit.jupiter.api.Test;
import org.junit.jupiter.api.io.TempDir;
import static org.junit.jupiter.api.Assertions.*;

public class BarcodeSignatureTest {
    
    @TempDir
    Path tempDir;
    
    @Test
    public void testSignAndVerify() throws Exception {
        // Setup
        String testDoc = "test-document.pdf";
        String outputDoc = tempDir.resolve("signed-test.pdf").toString();
        String testData = "TEST-USER-12345";
        
        // Sign
        try (Signature signature = new Signature(testDoc)) {
            BarcodeSignOptions signOptions = new BarcodeSignOptions(testData, BarcodeTypes.Code128);
            signature.sign(outputDoc, signOptions);
        }
        
        // Verify
        try (Signature signature = new Signature(outputDoc)) {
            BarcodeVerifyOptions verifyOptions = new BarcodeVerifyOptions();
            verifyOptions.setText(testData);
            verifyOptions.setEncodeType(BarcodeTypes.Code128);
            
            boolean isValid = signature.verify(verifyOptions) != null;
            assertTrue(isValid, "Signature should be valid");
        }
    }
    
    @Test
    public void testSearchFindsSignature() throws Exception {
        String signedDoc = "signed-document.pdf";
        
        try (Signature signature = new Signature(signedDoc)) {
            BarcodeSearchOptions searchOptions = new BarcodeSearchOptions();
            searchOptions.setAllPages(true);
            
            List<BarcodeSignature> signatures = signature.search(BarcodeSignature.class, searchOptions);
            
            assertFalse(signatures.isEmpty(), "Should find at least one signature");
            assertEquals("TEST-USER-12345", signatures.get(0).getText());
        }
    }
}
```

**Daftar Periksa Integrasi**

- ✅ Uji semua format yang didukung (PDF, DOCX, XLSX, PPTX, PNG).  
- ✅ Verifikasi barcode bertahan setelah siklus cetak‑scan.  
- ✅ Lakukan stress‑test dengan string data panjang maksimum.  
- ✅ Pastikan penempatan pada ukuran halaman A4, Letter, dan ukuran kustom.  
- ✅ Jalankan penandatanganan bersamaan pada beberapa dokumen.  
- ✅ Pantau penggunaan memori untuk dokumen > 500 halaman.  
- ✅ Pastikan pemindai barcode membaca output dengan andal.

### Logging dan Monitoring

Tambahkan log yang bermakna di sekitar setiap operasi:

```java
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

public class DocumentSigningService {
    private static final Logger logger = LoggerFactory.getLogger(DocumentSigningService.class);
    
    public void signDocument(String docPath, String barcodeData) {
        logger.info("Starting signature process for document: {}", docPath);
        logger.debug("Barcode data length: {} characters", barcodeData.length());
        
        try (Signature signature = new Signature(docPath)) {
            BarcodeSignOptions options = new BarcodeSignOptions(barcodeData, BarcodeTypes.Code128);
            
            long startTime = System.currentTimeMillis();
            signature.sign(docPath + ".signed", options);
            long duration = System.currentTimeMillis() - startTime;
            
            logger.info("Successfully signed document in {}ms", duration);
        } catch (Exception e) {
            logger.error("Failed to sign document: {}", docPath, e);
            throw new RuntimeException("Signature operation failed", e);
        }
    }
}
```

Lacak metrik utama seperti waktu pemrosesan, konsumsi memori, dan tingkat error:

```java
// Track success/failure rates
metricsService.incrementCounter("signature.sign.success");
metricsService.incrementCounter("signature.verify.failure");

// Track performance
metricsService.recordTimer("signature.sign.duration", duration);

// Track document sizes
metricsService.recordHistogram("signature.document.pages", pageCount);
```

## Tips Pro dari Penggunaan Dunia Nyata

### Strategi Pemrosesan Batch

Saat menangani ratusan file, proses dalam batch dan laporkan kemajuan:

```java
public void signBatch(List<String> documents, String barcodePrefix) {
    int total = documents.size();
    int completed = 0;
    int failed = 0;
    
    for (String docPath : documents) {
        try {
            String barcodeData = barcodePrefix + "-" + UUID.randomUUID().toString();
            signDocument(docPath, barcodeData);
            completed++;
            
            if (completed % 10 == 0) {
                logger.info("Progress: {}/{} documents signed", completed, total);
            }
        } catch (Exception e) {
            failed++;
            logger.warn("Failed to sign: {}", docPath, e);
        }
    }
    
    logger.info("Batch complete: {} succeeded, {} failed", completed, failed);
}
```

### Eksternalisasi Konfigurasi

Simpan pengaturan barcode (tipe, ukuran, warna) dalam file properti untuk penyesuaian mudah tanpa kompilasi ulang:

```java
public class BarcodeConfig {
    private int defaultWidth = 100;
    private int defaultHeight = 40;
    private String defaultBarcodeType = "Code128";
    private String defaultColor = "BLACK";
    
    // Load from properties file or environment variables
    public BarcodeConfig() {
        this.defaultWidth = Integer.parseInt(
            System.getProperty("barcode.width", "100")
        );
        // ... load other properties
    }
    
    public BarcodeSignOptions createDefaultOptions(String text) {
        BarcodeSignOptions options = new BarcodeSignOptions(text, getBarcodeType());
        options.setWidth(defaultWidth);
        options.setHeight(defaultHeight);
        options.setForeColor(getColor());
        return options;
    }
}
```

### Standarisasi Payload Barcode

Gunakan format terdelimitasi seperti `EMPID|TIMESTAMP|DOCID` untuk mempermudah dan konsisten dalam parsing:

```java
public class BarcodeDataBuilder {
    private String userId;
    private String action;
    private LocalDateTime timestamp;
    private String documentId;
    
    public BarcodeDataBuilder setUserId(String userId) {
        this.userId = userId;
        return this;
    }
    
    public BarcodeDataBuilder setAction(String action) {
        this.action = action;
        return this;
    }
    
    public BarcodeDataBuilder setDocumentId(String documentId) {
        this.documentId = documentId;
        return this;
    }
    
    public String build() {
        this.timestamp = LocalDateTime.now();
        
        // Format: VERSION|USER|ACTION|DOC_ID|TIMESTAMP|CHECKSUM
        String data = String.join("|",
            "v1",
            userId,
            action,
            documentId,
            timestamp.toString()
        );
        
        // Add simple checksum
        int checksum = data.hashCode();
        return data + "|" + checksum;
    }
    
    public static ParsedBarcodeData parse(String barcodeData) {
        String[] parts = barcodeData.split("\\|");
        if (parts.length != 6 || !parts[0].equals("v1")) {
            throw new IllegalArgumentException("Invalid barcode format");
        }
        
        return new ParsedBarcodeData(parts[1], parts[2], parts[3], 
                                     LocalDateTime.parse(parts[4]));
    }
}

// Usage:
String barcodeData = new BarcodeDataBuilder()
    .setUserId("john.smith")
    .setAction("APPROVED")
    .setDocumentId("INV-2025-042")
    .build();
```

### Deteksi Tipe Dokumen Secara Otomatis

Sesuaikan dimensi barcode berdasarkan apakah targetnya PDF, Word, atau gambar:

```java
public BarcodeSignOptions getOptimalOptions(String documentPath, String text) {
    String extension = documentPath.substring(documentPath.lastIndexOf(".") + 1).toLowerCase();
    
    BarcodeSignOptions options = new BarcodeSignOptions(text, BarcodeTypes.Code128);
    
    switch (extension) {
        case "pdf":
            // PDFs can handle larger, detailed barcodes
            options.setWidth(150);
            options.setHeight(50);
            break;
        case "docx":
        case "doc":
            // Word docs need compact signatures that don't disrupt flow
            options.setWidth(100);
            options.setHeight(35);
            options.setVerticalAlignment(VerticalAlignment.Bottom);
            break;
        case "xlsx":
        case "xls":
            // Excel needs signatures that don't obscure data
            options.setWidth(80);
            options.setHeight(30);
            options.setHorizontalAlignment(HorizontalAlignment.Right);
            break;
        default:
            // Safe defaults
            options.setWidth(100);
            options.setHeight(40);
    }
    
    return options;
}
```

## Sumber Daya Tambahan

- [GroupDocs.Signature documentation](https://docs.groupdocs.com/signature/java/) – Panduan API lengkap dan contoh penggunaan.  
- [GroupDocs support forum](https://forum.groupdocs.com/c/signature/13) – Bantuan komunitas dan pemecahan masalah.  
- [API reference](https://apireference.groupdocs.com/signature/java) – Deskripsi detail tanda tangan metode dan parameter.

## Pertanyaan yang Sering Diajukan

- **Q: Bisakah saya menggunakan GroupDocs.Signature dengan Java 17?**  
  A: Ya – pustaka sepenuhnya kompatibel dengan JDK 8, 11, dan 17.  

- **Q: Apakah barcode bertahan setelah siklus cetak‑scan?**  
  A: Ketika Anda menggunakan Code128 atau QR dengan ukuran dan kontras yang cukup, barcode tetap dapat dipindai setelah pencetakan dan pemindaian.  

- **Q: Berapa banyak barcode yang dapat dimuat dalam satu dokumen?**  
  A: Tidak ada batas keras; namun, untuk kinerja optimal, jaga total jumlah di bawah **200** per dokumen.  

- **Q: Apakah lisensi diperlukan untuk build pengembangan?**  
  A: Lisensi sementara menghapus watermark evaluasi; lisensi penuh wajib untuk setiap penerapan produksi.  

- **Q: Bisakah saya menandatangani PDF yang dilindungi kata sandi?**  
  A: Ya – berikan kata sandi saat membuat objek `Signature`; API akan membuka file secara internal.  

---

**Terakhir Diperbarui:** 2026-07-15  
**Diuji Dengan:** GroupDocs.Signature 23.9 untuk Java  
**Penulis:** GroupDocs  

{< /blocks/products/pf/tutorial-page-section >}
{< /blocks/products/pf/main-container >}
{< /blocks/products/pf/main-wrap-class >}
{< blocks/products/products-backtop-button >}

## Tutorial Terkait

- [Cara Memverifikasi Tanda Barcode di Java dengan GroupDocs.Signature](/signature/java/search-verification/groupdocs-signature-java-document-verification/)
- [Cara Mencari Tanda Digital di Dokumen Java dengan GroupDocs](/signature/java/search-verification/groupdocs-signature-java-digital-search-tutorial/)
- [Tutorial Tanda Barcode Java - Tambah, Verifikasi & Kelola Barcode di PDF](/signature/java/barcode-signatures/)