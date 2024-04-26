---
title: Ký với nhiều tùy chọn
linktitle: Ký với nhiều tùy chọn
second_title: API GroupDocs.Signature .NET
description: Tìm hiểu cách ký tài liệu với nhiều tùy chọn bằng GroupDocs.Signature cho .NET. Tăng cường bảo mật tài liệu bằng văn bản, mã vạch, mã QR, kỹ thuật số và hình ảnh.
type: docs
weight: 14
url: /vi/net/advanced-signature-techniques/sign-with-multiple-options/
---
## Giới thiệu
Trong hướng dẫn này, chúng ta sẽ khám phá cách ký một tài liệu bằng nhiều tùy chọn chữ ký bằng thư viện GroupDocs.Signature cho .NET. Việc ký tài liệu với nhiều tùy chọn khác nhau như chữ ký văn bản, mã vạch, mã QR, kỹ thuật số, hình ảnh và siêu dữ liệu có thể mang lại tính linh hoạt và tăng cường bảo mật tài liệu.
## Điều kiện tiên quyết
Trước khi bắt đầu, hãy đảm bảo bạn có các điều kiện tiên quyết sau:
1.  GroupDocs.Signature for .NET Library: Tải xuống và cài đặt thư viện GroupDocs.Signature for .NET từ[đây](https://releases.groupdocs.com/signature/net/).
2. Môi trường phát triển: Thiết lập môi trường phát triển có cài đặt .NET Framework.
3. Tài liệu cần ký: Chuẩn bị tài liệu (ví dụ: sample.docx) mà bạn muốn ký.
4. Chứng chỉ và hình ảnh: Chuẩn bị mọi chứng chỉ và hình ảnh cần thiết cho chữ ký số và hình ảnh.

## Nhập không gian tên
Trước tiên, hãy nhập các không gian tên cần thiết để sử dụng thư viện GroupDocs.Signature trong ứng dụng .NET của bạn:
```csharp
using System;
using System.IO;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## Bước 1: Tải tài liệu
```csharp
string filePath = "sample.docx";
string outputFilePath = Path.Combine("Your Document Directory", "SignWithMultiple", "SignWithMultiple.docx");
using (Signature signature = new Signature(filePath))
{
    // Mã của bạn tiếp tục...
}
```
## Bước 2: Xác định các tùy chọn chữ ký
Xác định một số tùy chọn chữ ký thuộc các loại và cài đặt khác nhau, chẳng hạn như chữ ký văn bản, mã vạch, mã QR, chữ ký số, hình ảnh và siêu dữ liệu:
```csharp
TextSignOptions textOptions = new TextSignOptions("Text signature")
{
    VerticalAlignment = VerticalAlignment.Top,
    HorizontalAlignment = HorizontalAlignment.Left
};
BarcodeSignOptions barcodeOptions = new BarcodeSignOptions("123456")
{
    EncodeType = BarcodeTypes.Code128,
    Left = 0,
    Top = 150,
    Height = 50,
    Width = 200
};
// Xác định các tùy chọn chữ ký khác (ví dụ: mã QR, kỹ thuật số, hình ảnh, siêu dữ liệu)...
```
## Bước 3: Tạo danh sách tùy chọn chữ ký
Xác định danh sách các tùy chọn chữ ký chứa tất cả các tùy chọn được xác định trước đó:
```csharp
List<SignOptions> listOptions = new List<SignOptions>();
listOptions.Add(textOptions);
listOptions.Add(barcodeOptions);
// Thêm các tùy chọn chữ ký khác vào danh sách...
```
## Bước 4: Ký vào tài liệu
Ký văn bản với danh sách các tùy chọn chữ ký và lưu văn bản đã ký:
```csharp
SignResult result = signature.Sign(outputFilePath, listOptions);
Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).\nFile saved at {outputFilePath}.");
```

## Phần kết luận
Ký tài liệu với nhiều tùy chọn bằng GroupDocs.Signature cho .NET cung cấp giải pháp mạnh mẽ để tăng cường tính linh hoạt và bảo mật tài liệu. Bằng cách làm theo các bước được nêu trong hướng dẫn này, bạn có thể tích hợp liền mạch các loại chữ ký khác nhau vào các ứng dụng .NET của mình.
## Câu hỏi thường gặp
### Tôi có thể sử dụng hình ảnh tùy chỉnh cho chữ ký số không?
Có, bạn có thể chỉ định hình ảnh tùy chỉnh cho chữ ký số bằng thư viện GroupDocs.Signature.
### GroupDocs.Signature có tương thích với các định dạng tài liệu khác nhau không?
Có, GroupDocs.Signature hỗ trợ nhiều định dạng tài liệu khác nhau, bao gồm DOCX, PDF, PPTX, v.v.
### Tôi có thể tùy chỉnh hình thức của chữ ký văn bản không?
Hoàn toàn có thể, bạn có thể tùy chỉnh giao diện của chữ ký văn bản, bao gồm kích thước phông chữ, màu sắc và kiểu dáng.
### GroupDocs.Signature có cung cấp mã hóa cho chữ ký số không?
Có, GroupDocs.Signature cung cấp các tùy chọn mã hóa cho chữ ký số để đảm bảo tính bảo mật của tài liệu.
### Có phiên bản dùng thử của GroupDocs.Signature cho .NET không?
 Có, bạn có thể tải xuống phiên bản dùng thử miễn phí của GroupDocs.Signature cho .NET từ[đây](https://releases.groupdocs.com/).