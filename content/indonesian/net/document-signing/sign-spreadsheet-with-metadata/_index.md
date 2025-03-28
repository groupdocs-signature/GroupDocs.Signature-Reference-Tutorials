---
title: Tandatangani Spreadsheet dengan Metadata
linktitle: Tandatangani Spreadsheet dengan Metadata
second_title: GroupDocs.Tanda Tangan .NET API
description: Pelajari cara menandatangani spreadsheet dengan metadata menggunakan Groupdocs.Signature untuk .NET. Tingkatkan integritas dan verifikasi dokumen dengan tanda tangan metadata.
weight: 13
url: /id/net/document-signing/sign-spreadsheet-with-metadata/
---

# Tandatangani Spreadsheet dengan Metadata

## Perkenalan
Dalam tutorial ini, kita akan memandu proses penandatanganan spreadsheet dengan metadata menggunakan Groupdocs.Signature untuk .NET. Penandatanganan metadata memungkinkan Anda menyematkan informasi tambahan ke dalam dokumen Anda, memberikan konteks atau verifikasi. Di akhir panduan ini, Anda akan dapat menerapkan tanda tangan metadata ke spreadsheet Anda dengan mudah.
## Prasyarat
Sebelum kita mulai, pastikan Anda memiliki prasyarat berikut:
1.  Groupdocs.Signature untuk .NET: Instal perpustakaan Groupdocs.Signature untuk .NET. Anda dapat mengunduhnya dari[Di Sini](https://releases.groupdocs.com/signature/net/).
2. Lingkungan .NET: Pastikan Anda telah menyiapkan lingkungan .NET di sistem Anda.
3. Dokumen Spreadsheet: Siapkan contoh dokumen spreadsheet yang ingin Anda tanda tangani dengan metadata.
## Impor Namespace
Sebelum mengimplementasikan kode, impor namespace yang diperlukan untuk mengakses kelas dan metode yang diperlukan:
```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
Sekarang, mari kita pecahkan kode contoh menjadi beberapa langkah untuk pemahaman yang lebih jelas:
## Langkah 1: Muat Dokumen Spreadsheet
```csharp
string filePath = "sample.xlsx";
string outputFilePath = Path.Combine("Your Document Directory", "SignSpreadsheetWithMetadata", "SignedWithMetadata.xlsx");
using (Signature signature = new Signature(filePath))
{
```
## Langkah 2: Tentukan Opsi Tanda Metadata
```csharp
	// buat opsi Metadata dengan teks Metadata yang telah ditentukan sebelumnya
	MetadataSignOptions options = new MetadataSignOptions();
```
## Langkah 3: Buat Tanda Tangan Metadata
```csharp
	// Buat beberapa tanda tangan Metadata Spreadsheet
	SpreadsheetMetadataSignature[] signatures = new SpreadsheetMetadataSignature[]
	{
		new SpreadsheetMetadataSignature("Author", "Mr.Scherlock Holmes"), // Nilai string
		new SpreadsheetMetadataSignature("CreatedOn", DateTime.Now), // Nilai TanggalWaktu
		new SpreadsheetMetadataSignature("DocumentId", 123456), // Nilai bilangan bulat
		new SpreadsheetMetadataSignature("SignatureId", 123.456D), // Nilai ganda
		new SpreadsheetMetadataSignature("Amount", 123.456M), // Nilai desimal
		new SpreadsheetMetadataSignature("Total", 123.456F) // Nilai mengambang
	};
	options.Signatures.AddRange(signatures);
```
## Langkah 4: Tandatangani Dokumen
```csharp
	// menandatangani dokumen ke file
	SignResult result = signature.Sign(outputFilePath, options);
	Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).\nFile saved at {outputFilePath}.");
}
```
## Kesimpulan
Selamat! Anda telah mempelajari cara menandatangani spreadsheet dengan metadata menggunakan Groupdocs.Signature untuk .NET. Penandatanganan metadata meningkatkan integritas dokumen dan memberikan informasi tambahan untuk tujuan verifikasi. Mulai terapkan tanda tangan metadata ke spreadsheet Anda sekarang dan pastikan keaslian dan konteks dokumen Anda.
## FAQ
### Apa yang dimaksud dengan penandatanganan metadata?
Penandatanganan metadata melibatkan penyematan informasi tambahan, seperti nama penulis, tanggal pembuatan, atau ID dokumen, ke dalam dokumen untuk tujuan verifikasi.
### Bisakah saya menyesuaikan tanda tangan metadata?
Ya, Anda dapat menyesuaikan tanda tangan metadata sesuai kebutuhan Anda, termasuk teks, tanggal, bilangan bulat, ganda, desimal, dan float.
### Apakah Groupdocs.Signature untuk .NET kompatibel dengan format dokumen lain?
Ya, Groupdocs.Signature untuk .NET mendukung berbagai format dokumen, termasuk spreadsheet, presentasi, PDF, dan banyak lagi.
### Bagaimana cara memverifikasi tanda tangan metadata?
Anda dapat memverifikasi tanda tangan metadata menggunakan Groupdocs.Signature atau perangkat lunak kompatibel lainnya yang mendukung ekstraksi metadata.
### Bisakah saya menerapkan tanda tangan metadata secara terprogram?
Ya, Anda dapat menerapkan tanda tangan metadata secara terprogram menggunakan pustaka Groupdocs.Signature untuk .NET dalam aplikasi .NET Anda.