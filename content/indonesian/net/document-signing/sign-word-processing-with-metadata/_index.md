---
"description": "Tambahkan tanda tangan metadata ke dokumen Word menggunakan GroupDocs.Signature untuk .NET. Sematkan detail penulis, stempel waktu, dan properti khusus untuk meningkatkan keamanan dan keterlacakan dokumen."
"linktitle": "Pengolahan Kata Isyarat dengan Metadata"
"second_title": "GroupDocs.Signature .NET API"
"title": "Meningkatkan Dokumen Word dengan Tanda Tangan Metadata di C# .NET"
"url": "/id/net/document-signing/sign-word-processing-with-metadata/"
"weight": 14
---

## Perkenalan

Dokumen pengolah kata merupakan salah satu jenis berkas yang paling umum digunakan dalam bisnis, pendidikan, dan komunikasi pribadi. Memastikan keaslian, melacak asal usul, dan menjaga integritas dokumen-dokumen ini sangat penting dalam banyak lingkungan profesional. Salah satu pendekatan efektif untuk meningkatkan keamanan dan ketertelusuran dokumen adalah dengan menyematkan tanda tangan metadata.

Tutorial komprehensif ini akan memandu Anda melalui proses penandatanganan dokumen pengolah kata dengan metadata menggunakan GroupDocs.Signature untuk .NET. Dengan menambahkan tanda tangan metadata, Anda dapat menanamkan informasi penting seperti detail penulis, stempel waktu pembuatan, pengidentifikasi dokumen, dan properti kustom lainnya langsung ke dalam struktur berkas dokumen.

## Prasyarat

Sebelum melanjutkan tutorial ini, pastikan Anda memiliki hal berikut:

1. [GroupDocs.Signature untuk .NET](https://releases.groupdocs.com/signature/net/) - Unduh dan instal perpustakaan
2. Lingkungan Pengembangan - Visual Studio atau IDE lain yang kompatibel dengan .NET
3. Dokumen Word - Contoh berkas dokumen (DOCX, DOC, dll.)
4. Pengetahuan Dasar C# - Keakraban dengan bahasa pemrograman C#

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

Tentukan jalur untuk dokumen Word sumber Anda dan tempat penyimpanan hasil yang ditandatangani:

```csharp
// Tentukan jalur ke dokumen Word Anda
string filePath = "sample.docx";

// Tentukan direktori keluaran dan nama file untuk dokumen yang ditandatangani
string outputDirectory = "Your Document Directory";
string outputFilePath = Path.Combine(outputDirectory, "SignWordProcessingWithMetadata", "SignedWithMetadata.docx");

// Pastikan direktori keluaran ada
Directory.CreateDirectory(Path.GetDirectoryName(outputFilePath));
```

## Langkah 2: Inisialisasi Objek Tanda Tangan

Buat contoh kelas Tanda Tangan dengan dokumen Word sumber Anda:

```csharp
using (Signature signature = new Signature(filePath))
{
    // Sisa kode akan berada di sini
}
```

## Langkah 3: Membuat dan Mengonfigurasi Tanda Tangan Metadata

Selanjutnya, tentukan opsi metadata dan tambahkan berbagai jenis tanda tangan metadata:

```csharp
// Buat objek opsi metadata
MetadataSignOptions options = new MetadataSignOptions();

// Tambahkan berbagai jenis metadata menggunakan antarmuka yang lancar
options
    .Add(new WordProcessingMetadataSignature("Author", "Mr.Sherlock Holmes")) // Nilai string
    .Add(new WordProcessingMetadataSignature("CreatedOn", DateTime.Now))      // Nilai DateTime
    .Add(new WordProcessingMetadataSignature("DocumentId", 123456))           // Nilai bilangan bulat
    .Add(new WordProcessingMetadataSignature("SignatureId", 123.456D))        // Nilai ganda
    .Add(new WordProcessingMetadataSignature("Amount", 123.456M))             // Nilai desimal
    .Add(new WordProcessingMetadataSignature("Total", 123.456F));             // Nilai mengambang
```

## Langkah 4: Tandatangani Dokumen dengan Metadata

Terapkan tanda tangan metadata ke dokumen Word dan simpan hasilnya:

```csharp
// Tanda tangani dokumen dan simpan ke jalur file keluaran
SignResult result = signature.Sign(outputFilePath, options);

// Tampilkan pesan sukses
Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} metadata signature(s).");
Console.WriteLine($"Signed document saved at: {outputFilePath}");
```

## Contoh Lengkap

Berikut contoh kode lengkap yang menyatukan semua langkah:

```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;

namespace SignWordProcessingWithMetadataExample
{
    class Program
    {
        static void Main(string[] args)
        {
            // Tentukan jalur file
            string filePath = "sample.docx";
            string outputFilePath = Path.Combine("Your Document Directory", "SignWordProcessingWithMetadata", "SignedWithMetadata.docx");
            
            // Pastikan direktori keluaran ada
            Directory.CreateDirectory(Path.GetDirectoryName(outputFilePath));

            // Tandatangani dokumen Word dengan metadata
            using (Signature signature = new Signature(filePath))
            {
                // Buat objek opsi metadata
                MetadataSignOptions options = new MetadataSignOptions();
                
                // Tambahkan berbagai jenis tanda tangan metadata
                options
                    .Add(new WordProcessingMetadataSignature("Author", "Mr.Sherlock Holmes")) // Nilai string
                    .Add(new WordProcessingMetadataSignature("CreatedOn", DateTime.Now))      // Nilai DateTime
                    .Add(new WordProcessingMetadataSignature("DocumentId", 123456))           // Nilai bilangan bulat
                    .Add(new WordProcessingMetadataSignature("SignatureId", 123.456D))        // Nilai ganda
                    .Add(new WordProcessingMetadataSignature("Amount", 123.456M))             // Nilai desimal
                    .Add(new WordProcessingMetadataSignature("Total", 123.456F));             // Nilai mengambang
                
                // Tanda tangani dokumen dan simpan ke file
                SignResult result = signature.Sign(outputFilePath, options);
                
                // Menampilkan hasil
                Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).");
                Console.WriteLine($"File saved at {outputFilePath}.");
            }
        }
    }
}
```

## Teknik Metadata Dokumen Word Tingkat Lanjut

### Bekerja dengan Properti Dokumen Kustom dan Bawaan

Dokumen Word memiliki properti bawaan dan kustom yang dapat diakses melalui panel properti dokumen. GroupDocs.Signature memungkinkan Anda bekerja dengan keduanya:

```csharp
// Tambahkan properti bawaan
options
    .Add(new WordProcessingMetadataSignature("Company", "Sherlock Holmes Consulting"))
    .Add(new WordProcessingMetadataSignature("Category", "Legal Document"))
    .Add(new WordProcessingMetadataSignature("Keywords", "contract,agreement,legal"))
    .Add(new WordProcessingMetadataSignature("Comments", "This document is confidential"))
    .Add(new WordProcessingMetadataSignature("Manager", "John Watson"));

// Tambahkan properti kustom
options.Add(new WordProcessingMetadataSignature("Department", "Legal"));
options.Add(new WordProcessingMetadataSignature("SecurityLevel", "Confidential"));
```

### Mencari Metadata dalam Dokumen Word yang Ditandatangani

Setelah menandatangani, Anda mungkin ingin memverifikasi atau mengekstrak metadata:

```csharp
// Buat opsi pencarian untuk metadata
MetadataSearchOptions searchOptions = new MetadataSearchOptions();

// Mencari tanda tangan metadata
SearchResult searchResult = signature.Search(searchOptions);

// Menampilkan tanda tangan yang ditemukan
Console.WriteLine($"Found {searchResult.Signatures.Count} metadata signatures:");
foreach (var foundSignature in searchResult.Signatures)
{
    MetadataSignature metadataSignature = foundSignature as MetadataSignature;
    if (metadataSignature != null)
    {
        Console.WriteLine($"- {metadataSignature.Name}: {metadataSignature.Value} ({metadataSignature.Value.GetType().Name})");
    }
}
```

### Bekerja dengan Variabel Dokumen

Dokumen Word juga mendukung variabel dokumen, yang merupakan bentuk lain dari metadata:

```csharp
// Tambahkan variabel dokumen
options.Add(new WordProcessingMetadataSignature("DocVariable1", "Custom Value 1", true));
options.Add(new WordProcessingMetadataSignature("DocVariable2", DateTime.Now, true));
```

## Kesimpulan

Dalam tutorial komprehensif ini, Anda telah mempelajari cara menandatangani dokumen pemrosesan Word dengan metadata menggunakan GroupDocs.Signature untuk .NET. Penyematan metadata ke dalam dokumen Word meningkatkan ketertelusuran dokumen, memberikan konteks yang berharga, dan membantu memastikan keasliannya.

Tanda tangan metadata dalam dokumen Word sangat berguna dalam lingkungan bisnis dan hukum yang mengutamakan asal dokumen, kepengarangan, dan pelacakan versi. Metadata yang disematkan dapat mencakup informasi tentang penulis, waktu pembuatan, pengidentifikasi dokumen, dan properti kustom yang relevan dengan kebutuhan organisasi Anda.

Dengan menerapkan tanda tangan metadata dengan GroupDocs.Signature, Anda dapat memastikan dokumen Word Anda mempertahankan integritasnya dan memberikan informasi yang dapat diverifikasi sepanjang siklus hidupnya.

## Pertanyaan yang Sering Diajukan

### Dapatkah saya menambahkan metadata ke dokumen Word yang beberapa propertinya sudah ditentukan?

Ya, Anda dapat menambahkan metadata baru atau memperbarui metadata yang sudah ada di dokumen Word. GroupDocs.Signature akan menangani integrasi tersebut, baik dengan menambahkan properti baru maupun memperbarui properti yang sudah ada dengan nama yang sama.

### Format pengolah kata apa yang didukung untuk penandatanganan metadata?

GroupDocs.Signature untuk .NET mendukung penandatanganan metadata untuk berbagai format pengolah kata, termasuk DOCX, DOC, RTF, ODT, dan lainnya. Untuk daftar lengkap, lihat [dokumentasi](https://docs.groupdocs.com/signature/net/).

### Apakah tanda tangan metadata dalam dokumen Word terlihat oleh pembaca?

Tanda tangan metadata tidak terlihat dalam konten dokumen itu sendiri. Namun, tanda tangan tersebut dapat dilihat melalui panel properti dokumen di Microsoft Word atau aplikasi lain yang kompatibel.

### Dapatkah saya memvalidasi secara terprogram apakah dokumen Word telah dirusak setelah menambahkan metadata?

Ya, GroupDocs.Signature menyediakan kemampuan verifikasi yang dapat membantu mendeteksi apakah suatu dokumen telah dimodifikasi setelah penandatanganan, termasuk perubahan pada metadata.

### Apakah mungkin untuk menghapus metadata dari dokumen Word?

Ya, GroupDocs.Signature menyediakan opsi untuk menghapus tanda tangan metadata dari dokumen jika diperlukan. Ini berguna untuk membersihkan informasi sensitif sebelum membagikan dokumen secara eksternal.

### Di mana saya dapat menemukan lebih banyak sumber daya dan dukungan?

- [Referensi API](https://reference.groupdocs.com/signature/net/)
- [Unduhan](https://releases.groupdocs.com/signature/net/)
- [Contoh](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
- [Dokumentasi](https://docs.groupdocs.com/signature/net/)
- [Halaman Produk](https://products.groupdocs.com/signature/net/)
- [Blog](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
- [Forum Dukungan](https://forum.groupdocs.com/c/signature/13)
- [Lisensi Sementara](https://purchase.groupdocs.com/temporary-license/)