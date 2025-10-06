---
"description": "Làm chủ việc tìm kiếm chữ ký số trong tài liệu với GroupDocs.Signature cho .NET. Nâng cao tính bảo mật và xác minh tài liệu với hướng dẫn từng bước chi tiết của chúng tôi."
"linktitle": "Tìm kiếm chữ ký số"
"second_title": "API GroupDocs.Signature .NET"
"title": "Tìm kiếm chữ ký số trong tài liệu"
"url": "/vi/net/signature-searching/search-for-digital-signatures/"
"weight": 11
type: docs
---
## Giới thiệu

Trong bối cảnh kỹ thuật số ngày nay, việc đảm bảo tính xác thực và toàn vẹn của tài liệu là vô cùng quan trọng đối với các doanh nghiệp và tổ chức. Chữ ký số cung cấp một cơ chế mạnh mẽ để xác minh tính xác thực của tài liệu và phát hiện các sửa đổi trái phép. GroupDocs.Signature for .NET cung cấp giải pháp toàn diện để làm việc với chữ ký số ở nhiều định dạng tài liệu khác nhau, cho phép các nhà phát triển tích hợp liền mạch chức năng chữ ký vào các ứng dụng .NET của họ.

Hướng dẫn này sẽ hướng dẫn bạn quy trình tìm kiếm chữ ký số trong tài liệu bằng GroupDocs.Signature cho .NET, cung cấp giải thích chi tiết và ví dụ mã thực tế.

## Điều kiện tiên quyết

Trước khi đi sâu vào chi tiết triển khai, hãy đảm bảo bạn có đủ các điều kiện tiên quyết sau:

1. GroupDocs.Signature cho .NET: Tải xuống và cài đặt thư viện từ [đây](https://releases.groupdocs.com/signature/net/).
   
2. Môi trường phát triển: Thiết lập môi trường phát triển .NET bằng Visual Studio hoặc IDE mà bạn thích.
   
3. Tài liệu mẫu: Chuẩn bị các tài liệu mẫu có chữ ký số để thử nghiệm.

4. Kiến thức cơ bản: Có kiến thức cơ bản về ngôn ngữ lập trình C# và .NET framework.

## Nhập không gian tên

Bắt đầu bằng cách nhập các không gian tên cần thiết để truy cập chức năng do GroupDocs.Signature cung cấp cho .NET:

```csharp
using System;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

Bây giờ, chúng ta hãy chia nhỏ quá trình tìm kiếm chữ ký số thành các bước rõ ràng và dễ quản lý:

## Bước 1: Khởi tạo đối tượng chữ ký

Bắt đầu bằng cách tạo một phiên bản của `Signature` lớp, truyền đường dẫn đến tài liệu của bạn:

```csharp
string filePath = "sample_multiple_signatures.docx";
using (Signature signature = new Signature(filePath))
{
    // Mã để tìm kiếm chữ ký số sẽ được thêm vào đây
}
```

## Bước 2: Tìm kiếm chữ ký số

Tiếp theo, sử dụng `Search` phương pháp với `SignatureType.Digital` tham số để tìm kiếm chữ ký số trong tài liệu:

```csharp
// Tìm kiếm chữ ký số trong tài liệu
List<DigitalSignature> signatures = signature.Search<DigitalSignature>(SignatureType.Digital);
```

## Bước 3: Xử lý và hiển thị kết quả

Cuối cùng, xử lý kết quả tìm kiếm và hiển thị thông tin có liên quan về chữ ký số được tìm thấy:

```csharp
Console.WriteLine($"\nSource document ['{filePath}'] contains the following digital signatures:");
foreach (var digitalSignature in signatures)
{
    Console.WriteLine($"Digital signature found from {digitalSignature.SignTime} with validation status: {digitalSignature.IsValid}");
    Console.WriteLine($"Certificate: Subject: {digitalSignature.Certificate?.SubjectName}");
    Console.WriteLine($"Certificate: Issuer: {digitalSignature.Certificate?.IssuerName}");
    Console.WriteLine($"Certificate: Serial Number: {digitalSignature.Certificate?.SerialNumber}");
    Console.WriteLine();
}
```

## Ví dụ đầy đủ

Sau đây là một ví dụ hoàn chỉnh và hữu ích minh họa cách tìm kiếm chữ ký số trong tài liệu:

```csharp
using System;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;

namespace SearchDigitalSignatures
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
                // Tìm kiếm chữ ký số trong tài liệu
                List<DigitalSignature> signatures = signature.Search<DigitalSignature>(SignatureType.Digital);
                
                // Hiển thị kết quả tìm kiếm
                Console.WriteLine($"\nSource document ['{filePath}'] contains the following digital signatures:");
                
                if (signatures.Count > 0)
                {
                    foreach (var digitalSignature in signatures)
                    {
                        Console.WriteLine($"Digital signature found from {digitalSignature.SignTime} with validation status: {digitalSignature.IsValid}");
                        Console.WriteLine($"Certificate: Subject: {digitalSignature.Certificate?.SubjectName}");
                        Console.WriteLine($"Certificate: Issuer: {digitalSignature.Certificate?.IssuerName}");
                        Console.WriteLine($"Certificate: Serial Number: {digitalSignature.Certificate?.SerialNumber}");
                        Console.WriteLine();
                    }
                }
                else
                {
                    Console.WriteLine("No digital signatures found in the document.");
                }
            }
        }
    }
}
```

## Tùy chọn tìm kiếm nâng cao

Để tìm kiếm có mục tiêu hơn, bạn có thể sử dụng `DigitalSearchOptions` để tùy chỉnh tiêu chí tìm kiếm:

```csharp
// Tạo tùy chọn tìm kiếm kỹ thuật số
DigitalSearchOptions options = new DigitalSearchOptions()
{
    // Chỉ tìm kiếm trên các trang cụ thể (ví dụ: trang 1 và 2)
    PageNumber = 1,
    PagesSetup = new PagesSetup() { Pages = new List<int> { 1, 2 } },
    
    // Lọc theo bình luận trong chữ ký số
    Comments = "Approved",
    
    // Đặt phạm vi ngày và giờ để tìm kiếm
    SignDateTimeFrom = new DateTime(2022, 1, 1),
    SignDateTimeTo = DateTime.Now
};

// Tìm kiếm với các tùy chọn cụ thể
List<DigitalSignature> signatures = signature.Search<DigitalSignature>(options);
```

## Làm việc với thông tin chứng chỉ

Chữ ký số chứa thông tin chứng chỉ có giá trị mà bạn có thể truy cập và xác thực:

```csharp
foreach (var digitalSignature in signatures)
{
    if (digitalSignature.Certificate != null)
    {
        // Truy cập thuộc tính chứng chỉ
        Console.WriteLine($"Certificate Valid From: {digitalSignature.Certificate.NotBefore}");
        Console.WriteLine($"Certificate Valid To: {digitalSignature.Certificate.NotAfter}");
        
        // Kiểm tra xem chứng chỉ có nằm trong phạm vi ngày hợp lệ không
        bool isDateValid = DateTime.Now >= digitalSignature.Certificate.NotBefore && 
                          DateTime.Now <= digitalSignature.Certificate.NotAfter;
        
        Console.WriteLine($"Certificate Date Validity: {isDateValid}");
        
        // Truy cập thông tin chi tiết của đơn vị phát hành chứng chỉ
        Console.WriteLine($"Certificate Issuer: {digitalSignature.Certificate.IssuerName}");
    }
}
```

## Phần kết luận

GroupDocs.Signature for .NET cung cấp một giải pháp mạnh mẽ và linh hoạt để tìm kiếm và xác thực chữ ký số trong tài liệu. Trong hướng dẫn này, chúng tôi đã khám phá quy trình từng bước triển khai chức năng tìm kiếm chữ ký số trong các ứng dụng .NET, trang bị cho bạn kiến thức để nâng cao tính bảo mật và xác minh tính toàn vẹn của tài liệu.

Bằng cách tận dụng GroupDocs.Signature, bạn có thể xây dựng các hệ thống quản lý tài liệu mạnh mẽ đảm bảo tính xác thực và toàn vẹn của tài liệu kỹ thuật số, thúc đẩy sự tin cậy và tuân thủ trong quy trình kinh doanh của bạn.

## Câu hỏi thường gặp

### GroupDocs.Signature có thể xác minh tính hợp lệ của chữ ký số không?

Có, GroupDocs.Signature tự động xác thực chữ ký số trong quá trình tìm kiếm và cung cấp trạng thái xác thực thông qua `IsValid` tài sản của `DigitalSignature` lớp học.

### Định dạng tài liệu nào hỗ trợ tìm kiếm chữ ký số?

GroupDocs.Signature hỗ trợ tìm kiếm chữ ký số ở nhiều định dạng khác nhau, bao gồm PDF, tài liệu Microsoft Office (Word, Excel, PowerPoint), định dạng OpenOffice, v.v.

### Tôi có thể tìm kiếm chữ ký số trong các tài liệu được bảo vệ bằng mật khẩu không?

Có, bạn có thể tìm kiếm chữ ký số trong các tài liệu được bảo vệ bằng mật khẩu bằng cách cung cấp mật khẩu khi khởi tạo `Signature` sự vật:

```csharp
LoadOptions loadOptions = new LoadOptions() { Password = "your_password" };
using (Signature signature = new Signature(filePath, loadOptions))
{
    // Tìm kiếm chữ ký số
}
```

### Làm thế nào tôi có thể xác minh xem chữ ký số có được tạo bởi một người cụ thể hay không?

Bạn có thể kiểm tra tên chủ thể của chứng chỉ và các thuộc tính khác để xác minh danh tính của người ký:

```csharp
foreach (var signature in signatures)
{
    if (signature.Certificate?.SubjectName?.Contains("John Doe") == true)
    {
        Console.WriteLine("Found signature by John Doe");
    }
}
```

### Tôi có thể trích xuất khóa công khai từ chứng chỉ chữ ký số không?

Có, bạn có thể truy cập thông tin khóa công khai thông qua thuộc tính chứng chỉ:

```csharp
if (signature.Certificate != null)
{
    // Truy cập thông tin khóa công khai
    Console.WriteLine($"Public Key: {signature.Certificate.GetPublicKeyString()}");
}
```

## Xem thêm

* [Tài liệu tham khảo API](https://reference.groupdocs.com/signature/net/)
* [Ví dụ về mã](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
* [Tài liệu sản phẩm](https://docs.groupdocs.com/signature/net/)
* [Trang sản phẩm](https://products.groupdocs.com/signature/net/)
* [Tải xuống phiên bản mới nhất](https://releases.groupdocs.com/signature/net/)
* [Bài viết trên blog](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
* [Diễn đàn hỗ trợ](https://forum.groupdocs.com/c/signature/13)
* [Giấy phép tạm thời](https://purchase.groupdocs.com/temporary-license/)