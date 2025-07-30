---
"date": "2025-05-07"
"description": "Pelajari cara menandatangani dokumen PDF dengan Kode QR HIBC menggunakan GroupDocs.Signature untuk .NET. Panduan ini mencakup kode LIC dan PAS, termasuk Kode QR, Kode Aztec, dan DataMatrix."
"title": "Cara Menandatangani Dokumen dengan Kode QR HIBC Menggunakan GroupDocs.Signature untuk .NET&#58; Panduan Lengkap"
"url": "/id/net/qr-code-signatures/sign-documents-hibc-qr-groupdocs-dotnet/"
"weight": 1
---

# Cara Menandatangani Dokumen dengan Kode QR HIBC Menggunakan GroupDocs.Signature untuk .NET

## Perkenalan

Dalam lingkungan bisnis yang serba cepat saat ini, memastikan keaslian dan integritas dokumen sangatlah penting. Baik Anda menangani produk farmasi, produk perawatan kesehatan, atau logistik, memiliki metode penandatanganan dan pelacakan dokumen yang aman dapat menghemat waktu dan mencegah kesalahan. Masukkan **GroupDocs.Signature untuk .NET**, pustaka canggih yang dirancang untuk menyederhanakan proses manajemen dokumen dengan memungkinkan integrasi Kode QR HIBC yang mulus ke dalam dokumen Anda.

Dalam tutorial ini, kita akan membahas cara memanfaatkan GroupDocs.Signature for .NET untuk menandatangani dokumen PDF dengan berbagai jenis kode QR HIBC—LIC (Lisensi) dan PAS (Sistem Autentikasi Produk)—termasuk Kode QR, Kode Aztec, dan DataMatrix. Pada akhirnya, Anda akan memiliki pemahaman yang mendalam tentang penerapan solusi ini dalam aplikasi .NET Anda.

**Apa yang Akan Anda Pelajari:**
- Cara mengatur GroupDocs.Signature untuk .NET
- Menerapkan Kode QR HIBC LIC, Kode Aztec, dan DataMatrix
- Menambahkan Kode QR HIBC PAS, Kode Aztec, dan DataMatrix
- Kasus penggunaan praktis dan kemungkinan integrasi

Mari selami prasyaratnya sebelum kita mulai menerapkan fitur-fitur ini.

## Prasyarat

Sebelum kita memulai pengkodean, pastikan Anda telah menyiapkan hal-hal berikut:

- **Lingkungan .NET**:Pastikan Anda telah menginstal .NET di sistem Anda (sebaiknya .NET Core atau .NET 5/6+).
- **GroupDocs.Signature untuk .NET**Pustaka ini akan menjadi alat utama kita. Anda dapat menginstalnya melalui NuGet.
- **Pengetahuan Pemrograman Dasar**: Disarankan untuk memahami C# dan menangani file dalam .NET.

### Perpustakaan yang Diperlukan

Untuk menggunakan GroupDocs.Signature untuk .NET, Anda perlu menambahkan paket menggunakan salah satu metode berikut:

**.NET CLI**
```bash
dotnet add package GroupDocs.Signature
```

**Manajer Paket**
```powershell
Install-Package GroupDocs.Signature
```

**Antarmuka Pengguna Pengelola Paket NuGet**
Cari "GroupDocs.Signature" dan instal versi terbaru.

### Akuisisi Lisensi

Untuk tujuan pengujian, Anda bisa mendapatkan lisensi uji coba gratis. Untuk penggunaan jangka panjang, pertimbangkan untuk membeli langganan atau meminta lisensi sementara:

- **Uji Coba Gratis**: Akses [Di Sini](https://releases.groupdocs.com/signature/net/)
- **Lisensi Sementara**: Permintaan di [tautan ini](https://purchase.groupdocs.com/temporary-license/)

### Pengaturan Lingkungan

Siapkan lingkungan Anda dengan memastikan proyek Anda menargetkan versi .NET yang sesuai dan memiliki akses ke GroupDocs.Signature. Inisialisasi di aplikasi Anda seperti yang ditunjukkan:

```csharp
using GroupDocs.Signature;
```

## Menyiapkan GroupDocs.Signature untuk .NET

Untuk mulai menggunakan GroupDocs.Signature untuk .NET, Anda perlu menginstal pustaka dan mengonfigurasi pengaturan dasar dalam proyek Anda.

### Instalasi

Ikuti salah satu metode yang disebutkan di atas untuk menambahkan GroupDocs.Signature ke proyek Anda. Setelah terinstal, pastikan proyek Anda dikonfigurasi untuk menggunakannya dengan merujuknya di berkas kode Anda.

### Inisialisasi Lisensi

Setelah memperoleh lisensi, inisialisasikan sebagai berikut:

```csharp
SignatureConfig signConfig = new SignatureConfig();
signConfig.LicensePath = "path/to/your/license.lic";
Signature signature = new Signature("Sample.pdf", signConfig);
```

Pengaturan ini akan memungkinkan Anda mengakses semua fitur GroupDocs.Signature tanpa batasan.

## Panduan Implementasi

Sekarang, mari selami penerapan setiap fitur menggunakan Kode QR HIBC dengan GroupDocs.Signature untuk .NET.

### Tandatangani Dokumen dengan Kode QR HIBC LIC

#### Ringkasan

Menandatangani dokumen dengan Kode QR HIBC LIC memastikan kepatuhan dan ketertelusuran dalam skenario perizinan. Bagian ini akan memandu Anda dalam membuat dan menyematkan kode QR di dalam dokumen PDF Anda.

#### Langkah-Langkah Implementasi

##### Langkah 1: Konfigurasikan Jalur Sumber dan Output

Tentukan di mana dokumen sumber Anda berada dan di mana keluaran yang ditandatangani harus disimpan:

```csharp
string sourceFilePath = Path.Combine("YOUR_DOCUMENT_DIRECTORY", "Sample.pdf");
string outputPath = Path.Combine("YOUR_OUTPUT_DIRECTORY", "SignWithHIBCLICQR");
string destinFilePath = Path.Combine(outputPath, "SignedDocumentWithHIBCLICQR.pdf");
```

##### Langkah 2: Buat Opsi Tanda Tangan Kode QR

Konfigurasikan kode QR Anda dengan teks dan pengaturan tertentu:

```csharp
using (Signature signature = new Signature(sourceFilePath))
{
    var hibcLic_QR_Options = new QrCodeSignOptions("A123PROD30917/75#422011907#GP293", QrCodeTypes.HIBCLICQR)
    {
        Left = 1,
        Top = 1,
        ReturnContent = true,
        ReturnContentType = FileType.PNG
    };

    // Tandatangani dokumen dengan pilihan ini.
    signature.Sign(destinFilePath, hibcLic_QR_Options);
}
```

**Penjelasan**: 
- `QrCodeSignOptions` Mengatur tampilan dan isi kode QR. Di sini, kami menentukan jenis Kode QR HIBC LIC dan memposisikannya pada dokumen.
- `ReturnContent` Ditetapkan ke benar memungkinkan Anda mengambil gambar dokumen yang ditandatangani.

#### Tips Pemecahan Masalah

- Pastikan jalur dokumen ditentukan dengan benar.
- Verifikasi bahwa GroupDocs.Signature memiliki lisensi yang sesuai untuk fungsionalitas penuh.

### Tandatangani Dokumen dengan Kode Aztec HIBC LIC

#### Ringkasan

Kode Aztec menawarkan bentuk penyandian lain yang cocok untuk penyimpanan informasi berdensitas tinggi. Bagian ini berfokus pada penyematan kode Aztec ke dalam dokumen Anda menggunakan GroupDocs.Signature.

#### Langkah-Langkah Implementasi

##### Langkah 1: Konfigurasikan Jalur

Mirip dengan fitur sebelumnya, tentukan jalur file Anda:

```csharp
string sourceFilePath = Path.Combine("YOUR_DOCUMENT_DIRECTORY", "Sample.pdf");
string outputPath = Path.Combine("YOUR_OUTPUT_DIRECTORY", "SignWithHIBCLICAztec");
string destinFilePath = Path.Combine(outputPath, "SignedDocumentWithHIBCLICAztec.pdf");
```

##### Langkah 2: Konfigurasikan Opsi Kode Aztec

Siapkan kode Aztec Anda menggunakan GroupDocs.Signature:

```csharp
using (Signature signature = new Signature(sourceFilePath))
{
    var hibcLic_AZ_Options = new QrCodeSignOptions("A123PROD30917/75#422011907#GP293", QrCodeTypes.HIBCLICAztec)
    {
        Left = 1,
        Top = 200,
        ReturnContent = true,
        ReturnContentType = FileType.PNG
    };

    signature.Sign(destinFilePath, hibcLic_AZ_Options);
}
```

**Penjelasan**: 
- Itu `QrCodeSignOptions` digunakan lagi di sini tetapi dengan tipe kode Aztec.
- Penempatan (`Top`, `Left`) dan pengaturan pengambilan konten serupa dengan kode QR.

#### Tips Pemecahan Masalah

- Konfirmasikan bahwa jalur berkas akurat.
- Pastikan versi GroupDocs.Signature mendukung jenis Kode Aztec.

### Tandatangani Dokumen dengan HIBC LIC DataMatrix

#### Ringkasan

Kode DataMatrix menyediakan metode lain yang andal untuk menyimpan data. Bagian ini menunjukkan cara mengintegrasikan DataMatrix ke dalam dokumen PDF Anda.

#### Langkah-Langkah Implementasi

##### Langkah 1: Tetapkan Jalur File

Seperti sebelumnya, tentukan di mana file Anda berada:

```csharp
string sourceFilePath = Path.Combine("YOUR_DOCUMENT_DIRECTORY", "Sample.pdf");
string outputPath = Path.Combine("YOUR_OUTPUT_DIRECTORY", "SignWithHIBCLICDataMatrix");
string destinFilePath = Path.Combine(outputPath, "SignedDocumentWithHIBCLICDataMatrix.pdf");
```

##### Langkah 2: Buat Opsi Tanda DataMatrix

Konfigurasikan dan terapkan kode DataMatrix:

```csharp
using (Signature signature = new Signature(sourceFilePath))
{
    var hibcLic_DM_Options = new QrCodeSignOptions("A123PROD30917/75#422011907#GP293", QrCodeTypes.HIBCLICDataMatrix)
    {
        Left = 1,
        Top = 400,
        ReturnContent = true,
        ReturnContentType = FileType.PNG
    };

    signature.Sign(destinFilePath, hibcLic_DM_Options);
}
```

**Penjelasan**: 
- `QrCodeSignOptions` digunakan untuk mengatur tampilan dan konten kode DataMatrix.
- Penempatan (`Top`, `Left`) dan pengaturan pengambilan mengikuti pola yang sama seperti kode sebelumnya.

#### Tips Pemecahan Masalah

- Pastikan semua jalur berkas ditentukan dengan benar.
- Verifikasi bahwa GroupDocs.Signature mendukung jenis Kode DataMatrix di versi Anda.

### Tandatangani Dokumen dengan Kode QR HIBC PAS

#### Ringkasan

Menandatangani dokumen dengan Kode QR HIBC PAS meningkatkan pelacakan dan ketertelusuran produk. Bagian ini memandu Anda untuk menyematkan kode QR PAS ke dalam PDF menggunakan GroupDocs.Signature.

#### Langkah-Langkah Implementasi

##### Langkah 1: Konfigurasikan Jalur Sumber dan Output

Tentukan di mana dokumen sumber Anda berada dan di mana keluaran yang ditandatangani harus disimpan:

```csharp
string sourceFilePath = Path.Combine("YOUR_DOCUMENT_DIRECTORY", "Sample.pdf");
string outputPath = Path.Combine("YOUR_OUTPUT_DIRECTORY", "SignWithHIBCPASQR");
string destinFilePath = Path.Combine(outputPath, "SignedDocumentWithHIBCPASQR.pdf");
```

##### Langkah 2: Buat Opsi Tanda Tangan Kode QR

Konfigurasikan kode QR PAS Anda dengan teks dan pengaturan tertentu:

```csharp
using (Signature signature = new Signature(sourceFilePath))
{
    var hibcPas_QR_Options = new QrCodeSignOptions("PAS123456789012", QrCodeTypes.HIBCPASQR)
    {
        Left = 1,
        Top = 500,
        ReturnContent = true,
        ReturnContentType = FileType.PNG
    };

    // Tandatangani dokumen dengan pilihan ini.
    signature.Sign(destinFilePath, hibcPas_QR_Options);
}
```

**Penjelasan**: 
- `QrCodeSignOptions` dikonfigurasikan untuk jenis Kode QR HIBC PAS dan diposisikan pada dokumen.
- `ReturnContent` diatur ke benar akan mengambil gambar dokumen yang ditandatangani.

#### Tips Pemecahan Masalah

- Pastikan semua jalur ditentukan dengan benar.
- Verifikasi bahwa GroupDocs.Signature mendukung jenis Kode QR PAS di versi Anda.

### Kesimpulan

Dengan mengikuti panduan ini, Anda dapat mengintegrasikan Kode QR HIBC LIC dan PAS ke dalam dokumen PDF secara efisien menggunakan GroupDocs.Signature untuk .NET. Proses ini meningkatkan keamanan dokumen, ketertelusuran, dan kepatuhan di berbagai industri. Untuk kustomisasi lebih lanjut dan fitur lanjutan, silakan lihat [Dokumentasi GroupDocs](https://docs.groupdocs.com/signature/net/).