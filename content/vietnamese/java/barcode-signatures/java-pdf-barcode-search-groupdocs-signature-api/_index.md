---
categories:
- Java Development
- Document Processing
date: '2026-01-26'
description: Tìm hiểu cách trích xuất mã QR từ PDF bằng Java và GroupDocs.Signature.
  Hướng dẫn từng bước với các ví dụ mã, khắc phục sự cố và các trường hợp sử dụng
  thực tế.
keywords: search barcodes in PDF Java, Java barcode verification PDF, GroupDocs barcode
  search tutorial, extract barcode data from PDF Java, Java PDF barcode scanner
lastmod: '2026-01-26'
linktitle: Search PDF Barcodes Java
tags:
- barcode-search
- pdf-processing
- groupdocs
- java-tutorial
- document-verification
title: Cách trích xuất mã QR từ PDF bằng Java – Tìm kiếm mã vạch với GroupDocs.Signature
type: docs
url: /vi/java/barcode-signatures/java-pdf-barcode-search-groupdocs-signature-api/
weight: 1
---

# Cách trích xuất mã QR từ PDF bằng Java

## Giới thiệu

Bạn đã bao giờ cần **trích xuất mã QR từ PDF**—như hàng trăm hoá đơn, nhãn vận chuyển hoặc tài liệu tồn kho? Việc quét thủ công qua các trang là tẻ nhạt và dễ gây lỗi. Dù bạn đang xây dựng hệ thống xử lý tài liệu tự động hay xác thực tính xác thực của sản phẩm, việc tìm kiếm mã vạch một cách hiệu quả trong PDF có thể là thách thức.

Đó là lúc **GroupDocs.Signature for Java** xuất hiện. API mạnh mẽ này biến những giờ làm việc thủ công thành chỉ vài dòng mã. Bạn có thể quét toàn bộ tài liệu, xác định các loại mã vạch cụ thể (như mã QR hoặc Code128), và tự động trích xuất dữ liệu của chúng.

Trong hướng dẫn này, bạn sẽ học cách tìm kiếm chữ ký mã vạch trong tài liệu PDF bằng Java. Chúng tôi sẽ hướng dẫn cài đặt, triển khai và ngay cả cách khắc phục các vấn đề thường gặp. Khi hoàn thành, bạn sẽ có một giải pháp tìm kiếm mã vạch hoạt động, sẵn sàng tích hợp vào dự án ngay lập tức.

**Bạn sẽ học được:**
- Cài đặt GroupDocs.Signature for Java trong vài phút  
- Tìm kiếm chữ ký mã vạch trong tài liệu PDF  
- Cấu hình tùy chọn tìm kiếm để có kết quả chính xác, mục tiêu  
- Xử lý các loại mã vạch khác nhau (mã QR, EAN, Code128, v.v.)  
- Khắc phục các vấn đề thường gặp và tối ưu hiệu suất  

Hãy cùng bắt đầu!

## Câu trả lời nhanh
- **GroupDocs.Signature có thể đọc mã QR từ PDF không?** Có, nó phát hiện QR, Code128, EAN, PDF417 và nhiều hơn nữa.  
- **Tôi có cần giấy phép trả phí không?** Bản dùng thử miễn phí đủ cho phát triển; giấy phép thương mại cần thiết cho môi trường sản xuất.  
- **Yêu cầu phiên bản Java nào?** Java 8 hoặc cao hơn (khuyến nghị Java 11+).  
- **Làm sao giới hạn tìm kiếm ở các trang cụ thể?** Dùng `options.setAllPages(false)` và đặt `options.setPageNumber(page)`.  
- **API có an toàn đa luồng cho xử lý batch không?** Có, tạo các thể hiện `Signature` riêng cho mỗi luồng.

## Tại sao cần tìm kiếm mã vạch trong PDF?

Trước khi đi vào chi tiết kỹ thuật, đây là lý do quan trọng trong các ứng dụng thực tế:

**Các kịch bản kinh doanh phổ biến**
- **Xử lý hoá đơn** – Tự động trích xuất số đơn hàng hoặc mã theo dõi từ hoá đơn của nhà cung cấp.  
- **Quản lý tồn kho** – Quét danh mục sản phẩm và trích xuất mã SKU để cập nhật cơ sở dữ liệu.  
- **Vận chuyển & Logistics** – Xác thực mã theo dõi gói hàng trong manifest vận chuyển.  
- **Xác thực tài liệu** – Kiểm tra tính hợp lệ của tài liệu ký bằng cách kiểm tra mã vạch bảo mật nhúng.  
- **Hồ sơ y tế** – Trích xuất ID bệnh nhân hoặc mã đơn thuốc từ tài liệu y khoa.  

API GroupDocs.Signature thực hiện phần nặng—bạn không cần lo về xử lý ảnh, thuật toán giải mã mã vạch, hay phức tạp khi render PDF. Tất cả đã được tích hợp sẵn.

## Yêu cầu trước

Trước khi bắt đầu tutorial này, hãy chắc chắn bạn đã chuẩn bị đầy đủ:

### Thư viện và phụ thuộc cần thiết

Bạn cần đưa thư viện GroupDocs.Signature vào dự án Java. Dưới đây là cách thêm bằng Maven hoặc Gradle:

**Maven:**  
```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

**Gradle:**  
```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

**Lưu ý:** Luôn kiểm tra phiên bản mới nhất tại [GroupDocs.Signature for Java releases](https://releases.groupdocs.com/signature và tính năng mới.

### Cài đặt môi trường

- **JDK 8 hoặc cao hơn** – GroupDocs.Signature yêu cầu tối thiểu Java 8 (khuyến nghị ( vận chuyển hoặc danh mục sản phẩm là những lựa chọn tốt).

### Kiến thức nền t niệm hướng đối tượng  
- Xử lý ngoại lệ bằng khối `try‑catch`  
- Sử dụng thư viện bên ngoài trong IDE  

Nếu bạn mới với các thư viện Java của bên thứ ba, đ tôi sẽ hướng dẫn từng bước.

## Cài đặt GroupDocs.Signature for Java

Bắt đầu với GroupDocs.Signature chỉ mất vài phút. Dưới đây là quy trình cài đặt đầy đủ:

### Bước 1: Thêm phụ thuộc

Sử dụng Maven hoặc Gradle để đưa thư viện vào (xem mã ở trên). Sau khi thêm phụ thuộc, làm mới dự án để tải các file JAR.

### Bước 2: Nhận giấy phép

GroupDocs cung cấp nhiều tùy chọn cấp phép:

- **Dùng thử miễn phí** – Thích hợp cho việc thử nghiệm. Tải về tại [GroupDocs releases](https://releases.groupdocs.com/signature/java/)  
- **Giấy phép tạm thời** – Nhận 30 ngày truy cập đầy đủ qua [Temporary License Page](https://purchase.groupdocs.com/temporary-license/)  
- **Giấy phép thương mại** – Dành cho môi trường sản xuất, mua tại [GroupDocs Purchase](https://purchase.groupdocs.com/)  

**Mẹo chuyên nghiệp**: Bắt đầu với bản dùng thử để xây dựng proof‑of‑concept, sau đó nâng cấp nếu API đáp ứng nhu cầu của bạn.

### Bước 3: Khởi tạo cơ bản

Dưới đây là cách tạo đối tượng `Signature` để làm việc với PDF:

```java
import com.groupdocs.signature.Signature;

String filePath = "YOUR_DOCUMENT_DIRECTORY/sample_signed.pdf"; // Replace with your PDF path
Signature signature = new Signature(filePath);
```

Lớp `Signature` là điểm vào chính. Nó tải PDF vào bộ nhớ và cung cấp các phương thức để tìm kiếm, xác thực và trích xuất dữ liệu chữ ký (bao gồm cả mã vạch).

**Quan trọng**: Đảm bảo đường dẫn file đúng và PDF tồn tại. Sai lầm phổ biến? Dùng dấu gạch chéo ngược trên Windows mà không escape (`C:\\Documents\\file.pdf` thay vì `C:\Documents\file.pdf`).

## Hướng dẫn triển khai

Bây giờ đến phần thú vị—viết mã để **tìm kiếm mã vạch trong PDF** của bạn.

### Tìm kiếm chữ ký mã vạch trong tài liệu

Phần này chỉ cho bạn cách quét PDF và các chữ ký mã vạch. Chúng tôi sẽ chia thành các bước dễ hiểu, kèm giải thích cho mỗi phần.

#### Bước 1: Khởi tạo đối tượng Signature

Bắt đầu bằng việc tải tài liệu PDF của bạn:

```java
import com.groupdocs.signature.Signature;

String filePath = "YOUR_DOCUMENT_DIRECTORY/sample_signed.pdf"; // Replace with actual file path
Signature signature = new Signature(filePath);
```

**Giải thích:**  
Lớp `Signature` mở PDF và chuẩn bị cho quá trình xử lý. Gi thực từ người dùng, luôn kiểm tra đường dẫn file và xác nhận file tồn tại trước khi tạo đối tượng `Signature`. Điều này ngăn ngừa các lỗi khó hiểu sau này.

#### Bước 2: Tạo BarcodeSearchOptions

Cấu hình cách bạn muốn tìm kiếm mã vạch:

```java
import com.groupdocs.signature.options.search.BarcodeSearchOptions;

// Configure options for searching barcodes
BarcodeSearchOptions options = new BarcodeSearchOptions();
options.setAllPages(true); // Search every page in the document
```

**Các tùy chọn cấu hình chính**

- `setAllPages(true)`: Quét tất cả các trang. ĐặtAllPages(true:** Bạn kiếm khi bạn biết chính xác định dạng cần tìm.

#### Bước 3: Thực thi tìm kiếm và xử lý kết quả

Bây giờ chạy tìm kiếm và xử lý các kết quả:

```java
import com.groupdocs.signature.domain.signatures.BarcodeSignature;
import java.util.List;

try {
    // Execute the barcode search
    List<BarcodeSignature> signatures = signature.search(BarcodeSignature.class, options);
    
    // Check if any barcodes were found
    if (signatures.isEmpty()) {
        System.out.println("No barcode signatures found in the document.");
    } else {
        System.out.println("Found " + signatures.size() + " barcode signature(s):\n");
        
        // Loop through each barcode and display details
        for (BarcodeSignature barcodeSignature : signatures) {
            System.out.println("----------------------------------------");
            System.out.println("Barcode Type: " + barcodeSignature.getEncodeType().getTypeName());
            System.out.println("Barcode Text: " + barcodeSignature.getText());
            System.out.println("Page Number: " + barcodeSignature.getPageNumber());
            System.out.println("Position: X=" + barcodeSignature.getLeft() + 
                             ", Y=" + barcodeSignature.getTop());
            System.out.println("Size: Width=" + barcodeSignature.getWidth() + 
                             ", Height=" + barcodeSignature.getHeight());
            System.out.println("----------------------------------------\n");
        }
    }
} catch (Exception e) {
    System.err.println("Error searching for barcodes: " + e.getMessage());
    e.printStackTrace();
} finally {
    // Always dispose of the signature object to free resources
    if (signature != null) {
        signature.dispose();
    }
}
```

**Giải thích mã**

1. **Thực thi tìm kiếm** – `signature.search()` quét PDFBarcodeSignature`.  
2. **Kiểm tra rỗng** – Xác nhận có tìm thấy mã vạch trước khi lặp ( - **Loại việc xác thực** – `try‑catch` ngăn chương trình sập nếu có sự cố (PDF hỏng, file không tồn tại, …).  
5. **Giải phóng tài nguyên** – Khối `finally` đảm bảo đối tượng `Signature` được giải phóng đúng cách, giải phóng bộ nhớ.

**Ứng dụng thực tế:**  
Giả sử bạn đang xử lý nhãn vận chuyển. Bạn sẽ lấy `barcodeSignature.getText()` (số theo dõi) và lưu vào cơ sở dữ liệu. Số trang cho biết nhãn nào tương ứng với lô hàng nào khi xử lý tài liệu batch.

## Các loại mã vạch được hỗ trợ

GroupDocs.Signature có thể phát hiện nhiều định dạng mã vạch. DUPC‑A chuẩn bán 2D (Matrix)**
- **QR Code** – Phổ biến nhất; dùng cho URL, mật khẩu Wi‑Fi, thông tin thanh toán  
- **Data Matrix** – Định dạng gọn cho các vật phẩm nhỏ (linh kiện điện tử)  
- **PDF417** – Thẻ ID chính phủ, vé máy bay, giấy phép lái xe  
- **Aztec Code** – Vé giao thông  

**Lọc theo loại** – Bạn có thể tăng tốc tìm kiếm bằng cách chỉ định loại mã vạch cần:

```java
import com.groupdocs.signature.domain.barcodes.BarcodeTypes;

BarcodeSearchOptions options = new BarcodeSearchOptions();
options.setEncodeType(BarcodeTypes.QR); // Only search for QR codes
options.setAllPages(true);
```

**Khi nào nên lọc:** Nếu hoá đơn của bạn chỉ chứa mã Code128, việc lọc theo loại sẽ giảm thời gian xử lý 30‑50 % trên tài liệu lớn.

## Các trường hợp sử dụng thực tế

Dưới đây là cách các nhà phát triển đang áp dụng tìm kiếm mã vạch trong môi trường sản xuất:

### 1. Xử lý hoá đơn tự động
**Kịch bản:** Bộ phận kế toán nhận hơn 500 hoá đơn nhà cung cấp mỗi ngày dưới dạng PDF.  
**Giải pháp:** Quét mỗi PDF để tìm mã Code39 chứa số hoá đơn, tự động khớp với đơn đặt hàng trong hệ thống ERP. Điều này loại bỏ nhập liệu thủ công và giảm lỗi.

```java
// Pseudo‑code workflow
for (PDF invoice : invoiceBatch) {
    List<BarcodeSignature> barcodes = searchBarcodes(invoice);
    String invoiceNumber = barcodes.get(0).getText();
    updateERPSystem(invoiceNumber, invoice);
}
```

### 2. Cập nhật tồn kho kho hàng
**Kịch bản:** Kho nhận lô hàng kèm danh sách đóng gói PDF chứa SKU dưới dạng mã EAN13.  
**Giải pháp:** Trích xuất tất cả mã vạch từ danh sách, cập nhật số lượng tồn kho tự động và đánh dấu các sai lệch để kiểm tra.

### 3. Xác thực tài liệu
**Kịch bản:** Các tài liệu pháp lý có mã QR chứa chữ ký mật mã để xác thực.  
**Giải pháp:** Tìm kiếm mã QR trong hợp đồng đã ký, giải mã dữ liệu chữ ký và xác thực với cơ quan chứng thực đáng tin cậy. Điều này đảm bảo tài liệu không bị thay đổi.

### 4. Quản lý hồ sơ y tế
**Kịch bản:** Hồ sơ bệnh nhân trong bệnh viện chứa báo cáo xét nghiệm PDF với mã Code128 cho ID mẫu.  
**Giải pháp:** Tự động trích xuất ID mẫu và liên kết kết quả xét nghiệm với hồ sơ bệnh nhân trong hệ thống HIS.

## Các vấn đề thường gặp và cách khắc phục

Dưới đây là những vấn đề bạn có thể gặp và cách giải quyết:

### Vấn đề 1: “Không tìm thấy mã vạch” (Mặc dù chúng tồn tại)

**Nguyên nhân có thể**
- Độ phân giải ảnh thấp (ảnh mờ, pixel thấp)  
- Mã vạch quá nhỏ trong PDF đã quét  
- Đang tìm kiếm loại mã vạch sai  

**Giải pháp**
1. **Kiểm tra độ phân giải ảnh** – Mã vạch cần ít nhất 200 DPI để phát hiện ổn định. Nên dùng 300 DPI hoặc cao hơn khi quét.  
2. **Bỏ lọc loại** – Đầu tiên tìm kiếm tất cả các loại mã vạch, sau đó thu hẹp khi đã xác định được loại trong tài liệu.  
3. **Xác nhận chất lượng mã vạch** – Mở PDF bằng Adobe Acrobat và phóng to. Nếu bạn thấy mã vạch mờ, API cũng sẽ gặp khó khăn.

### Vấn đề 2: OutOfMemoryError với PDF lớn

**Nguyên nhân:** Tải PDF 500 trang có hình ảnh độ phân giải cao tiêu tốn nhiều bộ nhớ.  

**Giải pháp**
1. **Xử lý trang theo lô** – Thay vì `setAllPages(true)`, xử lý 50 trang một lần:

```java
for (int startPage = 1; startPage <= totalPages; startPage += 50) {
    BarcodeSearchOptions options = new BarcodeSearchOptions();
    options.setPageNumber(startPage);
    options.setPagesSetup(new PagesSetup());
    options.getPagesSetup().setLastPage(Math.min(startPage + 49, totalPages));
    
    List<BarcodeSignature> batchResults = signature.search(BarcodeSignature.class, options);
    // Process results...
}
```

2. **Tăng kích thước heap JVM** – Thêm `-Xmx4g` vào lệnh Java để cấp 4 GB bộ nhớ (tùy chỉnh theo nhu cầu).

### Vấn đề 3: Hiệu năng chậm trên tài liệu đa trang

**Nguyên nhân:** Quét tuần tự tất cả các trang mất thời gian, đặc biệt với các mã vạch phức tạp như PDF417.  

**Giải pháp**
1. **Nhắm mục tiêu các trang cụ thể** – Nếu mã vạch luôn nằm ở trang 1, đặt `options.setAllPages(false)` và `options.setPageNumber(1)`.  
2. **Lưu cache kết quả** – Nếu bạn xử lý cùng một tài liệu nhiều lần, lưu trữ dữ liệu mã vạch để tránh quét lại.  
3. **Sử dụng SSD** – I/O nhanh hơn giảm thời gian tải lên tới 60‑70 % so với HDD.

### Vấn đề 4: Kết quả dương tính giả (Mẫu ngẫu nhiên bị nhận dạng là mã vạch)

**Nguyên nhân:** Bảng, lưới hoặc các đường kẻ có thể bị nhầm thành mã vạch.  

**Giải pháp:** Xác thực kết quả bằng cách kiểm tra định dạng văn bản đã giải mã:

```java
for (BarcodeSignature barcode : signatures) {
    String text = barcode.getText();
    
    // Example: Invoice numbers are always 10 digits
    if (text.matches("\\d{10}")) {
        // Valid invoice number
        processBarcode(barcode);
    } else {
        System.out.println("Skipping invalid barcode: " + text);
    }
}
```

## Mẹo tối ưu hiệu suất cho tài liệu lớn

Xử lý hàng ngàn PDF? Dưới đây là cách giữ tốc độ nhanh:

### 1. Chiến lược xử lý batch

Sử dụng thread pool để xử lý đồng thời nhiều PDF:

```java
ExecutorService executor = Executors.newFixedThreadPool(4); // 4 parallel threads

for (String pdfPath : pdfFiles) {
    executor.submit(() -> {
        try (Signature sig = new Signature(pdfPath)) {
            List<BarcodeSignature> results = sig.search(BarcodeSignature.class, options);
            // Process results...
        } catch (Exception e) {
            e.printStackTrace();
        }
    });
}

executor.shutdown();
executor.awaitTermination(1, TimeUnit.HOURS);
```

**Tăng tốc:** Xử lý 1 000 file giảm từ ~2 giờ xuống ~30 phút trên máy quad‑core.

### 2. Giảm phạm vi tìm kiếm

Nếu mã vạch luôn nằm ở khu vực nhất định, giới hạn hình chữ nhật:

```java
// Only search the top‑right corner where barcodes are typically placed
options.setRectangle(new Rectangle(400, 50, 150, 150)); // X, Y, Width, Height
```

**Tăng tốc:** Nhanh hơn 40‑60 % trên tài liệu có vị trí mã vạch cố định.

### 3. Giám sát sử dụng bộ nhớ

Đối với job batch kéo dài, theo dõi heap và kích hoạt GC khi cần:

```java
Runtime runtime = Runtime.getRuntime();
long usedMemory = runtime.totalMemory() - runtime.freeMemory();

if (usedMemory > (runtime.maxMemory() * 0.8)) {
    System.gc(); // Suggest garbage collection
}
```

## Các thực tiễn tốt nhất

Tuân thủ các hướng dẫn sau để có mã sẵn sàng cho môi trường production:

### 1. Luôn giải phóng đối tượng Signature
Đặt mã trong try‑with‑resources (Java 7+) để tự động đóng tài nguyên:

```java
try (Signature signature = new Signature(filePath)) {
    // Your search code here...
} // Automatically disposed
```

### 2. Xác thực file đầu vào
Trước khi xử lý, kiểm tra file tồn tại và là PDF hợp lệ:

```java
File pdfFile = new File(filePath);
if (!pdfFile.exists() || !pdfFile.canRead()) {
    throw new FileNotFoundException("PDF not found or not readable: " + filePath);
}

// Optional: Verify it's actually a PDF (check magic bytes)
```

### 3. Ghi log kết quả phát hiện mã vạch
Để debug và audit, ghi lại những gì bạn tìm thấy:

```java
Logger logger = Logger.getLogger(BarcodeSearcher.class.getName());

for (BarcodeSignature barcode : signatures) {
    logger.info(String.format("Detected %s barcode '%s' on page %d at (%.2f, %.2f)",
        barcode.getEncodeType().getTypeName(),
        barcode.getText(),
        barcode.getPageNumber(),
        barcode.getLeft(),
        barcode.getTop()));
}
```

### 4. Xử lý đa dạng định dạng mã vạch
Các ngành khác nhau dùng tiêu chuẩn khác. Làm cho code linh hoạt:

```java
switch (barcode.getEncodeType().getTypeName()) {
    case "QR":
        // QR codes might contain URLs or JSON data
        processQRCode(barcode.getText());
        break;
    case "Code128":
        // Code128 typically contains alphanumeric order/tracking numbers
        processTrackingNumber(barcode.getText());
        break;
    default:
        logger.warning("Unexpected barcode type: " + barcode.getEncodeType());
}
```

### 5. Kiểm thử với tài liệu thực tế
Đừng chỉ dùng các PDF mẫu hoàn hảo. Hãy thử với tài liệu thực tế từ production:
- Hoá đơn đã quét có vết cà phê  
- Nhãn vận chuyển fax có nhiễu  
- Ảnh chụp bằng điện thoại di động, chuyển sang PDF  

Điều này sẽ phát hiện các trường hợp góc cạnh mà demo không hiển thị.

## Câu hỏi thường gặp

**H: Có thể trích xuất mã QR từ PDF được bảo mật bằng mật khẩu không?**  
Đ: Có. Mở tài liệu bằng `Signature` sử dụng constructor có mật khẩu, sau đó chạy logic tìm kiếm như bình thường.

**: Làm sao giới hạn tìm kiếm chỉ ở mã QR?**  
Đ: Đặt kiểu mã trong `BarcodeSearchOptions` thành `BarcodeTypes.QR` (xem đoạn mã ở trên).

**H: API có an toàn đa luồng cho xử lý song song không?**  
Đ: Mỗi luồng nên tạo một thể hiện `Signature` riêng. Thư viện được thiết kế để sử dụng đồng thời.

**H: Nếu mã vạch bị xoay, có cần cấu hình gì không?**  
Đ: GroupDocs.Signature tự động phát hiện góc xoay. Không cần cấu hình thêm.

**H: Làm sao cải thiện phát hiện trên các bản quét độ phân giải thấp?**  
Đ: Tăng DPI khi quét (≥300 DPI) và cân nhắc tiền xử lý ảnh (độ tương phản/độ sáng) trước khiới đây nhanh:

 nhận giấy phép.  
- **Triển khai** – Khởi tạo `Signature`, cấu hình `BarcodeSearchOptions`, thực thi tìm kiếm và xử lý kết quả.  
- **Các loại mã vạch** – Hỗ trợ cả 1D (Code128, EAN) và 2D (QR, Data Matrix, PDF417).  
- **Trường hợp thực tế** – Xử lý hoá đơn, cập nhật tồn kho, xác thực tài liệu, quản lý hồ sơ y tế.  
- **Khắc phục** – Giải quyết vấn đề mã vạch không hiện, lỗi bộ nhớ, hiệu năng chậm và dương tính giả.  
- **Hiệu năng** – Xử lý batch, giới hạn phạm vi, giám sát bộ nhớ.  

API GroupDocs.Signature giúp bạn bỏ qua những phức tạp của việc phân tích PDF và giải mã mã vạch, cho phép tập trung vào logic kinh doanh thực sự. Dù bạn đang tự động hoá báo cáo y tế, bạn giờ đã có một giải pháp mạnh mẽ, sẵn sàng cho môi trường production.

---

**Cập nhật lần cuối:** 2026-01-26  
**Kiểm thử với:** GroupDocs.Signature 23.12 for Java  
**Tác giả:** GroupDocs