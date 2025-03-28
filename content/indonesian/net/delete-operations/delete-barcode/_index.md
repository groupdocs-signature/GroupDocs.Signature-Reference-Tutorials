---
title: Hapus Barcode dari Dokumen
linktitle: Hapus Barcode dari Dokumen
second_title: GroupDocs.Tanda Tangan .NET API
description: Pelajari cara menghapus kode batang dari dokumen menggunakan GroupDocs.Signature untuk .NET. Panduan langkah demi langkah dengan contoh kode.
weight: 10
url: /id/net/delete-operations/delete-barcode/
---

# Hapus Barcode dari Dokumen

## Perkenalan
GroupDocs.Signature for .NET adalah perpustakaan canggih yang memungkinkan pengembang bekerja dengan lancar dengan tanda tangan digital, stempel, dan kode batang dalam aplikasi .NET. Dalam tutorial ini, kami akan memandu Anda melalui proses menghapus kode batang dari dokumen menggunakan GroupDocs.Signature untuk .NET.
## Prasyarat
Sebelum kita mulai, pastikan Anda memiliki prasyarat berikut:
- Pengetahuan dasar bahasa pemrograman C#.
- Visual Studio diinstal pada sistem Anda.
-  GroupDocs.Signature untuk perpustakaan .NET diinstal. Anda dapat mengunduhnya dari[Di Sini](https://releases.groupdocs.com/signature/net/).
- Contoh dokumen dengan kode batang yang ingin Anda hapus.

## Impor Namespace
Pertama, pastikan untuk mengimpor namespace yang diperlukan ke dalam kode C# Anda:
```csharp
using System;
using System.IO;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

Mari kita uraikan proses menghapus kode batang dari dokumen menjadi langkah-langkah sederhana:
## Langkah 1: Tentukan Jalur File
```csharp
string filePath = "sample_multiple_signatures.docx";
string fileName = Path.GetFileName(filePath);
string outputFilePath = Path.Combine("Your Document Directory", "DeleteBarcode", fileName);
```
 Pastikan untuk mengganti`"sample_multiple_signatures.docx"` dengan jalur ke dokumen Anda yang berisi kode batang.
## Langkah 2: Salin File Sumber
```csharp
File.Copy(filePath, outputFilePath, true);
```
Langkah ini memastikan bahwa kita bekerja dengan salinan dokumen asli untuk melestarikan file asli.
## Langkah 3: Inisialisasi GroupDocs.Signature
```csharp
using (Signature signature = new Signature(outputFilePath))
{
    // Kode Anda ada di sini
}
```
Inisialisasi objek Tanda Tangan dengan meneruskan jalur ke salinan dokumen yang dibuat pada langkah sebelumnya.
## Langkah 4: Cari Tanda Tangan Barcode
```csharp
BarcodeSearchOptions options = new BarcodeSearchOptions();
List<BarcodeSignature> signatures = signature.Search<BarcodeSignature>(options);
```
Buat instance BarcodeSearchOptions dan gunakan untuk mencari tanda tangan barcode di dalam dokumen.
## Langkah 5: Hapus Tanda Tangan Barcode
```csharp
if (signatures.Count > 0)
{
    BarcodeSignature barcodeSignature = signatures[0];
    bool result = signature.Delete(barcodeSignature);
    if (result)
    {
        Console.WriteLine($"Signature with Barcode '{barcodeSignature.Text}' and encode type '{barcodeSignature.EncodeType.TypeName}' was deleted from document ['{fileName}'].");
    }
    else
    {
        Helper.WriteError($"Signature was not deleted from the document! Signature with Barcode '{barcodeSignature.Text}' and encode type '{barcodeSignature.EncodeType.TypeName}' was not found!");
    }
}
```
Periksa apakah tanda tangan kode batang ditemukan di dokumen. Jika ditemukan, hapus tanda tangan barcode pertama yang ditemukan.

## Kesimpulan
Dalam tutorial ini, kita telah mempelajari cara menghapus kode batang dari dokumen menggunakan GroupDocs.Signature untuk .NET. Dengan mengikuti panduan langkah demi langkah, Anda dapat dengan mudah mengintegrasikan fungsi penghapusan kode batang ke dalam aplikasi .NET Anda.
## FAQ
### Bisakah saya menghapus beberapa tanda tangan kode batang dari sebuah dokumen?
Ya, Anda dapat mengubah kode untuk menghapus beberapa tanda tangan kode batang dengan mengulangi daftar tanda tangan.
### Apakah GroupDocs.Signature untuk .NET mendukung jenis tanda tangan lainnya?
Ya, GroupDocs.Signature untuk .NET mendukung berbagai jenis tanda tangan, termasuk tanda tangan digital, stempel, dan tanda tangan teks.
### Bisakah saya menyesuaikan opsi pencarian untuk tanda tangan kode batang?
Ya, Anda dapat menyesuaikan opsi pencarian sesuai kebutuhan Anda, seperti menentukan jenis kode batang atau area pencarian dalam dokumen.
### Apakah GroupDocs.Signature untuk .NET kompatibel dengan berbagai format dokumen?
Ya, GroupDocs.Signature untuk .NET mendukung berbagai format dokumen, termasuk Word, Excel, PDF, dan banyak lagi.
### Di mana saya dapat menemukan dukungan atau sumber daya tambahan untuk GroupDocs.Signature untuk .NET?
 Anda dapat mengunjungi forum GroupDocs.Signature[Di Sini](https://forum.groupdocs.com/c/signature/13) untuk pertanyaan atau bantuan apa pun mengenai perpustakaan.