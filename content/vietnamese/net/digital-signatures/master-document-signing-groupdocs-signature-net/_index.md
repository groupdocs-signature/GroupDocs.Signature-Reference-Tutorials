---
"date": "2025-05-07"
"description": "Tìm hiểu cách ký, xác minh, tìm kiếm, cập nhật và xóa chữ ký văn bản trong tài liệu một cách hiệu quả bằng GroupDocs.Signature cho .NET. Đơn giản hóa quy trình ký số của bạn ngay hôm nay."
"title": "Chữ ký và xác minh tài liệu chính với GroupDocs.Signature cho .NET"
"url": "/vi/net/digital-signatures/master-document-signing-groupdocs-signature-net/"
"weight": 1
---

# Chữ ký và xác minh tài liệu chính với GroupDocs.Signature cho .NET

## Cách thành thạo việc ký và xác minh tài liệu với GroupDocs.Signature cho .NET

Trong bối cảnh kỹ thuật số ngày nay, các giải pháp ký kết tài liệu hiệu quả đóng vai trò quan trọng trong việc quản lý hợp đồng, thỏa thuận hoặc bất kỳ tài liệu pháp lý nào. Việc tự động hóa quy trình này giúp tiết kiệm thời gian và giảm thiểu sai sót. **GroupDocs.Signature cho .NET** cung cấp giải pháp mạnh mẽ để hợp lý hóa việc quản lý chữ ký văn bản trong ứng dụng của bạn. Hướng dẫn toàn diện này sẽ hướng dẫn bạn các tính năng của GroupDocs.Signature cho .NET, bao gồm ký, xác minh, tìm kiếm, cập nhật và xóa chữ ký văn bản.

## Những gì bạn sẽ học được

- Cách ký tài liệu bằng chữ ký văn bản có thể tùy chỉnh
- Các kỹ thuật để xác minh hiệu quả các tài liệu đã ký
- Phương pháp tìm kiếm chữ ký văn bản hiện có trong tài liệu
- Các bước để cập nhật và xóa chữ ký văn bản khi cần thiết
- Các phương pháp hay nhất để tối ưu hóa hiệu suất và quản lý bộ nhớ

Chúng ta hãy bắt đầu bằng cách xem xét các điều kiện tiên quyết.

## Điều kiện tiên quyết

Trước khi bắt đầu, hãy đảm bảo rằng môi trường phát triển của bạn được thiết lập với các công cụ cần thiết:

### Thư viện và phụ thuộc bắt buộc

- **GroupDocs.Signature cho .NET**: Thư viện này cho phép bạn thêm chức năng chữ ký vào ứng dụng của mình.
- **.NET Framework 4.6.1 trở lên** (hoặc .NET Core 2.x trở lên)

### Yêu cầu thiết lập môi trường

Bạn sẽ cần một môi trường phát triển C#, chẳng hạn như Visual Studio, và kết nối internet để tải xuống các gói cần thiết.

### Điều kiện tiên quyết về kiến thức

Nên làm quen với các khái niệm lập trình C# cơ bản. Nếu bạn mới làm quen với GroupDocs.Signature cho .NET, đừng lo lắng - hướng dẫn này sẽ hướng dẫn bạn từng bước.

## Thiết lập GroupDocs.Signature cho .NET

Để bắt đầu, bạn cần cài đặt thư viện GroupDocs.Signature vào dự án của mình. Cách thực hiện như sau:

### Cài đặt thông qua .NET CLI
```bash
dotnet add package GroupDocs.Signature
```

### Bảng điều khiển quản lý gói
```powershell
Install-Package GroupDocs.Signature
```

### Giao diện người dùng Trình quản lý gói NuGet
1. Mở dự án của bạn trong Visual Studio.
2. Điều hướng đến **Công cụ** > **Trình quản lý gói NuGet** > **Quản lý các gói NuGet cho giải pháp**.
3. Tìm kiếm "GroupDocs.Signature" và cài đặt phiên bản mới nhất.

#### Các bước xin giấy phép
- **Dùng thử miễn phí**: Bắt đầu với bản dùng thử miễn phí bằng cách tải xuống từ [Dùng thử miễn phí GroupDocs](https://releases.groupdocs.com/signature/net/).
- **Giấy phép tạm thời**: Nhận giấy phép tạm thời để đánh giá đầy đủ các tính năng tại [Giấy phép tạm thời](https://purchase.groupdocs.com/temporary-license/).
- **Mua**: Để tiếp tục sử dụng, hãy mua giấy phép từ [Trang mua hàng của GroupDocs](https://purchase.groupdocs.com/buy).

#### Khởi tạo và thiết lập cơ bản

Sau khi cài đặt, hãy khởi tạo GroupDocs.Signature trong dự án của bạn như sau:

```csharp
using GroupDocs.Signature;

// Khởi tạo phiên bản Signature với đường dẫn tài liệu.
Signature signature = new Signature("path/to/your/document.pdf");
```

Bây giờ bạn đã thiết lập xong, hãy cùng khám phá cách tận dụng GroupDocs.Signature cho nhiều chức năng khác nhau.

## Hướng dẫn thực hiện

### Ký tài liệu bằng chữ ký văn bản

Tính năng này cho phép bạn thêm chữ ký văn bản vào tài liệu. Chúng ta hãy cùng tìm hiểu chi tiết:

#### Tổng quan
Bạn có thể tùy chỉnh giao diện và vị trí chữ ký văn bản của mình bằng nhiều tùy chọn khác nhau như kích thước phông chữ, màu sắc, căn chỉnh, v.v.

#### Triển khai từng bước

**Bước 1**: Xác định đường dẫn tệp và vị trí đầu ra.
```csharp
string filePath = "YOUR_DOCUMENT_DIRECTORY"; // Đường dẫn đến tài liệu gốc
string outputFilePath = Path.Combine("YOUR_OUTPUT_DIRECTORY", "SignedDocument.docx");
```

**Bước 2**: Tạo chữ ký văn bản bằng cách sử dụng `TextSignOptions`.
```csharp
using (Signature signature = new Signature(filePath))
{
    TextSignOptions signOptions = new TextSignOptions("John Smith")
    {
        VerticalAlignment = GroupDocs.Signature.Options.VerticalAlignment.Top,
        HorizontalAlignment = GroupDocs.Signature.Options.HorizontalAlignment.Center,
        Width = 100,
        Height = 40,
        Margin = new Padding(20),
        ForeColor = Color.Red,
        Font = new SignatureFont { Size = 12, FamilyName = "Comic Sans MS" }
    };
```

**Bước 3**: Ký vào tài liệu và xuất kết quả.
```csharp
    SignResult signResult = signature.Sign(outputFilePath, signOptions);
    foreach (BaseSignature temp in signResult.Succeeded)
    {
        Console.WriteLine($"Signed Text Signature: Id:{temp.SignatureId}, Location: {temp.Left}x{temp.Top}. Size: {temp.Width}x{temp.Height}");
    }
}
```

#### Tùy chọn cấu hình chính
- **Căn chỉnh theo chiều dọc và căn chỉnh theo chiều ngang**Kiểm soát vị trí chữ ký xuất hiện trên trang.
- **Phông chữ**: Tùy chỉnh kích thước và kiểu phông chữ cho chữ ký văn bản của bạn.

### Xác minh tài liệu để có chữ ký văn bản

Việc xác minh đảm bảo tài liệu đã được ký đúng như dự định. Sau đây là cách thực hiện:

#### Tổng quan
Xác minh chữ ký văn bản hiện có trong tài liệu của bạn để xác nhận tính xác thực và toàn vẹn của chúng.

#### Triển khai từng bước

**Bước 1**: Chỉ định đường dẫn tệp của tài liệu đã ký.
```csharp
string filePath = "YOUR_OUTPUT_DIRECTORY"; // Đường dẫn đến tài liệu đã ký
```

**Bước 2**: Tạo tùy chọn xác minh bằng cách sử dụng `TextVerifyOptions`.
```csharp
using (Signature signature = new Signature(filePath))
{
    TextVerifyOptions verifyOptions = new TextVerifyOptions()
    {
        AllPages = false,
        PageNumber = 1,
        Text = "John Smith",
        MatchType = GroupDocs.Signature.Options.TextMatchType.Exact
    };
```

**Bước 3**: Xác minh tài liệu.
```csharp
    VerificationResult verifyResult = signature.Verify(verifyOptions);
    if (verifyResult.IsValid)
    {
        Console.WriteLine("Document was verified successfully!");
    }
    else
    {
        Console.WriteLine("Document failed verification process.");
    }
}
```

#### Mẹo khắc phục sự cố
- Đảm bảo `Text` thuộc tính khớp chính xác với nội dung trong tài liệu.
- Kiểm tra xem `PageNumber` tương ứng với trang đúng có chữ ký.

### Tìm kiếm chữ ký văn bản trong tài liệu

Xác định vị trí chữ ký văn bản trong tài liệu của bạn một cách hiệu quả bằng tính năng này.

#### Tổng quan
Tìm kiếm trong toàn bộ hoặc một số trang đã chọn của tài liệu để tìm chữ ký văn bản cụ thể.

#### Triển khai từng bước

**Bước 1**: Xác định đường dẫn tệp.
```csharp
string filePath = "YOUR_OUTPUT_DIRECTORY"; // Đường dẫn đến tài liệu đã ký
```

**Bước 2**: Sử dụng `TextSearchOptions` để tìm kiếm.
```csharp
using (Signature signature = new Signature(filePath))
{
    TextSearchOptions searchOptions = new TextSearchOptions()
    {
        AllPages = true,
        MatchType = GroupDocs.Signature.Options.TextMatchType.Exact,
        Text = "John Smith"
    };
```

**Bước 3**: Thực hiện tìm kiếm.
```csharp
    List<TextSignature> signatures = signature.Search<TextSignature>(searchOptions);
    foreach (TextSignature textSignature in signatures)
    {
        if (textSignature != null)
        {
            Console.WriteLine($"Found Text signature at page {textSignature.PageNumber} with type [{textSignature.SignatureImplementation}] and text '{textSignature.Text}'. Location: {textSignature.Left}-{textSignature.Top}. Size is {textSignature.Width}x{textSignature.Height}.");
        }
    }
}
```

### Cập nhật chữ ký văn bản tài liệu

Sửa đổi chữ ký văn bản hiện có trong tài liệu khi cần.

#### Tổng quan
Điều chỉnh các thuộc tính của chữ ký văn bản hiện có, chẳng hạn như kích thước và vị trí.

#### Triển khai từng bước

**Bước 1**: Chỉ định đường dẫn tệp và ID chữ ký.
```csharp
string filePath = "YOUR_OUTPUT_DIRECTORY"; // Đường dẫn đến tài liệu đã ký
List<string> signatureIds = new List<string>(); // Giả sử danh sách này được điền bằng ID chữ ký hợp lệ
```

**Bước 2**: Tạo nên `TextSignature` đối tượng để cập nhật.
```csharp
using (Signature signature = new Signature(filePath))
{
    foreach (var item in signatureIds)
    {
        TextSignature temp = new TextSignature(item)
        {
            Width = 150,
            Height = 50,
            HorizontalAlignment = GroupDocs.Signature.Options.HorizontalAlignment.Right
        };
```

**Bước 3**: Cập nhật tài liệu.
```csharp
        SignResult signResult = signature.UpdateSignatures(temp);
        if (signResult.Succeeded.Count > 0)
        {
            Console.WriteLine($"Updated Text Signature: Id:{temp.SignatureId}");
        }
    }
}
```

#### Tùy chọn cấu hình chính
- **Chiều rộng và chiều cao**: Điều chỉnh kích thước chữ ký.
- **Căn chỉnh theo chiều ngang**: Kiểm soát vị trí chữ ký được cập nhật sẽ xuất hiện trên trang.

## Phần kết luận

Bằng cách làm theo hướng dẫn này, bạn đã học cách ký, xác minh, tìm kiếm, cập nhật và xóa chữ ký văn bản trong tài liệu bằng GroupDocs.Signature cho .NET. Những tính năng này rất cần thiết để tự động hóa quy trình ký số trong ứng dụng của bạn. Để biết thêm thông tin chi tiết và các tùy chọn nâng cao, vui lòng tham khảo [tài liệu chính thức](https://docs.groupdocs.com/signature/net/).