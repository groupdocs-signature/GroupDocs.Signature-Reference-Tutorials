---
title: Tanda Tangani Gambar dengan Metadata
linktitle: Tanda Tangani Gambar dengan Metadata
second_title: GroupDocs.Tanda Tangan .NET API
description: Pelajari cara menandatangani gambar dengan metadata di .NET menggunakan GroupDocs.Signature. Solusi penandatanganan metadata yang mudah, efisien, dan dapat disesuaikan.
weight: 10
url: /id/net/document-signing/sign-image-with-metadata/
---

# Tanda Tangani Gambar dengan Metadata

## Perkenalan
GroupDocs.Signature untuk .NET memungkinkan pengembang menandatangani gambar dengan metadata secara efisien. Tutorial ini memandu Anda melalui proses langkah demi langkah.
## Prasyarat
Sebelum memulai, pastikan Anda memiliki hal berikut:
1. GroupDocs.Signature untuk .NET: Instal paket GroupDocs.Signature di proyek .NET Anda. Anda dapat mengunduhnya dari[Di Sini](https://releases.groupdocs.com/signature/net/).   
2. File Gambar: Siapkan file gambar yang ingin Anda tanda tangani dengan metadata.

## Impor Namespace
Pastikan untuk mengimpor namespace yang diperlukan dalam kode C# Anda:
```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## Langkah 1: Muat File Gambar
Pertama, tentukan jalur ke file gambar Anda dan direktori keluaran untuk gambar yang ditandatangani dengan metadata:
```csharp
string filePath = "sample.png";            
string outputFilePath = Path.Combine("Your Document Directory", "SignImageWithMetadata", "SignedWithMetadata.png");
```
## Langkah 2: Buat Tanda Tangan Metadata
Selanjutnya, buat tanda tangan metadata yang berbeda dan tambahkan ke koleksi tanda tangan opsi:
```csharp
using (Signature signature = new Signature(filePath))
{
    ushort imgsMetadataId = 41996;
    MetadataSignOptions options = new MetadataSignOptions();
    options
        .Add(new ImageMetadataSignature(imgsMetadataId++, "Mr.Scherlock Holmes")) // Nilai string
        .Add(new ImageMetadataSignature(imgsMetadataId++, DateTime.Now))          // Nilai Tanggal Waktu
        .Add(new ImageMetadataSignature(imgsMetadataId++, 123456))                // Nilai bilangan bulat
        .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456D))              // Nilai ganda
        .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456M))              // Nilai desimal
        .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456F));             // Nilai mengambang
    
    // menandatangani dokumen ke file
    SignResult result = signature.Sign(outputFilePath, options);
    Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).\nFile saved at {outputFilePath}.");
}
```

## Kesimpulan
Dalam tutorial ini, Anda mempelajari cara menandatangani gambar dengan metadata menggunakan GroupDocs.Signature untuk .NET. Dengan mengikuti langkah-langkah ini, Anda dapat dengan mudah memasukkan tanda tangan metadata ke dalam aplikasi .NET Anda.

## FAQ
### Bisakah saya menandatangani banyak gambar dengan metadata menggunakan GroupDocs.Signature untuk .NET?
Ya, Anda dapat menandatangani beberapa gambar dengan metadata dengan melakukan iterasi pada setiap file gambar dan menerapkan tanda tangan metadata.
### Apakah ada versi uji coba yang tersedia untuk GroupDocs.Signature untuk .NET?
 Ya, Anda dapat mengunduh versi uji coba dari[Di Sini](https://releases.groupdocs.com/).
### Apakah GroupDocs.Signature untuk .NET mendukung format file lain selain gambar?
Ya, GroupDocs.Signature mendukung berbagai format file, termasuk PDF, Word, Excel, dan lainnya.
### Bisakah saya menyesuaikan tampilan tanda tangan metadata?
Ya, Anda dapat menyesuaikan tampilan tanda tangan metadata, seperti ukuran font, warna, dan posisi.
### Di mana saya bisa mendapatkan dukungan untuk GroupDocs.Signature untuk .NET?
 Anda bisa mendapatkan dukungan dari forum GroupDocs.Signature[Di Sini](https://forum.groupdocs.com/c/signature/13).