---
"description": "Kuasai verifikasi tanda tangan teks di aplikasi .NET dengan GroupDocs.Signature. Panduan implementasi langkah demi langkah dengan contoh kode lengkap dan praktik terbaik."
"linktitle": "Verifikasi Teks"
"second_title": "GroupDocs.Signature .NET API"
"title": "Verifikasi Tanda Tangan Teks dalam Dokumen"
"url": "/id/net/verify-operations/verify-text/"
"weight": 13
---

## Perkenalan

Tanda tangan teks, meskipun seringkali lebih sederhana daripada tanda tangan digital atau elektronik, memainkan peran penting dalam manajemen dan verifikasi dokumen. Baik itu tanda air, teks footer, atau pola konten tertentu, validasi keberadaan dan integritas tanda tangan teks merupakan aspek penting dalam proses verifikasi dokumen.

GroupDocs.Signature untuk .NET menyediakan API yang andal untuk memverifikasi tanda tangan teks dalam berbagai format dokumen. Tutorial komprehensif ini akan memandu Anda dalam menerapkan fungsi verifikasi teks di aplikasi .NET Anda, memastikan dokumen Anda tetap utuh dan autentik.

## Prasyarat

Sebelum menerapkan fungsi verifikasi teks, pastikan Anda memiliki prasyarat berikut:

1. GroupDocs.Signature untuk .NET: Unduh dan instal pustaka dari [halaman unduhan](https://releases.groupdocs.com/signature/net/).
2. Lingkungan Pengembangan .NET: Visual Studio atau lingkungan pengembangan .NET yang kompatibel.
3. Pengetahuan Dasar: Keakraban dengan pemrograman C# dan konsep kerangka kerja .NET.
4. Dokumen Uji: Dokumen yang berisi tanda tangan teks untuk tujuan verifikasi.

## Mengimpor Namespace yang Diperlukan

Mulailah dengan mengimpor namespace yang diperlukan untuk mengakses fungsionalitas GroupDocs.Signature:

```csharp
using System;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

Mari kita uraikan proses verifikasi teks menjadi langkah-langkah yang jelas dan mudah dikelola:

## Langkah 1: Tentukan Jalur Dokumen

```csharp
// Jalur ke dokumen yang berisi tanda tangan teks
string filePath = "sample_multiple_signatures.docx";
```

Pastikan Anda mengganti jalur contoh dengan jalur sebenarnya ke dokumen Anda yang berisi tanda tangan teks.

## Langkah 2: Inisialisasi Objek Tanda Tangan

```csharp
// Buat instance kelas Signature dengan meneruskan jalur dokumen
using (Signature signature = new Signature(filePath))
{
    // Kode verifikasi akan diterapkan di sini
}
```

Kelas Signature adalah titik masuk utama untuk semua operasi di API GroupDocs.Signature.

## Langkah 3: Konfigurasikan Opsi Verifikasi Teks

```csharp
// Tentukan opsi verifikasi teks
TextVerifyOptions options = new TextVerifyOptions()
{
    AllPages = true,                               // Periksa semua halaman dokumen
    SignatureImplementation = TextSignatureImplementation.Native,
    Text = "signature",                            // Teks yang akan diverifikasi
    MatchType = TextMatchType.Contains             // Tentukan kriteria pencocokan
};
```

Opsi verifikasi memungkinkan Anda menentukan kriteria spesifik untuk proses verifikasi:
- `AllPages`: Atur ke benar untuk memeriksa semua halaman dokumen
- `SignatureImplementation`: Tentukan bagaimana teks diimplementasikan (Asli atau Stiker)
- `Text`: Konten teks yang cocok dalam dokumen
- `MatchType`: Metode untuk pencocokan teks (Berisi, Tepat, DimulaiDengan, dll.)

## Langkah 4: Jalankan Proses Verifikasi

```csharp
// Lakukan verifikasi
VerificationResult result = signature.Verify(options);
```

Ini mengeksekusi proses verifikasi berdasarkan opsi yang Anda tentukan.

## Langkah 5: Hasil Verifikasi Proses

```csharp
// Periksa hasil verifikasi dan proses sesuai ketentuan
if (result.IsValid)
{
    Console.WriteLine($"Document {filePath} contains valid text signatures!");
    
    // Menampilkan informasi tentang tanda tangan yang berhasil
    foreach (TextSignature textSignature in result.Succeeded)
    {
        Console.WriteLine($"\nFound valid text signature:");
        Console.WriteLine($"Text: {textSignature.Text}");
        Console.WriteLine($"Location: Page {textSignature.PageNumber}, {textSignature.Left}x{textSignature.Top}");
    }
}
else
{
    Console.WriteLine($"Document {filePath} failed verification process.");
    Console.WriteLine($"Number of failed signatures: {result.Failed.Count}");
}
```

Kode ini memeriksa apakah verifikasi berhasil dan memberikan informasi terperinci tentang tanda tangan teks yang diverifikasi.

## Contoh Lengkap

Berikut contoh kerja lengkap yang menunjukkan verifikasi tanda tangan teks:

```csharp
using System;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;

namespace GroupDocs.Signature.Examples
{
    class Program
    {
        static void Main(string[] args)
        {
            // Jalur dokumen
            string filePath = "sample_multiple_signatures.docx";
            
            try
            {
                // Inisialisasi instance Tanda Tangan
                using (Signature signature = new Signature(filePath))
                {
                    // Siapkan opsi verifikasi
                    TextVerifyOptions options = new TextVerifyOptions()
                    {
                        AllPages = true,
                        SignatureImplementation = TextSignatureImplementation.Native,
                        Text = "signature",
                        MatchType = TextMatchType.Contains
                    };
                    
                    // Verifikasi tanda tangan dokumen
                    VerificationResult result = signature.Verify(options);
                    
                    // Hasil verifikasi proses
                    if(result.IsValid)
                    {
                        Console.WriteLine($"\nDocument {filePath} was verified successfully!");
                        foreach (TextSignature item in result.Succeeded)
                        {
                            Console.WriteLine($"\nValid signature is found with text: {item.Text}");
                            Console.WriteLine($"Location: Page {item.PageNumber}, position {item.Left}x{item.Top}");
                        }
                    }
                    else
                    {
                        Console.WriteLine($"\nDocument {filePath} failed verification process.");
                    }
                }
            }
            catch (Exception ex)
            {
                Console.WriteLine($"Error: {ex.Message}");
            }
        }
    }
}
```

## Skenario Verifikasi Lanjutan

GroupDocs.Signature menyediakan opsi tambahan untuk skenario verifikasi yang lebih kompleks:

### Menggunakan Ekspresi Reguler untuk Verifikasi

Untuk pencocokan pola yang lebih fleksibel, Anda dapat menggunakan ekspresi reguler:

```csharp
TextVerifyOptions options = new TextVerifyOptions()
{
    Text = "Invoice\\s+#\\d{5,6}",  // Cocokkan pola seperti "Faktur #12345"
    MatchType = TextMatchType.Regex
};
```

### Memverifikasi Teks di Area Dokumen Tertentu

Anda dapat membatasi verifikasi ke area tertentu dalam dokumen:

```csharp
TextVerifyOptions options = new TextVerifyOptions()
{
    AllPages = false,
    PageNumber = 1,  // Verifikasi hanya di halaman pertama
    
    // Tentukan area untuk pencarian (koordinat dalam poin)
    PagesSetup = new PagesSetup() 
    { 
        FirstPage = true,
        LastPage = false,
        OddPages = false,
        EvenPages = false 
    },
    
    // Luas persegi panjang dalam milimeter
    Rectangle = new Rectangle(10, 10, 100, 30),
    
    Text = "Confidential"
};
```

### Memverifikasi Beberapa Pola Teks Secara Bersamaan

Anda dapat membuat beberapa opsi verifikasi untuk memeriksa pola teks yang berbeda:

```csharp
// Buat daftar opsi verifikasi
List<VerifyOptions> listOptions = new List<VerifyOptions>();

// Tambahkan verifikasi teks pertama
listOptions.Add(new TextVerifyOptions()
{
    Text = "Confidential",
    MatchType = TextMatchType.Exact
});

// Tambahkan verifikasi teks kedua
listOptions.Add(new TextVerifyOptions()
{
    Text = "Do not copy",
    MatchType = TextMatchType.Contains
});

// Verifikasi dengan beberapa opsi
VerificationResult result = signature.Verify(listOptions);
```

### Memverifikasi Teks dengan Tampilan Tertentu

Anda juga dapat memverifikasi teks dengan karakteristik pemformatan tertentu:

```csharp
TextVerifyOptions options = new TextVerifyOptions()
{
    Text = "APPROVED",
    MatchType = TextMatchType.Exact,
    
    // Verifikasi properti tampilan tertentu
    ForegroundColorRGB = System.Drawing.Color.Green,
    Font = new SignatureFont() { FontFamily = "Arial", FontSize = 12, Bold = true }
};
```

## Praktik Terbaik untuk Verifikasi Teks

1. Pilih Jenis Pencocokan yang Sesuai: Pilih jenis pencocokan yang tepat (Berisi, Tepat, Regex) berdasarkan persyaratan verifikasi Anda.
2. Optimalkan Performa: Untuk dokumen besar, pertimbangkan untuk memverifikasi halaman tertentu daripada keseluruhan dokumen.
3. Penanganan Kesalahan: Terapkan penanganan kesalahan yang tepat untuk mengelola skenario tak terduga dengan baik.
4. Pertimbangkan Kepekaan Huruf Besar-Kecil: Perhatikan kepekaan huruf besar-kecil dalam pencocokan teks, terutama untuk verifikasi penting.
5. Uji Secara Menyeluruh: Uji verifikasi dengan berbagai format dokumen dan pola teks untuk memastikan kompatibilitas.

## Pemecahan Masalah Umum

### Teks Tidak Terdeteksi
- Periksa apakah format teks atau pengkodean memengaruhi deteksi
- Pastikan teks benar-benar ada dalam dokumen sebagai teks biasa (bukan gambar)
- Coba kriteria pencocokan yang berbeda (Berisi, bukan Tepat)

### Masalah Kinerja
- Optimalkan verifikasi dengan menargetkan halaman atau area tertentu
- Gunakan pola teks yang lebih spesifik untuk mengurangi positif palsu

### Kegagalan Verifikasi
- Periksa apakah spasi, karakter khusus, atau pemformatan memengaruhi kecocokan
- Verifikasi bahwa teks bukan bagian dari gambar yang dipindai (yang memerlukan OCR)
- Pastikan dokumen belum dimodifikasi sejak teks ditambahkan

## Kesimpulan

Verifikasi teks adalah pendekatan yang serbaguna dan praktis untuk autentikasi dokumen yang dapat digunakan sendiri atau dikombinasikan dengan metode verifikasi lainnya. GroupDocs.Signature untuk .NET menyediakan API yang komprehensif dan mudah digunakan untuk menerapkan fungsionalitas verifikasi teks yang andal dalam aplikasi .NET Anda.

Dengan mengikuti panduan langkah demi langkah ini, Anda telah mempelajari cara:
- Konfigurasikan dan inisialisasi proses verifikasi teks
- Tentukan berbagai kriteria verifikasi
- Memproses dan menginterpretasikan hasil verifikasi
- Terapkan skenario verifikasi lanjutan

Kemampuan ini memungkinkan Anda membangun sistem pemrosesan dokumen yang aman dan andal yang dapat memverifikasi keaslian teks di berbagai format dokumen.

## Tanya Jawab Umum

### Bisakah GroupDocs.Signature memverifikasi teks dalam dokumen yang dipindai?
GroupDocs.Signature terutama dirancang untuk verifikasi teks digital. Untuk dokumen yang dipindai, Anda perlu menggunakan teknologi OCR (Pengenalan Karakter Optik) terlebih dahulu untuk mengonversi gambar pindaian menjadi teks.

### Format dokumen apa yang didukung untuk verifikasi teks?
GroupDocs.Signature mendukung berbagai format dokumen termasuk PDF, dokumen Word (DOC, DOCX), lembar kerja Excel (XLS, XLSX), presentasi PowerPoint (PPT, PPTX), gambar, dan banyak lagi.

### Dapatkah saya memverifikasi teks yang diformat (tebal, miring, font tertentu)?
Ya, GroupDocs.Signature menyediakan opsi untuk memverifikasi teks dengan karakteristik pemformatan tertentu termasuk jenis font, ukuran, gaya (tebal, miring), dan warna.

### Apakah mungkin untuk memverifikasi teks dalam dokumen yang dilindungi kata sandi?
Ya, GroupDocs.Signature menyediakan opsi untuk menentukan kata sandi dokumen saat membuka dokumen yang dilindungi untuk verifikasi.

### Bisakah saya memverifikasi tanda air dan teks latar belakang?
Ya, GroupDocs.Signature dapat memverifikasi berbagai jenis tanda tangan teks termasuk tanda air dan teks latar belakang, tergantung pada bagaimana penerapannya dalam dokumen.

### Sumber Terkait
* [Referensi API GroupDocs.Signature](https://reference.groupdocs.com/signature/net/)
* [Unduhan GroupDocs.Signature](https://releases.groupdocs.com/signature/net/)
* [Contoh Kode di GitHub](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
* [Dokumentasi](https://docs.groupdocs.com/signature/net/)
* [Halaman Produk](https://products.groupdocs.com/signature/net/)
* [Artikel Blog](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
* [Forum Dukungan](https://forum.groupdocs.com/c/signature/13)
* [Lisensi Sementara](https://purchase.groupdocs.com/temporary-license/)