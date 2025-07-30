---
"date": "2025-05-07"
"description": "Pelajari cara mengintegrasikan tanda tangan GS1DotCode dan Kode QR HanXin ke dalam dokumen Anda dengan GroupDocs.Signature untuk .NET. Tingkatkan keamanan dan sederhanakan alur kerja."
"title": "Penandatanganan Dokumen Aman dengan GS1DotCode & Kode QR HanXin menggunakan GroupDocs.Signature untuk .NET"
"url": "/id/net/barcode-signatures/sign-documents-gs1dotcode-hanxin-qr-groupdocs-signature-dotnet/"
"weight": 1
---

# Penandatanganan Dokumen Aman dengan GS1DotCode & Kode QR HanXin menggunakan GroupDocs.Signature untuk .NET
## Cara Menandatangani Dokumen dengan GS1DotCode dan Kode QR HanXin Menggunakan GroupDocs.Signature untuk .NET
Di era digital saat ini, menandatangani dokumen secara elektronik dengan aman sangatlah penting. Baik Anda seorang profesional bisnis maupun pengembang yang ingin mengotomatiskan alur kerja, mengintegrasikan tanda tangan kode batang dan kode QR dapat meningkatkan keamanan dan menyederhanakan proses. Tutorial ini memandu Anda dalam penggunaan GroupDocs.Signature untuk .NET untuk mengimplementasikan tanda tangan GS1DotCode dan Kode QR HanXin di aplikasi Anda.
## Apa yang Akan Anda Pelajari
- Integrasikan GroupDocs.Signature untuk .NET ke dalam proyek Anda.
- Tandatangani dokumen dengan kode batang GS1DotCode.
- Terapkan tanda tangan Kode QR HanXin.
- Daftar tanda tangan yang baru dibuat setelah menandatangani dokumen.
- Memahami aplikasi praktis di dunia nyata dan pertimbangan kinerja.
Siap meningkatkan alur kerja dokumen Anda? Mari kita mulai!
## Prasyarat
Sebelum memulai, pastikan Anda memiliki hal berikut:
### Perpustakaan yang Diperlukan
- **GroupDocs.Signature untuk .NET**:Pustaka ini memungkinkan Anda menandatangani berbagai jenis dokumen menggunakan berbagai format kode batang dan kode QR.
### Persyaratan Pengaturan Lingkungan
- Bekerja dengan lingkungan .NET yang kompatibel (sebaiknya .NET Core atau .NET Framework 4.7.2+).
- Instal Visual Studio jika Anda bekerja pada aplikasi desktop.
### Prasyarat Pengetahuan
- Pemahaman dasar tentang pengembangan C# dan .NET.
- Kemampuan menggunakan paket NuGet untuk manajemen ketergantungan.
## Menyiapkan GroupDocs.Signature untuk .NET
Untuk memulai, instal pustaka GroupDocs.Signature:
**Menggunakan .NET CLI**
```bash
dotnet add package GroupDocs.Signature
```
**Konsol Manajer Paket**
```powershell
Install-Package GroupDocs.Signature
```
**Antarmuka Pengguna Pengelola Paket NuGet**: 
Cari "GroupDocs.Signature" dan instal versi terbaru.
### Langkah-Langkah Perolehan Lisensi
- **Uji Coba Gratis**: Unduh uji coba untuk menguji fitur.
- **Lisensi Sementara**:Minta lisensi sementara untuk evaluasi lanjutan.
- **Pembelian**:Beli lisensi penuh jika Anda siap untuk menerapkannya dalam produksi.
#### Inisialisasi Dasar
Untuk menginisialisasi GroupDocs.Signature, buatlah sebuah instance dari `Signature` kelas dengan jalur dokumen Anda:
```csharp
using (Signature signature = new Signature("your-document-path"))
{
    // Kode penandatanganan Anda di sini
}
```
## Panduan Implementasi
Mari kita uraikan cara menerapkan setiap fitur langkah demi langkah.
### Tandatangani Dokumen dengan Kode Batang GS1DotCode
**Ringkasan**:Tambahkan kode batang GS1DotCode ke dokumen Anda, pilihan populer untuk manajemen rantai pasokan dan inventaris.
#### Langkah 1: Inisialisasi Objek Tanda Tangan
Buat contoh dari `Signature` menggunakan jalur file sumber:
```csharp
using (Signature signature = new Signature("YOUR_DOCUMENT_DIRECTORY"))
{
    // Kode berlanjut...
}
```
#### Langkah 2: Konfigurasikan Opsi GS1DotCode
Siapkan pilihan kode batang Anda, termasuk konten, format, dan dimensi.
```csharp
var gs1DotCodeOptions = new BarcodeSignOptions(
    "(01)04912345123459(15)970331(30)128(10)ABC123", 
    BarcodeTypes.GS1DotCode)
{
    Left = 1,
    Top = 1,
    Height = 150,
    Width = 200,
    ReturnContent = true, // Ambil konten gambar yang ditandatangani
    ReturnContentType = FileType.PNG // Keluaran sebagai PNG
};
```
#### Langkah 3: Tandatangani dan Simpan Dokumen
Jalankan proses penandatanganan dan simpan hasilnya ke jalur yang ditentukan.
```csharp
var signResult = signature.Sign("YOUR_OUTPUT_DIRECTORY/AdvancedBarCodeTypes.pptx", gs1DotCodeOptions);
```
### Tandatangani Dokumen dengan Kode QR HanXin
**Ringkasan**: Sematkan kode QR HanXin di dokumen Anda, banyak digunakan untuk berbagi data yang aman.
#### Langkah 1: Inisialisasi Objek Tanda Tangan
Mirip dengan pengaturan kode batang, inisialisasi `Signature`:
```csharp
using (Signature signature = new Signature("YOUR_DOCUMENT_DIRECTORY"))
{
    // Kode berlanjut...
}
```
#### Langkah 2: Konfigurasikan Opsi QR HanXin
Tentukan pilihan kode QR Anda dengan pengaturan konten dan tampilan.
```csharp
var hanXinOptions = new QrCodeSignOptions(
    "(01)04912345123459(15)970331(30)128(10)ABC123", 
    QrCodeTypes.HanXin)
{
    Left = 201,
    Top = 1,
    Height = 200,
    Width = 200,
    ReturnContent = true, // Ambil konten gambar yang ditandatangani
    ReturnContentType = FileType.PNG // Keluaran sebagai PNG
};
```
#### Langkah 3: Tandatangani dan Simpan Dokumen
Lanjutkan dengan menandatangani dan menyimpan dokumen Anda.
```csharp
var signResult = signature.Sign("YOUR_OUTPUT_DIRECTORY/AdvancedQRCodeTypes.pptx", hanXinOptions);
```
### Daftar Tanda Tangan yang Baru Dibuat
**Ringkasan**:Verifikasi tanda tangan yang ditambahkan dengan mencantumkannya setelah penandatanganan.
#### Langkah-langkah Implementasi:
1. **Inisialisasi Objek Tanda Tangan**:Sama seperti fitur sebelumnya.
2. **Daftar dan Keluaran Tanda Tangan**: Gunakan metode untuk mengulang item yang ditandatangani.
```csharp
void ListNewSignatures(SignResult signResult)
{
    Console.WriteLine("\nList of newly created signatures:");
    int number = 1;
    foreach (var item in signResult.Succeeded)
    {
        switch (item)
        {
            case BarcodeSignature barcodeSignature:
                string barOutputImagePath = Path.Combine("YOUR_OUTPUT_DIRECTORY", $"image{number}{barcodeSignature.Format.Extension}");
                using (FileStream fs = new FileStream(barOutputImagePath, FileMode.Create))
                {
                    fs.Write(barcodeSignature.Content, 0, barcodeSignature.Content.Length);
                }
                number++;
                break;
            case QrCodeSignature qrCodeSignature:
                string qrOutputImagePath = Path.Combine("YOUR_OUTPUT_DIRECTORY", $"image{number}{qrCodeSignature.Format.Extension}");
                using (FileStream fs = new FileStream(qrOutputImagePath, FileMode.Create))
                {
                    fs.Write(qrCodeSignature.Content, 0, qrCodeSignature.Content.Length);
                }
                number++;
                break;
        }
    }
}
```
## Aplikasi Praktis
- **Manajemen Rantai Pasokan**:Gunakan GS1DotCode untuk melacak produk dari produksi hingga eceran.
- **Berbagi Data Aman**Terapkan kode QR HanXin untuk berbagi informasi terenkripsi dalam dokumen bisnis.
- **Pemrosesan Faktur Otomatis**: Sederhanakan proses verifikasi dan persetujuan faktur menggunakan kode batang.
## Pertimbangan Kinerja
Saat bekerja dengan GroupDocs.Signature, pertimbangkan kiat berikut:
- **Optimalkan Penggunaan Sumber Daya**: Tutup aliran dan lepaskan sumber daya segera untuk menghindari kebocoran memori.
- **Pemrosesan Paralel**: Gunakan metode asinkron atau pemrosesan paralel jika memungkinkan untuk kinerja yang lebih baik.
- **Manajemen Memori**:Profilkan aplikasi Anda secara berkala untuk memastikan penggunaan pengumpul sampah .NET yang efisien.
## Kesimpulan
Dalam tutorial ini, Anda telah mempelajari cara mengimplementasikan kode batang GS1DotCode dan kode QR HanXin menggunakan GroupDocs.Signature untuk .NET. Alat-alat ini dapat meningkatkan keamanan dan efisiensi alur kerja dokumen Anda secara signifikan.
### Langkah Selanjutnya
- Bereksperimenlah dengan berbagai jenis kode batang yang ditawarkan oleh GroupDocs.Signature.
- Jelajahi integrasi dengan sistem lain seperti solusi CRM atau ERP.
Siap mulai menandatangani dokumen di aplikasi Anda? Coba terapkan fitur-fitur ini hari ini!
## Bagian FAQ
1. **Apa itu GroupDocs.Signature untuk .NET?**
   - Pustaka yang mengaktifkan fungsionalitas tanda tangan digital dalam aplikasi .NET, mendukung berbagai format dokumen dan jenis tanda tangan.
2. **Bisakah saya menggunakan format kode batang lain dengan GroupDocs.Signature?**
   - Ya, ia mendukung beberapa standar kode batang termasuk kode QR, Kode 128, PDF417, dll.
3. **Bagaimana cara menangani kesalahan selama proses penandatanganan?**
   - Terapkan penanganan pengecualian di sekitar Anda `Sign` pemanggilan metode untuk mengelola potensi kesalahan dengan baik.
4. **Apakah ada dampak kinerja saat menambahkan kode batang ke dokumen besar?**
   - Meskipun penambahan kode batang umumnya efisien, kinerjanya dapat bervariasi berdasarkan ukuran dan kompleksitas dokumen.