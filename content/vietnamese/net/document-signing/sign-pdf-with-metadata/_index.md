---
"description": "Tích hợp chữ ký siêu dữ liệu vào tài liệu PDF bằng GroupDocs.Signature cho .NET. Tìm hiểu cách nhúng thông tin tác giả, dấu thời gian và dữ liệu tùy chỉnh để tăng cường tính xác thực và khả năng truy xuất nguồn gốc của PDF."
"linktitle": "Ký PDF bằng Siêu dữ liệu"
"second_title": "API GroupDocs.Signature .NET"
"title": "Thêm chữ ký siêu dữ liệu vào tài liệu PDF trong C# .NET"
"url": "/vi/net/document-signing/sign-pdf-with-metadata/"
"weight": 11
type: docs
---
## Giới thiệu

Tài liệu PDF (Định dạng Tài liệu Di động) được sử dụng rộng rãi trong nhiều ngành nghề nhờ tính nhất quán và tính độc lập với nền tảng. Việc đảm bảo tính xác thực và khả năng truy xuất nguồn gốc của các tài liệu này là rất quan trọng trong nhiều môi trường chuyên nghiệp. Một cách hiệu quả để đạt được điều này là nhúng siêu dữ liệu vào chính các tệp PDF.

Trong hướng dẫn toàn diện này, chúng ta sẽ khám phá cách ký tài liệu PDF bằng siêu dữ liệu bằng GroupDocs.Signature cho .NET. Chữ ký siêu dữ liệu cho phép bạn nhúng thông tin bổ sung vào tài liệu, chẳng hạn như thông tin tác giả, dấu thời gian tạo, mã định danh tài liệu và giá trị tùy chỉnh, mà không làm thay đổi rõ rệt giao diện của tài liệu.

## Điều kiện tiên quyết

Trước khi bắt đầu, hãy đảm bảo bạn đã chuẩn bị những thứ sau:

1. [GroupDocs.Signature cho .NET](https://releases.groupdocs.com/signature/net/) - Tải xuống và cài đặt thư viện
2. Môi trường phát triển - Visual Studio hoặc bất kỳ IDE nào khác tương thích với .NET
3. Tài liệu PDF - Một tệp PDF mẫu để ký
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

Đầu tiên, hãy xác định đường dẫn đến tài liệu PDF của bạn và chỉ định nơi bạn muốn lưu đầu ra đã ký:

```csharp
// Chỉ định đường dẫn đến tài liệu PDF của bạn
string filePath = "sample.pdf";

// Xác định thư mục đầu ra và đường dẫn tệp
string outputDirectory = "Your Document Directory";
string outputFilePath = Path.Combine(outputDirectory, "SignPdfWithMetadata", "SignedWithMetadata.pdf");

// Đảm bảo thư mục đầu ra tồn tại
Directory.CreateDirectory(Path.GetDirectoryName(outputFilePath));
```

## Bước 2: Khởi tạo đối tượng chữ ký

Tạo một phiên bản của lớp Signature với tài liệu PDF nguồn của bạn:

```csharp
using (Signature signature = new Signature(filePath))
{
    // Mã để ký sẽ ở đây
}
```

## Bước 3: Xác định tùy chọn siêu dữ liệu

Tạo và cấu hình các tùy chọn siêu dữ liệu, thêm nhiều loại chữ ký siêu dữ liệu khác nhau:

```csharp
// Tạo đối tượng tùy chọn siêu dữ liệu
MetadataSignOptions options = new MetadataSignOptions();

// Thêm nhiều loại siêu dữ liệu khác nhau bằng giao diện Fluent
options
    .Add(new PdfMetadataSignature("Author", "Mr.Sherlock Holmes")) // Giá trị chuỗi
    .Add(new PdfMetadataSignature("CreatedOn", DateTime.Now))       // Giá trị DateTime
    .Add(new PdfMetadataSignature("DocumentId", 123456))            // Giá trị số nguyên
    .Add(new PdfMetadataSignature("SignatureId", 123.456D))         // Giá trị kép
    .Add(new PdfMetadataSignature("Amount", 123.456M))              // Giá trị thập phân
    .Add(new PdfMetadataSignature("Total", 123.456F));              // Giá trị float
```

## Bước 4: Ký PDF bằng Siêu dữ liệu

Áp dụng chữ ký siêu dữ liệu vào tài liệu PDF và lưu kết quả:

```csharp
// Ký tài liệu và lưu vào đường dẫn đầu ra
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

namespace SignPdfWithMetadataExample
{
    class Program
    {
        static void Main(string[] args)
        {
            // Chỉ định đường dẫn tệp
            string filePath = "sample.pdf";
            string outputFilePath = Path.Combine("Your Document Directory", "SignPdfWithMetadata", "SignedWithMetadata.pdf");
            
            // Đảm bảo thư mục đầu ra tồn tại
            Directory.CreateDirectory(Path.GetDirectoryName(outputFilePath));

            // Ký PDF bằng siêu dữ liệu
            using (Signature signature = new Signature(filePath))
            {
                // Tạo đối tượng tùy chọn siêu dữ liệu
                MetadataSignOptions options = new MetadataSignOptions();
                
                // Thêm các loại chữ ký siêu dữ liệu khác nhau
                options
                    .Add(new PdfMetadataSignature("Author", "Mr.Sherlock Holmes")) // Giá trị chuỗi
                    .Add(new PdfMetadataSignature("CreatedOn", DateTime.Now))       // Giá trị DateTime
                    .Add(new PdfMetadataSignature("DocumentId", 123456))            // Giá trị số nguyên
                    .Add(new PdfMetadataSignature("SignatureId", 123.456D))         // Giá trị kép
                    .Add(new PdfMetadataSignature("Amount", 123.456M))              // Giá trị thập phân
                    .Add(new PdfMetadataSignature("Total", 123.456F));              // Giá trị float
                
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

## Các thao tác siêu dữ liệu PDF nâng cao

### Thêm siêu dữ liệu tùy chỉnh với hỗ trợ không gian tên

Tài liệu PDF hỗ trợ siêu dữ liệu tùy chỉnh với hỗ trợ không gian tên XML:

```csharp
// Thêm siêu dữ liệu tùy chỉnh với không gian tên
options.Add(new PdfMetadataSignature("CustomProperty", "Custom Value")
{
    NamespaceUri = "http://your-namespace.com/schema"
});
```

### Tìm kiếm siêu dữ liệu trong tệp PDF đã ký

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

### Làm việc với siêu dữ liệu PDF chuẩn

Tài liệu PDF có các trường siêu dữ liệu chuẩn có thể được truy cập và sửa đổi:

```csharp
// Đặt trường siêu dữ liệu PDF chuẩn
options
    .Add(new PdfMetadataSignature("Title", "Important Contract"))
    .Add(new PdfMetadataSignature("Subject", "Legal Agreement"))
    .Add(new PdfMetadataSignature("Keywords", "contract, agreement, legal, binding"))
    .Add(new PdfMetadataSignature("Creator", "Legal Department"))
    .Add(new PdfMetadataSignature("Producer", "GroupDocs.Signature"));
```

## Phần kết luận

Trong hướng dẫn này, bạn đã học cách ký tài liệu PDF bằng siêu dữ liệu bằng GroupDocs.Signature cho .NET. Việc nhúng siêu dữ liệu vào tệp PDF là một cách tuyệt vời để tăng cường tính xác thực của tài liệu, bổ sung thông tin quan trọng và cải thiện quy trình quản lý tài liệu.

Chữ ký siêu dữ liệu trong PDF đặc biệt có giá trị trong môi trường kinh doanh, nơi việc truy xuất nguồn gốc và xác minh tính xác thực của tài liệu là vô cùng quan trọng. Siêu dữ liệu nhúng có thể bao gồm thông tin về nguồn gốc, tác giả, thời gian tạo, phiên bản và các thuộc tính tùy chỉnh liên quan đến quy trình làm việc của tổ chức bạn.

Bằng cách triển khai chữ ký siêu dữ liệu với GroupDocs.Signature, bạn có thể đảm bảo tài liệu PDF của mình duy trì tính toàn vẹn và cung cấp thông tin có thể xác minh trong suốt vòng đời của chúng.

## Câu hỏi thường gặp

### Tôi có thể sửa đổi siêu dữ liệu hiện có trong tài liệu PDF không?

Có, bạn có thể chỉnh sửa siêu dữ liệu hiện có trong tài liệu PDF. Khi bạn áp dụng chữ ký siêu dữ liệu mới có cùng tên với chữ ký hiện có, các giá trị sẽ được cập nhật tương ứng.

### Người dùng cuối có thể nhìn thấy chữ ký siêu dữ liệu trong tài liệu PDF không?

Chữ ký siêu dữ liệu không hiển thị trong nội dung tài liệu. Tuy nhiên, bạn có thể xem chúng thông qua bảng thuộc tính tài liệu trong các trình đọc PDF như Adobe Acrobat hoặc sử dụng các công cụ chuyên dụng để xem siêu dữ liệu.

### Tôi có thể mã hóa hoặc bảo vệ siêu dữ liệu trong tệp PDF không?

GroupDocs.Signature cung cấp các tùy chọn bảo mật tài liệu, bao gồm mã hóa. Bạn có thể áp dụng mã hóa cấp độ tài liệu để bảo vệ toàn bộ tệp PDF, bao gồm cả siêu dữ liệu của tệp.

### Có giới hạn về số lượng siêu dữ liệu tôi có thể thêm vào PDF không?

Mặc dù không có giới hạn nghiêm ngặt nào được áp dụng theo đặc tả PDF, việc thêm quá nhiều siêu dữ liệu có thể làm tăng kích thước tệp. Bạn nên chỉ đưa thông tin liên quan và cần thiết vào siêu dữ liệu.

### Tôi có thể xác thực theo chương trình xem tệp PDF có bị giả mạo sau khi thêm siêu dữ liệu không?

Có, GroupDocs.Signature cung cấp khả năng xác minh có thể giúp phát hiện xem tài liệu có bị sửa đổi sau khi ký hay không, bao gồm cả những thay đổi đối với siêu dữ liệu.

### Tôi có thể tìm thêm tài nguyên và hỗ trợ ở đâu?

- [Tài liệu tham khảo API](https://reference.groupdocs.com/signature/net/)
- [Tải xuống](https://releases.groupdocs.com/signature/net/)
- [Ví dụ](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
- [Tài liệu](https://docs.groupdocs.com/signature/net/)
- [Trang sản phẩm](https://products.groupdocs.com/signature/net/)
- [Blog](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
- [Diễn đàn hỗ trợ](https://forum.groupdocs.com/c/signature/13)
- [Giấy phép tạm thời](https://purchase.groupdocs.com/temporary-license/)