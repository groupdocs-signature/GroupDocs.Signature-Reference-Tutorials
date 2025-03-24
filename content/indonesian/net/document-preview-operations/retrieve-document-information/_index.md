---
title: Ambil Informasi Dokumen
linktitle: Ambil Informasi Dokumen
second_title: GroupDocs.Tanda Tangan .NET API
description: Tingkatkan manajemen dokumen di .NET dengan GroupDocs.Signature. Ambil info dokumen langkah demi langkah. Mendukung berbagai format.
weight: 11
url: /id/net/document-preview-operations/retrieve-document-information/
---

# Ambil Informasi Dokumen

## Perkenalan
Dalam bidang dokumentasi digital, memastikan keaslian dan integritas adalah hal yang terpenting. GroupDocs.Signature untuk .NET memberikan solusi tangguh untuk mengelola tanda tangan dokumen dalam lingkungan .NET. Dalam tutorial ini, kami mempelajari proses mengambil informasi dokumen menggunakan GroupDocs.Signature untuk .NET, menguraikan setiap langkah untuk pemahaman yang komprehensif.
## Prasyarat
Sebelum masuk ke tutorial, pastikan Anda memiliki prasyarat berikut:
1.  Instalasi: Instal GroupDocs.Signature untuk .NET dengan mengunduhnya dari[Di Sini](https://releases.groupdocs.com/signature/net/).
2. Lingkungan .NET: Memiliki pengetahuan tentang kerangka .NET.
3. Dokumen: Siapkan contoh dokumen (misalnya, "sample_multiple_signatures.docx") untuk tujuan pengujian.

## Mengimpor Namespace
Sebelum melanjutkan proses pengambilan tanda tangan dokumen, impor namespace yang diperlukan:
```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
```

## Langkah 1: Tetapkan Jalur File Dokumen:
Tentukan jalur file untuk dokumen yang ingin Anda ambil informasinya.
```csharp
string filePath = "sample_multiple_signatures.docx";
```
## Langkah 2: Buat Instansiasi Objek Tanda Tangan:
 Buat sebuah instance dari`Signature` kelas dengan melewati jalur file dokumen.
```csharp
using (Signature signature = new Signature(filePath))
{

}
```
## Langkah 3: Ambil Informasi Dokumen:
 Memanfaatkan`GetDocumentInfo()` metode untuk mengambil informasi komprehensif tentang dokumen.
```csharp
IDocumentInfo documentInfo = signature.GetDocumentInfo();
```
## Langkah 4: Tampilkan Properti Dokumen:
Keluarkan berbagai properti dokumen seperti format, ekstensi, ukuran, jumlah halaman, dll.
```csharp
Console.WriteLine($"Document properties {Path.GetFileName(filePath)}:");
Console.WriteLine($" - format : {documentInfo.FileType.FileFormat}");
Console.WriteLine($" - extension : {documentInfo.FileType.Extension}");
Console.WriteLine($" - size : {documentInfo.Size}");
Console.WriteLine($" - page count : {documentInfo.PageCount}");
Console.WriteLine($" - Form Fields count : {documentInfo.FormFields.Count}");
Console.WriteLine($" - Text signatures count : {documentInfo.TextSignatures.Count}");
Console.WriteLine($" - Image signatures count : {documentInfo.ImageSignatures.Count}");
Console.WriteLine($" - Digital signatures count : {documentInfo.DigitalSignatures.Count}");
Console.WriteLine($" - Barcode signatures count : {documentInfo.BarcodeSignatures.Count}");
Console.WriteLine($" - QrCode signatures count : {documentInfo.QrCodeSignatures.Count}");
Console.WriteLine($" - FormField signatures count : {documentInfo.FormFieldSignatures.Count}");
foreach (PageInfo pageInfo in documentInfo.Pages)
{
   Console.WriteLine($" - page-{pageInfo.PageNumber} Width {pageInfo.Width}, Height {pageInfo.Height}");
}
```


## Kesimpulan
GroupDocs.Signature untuk .NET menawarkan serangkaian alat canggih untuk mengelola tanda tangan dokumen dengan lancar dalam kerangka .NET. Dengan mengikuti langkah-langkah yang diuraikan dalam panduan ini, Anda dapat mengambil informasi komprehensif tentang dokumen Anda secara efisien, sehingga memfasilitasi peningkatan kemampuan manajemen dokumen.

## FAQ
### Bisakah GroupDocs.Signature untuk .NET menangani berbagai format dokumen?
Ya, GroupDocs.Signature mendukung berbagai format dokumen, termasuk namun tidak terbatas pada DOCX, PDF, PNG, dan JPEG.
### Apakah ada versi uji coba yang tersedia untuk GroupDocs.Signature untuk .NET?
 Ya, Anda dapat mengakses versi uji coba dari[Di Sini](https://releases.groupdocs.com/).
### Apakah GroupDocs.Signature untuk .NET menyediakan dukungan untuk tanda tangan digital?
Tentu saja, GroupDocs.Signature menawarkan dukungan kuat untuk tanda tangan digital, memastikan keaslian dan integritas dokumen.
### Di mana saya dapat menemukan dokumentasi dan dukungan tambahan untuk GroupDocs.Signature untuk .NET?
 Anda dapat merujuk ke dokumentasi komprehensif[Di Sini](https://tutorials.groupdocs.com/signature/net/) , dan untuk dukungan, kunjungi forum GroupDocs[Di Sini](https://forum.groupdocs.com/c/signature/13).
### Bisakah lisensi sementara diperoleh untuk GroupDocs.Signature untuk .NET?
 Ya, lisensi sementara tersedia untuk dibeli[Di Sini](https://purchase.groupdocs.com/temporary-license/).