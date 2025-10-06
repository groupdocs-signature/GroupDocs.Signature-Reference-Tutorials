---
"description": "Terapkan verifikasi kode batang yang andal di aplikasi .NET dengan GroupDocs.Signature. Contoh kode lengkap dan praktik terbaik untuk memastikan keaslian dokumen."
"linktitle": "Verifikasi Kode Batang"
"second_title": "GroupDocs.Signature .NET API"
"title": "Verifikasi Tanda Tangan Kode Batang dalam Dokumen"
"url": "/id/net/verify-operations/verify-barcode/"
"weight": 10
type: docs
---
## Perkenalan

Kode batang telah menjadi bagian integral dari sistem manajemen dokumen modern, memungkinkan akses cepat ke informasi yang dikodekan sekaligus berfungsi sebagai fitur keamanan. GroupDocs.Signature untuk .NET menyediakan API canggih untuk memverifikasi tanda tangan kode batang dalam dokumen, memastikan keaslian dan integritasnya.

Tutorial komprehensif ini membahas proses penerapan verifikasi kode batang di aplikasi .NET menggunakan GroupDocs.Signature. Baik Anda menangani dokumen bisnis, sertifikat, kontrak, atau jenis dokumen apa pun yang menggunakan kode batang untuk autentikasi, panduan ini akan membantu Anda menerapkan fungsionalitas verifikasi yang andal.

## Prasyarat

Sebelum menerapkan fungsi verifikasi kode batang, pastikan Anda memiliki prasyarat berikut:

1. GroupDocs.Signature untuk .NET: Unduh dan instal pustaka dari [halaman unduhan](https://releases.groupdocs.com/signature/net/).
2. Lingkungan Pengembangan .NET: Visual Studio atau lingkungan pengembangan .NET yang kompatibel.
3. Pengetahuan Dasar: Keakraban dengan pemrograman C# dan konsep kerangka kerja .NET.
4. Dokumen Uji: Dokumen yang berisi tanda tangan kode batang untuk tujuan verifikasi.

## Mengimpor Namespace yang Diperlukan

Mulailah dengan mengimpor namespace yang diperlukan untuk mengakses fungsionalitas GroupDocs.Signature:

```csharp
using System;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

Mari kita uraikan proses verifikasi kode batang menjadi langkah-langkah yang jelas dan mudah dikelola:

## Langkah 1: Tentukan Jalur Dokumen

```csharp
// Jalur ke dokumen yang berisi tanda tangan kode batang
string filePath = "sample_multiple_signatures.docx";
```

Pastikan Anda mengganti jalur contoh dengan jalur sebenarnya ke dokumen Anda yang berisi tanda tangan kode batang.

## Langkah 2: Inisialisasi Objek Tanda Tangan

```csharp
// Buat instance kelas Signature dengan meneruskan jalur dokumen
using (Signature signature = new Signature(filePath))
{
    // Kode verifikasi akan diterapkan di sini
}
```

Kelas Signature adalah titik masuk utama untuk semua operasi di API GroupDocs.Signature.

## Langkah 3: Konfigurasikan Opsi Verifikasi Kode Batang

```csharp
// Tentukan opsi verifikasi kode batang
BarcodeVerifyOptions options = new BarcodeVerifyOptions()
{
    AllPages = true,           // Periksa semua halaman dokumen
    Text = "12345",            // Teks yang cocok dengan kode batang
    MatchType = TextMatchType.Contains // Tentukan kriteria pencocokan teks
};
```

Opsi verifikasi memungkinkan Anda menentukan kriteria spesifik untuk proses verifikasi:
- `AllPages`: Atur ke benar untuk memeriksa semua halaman dokumen
- `Text`: Konten teks yang akan dicocokkan dengan kode batang
- `MatchType`: Metode untuk pencocokan teks (Berisi, Tepat, DimulaiDengan, BerakhirDengan)

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
    Console.WriteLine($"Document {filePath} contains valid barcode signatures!");
    
    // Menampilkan informasi tentang tanda tangan yang berhasil
    foreach (BarcodeSignature barcodeSignature in result.Succeeded)
    {
        Console.WriteLine($"\nFound valid barcode signature:");
        Console.WriteLine($"Text: {barcodeSignature.Text}");
        Console.WriteLine($"Type: {barcodeSignature.EncodeType.TypeName}");
        Console.WriteLine($"Location: Page {barcodeSignature.PageNumber}, {barcodeSignature.Left}x{barcodeSignature.Top}");
    }
}
else
{
    Console.WriteLine($"Document {filePath} failed verification process.");
    Console.WriteLine($"Number of failed signatures: {result.Failed.Count}");
}
```

Kode ini memeriksa apakah verifikasi berhasil dan memberikan informasi terperinci tentang tanda tangan kode batang yang diverifikasi.

## Contoh Lengkap

Berikut contoh kerja lengkap yang menunjukkan verifikasi kode batang:

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
                    BarcodeVerifyOptions options = new BarcodeVerifyOptions()
                    {
                        AllPages = true,
                        Text = "12345",
                        MatchType = TextMatchType.Contains
                    };
                    
                    // Verifikasi tanda tangan dokumen
                    VerificationResult result = signature.Verify(options);
                    
                    // Hasil verifikasi proses
                    if (result.IsValid)
                    {
                        Console.WriteLine($"Document {filePath} contains valid barcode signatures!");
                        
                        foreach (BarcodeSignature item in result.Succeeded)
                        {
                            Console.WriteLine($"\nValid signature found with text: {item.Text}");
                            Console.WriteLine($"Barcode type: {item.EncodeType.TypeName}");
                            Console.WriteLine($"Page: {item.PageNumber}");
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

### Memverifikasi Jenis Kode Batang Tertentu

Jika Anda mengetahui jenis kode batang tertentu yang Anda cari, Anda dapat membatasi verifikasi ke jenis tersebut:

```csharp
BarcodeVerifyOptions options = new BarcodeVerifyOptions()
{
    EncodeType = BarcodeTypes.Code128,  // Verifikasi hanya kode batang Code128
    Text = "PROD-12345",
    MatchType = TextMatchType.Exact
};
```

### Memverifikasi Kode Batang pada Halaman Tertentu

Untuk dokumen multi-halaman, Anda dapat membatasi verifikasi ke halaman tertentu:

```csharp
BarcodeVerifyOptions options = new BarcodeVerifyOptions()
{
    AllPages = false,
    PageNumber = 2,  // Verifikasi hanya di halaman 2
    Text = "INV-2023"
};
```

### Menggunakan Ekspresi Reguler untuk Verifikasi

Untuk pencocokan pola yang lebih fleksibel, Anda dapat menggunakan ekspresi reguler:

```csharp
BarcodeVerifyOptions options = new BarcodeVerifyOptions()
{
    Text = "INV-\\d{4}-\\d{2}",  // Cocokkan nomor faktur seperti INV-2023-01
    MatchType = TextMatchType.Regex
};
```

### Memverifikasi Beberapa Jenis Kode Batang Secara Bersamaan

Anda dapat membuat beberapa opsi verifikasi untuk memeriksa berbagai jenis kode batang:

```csharp
// Buat daftar opsi verifikasi
List<VerifyOptions> listOptions = new List<VerifyOptions>();

// Tambahkan verifikasi Kode QR
listOptions.Add(new BarcodeVerifyOptions()
{
    EncodeType = BarcodeTypes.QR,
    Text = "Security"
});

// Tambahkan verifikasi Code128
listOptions.Add(new BarcodeVerifyOptions()
{
    EncodeType = BarcodeTypes.Code128,
    Text = "12345"
});

// Verifikasi dengan beberapa opsi
VerificationResult result = signature.Verify(listOptions);
```

## Praktik Terbaik untuk Verifikasi Kode Batang

1. Penanganan Kesalahan: Selalu terapkan penanganan kesalahan yang tepat untuk mengelola skenario tak terduga dengan baik.
2. Optimalisasi Performa: Untuk dokumen besar, pertimbangkan untuk memverifikasi halaman tertentu daripada keseluruhan dokumen.
3. Pencatatan: Terapkan pencatatan untuk melacak upaya verifikasi dan hasil untuk tujuan audit.
4. Pertimbangan Keamanan: Simpan kriteria verifikasi dengan aman, terutama jika kriteria tersebut merupakan bagian dari infrastruktur keamanan Anda.
5. Pengujian: Verifikasi uji dengan berbagai format dokumen dan jenis kode batang untuk memastikan kompatibilitas.

## Pemecahan Masalah Umum

### Kode Batang Tidak Terdeteksi
- Pastikan kode batang terlihat jelas di dokumen
- Periksa apakah jenis kode batang didukung oleh GroupDocs.Signature
- Verifikasi bahwa kode batang tidak terdistorsi atau rusak

### Kegagalan Verifikasi
- Konfirmasikan bahwa kriteria verifikasi (teks, jenis kode batang) sudah benar
- Periksa apakah MatchType sesuai dengan kasus penggunaan Anda
- Verifikasi bahwa dokumen belum dimodifikasi sejak kode batang diterapkan

### Masalah Kinerja
- Optimalkan verifikasi dengan menargetkan halaman tertentu yang diperkirakan terdapat kode batang
- Batasi verifikasi ke jenis kode batang tertentu jika sudah diketahui sebelumnya

## Kesimpulan

Verifikasi kode batang merupakan alat penting untuk memastikan keaslian dan integritas dokumen dalam sistem manajemen dokumen modern. GroupDocs.Signature untuk .NET menyediakan API yang komprehensif dan mudah digunakan untuk menerapkan fungsionalitas verifikasi kode batang yang andal dalam aplikasi .NET Anda.

Dengan mengikuti panduan langkah demi langkah ini, Anda telah mempelajari cara:
- Konfigurasikan dan inisialisasi proses verifikasi
- Tentukan berbagai kriteria verifikasi
- Memproses dan menginterpretasikan hasil verifikasi
- Terapkan skenario verifikasi lanjutan

Kemampuan ini memungkinkan Anda membangun sistem pemrosesan dokumen yang aman dan andal yang dapat memverifikasi keaslian kode batang di berbagai format dokumen.

## Tanya Jawab Umum

### Format dokumen apa yang didukung untuk verifikasi kode batang?
GroupDocs.Signature mendukung berbagai format dokumen termasuk PDF, dokumen Word (DOC, DOCX), lembar kerja Excel (XLS, XLSX), presentasi PowerPoint (PPT, PPTX), gambar, dan banyak lagi.

### Bisakah GroupDocs.Signature memverifikasi beberapa kode batang dalam satu dokumen?
Ya, GroupDocs.Signature dapat memverifikasi beberapa kode batang dalam satu dokumen. Hasil verifikasi akan mencakup semua kode batang yang cocok.

### Jenis kode batang apa yang didukung untuk verifikasi?
GroupDocs.Signature mendukung berbagai jenis kode batang termasuk Code39, Code128, EAN13, EAN8, QR Code, DataMatrix, PDF417, dan banyak lainnya.

### Bisakah saya memverifikasi kode batang dalam dokumen yang dilindungi kata sandi?
Ya, GroupDocs.Signature menyediakan opsi untuk menentukan kata sandi dokumen saat membuka dokumen yang dilindungi untuk verifikasi.

### Apakah mungkin untuk memverifikasi kode batang yang berisi data biner, bukan teks?
Ya, GroupDocs.Signature menyediakan opsi untuk memverifikasi kode batang dengan data biner melalui `BinaryData` properti opsi verifikasi.

### Sumber Terkait
* [Referensi API GroupDocs.Signature](https://reference.groupdocs.com/signature/net/)
* [Unduhan GroupDocs.Signature](https://releases.groupdocs.com/signature/net/)
* [Contoh Kode di GitHub](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
* [Dokumentasi](https://docs.groupdocs.com/signature/net/)
* [Halaman Produk](https://products.groupdocs.com/signature/net/)
* [Artikel Blog](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
* [Forum Dukungan](https://forum.groupdocs.com/c/signature/13)
* [Lisensi Sementara](https://purchase.groupdocs.com/temporary-license/)