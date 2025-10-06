---
"description": "Lindungi dan tingkatkan spreadsheet Excel dengan menyematkan tanda tangan metadata menggunakan GroupDocs.Signature untuk .NET. Tambahkan informasi penulis, stempel waktu, dan data khusus untuk meningkatkan ketertelusuran dan keaslian dokumen."
"linktitle": "Tanda Tangani Spreadsheet dengan Metadata"
"second_title": "GroupDocs.Signature .NET API"
"title": "Menambahkan Tanda Tangan Metadata ke Spreadsheet Excel di C# .NET"
"url": "/id/net/document-signing/sign-spreadsheet-with-metadata/"
"weight": 13
type: docs
---
## Perkenalan

Lembar kerja Excel sering kali berisi data bisnis penting, informasi keuangan, dan perhitungan penting. Memastikan keaslian, melacak asal-usul, dan melindungi integritasnya sangat penting di banyak lingkungan profesional. Salah satu pendekatan efektif untuk meningkatkan keamanan dan ketertelusuran lembar kerja adalah dengan menyematkan tanda tangan metadata.

Tutorial komprehensif ini akan memandu Anda melalui proses penandatanganan spreadsheet Excel dengan metadata menggunakan GroupDocs.Signature untuk .NET. Dengan menambahkan tanda tangan metadata, Anda dapat menyematkan informasi penting seperti detail penulis, stempel waktu pembuatan, pengidentifikasi dokumen, dan properti kustom lainnya langsung ke dalam struktur berkas spreadsheet.

## Prasyarat

Sebelum melanjutkan tutorial ini, pastikan Anda memiliki hal berikut:

1. [GroupDocs.Signature untuk .NET](https://releases.groupdocs.com/signature/net/) - Unduh dan instal perpustakaan
2. Lingkungan Pengembangan - Visual Studio atau IDE lain yang kompatibel dengan .NET
3. Lembar Kerja Excel - Contoh berkas lembar kerja (XLSX, XLS, dll.)
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

Tentukan jalur untuk spreadsheet sumber Anda dan tempat penyimpanan output yang ditandatangani:

```csharp
// Tentukan jalur ke file Excel Anda
string filePath = "sample.xlsx";

// Tentukan direktori keluaran dan nama file untuk spreadsheet yang ditandatangani
string outputDirectory = "Your Document Directory";
string outputFilePath = Path.Combine(outputDirectory, "SignSpreadsheetWithMetadata", "SignedWithMetadata.xlsx");

// Pastikan direktori keluaran ada
Directory.CreateDirectory(Path.GetDirectoryName(outputFilePath));
```

## Langkah 2: Inisialisasi Objek Tanda Tangan

Buat contoh kelas Signature dengan file spreadsheet sumber Anda:

```csharp
using (Signature signature = new Signature(filePath))
{
    // Sisa kode akan berada di sini
}
```

## Langkah 3: Membuat dan Mengonfigurasi Tanda Tangan Metadata

Berikutnya, tentukan opsi metadata dan buat serangkaian tanda tangan metadata spreadsheet:

```csharp
// Buat objek opsi metadata
MetadataSignOptions options = new MetadataSignOptions();

// Buat serangkaian tanda tangan metadata spreadsheet dengan tipe data berbeda
SpreadsheetMetadataSignature[] signatures = new SpreadsheetMetadataSignature[]
{
    new SpreadsheetMetadataSignature("Author", "Mr.Sherlock Holmes"), // Nilai string
    new SpreadsheetMetadataSignature("CreatedOn", DateTime.Now),      // Nilai DateTime
    new SpreadsheetMetadataSignature("DocumentId", 123456),           // Nilai bilangan bulat
    new SpreadsheetMetadataSignature("SignatureId", 123.456D),        // Nilai ganda
    new SpreadsheetMetadataSignature("Amount", 123.456M),             // Nilai desimal
    new SpreadsheetMetadataSignature("Total", 123.456F)               // Nilai mengambang
};

// Tambahkan koleksi tanda tangan ke opsi
options.Signatures.AddRange(signatures);
```

## Langkah 4: Tandatangani Spreadsheet dengan Metadata

Terapkan tanda tangan metadata ke spreadsheet dan simpan hasilnya:

```csharp
// Tanda tangani dokumen dan simpan ke jalur file keluaran
SignResult result = signature.Sign(outputFilePath, options);

// Tampilkan pesan sukses
Console.WriteLine($"\nSource spreadsheet signed successfully with {result.Succeeded.Count} metadata signature(s).");
Console.WriteLine($"Signed spreadsheet saved at: {outputFilePath}");
```

## Contoh Lengkap

Berikut contoh kode lengkap yang menyatukan semua langkah:

```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;

namespace SignSpreadsheetWithMetadataExample
{
    class Program
    {
        static void Main(string[] args)
        {
            // Tentukan jalur file
            string filePath = "sample.xlsx";
            string outputFilePath = Path.Combine("Your Document Directory", "SignSpreadsheetWithMetadata", "SignedWithMetadata.xlsx");
            
            // Pastikan direktori keluaran ada
            Directory.CreateDirectory(Path.GetDirectoryName(outputFilePath));

            // Tandatangani spreadsheet dengan metadata
            using (Signature signature = new Signature(filePath))
            {
                // Buat objek opsi metadata
                MetadataSignOptions options = new MetadataSignOptions();
                
                // Buat serangkaian tanda tangan metadata spreadsheet dengan tipe data berbeda
                SpreadsheetMetadataSignature[] signatures = new SpreadsheetMetadataSignature[]
                {
                    new SpreadsheetMetadataSignature("Author", "Mr.Sherlock Holmes"), // Nilai string
                    new SpreadsheetMetadataSignature("CreatedOn", DateTime.Now),      // Nilai DateTime
                    new SpreadsheetMetadataSignature("DocumentId", 123456),           // Nilai bilangan bulat
                    new SpreadsheetMetadataSignature("SignatureId", 123.456D),        // Nilai ganda
                    new SpreadsheetMetadataSignature("Amount", 123.456M),             // Nilai desimal
                    new SpreadsheetMetadataSignature("Total", 123.456F)               // Nilai mengambang
                };
                
                // Tambahkan koleksi tanda tangan ke opsi
                options.Signatures.AddRange(signatures);
                
                // Tanda tangani dokumen dan simpan ke file
                SignResult result = signature.Sign(outputFilePath, options);
                
                // Menampilkan hasil
                Console.WriteLine($"\nSource spreadsheet signed successfully with {result.Succeeded.Count} signature(s).");
                Console.WriteLine($"File saved at {outputFilePath}.");
            }
        }
    }
}
```

## Teknik Metadata Spreadsheet Lanjutan

### Bekerja dengan Properti Spreadsheet Kustom dan Bawaan

Spreadsheet Excel memiliki properti bawaan dan kustom yang dapat diakses melalui dialog properti file. GroupDocs.Signature memungkinkan Anda bekerja dengan keduanya:

```csharp
// Tambahkan properti bawaan
signatures = new SpreadsheetMetadataSignature[]
{
    new SpreadsheetMetadataSignature("Company", "Sherlock Holmes Consulting"),
    new SpreadsheetMetadataSignature("Category", "Financial"),
    new SpreadsheetMetadataSignature("Keywords", "budget,forecast,analysis"),
    new SpreadsheetMetadataSignature("Comments", "This spreadsheet contains confidential information"),
    new SpreadsheetMetadataSignature("Manager", "John Watson")
};
options.Signatures.AddRange(signatures);

// Tambahkan properti kustom
options.Signatures.Add(new SpreadsheetMetadataSignature("Department", "Finance"));
options.Signatures.Add(new SpreadsheetMetadataSignature("SecurityLevel", "Confidential"));
```

### Mencari Metadata di Spreadsheet yang Ditandatangani

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

### Memperbarui Metadata yang Ada

Anda dapat memperbarui metadata yang ada di spreadsheet dengan menggunakan nama properti yang sama:

```csharp
// Perbarui metadata yang ada
options.Signatures.Add(new SpreadsheetMetadataSignature("Author", "Updated Author Name"));
```

## Kesimpulan

Dalam tutorial komprehensif ini, Anda telah mempelajari cara menandatangani lembar kerja Excel dengan metadata menggunakan GroupDocs.Signature untuk .NET. Penyematan metadata ke dalam berkas lembar kerja meningkatkan ketertelusuran dokumen, memberikan konteks yang berharga, dan membantu memastikan keasliannya.

Tanda tangan metadata dalam spreadsheet sangat berguna dalam lingkungan bisnis yang mengutamakan asal dokumen, kepengarangan, dan pelacakan versi. Metadata yang disematkan dapat mencakup informasi tentang penulis, waktu pembuatan, pengidentifikasi dokumen, dan properti khusus yang relevan dengan kebutuhan organisasi Anda.

Dengan menerapkan tanda tangan metadata dengan GroupDocs.Signature, Anda dapat memastikan lembar kerja Excel Anda mempertahankan integritasnya dan menyediakan informasi yang dapat diverifikasi sepanjang siklus hidupnya.

## Pertanyaan yang Sering Diajukan

### Dapatkah saya menambahkan metadata ke spreadsheet yang beberapa propertinya sudah ditentukan?

Ya, Anda dapat menambahkan metadata baru atau memperbarui metadata yang sudah ada di spreadsheet. GroupDocs.Signature akan menangani integrasi tersebut, baik dengan menambahkan properti baru maupun memperbarui properti yang sudah ada dengan nama yang sama.

### Format spreadsheet mana yang didukung untuk penandatanganan metadata?

GroupDocs.Signature untuk .NET mendukung penandatanganan metadata untuk berbagai format spreadsheet, termasuk XLSX, XLS, XLSM, ODS, dan lainnya. Untuk daftar lengkap, lihat [dokumentasi resmi](https://docs.groupdocs.com/signature/net/).

### Apakah tanda tangan metadata dalam spreadsheet terlihat oleh pengguna?

Tanda tangan metadata tidak terlihat dalam konten spreadsheet itu sendiri. Namun, tanda tangan tersebut dapat dilihat melalui panel properti dokumen di Excel atau aplikasi lain yang kompatibel.

### Dapatkah saya memvalidasi secara terprogram apakah suatu spreadsheet telah dirusak setelah menambahkan metadata?

Ya, GroupDocs.Signature menyediakan kemampuan verifikasi yang dapat membantu mendeteksi apakah suatu dokumen telah dimodifikasi setelah penandatanganan, termasuk perubahan pada metadata.

### Apakah penambahan metadata memengaruhi fungsionalitas spreadsheet?

Menambahkan metadata memiliki dampak minimal pada ukuran berkas dan tidak memengaruhi fungsionalitas spreadsheet. Ini adalah cara yang ringan untuk menyempurnakan properti dokumen tanpa memengaruhi perhitungan, rumus, atau fitur Excel lainnya.

### Di mana saya dapat menemukan lebih banyak sumber daya dan dukungan?

- [Referensi API](https://reference.groupdocs.com/signature/net/)
- [Unduhan](https://releases.groupdocs.com/signature/net/)
- [Contoh](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
- [Dokumentasi](https://docs.groupdocs.com/signature/net/)
- [Halaman Produk](https://products.groupdocs.com/signature/net/)
- [Blog](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
- [Forum Dukungan](https://forum.groupdocs.com/c/signature/13)
- [Lisensi Sementara](https://purchase.groupdocs.com/temporary-license/)