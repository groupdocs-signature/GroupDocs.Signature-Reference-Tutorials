---
"date": "2025-05-07"
"description": "Tìm hiểu cách ký hình ảnh DICOM bằng mã QR bằng GroupDocs.Signature cho .NET. Hướng dẫn này bao gồm thiết lập, triển khai và xác minh chữ ký mã QR trong hình ảnh y tế."
"title": "Cách ký hình ảnh DICOM bằng mã QR sử dụng GroupDocs.Signature cho .NET - Hướng dẫn toàn diện"
"url": "/vi/net/qr-code-signatures/groupdocs-signature-net-dicom-images-qr-codes/"
"weight": 1
---

# Cách ký hình ảnh DICOM bằng mã QR bằng GroupDocs.Signature cho .NET: Hướng dẫn toàn diện

Bạn đang tìm kiếm một phương pháp an toàn để xác thực tệp DICOM của mình? Hướng dẫn chi tiết này sẽ chỉ cho bạn cách sử dụng GroupDocs.Signature cho .NET để tích hợp chữ ký mã QR vào hình ảnh DICOM. Lý tưởng cho các chuyên gia chăm sóc sức khỏe, nhà phát triển và bất kỳ ai làm việc với tài liệu y tế kỹ thuật số, hướng dẫn này bao gồm từ thiết lập đến triển khai.

## Những gì bạn sẽ học:
- Thiết lập môi trường phát triển của bạn với GroupDocs.Signature cho .NET.
- Hướng dẫn từng bước về cách ký hình ảnh DICOM bằng mã QR.
- Phương pháp xác minh và tìm kiếm chữ ký mã QR trong tệp DICOM.
- Các kỹ thuật tạo bản xem trước của tài liệu đã ký để xem xét.
- Các biện pháp tốt nhất để tối ưu hóa hiệu suất và quản lý tài nguyên hiệu quả.

Chúng ta hãy bắt đầu với các điều kiện tiên quyết!

## Điều kiện tiên quyết

Để sử dụng GroupDocs.Signature cho .NET, hãy đảm bảo môi trường của bạn đã sẵn sàng. Dưới đây là những gì bạn cần:

### Thư viện và phiên bản bắt buộc
- **GroupDocs.Signature cho .NET**Đảm bảo khả năng tương thích với .NET framework của bạn.

### Yêu cầu thiết lập môi trường
- Môi trường phát triển trên Windows hoặc Linux.
- Đã cài đặt Visual Studio hoặc IDE tương thích với .NET khác.

### Điều kiện tiên quyết về kiến thức
- Hiểu biết cơ bản về lập trình C#.
- Quen thuộc với tệp I/O trong các ứng dụng .NET.

## Thiết lập GroupDocs.Signature cho .NET

Cài đặt thư viện GroupDocs.Signature bằng phương pháp bạn thích:

**Sử dụng .NET CLI:**
```bash
dotnet add package GroupDocs.Signature
```

**Trình quản lý gói:**
```powershell
Install-Package GroupDocs.Signature
```

**Giao diện người dùng của Trình quản lý gói NuGet:**
- Tìm kiếm "GroupDocs.Signature" và cài đặt phiên bản mới nhất.

### Mua lại giấy phép

Bắt đầu với bản dùng thử miễn phí để khám phá các tính năng. Để sử dụng lâu dài, hãy cân nhắc mua giấy phép tạm thời hoặc đầy đủ từ [GroupDocs](https://purchase.groupdocs.com/buy).

Sau khi cài đặt, hãy khởi tạo thư viện:

```csharp
using GroupDocs.Signature;
// Khởi tạo đối tượng Chữ ký với đường dẫn tệp DICOM của bạn.
Signature signature = new Signature("YOUR_DOCUMENT_DIRECTORY\\sample.dicom");
```

## Hướng dẫn thực hiện

### Ký hình ảnh DICOM bằng mã QR

#### Tổng quan
Thêm chữ ký mã QR để đảm bảo tính xác thực và khả năng truy xuất nguồn gốc của tài liệu y tế.

**Bước 1: Khởi tạo đối tượng chữ ký**

```csharp
string filePath = "YOUR_DOCUMENT_DIRECTORY\\sample.dicom";
using (Signature signature = new Signature(filePath))
{
    // Tiến hành ký kết các hoạt động...
}
```

**Bước 2: Tạo tùy chọn ký hiệu mã QR**

Cấu hình các thuộc tính như văn bản, kích thước và căn chỉnh.

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

**Bước 3: Thêm siêu dữ liệu XMP**

Cải thiện tài liệu bằng siêu dữ liệu bổ sung.

```csharp
DicomSaveOptions dicomSaveOptions = new DicomSaveOptions()
{
    XmpEntries = new List<DicomXmpEntry>() { new DicomXmpEntry(DicomXmpType.PatientName, "Patient #4") }
};
```

**Bước 4: Ký vào tài liệu**

Thực hiện ký và lưu.

```csharp
SignResult signResult = signature.Sign("YOUR_OUTPUT_DIRECTORY\\SignedDicom", options, dicomSaveOptions);
```

### Nhận thông tin tài liệu

Truy xuất siêu dữ liệu từ các tệp DICOM đã ký để đảm bảo tính toàn vẹn của dữ liệu.

**Tổng quan:**
Truy cập thông tin tài liệu và chữ ký siêu dữ liệu XMP để xác minh.

**Bước 1: Lấy thông tin tài liệu**

```csharp
using (Signature signature = new Signature("YOUR_DOCUMENT_DIRECTORY\\sample_signed.dicom"))
{
    IDocumentInfo signedDocumentInfo = signature.GetDocumentInfo();
}
```

**Bước 2: Lặp lại và in dữ liệu XMP**

Hiển thị chi tiết siêu dữ liệu.

```csharp
foreach (var item in signedDocumentInfo.MetadataSignatures)
{
    Console.WriteLine(item.ToString());
}
```

### Xác minh chữ ký DICOM

Xác thực tính xác thực của chữ ký mã QR trong hình ảnh DICOM.

**Tổng quan:**
Đảm bảo chữ ký chính xác và xác thực.

**Bước 1: Tạo tùy chọn xác minh mã QR**

Đặt tùy chọn phù hợp với văn bản cụ thể trong mã QR.

```csharp
QrCodeVerifyOptions options = new QrCodeVerifyOptions()
{
    AllPages = true,
    Text = "Patient #36363393",
    MatchType = TextMatchType.Contains
};
```

**Bước 2: Xác minh chữ ký**

Kiểm tra xem chữ ký có đáp ứng tiêu chí không.

```csharp
VerificationResult result = signature.Verify(options);

if (result.IsValid)
{
    Console.WriteLine($"DICOM {filePath} has {result.Succeeded.Count} successfully verified signatures!");
}
```

### Tìm kiếm chữ ký trong DICOM

Xác định chữ ký mã QR trong hình ảnh DICOM đã ký.

**Tổng quan:**
Tìm kiếm hiệu quả tất cả chữ ký mã QR để quản lý tính xác thực của tài liệu.

**Bước 1: Tìm kiếm chữ ký mã QR**

```csharp
List<QrCodeSignature> signatures = signature.Search<QrCodeSignature>(SignatureType.QrCode);
```

**Bước 2: Lặp lại và in chi tiết chữ ký**

Xem lại thông tin chi tiết của từng chữ ký được tìm thấy.

```csharp
foreach (var QrCodeSignature in signatures)
{
    Console.WriteLine($"QRCode signature found at page {QrCodeSignature.PageNumber} with type {QrCodeSignature.EncodeType.TypeName} and text {QrCodeSignature.Text}");
}
```

### Tạo bản xem trước của DICOM đã ký

Tạo bản xem trước trực quan để xác minh.

**Tổng quan:**
Tạo bản xem trước hình ảnh để xác minh nội dung mà không cần phần mềm chuyên dụng.

**Bước 1: Xác định phương thức luồng**

Thiết lập phương pháp quản lý luồng tệp trong quá trình tạo bản xem trước.

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

**Bước 2: Tạo bản xem trước**

Thực hiện quá trình tạo bản xem trước.

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

## Ứng dụng thực tế

1. **Quản lý hồ sơ bệnh án**: Xác thực hồ sơ bệnh nhân bằng chữ ký mã QR để tuân thủ.
2. **Kiểm toán theo dõi trong hệ thống chăm sóc sức khỏe**: Theo dõi các thay đổi của tài liệu và xác minh tính xác thực bằng mã QR.
3. **Chia sẻ dữ liệu an toàn**: Đảm bảo chia sẻ hình ảnh y tế an toàn bằng cách nhúng chữ ký số.
4. **Xác minh sự tuân thủ**: Thường xuyên kiểm tra tính toàn vẹn của tệp DICOM để đáp ứng các yêu cầu pháp lý.
5. **Tích hợp với Hệ thống EHR**: Tích hợp liền mạch các tệp DICOM đã ký vào hệ thống Hồ sơ sức khỏe điện tử (EHR) để vận hành hợp lý.