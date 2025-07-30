---
"description": "Tìm hiểu cách xác minh mã QR trong tài liệu bằng GroupDocs.Signature cho .NET. Hướng dẫn đầy đủ với các ví dụ mã và phương pháp hay nhất để xác thực tài liệu."
"linktitle": "Xác minh mã QR"
"second_title": "API GroupDocs.Signature .NET"
"title": "Xác minh mã QR trong tài liệu"
"url": "/vi/net/verify-operations/verify-qr-code/"
"weight": 12
---

## Giới thiệu

Bảo mật tài liệu là một khía cạnh quan trọng trong hoạt động kinh doanh hiện đại. Mã QR đã trở thành một phương pháp ngày càng phổ biến để nhúng thông tin vào tài liệu, có thể được xác minh tính xác thực. GroupDocs.Signature for .NET cung cấp một giải pháp mạnh mẽ và linh hoạt để xác minh mã QR được nhúng trong tài liệu ở nhiều định dạng khác nhau.

Hướng dẫn toàn diện này sẽ hướng dẫn bạn quy trình triển khai xác minh mã QR trong các ứng dụng .NET của bạn, đảm bảo tài liệu của bạn duy trì được tính toàn vẹn và tính xác thực.

## Điều kiện tiên quyết

Trước khi triển khai chức năng xác minh mã QR, hãy đảm bảo bạn có đủ các điều kiện tiên quyết sau:

1. GroupDocs.Signature cho .NET: Tải xuống và cài đặt thư viện từ [trang tải xuống](https://releases.groupdocs.com/signature/net/).
2. Môi trường phát triển: Visual Studio hoặc bất kỳ môi trường phát triển .NET tương thích nào.
3. Tài liệu thử nghiệm: Tài liệu chứa chữ ký mã QR nhằm mục đích xác minh.
4. Kiến thức cơ bản: Có hiểu biết về lập trình C# và các khái niệm về .NET framework.

## Nhập không gian tên

Bắt đầu bằng cách nhập các không gian tên cần thiết để truy cập chức năng GroupDocs.Signature:

```csharp
using System;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

## Quy trình xác minh mã QR từng bước

Thực hiện theo các bước chi tiết sau để xác minh mã QR trong tài liệu của bạn:

### Bước 1: Chỉ định Đường dẫn Tài liệu

```csharp
// Cung cấp đường dẫn đến tài liệu có chứa chữ ký mã QR
string filePath = "sample_multiple_signatures.docx";
```

Đảm bảo bạn thay thế đường dẫn ví dụ bằng đường dẫn thực tế tới tài liệu của bạn.

### Bước 2: Khởi tạo đối tượng chữ ký

```csharp
// Tạo một phiên bản Chữ ký bằng cách truyền đường dẫn tài liệu
using (Signature signature = new Signature(filePath))
{
    // Mã xác minh sẽ được triển khai tại đây
}
```

Lớp Signature là điểm vào chính cho tất cả các hoạt động trong API GroupDocs.Signature.

### Bước 3: Cấu hình tùy chọn xác minh mã QR

```csharp
// Xác định các tùy chọn xác minh mã QR
QrCodeVerifyOptions options = new QrCodeVerifyOptions()
{
    AllPages = true, // Kiểm tra tất cả các trang của tài liệu
    Text = "John",   // Văn bản để xác minh trong mã QR
    MatchType = TextMatchType.Contains // Chỉ định tiêu chí phù hợp với văn bản
};
```

Các tùy chọn xác minh cho phép bạn xác định các tiêu chí cụ thể cho quá trình xác minh:
- `AllPages`: Đặt thành true để kiểm tra tất cả các trang tài liệu (hành vi mặc định)
- `Text`: Nội dung văn bản phải khớp với mã QR
- `MatchType`: Phương pháp khớp văn bản (Contains, Exact, StartsWith, v.v.)

### Bước 4: Thực hiện quy trình xác minh

```csharp
// Thực hiện xác minh
VerificationResult result = signature.Verify(options);
```

Quá trình xác minh sẽ được thực hiện dựa trên các tùy chọn bạn đã chỉ định.

### Bước 5: Kết quả xác minh quy trình

```csharp
// Kiểm tra kết quả xác minh và xử lý theo quy định
if (result.IsValid)
{
    Console.WriteLine($"Document {filePath} contains valid QR code signature!");
    
    // Hiển thị thông tin về chữ ký thành công
    foreach (QrCodeSignature signature in result.Succeeded)
    {
        Console.WriteLine($"Found valid QR Code signature with text: {signature.Text}");
        Console.WriteLine($"QR Code type: {signature.EncodeType.TypeName}");
        Console.WriteLine($"Location: Page {signature.PageNumber}, {signature.Left}x{signature.Top}");
    }
}
else
{
    Console.WriteLine($"Document {filePath} failed verification process.");
    Console.WriteLine($"Number of failed signatures: {result.Failed.Count}");
}
```

Xử lý kết quả xác minh đúng cách cho phép ứng dụng của bạn thực hiện các hành động phù hợp dựa trên kết quả xác minh.

## Ví dụ đầy đủ

Sau đây là một ví dụ hoàn chỉnh và hữu ích minh họa cách xác minh mã QR:

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
            // Đường dẫn tài liệu
            string filePath = "sample_multiple_signatures.docx";
            
            // Khởi tạo phiên bản chữ ký
            using (Signature signature = new Signature(filePath))
            {
                // Thiết lập tùy chọn xác minh
                QrCodeVerifyOptions options = new QrCodeVerifyOptions()
                {
                    AllPages = true,
                    Text = "John",
                    MatchType = TextMatchType.Contains
                };
                
                // Xác minh chữ ký tài liệu
                VerificationResult result = signature.Verify(options);
                
                // Kết quả xác minh quy trình
                if (result.IsValid)
                {
                    Console.WriteLine($"Document {filePath} contains valid QR code signature!");
                    
                    foreach (QrCodeSignature qrSignature in result.Succeeded)
                    {
                        Console.WriteLine($"Found valid QR Code with text: {qrSignature.Text}");
                    }
                }
                else
                {
                    Console.WriteLine($"Document {filePath} failed verification process.");
                }
            }
        }
    }
}
```

## Tùy chọn xác minh nâng cao

GroupDocs.Signature cung cấp các tùy chọn bổ sung cho các tình huống xác minh phức tạp hơn:

### Xác minh các loại mã QR cụ thể

```csharp
QrCodeVerifyOptions options = new QrCodeVerifyOptions()
{
    EncodeType = QrCodeTypes.QR,  // Chỉ xác minh mã QR chuẩn
    Text = "Confidential",
    MatchType = TextMatchType.Exact
};
```

### Xác minh trên các trang cụ thể

```csharp
QrCodeVerifyOptions options = new QrCodeVerifyOptions()
{
    AllPages = false,
    PageNumber = 2,  // Chỉ xác minh ở trang 2
    Text = "Approved"
};
```

### Sử dụng biểu thức chính quy để xác minh

```csharp
QrCodeVerifyOptions options = new QrCodeVerifyOptions()
{
    Text = "INV-\\d{6}",  // So khớp số hóa đơn (ví dụ: INV-123456)
    MatchType = TextMatchType.Regex
};
```

## Thực hành tốt nhất để xác minh mã QR

1. Luôn xác thực đầu vào: Đảm bảo đường dẫn tài liệu và tiêu chí xác minh hợp lệ trước khi xử lý.
2. Triển khai xử lý lỗi: Sử dụng khối try-catch để xử lý các ngoại lệ tiềm ẩn trong quá trình xác minh.
3. Xem xét hiệu suất: Đối với các tài liệu lớn, hãy cân nhắc việc xác minh các trang cụ thể thay vì toàn bộ tài liệu.
4. Ghi lại kết quả xác minh: Lưu giữ nhật ký các quy trình xác minh cho mục đích kiểm tra.
5. Kiểm tra với nhiều định dạng tài liệu khác nhau: Đảm bảo quá trình xác minh của bạn hoạt động trên mọi định dạng tài liệu bắt buộc.

## Phần kết luận

Xác minh mã QR trong tài liệu là một khía cạnh thiết yếu để đảm bảo tính xác thực và toàn vẹn của tài liệu. GroupDocs.Signature for .NET cung cấp một API toàn diện và thân thiện với người dùng để triển khai xác minh mã QR trong các ứng dụng .NET của bạn.

Bằng cách làm theo hướng dẫn này, bạn đã học được cách:
- Cấu hình và khởi tạo quy trình xác minh
- Chỉ định các tiêu chí xác minh khác nhau
- Xử lý và diễn giải kết quả xác minh
- Triển khai các tùy chọn xác minh nâng cao

Kiến thức này giúp bạn nâng cao tính bảo mật và độ tin cậy của hệ thống quản lý tài liệu.

## Câu hỏi thường gặp

### GroupDocs.Signature có thể xác minh nhiều mã QR trong một tài liệu không?
Có, GroupDocs.Signature có thể xác minh nhiều mã QR trong một tài liệu. Kết quả xác minh sẽ bao gồm tất cả các mã QR trùng khớp.

### Định dạng tài liệu nào được hỗ trợ để xác minh mã QR?
GroupDocs.Signature hỗ trợ nhiều định dạng tài liệu bao gồm PDF, Word (DOC, DOCX), Excel (XLS, XLSX), PowerPoint (PPT, PPTX), hình ảnh, v.v.

### Tôi có thể xác minh mã QR bằng mã hóa hoặc định dạng cụ thể không?
Có, GroupDocs.Signature cung cấp các tùy chọn để xác minh mã QR với các loại mã hóa và mẫu định dạng nội dung cụ thể.

### Có thể xác minh mã QR do ứng dụng của bên thứ ba tạo ra không?
Có, GroupDocs.Signature có thể xác minh mã QR chuẩn do hầu hết các ứng dụng tạo ra, miễn là chúng tuân theo định dạng mã QR chuẩn.

### Làm thế nào để xử lý mã QR chứa dữ liệu nhị phân thay vì văn bản?
GroupDocs.Signature cung cấp các tùy chọn để xác minh mã QR bằng dữ liệu nhị phân thông qua `BinaryData` thuộc tính của các tùy chọn xác minh.

### Tài nguyên liên quan
* [Tài liệu tham khảo API GroupDocs.Signature](https://reference.groupdocs.com/signature/net/)
* [Tải xuống GroupDocs.Signature](https://releases.groupdocs.com/signature/net/)
* [Ví dụ mã trên GitHub](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
* [Tài liệu](https://docs.groupdocs.com/signature/net/)
* [Trang sản phẩm](https://products.groupdocs.com/signature/net/)
* [Bài viết trên blog](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
* [Diễn đàn hỗ trợ](https://forum.groupdocs.com/c/signature/13)
* [Giấy phép tạm thời](https://purchase.groupdocs.com/temporary-license/)