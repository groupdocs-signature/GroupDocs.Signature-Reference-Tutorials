---
title: Ký tài liệu bằng mã QR bằng GroupDocs.Signature
linktitle: Ký bằng mã QR
second_title: API GroupDocs.Signature .NET
description: Tìm hiểu cách thêm chữ ký mã QR vào tài liệu của bạn bằng GroupDocs.Signature cho .NET. Tăng cường bảo mật và xác thực dễ dàng.
weight: 15
url: /vi/net/advanced-signature-techniques/sign-with-qr-code/
---
## Giới thiệu
Trong hướng dẫn này, chúng ta sẽ tìm hiểu quy trình ký tài liệu bằng mã QR bằng GroupDocs.Signature cho .NET. GroupDocs.Signature cho .NET là một API mạnh mẽ cho phép các nhà phát triển thêm nhiều loại chữ ký khác nhau vào tài liệu kỹ thuật số theo chương trình. Ký tài liệu bằng mã QR có thể cung cấp thêm lớp bảo mật và xác thực cho tài liệu của bạn.
## Điều kiện tiên quyết
Trước khi chúng tôi bắt đầu, hãy đảm bảo bạn đã cài đặt các điều kiện tiên quyết sau:
1.  GroupDocs.Signature cho .NET: Bạn có thể tải xuống thư viện từ[trang mạng](https://releases.groupdocs.com/signature/net/).
2. Môi trường phát triển: Đảm bảo bạn đã thiết lập môi trường phát triển .NET trên máy của mình.
3. Tài liệu mẫu: Chuẩn bị một tài liệu mẫu (ví dụ: PDF) mà bạn muốn ký bằng mã QR.

## Nhập các không gian tên cần thiết
Trước khi đi sâu vào mã, hãy nhập các không gian tên cần thiết:
```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

## Bước 1: Xác định đường dẫn tệp
```csharp
string filePath = "sample.pdf";
string fileName = Path.GetFileName(filePath);
string outputFilePath = Path.Combine("Your Document Directory", "SignWithQRCode", fileName);
```
 Đảm bảo thay thế`"Your Document Directory"` với đường dẫn đến thư mục mà bạn muốn lưu tài liệu đã ký.
## Bước 2: Khởi tạo đối tượng chữ ký
```csharp
using (Signature signature = new Signature(filePath))
{
    //Mã để ký ở đây
}
```
 Khởi tạo một`Signature` đối tượng bằng đường dẫn đến tài liệu bạn muốn ký.
## Bước 3: Tạo QRCodeSignOptions
```csharp
QrCodeSignOptions options = new QrCodeSignOptions("JohnSmith")
{
    EncodeType = QrCodeTypes.QR,
    Left = 50,
    Top = 150,
    Width = 200,
    Height = 200
};
```
 Tạo một`QrCodeSignOptions` đối tượng có cài đặt mong muốn cho chữ ký mã QR. Bạn có thể tùy chỉnh các tham số như văn bản cần mã hóa, vị trí và kích thước của mã QR.
## Bước 4: Ký vào tài liệu
```csharp
SignResult result = signature.Sign(outputFilePath, options);
```
 Sử dụng`Sign` phương pháp của`Signature` đối tượng ký tài liệu với các tùy chọn được chỉ định. Phương thức này trả về một`SignResult` đối tượng chứa thông tin về quá trình ký.
## Bước 5: Hiển thị kết quả
```csharp
Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).\nFile saved at {outputFilePath}.");
```
Hiển thị thông báo cho biết quá trình ký đã thành công và vị trí lưu tài liệu đã ký.

## Phần kết luận
Trong hướng dẫn này, chúng ta đã tìm hiểu cách ký tài liệu bằng mã QR bằng GroupDocs.Signature cho .NET. Bằng cách làm theo các bước đơn giản này, bạn có thể thêm chữ ký mã QR vào tài liệu kỹ thuật số của mình, tăng cường bảo mật và xác thực.

## Câu hỏi thường gặp
### Tôi có thể tùy chỉnh giao diện của mã QR không?
Có, bạn có thể tùy chỉnh các thông số khác nhau như kích thước, vị trí và loại mã hóa của mã QR theo yêu cầu của mình.
### Những định dạng tài liệu nào được hỗ trợ để ký bằng mã QR?
GroupDocs.Signature cho .NET hỗ trợ nhiều định dạng tài liệu, bao gồm PDF, Word, Excel, PowerPoint, v.v.
### Có thể ký nhiều tài liệu trong một quy trình hàng loạt không?
Hoàn toàn có thể, bạn có thể sử dụng GroupDocs.Signature cho .NET để ký nhiều tài liệu cùng lúc, hợp lý hóa quy trình làm việc của bạn.
### Tôi có thể xác minh tính xác thực của tài liệu được ký bằng mã QR không?
Có, GroupDocs.Signature for .NET cung cấp cơ chế xác minh để đảm bảo tính toàn vẹn và xác thực của các tài liệu đã ký.
### Có phiên bản dùng thử để kiểm tra chức năng trước khi mua không?
 Có, bạn có thể tải xuống phiên bản dùng thử miễn phí từ[trang mạng](https://releases.groupdocs.com/) để đánh giá các tính năng và khả năng của GroupDocs.Signature cho .NET.