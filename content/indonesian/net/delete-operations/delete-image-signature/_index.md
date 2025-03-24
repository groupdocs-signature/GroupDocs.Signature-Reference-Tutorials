---
title: Hapus Tanda Tangan Gambar
linktitle: Hapus Tanda Tangan Gambar
second_title: GroupDocs.Tanda Tangan .NET API
description: Pelajari cara menghapus tanda tangan gambar dari dokumen menggunakan GroupDocs.Signature untuk .NET. Ikuti panduan langkah demi langkah kami untuk pengelolaan tanda tangan yang efisien.
weight: 14
url: /id/net/delete-operations/delete-image-signature/
---
## Perkenalan
Dalam tutorial ini, kita akan mempelajari cara menghapus tanda tangan gambar dari dokumen menggunakan GroupDocs.Signature untuk .NET. GroupDocs.Signature adalah perpustakaan canggih yang memungkinkan pengembang bekerja dengan tanda tangan digital, stempel, dan bidang formulir dalam berbagai format dokumen.
## Prasyarat
Sebelum kita mulai, pastikan Anda memiliki hal berikut:
### 1. GroupDocs.Signature untuk .NET
 Unduh dan instal GroupDocs.Signature untuk .NET dari[situs web](https://releases.groupdocs.com/signature/net/). Ikuti petunjuk instalasi yang disediakan dalam dokumentasi.
### 2. .NET Kerangka
Pastikan Anda telah menginstal .NET Framework di mesin Anda.
## Impor Namespace
Sertakan namespace yang diperlukan dalam proyek Anda:
```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
Mari kita uraikan proses penghapusan tanda tangan gambar menjadi beberapa langkah:
## Langkah 1: Tentukan Jalur File
Pertama, tentukan jalur untuk dokumen masukan dan dokumen keluaran setelah menghapus tanda tangan:
```csharp
string filePath = "sample_multiple_signatures.docx";
string fileName = Path.GetFileName(filePath);
string outputFilePath = Path.Combine("Your Document Directory", "DeleteImage", fileName);
```
## Langkah 2: Salin File Sumber
 Sejak itu`Delete`metode ini berfungsi dengan dokumen yang sama, penting untuk menyalin file sumber ke lokasi lain:
```csharp
File.Copy(filePath, outputFilePath, true);
```
## Langkah 3: Inisialisasi Objek Tanda Tangan
 Buat sebuah instance dari`Signature` kelas dan tentukan jalur ke dokumen keluaran:
```csharp
using (Signature signature = new Signature(outputFilePath))
{
    // Kode ada di sini
}
```
## Langkah 4: Cari Tanda Tangan Gambar
Tentukan opsi pencarian dan cari tanda tangan gambar di dalam dokumen:
```csharp
ImageSearchOptions options = new ImageSearchOptions();
List<ImageSignature> signatures = signature.Search<ImageSignature>(options);
```
## Langkah 5: Hapus Tanda Tangan Gambar
Jika tanda tangan gambar ditemukan, hapus yang pertama:
```csharp
if (signatures.Count > 0)
{
    ImageSignature imageSignature = signatures[0];
    bool result = signature.Delete(imageSignature);
    if (result)
    {
        Console.WriteLine($"Image signature at location {imageSignature.Left}x{imageSignature.Top} and Size {imageSignature.Size} was deleted from document ['{fileName}'].");
    }
    else
    {
        Helper.WriteError($"Signature was not deleted from the document! Signature at location {imageSignature.Left}x{imageSignature.Top} and Size {imageSignature.Size} was not found!");
    }
}
```
## Kesimpulan
Dalam tutorial ini, kita mempelajari cara menghapus tanda tangan gambar dari dokumen menggunakan GroupDocs.Signature untuk .NET. Dengan mengikuti panduan langkah demi langkah, pengembang dapat mengelola tanda tangan digital secara efisien dalam aplikasi mereka.
## FAQ
### Bisakah saya menghapus beberapa tanda tangan gambar dari sebuah dokumen?
 Ya, Anda dapat mengubah kode untuk menghapus beberapa tanda tangan gambar dengan mengulanginya`signatures` daftar.
### Apakah GroupDocs.Signature mendukung format dokumen lain selain DOCX?
Ya, GroupDocs.Signature mendukung berbagai format dokumen, termasuk PDF, PPT, XLS, dan banyak lagi.
### Apakah ada versi uji coba yang tersedia untuk GroupDocs.Signature untuk .NET?
 Ya, Anda dapat mengunduh versi uji coba gratis dari[situs web](https://releases.groupdocs.com/).
### Bagaimana saya bisa mendapatkan dukungan untuk GroupDocs.Signature?
 Anda dapat mengunjungi[GroupDocs.Forum tanda tangan](https://forum.groupdocs.com/c/signature/13) untuk bantuan dan dukungan.
### Bisakah saya membeli lisensi sementara untuk GroupDocs.Signature?
 Ya, Anda dapat membeli lisensi sementara dari[halaman pembelian](https://purchase.groupdocs.com/temporary-license/).