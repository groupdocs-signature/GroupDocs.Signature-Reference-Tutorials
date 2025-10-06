---
"description": "Pelajari cara mudah menghapus tanda tangan kode QR dari dokumen Anda menggunakan GroupDocs.Signature untuk .NET dengan panduan pengembang langkah demi langkah kami."
"linktitle": "Hapus Tanda Tangan Kode QR dari Dokumen"
"second_title": "GroupDocs.Signature .NET API"
"title": "Cara Menghapus Tanda Tangan Kode QR dari Dokumen di .NET"
"url": "/id/net/delete-operations/delete-qr-code-signature/"
"weight": 16
type: docs
---
# Cara Menghapus Tanda Tangan Kode QR dari Dokumen Anda

## Perkenalan

Pernahkah Anda perlu menghapus tanda tangan kode QR dari dokumen secara terprogram? Baik Anda sedang membersihkan informasi yang sudah usang atau mempersiapkan dokumen untuk didistribusikan ulang, kemampuan mengelola tanda tangan dokumen secara efektif merupakan keterampilan penting bagi pengembang .NET.

Dalam panduan praktis ini, kami akan memandu Anda secara detail cara menghapus tanda tangan kode QR dari dokumen menggunakan GroupDocs.Signature untuk .NET. Pustaka canggih ini memudahkan pengelolaan tanda tangan, memungkinkan Anda untuk fokus membangun aplikasi yang hebat alih-alih berkutat dengan tantangan manipulasi dokumen.

## Apa yang Anda Butuhkan Sebelum Memulai

Sebelum kita masuk ke kode, mari pastikan Anda telah menyiapkan semuanya:

- GroupDocs.Signature untuk .NET: Anda perlu menginstal pustaka ini di proyek Anda. Anda dapat mengunduhnya langsung dari [halaman rilis GroupDocs](https://releases.groupdocs.com/signature/net/).
- Dokumen dengan kode QR: Untuk latihan, siapkan dokumen yang berisi setidaknya satu tanda tangan kode QR yang ingin Anda hapus.
- Pengetahuan dasar C#: Anda harus merasa nyaman dengan dasar-dasar C# untuk mengikuti contoh-contoh kami.

Setelah prasyarat ini terpenuhi, Anda siap untuk mulai menghapus kode QR tersebut!

## Menyiapkan Proyek Anda dengan Namespace yang Tepat

Hal pertama yang harus dilakukan – mari impor namespace yang diperlukan agar kode kita berfungsi dengan lancar:

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

Impor ini memberi kita akses ke semua fungsi yang kita perlukan dari pustaka GroupDocs.Signature, serta beberapa kelas .NET penting untuk penanganan berkas.

## Langkah 1: Di Mana File Anda? Menyiapkan Jalur Dokumen

Mari kita mulai dengan menentukan di mana dokumen kita berada dan di mana kita ingin menyimpan versi yang dimodifikasi:

```csharp
// Jalur ke direktori dokumen.
string filePath = "sample_multiple_signatures.docx";
string fileName = Path.GetFileName(filePath);

// Tentukan jalur berkas keluaran untuk dokumen yang dimodifikasi.
string outputFilePath = Path.Combine("Your Document Directory", "DeleteQRCode", fileName);

// Salin berkas sumber karena metode Hapus berfungsi dengan Dokumen yang sama.
File.Copy(filePath, outputFilePath, true);
```

Perhatikan bahwa kita sedang membuat salinan dari dokumen asli kita. Ini penting karena proses penghapusan tanda tangan akan langsung mengubah berkas, dan kita selalu ingin mempertahankan dokumen asli kita.

## Langkah 2: Membuat Objek Tanda Tangan untuk Digunakan

Sekarang kita akan membuat objek Tanda Tangan yang terhubung ke dokumen kita:

```csharp
using (Signature signature = new Signature(outputFilePath))
{
    // Buat opsi untuk mencari tanda tangan kode QR.
    QrCodeSearchOptions options = new QrCodeSearchOptions();
    
    // Cari tanda tangan kode QR dalam dokumen.
    List<QrCodeSignature> signatures = signature.Search<QrCodeSignature>(options);
```

Kode ini menginisialisasi objek Tanda Tangan dengan dokumen kita, lalu mencari tanda tangan kode QR yang ada di dalamnya. Pencarian akan menampilkan daftar semua tanda tangan kode QR yang ditemukan.

## Langkah 3: Apakah Ada Kode QR yang Harus Dihapus?

Sebelum mencoba menghapus apa pun, kita harus memeriksa apakah benar-benar ada kode QR:

```csharp
    if (signatures.Count > 0)
    {
        // Dapatkan tanda tangan kode QR pertama yang ditemukan dalam dokumen.
        QrCodeSignature qrCodeSignature = signatures[0];
```

Pemeriksaan sederhana ini memastikan kami hanya melanjutkan jika terdapat setidaknya satu tanda tangan kode QR dalam dokumen. Dalam contoh ini, kami menargetkan kode QR pertama yang ditemukan, tetapi Anda dapat dengan mudah memodifikasinya untuk menangani beberapa tanda tangan jika diperlukan.

## Langkah 4: Menghapus Kode QR dari Dokumen Anda

Sekarang untuk acara utama – benar-benar menghapus kode QR:

```csharp
        // Hapus tanda tangan kode QR dari dokumen.
        bool result = signature.Delete(qrCodeSignature);
        
        if (result)
        {
            Console.WriteLine($"Signature with QR-Code '{qrCodeSignature.Text}' and encode type '{qrCodeSignature.EncodeType.TypeName}' was deleted from document ['{fileName}'].");
        }
        else
        {
            Console.WriteLine($"Signature was not deleted from the document! Signature with QR-Code '{qrCodeSignature.Text}' and encode type '{qrCodeSignature.EncodeType.TypeName}' was not found!");
        }
    }
}
```

Kode tersebut menghapus tanda tangan dan memberikan umpan balik tentang keberhasilan operasi. Umpan balik ini penting untuk men-debug dan memastikan kode Anda berfungsi sebagaimana mestinya.

## Apa yang Telah Kita Capai?

Selamat! Anda baru saja mempelajari cara menghapus tanda tangan kode QR dari dokumen menggunakan GroupDocs.Signature untuk .NET. Keterampilan ini membuka banyak kemungkinan untuk manajemen dokumen di aplikasi Anda.

Hanya dengan beberapa baris kode, Anda sekarang dapat membersihkan dokumen secara terprogram dengan menghapus tanda tangan kode QR yang kedaluwarsa atau tidak diperlukan, memastikan dokumen Anda selalu hanya berisi informasi yang relevan.

## Pertanyaan Umum yang Mungkin Anda Miliki

### Bisakah saya menghapus beberapa kode QR sekaligus?

Tentu saja! Alih-alih hanya menghapus tanda tangan pertama yang ditemukan, Anda dapat menelusuri seluruh daftar tanda tangan dan menghapus masing-masing seperti ini:

```csharp
foreach(var qrSignature in signatures)
{
    signature.Delete(qrSignature);
}
```

### Jenis tanda tangan apa lagi yang dapat saya kelola dengan GroupDocs.Signature?

GroupDocs.Signature sangat serbaguna, mendukung berbagai jenis tanda tangan termasuk:
- Tanda tangan teks
- Tanda tangan gambar
- Tanda tangan kode batang
- Tanda tangan digital
- Dan masih banyak lagi!

### Apakah ini akan berfungsi dengan semua format dokumen saya?

Anda akan senang mengetahui bahwa GroupDocs.Signature berfungsi dengan berbagai format dokumen, termasuk:
- Dokumen PDF
- Dokumen Microsoft Word
- Lembar kerja Excel
- presentasi PowerPoint
- Dan masih banyak lagi

### Bisakah saya mencari kode QR tertentu daripada menghapus semuanya?

Ya! Itu `QrCodeSearchOptions` Kelas ini menawarkan berbagai properti untuk memfilter pencarian Anda. Misalnya, Anda dapat mencari kode QR yang berisi teks tertentu atau dikodekan dengan format tertentu.

### Apakah ada cara untuk mencoba GroupDocs.Signature sebelum membeli?

Ya, Anda dapat mengunduh versi uji coba gratis dari [situs web GroupDocs](https://releases.groupdocs.com/) untuk mengujinya dengan kasus penggunaan spesifik Anda sebelum membuat komitmen.