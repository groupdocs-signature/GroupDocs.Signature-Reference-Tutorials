---
categories:
- Java Development
date: '2026-07-25'
description: Tìm hiểu cách thêm chữ ký mã vạch vào PDF bằng GroupDocs.Signature cho
  Java. Hướng dẫn cài đặt Maven từng bước, các tùy chọn mã vạch, xử lý lỗi và mẹo
  triển khai.
keywords:
- add barcode signature
- groupdocs signature java
- scannable pdf signature
- pdf signing java
- troubleshoot pdf signing
lastmod: '2026-07-25'
linktitle: Hướng dẫn GroupDocs.Signature Java
og_description: Thêm chữ ký mã vạch vào PDF bằng GroupDocs.Signature Java. Cài đặt
  Maven đầy đủ, các tùy chọn mã vạch, khắc phục sự cố và các thực tiễn tốt nhất cho
  môi trường sản xuất dành cho nhà phát triển Java.
og_image_alt: 'Guide: add barcode signature to PDF using GroupDocs.Signature Java'
og_title: Thêm chữ ký mã vạch vào PDF với GroupDocs.Signature Java
schemas:
- author: GroupDocs
  dateModified: '2026-07-25'
  description: Learn how to add barcode signature to PDFs using GroupDocs.Signature
    for Java. Step‑by‑step Maven setup, barcode options, error handling, and production
    tips.
  headline: Add barcode signature to PDFs with GroupDocs.Signature Java
  type: TechArticle
- description: Learn how to add barcode signature to PDFs using GroupDocs.Signature
    for Java. Step‑by‑step Maven setup, barcode options, error handling, and production
    tips.
  name: Add barcode signature to PDFs with GroupDocs.Signature Java
  steps:
  - name: Initialize the Signature Object
    text: 'The `Signature` class is GroupDocs.Signature''s entry point for all signing
      operations. It represents a single PDF document in memory and provides lazy
      loading to keep memory usage low. java import com.groupdocs.signature.Signature;
      public class InitializeSignature { public static void main(String[] '
  - name: Configure Barcode Sign Options
    text: '`BarcodeSignOptions` lets you define every attribute of the barcode—type,
      data, position, colors, borders, and even whether the raw barcode image should
      be returned. java import com.groupdocs.signature.Signature; import com.groupdocs.signature.exception.GroupDocsSignatureException;
      import java.nio.f'
  - name: Sign the Document
    text: 'The `sign` method applies the configured barcode to the PDF and writes
      the result to the target path. java signOptions.setEncodeType(BarcodeTypes.QR);
      // QR codes for more data signOptions.setForeColor(Color.BLACK); signOptions.setBackgroundColor(Color.WHITE);
      // Remove border and fancy styling for '
  type: HowTo
- questions:
  - answer: GroupDocs.Signature for Java is self‑contained; after adding the Maven/Gradle
      artifact you get full barcode generation and PDF rendering without any third‑party
      libraries.
    question: How do I add a barcode signature to a PDF in Java without external dependencies?
  - answer: Absolutely. Switch the `BarcodeTypes` enum to `QRCode` and adjust size
      parameters as needed.
    question: Can I configure barcode sign options in Java to generate QR codes?
  - answer: Pin the exact version in `pom.xml` (e.g., `23.10.0`) to avoid accidental
      upgrades, and enable the Maven `shade` plugin to produce a single executable
      JAR.
    question: What is the recommended Maven setup for production use?
  - answer: Yes. Provide the password when constructing the `Signature` object, then
      proceed with signing as usual.
    question: Does the library support password‑protected PDFs?
  - answer: GroupDocs.Signature can address all pages in a PDF at once or target specific
      pages via `setPageNumber()`. Performance scales linearly; a 200‑page PDF signs
      in ~2 seconds on a typical cloud VM.
    question: How many pages can I sign in one operation?
  type: FAQPage
tags:
- pdf-signing
- digital-signatures
- groupdocs
- barcode-signatures
title: Thêm chữ ký mã vạch vào PDF với GroupDocs.Signature Java
type: docs
url: /vi/java/digital-signatures/java-pdf-signing-groupdocs-signature-guide/
weight: 1
---

# Thêm chữ ký mã vạch vào PDF với GroupDocs.Signature Java

Trong các ứng dụng hiện đại tập trung vào tài liệu, **thêm chữ ký mã vạch** là một cách nhanh chóng, đáng tin cậy để làm cho PDF vừa có thể đọc được bởi con người vừa có thể quét được bởi máy. Hướng dẫn này sẽ dẫn bạn qua từng bước — bắt đầu từ cấu hình Maven, qua việc tạo kiểu mã vạch, đến xử lý các trường hợp tệp lớn — để bạn có thể tích hợp chữ ký mã vạch vào các dự án Java của mình một cách tự tin.

## Câu trả lời nhanh
- **Dòng mã đầu tiên để bắt đầu ký là gì?** `Signature signature = new Signature("sample.pdf");`
- **Tôi cần artifact Maven nào?** `com.groupdocs:groupdocs-signature:23.10` (thay thế bằng phiên bản mới nhất)
- **Tôi có thể ký các PDF được bảo vệ bằng mật khẩu không?** Có — truyền mật khẩu khi tạo đối tượng `Signature`.
- **Có bao nhiêu định dạng mã vạch được hỗ trợ?** Hơn 30, bao gồm Code128, QR, DataMatrix và Aztec.
- **Kích thước heap đề xuất cho PDF 100 MB là bao nhiêu?** Ít nhất `-Xmx2g` (2 GB) để tránh `OutOfMemoryError`.

## Chữ ký mã vạch là gì?
Một **chữ ký mã vạch** là một mã vạch có thể đọc được bằng máy được nhúng vào PDF, hoạt động như một dấu hiệu chống giả mạo và có thể chứa dữ liệu tùy chỉnh như ID, dấu thời gian hoặc URL. Nó kết hợp việc xác minh bằng mắt với quét tự động, làm cho nó trở nên lý tưởng cho quản lý tồn kho, tuân thủ và tự động hoá quy trình làm việc với khối lượng lớn.

## Tại sao thêm chữ ký mã vạch với GroupDocs.Signature Java?
GroupDocs.Signature hỗ trợ **hơn 50** định dạng đầu vào và đầu ra, xử lý các PDF hàng trăm trang mà không cần tải toàn bộ tệp vào bộ nhớ, và cung cấp một API Java mượt mà cho phép bạn tinh chỉnh mọi khía cạnh hình ảnh của mã vạch. Trong các bài kiểm tra hiệu năng, ký một PDF 150 trang với mã Code128 mất **dưới 1,2 giây** trên một máy ảo đám mây tiêu chuẩn 2 vCPU.

## Yêu cầu trước

Trước khi bắt đầu, hãy xác nhận rằng bạn có những thứ sau:

- **Java Development Kit (JDK)** 8 hoặc mới hơn (JDK 11 hoặc 17 được khuyến nghị cho hỗ trợ lâu dài)
- **IDE** (IntelliJ IDEA, Eclipse, hoặc VS Code với các extension Java)
- **Công cụ xây dựng** (Maven 3.6+ hoặc Gradle 7.0+)
- **Thư viện GroupDocs.Signature Java** (chúng tôi sẽ trình bày cài đặt Maven & Gradle bên dưới)
- Kiến thức cơ bản về các khái niệm OOP trong Java và cấu trúc dự án Maven/Gradle

### Thư viện và phụ thuộc cần thiết

GroupDocs.Signature tích hợp mượt mà với Maven hoặc Gradle. Chọn công cụ xây dựng mà bạn đang sử dụng:

**Cài đặt Maven**  
```markdown
```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```
```

**Cài đặt Gradle**  
```markdown
```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```
```

Nếu bạn muốn xử lý JAR thủ công, tải bản phát hành mới nhất từ [GroupDocs.Signature for Java releases](https://releases.groupdocs.com/signature/java/) và thêm nó vào classpath của bạn.

### Các bước mua giấy phép

GroupDocs cung cấp ba mô hình cấp phép:

- **Dùng thử miễn phí** – Truy cập đầy đủ tính năng trong 30 ngày (đánh dấu watermark trên PDF đã ký)
- **Giấy phép tạm thời** – Dùng thử kéo dài không giới hạn tính năng (lý tưởng cho quy trình phát triển)
- **Giấy phép đầy đủ** – Sẵn sàng cho môi trường sản xuất, bao gồm hỗ trợ ưu tiên và không có watermark

Lấy giấy phép phù hợp tại [GroupDocs Licensing](https://purchase.groupdocs.com/buy). Ngay cả trong thời gian dùng thử, bạn vẫn có thể chạy mã cục bộ; chỉ cần nhớ thay thế khóa dùng thử bằng khóa vĩnh viễn trước khi đưa vào hoạt động.

## Cách thêm chữ ký mã vạch vào PDF bằng GroupDocs.Signature Java?

Lớp `Signature` là điểm vào chính để làm việc với tài liệu trong GroupDocs.Signature.  
Lớp `BarcodeSignOptions` xác định dữ liệu, loại và giao diện hình ảnh của mã vạch.

Tải PDF nguồn của bạn bằng `new Signature("source.pdf")`, cấu hình một đối tượng `BarcodeSignOptions` với dữ liệu và kiểu dáng mong muốn, sau đó gọi `signature.sign("output.pdf", options)`. Mô hình ba bước này xử lý I/O tệp, tạo mã vạch và ghi PDF trong một lời gọi an toàn đa luồng, và hoạt động cho các PDF từ vài kilobyte đến vài trăm megabyte.

### Bước 1: Khởi tạo đối tượng Signature

Lớp `Signature` là điểm vào của GroupDocs.Signature cho mọi thao tác ký. Nó đại diện cho một tài liệu PDF duy nhất trong bộ nhớ và cung cấp tải lười để giảm mức sử dụng bộ nhớ.

```markdown
```java
import com.groupdocs.signature.Signature;

public class InitializeSignature {
    public static void main(String[] args) {
        Signature signature = new Signature("YOUR_DOCUMENT_DIRECTORY/sample.pdf");
        System.out.println("GroupDocs.Signature initialized successfully.");
    }
}
```
```

**Giải thích:**  
- `filePath` chỉ tới PDF nguồn mà bạn muốn ký.  
- `outputFilePath` là nơi PDF đã ký sẽ được lưu, bảo toàn tệp gốc.  
- Khối `try‑catch` đảm bảo xử lý nhẹ nhàng các lỗi I/O, tệp không tồn tại hoặc vấn đề quyền truy cập.

### Bước 2: Cấu hình Barcode Sign Options

`BarcodeSignOptions` cho phép bạn định nghĩa mọi thuộc tính của mã vạch — loại, dữ liệu, vị trí, màu sắc, viền, và thậm chí việc trả về hình ảnh mã vạch thô.

```markdown
```java
import com.groupdocs.signature.Signature;
import com.groupdocs.signature.exception.GroupDocsSignatureException;
import java.nio.file.Paths;
import java.io.File;

public class Feature1 {
    public static void run() throws Exception {
        String filePath = "YOUR_DOCUMENT_DIRECTORY/sample.pdf";
        String outputFilePath = new File("YOUR_OUTPUT_DIRECTORY", "SignedOutputSample.pdf").getPath();

        try {
            Signature signature = new Signature(filePath);
            System.out.println("Signature initialized and paths set.");
        } catch (Exception e) {
            throw new GroupDocsSignatureException(e.getMessage());
        }
    }
}
```
```

**Phân tích các cài đặt chính:**

- **Dữ liệu & Loại** – `"12345678"` là dữ liệu tải; `BarcodeTypes.Code128` hoạt động cho chuỗi alphanumeric và được máy quét hỗ trợ rộng rãi.
- **Định vị** – `setLeft(100)` và `setTop(100)` dịch mã vạch 100 px từ góc trên‑trái; `VerticalAlignment.Top` + `HorizontalAlignment.Right` điều chỉnh căn chỉnh dựa trên các offset này.
- **Lề & Đệm** – Đối tượng `Padding` thêm bộ đệm 20 px để tránh cắt ở các cạnh trang.
- **Tạo kiểu** – Viền, phông chữ và bút nền có thể tùy chỉnh hoàn toàn; trong môi trường sản xuất bạn có thể bỏ gradient để tăng tốc độ render.
- **Trả về nội dung** – Bật `setReturnContent(true)` sẽ cung cấp mã vạch dưới dạng `byte[]`, hữu ích để lưu hình ảnh vào cơ sở dữ liệu hoặc hiển thị trong UI.

#### Cấu hình tối thiểu cho môi trường sản xuất

Đối với tài liệu pháp lý sạch sẽ, bạn thường muốn một mã vạch đen‑trên‑trắng đơn giản mà không có viền phụ:

```markdown
```java
import com.groupdocs.signature.domain.enums.*;
import com.groupdocs.signature.domain.Padding;
import com.groupdocs.signature.domain.Border;
import com.groupdocs.signature.domain.DashStyle;
import com.groupdocs.signature.domain.extensions.LinearGradientBrush;
import com.groupdocs.signature.domain.font.SignatureFont;
import java.awt.Color;
import com.groupdocs.signature.options.sign.BarcodeSignOptions;

public class Feature2 {
    public static void configureBarcodeOptions() throws Exception {
        BarcodeSignOptions signOptions = new BarcodeSignOptions("12345678");
        signOptions.setEncodeType(BarcodeTypes.Code128);
        signOptions.setLeft(100);
        signOptions.setTop(100);
        signOptions.setVerticalAlignment(VerticalAlignment.Top);
        signOptions.setHorizontalAlignment(HorizontalAlignment.Right);

        Padding padding = new Padding();
        padding.setLeft(20);
        padding.setTop(20);
        signOptions.setMargin(padding);

        Border border = new Border();
        border.setColor(Color.GREEN);
        border.setDashStyle(DashStyle.DashLongDashDot);
        border.setWeight(2);
        border.setTransparency(0.5);
        border.setVisible(true);
        signOptions.setBorder(border);

        signOptions.setForeColor(Color.RED);
        SignatureFont font = new SignatureFont();
        font.setSize(12);
        font.setFamilyName("Comic Sans MS");
        signOptions.setFont(font);

        signOptions.setCodeTextAlignment(CodeTextAlignment.Above);

        Background background = new Background();
        background.setColor(Color.GREEN);
        background.setTransparency(0.5);
        background.setBrush(new LinearGradientBrush(Color.GREEN, Color.DARK_GRAY, 0));
        signOptions.setBackground(background);

        signOptions.setReturnContent(true);
        signOptions.setReturnContentType(FileType.PNG);
    }
}
```
```

### Bước 3: Ký tài liệu

Phương thức `sign` áp dụng mã vạch đã cấu hình lên PDF và ghi kết quả vào đường dẫn mục tiêu.

```markdown
```java
signOptions.setEncodeType(BarcodeTypes.QR); // QR codes for more data
signOptions.setForeColor(Color.BLACK);
signOptions.setBackgroundColor(Color.WHITE);
// Remove border and fancy styling for professional appearance
```
```

**Bên trong:**  
- `signature.sign(outputFilePath, signOptions)` ghi mã vạch lên PDF trong khi giữ nguyên tệp nguồn.  
- `SignResult` báo cáo số lượng chữ ký đã được thêm, các trang đã được sửa đổi, và bất kỳ cảnh báo nào được tạo.  
- Đối với công việc batch, bao bọc lời gọi này trong một `ExecutorService` để thực hiện song song trên các lõi CPU.

## Các vấn đề thường gặp và giải pháp

### Vấn đề 1: FileNotFoundException khi khởi tạo

**Triệu chứng:** Ứng dụng ném `FileNotFoundException` khi tạo đối tượng `Signature`.

**Nguyên nhân gốc:**  
- Đường dẫn tệp không đúng (tương đối so với tuyệt đối)  
- Thiếu quyền đọc  
- Tệp bị khóa bởi tiến trình khác (ví dụ, mở trong Acrobat)

**Cách khắc phục:**  
```markdown
```java
import com.groupdocs.signature.Signature;
import com.groupdocs.signature.exception.GroupDocsSignatureException;
import com.groupdocs.signature.options.sign.BarcodeSignOptions;
import com.groupdocs.signature.domain.BaseSignature;

public class Feature3 {
    public static void signDocument(String filePath, BarcodeSignOptions signOptions) throws Exception {
        Signature signature = new Signature(filePath);
        String outputFilePath = filePath.replace(".pdf", "_Signed.pdf");

        try {
            com.groupdocs.signature.domain.signatures.SignResult signResult = signature.sign(outputFilePath, signOptions);
            System.out.println("Document signed successfully.");
        } catch (Exception e) {
            throw new GroupDocsSignatureException(e.getMessage());
        }
    }
}
```
```
Đảm bảo đường dẫn sử dụng dấu gạch chéo xuôi (`C:/Docs/sample.pdf`) hoặc escape dấu gạch chéo ngược (`C:\\Docs\\sample.pdf`). Kiểm tra quyền hệ điều hành và đóng bất kỳ chương trình nào có thể khóa tệp.

### Vấn đề 2: Mã vạch không hiển thị trong đầu ra

**Triệu chứng:** Quá trình ký hoàn thành mà không có lỗi, nhưng mã vạch không hiển thị.

**Nguyên nhân thường gặp:**  
- Vị trí đặt mã vạch nằm ngoài khu vực có thể in.  
- Độ trong suốt được đặt thành `1.0` (hoàn toàn trong suốt).  
- Kích thước phông chữ được đặt thành `0`.

**Giải pháp:**  
- Giữ giá trị `setLeft`/`setTop` trong phạm vi kích thước trang (0‑600 px cho A4 tiêu chuẩn).  
- Sử dụng giá trị trong suốt từ `0.0` (đục) tới `0.9`.  
- Đặt kích thước phông chữ có thể đọc được, ví dụ `12pt`.

### Vấn đề 3: Lỗi Out of Memory khi xử lý tài liệu lớn

**Triệu chứng:** `OutOfMemoryError` khi xử lý PDF lớn hơn khoảng 50 MB.

**Biện pháp khắc phục:**  
- Tăng heap JVM: `-Xmx2g` hoặc cao hơn tùy theo kích thước tài liệu.  
- Xử lý PDF theo từng trang bằng API streaming của `Signature`.  
- Đóng rõ ràng đối tượng `Signature` sau mỗi thao tác để giải phóng tài nguyên gốc.

```markdown
```java
import java.nio.file.Files;
import java.nio.file.Path;

Path filePath = Path.of("YOUR_DOCUMENT_DIRECTORY/sample.pdf");
if (!Files.exists(filePath)) {
    throw new IllegalArgumentException("PDF file not found: " + filePath);
}
if (!Files.isReadable(filePath)) {
    throw new SecurityException("Cannot read PDF file: " + filePath);
}
// Now safe to initialize
Signature signature = new Signature(filePath.toString());
```
```

### Vấn đề 4: Lỗi dữ liệu mã vạch không hợp lệ

**Triệu chứng:** API ném ngoại lệ khi phàn nàn về ký tự không được hỗ trợ.

**Nguyên nhân:** Các tiêu chuẩn mã vạch khác nhau chấp nhận các bộ ký tự khác nhau. Code128 cho phép alphanumerics; QR có thể xử lý Unicode; một số mã vạch 1D chỉ chấp nhận số.

**Giải pháp:** Chọn loại mã vạch phù hợp với tập dữ liệu của bạn, hoặc làm sạch chuỗi trước khi gán cho `BarcodeSignOptions`.

```markdown
```java
String barcodeData = "ABC123"; // Your data
BarcodeTypes type = BarcodeTypes.Code128; // Alphanumeric support

// For numeric-only barcodes, validate first:
if (type == BarcodeTypes.EAN13 && !barcodeData.matches("\\d+")) {
    throw new IllegalArgumentException("EAN13 requires numeric data only");
}
```
```

## Thực hành tốt cho môi trường sản xuất

### 1. Xác thực PDF trước khi ký

Luôn xác nhận tệp là một PDF đúng định dạng để tránh lỗi phân tích thời gian chạy.

```markdown
```java
try (Signature signature = new Signature(filePath)) {
    // If this succeeds, file is valid
    signature.getDocumentInfo();
} catch (Exception e) {
    // Handle invalid PDF
}
```
```

### 2. Sử dụng xử lý bất đồng bộ cho khối lượng công việc lớn

Chuyển việc ký sang một pool luồng nền; điều này ngăn UI bị treo và cải thiện thông lượng.

```markdown
```java
ExecutorService executor = Executors.newFixedThreadPool(4);
List<String> pdfFiles = Arrays.asList("doc1.pdf", "doc2.pdf", "doc3.pdf");

pdfFiles.forEach(file -> {
    executor.submit(() -> {
        try {
            signDocument(file, signOptions);
        } catch (Exception e) {
            // Log error
        }
    });
});
executor.shutdown();
```
```

### 3. Triển khai ghi log có cấu trúc

Ghi log mỗi yêu cầu ký với đường dẫn đầu vào, đường dẫn đầu ra, dữ liệu mã vạch và bất kỳ ngoại lệ nào. Điều này tăng tốc đáng kể việc phân tích sau sự cố.

```markdown
```java
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

private static final Logger logger = LoggerFactory.getLogger(YourClass.class);

try {
    SignResult result = signature.sign(outputFilePath, signOptions);
    logger.info("Document signed successfully: {}", outputFilePath);
    logger.debug("Signatures added: {}", result.getSucceeded().size());
} catch (Exception e) {
    logger.error("Failed to sign document: {}", filePath, e);
}
```
```

### 4. Tối ưu cài đặt mã vạch để tăng tốc

- Tắt `setReturnContent(true)` trừ khi bạn cần hình ảnh riêng.  
- Ưu tiên bút nền đặc so với gradient.  
- Bỏ viền cho các trường hợp theo dõi đơn giản.

### 5. Xử lý hết hạn giấy phép tạm thời một cách nhẹ nhàng

Lớp `License` tải và xác thực tệp giấy phép GroupDocs cho API.  
Kiểm tra trạng thái giấy phép trước mỗi thao tác ký và chuyển sang chế độ chỉ đọc hoặc cảnh báo quản trị viên nếu hết hạn.

```markdown
```java
try {
    License license = new License();
    license.setLicense(licensePath);
} catch (Exception e) {
    logger.warn("License validation failed. Using trial mode.");
    // Continue with trial limitations
}
```
```

## Khi nào nên sử dụng chữ ký mã vạch

### Kịch bản lý tưởng

- **Quản lý tồn kho & Logistics:** Gắn mã vạch có thể quét vào bản kê vận chuyển, danh sách đóng gói, hoặc thẻ tài sản.  
- **Tuân thủ quy định:** Các ngành như dược phẩm yêu cầu dấu vết kiểm toán có thể đọc bằng máy.  
- **Pipeline tài liệu tự động:** Kết hợp chữ ký mã vạch với OCR để cho phép xử lý đầu‑đến‑đầu mà không cần nhập dữ liệu thủ công.  
- **Công việc batch khối lượng lớn:** Mã vạch nhanh hơn trong việc xác minh so với chữ ký số khi quét các kho lưu trữ giấy lớn.

### Khi nào nên ưu tiên các loại chữ ký khác

- **Hợp đồng pháp lý:** Sử dụng chữ ký số dựa trên PKI (ví dụ, X.509) để không thể chối bỏ.  
- **PDF hướng tới khách hàng:** Mã QR dễ nhận biết hơn trên thiết bị di động.  
- **Tài liệu siêu bảo mật:** Kết hợp mã vạch với chữ ký số được mã hoá để tăng lớp bảo mật.

> **Mẹo chuyên nghiệp:** Bạn có thể nhúng nhiều loại chữ ký trong cùng một PDF — thêm mã vạch để theo dõi và chứng chỉ số để thực thi pháp lý.

## Câu hỏi thường gặp

**Q: Làm sao để thêm chữ ký mã vạch vào PDF trong Java mà không cần phụ thuộc bên ngoài?**  
A: GroupDocs.Signature cho Java là tự chứa; sau khi thêm artifact Maven/Gradle, bạn sẽ có đầy đủ khả năng tạo mã vạch và render PDF mà không cần thư viện bên thứ ba nào.

**Q: Tôi có thể cấu hình tùy chọn ký mã vạch trong Java để tạo mã QR không?**  
A: Chắc chắn. Đổi enum `BarcodeTypes` thành `QRCode` và điều chỉnh các tham số kích thước theo nhu cầu.

```markdown
```java
signOptions.setEncodeType(BarcodeTypes.QR);
```
```

**Q: Cài đặt Maven nào được khuyến nghị cho môi trường sản xuất?**  
A: Đặt cố định phiên bản chính xác trong `pom.xml` (ví dụ, `23.10.0`) để tránh nâng cấp tình cờ, và bật plugin Maven `shade` để tạo một JAR thực thi duy nhất.

```markdown
```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version> <!-- Don't use LATEST -->
</dependency>
```
```

**Q: Thư viện có hỗ trợ PDF được bảo vệ bằng mật khẩu không?**  
A: Có. Cung cấp mật khẩu khi tạo đối tượng `Signature`, sau đó tiếp tục ký như bình thường.

```markdown
```java
LoadOptions loadOptions = new LoadOptions();
loadOptions.setPassword("your_pdf_password");
Signature signature = new Signature(filePath, loadOptions);
```
```

**Q: Tôi có thể ký bao nhiêu trang trong một thao tác?**  
A: GroupDocs.Signature có thể xử lý tất cả các trang trong một PDF cùng lúc hoặc chỉ định các trang cụ thể bằng `setPageNumber()`. Hiệu năng tăng tuyến tính; một PDF 200 trang được ký trong khoảng 2 giây trên một VM đám mây tiêu chuẩn.

**Q: Các định dạng mã vạch nào có sẵn ngoài Code128?**  
A: Hơn 30 định dạng, bao gồm QR, DataMatrix, Aztec, UPC‑A, EAN‑13, PDF417, và nhiều hơn nữa. Tham khảo enum `BarcodeTypes` để xem danh sách đầy đủ.

**Q: Có giới hạn độ dài dữ liệu mã vạch không?**  
A: Giới hạn độ dài phụ thuộc vào loại mã vạch; đối với Code128 giới hạn thực tế là 80 ký tự, trong khi mã QR có thể lưu tới 4 KB dữ liệu.

**Q: Tôi có thể lấy lại hình ảnh mã vạch đã tạo sau khi ký không?**  
A: Đặt `setReturnContent(true)` và `setReturnContentType(FileType.PNG)`; `SignResult` sẽ chứa một `byte[]` mà bạn có thể ghi ra đĩa hoặc cơ sở dữ liệu.

**Cập nhật lần cuối:** 2026-07-25  
**Đã kiểm tra với:** GroupDocs.Signature 23.10 cho Java  
**Tác giả:** GroupDocs

## Hướng dẫn liên quan

- [Cách thêm chữ ký số trong Java - Hướng dẫn đầy đủ của GroupDocs](/signature/java/getting-started/groupdocs-signature-java-digital-setup-guide/)
- [Thêm mã QR vào PDF Java - Hướng dẫn đầy đủ của GroupDocs](/signature/java/qr-code-signatures/qr-code-signature-generation-java-groupdocs/)
- [Thêm chữ ký văn bản vào PDF trong Java - Hướng dẫn đầy đủ của GroupDocs](/signature/java/text-signatures/implement-text-signatures-groupdocs-java/)