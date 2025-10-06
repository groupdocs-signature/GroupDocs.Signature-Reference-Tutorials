---
"date": "2025-05-08"
"description": "Tìm hiểu cách ký an toàn hình ảnh DICOM bằng GroupDocs.Signature cho Java. Tăng cường bảo mật tài liệu bằng cách nhúng mã QR và siêu dữ liệu."
"title": "Ký hình ảnh DICOM bằng mã QR và siêu dữ liệu bằng GroupDocs.Signature cho Java"
"url": "/vi/java/image-signatures/sign-dicom-images-groupdocs-signature-java/"
"weight": 1
type: docs
---
# Cách ký hình ảnh DICOM bằng mã QR và siêu dữ liệu bằng GroupDocs.Signature cho Java

## Giới thiệu

Trong bối cảnh chăm sóc sức khỏe số đang phát triển nhanh chóng, việc quản lý dữ liệu bệnh nhân một cách an toàn là vô cùng quan trọng. Hướng dẫn này sẽ hướng dẫn bạn triển khai một giải pháp mạnh mẽ sử dụng GroupDocs.Signature for Java để ký mã QR và siêu dữ liệu cho hình ảnh DICOM (Digital Imaging and Communications in Medicine). Các tính năng này đảm bảo tính xác thực, tăng cường khả năng truy xuất nguồn gốc và duy trì sự tuân thủ bằng cách nhúng thông tin quan trọng trực tiếp vào hình ảnh y tế.

### Những gì bạn sẽ học:
- Cách tích hợp GroupDocs.Signature cho Java vào dự án của bạn.
- Quá trình ký hình ảnh DICOM bằng mã QR.
- Thêm siêu dữ liệu XMP để tăng cường bảo mật tài liệu.
- Truy xuất, xác minh và tìm kiếm chữ ký trong các tệp DICOM.
- Tạo bản xem trước của hình ảnh DICOM đã ký.

Hãy cùng tìm hiểu nhé! Trước khi bắt đầu, hãy đảm bảo bạn có mọi thứ cần thiết để theo dõi một cách liền mạch.

## Điều kiện tiên quyết

Để triển khai các tính năng của GroupDocs.Signature một cách hiệu quả, hãy đảm bảo bạn đáp ứng các điều kiện tiên quyết sau:

### Thư viện và phụ thuộc bắt buộc
- **GroupDocs.Signature cho Java**: Bạn sẽ cần phiên bản 23.12 trở lên của thư viện này.

### Yêu cầu thiết lập môi trường
- **Bộ phát triển Java (JDK)**: Đảm bảo JDK đã được cài đặt trên hệ thống của bạn.
- **IDE**: Sử dụng Môi trường phát triển tích hợp như IntelliJ IDEA hoặc Eclipse.

### Điều kiện tiên quyết về kiến thức
Hiểu biết cơ bản về:
- Lập trình Java và các nguyên tắc hướng đối tượng.
- Công cụ xây dựng Maven hoặc Gradle để quản lý sự phụ thuộc.

## Thiết lập GroupDocs.Signature cho Java

Để bắt đầu sử dụng GroupDocs.Signature, bạn cần thêm nó vào dự án dưới dạng dependency. Sau đây là cách thực hiện bằng các công cụ build khác nhau:

### Maven
Thêm đoạn mã sau vào `pom.xml` tài liệu:
```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

### Gradle
Bao gồm điều này trong `build.gradle` tài liệu:
```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

### Tải xuống trực tiếp
Ngoài ra, bạn có thể tải xuống phiên bản mới nhất từ [GroupDocs.Signature cho các bản phát hành Java](https://releases.groupdocs.com/signature/java/).

#### Các bước xin giấy phép
1. **Dùng thử miễn phí**: Kiểm tra các tính năng bằng bản dùng thử miễn phí có thời hạn.
2. **Giấy phép tạm thời**Xin giấy phép tạm thời để khám phá đầy đủ các tính năng.
3. **Mua**: Mua gói đăng ký nếu bạn cần truy cập lâu dài.

#### Khởi tạo và thiết lập cơ bản

Để khởi tạo GroupDocs.Signature, hãy tạo một phiên bản của `Signature` lớp học:
```java
import com.groupdocs.signature.Signature;

// Khởi tạo đối tượng chữ ký với đường dẫn đến tệp DICOM của bạn
Signature signature = new Signature(filePath);
```

## Hướng dẫn thực hiện

### Ký hình ảnh DICOM bằng mã QR và siêu dữ liệu

#### Tổng quan
Tính năng này cho phép bạn ký hình ảnh DICOM bằng mã QR và thêm siêu dữ liệu XMP, tăng cường bảo mật tài liệu.

#### Bước 1: Thiết lập tùy chọn ký mã QR
```java
import com.groupdocs.signature.domain.Padding;
import com.groupdocs.signature.domain.enums.HorizontalAlignment;
import com.groupdocs.signature.domain.enums.VerticalAlignment;
import com.groupdocs.signature.domain.signatures.QrCodeSignOptions;

Padding padding = new Padding();
padding.setRight(5);
padding.setLeft(5);

QrCodeSignOptions options = new QrCodeSignOptions("Patient #36363393. R: No-Issues");
options.setAllPages(true);
options.setWidth(100);
options.setHeight(100);
options.setVerticalAlignment(VerticalAlignment.Bottom);
options.setHorizontalAlignment(HorizontalAlignment.Right);
options.setMargin(padding);
```
Tại đây, chúng tôi cấu hình giao diện và vị trí của mã QR trên hình ảnh DICOM.

#### Bước 2: Thêm siêu dữ liệu XMP
```java
import com.groupdocs.signature.options.saveoptions.imagessaveoptions.DicomSaveOptions;
import com.groupdocs.signature.options.saveoptions.imagessaveoptions.DicomXmpEntry;
import com.groupdocs.signature.options.saveoptions.imagessaveoptions.DicomXmpType;

DicomSaveOptions dicomSaveOptions = new DicomSaveOptions();
List<DicomXmpEntry> xmpEntries = new ArrayList<>();
xmpEntries.add(new DicomXmpEntry(DicomXmpType.PatientName, "Patient #4"));
dicomSaveOptions.setXmpEntries(xmpEntries);
```
Đoạn mã này thêm siêu dữ liệu vào tệp DICOM, nhúng thêm thông tin bệnh nhân.

#### Bước 3: Ký vào tài liệu
```java
String outputFilePath = YOUR_OUTPUT_DIRECTORY + "/SignDicomImageAdvanced/" + fileName;
signature.sign(outputFilePath, options, dicomSaveOptions);
```
Các `sign` phương pháp này ghi mã QR và siêu dữ liệu vào tệp DICOM của bạn, lưu vào vị trí đã chỉ định.

### Truy xuất thông tin hình ảnh DICOM đã ký

#### Tổng quan
Trích xuất siêu dữ liệu XMP từ hình ảnh DICOM đã ký để xác minh hoặc kiểm tra.
```java
import com.groupdocs.signature.domain.IDocumentInfo;
import com.groupdocs.signature.domain.signatures.MetadataSignature;

IDocumentInfo documentInfo = signature.getDocumentInfo();
for (MetadataSignature item : documentInfo.getMetadataSignatures()) {
    System.out.println(item.toString());
}
```
Mã này sẽ truy xuất và in tất cả chữ ký siêu dữ liệu liên quan đến tệp DICOM.

### Xác minh DICOM đã ký

#### Tổng quan
Xác minh xem có chữ ký mã QR trong hình ảnh DICOM đã ký hay không để xác nhận tính xác thực của nó.
```java
import com.groupdocs.signature.domain.VerificationResult;
import com.groupdocs.signature.options.verify.QrCodeVerifyOptions;
import com.groupdocs.signature.domain.enums.TextMatchType;

QrCodeVerifyOptions verifyOptions = new QrCodeVerifyOptions();
verifyOptions.setAllPages(true);
verifyOptions.setText("Patient #36363393");
verifyOptions.setMatchType(TextMatchType.Contains);

VerificationResult result = signature.verify(verifyOptions);
if (result.isValid()) {
    System.out.println(filePath + " has successfully verified signatures!");
} else {
    System.out.println(filePath + " failed verification process.");
}
```
Bước xác minh này đảm bảo mã QR khớp với các tiêu chí mong đợi, xác nhận tính toàn vẹn của tài liệu.

### Tìm kiếm chữ ký trong DICOM có chữ ký

#### Tổng quan
Xác định vị trí tất cả chữ ký mã QR trong hình ảnh DICOM đã ký để xem xét hoặc kiểm tra chúng.
```java
import com.groupdocs.signature.domain.signatures.QrCodeSignature;
import java.util.List;

List<QrCodeSignature> signatures = signature.search(QrCodeSignature.class);
for (QrCodeSignature qrCodeSignature : signatures) {
    System.out.println("QRCode signature found at page " +
        qrCodeSignature.getPageNumber() + ": " +
        qrCodeSignature.getEncodeType().getTypeName() + ": " +
        qrCodeSignature.getText());
}
```
Tính năng này hữu ích khi quét tất cả chữ ký mã QR trong tài liệu, mang lại khả năng hiển thị toàn diện.

### Tạo bản xem trước của DICOM đã ký

#### Tổng quan
Tạo bản xem trước cho từng trang của hình ảnh DICOM đã ký, cho phép kiểm tra trực quan nhanh chóng mà không cần mở toàn bộ tệp.
```java
import com.groupdocs.signature.options.PreviewOptions;
import java.io.File;
import java.io.FileOutputStream;
import java.nio.file.Paths;

PreviewOptions previewOption = new PreviewOptions(pageNumber -> {
    try {
        String pageFilePath = YOUR_OUTPUT_DIRECTORY + "/SignDicomImageAdvanced/image-" + pageNumber + ".jpg";
        return new FileOutputStream(Paths.get(pageFilePath).toFile());
    } catch (Exception e) {
        throw new RuntimeException(e.getMessage());
    }
});

signature.generatePreview(previewOption);
```
Đoạn mã này tạo bản xem trước hình ảnh cho mỗi trang, có thể hữu ích cho việc xác minh hoặc chia sẻ nhanh chóng.

## Ứng dụng thực tế

GroupDocs.Signature cho Java cung cấp một số ứng dụng thực tế:
- **Chụp ảnh y tế**: Ký và quản lý hình ảnh DICOM của bệnh nhân một cách an toàn bằng mã QR và siêu dữ liệu.
- **Quản lý tài liệu pháp lý**: Nâng cao tính xác thực và tuân thủ của tài liệu trong các thủ tục pháp lý.
- **Dịch vụ tài chính**: Triển khai chữ ký điện tử an toàn trên các tài liệu tài chính nhạy cảm.