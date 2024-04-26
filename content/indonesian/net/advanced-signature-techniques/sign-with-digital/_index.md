---
title: Penandatanganan dengan Tanda Tangan Digital
linktitle: Penandatanganan dengan Tanda Tangan Digital
second_title: GroupDocs.Tanda Tangan .NET API
description: Pelajari cara menandatangani dokumen secara digital di .NET menggunakan GroupDocs.Signature. Tingkatkan keamanan dan keaslian dengan tutorial komprehensif ini.
type: docs
weight: 12
url: /id/net/advanced-signature-techniques/sign-with-digital/
---
## Perkenalan
Tanda tangan digital memainkan peran penting dalam memastikan keaslian dan integritas dokumen elektronik. Dalam bidang pengembangan .NET, GroupDocs.Signature menawarkan solusi canggih untuk mengintegrasikan tanda tangan digital ke dalam aplikasi Anda dengan lancar. Tutorial ini akan memandu Anda melalui proses penandatanganan dokumen menggunakan tanda tangan digital dengan GroupDocs.Signature untuk .NET.
## Prasyarat
Sebelum kita mendalami penerapannya, pastikan Anda memiliki prasyarat berikut:
1.  GroupDocs.Signature untuk .NET: Unduh dan instal GroupDocs.Signature untuk .NET dari[Unduh Halaman](https://releases.groupdocs.com/signature/net/).
2. Sertifikat Digital: Dapatkan sertifikat digital (.pfx) yang akan digunakan untuk menandatangani dokumen. Jika tidak memilikinya, Anda dapat membuat sertifikat yang ditandatangani sendiri atau mendapatkannya dari otoritas sertifikat tepercaya.
3. Dokumen untuk Ditandatangani: Siapkan dokumen (misalnya PDF) yang ingin Anda tandatangani secara digital. Pastikan Anda memiliki izin yang diperlukan untuk mengakses dan memodifikasi dokumen.
4. Gambar Tanda Tangan: Secara opsional, Anda dapat memberikan gambar tanda tangan Anda yang akan disematkan ke dalam dokumen. Ini menambahkan sentuhan personal pada tanda tangan digital.

## Impor Namespace
Pertama, mari impor namespace yang diperlukan ke kode C# kita:
```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## Langkah 1: Tentukan Jalur dan Opsi File
Tentukan jalur file untuk dokumen yang akan ditandatangani, gambar tanda tangan (jika ada), dan sertifikat digital.
```csharp
string filePath = "sample.pdf";
string fileName = Path.GetFileName(filePath);
string imagePath = "signature_handwrite.jpg";
string certificatePath = "YourSignature.pfx";
string outputFilePath = Path.Combine("Your Document Directory", "SignWithDigital", fileName);
```
## Langkah 2: Inisialisasi Objek Tanda Tangan
 Buat sebuah instance dari`Signature` kelas dengan melewati jalur dokumen yang akan ditandatangani.
```csharp
using (Signature signature = new Signature(filePath))
{
    // Tentukan opsi tanda tangan digital
    DigitalSignOptions options = new DigitalSignOptions(certificatePath)
    {
        ImageFilePath = imagePath, // Tetapkan jalur file gambar (opsional)
        Left = 50,                 //Tetapkan koordinat X posisi tanda tangan
        Top = 50,                  // Tetapkan koordinat Y dari posisi tanda tangan
        PageNumber = 1,            // Tentukan nomor halaman yang akan ditandatangani
        Password = "1234567890"    // Tetapkan kata sandi untuk sertifikat (jika diperlukan)
    };
    // Langkah 3: Tandatangani Dokumen
    SignResult result = signature.Sign(outputFilePath, options);
    // Langkah 4: Tampilkan Hasil
    Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).\nFile saved at {outputFilePath}.");
}
```

## Kesimpulan
Dalam tutorial ini, kita telah mempelajari cara menandatangani dokumen menggunakan tanda tangan digital dengan GroupDocs.Signature untuk .NET. Dengan mengikuti langkah-langkah sederhana ini, Anda dapat meningkatkan keamanan dan keaslian dokumen elektronik Anda, memastikan dokumen tersebut tetap tahan terhadap kerusakan dan mengikat secara hukum.
## FAQ
### Apa itu tanda tangan digital?
Tanda tangan digital adalah teknik kriptografi yang digunakan untuk memverifikasi keaslian dan integritas dokumen atau pesan digital.
### Bisakah saya menandatangani dokumen dengan GroupDocs.Signature menggunakan sertifikat yang ditandatangani sendiri?
Ya, Anda dapat menandatangani dokumen menggunakan sertifikat yang ditandatangani sendiri yang dihasilkan oleh alat seperti OpenSSL atau MakeCert Microsoft.
### Apakah GroupDocs.Signature kompatibel dengan berbagai format dokumen?
Ya, GroupDocs.Signature mendukung berbagai format dokumen, termasuk PDF, Word, Excel, PowerPoint, dan banyak lagi.
### Bisakah saya menyesuaikan tampilan tanda tangan digital saya?
Sangat! GroupDocs.Signature memungkinkan Anda menyesuaikan berbagai aspek tanda tangan digital Anda, seperti posisi, ukuran, dan tampilannya.
### Apakah GroupDocs.Signature cocok untuk aplikasi tingkat perusahaan?
Ya, GroupDocs.Signature menawarkan fitur dan skalabilitas yang tangguh, menjadikannya pilihan ideal untuk aplikasi penandatanganan dokumen tingkat perusahaan.