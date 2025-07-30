---
"date": "2025-05-07"
"description": "Pelajari cara menandatangani PDF secara digital dengan GroupDocs.Signature untuk .NET. Sesuaikan tampilan, terapkan font dan gambar, untuk memastikan keamanan dan keaslian dokumen."
"title": "Penandatanganan PDF Digital di .NET&#58; Panduan Menggunakan GroupDocs.Signature"
"url": "/id/net/digital-signatures/sign-pdf-digital-signature-groupdocs-dotnet/"
"weight": 1
---

# Penandatanganan PDF Digital di .NET: Panduan Menggunakan GroupDocs.Signature

## Perkenalan

Tanda tangan digital pada dokumen PDF memastikan keaslian, keamanan, dan integritasnya—penting untuk kontrak hukum, faktur, dan catatan resmi. **GroupDocs.Signature untuk .NET** Menyederhanakan penambahan tanda tangan digital ke PDF Anda sekaligus memungkinkan kustomisasi tampilannya untuk meningkatkan daya tarik visual. Tutorial ini akan memandu Anda melalui proses penandatanganan dokumen PDF menggunakan GroupDocs.Signature dengan fokus khusus pada konfigurasi gambar dan font.

### Apa yang Akan Anda Pelajari:
- Cara menandatangani dokumen PDF secara digital menggunakan .NET
- Terapkan pengaturan tampilan khusus seperti gambar dan font ke tanda tangan digital Anda
- Siapkan dan inisialisasi GroupDocs.Signature untuk .NET di proyek Anda

Mari kita mulai dengan membahas prasyarat yang diperlukan untuk memulai.

## Prasyarat (H2)

Untuk mengikuti tutorial ini, Anda memerlukan:

- **GroupDocs.Signature untuk .NET** pustaka: Pastikan diinstal melalui .NET CLI atau NuGet Package Manager.
  - **.NET CLI**: `dotnet add package GroupDocs.Signature`
  - **Manajer Paket**: `Install-Package GroupDocs.Signature`

- Sertifikat digital yang valid dalam format PFX
- Pengetahuan dasar tentang C# dan pengaturan lingkungan .NET

## Menyiapkan GroupDocs.Signature untuk .NET (H2)

Mulailah dengan menginstal pustaka GroupDocs.Signature:

**.NET CLI**
```shell
dotnet add package GroupDocs.Signature
```

**Manajer Paket**
```shell
Install-Package GroupDocs.Signature
```

Atau, gunakan UI NuGet Package Manager untuk mencari dan menginstal "GroupDocs.Signature".

### Akuisisi Lisensi

- **Uji Coba Gratis**:Jelajahi fitur lengkap dengan lisensi evaluasi sementara.
- **Lisensi Sementara**:Dapatkan dari [Di Sini](https://purchase.groupdocs.com/temporary-license/).
- **Pembelian**:Untuk penggunaan jangka panjang, beli langganan di [tautan ini](https://purchase.groupdocs.com/buy).

### Inisialisasi dan Pengaturan Dasar

Untuk menginisialisasi GroupDocs.Signature di proyek .NET Anda:

```csharp
using GroupDocs.Signature;

// Inisialisasi objek Tanda Tangan dengan berkas PDF sumber.
using (Signature signature = new Signature("YOUR_DOCUMENT_DIRECTORY/SAMPLE_PDF.pdf")) {
    // Kode Anda untuk menandatangani dokumen ada di sini.
}
```

## Panduan Implementasi

### Menandatangani Dokumen PDF dengan Tanda Tangan Digital (H2)

Fitur ini memungkinkan Anda menambahkan tanda tangan digital ke dokumen PDF Anda, memastikan keaslian dan integritasnya.

#### Ikhtisar Fitur
Dengan menerapkan fitur ini, Anda dapat menandatangani berkas PDF apa pun secara digital menggunakan GroupDocs.Signature untuk .NET. Anda juga akan menerapkan pengaturan khusus untuk menyesuaikan tampilan tanda tangan Anda, termasuk gambar dan font.

#### Langkah-Langkah Implementasi (H3)

##### Langkah 1: Siapkan Lingkungan Anda

Pastikan proyek Anda dikonfigurasi dengan referensi yang diperlukan:

```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Options;
using GroupDocs.Signature.Domain;

namespace DigitalSignatureExample {
    public class SignPdfWithDigitalSignature {
        // Tentukan jalur untuk PDF sumber dan sertifikat digital
        private static string sourceFile = "YOUR_DOCUMENT_DIRECTORY/SAMPLE_PDF.pdf";
        private static string outputFile = Path.Combine("YOUR_OUTPUT_DIRECTORY", "SignWithPdfDigitalAdvanced_Signed.pdf");
        private static string certificatePath = "YOUR_DOCUMENT_DIRECTORY/CertificatePfx.pfx";

        public static void Run() {
            // Inisialisasi objek Tanda Tangan
            using (Signature signature = new Signature(sourceFile)) {
                // Siapkan opsi penandatanganan digital
                DigitalSignOptions options = new DigitalSignOptions(certificatePath) {
                    Password = "1234567890",  // Kata sandi sertifikat
                    Reason = "Sign",          // Alasan penandatanganan
                    Contact = "JohnSmith",    // Informasi kontak
                    Location = "Office1",     // Lokasi penandatanganan
                    Visible = true,            // Jadikan tanda tangan terlihat
                    Left = 400,                // Posisi horizontal
                    Top = 20,                  // Posisi vertikal
                    Height = 70,               // Tinggi tanda tangan
                    Width = 200,               // Lebar tanda tangan
                    ImageFilePath = "YOUR_DOCUMENT_DIRECTORY/ImageHandwrite.png", // Gambar penampilan
                    Appearance = new PdfDigitalSignatureAppearance() {
                        Foreground = System.Drawing.Color.FromArgb(50, System.Drawing.Color.Gray),
                        FontFamilyName = "TimesNewRoman",
                        FontSize = 12
                    }
                };

                // Tanda tangani dokumen dan simpan ke jalur keluaran.
                SignResult signResult = signature.Sign(outputFile, options);
                Console.WriteLine($"Document signed successfully with {signResult.Succeeded.Count} signature(s). File saved at {outputFile}.");
            }
        }
    }
}
```

##### Langkah 2: Sesuaikan Tampilan Tanda Tangan

Sesuaikan tampilan tanda tangan digital Anda menggunakan pengaturan font dan gambar:

```csharp
using System;
using GroupDocs.Signature.Options;
using GroupDocs.Signature.Domain;
using System.Drawing;

namespace DigitalSignatureAppearanceExample {
    public class CustomizeDigitalSignatureAppearance {
        public static void Run() {
            // Inisialisasi pengaturan tampilan untuk tanda tangan digital.
            PdfDigitalSignatureAppearance appearance = new PdfDigitalSignatureAppearance() {
                Foreground = Color.FromArgb(50, Color.Gray),  // Tetapkan warna font khusus
                FontFamilyName = "TimesNewRoman",          // Tentukan keluarga font
                FontSize = 12                               // Tentukan ukuran font
            };

            Console.WriteLine("Custom appearance settings for digital signature have been applied.");
        }
    }
}
```

#### Opsi Konfigurasi Utama
- **Jalur Sertifikat**: Pastikan Anda memberikan jalur yang benar ke berkas PFX Anda.
- **Kata sandi**: Gunakan kata sandi yang terkait dengan sertifikat digital Anda.
- **Pengaturan Tampilan**: Sesuaikan font dan warna agar sesuai dengan kebutuhan merek.

##### Tips Pemecahan Masalah
- Verifikasi bahwa sertifikat digital Anda valid dan dikonfigurasi dengan benar.
- Pastikan semua jalur (PDF, keluaran, gambar) dapat diakses dari lingkungan aplikasi Anda.

### Terapkan Pengaturan Tampilan Kustom ke Tanda Tangan Digital (H2)

Tingkatkan daya tarik visual tanda tangan digital Anda dengan pengaturan font dan gambar yang disesuaikan menggunakan GroupDocs.Signature untuk .NET.

#### Ringkasan
Menyesuaikan tampilan tanda tangan digital dapat membuatnya lebih menarik secara visual dan selaras dengan standar merek. Fitur ini memungkinkan Anda mengatur font, warna, dan gambar tertentu.

#### Langkah-Langkah Implementasi (H3)

##### Langkah 1: Inisialisasi Pengaturan Tampilan

Buat contoh dari `PdfDigitalSignatureAppearance`:

```csharp
using System.Drawing;

// Tentukan pengaturan tampilan khusus untuk tanda tangan digital.
PdfDigitalSignatureAppearance appearance = new PdfDigitalSignatureAppearance() {
    Foreground = Color.FromArgb(50, Color.Gray),  // Warna font khusus
    FontFamilyName = "TimesNewRoman",            // Keluarga font
    FontSize = 12                                // Ukuran huruf
};
```

##### Langkah 2: Terapkan Pengaturan Tampilan

Integrasikan pengaturan ini ke dalam opsi tanda tangan digital Anda:

```csharp
DigitalSignOptions options = new DigitalSignOptions(certificatePath) {
    ImageFilePath = "YOUR_DOCUMENT_DIRECTORY/ImageHandwrite.png",
    Appearance = appearance
};
```

## Aplikasi Praktis (H2)

Berikut adalah beberapa skenario dunia nyata di mana penandatanganan PDF dengan GroupDocs.Signature dapat bermanfaat:
1. **Penandatanganan Kontrak**Pastikan perjanjian hukum ditandatangani dan diverifikasi secara digital.
2. **Persetujuan Faktur**:Tanda tangani faktur secara digital untuk pemrosesan yang lebih cepat di departemen keuangan.
3. **Autentikasi Dokumen**: Autentikasi dokumen resmi untuk mencegah perubahan yang tidak sah.

Dengan mengikuti panduan ini, Anda akan secara efektif mengintegrasikan penandatanganan digital ke dalam aplikasi .NET Anda menggunakan GroupDocs.Signature, meningkatkan keamanan dan profesionalisme.