---
title: Ký tài liệu bằng hình ảnh bằng GroupDocs.Signature
linktitle: Ký bằng hình ảnh
second_title: API GroupDocs.Signature .NET
description: Tìm hiểu cách ký tài liệu bằng hình ảnh trong ứng dụng .NET với Groupdocs.Signature cho .NET. Tăng cường bảo mật tài liệu và tính xác thực một cách dễ dàng.
weight: 13
url: /vi/net/advanced-signature-techniques/sign-with-image/
---

# Ký tài liệu bằng hình ảnh bằng GroupDocs.Signature

## Giới thiệu
Trong hướng dẫn này, chúng ta sẽ khám phá cách ký tài liệu bằng hình ảnh với Groupdocs.Signature cho .NET. Việc ký tài liệu sẽ bổ sung thêm một lớp xác thực và bảo mật cho các tệp của bạn, giúp chúng chống giả mạo và ràng buộc về mặt pháp lý. Với sự trợ giúp của Groupdocs.Signature dành cho .NET, bạn có thể tích hợp liền mạch chức năng ký tài liệu vào các ứng dụng .NET của mình.
## Điều kiện tiên quyết
Trước khi đi sâu vào hướng dẫn, hãy đảm bảo bạn có các điều kiện tiên quyết sau:
1.  Groupdocs.Signature for .NET: Đảm bảo bạn đã cài đặt Groupdocs.Signature for .NET trong môi trường phát triển của mình. Bạn có thể tải nó xuống từ[trang mạng](https://releases.groupdocs.com/signature/net/).
2. Môi trường phát triển .NET: Đảm bảo bạn đã cài đặt môi trường phát triển .NET đang hoạt động trên máy của mình.

## Nhập không gian tên
Trước khi bắt đầu với phần mã hóa, hãy nhập các vùng tên cần thiết để truy cập các lớp và phương thức được yêu cầu:
```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## Bước 1: Tải tài liệu
Bước đầu tiên là tải tài liệu mà bạn muốn ký. Cung cấp đường dẫn tệp của tài liệu bạn muốn ký:
```csharp
string filePath = "sample.pdf";
```
## Bước 2: Chỉ định hình ảnh chữ ký
Tiếp theo, chỉ định đường dẫn đến hình ảnh chữ ký mà bạn muốn sử dụng để ký:
```csharp
string imagePath = "signature_handwrite.jpg";
```
## Bước 3: Đặt đường dẫn tệp đầu ra
Xác định đường dẫn nơi bạn muốn lưu tài liệu đã ký:
```csharp
string outputFilePath = Path.Combine("Your Document Directory", "SignWithImage", fileName);
```
## Bước 4: Khởi tạo đối tượng chữ ký
Khởi tạo đối tượng Signature bằng cách chuyển đường dẫn tệp tài liệu:
```csharp
using (Signature signature = new Signature(filePath))
```
## Bước 5: Đặt tùy chọn ký hình ảnh
Đặt các tùy chọn cho ký bằng hình ảnh, bao gồm vị trí chữ ký, có ký trên tất cả các trang hay không, v.v.:
```csharp
ImageSignOptions options = new ImageSignOptions(imagePath)
{
    Left = 50,
    Top = 50,
    AllPages = true
};
```
## Bước 6: Ký tài liệu
Ký tài liệu bằng hình ảnh và các tùy chọn được chỉ định:
```csharp
SignResult result = signature.Sign(outputFilePath, options);
```
## Bước 7: Hiển thị kết quả
Cuối cùng hiển thị kết quả cho biết quá trình ký thành công và vị trí của văn bản đã ký:
```csharp
Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).\nFile saved at {outputFilePath}.");
```

## Phần kết luận
Trong hướng dẫn này, chúng ta đã học cách ký tài liệu bằng hình ảnh trong các ứng dụng .NET bằng Groupdocs.Signature cho .NET. Ký tài liệu là một khía cạnh quan trọng của việc quản lý tài liệu, cung cấp tính xác thực và bảo mật cho các tệp của bạn.
## Câu hỏi thường gặp
### Tôi có thể sử dụng nhiều hình ảnh chữ ký trong một tài liệu không?
Có, bạn có thể ký một tài liệu có nhiều hình ảnh bằng Groupdocs.Signature cho .NET. Đơn giản chỉ cần lặp lại quá trình ký cho mỗi hình ảnh.
### Groupdocs.Signature for .NET có tương thích với tất cả các loại tài liệu không?
Groupdocs.Signature cho .NET hỗ trợ nhiều định dạng tài liệu, bao gồm PDF, Word, Excel, v.v.
### Tôi có thể tùy chỉnh hình thức của chữ ký không?
Có, bạn có thể tùy chỉnh các khía cạnh khác nhau của giao diện chữ ký, chẳng hạn như kích thước, vị trí, độ trong suốt, v.v.
### Có phiên bản dùng thử để thử nghiệm không?
Có, bạn có thể tải xuống phiên bản dùng thử miễn phí từ trang web để kiểm tra chức năng trước khi mua hàng.
### Làm cách nào tôi có thể nhận được hỗ trợ kỹ thuật cho Groupdocs.Signature cho .NET?
 Bạn có thể nhận được hỗ trợ kỹ thuật bằng cách truy cập diễn đàn Groupdocs.Signature[đây](https://forum.groupdocs.com/c/signature/13).