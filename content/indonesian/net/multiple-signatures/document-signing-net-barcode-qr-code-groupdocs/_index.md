---
"date": "2025-05-07"
"description": "Pelajari cara menerapkan tanda tangan kode batang dan kode QR di aplikasi .NET Anda menggunakan GroupDocs.Signature. Tingkatkan keamanan dokumen dan sederhanakan alur kerja digital."
"title": "Menguasai Penandatanganan Dokumen di .NET™ Barcode & QR Code Signature dengan GroupDocs.Signature"
"url": "/id/net/multiple-signatures/document-signing-net-barcode-qr-code-groupdocs/"
"weight": 1
type: docs
---
# Menguasai Penandatanganan Dokumen di .NET: Menerapkan Tanda Tangan Kode Batang dan Kode QR dengan GroupDocs.Signature

## Perkenalan
Di era digital saat ini, memastikan keaslian dan integritas dokumen menjadi lebih penting dari sebelumnya. Metode tradisional seperti tanda tangan tinta dengan cepat menjadi usang karena bisnis mengadopsi solusi elektronik untuk efisiensi dan keamanan. Masuk **GroupDocs.Signature untuk .NET**pustaka canggih yang dirancang untuk mengintegrasikan fungsionalitas tanda tangan kode batang dan kode QR secara mulus ke dalam aplikasi .NET Anda. Baik Anda perlu menandatangani kontrak, faktur, atau dokumen sensitif lainnya secara elektronik, GroupDocs.Signature menawarkan solusi canggih yang disesuaikan dengan kebutuhan modern.

Tutorial ini akan memandu Anda melalui proses penandatanganan dokumen menggunakan opsi kode batang dan kode QR dengan GroupDocs.Signature untuk .NET. Di akhir artikel ini, Anda akan mempelajari cara:
- Siapkan lingkungan Anda untuk menggunakan GroupDocs.Signature
- Terapkan penandatanganan dokumen dengan tanda tangan kode batang
- Terapkan penandatanganan dokumen dengan tanda tangan kode QR

## Prasyarat
Sebelum menerapkan tanda tangan kode batang dan kode QR, pastikan Anda telah menyiapkan hal-hal berikut:

### Pustaka, Versi, dan Ketergantungan yang Diperlukan
- **GroupDocs.Signature untuk .NET**: Pastikan Anda telah menginstal versi terbaru.
  
### Persyaratan Pengaturan Lingkungan
- Versi .NET framework yang kompatibel (misalnya, .NET Core 3.1 atau yang lebih baru).
- Visual Studio atau IDE pilihan apa pun yang mendukung pengembangan .NET.

### Prasyarat Pengetahuan
- Pemahaman dasar tentang pengembangan aplikasi C# dan .NET.
- Keakraban dengan penanganan berkas dan manajemen direktori dalam C#.

Dengan prasyarat yang terpenuhi, mari kita lanjutkan ke pengaturan GroupDocs.Signature untuk .NET.

## Menyiapkan GroupDocs.Signature untuk .NET
GroupDocs.Signature untuk .NET tersedia melalui beberapa pengelola paket. Berikut cara menambahkannya ke proyek Anda:

**Menggunakan .NET CLI:**
```bash
dotnet add package GroupDocs.Signature
```

**Menggunakan Konsol Manajer Paket:**
```powershell
Install-Package GroupDocs.Signature
```

**Menggunakan UI Pengelola Paket NuGet:**
1. Buka NuGet Package Manager di Visual Studio.
2. Cari "GroupDocs.Signature" dan instal versi terbaru.

### Langkah-Langkah Perolehan Lisensi
- **Uji Coba Gratis**: Uji coba GroupDocs.Signature dengan lisensi uji coba gratis untuk menjelajahi fitur-fiturnya.
- **Lisensi Sementara**Dapatkan lisensi sementara untuk pengujian lanjutan sebelum membeli.
- **Pembelian**: Beli langganan atau lisensi abadi untuk penggunaan produksi.

Untuk menginisialisasi GroupDocs.Signature, buatlah sebuah instance dari `Signature` kelas dan tentukan dokumen yang ingin Anda tanda tangani. Berikut pengaturan dasarnya:
```csharp
using (Signature signature = new Signature("path/to/your/document"))
{
    // Logika penandatanganan Anda di sini
}
```
Setelah lingkungan Anda siap, mari selami penerapan tanda tangan kode batang dan kode QR.

## Panduan Implementasi

### Menandatangani Dokumen dengan Opsi Kode Batang

#### Ringkasan
Kode batang adalah cara yang efisien untuk mengodekan informasi dalam format yang dapat dibaca mesin. Dengan GroupDocs.Signature, Anda dapat menambahkan tanda tangan kode batang ke dokumen untuk keamanan dan verifikasi data tambahan.

**Langkah 1: Tentukan Jalur File**
```csharp
string filePath = Path.Combine("YOUR_DOCUMENT_DIRECTORY", "sample.zip");
string fileName = Path.GetFileName(filePath);
string outputPath = Path.Combine("YOUR_OUTPUT_DIRECTORY", "SignWithBarcodeOptions");
string outputFilePath = Path.Combine(outputPath, fileName);
```

**Langkah 2: Buat Instansi Tanda Tangan dan Tentukan Opsi**
```csharp
using (Signature signature = new Signature(filePath))
{
    BarcodeSignOptions bcOptions1 = new BarcodeSignOptions("12345678", BarcodeTypes.Code128)
    {
        Left = 100,
        Top = 100
    };
    
    List<SignOptions> listOptions = new List<SignOptions>() { bcOptions1 };
    
    // Tanda tangani dokumen dan simpan di jalur keluaran yang ditentukan
    SignResult signResult = signature.Sign(outputFilePath, listOptions);
}
```

**Penjelasan:**
- `BarcodeSignOptions`: Menginisialisasi opsi penandatanganan kode batang dengan string data dan jenis.
- `Left` Dan `Top`Tentukan posisi pada halaman di mana kode batang akan ditempatkan.

### Menandatangani Dokumen dengan Opsi Kode QR

#### Ringkasan
Kode QR adalah alat serbaguna untuk menyimpan informasi yang dapat dengan mudah dipindai oleh perangkat. Mengintegrasikan tanda tangan kode QR ke dalam dokumen Anda meningkatkan ketertelusuran dan autentikasi.

**Langkah 1: Tentukan Jalur File**
```csharp
string filePath = Path.Combine("YOUR_DOCUMENT_DIRECTORY", "sample.zip");
string fileName = Path.GetFileName(filePath);
string outputPath = Path.Combine("YOUR_OUTPUT_DIRECTORY", "SignWithQrCodeOptions");
string outputFilePath = Path.Combine(outputPath, fileName);
```

**Langkah 2: Buat Instansi Tanda Tangan dan Tentukan Opsi**
```csharp
using (Signature signature = new Signature(filePath))
{
    QrCodeSignOptions qrOptions2 = new QrCodeSignOptions("12345678", QrCodeTypes.QR)
    {
        Left = 400,
        Top = 400
    };
    
    List<SignOptions> listOptions = new List<SignOptions>() { qrOptions2 };
    
    // Tanda tangani dokumen dan simpan di jalur keluaran yang ditentukan
    SignResult signResult = signature.Sign(outputFilePath, listOptions);
}
```

**Penjelasan:**
- `QrCodeSignOptions`: Menginisialisasi opsi penandatanganan kode QR dengan string data dan jenis.
- Parameter posisi (`Left` Dan `Top`) menentukan di mana pada halaman kode QR akan muncul.

### Tips Pemecahan Masalah
- Pastikan jalur berkas masukan Anda benar untuk menghindari kesalahan berkas tidak ditemukan.
- Validasi format data kode batang atau kode QR, karena format yang salah dapat menyebabkan kegagalan penandatanganan.
- Periksa apakah izin yang diberikan cukup pada direktori keluaran untuk menulis dokumen yang ditandatangani.

## Aplikasi Praktis
Berikut adalah beberapa kasus penggunaan dunia nyata di mana GroupDocs.Signature dengan kode batang dan kode QR dapat diterapkan:
1. **Kontrak dan Perjanjian**Penandatanganan kontrak yang aman dengan menyematkan pengenal unik atau metadata tambahan menggunakan kode batang/kode QR.
2. **Faktur dan Penagihan**: Gunakan tanda tangan kode batang untuk memastikan keaslian faktur dan mencegah pemalsuan pada dokumen keuangan.
3. **Dokumen Hukum**: Tambahkan lapisan keamanan ekstra ke dokumen hukum sensitif dengan tanda tangan kode QR yang dapat membawa data verifikasi tambahan.
4. **Rekam medis**: Tingkatkan manajemen rekam medis pasien dengan menyematkan kode QR untuk akses cepat ke riwayat medis atau rencana perawatan.

## Pertimbangan Kinerja
Saat bekerja dengan GroupDocs.Signature, pertimbangkan kiat berikut untuk mengoptimalkan kinerja:
- **Pemrosesan Batch**:Untuk dokumen bervolume besar, terapkan pemrosesan batch untuk menangani banyak penandatanganan secara efisien.
- **Manajemen Sumber Daya**Lepaskan sumber daya segera setelah operasi penandatanganan untuk mencegah kebocoran memori dan meningkatkan respons aplikasi.
- **Format Data Optimal**: Gunakan format kode batang atau kode QR yang tepat yang menyeimbangkan kerumitan dengan keterbacaan.

## Kesimpulan
Tutorial ini membahas cara menggunakan GroupDocs.Signature untuk .NET untuk menandatangani dokumen secara elektronik menggunakan kode batang dan kode QR. Fitur-fitur ini tidak hanya meningkatkan keamanan dokumen tetapi juga menyederhanakan alur kerja digital, menjadikannya sangat penting dalam lanskap bisnis saat ini.

Untuk melanjutkan perjalanan Anda dengan GroupDocs.Signature, jelajahi fungsionalitas tambahan seperti tanda tangan stempel atau gambar dan integrasikan fitur ini ke dalam sistem yang lebih besar sesuai kebutuhan.

## Bagian FAQ
1. **Bagaimana cara mendapatkan lisensi uji coba gratis untuk GroupDocs.Signature?**
   - Kunjungi [halaman uji coba gratis](https://releases.groupdocs.com/signature/net/) untuk mengunduh lisensi uji coba Anda.
2. **Bisakah saya menandatangani dokumen PDF menggunakan GroupDocs.Signature?**
   - Ya, Anda dapat menggunakan GroupDocs.Signature untuk menandatangani berbagai format dokumen termasuk PDF.
3. **Apa sajakah jenis kode batang umum yang didukung oleh GroupDocs.Signature?**
   - GroupDocs mendukung beberapa jenis kode batang seperti Code128, QR, dan lainnya untuk aplikasi yang fleksibel.