---
title: Tanda tangani PDF dengan Metadata
linktitle: Tanda tangani PDF dengan Metadata
second_title: GroupDocs.Tanda Tangan .NET API
description: Pelajari cara menandatangani dokumen PDF dengan metadata menggunakan GroupDocs.Signature untuk .NET. Tingkatkan ketertelusuran dan keaslian dokumen dengan mudah.
weight: 11
url: /id/net/document-signing/sign-pdf-with-metadata/
---

# Tanda tangani PDF dengan Metadata

## Perkenalan
Dalam tutorial ini, kita akan mempelajari cara menandatangani dokumen PDF dengan metadata menggunakan GroupDocs.Signature untuk .NET. Menambahkan metadata ke PDF dapat memberikan informasi tambahan tentang dokumen, seperti penulis, tanggal pembuatan, ID dokumen, dan lainnya.
## Prasyarat
Sebelum kita mulai, pastikan Anda memiliki hal berikut:
1.  GroupDocs.Signature untuk .NET: Anda dapat mengunduhnya dari[Di Sini](https://releases.groupdocs.com/signature/net/).
2. Dokumen PDF: Siapkan contoh file PDF untuk ditandatangani.
3. Pengetahuan Dasar Pemrograman C#: Keakraban dengan sintaks C# diperlukan untuk memahami contoh kode.
## Impor Namespace
Pertama, pastikan Anda mengimpor namespace yang diperlukan untuk mengakses kelas dan metode yang diperlukan:
```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## Langkah 1: Muat Dokumen PDF
Muat dokumen PDF yang ingin Anda tandatangani:
```csharp
string filePath = "sample.pdf";
```
## Langkah 2: Tentukan Jalur File Output
Tentukan jalur file keluaran tempat PDF yang ditandatangani dengan metadata akan disimpan:
```csharp
string outputFilePath = Path.Combine("Your Document Directory", "SignPdfWithMetadata", "SignedWithMetadata.pdf");
```
## Langkah 3: Buat Mesin Virtual Tanda Tangan
Inisialisasi instance Tanda Tangan dengan menyediakan jalur ke dokumen PDF:
```csharp
using (Signature signature = new Signature(filePath))
{
    // Kode terkait tanda tangan akan ditempatkan di sini
}
```
## Langkah 4: Tentukan Opsi Metadata
Buat MetadataSignOptions dan tambahkan kolom metadata dengan nilainya masing-masing:
```csharp
MetadataSignOptions options = new MetadataSignOptions();
options
    .Add(new PdfMetadataSignature("Author", "Mr.Sherlock Holmes")) // Nilai string
    .Add(new PdfMetadataSignature("CreatedOn", DateTime.Now))       // Nilai TanggalWaktu
    .Add(new PdfMetadataSignature("DocumentId", 123456))            // Nilai bilangan bulat
    .Add(new PdfMetadataSignature("SignatureId", 123.456D))         // Nilai ganda
    .Add(new PdfMetadataSignature("Amount", 123.456M))              // Nilai desimal
    .Add(new PdfMetadataSignature("Total", 123.456F));              // Nilai mengambang
```
## Langkah 5: Tandatangani Dokumen
Tanda tangani dokumen PDF dengan opsi metadata yang ditentukan dan simpan dokumen yang ditandatangani:
```csharp
SignResult result = signature.Sign(outputFilePath, options);
Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).\nFile saved at {outputFilePath}.");
```

## Kesimpulan
Dalam tutorial ini, kami telah membahas cara menandatangani dokumen PDF dengan metadata menggunakan GroupDocs.Signature untuk .NET. Dengan mengikuti panduan langkah demi langkah, Anda dapat dengan mudah menambahkan informasi metadata seperti penulis, tanggal pembuatan, dan lainnya ke file PDF Anda, sehingga meningkatkan kegunaan dan kemampuan penelusurannya.
## FAQ
### Bisakah saya menambahkan bidang metadata khusus ke dokumen PDF saya?
Ya, Anda dapat menambahkan bidang metadata khusus dengan menentukan nama bidang dan nilainya yang sesuai menggunakan GroupDocs.Signature untuk .NET.
### Apakah GroupDocs.Signature untuk .NET kompatibel dengan semua versi .NET Framework?
GroupDocs.Signature untuk .NET kompatibel dengan berbagai versi .NET Framework, memastikan fleksibilitas dan kemudahan integrasi.
### Apakah GroupDocs.Signature mendukung penandatanganan format dokumen lain selain PDF?
Ya, GroupDocs.Signature mendukung berbagai format dokumen, termasuk Word, Excel, PowerPoint, dan banyak lagi.
### Bisakah saya menandatangani banyak dokumen secara massal menggunakan GroupDocs.Signature untuk .NET?
Ya, Anda dapat menandatangani beberapa dokumen secara massal dengan mengulangi daftar file dan menerapkan proses tanda tangan secara terprogram.
### Apakah dukungan teknis tersedia untuk pengguna GroupDocs.Signature?
 Ya, GroupDocs menyediakan dukungan teknis khusus melalui forumnya. Anda dapat mengakses forum dukungan[Di Sini](https://forum.groupdocs.com/c/signature/13).