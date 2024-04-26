---
title: Xóa chữ ký mã QR khỏi tài liệu
linktitle: Xóa chữ ký mã QR khỏi tài liệu
second_title: API GroupDocs.Signature .NET
description: Tìm hiểu cách xóa chữ ký mã QR khỏi tài liệu bằng GroupDocs.Signature cho .NET. Hãy làm theo hướng dẫn từng bước của chúng tôi để quản lý chữ ký hiệu quả.
type: docs
weight: 16
url: /vi/net/delete-operations/delete-qr-code-signature/
---
## Giới thiệu
Trong hướng dẫn này, chúng tôi sẽ hướng dẫn bạn quy trình xóa chữ ký mã QR khỏi tài liệu bằng GroupDocs.Signature cho .NET. Hãy làm theo các hướng dẫn từng bước sau để xóa chữ ký mã QR một cách hiệu quả.
## Điều kiện tiên quyết
Trước khi bắt đầu, hãy đảm bảo bạn có các điều kiện tiên quyết sau:
-  GroupDocs.Signature dành cho .NET: Đảm bảo bạn đã cài đặt thư viện GroupDocs.Signature trong dự án .NET của mình. Bạn có thể tải nó xuống từ[đây](https://releases.groupdocs.com/signature/net/).
- Tài liệu có chữ ký mã QR: Chuẩn bị tài liệu có chứa chữ ký mã QR mà bạn muốn xóa.
- Kiến thức cơ bản về C#: Làm quen với những kiến thức cơ bản về ngôn ngữ lập trình C#.

## Nhập không gian tên
Trước khi đi sâu vào mã, hãy nhập các vùng tên cần thiết vào tệp C# của bạn:
```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## Bước 1: Xác định đường dẫn tệp
```csharp
// Đường dẫn đến thư mục tài liệu.
string filePath = "sample_multiple_signatures.docx";
string fileName = Path.GetFileName(filePath);
// Xác định đường dẫn tệp đầu ra cho tài liệu đã sửa đổi.
string outputFilePath = Path.Combine("Your Document Directory", "DeleteQRCode", fileName);
// Sao chép tệp nguồn vì phương thức Xóa hoạt động với cùng một Tài liệu.
File.Copy(filePath, outputFilePath, true);
```
## Bước 2: Khởi tạo đối tượng chữ ký
```csharp
using (Signature signature = new Signature(outputFilePath))
{
    // Tạo các tùy chọn tìm kiếm chữ ký mã QR.
    QrCodeSearchOptions options = new QrCodeSearchOptions();
    // Tìm kiếm chữ ký mã QR trong tài liệu.
    List<QrCodeSignature> signatures = signature.Search<QrCodeSignature>(options);
```
## Bước 3: Kiểm tra sự tồn tại của chữ ký mã QR
```csharp
    if (signatures.Count > 0)
    {
        // Nhận chữ ký mã QR đầu tiên được tìm thấy trong tài liệu.
        QrCodeSignature qrCodeSignature = signatures[0];
```
## Bước 4: Xóa chữ ký mã QR
```csharp
        // Xóa chữ ký mã QR khỏi tài liệu.
        bool result = signature.Delete(qrCodeSignature);
        if (result)
        {
            Console.WriteLine($"Signature with QR-Code '{qrCodeSignature.Text}' and encode type '{qrCodeSignature.EncodeType.TypeName}' was deleted from document ['{fileName}'].");
        }
        else
        {
            Helper.WriteError($"Signature was not deleted from the document! Signature with Barcode '{qrCodeSignature.Text}' and encode type '{qrCodeSignature.EncodeType.TypeName}' was not found!");
        }
    }
}
```
Chúc mừng! Bạn đã xóa thành công chữ ký mã QR khỏi tài liệu bằng GroupDocs.Signature cho .NET.

## Phần kết luận
Trong hướng dẫn này, chúng ta đã tìm hiểu cách xóa chữ ký mã QR khỏi tài liệu bằng GroupDocs.Signature cho .NET. Bằng cách làm theo các bước được cung cấp, bạn có thể quản lý và thao tác chữ ký một cách hiệu quả trong các ứng dụng .NET của mình.
## Câu hỏi thường gặp
### Tôi có thể xóa nhiều chữ ký mã QR khỏi một tài liệu không?
Có, bạn có thể sửa đổi mã để lặp lại tất cả các chữ ký mã QR và xóa chúng cho phù hợp.
### GroupDocs.Signature có hỗ trợ các loại chữ ký khác ngoài mã QR không?
Có, GroupDocs.Signature hỗ trợ nhiều loại chữ ký khác nhau như văn bản, hình ảnh, mã vạch, v.v.
### GroupDocs.Signature có tương thích với tất cả các định dạng tài liệu không?
GroupDocs.Signature hỗ trợ nhiều định dạng tài liệu bao gồm PDF, Microsoft Word, Excel, PowerPoint, v.v.
### Tôi có thể tùy chỉnh các tùy chọn tìm kiếm chữ ký không?
Có, bạn có thể điều chỉnh các tùy chọn tìm kiếm theo yêu cầu của mình để xác định các chữ ký cụ thể trong tài liệu.
### Có phiên bản dùng thử cho GroupDocs.Signature không?
 Có, bạn có thể truy cập phiên bản dùng thử miễn phí của GroupDocs.Signature từ[đây](https://releases.groupdocs.com/).