---
"date": "2025-05-07"
"description": "Tìm hiểu cách ký số tệp PDF với GroupDocs.Signature cho .NET. Tùy chỉnh giao diện, áp dụng phông chữ và hình ảnh, đảm bảo tính bảo mật và tính xác thực của tài liệu."
"title": "Ký PDF kỹ thuật số trong .NET - Hướng dẫn sử dụng GroupDocs.Signature"
"url": "/vi/net/digital-signatures/sign-pdf-digital-signature-groupdocs-dotnet/"
"weight": 1
---

# Ký PDF kỹ thuật số trong .NET: Hướng dẫn sử dụng GroupDocs.Signature

## Giới thiệu

Chữ ký số trên tài liệu PDF đảm bảo tính xác thực, bảo mật và toàn vẹn của tài liệu—rất cần thiết cho các hợp đồng pháp lý, hóa đơn và hồ sơ chính thức. **GroupDocs.Signature cho .NET** giúp đơn giản hóa việc thêm chữ ký số vào tệp PDF, đồng thời cho phép tùy chỉnh giao diện để tăng tính thẩm mỹ. Hướng dẫn này sẽ hướng dẫn bạn quy trình ký tài liệu PDF bằng GroupDocs.Signature, đặc biệt chú trọng đến cấu hình hình ảnh và phông chữ.

### Những gì bạn sẽ học:
- Cách ký số tài liệu PDF bằng .NET
- Áp dụng các thiết lập giao diện tùy chỉnh như hình ảnh và phông chữ cho chữ ký số của bạn
- Thiết lập và khởi tạo GroupDocs.Signature cho .NET trong dự án của bạn

Chúng ta hãy bắt đầu bằng cách tìm hiểu những điều kiện tiên quyết cần thiết để bắt đầu.

## Điều kiện tiên quyết (H2)

Để làm theo hướng dẫn này, bạn sẽ cần:

- **GroupDocs.Signature cho .NET** thư viện: Đảm bảo rằng nó được cài đặt thông qua .NET CLI hoặc NuGet Package Manager.
  - **.NET CLI**: `dotnet add package GroupDocs.Signature`
  - **Trình quản lý gói**: `Install-Package GroupDocs.Signature`

- Chứng chỉ số hợp lệ ở định dạng PFX
- Kiến thức cơ bản về C# và thiết lập môi trường .NET

## Thiết lập GroupDocs.Signature cho .NET (H2)

Bắt đầu bằng cách cài đặt thư viện GroupDocs.Signature:

**.NET CLI**
```shell
dotnet add package GroupDocs.Signature
```

**Trình quản lý gói**
```shell
Install-Package GroupDocs.Signature
```

Hoặc sử dụng Giao diện người dùng Trình quản lý gói NuGet để tìm kiếm và cài đặt "GroupDocs.Signature".

### Mua lại giấy phép

- **Dùng thử miễn phí**: Khám phá đầy đủ tính năng với giấy phép đánh giá tạm thời.
- **Giấy phép tạm thời**: Lấy từ [đây](https://purchase.groupdocs.com/temporary-license/).
- **Mua**: Để sử dụng lâu dài, hãy mua đăng ký tại [liên kết này](https://purchase.groupdocs.com/buy).

### Khởi tạo và thiết lập cơ bản

Để khởi tạo GroupDocs.Signature trong dự án .NET của bạn:

```csharp
using GroupDocs.Signature;

// Khởi tạo đối tượng Chữ ký bằng tệp PDF nguồn.
using (Signature signature = new Signature("YOUR_DOCUMENT_DIRECTORY/SAMPLE_PDF.pdf")) {
    // Mã để ký tài liệu của bạn sẽ nằm ở đây.
}
```

## Hướng dẫn thực hiện

### Ký tài liệu PDF bằng chữ ký số (H2)

Tính năng này cho phép bạn thêm chữ ký số vào tài liệu PDF, đảm bảo tính xác thực và toàn vẹn của chúng.

#### Tổng quan về tính năng
Bằng cách triển khai tính năng này, bạn có thể ký số bất kỳ tệp PDF nào bằng GroupDocs.Signature cho .NET. Bạn cũng sẽ áp dụng các cài đặt tùy chỉnh để tùy chỉnh giao diện chữ ký, bao gồm hình ảnh và phông chữ.

#### Các bước thực hiện (H3)

##### Bước 1: Thiết lập môi trường của bạn

Đảm bảo rằng dự án của bạn được cấu hình với các tham chiếu cần thiết:

```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Options;
using GroupDocs.Signature.Domain;

namespace DigitalSignatureExample {
    public class SignPdfWithDigitalSignature {
        // Xác định đường dẫn cho tệp PDF nguồn và chứng chỉ kỹ thuật số
        private static string sourceFile = "YOUR_DOCUMENT_DIRECTORY/SAMPLE_PDF.pdf";
        private static string outputFile = Path.Combine("YOUR_OUTPUT_DIRECTORY", "SignWithPdfDigitalAdvanced_Signed.pdf");
        private static string certificatePath = "YOUR_DOCUMENT_DIRECTORY/CertificatePfx.pfx";

        public static void Run() {
            // Khởi tạo đối tượng Chữ ký
            using (Signature signature = new Signature(sourceFile)) {
                // Thiết lập tùy chọn ký kỹ thuật số
                DigitalSignOptions options = new DigitalSignOptions(certificatePath) {
                    Password = "1234567890",  // Mật khẩu chứng chỉ
                    Reason = "Sign",          // Lý do chữ ký
                    Contact = "JohnSmith",    // Thông tin liên lạc
                    Location = "Office1",     // Địa điểm ký kết
                    Visible = true,            // Làm cho chữ ký hiển thị
                    Left = 400,                // Vị trí nằm ngang
                    Top = 20,                  // Vị trí thẳng đứng
                    Height = 70,               // Chiều cao chữ ký
                    Width = 200,               // Chiều rộng chữ ký
                    ImageFilePath = "YOUR_DOCUMENT_DIRECTORY/ImageHandwrite.png", // Hình ảnh xuất hiện
                    Appearance = new PdfDigitalSignatureAppearance() {
                        Foreground = System.Drawing.Color.FromArgb(50, System.Drawing.Color.Gray),
                        FontFamilyName = "TimesNewRoman",
                        FontSize = 12
                    }
                };

                // Ký tài liệu và lưu vào đường dẫn đầu ra.
                SignResult signResult = signature.Sign(outputFile, options);
                Console.WriteLine($"Document signed successfully with {signResult.Succeeded.Count} signature(s). File saved at {outputFile}.");
            }
        }
    }
}
```

##### Bước 2: Tùy chỉnh giao diện chữ ký

Tùy chỉnh giao diện chữ ký số của bạn bằng cách sử dụng cài đặt phông chữ và hình ảnh:

```csharp
using System;
using GroupDocs.Signature.Options;
using GroupDocs.Signature.Domain;
using System.Drawing;

namespace DigitalSignatureAppearanceExample {
    public class CustomizeDigitalSignatureAppearance {
        public static void Run() {
            // Khởi tạo cài đặt giao diện cho chữ ký số.
            PdfDigitalSignatureAppearance appearance = new PdfDigitalSignatureAppearance() {
                Foreground = Color.FromArgb(50, Color.Gray),  // Đặt màu phông chữ tùy chỉnh
                FontFamilyName = "TimesNewRoman",          // Chỉ định họ phông chữ
                FontSize = 12                               // Xác định kích thước phông chữ
            };

            Console.WriteLine("Custom appearance settings for digital signature have been applied.");
        }
    }
}
```

#### Tùy chọn cấu hình chính
- **Đường dẫn chứng chỉ**: Đảm bảo bạn cung cấp đúng đường dẫn đến tệp PFX của mình.
- **Mật khẩu**: Sử dụng mật khẩu được liên kết với chứng chỉ số của bạn.
- **Cài đặt giao diện**: Tùy chỉnh phông chữ và màu sắc để phù hợp với yêu cầu về thương hiệu.

##### Mẹo khắc phục sự cố
- Xác minh rằng chứng chỉ số của bạn hợp lệ và được cấu hình chính xác.
- Đảm bảo tất cả đường dẫn (PDF, đầu ra, hình ảnh) đều có thể truy cập được từ môi trường ứng dụng của bạn.

### Áp dụng Cài đặt Giao diện Tùy chỉnh cho Chữ ký Số (H2)

Tăng cường sức hấp dẫn trực quan cho chữ ký số của bạn với cài đặt phông chữ và hình ảnh tùy chỉnh bằng GroupDocs.Signature cho .NET.

#### Tổng quan
Việc tùy chỉnh giao diện chữ ký số có thể giúp chữ ký trở nên bắt mắt hơn và phù hợp với các tiêu chuẩn thương hiệu. Tính năng này cho phép bạn thiết lập phông chữ, màu sắc và hình ảnh cụ thể.

#### Các bước thực hiện (H3)

##### Bước 1: Khởi tạo Cài đặt Giao diện

Tạo một phiên bản của `PdfDigitalSignatureAppearance`:

```csharp
using System.Drawing;

// Xác định cài đặt giao diện tùy chỉnh cho chữ ký số.
PdfDigitalSignatureAppearance appearance = new PdfDigitalSignatureAppearance() {
    Foreground = Color.FromArgb(50, Color.Gray),  // Màu phông chữ tùy chỉnh
    FontFamilyName = "TimesNewRoman",            // Họ phông chữ
    FontSize = 12                                // Kích thước phông chữ
};
```

##### Bước 2: Áp dụng Cài đặt Giao diện

Tích hợp các cài đặt này vào tùy chọn chữ ký số của bạn:

```csharp
DigitalSignOptions options = new DigitalSignOptions(certificatePath) {
    ImageFilePath = "YOUR_DOCUMENT_DIRECTORY/ImageHandwrite.png",
    Appearance = appearance
};
```

## Ứng dụng thực tế (H2)

Sau đây là một số trường hợp thực tế mà việc ký PDF bằng GroupDocs.Signature có thể mang lại lợi ích:
1. **Ký kết hợp đồng**: Đảm bảo các thỏa thuận pháp lý được ký kết và xác minh kỹ thuật số.
2. **Phê duyệt hóa đơn**: Ký hóa đơn kỹ thuật số để xử lý nhanh hơn trong các phòng tài chính.
3. **Xác thực tài liệu**: Xác thực các tài liệu chính thức để ngăn chặn việc thay đổi trái phép.

Bằng cách làm theo hướng dẫn này, bạn sẽ tích hợp hiệu quả chữ ký số vào các ứng dụng .NET của mình bằng GroupDocs.Signature, nâng cao tính bảo mật và tính chuyên nghiệp.