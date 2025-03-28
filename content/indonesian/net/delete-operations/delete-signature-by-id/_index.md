---
title: Hapus Tanda Tangan berdasarkan ID
linktitle: Hapus Tanda Tangan berdasarkan ID
second_title: GroupDocs.Tanda Tangan .NET API
description: Pelajari cara menghapus tanda tangan berdasarkan ID di dokumen .NET menggunakan pustaka GroupDocs.Signature. Panduan langkah demi langkah yang mudah.
weight: 11
url: /id/net/delete-operations/delete-signature-by-id/
---

# Hapus Tanda Tangan berdasarkan ID

## Perkenalan
Dalam tutorial ini, kita akan mempelajari cara menghapus tanda tangan berdasarkan ID-nya menggunakan GroupDocs.Signature untuk .NET. GroupDocs.Signature for .NET adalah perpustakaan canggih yang memungkinkan pengembang menambahkan, menghapus, atau memverifikasi tanda tangan digital dalam berbagai format dokumen menggunakan aplikasi .NET.
## Prasyarat
Sebelum kita mulai, pastikan Anda memiliki prasyarat berikut:
1.  GroupDocs.Signature untuk .NET Library: Unduh dan instal perpustakaan dari[Di Sini](https://releases.groupdocs.com/signature/net/).
2. .NET Framework: Pastikan Anda telah menginstal .NET Framework di sistem Anda.
3. Dokumen dengan Tanda Tangan: Siapkan dokumen (misalnya DOCX, PDF) dengan tanda tangan yang ingin Anda hapus.

## Impor Namespace
```csharp
using System;
using System.IO;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## Langkah 1: Tentukan Jalur File
Pertama, tentukan jalur file untuk dokumen yang berisi tanda tangan, dan jalur file keluaran tempat dokumen yang dimodifikasi akan disimpan.
```csharp
string filePath = "sample_multiple_signatures.docx";
string fileName = Path.GetFileName(filePath);
string outputFilePath = Path.Combine("Your Document Directory", "DeleteById", fileName);
```
## Langkah 2: Salin Dokumen
 Sejak itu`Delete` metode memodifikasi dokumen di tempatnya, yang terbaik adalah membuat salinan dokumen asli.
```csharp
File.Copy(filePath, outputFilePath, true);
```
## Langkah 3: Hapus Tanda Tangan berdasarkan ID
 Inisialisasi`Signature` objek dengan jalur file dokumen dan gunakan`Delete` metode untuk menghapus tanda tangan berdasarkan ID-nya.
```csharp
using (Signature signature = new Signature(outputFilePath))
{
    string id = @"eff64a14-dad9-47b0-88e5-2ee4e3604e71";
    bool result = signature.Delete(id);
    if (result)
    {
        Console.WriteLine($"Signature with Id# '{id}' was deleted from document ['{fileName}'].");
    }
    else
    {
        Helper.WriteError($"Signature was not deleted from the document! Signature with id# '{id}' was not found!");
    }
}
```

## Kesimpulan
Dalam tutorial ini, kita telah mempelajari cara menghapus tanda tangan berdasarkan ID-nya menggunakan GroupDocs.Signature untuk .NET. Perpustakaan ini menyediakan cara mudah untuk mengelola tanda tangan digital dalam berbagai format dokumen secara terprogram.
## FAQ
### Bisakah saya menghapus banyak tanda tangan sekaligus?
 Ya, Anda dapat menghapus beberapa tanda tangan dengan mengulangi ID mereka dan memanggil`Delete` metode untuk setiap ID.
### Apakah GroupDocs.Signature untuk .NET kompatibel dengan semua format dokumen?
GroupDocs.Signature untuk .NET mendukung berbagai format dokumen, termasuk PDF, DOCX, XLSX, dan banyak lagi.
### Bisakah saya menyesuaikan tampilan tanda tangan?
Ya, Anda dapat menyesuaikan tampilan tanda tangan, termasuk posisi, ukuran, font, dan warnanya.
### Apakah ada versi uji coba yang tersedia?
 Ya, Anda dapat mengunduh versi uji coba gratis dari[Di Sini](https://releases.groupdocs.com/).
### Di mana saya dapat menemukan bantuan atau dukungan untuk GroupDocs.Signature untuk .NET?
 Anda dapat mengunjungi forum dukungan[Di Sini](https://forum.groupdocs.com/c/signature/13) untuk bantuan.