---
categories:
- Java PDF Processing
date: '2026-07-20'
description: Tìm hiểu cách tạo chữ ký mã vạch trong tài liệu PDF bằng Java và GroupDocs.Signature.
  Hướng dẫn chi tiết từng bước kèm ví dụ mã và các thực tiễn tốt nhất.
keywords:
- create barcode signature
- how to add barcode
- generate code128 barcode
- add barcode pdf
- tamper evident barcode
lastmod: '2026-07-20'
linktitle: Tạo chữ ký mã vạch bằng Java
og_description: Tạo chữ ký mã vạch trong PDF bằng Java với GroupDocs.Signature. Tìm
  hiểu từng bước cách thêm mã vạch Code128, định vị chúng và bảo mật tài liệu.
og_image_alt: 'Developer guide: Create barcode signature in PDF using Java and GroupDocs'
og_title: Tạo chữ ký mã vạch trong PDF bằng Java – Hướng dẫn đầy đủ
schemas:
- author: GroupDocs
  dateModified: '2026-07-20'
  description: Learn how to create barcode signature in PDF documents using Java and
    GroupDocs.Signature. Step-by-step tutorial with code examples and best practices.
  headline: How to Create Barcode Signature in PDF using Java
  type: TechArticle
- description: Learn how to create barcode signature in PDF documents using Java and
    GroupDocs.Signature. Step-by-step tutorial with code examples and best practices.
  name: How to Create Barcode Signature in PDF using Java
  steps:
  - name: Initialize the Signature object
    text: '**Definition anchor:** The `Signature` class is GroupDocs.Signature''s
      entry point for loading, modifying, and saving PDF documents. First, you need
      to tell GroupDocs which PDF you''re working with: **What''s happening here:**
      The `Signature` object loads your PDF into memory and prepares it for modifi'
  - name: Configure your barcode options (How to add barcode)
    text: '**Definition anchor:** `BarcodeSignOptions` encapsulates all settings required
      to render a barcode inside a PDF. Now let''s create the barcode signature with
      your data: - `"12345678"` is your barcode data — this could be an order ID,
      certificate number, or any identifier you need. - `Code128` is the '
  - name: Position your barcode (How to sign PDF with barcode)
    text: '**Definition anchor:** `SignatureOptions` provides layout properties such
      as page number, size, and alignment. Here''s where GroupDocs really shines —
      percentage‑based positioning means your barcode looks good on any PDF size:
      **Why percentages matter:** Imagine you''re signing both A4 documents and l'
  - name: Sign and save your document (How to add barcode pdf)
    text: 'Time to actually apply the signature and save your work: **Important note:**
      The output directory must exist before you run this code. GroupDocs won''t create
      nested directories for you, so create them first or handle that in your code:
      **What if something goes wrong?** Wrap this in a try‑catch block'
  type: HowTo
- questions:
  - answer: Yes! Call `signature.sign()` multiple times with different `BarcodeSignOptions`
      for each barcode type. Just ensure they don’t overlap.
    question: Can I use different barcode types in the same PDF?
  - answer: Code128 handles most ASCII characters fine. For Unicode or complex data,
      switch to QR codes—they support UTF‑8 encoding.
    question: How do I handle barcodes that contain special characters?
  - answer: Technically up to 128 characters, but readability drops significantly
      above 30‑40 characters. For larger payloads, use QR codes.
    question: What's the maximum data I can store in a Code128 barcode?
  - answer: Not noticeably—barcodes are vector graphics, typically adding only 5‑20
      KB per barcode depending on size and complexity.
    question: Will adding barcodes significantly increase my PDF file size?
  - answer: Yes! Use `options.setRotationAngle(90)` to rotate your barcode, which
      is handy for margin placement.
    question: Can I rotate barcodes or place them vertically?
  type: FAQPage
tags:
- pdf-signing
- barcode-signature
- document-security
- groupdocs
- java
- pdf
title: Cách tạo chữ ký mã vạch trong PDF bằng Java
type: docs
url: /vi/java/barcode-signatures/java-pdf-signing-barcode-groupdocs/
weight: 1
---

# Cách Tạo Chữ Ký Mã Vạch trong PDF bằng Java

Trong hướng dẫn này, bạn sẽ học cách **tạo chữ ký mã vạch** trong các tệp PDF bằng Java và GroupDocs.Signature. Chữ ký mã vạch nhúng các định danh có thể đọc được bằng máy, vừa chống giả mạo vừa dễ quét—hoàn hảo cho hợp đồng, chứng chỉ, hoá đơn và bất kỳ tài liệu nào cần xác thực đáng tin cậy.

## Câu trả lời nhanh
- **Chữ ký mã vạch là gì?** Một mã vạch được nhúng trong PDF, lưu trữ dữ liệu có cấu trúc và có thể được đọc bởi máy quét hoặc phần mềm.  
- **Loại mã vạch nào được khuyến nghị?** Code128, vì nó xử lý dữ liệu alphanumeric một cách gọn gàng.  
- **Tôi có cần giấy phép không?** Bản dùng thử miễn phí hoạt động cho việc thử nghiệm; giấy phép đầy đủ cần thiết cho môi trường sản xuất.  
- **Tôi có thể đặt mã vạch trên bất kỳ kích thước trang nào không?** Có—sử dụng vị trí dựa trên phần trăm để tự động điều chỉnh kích thước.  
- **Mã vạch có phải là dạng vector không?** Có, nó chỉ thêm vài kilobytes vào PDF và vẫn giữ độ nét ở bất kỳ độ phân giải nào.  

## Chữ ký mã vạch là gì?
Chữ ký mã vạch là một mã vạch dạng vector được nhúng trực tiếp vào trang PDF, vừa đóng vai trò là yếu tố hình ảnh vừa là chữ ký mật mã có thể được xác thực sau này. Nó lưu trữ dữ liệu có cấu trúc, chẳng hạn như ID hoặc dấu thời gian, và đảm bảo tính toàn vẹn của tài liệu đồng thời cung cấp một tham chiếu có thể đọc được bằng máy.

## Tại sao chữ ký mã vạch lại quan trọng đối với PDF của bạn
Chữ ký mã vạch cung cấp cho PDF một định danh gọn nhẹ, có thể đọc bằng máy và có thể quét ngay lập tức, loại bỏ việc nhập dữ liệu thủ công và giảm lỗi. Vì chúng được nhúng dưới dạng đồ họa vector, chúng vẫn sắc nét ở bất kỳ độ phân giải nào và chỉ thêm vài kilobytes vào tệp. Sự kết hợp giữa khả năng đọc, chống giả mạo và kích thước tối thiểu này khiến chúng lý tưởng cho hợp đồng, hoá đơn, chứng chỉ và bất kỳ tài liệu nào yêu cầu xác thực đáng tin cậy.

Đây là một thách thức mà bạn có thể đã gặp: bạn cần thêm các định danh duy nhất vào PDF mà vừa có thể đọc bằng máy vừa chống giả mạo. Có thể bạn đang làm việc trên hệ thống quản lý tài liệu, xử lý chứng chỉ, hoặc xử lý hợp đồng cần xác thực sau này.

Đó là lúc chữ ký mã vạch trở nên hữu ích. Khác với các dấu tem văn bản đơn giản, mã vạch cho phép bạn nhúng dữ liệu có cấu trúc mà máy quét (và phần mềm của bạn) có thể đọc ngay lập tức. Thêm nữa, khi bạn kết hợp chúng với việc ký PDF thông qua GroupDocs.Signature cho Java, bạn có được một cách mạnh mẽ để theo dõi và xác thực tài liệu mà không cần tra cứu cơ sở dữ liệu phức tạp.

Trong hướng dẫn này, bạn sẽ học cách triển khai chữ ký mã vạch trong PDF Java của mình — từ cài đặt cơ bản đến mã sẵn sàng cho môi trường sản xuất với vị trí linh hoạt. Dù bạn đang xây dựng hệ thống hoá đơn, trình tạo chứng chỉ, hay nền tảng quản lý hợp đồng, bạn sẽ có mọi thứ cần thiết vào cuối hướng dẫn.

**Bạn sẽ thành thạo:**
- Cài đặt GroupDocs.Signature cho Java trong vài phút  
- Tạo chữ ký mã vạch Code128 (và lý do tại sao chúng thường là lựa chọn tốt nhất của bạn)  
- Đặt mã vạch bằng bố cục dựa trên phần trăm, hoạt động trên mọi kích thước PDF  
- Tránh các bẫy thường gặp khiến nhà phát triển gặp khó khăn  
- Kiểm tra việc triển khai của bạn một cách đúng đắn  

## Cách tạo chữ ký mã vạch trong Java
Việc tạo chữ ký mã vạch trong Java bao gồm tải PDF mục tiêu, cấu hình các tùy chọn mã vạch như dữ liệu, loại, kích thước và vị trí, sau đó áp dụng chữ ký để tạo tài liệu mới. GroupDocs.Signature xử lý việc render và ràng buộc mật mã, vì vậy bạn chỉ cần cung cấp các tham số mong muốn và quản lý đường dẫn tệp.

## Yêu cầu trước và danh sách kiểm tra môi trường
Trước khi bắt đầu, hãy xác nhận rằng bạn đã chuẩn bị các mục sau:

- **Java Development Kit (JDK) 8 hoặc mới hơn** – bắt buộc cho tất cả các thư viện Java của GroupDocs.  
- **Maven hoặc Gradle** – để quản lý phụ thuộc GroupDocs.Signature.  
- **Một IDE** như IntelliJ IDEA, Eclipse, hoặc VS Code với các tiện ích mở rộng Java.  
- **GroupDocs.Signature cho Java** (phiên bản 23.12 hoặc mới hơn được khuyến nghị).  
- **Kiến thức Java cơ bản** – bạn nên thoải mái tạo lớp, xử lý ngoại lệ và làm việc với I/O tệp.  

## Cài đặt GroupDocs.Signature trong dự án của bạn
Việc đưa thư viện vào dự án của bạn rất đơn giản. Chọn công cụ xây dựng của bạn:

**Đối với người dùng Maven**, thêm phụ thuộc này vào `pom.xml` của bạn:

```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

**Sử dụng Gradle?** Thêm dòng này vào `build.gradle` của bạn:

```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

**Ưu tiên cài đặt thủ công?** Tải JAR trực tiếp từ [GroupDocs.Signature for Java releases](https://releases.groupdocs.com/signature/java/) và thêm vào classpath của bạn.

### Sắp xếp giấy phép của bạn
Trước khi đưa vào sản xuất đầy đủ, bạn sẽ muốn xử lý giấy phép:

- **Free Trial:** Hoàn hảo cho việc thử nghiệm — lấy nó từ trang web GroupDocs để khám phá các tính năng cốt lõi.  
- **Temporary License:** Cần thêm thời gian để đánh giá? Đăng ký giấy phép tạm thời 30 ngày.  
- **Full License:** Sẵn sàng cho sản xuất? Mua giấy phép để sử dụng không giới hạn.  

Dưới đây là một kiểm tra nhanh để đảm bảo mọi thứ hoạt động:

```java
Signature signature = new Signature("sample.pdf");
System.out.println("Signature object created successfully.");
```

Nếu chạy mà không có lỗi, bạn đã sẵn sàng!

## Cách tạo chữ ký mã vạch trong Java
Bây giờ là phần thú vị — hãy ký một PDF bằng mã vạch. Chúng tôi sẽ chia quá trình này thành các bước nhỏ để bạn hiểu chính xác những gì đang diễn ra ở mỗi giai đoạn.

### Bước 1: Khởi tạo đối tượng Signature
**Definition anchor:** Lớp `Signature` là điểm vào của GroupDocs.Signature để tải, sửa đổi và lưu tài liệu PDF.

Đầu tiên, bạn cần cho GroupDocs biết PDF nào bạn đang làm việc:

```java
Signature signature = new Signature("input.pdf");
```

**What's happening here:** Đối tượng `Signature` tải PDF của bạn vào bộ nhớ và chuẩn bị cho các sửa đổi. Đảm bảo đường dẫn tệp của bạn đúng — một lỗi phổ biến là sử dụng dấu gạch chéo ngược trên Windows mà không escape (sử dụng `\\` hoặc chỉ dùng dấu gạch chéo xuôi, chúng hoạt động đa nền tảng).

### Bước 2: Cấu hình các tùy chọn mã vạch (Cách thêm mã vạch)
**Definition anchor:** `BarcodeSignOptions` bao gồm tất cả cài đặt cần thiết để render mã vạch trong PDF.

Bây giờ hãy tạo chữ ký mã vạch với dữ liệu của bạn:

```java
BarcodeSignOptions options = new BarcodeSignOptions("12345678");
options.setEncodeType(BarcodeEncodeType.Code128);
```

- `"12345678"` là dữ liệu mã vạch của bạn — điều này có thể là ID đơn hàng, số chứng chỉ, hoặc bất kỳ định danh nào bạn cần.  
- `Code128` là loại mã hoá (sẽ nói thêm về cách chọn loại phù hợp bên dưới).

**Pro tip:** Code128 có thể xử lý cả số và chữ, làm cho nó linh hoạt cho hầu hết các trường hợp sử dụng. Nếu bạn chỉ cần số, `Code39` có thể đơn giản hơn, nhưng Code128 cung cấp nhiều linh hoạt hơn.

### Bước 3: Đặt vị trí mã vạch (Cách ký PDF bằng mã vạch)
**Definition anchor:** `SignatureOptions` cung cấp các thuộc tính bố cục như số trang, kích thước và căn chỉnh.

Đây là nơi GroupDocs thực sự tỏa sáng — vị trí dựa trên phần trăm có nghĩa là mã vạch của bạn trông tốt trên bất kỳ kích thước PDF nào:

```java
options.setLeft(10);   // 10% from the left edge
options.setTop(90);    // 90% from the bottom edge (near the footer)
options.setWidth(30);  // 30% of page width
options.setHeight(10); // 10% of page height
options.setPageNumber(1);
```

**Why percentages matter:** Hãy tưởng tượng bạn đang ký cả tài liệu A4 và các mẫu kích thước legal. Với vị trí phần trăm, mã vạch của bạn tự động điều chỉnh để trông đồng nhất trên cả hai. Sử dụng giá trị pixel cố định sẽ khiến mã vạch quá nhỏ trên tài liệu lớn hoặc quá lớn trên tài liệu nhỏ.

**Real‑world example:** Trên trang A4 (595 × 842 points), mã vạch rộng 30% sẽ khoảng 180 points. Trên trang legal (612 × 1008 points), nó sẽ khoảng 184 points — tự động tỷ lệ.

### Bước 4: Ký và lưu tài liệu của bạn (Cách thêm mã vạch vào PDF)
Đến lúc thực sự áp dụng chữ ký và lưu công việc của bạn:

```java
signature.sign(outputPath, options);
```

**Important note:** Thư mục đầu ra phải tồn tại trước khi bạn chạy đoạn mã này. GroupDocs sẽ không tạo các thư mục con cho bạn, vì vậy hãy tạo chúng trước hoặc xử lý trong mã của bạn:

```java
new File("output").mkdirs();
```

**What if something goes wrong?** Đặt đoạn này trong khối try‑catch:

```java
try {
    signature.sign("signed.pdf", options);
} catch (Exception e) {
    e.printStackTrace();
}
```

## Lựa chọn loại mã vạch phù hợp cho nhu cầu của bạn (tạo mã vạch code128)
GroupDocs hỗ trợ nhiều định dạng mã vạch, và việc chọn loại phù hợp rất quan trọng. Dưới đây là so sánh thực tế:

**Code128 (Lựa chọn mặc định của chúng tôi):**
- **Best for:** Dữ liệu alphanumeric hỗn hợp (ID như "INV2024-001")  
- **Capacity:** Lên tới 128 ký tự ASCII  
- **Why it wins:** Gọn gàng, được hỗ trợ rộng rãi, xử lý cả chữ và số  
- **Use when:** Bạn cần tính linh hoạt và không biết loại dữ liệu nào sẽ mã hoá  

**Code39:**
- **Best for:** Các mã alphanumeric đơn giản  
- **Capacity:** 43 ký tự (A‑Z, 0‑9 và một số ký hiệu)  
- **Why consider it:** Máy quét cũ thường hỗ trợ tốt hơn  
- **Use when:** Làm việc với hệ thống legacy hoặc khi tính đơn giản quan trọng hơn mật độ dữ liệu  

**QR Code:**
- **Best for:** Lượng dữ liệu lớn (URL, payload JSON)  
- **Capacity:** Lên tới 3 KB dữ liệu  
- **Why it's powerful:** Có thể lưu trữ cấu trúc dữ liệu phức tạp, có tính năng sửa lỗi tích hợp  
- **Use when:** Bạn cần nhúng dữ liệu có cấu trúc hoặc URL  

**EAN/UPC:**
- **Best for:** Nhận dạng sản phẩm  
- **Capacity:** Mã số cố định (8‑13 chữ số)  
- **Use when:** Bạn đang làm việc với hệ thống bán lẻ hoặc quản lý tồn kho  

**Hướng dẫn quyết định nhanh:**
- Cần chữ và số? → Code128  
- Chỉ số, giữ đơn giản? → Code39  
- Nhiều dữ liệu hoặc URL? → QR Code  
- Mã bán lẻ/sản phẩm? → EAN/UPC  

## Những bẫy thường gặp và cách tránh chúng (mã vạch chống giả mạo)
Dưới đây là các vấn đề mà các nhà phát triển thường gặp (để bạn không phải gặp):

### Vấn đề 1: Vị trí mã vạch hiển thị sai
**Symptom:** Mã vạch của bạn xuất hiện ở vị trí không mong muốn hoặc bị cắt.  
**Common causes:**  
- Sử dụng giá trị pixel trên các kích thước trang khác nhau  
- Quên rằng tọa độ PDF bắt đầu từ góc dưới‑trái, không phải trên‑trái  
- Lề đẩy nội dung ra ngoài khu vực hiển thị  

**Solution:** Luôn sử dụng vị trí dựa trên phần trăm để đồng nhất:

```java
options.setLeft(5);
options.setTop(95);
options.setWidth(40);
options.setHeight(12);
```

### Vấn đề 2: Văn bản mã vạch không đọc được
**Symptom:** Văn bản đã mã hoá hiển thị nhưng máy quét không thể đọc được.  
**Causes:**  
- Mã vạch quá nhỏ so với lượng dữ liệu  
- Loại mã hoá sai cho dữ liệu của bạn  
- Độ tương phản thấp giữa các thanh và nền  

**Solution:** Điều chỉnh kích thước mã vạch phù hợp với độ dài dữ liệu. Đối với Code128 với 10‑15 ký tự, nên đặt ít nhất 8‑10% chiều rộng trang.

### Vấn đề 3: Ngoại lệ đường dẫn tệp
**Symptom:** `FileNotFoundException` hoặc các lỗi tương tự.  
**Causes:**  
- Đường dẫn Windows được mã cứng với dấu gạch chéo ngược đơn  
- Thư mục đầu ra không tồn tại  
- Vấn đề quyền truy cập tệp  

**Solution:** Sử dụng dấu gạch chéo xuôi (chúng hoạt động ở mọi nơi) và tạo thư mục trước:

```java
Path output = Paths.get("output/signed.pdf");
Files.createDirectories(output.getParent());
```

### Vấn đề 4: Vấn đề bộ nhớ với PDF lớn
**Symptom:** Lỗi hết bộ nhớ khi xử lý tài liệu lớn.  
**Solution:** Đóng đối tượng `Signature` khi hoàn thành để giải phóng tài nguyên:

```java
signature.close();
```

## Kiểm tra việc triển khai mã vạch của bạn
Trước khi triển khai, hãy chắc chắn mã vạch của bạn thực sự hoạt động. Dưới đây là danh sách kiểm tra thực tế:

### 1. Kiểm tra bằng mắt
Mở PDF đã ký của bạn và kiểm tra:
- Mã vạch có hiển thị và được đặt đúng vị trí không?  
- Nó có sắc nét (không mờ hoặc bị pixel hoá) không?  
- Có đủ khoảng trắng xung quanh không?

### 2. Kiểm tra quét
Sử dụng ứng dụng quét mã vạch trên điện thoại (như “Barcode Scanner” hoặc “QR & Barcode Reader”) để xác minh:
- Máy quét có thể đọc mã vạch của bạn  
- Dữ liệu giải mã khớp với những gì bạn đã mã hoá  
- Nó hoạt động từ các góc và khoảng cách khác nhau

### 3. Kiểm tra đa nền tảng
Mở PDF của bạn trên các thiết bị khác nhau:
- Windows (Adobe Reader, Chrome)  
- Mac (Preview, Chrome)  
- Thiết bị di động (iOS, Android)  

Đảm bảo mã vạch được render đúng ở mọi nơi.

### 4. Mã kiểm thử tự động
Dưới đây là một bài kiểm tra đơn giản bạn có thể chạy:

```java
Signature testSignature = new Signature("signed.pdf");
List<BarcodeSignature> signatures = testSignature.search(BarcodeSignature.class);
if (signatures.size() > 0) {
    System.out.println("Barcode found: " + signatures.get(0).getText());
}
```

## Các trường hợp sử dụng thực tế cho chữ ký mã vạch
Hãy xem nơi kỹ thuật này thực sự tỏa sáng trong các hệ thống sản xuất:

### 1. Tạo và xác minh chứng chỉ
**Scenario:** Bạn đang xây dựng nền tảng đào tạo phát hành chứng chỉ hoàn thành.  
**Implementation:** Tạo một ID chứng chỉ duy nhất (ví dụ, “CERT‑2024‑00123”) và nhúng nó dưới dạng mã vạch Code128 ở góc dưới‑phải. Quét mã vạch cho phép API của bạn truy xuất chi tiết chứng chỉ ngay lập tức, loại bỏ việc nhập dữ liệu thủ công.

### 2. Hệ thống theo dõi hoá đơn
**Scenario:** Công ty của bạn xử lý hàng nghìn hoá đơn mỗi tháng.  
**Implementation:** Thêm số hoá đơn và ngày đến hạn dưới dạng QR code được đặt ở vị trí mà thiết bị quét có thể dễ dàng đọc. Hệ thống sắp xếp tự động có thể chuyển hướng hoá đơn mà không cần can thiệp của con người, giảm thời gian xử lý từ giờ xuống phút.

### 3. Quản lý hợp đồng pháp lý
**Scenario:** Một công ty luật cần theo dõi các phiên bản và sửa đổi hợp đồng.  
**Implementation:** Mỗi phiên bản hợp đồng nhận một định danh mã vạch duy nhất bao gồm ID hợp đồng, số phiên bản và ngày ký. Quét trong quá trình kiểm toán sẽ tự động hiển thị toàn bộ lịch sử phiên bản.

### 4. Bảo mật hồ sơ y tế
**Scenario:** Một bệnh viện muốn ngăn chặn truy cập hồ sơ không được phép.  
**Implementation:** Nhúng ID bệnh nhân và dấu thời gian tạo hồ sơ vào mã vạch. Chỉ các thiết bị đã xác thực mới có thể giải mã và truy cập toàn bộ hồ sơ, và mỗi lần quét tạo một nhật ký kiểm toán để tuân thủ.

## Mẹo tối ưu hiệu năng (bảo mật tài liệu java)
Khi bạn ký nhiều PDF, hiệu năng rất quan trọng. Dưới đây là một số mẹo để duy trì hoạt động trơn tru:

### Chiến lược xử lý batch
Thay vì ký một tài liệu mỗi lần, hãy batch chúng:

```java
for (String filePath : pdfList) {
    Signature batchSignature = new Signature(filePath);
    batchSignature.sign(outputPath, options);
    batchSignature.close();
}
```

**Why this helps:** Tái sử dụng đối tượng options và đóng đúng tài nguyên ngăn ngừa rò rỉ bộ nhớ.

### Quản lý bộ nhớ cho PDF lớn
Đối với PDF lớn hơn 50 MB:
- Xử lý chúng tuần tự thay vì tải nhiều cùng lúc.  
- Sử dụng try‑with‑resources để đảm bảo dọn dẹp.  
- Giám sát kích thước heap và điều chỉnh tham số JVM nếu cần: `-Xmx2g`.

### Caching các mã vạch thường dùng
Nếu bạn ký nhiều tài liệu với cùng một mã vạch, hãy cache đối tượng `BarcodeSignOptions`:

```java
BarcodeSignOptions cachedOptions = new BarcodeSignOptions("STATIC_ID");
cachedOptions.setEncodeType(BarcodeEncodeType.Code128);
```

## Khi nào nên sử dụng chữ ký mã vạch (và khi nào không nên)
**Perfect scenarios:**
- Bạn cần các định danh tài liệu có thể đọc bằng máy.  
- Tài liệu sẽ được quét hoặc xử lý tự động.  
- Bạn muốn theo dõi chống giả mạo mà không cần chứng chỉ số.  
- Cần tích hợp với hạ tầng mã vạch hiện có.  

**Not ideal when:**
- Bạn cần chữ ký số có tính pháp lý (sử dụng chứng chỉ số thay thế).  
- Tài liệu chỉ được con người xem (một watermark văn bản đơn giản có thể đủ).  
- Bạn đang làm việc với tài liệu cực nhỏ mà mã vạch sẽ chiếm phần lớn trang.  
- Yêu cầu bảo mật yêu cầu mã hoá—mã vạch có thể nhìn thấy và quét được bởi bất kỳ ai.  

**Can you combine approaches?** Chắc chắn! Nhiều hệ thống sử dụng cả chữ ký mã vạch để theo dõi và chữ ký số để có tính pháp lý.

## Câu hỏi thường gặp
**Q: Tôi có thể sử dụng các loại mã vạch khác nhau trong cùng một PDF không?**  
A: Có! Gọi `signature.sign()` nhiều lần với các `BarcodeSignOptions` khác nhau cho mỗi loại mã vạch. Chỉ cần đảm bảo chúng không chồng lên nhau.

**Q: Làm sao tôi xử lý các mã vạch chứa ký tự đặc biệt?**  
A: Code128 xử lý hầu hết các ký tự ASCII tốt. Đối với Unicode hoặc dữ liệu phức tạp, chuyển sang QR code—chúng hỗ trợ mã hoá UTF‑8.

**Q: Dữ liệu tối đa tôi có thể lưu trong mã vạch Code128 là bao nhiêu?**  
A: Về mặt kỹ thuật lên tới 128 ký tự, nhưng khả năng đọc giảm đáng kể trên 30‑40 ký tự. Đối với payload lớn hơn, sử dụng QR code.

**Q: Việc thêm mã vạch sẽ làm tăng đáng kể kích thước tệp PDF của tôi không?**  
A: Không đáng kể—mã vạch là đồ họa vector, thường chỉ thêm 5‑20 KB cho mỗi mã vạch tùy vào kích thước và độ phức tạp.

**Q: Tôi có thể xoay mã vạch hoặc đặt chúng theo chiều dọc không?**  
A: Có! Sử dụng `options.setRotationAngle(90)` để xoay mã vạch, rất hữu ích cho việc đặt ở lề.

**Q: Làm sao để mã vạch xuất hiện trên mỗi trang của PDF đa trang?**  
A: Lặp qua các trang và áp dụng chữ ký cho mỗi trang. Kiểm tra lớp `PagesSetup` trong tài liệu GroupDocs để điều khiển các trang sẽ được ký.

**Q: Nếu máy quét mã vạch của tôi không thể đọc mã vạch đã tạo thì sao?**  
A: Đầu tiên, xác minh máy quét hỗ trợ loại mã vạch đã chọn. Sau đó tăng kích thước mã vạch—hầu hết các vấn đề quét xuất phát từ các thanh quá nhỏ. Nhắm ít nhất 1 inch (2.54 cm) chiều rộng để đọc đáng tin cậy.

## Tài nguyên bổ sung
**Documentation:**  
- [GroupDocs.Signature for Java Docs](https://docs.groupdocs.com/signature/java/)  
- [API Reference Guide](https://reference.groupdocs.com/signature/java/)  

**Downloads and Licensing:**  
- [Download Latest Version](https://releases.groupdocs.com/signature/java/)  
- [Free Trial Access](https://releases.groupdocs.com/signature/java/)  
- [Get Temporary License](https://purchase.groupdocs.com/temporary-license/)  
- [Purchase Full License](https://purchase.groupdocs.com/buy)  

**Community and Support:**  
- [Support Forum](https://forum.groupdocs.com/c/signature/) - Active community with GroupDocs engineers  

**Cập nhật lần cuối:** 2026-07-20  
**Kiểm tra với:** GroupDocs.Signature 23.12 (Java)  
**Tác giả:** GroupDocs  

```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

```java
import com.groupdocs.signature.Signature;

public class QuickTest {
    public static void main(String[] args) {
        try {
            Signature signature = new Signature("test-document.pdf");
            System.out.println("GroupDocs.Signature is ready to go!");
        } catch (Exception e) {
            System.err.println("Setup issue: " + e.getMessage());
        }
    }
}
```

```java
String filePath = "YOUR_DOCUMENT_DIRECTORY/sample.pdf";
Signature signature = new Signature(filePath);
```

```java
import com.groupdocs.signature.options.sign.BarcodeSignOptions;
import com.groupdocs.signature.domain.barcodes.BarcodeTypes;

BarcodeSignOptions options = new BarcodeSignOptions("12345678");
options.setEncodeType(BarcodeTypes.Code128);
```

```java
import com.groupdocs.signature.domain.enums.MeasureType;
import com.groupdocs.signature.domain.Padding;

// Use percentages instead of fixed pixels
options.setLocationMeasureType(MeasureType.Percents);
options.setLeft(5);  // 5% from the left edge
options.setTop(5);   // 5% from the top

// Size it proportionally too
options.setSizeMeasureType(MeasureType.Percents);
options.setWidth(10);  // 10% of page width
options.setHeight(5);  // 5% of page height

// Add some breathing room with margins
Padding margins = new Padding();
margins.setLeft(1);
margins.setTop(1);
margins.setRight(1);
options.setMargin(margins);
```

```java
String outputFilePath = "YOUR_OUTPUT_DIRECTORY/SignWithPercents/sample_signed.pdf";
signature.sign(outputFilePath, options);
```

```java
Path outputPath = Paths.get(outputFilePath);
Files.createDirectories(outputPath.getParent());
signature.sign(outputFilePath, options);
```

```java
try {
    signature.sign(outputFilePath, options);
    System.out.println("PDF signed successfully at: " + outputFilePath);
} catch (Exception e) {
    System.err.println("Signing failed: " + e.getMessage());
    e.printStackTrace();
}
```

```java
options.setLocationMeasureType(MeasureType.Percents);
options.setLeft(5);  // 5% from left works on any page width
```

```java
options.setWidth(10);  // Give it room to breathe
options.setHeight(5);  // Maintain proper aspect ratio
```

```java
String filePath = "documents/sample.pdf";  // Works on Windows, Mac, Linux
Files.createDirectories(Paths.get("output/signed"));
```

```java
try (Signature signature = new Signature(filePath)) {
    signature.sign(outputFilePath, options);
} // Automatically closes and releases memory
```

```java
import org.junit.Test;
import static org.junit.Assert.*;

public class BarcodeSignatureTest {
    
    @Test
    public void testBarcodeSigning() {
        String testPdf = "test-data/sample.pdf";
        String output = "test-output/signed.pdf";
        
        try (Signature signature = new Signature(testPdf)) {
            BarcodeSignOptions options = new BarcodeSignOptions("TEST123");
            options.setEncodeType(BarcodeTypes.Code128);
            
            signature.sign(output, options);
            
            // Verify output file exists
            assertTrue(new File(output).exists());
            
            // Verify file size increased (signature was added)
            long originalSize = new File(testPdf).length();
            long signedSize = new File(output).length();
            assertTrue(signedSize > originalSize);
            
        } catch (Exception e) {
            fail("Signing should not throw exception: " + e.getMessage());
        }
    }
}
```

```java
List<String> pdfFiles = Arrays.asList("doc1.pdf", "doc2.pdf", "doc3.pdf");

for (String pdfFile : pdfFiles) {
    try (Signature signature = new Signature(pdfFile)) {
        BarcodeSignOptions options = createBarcodeOptions(); // Reuse options
        signature.sign(getOutputPath(pdfFile), options);
    }
}
```

```java
// Create options once, reuse many times
BarcodeSignOptions templateOptions = createStandardBarcodeOptions();

// For each document, clone and customize
BarcodeSignOptions documentOptions = templateOptions.clone();
documentOptions.setText(uniqueDocumentId);
```

## Hướng dẫn liên quan
- [Hướng dẫn Chữ ký Mã vạch Java - Thêm, Xác minh & Quản lý Mã vạch trong PDF](/signature/java/barcode-signatures/)
- [Tạo Chữ ký Mã vạch trong Java – Cập nhật Mã vạch PDF](/signature/java/barcode-signatures/java-groupdocs-signature-barcode-initialize-update/)
- [Cách đọc PDF mã QR bằng Java và GroupDocs.Signature](/signature/java/barcode-signatures/java-pdf-barcode-search-groupdocs-signature-api/)