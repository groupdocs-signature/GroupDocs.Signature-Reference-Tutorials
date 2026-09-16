---
categories:
- Document Signing
- Healthcare Integration
date: '2026-09-15'
description: Tìm hiểu cách ký PDF bằng mã vạch sử dụng GroupDocs.Signature for Java.
  Hướng dẫn từng bước để thêm Data Matrix và QR code vào tài liệu y tế.
keywords:
- sign pdf with barcode
- add qr code pdf
- hibc barcode java
- pdf signing java
- healthcare barcode signing
lastmod: '2026-09-15'
linktitle: Hướng dẫn ký PDF HIBC bằng Java
og_description: Ký PDF bằng mã vạch sử dụng GroupDocs.Signature for Java. Tìm hiểu
  cách nhúng Data Matrix và QR code vào tài liệu y tế trong vài bước.
og_image_alt: 'Developer tutorial: sign PDF with HIBC barcode using GroupDocs.Signature
  for Java'
og_title: Ký PDF bằng mã vạch sử dụng HIBC trong Java – Hướng dẫn của GroupDocs
schemas:
- author: GroupDocs
  dateModified: '2026-09-15'
  description: Learn how to sign PDF with barcode using GroupDocs.Signature for Java.
    Step‑by‑step guide for adding Data Matrix and QR codes in healthcare documents.
  headline: Sign PDF with barcode using HIBC in Java
  type: TechArticle
- description: Learn how to sign PDF with barcode using GroupDocs.Signature for Java.
    Step‑by‑step guide for adding Data Matrix and QR codes in healthcare documents.
  name: Sign PDF with barcode using HIBC in Java
  steps:
  - name: '**Import the required classes** – these give you access to the signature
      engine and Data Matrix options.'
    text: '**Import the required classes** – these give you access to the signature
      engine and Data Matrix options.'
  - name: '**Instantiate the `Signature` object** with absolute paths for source and
      destination files.'
    text: '**Instantiate the `Signature` object** with absolute paths for source and
      destination files.'
  - name: '**Configure the Data Matrix options** – set the HIBC string, choose `QrCodeTypes.HIBCLICDataMatrix`,
      and define placement coordinates. `QrCodeTypes` enumerates the supported barcode
      formats for HIBC signatures.'
    text: '**Configure the Data Matrix options** – set the HIBC string, choose `QrCodeTypes.HIBCLICDataMatrix`,
      and define placement coordinates. `QrCodeTypes` enumerates the supported barcode
      formats for HIBC signatures.'
  - name: '**Apply the signature** to the PDF.'
    text: '**Apply the signature** to the PDF.'
  - name: '**Dispose of resources** to free file handles and avoid memory leaks.'
    text: '**Dispose of resources** to free file handles and avoid memory leaks.'
  - name: '**Import QR‑specific classes**'
    text: '**Import QR‑specific classes**'
  - name: '**Create and configure QR options** – note the use of `QrCodeTypes.HIBCLICQR`.'
    text: '**Create and configure QR options** – note the use of `QrCodeTypes.HIBCLICQR`.'
  - name: '**Sign the document**'
    text: '**Sign the document**'
  type: HowTo
- questions:
  - answer: Yes, it also supports DOCX, XLSX, PPTX, PNG, JPEG, and TIFF with the same
      barcode‑signing API.
    question: Can GroupDocs.Signature sign file types other than PDF?
  - answer: Verify that your HIBC string follows the exact HIBCC syntax, use the online
      validator, and ensure you’re using the correct `QrCodeTypes` constant for the
      chosen format.
    question: How do I troubleshoot “Invalid barcode content” errors?
  - answer: QR ≈ 4,296 alphanumeric characters, Aztec ≈ 3,832 numeric / 3,067 alphanumeric,
      Data Matrix ≈ 3,116 numeric / 2,335 alphanumeric. Keep codes under 200 characters
      for optimal scan reliability.
    question: What is the maximum data capacity for each HIBC format?
  - answer: Absolutely. Create separate `QrCodeSignOptions` objects with different
      positions and call `signature.sign()` for each. Just ensure they don’t overlap.
    question: Is it possible to embed multiple barcode types in one PDF?
  - answer: No. After the JAR is on the classpath and the license is activated, all
      operations are performed locally.
    question: Do I need an internet connection for signing at runtime?
  type: FAQPage
tags:
- sign pdf
- barcode
- java
- healthcare
- groupdocs
title: Cách ký PDF bằng mã vạch sử dụng HIBC trong Java
type: docs
url: /vi/java/barcode-signatures/sign-pdfs-hibc-lic-codes-groupdocs-java/
weight: 1
---

# Ký PDF bằng mã vạch sử dụng HIBC trong Java

Nếu bạn đang xây dựng phần mềm logistics dược phẩm hoặc chăm sóc sức khỏe, có thể bạn đã gặp phải vấn đề theo dõi dựa trên giấy, chữ ký mất và cơn ác mộng kiểm toán. **Ký một PDF bằng mã vạch**—đặc biệt là mã Data Matrix hoặc QR của HIBC—tạo ra một dấu vết không thể giả mạo, có thể đọc bằng máy, tồn tại qua việc in, quét và kiểm tra quy định. Trong hướng dẫn này, bạn sẽ thấy chính xác cách thêm cả mã Data Matrix và QR vào PDF bằng GroupDocs.Signature cho Java.

## Câu trả lời nhanh
- **Thư viện nào xử lý mã vạch HIBC trong Java?** GroupDocs.Signature for Java.  
- **Định dạng mã vạch nào gọn nhất?** Data Matrix – lý tưởng cho nhãn nhỏ.  
- **Tôi có thể thêm cả QR và Data Matrix vào cùng một PDF không?** Có, chỉ cần tạo các `QrCodeSignOptions` riêng biệt.  
- **Tôi có cần kết nối internet khi chạy không?** Không, thư viện hoạt động hoàn toàn offline sau khi cài đặt.  
- **Phiên bản Java nào được khuyến nghị?** Java 11+ cho hiệu năng cấp sản xuất.

## Chữ ký PDF bằng mã vạch HIBC là gì?
`Signature` là lớp cốt lõi của GroupDocs.Signature đại diện cho tài liệu PDF và cho phép nhúng chữ ký số. Lớp `Signature` trong GroupDocs.Signature cho Java cung cấp các phương thức để nhúng mã vạch HIBC như là chữ ký số. Bằng cách ký một PDF bằng mã vạch HIBC, bạn tạo ra một bản ghi có thể xác minh, không thể giả mạo và có thể được quét ở bất kỳ điểm nào trong chuỗi cung ứng.

## Tại sao lại sử dụng đồng thời Data Matrix và QR code?
Data Matrix cung cấp kích thước nhỏ nhất trong khi vẫn chứa tới 2.335 ký tự alphanumeric, làm cho nó hoàn hảo cho các khu vực nhãn dày đặc. QR code, ngược lại, hỗ trợ tới 4.296 ký tự và có thể đọc được rộng rãi bởi điện thoại thông minh. Kết hợp cả hai mang lại sự cân bằng tốt nhất giữa hiệu quả không gian và dung lượng dữ liệu, đảm bảo mọi bên liên quan—từ máy quét kho đến ứng dụng di động—có thể đọc được thông tin cần thiết.

## Yêu cầu trước
- **JDK 11 hoặc cao hơn** (Java 8 vẫn hoạt động nhưng Java 11+ được khuyến nghị để đạt hiệu năng tối ưu).  
- **IDE** như IntelliJ IDEA, Eclipse, hoặc VS Code với các tiện ích mở rộng Java.  
- **Maven hoặc Gradle** để quản lý phụ thuộc (các ví dụ bên dưới).  
- **PDF mẫu** (ví dụ, `sample.pdf`) để kiểm tra triển khai.  
- **Giấy phép GroupDocs.Signature hợp lệ** (bản dùng thử miễn phí cho phát triển, giấy phép trả phí cho sản xuất).

## Cài đặt GroupDocs.Signature cho Java

### Cấu hình Maven
Thêm phụ thuộc vào `pom.xml` của bạn:

```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

### Cấu hình Gradle
Đối với dự án Gradle, thêm đoạn này vào `build.gradle` của bạn:

```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

### Tùy chọn tải xuống trực tiếp
Bạn cũng có thể tải tệp JAR trực tiếp từ [GroupDocs.Signature for Java releases](https://releases.groupdocs.com/signature/java/) và thêm nó vào classpath của dự án một cách thủ công. Cách này hoạt động tốt trong môi trường mạng bị hạn chế.

### Nhận giấy phép
Yêu cầu bản dùng thử miễn phí hoặc giấy phép tạm thời từ GroupDocs để loại bỏ watermark và mở khóa tất cả tính năng. Triển khai sản xuất yêu cầu mua giấy phép.

### Khởi tạo cơ bản
`Signature` là điểm vào cho tất cả các thao tác ký. Nó tải PDF, áp dụng mã vạch và ghi tệp đã ký.

```java
import com.groupdocs.signature.Signature;

class InitializeSignature {
    public static void main(String[] args) {
        Signature signature = new Signature("sample.pdf");
        // Proceed with signing operations...
    }
}
```

## Cách tạo PDF Data Matrix với mã vạch HIBC?
Khởi tạo `Signature` với PDF nguồn của bạn, đặt `QrCodeSignOptions` ở định dạng **Data Matrix**, cung cấp một chuỗi HIBC được định dạng đúng và gọi `sign()`. Thư viện sẽ ghi PDF đã ký vào đích, giữ nguyên bố cục và nhúng mã vạch như một chữ ký không thể giả mạo.

`QrCodeSignOptions` chỉ định loại mã vạch, nội dung, kích thước và vị trí cho một chữ ký.

1. **Nhập các lớp cần thiết** – các lớp này cho phép bạn truy cập vào engine ký và các tùy chọn Data Matrix.  
```java
import com.groupdocs.signature.Signature;
import com.groupdocs.signature.options.sign.QrCodeSignOptions;
import com.groupdocs.signature.domain.qrcodes.QrCodeTypes;
```

2. **Khởi tạo đối tượng `Signature`** với đường dẫn tuyệt đối cho các tệp nguồn và đích.  
```java
String sourceFilePath = "YOUR_DOCUMENT_DIRECTORY";
String destinFilePath = "YOUR_OUTPUT_DIRECTORY/SignWithHIBCLICQR.pdf";

final Signature signature = new Signature(sourceFilePath);
```

3. **Cấu hình các tùy chọn Data Matrix** – đặt chuỗi HIBC, chọn `QrCodeTypes.HIBCLICDataMatrix`, và xác định tọa độ vị trí. `QrCodeTypes` liệt kê các định dạng mã vạch được hỗ trợ cho chữ ký HIBC.  
```java
QrCodeSignOptions hibcLic_QR = new QrCodeSignOptions("A123PROD30917/75#422011907#GP293", QrCodeTypes.HIBCLICQR);
hibcLic_QR.setLeft(1); // Set the position from left
hibcLic_QR.setTop(1);   // Set the position from top
hibcLic_QR.setReturnContent(true); // Return content after signing
hibcLic_QR.setReturnContentType(FileType.PNG); // Specify return content type as PNG
```

4. **Áp dụng chữ ký** vào PDF.  
```java
signature.sign(destinFilePath, hibcLic_QR);
```

5. **Giải phóng tài nguyên** để giải phóng các handle tệp và tránh rò rỉ bộ nhớ.  
```java
finally {
    if (signature != null) signature.dispose();
}
```

### Ví dụ làm việc đầy đủ
Dưới đây là luồng đầy đủ trong một khối duy nhất (các placeholder đại diện cho mã chính xác bạn sẽ dán từ các đoạn mã trước):

```java
import com.groupdocs.signature.Signature;
import com.groupdocs.signature.options.sign.QrCodeSignOptions;
import com.groupdocs.signature.domain.qrcodes.QrCodeTypes;

public class HibcQrSigning {
    public static void main(String[] args) {
        String sourceFilePath = "sample.pdf";
        String destinFilePath = "output/SignWithHIBCLICQR.pdf";
        
        Signature signature = null;
        try {
            signature = new Signature(sourceFilePath);
            
            QrCodeSignOptions hibcLic_QR = new QrCodeSignOptions(
                "A123PROD30917/75#422011907#GP293", 
                QrCodeTypes.HIBCLICQR
            );
            hibcLic_QR.setLeft(1);
            hibcLic_QR.setTop(1);
            hibcLic_QR.setReturnContent(true);
            hibcLic_QR.setReturnContentType(FileType.PNG);
            
            signature.sign(destinFilePath, hibcLic_QR);
            System.out.println("PDF signed successfully with HIBC QR code");
            
        } catch (Exception e) {
            System.err.println("Error signing PDF: " + e.getMessage());
            e.printStackTrace();
        } finally {
            if (signature != null) signature.dispose();
        }
    }
}
```

#### Câu trả lời ngắn gọn (40–70 từ)
Để **tạo PDF Data Matrix**, khởi tạo `Signature` với PDF nguồn của bạn, đặt `QrCodeSignOptions` thành `QrCodeTypes.HIBCLICDataMatrix` và cung cấp một chuỗi HIBC được định dạng đúng, sau đó gọi `signature.sign(outputPath, options)`. Thư viện sẽ ghi PDF đã ký vào đích, giữ nguyên bố cục và nhúng mã vạch như một chữ ký không thể giả mạo.

## Cách thêm QR code vào PDF bằng GroupDocs.Signature?
Tải PDF, cấu hình `QrCodeSignOptions` cho định dạng QR, và gọi `sign()`. Thư viện sẽ điều chỉnh kích thước hình ảnh QR để dễ đọc và đặt vị trí dựa trên tọa độ bạn thiết lập, tránh chồng lấn với nội dung hiện có. Điều này đảm bảo mã vạch vẫn có thể quét được sau khi in và tuân thủ tiêu chuẩn HIBC.

`QrCodeSignOptions` định nghĩa nội dung, kích thước và vị trí của mã QR.

1. **Nhập các lớp đặc thù cho QR**  
```java
QrCodeSignOptions hibcLic_AZ = new QrCodeSignOptions("A123PROD30917/75#422011907#GP293", QrCodeTypes.HIBCLICAztec);
hibcLic_AZ.setLeft(1); // Set the position from left
hibcLic_AZ.setTop(200); // Set the position from top
hibcLic_AZ.setReturnContent(true); // Return content after signing
hibcLic_AZ.setReturnContentType(FileType.PNG); // Specify return content type as PNG
```

2. **Tạo và cấu hình các tùy chọn QR** – lưu ý việc sử dụng `QrCodeTypes.HIBCLICQR`.  
```java
signature.sign(destinFilePath, hibcLic_AZ);
```

3. **Ký tài liệu**  
```java
QrCodeSignOptions hibcLic_DM = new QrCodeSignOptions("A123PROD30917/75#422011907#GP293", QrCodeTypes.HIBCLICDataMatrix);
hibcLic_DM.setLeft(1); // Set the position from left
hibcLic_DM.setTop(400); // Set the position from top
hibcLic_DM.setReturnContent(true); // Return content after signing
hibcLic_DM.setReturnContentType(FileType.PNG); // Specify return content type as PNG
```

> **Direct answer:** Sử dụng `QrCodeTypes.HIBCLICQR` trong `QrCodeSignOptions`, đặt chuỗi nội dung HIBC, định vị mã bằng `setLeft()` và `setTop()`, sau đó gọi `signature.sign(outputPath, options)`. Mã QR được nhúng ngay lập tức, sẵn sàng cho việc quét bằng điện thoại thông minh hoặc máy quét.

## Những lỗi thường gặp cần tránh

### 1. Quên giải phóng tài nguyên
**Sai:**  
```java
Signature signature = new Signature("sample.pdf");
signature.sign(destinFilePath, options);
// Oops, no dispose() call
```  

**Sửa:** Đặt việc sử dụng `Signature` trong khối try‑with‑resources hoặc gọi `close()` một cách rõ ràng trong khối finally.

### 2. Sử dụng chuỗi định dạng HIBC không đúng
**Sai:** Sử dụng các chuỗi chung như “12345”.  
**Sửa:** Tuân theo tiêu chuẩn HIBCC (ví dụ, `A123PROD30917/75#422011907#GP293`). Xác thực với [HIBCC online validator](https://www.hibcc.org/).

### 3. Ghi cứng đường dẫn tệp
**Sai:**  
```java
String sourceFilePath = "C:/Users/John/Documents/test.pdf";
```  

**Sửa:** Lưu các đường dẫn trong tệp cấu hình hoặc biến môi trường và đọc chúng khi chạy.

### 4. Bỏ qua xung đột vị trí mã vạch
Đặt mã vạch cách xa văn bản hoặc chữ ký hiện có. Sử dụng tọa độ PDF (gốc ở góc dưới‑trái) và kiểm tra với mẫu đã in.

### 5. Không kiểm tra với máy quét thực tế
In PDF đã ký và quét nó bằng phần cứng chính xác được sử dụng trong quy trình của bạn. Xác minh khả năng đọc ở các chất lượng in khác nhau.

## Ứng dụng thực tiễn trong chăm sóc sức khỏe

| Kịch bản | Mã vạch đề xuất | Lý do phù hợp |
|----------|--------------------|--------------|
| **Phân phối dược phẩm** | QR Code | Dung lượng dữ liệu cao, được quét rộng rãi bởi điện thoại thông minh. |
| **Quản lý tồn kho** | Data Matrix | Kích thước nhỏ, lý tưởng cho nhãn kệ dày đặc. |
| **Tuân thủ quy định (FDA 21 CFR Part 11)** | QR + Data Matrix | Định dạng kép cung cấp tính dư thừa và khả năng kiểm toán. |
| **Theo dõi thiết bị y tế** | Aztec Code | Kích thước gọn gàng phù hợp với bao bì không gian hạn chế. |

## Các cân nhắc về hiệu năng và thực hành tốt nhất

### Batch processing pattern
```java
List<String> filesToSign = getFileList();
for (String filePath : filesToSign) {
    Signature signature = null;
    try {
        signature = new Signature(filePath);
        // Sign and save
    } finally {
        if (signature != null) signature.dispose();
    }
}
```

- Tạo một thể hiện `Signature` mới cho mỗi tệp để giữ mức sử dụng bộ nhớ thấp.  
- Sử dụng một pool thread cố định (`Executors.newFixedThreadPool(Runtime.getRuntime().availableProcessors() - 1)`) cho xử lý song song, nhưng giám sát kích thước heap vì mỗi `Signature` giữ toàn bộ PDF trong bộ nhớ.  

### Giữ thư viện luôn cập nhật
Các bản phát hành của GroupDocs cải thiện tốc độ xử lý lên tới **20 %** và thêm các tính năng tuân thủ HIBC mới. Lên lịch kiểm tra phụ thuộc hàng quý.

### Lưu trữ mẫu trong bộ nhớ đệm
Tải một mẫu PDF một lần, sao chép nó cho mỗi biến thể mã vạch, và ký các bản sao. Điều này giảm I/O và tăng tốc quy trình khối lượng lớn.

## Câu hỏi thường gặp

**Q: GroupDocs.Signature có thể ký các loại tệp khác ngoài PDF không?**  
A: Có, nó cũng hỗ trợ DOCX, XLSX, PPTX, PNG, JPEG và TIFF với cùng API ký mã vạch.

**Q: Làm thế nào để khắc phục lỗi “Invalid barcode content”?**  
A: Xác minh rằng chuỗi HIBC của bạn tuân theo cú pháp HIBCC chính xác, sử dụng công cụ kiểm tra trực tuyến, và đảm bảo bạn đang sử dụng hằng số `QrCodeTypes` đúng cho định dạng đã chọn.

**Q: Dung lượng dữ liệu tối đa cho mỗi định dạng HIBC là bao nhiêu?**  
A: QR ≈ 4.296 ký tự alphanumeric, Aztec ≈ 3.832 số / 3.067 alphanumeric, Data Matrix ≈ 3.116 số / 2.335 alphanumeric. Giữ mã dưới 200 ký tự để độ tin cậy quét tối ưu.

**Q: Có thể nhúng nhiều loại mã vạch trong một PDF không?**  
A: Chắc chắn. Tạo các đối tượng `QrCodeSignOptions` riêng biệt với vị trí khác nhau và gọi `signature.sign()` cho mỗi cái. Chỉ cần đảm bảo chúng không chồng lên nhau.

**Q: Tôi có cần kết nối internet để ký khi chạy không?**  
A: Không. Sau khi JAR được đặt trong classpath và giấy phép được kích hoạt, mọi thao tác đều được thực hiện cục bộ.

## Tài nguyên bổ sung

- [GroupDocs.Signature for Java Documentation](https://docs.groupdocs.com/signature/java/)  
- [API Reference Guide](https://reference.groupdocs.com/signature/java/)  
- [Latest Release Downloads](https://releases.groupdocs.com/signature/java/)  
- [Purchase License](https://purchase.groupdocs.com/buy)  
- [Get Free Trial](https://releases.groupdocs.com/signature/java/)  
- [Request Temporary License](https://purchase.groupdocs.com/temporary-license/)  
- [GroupDocs Forum](https://forum.groupdocs.com/c/signature/)  

---

**Last Updated:** 2026-09-15  
**Tested With:** GroupDocs.Signature 23.12 for Java  
**Author:** GroupDocs  

## Các hướng dẫn liên quan

- [Create Barcode Signature PDF in Java – GroupDocs Guide](/signature/java/barcode-signatures/create-sign-pdfs-groupdocs-barcode-java/)
- [Create Barcode Signature in Java – Update PDF Barcodes](/signature/java/barcode-signatures/java-groupdocs-signature-barcode-initialize-update/)
- [How to read QR code PDF using Java and GroupDocs.Signature](/signature/java/barcode-signatures/java-pdf-barcode-search-groupdocs-signature-api/)

```java
signature.sign(destinFilePath, hibcLic_DM);
```

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}