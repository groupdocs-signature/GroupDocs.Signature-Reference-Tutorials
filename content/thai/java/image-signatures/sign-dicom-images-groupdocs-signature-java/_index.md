---
"date": "2025-05-08"
"description": "เรียนรู้วิธีลงนามในรูปภาพ DICOM อย่างปลอดภัยโดยใช้ GroupDocs.Signature สำหรับ Java เพิ่มความปลอดภัยของเอกสารด้วยการฝังรหัส QR และเมตาดาต้า"
"title": "ลงนามภาพ DICOM ด้วยรหัส QR และข้อมูลเมตาโดยใช้ GroupDocs.Signature สำหรับ Java"
"url": "/th/java/image-signatures/sign-dicom-images-groupdocs-signature-java/"
"weight": 1
type: docs
---
# วิธีการลงนามภาพ DICOM ด้วยรหัส QR และข้อมูลเมตาโดยใช้ GroupDocs.Signature สำหรับ Java

## การแนะนำ

ในโลกการดูแลสุขภาพดิจิทัลที่เปลี่ยนแปลงอย่างรวดเร็ว การจัดการข้อมูลผู้ป่วยอย่างปลอดภัยถือเป็นสิ่งสำคัญยิ่ง บทช่วยสอนนี้จะแนะนำคุณเกี่ยวกับการใช้งานโซลูชันที่มีประสิทธิภาพโดยใช้ GroupDocs.Signature สำหรับ Java เพื่อลงนามภาพดิจิทัลและการสื่อสารทางการแพทย์ (DICOM) ด้วยรหัส QR และเมตาดาต้า ฟีเจอร์เหล่านี้ช่วยรับประกันความถูกต้อง เพิ่มความสามารถในการตรวจสอบย้อนกลับ และรักษาการปฏิบัติตามข้อกำหนดโดยการฝังข้อมูลสำคัญลงในภาพทางการแพทย์โดยตรง

### สิ่งที่คุณจะได้เรียนรู้:
- วิธีการรวม GroupDocs.Signature สำหรับ Java เข้ากับโปรเจ็กต์ของคุณ
- ขั้นตอนการลงนามภาพ DICOM ด้วยรหัส QR
- การเพิ่มข้อมูลเมตา XMP เพื่อเพิ่มความปลอดภัยของเอกสาร
- การดึงข้อมูล ตรวจสอบ และค้นหาลายเซ็นภายในไฟล์ DICOM
- การสร้างตัวอย่างของภาพ DICOM ที่ลงนาม

เริ่มกันเลย! ก่อนที่เราจะเริ่ม เรามาตรวจสอบให้แน่ใจว่าคุณมีทุกสิ่งที่จำเป็นสำหรับการปฏิบัติตามอย่างราบรื่น

## ข้อกำหนดเบื้องต้น

หากต้องการนำคุณลักษณะ GroupDocs.Signature ไปใช้ได้อย่างมีประสิทธิภาพ โปรดตรวจสอบให้แน่ใจว่าคุณปฏิบัติตามข้อกำหนดเบื้องต้นต่อไปนี้:

### ไลบรารีและการอ้างอิงที่จำเป็น
- **GroupDocs.Signature สำหรับ Java**:คุณต้องมีไลบรารีนี้เวอร์ชัน 23.12 ขึ้นไป

### ข้อกำหนดการตั้งค่าสภาพแวดล้อม
- **ชุดพัฒนา Java (JDK)**:ตรวจสอบให้แน่ใจว่าได้ติดตั้ง JDK ไว้ในระบบของคุณแล้ว
- **ไอดีอี**:ใช้สภาพแวดล้อมการพัฒนาแบบบูรณาการ เช่น IntelliJ IDEA หรือ Eclipse

### ข้อกำหนดเบื้องต้นของความรู้
ความเข้าใจพื้นฐานเกี่ยวกับ:
- การเขียนโปรแกรม Java และหลักการเชิงวัตถุ
- เครื่องมือสร้าง Maven หรือ Gradle สำหรับการจัดการการอ้างอิง

## การตั้งค่า GroupDocs.Signature สำหรับ Java

ในการเริ่มต้นใช้งาน GroupDocs.Signature คุณต้องเพิ่ม GroupDocs.Signature เป็นส่วนอ้างอิงในโปรเจกต์ของคุณ คุณสามารถทำได้โดยใช้เครื่องมือสร้างต่างๆ ดังนี้

### เมเวน
เพิ่มข้อความต่อไปนี้ลงในของคุณ `pom.xml` ไฟล์:
```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

### แกรเดิล
รวมสิ่งนี้ไว้ในของคุณ `build.gradle` ไฟล์:
```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

### ดาวน์โหลดโดยตรง
หรือคุณสามารถดาวน์โหลดเวอร์ชันล่าสุดได้จาก [GroupDocs.Signature สำหรับรุ่น Java](https://releases-groupdocs.com/signature/java/).

#### ขั้นตอนการขอใบอนุญาต
1. **ทดลองใช้ฟรี**:ทดสอบคุณสมบัติต่างๆ ด้วยการทดลองใช้ฟรีแบบจำกัดเวลา
2. **ใบอนุญาตชั่วคราว**:รับใบอนุญาตชั่วคราวเพื่อสำรวจศักยภาพเต็มรูปแบบ
3. **ซื้อ**:ซื้อการสมัครสมาชิกหากคุณต้องการการเข้าถึงในระยะยาว

#### การเริ่มต้นและการตั้งค่าขั้นพื้นฐาน

ในการเริ่มต้น GroupDocs.Signature ให้สร้างอินสแตนซ์ของ `Signature` ระดับ:
```java
import com.groupdocs.signature.Signature;

// เริ่มต้นวัตถุลายเซ็นด้วยเส้นทางไปยังไฟล์ DICOM ของคุณ
Signature signature = new Signature(filePath);
```

## คู่มือการใช้งาน

### การลงนามภาพ DICOM ด้วยรหัส QR และข้อมูลเมตา

#### ภาพรวม
ฟีเจอร์นี้ช่วยให้คุณลงนามภาพ DICOM ด้วยรหัส QR และเพิ่มข้อมูลเมตา XMP เพื่อเพิ่มความปลอดภัยของเอกสาร

#### ขั้นตอนที่ 1: ตั้งค่าตัวเลือกการลงนามรหัส QR
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
ที่นี่เราจะกำหนดค่าลักษณะและตำแหน่งของรหัส QR บนภาพ DICOM

#### ขั้นตอนที่ 2: เพิ่มข้อมูลเมตา XMP
```java
import com.groupdocs.signature.options.saveoptions.imagessaveoptions.DicomSaveOptions;
import com.groupdocs.signature.options.saveoptions.imagessaveoptions.DicomXmpEntry;
import com.groupdocs.signature.options.saveoptions.imagessaveoptions.DicomXmpType;

DicomSaveOptions dicomSaveOptions = new DicomSaveOptions();
List<DicomXmpEntry> xmpEntries = new ArrayList<>();
xmpEntries.add(new DicomXmpEntry(DicomXmpType.PatientName, "Patient #4"));
dicomSaveOptions.setXmpEntries(xmpEntries);
```
สไนปเป็ตนี้จะเพิ่มข้อมูลเมตาลงในไฟล์ DICOM โดยฝังข้อมูลผู้ป่วยเพิ่มเติม

#### ขั้นตอนที่ 3: ลงนามในเอกสาร
```java
String outputFilePath = YOUR_OUTPUT_DIRECTORY + "/SignDicomImageAdvanced/" + fileName;
signature.sign(outputFilePath, options, dicomSaveOptions);
```
การ `sign` วิธีการนี้จะเขียนโค้ด QR และข้อมูลเมตาลงในไฟล์ DICOM ของคุณ และบันทึกลงในตำแหน่งที่ระบุ

### การดึงข้อมูลภาพ DICOM ที่ลงนาม

#### ภาพรวม
แยกข้อมูลเมตา XMP จากภาพ DICOM ที่ลงนามเพื่อวัตถุประสงค์ในการตรวจยืนยันหรือตรวจสอบ
```java
import com.groupdocs.signature.domain.IDocumentInfo;
import com.groupdocs.signature.domain.signatures.MetadataSignature;

IDocumentInfo documentInfo = signature.getDocumentInfo();
for (MetadataSignature item : documentInfo.getMetadataSignatures()) {
    System.out.println(item.toString());
}
```
โค้ดนี้จะดึงและพิมพ์ลายเซ็นเมตาข้อมูลทั้งหมดที่เกี่ยวข้องกับไฟล์ DICOM

### การตรวจสอบ DICOM ที่ลงนาม

#### ภาพรวม
ตรวจสอบว่ามีลายเซ็นรหัส QR ในภาพ DICOM ที่ลงนามแล้วเพื่อยืนยันความถูกต้อง
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
ขั้นตอนการตรวจยืนยันนี้จะช่วยให้แน่ใจว่ารหัส QR ตรงตามเกณฑ์ที่คาดหวัง และยืนยันความสมบูรณ์ของเอกสาร

### การค้นหาลายเซ็นใน Signed DICOM

#### ภาพรวม
ระบุตำแหน่งลายเซ็นโค้ด QR ทั้งหมดภายในภาพ DICOM ที่ลงนามเพื่อตรวจสอบหรือตรวจสอบ
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
คุณลักษณะนี้มีประโยชน์สำหรับการสแกนลายเซ็น QR code ทั้งหมดภายในเอกสาร ช่วยให้มองเห็นได้อย่างครอบคลุม

### การสร้างตัวอย่างของ DICOM ที่ลงนาม

#### ภาพรวม
สร้างการแสดงตัวอย่างสำหรับแต่ละหน้าของภาพ DICOM ที่ลงนาม ช่วยให้ตรวจสอบภาพได้อย่างรวดเร็วโดยไม่ต้องเปิดไฟล์ทั้งหมด
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
สไนปเป็ตนี้จะสร้างภาพตัวอย่างสำหรับแต่ละหน้า ซึ่งอาจเป็นประโยชน์สำหรับการตรวจยืนยันหรือการแชร์อย่างรวดเร็ว

## การประยุกต์ใช้งานจริง

GroupDocs.Signature สำหรับ Java นำเสนอแอปพลิเคชันในโลกแห่งความเป็นจริงหลายประการ:
- **การถ่ายภาพทางการแพทย์**:ลงนามและจัดการภาพ DICOM ของผู้ป่วยอย่างปลอดภัยด้วยรหัส QR และข้อมูลเมตา
- **การจัดการเอกสารทางกฎหมาย**:เพิ่มความถูกต้องของเอกสารและความสอดคล้องในกระบวนการทางกฎหมาย
- **บริการทางการเงิน**:นำลายเซ็นอิเล็กทรอนิกส์ที่ปลอดภัยไปใช้กับเอกสารทางการเงินที่ละเอียดอ่อน