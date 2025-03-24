---
title: Ký PDF bằng siêu dữ liệu
linktitle: Ký PDF bằng siêu dữ liệu
second_title: API GroupDocs.Signature .NET
description: Tìm hiểu cách ký tài liệu PDF có siêu dữ liệu bằng GroupDocs.Signature cho .NET. Tăng cường khả năng truy xuất nguồn gốc và tính xác thực của tài liệu một cách dễ dàng.
weight: 11
url: /vi/net/document-signing/sign-pdf-with-metadata/
---
## Giới thiệu
Trong hướng dẫn này, chúng ta sẽ tìm hiểu cách ký tài liệu PDF có siêu dữ liệu bằng GroupDocs.Signature cho .NET. Việc thêm siêu dữ liệu vào tệp PDF có thể cung cấp thông tin bổ sung về tài liệu, chẳng hạn như quyền tác giả, ngày tạo, ID tài liệu, v.v.
## Điều kiện tiên quyết
Trước khi chúng ta bắt đầu, hãy đảm bảo bạn có những điều sau:
1.  GroupDocs.Signature cho .NET: Bạn có thể tải xuống từ[đây](https://releases.groupdocs.com/signature/net/).
2. Tài liệu PDF: Chuẩn bị sẵn tệp PDF mẫu để ký.
3. Kiến thức cơ bản về lập trình C#: Cần phải làm quen với cú pháp C# để hiểu các ví dụ về mã.
## Nhập không gian tên
Trước tiên, hãy đảm bảo bạn nhập các không gian tên cần thiết để truy cập các lớp và phương thức được yêu cầu:
```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## Bước 1: Tải tài liệu PDF
Tải tài liệu PDF bạn muốn ký:
```csharp
string filePath = "sample.pdf";
```
## Bước 2: Chỉ định đường dẫn tệp đầu ra
Xác định đường dẫn tệp đầu ra nơi tệp PDF đã ký với siêu dữ liệu sẽ được lưu:
```csharp
string outputFilePath = Path.Combine("Your Document Directory", "SignPdfWithMetadata", "SignedWithMetadata.pdf");
```
## Bước 3: Tạo phiên bản chữ ký
Khởi tạo phiên bản Chữ ký bằng cách cung cấp đường dẫn đến tài liệu PDF:
```csharp
using (Signature signature = new Signature(filePath))
{
    // Mã liên quan đến chữ ký sẽ ở đây
}
```
## Bước 4: Xác định tùy chọn siêu dữ liệu
Tạo MetadataSignOptions và thêm các trường siêu dữ liệu với các giá trị tương ứng:
```csharp
MetadataSignOptions options = new MetadataSignOptions();
options
    .Add(new PdfMetadataSignature("Author", "Mr.Sherlock Holmes")) // Chuỗi giá trị
    .Add(new PdfMetadataSignature("CreatedOn", DateTime.Now))       // Giá trị ngày giờ
    .Add(new PdfMetadataSignature("DocumentId", 123456))            // Giá trị số nguyên
    .Add(new PdfMetadataSignature("SignatureId", 123.456D))         // Giá trị kép
    .Add(new PdfMetadataSignature("Amount", 123.456M))              // Giá trị thập phân
    .Add(new PdfMetadataSignature("Total", 123.456F));              // Giá trị nổi
```
## Bước 5: Ký vào tài liệu
Ký tài liệu PDF với các tùy chọn siêu dữ liệu được chỉ định và lưu tài liệu đã ký:
```csharp
SignResult result = signature.Sign(outputFilePath, options);
Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).\nFile saved at {outputFilePath}.");
```

## Phần kết luận
Trong hướng dẫn này, chúng tôi đã đề cập đến cách ký tài liệu PDF có siêu dữ liệu bằng GroupDocs.Signature cho .NET. Bằng cách làm theo hướng dẫn từng bước, bạn có thể dễ dàng thêm thông tin siêu dữ liệu như quyền tác giả, ngày tạo, v.v. vào tệp PDF của mình, nâng cao tiện ích và khả năng truy xuất nguồn gốc của chúng.
## Câu hỏi thường gặp
### Tôi có thể thêm các trường siêu dữ liệu tùy chỉnh vào tài liệu PDF của mình không?
Có, bạn có thể thêm các trường siêu dữ liệu tùy chỉnh bằng cách chỉ định tên trường và giá trị tương ứng của nó bằng GroupDocs.Signature cho .NET.
### GroupDocs.Signature cho .NET có tương thích với tất cả các phiên bản .NET Framework không?
GroupDocs.Signature cho .NET tương thích với nhiều phiên bản .NET Framework khác nhau, đảm bảo tính linh hoạt và dễ tích hợp.
### GroupDocs.Signature có hỗ trợ ký các định dạng tài liệu khác ngoài PDF không?
Có, GroupDocs.Signature hỗ trợ nhiều định dạng tài liệu, bao gồm Word, Excel, PowerPoint, v.v.
### Tôi có thể ký hàng loạt nhiều tài liệu bằng GroupDocs.Signature cho .NET không?
Có, bạn có thể ký hàng loạt nhiều tài liệu bằng cách duyệt qua danh sách tệp và áp dụng quy trình chữ ký theo chương trình.
### Có hỗ trợ kỹ thuật cho người dùng GroupDocs.Signature không?
 Có, GroupDocs cung cấp hỗ trợ kỹ thuật chuyên dụng thông qua các diễn đàn của mình. Bạn có thể truy cập diễn đàn hỗ trợ[đây](https://forum.groupdocs.com/c/signature/13).