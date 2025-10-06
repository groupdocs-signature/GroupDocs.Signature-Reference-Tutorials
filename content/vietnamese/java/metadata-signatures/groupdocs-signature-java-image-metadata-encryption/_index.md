---
"date": "2025-05-08"
"description": "Tìm hiểu cách bảo mật siêu dữ liệu hình ảnh bằng mã hóa với GroupDocs.Signature cho Java. Đảm bảo tính toàn vẹn và xác thực của dữ liệu với hướng dẫn từng bước."
"title": "Triển khai ký và mã hóa siêu dữ liệu hình ảnh trong Java với GroupDocs.Signature"
"url": "/vi/java/metadata-signatures/groupdocs-signature-java-image-metadata-encryption/"
"weight": 1
type: docs
---
# Triển khai chữ ký siêu dữ liệu hình ảnh với mã hóa trong Java bằng GroupDocs.Signature

## Giới thiệu

Trong bối cảnh kỹ thuật số ngày nay, việc bảo mật thông tin nhạy cảm trong siêu dữ liệu tài liệu là vô cùng quan trọng. Dù là xử lý hợp đồng kinh doanh mật hay ảnh nhận dạng cá nhân, việc duy trì tính toàn vẹn và tính xác thực của siêu dữ liệu hình ảnh giúp ngăn chặn truy cập và giả mạo trái phép. **GroupDocs.Signature cho Java** cung cấp giải pháp mạnh mẽ để ký và mã hóa siêu dữ liệu hình ảnh một cách an toàn.

Hướng dẫn này hướng dẫn bạn cách triển khai ký siêu dữ liệu hình ảnh bằng mã hóa trong Java bằng các tính năng mạnh mẽ của GroupDocs.Signature. Bằng cách làm theo các bước này, bạn sẽ tích hợp chức năng này vào các ứng dụng Java của mình một cách hiệu quả.

**Những gì bạn sẽ học:**
- Ký siêu dữ liệu tài liệu bằng GroupDocs.Signature cho Java
- Triển khai chữ ký đối tượng tùy chỉnh với mã hóa
- Thiết lập môi trường an toàn bằng cách sử dụng mã hóa khóa đối xứng

## Điều kiện tiên quyết

Trước khi bắt đầu, hãy đảm bảo đáp ứng các điều kiện tiên quyết sau:

### Thư viện và phụ thuộc bắt buộc:
- **GroupDocs.Signature cho Java**: Đảm bảo bạn có phiên bản 23.12 trở lên.

### Yêu cầu thiết lập môi trường:
- Cài đặt Java Development Kit (JDK) trên máy của bạn.
- Sử dụng Môi trường phát triển tích hợp (IDE) như IntelliJ IDEA, Eclipse hoặc NetBeans.

### Điều kiện tiên quyết về kiến thức:
- Hiểu biết cơ bản về lập trình Java.
- Quen thuộc với Maven hoặc Gradle để quản lý sự phụ thuộc.

## Thiết lập GroupDocs.Signature cho Java

Để sử dụng GroupDocs.Signature trong dự án của bạn, hãy bao gồm các phụ thuộc cần thiết như sau:

### Sử dụng Maven
Thêm điều này vào `pom.xml` tài liệu:
```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

### Sử dụng Gradle
Bao gồm điều này trong `build.gradle` tài liệu:
```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

### Tải xuống trực tiếp
Ngoài ra, hãy tải xuống phiên bản mới nhất từ [GroupDocs.Signature cho các bản phát hành Java](https://releases.groupdocs.com/signature/java/).

#### Các bước xin giấy phép
- **Dùng thử miễn phí**: Bắt đầu bằng bản dùng thử để khám phá các tính năng.
- **Giấy phép tạm thời**: Áp dụng cho xét nghiệm mở rộng nếu cần thiết.
- **Mua**: Xin giấy phép sử dụng sản xuất từ [GroupDocs](https://purchase.groupdocs.com/buy).

## Khởi tạo và thiết lập cơ bản

Sau đây là cách bạn có thể khởi tạo GroupDocs.Signature trong ứng dụng Java của mình:

```java
import com.groupdocs.signature.Signature;

public class InitializeSignature {
    public static void main(String[] args) {
        // Đường dẫn đến tài liệu
        String filePath = "path/to/your/document.jpg";
        
        // Tạo một phiên bản mới của Signature
        Signature signature = new Signature(filePath);

        System.out.println("GroupDocs.Signature initialized successfully.");
    }
}
```

## Hướng dẫn thực hiện

### Tính năng: Chữ ký siêu dữ liệu với Đối tượng tùy chỉnh

#### Tổng quan
Tính năng này cho phép ký siêu dữ liệu hình ảnh bằng một đối tượng tùy chỉnh và mã hóa nó để tăng cường bảo mật, đảm bảo rằng chỉ những bên được ủy quyền mới có thể truy cập hoặc sửa đổi siêu dữ liệu.

#### Triển khai từng bước

##### 1. Xác định lớp dữ liệu chữ ký tài liệu của bạn
Tạo một lớp để lưu trữ thông tin siêu dữ liệu của bạn:

```java
import java.math.BigDecimal;
import java.util.Date;

class DocumentSignatureData {
    private String ID;
    private String Author;
    private Date Signed = new Date();
    private BigDecimal DataFactor = new BigDecimal(0.01);

    public String getID() { return ID; }
    public void setID(String value) { ID = value; }

    @FormatAttribute(propertyName = "SignID")
    public final String getAuthor() { return Author; }
    public final void setAuthor(String value) { Author = value; }

    @FormatAttribute(propertyName = "SAuth")
    public final Date getSigned() { return Signed; }
    public final void setSigned(Date value) { Signed = value; }

    @FormatAttribute(propertyName = "SDate", propertyFormat = "yyyy-MM-dd")
    public final BigDecimal getDataFactor() { return DataFactor; }
    public final void setDataFactor(BigDecimal value) { DataFactor = value; }
}
```

##### 2. Triển khai Logic Chữ ký
Sau đây là cách ký siêu dữ liệu bằng mã hóa:

```java
import com.groupdocs.signature.Signature;
import com.groupdocs.signature.domain.extensions.encryption.IDataEncryption;
import com.groupdocs.signature.domain.extensions.encryption.SymmetricAlgorithmType;
import com.groupdocs.signature.domain.extensions.encryption.SymmetricEncryption;
import com.groupdocs.signature.domain.signatures.metadata.ImageMetadataSignature;
import com.groupdocs.signature.exception.GroupDocsSignatureException;
import com.groupdocs.signature.options.sign.MetadataSignOptions;

import java.io.File;
import java.nio.file.Paths;
import java.util.UUID;

public class SignMetadataWithCustomObject {
    // Khởi tạo đường dẫn tệp bằng trình giữ chỗ
    String filePath = "YOUR_DOCUMENT_DIRECTORY/SampleImage.jpg";
    String outputFilePath = new File("YOUR_OUTPUT_DIRECTORY", 
                                       "SignedImageWithCustomMetadata/SampleImage_signed.jpg").getPath();

    public void run() throws Exception {
        Signature signature = new Signature(filePath);

        // Thiết lập khóa và mật khẩu để mã hóa
        String key = "1234567890";
        String salt = "1234567890";
        IDataEncryption encryption = new SymmetricEncryption(
            SymmetricAlgorithmType.Rijndael, key, salt);

        MetadataSignOptions options = new MetadataSignOptions();
        DocumentSignatureData documentSignature = new DocumentSignatureData();
        
        // Đặt thuộc tính siêu dữ liệu tùy chỉnh
        documentSignature.setID(UUID.randomUUID().toString());
        documentSignature.setAuthor(System.getenv("USERNAME"));
        documentSignature.setSigned(new Date());
        documentSignature.setDataFactor(new BigDecimal("11.22"));

        ImageMetadataSignature mdDocument = new ImageMetadataSignature(41996, documentSignature);
        mdDocument.setDataEncryption(encryption);

        // Thêm chữ ký siêu dữ liệu vào các tùy chọn
        options.getSignatures().add(mdDocument);

        signature.sign(outputFilePath, options);
    }
}
```

#### Tùy chọn cấu hình chính
- **Mã hóa đối xứng**: Sử dụng thuật toán Rijndael để mã hóa.
- **Siêu dữ liệu SignOptions**: Cấu hình quy trình ký và chỉ định siêu dữ liệu nào sẽ được ký.

##### Mẹo khắc phục sự cố
- Đảm bảo đường dẫn tệp của bạn chính xác và có thể truy cập được.
- Kiểm tra xem biến môi trường `USERNAME` được thiết lập đúng cách.
- Xác minh rằng phiên bản thư viện GroupDocs.Signature khớp với mã phụ thuộc của bạn.

### Tính năng: Chữ ký siêu dữ liệu có mã hóa

#### Tổng quan
Tính năng này tập trung vào việc mã hóa chữ ký siêu dữ liệu để bảo vệ thông tin nhạy cảm trong các tệp hình ảnh.

#### Triển khai từng bước
##### 1. Triển khai Logic mã hóa
Sau đây là cách ký siêu dữ liệu bằng mã hóa:
```java
import com.groupdocs.signature.Signature;
import com.groupdocs.signature.domain.extensions.encryption.IDataEncryption;
import com.groupdocs.signature.domain.extensions.encryption.SymmetricAlgorithmType;
import com.groupdocs.signature.domain.extensions.encryption.SymmetricEncryption;
import com.groupdocs.signature.exception.GroupDocsSignatureException;
import com.groupdocs.signature.options.sign.MetadataSignOptions;

import java.io.File;
import java.nio.file.Paths;
import java.util.UUID;

public class SignMetadataWithEncryption {
    // Khởi tạo đường dẫn tệp bằng trình giữ chỗ
    String filePath = "YOUR_DOCUMENT_DIRECTORY/SampleImage.jpg";
    String outputFilePath = new File("YOUR_OUTPUT_DIRECTORY", 
                                       "SignedImageWithEncryption/SampleImage_signed.jpg").getPath();

    public void run() throws Exception {
        Signature signature = new Signature(filePath);

        // Thiết lập khóa và mật khẩu để mã hóa
        String key = "1234567890";
        String salt = "1234567890";
        IDataEncryption encryption = new SymmetricEncryption(
            SymmetricAlgorithmType.Rijndael, key, salt);

        MetadataSignOptions options = new MetadataSignOptions();
        DocumentSignatureData documentSignature = new DocumentSignatureData();
        
        // Đặt thuộc tính siêu dữ liệu tùy chỉnh
        documentSignature.setID(UUID.randomUUID().toString());
        documentSignature.setAuthor(System.getenv("USERNAME"));
        documentSignature.setSigned(new Date());
        documentSignature.setDataFactor(new BigDecimal("11.22"));

        ImageMetadataSignature mdDocument = new ImageMetadataSignature(41996, documentSignature);
        mdDocument.setDataEncryption(encryption);

        // Thêm chữ ký siêu dữ liệu vào các tùy chọn
        options.getSignatures().add(mdDocument);

        signature.sign(outputFilePath, options);
    }
}
```