---
"date": "2025-05-08"
"description": "Tìm hiểu cách ký mã QR vào bảng tính Excel và lưu chúng ở nhiều định dạng khác nhau bằng GroupDocs.Signature for Java. Bảo mật tài liệu của bạn một cách hiệu quả."
"title": "Ký và lưu bảng tính Excel bằng mã QR trong Java bằng GroupDocs.Signature"
"url": "/vi/java/qr-code-signatures/sign-save-spreadsheets-java-qr-codes-groupdocs-signature/"
"weight": 1
type: docs
---
# Ký và lưu bảng tính Excel bằng mã QR trong Java bằng GroupDocs.Signature

## Giới thiệu

Trong thời đại kỹ thuật số ngày nay, việc đảm bảo tính xác thực của tài liệu trở nên quan trọng hơn bao giờ hết. Cho dù bạn đang xử lý hợp đồng, thỏa thuận hay bảng tính tài chính, việc ký tài liệu một cách an toàn có thể tiết kiệm thời gian và ngăn ngừa gian lận. **GroupDocs.Signature cho Java** là một thư viện mạnh mẽ giúp đơn giản hóa việc tạo chữ ký điện tử ở nhiều định dạng tài liệu khác nhau. Hướng dẫn này sẽ hướng dẫn bạn sử dụng GroupDocs.Signature để ký mã QR vào bảng tính Excel và lưu chúng ở nhiều định dạng khác nhau.

### Những gì bạn sẽ học:
- Cách ký bảng tính bằng chữ ký mã QR.
- Lưu tài liệu đã ký ở nhiều định dạng đầu ra như PDF, XLSX, v.v.
- Tối ưu hóa hiệu suất ứng dụng Java của bạn khi xử lý chữ ký tài liệu.

Đến cuối hướng dẫn này, bạn sẽ có hiểu biết vững chắc về cách tích hợp và sử dụng GroupDocs.Signature để ký các tác vụ trong ứng dụng Java của mình. Hãy cùng tìm hiểu cách thiết lập các công cụ cần thiết trước khi bắt đầu triển khai các tính năng này!

## Điều kiện tiên quyết

Trước khi thực hiện theo hướng dẫn này, hãy đảm bảo bạn có những điều sau:
- **Bộ phát triển Java (JDK)** được cài đặt trên máy của bạn.
- Kiến thức cơ bản về lập trình Java và quen thuộc với hệ thống xây dựng Maven hoặc Gradle.
- Một IDE như IntelliJ IDEA, Eclipse hoặc NetBeans.

Ngoài ra, bạn sẽ cần thiết lập GroupDocs.Signature cho Java trong dự án của mình. Quá trình thiết lập rất đơn giản và có thể thực hiện bằng cách sử dụng các phụ thuộc Maven hoặc Gradle như minh họa bên dưới:

## Thiết lập GroupDocs.Signature cho Java

Để bắt đầu, hãy thêm phụ thuộc GroupDocs.Signature vào tệp dựng của dự án.

### Maven
```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

### Gradle
```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

Ngoài ra, bạn có thể tải xuống thư viện trực tiếp từ [GroupDocs.Signature cho các bản phát hành Java](https://releases.groupdocs.com/signature/java/).

#### Mua lại giấy phép
Để sử dụng đầy đủ các tính năng của GroupDocs.Signature:
- **Dùng thử miễn phí**: Bắt đầu bằng bản dùng thử miễn phí để khám phá các chức năng cơ bản.
- **Giấy phép tạm thời**: Xin giấy phép tạm thời để có quyền truy cập đầy đủ trong quá trình đánh giá.
- **Mua**: Để sử dụng lâu dài, hãy cân nhắc mua giấy phép thương mại.

### Khởi tạo và thiết lập cơ bản
Khởi tạo `Signature` lớp bằng cách truyền đường dẫn tệp tài liệu của bạn như được hiển thị bên dưới:
```java
import com.groupdocs.signature.Signature;

// Khởi tạo với đường dẫn tài liệu của bạn
Signature signature = new Signature("YOUR_DOCUMENT_DIRECTORY/SampleSpreadsheet.xlsx");
```

## Hướng dẫn thực hiện
Trong phần này, chúng tôi sẽ hướng dẫn bạn các bước để ký bảng tính và lưu bảng tính đó bằng GroupDocs.Signature.

### Ký bảng tính bằng mã QR
#### Tổng quan
Tính năng này cho phép bạn thêm chữ ký mã QR vào bảng tính Excel. Tính năng này đặc biệt hữu ích khi thêm mã định danh điện tử an toàn, có thể dễ dàng quét.
##### Bước 1: Xác định đường dẫn tệp
Bắt đầu bằng cách xác định đường dẫn cho cả tệp đầu vào và đầu ra:
```java
String filePath = "YOUR_DOCUMENT_DIRECTORY/SampleSpreadsheet.xlsx";
String outputFilePath = "YOUR_OUTPUT_DIRECTORY/signedDocument.pdf";
```
##### Bước 2: Khởi tạo đối tượng chữ ký
Tạo một `Signature` đối tượng với đường dẫn tệp tài liệu của bạn.
```java
Signature signature = new Signature(filePath);
```
##### Bước 3: Tạo tùy chọn ký hiệu mã QR
Cấu hình các tùy chọn ký mã QR. Chỉ định các thuộc tính như văn bản, loại và vị trí của mã QR:
```java
import com.groupdocs.signature.options.sign.QrCodeSignOptions;
import com.groupdocs.signature.domain.qrcodes.QrCodeTypes;

QrCodeSignOptions signOptions = new QrCodeSignOptions("JohnSmith");
signOptions.setEncodeType(QrCodeTypes.QR);
signOptions.setLeft(100); // Tọa độ X
signOptions.setTop(100);  // Tọa độ Y
```
##### Bước 4: Cấu hình tùy chọn lưu
Chỉ định cách bạn muốn lưu tài liệu đã ký, bao gồm cả định dạng của tài liệu:
```java
import com.groupdocs.signature.options.saveoptions.SpreadsheetSaveOptions;
import com.groupdocs.signature.domain.enums.SpreadsheetSaveFileFormat;

SpreadsheetSaveOptions saveOptions = new SpreadsheetSaveOptions();
saveOptions.setFileFormat(SpreadsheetSaveFileFormat.Pdf);
saveOptions.setOverwriteExistingFiles(true);
```
##### Bước 5: Ký và lưu tài liệu
Cuối cùng, sử dụng `sign` phương pháp áp dụng chữ ký mã QR và lưu tài liệu:
```java
try {
    signature.sign(outputFilePath, signOptions, saveOptions);
} catch (Exception e) {
    e.printStackTrace();
}
```
### Lưu tài liệu ở nhiều định dạng tệp đầu ra khác nhau
#### Tổng quan
GroupDocs.Signature cho phép bạn lưu các tài liệu đã ký thành nhiều định dạng khác nhau như PDF, XLSX và DOCX.
##### Bước 1: Xác định Đường dẫn đầu ra
Chỉ định đường dẫn và định dạng tệp đầu ra mong muốn của bạn:
```java
String outputPath = "YOUR_OUTPUT_DIRECTORY/signedDocument.pdf"; // Thay đổi định dạng khi cần thiết
```
##### Bước 2: Thiết lập tùy chọn lưu
Cấu hình `SpreadsheetSaveOptions` để xác định cách bạn muốn lưu tài liệu:
```java
SpreadsheetSaveOptions saveOptions = new SpreadsheetSaveOptions();
saveOptions.setFileFormat(SpreadsheetSaveFileFormat.Pdf); // Có thể thay đổi cho các định dạng khác nhau
saveOptions.setOverwriteExistingFiles(true);
```
##### Bước 3: Triển khai hoạt động ký
Sử dụng các tùy chọn này trong thao tác ký. Đảm bảo `signature` đối tượng được khởi tạo đúng cách:
```java
// Ví dụ sử dụng (giả sử đối tượng chữ ký tồn tại)
signature.sign(outputPath, signOptions, saveOptions);
```
## Ứng dụng thực tế
Sau đây là một số tình huống thực tế mà chức năng này có thể mang lại lợi ích:
- **Tài liệu pháp lý**: Ký hợp đồng an toàn bằng mã QR để dễ dàng xác minh.
- **Báo cáo tài chính**: Thêm chữ ký vào bảng tính có chứa dữ liệu tài chính nhạy cảm.
- **Quản lý hàng tồn kho**: Sử dụng mã QR trên bảng kê khai hàng tồn kho để theo dõi và xác thực dễ dàng hơn.

## Cân nhắc về hiệu suất
Khi làm việc với việc ký tài liệu, hãy cân nhắc những mẹo sau:
- Tối ưu hóa việc quản lý bộ nhớ Java của bạn bằng cách lập hồ sơ sử dụng tài nguyên trong các hoạt động chữ ký.
- GroupDocs.Signature được tối ưu hóa về hiệu suất, nhưng hãy đảm bảo bạn chạy nó trong môi trường phù hợp để xử lý hiệu quả các tài liệu lớn.

## Phần kết luận
Đến thời điểm này, bạn hẳn đã quen với việc sử dụng GroupDocs.Signature để ký và lưu bảng tính Excel bằng mã QR. Công cụ mạnh mẽ này có thể tăng cường đáng kể tính bảo mật và tính xác thực cho tài liệu kỹ thuật số của bạn. Tiếp theo, hãy khám phá các tính năng bổ sung như chữ ký văn bản hoặc chữ ký đóng dấu để bảo mật tài liệu của bạn tốt hơn.

**Kêu gọi hành động**: Hãy thử áp dụng những giải pháp này vào dự án của bạn ngay hôm nay!

## Phần Câu hỏi thường gặp
1. **GroupDocs.Signature hỗ trợ những định dạng nào?**
   - Nó hỗ trợ PDF, XLSX, DOCX và nhiều định dạng khác.
2. **Làm thế nào để tôi có thể khắc phục sự cố chữ ký?**
   - Kiểm tra thông báo ngoại lệ để tìm manh mối; đảm bảo tất cả đường dẫn tệp đều chính xác.
3. **Có thể ký nhiều trang trong một tài liệu không?**
   - Có, hãy chỉ định số trang trong tùy chọn ký tên của bạn.
4. **GroupDocs.Signature có thể được sử dụng trong các ứng dụng web không?**
   - Chắc chắn rồi, nó rất phù hợp cho các ứng dụng Java phía máy chủ.
5. **Tôi có thể nhận được hỗ trợ như thế nào nếu cần?**
   - Sử dụng [Diễn đàn hỗ trợ GroupDocs](https://forum.groupdocs.com/c/signature) để được hỗ trợ.

## Tài nguyên
- **Tài liệu**: Hướng dẫn toàn diện và tài liệu tham khảo API có thể được tìm thấy tại [Tài liệu GroupDocs](https://docs.groupdocs.com/signature/java/).
- **Tài liệu tham khảo API**: Thông tin chi tiết có sẵn trên [Trang tham khảo API](https://reference.groupdocs.com/signature/java/).
- **Tải xuống**: Truy cập phiên bản mới nhất tại [Bản phát hành GroupDocs](https://releases.groupdocs.com/signature/java/).
- **Mua và cấp phép**: Tìm hiểu thêm về các tùy chọn cấp phép tại [Mua GroupDocs](https://purchase.groupdocs.com/buy) và nhận bản dùng thử miễn phí qua [Dùng thử miễn phí GroupDocs](http://www.groupdocs.com/pricing)