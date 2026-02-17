---
categories:
- Java Development
date: '2025-12-31'
description: Pelajari cara menghasilkan tanda tangan kode QR dalam PDF menggunakan
  GroupDocs.Signature untuk Java. Termasuk pengaturan dependensi Maven, penempatan,
  dan tips produksi.
keywords: java generate qr code, groupdocs signature java, maven dependency groupdocs,
  QR code document signing Java, add QR code to PDF Java
lastmod: '2025-12-31'
linktitle: QR Code Signing Java Guide
tags:
- QR codes
- PDF signing
- digital signatures
- document security
title: 'java menghasilkan kode QR - Panduan Penandatanganan Kode QR di Java'
type: docs
url: /id/java/advanced-options/master-groupdocs-signature-java-qr-code-signing/
weight: 1
---

# java generate qr code: Penandatanganan Kode QR di Java – Implementasi Lengkap

Anda mungkin telah memperhatikan bagaimana tanda tangan digital ada di mana-mana sekarang—dari kontrak hingga faktur. Namun faktanya: metode tanda tangan tradisional bisa merepotkan dan tidak selalu menyediakan fitur verifikasi yang dibutuhkan bisnis modern. Di mendapatkan tanda tangan **java generate qr code** berpartisipasi.

Dalam panduan ini, Anda akan mempelajari cara mengimplementasikan penandatanganan kode QR di Java, menempatkan tanda tangan ini tepat di lokasi yang Anda butuhkan, dan menghindari jebakan umum yang sering membuat pengembang terjebak. Baik Anda sedang membangun sistem manajemen kontrak atau hanya perlu mengamankan PDF secara terprogram, tutorial ini akan membantu Anda mencapainya.

Kami akan menggunakan **GroupDocs.Signature for Java** (perpustakaan yang kuat dan menangani pekerjaan berat), namun konsepnya dapat diterapkan secara luas pada implementasi penandatanganan kode QR apa pun.

## Jawaban Singkat
- **Pustaka apa yang menambahkan tanda tangan kode QR di Java?** GroupDocs.Signature untuk Java
- **Alat build mana yang mendukung dependensi Maven?** Maven (lihat *dependensi maven groupdocs*)
- **Bisakah saya memposisikan kode QR di halaman tertentu?** Ya, menggunakan opsi perataan dan nomor halaman
- **Apakah saya memerlukan lisensi untuk produksi?** Ya, lisensi GroupDocs komersial diperlukan
- **Apakah kode QR dapat dipindai setelah ditandatangani?** Tentu saja, jika ukurannya ≥100×100px dan ditempatkan dengan margin yang tepat

## Apa yang Akan Anda Pelajari

Pada akhir panduan ini, Anda akan mengetahui cara:

- Menyiapkan penandatanganan kode QR di proyek Java Anda (Maven, Gradle, atau unduhan langsung)
- Menambahkan kode QR ke dokumen pada posisi tertentu (sudut, tengah, perataan khusus)
- Menangani masalah implementasi umum sebelum menjadi masalah produksi
- Mengoptimalkan kinerja untuk alur kerja pemrosesan dokumen
- Menerapkan teknik ini untuk Skenario bisnis dunia nyata

## Prasyarat

Sebelum kita masuk ke kode, pastikan Anda memiliki:

- **GroupDocs.Signature for Java Library** – versi 23.12 atau lebih baru (kita akan membahas instalasi di bawah)
- **Java Development Kit** – JDK8 atau lebih tinggi (sebagian besar lingkungan produksi menggunakan JDK11+)
- **Build Tool** – Maven atau Gradle untuk manajemen dependensi
- **Pengetahuan Dasar Java** – terbiasa dengan blok try-catch dan penanganan jalur file

Jangan khawatir jika Anda baru mengenal GroupDocs—kita akan membahas semuanya langkah demi langkah.

## Menyiapkan Lingkungan Anda

Memasukkan GroupDocs.Signature ke dalam proyek Anda sangat mudah. ​​Pilih metode yang sesuai dengan sistem build Anda.

### Menggunakan Maven

Tambahkan **maven dependency groupdocs** ini ke file `pom.xml` Anda:

```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

Setelah menambahkan ini, jalankan `mvn clean install` untuk mengunduh pustaka.

### Menggunakan Gradle

Untuk proyek Gradle, tambahkan baris ini ke `build.gradle` Anda:

```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

Kemudian sinkronkan proyek Anda dengan `gradle build`.

### Opsi Unduhan Langsung

Lebih suka instalasi manual? Unduh JAR langsung dari [GroupDocs.Signature untuk rilis Java](https://releases.groupdocs.com/signature/java/) dan tambahkan ke classpath proyek Anda.

### Pengaturan Lisensi (Penting!)

Berikut adalah sesuatu yang mengejutkan orang: GroupDocs memerlukan lisensi untuk penggunaan produksi. Berikut adalah pilihan Anda:

- **Uji Coba Gratis** – bagus untuk pengujian; fitur lengkap, waktu terbatas
- **Lisensi Sementara** – butuh lebih banyak waktu untuk evaluasi? Dapatkan [lisensi sementara](https://purchase.groupdocs.com/temporary-license/) untuk pengujian lebih lanjut
- **Lisensi Komersial** – untuk penerapan produksi, [beli lisensi](https://purchase.groupdocs.com/buy)

Versi uji coba menambahkan watermark ke dokumen Anda, jadi rencanakan dengan tepat untuk demo.

### Inisialisasi Dasar

Setelah Anda menginstal pustaka, menginisialisasi GroupDocs.Signature semudah mengarahkannya ke dokumen Anda:
```java
String filePath = "YOUR_DOCUMENT_DIRECTORY/sample.pdf";
Signature signature = new Signature(filePath);
```

Selesai! Anda sekarang memiliki objek `Signature` yang siap digunakan. Mari kita lanjutkan ke bagian yang menarik—yaitu menambahkan kode QR.

## Memahami Tanda Tangan Kode QR

Sebelum kita masuk ke kode, mari kita klarifikasi apa sebenarnya fungsi tanda tangan kode QR (karena ada beberapa kebingungan mengenai hal ini).

Tanda tangan kode QR bukan hanya sekadar menempelkan kode QR acak pada dokumen Anda. Ini tentang menyematkan informasi yang dapat diverifikasi—seperti stempel waktu, identitas penanda tangan, atau URL verifikasi—langsung ke dalam dokumen dalam format yang dapat dipindai. Ketika seseorang memindai kode QR, mereka dapat memverifikasi keaslian dokumen tanpa memerlukan perangkat lunak khusus.

**Kapan Anda harus menggunakan tanda tangan kode QR?**

- Anda memerlukan verifikasi seluler cepat (pindai dengan ponsel)
- Anda bekerja dengan salinan fisik yang mungkin akan dicetak
- Anda ingin menyematkan tautan ke portal verifikasi
- Anda perlu mendukung alur kerja verifikasi offline

Sekarang mari kita implementasikan ini.

## Panduan Implementasi: Menambahkan Tanda Tangan Kode QR

Di sinilah hal-hal menjadi praktis. Kita akan membahas cara menandatangani PDF dengan kode QR yang ditempatkan di berbagai lokasi pada halaman.

### Mengapa Penempatan Penting

Anda mungkin bertanya-tanya: "Bukankah saya bisa meletakkan kode QR di mana saja?" Secara teknis ya, tetapi inilah kenyataannya—penempatan memengaruhi kegunaan dan validitas hukum. Untuk kontrak, Anda biasanya menginginkan tanda tangan di sudut kanan bawah. Untuk faktur, kanan atas adalah hal yang umum. Untuk sertifikat, penempatan di tengah bagian bawah berfungsi dengan baik.

Keunggulan **GroupDocs.Signature** adalah Anda dapat menentukan dengan tepat di mana kode QR Anda muncul menggunakan opsi perataan.

### Implementasi Langkah demi Langkah

#### 1. Konfigurasi Jalur File Anda

Pertama, tentukan di mana dokumen sumber Anda berada dan di mana Anda ingin versi yang ditandatangani disimpan:

```java
String filePath = "YOUR_DOCUMENT_DIRECTORY/sample.pdf";
String fileName = Paths.get(filePath).getFileName().toString();
String outputFilePath = new File("YOUR_OUTPUT_DIRECTORY", "SignWithAlignment/" + fileName).getPath();
```

**Tips Pro**: Gunakan `Paths.get()` alih-alih penggabungan string untuk jalur file—ini menangani pemisah jalur khusus OS secara otomatis (berfungsi di Windows, Linux, dan Mac tanpa perubahan).

#### 2. Inisialisasi Objek Tanda Tangan

Bungkus inisialisasi Anda dalam blok try-catch untuk menangani potensi masalah akses file:

```java
try {
    Signature signature = new Signature(filePath);
    // Signing logic goes here...
} catch (Exception e) {
    throw new RuntimeException("Error initializing signature: " + e.getMessage(), e);
}
```

Mengapa pembungkus `RuntimeException`? Ini memberikan lebih banyak konteks saat men-debug masalah di lingkungan produksi. Anda akan berterima kasih pada diri sendiri nanti saat melacak mengapa dokumen tidak dapat dimuat.

#### 3. Tentukan Ukuran dan Posisi Kode QR

Di sinilah kita mengatur kode QR di beberapa posisi. Contoh ini membuat kode QR di setiap kombinasi perataan yang mungkin (kiri atas, tengah atas, kanan atas, dll.):

```java
int qrWidth = 100;
int qrHeight = 100;
List<SignOptions> listOptions = new ArrayList<>();

for (int horizontalAlignment : HorizontalAlignment.getValues()) {
    for (int verticalAlignment : VerticalAlignment.getValues()) {
        if (verticalAlignment != VerticalAlignment.None && horizontalAlignment != HorizontalAlignment.None) {
            QrCodeSignOptions options = new QrCodeSignOptions("Left-Top");
            options.setWidth(qrWidth);
            options.setHeight(qrHeight);
            options.setHorizontalAlignment(horizontalAlignment);
            options.setVerticalAlignment(verticalAlignment);
            options.setMargin(new Padding(5));
            listOptions.add(options);
        }
    }
}
```

**Apa yang terjadi di sini?** Kita melakukan perulangan melalui semua perataan horizontal (Kiri, Tengah, Kanan) dan semua perataan vertikal (Atas, Tengah, Bawah), membuat opsi kode QR untuk setiap kombinasi yang valid. `new Padding(5)` menambahkan margin 5 piksel di sekitar setiap kode QR agar tidak tumpang tindih dengan konten dokumen.

**Penyesuaian di dunia nyata**: Dalam produksi, Anda mungkin tidak menginginkan kode QR di **setiap** posisi. Pilih posisi yang sesuai dengan kasus penggunaan Anda. Misalnya, hanya kanan bawah untuk kontrak:

```java
QrCodeSignOptions options = new QrCodeSignOptions("Signature");
options.setWidth(100);
options.setHeight(100);
options.setHorizontalAlignment(HorizontalAlignment.Right);
options.setVerticalAlignment(VerticalAlignment.Bottom);
options.setMargin(new Padding(10));
```

#### 4. Menandatangani Dokumen

Sekarang kita menerapkan semua tanda tangan yang telah dikonfigurasi dalam satu operasi:

```java
SignResult signResult = signature.sign(outputFilePath, listOptions);
```

Metode `sign()` memproses semua kode QR dalam daftar dan menyimpan hasilnya ke jalur output Anda. Metode ini mengembalikan objek `SignResult` yang berisi informasi tentang berapa banyak tanda tangan yang berhasil ditambahkan (berguna untuk pencatatan log).

**Catatan kinerja**: Penandatanganan terjadi secara sinkron. Untuk skenario volume tinggi (ratusan dokumen per jam), pertimbangkan untuk mengimplementasikannya dalam antrian pekerjaan latar belakang daripada dalam permintaan yang berhadapan dengan pengguna.

## Kesalahan Umum dan Solusinya

Mari kita bahas masalah yang paling sering dihadapi pengembang.

### Masalah 1: Kesalahan "File Tidak Ditemukan"

**Gejala**: Kode Anda melempar pengecualian file tidak ditemukan meskipun file tersebut ada.

**Solusi**: Periksa tiga hal ini:

1. Apakah Anda menggunakan jalur absolut? Jalur relatif bisa rumit tergantung di mana aplikasi Anda berjalan.
2. Apakah aplikasi Anda memiliki izin baca untuk file sumber dan izin tulis untuk direktori output?
3. Apakah ada karakter khusus dalam jalur file yang perlu di-escape?

```java
// Better approach: Use absolute paths
String absolutePath = new File(filePath).getAbsolutePath();
Signature signature = new Signature(absolutePath);
```

### Masalah 2: Kode QR Tumpang Tindih dengan Konten Dokumen

**Gejala**: Kode QR menutupi teks penting atau tampak terpotong di tepi halaman.

**Solusi**: Tingkatkan nilai margin dan sesuaikan perataan secara strategis:

```java
options.setMargin(new Padding(20)); // Increase from 5 to 20 pixels
```
Untuk dokumen dengan tata letak konten yang beragam, pertimbangkan untuk menambahkan kode QR ke area halaman tertentu yang selalu kosong (seperti area blok tanda tangan).

### Masalah 3: Masalah Memori dengan Dokumen Besar

**Gejala**: `OutOfMemoryError` saat memproses PDF di atas 10MB.

**Solusi**: Pastikan Anda membuang objek `Signature` dengan benar dan pertimbangkan untuk memproses dokumen besar secara bertahap:

```java
try (Signature signature = new Signature(filePath)) {
    // Your signing code
} // Automatically closes and releases resources
```

Pernyataan try-with-resources memastikan pembersihan yang tepat bahkan jika terjadi pengecualian.

### Masalah 4: Konten Kode QR Tidak Diperbarui

**Gejala**: Semua kode QR menampilkan teks yang sama, meskipun Anda mencoba menyesuaikannya.

**Solusi**: Pastikan Anda membuat objek `QrCodeSignOptions` **baru** untuk setiap posisi, bukan menggunakan kembali objek yang sama:

```java
// Wrong - reuses same object
QrCodeSignOptions options = new QrCodeSignOptions("Text");
options.setHorizontalAlignment(HorizontalAlignment.Left);
listOptions.add(options);
options.setHorizontalAlignment(HorizontalAlignment.Right); // Modifies existing!
listOptions.add(options);

// Correct - creates new object each time
listOptions.add(new QrCodeSignOptions("Left"));
listOptions.add(new QrCodeSignOptions("Right"));
```

## Aplikasi Praktis

Sekarang mari kita bahas di mana ini sebenarnya digunakan dalam skenario bisnis nyata.

### 1. Sistem Manajemen Kontrak

Anda sedang membangun sistem di mana kontrak hukum memerlukan tanda tangan digital dengan kemampuan verifikasi. Berikut alur kerjanya:

- Buat PDF kontrak dari templat
- Tambahkan tanda tangan kode QR yang berisi: ID kontrak, stempel waktu, hash penanda tangan
- Simpan dokumen di penyimpanan yang aman
- Saat memverifikasi, pengguna memindai kode QR → dialihkan ke portal verifikasi → menampilkan detail kontrak

**Mengapa ini berhasil**: Tim hukum dapat memverifikasi keaslian bahkan dari salinan cetak, dan kode QR menyediakan jejak audit.

### 2. Otomatisasi Pemrosesan Faktur

Sistem hutang dagang Anda menerima ratusan faktur setiap hari. Anda perlu:

- Menambahkan kode QR ke setiap faktur yang diproses
- Mengenkode nomor faktur, ID vendor, dan stempel waktu pemrosesan
- Menggunakan posisi kanan atas agar tidak mengganggu data faktur
- Mengarsipkan faktur yang telah ditandatangani untuk kepatuhan

**Tips implementasi**: Posisikan kode QR secara konsisten di semua faktur agar pemindai otomatis tahu persis di mana harus mencari.

### 3. Sertifikasi Dokumen

Anda menerbitkan sertifikat (penyelesaian pelatihan, kepatuhan, dll.) yang perlu diverifikasi:

- Menghasilkan PDF sertifikat dengan detail penerima
- Menambahkan kode QR di bagian bawah tengah dengan ID sertifikat dan URL verifikasi
- Penerima dapat memindai untuk memverifikasi keaslian
- Pemberi kerja dapat memverifikasi kredensial secara instan

**Bonus**: Sertakan URL kecil yang dicetak di bawah kode QR untuk orang yang tidak dapat memindainya.

### 4. Pelacakan Dokumen Internal

Untuk organisasi besar dengan alur kerja persetujuan dokumen:

- Tambahkan kode QR selama setiap tahap persetujuan
- Kode QR berisi: ID pemberi persetujuan, stempel waktu persetujuan, versi dokumen
- Pindai untuk melihat riwayat persetujuan lengkap
- Membantu dalam jejak audit dan kepatuhan

## Praktik Terbaik Produksi

Beralih dari prototipe ke produksi? Perhatikan praktik-praktik ini.

### Manajemen Sumber Daya

Selalu tutup objek `Signature` untuk mencegah kebocoran memori:

```java
try (Signature signature = new Signature(filePath)) {
    // Your code
} // Auto‑closes
```

Untuk aplikasi web, pertimbangkan untuk menerapkan kumpulan pemrosesan dokumen untuk membatasi operasi bersamaan.

### Strategi Penanganan Kesalahan

Jangan hanya menangkap dan mencatat—berikan informasi kesalahan yang dapat ditindaklanjuti:

```java
try {
    SignResult result = signature.sign(outputFilePath, listOptions);
    if (result.getSucceeded().size() < listOptions.size()) {
        logger.warn("Only {} of {} signatures applied",
                    result.getSucceeded().size(),
                    listOptions.size());
    }
} catch (Exception e) {
    logger.error("Signature failed for document: {}", filePath, e);
    // Implement retry logic or alert mechanism
}
```

### Optimasi Kinerja

Untuk skenario volume tinggi:

1. **Pemrosesan Batch** – proses beberapa dokumen secara paralel (tetapi batasi konkurensi berdasarkan memori yang tersedia)
2. **Caching** – jika menggunakan opsi tanda tangan yang sama berulang kali, buat sekali dan gunakan kembali
3. **Operasi Asinkron** – implementasikan penandatanganan di pekerja latar belakang untuk aplikasi yang berhadapan dengan pengguna
4. **Pemantauan Memori** – atur peringatan untuk lonjakan penggunaan memori

### Pertimbangan Keamanan

- Simpan dokumen yang telah ditandatangani secara terpisah dari dokumen asli
- Catat semua operasi penandatanganan untuk tujuan audit
- Implementasikan kontrol akses untuk operasi tanda tangan
- Pertimbangkan untuk mengenkripsi konten kode QR untuk informasi sensitif

## Kapan Menggunakan Tanda Tangan Kode QR (Dan Kapan Tidak)

**Gunakan tanda tangan kode QR ketika:**

- Anda memerlukan verifikasi yang ramah seluler
- Dokumen mungkin dicetak dan dipindai ulang
- Anda ingin menyematkan URL atau ID verifikasi
- Anda sedang bekerja dengan Dokumen yang dapat diakses publik (sertifikat, tanda terima)

**Jangan gunakan tanda tangan kode QR jika:**

- Anda memerlukan tanda tangan kriptografi yang mengikat secara hukum (gunakan tanda tangan berbasis PKI sebagai gantinya)
- Kode QR mungkin rusak atau terhalang saat dicetak
- Sistem verifikasi Anda hanya offline
- Ukuran dokumen sangat penting (kode QR menambah beberapa kilobyte)

**Pertimbangkan untuk menggabungkan**: Gunakan tanda tangan kriptografi **dan** kode QR. Anda mendapatkan validitas hukum plus verifikasi seluler yang mudah.

## Panduan Pemecahan Masalah

### Tanda Tangan Tidak Muncul

1. Apakah file output sedang dibuat? (Periksa sistem file Anda)
2. Apakah Anda membuka file output yang benar?

3. Apakah `SignResult` menunjukkan keberhasilan?

4. Apakah nilai perataan dan margin Anda mendorong kode QR keluar dari area halaman yang terlihat?

### Kode QR Tidak Dapat Dipindai

- Jaga ukuran kode QR ≥100×100px
- Pastikan kontras tinggi dengan latar belakang
- Batasi data yang dikodekan hingga <100 karakter untuk pemindaian yang andal
- Gunakan DPI yang lebih tinggi saat mencetak salinan fisik

### Penurunan Kinerja

- Kurangi jumlah tanda tangan per dokumen
- Verifikasi bahwa Anda tidak membuat objek `Signature` baru secara tidak perlu
- Profilkan penggunaan memori; pertimbangkan untuk memproses dokumen dalam batch yang lebih kecil

## Pertanyaan yang Sering Diajukan

**T:** *Bisakah saya menandatangani dokumen selain PDF?*
**J:** Tentu saja. GroupDocs.Signature mendukung Word (DOC/DOCX), Excel (XLS/XLSX), PowerPoint (PPT/PPTX), dan format gambar (JPG, PNG, TIFF). API sebagian besar tetap sama di semua format.

**T:** *Bagaimana cara menyesuaikan tampilan kode QR?*
**J:** Gunakan properti `QrCodeSignOptions` seperti `setForeColor()`, `setBackgroundColor()`, dan `setBorder()`. Jaga agar penyesuaian tetap sederhana untuk mempertahankan kemudahan pemindaian.

**T:** *Bisakah saya menambahkan kode QR ke halaman tertentu dalam dokumen multi-halaman?*
**J:** Ya! Atur nomor halaman dengan `options.setPageNumber(pageNumber);`. Contoh:

```java
options.setPageNumber(1); // Add to first page only
```

**T:** *Data apa yang dapat saya encode dalam kode QR?*
**J:** Apa pun yang Anda inginkan—teks biasa, URL, JSON, XML. Jaga agar panjangnya kurang dari ~200 karakter agar pemindaian lebih andal. Untuk muatan yang lebih besar, encode URL pendek yang mengarah ke data lengkap.

**T:** *Bagaimana cara memverifikasi tanda tangan kode QR secara terprogram?*
**J:** GroupDocs.Signature menyediakan metode `verify`. Contoh:

```java
VerificationResult result = signature.verify(verifyOptions);
if (result.isValid()) {
    // Signature is authentic
}
```

**T:** *Bisakah saya menggunakan ini di lingkungan multi-thread?*
**J:** Ya, tetapi buat instance `Signature` terpisah untuk setiap thread—instance tidak aman untuk thread. Gunakan antrian pemrosesan untuk skenario konkurensi tinggi.

**T:** *Berapa dampak ukuran file jika menambahkan kode QR?*
**J:** Minimal—biasanya 5-20KB per kode QR tergantung pada ukuran dan konten. Untuk sebagian besar PDF, ini dapat diabaikan, tetapi perhitungkan penyimpanan jika menambahkan banyak kode QR ke dalam batch besar.

## Langkah Selanjutnya

Anda sekarang memiliki dasar yang kuat untuk mengimplementasikan tanda tangan **java generate qr code** di Java. Berikut beberapa hal yang dapat Anda jelajahi selanjutnya:

1. **Kustomisasi Tingkat Lanjut** – pelajari opsi penataan kode QR di [dokumentasi GroupDocs](https://docs.groupdocs.com/signature/java/)
2. **Sistem Verifikasi** – bangun portal web tempat pengguna dapat memverifikasi dokumen dengan mengunggah atau memindai kode QR
3. **Integrasi Alur Kerja** – hubungkan ini ke sistem manajemen dokumen Anda yang sudah ada
4. **Aplikasi Seluler** – buat aplikasi seluler pendamping untuk memindai dan memverifikasi kode QR

Selamat berkoding, dan nikmati keamanan dan kenyamanan tambahan yang diberikan oleh tanda tangan kode QR pada aplikasi Java Anda!

## Sumber Daya dan Dukungan

- **Dokumentasi**: [GroupDocs.Signature Java Docs](https://docs.groupdocs.com/signature/java/)
- **Referensi API**: [Referensi API Lengkap](https://reference.groupdocs.com/signature/java/)
- **Unduhan**: [Rilis Java Terbaru](https://releases.groupdocs.com/signature/java/)
- **Pembelian Lisensi**: [Beli GroupDocs.Signature](https://purchase.groupdocs.com/buy)
- **Uji Coba Gratis**: [Mulai Uji Coba Gratis Anda](https://releases.groupdocs.com/signature/java/)
- **Lisensi Sementara**: [Dapatkan Lisensi Sementara](https://purchase.groupdocs.com/temporary-license/)
- **Dukungan Komunitas**: [GroupDocs Forum](https://forum.groupdocs.com/c/signature/)

---

**Terakhir Diperbarui:** 2025-12-31
**Diuji Dengan:** GroupDocs.Signature 23.12 untuk Java
**Penulis:** GroupDocs