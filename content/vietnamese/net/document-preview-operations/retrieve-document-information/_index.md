---
title: Truy xuất thông tin tài liệu
linktitle: Truy xuất thông tin tài liệu
second_title: API GroupDocs.Signature .NET
description: Tăng cường quản lý tài liệu trong .NET với GroupDocs.Signature. Truy xuất thông tin tài liệu từng bước. Hỗ trợ các định dạng khác nhau.
type: docs
weight: 11
url: /vi/net/document-preview-operations/retrieve-document-information/
---
## Giới thiệu
Trong lĩnh vực tài liệu kỹ thuật số, việc đảm bảo tính xác thực và toàn vẹn là điều tối quan trọng. GroupDocs.Signature cho .NET cung cấp giải pháp mạnh mẽ để quản lý chữ ký tài liệu trong môi trường .NET. Trong hướng dẫn này, chúng tôi đi sâu vào quy trình truy xuất thông tin tài liệu bằng GroupDocs.Signature cho .NET, chia nhỏ từng bước để hiểu toàn diện.
## Điều kiện tiên quyết
Trước khi đi sâu vào hướng dẫn, hãy đảm bảo bạn có sẵn các điều kiện tiên quyết sau:
1.  Cài đặt: Cài đặt GroupDocs.Signature cho .NET bằng cách tải xuống từ[đây](https://releases.groupdocs.com/signature/net/).
2. Môi trường .NET: Có kiến thức làm việc về .NET framework.
3. Tài liệu: Chuẩn bị một tài liệu mẫu (ví dụ: "sample_multiple_signatures.docx") cho mục đích thử nghiệm.

## Nhập không gian tên
Trước khi tiếp tục quá trình truy xuất chữ ký tài liệu, hãy nhập các không gian tên cần thiết:
```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
```

## Bước 1: Đặt đường dẫn tệp tài liệu:
Xác định đường dẫn tệp cho tài liệu bạn định lấy thông tin từ đó.
```csharp
string filePath = "sample_multiple_signatures.docx";
```
## Bước 2: Khởi tạo đối tượng chữ ký:
 Tạo một thể hiện của`Signature` class bằng cách chuyển đường dẫn tệp tài liệu.
```csharp
using (Signature signature = new Signature(filePath))
{

}
```
## Bước 3: Truy xuất thông tin tài liệu:
 Sử dụng`GetDocumentInfo()` phương pháp để lấy thông tin toàn diện về tài liệu.
```csharp
IDocumentInfo documentInfo = signature.GetDocumentInfo();
```
## Bước 4: Hiển thị thuộc tính tài liệu:
Xuất ra các thuộc tính khác nhau của tài liệu như định dạng, phần mở rộng, kích thước, số trang, v.v.
```csharp
Console.WriteLine($"Document properties {Path.GetFileName(filePath)}:");
Console.WriteLine($" - format : {documentInfo.FileType.FileFormat}");
Console.WriteLine($" - extension : {documentInfo.FileType.Extension}");
Console.WriteLine($" - size : {documentInfo.Size}");
Console.WriteLine($" - page count : {documentInfo.PageCount}");
Console.WriteLine($" - Form Fields count : {documentInfo.FormFields.Count}");
Console.WriteLine($" - Text signatures count : {documentInfo.TextSignatures.Count}");
Console.WriteLine($" - Image signatures count : {documentInfo.ImageSignatures.Count}");
Console.WriteLine($" - Digital signatures count : {documentInfo.DigitalSignatures.Count}");
Console.WriteLine($" - Barcode signatures count : {documentInfo.BarcodeSignatures.Count}");
Console.WriteLine($" - QrCode signatures count : {documentInfo.QrCodeSignatures.Count}");
Console.WriteLine($" - FormField signatures count : {documentInfo.FormFieldSignatures.Count}");
foreach (PageInfo pageInfo in documentInfo.Pages)
{
   Console.WriteLine($" - page-{pageInfo.PageNumber} Width {pageInfo.Width}, Height {pageInfo.Height}");
}
```


## Phần kết luận
GroupDocs.Signature cho .NET cung cấp một bộ công cụ mạnh mẽ để quản lý chữ ký tài liệu một cách liền mạch trong khung .NET. Bằng cách làm theo các bước được nêu trong hướng dẫn này, bạn có thể truy xuất thông tin toàn diện về tài liệu của mình một cách hiệu quả, tạo điều kiện thuận lợi cho khả năng quản lý tài liệu nâng cao.

## Câu hỏi thường gặp
### GroupDocs.Signature cho .NET có thể xử lý nhiều định dạng tài liệu không?
Có, GroupDocs.Signature hỗ trợ nhiều định dạng tài liệu, bao gồm nhưng không giới hạn ở DOCX, PDF, PNG và JPEG.
### Có phiên bản dùng thử của GroupDocs.Signature cho .NET không?
 Có, bạn có thể truy cập phiên bản dùng thử từ[đây](https://releases.groupdocs.com/).
### GroupDocs.Signature cho .NET có hỗ trợ chữ ký số không?
Hoàn toàn có thể, GroupDocs.Signature cung cấp sự hỗ trợ mạnh mẽ cho chữ ký số, đảm bảo tính xác thực và toàn vẹn của tài liệu.
### Tôi có thể tìm tài liệu bổ sung và hỗ trợ cho GroupDocs.Signature cho .NET ở đâu?
 Bạn có thể tham khảo tài liệu đầy đủ[đây](https://reference.groupdocs.com/signature/net/) và để được hỗ trợ, hãy truy cập diễn đàn GroupDocs[đây](https://forum.groupdocs.com/c/signature/13).
### Có thể lấy giấy phép tạm thời cho GroupDocs.Signature cho .NET không?
 Có, giấy phép tạm thời có sẵn để mua[đây](https://purchase.groupdocs.com/temporary-license/).