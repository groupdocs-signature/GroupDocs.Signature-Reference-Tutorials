---
"description": "Tìm hiểu cách tìm kiếm nhiều loại chữ ký trong tài liệu bằng GroupDocs.Signature cho .NET. Hướng dẫn toàn diện kèm ví dụ mã để tăng cường bảo mật tài liệu."
"linktitle": "Tìm kiếm nhiều chữ ký"
"second_title": "API GroupDocs.Signature .NET"
"title": "Tìm kiếm nhiều loại chữ ký trong tài liệu"
"url": "/vi/net/signature-searching/search-for-multiple-signatures/"
"weight": 14
type: docs
---
## Giới thiệu

Trong các hệ thống quản lý tài liệu hiện đại, khả năng tìm kiếm và xác thực nhiều loại chữ ký trong một tài liệu ngày càng trở nên quan trọng. Các tổ chức thường sử dụng nhiều loại chữ ký khác nhau—chẳng hạn như chữ ký số, chữ ký văn bản, mã vạch, mã QR, v.v.—để tăng cường bảo mật tài liệu và đơn giản hóa quy trình xác minh. GroupDocs.Signature for .NET cung cấp một nền tảng mạnh mẽ cho phép các nhà phát triển triển khai chức năng tìm kiếm chữ ký toàn diện trên nhiều định dạng tài liệu khác nhau.

Hướng dẫn này sẽ hướng dẫn bạn quy trình tìm kiếm nhiều loại chữ ký trong tài liệu bằng GroupDocs.Signature cho .NET, cung cấp các giải thích chi tiết và ví dụ mã thực tế.

## Điều kiện tiên quyết

Trước khi bắt đầu triển khai chức năng tìm kiếm nhiều chữ ký, hãy đảm bảo bạn có đủ các điều kiện tiên quyết sau:

1. Môi trường phát triển: Visual Studio hoặc bất kỳ môi trường phát triển .NET nào được cài đặt trên hệ thống của bạn.
  
2. GroupDocs.Signature cho .NET: Tải xuống và cài đặt thư viện GroupDocs.Signature cho .NET từ [đây](https://releases.groupdocs.com/signature/net/).

3. Kiến thức cơ bản về C#: Quen thuộc với ngôn ngữ lập trình C# và các khái niệm về .NET framework.

4. Tài liệu mẫu: Chuẩn bị tài liệu thử nghiệm có chứa nhiều loại chữ ký khác nhau cho mục đích thử nghiệm.

## Nhập không gian tên

Bắt đầu bằng cách nhập các không gian tên cần thiết để truy cập chức năng GroupDocs.Signature:

```csharp
using System;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

Bây giờ, chúng ta hãy chia nhỏ quá trình tìm kiếm nhiều loại chữ ký thành các bước rõ ràng và dễ quản lý:

## Bước 1: Tải tài liệu

Đầu tiên, hãy tải tài liệu có chứa chữ ký mà bạn muốn tìm kiếm:

```csharp
string filePath = "sample_multiple_signatures.docx";
using (Signature signature = new Signature(filePath))
{
    // Mã tìm kiếm đa chữ ký sẽ được thêm vào đây
}
```

## Bước 2: Xác định các tùy chọn tìm kiếm cho các loại chữ ký khác nhau

Tạo tùy chọn tìm kiếm cho từng loại chữ ký bạn muốn tìm kiếm:

```csharp
// Xác định các tùy chọn tìm kiếm cho chữ ký văn bản
TextSearchOptions textOptions = new TextSearchOptions
{
    AllPages = true,  // Tìm kiếm trên tất cả các trang
    Text = "Signature",  // Tùy chọn: văn bản để tìm
    MatchType = TextMatchType.Contains  // Tiêu chí phù hợp
};

// Xác định các tùy chọn tìm kiếm cho chữ ký số
DigitalSearchOptions digitalOptions = new DigitalSearchOptions
{
    AllPages = true
};

// Xác định các tùy chọn tìm kiếm cho chữ ký mã vạch
BarcodeSearchOptions barcodeOptions = new BarcodeSearchOptions
{
    AllPages = true,
    Text = "123456",  // Tùy chọn: văn bản mã vạch để khớp
    MatchType = TextMatchType.Exact  // Tiêu chí phù hợp
};

// Xác định các tùy chọn tìm kiếm cho chữ ký mã QR
QrCodeSearchOptions qrCodeOptions = new QrCodeSearchOptions
{
    AllPages = true,
    Text = "John",  // Tùy chọn: Văn bản mã QR để khớp
    MatchType = TextMatchType.Contains  // Tiêu chí phù hợp
};

// Xác định các tùy chọn tìm kiếm cho chữ ký siêu dữ liệu
MetadataSearchOptions metadataOptions = new MetadataSearchOptions();
```

## Bước 3: Thêm tùy chọn vào bộ sưu tập

Thêm tất cả các tùy chọn tìm kiếm vào bộ sưu tập:

```csharp
// Tạo danh sách để lưu trữ tất cả các tùy chọn tìm kiếm
List<SearchOptions> searchOptions = new List<SearchOptions>
{
    textOptions,
    digitalOptions,
    barcodeOptions,
    qrCodeOptions,
    metadataOptions
};
```

## Bước 4: Thực hiện tìm kiếm và xử lý kết quả

Thực hiện tìm kiếm bằng cách sử dụng các tùy chọn tìm kiếm kết hợp và xử lý kết quả:

```csharp
// Tìm kiếm tất cả các loại chữ ký bằng các tùy chọn được xác định
SearchResult result = signature.Search(searchOptions);

// Kiểm tra xem có tìm thấy chữ ký không
if (result.Signatures.Count > 0)
{
    Console.WriteLine($"\nSource document ['{filePath}'] contains {result.Signatures.Count} signature(s):");
    
    // Lặp lại các chữ ký đã tìm thấy
    foreach (var foundSignature in result.Signatures)
    {
        Console.WriteLine($"Signature found: Type: {foundSignature.SignatureType}, Page: {foundSignature.PageNumber}, ID: {foundSignature.SignatureId}");
        
        // Các loại chữ ký cụ thể của quy trình
        if (foundSignature is TextSignature textSignature)
        {
            Console.WriteLine($"Text: '{textSignature.Text}'");
        }
        else if (foundSignature is BarcodeSignature barcodeSignature)
        {
            Console.WriteLine($"Barcode Type: {barcodeSignature.EncodeType.TypeName}, Text: '{barcodeSignature.Text}'");
        }
        else if (foundSignature is QrCodeSignature qrCodeSignature)
        {
            Console.WriteLine($"QR Code Type: {qrCodeSignature.EncodeType.TypeName}, Text: '{qrCodeSignature.Text}'");
        }
        else if (foundSignature is DigitalSignature digitalSignature)
        {
            Console.WriteLine($"Certificate: {digitalSignature.Certificate?.SubjectName}, Valid: {digitalSignature.IsValid}");
        }
        else if (foundSignature is MetadataSignature metadataSignature)
        {
            Console.WriteLine($"Metadata: Name: {metadataSignature.Name}, Value: {metadataSignature.Value}");
        }
    }
}
else
{
    Console.WriteLine("No signatures were found in the document.");
}
```

## Ví dụ đầy đủ

Sau đây là một ví dụ hoàn chỉnh, hữu ích minh họa cách tìm kiếm nhiều loại chữ ký trong một tài liệu:

```csharp
using System;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;

namespace MultiSignatureSearch
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
                try
                {
                    // Xác định các tùy chọn tìm kiếm cho chữ ký văn bản
                    TextSearchOptions textOptions = new TextSearchOptions
                    {
                        AllPages = true,
                        MatchType = TextMatchType.Contains
                    };

                    // Xác định các tùy chọn tìm kiếm cho chữ ký số
                    DigitalSearchOptions digitalOptions = new DigitalSearchOptions
                    {
                        AllPages = true
                    };

                    // Xác định các tùy chọn tìm kiếm cho chữ ký mã vạch
                    BarcodeSearchOptions barcodeOptions = new BarcodeSearchOptions
                    {
                        AllPages = true
                    };

                    // Xác định các tùy chọn tìm kiếm cho chữ ký mã QR
                    QrCodeSearchOptions qrCodeOptions = new QrCodeSearchOptions
                    {
                        AllPages = true
                    };

                    // Xác định các tùy chọn tìm kiếm cho chữ ký siêu dữ liệu
                    MetadataSearchOptions metadataOptions = new MetadataSearchOptions();

                    // Tạo danh sách để lưu trữ tất cả các tùy chọn tìm kiếm
                    List<SearchOptions> searchOptions = new List<SearchOptions>
                    {
                        textOptions,
                        digitalOptions,
                        barcodeOptions,
                        qrCodeOptions,
                        metadataOptions
                    };

                    // Tìm kiếm tất cả các loại chữ ký
                    SearchResult result = signature.Search(searchOptions);

                    // Kiểm tra xem có tìm thấy chữ ký không
                    if (result.Signatures.Count > 0)
                    {
                        Console.WriteLine($"\nSource document ['{filePath}'] contains {result.Signatures.Count} signature(s):");
                        
                        // Xử lý kết quả theo loại chữ ký
                        foreach (var foundSignature in result.Signatures)
                        {
                            Console.WriteLine($"Signature found: Type: {foundSignature.SignatureType}, Page: {foundSignature.PageNumber}");
                            
                            // Các loại chữ ký cụ thể của quy trình
                            switch (foundSignature.SignatureType)
                            {
                                case SignatureType.Text:
                                    var textSignature = foundSignature as TextSignature;
                                    Console.WriteLine($"Text: '{textSignature.Text}'");
                                    break;
                                    
                                case SignatureType.Barcode:
                                    var barcodeSignature = foundSignature as BarcodeSignature;
                                    Console.WriteLine($"Barcode Type: {barcodeSignature.EncodeType.TypeName}, Text: '{barcodeSignature.Text}'");
                                    break;
                                    
                                case SignatureType.QrCode:
                                    var qrCodeSignature = foundSignature as QrCodeSignature;
                                    Console.WriteLine($"QR Code Type: {qrCodeSignature.EncodeType.TypeName}, Text: '{qrCodeSignature.Text}'");
                                    break;
                                    
                                case SignatureType.Digital:
                                    var digitalSignature = foundSignature as DigitalSignature;
                                    Console.WriteLine($"Certificate: {digitalSignature.Certificate?.SubjectName}, Valid: {digitalSignature.IsValid}");
                                    break;
                                    
                                case SignatureType.Metadata:
                                    var metadataSignature = foundSignature as MetadataSignature;
                                    Console.WriteLine($"Metadata: Name: {metadataSignature.Name}, Value: {metadataSignature.Value}");
                                    break;
                            }
                            
                            Console.WriteLine(); // Thêm ngắt dòng giữa các chữ ký
                        }
                    }
                    else
                    {
                        Console.WriteLine("No signatures were found in the document.");
                    }
                }
                catch (Exception ex)
                {
                    Console.WriteLine($"Error occurred: {ex.Message}");
                }
            }
            
            Console.WriteLine("Press any key to exit...");
            Console.ReadKey();
        }
    }
}
```

## Kỹ thuật tìm kiếm đa chữ ký nâng cao

### Lọc kết quả tìm kiếm

Bạn có thể triển khai tính năng lọc nâng cao để thu hẹp kết quả tìm kiếm:

```csharp
// Lọc kết quả theo số trang
var signaturesOnFirstPage = result.Signatures.FindAll(s => s.PageNumber == 1);

// Lọc kết quả theo loại chữ ký
var digitalSignatures = result.Signatures.FindAll(s => s.SignatureType == SignatureType.Digital);
var qrCodeSignatures = result.Signatures.FindAll(s => s.SignatureType == SignatureType.QrCode);

// Lọc chữ ký văn bản có chứa nội dung cụ thể
var approvalSignatures = result.Signatures
    .FindAll(s => s is TextSignature && ((TextSignature)s).Text.Contains("Approved"));
```

### Xác thực nhiều chữ ký

Triển khai logic xác thực cho các loại chữ ký khác nhau:

```csharp
bool ValidateAllSignatures(SearchResult result)
{
    bool isDocumentValid = true;
    
    // Kiểm tra xem tài liệu có chữ ký số hợp lệ không
    bool hasValidDigitalSignature = result.Signatures
        .Any(s => s is DigitalSignature && ((DigitalSignature)s).IsValid);
    
    if (!hasValidDigitalSignature)
    {
        Console.WriteLine("Warning: Document does not contain a valid digital signature");
        isDocumentValid = false;
    }
    
    // Kiểm tra xem tài liệu có yêu cầu mã QR không
    bool hasRequiredQRCode = result.Signatures
        .Any(s => s is QrCodeSignature && ((QrCodeSignature)s).Text.Contains("Auth-Code"));
    
    if (!hasRequiredQRCode)
    {
        Console.WriteLine("Warning: Document does not contain the required authentication QR code");
        isDocumentValid = false;
    }
    
    return isDocumentValid;
}
```

### Tìm kiếm với Xử lý tùy chỉnh

Bạn có thể xác định logic xử lý tùy chỉnh cho các hoạt động tìm kiếm:

```csharp
// Tạo tùy chọn tìm kiếm với xử lý tùy chỉnh
TextSearchOptions textOptions = new TextSearchOptions
{
    AllPages = true,
    
    // Xác định xử lý tùy chỉnh bằng cách sử dụng một đại biểu
    ProcessCompleted = (signature) =>
    {
        // Logic xác thực tùy chỉnh - chỉ chấp nhận chữ ký trên các trang được chỉ định
        TextSignature textSignature = signature as TextSignature;
        return textSignature != null && (textSignature.PageNumber == 1 || textSignature.PageNumber == 2);
    }
};
```

## Phần kết luận

Trong hướng dẫn toàn diện này, chúng tôi đã khám phá cách tìm kiếm nhiều loại chữ ký trong tài liệu bằng GroupDocs.Signature cho .NET. Từ việc thiết lập các tùy chọn tìm kiếm cho các loại chữ ký khác nhau đến xử lý và xác thực kết quả, giờ đây bạn đã có kiến thức để triển khai chức năng tìm kiếm chữ ký mạnh mẽ trong các ứng dụng .NET của mình.

Khả năng tìm kiếm nhiều loại chữ ký cùng lúc giúp nâng cao quy trình xác minh tài liệu, tăng cường các biện pháp bảo mật và hợp lý hóa quy trình xác thực tài liệu. GroupDocs.Signature cung cấp một khuôn khổ mạnh mẽ và linh hoạt để làm việc với nhiều loại chữ ký trên nhiều định dạng tài liệu khác nhau, khiến nó trở thành lựa chọn tuyệt vời cho các ứng dụng xử lý tài liệu.

## Câu hỏi thường gặp

### Tôi có thể tìm kiếm chữ ký trong các tài liệu được bảo vệ bằng mật khẩu không?

Có, GroupDocs.Signature hỗ trợ tìm kiếm chữ ký trong các tài liệu được bảo vệ bằng mật khẩu. Bạn có thể cung cấp mật khẩu khi khởi tạo `Signature` sự vật:

```csharp
LoadOptions loadOptions = new LoadOptions { Password = "your_password" };
using (Signature signature = new Signature(filePath, loadOptions))
{
    // Tìm kiếm chữ ký
}
```

### Định dạng tài liệu nào được hỗ trợ để tìm kiếm chữ ký?

GroupDocs.Signature hỗ trợ nhiều định dạng tài liệu, bao gồm PDF, tài liệu Microsoft Office (Word, Excel, PowerPoint), định dạng OpenOffice, hình ảnh, v.v.

### Tôi có thể giới hạn tìm kiếm ở những trang cụ thể trong tài liệu không?

Có, mỗi loại tùy chọn tìm kiếm đều có các thuộc tính cho phép bạn chỉ định những trang nào cần tìm kiếm:

```csharp
TextSearchOptions options = new TextSearchOptions
{
    AllPages = false,  // Không tìm kiếm tất cả các trang
    PageNumber = 1,    // Chỉ tìm kiếm trên trang 1
    
    // Hoặc chỉ định nhiều trang
    PagesSetup = new PagesSetup { Pages = new List<int> { 1, 3, 5 } }
};
```

### Làm thế nào để tối ưu hóa hiệu suất khi tìm kiếm trong các tài liệu lớn?

Đối với các tài liệu lớn, bạn có thể tối ưu hóa hiệu suất bằng cách:

1. Giới hạn tìm kiếm ở các trang hoặc phạm vi trang cụ thể
2. Sử dụng tiêu chí tìm kiếm cụ thể hơn để giảm số lượng kết quả trùng khớp tiềm năng
3. Triển khai phân trang trong màn hình hiển thị kết quả của bạn
4. Tìm kiếm từng loại chữ ký một nếu bạn không cần kết quả đồng thời

### Tôi có thể mở rộng GroupDocs.Signature để hỗ trợ các loại chữ ký tùy chỉnh không?

Mặc dù GroupDocs.Signature cung cấp hỗ trợ tích hợp cho các loại chữ ký phổ biến, bạn có thể mở rộng chức năng của nó bằng cách:

1. Tạo các lớp tùy chọn tìm kiếm tùy chỉnh bắt nguồn từ `SearchOptions`
2. Triển khai logic xử lý tùy chỉnh bằng cách sử dụng `ProcessCompleted` đại biểu
3. Phát triển các lớp bao bọc kết hợp nhiều tìm kiếm chữ ký với logic kinh doanh nâng cao

## Xem thêm

* [Tài liệu tham khảo API](https://reference.groupdocs.com/signature/net/)
* [Ví dụ mã trên GitHub](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
* [Tài liệu sản phẩm](https://docs.groupdocs.com/signature/net/)
* [Trang sản phẩm](https://products.groupdocs.com/signature/net/)
* [Tải xuống phiên bản mới nhất](https://releases.groupdocs.com/signature/net/)
* [Bài viết trên blog](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
* [Diễn đàn hỗ trợ miễn phí](https://forum.groupdocs.com/c/signature/13)
* [Giấy phép tạm thời](https://purchase.groupdocs.com/temporary-license/)