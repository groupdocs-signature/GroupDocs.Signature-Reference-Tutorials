---
title: Menandatangani dengan Teks menggunakan GroupDocs.Signature untuk .NET
linktitle: Menandatangani dengan Teks
second_title: GroupDocs.Tanda Tangan .NET API
description: Pelajari cara menandatangani dokumen dengan teks menggunakan GroupDocs.Signature untuk .NET. Panduan langkah demi langkah untuk menambahkan tanda tangan teks secara terprogram.
weight: 17
url: /id/net/advanced-signature-techniques/sign-with-text/
---

# Menandatangani dengan Teks menggunakan GroupDocs.Signature untuk .NET

## Perkenalan
Di era digital, menandatangani dokumen secara elektronik telah menjadi praktik standar, sehingga menghemat waktu dan sumber daya. GroupDocs.Signature untuk .NET menawarkan solusi komprehensif untuk menambahkan tanda tangan teks ke berbagai format dokumen secara terprogram. Dalam tutorial ini, kami akan memandu Anda melalui proses penandatanganan dokumen dengan teks menggunakan GroupDocs.Signature untuk .NET.
## Prasyarat
Sebelum kita masuk ke tutorialnya, pastikan Anda memiliki prasyarat berikut:
1.  GroupDocs.Signature untuk .NET: Pastikan Anda telah menginstal perpustakaan GroupDocs.Signature untuk .NET. Anda dapat mengunduhnya dari[Di Sini](https://releases.groupdocs.com/signature/net/).
2. Lingkungan Pengembangan: Siapkan lingkungan kerja untuk pengembangan .NET.
3. Dokumen: Siapkan dokumen (misalnya PDF, Word) yang ingin Anda tanda tangani dengan teks.

## Impor Namespace
Pertama, Anda perlu mengimpor namespace yang diperlukan ke proyek .NET Anda untuk menggunakan fungsionalitas GroupDocs.Signature.
```csharp
using System;
using System.IO;
using System.Drawing;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

Mari kita uraikan proses penandatanganan dokumen dengan teks menjadi beberapa langkah:
## Langkah 1: Muat Dokumen
Muat dokumen yang ingin Anda tandatangani dengan teks.
```csharp
string filePath = "sample.pdf"; // Jalur ke dokumen
string fileName = Path.GetFileName(filePath);
```
## Langkah 2: Tetapkan Jalur File Output
Tentukan jalur file keluaran tempat dokumen yang ditandatangani akan disimpan.
```csharp
string outputFilePath = Path.Combine("Your Document Directory", "SignWithText", fileName);
```
## Langkah 3: Buat Opsi Tanda Tangan
Atur opsi untuk tanda tangan teks, termasuk konten teks, posisi, ukuran, warna, dan font.
```csharp
TextSignOptions options = new TextSignOptions("John Smith")
{
    Left = 50, // Tetapkan posisi tanda tangan
    Top = 200,
    Width = 100, // Tetapkan persegi panjang tanda tangan
    Height = 30,
    ForeColor = Color.Red, // Atur warna teks
    Font = new SignatureFont { Size = 14, FamilyName = "Comic Sans MS" } // Atur font
};
```
## Langkah 4: Tanda Tangani Dokumen
Gunakan GroupDocs.Signature untuk menandatangani dokumen dengan opsi yang ditentukan dan menyimpan dokumen yang ditandatangani ke jalur file keluaran.
```csharp
using (Signature signature = new Signature(filePath))
{
    SignResult result = signature.Sign(outputFilePath, options); // Tanda tangani dokumen
    Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).\nFile saved at {outputFilePath}.");
}
```

## Kesimpulan
Dalam tutorial ini, kita telah mempelajari cara menandatangani dokumen dengan teks menggunakan GroupDocs.Signature untuk .NET. Dengan mengikuti langkah-langkah ini, Anda dapat secara efisien menambahkan tanda tangan teks ke dokumen Anda secara terprogram, sehingga meningkatkan keamanan dan keaslian.
## FAQ
### Bisakah saya menyesuaikan tampilan tanda tangan teks?
Ya, Anda dapat menyesuaikan berbagai parameter seperti warna, font, ukuran, dan posisi tanda tangan teks sesuai preferensi Anda.
### Apakah GroupDocs.Signature kompatibel dengan berbagai format dokumen?
Ya, GroupDocs.Signature mendukung berbagai format dokumen termasuk PDF, Word, Excel, PowerPoint, dan lainnya.
### Bisakah saya menambahkan beberapa tanda tangan teks ke satu dokumen?
Tentu saja, Anda dapat menambahkan beberapa tanda tangan teks ke dokumen, masing-masing dengan serangkaian opsi penyesuaiannya sendiri.
### Apakah GroupDocs.Signature memastikan integritas dokumen setelah penandatanganan?
Ya, GroupDocs.Signature menggunakan algoritme kriptografi yang kuat untuk memastikan integritas dokumen dan mencegah gangguan setelah penandatanganan.
### Apakah ada versi uji coba yang tersedia untuk pengujian sebelum membeli?
 Ya, Anda dapat mengunduh versi uji coba gratis dari[Di Sini](https://releases.groupdocs.com/) untuk menjelajahi fitur sebelum melakukan pembelian.