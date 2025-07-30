---
"date": "2025-05-07"
"description": "Tìm hiểu cách ký tài liệu PDF bằng Mã QR HIBC bằng GroupDocs.Signature cho .NET. Hướng dẫn này bao gồm các mã LIC và PAS, bao gồm Mã QR, Mã Aztec và DataMatrix."
"title": "Cách ký tài liệu bằng mã QR HIBC bằng GroupDocs.Signature cho .NET - Hướng dẫn toàn diện"
"url": "/vi/net/qr-code-signatures/sign-documents-hibc-qr-groupdocs-dotnet/"
"weight": 1
---

# Cách ký tài liệu bằng mã QR HIBC bằng GroupDocs.Signature cho .NET

## Giới thiệu

Trong môi trường kinh doanh năng động ngày nay, việc đảm bảo tính xác thực và toàn vẹn của tài liệu là vô cùng quan trọng. Cho dù bạn đang xử lý dược phẩm, sản phẩm chăm sóc sức khỏe hay hậu cần, việc có một phương pháp ký và theo dõi tài liệu an toàn có thể giúp tiết kiệm thời gian và ngăn ngừa sai sót. Nhập **GroupDocs.Signature cho .NET**, một thư viện mạnh mẽ được thiết kế để hợp lý hóa quy trình quản lý tài liệu bằng cách cho phép tích hợp liền mạch Mã QR HIBC vào tài liệu của bạn.

Trong hướng dẫn này, chúng ta sẽ khám phá cách tận dụng GroupDocs.Signature cho .NET để ký tài liệu PDF với nhiều loại mã QR HIBC khác nhau—LIC (Giấy phép) và PAS (Hệ thống Xác thực Sản phẩm)—bao gồm Mã QR, Mã Aztec và DataMatrix. Cuối cùng, bạn sẽ có kiến thức vững chắc về việc triển khai các giải pháp này trong các ứng dụng .NET của mình.

**Những gì bạn sẽ học:**
- Cách thiết lập GroupDocs.Signature cho .NET
- Triển khai Mã QR HIBC LIC, Mã Aztec và DataMatrix
- Thêm mã QR HIBC PAS, mã Aztec và DataMatrix
- Các trường hợp sử dụng thực tế và khả năng tích hợp

Hãy cùng tìm hiểu các điều kiện tiên quyết trước khi bắt đầu triển khai các tính năng này.

## Điều kiện tiên quyết

Trước khi bắt đầu viết mã, hãy đảm bảo bạn đã chuẩn bị những điều sau:

- **Môi trường .NET**: Đảm bảo rằng bạn đã cài đặt .NET trên hệ thống của mình (tốt nhất là .NET Core hoặc .NET 5/6+).
- **GroupDocs.Signature cho .NET**: Thư viện này sẽ là công cụ chính của chúng ta. Bạn có thể cài đặt nó thông qua NuGet.
- **Kiến thức lập trình cơ bản**: Khuyến khích sử dụng C# và xử lý tệp trong .NET.

### Thư viện bắt buộc

Để sử dụng GroupDocs.Signature cho .NET, bạn cần thêm gói bằng một trong các phương pháp sau:

**.NET CLI**
```bash
dotnet add package GroupDocs.Signature
```

**Trình quản lý gói**
```powershell
Install-Package GroupDocs.Signature
```

**Giao diện người dùng Trình quản lý gói NuGet**
Tìm kiếm "GroupDocs.Signature" và cài đặt phiên bản mới nhất.

### Mua lại giấy phép

Để dùng thử, bạn có thể mua bản quyền dùng thử miễn phí. Để sử dụng lâu dài, hãy cân nhắc mua gói đăng ký hoặc yêu cầu bản quyền tạm thời:

- **Dùng thử miễn phí**: Truy cập [đây](https://releases.groupdocs.com/signature/net/)
- **Giấy phép tạm thời**: Yêu cầu tại [liên kết này](https://purchase.groupdocs.com/temporary-license/)

### Thiết lập môi trường

Thiết lập môi trường của bạn bằng cách đảm bảo dự án của bạn nhắm đến phiên bản .NET phù hợp và có quyền truy cập vào GroupDocs.Signature. Khởi tạo nó trong ứng dụng của bạn như sau:

```csharp
using GroupDocs.Signature;
```

## Thiết lập GroupDocs.Signature cho .NET

Để bắt đầu sử dụng GroupDocs.Signature cho .NET, bạn cần cài đặt thư viện và cấu hình thiết lập cơ bản trong dự án của mình.

### Cài đặt

Hãy làm theo một trong các phương pháp được đề cập ở trên để thêm GroupDocs.Signature vào dự án của bạn. Sau khi cài đặt, hãy đảm bảo dự án của bạn được cấu hình để sử dụng GroupDocs.Signature bằng cách tham chiếu đến nó trong các tệp mã.

### Khởi tạo giấy phép

Sau khi có được giấy phép, hãy khởi tạo giấy phép như sau:

```csharp
SignatureConfig signConfig = new SignatureConfig();
signConfig.LicensePath = "path/to/your/license.lic";
Signature signature = new Signature("Sample.pdf", signConfig);
```

Thiết lập này sẽ cho phép bạn truy cập tất cả các tính năng của GroupDocs.Signature mà không bị giới hạn.

## Hướng dẫn thực hiện

Bây giờ, chúng ta hãy cùng tìm hiểu cách triển khai từng tính năng bằng Mã QR HIBC với GroupDocs.Signature cho .NET.

### Ký tài liệu bằng mã QR HIBC LIC

#### Tổng quan

Việc ký tài liệu bằng Mã QR HIBC LIC đảm bảo tính tuân thủ và khả năng truy xuất nguồn gốc trong các trường hợp cấp phép. Phần này sẽ hướng dẫn bạn cách tạo và nhúng mã QR vào tài liệu PDF của mình.

#### Các bước thực hiện

##### Bước 1: Cấu hình Đường dẫn Nguồn và Đường dẫn Đầu ra

Xác định vị trí của tài liệu nguồn và nơi lưu đầu ra đã ký:

```csharp
string sourceFilePath = Path.Combine("YOUR_DOCUMENT_DIRECTORY", "Sample.pdf");
string outputPath = Path.Combine("YOUR_OUTPUT_DIRECTORY", "SignWithHIBCLICQR");
string destinFilePath = Path.Combine(outputPath, "SignedDocumentWithHIBCLICQR.pdf");
```

##### Bước 2: Tạo tùy chọn ký hiệu mã QR

Cấu hình mã QR của bạn với văn bản và cài đặt cụ thể:

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

    // Ký tài liệu bằng những tùy chọn này.
    signature.Sign(destinFilePath, hibcLic_QR_Options);
}
```

**Giải thích**: 
- `QrCodeSignOptions` Thiết lập giao diện và nội dung của mã QR. Ở đây, chúng tôi chỉ định loại Mã QR HIBC LIC và đặt nó trên tài liệu.
- `ReturnContent` đặt thành true cho phép bạn lấy lại hình ảnh đã hiển thị của tài liệu đã ký.

#### Mẹo khắc phục sự cố

- Đảm bảo đường dẫn tài liệu được chỉ định chính xác.
- Xác minh rằng GroupDocs.Signature được cấp phép đầy đủ chức năng.

### Ký tài liệu bằng mã HIBC LIC Aztec

#### Tổng quan

Mã Aztec cung cấp một hình thức mã hóa khác, phù hợp cho việc lưu trữ thông tin mật độ cao. Phần này tập trung vào việc nhúng mã Aztec vào tài liệu của bạn bằng GroupDocs.Signature.

#### Các bước thực hiện

##### Bước 1: Cấu hình Đường dẫn

Tương tự như tính năng trước, hãy xác định đường dẫn tệp của bạn:

```csharp
string sourceFilePath = Path.Combine("YOUR_DOCUMENT_DIRECTORY", "Sample.pdf");
string outputPath = Path.Combine("YOUR_OUTPUT_DIRECTORY", "SignWithHIBCLICAztec");
string destinFilePath = Path.Combine(outputPath, "SignedDocumentWithHIBCLICAztec.pdf");
```

##### Bước 2: Cấu hình tùy chọn Aztec Code

Thiết lập mã Aztec của bạn bằng GroupDocs.Signature:

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

**Giải thích**: 
- Các `QrCodeSignOptions` được sử dụng lại ở đây nhưng với kiểu mã Aztec.
- Định vị (`Top`, `Left`) và cài đặt truy xuất nội dung tương tự như mã QR.

#### Mẹo khắc phục sự cố

- Xác nhận đường dẫn tệp là chính xác.
- Đảm bảo phiên bản GroupDocs.Signature hỗ trợ các loại Mã Aztec.

### Ký tài liệu bằng HIBC LIC DataMatrix

#### Tổng quan

Mã DataMatrix cung cấp một phương pháp mạnh mẽ khác để lưu trữ dữ liệu. Phần này trình bày cách tích hợp DataMatrix vào tài liệu PDF của bạn.

#### Các bước thực hiện

##### Bước 1: Thiết lập đường dẫn tệp

Như trước đây, hãy xác định vị trí lưu trữ các tệp của bạn:

```csharp
string sourceFilePath = Path.Combine("YOUR_DOCUMENT_DIRECTORY", "Sample.pdf");
string outputPath = Path.Combine("YOUR_OUTPUT_DIRECTORY", "SignWithHIBCLICDataMatrix");
string destinFilePath = Path.Combine(outputPath, "SignedDocumentWithHIBCLICDataMatrix.pdf");
```

##### Bước 2: Tạo tùy chọn ký hiệu DataMatrix

Cấu hình và áp dụng mã DataMatrix:

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

**Giải thích**: 
- `QrCodeSignOptions` được sử dụng để thiết lập giao diện và nội dung của mã DataMatrix.
- Định vị (`Top`, `Left`) và cài đặt truy xuất tuân theo cùng một mẫu như các mã trước đó.

#### Mẹo khắc phục sự cố

- Đảm bảo tất cả đường dẫn tệp được chỉ định chính xác.
- Xác minh rằng GroupDocs.Signature hỗ trợ các loại Mã DataMatrix trong phiên bản của bạn.

### Ký tài liệu bằng mã QR HIBC PAS

#### Tổng quan

Việc ký tài liệu bằng Mã QR PAS HIBC giúp tăng cường khả năng theo dõi và truy xuất nguồn gốc sản phẩm. Phần này hướng dẫn bạn cách nhúng mã QR PAS vào tệp PDF bằng GroupDocs.Signature.

#### Các bước thực hiện

##### Bước 1: Cấu hình Đường dẫn Nguồn và Đường dẫn Đầu ra

Xác định vị trí của tài liệu nguồn và nơi lưu đầu ra đã ký:

```csharp
string sourceFilePath = Path.Combine("YOUR_DOCUMENT_DIRECTORY", "Sample.pdf");
string outputPath = Path.Combine("YOUR_OUTPUT_DIRECTORY", "SignWithHIBCPASQR");
string destinFilePath = Path.Combine(outputPath, "SignedDocumentWithHIBCPASQR.pdf");
```

##### Bước 2: Tạo tùy chọn ký hiệu mã QR

Cấu hình mã QR PAS của bạn với văn bản và cài đặt cụ thể:

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

    // Ký tài liệu bằng những tùy chọn này.
    signature.Sign(destinFilePath, hibcPas_QR_Options);
}
```

**Giải thích**: 
- `QrCodeSignOptions` được cấu hình cho loại Mã QR HIBC PAS và được định vị trên tài liệu.
- `ReturnContent` đặt thành true để lấy hình ảnh đã hiển thị của tài liệu đã ký.

#### Mẹo khắc phục sự cố

- Đảm bảo tất cả các đường dẫn được chỉ định chính xác.
- Xác minh rằng GroupDocs.Signature hỗ trợ loại Mã QR PAS trong phiên bản của bạn.

### Phần kết luận

Bằng cách làm theo hướng dẫn này, bạn có thể tích hợp hiệu quả Mã QR HIBC LIC và PAS vào tài liệu PDF bằng GroupDocs.Signature cho .NET. Quy trình này giúp tăng cường bảo mật tài liệu, khả năng truy xuất nguồn gốc và tính tuân thủ trong nhiều ngành khác nhau. Để biết thêm tùy chỉnh và các tính năng nâng cao, vui lòng tham khảo [Tài liệu GroupDocs](https://docs.groupdocs.com/signature/net/).