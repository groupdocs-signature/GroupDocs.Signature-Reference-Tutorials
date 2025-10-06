---
"date": "2025-05-07"
"description": "Tìm hiểu cách sử dụng GroupDocs.Signature cho .NET để trích xuất thông tin tài liệu chi tiết, bao gồm chữ ký, siêu dữ liệu, v.v. Hướng dẫn này bao gồm thiết lập, triển khai và các phương pháp hay nhất."
"title": "Master GroupDocs.Signature cho .NET - Trích xuất và hiển thị thông tin tài liệu hiệu quả"
"url": "/vi/net/preview-info/groupdocs-signature-net-document-info-extraction/"
"weight": 1
type: docs
---
# Làm chủ GroupDocs.Signature cho .NET: Trích xuất và hiển thị thông tin tài liệu hiệu quả

## Giới thiệu

Bạn đang tìm cách trích xuất thông tin chi tiết toàn diện từ các tài liệu trong ứng dụng của mình một cách hiệu quả? Cho dù đó là quản lý hợp đồng, thỏa thuận hay tệp PDF nhiều trang, một giải pháp mạnh mẽ là điều cần thiết. **GroupDocs.Signature cho .NET** cung cấp các tính năng mạnh mẽ được thiết kế để hợp lý hóa việc phân tích tài liệu bằng cách truy xuất và hiển thị các thành phần như trường biểu mẫu, chữ ký, siêu dữ liệu, v.v. Hướng dẫn này sẽ hướng dẫn bạn cách sử dụng các tính năng này để nâng cao chức năng của ứng dụng.

**Những gì bạn sẽ học:**
- Cách lấy thông tin chi tiết về tài liệu bằng GroupDocs.Signature cho .NET
- Hiển thị nhiều loại chữ ký và thông tin chi tiết về trường biểu mẫu
- Trích xuất siêu dữ liệu và các thuộc tính cụ thể của trang

Chúng ta hãy cùng xem lại các điều kiện tiên quyết trước khi bắt đầu triển khai.

## Điều kiện tiên quyết

Trước khi sử dụng GroupDocs.Signature cho .NET, hãy đảm bảo môi trường của bạn được thiết lập chính xác. Hướng dẫn này yêu cầu bạn đã quen thuộc với C# và có kiến thức cơ bản về các khái niệm xử lý tài liệu.

### Thư viện và phụ thuộc bắt buộc
- **GroupDocs.Signature cho .NET**: Thư viện chính mà chúng ta sẽ sử dụng.
- **.NET Framework hoặc .NET Core**: Tùy thuộc vào thiết lập dự án của bạn.

### Thiết lập môi trường
Đảm bảo bạn có sẵn môi trường phát triển với Visual Studio hoặc IDE phù hợp khác hỗ trợ các dự án .NET.

### Điều kiện tiên quyết về kiến thức
- Hiểu biết cơ bản về lập trình C#.
- Làm quen với các loại tài liệu (PDF, Word, Excel) và các thuộc tính của chúng.

## Thiết lập GroupDocs.Signature cho .NET

Để sử dụng GroupDocs.Signature cho .NET, bạn cần cài đặt thư viện. Dưới đây là một số phương pháp:

### Hướng dẫn cài đặt

**Sử dụng .NET CLI:**
```bash
dotnet add package GroupDocs.Signature
```

**Sử dụng Bảng điều khiển Trình quản lý gói:**
```powershell
Install-Package GroupDocs.Signature
```

**Giao diện người dùng của Trình quản lý gói NuGet:**
Tìm kiếm "GroupDocs.Signature" trong Trình quản lý gói NuGet và cài đặt phiên bản mới nhất.

### Mua lại giấy phép
Để tận dụng tối đa GroupDocs.Signature, hãy cân nhắc mua giấy phép:
- **Dùng thử miễn phí**: Bắt đầu bằng bản dùng thử miễn phí để khám phá các tính năng.
- **Giấy phép tạm thời**: Xin giấy phép tạm thời để thử nghiệm kéo dài.
- **Mua**: Mua giấy phép đầy đủ để sử dụng cho mục đích sản xuất.

Sau khi cài đặt và cấp phép, hãy khởi tạo dự án của bạn bằng cách thiết lập môi trường GroupDocs.Signature như hiển thị bên dưới:

```csharp
using System;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;

public class GetDocumentInfoFeature
{
    public static void Run()
    {
        // Xác định đường dẫn tệp cho tài liệu bạn muốn phân tích
        string filePath = "YOUR_DOCUMENT_DIRECTORY\Sample_Signed_Multi_Document.pdf";  // Thay thế bằng đường dẫn tài liệu thực tế của bạn
        
        SignatureSettings signatureSettings = new SignatureSettings
        {
            IncludeStandardMetadataSignatures = true
        };

        using (Signature signature = new Signature(filePath, signatureSettings))
        {
            IDocumentInfo documentInfo = signature.GetDocumentInfo();
            // Các hoạt động tiếp theo sẽ được thực hiện ở đây...
        }
    }
}
```

## Hướng dẫn thực hiện

Sau khi thiết lập xong, chúng ta hãy khám phá cách triển khai nhiều tính năng khác nhau của GroupDocs.Signature cho .NET.

### Truy xuất và hiển thị các thuộc tính cơ bản của tài liệu

**Tổng quan**: Trích xuất các thuộc tính cần thiết như định dạng tệp, kích thước và số trang.

#### Triển khai từng bước:
1. **Khởi tạo đối tượng chữ ký**: Tạo một phiên bản của `Signature` lớp với đường dẫn tài liệu của bạn.
2. **Phương thức GetDocumentInfo**: Sử dụng `GetDocumentInfo()` phương pháp để lấy thông tin chi tiết về tài liệu.
3. **Hiển thị Thuộc tính Tài liệu**: Xuất ra các thuộc tính cơ bản như định dạng, phần mở rộng và kích thước bằng cách sử dụng `Console.WriteLine` cho mục đích gỡ lỗi hoặc ghi nhật ký.

```csharp
IDocumentInfo documentInfo = signature.GetDocumentInfo();
Console.WriteLine($"Document properties {Path.GetFileName(filePath)}:");
Console.WriteLine($" - format : {documentInfo.FileType.FileFormat}");
Console.WriteLine($" - extension : {documentInfo.FileType.Extension}");
Console.WriteLine($" - size : {documentInfo.Size}");
Console.WriteLine($" - page count : {documentInfo.PageCount}");
```

### Hiển thị thông tin về từng trang tài liệu

**Tổng quan**: Tìm hiểu sâu hơn bằng cách truy xuất và hiển thị thông tin về từng trang trong tài liệu.

#### Triển khai từng bước:
1. **Lặp lại qua các trang**: Lặp lại `documentInfo.Pages` để truy cập vào thông tin chi tiết của từng trang như chiều rộng và chiều cao.

```csharp
foreach (PageInfo pageInfo in documentInfo.Pages)
{
    Console.WriteLine($" - page-{pageInfo.PageNumber} Width {pageInfo.Width}, Height {pageInfo.Height}");
}
```

### Hiển thị thông tin chữ ký trường biểu mẫu

**Tổng quan**: Trích xuất và hiển thị thông tin liên quan đến các trường biểu mẫu trong tài liệu.

#### Triển khai từng bước:
1. **Truy cập các trường biểu mẫu**: Sử dụng `documentInfo.FormFields` để lấy lại tất cả chữ ký trường biểu mẫu có trong tài liệu.
2. **Hiển thị chi tiết từng trường biểu mẫu**: Lặp lại từng trường biểu mẫu và đưa ra loại, tên và giá trị của trường đó.

```csharp
Console.WriteLine($"Document Form Fields information: count = {documentInfo.FormFields.Count}");
foreach (FormFieldSignature formField in documentInfo.FormFields)
{
    Console.WriteLine($" - type #{formField.Type}: Name: {formField.Name} Value: {formField.Value}");
}
```

### Hiển thị thông tin chữ ký khác nhau

**Tổng quan**: Truy xuất và hiển thị thông tin cho văn bản, hình ảnh, kỹ thuật số, mã vạch, mã QR, trường biểu mẫu và chữ ký siêu dữ liệu.

#### Các bước thực hiện:
- **Chữ ký văn bản**: Truy cập `documentInfo.TextSignatures` để biết thông tin chi tiết về từng chữ ký văn bản bao gồm ID, vị trí, kích thước và ngày tạo.

```csharp
Console.WriteLine($"Document Text signatures: {documentInfo.TextSignatures.Count}");
foreach (TextSignature textSignature in documentInfo.TextSignatures)
{
    Console.WriteLine($" - #{textSignature.SignatureId}: Text: {textSignature.Text} Location: {textSignature.Left}x{textSignature.Top}. Size: {textSignature.Width}x{textSignature.Height}. CreatedOn/ModifiedOn: {textSignature.CreatedOn.ToShortDateString()} / {textSignature.ModifiedOn.ToShortDateString()}");
}
```

- **Chữ ký hình ảnh**: Tương tự như chữ ký văn bản, sử dụng `documentInfo.ImageSignatures` để biết thông tin chi tiết như kích thước và định dạng của chữ ký hình ảnh.

```csharp
Console.WriteLine($"Document Image signatures: {documentInfo.ImageSignatures.Count}");
foreach (ImageSignature imageSignature in documentInfo.ImageSignatures)
{
    Console.WriteLine($" - #{imageSignature.SignatureId}: Size: {imageSignature.Size} bytes, Format: {imageSignature.Format}. CreatedOn/ModifiedOn: {imageSignature.CreatedOn.ToShortDateString()} / {imageSignature.ModifiedOn.ToShortDateString()}");
}
```

- **Chữ ký số**: Đối với chữ ký số, hãy sử dụng `documentInfo.DigitalSignatures` để trích xuất ID chữ ký và dấu thời gian.

```csharp
Console.WriteLine($"Document Digital signatures: {documentInfo.DigitalSignatures.Count}");
foreach (DigitalSignature digitalSignature in documentInfo.DigitalSignatures)
{
    Console.WriteLine($" - #{digitalSignature.SignatureId}. CreatedOn/ModifiedOn: {digitalSignature.CreatedOn.ToShortDateString()} / {digitalSignature.ModifiedOn.ToShortDateString()}");
}
```

- **Chữ ký mã vạch và mã QR**: Sử dụng `documentInfo.BarcodeSignatures` Và `documentInfo.QrCodeSignatures` để thu thập thông tin chi tiết về mã vạch và mã QR.

```csharp
Console.WriteLine($"Document Barcode signatures: {documentInfo.BarcodeSignatures.Count}");
foreach (BarcodeSignature barcodeSignature in documentInfo.BarcodeSignatures)
{
    Console.WriteLine($" - #{barcodeSignature.SignatureId}: Type: {barcodeSignature.EncodeType?.TypeName}. Text: {barcodeSignature.Text}");
}

Console.WriteLine($"Document QR Code signatures: {documentInfo.QrCodeSignatures.Count}");
foreach (QrCodeSignature qrCodeSignature in documentInfo.QrCodeSignatures)
{
    Console.WriteLine($" - #{qrCodeSignature.SignatureId}: Type: {qrCodeSignature.EncodeType?.TypeName}. Text: {qrCodeSignature.Text}");
}
```

### Phần kết luận

Bằng cách làm theo hướng dẫn này, bạn đã học cách tận dụng GroupDocs.Signature cho .NET để trích xuất và hiển thị thông tin tài liệu toàn diện một cách hiệu quả. Bộ kỹ năng này sẽ nâng cao khả năng quản lý tài liệu của ứng dụng một cách chính xác và dễ dàng.

**Các bước tiếp theo:**
- Khám phá các tính năng bổ sung của GroupDocs.Signature.
- Triển khai xác thực chữ ký trong ứng dụng của bạn.
- Tích hợp chức năng này vào quy trình làm việc lớn hơn để xử lý tài liệu tự động.