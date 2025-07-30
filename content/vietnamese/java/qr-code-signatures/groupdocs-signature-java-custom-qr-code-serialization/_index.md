---
"date": "2025-05-08"
"description": "Tìm hiểu cách triển khai tuần tự hóa mã QR tùy chỉnh với mã hóa trong PDF bằng GroupDocs.Signature cho Java. Bảo mật tài liệu của bạn một cách hiệu quả."
"title": "Triển khai mã hóa và tuần tự hóa mã QR tùy chỉnh trong PDF bằng GroupDocs.Signature cho Java"
"url": "/vi/java/qr-code-signatures/groupdocs-signature-java-custom-qr-code-serialization/"
"weight": 1
---

# Cách triển khai mã hóa và tuần tự hóa mã QR tùy chỉnh trong PDF bằng GroupDocs.Signature cho Java

## Giới thiệu

Trong thời đại kỹ thuật số, việc ký tài liệu an toàn là điều cần thiết để duy trì tính toàn vẹn và xác thực của dữ liệu. Hãy đến với GroupDocs.Signature for Java—một thư viện mạnh mẽ được thiết kế để đơn giản hóa việc thêm chữ ký vào tài liệu. Hướng dẫn này sẽ hướng dẫn bạn cách triển khai tuần tự hóa mã QR tùy chỉnh với mã hóa trong PDF bằng GroupDocs.Signature for Java.

**Những gì bạn sẽ học:**
- Cách thiết lập và cấu hình GroupDocs.Signature cho Java
- Triển khai tuần tự hóa tùy chỉnh cho chữ ký mã QR
- Mã hóa dữ liệu tuần tự trong mã QR
- Áp dụng các tính năng này để bảo mật tài liệu của bạn

Trước khi bắt đầu triển khai, hãy đảm bảo rằng bạn có mọi thứ cần thiết để thực hiện.

### Điều kiện tiên quyết

Để sử dụng hướng dẫn này một cách hiệu quả, hãy đảm bảo bạn đáp ứng các điều kiện tiên quyết sau:

1. **Thư viện và phụ thuộc bắt buộc:**
   - GroupDocs.Signature dành cho Java phiên bản 23.12 trở lên
   - Maven hoặc Gradle để quản lý phụ thuộc (tùy chọn)

2. **Yêu cầu thiết lập môi trường:**
   - Bộ công cụ phát triển Java (JDK) được cài đặt trên máy của bạn
   - Hiểu biết cơ bản về lập trình Java

3. **Điều kiện tiên quyết về kiến thức:**
   - Quen thuộc với Java và các khái niệm lập trình hướng đối tượng
   - Kiến thức cơ bản về làm việc với PDF trong Java

## Thiết lập GroupDocs.Signature cho Java

Để bắt đầu, bạn cần thiết lập thư viện GroupDocs.Signature trong môi trường dự án của mình.

### Cài đặt Maven

Nếu bạn đang sử dụng Maven, hãy thêm phần phụ thuộc sau vào `pom.xml` tài liệu:

```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

### Cài đặt Gradle

Đối với người dùng Gradle, hãy bao gồm dòng này trong `build.gradle` tài liệu:

```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

### Tải xuống trực tiếp

Ngoài ra, bạn có thể tải xuống phiên bản mới nhất trực tiếp từ [GroupDocs.Signature cho các bản phát hành Java](https://releases.groupdocs.com/signature/java/).

#### Các bước xin giấy phép
- **Dùng thử miễn phí:** Bắt đầu bằng cách tải xuống phiên bản dùng thử để kiểm tra các tính năng của nó.
- **Giấy phép tạm thời:** Bạn có thể yêu cầu giấy phép tạm thời nếu cần, cho phép bạn đánh giá sản phẩm mà không có bất kỳ hạn chế nào.
- **Mua:** Để sử dụng lâu dài, hãy cân nhắc mua giấy phép đầy đủ.

Sau khi cài đặt, hãy khởi tạo GroupDocs.Signature trong dự án của bạn:

```java
import com.groupdocs.signature.Signature;

public class SetupGroupDocs {
    public static void main(String[] args) {
        Signature signature = new Signature("YOUR_DOCUMENT_DIRECTORY/sample.pdf");
        // Mã của bạn ở đây...
    }
}
```

## Hướng dẫn thực hiện

Bây giờ, chúng ta hãy cùng tìm hiểu sâu hơn về việc triển khai mã hóa và tuần tự hóa mã QR tùy chỉnh bằng GroupDocs.Signature cho Java.

### Lớp tuần tự hóa tùy chỉnh cho chữ ký mã QR

#### Tổng quan

Tính năng này liên quan đến việc tạo một lớp xử lý việc tuần tự hóa siêu dữ liệu thành chữ ký mã QR. `DocumentSignatureData` lớp lưu trữ các thuộc tính như ID, tác giả, ngày ký và yếu tố dữ liệu.

```java
import com.groupdocs.signature.domain.extensions.serialization.FormatAttribute;
import java.math.BigDecimal;
import java.util.Date;

class DocumentSignatureData {
    @FormatAttribute(propertyName = "SignID")
    public String ID;

    public void setID(String value) { 
        this.ID = value; 
    }

    @FormatAttribute(propertyName = "SAuth")
    public String author;

    public void setAuthor(String value) {
        this.author = value;
    }

    @FormatAttribute(propertyName = "SDate", propertyFormat = "yyyy-MM-dd")
    public Date signed = new Date();

    public void setSigned(Date value) {
        this.signed = value;
    }

    @FormatAttribute(propertyName = "SDFact", propertyFormat = "N2")
    public BigDecimal dataFactor = new BigDecimal(0.01);

    public void setDataFactor(BigDecimal value) {
        this.dataFactor = value;
    }
}
```

#### Giải thích
- **Thuộc tính:** Các `@FormatAttribute` chú thích chỉ rõ cách từng thuộc tính được tuần tự hóa thành mã QR.
  - **NHẬN DẠNG**Mã định danh duy nhất cho chữ ký.
  - **Tác giả**: Người đã ký vào tài liệu.
  - **Ngày ký**: Dấu thời gian khi tài liệu được ký.
  - **Yếu tố dữ liệu**: Dữ liệu số bổ sung liên quan đến chữ ký.

### Chữ ký mã QR với dữ liệu tùy chỉnh và mã hóa

#### Tổng quan

Phần này trình bày cách ký tài liệu bằng mã QR bao gồm dữ liệu tuần tự tùy chỉnh và mã hóa.

```java
import com.groupdocs.signature.Signature;
import com.groupdocs.signature.domain.Padding;
import com.groupdocs.signature.domain.enums.HorizontalAlignment;
import com.groupdocs.signature.domain.enums.VerticalAlignment;
import com.groupdocs.signature.domain.extensions.encryption.IDataEncryption;
import com.groupdocs.signature.domain.qrcodes.QrCodeTypes;
import com.groupdocs.signature.exception.GroupDocsSignatureException;
import com.groupdocs.signature.options.sign.QrCodeSignOptions;
import java.io.File;
import java.math.BigDecimal;
import java.util.Date;
import java.util.UUID;

class SignWithQRCodeCustomSerialization {
    String filePath = "YOUR_DOCUMENT_DIRECTORY/sample.pdf"; 
    String outputFilePath = new File("YOUR_OUTPUT_DIRECTORY", "SignedQRCodeCustomSerialization.pdf").getPath();

    public void signDocument() throws Exception {
        Signature signature = new Signature(filePath);

        // Triển khai logic mã hóa tùy chỉnh của bạn tại đây
        IDataEncryption encryption = new CustomXOREncryption();

        DocumentSignatureData documentSignature = new DocumentSignatureData();
        documentSignature.setID(UUID.randomUUID().toString());
        documentSignature.setAuthor(System.getenv("USERNAME")); 
        documentSignature.setSigned(new Date());
        documentSignature.setDataFactor(new BigDecimal("11.22"));

        QrCodeSignOptions options = new QrCodeSignOptions();
        options.setData(documentSignature);
        options.setEncodeType(QrCodeTypes.QR);
        options.setDataEncryption(encryption);

        // Cấu hình căn chỉnh và giao diện
        options.setHeight(100);
        options.setWidth(100);
        options.setVerticalAlignment(VerticalAlignment.Bottom);
        options.setHorizontalAlignment(HorizontalAlignment.Right);
        
        Padding padding = new Padding();
        padding.setRight(10);
        padding.setBottom(10);
        options.setMargin(padding);

        signature.sign(outputFilePath, options);
    }
}
```

#### Giải thích
- **Mã hóa tùy chỉnh:** Triển khai logic mã hóa của riêng bạn trong `CustomXOREncryption` hoặc sử dụng bất kỳ phương pháp nào khác để thực hiện `IDataEncryption`.
- **Tùy chọn chữ ký:** Cấu hình giao diện và căn chỉnh mã QR bằng các tùy chọn như chiều cao, chiều rộng, khoảng đệm, v.v.
- **Quy trình ký kết:** Các `signature.sign()` phương pháp này áp dụng chữ ký mã QR vào tài liệu.

### Mẹo khắc phục sự cố

- Đảm bảo tất cả các phụ thuộc được cấu hình chính xác trong công cụ xây dựng của bạn (Maven/Gradle).
- Xác minh rằng đường dẫn tệp cho tài liệu đầu vào và đầu ra là chính xác.
- Xác nhận rằng logic mã hóa tùy chỉnh của bạn được triển khai và tích hợp đúng cách.

## Ứng dụng thực tế

Sau đây là một số ứng dụng thực tế của tính năng này:

1. **Ký kết văn bản pháp lý:** Ký hợp đồng một cách an toàn với siêu dữ liệu được nhúng trong mã QR để đảm bảo tính xác thực.
2. **Xử lý hóa đơn:** Tự động thêm chữ ký được mã hóa vào hóa đơn để tăng cường bảo mật và khả năng truy xuất.
3. **Theo dõi hậu cần:** Sử dụng tài liệu đã ký để theo dõi lô hàng, nhúng mã định danh duy nhất và dấu thời gian vào mã QR.
4. **Chứng chỉ học thuật:** Nhúng thông tin học sinh một cách an toàn vào chứng chỉ kỹ thuật số bằng chữ ký mã QR