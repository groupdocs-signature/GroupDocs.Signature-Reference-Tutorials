---
title: Xác minh mã QR
linktitle: Xác minh mã QR
second_title: API GroupDocs.Signature .NET
description: Tìm hiểu cách xác minh mã QR trong tài liệu bằng GroupDocs.Signature cho .NET. Hướng dẫn toàn diện với hướng dẫn từng bước.
type: docs
weight: 12
url: /vi/net/verify-operations/verify-qr-code/
---
## Giới thiệu
Trong lĩnh vực quản lý và xác thực tài liệu, việc đảm bảo tính toàn vẹn và hợp lệ của chữ ký là điều tối quan trọng. GroupDocs.Signature cho .NET cung cấp giải pháp toàn diện để xác minh mã QR được nhúng trong tài liệu. Trong hướng dẫn này, chúng ta sẽ đi sâu vào quy trình từng bước xác minh mã QR bằng GroupDocs.Signature cho .NET.
## Điều kiện tiên quyết
Trước khi đi sâu vào quy trình xác minh, hãy đảm bảo rằng bạn có sẵn các điều kiện tiên quyết sau:
1.  Cài đặt GroupDocs.Signature cho .NET: Tải xuống và cài đặt GroupDocs.Signature cho .NET từ[Liên kết tải xuống](https://releases.groupdocs.com/signature/net/).
2. Truy cập vào tài liệu chứa mã QR: Chuẩn bị tài liệu mẫu có chứa mã QR để xác minh. 

## Nhập không gian tên
Trước tiên, bạn cần nhập các không gian tên cần thiết để sử dụng các chức năng do GroupDocs.Signature cung cấp cho .NET. Thực hiện theo các bước sau:

```csharp
using System;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```


Bây giờ, hãy chia nhỏ quy trình xác minh mã QR được nhúng trong tài liệu bằng GroupDocs.Signature cho .NET:
## Bước 1: Chỉ định đường dẫn tài liệu
```csharp
string filePath = "sample_multiple_signatures.docx";
```
 Đảm bảo thay thế`"sample_multiple_signatures.docx"` với đường dẫn đến tài liệu của bạn.
## Bước 2: Khởi tạo đối tượng chữ ký
```csharp
using (Signature signature = new Signature(filePath))
{
    //Mã xác minh ở đây
}
```
 Khởi tạo một`Signature` đối tượng bằng cách cung cấp đường dẫn đến tài liệu.
## Bước 3: Chỉ định tùy chọn xác minh
```csharp
QrCodeVerifyOptions options = new QrCodeVerifyOptions()
{
    AllPages = true, // giá trị này được đặt theo mặc định
    Text = "John",
    MatchType = TextMatchType.Contains
};
```
 Xác định các tùy chọn xác minh như`AllPages` để xác minh tất cả các trang,`Text` để chỉ định văn bản phù hợp trong mã QR và`MatchType` để xác định các tiêu chí phù hợp.
## Bước 4: Xác minh chữ ký tài liệu
```csharp
VerificationResult result = signature.Verify(options);
```
 Gọi`Verify` phương pháp của`Signature` đối tượng, chuyển các tùy chọn xác minh.
## Bước 5: Xử lý kết quả xác minh
```csharp
if (result.IsValid)
{
    // Đã tìm thấy chữ ký hợp lệ
}
else
{
    // Đã tìm thấy chữ ký không hợp lệ
}
```
Căn cứ vào kết quả xác minh để xử lý các tình huống thành công hay thất bại cho phù hợp.

## Phần kết luận
Trong hướng dẫn này, chúng ta đã khám phá quy trình xác minh mã QR trong tài liệu bằng GroupDocs.Signature cho .NET. Bằng cách làm theo các bước này, bạn có thể tích hợp liền mạch chức năng xác minh mã QR vào các ứng dụng .NET của mình, đảm bảo tính toàn vẹn và xác thực của tài liệu.
## Câu hỏi thường gặp
### GroupDocs.Signature cho .NET có thể xác minh mã QR trên các định dạng tài liệu khác nhau không?
Có, GroupDocs.Signature for .NET hỗ trợ nhiều định dạng tài liệu bao gồm DOCX, PDF, v.v. để xác minh mã QR.
### Có bản dùng thử miễn phí GroupDocs.Signature cho .NET không?
 Có, bạn có thể tận dụng bản dùng thử miễn phí từ[trang phát hành](https://releases.groupdocs.com/).
### Những tùy chọn hỗ trợ nào có sẵn cho GroupDocs.Signature dành cho người dùng .NET?
 Người dùng có thể truy cập hỗ trợ thông qua[diễn đàn](https://forum.groupdocs.com/c/signature/13) cho GroupDocs.Signature.
### Tôi có thể mua giấy phép tạm thời cho GroupDocs.Signature cho .NET không?
 Có, giấy phép tạm thời có sẵn để mua từ[Trang mua GroupDocs](https://purchase.groupdocs.com/temporary-license/).
### Có sẵn tài liệu mở rộng về GroupDocs.Signature cho .NET không?
 Hoàn toàn có thể tham khảo tài liệu chi tiết được cung cấp[đây](https://reference.groupdocs.com/signature/net/) để có hướng dẫn toàn diện về cách sử dụng các chức năng của GroupDocs.Signature cho .NET.