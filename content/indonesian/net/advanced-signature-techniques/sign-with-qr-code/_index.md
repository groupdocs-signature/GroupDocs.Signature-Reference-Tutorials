---
"description": "Pelajari cara meningkatkan keamanan dokumen dengan menambahkan tanda tangan kode QR menggunakan GroupDocs.Signature untuk .NET. Implementasi sederhana dengan contoh kode lengkap."
"linktitle": "Penandatanganan dengan Kode QR"
"second_title": "GroupDocs.Signature .NET API"
"title": "Cara Menandatangani Dokumen dengan Kode QR Menggunakan GroupDocs.Signature"
"url": "/id/net/advanced-signature-techniques/sign-with-qr-code/"
"weight": 15
---

# Menambahkan Tanda Tangan Kode QR ke Dokumen dengan GroupDocs.Signature

Pernahkah Anda bertanya-tanya bagaimana cara menambahkan lapisan keamanan dan autentikasi ekstra ke dokumen digital Anda? Tanda tangan kode QR mungkin yang Anda cari. Dalam panduan praktis ini, kami akan memandu Anda melalui seluruh proses penerapan tanda tangan kode QR menggunakan GroupDocs.Signature untuk .NET.

## Mengapa Anda Ingin Menggunakan Kode QR dalam Dokumen?

Kode QR bukan hanya untuk menu restoran dan materi pemasaran. Ketika diintegrasikan ke dalam alur kerja dokumen Anda, kode QR dapat:

- Memberikan verifikasi instan keaslian dokumen
- Simpan metadata penting yang tidak mengacaukan dokumen Anda secara visual
- Aktifkan akses cepat ke sumber daya digital terkait
- Buat jembatan antara sistem dokumentasi fisik dan digital Anda

Mari selami bagaimana Anda dapat mengimplementasikan fitur hebat ini dalam aplikasi .NET Anda!

## Apa yang Anda Butuhkan Sebelum Memulai

Sebelum kita masuk ke kode, pastikan Anda telah menyiapkan semuanya:

1. GroupDocs.Signature untuk .NET: Anda dapat mengunduh pustaka hebat ini langsung dari [Situs web GroupDocs](https://releases.groupdocs.com/signature/net/).

2. Lingkungan Pengembangan .NET: Versi Visual Studio terbaru mana pun akan berfungsi sempurna untuk tujuan kita.

3. Dokumen Uji: Ambil PDF, Word, atau dokumen pendukung lainnya yang ingin Anda uji coba.

Setelah Anda menyiapkan hal-hal penting ini, Anda siap untuk mulai menerapkan tanda tangan kode QR!

## Menyiapkan Proyek Anda dengan Namespace yang Tepat

Hal pertama yang terpenting, kita perlu mengimpor namespace yang diperlukan untuk mengakses semua fungsi yang kita perlukan:

```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

Ruang nama ini akan memberi kita akses ke fungsionalitas inti pustaka GroupDocs.Signature, termasuk opsi khusus untuk tanda tangan kode QR.

## Bagaimana Anda Menentukan Jalur Dokumen Anda?

Mari kita atur jalur berkas untuk dokumen sumber kita dan tempat kita ingin menyimpan versi yang ditandatangani:

```csharp
string filePath = "sample.pdf";
string fileName = Path.GetFileName(filePath);
string outputFilePath = Path.Combine("Your Document Directory", "SignWithQRCode", fileName);
```

Ingat untuk mengganti `"Your Document Directory"` dengan jalur penyimpanan dokumen yang sudah ditandatangani. Pengelolaan berkas yang baik akan menghemat masalah Anda nantinya!

## Membuat Objek Tanda Tangan Anda

Sekarang kita akan menginisialisasi `Signature` objek yang akan menangani semua kebutuhan penandatanganan dokumen kita:

```csharp
using (Signature signature = new Signature(filePath))
{
    // Kami akan menambahkan kode penandatanganan kami di sini pada langkah berikutnya
}
```

Objek ini berfungsi sebagai antarmuka utama kita ke dokumen yang ingin kita ubah. `using` pernyataan tersebut memastikan bahwa semua sumber daya dibuang dengan benar setelah selesai.

## Cara Mengonfigurasi Tanda Tangan Kode QR Anda

Di sinilah keajaiban terjadi - kami akan membuat dan menyesuaikan tanda tangan kode QR kami:

```csharp
QrCodeSignOptions options = new QrCodeSignOptions("JohnSmith")
{
    EncodeType = QrCodeTypes.QR,
    Left = 50,
    Top = 150,
    Width = 200,
    Height = 200
};
```

Dalam contoh ini, kami mengodekan "JohnSmith" dalam kode QR kami, tetapi Anda dapat menyertakan teks apa pun yang Anda inginkan - mungkin URL verifikasi, tanda tangan digital, atau metadata dokumen. Kami juga memposisikan kode QR 50 piksel dari kiri dan 150 piksel dari atas halaman, dengan dimensi 200x200 piksel.

## Menerapkan Kode QR ke Dokumen Anda

Dengan pilihan yang telah dikonfigurasi, penerapan tanda tangan ternyata sangat mudah:

```csharp
SignResult result = signature.Sign(outputFilePath, options);
```

Baris kode tunggal ini menerapkan kode QR ke dokumen Anda dan menyimpan hasilnya ke jalur keluaran yang Anda tentukan. `SignResult` Objek memberi kita informasi tentang bagaimana prosesnya berlangsung.

## Cara Memverifikasi Bahwa Semuanya Bekerja dengan Benar

Terakhir, mari tambahkan beberapa masukan untuk mengonfirmasi bahwa proses penandatanganan kami berhasil:

```csharp
Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).\nFile saved at {outputFilePath}.");
```

Ini akan menampilkan pesan bermanfaat yang menunjukkan berapa banyak tanda tangan yang ditambahkan dan di mana menemukan dokumen yang baru Anda tandatangani.

## Aplikasi Dunia Nyata untuk Tanda Tangan Kode QR

Anda mungkin bertanya-tanya bagaimana Anda bisa menggunakan ini dalam konteks spesifik Anda. Berikut beberapa aplikasi praktisnya:

- Dokumen Hukum: Tambahkan kode QR yang tertaut ke situs web verifikasi atau berisi data verifikasi terenkripsi
- Laporan Perusahaan: Sertakan kode QR yang terhubung ke sumber daya online tambahan atau informasi terkini
- Materi Pendidikan: Sematkan kode QR yang terhubung ke tutorial video atau sumber belajar interaktif
- Dokumentasi Medis: Gunakan kode QR untuk mengakses riwayat pasien atau informasi pengobatan dengan cepat

## Apa Selanjutnya Setelah Menerapkan Tanda Tangan Kode QR?

Sekarang setelah Anda menguasai penambahan tanda tangan kode QR ke dokumen Anda, Anda mungkin ingin menjelajahi fitur lain dari pustaka GroupDocs.Signature, seperti:

- Menerapkan beberapa jenis tanda tangan dalam satu dokumen
- Membuat alur kerja pemrosesan batch untuk penandatanganan dokumen bervolume tinggi
- Mengembangkan mekanisme verifikasi untuk memvalidasi dokumen yang ditandatangani
- Menjelajahi opsi kode QR yang lebih canggih seperti metadata yang dikodekan dan tampilan khusus

## Pertanyaan Umum Tentang Tanda Tangan Dokumen Kode QR

### Bisakah saya menyesuaikan tampilan kode QR saya dalam dokumen?

Tentu saja! Anda memiliki kendali penuh atas tampilan kode QR Anda. Selain posisi dan ukuran yang kami tunjukkan, Anda juga dapat menyesuaikan warna, menambahkan batas, dan memodifikasi jenis penyandian sesuai kebutuhan spesifik Anda.

### Format dokumen mana yang mendukung tanda tangan kode QR?

Pustaka GroupDocs.Signature untuk .NET mendukung berbagai format dokumen, termasuk:
- Dokumen PDF
- Dokumen Microsoft Word (.docx, .doc)
- Lembar kerja Excel
- presentasi PowerPoint
- Dan masih banyak lagi

### Apakah ada cara untuk memproses beberapa dokumen secara batch?

Ya! GroupDocs.Signature memudahkan penerapan pemrosesan batch. Anda dapat membuat loop sederhana atau menggunakan pemrosesan paralel yang lebih canggih untuk menandatangani beberapa dokumen secara efisien, yang sempurna untuk skenario volume tinggi.

### Bagaimana saya dapat memverifikasi keaslian tanda tangan kode QR?

GroupDocs.Signature menyediakan mekanisme verifikasi komprehensif yang memungkinkan Anda memeriksa integritas dan keaslian dokumen yang ditandatangani dengan kode QR. Ini memastikan dokumen Anda tidak dirusak setelah ditandatangani.

### Dapatkah saya mencoba fungsi ini sebelum membeli?

Tentu saja! GroupDocs menawarkan versi uji coba gratis yang dapat Anda unduh dari [situs web](https://releases.groupdocs.com/)Hal ini memungkinkan Anda untuk mengevaluasi semua fitur secara menyeluruh dan memastikannya memenuhi kebutuhan Anda sebelum membuat komitmen.