---
"description": "Pelajari cara memverifikasi kode QR dalam dokumen menggunakan GroupDocs.Signature untuk .NET. Panduan lengkap dengan contoh kode dan praktik terbaik untuk autentikasi dokumen."
"linktitle": "Verifikasi Kode QR"
"second_title": "GroupDocs.Signature .NET API"
"title": "Verifikasi Kode QR dalam Dokumen"
"url": "/id/net/verify-operations/verify-qr-code/"
"weight": 12
type: docs
---
## Perkenalan

Keamanan dokumen merupakan aspek penting dalam operasional bisnis modern. Kode QR telah menjadi metode yang semakin populer untuk menyisipkan informasi ke dalam dokumen yang dapat diverifikasi keasliannya. GroupDocs.Signature untuk .NET menyediakan solusi yang andal dan fleksibel untuk memverifikasi kode QR yang tertanam dalam dokumen dalam berbagai format.

Tutorial komprehensif ini akan memandu Anda melalui proses penerapan verifikasi kode QR di aplikasi .NET Anda, memastikan dokumen Anda tetap terjaga integritas dan keasliannya.

## Prasyarat

Sebelum menerapkan fungsi verifikasi kode QR, pastikan Anda memiliki prasyarat berikut:

1. GroupDocs.Signature untuk .NET: Unduh dan instal pustaka dari [halaman unduhan](https://releases.groupdocs.com/signature/net/).
2. Lingkungan Pengembangan: Visual Studio atau lingkungan pengembangan .NET yang kompatibel.
3. Dokumen Uji: Dokumen yang berisi tanda tangan kode QR untuk tujuan verifikasi.
4. Pengetahuan Dasar: Keakraban dengan pemrograman C# dan konsep kerangka kerja .NET.

## Mengimpor Ruang Nama

Mulailah dengan mengimpor namespace yang diperlukan untuk mengakses fungsionalitas GroupDocs.Signature:

```csharp
using System;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

## Proses Verifikasi Kode QR Langkah demi Langkah

Ikuti langkah-langkah terperinci ini untuk memverifikasi kode QR dalam dokumen Anda:

### Langkah 1: Tentukan Jalur Dokumen

```csharp
// Berikan jalur ke dokumen yang berisi tanda tangan kode QR
string filePath = "sample_multiple_signatures.docx";
```

Pastikan Anda mengganti jalur contoh dengan jalur sebenarnya ke dokumen Anda.

### Langkah 2: Inisialisasi Objek Tanda Tangan

```csharp
// Buat instance Tanda Tangan dengan meneruskan jalur dokumen
using (Signature signature = new Signature(filePath))
{
    // Kode verifikasi akan diterapkan di sini
}
```

Kelas Signature adalah titik masuk utama untuk semua operasi di API GroupDocs.Signature.

### Langkah 3: Konfigurasikan Opsi Verifikasi Kode QR

```csharp
// Tentukan opsi verifikasi kode QR
QrCodeVerifyOptions options = new QrCodeVerifyOptions()
{
    AllPages = true, // Periksa semua halaman dokumen
    Text = "John",   // Teks untuk verifikasi dalam kode QR
    MatchType = TextMatchType.Contains // Tentukan kriteria pencocokan teks
};
```

Opsi verifikasi memungkinkan Anda menentukan kriteria spesifik untuk proses verifikasi:
- `AllPages`: Atur ke benar untuk memeriksa semua halaman dokumen (perilaku default)
- `Text`: Konten teks yang cocok dengan kode QR
- `MatchType`: Metode untuk pencocokan teks (Berisi, Tepat, DimulaiDengan, dll.)

### Langkah 4: Jalankan Proses Verifikasi

```csharp
// Lakukan verifikasi
VerificationResult result = signature.Verify(options);
```

Ini mengeksekusi proses verifikasi berdasarkan opsi yang Anda tentukan.

### Langkah 5: Hasil Verifikasi Proses

```csharp
// Periksa hasil verifikasi dan proses sesuai ketentuan
if (result.IsValid)
{
    Console.WriteLine($"Document {filePath} contains valid QR code signature!");
    
    // Menampilkan informasi tentang tanda tangan yang berhasil
    foreach (QrCodeSignature signature in result.Succeeded)
    {
        Console.WriteLine($"Found valid QR Code signature with text: {signature.Text}");
        Console.WriteLine($"QR Code type: {signature.EncodeType.TypeName}");
        Console.WriteLine($"Location: Page {signature.PageNumber}, {signature.Left}x{signature.Top}");
    }
}
else
{
    Console.WriteLine($"Document {filePath} failed verification process.");
    Console.WriteLine($"Number of failed signatures: {result.Failed.Count}");
}
```

Penanganan hasil verifikasi yang tepat memungkinkan aplikasi Anda mengambil tindakan yang tepat berdasarkan hasil verifikasi.

## Contoh Lengkap

Berikut ini contoh lengkap dan berfungsi yang menunjukkan verifikasi kode QR:

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
            
            // Inisialisasi instance Tanda Tangan
            using (Signature signature = new Signature(filePath))
            {
                // Siapkan opsi verifikasi
                QrCodeVerifyOptions options = new QrCodeVerifyOptions()
                {
                    AllPages = true,
                    Text = "John",
                    MatchType = TextMatchType.Contains
                };
                
                // Verifikasi tanda tangan dokumen
                VerificationResult result = signature.Verify(options);
                
                // Hasil verifikasi proses
                if (result.IsValid)
                {
                    Console.WriteLine($"Document {filePath} contains valid QR code signature!");
                    
                    foreach (QrCodeSignature qrSignature in result.Succeeded)
                    {
                        Console.WriteLine($"Found valid QR Code with text: {qrSignature.Text}");
                    }
                }
                else
                {
                    Console.WriteLine($"Document {filePath} failed verification process.");
                }
            }
        }
    }
}
```

## Opsi Verifikasi Lanjutan

GroupDocs.Signature menyediakan opsi tambahan untuk skenario verifikasi yang lebih kompleks:

### Memverifikasi Jenis Kode QR Tertentu

```csharp
QrCodeVerifyOptions options = new QrCodeVerifyOptions()
{
    EncodeType = QrCodeTypes.QR,  // Verifikasi hanya kode QR standar
    Text = "Confidential",
    MatchType = TextMatchType.Exact
};
```

### Memverifikasi pada Halaman Tertentu

```csharp
QrCodeVerifyOptions options = new QrCodeVerifyOptions()
{
    AllPages = false,
    PageNumber = 2,  // Verifikasi hanya di halaman 2
    Text = "Approved"
};
```

### Menggunakan Ekspresi Reguler untuk Verifikasi

```csharp
QrCodeVerifyOptions options = new QrCodeVerifyOptions()
{
    Text = "INV-\\d{6}",  // Cocokkan nomor faktur (misalnya, INV-123456)
    MatchType = TextMatchType.Regex
};
```

## Praktik Terbaik untuk Verifikasi Kode QR

1. Selalu validasi masukan: Pastikan jalur dokumen dan kriteria verifikasi valid sebelum diproses.
2. Terapkan penanganan kesalahan: Gunakan blok try-catch untuk menangani potensi pengecualian selama verifikasi.
3. Pertimbangkan kinerja: Untuk dokumen besar, pertimbangkan untuk memverifikasi halaman tertentu daripada keseluruhan dokumen.
4. Hasil verifikasi log: Menyimpan log proses verifikasi untuk keperluan audit.
5. Uji dengan berbagai format dokumen: Pastikan verifikasi Anda berfungsi di semua format dokumen yang diperlukan.

## Kesimpulan

Verifikasi kode QR dalam dokumen merupakan aspek penting untuk memastikan keaslian dan integritas dokumen. GroupDocs.Signature untuk .NET menyediakan API yang komprehensif dan mudah digunakan untuk menerapkan verifikasi kode QR di aplikasi .NET Anda.

Dengan mengikuti tutorial ini, Anda telah mempelajari cara:
- Konfigurasikan dan inisialisasi proses verifikasi
- Tentukan berbagai kriteria verifikasi
- Memproses dan menginterpretasikan hasil verifikasi
- Terapkan opsi verifikasi lanjutan

Pengetahuan ini memberdayakan Anda untuk meningkatkan keamanan dan keandalan sistem manajemen dokumen Anda.

## Pertanyaan yang Sering Diajukan

### Bisakah GroupDocs.Signature memverifikasi beberapa kode QR dalam satu dokumen?
Ya, GroupDocs.Signature dapat memverifikasi beberapa kode QR dalam satu dokumen. Hasil verifikasi akan mencakup semua kode QR yang cocok.

### Format dokumen apa yang didukung untuk verifikasi kode QR?
GroupDocs.Signature mendukung berbagai format dokumen termasuk PDF, Word (DOC, DOCX), Excel (XLS, XLSX), PowerPoint (PPT, PPTX), gambar, dan banyak lagi.

### Bisakah saya memverifikasi kode QR dengan enkripsi atau format tertentu?
Ya, GroupDocs.Signature menyediakan opsi untuk memverifikasi kode QR dengan jenis penyandian dan pola pemformatan konten tertentu.

### Apakah mungkin untuk memverifikasi kode QR yang dibuat oleh aplikasi pihak ketiga?
Ya, GroupDocs.Signature dapat memverifikasi kode QR standar yang dihasilkan oleh sebagian besar aplikasi, selama kode tersebut mengikuti format kode QR standar.

### Bagaimana cara menangani kode QR yang berisi data biner, bukan teks?
GroupDocs.Signature menyediakan opsi untuk memverifikasi kode QR dengan data biner melalui `BinaryData` properti opsi verifikasi.

### Sumber Terkait
* [Referensi API GroupDocs.Signature](https://reference.groupdocs.com/signature/net/)
* [Unduhan GroupDocs.Signature](https://releases.groupdocs.com/signature/net/)
* [Contoh Kode di GitHub](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
* [Dokumentasi](https://docs.groupdocs.com/signature/net/)
* [Halaman Produk](https://products.groupdocs.com/signature/net/)
* [Artikel Blog](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
* [Forum Dukungan](https://forum.groupdocs.com/c/signature/13)
* [Lisensi Sementara](https://purchase.groupdocs.com/temporary-license/)