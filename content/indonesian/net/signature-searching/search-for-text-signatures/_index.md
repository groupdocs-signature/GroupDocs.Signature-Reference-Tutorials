---
"description": "Pelajari cara mencari tanda tangan teks dalam dokumen secara efisien menggunakan GroupDocs.Signature untuk .NET dengan panduan langkah demi langkah yang komprehensif dan contoh kode."
"linktitle": "Cari Tanda Tangan Teks"
"second_title": "GroupDocs.Signature .NET API"
"title": "Mencari Tanda Tangan Teks dalam Dokumen"
"url": "/id/net/signature-searching/search-for-text-signatures/"
"weight": 16
---

## Perkenalan

Tanda tangan teks merupakan metode umum untuk menunjukkan kepengarangan, persetujuan, atau verifikasi dokumen. Dalam manajemen dokumen digital, kemampuan untuk mencari dan mengekstrak tanda tangan teks secara terprogram sangat penting untuk validasi dokumen, otomatisasi alur kerja, dan verifikasi kepatuhan. GroupDocs.Signature untuk .NET menawarkan solusi komprehensif untuk mengimplementasikan fungsi pencarian tanda tangan teks di aplikasi .NET Anda, mendukung berbagai format dokumen dan kemampuan pencarian tingkat lanjut.

Tutorial ini akan memandu Anda melalui proses pencarian tanda tangan teks dalam dokumen menggunakan GroupDocs.Signature untuk .NET, memberikan penjelasan terperinci, petunjuk langkah demi langkah, dan contoh kode praktis.

## Prasyarat

Sebelum terjun ke pencarian tanda tangan teks, pastikan Anda memiliki prasyarat berikut:

1. GroupDocs.Signature untuk Pustaka .NET: Unduh dan instal pustaka dari [halaman rilis](https://releases.groupdocs.com/signature/net/).

2. Lingkungan Pengembangan: Siapkan lingkungan pengembangan yang sesuai seperti Visual Studio atau IDE yang kompatibel dengan dukungan .NET.

3. Contoh Dokumen: Siapkan dokumen uji yang berisi tanda tangan teks untuk verifikasi dan pengujian.

4. Pengetahuan Dasar C#: Keakraban dengan bahasa pemrograman C# dan konsep kerangka kerja .NET.

## Mengimpor Ruang Nama

Mulailah dengan mengimpor namespace yang diperlukan untuk mengakses fungsionalitas GroupDocs.Signature:

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

Sekarang, mari kita uraikan proses pencarian tanda tangan teks menjadi langkah-langkah yang jelas dan mudah dikelola:

## Langkah 1: Muat Dokumen

Pertama, tentukan jalur dokumen dan inisialisasi `Signature` obyek:

```csharp
string filePath = "sample_multiple_signatures.docx";
string fileName = Path.GetFileName(filePath);

using (Signature signature = new Signature(filePath))
{
    // Kode pencarian tanda tangan teks akan ditambahkan di sini
}
```

## Langkah 2: Konfigurasikan Opsi Pencarian

Buat dan konfigurasikan `TextSearchOptions` untuk menentukan bagaimana tanda tangan teks harus dicari:

```csharp
// Konfigurasikan opsi pencarian teks
TextSearchOptions options = new TextSearchOptions
{
    // Cari di semua halaman
    AllPages = true,
    
    // Opsional: tentukan teks yang cocok
    // Teks = "Disetujui",
    
    // Opsional: tentukan jenis pencocokan
    // MatchType = TextMatchType.Berisi
};
```

## Langkah 3: Lakukan Pencarian Tanda Tangan Teks

Jalankan operasi pencarian menggunakan opsi yang dikonfigurasi:

```csharp
// Cari tanda tangan teks
List<TextSignature> signatures = signature.Search<TextSignature>(options);
```

## Langkah 4: Proses dan Tampilkan Hasil

Ulangi tanda tangan teks yang ditemukan dan tampilkan detailnya:

```csharp
// Menampilkan hasil pencarian
Console.WriteLine($"\nSource document '{fileName}' contains {signatures.Count} text signature(s):");

foreach (TextSignature textSignature in signatures)
{
    Console.WriteLine($"Text signature found at page {textSignature.PageNumber} with text '{textSignature.Text}'");
    Console.WriteLine($"Location: X={textSignature.Left}, Y={textSignature.Top}, Width={textSignature.Width}, Height={textSignature.Height}");
    Console.WriteLine($"Signature type: {textSignature.SignatureImplementation}");
    Console.WriteLine();
}
```

## Contoh Lengkap

Berikut adalah contoh kerja lengkap yang menunjukkan cara mencari tanda tangan teks dalam dokumen:

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;

namespace TextSignatureSearch
{
    class Program
    {
        static void Main(string[] args)
        {
            // Jalur dokumen - perbarui dengan jalur file Anda
            string filePath = "sample_multiple_signatures.docx";
            string fileName = Path.GetFileName(filePath);
            
            // Inisialisasi instance Tanda Tangan
            using (Signature signature = new Signature(filePath))
            {
                try
                {
                    // Konfigurasikan opsi pencarian teks
                    TextSearchOptions options = new TextSearchOptions
                    {
                        // Cari di semua halaman
                        AllPages = true
                    };
                    
                    // Cari tanda tangan teks
                    List<TextSignature> signatures = signature.Search<TextSignature>(options);
                    
                    // Menampilkan hasil pencarian
                    Console.WriteLine($"\nSource document '{fileName}' contains {signatures.Count} text signature(s):");
                    
                    foreach (TextSignature textSignature in signatures)
                    {
                        Console.WriteLine($"Text signature found at page {textSignature.PageNumber} with text '{textSignature.Text}'");
                        Console.WriteLine($"Location: X={textSignature.Left}, Y={textSignature.Top}, Width={textSignature.Width}, Height={textSignature.Height}");
                        Console.WriteLine($"Signature type: {textSignature.SignatureImplementation}");
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

## Teknik Pencarian Tanda Tangan Teks Lanjutan

### Pencarian dengan Kriteria Teks Tertentu

Untuk pencarian yang lebih tertarget, Anda dapat menyesuaikan `TextSearchOptions` untuk memfilter berdasarkan konten teks tertentu:

```csharp
// Buat opsi pencarian dengan kriteria teks tertentu
TextSearchOptions options = new TextSearchOptions
{
    // Cari di semua halaman
    AllPages = true,
    
    // Cari teks tertentu
    Text = "Approved",
    
    // Tentukan jenis pencocokan (Berisi, Tepat, DimulaiDengan, BerakhirDengan)
    MatchType = TextMatchType.Contains,
    
    // Pencarian peka huruf besar-kecil
    MatchCase = true
};
```

### Pencarian di Area Dokumen Tertentu

Anda dapat membatasi pencarian ke area tertentu dalam dokumen:

```csharp
// Buat opsi pencarian untuk area dokumen tertentu
TextSearchOptions options = new TextSearchOptions
{
    // Cari hanya pada halaman tertentu
    AllPages = false,
    PageNumber = 1,
    
    // Atau tentukan beberapa halaman
    PagesSetup = new PagesSetup { Pages = new List<int> { 1, 3, 5 } },
    
    // Tentukan area tertentu untuk pencarian di dalamnya
    Rectangle = new Rectangle(100, 100, 400, 200)
};
```

### Pemfilteran Teks Lanjutan

Terapkan logika penyaringan khusus untuk persyaratan pencarian yang lebih kompleks:

```csharp
// Buat opsi pencarian dengan pemrosesan khusus
TextSearchOptions options = new TextSearchOptions
{
    AllPages = true,
    
    // Tentukan pemrosesan kustom menggunakan delegasi
    ProcessCompleted = (TextSignature signature) =>
    {
        // Logika validasi khusus
        bool isValid = signature.Text.Length > 5 && 
                      (signature.Text.Contains("Approved") || signature.Text.Contains("Verified"));
        
        return isValid;
    }
};
```

### Mencari Gaya Teks yang Berbeda

Gunakan properti font dan gaya untuk memfilter tanda tangan teks:

```csharp
// Buat opsi pencarian yang menargetkan tampilan teks tertentu
TextSearchOptions options = new TextSearchOptions
{
    // Filter berdasarkan nama font
    FontName = "Arial",
    
    // Filter berdasarkan rentang ukuran font
    MinFontSize = 10,
    MaxFontSize = 14,
    
    // Filter berdasarkan warna font
    ForeColor = System.Drawing.Color.Blue
};
```

### Mengekstrak Metadata Tanda Tangan

Ekstrak dan proses metadata yang terkait dengan tanda tangan teks:

```csharp
foreach (TextSignature signature in signatures)
{
    // Akses metadata tanda tangan
    if (signature.Metadata != null && signature.Metadata.Count > 0)
    {
        Console.WriteLine("Signature Metadata:");
        
        foreach (var item in signature.Metadata)
        {
            Console.WriteLine($"  {item.Key}: {item.Value}");
        }
    }
    
    // Periksa tanggal pembuatan dan modifikasi tanda tangan
    if (signature.CreatedOn.HasValue)
    {
        Console.WriteLine($"Created on: {signature.CreatedOn.Value}");
    }
    
    if (signature.ModifiedOn.HasValue)
    {
        Console.WriteLine($"Modified on: {signature.ModifiedOn.Value}");
    }
}
```

## Kesimpulan

Dalam panduan komprehensif ini, kami telah membahas cara mencari tanda tangan teks dalam dokumen menggunakan GroupDocs.Signature untuk .NET. Dari operasi pencarian dasar hingga teknik lanjutan, kini Anda memiliki pengetahuan untuk menerapkan fungsionalitas tanda tangan teks yang andal di aplikasi .NET Anda.

GroupDocs.Signature menyediakan kerangka kerja yang kuat dan fleksibel untuk bekerja dengan tanda tangan teks, memungkinkan Anda membangun sistem verifikasi dokumen yang canggih, solusi alur kerja otomatis, dan alat validasi kepatuhan.

## Pertanyaan yang Sering Diajukan

### Bisakah saya mencari tanda tangan teks dalam dokumen yang dilindungi kata sandi?

Ya, GroupDocs.Signature mendukung pencarian tanda tangan teks dalam dokumen yang dilindungi kata sandi. Anda dapat memberikan kata sandi saat menginisialisasi `Signature` obyek:

```csharp
LoadOptions loadOptions = new LoadOptions { Password = "your_password" };
using (Signature signature = new Signature(filePath, loadOptions))
{
    // Cari tanda tangan teks
}
```

### Format dokumen apa yang didukung untuk pencarian tanda tangan teks?

GroupDocs.Signature mendukung berbagai format dokumen termasuk PDF, dokumen Microsoft Office (Word, Excel, PowerPoint), format OpenOffice, gambar, dan banyak lagi.

### Dapatkah saya mencari tanda tangan teks dengan format tertentu seperti tebal atau miring?

Ya, Anda dapat mencari tanda tangan teks dengan format tertentu dengan menggunakan `FontBold` Dan `FontItalic` properti di `TextSearchOptions`:

```csharp
TextSearchOptions options = new TextSearchOptions
{
    FontBold = true,
    FontItalic = true
};
```

### Bagaimana cara meningkatkan kinerja pencarian untuk dokumen berukuran besar?

Untuk dokumen besar, Anda dapat mengoptimalkan kinerja pencarian dengan:

1. Membatasi pencarian ke halaman tertentu alih-alih mencari seluruh dokumen
2. Menggunakan kriteria pencarian yang lebih spesifik untuk mengurangi jumlah kecocokan
3. Menentukan area pencarian menggunakan `Rectangle` properti jika Anda tahu di mana tanda tangan biasanya berada
4. Menerapkan pagination di aplikasi Anda untuk memproses hasil pencarian secara batch

### Dapatkah saya mendeteksi apakah tanda tangan teks ditambahkan secara elektronik atau merupakan bagian dari konten dokumen asli?

GroupDocs.Signature dapat membedakan berbagai jenis elemen teks dalam dokumen. `SignatureImplementation` milik `TextSignature` menunjukkan apakah teks tersebut merupakan tanda tangan formal atau konten dokumen biasa. Namun, penentuan definitif mungkin bergantung pada bagaimana teks tersebut awalnya ditambahkan ke dalam dokumen.

## Lihat Juga

* [Referensi API](https://reference.groupdocs.com/signature/net/)
* [Contoh Kode di GitHub](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
* [Dokumentasi Produk](https://docs.groupdocs.com/signature/net/)
* [Halaman Produk](https://products.groupdocs.com/signature/net/)
* [Unduh Versi Terbaru](https://releases.groupdocs.com/signature/net/)
* [Artikel Blog](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
* [Forum Dukungan Gratis](https://forum.groupdocs.com/c/signature/13)
* [Lisensi Sementara](https://purchase.groupdocs.com/temporary-license/)