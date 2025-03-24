---
title: Menandatangani dengan Stempel menggunakan GroupDocs.Signature
linktitle: Menandatangani dengan Stempel
second_title: GroupDocs.Tanda Tangan .NET API
description: Pelajari cara menambahkan tanda tangan stempel ke dokumen .NET Anda dengan mudah menggunakan GroupDocs.Signature untuk .NET. Meningkatkan keamanan dokumen.
weight: 16
url: /id/net/advanced-signature-techniques/sign-with-stamp/
---
## Perkenalan
Dalam tutorial ini, kami akan memandu Anda melalui proses penandatanganan dokumen dengan stempel menggunakan GroupDocs.Signature untuk .NET. Dengan mengikuti petunjuk langkah demi langkah ini, Anda akan dapat menambahkan tanda tangan stempel ke dokumen Anda dengan mudah.
## Prasyarat
Sebelum kita mulai, pastikan Anda memiliki prasyarat berikut:
1.  GroupDocs.Signature untuk .NET SDK: Unduh dan instal SDK dari[situs web](https://releases.groupdocs.com/signature/net/).
2. Lingkungan Pengembangan: Pastikan Anda memiliki lingkungan pengembangan yang sesuai untuk pengembangan .NET.
3. Dokumen untuk Ditandatangani: Siapkan dokumen (misalnya PDF) yang ingin Anda tanda tangani dengan stempel.

## Mengimpor Namespace
Mulailah dengan mengimpor namespace yang diperlukan ke dalam proyek Anda:
```csharp
using System;
using System.IO;
using System.Drawing;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## Langkah 1: Muat Dokumen
```csharp
string filePath = "sample.pdf";
using (Signature signature = new Signature(filePath))
{
    // Kode Anda ada di sini
}
```
## Langkah 2: Tetapkan Opsi Tanda Stempel
```csharp
StampSignOptions options = new StampSignOptions()
{
    Left = 50,
    Top = 150,                    
    Width = 200,
    Height = 200
};
```
## Langkah 3: Konfigurasikan Tampilan Stempel
```csharp
StampLine outerLine = new StampLine();
outerLine.Text = " * European Union ";
outerLine.TextRepeatType = StampTextRepeatType.FullTextRepeat;
outerLine.Font.Size = 12;
outerLine.Height = 22;
outerLine.TextBottomIntent = 6;
outerLine.TextColor = Color.WhiteSmoke;
outerLine.BackgroundColor = Color.DarkSlateBlue;
options.OuterLines.Add(outerLine);
StampLine innerLine = new StampLine();
innerLine.Text = "John Smith";
innerLine.TextColor = Color.MediumVioletRed;
innerLine.Font.Size = 20;
innerLine.Font.Bold = true;
innerLine.Height = 40;
options.InnerLines.Add(innerLine);
```
## Langkah 4: Tandatangani Dokumen
```csharp
string outputFilePath = Path.Combine("Your Document Directory", "SignWithStamp", fileName);
SignResult result = signature.Sign(outputFilePath, options);
Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).\nFile saved at {outputFilePath}.");
```

## Kesimpulan
Menambahkan tanda tangan stempel ke dokumen Anda menggunakan GroupDocs.Signature untuk .NET adalah proses yang mudah, seperti yang ditunjukkan dalam tutorial ini. Dengan langkah-langkah yang diberikan, Anda dapat dengan mudah meningkatkan keamanan dan keaslian dokumen Anda.
## FAQ
### Bisakah saya menyesuaikan tampilan tanda tangan prangko?
Ya, Anda dapat menyesuaikan berbagai aspek seperti teks, font, warna, dan posisi tanda tangan stempel sesuai kebutuhan Anda.
### Apakah GroupDocs.Signature mendukung penandatanganan berbagai format dokumen?
Ya, GroupDocs.Signature mendukung berbagai format dokumen termasuk PDF, Microsoft Word, Excel, PowerPoint, dan banyak lagi.
### Apakah ada versi uji coba yang tersedia untuk GroupDocs.Signature?
 Ya, Anda dapat mengakses versi uji coba gratis dari[situs web](https://releases.groupdocs.com/).
### Bisakah saya menambahkan banyak tanda tangan ke satu dokumen?
Tentu saja, GroupDocs.Signature memungkinkan Anda menambahkan banyak tanda tangan, termasuk stempel, teks, gambar, dan tanda tangan digital, ke satu dokumen.
### Di mana saya bisa mendapatkan dukungan jika saya mengalami masalah selama penerapan?
 Anda dapat menemukan dukungan dan bantuan dari forum komunitas GroupDocs.Signature[Di Sini](https://forum.groupdocs.com/c/signature/13).