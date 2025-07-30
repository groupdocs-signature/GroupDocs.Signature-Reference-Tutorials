---
"description": "Pelajari cara menandatangani dan menyematkan metadata dalam gambar menggunakan GroupDocs.Signature untuk .NET. Tambahkan informasi penulis, stempel waktu, dan data khusus untuk meningkatkan keaslian dan keterlacakan gambar."
"linktitle": "Gambar Tanda dengan Metadata"
"second_title": "GroupDocs.Signature .NET API"
"title": "Menandatangani Gambar dengan Metadata di C# .NET"
"url": "/id/net/document-signing/sign-image-with-metadata/"
"weight": 10
---

## Perkenalan

Penandatanganan gambar digital dengan metadata semakin penting untuk memastikan keaslian, kepemilikan, dan keterlacakan. GroupDocs.Signature untuk .NET menyediakan solusi yang canggih namun mudah digunakan untuk menambahkan tanda tangan metadata ke berbagai format gambar. Tutorial ini memandu Anda melalui seluruh proses penandatanganan gambar dengan metadata menggunakan C#.

Tanda tangan metadata memungkinkan Anda menyematkan informasi penting langsung ke dalam berkas gambar, seperti informasi pembuat, stempel waktu pembuatan, pengenal unik, dan lainnya. Informasi ini menjadi bagian dari berkas gambar itu sendiri, menyediakan metode yang andal untuk melacak dan memverifikasi keaslian gambar.

## Prasyarat

Sebelum melanjutkan tutorial ini, pastikan Anda memiliki hal berikut:

1. [GroupDocs.Signature untuk .NET](https://releases.groupdocs.com/signature/net/) - Unduh dan instal perpustakaan
2. Lingkungan Pengembangan - Visual Studio atau IDE apa pun yang kompatibel dengan dukungan .NET
3. Berkas Gambar - Contoh berkas gambar dalam format yang didukung (PNG, JPG, TIFF, dll.)
4. Pengetahuan Dasar Pemrograman C# - Keakraban dengan konsep pemrograman C#

## Mengimpor Ruang Nama

Mulailah dengan mengimpor namespace yang diperlukan untuk mengakses fungsionalitas GroupDocs.Signature:

```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

## Langkah 1: Siapkan Jalur File

Tentukan jalur untuk gambar sumber Anda dan tempat penyimpanan output yang ditandatangani:

```csharp
// Tentukan jalur ke file gambar sumber Anda
string filePath = "sample.png";

// Tentukan direktori keluaran dan nama file untuk gambar yang ditandatangani
string outputDirectory = "Your Document Directory";
string outputFilePath = Path.Combine(outputDirectory, "SignImageWithMetadata", "SignedWithMetadata.png");

// Pastikan direktori keluaran ada
Directory.CreateDirectory(Path.GetDirectoryName(outputFilePath));
```

## Langkah 2: Inisialisasi Objek Tanda Tangan

Buat contoh kelas Signature dengan file gambar sumber Anda:

```csharp
using (Signature signature = new Signature(filePath))
{
    // Sisa kode akan berada di sini
}
```

## Langkah 3: Membuat dan Mengonfigurasi Tanda Tangan Metadata

Selanjutnya, tentukan metadata yang ingin Anda sematkan pada gambar. GroupDocs.Signature mendukung berbagai tipe data metadata:

```csharp
// Inisialisasi ID metadata (khusus untuk format gambar)
ushort imgsMetadataId = 41996;

// Buat objek opsi metadata
MetadataSignOptions options = new MetadataSignOptions();

// Tambahkan berbagai jenis tanda tangan metadata
options
    .Add(new ImageMetadataSignature(imgsMetadataId++, "Mr.Sherlock Holmes"))  // Nilai string
    .Add(new ImageMetadataSignature(imgsMetadataId++, DateTime.Now))          // Nilai Tanggal Waktu
    .Add(new ImageMetadataSignature(imgsMetadataId++, 123456))                // Nilai bilangan bulat
    .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456D))              // Nilai ganda
    .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456M))              // Nilai desimal
    .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456F));             // Nilai mengambang
```

## Langkah 4: Menandatangani Gambar dengan Metadata

Terapkan tanda tangan metadata ke gambar dan simpan hasilnya:

```csharp
// Tanda tangani dokumen dan simpan ke jalur file keluaran
SignResult result = signature.Sign(outputFilePath, options);

// Tampilkan pesan sukses
Console.WriteLine($"\nSource image signed successfully with {result.Succeeded.Count} metadata signature(s).");
Console.WriteLine($"Signed image saved at: {outputFilePath}");
```

## Contoh Lengkap

Berikut contoh kode lengkap yang menyatukan semua langkah:

```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;

namespace SignImageWithMetadataExample
{
    class Program
    {
        static void Main(string[] args)
        {
            // Tentukan jalur file
            string filePath = "sample.png";            
            string outputFilePath = Path.Combine("Your Document Directory", "SignImageWithMetadata", "SignedWithMetadata.png");
            
            // Pastikan direktori keluaran ada
            Directory.CreateDirectory(Path.GetDirectoryName(outputFilePath));

            // Tanda tangani gambar dengan metadata
            using (Signature signature = new Signature(filePath))
            {
                // Inisialisasi ID metadata (khusus untuk format gambar)
                ushort imgsMetadataId = 41996;
                
                // Buat opsi metadata
                MetadataSignOptions options = new MetadataSignOptions();
                
                // Tambahkan berbagai jenis tanda tangan metadata
                options
                    .Add(new ImageMetadataSignature(imgsMetadataId++, "Mr.Sherlock Holmes")) // Nilai string
                    .Add(new ImageMetadataSignature(imgsMetadataId++, DateTime.Now))          // Nilai Tanggal Waktu
                    .Add(new ImageMetadataSignature(imgsMetadataId++, 123456))                // Nilai bilangan bulat
                    .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456D))              // Nilai ganda
                    .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456M))              // Nilai desimal
                    .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456F));             // Nilai mengambang
                
                // Tanda tangani dokumen dan simpan ke file
                SignResult result = signature.Sign(outputFilePath, options);
                
                // Menampilkan hasil
                Console.WriteLine($"\nSource image signed successfully with {result.Succeeded.Count} signature(s).");
                Console.WriteLine($"File saved at {outputFilePath}.");
            }
        }
    }
}
```

## Teknik Penandatanganan Metadata Lanjutan

### Bekerja dengan Metadata Kustom

Anda juga dapat membuat bidang metadata khusus dengan ID tertentu:

```csharp
// Buat metadata khusus dengan ID tertentu
options.Add(new ImageMetadataSignature(42000, "CustomValue"));
```

### Memverifikasi Tanda Tangan Metadata

Setelah menandatangani, Anda mungkin ingin memverifikasi tanda tangan metadata:

```csharp
// Buat opsi verifikasi
MetadataSearchOptions searchOptions = new MetadataSearchOptions();

// Mencari tanda tangan metadata
SearchResult result = signature.Search(searchOptions);

// Menampilkan tanda tangan yang ditemukan
Console.WriteLine($"Found {result.Signatures.Count} metadata signatures:");
foreach(var metadataSignature in result.Signatures)
{
    Console.WriteLine($"- {metadataSignature.Name}: {metadataSignature.Value}");
}
```

## Kesimpulan

Dalam tutorial ini, Anda telah mempelajari cara menandatangani gambar dengan metadata menggunakan GroupDocs.Signature untuk .NET. Penyematan metadata ke dalam gambar merupakan cara yang sangat baik untuk meningkatkan keaslian gambar, menambahkan informasi penting, dan meningkatkan alur kerja manajemen dokumen. Prosesnya sederhana namun canggih, memungkinkan kustomisasi berdasarkan kebutuhan spesifik Anda.

Metadata yang tertanam dalam berkas gambar dapat digunakan untuk berbagai tujuan seperti perlindungan hak cipta, pelacakan asal gambar, penambahan informasi deskriptif, dan penetapan rantai penyimpanan digital. Dengan menerapkan tanda tangan metadata, Anda dapat memastikan integritas dan keaslian gambar Anda tetap terjaga sepanjang siklus hidupnya.

## Pertanyaan yang Sering Diajukan

### Bisakah saya menambahkan metadata ke gambar bertanda tangan yang sudah ada?

Ya, Anda dapat menambahkan metadata tambahan ke gambar yang sudah berisi tanda tangan metadata. Metadata yang ada akan dipertahankan, dan metadata baru akan ditambahkan sesuai kebutuhan.

### Format gambar apa yang didukung untuk penandatanganan metadata?

GroupDocs.Signature untuk .NET mendukung penandatanganan metadata untuk berbagai format gambar, termasuk PNG, JPEG, TIFF, BMP, GIF, dan lainnya. Untuk daftar lengkap, lihat [dokumentasi resmi](https://docs.groupdocs.com/signature/net/).

### Apakah mungkin untuk mengenkripsi metadata dalam gambar?

Ya, GroupDocs.Signature menyediakan opsi untuk mengenkripsi metadata demi keamanan yang lebih baik. Anda dapat menggunakan opsi enkripsi yang disediakan oleh pustaka untuk melindungi informasi metadata sensitif.

### Bisakah saya memvalidasi keaslian gambar yang ditandatangani secara terprogram?

Tentu saja. Anda dapat menggunakan metode verifikasi di GroupDocs.Signature untuk memvalidasi tanda tangan metadata dan mengonfirmasi keaslian gambar yang ditandatangani.

### Apakah ada batasan ukuran file saat menandatangani gambar dengan metadata?

Tidak ada batasan ukuran berkas khusus yang diberlakukan oleh pustaka itu sendiri, tetapi berkas yang sangat besar mungkin memerlukan waktu pemrosesan dan memori yang lebih besar. Disarankan untuk mempertimbangkan sumber daya sistem saat bekerja dengan gambar yang sangat besar.

### Bagaimana saya bisa mendapatkan lisensi sementara untuk tujuan pengujian?

Anda bisa mendapatkan [lisensi sementara](https://purchase.groupdocs.com/temporary-license/) untuk menguji GroupDocs.Signature sebelum melakukan pembelian.

### Di mana saya dapat menemukan lebih banyak sumber daya dan dukungan?

- [Referensi API](https://reference.groupdocs.com/signature/net/)
- [Unduhan](https://releases.groupdocs.com/signature/net/)
- [Contoh](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
- [Dokumentasi](https://docs.groupdocs.com/signature/net/)
- [Halaman Produk](https://products.groupdocs.com/signature/net/)
- [Blog](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
- [Forum Dukungan](https://forum.groupdocs.com/c/signature/13)