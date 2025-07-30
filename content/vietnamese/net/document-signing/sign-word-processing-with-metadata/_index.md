---
"description": "Thêm chữ ký siêu dữ liệu vào tài liệu Word bằng GroupDocs.Signature cho .NET. Nhúng thông tin tác giả, dấu thời gian và thuộc tính tùy chỉnh để tăng cường bảo mật và khả năng truy xuất nguồn gốc tài liệu."
"linktitle": "Ký hiệu Xử lý văn bản với Siêu dữ liệu"
"second_title": "API GroupDocs.Signature .NET"
"title": "Cải thiện tài liệu Word bằng chữ ký siêu dữ liệu trong C# .NET"
"url": "/vi/net/document-signing/sign-word-processing-with-metadata/"
"weight": 14
---

## Giới thiệu

Tài liệu xử lý văn bản là một trong những loại tệp phổ biến nhất được sử dụng trong kinh doanh, giáo dục và giao tiếp cá nhân. Việc đảm bảo tính xác thực, truy xuất nguồn gốc và duy trì tính toàn vẹn của các tài liệu này là rất quan trọng trong nhiều môi trường chuyên nghiệp. Một cách tiếp cận hiệu quả để tăng cường bảo mật và khả năng truy xuất nguồn gốc tài liệu là nhúng chữ ký siêu dữ liệu.

Hướng dẫn toàn diện này sẽ hướng dẫn bạn quy trình ký tài liệu Word bằng siêu dữ liệu bằng GroupDocs.Signature cho .NET. Bằng cách thêm chữ ký siêu dữ liệu, bạn có thể nhúng các thông tin quan trọng như chi tiết tác giả, dấu thời gian tạo, mã định danh tài liệu và các thuộc tính tùy chỉnh khác trực tiếp vào cấu trúc tệp tài liệu.

## Điều kiện tiên quyết

Trước khi thực hiện hướng dẫn này, hãy đảm bảo bạn có những điều sau:

1. [GroupDocs.Signature cho .NET](https://releases.groupdocs.com/signature/net/) - Tải xuống và cài đặt thư viện
2. Môi trường phát triển - Visual Studio hoặc bất kỳ IDE nào khác tương thích với .NET
3. Tài liệu Word - Một tệp tài liệu mẫu (DOCX, DOC, v.v.)
4. Kiến thức cơ bản về C# - Làm quen với ngôn ngữ lập trình C#

## Nhập không gian tên

Bắt đầu bằng cách nhập các không gian tên cần thiết để truy cập chức năng GroupDocs.Signature:

```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

## Bước 1: Thiết lập đường dẫn tệp

Xác định đường dẫn cho tài liệu Word nguồn của bạn và nơi lưu đầu ra đã ký:

```csharp
// Chỉ định đường dẫn đến tài liệu Word của bạn
string filePath = "sample.docx";

// Xác định thư mục đầu ra và tên tệp cho tài liệu đã ký
string outputDirectory = "Your Document Directory";
string outputFilePath = Path.Combine(outputDirectory, "SignWordProcessingWithMetadata", "SignedWithMetadata.docx");

// Đảm bảo thư mục đầu ra tồn tại
Directory.CreateDirectory(Path.GetDirectoryName(outputFilePath));
```

## Bước 2: Khởi tạo đối tượng chữ ký

Tạo một phiên bản của lớp Signature với tài liệu Word nguồn của bạn:

```csharp
using (Signature signature = new Signature(filePath))
{
    // Phần còn lại của mã sẽ ở đây
}
```

## Bước 3: Tạo và cấu hình chữ ký siêu dữ liệu

Tiếp theo, hãy xác định các tùy chọn siêu dữ liệu và thêm các loại chữ ký siêu dữ liệu khác nhau:

```csharp
// Tạo đối tượng tùy chọn siêu dữ liệu
MetadataSignOptions options = new MetadataSignOptions();

// Thêm nhiều loại siêu dữ liệu khác nhau bằng giao diện Fluent
options
    .Add(new WordProcessingMetadataSignature("Author", "Mr.Sherlock Holmes")) // Giá trị chuỗi
    .Add(new WordProcessingMetadataSignature("CreatedOn", DateTime.Now))      // Giá trị DateTime
    .Add(new WordProcessingMetadataSignature("DocumentId", 123456))           // Giá trị số nguyên
    .Add(new WordProcessingMetadataSignature("SignatureId", 123.456D))        // Giá trị kép
    .Add(new WordProcessingMetadataSignature("Amount", 123.456M))             // Giá trị thập phân
    .Add(new WordProcessingMetadataSignature("Total", 123.456F));             // Giá trị float
```

## Bước 4: Ký tài liệu bằng siêu dữ liệu

Áp dụng chữ ký siêu dữ liệu vào tài liệu Word và lưu kết quả:

```csharp
// Ký tài liệu và lưu vào đường dẫn tệp đầu ra
SignResult result = signature.Sign(outputFilePath, options);

// Hiển thị thông báo thành công
Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} metadata signature(s).");
Console.WriteLine($"Signed document saved at: {outputFilePath}");
```

## Ví dụ đầy đủ

Sau đây là ví dụ mã hoàn chỉnh kết hợp tất cả các bước:

```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;

namespace SignWordProcessingWithMetadataExample
{
    class Program
    {
        static void Main(string[] args)
        {
            // Chỉ định đường dẫn tệp
            string filePath = "sample.docx";
            string outputFilePath = Path.Combine("Your Document Directory", "SignWordProcessingWithMetadata", "SignedWithMetadata.docx");
            
            // Đảm bảo thư mục đầu ra tồn tại
            Directory.CreateDirectory(Path.GetDirectoryName(outputFilePath));

            // Ký tài liệu Word bằng siêu dữ liệu
            using (Signature signature = new Signature(filePath))
            {
                // Tạo đối tượng tùy chọn siêu dữ liệu
                MetadataSignOptions options = new MetadataSignOptions();
                
                // Thêm các loại chữ ký siêu dữ liệu khác nhau
                options
                    .Add(new WordProcessingMetadataSignature("Author", "Mr.Sherlock Holmes")) // Giá trị chuỗi
                    .Add(new WordProcessingMetadataSignature("CreatedOn", DateTime.Now))      // Giá trị DateTime
                    .Add(new WordProcessingMetadataSignature("DocumentId", 123456))           // Giá trị số nguyên
                    .Add(new WordProcessingMetadataSignature("SignatureId", 123.456D))        // Giá trị kép
                    .Add(new WordProcessingMetadataSignature("Amount", 123.456M))             // Giá trị thập phân
                    .Add(new WordProcessingMetadataSignature("Total", 123.456F));             // Giá trị float
                
                // Ký tài liệu và lưu vào hồ sơ
                SignResult result = signature.Sign(outputFilePath, options);
                
                // Hiển thị kết quả
                Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).");
                Console.WriteLine($"File saved at {outputFilePath}.");
            }
        }
    }
}
```

## Kỹ thuật siêu dữ liệu tài liệu Word nâng cao

### Làm việc với Thuộc tính Tài liệu Tùy chỉnh và Tích hợp

Tài liệu Word có cả thuộc tính tích hợp và thuộc tính tùy chỉnh có thể được truy cập thông qua bảng thuộc tính tài liệu. GroupDocs.Signature cho phép bạn làm việc với cả hai:

```csharp
// Thêm các thuộc tính tích hợp
options
    .Add(new WordProcessingMetadataSignature("Company", "Sherlock Holmes Consulting"))
    .Add(new WordProcessingMetadataSignature("Category", "Legal Document"))
    .Add(new WordProcessingMetadataSignature("Keywords", "contract,agreement,legal"))
    .Add(new WordProcessingMetadataSignature("Comments", "This document is confidential"))
    .Add(new WordProcessingMetadataSignature("Manager", "John Watson"));

// Thêm thuộc tính tùy chỉnh
options.Add(new WordProcessingMetadataSignature("Department", "Legal"));
options.Add(new WordProcessingMetadataSignature("SecurityLevel", "Confidential"));
```

### Tìm kiếm siêu dữ liệu trong tài liệu Word đã ký

Sau khi ký, bạn có thể muốn xác minh hoặc trích xuất siêu dữ liệu:

```csharp
// Tạo tùy chọn tìm kiếm cho siêu dữ liệu
MetadataSearchOptions searchOptions = new MetadataSearchOptions();

// Tìm kiếm chữ ký siêu dữ liệu
SearchResult searchResult = signature.Search(searchOptions);

// Hiển thị chữ ký tìm thấy
Console.WriteLine($"Found {searchResult.Signatures.Count} metadata signatures:");
foreach (var foundSignature in searchResult.Signatures)
{
    MetadataSignature metadataSignature = foundSignature as MetadataSignature;
    if (metadataSignature != null)
    {
        Console.WriteLine($"- {metadataSignature.Name}: {metadataSignature.Value} ({metadataSignature.Value.GetType().Name})");
    }
}
```

### Làm việc với các biến tài liệu

Các tài liệu Word cũng hỗ trợ các biến tài liệu, đây là một dạng siêu dữ liệu khác:

```csharp
// Thêm biến tài liệu
options.Add(new WordProcessingMetadataSignature("DocVariable1", "Custom Value 1", true));
options.Add(new WordProcessingMetadataSignature("DocVariable2", DateTime.Now, true));
```

## Phần kết luận

Trong hướng dẫn toàn diện này, bạn đã học cách ký tài liệu Word bằng siêu dữ liệu bằng GroupDocs.Signature cho .NET. Việc nhúng siêu dữ liệu vào tài liệu Word giúp tăng cường khả năng truy xuất nguồn gốc tài liệu, cung cấp ngữ cảnh có giá trị và giúp xác minh tính xác thực.

Chữ ký siêu dữ liệu trong tài liệu Word đặc biệt hữu ích trong môi trường kinh doanh và pháp lý, nơi nguồn gốc tài liệu, quyền tác giả và theo dõi phiên bản là rất quan trọng. Siêu dữ liệu nhúng có thể bao gồm thông tin về tác giả, thời gian tạo, mã định danh tài liệu và các thuộc tính tùy chỉnh phù hợp với nhu cầu của tổ chức bạn.

Bằng cách triển khai chữ ký siêu dữ liệu với GroupDocs.Signature, bạn có thể đảm bảo tài liệu Word của mình duy trì tính toàn vẹn và cung cấp thông tin có thể xác minh trong suốt vòng đời của chúng.

## Câu hỏi thường gặp

### Tôi có thể thêm siêu dữ liệu vào các tài liệu Word đã có một số thuộc tính được xác định không?

Có, bạn có thể thêm siêu dữ liệu mới hoặc cập nhật siêu dữ liệu hiện có trong tài liệu Word. GroupDocs.Signature sẽ xử lý việc tích hợp, bằng cách thêm thuộc tính mới hoặc cập nhật các thuộc tính hiện có có cùng tên.

### Định dạng xử lý văn bản nào được hỗ trợ để ký siêu dữ liệu?

GroupDocs.Signature cho .NET hỗ trợ ký siêu dữ liệu cho nhiều định dạng xử lý văn bản khác nhau, bao gồm DOCX, DOC, RTF, ODT, v.v. Để biết danh sách đầy đủ, hãy tham khảo [tài liệu](https://docs.groupdocs.com/signature/net/).

### Chữ ký siêu dữ liệu trong tài liệu Word có hiển thị cho người đọc không?

Chữ ký siêu dữ liệu không hiển thị trong nội dung tài liệu. Tuy nhiên, bạn có thể xem chúng thông qua bảng thuộc tính tài liệu trong Microsoft Word hoặc các ứng dụng tương thích khác.

### Tôi có thể xác thực theo chương trình xem tài liệu Word có bị giả mạo sau khi thêm siêu dữ liệu không?

Có, GroupDocs.Signature cung cấp khả năng xác minh có thể giúp phát hiện xem tài liệu có bị sửa đổi sau khi ký hay không, bao gồm cả những thay đổi đối với siêu dữ liệu.

### Có thể xóa siêu dữ liệu khỏi tài liệu Word không?

Có, GroupDocs.Signature cung cấp tùy chọn xóa chữ ký siêu dữ liệu khỏi tài liệu nếu cần. Điều này có thể hữu ích để xóa thông tin nhạy cảm trước khi chia sẻ tài liệu ra bên ngoài.

### Tôi có thể tìm thêm tài nguyên và hỗ trợ ở đâu?

- [Tài liệu tham khảo API](https://reference.groupdocs.com/signature/net/)
- [Tải xuống](https://releases.groupdocs.com/signature/net/)
- [Ví dụ](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
- [Tài liệu](https://docs.groupdocs.com/signature/net/)
- [Trang sản phẩm](https://products.groupdocs.com/signature/net/)
- [Blog](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
- [Diễn đàn hỗ trợ](https://forum.groupdocs.com/c/signature/13)
- [Giấy phép tạm thời](https://purchase.groupdocs.com/temporary-license/)