---
"description": "Pelajari cara memperbarui tanda tangan kode QR secara dinamis dalam berbagai format dokumen dengan GroupDocs.Signature untuk .NET. Panduan pengembang komprehensif untuk solusi manajemen dokumen modern."
"linktitle": "Perbarui Kode QR"
"second_title": "GroupDocs.Signature .NET API"
"title": "Perbarui Tanda Tangan Kode QR di Dokumen"
"url": "/id/net/update-operations/update-qr-code/"
"weight": 12
---

## Perkenalan
Dalam lingkungan bisnis digital masa kini, kode QR telah menjadi elemen penting dalam sistem manajemen dan autentikasi dokumen. Kode QR menyediakan cara yang praktis untuk mengodekan dan mengakses informasi, mulai dari URL sederhana hingga data terstruktur yang kompleks. GroupDocs.Signature untuk .NET menawarkan perangkat komprehensif yang memungkinkan pengembang mengintegrasikan kemampuan tanda tangan elektronik canggih ke dalam aplikasi mereka, termasuk kemampuan untuk memperbarui tanda tangan kode QR yang ada di dalam dokumen.

Tutorial ini berfokus secara khusus pada pembaruan tanda tangan kode QR dalam dokumen menggunakan GroupDocs.Signature untuk .NET. Baik Anda perlu mengubah posisi, ukuran, atau data terkode dari kode QR yang sudah ada, panduan ini akan memandu Anda melalui prosesnya langkah demi langkah dengan contoh dan penjelasan kode yang jelas.

## Prasyarat
Sebelum menyelami pembaruan tanda tangan kode QR dengan GroupDocs.Signature untuk .NET, pastikan Anda memiliki prasyarat berikut:

1. Lingkungan Pengembangan: Lingkungan pengembangan .NET yang berfungsi, seperti Visual Studio 2017 atau yang lebih baru.
2. Pustaka GroupDocs.Signature: Unduh dan instal pustaka GroupDocs.Signature untuk .NET dari [halaman unduhan](https://releases.groupdocs.com/signature/net/).
3. Lisensi (Opsional): Untuk penggunaan produksi, Anda memerlukan lisensi yang valid. Untuk tujuan pengujian, Anda dapat menggunakan [lisensi sementara](https://purchase.groupdocs.com/temporary-license/).
4. Contoh Dokumen: Dokumen yang berisi tanda tangan kode QR yang ingin Anda perbarui.
5. Pengetahuan Dasar C#: Keakraban dengan konsep pemrograman C#.

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

Mari kita uraikan proses pembaruan tanda tangan kode QR menjadi langkah-langkah yang jelas dan mudah dikelola:

## Langkah 1: Siapkan Jalur Dokumen
Pertama, tentukan jalur untuk dokumen sumber Anda dan tempat dokumen yang diperbarui akan disimpan:

```csharp
// Jalur ke dokumen sumber dengan tanda tangan kode QR
string filePath = "sample_multiple_signatures.docx";

// Dapatkan nama file untuk keluaran
string fileName = Path.GetFileName(filePath);

// Tentukan direktori keluaran dan jalur file
string outputDirectory = Path.Combine("Your Document Directory", "UpdateQRCode");
string outputFilePath = Path.Combine(outputDirectory, fileName);

// Pastikan direktori keluaran ada
Directory.CreateDirectory(outputDirectory);
```

## Langkah 2: Salin Dokumen Sumber
Karena operasi pembaruan memodifikasi dokumen secara langsung, buat salinan dokumen asli untuk menyimpannya:

```csharp
// Buat salinan dokumen asli
File.Copy(filePath, outputFilePath, true);
```

## Langkah 3: Inisialisasi Instansi Tanda Tangan
Buat contoh dari `Signature` kelas untuk bekerja dengan dokumen:

```csharp
// Inisialisasi instance Tanda Tangan dengan jalur file keluaran
using (Signature signature = new Signature(outputFilePath))
{
    // Operasi tanda tangan akan dilakukan di sini
}
```

## Langkah 4: Konfigurasikan Opsi Pencarian Kode QR
Siapkan opsi pencarian untuk menemukan tanda tangan kode QR yang ada dalam dokumen:

```csharp
// Konfigurasikan opsi pencarian untuk tanda tangan kode QR
QrCodeSearchOptions options = new QrCodeSearchOptions();

// Anda dapat menyesuaikan opsi pencarian jika diperlukan
// options.AllPages = true; // Cari di semua halaman
// options.PageNumber = 1; // Cari di halaman tertentu
// options.EncodeType = QrCodeTypes.QR; // Cari jenis kode QR tertentu
```

## Langkah 5: Cari Tanda Tangan Kode QR
Gunakan opsi pencarian yang dikonfigurasi untuk menemukan tanda tangan kode QR dalam dokumen:

```csharp
// Cari tanda tangan kode QR
List<QrCodeSignature> signatures = signature.Search<QrCodeSignature>(options);
```

## Langkah 6: Perbarui Properti Tanda Tangan Kode QR
Jika tanda tangan kode QR ditemukan, perbarui propertinya sesuai kebutuhan:

```csharp
// Periksa apakah tanda tangan ditemukan
if (signatures.Count > 0)
{
    // Dapatkan tanda tangan kode QR pertama
    QrCodeSignature qrCodeSignature = signatures[0];
    
    // Perbarui posisi
    qrCodeSignature.Left = 200;
    qrCodeSignature.Top = 250;
    
    // Perbarui ukuran
    qrCodeSignature.Width = 200;
    qrCodeSignature.Height = 200;
    
    // Anda juga dapat memperbarui data kode QR jika diperlukan
    // qrCodeSignature.Text = "Data Kode QR yang Diperbarui";
    
    // Terapkan pembaruan
    bool result = signature.Update(qrCodeSignature);
    
    // Periksa hasilnya
    if (result)
    {
        Console.WriteLine($"QR Code signature was successfully updated in the document '{fileName}'.");
        Console.WriteLine($"New position: {qrCodeSignature.Left}x{qrCodeSignature.Top}");
        Console.WriteLine($"New size: {qrCodeSignature.Width}x{qrCodeSignature.Height}");
    }
    else
    {
        Console.WriteLine($"Failed to update QR Code signature in the document!");
    }
}
else
{
    Console.WriteLine("No QR Code signatures found in the document.");
}
```

## Contoh Lengkap
Berikut contoh lengkap dan fungsional yang menunjukkan cara memperbarui tanda tangan kode QR dalam dokumen:

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;

namespace UpdateQRCodeSignatureExample
{
    class Program
    {
        static void Main(string[] args)
        {
            // Jalur dokumen
            string filePath = "sample_multiple_signatures.docx";
            
            // Tentukan jalur keluaran
            string fileName = Path.GetFileName(filePath);
            string outputDirectory = Path.Combine(Environment.CurrentDirectory, "UpdateQRCode");
            string outputFilePath = Path.Combine(outputDirectory, fileName);
            
            // Pastikan direktori keluaran ada
            Directory.CreateDirectory(outputDirectory);
            
            // Buat salinan dokumen asli
            File.Copy(filePath, outputFilePath, true);
            
            // Inisialisasi instance Tanda Tangan
            using (Signature signature = new Signature(outputFilePath))
            {
                // Konfigurasikan opsi pencarian
                QrCodeSearchOptions options = new QrCodeSearchOptions();
                
                // Cari tanda tangan kode QR
                List<QrCodeSignature> signatures = signature.Search<QrCodeSignature>(options);
                
                // Periksa apakah tanda tangan ditemukan
                if (signatures.Count > 0)
                {
                    // Dapatkan tanda tangan pertama
                    QrCodeSignature qrCodeSignature = signatures[0];
                    
                    // Perbarui posisi dan ukuran
                    qrCodeSignature.Left = 200;
                    qrCodeSignature.Top = 250;
                    qrCodeSignature.Width = 200;
                    qrCodeSignature.Height = 200;
                    
                    // Terapkan pembaruan
                    bool result = signature.Update(qrCodeSignature);
                    
                    // Periksa hasil
                    if (result)
                    {
                        Console.WriteLine($"QR Code signature was successfully updated in document '{fileName}'.");
                        Console.WriteLine($"New position: {qrCodeSignature.Left}x{qrCodeSignature.Top}");
                        Console.WriteLine($"New size: {qrCodeSignature.Width}x{qrCodeSignature.Height}");
                        Console.WriteLine($"Output file path: {outputFilePath}");
                    }
                    else
                    {
                        Console.WriteLine("Failed to update QR Code signature!");
                    }
                }
                else
                {
                    Console.WriteLine("No QR Code signatures found in the document.");
                }
            }
            
            Console.WriteLine("\nPress any key to exit...");
            Console.ReadKey();
        }
    }
}
```

## Kustomisasi Tanda Tangan Kode QR Tingkat Lanjut
GroupDocs.Signature menyediakan opsi tambahan untuk menyesuaikan tanda tangan kode QR di luar posisi dan ukuran dasar:

### Memperbarui Data yang Dikodekan
Anda dapat memperbarui data aktual yang dikodekan dalam kode QR:

```csharp
// Perbarui data yang dikodekan
qrCodeSignature.Text = "https://www.updated-website.com";
```

### Menyesuaikan Properti Penampilan
Sesuaikan aspek visual kode QR:

```csharp
// Tetapkan warna latar depan (warna kode QR)
qrCodeSignature.ForeColor = System.Drawing.Color.Blue;

// Atur warna latar belakang
qrCodeSignature.BackgroundColor = System.Drawing.Color.LightYellow;

// Sesuaikan transparansi
qrCodeSignature.Opacity = 0.8;
```

### Menambahkan Batas
Tingkatkan kode QR dengan batas khusus:

```csharp
qrCodeSignature.Border.Color = System.Drawing.Color.Red;
qrCodeSignature.Border.DashStyle = System.Drawing.Drawing2D.DashStyle.Dash;
qrCodeSignature.Border.Weight = 2;
qrCodeSignature.Border.Visible = true;
```

### Memutar Kode QR
Putar tanda tangan kode QR ke sudut tertentu:

```csharp
qrCodeSignature.Angle = 30; // Putar 30 derajat
```

## Bekerja dengan Format Dokumen yang Berbeda
GroupDocs.Signature mendukung pembaruan tanda tangan kode QR dalam berbagai format dokumen:

- Dokumen PDF
- Dokumen Microsoft Word (DOC, DOCX)
- Lembar kerja Microsoft Excel (XLS, XLSX)
- Presentasi Microsoft PowerPoint (PPT, PPTX)
- Format OpenDocument
- Format gambar

Kode yang sama dapat digunakan di seluruh format ini dengan penyesuaian minimal.

## Kesimpulan
GroupDocs.Signature untuk .NET menyediakan solusi yang andal dan fleksibel untuk memperbarui tanda tangan kode QR dalam dokumen. Dengan mengikuti langkah-langkah yang diuraikan dalam tutorial ini, pengembang dapat secara efisien mengimplementasikan fungsionalitas pembaruan tanda tangan kode QR di aplikasi .NET mereka, yang meningkatkan kemampuan manajemen dokumen dan autentikasi.

Dengan rangkaian fitur yang komprehensif dan API yang intuitif, GroupDocs.Signature memungkinkan pengembang untuk membangun solusi penandatanganan dokumen canggih yang memenuhi persyaratan aplikasi bisnis modern sekaligus memastikan integritas dan aksesibilitas dokumen.

## Pertanyaan yang Sering Diajukan
### Bisakah saya memperbarui beberapa tanda tangan kode QR dalam satu dokumen?
Ya, GroupDocs.Signature memungkinkan Anda memperbarui beberapa tanda tangan kode QR dalam dokumen yang sama. Setelah mencari tanda tangan, Anda dapat menelusuri daftar yang dihasilkan dan memperbarui setiap tanda tangan kode QR satu per satu.

### Apakah GroupDocs.Signature mendukung berbagai jenis kode QR?
Ya, GroupDocs.Signature mendukung berbagai jenis kode QR, termasuk QR standar, QR Mikro, dan lainnya. Anda dapat menentukan jenis kode QR menggunakan `EncodeType` milik.

### Apakah ada versi uji coba yang tersedia untuk GroupDocs.Signature untuk .NET?
Ya, Anda dapat mengunduh versi uji coba gratis dari [Situs web GroupDocs](https://releases.groupdocs.com/signature/net/) untuk mengevaluasi fitur perpustakaan sebelum melakukan pembelian.

### Bisakah saya mengubah tingkat koreksi kesalahan kode QR secara terprogram?
Ya, Anda dapat mengubah tingkat koreksi kesalahan saat menambahkan kode QR baru, tetapi memperbarui properti ini untuk kode QR yang ada mungkin tidak didukung di semua format dokumen.

### Di mana saya dapat menemukan dukungan tambahan untuk GroupDocs.Signature untuk .NET?
Anda dapat menemukan dukungan komprehensif melalui sumber daya berikut:
- [Dokumentasi API](https://docs.groupdocs.com/signature/net/)
- [Referensi API](https://reference.groupdocs.com/signature/net/)
- [Contoh GitHub](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
- [Forum Dukungan](https://forum.groupdocs.com/c/signature/13)
- [Blog](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)