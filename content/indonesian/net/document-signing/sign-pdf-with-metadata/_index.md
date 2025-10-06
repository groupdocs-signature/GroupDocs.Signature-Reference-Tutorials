---
"description": "Integrasikan tanda tangan metadata ke dalam dokumen PDF menggunakan GroupDocs.Signature untuk .NET. Pelajari cara menyematkan informasi penulis, stempel waktu, dan data khusus untuk meningkatkan keaslian dan keterlacakan PDF."
"linktitle": "Tandatangani PDF dengan Metadata"
"second_title": "GroupDocs.Signature .NET API"
"title": "Menambahkan Tanda Tangan Metadata ke Dokumen PDF di C# .NET"
"url": "/id/net/document-signing/sign-pdf-with-metadata/"
"weight": 11
type: docs
---
## Perkenalan

Dokumen PDF (Portable Document Format) banyak digunakan di berbagai industri karena konsistensi dan independensi platformnya. Memastikan keaslian dan keterlacakan dokumen-dokumen ini sangat penting di banyak lingkungan profesional. Salah satu cara efektif untuk mencapai hal ini adalah dengan menyematkan metadata ke dalam berkas PDF itu sendiri.

Dalam tutorial komprehensif ini, kita akan membahas cara menandatangani dokumen PDF dengan metadata menggunakan GroupDocs.Signature untuk .NET. Tanda tangan metadata memungkinkan Anda untuk menyematkan informasi tambahan di dalam dokumen, seperti detail penulis, stempel waktu pembuatan, pengidentifikasi dokumen, dan nilai khusus, tanpa mengubah tampilan dokumen secara nyata.

## Prasyarat

Sebelum kita mulai, pastikan Anda telah menyiapkan hal-hal berikut:

1. [GroupDocs.Signature untuk .NET](https://releases.groupdocs.com/signature/net/) - Unduh dan instal perpustakaan
2. Lingkungan Pengembangan - Visual Studio atau IDE lain yang kompatibel dengan .NET
3. Dokumen PDF - Contoh file PDF untuk ditandatangani
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

Pertama, tentukan jalur ke dokumen PDF Anda dan tentukan di mana Anda ingin menyimpan keluaran yang ditandatangani:

```csharp
// Tentukan jalur ke dokumen PDF Anda
string filePath = "sample.pdf";

// Tentukan direktori keluaran dan jalur file
string outputDirectory = "Your Document Directory";
string outputFilePath = Path.Combine(outputDirectory, "SignPdfWithMetadata", "SignedWithMetadata.pdf");

// Pastikan direktori keluaran ada
Directory.CreateDirectory(Path.GetDirectoryName(outputFilePath));
```

## Langkah 2: Inisialisasi Objek Tanda Tangan

Buat contoh kelas Signature dengan dokumen PDF sumber Anda:

```csharp
using (Signature signature = new Signature(filePath))
{
    // Kode untuk penandatanganan akan ada di sini
}
```

## Langkah 3: Tentukan Opsi Metadata

Buat dan konfigurasikan opsi metadata, tambahkan berbagai jenis tanda tangan metadata:

```csharp
// Buat objek opsi metadata
MetadataSignOptions options = new MetadataSignOptions();

// Tambahkan berbagai jenis metadata menggunakan antarmuka yang lancar
options
    .Add(new PdfMetadataSignature("Author", "Mr.Sherlock Holmes")) // Nilai string
    .Add(new PdfMetadataSignature("CreatedOn", DateTime.Now))       // Nilai DateTime
    .Add(new PdfMetadataSignature("DocumentId", 123456))            // Nilai bilangan bulat
    .Add(new PdfMetadataSignature("SignatureId", 123.456D))         // Nilai ganda
    .Add(new PdfMetadataSignature("Amount", 123.456M))              // Nilai desimal
    .Add(new PdfMetadataSignature("Total", 123.456F));              // Nilai mengambang
```

## Langkah 4: Tandatangani PDF dengan Metadata

Terapkan tanda tangan metadata ke dokumen PDF dan simpan hasilnya:

```csharp
// Tanda tangani dokumen dan simpan ke jalur keluaran
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

namespace SignPdfWithMetadataExample
{
    class Program
    {
        static void Main(string[] args)
        {
            // Tentukan jalur file
            string filePath = "sample.pdf";
            string outputFilePath = Path.Combine("Your Document Directory", "SignPdfWithMetadata", "SignedWithMetadata.pdf");
            
            // Pastikan direktori keluaran ada
            Directory.CreateDirectory(Path.GetDirectoryName(outputFilePath));

            // Tandatangani PDF dengan metadata
            using (Signature signature = new Signature(filePath))
            {
                // Buat objek opsi metadata
                MetadataSignOptions options = new MetadataSignOptions();
                
                // Tambahkan berbagai jenis tanda tangan metadata
                options
                    .Add(new PdfMetadataSignature("Author", "Mr.Sherlock Holmes")) // Nilai string
                    .Add(new PdfMetadataSignature("CreatedOn", DateTime.Now))       // Nilai DateTime
                    .Add(new PdfMetadataSignature("DocumentId", 123456))            // Nilai bilangan bulat
                    .Add(new PdfMetadataSignature("SignatureId", 123.456D))         // Nilai ganda
                    .Add(new PdfMetadataSignature("Amount", 123.456M))              // Nilai desimal
                    .Add(new PdfMetadataSignature("Total", 123.456F));              // Nilai mengambang
                
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

## Operasi Metadata PDF Lanjutan

### Menambahkan Metadata Kustom dengan Dukungan Namespace

Dokumen PDF mendukung metadata khusus dengan dukungan namespace XML:

```csharp
// Tambahkan metadata khusus dengan namespace
options.Add(new PdfMetadataSignature("CustomProperty", "Custom Value")
{
    NamespaceUri = "http://namespace-anda.com/skema"
});
```

### Mencari Metadata dalam PDF yang Ditandatangani

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

### Bekerja dengan Metadata PDF Standar

Dokumen PDF memiliki bidang metadata standar yang dapat diakses dan dimodifikasi:

```csharp
// Tetapkan bidang metadata PDF standar
options
    .Add(new PdfMetadataSignature("Title", "Important Contract"))
    .Add(new PdfMetadataSignature("Subject", "Legal Agreement"))
    .Add(new PdfMetadataSignature("Keywords", "contract, agreement, legal, binding"))
    .Add(new PdfMetadataSignature("Creator", "Legal Department"))
    .Add(new PdfMetadataSignature("Producer", "GroupDocs.Signature"));
```

## Kesimpulan

Dalam tutorial ini, Anda telah mempelajari cara menandatangani dokumen PDF dengan metadata menggunakan GroupDocs.Signature untuk .NET. Penyematan metadata ke dalam berkas PDF merupakan cara yang sangat baik untuk meningkatkan keaslian dokumen, menambahkan informasi penting, dan meningkatkan alur kerja manajemen dokumen.

Tanda tangan metadata dalam PDF sangat berharga dalam lingkungan bisnis yang sangat membutuhkan ketertelusuran dan verifikasi keaslian dokumen. Metadata yang disematkan dapat mencakup informasi tentang asal dokumen, penulis, waktu pembuatan, versi, dan properti khusus yang relevan dengan alur kerja organisasi Anda.

Dengan menerapkan tanda tangan metadata dengan GroupDocs.Signature, Anda dapat memastikan dokumen PDF Anda mempertahankan integritasnya dan memberikan informasi yang dapat diverifikasi sepanjang siklus hidupnya.

## Pertanyaan yang Sering Diajukan

### Bisakah saya mengubah metadata yang ada dalam dokumen PDF?

Ya, Anda dapat mengubah metadata yang ada dalam dokumen PDF. Saat Anda menerapkan tanda tangan metadata baru dengan nama yang sama dengan yang sudah ada, nilainya akan diperbarui.

### Apakah tanda tangan metadata dalam dokumen PDF terlihat oleh pengguna akhir?

Tanda tangan metadata tidak terlihat dalam konten dokumen itu sendiri. Namun, tanda tangan tersebut dapat dilihat melalui panel properti dokumen di pembaca PDF seperti Adobe Acrobat atau menggunakan alat khusus untuk melihat metadata.

### Dapatkah saya mengenkripsi atau melindungi metadata dalam PDF?

GroupDocs.Signature menyediakan opsi untuk mengamankan dokumen, termasuk enkripsi. Anda dapat menerapkan enkripsi tingkat dokumen untuk melindungi seluruh PDF, termasuk metadatanya.

### Apakah ada batasan berapa banyak metadata yang dapat saya tambahkan ke PDF?

Meskipun spesifikasi PDF tidak menetapkan batasan ketat, menambahkan metadata secara berlebihan dapat meningkatkan ukuran file. Disarankan untuk hanya menyertakan informasi yang relevan dan diperlukan dalam metadata.

### Dapatkah saya memvalidasi secara terprogram apakah PDF telah dirusak setelah menambahkan metadata?

Ya, GroupDocs.Signature menyediakan kemampuan verifikasi yang dapat membantu mendeteksi apakah suatu dokumen telah dimodifikasi setelah penandatanganan, termasuk perubahan pada metadata.

### Di mana saya dapat menemukan lebih banyak sumber daya dan dukungan?

- [Referensi API](https://reference.groupdocs.com/signature/net/)
- [Unduhan](https://releases.groupdocs.com/signature/net/)
- [Contoh](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
- [Dokumentasi](https://docs.groupdocs.com/signature/net/)
- [Halaman Produk](https://products.groupdocs.com/signature/net/)
- [Blog](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
- [Forum Dukungan](https://forum.groupdocs.com/c/signature/13)
- [Lisensi Sementara](https://purchase.groupdocs.com/temporary-license/)