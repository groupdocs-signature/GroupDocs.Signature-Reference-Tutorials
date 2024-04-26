---
title: Menandatangani Dokumen dengan Kode QR menggunakan GroupDocs.Signature
linktitle: Menandatangani dengan Kode QR
second_title: GroupDocs.Tanda Tangan .NET API
description: Pelajari cara menambahkan tanda tangan kode QR ke dokumen Anda dengan GroupDocs.Signature untuk .NET. Tingkatkan keamanan dan autentikasi dengan mudah.
type: docs
weight: 15
url: /id/net/advanced-signature-techniques/sign-with-qr-code/
---
## Perkenalan
Dalam tutorial ini, kita akan memandu proses penandatanganan dokumen dengan kode QR menggunakan GroupDocs.Signature untuk .NET. GroupDocs.Signature for .NET adalah API canggih yang memungkinkan pengembang menambahkan berbagai jenis tanda tangan ke dokumen digital secara terprogram. Menandatangani dokumen dengan kode QR dapat memberikan lapisan keamanan dan autentikasi tambahan pada dokumen Anda.
## Prasyarat
Sebelum kita mulai, pastikan Anda telah menginstal prasyarat berikut:
1.  GroupDocs.Signature untuk .NET: Anda dapat mengunduh perpustakaan dari[situs web](https://releases.groupdocs.com/signature/net/).
2. Lingkungan Pengembangan: Pastikan Anda telah menyiapkan lingkungan pengembangan .NET di mesin Anda.
3. Contoh Dokumen: Siapkan contoh dokumen (misalnya PDF) yang ingin Anda tanda tangani dengan kode QR.

## Mengimpor Namespace yang Diperlukan
Sebelum mendalami kodenya, mari impor namespace yang diperlukan:
```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

## Langkah 1: Tentukan Jalur File
```csharp
string filePath = "sample.pdf";
string fileName = Path.GetFileName(filePath);
string outputFilePath = Path.Combine("Your Document Directory", "SignWithQRCode", fileName);
```
 Pastikan untuk mengganti`"Your Document Directory"` dengan jalur ke direktori tempat Anda ingin menyimpan dokumen yang ditandatangani.
## Langkah 2: Inisialisasi Objek Tanda Tangan
```csharp
using (Signature signature = new Signature(filePath))
{
    //Kode untuk penandatanganan ada di sini
}
```
 Inisialisasi a`Signature` objek dengan jalur ke dokumen yang ingin Anda tandatangani.
## Langkah 3: Buat QRCodeSignOptions
```csharp
QrCodeSignOptions options = new QrCodeSignOptions("JohnSmith")
{
    EncodeType = QrCodeTypes.QR,
    Left = 50,
    Top = 150,
    Width = 200,
    Height = 200
};
```
 Membuat`QrCodeSignOptions` objek dengan pengaturan yang diinginkan untuk tanda tangan kode QR. Anda dapat menyesuaikan parameter seperti teks yang akan dikodekan, posisi, dan dimensi kode QR.
## Langkah 4: Tandatangani Dokumen
```csharp
SignResult result = signature.Sign(outputFilePath, options);
```
 Menggunakan`Sign` metode`Signature` keberatan untuk menandatangani dokumen dengan opsi yang ditentukan. Metode ini mengembalikan a`SignResult` objek yang berisi informasi tentang proses penandatanganan.
## Langkah 5: Tampilkan Hasil
```csharp
Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).\nFile saved at {outputFilePath}.");
```
Menampilkan pesan yang menunjukkan keberhasilan proses penandatanganan dan lokasi penyimpanan dokumen yang ditandatangani.

## Kesimpulan
Dalam tutorial ini, kita telah mempelajari cara menandatangani dokumen dengan kode QR menggunakan GroupDocs.Signature untuk .NET. Dengan mengikuti langkah-langkah sederhana ini, Anda dapat menambahkan tanda tangan kode QR ke dokumen digital Anda, sehingga meningkatkan keamanan dan autentikasi.

## FAQ
### Bisakah saya menyesuaikan tampilan kode QR?
Ya, Anda dapat menyesuaikan berbagai parameter seperti ukuran, posisi, dan jenis pengkodean kode QR sesuai kebutuhan Anda.
### Format dokumen apa yang didukung untuk penandatanganan dengan kode QR?
GroupDocs.Signature untuk .NET mendukung berbagai format dokumen, termasuk PDF, Word, Excel, PowerPoint, dan banyak lagi.
### Apakah mungkin untuk menandatangani banyak dokumen dalam proses batch?
Tentu saja, Anda dapat menggunakan GroupDocs.Signature untuk .NET untuk menandatangani beberapa dokumen secara bersamaan, sehingga menyederhanakan alur kerja Anda.
### Bisakah saya memverifikasi keaslian dokumen yang ditandatangani dengan kode QR?
Ya, GroupDocs.Signature untuk .NET menyediakan mekanisme verifikasi untuk memastikan integritas dan keaslian dokumen yang ditandatangani.
### Apakah ada versi uji coba yang tersedia untuk menguji fungsionalitasnya sebelum membeli?
 Ya, Anda dapat mengunduh versi uji coba gratis dari[situs web](https://releases.groupdocs.com/) untuk mengevaluasi fitur dan kemampuan GroupDocs.Signature untuk .NET.