---
"description": "Bảo vệ và cải thiện bảng tính Excel bằng cách nhúng chữ ký siêu dữ liệu bằng GroupDocs.Signature cho .NET. Thêm thông tin tác giả, dấu thời gian và dữ liệu tùy chỉnh để cải thiện khả năng truy xuất nguồn gốc và tính xác thực của tài liệu."
"linktitle": "Ký bảng tính với siêu dữ liệu"
"second_title": "API GroupDocs.Signature .NET"
"title": "Thêm chữ ký siêu dữ liệu vào bảng tính Excel trong C# .NET"
"url": "/vi/net/document-signing/sign-spreadsheet-with-metadata/"
"weight": 13
type: docs
---
## Giới thiệu

Bảng tính Excel thường chứa dữ liệu kinh doanh quan trọng, thông tin tài chính và các phép tính quan trọng. Việc đảm bảo tính xác thực, truy xuất nguồn gốc và bảo vệ tính toàn vẹn của chúng là rất quan trọng trong nhiều môi trường chuyên nghiệp. Một cách tiếp cận hiệu quả để tăng cường bảo mật và khả năng truy xuất nguồn gốc của bảng tính là nhúng chữ ký siêu dữ liệu.

Hướng dẫn toàn diện này sẽ hướng dẫn bạn quy trình ký siêu dữ liệu vào bảng tính Excel bằng GroupDocs.Signature cho .NET. Bằng cách thêm chữ ký siêu dữ liệu, bạn có thể nhúng thông tin quan trọng như chi tiết tác giả, dấu thời gian tạo, mã định danh tài liệu và các thuộc tính tùy chỉnh khác trực tiếp vào cấu trúc tệp bảng tính.

## Điều kiện tiên quyết

Trước khi thực hiện hướng dẫn này, hãy đảm bảo bạn có những điều sau:

1. [GroupDocs.Signature cho .NET](https://releases.groupdocs.com/signature/net/) - Tải xuống và cài đặt thư viện
2. Môi trường phát triển - Visual Studio hoặc bất kỳ IDE nào khác tương thích với .NET
3. Bảng tính Excel - Một tệp bảng tính mẫu (XLSX, XLS, v.v.)
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

Xác định đường dẫn cho bảng tính nguồn của bạn và nơi lưu đầu ra đã ký:

```csharp
// Chỉ định đường dẫn đến tệp Excel của bạn
string filePath = "sample.xlsx";

// Xác định thư mục đầu ra và tên tệp cho bảng tính đã ký
string outputDirectory = "Your Document Directory";
string outputFilePath = Path.Combine(outputDirectory, "SignSpreadsheetWithMetadata", "SignedWithMetadata.xlsx");

// Đảm bảo thư mục đầu ra tồn tại
Directory.CreateDirectory(Path.GetDirectoryName(outputFilePath));
```

## Bước 2: Khởi tạo đối tượng chữ ký

Tạo một phiên bản của lớp Signature với tệp bảng tính nguồn của bạn:

```csharp
using (Signature signature = new Signature(filePath))
{
    // Phần còn lại của mã sẽ ở đây
}
```

## Bước 3: Tạo và cấu hình chữ ký siêu dữ liệu

Tiếp theo, hãy xác định các tùy chọn siêu dữ liệu và tạo một mảng chữ ký siêu dữ liệu bảng tính:

```csharp
// Tạo đối tượng tùy chọn siêu dữ liệu
MetadataSignOptions options = new MetadataSignOptions();

// Tạo một mảng chữ ký siêu dữ liệu bảng tính với các kiểu dữ liệu khác nhau
SpreadsheetMetadataSignature[] signatures = new SpreadsheetMetadataSignature[]
{
    new SpreadsheetMetadataSignature("Author", "Mr.Sherlock Holmes"), // Giá trị chuỗi
    new SpreadsheetMetadataSignature("CreatedOn", DateTime.Now),      // Giá trị DateTime
    new SpreadsheetMetadataSignature("DocumentId", 123456),           // Giá trị số nguyên
    new SpreadsheetMetadataSignature("SignatureId", 123.456D),        // Giá trị kép
    new SpreadsheetMetadataSignature("Amount", 123.456M),             // Giá trị thập phân
    new SpreadsheetMetadataSignature("Total", 123.456F)               // Giá trị float
};

// Thêm bộ sưu tập chữ ký vào tùy chọn
options.Signatures.AddRange(signatures);
```

## Bước 4: Ký bảng tính bằng siêu dữ liệu

Áp dụng chữ ký siêu dữ liệu vào bảng tính và lưu kết quả:

```csharp
// Ký tài liệu và lưu vào đường dẫn tệp đầu ra
SignResult result = signature.Sign(outputFilePath, options);

// Hiển thị thông báo thành công
Console.WriteLine($"\nSource spreadsheet signed successfully with {result.Succeeded.Count} metadata signature(s).");
Console.WriteLine($"Signed spreadsheet saved at: {outputFilePath}");
```

## Ví dụ đầy đủ

Sau đây là ví dụ mã hoàn chỉnh kết hợp tất cả các bước:

```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;

namespace SignSpreadsheetWithMetadataExample
{
    class Program
    {
        static void Main(string[] args)
        {
            // Chỉ định đường dẫn tệp
            string filePath = "sample.xlsx";
            string outputFilePath = Path.Combine("Your Document Directory", "SignSpreadsheetWithMetadata", "SignedWithMetadata.xlsx");
            
            // Đảm bảo thư mục đầu ra tồn tại
            Directory.CreateDirectory(Path.GetDirectoryName(outputFilePath));

            // Ký bảng tính bằng siêu dữ liệu
            using (Signature signature = new Signature(filePath))
            {
                // Tạo đối tượng tùy chọn siêu dữ liệu
                MetadataSignOptions options = new MetadataSignOptions();
                
                // Tạo một mảng chữ ký siêu dữ liệu bảng tính với các kiểu dữ liệu khác nhau
                SpreadsheetMetadataSignature[] signatures = new SpreadsheetMetadataSignature[]
                {
                    new SpreadsheetMetadataSignature("Author", "Mr.Sherlock Holmes"), // Giá trị chuỗi
                    new SpreadsheetMetadataSignature("CreatedOn", DateTime.Now),      // Giá trị DateTime
                    new SpreadsheetMetadataSignature("DocumentId", 123456),           // Giá trị số nguyên
                    new SpreadsheetMetadataSignature("SignatureId", 123.456D),        // Giá trị kép
                    new SpreadsheetMetadataSignature("Amount", 123.456M),             // Giá trị thập phân
                    new SpreadsheetMetadataSignature("Total", 123.456F)               // Giá trị float
                };
                
                // Thêm bộ sưu tập chữ ký vào tùy chọn
                options.Signatures.AddRange(signatures);
                
                // Ký tài liệu và lưu vào hồ sơ
                SignResult result = signature.Sign(outputFilePath, options);
                
                // Hiển thị kết quả
                Console.WriteLine($"\nSource spreadsheet signed successfully with {result.Succeeded.Count} signature(s).");
                Console.WriteLine($"File saved at {outputFilePath}.");
            }
        }
    }
}
```

## Kỹ thuật siêu dữ liệu bảng tính nâng cao

### Làm việc với các thuộc tính bảng tính tùy chỉnh và tích hợp sẵn

Bảng tính Excel có cả thuộc tính tích hợp và thuộc tính tùy chỉnh có thể được truy cập thông qua hộp thoại thuộc tính tệp. GroupDocs.Signature cho phép bạn làm việc với cả hai:

```csharp
// Thêm các thuộc tính tích hợp
signatures = new SpreadsheetMetadataSignature[]
{
    new SpreadsheetMetadataSignature("Company", "Sherlock Holmes Consulting"),
    new SpreadsheetMetadataSignature("Category", "Financial"),
    new SpreadsheetMetadataSignature("Keywords", "budget,forecast,analysis"),
    new SpreadsheetMetadataSignature("Comments", "This spreadsheet contains confidential information"),
    new SpreadsheetMetadataSignature("Manager", "John Watson")
};
options.Signatures.AddRange(signatures);

// Thêm thuộc tính tùy chỉnh
options.Signatures.Add(new SpreadsheetMetadataSignature("Department", "Finance"));
options.Signatures.Add(new SpreadsheetMetadataSignature("SecurityLevel", "Confidential"));
```

### Tìm kiếm siêu dữ liệu trong bảng tính đã ký

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

### Cập nhật siêu dữ liệu hiện có

Bạn có thể cập nhật siêu dữ liệu hiện có trong bảng tính bằng cách sử dụng cùng tên thuộc tính:

```csharp
// Cập nhật siêu dữ liệu hiện có
options.Signatures.Add(new SpreadsheetMetadataSignature("Author", "Updated Author Name"));
```

## Phần kết luận

Trong hướng dẫn toàn diện này, bạn đã học cách ký bảng tính Excel bằng siêu dữ liệu bằng GroupDocs.Signature cho .NET. Việc nhúng siêu dữ liệu vào tệp bảng tính giúp tăng cường khả năng truy xuất nguồn gốc tài liệu, cung cấp ngữ cảnh có giá trị và giúp xác định tính xác thực.

Chữ ký siêu dữ liệu trong bảng tính đặc biệt hữu ích trong môi trường kinh doanh, nơi nguồn gốc tài liệu, quyền tác giả và theo dõi phiên bản là rất quan trọng. Siêu dữ liệu nhúng có thể bao gồm thông tin về tác giả, thời gian tạo, mã định danh tài liệu và các thuộc tính tùy chỉnh phù hợp với nhu cầu của tổ chức bạn.

Bằng cách triển khai chữ ký siêu dữ liệu với GroupDocs.Signature, bạn có thể đảm bảo bảng tính Excel của mình duy trì tính toàn vẹn và cung cấp thông tin có thể xác minh trong suốt vòng đời của chúng.

## Câu hỏi thường gặp

### Tôi có thể thêm siêu dữ liệu vào bảng tính đã xác định một số thuộc tính không?

Có, bạn có thể thêm siêu dữ liệu mới hoặc cập nhật siêu dữ liệu hiện có trong bảng tính. GroupDocs.Signature sẽ xử lý việc tích hợp, bằng cách thêm thuộc tính mới hoặc cập nhật các thuộc tính hiện có có cùng tên.

### Định dạng bảng tính nào được hỗ trợ để ký siêu dữ liệu?

GroupDocs.Signature cho .NET hỗ trợ ký siêu dữ liệu cho nhiều định dạng bảng tính khác nhau, bao gồm XLSX, XLS, XLSM, ODS, v.v. Để biết danh sách đầy đủ, hãy tham khảo [tài liệu chính thức](https://docs.groupdocs.com/signature/net/).

### Chữ ký siêu dữ liệu trong bảng tính có hiển thị cho người dùng không?

Chữ ký siêu dữ liệu không hiển thị trong nội dung bảng tính. Tuy nhiên, bạn có thể xem chúng thông qua bảng thuộc tính tài liệu trong Excel hoặc các ứng dụng tương thích khác.

### Tôi có thể xác thực theo chương trình xem bảng tính có bị giả mạo sau khi thêm siêu dữ liệu không?

Có, GroupDocs.Signature cung cấp khả năng xác minh có thể giúp phát hiện xem tài liệu có bị sửa đổi sau khi ký hay không, bao gồm cả những thay đổi đối với siêu dữ liệu.

### Việc thêm siêu dữ liệu có ảnh hưởng đến chức năng của bảng tính không?

Việc thêm siêu dữ liệu chỉ ảnh hưởng tối thiểu đến kích thước tệp và không ảnh hưởng đến chức năng của bảng tính. Đây là một cách đơn giản để cải thiện các thuộc tính của tài liệu mà không ảnh hưởng đến các phép tính, công thức hoặc các tính năng khác của Excel.

### Tôi có thể tìm thêm tài nguyên và hỗ trợ ở đâu?

- [Tài liệu tham khảo API](https://reference.groupdocs.com/signature/net/)
- [Tải xuống](https://releases.groupdocs.com/signature/net/)
- [Ví dụ](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
- [Tài liệu](https://docs.groupdocs.com/signature/net/)
- [Trang sản phẩm](https://products.groupdocs.com/signature/net/)
- [Blog](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
- [Diễn đàn hỗ trợ](https://forum.groupdocs.com/c/signature/13)
- [Giấy phép tạm thời](https://purchase.groupdocs.com/temporary-license/)