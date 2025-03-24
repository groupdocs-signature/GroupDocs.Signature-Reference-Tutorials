---
title: Ký bằng chữ ký số
linktitle: Ký bằng chữ ký số
second_title: API GroupDocs.Signature .NET
description: Tìm hiểu cách ký tài liệu kỹ thuật số trong .NET bằng GroupDocs.Signature. Tăng cường tính bảo mật và tính xác thực với hướng dẫn toàn diện này.
weight: 12
url: /vi/net/advanced-signature-techniques/sign-with-digital/
---

# Ký bằng chữ ký số

## Giới thiệu
Chữ ký số đóng vai trò quan trọng trong việc đảm bảo tính xác thực và toàn vẹn của tài liệu điện tử. Trong lĩnh vực phát triển .NET, GroupDocs.Signature cung cấp giải pháp mạnh mẽ để tích hợp liền mạch chữ ký số vào ứng dụng của bạn. Hướng dẫn này sẽ hướng dẫn bạn quy trình ký tài liệu bằng chữ ký điện tử với GroupDocs.Signature cho .NET.
## Điều kiện tiên quyết
Trước khi chúng ta đi sâu vào triển khai, hãy đảm bảo bạn có sẵn các điều kiện tiên quyết sau:
1.  GroupDocs.Signature cho .NET: Tải xuống và cài đặt GroupDocs.Signature cho .NET từ[trang tải xuống](https://releases.groupdocs.com/signature/net/).
2. Chứng chỉ kỹ thuật số: Lấy chứng chỉ kỹ thuật số (.pfx) sẽ được sử dụng để ký tài liệu. Nếu chưa có, bạn có thể tạo chứng chỉ tự ký hoặc lấy chứng chỉ đó từ cơ quan cấp chứng chỉ đáng tin cậy.
3. Tài liệu cần ký: Chuẩn bị tài liệu (ví dụ: PDF) mà bạn muốn ký điện tử. Đảm bảo rằng bạn có các quyền cần thiết để truy cập và sửa đổi tài liệu.
4. Hình ảnh chữ ký: Tùy chọn, bạn có thể cung cấp hình ảnh chữ ký của mình sẽ được nhúng vào tài liệu. Điều này thêm một liên lạc cá nhân hóa cho chữ ký số.

## Nhập không gian tên
Trước tiên, hãy nhập các không gian tên cần thiết vào mã C# của chúng ta:
```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## Bước 1: Chỉ định đường dẫn và tùy chọn tệp
Xác định đường dẫn tệp cho tài liệu cần ký, hình ảnh chữ ký (nếu có) và chứng chỉ kỹ thuật số.
```csharp
string filePath = "sample.pdf";
string fileName = Path.GetFileName(filePath);
string imagePath = "signature_handwrite.jpg";
string certificatePath = "YourSignature.pfx";
string outputFilePath = Path.Combine("Your Document Directory", "SignWithDigital", fileName);
```
## Bước 2: Khởi tạo đối tượng chữ ký
 Tạo một thể hiện của`Signature` lớp bằng cách chuyển đường dẫn của tài liệu tới sign.
```csharp
using (Signature signature = new Signature(filePath))
{
    // Xác định các tùy chọn chữ ký số
    DigitalSignOptions options = new DigitalSignOptions(certificatePath)
    {
        ImageFilePath = imagePath, // Đặt đường dẫn tệp hình ảnh (tùy chọn)
        Left = 50,                 //Đặt tọa độ X của vị trí chữ ký
        Top = 50,                  // Đặt tọa độ Y của vị trí chữ ký
        PageNumber = 1,            // Ghi rõ số trang cần ký
        Password = "1234567890"    // Đặt mật khẩu cho chứng chỉ (nếu cần)
    };
    // Bước 3: Ký vào tài liệu
    SignResult result = signature.Sign(outputFilePath, options);
    // Bước 4: Hiển thị kết quả
    Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).\nFile saved at {outputFilePath}.");
}
```

## Phần kết luận
Trong hướng dẫn này, chúng tôi đã khám phá cách ký tài liệu bằng chữ ký điện tử với GroupDocs.Signature cho .NET. Bằng cách làm theo các bước đơn giản này, bạn có thể nâng cao tính bảo mật và tính xác thực của tài liệu điện tử của mình, đảm bảo chúng luôn chống giả mạo và ràng buộc về mặt pháp lý.
## Câu hỏi thường gặp
### Chữ ký số là gì?
Chữ ký số là một kỹ thuật mã hóa được sử dụng để xác minh tính xác thực và tính toàn vẹn của tài liệu hoặc tin nhắn kỹ thuật số.
### Tôi có thể ký tài liệu bằng GroupDocs.Signature bằng chứng chỉ tự ký không?
Có, bạn có thể ký tài liệu bằng chứng chỉ tự ký được tạo bởi các công cụ như OpenSSL hoặc MakeCert của Microsoft.
### GroupDocs.Signature có tương thích với các định dạng tài liệu khác nhau không?
Có, GroupDocs.Signature hỗ trợ nhiều định dạng tài liệu, bao gồm PDF, Word, Excel, PowerPoint, v.v.
### Tôi có thể tùy chỉnh giao diện chữ ký số của mình không?
Tuyệt đối! GroupDocs.Signature cho phép bạn tùy chỉnh các khía cạnh khác nhau của chữ ký số, chẳng hạn như vị trí, kích thước và hình thức của nó.
### GroupDocs.Signature có phù hợp với các ứng dụng cấp doanh nghiệp không?
Có, GroupDocs.Signature cung cấp các tính năng mạnh mẽ và khả năng mở rộng, khiến nó trở thành lựa chọn lý tưởng cho các ứng dụng ký tài liệu cấp doanh nghiệp.