---
"date": "2025-05-08"
"description": "Tìm hiểu cách sử dụng GroupDocs.Signature for Java để ký tài liệu an toàn bằng mã QR mã hóa dữ liệu HIBC. Tối ưu hóa quy trình quản lý tài liệu của bạn ngay hôm nay."
"title": "Hướng dẫn toàn diện về ký tài liệu bằng mã QR sử dụng GroupDocs.Signature cho Java"
"url": "/vi/java/qr-code-signatures/groupdocs-signature-qr-code-document-signing/"
"weight": 1
---

# Chữ ký tài liệu chính bằng mã QR sử dụng GroupDocs.Signature cho Java

## Giới thiệu

Trong kỷ nguyên số, việc quản lý và bảo mật dữ liệu dược phẩm hiệu quả là rất quan trọng để đảm bảo tuân thủ và hiệu quả hoạt động. Việc tích hợp thông tin sản phẩm toàn diện vào tài liệu có thể là một thách thức. Hướng dẫn này sẽ trình bày cách sử dụng **GroupDocs.Signature cho Java** để mã hóa dữ liệu Mã vạch ngành y tế (HIBC) trong mã QR và ký tài liệu một cách liền mạch.

### Những gì bạn sẽ học:
- Thiết lập GroupDocs.Signature cho Java.
- Tạo các phiên bản của HIBCLICPrimaryData, HIBCLICSecondaryAdditionalData và dạng kết hợp của chúng.
- Ký tài liệu bằng mã QR mã hóa thông tin chi tiết về sản phẩm.
- Tối ưu hóa hiệu suất trong khi quản lý tài nguyên hiệu quả.

## Điều kiện tiên quyết

### Thư viện và phụ thuộc bắt buộc
Để sử dụng GroupDocs.Signature cho Java, hãy đảm bảo bạn có:
- **Bộ phát triển Java (JDK)**: Phiên bản 8 trở lên.
- **Maven** hoặc **Gradle**: Để quản lý sự phụ thuộc.

### Yêu cầu thiết lập môi trường
Đảm bảo môi trường phát triển của bạn được cấu hình để sử dụng Maven hoặc Gradle, giúp đơn giản hóa việc quản lý phụ thuộc và xây dựng dự án.

### Điều kiện tiên quyết về kiến thức
Sự quen thuộc với lập trình Java sẽ giúp hiểu được các đoạn mã và chi tiết triển khai.

## Thiết lập GroupDocs.Signature cho Java

### Thông tin cài đặt

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

**Tải xuống trực tiếp**: Tải xuống phiên bản mới nhất từ [GroupDocs.Signature cho các bản phát hành Java](https://releases.groupdocs.com/signature/java/).

### Các bước xin giấy phép
1. **Dùng thử miễn phí**: Bắt đầu bằng cách tải xuống bản dùng thử để kiểm tra các chức năng cơ bản.
2. **Giấy phép tạm thời**: Nhận quyền truy cập đầy đủ mà không bị giới hạn trong thời gian đánh giá của bạn.
3. **Mua**: Hãy cân nhắc việc mua giấy phép cho các dự án dài hạn.

#### Khởi tạo và thiết lập cơ bản
Sau khi cài đặt, khởi tạo `Signature` đối tượng có đường dẫn tệp của tài liệu bạn muốn ký:
```java
String filePath = "Sample.pdf";
Signature signature = new Signature(filePath);
```

## Hướng dẫn thực hiện

### Tạo dữ liệu chính của HIBC LIC
**Tổng quan**: Phần này trình bày cách tạo và cấu hình một phiên bản của `HIBCLICPrimaryData`, nơi chứa thông tin sản phẩm cần thiết.

#### Bước 1: Khởi tạo đối tượng dữ liệu chính
```java
HIBCLICPrimaryData primaryData = new HIBCLICPrimaryData();
```

#### Bước 2: Thiết lập các thuộc tính thiết yếu
- **Số sản phẩm hoặc danh mục**: Mã định danh duy nhất cho sản phẩm.
- **Mã nhận dạng người dán nhãn**: Xác định nhà sản xuất.
- **ID đơn vị đo lường**: Chỉ định đơn vị đo lường.

```java
primaryData.setProductOrCatalogNumber("12345");
primaryData.setLabelerIdentificationCode("A999");
primaryData.setUnitOfMeasureID(1);
```

### Tạo dữ liệu bổ sung thứ cấp của HIBC LIC
**Tổng quan**: Phần này bao gồm việc tạo và cấu hình một phiên bản của `HIBCLICSecondaryAdditionalData`, bao gồm các thông tin chi tiết bổ sung như ngày hết hạn và số lô.

#### Bước 1: Khởi tạo đối tượng dữ liệu thứ cấp
```java
HIBCLICSecondaryAdditionalData secondaryData = new HIBCLICSecondaryAdditionalData();
```

#### Bước 2: Thiết lập các thuộc tính bổ sung
- **Ngày hết hạn**: Sử dụng ngày hiện tại để trình diễn.
- **Số lượng, Số lô, Số sê-ri**: Xác định thông số cụ thể của sản phẩm.
- **Ngày sản xuất và ký tự liên kết**: Thiết lập chi tiết sản xuất.

```java
secondaryData.setExpiryDate(new Date());
secondaryData.setExpiryDateFormat(HIBCLICDateFormat.MMDDYY);
secondaryData.setQuantity(30);
secondaryData.setLotNumber("LOT123");
secondaryData.setSerialNumber("SERIAL123");
secondaryData.setDateOfManufacture(new Date());
secondaryData.setLinkCharacter('S');
```

### Kết hợp dữ liệu chính và phụ của HIBC LIC
**Tổng quan**: Tìm hiểu cách hợp nhất dữ liệu chính và dữ liệu phụ thành một `HIBCLICCombinedData` đối tượng để xử lý hợp lý.

#### Bước 1: Khởi tạo đối tượng dữ liệu kết hợp
```java
HIBCLICCombinedData combinedData = new HIBCLICCombinedData();
```

#### Bước 2: Thiết lập dữ liệu chính và dữ liệu phụ
- Liên kết cả hai tập dữ liệu để tạo thành một cấu trúc dữ liệu hoàn chỉnh.

```java
combinedData.setPrimaryData(primaryData);
combinedData.setSecondaryAdditionalData(secondaryData);
```

### Ký tài liệu bằng mã QR chứa dữ liệu kết hợp HIBC LIC
**Tổng quan**:Phần cuối cùng này trình bày cách ký tài liệu bằng mã QR mã hóa dữ liệu HIBC kết hợp.

#### Bước 1: Xác định đường dẫn tệp
```java
String filePath = "YOUR_DOCUMENT_DIRECTORY/Sample.pdf";
String outputFilePath = "YOUR_OUTPUT_DIRECTORY/SignWithQRCodeHIBCLICCombinedData/" + fileName;
```

#### Bước 2: Thiết lập tùy chọn ký mã QR
- **Loại mã hóa**: Sử dụng `QrCodeTypes.HIBCLICQR` để chỉ định loại mã hóa.
- **Phân công dữ liệu**: Truyền dữ liệu kết hợp để đưa vào mã QR.

```java
Signature signature = new Signature(filePath);
try {
    QrCodeSignOptions options = new QrCodeSignOptions();
    options.setEncodeType(QrCodeTypes.HIBCLICQR);
    options.setData(combinedData);

    // Ký và lưu tài liệu
    signature.sign(outputFilePath, options);
} finally {
    if (signature != null) signature.dispose();
}
```

## Ứng dụng thực tế
1. **Tuân thủ dược phẩm**Tăng cường tuân thủ các tiêu chuẩn quy định bằng cách sử dụng tích hợp này.
2. **Quản lý chuỗi cung ứng**: Nâng cao khả năng truy xuất nguồn gốc dược phẩm thông qua mã QR trong tài liệu.
3. **Tích hợp hệ thống chăm sóc sức khỏe**: Nhúng dữ liệu sản phẩm toàn diện vào hồ sơ chăm sóc sức khỏe để đảm bảo an toàn cho bệnh nhân tốt hơn.

## Cân nhắc về hiệu suất
- **Tối ưu hóa việc sử dụng tài nguyên**: Đảm bảo quản lý bộ nhớ hiệu quả bằng cách loại bỏ `Signature` đối tượng sau khi phẫu thuật.
- **Thực hành tốt nhất**: Thường xuyên cập nhật lên phiên bản GroupDocs.Signature mới nhất để cải thiện hiệu suất và sửa lỗi.

## Phần kết luận
Bằng cách làm theo hướng dẫn này, bạn đã học cách tạo các đối tượng dữ liệu chính và phụ HIBC LIC, kết hợp chúng thành một thực thể duy nhất và ký tài liệu bằng mã QR bằng GroupDocs.Signature cho Java. Những kỹ năng này giúp tăng cường bảo mật tài liệu và đảm bảo tuân thủ trong ngành dược phẩm.

### Các bước tiếp theo
- Khám phá các chức năng bổ sung của GroupDocs.Signature.
- Tích hợp giải pháp này vào hệ thống hiện có của bạn để tự động hóa quy trình ký tài liệu.

## Phần Câu hỏi thường gặp
1. **Dữ liệu HIBC là gì?**
   - Dữ liệu Mã vạch ngành y tế (HIBC) bao gồm thông tin sản phẩm thiết yếu được sử dụng trong ngành y tế và dược phẩm.
2. **Tôi có thể sử dụng GroupDocs.Signature cho các loại mã vạch khác không?**
   - Có, GroupDocs.Signature hỗ trợ nhiều định dạng mã vạch khác nhau ngoài mã QR.
3. **Nếu định dạng tài liệu của tôi không phải là PDF thì sao?**
   - GroupDocs.Signature hỗ trợ nhiều định dạng tài liệu, bao gồm Word và Excel.
4. **Tôi phải xử lý các trường hợp ngoại lệ trong quá trình ký như thế nào?**
   - Triển khai các khối try-catch để quản lý các ngoại lệ một cách hiệu quả và đảm bảo dọn dẹp tài nguyên.
5. **Có giới hạn số lượng mã QR cho mỗi tài liệu không?**
   - Không có giới hạn cố hữu; tuy nhiên, hãy cân nhắc đến tác động về hiệu suất khi thêm nhiều mã.

## Tài nguyên
- **Tài liệu**: [GroupDocs.Signature cho Java Docs](https://docs.groupdocs.com/signature/java/)
- **Tài liệu tham khảo API**: [Tài liệu tham khảo API GroupDocs](https://reference.groupdocs.com/signature/java/)
- **Tải xuống**: [Bản phát hành mới nhất của GroupDocs.Release](https://releases.groupdocs.com/signature/java/)
- **Mua**: [Mua giấy phép](https://purchase.groupdocs.com/buy)
- **Dùng thử miễn phí**: [Dùng thử miễn phí](https://releases.groupdocs.com/signature/java/)
- **Giấy phép tạm thời**: [Nộp đơn tại đây](https://purchase.groupdocs.com/temporary-license/)