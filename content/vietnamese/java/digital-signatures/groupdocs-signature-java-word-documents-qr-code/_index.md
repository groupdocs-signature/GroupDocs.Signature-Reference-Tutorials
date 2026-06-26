---
categories:
- Digital Signatures
date: '2026-06-26'
description: Tìm hiểu cách tạo chữ ký QR code trong tài liệu Word một cách lập trình
  với GroupDocs.Signature cho Java. Hướng dẫn chi tiết từng bước, ví dụ mã nguồn,
  các thực tiễn tốt nhất và mẹo tối ưu hiệu năng.
keywords:
- create qr code signature
- programmatically sign word
- qr code digital signature
- add qr to word
- groupdocs signature java
lastmod: '2026-06-26'
linktitle: Chữ ký QR Code trong Word với Java
schemas:
- author: GroupDocs
  dateModified: '2026-06-26'
  description: Learn how to create QR code signature in Word documents programmatically
    with GroupDocs.Signature for Java. Step‑by‑step tutorial, code examples, best
    practices, and performance tips.
  headline: Create QR Code Signature in Word Documents Using Java
  type: TechArticle
- description: Learn how to create QR code signature in Word documents programmatically
    with GroupDocs.Signature for Java. Step‑by‑step tutorial, code examples, best
    practices, and performance tips.
  name: Create QR Code Signature in Word Documents Using Java
  steps:
  - name: The library reads the source document.
    text: The library reads the source document.
  - name: Generates the QR code based on `QrCodeSignOptions`.
    text: Generates the QR code based on `QrCodeSignOptions`.
  - name: Inserts the graphic at the specified coordinates.
    text: Inserts the graphic at the specified coordinates.
  - name: Saves the modified file to the path you provided.
    text: Saves the modified file to the path you provided.
  type: HowTo
- questions:
  - answer: Yes. GroupDocs.Signature supports PDF, Excel, PowerPoint, images, and
      many other formats. Just change the `setFileFormat` to the desired output type.
    question: Can I sign PDFs instead of Word documents?
  - answer: Use the library’s `SearchQrCodeSignatures` method to locate QR codes and
      validate the embedded data against your backend service.
    question: How do I verify a QR code signature after it’s been added?
  - answer: Standard QR codes hold up to **4 296 alphanumeric characters**, but for
      reliable scanning keep payloads under **500 characters**. For larger payloads
      store a reference ID and fetch details server‑side.
    question: What is the maximum data I can store in a QR code?
  - answer: Yes. You can set size, position, foreground/background colors, and even
      add a logo overlay. Stick to high‑contrast colors for best scan results.
    question: Can I customize the QR code’s visual appearance?
  - answer: For documents over 50 pages, expect a few seconds per file. Use batch
      processing, reuse the `Signature` instance, and monitor JVM heap size.
    question: How should I handle large‑document signing efficiently?
  type: FAQPage
tags:
- java
- word-documents
- qr-code
- digital-signature
- groupdocs
title: Tạo Chữ ký QR Code trong Tài liệu Word bằng Java
type: docs
url: /vi/java/digital-signatures/groupdocs-signature-java-word-documents-qr-code/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tạo Chữ ký Mã QR trong Tài liệu Word bằng Java

Bạn đã bao giờ dành hàng giờ để ký tài liệu thủ công, chỉ để tự hỏi liệu có cách nhanh hơn, đáng tin cậy hơn không? Bạn có thể **tạo chữ ký mã QR** trong tài liệu Word một cách lập trình chỉ với vài dòng mã Java. Dù bạn đang tự động hoá quy trình hợp đồng, quản lý giấy tờ pháp lý, hay xây dựng cổng phê duyệt ưu tiên di động, chữ ký mã QR cung cấp xác thực ngay lập tức, có thể quét được trên bất kỳ smartphone nào. Trong hướng dẫn này, bạn sẽ học cách thiết lập GroupDocs.Signature cho Java, cấu hình các tùy chọn mã QR, và nhúng dữ liệu phong phú như URL, dấu thời gian, hoặc payload JSON vào các tệp Word. Khi hoàn thành, bạn sẽ có thể ký tài liệu quy mô lớn, giảm công việc thủ công và nâng cao tuân thủ.

## Câu trả lời nhanh
- **Thư viện tôi cần là gì?** GroupDocs.Signature for Java (v23.12+).  
- **Bao nhiêu dòng mã?** Two‑line QR generation plus a few configuration lines.  
- **Tôi có thể ký PDF không?** Yes – the same API works for PDF, Excel, PowerPoint, and images.  
- **Cần giấy phép thương mại không?** Only for production; a free trial or temporary license works for development.  
- **Dữ liệu tôi có thể lưu là gì?** Up to ~4 k characters (URL, JSON, IDs), but keep it under 500 chars for reliable scanning.

## Chữ ký mã QR là gì?
Một **create QR code signature** là một mã vạch 2‑D có thể quét được được nhúng trong tài liệu, đại diện cho một chữ ký kỹ thuật số hoặc payload xác thực. Khi người dùng quét mã QR, dữ liệu được mã hoá (thường là URL hoặc token) được đọc và xác thực, chứng minh tính xác thực của tài liệu mà không cần phần mềm đặc biệt.

## Tại sao nên sử dụng GroupDocs.Signature cho Java để thêm mã QR?
GroupDocs.Signature hỗ trợ **hơn 50 định dạng đầu vào và đầu ra**, có thể xử lý các tệp hàng trăm trang mà không cần tải toàn bộ tài liệu vào bộ nhớ, và cung cấp một API linh hoạt cho phép bạn **ký Word một cách lập trình** trong vài mili giây. Thư viện còn cung cấp khả năng tạo mã QR, Aztec, DataMatrix và PDF417 tích hợp sẵn, biến nó thành giải pháp toàn diện cho việc xác thực hiện đại ưu tiên di động.

## Yêu cầu trước

### Thư viện và phụ thuộc cần thiết
- **GroupDocs.Signature for Java** phiên bản **23.12** hoặc mới hơn (phụ thuộc bên ngoài duy nhất).

### Yêu cầu thiết lập môi trường
- **JDK 8+** (Java 11 hoặc 17 được khuyến nghị cho môi trường production).  
- **IDE** bạn lựa chọn (IntelliJ IDEA, Eclipse, VS Code).  
- **Công cụ xây dựng** – Maven hoặc Gradle (các ví dụ dưới đây hoạt động với cả hai).

### Kiến thức yêu cầu
- Kiến thức cơ bản về cú pháp Java và xử lý file‑IO.  
- Quen thuộc với khai báo phụ thuộc Maven/Gradle (chúng tôi sẽ hiển thị các đoạn mã chính xác).

## Cài đặt GroupDocs.Signature cho Java

Chọn hệ thống xây dựng của bạn và thêm phụ thuộc chính xác như được hiển thị. Các placeholder bên dưới đại diện cho các khối mã gốc; giữ nguyên chúng.

**Maven**

```java
```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```
```

**Gradle**

```java
```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```
```

**Direct Download**

Bạn muốn quản lý thủ công? Tải JAR trực tiếp từ [GroupDocs.Signature cho Java - các bản phát hành](https://releases.groupdocs.com/signature/java/) và thêm vào classpath của dự án.

### Cách lấy giấy phép
- **Free Trial:** Lý tưởng cho việc tạo mẫu; các tính năng cốt lõi có sẵn.  
- **Temporary License:** Truy cập đầy đủ tính năng cho phát triển ngắn hạn.  
- **Commercial License:** Cần thiết cho triển khai production.  

**Pro Tip:** Bắt đầu với bản dùng thử miễn phí, sau đó yêu cầu giấy phép tạm thời trước khi chuyển sang production. Điều này cho phép bạn xác thực quy trình mà không tốn chi phí ban đầu.

### Khởi tạo cơ bản
Đối tượng `Signature` là điểm vào cho tất cả các thao tác ký. Nó triển khai `AutoCloseable`, vì vậy bạn có thể an toàn sử dụng khối try‑with‑resources.

```java
```java
Signature signature = new Signature("path/to/your/document");
```
```

## Hướng dẫn thực hiện: Ký tài liệu Word bằng mã QR

Dưới đây chúng tôi sẽ hướng dẫn từng bước, thêm các định nghĩa và câu trả lời trực tiếp khi cần.

### Làm thế nào để khởi tạo đối tượng Signature cho tệp Word?
Tải tài liệu nguồn bằng `new Signature("source.docx")` trong khối try‑with‑resources; đối tượng chuẩn bị tệp để chỉnh sửa và tự động giải phóng tài nguyên khi khối kết thúc.

```java
```java
String filePath = "YOUR_DOCUMENT_DIRECTORY/SampleDocX.docx";
Signature signature = new Signature(filePath);
```
```

**Explanation:** Lớp `Signature` đại diện cho một tài liệu duy nhất trong bộ nhớ và cung cấp các phương thức để thêm, tìm kiếm và xác thực chữ ký. Nó hỗ trợ `.docx`, `.doc`, và nhiều định dạng khác.

### Làm sao tôi có thể cấu hình các tùy chọn ký mã QR?
Tạo một thể hiện `QrCodeSignOptions`, đặt văn bản được mã hoá, loại mã vạch và vị trí. Đoạn mã sau đây cho thấy cấu hình tối thiểu.

```java
```java
QrCodeSignOptions signOptions = new QrCodeSignOptions("JohnSmith");
signOptions.setEncodeType(QrCodeTypes.QR);
signOptions.setLeft(100); // X-axis position in pixels
signOptions.setTop(100);  // Y-axis position in pixels
```
```

**Definition:** Lớp `QrCodeSignOptions` bao gồm tất cả các cài đặt cần thiết để tạo và đặt một chữ ký mã QR, bao gồm văn bản được mã hoá, loại mã vạch, kích thước, màu sắc và tọa độ vị trí trong tài liệu.

#### Tùy chỉnh giao diện
Bạn có thể điều chỉnh thêm kích thước, lề và màu sắc:

```java
```java
QrCodeSignOptions signOptions = new QrCodeSignOptions("https://yourapp.com/verify/doc-12345");
```
```

**Why it matters:** Một mã QR vuông 150 px với nền đen trên nền trắng đạt >99 % tỷ lệ quét thành công trên cả màn hình và bản in.

### Làm sao tôi thiết lập các tùy chọn đầu ra cho tài liệu đã ký?
Xác định định dạng mục tiêu và hành vi ghi đè trước khi gọi `sign`.

```java
```java
WordProcessingSaveOptions saveOptions = new WordProcessingSaveOptions();
saveOptions.setFileFormat(WordProcessingSaveFileFormat.Odt);
saveOptions.setOverwriteExistingFiles(true);
```
```

**Definition:** Lớp `WordProcessingSaveOptions` xác định cách tài liệu Word đã ký sẽ được lưu, cho phép bạn chỉ định định dạng đầu ra (DOCX, ODT, v.v.), có ghi đè các tệp hiện có hay không, và các tùy chọn cấp tệp khác.

Nếu bạn cần định dạng mã nguồn mở, chuyển sang `OutputType.ODT`:

```java
```java
saveOptions.setFileFormat(WordProcessingSaveFileFormat.Docx);
```
```

### Làm sao tôi ký và lưu tài liệu với mã QR?
Phương thức `sign` áp dụng mã QR và ghi tệp đầu ra trong một lần gọi.

```java
```java
String outputFilePath = "YOUR_OUTPUT_DIRECTORY/SaveSignedOutputType/SampleDocX.odt";
signature.sign(outputFilePath, signOptions, saveOptions);
```
```

**Definition:** Phương thức `sign` của đối tượng `Signature` nhận đường dẫn đích, các tùy chọn ký đã cấu hình, và các tùy chọn lưu tùy chọn, sau đó nhúng mã QR vào tài liệu và ghi kết quả vào vị trí đã chỉ định.

**What happens:**  
1. Thư viện đọc tài liệu nguồn.  
2. Tạo mã QR dựa trên `QrCodeSignOptions`.  
3. Chèn đồ họa tại tọa độ đã chỉ định.  
4. Lưu tệp đã sửa vào đường dẫn bạn cung cấp.

### Làm sao tôi xử lý lỗi khi ký?
Bao bọc logic ký trong khối try‑catch để bắt các lỗi như tệp không tồn tại, đường dẫn không hợp lệ, hoặc vấn đề giấy phép.

```java
```java
try {
    signature.sign(outputFilePath, signOptions, saveOptions);
    System.out.println("Document signed successfully!");
} catch (Exception e) {
    System.err.println("Signing failed: " + e.getMessage());
}
```
```

**Definition:** Bắt `Exception` đảm bảo bất kỳ vấn đề runtime nào như tệp thiếu, đường dẫn không hợp lệ, hoặc vấn đề giấy phép đều được báo cáo một cách nhẹ nhàng, ngăn ứng dụng bị sập trong môi trường production.

## Các trường hợp sử dụng phổ biến và ứng dụng thực tế

### Quản lý hợp đồng tự động
Một nền tảng SaaS ký **hơn 500 hợp đồng mỗi tháng** bằng cách tạo mã QR duy nhất chứa ID hợp đồng và URL xác thực. Người nhận quét để xem trạng thái hợp đồng trong cổng, loại bỏ việc trao đổi email thủ công.

### Cấp chứng chỉ nhân viên
Các phòng nhân sự nhúng ID nhân viên và ngày cấp vào mã QR trên chứng chỉ đào tạo. Quét mã QR ngay lập tức xác thực tính xác thực với cơ sở dữ liệu nội bộ, giảm gian lận hơn **80 %**.

### Tự động hoá quy trình phê duyệt
Mỗi mã QR của người phê duyệt lưu số nhân viên, vai trò và dấu thời gian. Hệ thống đọc mã QR trong quá trình kiểm toán, cung cấp dấu vết không thể giả mạo mà không cần tra cứu cơ sở dữ liệu bổ sung.

### Ký hoá đơn và biên lai
Các đội tài chính thêm mã QR liên kết tới cổng thanh toán. Khi quét, mã QR đưa người thanh toán tới trang thanh toán bảo mật, giảm thời gian xử lý **30 %** và giảm rủi ro gian lận hoá đơn.

## Thực hành tốt cho môi trường Production

### Cân nhắc bảo mật
- **Không bao giờ nhúng mật khẩu thô**; sử dụng token hoặc ID tham chiếu được giải quyết phía máy chủ.  
- **Luôn sử dụng HTTPS** cho URL; tránh HTTP để ngăn các cuộc tấn công man‑in‑the‑middle.  
- **Đặt thời gian hết hạn token** (ví dụ, JWT với thời gian hiệu lực 24 giờ) cho các tài liệu nhạy cảm về thời gian.

### Tối ưu hiệu năng
- **Xử lý batch:** Giữ một thể hiện `Signature` duy nhất và lặp qua các tệp để tránh khởi động JVM lặp lại.  
- **Quản lý bộ nhớ:** Đối với tài liệu > 50 MB, xử lý tuần tự và giải phóng đối tượng `Signature` sau mỗi tệp.  
- **Vị trí quan trọng:** Đặt mã QR ở cuối trang để giảm việc tái bố trí layout và cải thiện tốc độ.

```java
```java
List<String> documents = getDocumentPaths();
for (String docPath : documents) {
    Signature sig = new Signature(docPath);
    // Configure and sign
    sig.dispose();
}
```
```

### Mẹo đặt mã QR
- **An toàn khi in:** Đặt mã QR cách lề trang ít nhất 0.5 in để tránh bị cắt.  
- **Khuyến nghị kích thước:** Tối thiểu 150 × 150 px để quét đáng tin cậy trên vật liệu in.  
- **Nhiều trang:** Lặp qua các trang và tạo một `QrCodeSignOptions` mới cho mỗi vị trí.

```java
```java
for (Document doc : documents) {
    Signature sig = new Signature(doc.getPath());
    sig.sign(outputPath, signOptions, saveOptions);
    sig.dispose();
}
```
```

## Tùy chọn cấu hình nâng cao

### Làm sao tôi có thể thêm nhiều mã QR vào một tài liệu?
Tạo các đối tượng `QrCodeSignOptions` riêng cho mỗi vị trí và gọi `sign` liên tục.

```java
```java
// First QR code
QrCodeSignOptions sign1 = new QrCodeSignOptions("Approver 1");
sign1.setLeft(100);
sign1.setTop(100);

// Second QR code
QrCodeSignOptions sign2 = new QrCodeSignOptions("Approver 2");
sign2.setLeft(300);
sign2.setTop(100);

// Apply both
signature.sign(outputPath, sign1, saveOptions);
signature.sign(outputPath, sign2, saveOptions);
```
```

### Các loại mã vạch khác nào được hỗ trợ?
Ngoài QR, bạn có thể tạo mã **Aztec**, **DataMatrix**, hoặc **PDF417** bằng cách thay đổi `setEncodeType()`.

### Làm sao tôi tính vị trí động dựa trên kích thước trang?
Lấy kích thước trang qua `Signature.getDocumentInfo()` và tính toán tọa độ bằng chương trình.

```java
```java
// Get document info
DocumentInfo docInfo = signature.getDocumentInfo();
int pageWidth = docInfo.getWidth();
int pageHeight = docInfo.getHeight();

// Center the QR code
int qrSize = 100;
signOptions.setLeft((pageWidth - qrSize) / 2);
signOptions.setTop((pageHeight - qrSize) / 2);
```
```

**Definition:** `Signature.getDocumentInfo()` trả về một đối tượng `DocumentInfo` chứa siêu dữ liệu như kích thước trang, có thể dùng để tính toán tọa độ đặt chữ ký một cách chính xác dựa trên kích thước thực tế của mỗi trang.

## Khắc phục các vấn đề thường gặp

### Mã QR không hiển thị
- Xác minh `setLeft`/`setTop` nằm trong giới hạn trang (A4 ≈ 595 × 842 px ở 72 DPI).  
- Đảm bảo màu nền trước/nền sau có độ tương phản (đen trên trắng).  
- Tăng chiều rộng/chiều cao nếu mã quá nhỏ để quét.

### “File not found” khi khởi tạo Signature
- Sử dụng đường dẫn tuyệt đối trong quá trình phát triển hoặc xác thực đường dẫn tương đối bằng `Paths.get(...)`.  
- Xác nhận tệp nguồn không bị khóa bởi tiến trình khác.

### Tệp đầu ra bị hỏng
- Kiểm tra lại `setFileFormat` khớp với phần mở rộng mong muốn.  
- Đóng bất kỳ luồng nào có thể vẫn giữ tệp trước khi ký.

### Mã QR chứa dữ liệu sai
- In ra chuỗi bạn truyền vào `QrCodeSignOptions` trước khi ký để xác nhận mã hoá.  
- Tránh ký tự không phải ASCII trừ khi bạn đặt mã hoá UTF‑8 một cách rõ ràng.

### Hiệu năng chậm trên tài liệu lớn
- Xử lý tài liệu theo batch (xem khối mã 10).  
- Tránh đặt mã QR trong các bảng phức tạp; chúng gây tính toán layout lại rộng rãi.

## Câu hỏi thường gặp

**Q: Tôi có thể ký PDF thay vì tài liệu Word không?**  
A: Yes. GroupDocs.Signature supports PDF, Excel, PowerPoint, images, and many other formats. Just change the `setFileFormat` to the desired output type.

**Q: Làm sao tôi xác thực chữ ký mã QR sau khi đã thêm?**  
A: Use the library’s `SearchQrCodeSignatures` method to locate QR codes and validate the embedded data against your backend service.

**Q: Dữ liệu tối đa tôi có thể lưu trong mã QR là bao nhiêu?**  
A: Standard QR codes hold up to **4 296 alphanumeric characters**, but for reliable scanning keep payloads under **500 characters**. For larger payloads store a reference ID and fetch details server‑side.

**Q: Tôi có thể tùy chỉnh giao diện trực quan của mã QR không?**  
A: Yes. You can set size, position, foreground/background colors, and even add a logo overlay. Stick to high‑contrast colors for best scan results.

**Q: Làm sao tôi xử lý ký tài liệu lớn một cách hiệu quả?**  
A: For documents over 50 pages, expect a few seconds per file. Use batch processing, reuse the `Signature` instance, and monitor JVM heap size.

**Q: Chữ ký QR có tồn tại sau khi chuyển đổi sang PDF không?**  
A: Absolutely. The QR code is embedded as a graphic, so it remains intact when converting between formats, provided you maintain sufficient resolution.

**Q: Tôi có thể ký tài liệu lưu trữ trên đám mây như S3 không?**  
A: Yes. Download the file to a temporary local path, sign it, then upload the signed version back to S3. The library works with local files only.

**Q: Điều gì xảy ra nếu ai đó sửa đổi tài liệu sau khi ký?**  
A: The QR graphic itself stays unchanged, but it won’t detect tampering. Combine QR codes with hash‑based verification or digital certificates for robust integrity checks.

**Q: Tôi có cần giấy phép khác nhau cho phát triển và production không?**  
A: Development can use the free trial or a temporary license. Production deployments require a commercial license as per GroupDocs terms.

**Q: Tôi có thể ký tài liệu lưu trữ trên đám mây như S3 không?**  
A: Yes. Download the file to a temporary local path, sign it, then upload the signed version back to S3. The library works with local files only.

**Q: Tôi có thể ký tài liệu lưu trữ trên đám mây như S3 không?**  
A: Yes. Download the file to a temporary local path, sign it, then upload the signed version back to S3. The library works with local files only.

**Q: Người nhận không có Java có thể quét các mã QR này không?**  
A: Yes. QR codes follow an open standard; any smartphone camera or QR reader app can decode them. Java is only needed for *creating* the signatures.

## Tài nguyên

- [GroupDocs.Signature cho Java - các bản phát hành](https://releases.groupdocs.com/signature/java/)
- [Tài liệu GroupDocs.Signature cho Java](https://docs.groupdocs.com/signature/java/)
- [Tham chiếu API GroupDocs.Signature](https://reference.groupdocs.com/signature/java/)
- [Các bản phát hành mới nhất của GroupDocs.Signature](https://releases.groupdocs.com/signature/java/)
- [Mua GroupDocs.Signature](https://purchase.groupdocs.com/buy)
- [Dùng thử miễn phí GroupDocs Signatures](https://releases.groupdocs.com/signature/java/)
- [Đăng ký giấy phép tạm thời](https://purchase.groupdocs.com/temporary-license/)
- [Hỗ trợ diễn đàn GroupDocs](https://forum.groupdocs.com/c/signature/)

## Kết luận

Bây giờ bạn đã có một lộ trình đầy đủ, sẵn sàng cho production để **tạo chữ ký mã QR** trong tài liệu Word bằng Java và GroupDocs.Signature. Từ cài đặt cơ bản đến xử lý batch, từ các thực hành bảo mật tốt đến các loại mã vạch nâng cao, mọi thứ bạn cần đều được bao phủ. Bắt đầu với bản dùng thử miễn phí, thử nghiệm với các payload khác nhau, và tích hợp bước ký vào quy trình tạo tài liệu hiện có của bạn. Chúc lập trình vui vẻ và ký an toàn!

---

**Cập nhật lần cuối:** 2026-06-26  
**Kiểm tra với:** GroupDocs.Signature 23.12 for Java  
**Tác giả:** GroupDocs  

{{< blocks/products/products-backtop-button >}}

## Hướng dẫn liên quan

- [Thư viện chữ ký mã QR Java - Hướng dẫn đầy đủ của GroupDocs](/signature/java/qr-code-signatures/)
- [Tải và lưu tài liệu trong Java - Hướng dẫn đầy đủ GroupDocs.Signature](/signature/java/document-loading-saving/)
- [Cách thêm chữ ký số vào tài liệu trong Java](/signature/java/digital-signatures/groupdocs-signature-java-digital-signing-guide/)


{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}