---
"date": "2025-05-08"
"description": "Tìm hiểu cách bảo mật tệp PDF bằng mã hóa mã QR và chữ ký số với GroupDocs.Signature cho Java. Nâng cao hiệu quả bảo mật tài liệu của bạn."
"title": "Triển khai chữ ký PDF an toàn với mã hóa mã QR trong Java bằng GroupDocs.Signature"
"url": "/vi/java/qr-code-signatures/secure-pdf-signing-qr-code-groupdocs-java/"
"weight": 1
---

# Cách triển khai chữ ký PDF an toàn với mã hóa mã QR trong Java bằng GroupDocs.Signature

Trong thời đại kỹ thuật số ngày nay, việc bảo mật thông tin nhạy cảm trong tài liệu là vô cùng quan trọng. Sự gia tăng của các mối đe dọa an ninh mạng đã khiến mã hóa dữ liệu trở thành một phần thiết yếu trong quản lý tài liệu. Hướng dẫn này sẽ hướng dẫn bạn cách triển khai chữ ký PDF an toàn bằng mã hóa mã QR với GroupDocs.Signature for Java. Sau khi hoàn thành bài viết này, bạn sẽ được trang bị đầy đủ để tích hợp các tính năng bảo mật mạnh mẽ vào ứng dụng của mình.

## Những gì bạn sẽ học:
- Hiểu về mã hóa dữ liệu đối xứng trong Java
- Tạo một lớp chữ ký tùy chỉnh
- Cấu hình chữ ký mã QR với dữ liệu tùy chỉnh và căn chỉnh
- Tích hợp GroupDocs.Signature để ký PDF an toàn

Bạn đã sẵn sàng chưa? Hãy bắt đầu thôi!

## Điều kiện tiên quyết
Trước khi bắt đầu, hãy đảm bảo bạn có những điều sau:
- **Bộ phát triển Java (JDK):** Phiên bản 8 trở lên.
- **Maven hoặc Gradle:** Để quản lý sự phụ thuộc. Chọn dựa trên thiết lập dự án của bạn.
- **Kiến thức về lập trình Java:** Hiểu biết cơ bản về lập trình hướng đối tượng trong Java.

## Thiết lập GroupDocs.Signature cho Java
Để bắt đầu sử dụng GroupDocs.Signature, bạn cần thêm nó vào dự án của mình. Thư viện này cung cấp các công cụ mạnh mẽ để quản lý chữ ký số và mã hóa tài liệu.

### Thiết lập Maven
Thêm sự phụ thuộc sau vào `pom.xml` tài liệu:
```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

### Thiết lập Gradle
Đối với người dùng Gradle, hãy bao gồm điều này trong `build.gradle` tài liệu:
```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

### Tải xuống trực tiếp
Ngoài ra, hãy tải xuống phiên bản mới nhất từ [GroupDocs.Signature cho các bản phát hành Java](https://releases.groupdocs.com/signature/java/).

### Mua lại giấy phép
Bạn có thể bắt đầu dùng thử GroupDocs.Signature miễn phí để đánh giá các tính năng. Để sử dụng lâu dài, hãy cân nhắc mua giấy phép hoặc đăng ký giấy phép tạm thời thông qua trang web của họ.

## Hướng dẫn thực hiện
Hướng dẫn này được chia thành các phần chính bao gồm mã hóa dữ liệu, tạo chữ ký tùy chỉnh và cấu hình chữ ký mã QR.

### Mã hóa dữ liệu bằng thuật toán đối xứng
Mã hóa dữ liệu của bạn đảm bảo dữ liệu được bảo mật trong quá trình truyền tải và lưu trữ. Sau đây là cách thiết lập mã hóa đối xứng bằng GroupDocs.Signature:

#### Thiết lập mã hóa đối xứng
1. **Nhập các gói cần thiết:**
   ```java
   import com.groupdocs.signature.domain.extensions.encryption.IDataEncryption;
   import com.groupdocs.signature.domain.extensions.encryption.SymmetricAlgorithmType;
   import com.groupdocs.signature.domain.extensions.encryption.SymmetricEncryption;
   ```
2. **Khởi tạo Đối tượng mã hóa:**
   Sử dụng khóa bảo mật và muối để mã hóa. Thay thế `"YOUR_SECURE_KEY"` với chìa khóa của riêng bạn.
   ```java
   String key = "YOUR_SECURE_KEY";
   String salt = "YOUR_SECURE_SALT";

   IDataEncryption encryption = new SymmetricEncryption(
       SymmetricAlgorithmType.Rijndael, 
       key, 
       salt
   );
   ```
   - **SymmetricAlgorithmType.Rijndael:** Phần này chỉ rõ loại thuật toán đối xứng cần sử dụng.
   - **Chìa khóa và muối:** Đảm bảo chúng là duy nhất và an toàn cho ứng dụng của bạn.

### Lớp chữ ký dữ liệu tùy chỉnh
Việc tạo một lớp tùy chỉnh cho phép bạn quản lý các thuộc tính chữ ký một cách hiệu quả. Cách thực hiện như sau:

#### Định nghĩa `DocumentSignatureData` Lớp học
```java
class DocumentSignatureData {
    private String ID;
    private String Author;
    private Date Signed = new Date();
    private BigDecimal DataFactor = new BigDecimal(0.01);

    public String getID() { return ID; }
    public void setID(String value) { ID = value; }

    public final String getAuthor() { return Author; }
    public final void setAuthor(String value) { Author = value; }

    public final Date getSigned() { return Signed; }
    public final void setSigned(Date value) { Signed = value; }

    public final BigDecimal getDataFactor() { return DataFactor; }
    public final void setDataFactor(BigDecimal value) { DataFactor = value; }
}
```
- **ID, Tác giả, Chữ ký:** Các trường này lưu trữ siêu dữ liệu của chữ ký.
- **Yếu tố dữ liệu:** Lưu trữ giá trị số có liên quan đến logic của ứng dụng của bạn.

### Tùy chọn chữ ký mã QR
Mã QR cung cấp một cách thức nhúng thông tin gọn nhẹ. Hãy cấu hình chúng với dữ liệu tùy chỉnh và mã hóa:

#### Thiết lập chữ ký mã QR
1. **Khởi tạo `Signature` Sự vật:**
   ```java
   import com.groupdocs.signature.Signature;
   
   Signature signature = new Signature("YOUR_DOCUMENT_DIRECTORY");
   ```
2. **Cấu hình tùy chọn mã QR:**
   ```java
   import com.groupdocs.signature.domain.qrcodes.QrCodeTypes;
   import com.groupdocs.signature.options.sign.QrCodeSignOptions;
   import java.util.UUID;

   DocumentSignatureData documentSignature = new DocumentSignatureData();
   documentSignature.setID(UUID.randomUUID().toString());
   documentSignature.setAuthor(System.getenv("USERNAME"));
   documentSignature.setDataFactor(new BigDecimal("11.22"));

   QrCodeSignOptions options = new QrCodeSignOptions();
   options.setData(documentSignature);
   options.setEncodeType(QrCodeTypes.QR);
   options.setDataEncryption(encryption); // Sử dụng đối tượng mã hóa
   options.setHeight(100);
   options.setWidth(100);
   options.setVerticalAlignment(com.groupdocs.signature.domain.enums.VerticalAlignment.Bottom);
   options.setHorizontalAlignment(com.groupdocs.signature.domain.enums.HorizontalAlignment.Right);

   import com.groupdocs.signature.domain.Padding;
   Padding padding = new Padding();
   padding.setRight(10);
   padding.setBottom(10);
   options.setMargin(padding);
   ```
   - **Loại mã hóa:** Chỉ định định dạng mã QR.
   - **Căn chỉnh và lề:** Tùy chỉnh cách mã QR xuất hiện trên tài liệu.

### Ví dụ sử dụng
Để ký một tài liệu bằng các tùy chọn đã cấu hình của bạn:
```java
signature.sign("YOUR_OUTPUT_DIRECTORY/QRCodeEncryptedObject.pdf\