---
title: Hapus Banyak Tanda Tangan dari Dokumen
linktitle: Hapus Banyak Tanda Tangan dari Dokumen
second_title: GroupDocs.Tanda Tangan .NET API
description: Hapus beberapa tanda tangan dari dokumen dengan mudah menggunakan GroupDocs.Signature untuk .NET. Sederhanakan alur kerja manajemen dokumen Anda.
type: docs
weight: 15
url: /id/net/delete-operations/delete-multiple-signatures/
---
## Perkenalan
Di dunia digital, pengelolaan dokumen seringkali melibatkan penanganan berbagai tanda tangan. Menghapus banyak tanda tangan dari dokumen secara terprogram dapat menyederhanakan alur kerja dan meningkatkan efisiensi. Dengan GroupDocs.Signature untuk .NET, tugas ini menjadi lancar dan mudah. Tutorial ini akan memandu Anda melalui proses menghapus banyak tanda tangan dari dokumen langkah demi langkah.
## Prasyarat
Sebelum masuk ke tutorial, pastikan Anda memiliki prasyarat berikut:
- Pemahaman dasar bahasa pemrograman C#.
- Menginstal GroupDocs.Signature untuk perpustakaan .NET.
- Contoh dokumen dengan banyak tanda tangan untuk pengujian.

## Impor Namespace
Mulailah dengan mengimpor namespace yang diperlukan untuk mengakses fungsionalitas GroupDocs.Signature untuk .NET:
```csharp
using System;
using System.IO;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## Langkah 1: Tentukan Jalur Dokumen dan Nama File
Tetapkan jalur file dokumen yang berisi banyak tanda tangan. Pastikan Anda memiliki jalur file dan nama file yang sesuai:
```csharp
string filePath = "sample_multiple_signatures.docx";
string fileName = Path.GetFileName(filePath);
```
## Langkah 2: Salin Dokumen untuk Diproses
Untuk menghindari modifikasi dokumen asli, buat salinan untuk diproses:
```csharp
string outputFilePath = Path.Combine("Your Document Directory", "DeleteMultiple", fileName);
File.Copy(filePath, outputFilePath, true);
```
## Langkah 3: Inisialisasi Objek Tanda Tangan
Buat instance objek Tanda Tangan menggunakan jalur file keluaran:
```csharp
using (Signature signature = new Signature(outputFilePath))
{
    // Kode pemrosesan tanda tangan ada di sini
}
```
## Langkah 4: Tentukan Opsi Pencarian
Tentukan berbagai opsi pencarian untuk mengidentifikasi tanda tangan dalam dokumen. Pilihannya mencakup pencarian teks, pencarian gambar, pencarian kode batang, dan pencarian kode QR:
```csharp
TextSearchOptions textSearchOptions = new TextSearchOptions();
ImageSearchOptions imageSearchOptions = new ImageSearchOptions();
BarcodeSearchOptions barcodeOptions = new BarcodeSearchOptions();
QrCodeSearchOptions qrCodeOptions = new QrCodeSearchOptions();
// Tambahkan opsi ke daftar
List<SearchOptions> listOptions = new List<SearchOptions>();
listOptions.Add(textSearchOptions);
listOptions.Add(imageSearchOptions);
listOptions.Add(barcodeOptions);
listOptions.Add(qrCodeOptions);
```
## Langkah 5: Cari Tanda Tangan
Jalankan operasi pencarian untuk menemukan semua tanda tangan dalam dokumen berdasarkan opsi pencarian yang ditentukan:
```csharp
SearchResult result = signature.Search(listOptions);
```
## Langkah 6: Hapus Tanda Tangan
Jika tanda tangan ditemukan, lanjutkan untuk menghapusnya:
```csharp
if (result.Signatures.Count > 0)
{
    // Cobalah untuk menghapus semua tanda tangan
    DeleteResult deleteResult = signature.Delete(result.Signatures);
    //Periksa apakah penghapusan berhasil
    if(deleteResult.Succeeded.Count == result.Signatures.Count)
    {
        Console.WriteLine("\nAll signatures were successfully deleted!");                        
    }
    else
    {
        Console.WriteLine($"Successfully deleted signatures : {deleteResult.Succeeded.Count}");
        Helper.WriteError($"Not deleted signatures : {deleteResult.Failed.Count}");
    }
    // Menampilkan informasi tentang tanda tangan yang dihapus
    Console.WriteLine("\nList of deleted signatures:");
    int number = 1;
    foreach(BaseSignature temp in deleteResult.Succeeded)
    {
        Console.WriteLine($"Signature #{number++}: Type: {temp.SignatureType} Id:{temp.SignatureId}, Location: {temp.Left}x{temp.Top}. Size: {temp.Width}x{temp.Height}");
    }
}
else
{
    Helper.WriteError("No one signature was found.");
}
```

## Kesimpulan
Menghapus banyak tanda tangan dari dokumen secara terprogram adalah tugas penting dalam manajemen dokumen. Dengan GroupDocs.Signature untuk .NET, proses ini menjadi efisien dan andal. Dengan mengikuti langkah-langkah yang diuraikan dalam tutorial ini, Anda dapat dengan mudah mengintegrasikan fungsionalitas penghapusan tanda tangan ke dalam aplikasi .NET Anda.
## FAQ
### Bisakah GroupDocs.Signature untuk .NET menangani berbagai format dokumen?
Ya, GroupDocs.Signature untuk .NET mendukung berbagai format dokumen, termasuk DOCX, PDF, PPTX, XLSX, dan banyak lagi.
### Apakah mungkin untuk menyesuaikan opsi pencarian untuk deteksi tanda tangan?
Tentu saja, Anda dapat menyesuaikan opsi pencarian seperti pencarian teks, pencarian gambar, pencarian kode batang, dan pencarian kode QR untuk memenuhi kebutuhan spesifik Anda.
### Apakah GroupDocs.Signature untuk .NET menyediakan mekanisme penanganan kesalahan?
Ya, perpustakaan menawarkan kemampuan penanganan kesalahan yang kuat untuk memastikan kelancaran pelaksanaan tugas pemrosesan dokumen.
### Bisakah saya mengintegrasikan GroupDocs.Signature untuk .NET dengan perpustakaan pihak ketiga lainnya?
Tentu saja, GroupDocs.Signature untuk .NET dirancang untuk berintegrasi secara mulus dengan pustaka .NET lainnya, memberikan fleksibilitas dan ekstensibilitas.
### Di mana saya dapat menemukan dukungan dan sumber daya tambahan untuk GroupDocs.Signature untuk .NET?
 Anda dapat mengunjungi GroupDocs[forum](https://forum.groupdocs.com/c/signature/13) didedikasikan untuk diskusi terkait tanda tangan dan mencari bantuan dari komunitas dan para ahli.