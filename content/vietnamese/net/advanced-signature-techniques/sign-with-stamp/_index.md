---
title: Ký bằng Stamp bằng GroupDocs.Signature
linktitle: Ký bằng tem
second_title: API GroupDocs.Signature .NET
description: Tìm hiểu cách thêm chữ ký đóng dấu vào tài liệu .NET của bạn một cách dễ dàng với GroupDocs.Signature cho .NET. Tăng cường bảo mật tài liệu.
type: docs
weight: 16
url: /vi/net/advanced-signature-techniques/sign-with-stamp/
---
## Giới thiệu
Trong hướng dẫn này, chúng tôi sẽ hướng dẫn bạn quy trình ký tài liệu có đóng dấu bằng GroupDocs.Signature cho .NET. Bằng cách làm theo các hướng dẫn từng bước này, bạn sẽ có thể thêm chữ ký đóng dấu vào tài liệu của mình một cách dễ dàng.
## Điều kiện tiên quyết
Trước khi chúng tôi bắt đầu, hãy đảm bảo bạn có các điều kiện tiên quyết sau:
1.  GroupDocs.Signature for .NET SDK: Tải xuống và cài đặt SDK từ[trang mạng](https://releases.groupdocs.com/signature/net/).
2. Môi trường phát triển: Đảm bảo bạn có môi trường phát triển phù hợp được thiết lập để phát triển .NET.
3. Tài liệu cần ký: Chuẩn bị tài liệu (ví dụ: PDF) mà bạn muốn ký bằng tem.

## Nhập không gian tên
Bắt đầu bằng cách nhập các không gian tên cần thiết vào dự án của bạn:
```csharp
using System;
using System.IO;
using System.Drawing;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## Bước 1: Tải tài liệu
```csharp
string filePath = "sample.pdf";
using (Signature signature = new Signature(filePath))
{
    // Mã của bạn ở đây
}
```
## Bước 2: Đặt tùy chọn dấu tem
```csharp
StampSignOptions options = new StampSignOptions()
{
    Left = 50,
    Top = 150,                    
    Width = 200,
    Height = 200
};
```
## Bước 3: Cấu hình giao diện tem
```csharp
StampLine outerLine = new StampLine();
outerLine.Text = " * European Union ";
outerLine.TextRepeatType = StampTextRepeatType.FullTextRepeat;
outerLine.Font.Size = 12;
outerLine.Height = 22;
outerLine.TextBottomIntent = 6;
outerLine.TextColor = Color.WhiteSmoke;
outerLine.BackgroundColor = Color.DarkSlateBlue;
options.OuterLines.Add(outerLine);
StampLine innerLine = new StampLine();
innerLine.Text = "John Smith";
innerLine.TextColor = Color.MediumVioletRed;
innerLine.Font.Size = 20;
innerLine.Font.Bold = true;
innerLine.Height = 40;
options.InnerLines.Add(innerLine);
```
## Bước 4: Ký vào tài liệu
```csharp
string outputFilePath = Path.Combine("Your Document Directory", "SignWithStamp", fileName);
SignResult result = signature.Sign(outputFilePath, options);
Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).\nFile saved at {outputFilePath}.");
```

## Phần kết luận
Thêm chữ ký đóng dấu vào tài liệu của bạn bằng GroupDocs.Signature cho .NET là một quy trình đơn giản, như được minh họa trong hướng dẫn này. Với các bước được cung cấp, bạn có thể dễ dàng nâng cao tính bảo mật và tính xác thực của tài liệu của mình.
## Câu hỏi thường gặp
### Tôi có thể tùy chỉnh hình thức của chữ ký tem không?
Có, bạn có thể tùy chỉnh các khía cạnh khác nhau như văn bản, phông chữ, màu sắc và vị trí của chữ ký tem theo yêu cầu của bạn.
### GroupDocs.Signature có hỗ trợ ký nhiều định dạng tài liệu không?
Có, GroupDocs.Signature hỗ trợ nhiều định dạng tài liệu bao gồm PDF, Microsoft Word, Excel, PowerPoint, v.v.
### Có phiên bản dùng thử cho GroupDocs.Signature không?
 Có, bạn có thể truy cập phiên bản dùng thử miễn phí từ[trang mạng](https://releases.groupdocs.com/).
### Tôi có thể thêm nhiều chữ ký vào một tài liệu không?
Hoàn toàn có thể, GroupDocs.Signature cho phép bạn thêm nhiều chữ ký, bao gồm tem, văn bản, hình ảnh và chữ ký điện tử vào một tài liệu.
### Tôi có thể tìm hỗ trợ ở đâu nếu gặp bất kỳ vấn đề nào trong quá trình triển khai?
 Bạn có thể tìm thấy sự hỗ trợ và trợ giúp từ diễn đàn cộng đồng GroupDocs.Signature[đây](https://forum.groupdocs.com/c/signature/13).