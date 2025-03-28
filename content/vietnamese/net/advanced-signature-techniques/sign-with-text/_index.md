---
title: Ký bằng văn bản bằng GroupDocs.Signature cho .NET
linktitle: Ký bằng văn bản
second_title: API GroupDocs.Signature .NET
description: Tìm hiểu cách ký tài liệu bằng văn bản bằng GroupDocs.Signature cho .NET. Hướng dẫn từng bước để thêm chữ ký văn bản theo chương trình.
weight: 17
url: /vi/net/advanced-signature-techniques/sign-with-text/
---

# Ký bằng văn bản bằng GroupDocs.Signature cho .NET

## Giới thiệu
Trong thời đại kỹ thuật số, việc ký các văn bản điện tử đã trở thành thông lệ tiêu chuẩn, tiết kiệm thời gian và nguồn lực. GroupDocs.Signature cho .NET cung cấp giải pháp toàn diện để thêm chữ ký văn bản vào các định dạng tài liệu khác nhau theo chương trình. Trong hướng dẫn này, chúng tôi sẽ hướng dẫn bạn quy trình ký tài liệu có văn bản bằng GroupDocs.Signature cho .NET.
## Điều kiện tiên quyết
Trước khi chúng ta đi sâu vào hướng dẫn, hãy đảm bảo bạn có các điều kiện tiên quyết sau:
1.  GroupDocs.Signature cho .NET: Đảm bảo bạn đã cài đặt thư viện GroupDocs.Signature cho .NET. Bạn có thể tải nó xuống từ[đây](https://releases.groupdocs.com/signature/net/).
2. Môi trường phát triển: Có môi trường làm việc được thiết lập để phát triển .NET.
3. Tài liệu: Chuẩn bị tài liệu (ví dụ: PDF, Word) mà bạn muốn ký bằng văn bản.

## Nhập không gian tên
Trước tiên, bạn cần nhập các vùng tên cần thiết vào dự án .NET của mình để sử dụng các chức năng GroupDocs.Signature.
```csharp
using System;
using System.IO;
using System.Drawing;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

Hãy chia nhỏ quá trình ký một tài liệu có văn bản thành nhiều bước:
## Bước 1: Tải tài liệu
Tải tài liệu bạn muốn ký bằng văn bản.
```csharp
string filePath = "sample.pdf"; // Đường dẫn đến tài liệu
string fileName = Path.GetFileName(filePath);
```
## Bước 2: Đặt đường dẫn tệp đầu ra
Xác định đường dẫn tệp đầu ra nơi tài liệu đã ký sẽ được lưu.
```csharp
string outputFilePath = Path.Combine("Your Document Directory", "SignWithText", fileName);
```
## Bước 3: Tạo tùy chọn chữ ký
Thiết lập các tùy chọn cho chữ ký văn bản bao gồm nội dung văn bản, vị trí, kích thước, màu sắc, font chữ.
```csharp
TextSignOptions options = new TextSignOptions("John Smith")
{
    Left = 50, // Đặt vị trí chữ ký
    Top = 200,
    Width = 100, // Đặt hình chữ nhật chữ ký
    Height = 30,
    ForeColor = Color.Red, // Đặt màu văn bản
    Font = new SignatureFont { Size = 14, FamilyName = "Comic Sans MS" } // Đặt phông chữ
};
```
## Bước 4: Ký tài liệu
Sử dụng GroupDocs.Signature để ký tài liệu với các tùy chọn đã chỉ định và lưu tài liệu đã ký vào đường dẫn tệp đầu ra.
```csharp
using (Signature signature = new Signature(filePath))
{
    SignResult result = signature.Sign(outputFilePath, options); // Ký văn bản
    Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).\nFile saved at {outputFilePath}.");
}
```

## Phần kết luận
Trong hướng dẫn này, chúng ta đã học cách ký một tài liệu có văn bản bằng GroupDocs.Signature cho .NET. Bằng cách làm theo các bước này, bạn có thể thêm chữ ký văn bản vào tài liệu của mình một cách hiệu quả theo chương trình, tăng cường tính bảo mật và tính xác thực.
## Câu hỏi thường gặp
### Tôi có thể tùy chỉnh hình thức của chữ ký văn bản không?
Có, bạn có thể tùy chỉnh các thông số khác nhau như màu sắc, phông chữ, kích thước và vị trí của chữ ký văn bản theo sở thích của bạn.
### GroupDocs.Signature có tương thích với nhiều định dạng tài liệu không?
Có, GroupDocs.Signature hỗ trợ nhiều định dạng tài liệu khác nhau bao gồm PDF, Word, Excel, PowerPoint, v.v.
### Tôi có thể thêm nhiều chữ ký văn bản vào một tài liệu không?
Hoàn toàn có thể, bạn có thể thêm nhiều chữ ký văn bản vào một tài liệu, mỗi chữ ký có bộ tùy chọn tùy chỉnh riêng.
### GroupDocs.Signature có đảm bảo tính toàn vẹn của tài liệu sau khi ký không?
Có, GroupDocs.Signature sử dụng các thuật toán mã hóa mạnh mẽ để đảm bảo tính toàn vẹn của tài liệu và ngăn ngừa giả mạo sau khi ký.
### Có phiên bản dùng thử để thử nghiệm trước khi mua không?
 Có, bạn có thể tải xuống phiên bản dùng thử miễn phí từ[đây](https://releases.groupdocs.com/) để khám phá các tính năng trước khi mua hàng.