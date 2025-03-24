---
title: Hình ảnh ký hiệu với siêu dữ liệu
linktitle: Hình ảnh ký hiệu với siêu dữ liệu
second_title: API GroupDocs.Signature .NET
description: Tìm hiểu cách ký hình ảnh bằng siêu dữ liệu trong .NET bằng GroupDocs.Signature. Giải pháp ký siêu dữ liệu dễ dàng, hiệu quả và có thể tùy chỉnh.
weight: 10
url: /vi/net/document-signing/sign-image-with-metadata/
---
## Giới thiệu
GroupDocs.Signature for .NET cho phép các nhà phát triển ký hình ảnh bằng siêu dữ liệu một cách hiệu quả. Hướng dẫn này hướng dẫn bạn từng bước thực hiện quy trình.
## Điều kiện tiên quyết
Trước khi bắt đầu, hãy đảm bảo bạn có những điều sau:
1. GroupDocs.Signature cho .NET: Cài đặt gói GroupDocs.Signature trong dự án .NET của bạn. Bạn có thể tải nó xuống từ[đây](https://releases.groupdocs.com/signature/net/).   
2. Tệp hình ảnh: Chuẩn bị tệp hình ảnh mà bạn muốn ký bằng siêu dữ liệu.

## Nhập không gian tên
Đảm bảo nhập các không gian tên cần thiết trong mã C# của bạn:
```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## Bước 1: Tải tệp hình ảnh
Đầu tiên, chỉ định đường dẫn đến tệp hình ảnh của bạn và thư mục đầu ra cho hình ảnh đã ký với siêu dữ liệu:
```csharp
string filePath = "sample.png";            
string outputFilePath = Path.Combine("Your Document Directory", "SignImageWithMetadata", "SignedWithMetadata.png");
```
## Bước 2: Tạo chữ ký siêu dữ liệu
Tiếp theo, tạo các chữ ký siêu dữ liệu khác nhau và thêm chúng vào bộ sưu tập chữ ký tùy chọn:
```csharp
using (Signature signature = new Signature(filePath))
{
    ushort imgsMetadataId = 41996;
    MetadataSignOptions options = new MetadataSignOptions();
    options
        .Add(new ImageMetadataSignature(imgsMetadataId++, "Mr.Scherlock Holmes")) // Chuỗi giá trị
        .Add(new ImageMetadataSignature(imgsMetadataId++, DateTime.Now))          // Giá trị ngày giờ
        .Add(new ImageMetadataSignature(imgsMetadataId++, 123456))                // Giá trị số nguyên
        .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456D))              // Giá trị kép
        .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456M))              // Giá trị thập phân
        .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456F));             // Giá trị nổi
    
    // ký tài liệu vào tập tin
    SignResult result = signature.Sign(outputFilePath, options);
    Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).\nFile saved at {outputFilePath}.");
}
```

## Phần kết luận
Trong hướng dẫn này, bạn đã học cách ký một hình ảnh bằng siêu dữ liệu bằng GroupDocs.Signature cho .NET. Bằng cách làm theo các bước này, bạn có thể dễ dàng kết hợp chữ ký siêu dữ liệu vào các ứng dụng .NET của mình.

## Câu hỏi thường gặp
### Tôi có thể ký nhiều hình ảnh bằng siêu dữ liệu bằng GroupDocs.Signature cho .NET không?
Có, bạn có thể ký nhiều hình ảnh bằng siêu dữ liệu bằng cách lặp qua từng tệp hình ảnh và áp dụng chữ ký siêu dữ liệu.
### Có phiên bản dùng thử của GroupDocs.Signature cho .NET không?
 Có, bạn có thể tải xuống phiên bản dùng thử từ[đây](https://releases.groupdocs.com/).
### GroupDocs.Signature cho .NET có hỗ trợ các định dạng tệp khác ngoài hình ảnh không?
Có, GroupDocs.Signature hỗ trợ nhiều định dạng tệp khác nhau, bao gồm PDF, Word, Excel, v.v.
### Tôi có thể tùy chỉnh giao diện của chữ ký siêu dữ liệu không?
Có, bạn có thể tùy chỉnh hình thức của chữ ký siêu dữ liệu, chẳng hạn như kích thước phông chữ, màu sắc và vị trí.
### Tôi có thể nhận hỗ trợ cho GroupDocs.Signature cho .NET ở đâu?
 Bạn có thể nhận hỗ trợ từ diễn đàn GroupDocs.Signature[đây](https://forum.groupdocs.com/c/signature/13).