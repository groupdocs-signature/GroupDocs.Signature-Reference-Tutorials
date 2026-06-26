---
categories:
- Java PDF Processing
date: '2026-06-26'
description: Pelajari cara menandatangani file PDF di Java menggunakan GroupDocs.Signature.
  Panduan langkah demi langkah dengan kode, pemecahan masalah, praktik terbaik keamanan,
  dan contoh penggunaan dunia nyata.
keywords:
- how to sign pdf
- digital signature pdf java
- java pdf digital signature
- use pfx certificate java
lastmod: '2026-06-26'
linktitle: Tanda Tangan Digital PDF Java
schemas:
- author: GroupDocs
  dateModified: '2026-06-26'
  description: Learn how to sign PDF files in Java using GroupDocs.Signature. Step‑by‑step
    guide with code, troubleshooting, security best practices, and real‑world use
    cases.
  headline: How to Sign PDF in Java with GroupDocs
  type: TechArticle
- description: Learn how to sign PDF files in Java using GroupDocs.Signature. Step‑by‑step
    guide with code, troubleshooting, security best practices, and real‑world use
    cases.
  name: How to Sign PDF in Java with GroupDocs
  steps:
  - name: '**Free trial** – perfect for evaluation. [Grab it here](https://releases.groupdocs.com/signature/java/)'
    text: '**Free trial** – perfect for evaluation. [Grab it here](https://releases.groupdocs.com/signature/java/)'
  - name: '**Temporary license** – extended evaluation period. [Request one](https://purchase.groupdocs.com/temporary-license/)'
    text: '**Temporary license** – extended evaluation period. [Request one](https://purchase.groupdocs.com/temporary-license/)'
  - name: '**Full license** – production‑ready. [Purchase here](https://purchase.groupdocs.com/buy)'
    text: '**Full license** – production‑ready. [Purchase here](https://purchase.groupdocs.com/buy)'
  type: HowTo
- questions:
  - answer: No. The free trial is for evaluation only. Production deployments require
      a purchased license.
    question: Can I use GroupDocs.Signature for free in production?
  - answer: A digital signature uses cryptographic certificates to guarantee authenticity
      and detect tampering, while an electronic signature is merely a digital representation
      of a handwritten mark.
    question: What’s the difference between a digital signature and an electronic
      signature?
  - answer: 'Yes—provide the PDF password when opening the document:'
    question: Can I sign password‑protected PDFs?
  - answer: Call `sign` repeatedly with different `DigitalSignOptions` or pass an
      array of options to sign sequentially.
    question: How do I apply multiple signatures to one PDF?
  - answer: Absolutely. GroupDocs.Signature creates ISO‑standard signatures that render
      correctly in Adobe Reader, iOS Preview, and Android PDF viewers.
    question: Will the signatures work on mobile PDF readers?
  type: FAQPage
tags:
- digital-signatures
- pdf-security
- groupdocs
- java-tutorial
title: Cara Menandatangani PDF di Java dengan GroupDocs
type: docs
url: /id/java/digital-signatures/implement-digital-signatures-pdf-groupdocs-java/
weight: 1
---

# Cara Menandatangani PDF di Java dengan GroupDocs

## Pendahuluan

Jika Anda perlu **how to sign pdf** file secara programatis dalam aplikasi Java, Anda berada di tempat yang tepat. Bayangkan sistem manajemen kontrak perusahaan yang harus melampirkan tanda tangan yang sah secara hukum pada setiap PDF sebelum dikirim ke klien. Tanpa solusi penandatanganan yang dapat diandalkan, Anda berisiko tidak mematuhi regulasi, manipulasi, dan pekerjaan manual yang tak berujung.

Dalam tutorial ini Anda akan mempelajari cara menambahkan tanda tangan digital ke file PDF di Java menggunakan **GroupDocs.Signature**. Kami akan membahas semuanya mulai dari penyiapan lingkungan hingga menyesuaikan tampilan tanda tangan yang terlihat, menangani dokumen besar, dan menerapkan praktik keamanan tingkat produksi.

Pada akhir panduan ini Anda akan dapat:

* Menginstal dan mengkonfigurasi GroupDocs.Signature untuk Java.
* Menginisialisasi objek `Signature` dan memuat PDF.
* Mengkonfigurasi `DigitalSignOptions` dengan sertifikat .pfx.
* Menyesuaikan tampilan, posisi, dan border tanda tangan.
* Menandatangani dokumen, memverifikasi hasil, dan menangani jebakan umum.

Mari kita mulai dan membuat PDF Anda tahan manipulasi.

## Jawaban Cepat
- **Apa perpustakaan yang menandatangani PDF di Java?** GroupDocs.Signature untuk Java.  
- **Format sertifikat apa yang diperlukan?** File PKCS#12 (.pfx) yang berisi kunci pribadi.  
- **Bisakah saya menandatangani semua halaman sekaligus?** Ya—atur `allPages(true)` dalam opsi.  
- **Bagaimana cara menambahkan timestamp?** Konfigurasikan `options.setTimestampOptions(...)` dengan URL TSA tepercaya.  
- **Versi Java apa yang didukung?** JDK 8 atau lebih tinggi; JDK 11 disarankan untuk produksi.

## Apa itu “how to sign pdf”?
**how to sign pdf** mengacu pada proses penerapan tanda tangan digital yang aman secara kriptografis pada dokumen PDF sehingga integritas dan kepenulisan dapat diverifikasi. GroupDocs.Signature mengimplementasikan standar PDF ISO 32000‑1, memastikan tanda tangan dikenali oleh Adobe Acrobat dan pembaca lainnya.

## Mengapa menggunakan GroupDocs.Signature untuk Java?
GroupDocs.Signature mendukung **50+** format input dan output, dapat memproses PDF dengan **500+ halaman** tanpa memuat seluruh file ke memori, dan menawarkan timestamp bawaan. API-nya memungkinkan Anda membuat blok tanda tangan yang tampak profesional hanya dengan beberapa baris kode, secara dramatis mengurangi upaya pengembangan dibandingkan dengan perpustakaan PDF tingkat rendah.

## Prasyarat

- **Pengetahuan Java** – pemahaman dasar tentang kelas, objek, dan Maven/Gradle.
- **IDE** – IntelliJ IDEA, Eclipse, atau editor kompatibel Java apa pun.
- **Alat build** – Maven **atau** Gradle (kedua-duanya dibahas).
- **Sertifikat digital** – file .pfx (self‑signed untuk pengujian, diterbitkan CA untuk produksi).
- **JDK** – versi 8 atau lebih baru; JDK 11 atau lebih baru disarankan untuk kinerja optimal.

### Tentang sertifikat digital
Sertifikat digital adalah kartu identitas elektronik Anda. Untuk penggunaan produksi dapatkan satu dari Otoritas Sertifikat (CA) tepercaya seperti DigiCert atau GlobalSign. Untuk pengembangan Anda dapat membuat sertifikat self‑signed dengan `keytool` (lihat bagian “Pengembangan/Pengujian” nanti).

## Menyiapkan GroupDocs.Signature untuk Java

### Instalasi dengan Maven

Tambahkan dependensi berikut ke `pom.xml` Anda:

```xml
<!-- ```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
``` -->
```

**Mengapa versi 23.12?** Ini adalah rilis stabil yang mencakup semua fitur penandatanganan PDF dan telah diuji secara intensif di lingkungan perusahaan. Versi yang lebih baru kompatibel ke depan, tetapi 23.12 menjamin permukaan API yang digunakan dalam tutorial ini.

### Instalasi dengan Gradle

Jika Anda lebih suka Gradle, sisipkan baris ini ke dalam `build.gradle`:

```groovy
// ```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```
```

Setelah mengedit, sinkronkan proyek untuk mengunduh perpustakaan—melewatkan langkah ini adalah penyebab umum error “class not found”.

### Mengatur Lisensi Anda

GroupDocs.Signature adalah produk komersial. Pilih opsi yang sesuai dengan jadwal Anda:

1. **Uji coba gratis** – sempurna untuk evaluasi. [Grab it here](https://releases.groupdocs.com/signature/java/)
2. **Lisensi sementara** – periode evaluasi yang diperpanjang. [Request one](https://purchase.groupdocs.com/temporary-license/)
3. **Lisensi penuh** – siap produksi. [Purchase here](https://purchase.groupdocs.com/buy)

Uji coba gratis sudah cukup untuk mengikuti tutorial ini.

## Cara Menandatangani PDF secara Programatis di Java: Implementasi Langkah‑per‑Langkah

Di bawah ini kami membagi implementasi menjadi bagian‑bagian terfokus dengan gaya pertanyaan. Setiap bagian dimulai dengan jawaban langsung yang singkat (40‑70 kata) diikuti oleh penjelasan dan placeholder kode yang relevan.

### Bagaimana cara menginisialisasi objek Signature?

Buat instance `Signature` yang membungkus file PDF target; ini memuat dokumen ke memori dan menyiapkannya untuk penandatanganan.

```java
// ```java
Signature signature = new Signature("YOUR_DOCUMENT_DIRECTORY/samplePdf.pdf");
```
```

*Definition anchor:* Kelas `Signature` adalah titik masuk GroupDocs.Signature untuk memuat, memodifikasi, dan menyimpan file PDF.

### Bagaimana cara mengkonfigurasi opsi tanda tangan digital?

Atur jalur sertifikat, kata sandi, alasan, dan lokasi. Nilai‑nilai ini menjadi bagian dari tanda tangan kriptografis dan ditampilkan di pembaca PDF.

```java
// ```java
DigitalSignOptions options = new DigitalSignOptions("YOUR_DOCUMENT_DIRECTORY/certificate.pfx");
options.setPassword("1234567890"); // Your certificate's password
options.setReason("Approved"); // Why you're signing (appears in PDF metadata)
options.setLocation("New York"); // Where the signing occurred
```
```

*Definition anchor:* `DigitalSignOptions` mengenkapsulasi semua parameter yang diperlukan untuk tanda tangan digital, termasuk tampilan visual dan pengaturan kriptografis.

### Bagaimana cara menyesuaikan tampilan tanda tangan?

Sesuaikan label, simbol, warna latar belakang, dan font agar sesuai dengan merek perusahaan atau pedoman kepatuhan.

```java
// ```java
PdfDigitalSignatureAppearance appearance = new PdfDigitalSignatureAppearance();
appearance.setContactInfoLabel("");
appearance.setReasonLabel("R:");
appearance.setLocationLabel("@⇒");
appearance.setDigitalSignedLabel("By:");
appearance.setDateSignedAtLabel("On");
appearance.setBackground(java.awt.Color.red);
appearance.setFontFamilyName("Courier");
appearance.setFontSize(8);

options.setAppearance(appearance);
```
```

*Definition anchor:* `SignatureAppearance` mendefinisikan representasi visual dari blok tanda tangan yang dilihat pengguna akhir di PDF.

### Bagaimana cara memposisikan dan mengatur ukuran blok tanda tangan?

Tentukan pemilihan halaman, dimensi, perataan, dan padding untuk mengontrol secara tepat di mana tanda tangan ditempatkan.

```java
// ```java
options.setAllPages(true); // Apply to all pages
options.setWidth(160); // Width in pixels
options.setHeight(80); // Height in pixels
options.setVerticalAlignment(VerticalAlignment.Center);
options.setHorizontalAlignment(HorizontalAlignment.Left);
options.setMargin(new Padding(0, 10, 0, 10)); // Top, Right, Bottom, Left margins
```
```

*Definition anchor:* `SignatureOptions` (atau subclassnya) mengontrol penempatan, ukuran, dan ruang lingkup halaman untuk tanda tangan yang terlihat.

### Bagaimana cara menambahkan border terlihat di sekitar tanda tangan?

Border membuat tanda tangan menonjol dan memberi sinyal kepada peninjau di mana area penandatanganan berada.

```java
// ```java
Border border = new Border();
border.setVisible(true);
border.setColor(java.awt.Color.red);
border.setDashStyle(DashStyle.DashDot);
border.setWeight(2); // Thickness in pixels
options.setBorder(border);
```
```

*Definition anchor:* `Border` mengkonfigurasi gaya garis, ketebalan, dan visibilitas untuk bingkai tanda tangan.

### Bagaimana cara menandatangani dokumen dan menyimpan hasilnya?

Panggil `sign` dengan opsi yang dikonfigurasi; metode ini mengembalikan `SignResult` yang menunjukkan keberhasilan dan peringatan apa pun.

```java
// ```java
SignResult signResult = signature.sign("YOUR_OUTPUT_DIRECTORY/digitallySignedPdfAppearance.pdf", options);
```
```

*Definition anchor:* `SignResult` memberikan detail tentang operasi penandatanganan, termasuk jumlah halaman yang berhasil ditandatangani.

### Bagaimana cara memverifikasi operasi penandatanganan berhasil?

Periksa objek `SignResult`; jika `isSuccessful()` mengembalikan `true`, PDF kini berisi tanda tangan digital yang valid.

```java
// ```java
if (signResult.getSucceeded().size() > 0) {
    System.out.println("Document signed successfully!");
} else {
    System.err.println("Signing failed: " + signResult.getFailed());
}
```
```

## Kesalahan Umum dan Cara Menghindarinya

### Masalah 1: Error “Certificate Not Found”

**Jawaban langsung:** Pastikan jalur file .pfx bersifat absolut selama pengembangan dan simpan sertifikat di luar folder aplikasi di produksi, merujuknya melalui variabel lingkungan.

```java
// ```java
String certPath = System.getenv("CERTIFICATE_PATH");
DigitalSignOptions options = new DigitalSignOptions(certPath);
```
```

### Masalah 2: Pengecualian Password Tidak Valid

**Jawaban langsung:** Verifikasi kata sandi cocok dengan yang digunakan saat sertifikat dibuat; kata sandi bersifat case‑sensitive dan sebaiknya diambil dari vault yang aman, bukan ditulis keras.

```java
// ```java
// Good practice
DigitalSignOptions options = new DigitalSignOptions("cert.pfx");
signature.sign("output.pdf", options);

// Later, for a different document
DigitalSignOptions newOptions = new DigitalSignOptions("cert.pfx"); // Fresh object
signature.sign("output2.pdf", newOptions);
```
```

### Masalah 3: Tanda Tangan Muncul di Halaman yang Salah

**Jawaban langsung:** Buat instance `DigitalSignOptions` baru untuk setiap operasi penandatanganan; menggunakan kembali objek yang sama dapat menyebabkan pengaturan halaman lama tetap berlaku.

```java
// ```java
options.setWidth(320); // Instead of 160
options.setHeight(160); // Instead of 80
```
```

### Masalah 4: Rendering Tanda Tangan Buram

**Jawaban langsung:** Tingkatkan dimensi piksel blok tanda tangan (mis., lebar = 320, tinggi = 160) untuk mencapai rendering 300 DPI yang cocok untuk cetak.

```java
// ```bash
java -Xmx2G -jar your-application.jar
```
```

### Masalah 5: OutOfMemoryError dengan PDF Besar

**Jawaban langsung:** Alokasikan lebih banyak memori heap (`-Xmx2g`) dan tutup objek `Signature` setelah digunakan; objek ini mengimplementasikan `AutoCloseable` untuk membebaskan sumber daya native.

```java
// ```java
try (Signature signature = new Signature("document.pdf")) {
    signature.sign("signed.pdf", options);
} // Automatically releases resources
```
```

## Praktik Keamanan Terbaik untuk Penggunaan Produksi

### Jangan pernah menulis keras kata sandi sertifikat

Simpan mereka di manajer rahasia (AWS Secrets Manager, Azure Key Vault, HashiCorp Vault) dan muat saat runtime.

```java
// ```java
// BAD - Don't do this
options.setPassword("1234567890");

// GOOD - Load from environment or vault
String password = System.getenv("CERT_PASSWORD");
options.setPassword(password);
```
```

### Batasi izin file sertifikat

Di Linux, atur izin menjadi `400` (hanya baca untuk pemilik) untuk mencegah akses tidak sah.

```java
// ```bash
chmod 400 /secure/certificates/signing-cert.pfx
```
```

### Gunakan timestamping untuk keabsahan jangka panjang

Tambahkan server Timestamp Authority (TSA) tepercaya sehingga tanda tangan tetap valid setelah sertifikat penandatangan kedaluwarsa.

```java
// ```java
options.setTimestampUrl("http://timestamp.digicert.com");
```
```

### Validasi tanda tangan setelah penandatanganan

Jalankan proses verifikasi untuk memastikan tanda tangan tertanam dengan benar dan dapat dikenali oleh pembaca PDF.

```java
// ```java
SignResult result = signature.sign("output.pdf", options);
if (result.getSucceeded().size() > 0) {
    // Verify the signature
    VerifyResult verifyResult = signature.verify();
    if (!verifyResult.isValid()) {
        throw new SecurityException("Signature verification failed!");
    }
}
```
```

### Catat setiap operasi penandatanganan

Pertahankan jejak audit dengan detail seperti ID pengguna, ID dokumen, timestamp, dan thumbprint sertifikat penandatangan.

```java
// ```java
logger.info("Document signed: {}, User: {}, Timestamp: {}", 
    documentName, currentUser, LocalDateTime.now());
```
```

## Memilih Sertifikat yang Tepat untuk Kasus Penggunaan Anda

### Pengembangan / Pengujian – Self‑Signed

Buat dengan cepat menggunakan `keytool` Java; cocok untuk demo internal tetapi **tidak** untuk dokumen yang mengikat secara hukum.

```java
// ```bash
keytool -genkeypair -alias testcert -keyalg RSA -keysize 2048 \
  -keystore test.pfx -storetype PKCS12 -validity 365
```
```

### Produksi – CA Komersial

Beli **Certificate Penandatangan Dokumen** (DigiCert, GlobalSign) seharga $70‑$400 per tahun. Sertifikat ini dipercaya oleh semua pembaca PDF utama.

### Perusahaan – CA Internal

Jalankan Otoritas Sertifikat Anda sendiri untuk sertifikat internal tak terbatas. Ingat: CA internal tidak dipercaya di luar organisasi.

## Kasus Penggunaan Dunia Nyata dan Implementasi

### Sistem Manajemen Kontrak
- **Tujuan:** Menandatangani setiap halaman NDA multi‑halaman.  
- **Implementasi:** `allPages(true)`, penempatan kanan‑bawah, server timestamp, pencatatan audit.  
- **Tips kinerja:** Proses kontrak dalam batch paralel menggunakan thread pool berukuran tetap.

### Otomasi Faktur
- **Tujuan:** Menambahkan tanda tangan yang tidak mencolok pada halaman pertama faktur.  
- **Implementasi:** `allPages(false)`, tampilan minimal, tanpa border, gunakan logo perusahaan sebagai gambar latar belakang.

### Sistem Rekam Medis (HIPAA)
- **Tujuan:** Memastikan ringkasan pemulangan pasien ditandatangani oleh dokter yang merawat.  
- **Implementasi:** Sertakan kredensial dokter dalam tampilan tanda tangan, sertifikat CA berjaminan tinggi, kunci pribadi dilindungi dua‑faktor.

### Pemrosesan Dokumen Pemerintah
- **Tujuan:** Menerapkan rangkaian persetujuan (banyak tanda tangan) pada formulir sektor publik.  
- **Implementasi:** Panggil `sign` secara berurutan dengan `DigitalSignOptions` yang berbeda, masing‑masing dengan sertifikat dan timestamp sendiri.

## Tips Optimasi Kinerja

### Gunakan kembali objek Signature untuk pekerjaan batch

```java
// ```java
try (Signature signature = new Signature("template.pdf")) {
    for (Document doc : documents) {
        signature.sign(doc.getOutputPath(), getOptionsForDoc(doc));
    }
}
```
```

### Cache sertifikat yang dimuat

```java
// ```java
// Load certificate once
DigitalSignOptions baseOptions = new DigitalSignOptions("cert.pfx");
baseOptions.setPassword(certPassword);

// Clone for each document
for (Document doc : documents) {
    DigitalSignOptions options = baseOptions.clone();
    options.setReason(doc.getReason());
    signature.sign(doc.getPath(), options);
}
```
```

### Optimalkan JVM untuk throughput tinggi

```java
// ```bash
java -Xmx4G -XX:+UseG1GC -XX:MaxGCPauseMillis=200 -jar app.jar
```
```

### Tanda tangani dokumen secara asynchronous

```java
// ```java
CompletableFuture.supplyAsync(() -> {
    signature.sign(outputPath, options);
    return "Success";
}).thenAccept(result -> notifyUser(result));
```
```

## Panduan Pemecahan Masalah

| Masalah | Pemeriksaan Cepat | Solusi |
|---------|-------------------|--------|
| Tanda tangan tidak terlihat | `border.setVisible(true)`? Lebar/tinggi > 0? Koordinat di luar halaman? | Atur latar belakang terang sementara untuk menemukan blok. |
| “Sertifikat Tidak Valid” | Verifikasi masa berlaku (`keytool -list -v -keystore cert.pfx`). | Gunakan sertifikat yang valid dan belum kedaluwarsa; konversi ke PKCS#12 jika diperlukan. |
| PDF yang ditandatangani tidak dapat dibuka | Ruang disk? Izin file? Kompatibilitas versi PDF? | Jaga file asli tidak berubah; tulis PDF yang ditandatangani ke jalur baru. |

## Pertanyaan yang Sering Diajukan

**Q: Bisakah saya menggunakan GroupDocs.Signature secara gratis di produksi?**  
A: Tidak. Uji coba gratis hanya untuk evaluasi. Deploymen produksi memerlukan lisensi berbayar.

**Q: Apa perbedaan antara tanda tangan digital dan tanda tangan elektronik?**  
A: Tanda tangan digital menggunakan sertifikat kriptografis untuk menjamin keaslian dan mendeteksi manipulasi, sedangkan tanda tangan elektronik hanyalah representasi digital dari goresan tangan.

**Q: Bisakah saya menandatangani PDF yang dilindungi kata sandi?**  
A: Ya—berikan kata sandi PDF saat membuka dokumen:

```java
// ```java
LoadOptions loadOptions = new LoadOptions();
loadOptions.setPassword("pdfPassword");
Signature signature = new Signature("protected.pdf", loadOptions);
```

Anda dapat mengunduh rilis perpustakaan terbaru dari halaman resmi: [Grab it here](https://releases.groupdocs.com/signature/java/).  
Untuk lisensi evaluasi sementara, gunakan formulir permintaan: [Request one](https://purchase.groupdocs.com/temporary-license/).  
Saat Anda siap untuk produksi, beli lisensi penuh: [Purchase here](https://purchase.groupdocs.com/buy) atau [purchase a license](https://purchase.groupdocs.com/buy).

**Q: Bagaimana cara menerapkan beberapa tanda tangan pada satu PDF?**  
A: Panggil `sign` berulang kali dengan `DigitalSignOptions` yang berbeda atau berikan array opsi untuk menandatangani secara berurutan.

**Q: Apakah tanda tangan akan berfungsi pada pembaca PDF seluler?**  
A: Tentu saja. GroupDocs.Signature membuat tanda tangan standar ISO yang ditampilkan dengan benar di Adobe Reader, iOS Preview, dan pembaca PDF Android.

**Q: Berapa lama waktu yang dibutuhkan untuk menandatangani PDF tipikal?**  
A: File 10‑halaman ditandatangani dalam ~200‑500 ms pada CPU modern; file 100‑halaman dengan timestamp dapat memakan 1‑3 detik.

**Q: Apa yang terjadi jika sertifikat saya kedaluwarsa setelah penandatanganan?**  
A: Jika Anda menggunakan server timestamp, tanda tangan tetap valid karena TSA membuktikan waktu penandatanganan terjadi saat sertifikat masih dipercaya.

## Langkah Selanjutnya dan Pembelajaran Lebih Lanjut

- **Verifikasi tanda tangan** – pelajari cara memvalidasi tanda tangan yang ada secara programatis.  
- **Penandatanganan batch** – skalakan ke ribuan dokumen menggunakan pola paralel yang ditunjukkan di atas.  
- **Tanda tangan QR‑code** – sematkan kode yang dapat dipindai untuk verifikasi cepat.  
- **Integrasi** – hubungkan layanan penandatanganan ke SharePoint, Alfresco, atau API REST kustom.

### Sumber Daya Berguna
- **Dokumentasi:** [GroupDocs.Signature Java Docs](https://docs.groupdocs.com/signature/java/) – referensi API lengkap.  
- **Referensi API:** [Java API Reference](https://reference.groupdocs.com/signature/java/) – tanda tangan metode terperinci dan contoh.

---

**Terakhir Diperbarui:** 2026-06-26  
**Diuji Dengan:** GroupDocs.Signature 23.12 untuk Java  
**Penulis:** GroupDocs

## Tutorial Terkait

- [Tanda Tangan Digital di Java - Panduan Lengkap Memuat Sertifikat dan Menandatangani Dokumen](/signature/java/digital-signatures/digital-signature-loading-signing-groupdocs-java/)
- [Cara Menambahkan Tanda Tangan Digital ke PDF Java dengan Timestamp](/signature/java/digital-signatures/digital-signature-timestamp-pdf-java-groupdocs/)
- [Tanda Tangan PDF dari URL Java - Tutorial Lengkap GroupDocs](/signature/java/digital-signatures/sign-pdf-from-url-groupdocs-signature-java/)