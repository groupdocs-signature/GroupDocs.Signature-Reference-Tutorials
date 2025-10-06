---
"description": "Kuasai pencarian tanda tangan digital dalam dokumen dengan GroupDocs.Signature untuk .NET. Tingkatkan keamanan dan verifikasi dokumen dengan panduan langkah demi langkah kami yang terperinci."
"linktitle": "Cari Tanda Tangan Digital"
"second_title": "GroupDocs.Signature .NET API"
"title": "Mencari Tanda Tangan Digital dalam Dokumen"
"url": "/id/net/signature-searching/search-for-digital-signatures/"
"weight": 11
type: docs
---
## Perkenalan

Dalam lanskap digital saat ini, memastikan keaslian dan integritas dokumen sangat penting bagi bisnis dan organisasi. Tanda tangan digital menyediakan mekanisme yang andal untuk memverifikasi keaslian dokumen dan mendeteksi modifikasi yang tidak sah. GroupDocs.Signature untuk .NET menawarkan solusi komprehensif untuk bekerja dengan tanda tangan digital dalam berbagai format dokumen, yang memungkinkan pengembang untuk mengintegrasikan fungsionalitas tanda tangan dengan lancar ke dalam aplikasi .NET mereka.

Tutorial ini akan memandu Anda melalui proses pencarian tanda tangan digital dalam dokumen menggunakan GroupDocs.Signature untuk .NET, memberikan penjelasan terperinci dan contoh kode praktis.

## Prasyarat

Sebelum menyelami detail implementasi, pastikan Anda memiliki prasyarat berikut:

1. GroupDocs.Signature untuk .NET: Unduh dan instal pustaka dari [Di Sini](https://releases.groupdocs.com/signature/net/).
   
2. Lingkungan Pengembangan: Siapkan lingkungan pengembangan .NET dengan Visual Studio atau IDE pilihan Anda.
   
3. Contoh Dokumen: Siapkan contoh dokumen yang berisi tanda tangan digital untuk tujuan pengujian.

4. Pengetahuan Dasar: Keakraban dengan bahasa pemrograman C# dan dasar-dasar kerangka kerja .NET.

## Mengimpor Ruang Nama

Mulailah dengan mengimpor namespace yang diperlukan untuk mengakses fungsionalitas yang disediakan oleh GroupDocs.Signature untuk .NET:

```csharp
using System;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

Sekarang, mari kita uraikan proses pencarian tanda tangan digital menjadi langkah-langkah yang jelas dan mudah dikelola:

## Langkah 1: Inisialisasi Objek Tanda Tangan

Mulailah dengan membuat contoh `Signature` kelas, meneruskan jalur ke dokumen Anda:

```csharp
string filePath = "sample_multiple_signatures.docx";
using (Signature signature = new Signature(filePath))
{
    // Kode untuk mencari tanda tangan digital akan ditambahkan di sini
}
```

## Langkah 2: Cari Tanda Tangan Digital

Selanjutnya, gunakan `Search` metode dengan `SignatureType.Digital` parameter untuk mencari tanda tangan digital dalam dokumen:

```csharp
// Mencari tanda tangan digital dalam dokumen
List<DigitalSignature> signatures = signature.Search<DigitalSignature>(SignatureType.Digital);
```

## Langkah 3: Proses dan Tampilkan Hasil

Terakhir, proses hasil pencarian dan tampilkan informasi relevan tentang tanda tangan digital yang ditemukan:

```csharp
Console.WriteLine($"\nSource document ['{filePath}'] contains the following digital signatures:");
foreach (var digitalSignature in signatures)
{
    Console.WriteLine($"Digital signature found from {digitalSignature.SignTime} with validation status: {digitalSignature.IsValid}");
    Console.WriteLine($"Certificate: Subject: {digitalSignature.Certificate?.SubjectName}");
    Console.WriteLine($"Certificate: Issuer: {digitalSignature.Certificate?.IssuerName}");
    Console.WriteLine($"Certificate: Serial Number: {digitalSignature.Certificate?.SerialNumber}");
    Console.WriteLine();
}
```

## Contoh Lengkap

Berikut ini contoh lengkap dan praktis yang menunjukkan cara mencari tanda tangan digital dalam sebuah dokumen:

```csharp
using System;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;

namespace SearchDigitalSignatures
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
                // Mencari tanda tangan digital dalam dokumen
                List<DigitalSignature> signatures = signature.Search<DigitalSignature>(SignatureType.Digital);
                
                // Menampilkan hasil pencarian
                Console.WriteLine($"\nSource document ['{filePath}'] contains the following digital signatures:");
                
                if (signatures.Count > 0)
                {
                    foreach (var digitalSignature in signatures)
                    {
                        Console.WriteLine($"Digital signature found from {digitalSignature.SignTime} with validation status: {digitalSignature.IsValid}");
                        Console.WriteLine($"Certificate: Subject: {digitalSignature.Certificate?.SubjectName}");
                        Console.WriteLine($"Certificate: Issuer: {digitalSignature.Certificate?.IssuerName}");
                        Console.WriteLine($"Certificate: Serial Number: {digitalSignature.Certificate?.SerialNumber}");
                        Console.WriteLine();
                    }
                }
                else
                {
                    Console.WriteLine("No digital signatures found in the document.");
                }
            }
        }
    }
}
```

## Opsi Pencarian Lanjutan

Untuk pencarian yang lebih tertarget, Anda dapat menggunakan `DigitalSearchOptions` untuk menyesuaikan kriteria pencarian:

```csharp
// Buat opsi pencarian digital
DigitalSearchOptions options = new DigitalSearchOptions()
{
    // Cari hanya pada halaman tertentu (misalnya, halaman 1 dan 2)
    PageNumber = 1,
    PagesSetup = new PagesSetup() { Pages = new List<int> { 1, 2 } },
    
    // Filter berdasarkan komentar dalam tanda tangan digital
    Comments = "Approved",
    
    // Tetapkan rentang tanggal dan waktu untuk pencarian
    SignDateTimeFrom = new DateTime(2022, 1, 1),
    SignDateTimeTo = DateTime.Now
};

// Pencarian dengan opsi tertentu
List<DigitalSignature> signatures = signature.Search<DigitalSignature>(options);
```

## Bekerja dengan Informasi Sertifikat

Tanda tangan digital berisi informasi sertifikat berharga yang dapat Anda akses dan validasi:

```csharp
foreach (var digitalSignature in signatures)
{
    if (digitalSignature.Certificate != null)
    {
        // Properti sertifikat akses
        Console.WriteLine($"Certificate Valid From: {digitalSignature.Certificate.NotBefore}");
        Console.WriteLine($"Certificate Valid To: {digitalSignature.Certificate.NotAfter}");
        
        // Periksa apakah sertifikat berada dalam rentang tanggal yang valid
        bool isDateValid = DateTime.Now >= digitalSignature.Certificate.NotBefore && 
                          DateTime.Now <= digitalSignature.Certificate.NotAfter;
        
        Console.WriteLine($"Certificate Date Validity: {isDateValid}");
        
        // Detail penerbit sertifikat akses
        Console.WriteLine($"Certificate Issuer: {digitalSignature.Certificate.IssuerName}");
    }
}
```

## Kesimpulan

GroupDocs.Signature untuk .NET menyediakan solusi yang andal dan fleksibel untuk mencari dan memvalidasi tanda tangan digital dalam dokumen. Dalam tutorial ini, kami mengeksplorasi proses langkah demi langkah penerapan fungsi pencarian tanda tangan digital dalam aplikasi .NET, membekali Anda dengan pengetahuan untuk meningkatkan keamanan dan verifikasi integritas dokumen.

Dengan memanfaatkan GroupDocs.Signature, Anda dapat membangun sistem manajemen dokumen tangguh yang memastikan keaslian dan integritas dokumen digital Anda, menumbuhkan kepercayaan dan kepatuhan dalam proses bisnis Anda.

## Pertanyaan yang Sering Diajukan

### Bisakah GroupDocs.Signature memverifikasi keabsahan tanda tangan digital?

Ya, GroupDocs.Signature secara otomatis memvalidasi tanda tangan digital selama proses pencarian dan memberikan status validasi melalui `IsValid` milik `DigitalSignature` kelas.

### Format dokumen mana yang mendukung pencarian tanda tangan digital?

GroupDocs.Signature mendukung pencarian tanda tangan digital dalam berbagai format, termasuk PDF, dokumen Microsoft Office (Word, Excel, PowerPoint), format OpenOffice, dan banyak lagi.

### Dapatkah saya mencari tanda tangan digital dalam dokumen yang dilindungi kata sandi?

Ya, Anda dapat mencari tanda tangan digital dalam dokumen yang dilindungi kata sandi dengan memberikan kata sandi saat menginisialisasi `Signature` obyek:

```csharp
LoadOptions loadOptions = new LoadOptions() { Password = "your_password" };
using (Signature signature = new Signature(filePath, loadOptions))
{
    // Cari tanda tangan digital
}
```

### Bagaimana saya dapat memverifikasi apakah tanda tangan digital dibuat oleh orang tertentu?

Anda dapat memeriksa nama subjek sertifikat dan properti lainnya untuk memverifikasi identitas penandatangan:

```csharp
foreach (var signature in signatures)
{
    if (signature.Certificate?.SubjectName?.Contains("John Doe") == true)
    {
        Console.WriteLine("Found signature by John Doe");
    }
}
```

### Bisakah saya mengekstrak kunci publik dari sertifikat tanda tangan digital?

Ya, Anda dapat mengakses informasi kunci publik melalui properti sertifikat:

```csharp
if (signature.Certificate != null)
{
    // Akses informasi kunci publik
    Console.WriteLine($"Public Key: {signature.Certificate.GetPublicKeyString()}");
}
```

## Lihat Juga

* [Referensi API](https://reference.groupdocs.com/signature/net/)
* [Contoh Kode](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
* [Dokumentasi Produk](https://docs.groupdocs.com/signature/net/)
* [Halaman Produk](https://products.groupdocs.com/signature/net/)
* [Unduh Versi Terbaru](https://releases.groupdocs.com/signature/net/)
* [Artikel Blog](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
* [Forum Dukungan](https://forum.groupdocs.com/c/signature/13)
* [Lisensi Sementara](https://purchase.groupdocs.com/temporary-license/)