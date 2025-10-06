---
"date": "2025-05-07"
"description": "Pelajari cara menandatangani citra DICOM dengan kode QR menggunakan GroupDocs.Signature untuk .NET. Panduan ini mencakup pengaturan, implementasi, dan verifikasi tanda tangan kode QR dalam pencitraan medis."
"title": "Cara Menandatangani Gambar DICOM dengan Kode QR Menggunakan GroupDocs.Signature untuk .NET&#58; Panduan Lengkap"
"url": "/id/net/qr-code-signatures/groupdocs-signature-net-dicom-images-qr-codes/"
"weight": 1
type: docs
---
# Cara Menandatangani Gambar DICOM dengan Kode QR Menggunakan GroupDocs.Signature untuk .NET: Panduan Lengkap

Mencari metode aman untuk mengautentikasi berkas DICOM Anda? Panduan lengkap ini akan menunjukkan cara menggunakan GroupDocs.Signature for .NET untuk mengintegrasikan tanda tangan kode QR ke dalam citra DICOM. Ideal untuk tenaga kesehatan profesional, pengembang, dan siapa pun yang bekerja dengan dokumen medis digital, tutorial ini mencakup pengaturan hingga implementasi.

## Apa yang Akan Anda Pelajari:
- Menyiapkan lingkungan pengembangan Anda dengan GroupDocs.Signature untuk .NET.
- Petunjuk langkah demi langkah tentang penandatanganan gambar DICOM menggunakan kode QR.
- Metode untuk memverifikasi dan mencari tanda tangan kode QR dalam file DICOM.
- Teknik untuk membuat pratinjau dokumen yang ditandatangani untuk tujuan peninjauan.
- Praktik terbaik untuk mengoptimalkan kinerja dan mengelola sumber daya secara efektif.

Mari kita mulai dengan prasyarat!

## Prasyarat

Untuk menggunakan GroupDocs.Signature untuk .NET, pastikan lingkungan Anda sudah siap. Berikut yang Anda perlukan:

### Pustaka dan Versi yang Diperlukan
- **GroupDocs.Signature untuk .NET**Pastikan kompatibilitas dengan kerangka kerja .NET Anda.

### Persyaratan Pengaturan Lingkungan
- Lingkungan pengembangan pada Windows atau Linux.
- Visual Studio atau IDE lain yang kompatibel dengan .NET terpasang.

### Prasyarat Pengetahuan
- Pemahaman dasar tentang pemrograman C#.
- Keakraban dengan file I/O dalam aplikasi .NET.

## Menyiapkan GroupDocs.Signature untuk .NET

Instal pustaka GroupDocs.Signature menggunakan metode pilihan Anda:

**Menggunakan .NET CLI:**
```bash
dotnet add package GroupDocs.Signature
```

**Manajer Paket:**
```powershell
Install-Package GroupDocs.Signature
```

**Antarmuka Pengguna Pengelola Paket NuGet:**
- Cari "GroupDocs.Signature" dan instal versi terbaru.

### Akuisisi Lisensi

Mulailah dengan uji coba gratis untuk menjelajahi berbagai kemampuannya. Untuk penggunaan jangka panjang, pertimbangkan untuk mendapatkan lisensi sementara atau penuh dari [GroupDocs](https://purchase.groupdocs.com/buy).

Setelah terinstal, inisialisasi perpustakaan:

```csharp
using GroupDocs.Signature;
// Inisialisasi objek Tanda Tangan dengan jalur file DICOM Anda.
Signature signature = new Signature("YOUR_DOCUMENT_DIRECTORY\\sample.dicom");
```

## Panduan Implementasi

### Tandatangani Gambar DICOM dengan Kode QR

#### Ringkasan
Tambahkan tanda tangan kode QR untuk memastikan keaslian dan keterlacakan dokumen medis.

**Langkah 1: Inisialisasi Objek Tanda Tangan**

```csharp
string filePath = "YOUR_DOCUMENT_DIRECTORY\\sample.dicom";
using (Signature signature = new Signature(filePath))
{
    // Lanjutkan dengan operasi penandatanganan...
}
```

**Langkah 2: Buat Opsi Tanda Tangan Kode QR**

Konfigurasikan properti seperti teks, ukuran, dan perataan.

```csharp
QrCodeSignOptions options = new QrCodeSignOptions("Patient #36363393. R: No-Issues")
{
    AllPages = true,
    Width = 100,
    Height = 100,
    VerticalAlignment = VerticalAlignment.Bottom,
    HorizontalAlignment = HorizontalAlignment.Right,
    Margin = new Padding() { Right = 5, Left = 5 }
};
```

**Langkah 3: Tambahkan Metadata XMP**

Tingkatkan dokumen dengan metadata tambahan.

```csharp
DicomSaveOptions dicomSaveOptions = new DicomSaveOptions()
{
    XmpEntries = new List<DicomXmpEntry>() { new DicomXmpEntry(DicomXmpType.PatientName, "Patient #4") }
};
```

**Langkah 4: Tandatangani Dokumen**

Jalankan penandatanganan dan simpan.

```csharp
SignResult signResult = signature.Sign("YOUR_OUTPUT_DIRECTORY\\SignedDicom", options, dicomSaveOptions);
```

### Dapatkan Info Dokumen

Ambil metadata dari file DICOM yang ditandatangani untuk memastikan integritas data.

**Ringkasan:**
Akses informasi dokumen dan tanda tangan metadata XMP untuk verifikasi.

**Langkah 1: Ambil Informasi Dokumen**

```csharp
using (Signature signature = new Signature("YOUR_DOCUMENT_DIRECTORY\\sample_signed.dicom"))
{
    IDocumentInfo signedDocumentInfo = signature.GetDocumentInfo();
}
```

**Langkah 2: Ulangi dan Cetak Data XMP**

Menampilkan detail metadata.

```csharp
foreach (var item in signedDocumentInfo.MetadataSignatures)
{
    Console.WriteLine(item.ToString());
}
```

### Verifikasi Tanda Tangan DICOM

Validasi keaslian tanda tangan kode QR dalam gambar DICOM.

**Ringkasan:**
Pastikan tanda tangan benar dan autentik.

**Langkah 1: Buat Opsi Verifikasi Kode QR**

Tetapkan pilihan yang cocok dengan teks tertentu dalam kode QR.

```csharp
QrCodeVerifyOptions options = new QrCodeVerifyOptions()
{
    AllPages = true,
    Text = "Patient #36363393",
    MatchType = TextMatchType.Contains
};
```

**Langkah 2: Verifikasi Tanda Tangan**

Periksa apakah tanda tangan memenuhi kriteria.

```csharp
VerificationResult result = signature.Verify(options);

if (result.IsValid)
{
    Console.WriteLine($"DICOM {filePath} has {result.Succeeded.Count} successfully verified signatures!");
}
```

### Mencari Tanda Tangan di DICOM

Temukan tanda tangan kode QR dalam gambar DICOM yang ditandatangani.

**Ringkasan:**
Temukan semua tanda tangan kode QR secara efisien untuk mengelola keaslian dokumen.

**Langkah 1: Cari Tanda Tangan Kode QR**

```csharp
List<QrCodeSignature> signatures = signature.Search<QrCodeSignature>(SignatureType.QrCode);
```

**Langkah 2: Ulangi dan Cetak Detail Tanda Tangan**

Tinjau detail setiap tanda tangan yang ditemukan.

```csharp
foreach (var QrCodeSignature in signatures)
{
    Console.WriteLine($"QRCode signature found at page {QrCodeSignature.PageNumber} with type {QrCodeSignature.EncodeType.TypeName} and text {QrCodeSignature.Text}");
}
```

### Hasilkan Pratinjau DICOM yang Ditandatangani

Buat pratinjau visual untuk verifikasi.

**Ringkasan:**
Hasilkan pratinjau gambar untuk memverifikasi konten tanpa perangkat lunak khusus.

**Langkah 1: Tentukan Metode Aliran**

Siapkan metode untuk manajemen aliran berkas selama pembuatan pratinjau.

```csharp
Stream CreatePageStream(PreviewPageData pageData)
{
    string imageFilePath = Path.Combine("YOUR_OUTPUT_DIRECTORY", "SignDicomImageAdvanced", $"preview-{pageData.PageNumber}.jpg");
    var folder = Path.GetDirectoryName(imageFilePath);
    if (!Directory.Exists(folder))
    {
        Directory.CreateDirectory(folder);
    }
    return new FileStream(imageFilePath, FileMode.Create);
}

void ReleasePageStream(PreviewPageData pageData, Stream pageStream)
{
    pageStream.Dispose();
}
```

**Langkah 2: Buat Pratinjau**

Jalankan proses pembuatan pratinjau.

```csharp
using (Signature signature = new Signature("YOUR_DOCUMENT_DIRECTORY\\sample_signed.dicom"))
{
    PreviewOptions previewOption = new PreviewOptions(CreatePageStream, ReleasePageStream)
    {
        PreviewFormat = PreviewOptions.PreviewFormats.PNG,
    };

    signature.GeneratePreview(previewOption);
}
```

## Aplikasi Praktis

1. **Manajemen Rekam Medis**: Autentikasi catatan pasien menggunakan tanda tangan kode QR untuk kepatuhan.
2. **Jejak Audit dalam Sistem Pelayanan Kesehatan**: Melacak perubahan dokumen dan memverifikasi keaslian dengan kode QR.
3. **Berbagi Data Aman**: Pastikan pembagian gambar medis aman dengan menanamkan tanda tangan digital.
4. **Verifikasi Kepatuhan**: Verifikasi integritas berkas DICOM secara berkala untuk memenuhi persyaratan hukum.
5. **Integrasi dengan Sistem EHR**:Integrasikan secara mulus file DICOM yang telah ditandatangani ke dalam sistem Catatan Kesehatan Elektronik (EHR) untuk operasi yang efisien.