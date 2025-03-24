---
title: Ký bản trình bày với siêu dữ liệu
linktitle: Ký bản trình bày với siêu dữ liệu
second_title: API GroupDocs.Signature .NET
description: Tìm hiểu cách ký các tệp bản trình bày có siêu dữ liệu bằng GroupDocs.Signature cho .NET. Tăng cường tính toàn vẹn của tài liệu và thêm thông tin có giá trị.
weight: 12
url: /vi/net/document-signing/sign-presentation-with-metadata/
---
## Giới thiệu
Trong hướng dẫn này, chúng ta sẽ tìm hiểu cách ký vào tệp bản trình bày (PPTX) bằng siêu dữ liệu bằng thư viện GroupDocs.Signature cho .NET. Ký bản trình bày bằng siêu dữ liệu sẽ thêm thông tin có giá trị vào tài liệu, chẳng hạn như tên tác giả, ngày tạo, ID tài liệu, ID chữ ký và các giá trị số khác nhau.
## Điều kiện tiên quyết
Trước khi chúng ta bắt đầu, hãy đảm bảo bạn có những điều sau:
1.  GroupDocs.Signature for .NET Library: Tải xuống và cài đặt thư viện từ[đây](https://releases.groupdocs.com/signature/net/).
2. Môi trường phát triển: Đảm bảo bạn đã thiết lập môi trường phát triển .NET.
3. Tệp trình bày: Chuẩn bị sẵn tệp trình bày mẫu (định dạng PPTX) để ký.
4. Hiểu biết cơ bản về C#: Làm quen với ngôn ngữ lập trình C# sẽ có lợi.

## Nhập không gian tên
Trước khi đi sâu vào mã, hãy nhập các không gian tên cần thiết:
```csharp
using System;
using System.IO;
    using GroupDocs.Signature;
    using GroupDocs.Signature.Domain;
    using GroupDocs.Signature.Options;
```
## Bước 1: Tải tệp trình bày
```csharp
string filePath = "sample.pptx";
```
 Thay thế`"sample.pptx"` với đường dẫn đến tập tin trình bày của bạn.
## Bước 2: Chỉ định đường dẫn tệp đầu ra
```csharp
string outputFilePath = Path.Combine("Your Document Directory", "SignPresentationWithMetadata", "SignedWithMetadata.pptx");
```
Chỉ định thư mục nơi bạn muốn lưu tệp bản trình bày đã ký cùng với tên tệp.
## Bước 3: Khởi tạo đối tượng chữ ký
```csharp
using (Signature signature = new Signature(filePath))
```
Khởi tạo đối tượng Signature bằng cách cung cấp đường dẫn đến tệp trình bày.
## Bước 4: Xác định các tùy chọn ký hiệu siêu dữ liệu
```csharp
MetadataSignOptions options = new MetadataSignOptions();
```
Tạo một phiên bản MetadataSignOptions để xác định các tùy chọn ký siêu dữ liệu.
## Bước 5: Tạo chữ ký siêu dữ liệu
```csharp
PresentationMetadataSignature[] signatures = new PresentationMetadataSignature[]
{
    new PresentationMetadataSignature("Author", "Mr.Scherlock Holmes"),
    new PresentationMetadataSignature("CreatedOn", DateTime.Now),
    new PresentationMetadataSignature("DocumentId", 123456),
    new PresentationMetadataSignature("SignatureId", 123.456D),
    new PresentationMetadataSignature("Amount", 123.456M),
    new PresentationMetadataSignature("Total", 123.456F)
};
```
Tạo một mảng các đối tượng PresentMetadataSignature, mỗi đối tượng đại diện cho một chữ ký siêu dữ liệu. Bạn có thể thêm nhiều loại siêu dữ liệu khác nhau, bao gồm chuỗi, DateTime, số nguyên, double, thập phân và float.
## Bước 6: Thêm chữ ký vào tùy chọn
```csharp
options.Signatures.AddRange(signatures);
```
Thêm chữ ký siêu dữ liệu đã tạo vào đối tượng MetadataSignOptions.
## Bước 7: Ký tài liệu
```csharp
SignResult result = signature.Sign(outputFilePath, options);
```
Ký tệp bản trình bày có siêu dữ liệu bằng cách sử dụng các tùy chọn đã chỉ định và lưu tệp đã ký vào đường dẫn đầu ra.
## Bước 8: Hiển thị kết quả
```csharp
Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).\nFile saved at {outputFilePath}.");
```
Hiển thị thông báo thành công cùng với số chữ ký được áp dụng và đường dẫn lưu file đã ký.

## Phần kết luận
Trong hướng dẫn này, chúng ta đã tìm hiểu cách ký vào tệp bản trình bày có siêu dữ liệu bằng thư viện GroupDocs.Signature cho .NET. Việc thêm chữ ký siêu dữ liệu sẽ nâng cao tính toàn vẹn của tài liệu và cung cấp thông tin có giá trị về nội dung của tài liệu.

## Câu hỏi thường gặp
### Tôi có thể ký các định dạng tài liệu khác ngoài PPTX bằng siêu dữ liệu bằng GroupDocs.Signature cho .NET không?
Có, GroupDocs.Signature hỗ trợ nhiều định dạng tài liệu khác nhau, bao gồm Word, Excel, PDF, v.v., để ký bằng siêu dữ liệu.
### GroupDocs.Signature cho .NET có tương thích với .NET Core không?
Có, thư viện tương thích với cả .NET Framework và .NET Core.
### Tôi có thể tùy chỉnh giao diện của chữ ký siêu dữ liệu không?
Có, bạn có thể tùy chỉnh giao diện, vị trí và các thuộc tính khác của chữ ký siêu dữ liệu theo yêu cầu của bạn.
### GroupDocs.Signature cho .NET có cung cấp mã hóa cho các tài liệu đã ký không?
Có, GroupDocs.Signature cung cấp các tùy chọn mã hóa để bảo mật các tài liệu đã ký khỏi bị truy cập trái phép.
### Có phiên bản dùng thử để thử nghiệm trước khi mua không?
 Có, bạn có thể tận dụng bản dùng thử miễn phí GroupDocs.Signature cho .NET từ[đây](https://releases.groupdocs.com/).