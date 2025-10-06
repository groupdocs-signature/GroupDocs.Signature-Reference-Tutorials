---
"date": "2025-05-08"
"description": "Tìm hiểu cách triển khai ký mã QR Java bằng GroupDocs.Signature. Nâng cao bảo mật tài liệu, cấu hình tùy chọn ký và áp dụng mã hóa tùy chỉnh trong các ứng dụng Java của bạn."
"title": "Hướng dẫn ký mã QR Java - Bảo mật tài liệu của bạn với GroupDocs.Signature"
"url": "/vi/java/qr-code-signatures/java-qr-code-signing-groupdocs-signature/"
"weight": 1
type: docs
---
# Triển khai chữ ký mã QR Java với GroupDocs.Signature cho Java

## Giới thiệu

Nâng cao tính bảo mật cho tài liệu kỹ thuật số của bạn bằng cách nhúng mã QR vào các ứng dụng Java. Tận dụng GroupDocs.Signature cho Java cho phép bạn đảm bảo tính xác thực và khả năng truy xuất nguồn gốc của tài liệu một cách hiệu quả. Hướng dẫn này sẽ hướng dẫn bạn cách tạo chữ ký dữ liệu tùy chỉnh, cấu hình các tùy chọn ký mã QR và bảo mật tài liệu của bạn bằng mã hóa mạnh mẽ.

**Những gì bạn sẽ học:**
- Cách tạo lớp chữ ký dữ liệu tùy chỉnh bằng GroupDocs.Signature
- Cấu hình tùy chọn ký mã QR trong ứng dụng Java
- Ký tài liệu bằng mã QR và áp dụng mã hóa tùy chỉnh

Hãy cùng tìm hiểu các điều kiện tiên quyết và bắt đầu tích hợp chức năng này vào dự án của bạn!

## Điều kiện tiên quyết

Trước khi bắt đầu, hãy đảm bảo rằng bạn đã thiết lập các thư viện và phụ thuộc cần thiết trong môi trường phát triển của mình.

### Thư viện và phiên bản bắt buộc

Để triển khai GroupDocs.Signature cho Java, hãy bao gồm phần phụ thuộc sau:

**Maven**
```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

**Gradle**
```gradle
implementation 'com.groupdocs:groupdocs-signation:23.12'
```

Bạn cũng có thể tải xuống phiên bản mới nhất trực tiếp từ [GroupDocs.Signature cho các bản phát hành Java](https://releases.groupdocs.com/signature/java/).

### Yêu cầu thiết lập môi trường

- Đảm bảo bạn đã cài đặt Java Development Kit (JDK) đang hoạt động.
- Thiết lập Môi trường phát triển tích hợp (IDE) của bạn, chẳng hạn như IntelliJ IDEA hoặc Eclipse.

### Điều kiện tiên quyết về kiến thức

- Hiểu biết cơ bản về lập trình Java và các khái niệm hướng đối tượng.
- Quen thuộc với việc xử lý các phụ thuộc bằng Maven hoặc Gradle.

## Thiết lập GroupDocs.Signature cho Java

Để bắt đầu, hãy thiết lập GroupDocs.Signature trong dự án của bạn bằng cách làm theo hướng dẫn cài đặt ở trên để đưa vào cấu hình bản dựng.

### Các bước xin giấy phép

GroupDocs cung cấp nhiều tùy chọn cấp phép khác nhau:
- **Dùng thử miễn phí**: Kiểm tra tất cả các tính năng mà không có giới hạn.
- **Giấy phép tạm thời**: Xin giấy phép để đánh giá.
- **Mua**: Có được giấy phép đầy đủ để sử dụng cho mục đích thương mại.

Sau khi tải xuống, hãy khởi tạo GroupDocs.Signature như sau:

```java
import com.groupdocs.signature.Signature;

class InitializeGroupDocs {
    public static void main(String[] args) {
        Signature signature = new Signature("path/to/your/document");
        // Bây giờ bạn có thể bắt đầu sử dụng đối tượng chữ ký để làm việc với tài liệu.
    }
}
```

## Hướng dẫn thực hiện

Chúng ta hãy chia nhỏ quá trình triển khai thành các phần dễ quản lý, tập trung vào các tính năng chính.

### Lớp chữ ký dữ liệu tùy chỉnh

#### Tổng quan
Tạo một lớp tùy chỉnh để lưu trữ dữ liệu chữ ký như ID, tác giả, ngày ký và các yếu tố bổ sung. Điều này đảm bảo bạn có tất cả siêu dữ liệu cần thiết được đóng gói trong chữ ký của mình.

#### Triển khai từng bước

**Định nghĩa lớp DocumentSignatureData**

```java
import com.groupdocs.signature.domain.extensions.serialization.FormatAttribute;
import java.util.Date;
import java.math.BigDecimal;

class DocumentSignatureData {
    @FormatAttribute(propertyName = "SignID")
    public String ID; // Mã định danh duy nhất cho chữ ký
    
    public String getID() { return ID; }
    public void setID(String value) { ID = value; }
    
    @FormatAttribute(propertyName = "SAuth")
    public final String Author; // Tác giả của tài liệu
    
    public final String getAuthor() { return Author; }
    public final void setAuthor(String value) { Author = value; }
    
    @FormatAttribute(propertyName = "SDate", propertyFormat = "yyyy-MM-dd")
    public final Date Signed = new Date(); // Ngày và giờ ký
    
    public final Date getSigned() { return Signed; }
    public final void setSigned(Date value) { Signed = value; }
    
    @FormatAttribute(propertyName = "SDFact", propertyFormat = "N2")
    public final BigDecimal DataFactor = new BigDecimal(0.01); // Yếu tố dữ liệu bổ sung cho chữ ký
    
    public final BigDecimal getDataFactor() { return DataFactor; }
    public final void setDataFactor(BigDecimal value) { DataFactor = value; }
}
```

**Giải thích:**
- **Định dạng Thuộc tính**: Chú thích các thuộc tính để tùy chỉnh tuần tự hóa.
- **Của cải**: Ghi lại các thông tin cần thiết như ID duy nhất, tên tác giả, ngày ký và yếu tố dữ liệu.

### Cấu hình tùy chọn ký hiệu mã QR

#### Tổng quan
Cấu hình các tùy chọn ký mã QR để xác định cách mã QR của bạn sẽ xuất hiện trên tài liệu, bao gồm kích thước, căn chỉnh và khoảng đệm.

#### Triển khai từng bước

**Xác định lớp QrCodeSignOptionsConfig**

```java
import com.groupdocs.signature.domain.enums.HorizontalAlignment;
import com.groupdocs.signature.domain.enums.VerticalAlignment;
import com.groupdocs.signature.domain.qrcodes.QrCodeTypes;
import com.groupdocs.signature.domain.Padding;
import com.groupdocs.signature.options.sign.QrCodeSignOptions;

class QrCodeSignOptionsConfig {
    public static QrCodeSignOptions setupQrCodeSignOptions(DocumentSignatureData documentSignature) {
        QrCodeSignOptions options = new QrCodeSignOptions();
        
        // Tuần tự hóa đối tượng dữ liệu tùy chỉnh thành mã QR
        options.setData(documentSignature);
        
        // Chỉ định loại mã QR
        options.setEncodeType(QrCodeTypes.QR);
        
        // Cấu hình phần đệm để căn chỉnh
        Padding padding = new Padding();
        padding.setRight(10); // Đệm phải tính bằng pixel
        padding.setBottom(10); // Đệm dưới cùng tính bằng pixel
        options.setMargin(padding);
        
        // Xác định kích thước và vị trí của mã QR
        options.setHeight(100);
        options.setWidth(100);
        options.setVerticalAlignment(VerticalAlignment.Bottom);
        options.setHorizontalAlignment(HorizontalAlignment.Right);
        
        return options;
    }
}
```

**Giải thích:**
- **Tùy chọn Mã QRSign**: Quản lý cách hiển thị mã QR, bao gồm kích thước và vị trí của mã.
- **Đệm**Điều chỉnh căn chỉnh trong tài liệu.

### Ký tài liệu bằng mã QR và mã hóa tùy chỉnh

#### Tổng quan
Kết hợp mã QR và mã hóa tùy chỉnh để ký tài liệu một cách an toàn. Điều này đảm bảo tính toàn vẹn và bảo mật của dữ liệu.

#### Triển khai từng bước

**Ký tài liệu bằng mã QR**

```java
import com.groupdocs.signature.Signature;
import com.groupdocs.signature.domain.extensions.encryption.IDataEncryption;
import com.groupdocs.signature.exception.GroupDocsSignatureException;

import java.util.UUID;

class SignDocumentWithQRCode {
    public static void signDocument(String filePath, String outputFilePath) throws Exception {
        try {
            Signature signature = new Signature(filePath);

            // Chiến lược mã hóa XOR tùy chỉnh
            IDataEncryption encryption = new CustomXOREncryption();

            // Cấu hình đối tượng dữ liệu chữ ký tài liệu tùy chỉnh
            DocumentSignatureData documentSignature = new DocumentSignatureData();
            documentSignature.setID(UUID.randomUUID().toString());
            documentSignature.setAuthor(System.getenv("USERNAME"));
            documentSignature.setSigned(new Date());
            documentSignature.setDataFactor(new BigDecimal("11.22"));

            // Thiết lập tùy chọn Mã QR
            QrCodeSignOptions options = QrCodeSignOptionsConfig.setupQrCodeSignOptions(documentSignature);

            // Áp dụng mã hóa cho dữ liệu trong mã QR
            options.setDataEncryption(encryption);

            // Ký và lưu tài liệu
            signature.sign(outputFilePath, options);
        } catch (Exception e) {
            throw new GroupDocsSignatureException(e.getMessage());
        }
    }
}
```

**Giải thích:**
- **Mã hóa XOREncryption tùy chỉnh**: Triển khai chiến lược mã hóa tùy chỉnh để bảo mật dữ liệu mã QR.
- **UUID**: Tạo một mã định danh duy nhất cho mỗi chữ ký.