---
"description": "Pelajari cara mencari berbagai jenis tanda tangan dalam dokumen menggunakan GroupDocs.Signature untuk .NET. Panduan lengkap dengan contoh kode untuk meningkatkan keamanan dokumen."
"linktitle": "Cari Beberapa Tanda Tangan"
"second_title": "GroupDocs.Signature .NET API"
"title": "Mencari Beberapa Jenis Tanda Tangan dalam Dokumen"
"url": "/id/net/signature-searching/search-for-multiple-signatures/"
"weight": 14
---

## Perkenalan

Dalam sistem manajemen dokumen modern, kemampuan untuk mencari dan memvalidasi berbagai jenis tanda tangan dalam satu dokumen semakin penting. Organisasi sering menggunakan berbagai jenis tanda tangan—seperti tanda tangan digital, tanda tangan teks, kode batang, kode QR, dan lainnya—untuk meningkatkan keamanan dokumen dan menyederhanakan proses verifikasi. GroupDocs.Signature untuk .NET menyediakan kerangka kerja canggih yang memungkinkan pengembang untuk menerapkan fungsionalitas pencarian tanda tangan yang komprehensif di berbagai format dokumen.

Tutorial ini akan memandu Anda melalui proses pencarian beberapa jenis tanda tangan dalam dokumen menggunakan GroupDocs.Signature untuk .NET, menawarkan penjelasan terperinci dan contoh kode praktis.

## Prasyarat

Sebelum terjun ke penerapan fungsi pencarian banyak tanda tangan, pastikan Anda memiliki prasyarat berikut:

1. Lingkungan Pengembangan: Visual Studio atau lingkungan pengembangan .NET pilihan apa pun yang terinstal di sistem Anda.
  
2. GroupDocs.Signature untuk .NET: Unduh dan instal pustaka GroupDocs.Signature untuk .NET dari [Di Sini](https://releases.groupdocs.com/signature/net/).

3. Pengetahuan Dasar C#: Keakraban dengan bahasa pemrograman C# dan konsep kerangka kerja .NET.

4. Contoh Dokumen: Siapkan dokumen uji yang berisi berbagai jenis tanda tangan untuk tujuan pengujian.

## Mengimpor Ruang Nama

Mulailah dengan mengimpor namespace yang diperlukan untuk mengakses fungsionalitas GroupDocs.Signature:

```csharp
using System;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

Sekarang, mari kita uraikan proses pencarian berbagai jenis tanda tangan menjadi langkah-langkah yang jelas dan mudah dikelola:

## Langkah 1: Muat Dokumen

Pertama, muat dokumen yang berisi tanda tangan yang ingin Anda cari:

```csharp
string filePath = "sample_multiple_signatures.docx";
using (Signature signature = new Signature(filePath))
{
    // Kode pencarian multi-tanda tangan akan ditambahkan di sini
}
```

## Langkah 2: Tentukan Opsi Pencarian untuk Berbagai Jenis Tanda Tangan

Buat opsi pencarian untuk setiap jenis tanda tangan yang ingin Anda cari:

```csharp
// Tentukan opsi pencarian untuk tanda tangan teks
TextSearchOptions textOptions = new TextSearchOptions
{
    AllPages = true,  // Cari di semua halaman
    Text = "Signature",  // Opsional: teks untuk ditemukan
    MatchType = TextMatchType.Contains  // Kriteria pencocokan
};

// Tentukan opsi pencarian untuk tanda tangan digital
DigitalSearchOptions digitalOptions = new DigitalSearchOptions
{
    AllPages = true
};

// Tentukan opsi pencarian untuk tanda tangan kode batang
BarcodeSearchOptions barcodeOptions = new BarcodeSearchOptions
{
    AllPages = true,
    Text = "123456",  // Opsional: teks kode batang yang cocok
    MatchType = TextMatchType.Exact  // Kriteria pencocokan
};

// Tentukan opsi pencarian untuk tanda tangan kode QR
QrCodeSearchOptions qrCodeOptions = new QrCodeSearchOptions
{
    AllPages = true,
    Text = "John",  // Opsional: Teks kode QR untuk dicocokkan
    MatchType = TextMatchType.Contains  // Kriteria pencocokan
};

// Tentukan opsi pencarian untuk tanda tangan metadata
MetadataSearchOptions metadataOptions = new MetadataSearchOptions();
```

## Langkah 3: Tambahkan Opsi ke Koleksi

Tambahkan semua opsi pencarian ke koleksi:

```csharp
// Buat daftar untuk menampung semua opsi pencarian
List<SearchOptions> searchOptions = new List<SearchOptions>
{
    textOptions,
    digitalOptions,
    barcodeOptions,
    qrCodeOptions,
    metadataOptions
};
```

## Langkah 4: Lakukan Pencarian dan Proses Hasil

Jalankan pencarian menggunakan opsi pencarian gabungan dan proses hasilnya:

```csharp
// Cari semua jenis tanda tangan menggunakan opsi yang ditentukan
SearchResult result = signature.Search(searchOptions);

// Periksa apakah tanda tangan ditemukan
if (result.Signatures.Count > 0)
{
    Console.WriteLine($"\nSource document ['{filePath}'] contains {result.Signatures.Count} signature(s):");
    
    // Ulangi melalui tanda tangan yang ditemukan
    foreach (var foundSignature in result.Signatures)
    {
        Console.WriteLine($"Signature found: Type: {foundSignature.SignatureType}, Page: {foundSignature.PageNumber}, ID: {foundSignature.SignatureId}");
        
        // Memproses jenis tanda tangan tertentu
        if (foundSignature is TextSignature textSignature)
        {
            Console.WriteLine($"Text: '{textSignature.Text}'");
        }
        else if (foundSignature is BarcodeSignature barcodeSignature)
        {
            Console.WriteLine($"Barcode Type: {barcodeSignature.EncodeType.TypeName}, Text: '{barcodeSignature.Text}'");
        }
        else if (foundSignature is QrCodeSignature qrCodeSignature)
        {
            Console.WriteLine($"QR Code Type: {qrCodeSignature.EncodeType.TypeName}, Text: '{qrCodeSignature.Text}'");
        }
        else if (foundSignature is DigitalSignature digitalSignature)
        {
            Console.WriteLine($"Certificate: {digitalSignature.Certificate?.SubjectName}, Valid: {digitalSignature.IsValid}");
        }
        else if (foundSignature is MetadataSignature metadataSignature)
        {
            Console.WriteLine($"Metadata: Name: {metadataSignature.Name}, Value: {metadataSignature.Value}");
        }
    }
}
else
{
    Console.WriteLine("No signatures were found in the document.");
}
```

## Contoh Lengkap

Berikut ini adalah contoh lengkap dan berfungsi yang menunjukkan pencarian beberapa jenis tanda tangan dalam sebuah dokumen:

```csharp
using System;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;

namespace MultiSignatureSearch
{
    class Program
    {
        static void Main(string[] args)
        {
            // Jalur dokumen
            string filePath = "sample_multiple_signatures.docx";
            
            // Inisialisasi instance Tanda Tangan
            using (Signature signature = new Signature(filePath))
            {
                try
                {
                    // Tentukan opsi pencarian untuk tanda tangan teks
                    TextSearchOptions textOptions = new TextSearchOptions
                    {
                        AllPages = true,
                        MatchType = TextMatchType.Contains
                    };

                    // Tentukan opsi pencarian untuk tanda tangan digital
                    DigitalSearchOptions digitalOptions = new DigitalSearchOptions
                    {
                        AllPages = true
                    };

                    // Tentukan opsi pencarian untuk tanda tangan kode batang
                    BarcodeSearchOptions barcodeOptions = new BarcodeSearchOptions
                    {
                        AllPages = true
                    };

                    // Tentukan opsi pencarian untuk tanda tangan kode QR
                    QrCodeSearchOptions qrCodeOptions = new QrCodeSearchOptions
                    {
                        AllPages = true
                    };

                    // Tentukan opsi pencarian untuk tanda tangan metadata
                    MetadataSearchOptions metadataOptions = new MetadataSearchOptions();

                    // Buat daftar untuk menampung semua opsi pencarian
                    List<SearchOptions> searchOptions = new List<SearchOptions>
                    {
                        textOptions,
                        digitalOptions,
                        barcodeOptions,
                        qrCodeOptions,
                        metadataOptions
                    };

                    // Cari semua jenis tanda tangan
                    SearchResult result = signature.Search(searchOptions);

                    // Periksa apakah tanda tangan ditemukan
                    if (result.Signatures.Count > 0)
                    {
                        Console.WriteLine($"\nSource document ['{filePath}'] contains {result.Signatures.Count} signature(s):");
                        
                        // Memproses hasil berdasarkan jenis tanda tangan
                        foreach (var foundSignature in result.Signatures)
                        {
                            Console.WriteLine($"Signature found: Type: {foundSignature.SignatureType}, Page: {foundSignature.PageNumber}");
                            
                            // Memproses jenis tanda tangan tertentu
                            switch (foundSignature.SignatureType)
                            {
                                case SignatureType.Text:
                                    var textSignature = foundSignature as TextSignature;
                                    Console.WriteLine($"Text: '{textSignature.Text}'");
                                    break;
                                    
                                case SignatureType.Barcode:
                                    var barcodeSignature = foundSignature as BarcodeSignature;
                                    Console.WriteLine($"Barcode Type: {barcodeSignature.EncodeType.TypeName}, Text: '{barcodeSignature.Text}'");
                                    break;
                                    
                                case SignatureType.QrCode:
                                    var qrCodeSignature = foundSignature as QrCodeSignature;
                                    Console.WriteLine($"QR Code Type: {qrCodeSignature.EncodeType.TypeName}, Text: '{qrCodeSignature.Text}'");
                                    break;
                                    
                                case SignatureType.Digital:
                                    var digitalSignature = foundSignature as DigitalSignature;
                                    Console.WriteLine($"Certificate: {digitalSignature.Certificate?.SubjectName}, Valid: {digitalSignature.IsValid}");
                                    break;
                                    
                                case SignatureType.Metadata:
                                    var metadataSignature = foundSignature as MetadataSignature;
                                    Console.WriteLine($"Metadata: Name: {metadataSignature.Name}, Value: {metadataSignature.Value}");
                                    break;
                            }
                            
                            Console.WriteLine(); // Tambahkan jeda baris di antara tanda tangan
                        }
                    }
                    else
                    {
                        Console.WriteLine("No signatures were found in the document.");
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

## Teknik Pencarian Multi-Tanda Tangan Lanjutan

### Memfilter Hasil Pencarian

Anda dapat menerapkan penyaringan lanjutan untuk mempersempit hasil pencarian:

```csharp
// Filter hasil berdasarkan nomor halaman
var signaturesOnFirstPage = result.Signatures.FindAll(s => s.PageNumber == 1);

// Filter hasil berdasarkan jenis tanda tangan
var digitalSignatures = result.Signatures.FindAll(s => s.SignatureType == SignatureType.Digital);
var qrCodeSignatures = result.Signatures.FindAll(s => s.SignatureType == SignatureType.QrCode);

// Filter tanda tangan teks yang berisi konten tertentu
var approvalSignatures = result.Signatures
    .FindAll(s => s is TextSignature && ((TextSignature)s).Text.Contains("Approved"));
```

### Memvalidasi Beberapa Tanda Tangan

Terapkan logika validasi untuk berbagai jenis tanda tangan:

```csharp
bool ValidateAllSignatures(SearchResult result)
{
    bool isDocumentValid = true;
    
    // Periksa apakah dokumen memiliki tanda tangan digital yang valid
    bool hasValidDigitalSignature = result.Signatures
        .Any(s => s is DigitalSignature && ((DigitalSignature)s).IsValid);
    
    if (!hasValidDigitalSignature)
    {
        Console.WriteLine("Warning: Document does not contain a valid digital signature");
        isDocumentValid = false;
    }
    
    // Periksa apakah dokumen memiliki kode QR yang diperlukan
    bool hasRequiredQRCode = result.Signatures
        .Any(s => s is QrCodeSignature && ((QrCodeSignature)s).Text.Contains("Auth-Code"));
    
    if (!hasRequiredQRCode)
    {
        Console.WriteLine("Warning: Document does not contain the required authentication QR code");
        isDocumentValid = false;
    }
    
    return isDocumentValid;
}
```

### Pencarian dengan Pemrosesan Kustom

Anda dapat menentukan logika pemrosesan khusus untuk operasi pencarian:

```csharp
// Buat opsi pencarian dengan pemrosesan khusus
TextSearchOptions textOptions = new TextSearchOptions
{
    AllPages = true,
    
    // Tentukan pemrosesan kustom menggunakan delegasi
    ProcessCompleted = (signature) =>
    {
        // Logika validasi khusus - hanya menerima tanda tangan pada halaman tertentu
        TextSignature textSignature = signature as TextSignature;
        return textSignature != null && (textSignature.PageNumber == 1 || textSignature.PageNumber == 2);
    }
};
```

## Kesimpulan

Dalam panduan komprehensif ini, kami telah membahas cara mencari berbagai jenis tanda tangan dalam dokumen menggunakan GroupDocs.Signature untuk .NET. Mulai dari menyiapkan opsi pencarian untuk berbagai jenis tanda tangan hingga memproses dan memvalidasi hasilnya, kini Anda memiliki pengetahuan untuk menerapkan fungsionalitas pencarian tanda tangan yang andal di aplikasi .NET Anda.

Kemampuan untuk mencari beberapa jenis tanda tangan secara bersamaan meningkatkan proses verifikasi dokumen, memperkuat langkah-langkah keamanan, dan menyederhanakan alur kerja validasi dokumen. GroupDocs.Signature menyediakan kerangka kerja yang andal dan fleksibel untuk bekerja dengan berbagai jenis tanda tangan di berbagai format dokumen, menjadikannya pilihan yang sangat baik untuk aplikasi pemrosesan dokumen.

## Pertanyaan yang Sering Diajukan

### Bisakah saya mencari tanda tangan dalam dokumen yang dilindungi kata sandi?

Ya, GroupDocs.Signature mendukung pencarian tanda tangan dalam dokumen yang dilindungi kata sandi. Anda dapat memberikan kata sandi saat menginisialisasi `Signature` obyek:

```csharp
LoadOptions loadOptions = new LoadOptions { Password = "your_password" };
using (Signature signature = new Signature(filePath, loadOptions))
{
    // Cari tanda tangan
}
```

### Format dokumen apa yang didukung untuk pencarian tanda tangan?

GroupDocs.Signature mendukung berbagai format dokumen, termasuk PDF, dokumen Microsoft Office (Word, Excel, PowerPoint), format OpenOffice, gambar, dan banyak lagi.

### Bisakah saya membatasi pencarian ke halaman tertentu dalam suatu dokumen?

Ya, setiap jenis opsi pencarian memiliki properti yang memungkinkan Anda menentukan halaman mana yang akan dicari:

```csharp
TextSearchOptions options = new TextSearchOptions
{
    AllPages = false,  // Jangan mencari semua halaman
    PageNumber = 1,    // Cari hanya di halaman 1
    
    // Atau tentukan beberapa halaman
    PagesSetup = new PagesSetup { Pages = new List<int> { 1, 3, 5 } }
};
```

### Bagaimana saya dapat mengoptimalkan kinerja saat mencari dalam dokumen besar?

Untuk dokumen besar, Anda dapat mengoptimalkan kinerja dengan:

1. Membatasi pencarian ke halaman atau rentang halaman tertentu
2. Menggunakan kriteria pencarian yang lebih spesifik untuk mengurangi jumlah kecocokan potensial
3. Menerapkan pagination dalam tampilan hasil Anda
4. Mencari satu jenis tanda tangan pada satu waktu jika Anda tidak memerlukan hasil yang simultan

### Dapatkah saya memperluas GroupDocs.Signature untuk mendukung jenis tanda tangan kustom?

Meskipun GroupDocs.Signature menyediakan dukungan bawaan untuk jenis tanda tangan umum, Anda dapat memperluas fungsinya dengan:

1. Membuat kelas opsi pencarian khusus yang berasal dari `SearchOptions`
2. Menerapkan logika pemrosesan khusus menggunakan `ProcessCompleted` melimpahkan
3. Mengembangkan kelas pembungkus yang menggabungkan beberapa pencarian tanda tangan dengan logika bisnis tingkat lanjut

## Lihat Juga

* [Referensi API](https://reference.groupdocs.com/signature/net/)
* [Contoh Kode di GitHub](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
* [Dokumentasi Produk](https://docs.groupdocs.com/signature/net/)
* [Halaman Produk](https://products.groupdocs.com/signature/net/)
* [Unduh Versi Terbaru](https://releases.groupdocs.com/signature/net/)
* [Artikel Blog](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
* [Forum Dukungan Gratis](https://forum.groupdocs.com/c/signature/13)
* [Lisensi Sementara](https://purchase.groupdocs.com/temporary-license/)