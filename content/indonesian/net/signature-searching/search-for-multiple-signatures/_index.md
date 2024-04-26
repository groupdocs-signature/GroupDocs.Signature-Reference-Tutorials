---
title: Cari Banyak Tanda Tangan
linktitle: Cari Banyak Tanda Tangan
second_title: GroupDocs.Tanda Tangan .NET API
description: Pelajari cara mencari beberapa tanda tangan di dokumen .NET menggunakan GroupDocs.Signature untuk keamanan dan integritas dokumen yang efisien.
type: docs
weight: 14
url: /id/net/signature-searching/search-for-multiple-signatures/
---
## Perkenalan
GroupDocs.Signature untuk .NET adalah perpustakaan canggih yang memungkinkan pengembang menambahkan, mencari, dan menghapus berbagai jenis tanda tangan dalam format dokumen populer menggunakan aplikasi .NET. Dalam tutorial ini, kita akan fokus mencari beberapa tanda tangan dalam dokumen menggunakan GroupDocs.Signature untuk .NET.
## Prasyarat
Sebelum kita mulai, pastikan Anda memiliki prasyarat berikut:
- Visual Studio diinstal pada sistem Anda.
- Pemahaman dasar bahasa pemrograman C#.
- GroupDocs.Signature untuk perpustakaan .NET diinstal di proyek Anda. Anda dapat mengunduhnya dari[Di Sini](https://releases.groupdocs.com/signature/net/).

## Impor Namespace
Pertama, Anda perlu mengimpor namespace yang diperlukan untuk mengakses kelas dan metode yang disediakan oleh GroupDocs.Signature untuk .NET.
```csharp
using System;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## Langkah 1: Muat Dokumen
Muat dokumen tempat Anda ingin mencari banyak tanda tangan. Pastikan Anda memberikan jalur file yang benar.
```csharp
string filePath = "sample_multiple_signatures.docx";
using (Signature signature = new Signature(filePath))
{
    // Kode Anda ada di sini
}
```
## Langkah 2: Tentukan Opsi Pencarian
Tentukan opsi pencarian untuk berbagai jenis tanda tangan seperti teks, digital, kode batang, kode QR, dan metadata. Anda dapat menentukan kriteria pencarian seperti teks yang akan dicocokkan, jenis pencocokan, dan pencarian di semua halaman.
```csharp
// Tentukan opsi pencarian
TextSearchOptions textOptions = new TextSearchOptions()
{
    AllPages = true
};
DigitalSearchOptions digitalOptions = new DigitalSearchOptions()
{
    AllPages = true
};
BarcodeSearchOptions barcodeOptions = new BarcodeSearchOptions()
{
    AllPages = true,
    Text = "123456",
    MatchType = TextMatchType.Exact
};
QrCodeSearchOptions qrCodeOptions = new QrCodeSearchOptions()
{
    AllPages = true,
    Text = "John",
    MatchType = TextMatchType.Contains
};
MetadataSearchOptions metadataOptions = new MetadataSearchOptions();
```
## Langkah 3: Tambahkan Opsi Pencarian ke Daftar
Tambahkan opsi pencarian yang ditentukan ke daftar.
```csharp
// Tambahkan opsi ke daftar
List<SearchOptions> listOptions = new List<SearchOptions>();
listOptions.Add(textOptions);
listOptions.Add(barcodeOptions);
listOptions.Add(qrCodeOptions);
listOptions.Add(metadataOptions);
listOptions.Add(digitalOptions);
```
## Langkah 4: Cari Tanda Tangan
Cari tanda tangan dalam dokumen menggunakan opsi pencarian yang ditentukan.
```csharp
// Cari tanda tangan di dokumen
SearchResult result = signature.Search(listOptions);
if (result.Signatures.Count > 0)
{
    Console.WriteLine($"\nSource document ['{filePath}'] contains following signatures.");
    foreach (var resSignature in result.Signatures)
    {
        Console.WriteLine($"Signature found at page {resSignature.PageNumber} with type {resSignature.SignatureType} and Id#: {resSignature.SignatureId}");
    }
}
else
{
    Helper.WriteError("No one signature was found.");
}
```

## Kesimpulan
Dalam tutorial ini, kita mempelajari cara mencari beberapa tanda tangan dalam dokumen menggunakan GroupDocs.Signature untuk .NET. Dengan mengikuti langkah-langkah yang diberikan, Anda dapat secara efisien menemukan berbagai jenis tanda tangan di dokumen Anda, sehingga meningkatkan keamanan dan integritas dokumen.
## FAQ
### Bisakah saya mencari tanda tangan dalam format dokumen berbeda?
Ya, GroupDocs.Signature untuk .NET mendukung berbagai format dokumen termasuk Word, PDF, Excel, dan banyak lagi.
### Apakah mungkin untuk menyesuaikan kriteria pencarian tanda tangan?
Tentu saja, Anda dapat menyesuaikan kriteria pencarian sesuai dengan kebutuhan Anda, seperti menentukan teks yang sama persis atau mencari di semua halaman.
### Apakah GroupDocs.Signature untuk .NET menawarkan dukungan untuk tanda tangan digital?
Ya, Anda dapat mencari tanda tangan digital serta jenis lainnya seperti tanda tangan teks, kode batang, dan kode QR.
### Bisakah saya mengintegrasikan fungsionalitas pencarian tanda tangan ke dalam aplikasi .NET saya dengan mudah?
Ya, GroupDocs.Signature untuk .NET menyediakan API langsung yang menyederhanakan proses integrasi.
### Di mana saya bisa mendapatkan dukungan atau bantuan tambahan?
 Anda dapat mengunjungi forum GroupDocs.Signature[Di Sini](https://forum.groupdocs.com/c/signature/13) untuk pertanyaan atau bantuan apa pun.