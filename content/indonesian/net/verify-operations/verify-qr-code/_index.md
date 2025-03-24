---
title: Verifikasi Kode QR
linktitle: Verifikasi Kode QR
second_title: GroupDocs.Tanda Tangan .NET API
description: Pelajari cara memverifikasi kode QR dalam dokumen menggunakan GroupDocs.Signature untuk .NET. Tutorial komprehensif dengan panduan langkah demi langkah.
weight: 12
url: /id/net/verify-operations/verify-qr-code/
---
## Perkenalan
Dalam bidang pengelolaan dan autentikasi dokumen, memastikan integritas dan validitas tanda tangan adalah hal yang terpenting. GroupDocs.Signature untuk .NET memberikan solusi komprehensif untuk memverifikasi kode QR yang tertanam dalam dokumen. Dalam tutorial ini, kita akan mempelajari proses langkah demi langkah memverifikasi kode QR menggunakan GroupDocs.Signature untuk .NET.
## Prasyarat
Sebelum masuk ke proses verifikasi, pastikan Anda memiliki prasyarat berikut:
1.  Instalasi GroupDocs.Signature untuk .NET: Unduh dan instal GroupDocs.Signature untuk .NET dari[tautan unduhan](https://releases.groupdocs.com/signature/net/).
2. Akses ke Dokumen yang Berisi Kode QR: Siapkan contoh dokumen yang berisi kode QR untuk verifikasi. 

## Impor Namespace
Pertama, Anda perlu mengimpor namespace yang diperlukan untuk memanfaatkan fungsi yang disediakan oleh GroupDocs.Signature untuk .NET. Ikuti langkah ini:

```csharp
using System;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```


Sekarang, mari kita uraikan proses verifikasi kode QR yang tertanam dalam dokumen menggunakan GroupDocs.Signature untuk .NET:
## Langkah 1: Tentukan Jalur Dokumen
```csharp
string filePath = "sample_multiple_signatures.docx";
```
 Pastikan untuk mengganti`"sample_multiple_signatures.docx"` dengan jalur ke dokumen Anda.
## Langkah 2: Inisialisasi Objek Tanda Tangan
```csharp
using (Signature signature = new Signature(filePath))
{
    //Kode verifikasi ada di sini
}
```
 Inisialisasi a`Signature` objek dengan menyediakan jalur ke dokumen.
## Langkah 3: Tentukan Opsi Verifikasi
```csharp
QrCodeVerifyOptions options = new QrCodeVerifyOptions()
{
    AllPages = true, // nilai ini ditetapkan secara default
    Text = "John",
    MatchType = TextMatchType.Contains
};
```
 Tentukan opsi verifikasi seperti`AllPages` untuk memverifikasi semua halaman,`Text` untuk menentukan teks yang akan dicocokkan dalam kode QR, dan`MatchType` untuk menentukan kriteria yang cocok.
## Langkah 4: Verifikasi Tanda Tangan Dokumen
```csharp
VerificationResult result = signature.Verify(options);
```
 Panggil`Verify` metode`Signature` objek, melewati opsi verifikasi.
## Langkah 5: Tangani Hasil Verifikasi
```csharp
if (result.IsValid)
{
    // Tanda tangan sah ditemukan
}
else
{
    // Ditemukan tanda tangan yang tidak valid
}
```
Berdasarkan hasil verifikasi, tangani skenario keberhasilan atau kegagalan dengan tepat.

## Kesimpulan
Dalam tutorial ini, kami telah menjelajahi proses verifikasi kode QR dalam dokumen menggunakan GroupDocs.Signature untuk .NET. Dengan mengikuti langkah-langkah ini, Anda dapat dengan mudah mengintegrasikan fungsi verifikasi kode QR ke dalam aplikasi .NET Anda, memastikan integritas dan keaslian dokumen.
## FAQ
### Bisakah GroupDocs.Signature for .NET memverifikasi kode QR di berbagai format dokumen?
Ya, GroupDocs.Signature untuk .NET mendukung berbagai format dokumen termasuk DOCX, PDF, dan lainnya untuk verifikasi kode QR.
### Apakah ada uji coba gratis yang tersedia untuk GroupDocs.Signature untuk .NET?
 Ya, Anda dapat memanfaatkan uji coba gratis dari[halaman rilis](https://releases.groupdocs.com/).
### Opsi dukungan apa yang tersedia untuk GroupDocs.Signature untuk pengguna .NET?
 Pengguna dapat mengakses dukungan melalui[forum](https://forum.groupdocs.com/c/signature/13) untuk GroupDocs.Tanda Tangan.
### Bisakah saya membeli lisensi sementara untuk GroupDocs.Signature untuk .NET?
 Ya, lisensi sementara tersedia untuk dibeli dari[Halaman pembelian GroupDocs](https://purchase.groupdocs.com/temporary-license/).
### Apakah ada dokumentasi ekstensif yang tersedia untuk GroupDocs.Signature untuk .NET?
 Tentu saja, Anda dapat merujuk pada dokumentasi terperinci yang disediakan[Di Sini](https://tutorials.groupdocs.com/signature/net/) untuk panduan komprehensif dalam memanfaatkan fungsi GroupDocs.Signature untuk .NET.