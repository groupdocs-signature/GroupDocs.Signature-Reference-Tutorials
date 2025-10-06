---
"description": "Terapkan verifikasi tanda tangan digital yang aman di aplikasi .NET dengan GroupDocs.Signature. Panduan langkah demi langkah dengan contoh kode lengkap untuk autentikasi dokumen."
"linktitle": "Verifikasi Tanda Tangan Digital"
"second_title": "GroupDocs.Signature .NET API"
"title": "Verifikasi Tanda Tangan Digital dalam Dokumen"
"url": "/id/net/verify-operations/verify-digital/"
"weight": 11
type: docs
---
## Perkenalan

Tanda tangan digital memainkan peran penting dalam memastikan keaslian, integritas, dan nir-penyangkalan dokumen dalam proses bisnis modern. Tidak seperti tanda tangan tradisional, tanda tangan digital menggunakan teknik kriptografi untuk memverifikasi identitas penanda tangan dan memastikan bahwa dokumen tersebut tidak diubah sejak ditandatangani.

GroupDocs.Signature untuk .NET menyediakan perangkat lengkap yang memungkinkan pengembang menerapkan verifikasi tanda tangan digital yang andal dalam aplikasi .NET mereka. Tutorial mendetail ini akan memandu Anda melalui proses verifikasi tanda tangan digital dalam dokumen menggunakan GroupDocs.Signature untuk .NET.

## Prasyarat

Sebelum menerapkan fungsi verifikasi tanda tangan digital, pastikan Anda memiliki prasyarat berikut:

1. GroupDocs.Signature untuk .NET: Unduh dan instal pustaka dari [GroupDocs.Signature untuk rilis .NET](https://releases.groupdocs.com/signature/net/).
2. Lingkungan Pengembangan .NET: Visual Studio atau lingkungan pengembangan .NET yang kompatibel.
3. Sertifikat Digital: Berkas sertifikat digital (misalnya, .pfx) yang digunakan untuk menandatangani dokumen atau sertifikat yang termasuk dalam rantai tepercaya.
4. Dokumen untuk Verifikasi: Dokumen yang berisi tanda tangan digital yang memerlukan verifikasi.

## Mengimpor Namespace yang Diperlukan

Mulailah dengan mengimpor namespace yang diperlukan untuk mengakses fungsionalitas GroupDocs.Signature:

```csharp
using System;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

Mari kita uraikan proses verifikasi tanda tangan digital menjadi langkah-langkah yang jelas dan mudah dikelola:

## Langkah 1: Tentukan Jalur Dokumen

```csharp
// Jalur ke dokumen yang berisi tanda tangan digital
string filePath = "sample_multiple_signatures.docx";
```

Ganti jalur contoh dengan jalur sebenarnya ke dokumen Anda yang berisi tanda tangan digital.

## Langkah 2: Inisialisasi Objek Tanda Tangan

```csharp
// Buat instance kelas Signature dengan meneruskan jalur dokumen
using (Signature signature = new Signature(filePath))
{
    // Kode verifikasi akan diterapkan di sini
}
```

Kelas Signature adalah titik masuk utama untuk semua operasi di API GroupDocs.Signature.

## Langkah 3: Konfigurasikan Opsi Verifikasi Digital

```csharp
// Siapkan opsi verifikasi
DigitalVerifyOptions options = new DigitalVerifyOptions("YourSignature.pfx")
{
    Contact = "Mr.Smith",     // Kontak penandatangan yang diharapkan
    Password = "1234567890",  // Kata sandi sertifikat jika diperlukan
    AllPages = true           // Periksa semua halaman untuk tanda tangan
};
```

Pilihan verifikasi memungkinkan Anda menentukan:
- Jalur file sertifikat digital
- Informasi kontak penandatangan yang diharapkan
- Kata sandi untuk sertifikat jika dilindungi kata sandi
- Rentang halaman yang akan diverifikasi (semua halaman secara default)

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
    Console.WriteLine($"Document {filePath} contains valid digital signatures!");
    
    // Menampilkan detail tanda tangan yang valid
    foreach (DigitalSignature digitalSignature in result.Succeeded)
    {
        Console.WriteLine($"\nValid signature found:");
        Console.WriteLine($"Signer: {digitalSignature.Subject}");
        Console.WriteLine($"Issuer: {digitalSignature.Issuer}");
        Console.WriteLine($"Valid From: {digitalSignature.ValidFrom}");
        Console.WriteLine($"Valid To: {digitalSignature.ValidTo}");
    }
}
else
{
    Console.WriteLine($"Document {filePath} failed verification process.");
    
    // Menampilkan informasi tentang tanda tangan yang gagal jika diperlukan
    foreach (DigitalSignature failedSignature in result.Failed)
    {
        Console.WriteLine($"Failed signature reason: {failedSignature.Comments}");
    }
}
```

Kode ini memeriksa apakah verifikasi berhasil dan memberikan informasi terperinci tentang tanda tangan yang diverifikasi.

## Contoh Lengkap

Berikut contoh kerja lengkap yang menunjukkan verifikasi tanda tangan digital:

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
                    DigitalVerifyOptions options = new DigitalVerifyOptions("YourSignature.pfx")
                    {
                        Contact = "Mr.Smith",
                        Password = "1234567890"
                    };
                    
                    // Verifikasi tanda tangan dokumen
                    VerificationResult result = signature.Verify(options);
                    
                    // Hasil verifikasi proses
                    if (result.IsValid)
                    {
                        Console.WriteLine($"Document {filePath} contains valid digital signatures!");
                        
                        foreach (DigitalSignature item in result.Succeeded)
                        {
                            Console.WriteLine($"\nValid signature found.");
                            Console.WriteLine($"Subject: {item.Subject}");
                            Console.WriteLine($"Comments: {item.Comments}");
                            Console.WriteLine($"Sign Time: {item.SignTime}");
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

### Memverifikasi Beberapa Tanda Tangan Digital

```csharp
// Buat daftar opsi verifikasi
List<VerifyOptions> listOptions = new List<VerifyOptions>();

// Tambahkan opsi verifikasi sertifikat pertama
listOptions.Add(new DigitalVerifyOptions("Certificate1.pfx")
{
    Contact = "John Smith"
});

// Tambahkan opsi verifikasi sertifikat kedua
listOptions.Add(new DigitalVerifyOptions("Certificate2.pfx")
{
    Contact = "Jane Doe"
});

// Verifikasi dengan beberapa opsi
VerificationResult result = signature.Verify(listOptions);
```

### Memverifikasi Tanda Tangan pada Halaman Tertentu

```csharp
// Verifikasi tanda tangan digital hanya di halaman pertama
DigitalVerifyOptions options = new DigitalVerifyOptions("YourSignature.pfx")
{
    AllPages = false,
    PageNumber = 1
};
```

### Menggunakan Validasi Stempel Waktu dan Otoritas Sertifikat

```csharp
DigitalVerifyOptions options = new DigitalVerifyOptions("YourSignature.pfx")
{
    ValidateTimeStampOnly = true,   // Validasi hanya stempel waktu
    CertificateAuth = CertificateAuthType.Standard  // Memvalidasi sertifikat penandatangan
};
```

## Praktik Terbaik untuk Verifikasi Tanda Tangan Digital

1. Manajemen Sertifikat yang Tepat: Simpan file sertifikat dengan aman dan kelola kata sandi dengan tepat.
2. Validasi Sertifikat: Terapkan validasi rantai sertifikat untuk memastikan sertifikat itu sendiri valid.
3. Penanganan Kesalahan: Terapkan penanganan kesalahan yang kuat untuk mengelola kegagalan verifikasi dengan baik.
4. Pencatatan: Mencatat upaya verifikasi dan hasil untuk tujuan audit dan kepatuhan.
5. Pembaruan Sertifikat Secara Berkala: Pastikan sertifikat diperbarui sebelum kedaluwarsa.

## Pemecahan Masalah Umum

### Sertifikat Tidak Valid
- Verifikasi bahwa jalur file sertifikat sudah benar
- Pastikan kata sandi sertifikat benar
- Periksa apakah sertifikat telah kedaluwarsa

### Tanda Tangan Tidak Ditemukan
- Konfirmasikan bahwa dokumen tersebut benar-benar berisi tanda tangan digital
- Verifikasi bahwa Anda memeriksa halaman yang benar

### Kegagalan Verifikasi
- Periksa apakah dokumen telah dimodifikasi setelah penandatanganan
- Verifikasi bahwa sertifikat penanda tangan ada di rantai sertifikat tepercaya

## Kesimpulan

GroupDocs.Signature untuk .NET menyediakan solusi yang andal dan fleksibel untuk memverifikasi tanda tangan digital dalam dokumen. Dengan mengikuti panduan langkah demi langkah ini, Anda dapat menerapkan verifikasi tanda tangan digital yang andal di aplikasi .NET Anda, memastikan keaslian dan integritas dokumen.

Verifikasi tanda tangan digital merupakan komponen penting dari alur kerja dokumen yang aman di lingkungan bisnis modern. Dengan GroupDocs.Signature, Anda dapat menerapkan fungsionalitas ini dengan percaya diri dan mudah, memanfaatkan API yang komprehensif untuk menangani berbagai skenario verifikasi.

## Tanya Jawab Umum

### Bisakah GroupDocs.Signature memverifikasi tanda tangan dalam dokumen PDF yang ditandatangani menggunakan Adobe Acrobat?
Ya, GroupDocs.Signature dapat memverifikasi tanda tangan digital standar dalam dokumen PDF yang dibuat oleh Adobe Acrobat dan perangkat lunak PDF lain yang sesuai.

### Apakah GroupDocs.Signature mendukung verifikasi stempel waktu dokumen?
Ya, API menyediakan opsi untuk memverifikasi stempel waktu dokumen sebagai bagian dari proses verifikasi tanda tangan digital.

### Dapatkah saya memverifikasi tanda tangan pada halaman tertentu dari dokumen multi-halaman?
Ya, Anda dapat mengonfigurasi opsi verifikasi untuk memeriksa tanda tangan pada halaman tertentu, bukan keseluruhan dokumen.

### Apakah GroupDocs.Signature mendukung verifikasi beberapa tanda tangan dalam satu dokumen?
Ya, GroupDocs.Signature dapat memverifikasi beberapa tanda tangan digital dalam satu dokumen dan memberikan hasil terperinci untuk setiap tanda tangan.

### Apakah mungkin untuk memverifikasi tanda tangan yang dibuat dengan sertifikat dari otoritas sertifikat yang berbeda?
Ya, GroupDocs.Signature mendukung verifikasi tanda tangan yang dibuat dengan sertifikat dari otoritas sertifikat yang berbeda, selama mereka berada dalam rantai sertifikat tepercaya.

### Sumber Terkait
* [Referensi API GroupDocs.Signature](https://reference.groupdocs.com/signature/net/)
* [Unduhan GroupDocs.Signature](https://releases.groupdocs.com/signature/net/)
* [Contoh Kode di GitHub](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
* [Dokumentasi](https://docs.groupdocs.com/signature/net/)
* [Halaman Produk](https://products.groupdocs.com/signature/net/)
* [Artikel Blog](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
* [Forum Dukungan](https://forum.groupdocs.com/c/signature/13)
* [Lisensi Sementara](https://purchase.groupdocs.com/temporary-license/)