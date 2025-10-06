---
"date": "2025-05-08"
"description": "Học cách ký, xác minh, tìm kiếm, cập nhật và xóa chữ ký mã vạch trong tài liệu bằng GroupDocs.Signature cho Java. Nâng cao hiệu quả quy trình làm việc với tài liệu của bạn."
"title": "Chữ ký tài liệu chính trong Java với GroupDocs.Signature&#58; Hướng dẫn về chữ ký mã vạch"
"url": "/vi/java/digital-signatures/java-document-signature-groupdocs-signature-barcode/"
"weight": 1
type: docs
---
# Làm chủ chữ ký tài liệu trong Java với GroupDocs.Signature

**Tối ưu hóa quy trình làm việc tài liệu kỹ thuật số của bạn bằng cách ký, xác minh, tìm kiếm, cập nhật và xóa chữ ký mã vạch bằng GroupDocs.Signature cho Java.**

Trong thế giới tương tác số đầy biến động, việc quản lý tài liệu hiệu quả là vô cùng quan trọng. Dù xử lý hợp đồng hay bất kỳ giấy tờ quan trọng nào, khả năng ký, xác minh, tìm kiếm, cập nhật và xóa chữ ký tài liệu đều giúp tăng đáng kể năng suất và bảo mật. Hướng dẫn toàn diện này sẽ hướng dẫn bạn cách sử dụng GroupDocs.Signature for Java — một thư viện mạnh mẽ giúp đơn giản hóa các tác vụ này với chữ ký mã vạch.

**Những gì bạn sẽ học:**
- Cách ký tài liệu bằng chữ ký mã vạch.
- Các kỹ thuật để xác minh tính xác thực của các tài liệu đã ký.
- Phương pháp tìm kiếm, cập nhật và xóa chữ ký mã vạch hiện có trong tài liệu của bạn.
- Ứng dụng thực tế và mẹo tối ưu hóa hiệu suất.

Trước khi đi sâu vào chi tiết triển khai, hãy đảm bảo bạn có mọi thứ cần thiết để bắt đầu.

## Điều kiện tiên quyết

Để làm theo hướng dẫn này, bạn sẽ cần:
- **Bộ phát triển Java (JDK):** Đảm bảo JDK 8 trở lên đã được cài đặt trên hệ thống của bạn.
- **Môi trường phát triển tích hợp (IDE):** Chúng tôi khuyên bạn nên sử dụng IntelliJ IDEA hoặc Eclipse để phát triển Java.
- **Thư viện GroupDocs.Signature:** Thư viện này rất cần thiết cho việc ký và xác minh tài liệu.

### Thư viện và phụ thuộc bắt buộc

Bạn có thể thêm GroupDocs.Signature vào dự án của mình bằng Maven, Gradle hoặc bằng cách tải trực tiếp JAR:

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
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

Đối với những người thích tải xuống trực tiếp, phiên bản mới nhất có thể được tìm thấy tại [GroupDocs.Signature cho các bản phát hành Java](https://releases.groupdocs.com/signature/java/).

### Mua lại giấy phép

Để khám phá toàn bộ tính năng của GroupDocs.Signature, hãy cân nhắc việc mua giấy phép tạm thời hoặc đăng ký. Bạn có thể bắt đầu dùng thử miễn phí để kiểm tra các tính năng:

- **Dùng thử miễn phí:** Ghé thăm [Trang tải xuống GroupDocs](https://releases.groupdocs.com/signature/java/) cho những bước đi đầu tiên của bạn.
- **Giấy phép tạm thời:** Có được nó thông qua [Trang giấy phép tạm thời của GroupDocs](https://purchase.groupdocs.com/temporary-license/).
- **Tùy chọn mua hàng:** Để sử dụng lâu dài, hãy đến [Tùy chọn mua GroupDocs](https://purchase.groupdocs.com/buy).

### Thiết lập môi trường

Đảm bảo bạn đã có một dự án Java sẵn sàng trong IDE ưa thích của mình. Cấu hình đường dẫn xây dựng hoặc `pom.xml` (cho Maven) hoặc `build.gradle` (cho Gradle) tệp với sự phụ thuộc GroupDocs.Signature. Sau khi thiết lập, hãy khởi tạo thư viện trong dự án của bạn bằng cách tạo một phiên bản của `Signature`.

## Thiết lập GroupDocs.Signature cho Java

GroupDocs.Signature đơn giản hóa quy trình ký và xác minh tài liệu bằng nhiều loại chữ ký khác nhau, bao gồm cả mã vạch. Hãy bắt đầu bằng cách nhập các lớp cần thiết:

```java
import com.groupdocs.signature.Signature;
```

### Khởi tạo cơ bản

Để khởi tạo GroupDocs.Signature trong ứng dụng Java của bạn, hãy tạo một `Signature` đối tượng có đường dẫn đến tài liệu mục tiêu của bạn:

```java
Signature signature = new Signature("path/to/your/document.pdf");
```

Với thiết lập này, bạn đã sẵn sàng triển khai nhiều chức năng khác nhau do GroupDocs.Signature cung cấp.

## Hướng dẫn thực hiện

### Ký tài liệu bằng chữ ký mã vạch

**Tổng quan:** Tính năng này cho phép bạn thêm chữ ký mã vạch vào bất kỳ tài liệu nào. Mã vạch có thể bao gồm văn bản như tên hoặc số nhận dạng để tăng cường bảo mật và dễ dàng xác minh.

#### Triển khai từng bước:
1. **Xác định đường dẫn:**
   Chỉ định đường dẫn cho tài liệu đầu vào và đầu ra của bạn:
   
   ```java
   String filePath = "YOUR_DOCUMENT_DIRECTORY/sample.docx";
   String outputFilePath = "YOUR_OUTPUT_DIRECTORY/signed_sample.docx";
   ```

2. **Tạo đối tượng chữ ký:**
   Khởi tạo một `Signature` đối tượng với đường dẫn tài liệu của bạn:

   ```java
   Signature signature = new Signature(filePath);
   ```

3. **Đặt tùy chọn mã vạch:**
   Cấu hình các tùy chọn cho ký hiệu mã vạch, bao gồm văn bản, loại, căn chỉnh, kích thước và màu sắc:

   ```java
   BarcodeSignOptions signOptions = new BarcodeSignOptions("John Smith", BarcodeTypes.Code128);
   signOptions.setVerticalAlignment(VerticalAlignment.Top);
   signOptions.setHorizontalAlignment(HorizontalAlignment.Center);
   signOptions.setWidth(100);
   signOptions.setHeight(40);
   signOptions.setMargin(new java.awt.Rectangle(20, 20, 0, 0));
   signOptions.setForeColor(Color.RED);

   SignatureFont signatureFont = new SignatureFont();
   signatureFont.setSize(12);
   signatureFont.setFamilyName("Comic Sans MS");
   signOptions.setFont(signatureFont);
   ```

4. **Ký vào tài liệu:**
   Áp dụng chữ ký mã vạch đã cấu hình của bạn vào tài liệu:

   ```java
   signature.sign(outputFilePath, signOptions);
   ```

### Xác minh tài liệu để có chữ ký mã vạch

**Tổng quan:** Đảm bảo tính toàn vẹn và xác thực của tài liệu đã ký bằng cách xác minh chữ ký mã vạch.

#### Triển khai từng bước:
1. **Xác minh thiết lập:**
   Tải tài liệu đã ký của bạn vào `Signature` sự vật:

   ```java
   Signature signature = new Signature("YOUR_OUTPUT_DIRECTORY/signed_sample.docx");
   ```

2. **Cấu hình tùy chọn xác minh:**
   Đặt tùy chọn xác minh để khớp với chữ ký mã vạch cụ thể:

   ```java
   BarcodeVerifyOptions verifyOptions = new BarcodeVerifyOptions();
   verifyOptions.setAllPages(false); // Chỉ xác minh trang đầu tiên
   verifyOptions.setPageNumber(1);
   verifyOptions.setEncodeType(BarcodeTypes.Code128);
   verifyOptions.setText("John Smith");
   ```

3. **Thực hiện xác minh:**
   Thực hiện quá trình xác minh và kiểm tra xem chữ ký có hợp lệ không:

   ```java
   boolean isValid = signature.verify(verifyOptions) != null;
   ```

### Tìm kiếm tài liệu cho chữ ký mã vạch

**Tổng quan:** Nhanh chóng xác định vị trí chữ ký mã vạch trong tài liệu để xác nhận sự hiện diện của chúng hoặc thu thập thông tin.

#### Triển khai từng bước:
1. **Khởi tạo tìm kiếm:**
   Tải tài liệu của bạn vào `Signature` lớp học:

   ```java
   Signature signature = new Signature("YOUR_OUTPUT_DIRECTORY/signed_sample.docx");
   ```

2. **Đặt tùy chọn tìm kiếm:**
   Xác định các tùy chọn để tìm kiếm chữ ký mã vạch trên tất cả các trang của tài liệu:

   ```java
   BarcodeSearchOptions searchOptions = new BarcodeSearchOptions();
   searchOptions.setAllPages(true);
   ```

3. **Thực hiện tìm kiếm:**
   Lấy danh sách chữ ký mã vạch đã tìm thấy:

   ```java
   java.util.List<BarcodeSignature> signatures = signature.search(BarcodeSignature.class, searchOptions);
   ```

### Cập nhật chữ ký mã vạch tài liệu

**Tổng quan:** Sửa đổi chữ ký mã vạch hiện có trong tài liệu của bạn để phản ánh những thay đổi hoặc cập nhật.

#### Triển khai từng bước:
1. **Chuẩn bị cho bản cập nhật:**
   Giả sử bạn có danh sách chữ ký được lấy từ hoạt động tìm kiếm trước đó:

   ```java
   List<BarcodeSignature> signaturesToUpdate = new ArrayList<>();
   ```

2. **Sửa đổi Thuộc tính Chữ ký:**
   Điều chỉnh các thuộc tính như vị trí và kích thước để cập nhật chữ ký:

   ```java
   if (!signaturesToUpdate.isEmpty()) {
       BarcodeSignature bcSignature = signaturesToUpdate.get(0);
       bcSignature.setLeft(bcSignature.getLeft() + 100);
       bcSignature.setTop(bcSignature.getTop() + 100);
       bcSignature.setWidth(200);
       bcSignature.setHeight(50);
   }
   ```

3. **Áp dụng bản cập nhật:**
   Lưu các thay đổi vào tài liệu của bạn:

   ```java
   ByteArrayOutputStream outputStream = new ByteArrayOutputStream();
   signature.update(outputStream, signaturesToUpdate);
   ```

### Xóa chữ ký mã vạch tài liệu

**Tổng quan:** Xóa chữ ký mã vạch không cần thiết hoặc lỗi thời khỏi tài liệu.

#### Triển khai từng bước:
1. **Chuẩn bị xóa:**
   Giả sử bạn có danh sách chữ ký được lấy từ hoạt động tìm kiếm trước đó:

   ```java
   List<BarcodeSignature> signaturesToDelete = new ArrayList<>();
   ```

2. **Xóa chữ ký:**
   Xóa chữ ký mã vạch đã chỉ định khỏi tài liệu của bạn:

   ```java
   signature.delete(signaturesToDelete);
   ```