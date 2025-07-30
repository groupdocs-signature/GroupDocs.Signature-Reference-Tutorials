---
"description": "Pelajari cara mencari kode QR dalam dokumen secara efisien menggunakan GroupDocs.Signature untuk .NET dengan panduan langkah demi langkah yang komprehensif dan contoh kode ini."
"linktitle": "Cari Kode QR"
"second_title": "GroupDocs.Signature .NET API"
"title": "Cari Tanda Tangan Kode QR di Dokumen"
"url": "/id/net/signature-searching/search-for-qr-codes/"
"weight": 15
---

## Perkenalan

Dalam ekosistem dokumen digital saat ini, tanda tangan kode QR telah menjadi alat yang sangat berharga untuk mengintegrasikan informasi, autentikasi, dan meningkatkan keamanan dokumen. GroupDocs.Signature untuk .NET menyediakan API canggih bagi pengembang untuk mencari dan mengekstrak kode QR dari berbagai format dokumen, yang memungkinkan analisis dokumen tingkat lanjut dan kemampuan verifikasi dalam aplikasi .NET.

Tutorial komprehensif ini akan memandu Anda melalui proses penerapan fungsionalitas pencarian kode QR menggunakan GroupDocs.Signature untuk .NET, memberikan penjelasan yang jelas, petunjuk langkah demi langkah, dan contoh kode praktis yang dapat Anda integrasikan ke dalam aplikasi Anda sendiri.

## Prasyarat

Sebelum terjun ke pencarian tanda tangan kode QR, pastikan Anda memiliki prasyarat berikut:

1. GroupDocs.Signature untuk .NET SDK: Unduh dan instal SDK dari [halaman unduhan](https://releases.groupdocs.com/signature/net/).

2. Lingkungan Pengembangan: Siapkan lingkungan pengembangan .NET, seperti Visual Studio, dengan .NET Framework atau .NET Core terinstal.

3. Pengetahuan Dasar: Keakraban dengan pemrograman C# dan konsep pengembangan .NET.

4. Contoh Dokumen: Siapkan dokumen uji yang berisi kode QR untuk verifikasi dan pengujian.

## Mengimpor Ruang Nama

Mulailah dengan mengimpor namespace yang diperlukan untuk mengakses fungsionalitas GroupDocs.Signature:

```csharp
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
using System;
using System.Collections.Generic;
```

Sekarang, mari kita uraikan proses pencarian kode QR menjadi langkah-langkah yang jelas dan mudah diikuti:

## Langkah 1: Tentukan Jalur Dokumen

Pertama, tentukan jalur ke dokumen yang berisi kode QR yang ingin Anda cari:

```csharp
string filePath = "sample_multiple_signatures.docx";
```

## Langkah 2: Inisialisasi Objek Tanda Tangan

Buat contoh dari `Signature` kelas dengan meneruskan jalur dokumen:

```csharp
using (Signature signature = new Signature(filePath))
{
    // Kode pencarian kode QR akan ditambahkan di sini
}
```

## Langkah 3: Cari Tanda Tangan Kode QR

Gunakan `Search` metode dengan jenis tanda tangan yang tepat untuk menemukan kode QR dalam dokumen:

```csharp
// Cari tanda tangan kode QR dalam dokumen
List<QrCodeSignature> signatures = signature.Search<QrCodeSignature>(SignatureType.QrCode);
```

## Langkah 4: Proses dan Tampilkan Hasil

Ulangi tanda tangan kode QR yang ditemukan dan akses propertinya:

```csharp
// Menampilkan informasi tentang kode QR yang ditemukan
Console.WriteLine($"\nSource document contains {signatures.Count} QR code signature(s):");

foreach (var qrCodeSignature in signatures)
{
    Console.WriteLine($"QR Code found at page {qrCodeSignature.PageNumber} with type {qrCodeSignature.EncodeType.TypeName}");
    Console.WriteLine($"Content: {qrCodeSignature.Text}");
    Console.WriteLine($"Location: X={qrCodeSignature.Left}, Y={qrCodeSignature.Top}, Width={qrCodeSignature.Width}, Height={qrCodeSignature.Height}");
    Console.WriteLine();
}
```

## Contoh Lengkap

Berikut adalah contoh kerja komprehensif yang menunjukkan proses lengkap pencarian kode QR dalam sebuah dokumen:

```csharp
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
using System;
using System.Collections.Generic;

namespace QrCodeSignatureSearch
{
    class Program
    {
        static void Main(string[] args)
        {
            // Jalur dokumen - perbarui dengan jalur file Anda
            string filePath = "sample_multiple_signatures.docx";
            
            // Inisialisasi instance Tanda Tangan
            using (Signature signature = new Signature(filePath))
            {
                try
                {
                    // Cari tanda tangan kode QR dalam dokumen
                    List<QrCodeSignature> signatures = signature.Search<QrCodeSignature>(SignatureType.QrCode);
                    
                    // Menampilkan hasil pencarian
                    Console.WriteLine($"\nSource document ['{filePath}'] contains {signatures.Count} QR code signature(s):");
                    
                    foreach (var qrCodeSignature in signatures)
                    {
                        Console.WriteLine($"QR Code found at page {qrCodeSignature.PageNumber} with type {qrCodeSignature.EncodeType.TypeName}");
                        Console.WriteLine($"Content: {qrCodeSignature.Text}");
                        Console.WriteLine($"Location: X={qrCodeSignature.Left}, Y={qrCodeSignature.Top}, Width={qrCodeSignature.Width}, Height={qrCodeSignature.Height}");
                        Console.WriteLine();
                    }
                }
                catch (Exception ex)
                {
                    Console.WriteLine($"Error occurred: {ex.Message}");
                }
            }
            
            Console.WriteLine("Press any key to exit...");
            Console.ReadKey();
        }
    }
}
```

## Teknik Pencarian Kode QR Lanjutan

### Pencarian dengan Kriteria Tertentu

Untuk pencarian yang lebih tertarget, Anda dapat menggunakan `QrCodeSearchOptions` untuk menyesuaikan kriteria pencarian Anda:

```csharp
// Buat opsi pencarian kode QR dengan kriteria tertentu
QrCodeSearchOptions options = new QrCodeSearchOptions
{
    // Cari hanya pada halaman tertentu
    AllPages = false,
    PageNumber = 1,
    PagesSetup = new PagesSetup { Pages = new List<int> { 1, 3, 5 } },
    
    // Filter berdasarkan konten kode QR
    Text = "Invoice",
    MatchType = TextMatchType.Contains,
    
    // Filter berdasarkan jenis kode QR tertentu
    EncodeType = QrCodeTypes.QR,
    
    // Tentukan area tertentu untuk pencarian di dalamnya
    Rectangle = new Rectangle(100, 100, 400, 400)
};

// Pencarian dengan opsi tertentu
List<QrCodeSignature> filteredSignatures = signature.Search<QrCodeSignature>(options);
```

### Memproses Data Kode QR

Anda dapat menerapkan pemrosesan khusus untuk data kode QR berdasarkan persyaratan aplikasi Anda:

```csharp
foreach (var qrCode in signatures)
{
    // Ekstrak dan proses data kode QR berdasarkan konten
    string qrContent = qrCode.Text;
    
    if (qrContent.StartsWith("URL:"))
    {
        // Memproses data URL
        string url = qrContent.Substring(4);
        Console.WriteLine($"Found URL in QR code: {url}");
    }
    else if (qrContent.StartsWith("CONTACT:"))
    {
        // Informasi kontak proses
        string contact = qrContent.Substring(8);
        Console.WriteLine($"Found contact information in QR code: {contact}");
    }
    else if (qrContent.StartsWith("INVOICE:"))
    {
        // Memproses informasi faktur
        string invoiceData = qrContent.Substring(8);
        Console.WriteLine($"Found invoice information in QR code: {invoiceData}");
        
        // Mengurai dan memvalidasi data faktur
        if (ValidateInvoiceData(invoiceData))
        {
            Console.WriteLine("Invoice data is valid!");
        }
        else
        {
            Console.WriteLine("Warning: Invalid invoice data detected!");
        }
    }
}

// Contoh metode validasi
static bool ValidateInvoiceData(string data)
{
    // Terapkan logika validasi Anda
    return !string.IsNullOrEmpty(data) && data.Contains("ID") && data.Contains("Amount");
}
```

### Menerapkan Verifikasi Keamanan

Kode QR sering digunakan untuk tujuan autentikasi. Berikut cara menerapkan verifikasi keamanan dasar:

```csharp
// Periksa apakah dokumen berisi kode QR autentikasi yang valid
bool hasValidAuthQrCode = false;

foreach (var qrCode in signatures)
{
    if (qrCode.Text.StartsWith("AUTH:"))
    {
        string authCode = qrCode.Text.Substring(5);
        
        // Verifikasi kode autentikasi (misalnya, terhadap database atau daftar yang telah ditentukan sebelumnya)
        if (VerifyAuthCode(authCode))
        {
            hasValidAuthQrCode = true;
            Console.WriteLine("Document contains valid authentication QR code!");
            break;
        }
    }
}

if (!hasValidAuthQrCode)
{
    Console.WriteLine("Warning: Document does not contain a valid authentication QR code!");
}

// Contoh metode verifikasi
static bool VerifyAuthCode(string code)
{
    // Terapkan logika verifikasi Anda
    // Ini bisa berupa pencarian basis data, panggilan API, atau perbandingan terhadap nilai yang telah ditentukan sebelumnya
    return code == "A7B82C3D" || code == "X9Y8Z7W6";
}
```

### Mengekstrak Gambar Kode QR

Anda dapat mengekstrak gambar kode QR dari dokumen untuk diproses lebih lanjut atau ditampilkan:

```csharp
// Simpan gambar kode QR ke disk
foreach (var qrCode in signatures)
{
    if (qrCode.Content != null)
    {
        // Buat nama file unik berdasarkan nomor halaman dan posisi
        string outputPath = $"QrCode_P{qrCode.PageNumber}_X{qrCode.Left}_Y{qrCode.Top}.png";
        
        // Simpan data gambar
        File.WriteAllBytes(outputPath, qrCode.Content);
        Console.WriteLine($"Saved QR code image to {outputPath}");
    }
}
```

## Kesimpulan

Dalam panduan komprehensif ini, kami telah membahas cara mencari tanda tangan kode QR dalam dokumen menggunakan GroupDocs.Signature untuk .NET. Dari pencarian dasar hingga teknik lanjutan, Anda kini memiliki pengetahuan untuk menerapkan penanganan kode QR yang andal di aplikasi .NET Anda. API GroupDocs.Signature menyediakan kerangka kerja yang andal dan fleksibel untuk bekerja dengan berbagai jenis tanda tangan, termasuk kode QR, di berbagai format dokumen.

Dengan memanfaatkan kemampuan ini, Anda dapat meningkatkan proses verifikasi dokumen, menerapkan sistem autentikasi, dan mengekstrak informasi berharga yang tertanam dalam kode QR, semuanya dalam aplikasi .NET Anda.

## Pertanyaan yang Sering Diajukan

### Format kode QR mana yang didukung oleh GroupDocs.Signature?

GroupDocs.Signature mendukung berbagai format kode QR, termasuk Kode QR standar, Kode QR Mikro, dan standar kode QR umum lainnya. Format spesifik dapat diakses melalui `EncodeType` milik `QrCodeSignature` obyek.

### Bisakah saya mencari kode QR dalam dokumen yang dilindungi kata sandi?

Ya, GroupDocs.Signature mendukung pencarian kode QR dalam dokumen yang dilindungi kata sandi dengan memberikan kata sandi saat menginisialisasi `Signature` obyek:

```csharp
LoadOptions loadOptions = new LoadOptions { Password = "your_password" };
using (Signature signature = new Signature(filePath, loadOptions))
{
    // Cari kode QR
}
```

### Bagaimana cara memfilter kode QR berdasarkan kontennya?

Anda dapat memfilter kode QR berdasarkan kontennya menggunakan `Text` Dan `MatchType` properti dari `QrCodeSearchOptions`:

```csharp
QrCodeSearchOptions options = new QrCodeSearchOptions
{
    Text = "Invoice",
    MatchType = TextMatchType.Contains // Pilihan lainnya: Tepat, DimulaiDengan, BerakhirDengan
};
```

### Bisakah GroupDocs.Signature mendeteksi kode QR yang rusak atau terlihat sebagian?

GroupDocs.Signature memiliki kemampuan untuk mendeteksi kode QR yang terlihat sebagian, tetapi kode QR yang rusak parah mungkin tidak dapat dikenali. Akurasi deteksi bergantung pada kualitas dan visibilitas kode QR dalam dokumen.

### Format dokumen apa yang didukung untuk pencarian kode QR?

GroupDocs.Signature mendukung pencarian kode QR dalam berbagai format dokumen termasuk PDF, dokumen Microsoft Office (Word, Excel, PowerPoint), gambar (JPEG, PNG, TIFF), dan banyak lainnya.

## Lihat Juga

* [Referensi API](https://reference.groupdocs.com/signature/net/)
* [Contoh Kode di GitHub](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
* [Dokumentasi Produk](https://docs.groupdocs.com/signature/net/)
* [Halaman Produk](https://products.groupdocs.com/signature/net/)
* [Unduh Versi Terbaru](https://releases.groupdocs.com/signature/net/)
* [Artikel Blog](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
* [Forum Dukungan Gratis](https://forum.groupdocs.com/c/signature/13)
* [Lisensi Sementara](https://purchase.groupdocs.com/temporary-license/)