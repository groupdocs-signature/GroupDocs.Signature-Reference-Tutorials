---
title: Tanda Tangani Presentasi dengan Metadata
linktitle: Tanda Tangani Presentasi dengan Metadata
second_title: GroupDocs.Tanda Tangan .NET API
description: Pelajari cara menandatangani file presentasi dengan metadata menggunakan GroupDocs.Signature untuk .NET. Tingkatkan integritas dokumen dan tambahkan informasi berharga.
weight: 12
url: /id/net/document-signing/sign-presentation-with-metadata/
---

# Tanda Tangani Presentasi dengan Metadata

## Perkenalan
Dalam tutorial ini, kita akan mempelajari cara menandatangani file presentasi (PPTX) dengan metadata menggunakan pustaka GroupDocs.Signature untuk .NET. Menandatangani presentasi dengan metadata menambahkan informasi berharga pada dokumen, seperti nama penulis, tanggal pembuatan, ID dokumen, ID tanda tangan, dan berbagai nilai numerik.
## Prasyarat
Sebelum kita mulai, pastikan Anda memiliki hal berikut:
1.  GroupDocs.Signature untuk .NET Library: Unduh dan instal perpustakaan dari[Di Sini](https://releases.groupdocs.com/signature/net/).
2. Lingkungan Pengembangan: Pastikan Anda telah menyiapkan lingkungan pengembangan .NET.
3. File Presentasi: Siapkan contoh file presentasi (format PPTX) untuk ditandatangani.
4. Pemahaman Dasar C#: Keakraban dengan bahasa pemrograman C# akan bermanfaat.

## Impor Namespace
Sebelum mendalami kodenya, mari impor namespace yang diperlukan:
```csharp
using System;
using System.IO;
    using GroupDocs.Signature;
    using GroupDocs.Signature.Domain;
    using GroupDocs.Signature.Options;
```
## Langkah 1: Muat File Presentasi
```csharp
string filePath = "sample.pptx";
```
 Mengganti`"sample.pptx"` dengan jalur ke file presentasi Anda.
## Langkah 2: Tentukan Jalur File Output
```csharp
string outputFilePath = Path.Combine("Your Document Directory", "SignPresentationWithMetadata", "SignedWithMetadata.pptx");
```
Tentukan direktori tempat Anda ingin menyimpan file presentasi yang telah ditandatangani beserta nama filenya.
## Langkah 3: Inisialisasi Objek Tanda Tangan
```csharp
using (Signature signature = new Signature(filePath))
```
Inisialisasi objek Tanda Tangan dengan menyediakan jalur ke file presentasi.
## Langkah 4: Tentukan Opsi Tanda Metadata
```csharp
MetadataSignOptions options = new MetadataSignOptions();
```
Buat instance MetadataSignOptions untuk menentukan opsi penandatanganan metadata.
## Langkah 5: Buat Tanda Tangan Metadata
```csharp
PresentationMetadataSignature[] signatures = new PresentationMetadataSignature[]
{
    new PresentationMetadataSignature("Author", "Mr.Scherlock Holmes"),
    new PresentationMetadataSignature("CreatedOn", DateTime.Now),
    new PresentationMetadataSignature("DocumentId", 123456),
    new PresentationMetadataSignature("SignatureId", 123.456D),
    new PresentationMetadataSignature("Amount", 123.456M),
    new PresentationMetadataSignature("Total", 123.456F)
};
```
Buat array objek PresentationMetadataSignature, masing-masing mewakili tanda tangan metadata. Anda dapat menambahkan berbagai jenis metadata, termasuk string, DateTime, integer, double, desimal, dan float.
## Langkah 6: Tambahkan Tanda Tangan ke Opsi
```csharp
options.Signatures.AddRange(signatures);
```
Tambahkan tanda tangan metadata yang dibuat ke objek MetadataSignOptions.
## Langkah 7: Tanda Tangani Dokumen
```csharp
SignResult result = signature.Sign(outputFilePath, options);
```
Tanda tangani file presentasi dengan metadata menggunakan opsi yang ditentukan dan simpan file yang ditandatangani ke jalur keluaran.
## Langkah 8: Tampilkan Hasil
```csharp
Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).\nFile saved at {outputFilePath}.");
```
Menampilkan pesan sukses beserta jumlah tanda tangan yang diterapkan dan jalur penyimpanan file yang ditandatangani.

## Kesimpulan
Dalam tutorial ini, kita telah mempelajari cara menandatangani file presentasi dengan metadata menggunakan pustaka GroupDocs.Signature untuk .NET. Menambahkan tanda tangan metadata akan meningkatkan integritas dokumen dan memberikan informasi berharga tentang kontennya.

## FAQ
### Bisakah saya menandatangani format dokumen lain selain PPTX dengan metadata menggunakan GroupDocs.Signature untuk .NET?
Ya, GroupDocs.Signature mendukung berbagai format dokumen, termasuk Word, Excel, PDF, dan lainnya, untuk penandatanganan dengan metadata.
### Apakah GroupDocs.Signature untuk .NET kompatibel dengan .NET Core?
Ya, perpustakaan ini kompatibel dengan .NET Framework dan .NET Core.
### Bisakah saya menyesuaikan tampilan tanda tangan metadata?
Ya, Anda dapat menyesuaikan tampilan, posisi, dan properti tanda tangan metadata lainnya sesuai dengan kebutuhan Anda.
### Apakah GroupDocs.Signature untuk .NET menyediakan enkripsi untuk dokumen yang ditandatangani?
Ya, GroupDocs.Signature menawarkan opsi enkripsi untuk mengamankan dokumen yang ditandatangani dari akses tidak sah.
### Apakah ada versi uji coba yang tersedia untuk pengujian sebelum membeli?
 Ya, Anda dapat memanfaatkan uji coba gratis GroupDocs.Signature untuk .NET dari[Di Sini](https://releases.groupdocs.com/).