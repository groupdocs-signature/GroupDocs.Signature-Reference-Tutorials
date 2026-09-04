---
categories:
- Java Development
date: '2026-05-21'
description: Tìm hiểu cách triển khai digital signature java bằng cách sử dụng barcodes
  và QR codes. Hướng dẫn chi tiết từng bước với GroupDocs.Signature để bảo mật TAR
  archives và các tài liệu khác.
keywords:
- digital signature java
- how to sign java
- java document signing
- java file integrity check
- add barcode to file
lastmod: '2026-05-21'
linktitle: Hướng dẫn Java Digital Signature
schemas:
- author: GroupDocs
  dateModified: '2026-05-21'
  description: Learn how to implement digital signature java using barcodes and QR
    codes. Step‑by‑step guide with GroupDocs.Signature for securing TAR archives and
    other documents.
  headline: 'Digital Signature Java: Sign Files with Barcodes & QR Codes'
  type: TechArticle
- description: Learn how to implement digital signature java using barcodes and QR
    codes. Step‑by‑step guide with GroupDocs.Signature for securing TAR archives and
    other documents.
  name: 'Digital Signature Java: Sign Files with Barcodes & QR Codes'
  steps:
  - name: Test new versions in staging.
    text: Test new versions in staging.
  - name: Review breaking changes.
    text: Review breaking changes.
  - name: Benchmark with real files.
    text: Benchmark with real files.
  - name: Roll out incrementally.
    text: Roll out incrementally.
  - name: Explore signature verification with the `search()` method.
    text: Explore signature verification with the `search()` method.
  - name: Try other document formats—GroupDocs.Signature supports PDF, DOCX, XLSX,
      PNG, and more.
    text: Try other document formats—GroupDocs.Signature supports PDF, DOCX, XLSX,
      PNG, and more.
  - name: customise signature appearance (colors, sizes, borders).
    text: customise signature appearance (colors, sizes, borders).
  - name: Build a verification API to validate signatures programmatically.
    text: Build a verification API to validate signatures programmatically.
  type: HowTo
- questions:
  - answer: Absolutely! GroupDocs.Signature supports over 50 file formats, including
      PDF, DOCX, XLSX, PNG, and more. Change only the file extension in the `Signature`
      constructor to work with any supported type.
    question: Can I sign documents other than TAR archives?
  - answer: 'Use the `search()` method to locate and validate signatures: ```java
      Signature signature = new Signature("signed-document.tar"); BarcodeSearchOptions
      searchOptions = new BarcodeSearchOptions(); List<BarcodeSignature> signatures
      = signature.search(BarcodeSignature.class, searchOptions); ```'
    question: How do I verify signatures after signing?
  - answer: Barcode and QR code signatures provide visual verification but are not
      cryptographically strong like digital certificates. For maximum security, combine
      them with traditional PKI or store signature hashes in an external database.
    question: Are the signatures secure against tampering?
  - answer: 'Yes! Control colours, sizes, borders, and more: ```java bcOptions.setForeColor(Color.BLUE);
      bcOptions.setBackgroundColor(Color.YELLOW); bcOptions.setBorder(new Border());
      bcOptions.getBorder().setColor(Color.RED); bcOptions.getBorder().setWeight(2);
      ```'
    question: Can I customise the signature appearance?
  - answer: Each `sign()` call adds a new signature. To replace an existing one, delete
      it first with the `delete()` method.
    question: What happens if I sign a file twice?
  type: FAQPage
tags:
- digital-signature
- document-security
- java-tutorial
- groupdocs
title: 'Digital Signature Java: Ký tệp với Barcodes & QR Codes'
type: docs
url: /vi/java/barcode-signatures/sign-tar-archives-barcode-qr-code-java/
weight: 1
---

# Cách Thêm Chữ Ký Số Vào Tệp Trong Java Sử Dụng Mã Vạch và Mã QR

## Giới thiệu

Bạn đã bao giờ tự hỏi làm thế nào để chứng minh các tệp của mình không bị thay đổi bằng cách sử dụng **digital signature java**? Hoặc cần một cách để xác thực tài liệu một cách lập trình mà không cần cài đặt mật mã phức tạp? Các chữ ký số truyền thống có thể quá mức đối với một số trường hợp. Đôi khi bạn chỉ cần một phương pháp nhẹ, có thể quét để xác minh tính toàn vẹn của tệp—đặc biệt khi làm việc với các kho lưu trữ, bản sao lưu hoặc quy trình tự động. Đó là lúc các chữ ký bằng mã vạch và mã QR xuất hiện.

Trong hướng dẫn này, bạn sẽ học cách triển khai chữ ký số trong Java bằng GroupDocs.Signature. Chúng tôi sẽ tập trung vào việc ký các tệp TAR (lý tưởng cho hệ thống sao lưu và phân phối phần mềm), nhưng các kỹ thuật này cũng hoạt động với nhiều định dạng tài liệu khác. Dù bạn đang xây dựng hệ thống quản lý tài liệu hay chỉ muốn thêm một lớp bảo mật cho các tệp, bạn đã đến đúng nơi.

**Bạn sẽ nhận được:**
- Một triển khai hoạt động của chữ ký mã vạch và mã QR trong Java  
- Hiểu khi nào nên sử dụng mỗi loại chữ ký (và lý do)  
- Các giải pháp thực tế cho các thách thức ký thường gặp  
- Các mẫu tích hợp thực tế mà bạn có thể dùng ngay hôm nay  
- Mẹo tối ưu hiệu năng cho hệ thống sản xuất  

Hãy bắt đầu—không cần bằng cấp về mật mã.

## Câu trả lời nhanh
- **Thư viện nào xử lý chữ ký mã vạch trong Java?** GroupDocs.Signature for Java.  
- **Loại chữ ký nào lưu trữ dữ liệu nhiều hơn?** Mã QR (tối đa 4.296 ký tự chữ và số).  
- **Tôi có thể ký các tệp TAR lớn (>100 MB)?** Có—sử dụng luồng nền và tăng heap JVM.  
- **Có cần kết nối internet không?** Không, thư viện hoạt động hoàn toàn offline.  
- **Có cần giấy phép cho môi trường production không?** Có, giấy phép GroupDocs.Signature hợp lệ là bắt buộc.

## Chữ ký số Java là gì?

**digital signature java** là quá trình nhúng một token hình ảnh có thể xác minh—như mã vạch hoặc mã QR—trực tiếp vào tệp được tạo bằng Java để chứng minh tính xác thực và toàn vẹn của nó. Bằng cách gắn token này, các nhà phát triển có thể cung cấp một cách nhanh chóng, có thể đọc được bằng mắt người để xác nhận tệp không bị thay đổi kể từ khi ký, đồng thời vẫn cho phép xác minh bằng chương trình thông qua API GroupDocs.Signature.

## Tại sao nên sử dụng chữ ký bằng mã vạch hoặc mã QR?

GroupDocs.Signature hỗ trợ **50+ định dạng đầu vào và đầu ra** (bao gồm PDF, DOCX, XLSX, HTML, PNG và TAR) và có thể xử lý các tài liệu hàng trăm trang mà không cần tải toàn bộ tệp vào bộ nhớ. Mã vạch và mã QR cung cấp bằng chứng xác thực có thể quét, tự chứa, loại bỏ nhu cầu sử dụng các cơ quan chứng thực bên ngoài trong nhiều quy trình nội bộ.

## Yêu cầu trước

- **Thư viện GroupDocs.Signature for Java** – phiên bản 23.12 trở lên  
- **Java Development Kit (JDK)** – phiên bản 8 hoặc cao hơn  
- **IDE** – IntelliJ IDEA, Eclipse, hoặc bất kỳ trình soạn thảo Java nào tương thích  
- **Kiến thức Java cơ bản** – bạn nên quen thuộc với lớp và import  

### Cài đặt môi trường

Đưa GroupDocs.Signature vào dự án của bạn rất đơn giản. Chọn công cụ xây dựng bạn đang dùng:

**Maven** (thêm vào `pom.xml` của bạn):
```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

**Gradle** (thêm vào `build.gradle`):
```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

**Tải thủ công**: Không dùng Maven hay Gradle? Tải JAR trực tiếp từ [GroupDocs.Signature releases](https://releases.groupdocs.com/signature/java/) và thêm vào classpath.

### Mua giấy phép

GroupDocs cung cấp các gói giấy phép linh hoạt:

- **Dùng thử miễn phí**: Lý tưởng để thử nghiệm—không cần thẻ tín dụng. [Bắt đầu tại đây](https://releases.groupdocs.com/signature/java/)  
- **Giấy phép tạm thời**: Cần thêm thời gian để đánh giá? [Yêu cầu giấy phép tạm thời](https://purchase.groupdocs.com/temporary-license/) để truy cập đầy đủ tính năng trong quá trình phát triển  
- **Giấy phép production**: Khi bạn sẵn sàng triển khai, [mua giấy phép](https://purchase.groupdocs.com/buy) phù hợp với nhu cầu  

**Các liên kết hữu ích khác**

- [Tài liệu GroupDocs.Signature for Java](https://docs.groupdocs.com/signature/java/)  
- [Hướng dẫn tham chiếu API](https://reference.groupdocs.com/signature/java/)  
- [Diễn đàn hỗ trợ cộng đồng](https://forum.groupdocs.com/c/signature/)  
- [Bản phát hành mới nhất](https://releases.groupdocs.com/signature/java/)  
- [Tải bản dùng thử miễn phí](https://releases.groupdocs.com/signature/java/)  
- [Yêu cầu giấy phép tạm thời](https://purchase.groupdocs.com/temporary-license/)  
- [Mua giấy phép đầy đủ](https://purchase.groupdocs.com/buy)

Mẹo: Bắt đầu với bản dùng thử miễn phí để tạo mẫu giải pháp, sau đó lấy giấy phép tạm thời nếu cần thời gian thêm trước khi cam kết.

## Cài đặt GroupDocs.Signature cho Java

Lớp `Signature` là điểm vào cho mọi thao tác ký trong GroupDocs.Signature. Nó đại diện cho một tệp duy nhất được tải vào bộ nhớ và cung cấp các phương thức để thêm, tìm kiếm hoặc xóa chữ ký hình ảnh.

Tạo một thể hiện `Signature` trỏ tới tệp TAR của bạn. Điều này sẽ tải tệp vào bộ nhớ để xử lý:
```java
import com.groupdocs.signature.Signature;

public class InitializeSignature {
    public static void main(String[] args) {
        Signature signature = new Signature("your-document-path");
        // Additional setup and usage here...
    }
}
```

**Quan trọng**: Luôn đóng đối tượng `Signature` khi hoàn tất (hoặc sử dụng try‑with‑resources) để tránh rò rỉ bộ nhớ với các tệp lớn.

## Lựa chọn giữa chữ ký mã vạch và mã QR

Không chắc nên dùng loại chữ ký nào? Dưới đây là bảng quyết định nhanh:

| Yếu tố | Mã vạch (Code128) | Mã QR |
|--------|-------------------|-------|
| **Dung lượng dữ liệu** | ~80 ký tự | Lên tới 4.296 ký tự chữ và số |
| **Khả năng đọc** | Cần máy quét mã vạch | Hoạt động với camera smartphone |
| **Tiết kiệm không gian** | Hẹp hơn theo chiều ngang | Yêu cầu khu vực hình vuông |
| **Thích hợp cho** | ID đơn giản, dấu thời gian, mã ngắn | URL, dữ liệu JSON, siêu dữ liệu chi tiết |
| **Sửa lỗi** | Tối thiểu | Tích hợp (có thể khôi phục khi hỏng) |

**Quy tắc chung**:  
- Dùng **mã vạch** cho các ID nhanh, có thể quét hoặc dấu thời gian.  
- Dùng **mã QR** khi cần nhúng dữ liệu phong phú hơn hoặc muốn tương thích smartphone.  
- Kết hợp cả hai để đạt độ dư thừa và khả năng kiểm toán tối đa.

## Hướng dẫn triển khai

### Ký tệp TAR bằng mã vạch

#### Tại sao ký bằng mã vạch?
Mã vạch rất phù hợp cho các tệp TAR vì chúng gọn gàng và có thể quét. Bạn có thể nhúng dấu thời gian, số phiên bản, ID người dùng hoặc giá trị checksum để kiểm tra nhanh.

#### Các bước

**1. Initialise Signature**  
Đầu tiên, tạo một thể hiện `Signature` cho tệp TAR:
```java
import com.groupdocs.signature.Signature;

final Signature signature = new Signature("path/to/your/archive.tar");
```

**Mẹo**: Đối với các tệp TAR lớn (hơn 100 MB), chạy thao tác ký trong luồng nền để UI không bị treo.

**2. Configure Barcode Options**  
Lớp `BarcodeSignature` định nghĩa nội dung, loại và vị trí của mã vạch. Đối tượng `BarcodeOptions` chứa các cài đặt này:
```java
import com.groupdocs.signature.options.sign.BarcodeSignOptions;
import com.groupdocs.signature.domain.barcodes.BarcodeTypes;

BarcodeSignOptions bcOptions = new BarcodeSignOptions("12345678", BarcodeTypes.Code128);
bcOptions.setLeft(100);  // X position in pixels
bcOptions.setTop(100);   // Y position in pixels
```

`BarcodeOptions` cho phép bạn chỉ định giao diện và vị trí của mã vạch.  
`BarcodeTypes` là enum liệt kê các loại mã vạch được hỗ trợ như `Code128`, `Code39`, v.v.

**Điều gì đang xảy ra?**  
- `"12345678"` là dữ liệu được mã hoá trong mã vạch—thay bằng ID, dấu thời gian hoặc mã xác thực thực tế của bạn.  
- `BarcodeTypes.Code128` cân bằng giữa dung lượng dữ liệu và độ tin cậy khi quét.  
- Các giá trị vị trí (100, 100) đặt mã vạch cách góc trên‑trái 100 px.

**Các tùy chọn tùy chỉnh bạn có thể muốn:**  
```java
bcOptions.setWidth(200);        // Barcode width in pixels
bcOptions.setHeight(50);        // Barcode height in pixels
bcOptions.setForeColor(Color.BLACK);  // Barcode color
bcOptions.setBackgroundColor(Color.WHITE);  // Background color
```

**3. Sign and Save the Document**  
Thực hiện thao tác ký và lưu lại tệp đã ký:
```java
import com.groupdocs.signature.domain.SignResult;

String outputFilePath = "output/path/SignWithBarcode/archive_signed.tar";
SignResult signResult = signature.sign(outputFilePath, bcOptions);
```

Đối tượng `SignResult` trả về cho biết thao tác có thành công và chữ ký được đặt ở đâu.  
**Lỗi thường gặp**: Đảm bảo thư mục đầu ra tồn tại trước khi gọi `sign()`. Thư viện sẽ không tự tạo thư mục cha.

### Ký tệp TAR bằng mã QR

#### Khi nào nên sử dụng mã QR
Mã QR tỏa sáng khi bạn cần lưu trữ dữ liệu có cấu trúc (JSON, XML), nhúng URL xác thực, hoặc cho phép quét bằng smartphone.

#### Các bước

**1. Initialise Signature**  
Giống như trước—tạo thể hiện `Signature` của bạn:
```java
final Signature signature = new Signature("path/to/your/archive.tar");
```

**2. Configure QR Code Options**  
Cài đặt mã QR với dữ liệu bạn muốn nhúng:
```java
import com.groupdocs.signature.options.sign.QrCodeSignOptions;
import com.groupdocs.signature.domain.qrcodes.QrCodeTypes;

QrCodeSignOptions qrOptions = new QrCodeSignOptions("12345678", QrCodeTypes.QR);
qrOptions.setLeft(400);  // X position
qrOptions.setTop(400);   // Y position
```

`QrCodeTypes` là enum chỉ định loại mã QR sẽ tạo (QR chuẩn, DataMatrix, Aztec, v.v.).  

**Ví dụ thực tế** – nhúng payload JSON với dữ liệu xác thực:
```java
String verificationData = "{\"version\":\"1.0\",\"timestamp\":\"2025-01-02T10:30:00Z\",\"user\":\"john.doe\"}";
QrCodeSignOptions qrOptions = new QrCodeSignOptions(verificationData, QrCodeTypes.QR);
```

**Các tùy chọn loại mã QR:**  
- `QrCodeTypes.QR` – mã QR chuẩn (phổ biến nhất)  
- `QrCodeTypes.DataMatrix` – gọn hơn cho dữ liệu nhỏ  
- `QrCodeTypes.Aztec` – tốt cho bề mặt cong  

**3. Sign and Save the Document**  
Hoàn tất quá trình ký giống như với mã vạch:
```java
String outputFilePath = "output/path/SignWithQRCode/archive_signed.tar";
SignResult signResult = signature.sign(outputFilePath, qrOptions);
```

**Lưu ý về hiệu năng**: Tạo mã QR hơi chậm hơn mã vạch do tính toán sửa lỗi, nhưng chênh lệch là không đáng kể cho hầu hết các trường hợp (thường chỉ vài mili giây).

### Ký tệp TAR bằng nhiều chữ ký

#### Tại sao nên dùng nhiều chữ ký?
- **Dư thừa** – nếu một chữ ký bị hỏng, chữ ký còn lại vẫn có thể xác minh.  
- **Đối tượng khác nhau** – mã vạch cho máy quét, mã QR cho smartphone.  
- **Dữ liệu lớp** – ID nhanh trong mã vạch, siêu dữ liệu chi tiết trong mã QR.  
- **Tuân thủ** – một số quy định yêu cầu nhiều phương pháp xác thực.

#### Các bước

**1. Initialise Signature**  
Cũng giống như trước:
```java
final Signature signature = new Signature("path/to/your/archive.tar");
```

**2. Configure Multiple Options**  
Tạo cả hai loại chữ ký và ghép chúng vào một danh sách:
```java
import java.util.ArrayList;
import java.util.List;

// Set up barcode (reusing from earlier example)
BarcodeSignOptions bcOptions = new BarcodeSignOptions("12345678", BarcodeTypes.Code128);
bcOptions.setLeft(100);
bcOptions.setTop(100);

// Set up QR code (different position to avoid overlap)
QrCodeSignOptions qrOptions = new QrCodeSignOptions("12345678", QrCodeTypes.QR);
qrOptions.setLeft(400);
qrOptions.setTop(400);

// Combine them
List<com.groupdocs.signature.options.sign.SignOptions> listOptions = new ArrayList<>();
listOptions.add(bcOptions);
listOptions.add(qrOptions);
```

**Mẹo**: Đặt chữ ký ở các vị trí chiến lược—góc hoặc khu vực không gây cản trở là tốt nhất cho các tệp TAR.

**3. Sign and Save the Document**  
Chuyển danh sách tùy chọn vào phương thức `sign()`:
```java
String outputFilePath = "output/path/SignWithMultipleSignatures/archive_signed.tar";
SignResult signResult = signature.sign(outputFilePath, listOptions);
```

GroupDocs sẽ xử lý từng chữ ký theo thứ tự, nhúng chúng vào metadata của tài liệu. Thứ tự trong danh sách không ảnh hưởng đến việc xác minh.

## Các trường hợp sử dụng thực tế

### 1. Quy trình phân phối phần mềm
**Kịch bản**: Phân phối các gói phần mềm dưới dạng tệp TAR và chứng minh chúng không bị sửa đổi.  
**Giải pháp**: Ký mỗi bản phát hành bằng mã QR chứa payload JSON:
```java
String releaseData = String.format(
    "{\"version\":\"%s\",\"buildDate\":\"%s\",\"sha256\":\"%s\"}",
    version, buildDate, checksum
);
```  
**Tại sao hiệu quả**: Người dùng có thể quét mã QR để xác minh tính toàn vẹn của gói trước khi cài đặt—không cần quản lý khóa GPG.

### 2. Hệ thống sao lưu tự động
**Kịch bản**: Các tệp sao lưu TAR hàng ngày cần có dấu vết kiểm toán.  
**Giải pháp**: Thêm mã vạch với dấu thời gian sao lưu và ID máy chủ:
```java
String backupId = String.format("SRV01-%s", LocalDateTime.now().format(formatter));
BarcodeSignOptions bcOptions = new BarcodeSignOptions(backupId, BarcodeTypes.Code128);
```  
**Tại sao hiệu quả**: Kiểm tra nhanh tính xác thực của sao lưu mà không cần mở tệp.

### 3. Hệ thống quản lý tài liệu
**Kịch bản**: Các tài liệu pháp lý lưu trữ dưới dạng kho lưu trữ yêu cầu xác thực không thể giả mạo.  
**Giải pháp**: Sử dụng cả mã vạch (quét nhanh) và mã QR (siêu dữ liệu chi tiết) trên cùng một tệp lưu trữ.

### 4. Theo dõi chuỗi cung ứng
**Kịch bản**: Theo dõi các gói tệp qua nhiều tổ chức.  
**Giải pháp**: Nhúng mã QR với URL theo dõi liên kết tới API xác thực:
```java
String trackingUrl = "https://verify.yourcompany.com/track/" + uniqueId;
QrCodeSignOptions qrOptions = new QrCodeSignOptions(trackingUrl, QrCodeTypes.QR);
```  

## Các vấn đề thường gặp và giải pháp

### Vấn đề 1: “Không tìm thấy chữ ký” sau khi ký
**Triệu chứng**: `sign()` trả về thành công, nhưng chữ ký không hiển thị.  
**Nguyên nhân**: Vị trí sai, ghi đè tệp gốc, hoặc giới hạn của trình xem TAR.  
**Giải pháp**:  
```java
// Always verify the signing succeeded
SignResult result = signature.sign(outputFilePath, bcOptions);
if (result.getSucceeded().size() > 0) {
    System.out.println("Signature added successfully at: " + outputFilePath);
} else {
    System.err.println("Signing failed: " + result.getFailed());
}

// Use absolute paths to avoid confusion
String absolutePath = new File(outputFilePath).getAbsolutePath();
```  

### Vấn đề 2: Lỗi OutOfMemoryError với tệp TAR lớn
**Triệu chứng**: JVM sập khi xử lý các kho lưu trữ > 500 MB.  
**Giải pháp**: Tăng kích thước heap (`-Xmx`) và giải phóng đối tượng `Signature` kịp thời:
```bash
java -Xmx2G -jar your-application.jar
```  

Hoặc triển khai xử lý theo khối:
```java
// For very large files, consider signing metadata separately
// rather than embedding in the TAR itself
```  

### Vấn đề 3: Dữ liệu chữ ký bị cắt ngắn
**Triệu chứng**: Các chuỗi dài bị cắt.  
**Nguyên nhân**: Vượt quá khả năng của Code128 (≈ 80 ký tự).  
**Giải pháp**: Chuyển sang mã QR để lưu trữ payload dài hơn:
```java
// Bad: Too much data for Code128
BarcodeSignOptions bcOptions = new BarcodeSignOptions(veryLongString, BarcodeTypes.Code128);

// Good: Use QR code instead
QrCodeSignOptions qrOptions = new QrCodeSignOptions(veryLongString, QrCodeTypes.QR);
```  

### Vấn đề 4: Lỗi xác thực giấy phép
**Triệu chứng**: `LicenseException` hoặc cảnh báo “Phiên bản dùng thử” trong môi trường production.  
**Giải pháp**: Tải giấy phép trước khi tạo bất kỳ thể hiện `Signature` nào:
```java
import com.groupdocs.signature.License;

License license = new License();
license.setLicense("path/to/GroupDocs.Signature.lic");

// Now create signatures
Signature signature = new Signature("document.tar");
```  

**Mẹo**: Tải giấy phép một lần khi khởi động ứng dụng, không phải trước mỗi lần ký.

### Vấn đề 5: Giá trị vị trí không hoạt động như mong đợi
**Triệu chứng**: Chữ ký xuất hiện ở vị trí không đúng.  
**Nguyên nhân**: Nhầm lẫn giữa pixel và point.  
**Giải pháp**: GroupDocs mặc định sử dụng pixel. Để đặt chính xác:
```java
bcOptions.setLeft(100);  // 100 pixels from left edge
bcOptions.setTop(100);   // 100 pixels from top edge

// If you need percentage-based positioning:
bcOptions.setHorizontalAlignment(HorizontalAlignment.Center);
bcOptions.setVerticalAlignment(VerticalAlignment.Center);
```  

## Mẫu tích hợp

### Mẫu 1: Dịch vụ REST API
Cung cấp ký dưới dạng microservice:
```java
@RestController
@RequestMapping("/api/signature")
public class SignatureController {
    
    @PostMapping("/sign")
    public ResponseEntity<SignatureResponse> signFile(
            @RequestParam("file") MultipartFile file,
            @RequestParam("signatureType") String type) {
        
        try {
            // Save uploaded file temporarily
            File tempFile = File.createTempFile("upload-", ".tar");
            file.transferTo(tempFile);
            
            // Sign based on type
            Signature signature = new Signature(tempFile.getAbsolutePath());
            
            SignOptions options = type.equals("barcode") 
                ? createBarcodeOptions() 
                : createQROptions();
            
            String outputPath = generateOutputPath();
            SignResult result = signature.sign(outputPath, options);
            
            // Return signed file
            return ResponseEntity.ok(new SignatureResponse(outputPath, result));
            
        } catch (Exception e) {
            return ResponseEntity.status(500).body(null);
        }
    }
}
```  

### Mẫu 2: Quy trình xử lý hàng loạt
Ký nhiều kho lưu trữ trong một pipeline:
```java
public class BatchSigner {
    
    public void signArchiveBatch(List<File> archives) {
        ExecutorService executor = Executors.newFixedThreadPool(4);
        
        archives.forEach(archive -> {
            executor.submit(() -> {
                try {
                    signSingleArchive(archive);
                } catch (Exception e) {
                    logger.error("Failed to sign: " + archive.getName(), e);
                }
            });
        });
        
        executor.shutdown();
        executor.awaitTermination(1, TimeUnit.HOURS);
    }
    
    private void signSingleArchive(File archive) throws Exception {
        Signature signature = new Signature(archive.getAbsolutePath());
        // ... signing logic
    }
}
```  

### Mẫu 3: Kiến trúc dựa trên sự kiện
Kích hoạt ký khi tạo ra các kho lưu trữ:
```java
@Component
public class ArchiveCreatedListener {
    
    @EventListener
    public void onArchiveCreated(ArchiveCreatedEvent event) {
        CompletableFuture.runAsync(() -> {
            signArchive(event.getFilePath());
        });
    }
    
    private void signArchive(String filePath) {
        // ... signing logic
    }
}
```  

## Xem xét về hiệu năng

### Quản lý bộ nhớ
**Vấn đề**: Mỗi thể hiện `Signature` tải toàn bộ tệp vào bộ nhớ.  
**Thực hành tốt**:
```java
// Bad: Creating multiple instances for same file
Signature sig1 = new Signature("file.tar");
Signature sig2 = new Signature("file.tar");  // Loads again!

// Good: Reuse the instance
try (Signature signature = new Signature("file.tar")) {
    signature.sign(output1, options1);
    signature.sign(output2, options2);  // Same instance, different outputs
}
```  

### Tối ưu kích thước tệp
- **Tệp nhỏ (< 10 MB)** – ký đồng bộ.  
- **Tệp trung bình (10‑100 MB)** – dùng luồng nền.  
- **Tệp lớn (> 100 MB)** – cân nhắc ký metadata riêng hoặc sử dụng API streaming.

### Độ phức tạp của chữ ký (thời gian ước tính trên máy chủ tiêu chuẩn)

| Loại chữ ký | Thời gian mỗi tài liệu |
|-------------|------------------------|
| Mã vạch đơn | 50‑100 ms |
| Mã QR đơn | 100‑200 ms |
| Nhiều chữ ký | 150‑300 ms |

**Mẹo tối ưu**: Đối với hàng ngàn tệp, gom chúng thành batch và dùng thread pool (xem mẫu xử lý hàng loạt ở trên).

### Cập nhật thư viện
GroupDocs thường xuyên phát hành cải tiến hiệu năng. Luôn kiểm tra [changelog](https://releases.groupdocs.com/signature/java/) trước khi triển khai lớn.

**Chiến lược cập nhật**:  
1. Kiểm thử phiên bản mới trong môi trường staging.  
2. Xem xét các thay đổi gây phá vỡ.  
3. Đánh giá hiệu năng với tệp thực tế.  
4. Triển khai dần dần.

## Thực hành tốt cho môi trường sản xuất

**1. Xác thực trạng thái giấy phép**
```java
License license = new License();
if (!license.isLicensed()) {
    logger.warn("Running in trial mode - features may be limited");
}
```  

**2. Triển khai xử lý lỗi mạnh mẽ**
```java
try {
    signature.sign(outputPath, options);
} catch (Exception e) {
    logger.error("Signature failed", e);
    // Don't just swallow exceptions - log or re-throw
    throw new SignatureException("Failed to sign document", e);
}
```  

**3. Sử dụng dữ liệu chữ ký mô tả**
```java
// Bad: Meaningless ID
new BarcodeSignOptions("12345678", BarcodeTypes.Code128);

// Good: Self-documenting data
String signatureData = String.format("DOC-%s-%s", 
    docType, 
    LocalDateTime.now().format(DateTimeFormatter.ISO_DATE_TIME)
);
new BarcodeSignOptions(signatureData, BarcodeTypes.Code128);
```  

**4. Phiên bản hoá định dạng chữ ký**
Bao gồm số phiên bản trong JSON nhúng để tương lai có thể xác thực logic:  
```java
String qrData = String.format(
    "{\"v\":\"1.0\",\"type\":\"archive\",\"timestamp\":\"%s\"}", 
    timestamp
);
```  

**5. Kiểm thử với tệp thực tế** – luôn xác minh với các kho lưu trữ kích thước production để phát hiện sớm vấn đề bộ nhớ và hiệu năng.

## Kết luận

Bạn đã có nền tảng vững chắc để triển khai **digital signature java** bằng mã vạch và mã QR. Đây là những gì bạn đã học:

- Cách ký các tệp TAR (và các tài liệu khác) bằng cả mã vạch và mã QR  
- Khi nào chọn loại chữ ký dựa trên nhu cầu cụ thể  
- Cách khắc phục các vấn đề thường gặp trước khi đưa vào production  
- Các mẫu tích hợp thực tế cho REST API, xử lý batch và kiến trúc dựa trên sự kiện  
- Kỹ thuật tối ưu hiệu năng cho mọi kích thước tệp  

**Bước tiếp theo**:  
1. Khám phá xác thực chữ ký bằng phương thức `search()`.  
2. Thử các định dạng tài liệu khác—GroupDocs.Signature hỗ trợ PDF, DOCX, XLSX, PNG và nhiều hơn nữa.  
3. Tùy chỉnh giao diện chữ ký (màu, kích thước, viền).  
4. Xây dựng API xác thực để kiểm tra chữ ký một cách lập trình.

Sức mạnh của GroupDocs.Signature vượt xa hướng dẫn này. Hãy xem [tài liệu đầy đủ](https://docs.groupdocs.com/signature/java/) để khám phá các tính năng nâng cao như chữ ký văn bản, chữ ký hình ảnh và trích xuất metadata.

Có câu hỏi hoặc muốn chia sẻ cách thực hiện? Tham gia diễn đàn cộng đồng GroupDocs để nhận hỗ trợ từ các nhà phát triển khác.

## Câu hỏi thường gặp

**Q: Tôi có thể ký các tài liệu khác ngoài tệp TAR không?**  
A: Chắc chắn! GroupDocs.Signature hỗ trợ hơn 50 định dạng, bao gồm PDF, DOCX, XLSX, PNG và nhiều hơn nữa. Chỉ cần thay đổi phần mở rộng trong hàm khởi tạo `Signature` để làm việc với bất kỳ loại hỗ trợ nào.

**Q: Làm sao tôi xác thực chữ ký sau khi ký?**  
A: Sử dụng phương thức `search()` để tìm và xác thực chữ ký:  
```java
Signature signature = new Signature("signed-document.tar");
BarcodeSearchOptions searchOptions = new BarcodeSearchOptions();
List<BarcodeSignature> signatures = signature.search(BarcodeSignature.class, searchOptions);
```  

**Q: Các chữ ký có an toàn trước việc giả mạo không?**  
A: Chữ ký mã vạch và mã QR cung cấp xác thực hình ảnh nhưng không mạnh về mặt mật mã như chứng chỉ số. Để bảo mật tối đa, kết hợp chúng với PKI truyền thống hoặc lưu trữ hash chữ ký trong cơ sở dữ liệu bên ngoài.

**Q: Dung lượng dữ liệu tối đa tôi có thể lưu trong một chữ ký là bao nhiêu?**  
- Mã vạch Code128: ~80 ký tự chữ và số  
- Mã QR (Phiên bản 40): lên tới 4.296 ký tự chữ và số hoặc 7.089 ký tự số  

**Q: Tôi có thể tùy chỉnh giao diện chữ ký không?**  
A: Có! Kiểm soát màu, kích thước, viền và hơn thế nữa:  
```java
bcOptions.setForeColor(Color.BLUE);
bcOptions.setBackgroundColor(Color.YELLOW);
bcOptions.setBorder(new Border());
bcOptions.getBorder().setColor(Color.RED);
bcOptions.getBorder().setWeight(2);
```  

**Q: Điều gì xảy ra nếu tôi ký một tệp hai lần?**  
A: Mỗi lần gọi `sign()` sẽ thêm một chữ ký mới. Để thay thế chữ ký hiện có, hãy xóa nó trước bằng phương thức `delete()`.

**Q: Làm sao tôi xử lý các tệp lớn mà không hết bộ nhớ?**  
A: Tăng heap JVM (`-Xmx`), giải phóng đối tượng `Signature` kịp thời, và cân nhắc ký metadata riêng cho các kho lưu trữ đa gigabyte.

**Q: Tôi có cần kết nối internet để ký tài liệu không?**  
A: Không. GroupDocs.Signature hoạt động hoàn toàn offline sau khi thư viện được cài đặt.

---

**Cập nhật lần cuối:** 2026-05-21  
**Kiểm thử với:** GroupDocs.Signature 23.12 for Java  
**Tác giả:** GroupDocs

## Hướng dẫn liên quan

- [Digital Signature in Java - Complete Guide to Certificate Loading and Document Signing](/signature/java/digital-signatures/digital-signature-loading-signing-groupdocs-java/)
- [Java Signature Verification Tutorial - Validate Documents with Text, Barcode & QR Codes](/signature/java/search-verification/groupdocs-signature-java-document-verification-guide/)
- [Sign ZIP Files in Java with Barcodes & QR Codes](/signature/java/multiple-signatures/sign-zip-files-barcode-qr-code-java/)
