---
title: Menandatangani dengan Banyak Pilihan
linktitle: Menandatangani dengan Banyak Pilihan
second_title: GroupDocs.Tanda Tangan .NET API
description: Pelajari cara menandatangani dokumen dengan beberapa opsi menggunakan GroupDocs.Signature untuk .NET. Tingkatkan keamanan dokumen dengan teks, barcode, kode QR, digital dan gambar.
weight: 14
url: /id/net/advanced-signature-techniques/sign-with-multiple-options/
---
## Perkenalan
Dalam tutorial ini, kita akan mempelajari cara menandatangani dokumen menggunakan beberapa opsi tanda tangan menggunakan perpustakaan GroupDocs.Signature untuk .NET. Menandatangani dokumen dengan berbagai opsi seperti tanda tangan teks, kode batang, kode QR, digital, gambar, dan metadata dapat memberikan keserbagunaan dan meningkatkan keamanan dokumen.
## Prasyarat
Sebelum memulai, pastikan Anda memiliki prasyarat berikut:
1.  GroupDocs.Signature untuk .NET Library: Unduh dan instal perpustakaan GroupDocs.Signature untuk .NET dari[Di Sini](https://releases.groupdocs.com/signature/net/).
2. Lingkungan Pengembangan: Siapkan lingkungan pengembangan dengan .NET Framework terinstal.
3. Dokumen yang Akan Ditandatangani: Siapkan dokumen (misalnya sample.docx) yang ingin Anda tanda tangani.
4. Sertifikat dan Gambar: Siapkan sertifikat dan gambar yang diperlukan untuk tanda tangan digital dan gambar.

## Impor Namespace
Pertama, impor namespace yang diperlukan untuk menggunakan perpustakaan GroupDocs.Signature di aplikasi .NET Anda:
```csharp
using System;
using System.IO;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## Langkah 1: Muat Dokumen
```csharp
string filePath = "sample.docx";
string outputFilePath = Path.Combine("Your Document Directory", "SignWithMultiple", "SignWithMultiple.docx");
using (Signature signature = new Signature(filePath))
{
    // Kode Anda berlanjut...
}
```
## Langkah 2: Tentukan Opsi Tanda Tangan
Tentukan beberapa opsi tanda tangan dari berbagai jenis dan pengaturan, seperti tanda tangan teks, kode batang, kode QR, digital, gambar, dan metadata:
```csharp
TextSignOptions textOptions = new TextSignOptions("Text signature")
{
    VerticalAlignment = VerticalAlignment.Top,
    HorizontalAlignment = HorizontalAlignment.Left
};
BarcodeSignOptions barcodeOptions = new BarcodeSignOptions("123456")
{
    EncodeType = BarcodeTypes.Code128,
    Left = 0,
    Top = 150,
    Height = 50,
    Width = 200
};
// Tentukan opsi tanda tangan lainnya (misalnya, kode QR, digital, gambar, metadata)...
```
## Langkah 3: Buat Daftar Opsi Tanda Tangan
Tentukan daftar opsi tanda tangan yang berisi semua opsi yang ditentukan sebelumnya:
```csharp
List<SignOptions> listOptions = new List<SignOptions>();
listOptions.Add(textOptions);
listOptions.Add(barcodeOptions);
// Tambahkan opsi tanda tangan lainnya ke daftar...
```
## Langkah 4: Tandatangani Dokumen
Tanda tangani dokumen dengan daftar opsi tanda tangan dan simpan dokumen yang ditandatangani:
```csharp
SignResult result = signature.Sign(outputFilePath, listOptions);
Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).\nFile saved at {outputFilePath}.");
```

## Kesimpulan
Menandatangani dokumen dengan berbagai opsi menggunakan GroupDocs.Signature untuk .NET memberikan solusi kuat untuk meningkatkan keamanan dan fleksibilitas dokumen. Dengan mengikuti langkah-langkah yang diuraikan dalam tutorial ini, Anda dapat dengan mudah mengintegrasikan berbagai jenis tanda tangan ke dalam aplikasi .NET Anda.
## FAQ
### Bisakah saya menggunakan gambar khusus untuk tanda tangan digital?
Ya, Anda dapat menentukan gambar khusus untuk tanda tangan digital menggunakan perpustakaan GroupDocs.Signature.
### Apakah GroupDocs.Signature kompatibel dengan berbagai format dokumen?
Ya, GroupDocs.Signature mendukung berbagai format dokumen, termasuk DOCX, PDF, PPTX, dan banyak lagi.
### Bisakah saya menyesuaikan tampilan tanda tangan teks?
Tentu saja, Anda dapat menyesuaikan tampilan tanda tangan teks, termasuk ukuran font, warna, dan gaya.
### Apakah GroupDocs.Signature menyediakan enkripsi untuk tanda tangan digital?
Ya, GroupDocs.Signature menawarkan opsi enkripsi untuk tanda tangan digital untuk memastikan keamanan dokumen.
### Apakah ada versi uji coba yang tersedia untuk GroupDocs.Signature untuk .NET?
 Ya, Anda dapat mengunduh GroupDocs.Signature versi uji coba gratis untuk .NET dari[Di Sini](https://releases.groupdocs.com/).