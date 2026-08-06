---
date: '2026-07-15'
description: Tìm hiểu cách thêm barcode PDF Java bằng GroupDocs.Signature – hướng
  dẫn từng bước để sign, verify, search, update và delete chữ ký barcode trong tài
  liệu Java.
keywords:
- add barcode pdf java
- groupdocs barcode signature
- java document signing
lastmod: '2026-07-15'
linktitle: Hướng dẫn Barcode Signature Java
og_description: Tìm hiểu cách thêm barcode PDF Java bằng GroupDocs.Signature – hướng
  dẫn từng bước để sign, verify, search, update và delete chữ ký barcode trong tài
  liệu Java.
og_image_alt: Guide showing how to add barcode PDF Java using GroupDocs.Signature
og_title: Thêm Barcode PDF Java – Sign & Verify với GroupDocs
schemas:
- author: GroupDocs
  dateModified: '2026-07-15'
  description: Learn how to add barcode PDF Java using GroupDocs.Signature – step‑by‑step
    guide to sign, verify, search, update and delete barcode signatures in Java documents.
  headline: Add Barcode PDF Java – Sign & Verify with GroupDocs
  type: TechArticle
- description: Learn how to add barcode PDF Java using GroupDocs.Signature – step‑by‑step
    guide to sign, verify, search, update and delete barcode signatures in Java documents.
  name: Add Barcode PDF Java – Sign & Verify with GroupDocs
  steps:
  - name: Case mismatch (e.g., “John Smith” vs. “john smith”).
    text: Case mismatch (e.g., “John Smith” vs. “john smith”).
  - name: Extra whitespace in the encoded text.
    text: Extra whitespace in the encoded text.
  - name: Wrong barcode type specified in the verification options.
    text: Wrong barcode type specified in the verification options.
  - name: Searching the wrong page number.
    text: Searching the wrong page number.
  - name: '**Reuse Signature Instances** – Create a single `Signature` object per
      document and reuse it for multiple operations.'
    text: '**Reuse Signature Instances** – Create a single `Signature` object per
      document and reuse it for multiple operations.'
  - name: '**Search Specific Pages Only** – Limit the page range to where barcodes
      are expected.'
    text: '**Search Specific Pages Only** – Limit the page range to where barcodes
      are expected.'
  - name: '**Choose the Simplest Barcode Type** – Simpler barcodes generate faster;
      only use QR or Data Matrix when you truly need the extra capacity.'
    text: '**Choose the Simplest Barcode Type** – Simpler barcodes generate faster;
      only use QR or Data Matrix when you truly need the extra capacity.'
  - name: '**Never Encode Sensitive Personal Data** – Barcodes are easily readable;
      avoid PII such as SSNs or passwords.'
    text: '**Never Encode Sensitive Personal Data** – Barcodes are easily readable;
      avoid PII such as SSNs or passwords.'
  - name: '**Validate Server‑Side** – Never trust client‑side verification alone;
      always re‑verify on a trusted backend.'
    text: '**Validate Server‑Side** – Never trust client‑side verification alone;
      always re‑verify on a trusted backend.'
  - name: '**Add Timestamps** – Include a timestamp in the barcode payload to prevent
      replay attacks.'
    text: '**Add Timestamps** – Include a timestamp in the barcode payload to prevent
      replay attacks.'
  type: HowTo
- questions:
  - answer: Yes – the library is fully compatible with JDK 8, 11, and 17.
    question: Can I use GroupDocs.Signature with Java 17?
  - answer: When you use Code128 or QR with sufficient size and contrast, the barcode
      remains scannable after printing and scanning.
    question: Does the barcode survive a print‑scan cycle?
  - answer: There is no hard limit; however, for optimal performance keep the total
      count below **200** per document.
    question: How many barcodes can a single document contain?
  - answer: A temporary license removes evaluation watermarks; a full license is mandatory
      for any production deployment.
    question: Is a license required for development builds?
  - answer: Yes – provide the password when creating the `Signature` object; the API
      will unlock the file internally.
    question: Can I sign password‑protected PDFs?
  type: FAQPage
tags:
- barcode signature
- groupdocs
- java
- pdf
- document signing
title: Thêm Barcode PDF Java – Sign & Verify với GroupDocs
type: docs
url: /vi/java/digital-signatures/java-document-signature-groupdocs-signature-barcode/
weight: 1
---

# Thêm Mã vạch PDF Java – Ký & Xác minh với GroupDocs

Nếu bạn cần một cách nhanh chóng, trực quan để gắn thẻ tài liệu cho quy trình nội bộ, việc thêm mã vạch vào PDF trong Java là giải pháp hoàn hảo. Với **GroupDocs.Signature**, bạn có thể nhúng, xác minh, tìm kiếm, cập nhật và xóa các chữ ký mã vạch mà không phải chịu gánh nặng của chữ ký số dựa trên PKI. Hướng dẫn này sẽ dẫn bạn qua từng bước, từ thiết lập môi trường đến các thực tiễn tốt nhất cho môi trường sản xuất.

## Câu trả lời nhanh
- **Thư viện nào thêm mã vạch vào PDF trong Java?** GroupDocs.Signature cho Java.  
- **Tôi có thể ký PDF, Word và hình ảnh không?** Có – API hỗ trợ hơn 30 định dạng.  
- **Có cần giấy phép cho việc phát triển không?** Giấy phép tạm thời 30 ngày là miễn phí; giấy phép đầy đủ cần thiết cho môi trường sản xuất.  
- **Cần bao nhiêu dòng code để ký một PDF?** Chỉ hai dòng: tạo đối tượng `Signature` và gọi `sign`.  
- **Xác minh mã vạch có phân biệt chữ hoa‑thường không?** Có – văn bản phải khớp chính xác, bao gồm cả chữ hoa‑thường và khoảng trắng.

## add barcode pdf java là gì?
`add barcode pdf java` đề cập đến quá trình sử dụng mã Java để nhúng một mã vạch (như Code128, QR, hoặc Data Matrix) vào tệp PDF. Kỹ thuật này cung cấp một thẻ có thể đọc bằng máy, có thể quét hoặc xác minh bằng chương trình, cho phép theo dõi tài liệu nhanh chóng trong các hệ thống nội bộ.

## Tại sao sử dụng chữ ký mã vạch thay vì chữ ký số đầy đủ?
Chữ ký mã vạch **nhanh hơn 30‑50 %** so với việc tạo và xác minh chữ ký số dựa trên PKI, và chúng hoạt động ổn định sau chu kỳ in‑quét. Ngoài ra, chúng không yêu cầu quản lý chứng chỉ, rất phù hợp cho các quy trình nội bộ có khối lượng lớn mà không cần bằng chứng mật mã.

## Yêu cầu trước

- **Java Development Kit (JDK) 8+** – Java 11 hoặc 17 được khuyến nghị để có hiệu năng tốt hơn.  
- **IDE** – IntelliJ IDEA hoặc Eclipse (các ví dụ sử dụng cú pháp IntelliJ).  
- **Công cụ xây dựng** – Maven hoặc Gradle để quản lý phụ thuộc.  

### Thêm GroupDocs.Signature vào dự án của bạn

Cách dễ nhất để bắt đầu là thêm thư viện qua công cụ xây dựng. Đây là cách thực hiện:

**Maven Users** – Thêm đoạn này vào `pom.xml` của bạn:

```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

**Gradle Users** – Thêm đoạn này vào `build.gradle` của bạn:

```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

**Tải JAR trực tiếp** – Nếu bạn muốn thiết lập thủ công, tải JAR từ [GroupDocs.Signature releases](https://releases.groupdocs.com/signature/java/) và thêm vào classpath.

### Sắp xếp giấy phép của bạn

GroupDocs.Signature không miễn phí cho việc sử dụng trong môi trường sản xuất, nhưng bạn có các tùy chọn linh hoạt:

- **Dùng thử miễn phí** – Tải từ [trang tải GroupDocs](https://releases.groupdocs.com/signature/java/) để thử các tính năng (đánh dấu nước sẽ được thêm).  
- **Giấy phép tạm thời** – Nhận 30 ngày truy cập đầy đủ qua [trang giấy phép tạm thời của GroupDocs](https://purchase.groupdocs.com/temporary-license/) – lý tưởng cho các bằng chứng khái niệm.  
- **Giấy phép đầy đủ** – Đối với triển khai sản xuất, xem [các tùy chọn mua GroupDocs](https://purchase.groupdocs.com/buy).  

**Mẹo chuyên nghiệp:** Bắt đầu với giấy phép tạm thời cho quá trình phát triển; nó sẽ loại bỏ các dấu nước khi bạn chuyển sang khóa vĩnh viễn.

### Kiểm tra môi trường nhanh

Sau khi đã thêm phụ thuộc, chạy một bài kiểm tra nhanh:

```java
import com.groupdocs.signature.Signature;

public class SignatureTest {
    public static void main(String[] args) {
        try {
            Signature signature = new Signature("test.pdf");
            System.out.println("GroupDocs.Signature initialized successfully!");
            signature.dispose();
        } catch (Exception e) {
            System.err.println("Setup issue: " + e.getMessage());
        }
    }
}
```

Nếu chương trình chạy mà không có lỗi, môi trường của bạn đã sẵn sàng. Nếu gặp vấn đề, hãy kiểm tra lại phiên bản JDK và phiên bản thư viện bạn đã thêm.

## Khi nào nên sử dụng chữ ký mã vạch

Chữ ký mã vạch tỏa sáng trong các kịch bản cụ thể:

- **Quy trình công việc tài liệu nội bộ** – Theo dõi hoá đơn, đơn đặt hàng hoặc ghi chú qua các chuỗi phê duyệt.  
- **Xử lý khối lượng lớn** – Ký hàng ngàn tài liệu nhanh chóng; việc tạo mã vạch nhanh tới **2×** so với ký số đầy đủ.  
- **Cầu nối in‑quét** – Mã vạch chịu được chu kỳ in‑quét, rất thích hợp cho quy trình hỗn hợp giấy‑số.  
- **Tích hợp hệ thống legacy** – Các máy quét mã vạch hiện có có thể đọc thẻ mà không cần phần mềm bổ sung.  
- **Dấu vết kiểm toán** – Nhúng ID giao dịch hoặc dấu thời gian mà kiểm toán viên có thể xác minh ngay lập tức.

Tránh sử dụng chữ ký mã vạch cho hợp đồng pháp lý, tài liệu bảo mật cao, hoặc trao đổi với đối tác bên ngoài nơi yêu cầu chữ ký số dựa trên PKI.

## Cài đặt GroupDocs.Signature cho Java

### Định nghĩa lớp cốt lõi

Lớp `Signature` là điểm vào cho tất cả các thao tác ký, xác minh, tìm kiếm, cập nhật và xóa trong GroupDocs.Signature.

```java
import com.groupdocs.signature.Signature;
```

### Khởi tạo cơ bản

Tạo một đối tượng `Signature` trỏ tới tệp mục tiêu:

```java
Signature signature = new Signature("path/to/your/document.pdf");
```

**Lưu ý quan trọng**

- Đường dẫn có thể là tuyệt đối hoặc tương đối; sử dụng `System.getProperty("user.home")` để tương thích đa nền tảng.  
- GroupDocs hỗ trợ **hơn 30** định dạng đầu vào và đầu ra, bao gồm PDF, DOCX, XLSX, PPTX và PNG.  
- Luôn giải phóng tài nguyên bằng `signature.dispose()` hoặc khối try‑with‑resources:

```java
try (Signature signature = new Signature("path/to/your/document.pdf")) {
    // Your signing operations here
} catch (Exception e) {
    System.err.println("Error working with document: " + e.getMessage());
}
```

Bây giờ bạn đã sẵn sàng để thêm mã vạch.

## Làm thế nào để thêm mã vạch vào PDF trong Java?

Tải PDF nguồn bằng `new Signature("input.pdf")`, cấu hình đối tượng `BarcodeSignature` (ví dụ Code128 với văn bản “John Smith”), và gọi `sign` để tạo tệp đã ký – tất cả trong ba dòng code ngắn gọn. Cách tiếp cận này cho phép bạn nhúng thẻ có thể đọc bằng máy trong khi giữ nguyên bố cục tài liệu gốc, và nó hoạt động cho bất kỳ định dạng hỗ trợ nào, không chỉ PDF.

### Triển khai từng bước

#### 1. Xác định đường dẫn tệp

Đặt vị trí cho tệp nguồn và tệp đầu ra:

```java
String filePath = "YOUR_DOCUMENT_DIRECTORY/sample.docx";
String outputFilePath = "YOUR_OUTPUT_DIRECTORY/signed_sample.docx";
```

#### 2. Tạo Trình xử lý chữ ký

Khởi tạo trình xử lý với tài liệu nguồn:

```java
Signature signature = new Signature(filePath);
```

#### 3. Cấu hình tùy chọn mã vạch

Đối tượng `BarcodeSignature` định nghĩa các thuộc tính hình ảnh và dữ liệu của mã vạch sẽ được nhúng. Đặt loại mã vạch, văn bản mã hoá, vị trí, kích thước, màu sắc và phông chữ có thể đọc được tùy chọn:

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

> **Mẹo chuyên nghiệp:** Nếu chuỗi mã hoá dài hơn 20 ký tự, tăng chiều rộng mã vạch để tránh lỗi quét.

#### 4. Áp dụng chữ ký

Thực hiện thao tác ký và tạo tệp đầu ra:

```java
signature.sign(outputFilePath, signOptions);
```

#### 5. Ví dụ thực tế

Trong hệ thống phê duyệt hoá đơn, bạn có thể nhúng ID nhân viên người phê duyệt và dấu thời gian:

```java
String invoiceId = "INV-2025-0042";
String approver = "john.smith@company.com";
String timestamp = LocalDateTime.now().toString();

// Combine into barcode data
String barcodeData = invoiceId + "|" + approver + "|" + timestamp;

BarcodeSignOptions signOptions = new BarcodeSignOptions(barcodeData, BarcodeTypes.QR);
signOptions.setVerticalAlignment(VerticalAlignment.Bottom);
signOptions.setHorizontalAlignment(HorizontalAlignment.Right);

signature.sign(outputFilePath, signOptions);
```

PDF kết quả giờ đã chứa một mã vạch có thể quét, mã hoá toàn bộ siêu dữ liệu phê duyệt cần thiết.

## Làm sao để xác minh chữ ký mã vạch trong tài liệu Java?

Phương thức `Signature.verify` kiểm tra tài liệu xem có tồn tại chữ ký mã vạch khớp với các tùy chọn đã cung cấp hay không, trả về giá trị boolean cho biết mã vạch mong muốn có xuất hiện hay không. Việc xác minh hữu ích cho các quy trình tự động nơi bạn cần chắc chắn tài liệu đã được xử lý bởi bên đúng trước khi thực hiện các hành động tiếp theo.

### Các bước xác minh

#### 1. Tải tài liệu đã ký

```java
Signature signature = new Signature("YOUR_OUTPUT_DIRECTORY/signed_sample.docx");
```

#### 2. Đặt tiêu chí xác minh

Xác định văn bản, định dạng mã vạch và số trang chính xác mà bạn mong đợi:

```java
BarcodeVerifyOptions verifyOptions = new BarcodeVerifyOptions();
verifyOptions.setAllPages(false); // Only check the first page
verifyOptions.setPageNumber(1);
verifyOptions.setEncodeType(BarcodeTypes.Code128);
verifyOptions.setText("John Smith");
```

#### 3. Chạy xác minh

Thực hiện kiểm tra và xử lý kết quả:

```java
boolean isValid = signature.verify(verifyOptions) != null;

if (isValid) {
    System.out.println("Document signature verified successfully!");
} else {
    System.out.println("Warning: Signature verification failed!");
}
```

**Mẫu phổ biến:** Để chỉ xác nhận rằng *bất kỳ* mã vạch nào của loại cho trước tồn tại, bỏ qua bộ lọc `setText`:

```java
BarcodeVerifyOptions flexibleOptions = new BarcodeVerifyOptions();
flexibleOptions.setAllPages(true);
flexibleOptions.setEncodeType(BarcodeTypes.Code128);
// No setText() call = accept any text with this barcode type

boolean hasAnySignature = signature.verify(flexibleOptions) != null;
```

Hoặc xác minh chỉ định dạng mã vạch mà không quan tâm tới nội dung:

```java
BarcodeVerifyOptions formatOnly = new BarcodeVerifyOptions();
formatOnly.setEncodeType(BarcodeTypes.QR);
// Confirms a QR code exists, regardless of content
```

> **Cảnh báo:** Xác minh phân biệt chữ hoa‑thường và khoảng trắng; luôn cắt bỏ và chuẩn hoá dữ liệu trước khi ký.

## Làm sao để tìm kiếm chữ ký mã vạch trong tài liệu?

Phương thức `Signature.search` quét tài liệu để tìm các chữ ký mã vạch khớp với `BarcodeSearchOptions` đã cung cấp, trả về một tập hợp bao gồm vị trí, số trang và giá trị mã hoá của mỗi mã vạch. Khả năng này cho phép trích xuất siêu dữ liệu hàng loạt mà không cần mở từng tệp một.

### Quy trình tìm kiếm

#### 1. Khởi tạo tìm kiếm

```java
Signature signature = new Signature("YOUR_OUTPUT_DIRECTORY/signed_sample.docx");
```

#### 2. Cấu hình tham số tìm kiếm

Chỉ định phạm vi trang, loại mã vạch hoặc bộ lọc văn bản:

```java
BarcodeSearchOptions searchOptions = new BarcodeSearchOptions();
searchOptions.setAllPages(true); // Search the entire document
```

Tùy chọn thu hẹp phạm vi tìm kiếm để cải thiện hiệu năng:

```java
BarcodeSearchOptions narrowSearch = new BarcodeSearchOptions();
narrowSearch.setAllPages(false);
narrowSearch.setPageNumber(1); // Only search page 1
narrowSearch.setEncodeType(BarcodeTypes.Code128); // Only find Code128 barcodes
```

#### 3. Thực thi tìm kiếm

```java
java.util.List<BarcodeSignature> signatures = signature.search(BarcodeSignature.class, searchOptions);

System.out.println("Found " + signatures.size() + " barcode signature(s)");

for (BarcodeSignature bcSignature : signatures) {
    System.out.println("Barcode Type: " + bcSignature.getEncodeType().getTypeName());
    System.out.println("Text: " + bcSignature.getText());
    System.out.println("Position: (" + bcSignature.getLeft() + ", " + bcSignature.getTop() + ")");
    System.out.println("Size: " + bcSignature.getWidth() + "x" + bcSignature.getHeight());
    System.out.println("---");
}
```

#### 4. Ví dụ trích xuất dữ liệu

Lấy dữ liệu phê duyệt từ mọi mã vạch trong một lô hoá đơn:

```java
List<BarcodeSignature> foundSignatures = signature.search(BarcodeSignature.class, searchOptions);

for (BarcodeSignature sig : foundSignatures) {
    String barcodeData = sig.getText();
    
    // Parse your custom format (remember our invoice example?)
    String[] parts = barcodeData.split("\\|");
    if (parts.length == 3) {
        String invoiceId = parts[0];
        String approver = parts[1];
        String timestamp = parts[2];
        
        System.out.println("Invoice " + invoiceId + " approved by " + approver + " at " + timestamp);
    }
}
```

> **Mẹo hiệu năng:** Đối với tài liệu trên 100 trang, luôn giới hạn tìm kiếm chỉ ở các trang thực sự chứa mã vạch; điều này có thể giảm thời gian chạy tới **70 %**.

## Làm sao để cập nhật một chữ ký mã vạch hiện có?

Phương thức `Signature.update` sửa đổi các thuộc tính hình ảnh của một chữ ký mã vạch hiện có—như vị trí, kích thước hoặc màu sắc—trong khi giữ nguyên dữ liệu mã hoá gốc. Điều này hữu ích khi cần thay đổi bố cục sau khi tài liệu đã được ký.

### Quy trình cập nhật

#### 1. Tìm các chữ ký cần cập nhật

```java
Signature signature = new Signature("YOUR_OUTPUT_DIRECTORY/signed_sample.docx");

BarcodeSearchOptions searchOptions = new BarcodeSearchOptions();
searchOptions.setAllPages(true);

List<BarcodeSignature> signatures = signature.search(BarcodeSignature.class, searchOptions);
```

#### 2. Thay đổi các thuộc tính mong muốn

```java
List<BarcodeSignature> signaturesToUpdate = new ArrayList<>();

if (!signatures.isEmpty()) {
    BarcodeSignature bcSignature = signatures.get(0); // Update the first found signature
    
    // Move it 100px right and 100px down
    bcSignature.setLeft(bcSignature.getLeft() + 100);
    bcSignature.setTop(bcSignature.getTop() + 100);
    
    // Make it bigger
    bcSignature.setWidth(200);
    bcSignature.setHeight(50);
    
    signaturesToUpdate.add(bcSignature);
}
```

Bạn có thể thay đổi nhiều thuộc tính cùng lúc:

```java
bcSignature.setLeft(50);
bcSignature.setTop(50);
bcSignature.setWidth(150);
bcSignature.setHeight(45);
// Note: You can't change the encoded text or barcode type with update
// For that, you'd need to delete and re-sign
```

#### 3. Lưu thay đổi

```java
ByteArrayOutputStream outputStream = new ByteArrayOutputStream();
signature.update(outputStream, signaturesToUpdate);

// If you want to save to a file instead:
// signature.update("path/to/updated_document.docx", signaturesToUpdate);
```

#### 4. Kịch bản thực tế

Đặt lại vị trí tất cả các chữ ký để tránh chồng lên logo công ty mới được thêm:

```java
List<BarcodeSignature> allSignatures = signature.search(BarcodeSignature.class, searchOptions);
List<BarcodeSignature> toUpdate = new ArrayList<>();

for (BarcodeSignature sig : allSignatures) {
    // Move all signatures down by 50px to clear space for new logo
    if (sig.getTop() < 100) {
        sig.setTop(sig.getTop() + 50);
        toUpdate.add(sig);
    }
}

if (!toUpdate.isEmpty()) {
    signature.update(outputStream, toUpdate);
    System.out.println("Repositioned " + toUpdate.size() + " signature(s)");
}
```

> **Hạn chế:** Thay đổi văn bản đã mã hoá yêu cầu xóa và chèn lại một chữ ký mới.

## Làm sao để xóa chữ ký mã vạch khỏi tài liệu?

Phương thức `Signature.delete` loại bỏ vĩnh viễn các chữ ký mã vạch đã chọn khỏi tài liệu, xóa cả phần hình ảnh và dữ liệu mã hoá. Sử dụng thao tác này khi dọn dẹp các chữ ký thử nghiệm hoặc khi mã vạch không còn cần thiết.

### Các bước xóa

#### 1. Xác định chữ ký

```java
Signature signature = new Signature("YOUR_OUTPUT_DIRECTORY/signed_sample.docx");

BarcodeSearchOptions searchOptions = new BarcodeSearchOptions();
searchOptions.setAllPages(true);

List<BarcodeSignature> signatures = signature.search(BarcodeSignature.class, searchOptions);
```

#### 2. Xóa các chữ ký đã chọn

```java
List<BarcodeSignature> signaturesToDelete = new ArrayList<>();

// Delete all Code128 signatures (for example)
for (BarcodeSignature sig : signatures) {
    if (sig.getEncodeType().equals(BarcodeTypes.Code128)) {
        signaturesToDelete.add(sig);
    }
}

if (!signaturesToDelete.isEmpty()) {
    boolean result = signature.delete(signaturesToDelete);
    
    if (result) {
        System.out.println("Successfully deleted " + signaturesToDelete.size() + " signature(s)");
    } else {
        System.err.println("Failed to delete signatures");
    }
}
```

#### 3. Ví dụ xóa có điều kiện

Xóa chỉ những mã vạch cũ hơn một thời gian cụ thể (giả sử thời gian được nhúng trong văn bản mã hoá):

```java
LocalDateTime cutoffDate = LocalDateTime.now().minusDays(30);
List<BarcodeSignature> outdatedSignatures = new ArrayList<>();

for (BarcodeSignature sig : signatures) {
    try {
        String text = sig.getText();
        // Assuming format like "data|timestamp"
        String[] parts = text.split("\\|");
        if (parts.length > 1) {
            LocalDateTime sigDate = LocalDateTime.parse(parts[1]);
            if (sigDate.isBefore(cutoffDate)) {
                outdatedSignatures.add(sig);
            }
        }
    } catch (Exception e) {
        // Skip signatures that don't match our format
        continue;
    }
}

if (!outdatedSignatures.isEmpty()) {
    signature.delete(outdatedSignatures);
    System.out.println("Removed " + outdatedSignatures.size() + " outdated signature(s)");
}
```

> **Cảnh báo:** Xóa không thể hoàn tác; luôn thao tác trên bản sao của tệp sản xuất trong quá trình thử nghiệm.

#### 4. Mẫu xóa hàng loạt

Dọn dẹp các chữ ký thử nghiệm trước khi phát hành:

```java
// Remove all signatures containing "TEST" in their text
List<BarcodeSignature> testSignatures = signatures.stream()
    .filter(sig -> sig.getText().toUpperCase().contains("TEST"))
    .collect(Collectors.toList());

if (!testSignatures.isEmpty()) {
    signature.delete(testSignatures);
    System.out.println("Cleaned up " + testSignatures.size() + " test signature(s)");
}
```

## Các loại mã vạch: Hướng dẫn thực tiễn

Lựa chọn mã vạch phù hợp ảnh hưởng đến độ tin cậy khi quét, khả năng chứa dữ liệu và tính tương thích với máy in.

### Code128 (Lựa chọn phổ biến nhất)

- **Khi nào dùng:** Dữ liệu alphanumeric, mật độ cao, tài liệu in.  
- **Ưu điểm:** Gọn nhẹ, hoạt động với máy quét tiêu chuẩn, in rõ ở kích thước nhỏ.  
- **Nhược điểm:** Giới hạn ASCII, ít khả năng chống lỗi hơn so với mã 2‑D.  

Ví dụ:

```java
BarcodeSignOptions code128 = new BarcodeSignOptions("INV-2025-042", BarcodeTypes.Code128);
```

### QR Code (Tốt nhất cho di động)

- **Khi nào dùng:** Quét bằng điện thoại, tải dữ liệu lớn (URL, JSON, …), tài liệu có khả năng bị hỏng.  
- **Ưu điểm:** Lên tới 4 000 ký tự, có khả năng sửa lỗi tích hợp, thân thiện với smartphone.  
- **Nhược điểm:** Diện tích hình ảnh lớn hơn, cần độ phân giải cao hơn cho kích thước nhỏ.  

Ví dụ:

```java
String jsonData = "{\"invoice\":\"INV-042\",\"amount\":1500.00,\"approver\":\"john@company.com\"}";
BarcodeSignOptions qrCode = new BarcodeSignOptions(jsonData, BarcodeTypes.QR);
```

### Code39 (Cổ điển đáng tin cậy)

- **Khi nào dùng:** Môi trường máy quét legacy, cần văn bản có thể đọc được bằng mắt.  
- **Ưu điểm:** Hỗ trợ rộng rãi, định dạng đơn giản, không cần checksum.  
- **Nhược điểm:** Độ mật độ dữ liệu thấp, bộ ký tự hạn chế, chiếm không gian lớn hơn.  

### Data Matrix (Sức mạnh gọn nhẹ)

- **Khi nào dùng:** Không gian cực hạn, đánh dấu các vật phẩm nhỏ, dữ liệu mật độ cao.  
- **Ưu điểm:** Rất gọn, sửa lỗi mạnh, hoạt động trên bề mặt cong.  
- **Nhược điểm:** Cần in chất lượng cao, hỗ trợ máy quét không phổ biến.  

#### So sánh nhanh

| Loại mã vạch | Dung lượng dữ liệu | Thích hợp cho | Kích thước điển hình |
|--------------|--------------------|---------------|-----------------------|
| Code128      | ~100 ký tự         | Gắn thẻ đa mục đích | Nhỏ |
| QR Code      | ~4 000 ký tự       | Quét di động, dữ liệu phong phú | Trung bình |
| Code39       | ~43 ký tự          | Phần cứng legacy | Lớn |
| Data Matrix  | ~3 000 ký tự       | Không gian siêu nhỏ, nhãn công nghiệp | Rất nhỏ |

**Khuyến nghị:** Bắt đầu với **Code128** cho các ID đơn giản. Chuyển sang **QR** khi cần nhúng URL hoặc payload lớn. Chỉ dùng **Code39** cho các tích hợp legacy.

## Các vấn đề thường gặp & Giải pháp

### Vấn đề: “Không tìm thấy mã vạch khi xác minh”

**Triệu chứng:** Xác minh trả về `false` mặc dù mã vạch hiển thị.

**Nguyên nhân thường gặp**

1. Không khớp chữ hoa‑thường (ví dụ “John Smith” vs. “john smith”).  
2. Khoảng trắng thừa trong văn bản mã hoá.  
3. Loại mã vạch sai trong tùy chọn xác minh.  
4. Tìm kiếm trên số trang không đúng.

**Giải pháp:** Chuẩn hoá văn bản trước khi ký và xác minh, và đảm bảo `setEncodeType` khớp với loại gốc.

```java
// Always normalize your data
String signatureText = originalText.trim().toLowerCase();

// When signing:
BarcodeSignOptions signOptions = new BarcodeSignOptions(signatureText, BarcodeTypes.Code128);

// When verifying:
BarcodeVerifyOptions verifyOptions = new BarcodeVerifyOptions();
verifyOptions.setText(signatureText); // Use the same normalized text
verifyOptions.setEncodeType(BarcodeTypes.Code128);
```

### Vấn đề: “Mã vạch bị mờ hoặc không đọc được”

**Triệu chứng:** Mã vạch đã in không thể quét.

**Nguyên nhân**

- Kích thước mã vạch quá nhỏ so với dữ liệu mã hoá.  
- Cài đặt máy in độ phân giải thấp.  
- Độ tương phản màu mã vạch và nền không đủ.

**Giải pháp:** Tăng chiều rộng/chiều cao mã vạch, sử dụng màu tương phản cao (đen trên trắng), và đặt DPI máy in ít nhất 300 dpi.

```java
// Increase size for longer strings
int dataLength = barcodeText.length();
int minWidth = Math.max(100, dataLength * 10); // 10px per character minimum

BarcodeSignOptions signOptions = new BarcodeSignOptions(barcodeText, BarcodeTypes.Code128);
signOptions.setWidth(minWidth);
signOptions.setHeight(60); // Taller = easier to scan

// Use high-contrast colors
signOptions.setForeColor(Color.BLACK); // Black on white is most reliable
signOptions.setBackColor(Color.WHITE);
```

### Vấn đề: “OutOfMemoryError với tài liệu lớn”

**Triệu chứng:** Ứng dụng bị sập khi xử lý PDF hàng trăm trang.

**Nguyên nhân:** Thư viện tải toàn bộ tài liệu vào bộ nhớ.

**Giải pháp:** Bật chế độ streaming và xử lý các trang theo từng phần.

```java
// Process pages in batches instead of all at once
BarcodeSearchOptions searchOptions = new BarcodeSearchOptions();
searchOptions.setAllPages(false);

List<BarcodeSignature> allSignatures = new ArrayList<>();

for (int page = 1; page <= totalPages; page++) {
    searchOptions.setPageNumber(page);
    List<BarcodeSignature> pageSignatures = signature.search(BarcodeSignature.class, searchOptions);
    allSignatures.addAll(pageSignatures);
    
    // Process and clear as you go
    if (page % 10 == 0) {
        System.gc(); // Suggest garbage collection every 10 pages
    }
}
```

### Vấn đề: “Vị trí chữ ký không đồng nhất giữa các loại tài liệu”

**Triệu chứng:** Mã vạch xuất hiện ở vị trí khác nhau khi ký PDF so với Word.

**Nguyên nhân:** PDF dùng gốc tọa độ góc dưới‑trái, trong khi Word dùng góc trên‑trái.

**Giải pháp:** Phát hiện loại tài liệu và áp dụng phép biến đổi tọa độ phù hợp.

```java
// Use relative positioning instead of absolute
signOptions.setVerticalAlignment(VerticalAlignment.Bottom);
signOptions.setHorizontalAlignment(HorizontalAlignment.Right);

// Then use margins for fine-tuning
Padding margin = new Padding();
margin.setRight(50); // 50px from right edge
margin.setBottom(50); // 50px from bottom
signOptions.setMargin(margin);

// This works consistently across PDF, DOCX, XLSX, etc.
```

### Vấn đề: “Chữ ký cập nhật mất định dạng”

**Triệu chứng:** Sau khi gọi `update`, màu hoặc phông chữ của mã vạch thay đổi không mong muốn.

**Nguyên nhân:** Không phải tất cả các thuộc tính hình ảnh đều được lưu lại trong quá trình cập nhật.

**Giải pháp:** Áp dụng lại các thiết lập hình ảnh sau khi gọi `update`.

```java
// When updating, explicitly set all visual properties
bcSignature.setLeft(newLeft);
bcSignature.setTop(newTop);
bcSignature.setWidth(originalWidth); // Don't forget these!
bcSignature.setHeight(originalHeight);
// Note: Color and font can't be updated - you'd need to delete and re-sign
```

## Thực tiễn tốt nhất cho môi trường sản xuất

### Tối ưu hoá hiệu năng

1. **Tái sử dụng đối tượng Signature** – Tạo một đối tượng `Signature` duy nhất cho mỗi tài liệu và tái sử dụng cho nhiều thao tác.

```java
// Bad - Creates new instance each time
public void processDocument(String path) {
    Signature sig1 = new Signature(path);
    sig1.search(/* ... */);
    
    Signature sig2 = new Signature(path); // Unnecessary reload
    sig2.verify(/* ... */);
}

// Good - Reuse the same instance
public void processDocument(String path) {
    try (Signature signature = new Signature(path)) {
        signature.search(/* ... */);
        signature.verify(/* ... */);
        signature.update(/* ... */);
    }
}
```

2. **Tìm kiếm chỉ trên các trang cụ thể** – Giới hạn phạm vi trang tới nơi có khả năng chứa mã vạch.

```java
// Slow for 100+ page documents
BarcodeSearchOptions slowSearch = new BarcodeSearchOptions();
slowSearch.setAllPages(true);

// Fast - only check where signatures actually are
BarcodeSearchOptions fastSearch = new BarcodeSearchOptions();
fastSearch.setAllPages(false);
fastSearch.setPageNumber(1); // Only check cover page
```

3. **Chọn loại mã vạch đơn giản nhất** – Mã vạch đơn giản tạo nhanh hơn; chỉ dùng QR hoặc Data Matrix khi thực sự cần dung lượng lớn.

```java
// Overkill for simple IDs
BarcodeSignOptions slow = new BarcodeSignOptions("12345", BarcodeTypes.QR);

// Faster and more appropriate
BarcodeSignOptions fast = new BarcodeSignOptions("12345", BarcodeTypes.Code128);
```

### Xem xét bảo mật

1. **Không bao giờ mã hoá dữ liệu cá nhân nhạy cảm** – Mã vạch dễ đọc; tránh lưu SSN hoặc mật khẩu.

```java
// Bad - exposes sensitive data
String barcodeData = "SSN:123-45-6789|Password:hunter2";

// Good - use reference IDs
String barcodeData = "USER-REF-7721X"; // Look up sensitive data server-side
```

2. **Xác minh phía server** – Không bao giờ tin vào xác minh chỉ trên client; luôn xác minh lại trên backend đáng tin cậy.

```java
// Client scans barcode and extracts "APPROVED-BY-ADMIN"
// Always verify server-side:
public boolean verifyApproval(String documentId, String scannedData) {
    // Load document from secure storage
    Signature signature = new Signature(getSecureDocument(documentId));
    
    BarcodeVerifyOptions verifyOptions = new BarcodeVerifyOptions();
    verifyOptions.setText(scannedData);
    
    boolean isValid = signature.verify(verifyOptions) != null;
    
    // Also check against your database
    boolean isInDatabase = checkApprovalDatabase(documentId, scannedData);
    
    return isValid && isInDatabase;
}
```

3. **Thêm dấu thời gian** – Bao gồm timestamp trong payload mã vạch để ngăn chặn tấn công replay.

```java
import java.time.LocalDateTime;
import java.time.temporal.ChronoUnit;

String timestamp = LocalDateTime.now().truncatedTo(ChronoUnit.SECONDS).toString();
String barcodeData = "APPROVAL|" + userId + "|" + timestamp;

// When verifying, check the timestamp isn't too old
public boolean isSignatureRecent(String barcodeData, int maxAgeHours) {
    String[] parts = barcodeData.split("\\|");
    if (parts.length < 3) return false;
    
    LocalDateTime signatureTime = LocalDateTime.parse(parts[2]);
    LocalDateTime now = LocalDateTime.now();
    
    long hoursSince = ChronoUnit.HOURS.between(signatureTime, now);
    return hoursSince <= maxAgeHours;
}
```

### Mẫu xử lý lỗi

- **Luôn dùng Try‑With‑Resources** để đảm bảo đối tượng `Signature` được giải phóng.

```java
try (Signature signature = new Signature(documentPath)) {
    // Your operations here
    signature.sign(outputPath, signOptions);
} catch (Exception e) {
    logger.error("Failed to sign document: " + documentPath, e);
    throw new DocumentSigningException("Could not process document", e);
}
```

- **Kiểm tra quyền truy cập tệp** trước khi ký.

```java
public void signDocument(String inputPath, String outputPath) {
    File inputFile = new File(inputPath);
    
    if (!inputFile.exists()) {
        throw new IllegalArgumentException("Input file not found: " + inputPath);
    }
    
    if (!inputFile.canRead()) {
        throw new SecurityException("Cannot read input file: " + inputPath);
    }
    
    File outputDir = new File(outputPath).getParentFile();
    if (outputDir != null && !outputDir.exists()) {
        outputDir.mkdirs();
    }
    
    try (Signature signature = new Signature(inputPath)) {
        signature.sign(outputPath, signOptions);
    }
}
```

- **Đồng bộ hoá truy cập** nếu nhiều luồng có thể làm việc trên cùng một tệp.

```java
import java.util.concurrent.locks.ReentrantLock;
import java.util.concurrent.ConcurrentHashMap;

public class SignatureManager {
    private final ConcurrentHashMap<String, ReentrantLock> documentLocks = new ConcurrentHashMap<>();
    
    public void signDocument(String documentPath, BarcodeSignOptions options) {
        ReentrantLock lock = documentLocks.computeIfAbsent(documentPath, k -> new ReentrantLock());
        
        lock.lock();
        try (Signature signature = new Signature(documentPath)) {
            signature.sign(documentPath + ".signed", options);
        } finally {
            lock.unlock();
        }
    }
}
```

### Kiểm thử triển khai của bạn

**Mẫu Unit Test**

```java
import org.junit.jupiter.api.Test;
import org.junit.jupiter.api.io.TempDir;
import static org.junit.jupiter.api.Assertions.*;

public class BarcodeSignatureTest {
    
    @TempDir
    Path tempDir;
    
    @Test
    public void testSignAndVerify() throws Exception {
        // Setup
        String testDoc = "test-document.pdf";
        String outputDoc = tempDir.resolve("signed-test.pdf").toString();
        String testData = "TEST-USER-12345";
        
        // Sign
        try (Signature signature = new Signature(testDoc)) {
            BarcodeSignOptions signOptions = new BarcodeSignOptions(testData, BarcodeTypes.Code128);
            signature.sign(outputDoc, signOptions);
        }
        
        // Verify
        try (Signature signature = new Signature(outputDoc)) {
            BarcodeVerifyOptions verifyOptions = new BarcodeVerifyOptions();
            verifyOptions.setText(testData);
            verifyOptions.setEncodeType(BarcodeTypes.Code128);
            
            boolean isValid = signature.verify(verifyOptions) != null;
            assertTrue(isValid, "Signature should be valid");
        }
    }
    
    @Test
    public void testSearchFindsSignature() throws Exception {
        String signedDoc = "signed-document.pdf";
        
        try (Signature signature = new Signature(signedDoc)) {
            BarcodeSearchOptions searchOptions = new BarcodeSearchOptions();
            searchOptions.setAllPages(true);
            
            List<BarcodeSignature> signatures = signature.search(BarcodeSignature.class, searchOptions);
            
            assertFalse(signatures.isEmpty(), "Should find at least one signature");
            assertEquals("TEST-USER-12345", signatures.get(0).getText());
        }
    }
}
```

**Checklist tích hợp**

- ✅ Kiểm tra tất cả các định dạng được hỗ trợ (PDF, DOCX, XLSX, PPTX, PNG).  
- ✅ Xác minh mã vạch chịu được chu kỳ in‑quét.  
- ✅ Stress‑test với chuỗi dữ liệu dài tối đa.  
- ✅ Xác nhận vị trí trên các kích thước trang A4, Letter và tùy chỉnh.  
- ✅ Chạy ký đồng thời trên nhiều tài liệu.  
- ✅ Giám sát mức sử dụng bộ nhớ cho tài liệu > 500 trang.  
- ✅ Đảm bảo máy quét mã vạch đọc được đầu ra một cách ổn định.

### Ghi log và giám sát

Thêm log có ý nghĩa quanh mỗi thao tác:

```java
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

public class DocumentSigningService {
    private static final Logger logger = LoggerFactory.getLogger(DocumentSigningService.class);
    
    public void signDocument(String docPath, String barcodeData) {
        logger.info("Starting signature process for document: {}", docPath);
        logger.debug("Barcode data length: {} characters", barcodeData.length());
        
        try (Signature signature = new Signature(docPath)) {
            BarcodeSignOptions options = new BarcodeSignOptions(barcodeData, BarcodeTypes.Code128);
            
            long startTime = System.currentTimeMillis();
            signature.sign(docPath + ".signed", options);
            long duration = System.currentTimeMillis() - startTime;
            
            logger.info("Successfully signed document in {}ms", duration);
        } catch (Exception e) {
            logger.error("Failed to sign document: {}", docPath, e);
            throw new RuntimeException("Signature operation failed", e);
        }
    }
}
```

Theo dõi các chỉ số quan trọng như thời gian xử lý, tiêu thụ bộ nhớ và tỷ lệ lỗi:

```java
// Track success/failure rates
metricsService.incrementCounter("signature.sign.success");
metricsService.incrementCounter("signature.verify.failure");

// Track performance
metricsService.recordTimer("signature.sign.duration", duration);

// Track document sizes
metricsService.recordHistogram("signature.document.pages", pageCount);
```

## Mẹo chuyên nghiệp từ thực tiễn

**Chiến lược xử lý batch**

Khi xử lý hàng trăm tệp, chia thành các batch và báo cáo tiến độ:

```java
public void signBatch(List<String> documents, String barcodePrefix) {
    int total = documents.size();
    int completed = 0;
    int failed = 0;
    
    for (String docPath : documents) {
        try {
            String barcodeData = barcodePrefix + "-" + UUID.randomUUID().toString();
            signDocument(docPath, barcodeData);
            completed++;
            
            if (completed % 10 == 0) {
                logger.info("Progress: {}/{} documents signed", completed, total);
            }
        } catch (Exception e) {
            failed++;
            logger.warn("Failed to sign: {}", docPath, e);
        }
    }
    
    logger.info("Batch complete: {} succeeded, {} failed", completed, failed);
}
```

**Tách cấu hình ra bên ngoài**

Lưu các thiết lập mã vạch (loại, kích thước, màu) trong file properties để dễ tinh chỉnh mà không cần biên dịch lại:

```java
public class BarcodeConfig {
    private int defaultWidth = 100;
    private int defaultHeight = 40;
    private String defaultBarcodeType = "Code128";
    private String defaultColor = "BLACK";
    
    // Load from properties file or environment variables
    public BarcodeConfig() {
        this.defaultWidth = Integer.parseInt(
            System.getProperty("barcode.width", "100")
        );
        // ... load other properties
    }
    
    public BarcodeSignOptions createDefaultOptions(String text) {
        BarcodeSignOptions options = new BarcodeSignOptions(text, getBarcodeType());
        options.setWidth(defaultWidth);
        options.setHeight(defaultHeight);
        options.setForeColor(getColor());
        return options;
    }
}
```

**Chuẩn hoá payload mã vạch**

Sử dụng định dạng phân tách như `EMPID|TIMESTAMP|DOCID` để việc phân tích cú pháp đơn giản và nhất quán:

```java
public class BarcodeDataBuilder {
    private String userId;
    private String action;
    private LocalDateTime timestamp;
    private String documentId;
    
    public BarcodeDataBuilder setUserId(String userId) {
        this.userId = userId;
        return this;
    }
    
    public BarcodeDataBuilder setAction(String action) {
        this.action = action;
        return this;
    }
    
    public BarcodeDataBuilder setDocumentId(String documentId) {
        this.documentId = documentId;
        return this;
    }
    
    public String build() {
        this.timestamp = LocalDateTime.now();
        
        // Format: VERSION|USER|ACTION|DOC_ID|TIMESTAMP|CHECKSUM
        String data = String.join("|",
            "v1",
            userId,
            action,
            documentId,
            timestamp.toString()
        );
        
        // Add simple checksum
        int checksum = data.hashCode();
        return data + "|" + checksum;
    }
    
    public static ParsedBarcodeData parse(String barcodeData) {
        String[] parts = barcodeData.split("\\|");
        if (parts.length != 6 || !parts[0].equals("v1")) {
            throw new IllegalArgumentException("Invalid barcode format");
        }
        
        return new ParsedBarcodeData(parts[1], parts[2], parts[3], 
                                     LocalDateTime.parse(parts[4]));
    }
}

// Usage:
String barcodeData = new BarcodeDataBuilder()
    .setUserId("john.smith")
    .setAction("APPROVED")
    .setDocumentId("INV-2025-042")
    .build();
```

**Tự động phát hiện loại tài liệu**

Điều chỉnh kích thước mã vạch dựa trên việc mục tiêu là PDF, Word hay hình ảnh:

```java
public BarcodeSignOptions getOptimalOptions(String documentPath, String text) {
    String extension = documentPath.substring(documentPath.lastIndexOf(".") + 1).toLowerCase();
    
    BarcodeSignOptions options = new BarcodeSignOptions(text, BarcodeTypes.Code128);
    
    switch (extension) {
        case "pdf":
            // PDFs can handle larger, detailed barcodes
            options.setWidth(150);
            options.setHeight(50);
            break;
        case "docx":
        case "doc":
            // Word docs need compact signatures that don't disrupt flow
            options.setWidth(100);
            options.setHeight(35);
            options.setVerticalAlignment(VerticalAlignment.Bottom);
            break;
        case "xlsx":
        case "xls":
            // Excel needs signatures that don't obscure data
            options.setWidth(80);
            options.setHeight(30);
            options.setHorizontalAlignment(HorizontalAlignment.Right);
            break;
        default:
            // Safe defaults
            options.setWidth(100);
            options.setHeight(40);
    }
    
    return options;
}
```

## Tài nguyên bổ sung

- [GroupDocs.Signature documentation](https://docs.groupdocs.com/signature/java/) – Hướng dẫn API đầy đủ và các ví dụ sử dụng.  
- [GroupDocs support forum](https://forum.groupdocs.com/c/signature/13) – Cộng đồng hỗ trợ và giải đáp vấn đề.  
- [API reference](https://apireference.groupdocs.com/signature/java) – Chi tiết các chữ ký phương thức và mô tả tham số.

## Câu hỏi thường gặp

**Q: Có thể dùng GroupDocs.Signature với Java 17 không?**  
A: Có – thư viện hoàn toàn tương thích với JDK 8, 11 và 17.

**Q: Mã vạch có tồn tại sau chu kỳ in‑quét không?**  
A: Khi sử dụng Code128 hoặc QR với kích thước và độ tương phản đủ, mã vạch vẫn có thể quét được sau khi in và quét lại.

**Q: Một tài liệu có thể chứa bao nhiêu mã vạch?**  
A: Không có giới hạn cứng; tuy nhiên, để hiệu năng tối ưu, nên giữ tổng số dưới **200** mã vạch mỗi tài liệu.

**Q: Có cần giấy phép cho bản dựng phát triển không?**  
A: Giấy phép tạm thời loại bỏ các dấu nước đánh giá; giấy phép đầy đủ là bắt buộc cho bất kỳ triển khai sản xuất nào.

**Q: Có thể ký PDF được bảo vệ bằng mật khẩu không?**  
A: Có – cung cấp mật khẩu khi tạo đối tượng `Signature`; API sẽ mở khóa tệp nội bộ.

---

**Cập nhật lần cuối:** 2026-07-15  
**Kiểm thử với:** GroupDocs.Signature 23.9 cho Java  
**Tác giả:** GroupDocs  

{< /blocks/products/pf/tutorial-page-section >}
{< /blocks/products/pf/main-container >}
{< /blocks/products/pf/main-wrap-class >}
{< blocks/products/products-backtop-button >}

## Hướng dẫn liên quan

- [How to Verify Barcode Signatures in Java with GroupDocs.Signature](/signature/java/search-verification/groupdocs-signature-java-document-verification/)
- [How to Search Digital Signatures in Java Documents with GroupDocs](/signature/java/search-verification/groupdocs-signature-java-digital-search-tutorial/)
- [Java Barcode Signature Tutorial - Add, Verify & Manage Barcodes in PDFs](/signature/java/barcode-signatures/)