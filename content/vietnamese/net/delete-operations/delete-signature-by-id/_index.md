---
title: Xóa chữ ký theo ID
linktitle: Xóa chữ ký theo ID
second_title: API GroupDocs.Signature .NET
description: Tìm hiểu cách xóa chữ ký theo ID trong tài liệu .NET bằng thư viện GroupDocs.Signature. Hướng dẫn từng bước dễ dàng.
type: docs
weight: 11
url: /vi/net/delete-operations/delete-signature-by-id/
---
## Giới thiệu
Trong hướng dẫn này, chúng ta sẽ khám phá cách xóa chữ ký theo ID của nó bằng GroupDocs.Signature cho .NET. GroupDocs.Signature for .NET là một thư viện mạnh mẽ cho phép các nhà phát triển thêm, xóa hoặc xác minh chữ ký số ở nhiều định dạng tài liệu khác nhau bằng ứng dụng .NET.
## Điều kiện tiên quyết
Trước khi chúng tôi bắt đầu, hãy đảm bảo bạn có các điều kiện tiên quyết sau:
1.  GroupDocs.Signature for .NET Library: Tải xuống và cài đặt thư viện từ[đây](https://releases.groupdocs.com/signature/net/).
2. .NET Framework: Đảm bảo bạn đã cài đặt .NET Framework trên hệ thống của mình.
3. Tài liệu có chữ ký: Chuẩn bị một tài liệu (ví dụ: DOCX, PDF) có chữ ký mà bạn muốn xóa.

## Nhập không gian tên
```csharp
using System;
using System.IO;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## Bước 1: Xác định đường dẫn tệp
Đầu tiên, chỉ định đường dẫn tệp cho tài liệu chứa chữ ký và đường dẫn tệp đầu ra nơi tài liệu đã sửa đổi sẽ được lưu.
```csharp
string filePath = "sample_multiple_signatures.docx";
string fileName = Path.GetFileName(filePath);
string outputFilePath = Path.Combine("Your Document Directory", "DeleteById", fileName);
```
## Bước 2: Sao chép tài liệu
 Kể từ khi`Delete` phương pháp sửa đổi tài liệu tại chỗ, tốt nhất nên tạo một bản sao của tài liệu gốc.
```csharp
File.Copy(filePath, outputFilePath, true);
```
## Bước 3: Xóa chữ ký theo ID
 Khởi tạo`Signature` đối tượng bằng đường dẫn tệp tài liệu và sử dụng`Delete` phương pháp xóa chữ ký bằng ID của nó.
```csharp
using (Signature signature = new Signature(outputFilePath))
{
    string id = @"eff64a14-dad9-47b0-88e5-2ee4e3604e71";
    bool result = signature.Delete(id);
    if (result)
    {
        Console.WriteLine($"Signature with Id# '{id}' was deleted from document ['{fileName}'].");
    }
    else
    {
        Helper.WriteError($"Signature was not deleted from the document! Signature with id# '{id}' was not found!");
    }
}
```

## Phần kết luận
Trong hướng dẫn này, chúng ta đã học cách xóa chữ ký theo ID của nó bằng GroupDocs.Signature cho .NET. Thư viện này cung cấp một cách thuận tiện để quản lý chữ ký số ở các định dạng tài liệu khác nhau theo chương trình.
## Câu hỏi thường gặp
### Tôi có thể xóa nhiều chữ ký cùng một lúc không?
 Có, bạn có thể xóa nhiều chữ ký bằng cách duyệt qua ID của chúng và gọi`Delete` phương pháp cho mỗi ID.
### GroupDocs.Signature cho .NET có tương thích với tất cả các định dạng tài liệu không?
GroupDocs.Signature cho .NET hỗ trợ nhiều định dạng tài liệu, bao gồm PDF, DOCX, XLSX, v.v.
### Tôi có thể tùy chỉnh hình thức của chữ ký không?
Có, bạn có thể tùy chỉnh giao diện của chữ ký, bao gồm vị trí, kích thước, phông chữ và màu sắc.
### Có sẵn phiên bản dùng thử không?
 Có, bạn có thể tải xuống phiên bản dùng thử miễn phí từ[đây](https://releases.groupdocs.com/).
### Tôi có thể tìm trợ giúp hoặc hỗ trợ cho GroupDocs.Signature cho .NET ở đâu?
 Bạn có thể truy cập diễn đàn hỗ trợ[đây](https://forum.groupdocs.com/c/signature/13) để được hỗ trợ.