---
title: Hapus Tanda Tangan Kode QR dari Dokumen
linktitle: Hapus Tanda Tangan Kode QR dari Dokumen
second_title: GroupDocs.Tanda Tangan .NET API
description: Pelajari cara menghapus tanda tangan kode QR dari dokumen menggunakan GroupDocs.Signature untuk .NET. Ikuti panduan langkah demi langkah kami untuk pengelolaan tanda tangan yang efisien.
weight: 16
url: /id/net/delete-operations/delete-qr-code-signature/
---

# Hapus Tanda Tangan Kode QR dari Dokumen

## Perkenalan
Dalam tutorial ini, kami akan memandu Anda melalui proses menghapus tanda tangan kode QR dari dokumen menggunakan GroupDocs.Signature untuk .NET. Ikuti petunjuk langkah demi langkah ini untuk menghapus tanda tangan kode QR secara efektif.
## Prasyarat
Sebelum memulai, pastikan Anda memiliki prasyarat berikut:
-  GroupDocs.Signature untuk .NET: Pastikan Anda telah menginstal perpustakaan GroupDocs.Signature di proyek .NET Anda. Anda dapat mengunduhnya dari[Di Sini](https://releases.groupdocs.com/signature/net/).
- Dokumen dengan Tanda Tangan Kode QR: Siapkan dokumen berisi tanda tangan kode QR yang ingin Anda hapus.
- Pengetahuan Dasar C#: Biasakan diri Anda dengan dasar-dasar bahasa pemrograman C#.

## Mengimpor Namespace
Sebelum mendalami kode, impor namespace yang diperlukan ke file C# Anda:
```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## Langkah 1: Tentukan Jalur File
```csharp
// Jalur ke direktori dokumen.
string filePath = "sample_multiple_signatures.docx";
string fileName = Path.GetFileName(filePath);
// Tentukan jalur file keluaran untuk dokumen yang dimodifikasi.
string outputFilePath = Path.Combine("Your Document Directory", "DeleteQRCode", fileName);
// Salin file sumber karena metode Hapus berfungsi dengan Dokumen yang sama.
File.Copy(filePath, outputFilePath, true);
```
## Langkah 2: Inisialisasi Objek Tanda Tangan
```csharp
using (Signature signature = new Signature(outputFilePath))
{
    // Buat opsi untuk mencari tanda tangan kode QR.
    QrCodeSearchOptions options = new QrCodeSearchOptions();
    // Cari tanda tangan kode QR di dokumen.
    List<QrCodeSignature> signatures = signature.Search<QrCodeSignature>(options);
```
## Langkah 3: Periksa Keberadaan Tanda Tangan Kode QR
```csharp
    if (signatures.Count > 0)
    {
        // Dapatkan tanda tangan kode QR pertama yang ditemukan di dokumen.
        QrCodeSignature qrCodeSignature = signatures[0];
```
## Langkah 4: Hapus Tanda Tangan Kode QR
```csharp
        // Hapus tanda tangan kode QR dari dokumen.
        bool result = signature.Delete(qrCodeSignature);
        if (result)
        {
            Console.WriteLine($"Signature with QR-Code '{qrCodeSignature.Text}' and encode type '{qrCodeSignature.EncodeType.TypeName}' was deleted from document ['{fileName}'].");
        }
        else
        {
            Helper.WriteError($"Signature was not deleted from the document! Signature with Barcode '{qrCodeSignature.Text}' and encode type '{qrCodeSignature.EncodeType.TypeName}' was not found!");
        }
    }
}
```
Selamat! Anda telah berhasil menghapus tanda tangan kode QR dari dokumen menggunakan GroupDocs.Signature untuk .NET.

## Kesimpulan
Dalam tutorial ini, kita mempelajari cara menghapus tanda tangan kode QR dari dokumen menggunakan GroupDocs.Signature untuk .NET. Dengan mengikuti langkah-langkah yang disediakan, Anda dapat mengelola dan memanipulasi tanda tangan secara efisien dalam aplikasi .NET Anda.
## FAQ
### Bisakah saya menghapus beberapa tanda tangan kode QR dari sebuah dokumen?
Ya, Anda dapat memodifikasi kode untuk mengulangi semua tanda tangan kode QR dan menghapusnya sesuai kebutuhan.
### Apakah GroupDocs.Signature mendukung jenis tanda tangan lain selain kode QR?
Ya, GroupDocs.Signature mendukung berbagai jenis tanda tangan seperti teks, gambar, kode batang, dan lainnya.
### Apakah GroupDocs.Signature kompatibel dengan semua format dokumen?
GroupDocs.Signature mendukung berbagai format dokumen termasuk PDF, Microsoft Word, Excel, PowerPoint, dan banyak lagi.
### Bisakah saya menyesuaikan opsi pencarian tanda tangan?
Ya, Anda dapat menyesuaikan opsi pencarian sesuai kebutuhan Anda untuk menemukan tanda tangan tertentu di dalam dokumen.
### Apakah ada versi uji coba yang tersedia untuk GroupDocs.Signature?
 Ya, Anda dapat mengakses versi uji coba gratis GroupDocs.Signature dari[Di Sini](https://releases.groupdocs.com/).