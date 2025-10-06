---
"date": "2025-05-08"
"description": "เรียนรู้วิธีเพิ่มความปลอดภัยให้กับเอกสารด้วยการใช้งานและตรวจสอบลายเซ็น QR Code ใน Java ด้วย GroupDocs.Signature ทำตามคำแนะนำทีละขั้นตอนนี้เพื่อกระบวนการลงนามที่ปลอดภัย"
"title": "รักษาความปลอดภัยเอกสารของคุณ & ใช้ลายเซ็น QR Code ใน Java โดยใช้ GroupDocs.Signature"
"url": "/th/java/qr-code-signatures/qr-code-signatures-java-groupdocs/"
"weight": 1
type: docs
---
# รักษาความปลอดภัยเอกสารของคุณ: นำลายเซ็น QR Code ไปใช้ใน Java โดยใช้ GroupDocs.Signature

ในยุคดิจิทัลปัจจุบัน การรับรองความปลอดภัยของเอกสารต่างๆ เช่น สัญญา ใบแจ้งหนี้ หรือข้อมูลส่วนบุคคลที่ละเอียดอ่อน ถือเป็นสิ่งสำคัญอย่างยิ่ง แนวทางใหม่ในการยกระดับความปลอดภัยของเอกสารและลดความซับซ้อนของกระบวนการตรวจสอบคือการใช้ลายเซ็น QR Code บทช่วยสอนนี้จะแนะนำคุณเกี่ยวกับการใช้งานและการตรวจสอบลายเซ็น QR Code สำหรับเอกสารของคุณใน Java โดยใช้ GroupDocs.Signature

## สิ่งที่คุณจะได้เรียนรู้
- วิธีการลงนามเอกสารโดยใช้ QR Code
- การตรวจสอบเอกสารที่ลงนามด้วย QR Code
- การค้นหาลายเซ็น QR Code ที่มีอยู่ภายในเอกสาร
- การอัปเดตและการลบลายเซ็น QR Code จากเอกสารของคุณ

มาตั้งค่าสภาพแวดล้อมของคุณและเริ่มต้นกันเลย!

### ข้อกำหนดเบื้องต้น
ก่อนเริ่มต้น ให้แน่ใจว่าคุณมีข้อกำหนดเบื้องต้นดังต่อไปนี้:

#### ไลบรารีและการอ้างอิงที่จำเป็น
คุณต้องใช้ GroupDocs.Signature สำหรับ Java คุณสามารถรวมไฟล์นี้ผ่าน Maven หรือ Gradle หรือดาวน์โหลดโดยตรงก็ได้

**เมเวน**
```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

**แกรเดิล**
```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

**ดาวน์โหลดโดยตรง**
ดาวน์โหลดเวอร์ชันล่าสุดได้จาก [GroupDocs.Signature สำหรับรุ่น Java](https://releases-groupdocs.com/signature/java/).

#### ข้อกำหนดการตั้งค่าสภาพแวดล้อม
- ตรวจสอบให้แน่ใจว่าคุณได้ติดตั้ง Java Development Kit (JDK) 8 หรือสูงกว่า
- ใช้ IDE เช่น IntelliJ IDEA, Eclipse หรือ NetBeans

#### ข้อกำหนดเบื้องต้นของความรู้
ความเข้าใจพื้นฐานเกี่ยวกับการเขียนโปรแกรม Java และการประมวลผลเอกสารจะเป็นประโยชน์

## การตั้งค่า GroupDocs.Signature สำหรับ Java
ในการใช้ GroupDocs.Signature ในโครงการของคุณ ให้ทำตามขั้นตอนเหล่านี้:
1. **การติดตั้ง**:เลือกได้ระหว่าง Maven, Gradle หรือดาวน์โหลดโดยตรงตามการตั้งค่าของคุณ
2. **การได้มาซึ่งใบอนุญาต**-
   - เริ่มต้นด้วยการทดลองใช้ฟรีที่มีให้ใน [เว็บไซต์ GroupDocs](https://releases-groupdocs.com/signature/java/).
   - พิจารณาการขอใบอนุญาตชั่วคราวสำหรับการทดสอบและการพัฒนาขยายเวลาจาก [ที่นี่](https://purchase-groupdocs.com/temporary-license/).
3. **การเริ่มต้นขั้นพื้นฐาน**- 
    วิธีการเริ่มต้น GroupDocs.Signature มีดังนี้:

    ```java
    Signature signature = new Signature("YOUR_DOCUMENT_PATH");
    ```

สิ่งนี้เตรียมคุณให้พร้อมสำหรับการใช้งานลายเซ็น QR Code

## คู่มือการใช้งาน

### ลงนามเอกสารด้วยลายเซ็น QR-Code
#### ภาพรวม
การลงนามในเอกสารโดยใช้คิวอาร์โค้ดเกี่ยวข้องกับการฝังรหัสเฉพาะที่ใช้แทนลายเซ็นดิจิทัลของคุณ กระบวนการนี้จะช่วยรักษาความปลอดภัยของเอกสารและช่วยให้ตรวจสอบความถูกต้องได้ง่ายในภายหลัง

##### ขั้นตอนที่ 1: ตั้งค่าตัวเลือกการลงนามของคุณ
```java
import com.groupdocs.signature.Signature;
import com.groupdocs.signature.domain.enums.HorizontalAlignment;
import com.groupdocs.signature.domain.enums.VerticalAlignment;
import com.groupdocs.signature.options.sign.QrCodeSignOptions;

Signature signature = new Signature("YOUR_DOCUMENT_PATH");
QrCodeSignOptions signOptions = new QrCodeSignOptions("John Smith", com.groupdocs.signature.domain.qrcodes.QrCodeTypes.QR);

signOptions.setVerticalAlignment(VerticalAlignment.Top);
signOptions.setHorizontalAlignment(HorizontalAlignment.Center);
signOptions.setWidth(100);
signOptions.setHeight(40);
```
**คำอธิบาย**- `QrCodeSignOptions` ได้รับการกำหนดค่าให้สร้าง QR Code พร้อมข้อความและการจัดวางที่เฉพาะเจาะจง ปรับความกว้างและความสูงได้ตามต้องการ

##### ขั้นตอนที่ 2: ปรับแต่งลักษณะลายเซ็น
```java
import java.awt.Color;

signOptions.setForeColor(Color.RED); // ตั้งค่าสีรหัส QR
com.groupdocs.signature.domain.SignatureFont signatureFont = new com.groupdocs.signature.domain.SignatureFont();
signatureFont.setSize(12);
signatureFont.setFamilyName("Comic Sans MS");
signOptions.setFont(signatureFont);
```
**คำอธิบาย**:การปรับแต่งแบบอักษรและสีจะช่วยให้ระบุภาพได้ดีขึ้น

##### ขั้นตอนที่ 3: ลงนามในเอกสาร
```java
import java.util.ArrayList;
import java.util.List;

List<String> signatureIds = new ArrayList<>();
List<com.groupdocs.signature.domain.BaseSignature> signedSignatures = signature.sign("YOUR_OUTPUT_PATH", signOptions).getSucceeded();

for (com.groupdocs.signature.domain.BaseSignature temp : signedSignatures) {
    signatureIds.add(temp.getSignatureId());
}
```
**คำอธิบาย**ขั้นตอนนี้จะลงนามในเอกสารและจัดเก็บรหัสลายเซ็นเพื่อใช้อ้างอิงในอนาคต

### ตรวจสอบเอกสารด้วยลายเซ็น QR-Code
#### ภาพรวม
การตรวจสอบยืนยันจะช่วยให้มั่นใจได้ว่าเอกสารได้รับการลงนามอย่างถูกต้อง คุณสามารถตรวจสอบลายเซ็น QR Code ในเอกสารได้ดังนี้

##### ขั้นตอนที่ 1: ตั้งค่าตัวเลือกการยืนยัน
```java
import com.groupdocs.signature.Signature;
import com.groupdocs.signature.options.verify.QrCodeVerifyOptions;

Signature signature2 = new Signature("YOUR_OUTPUT_PATH");
QrCodeVerifyOptions verifyOptions = new QrCodeVerifyOptions();

verifyOptions.setEncodeType(QrCodeTypes.QR);
verifyOptions.setText("John Smith"); // ข้อความที่ต้องตรวจสอบ
verifyOptions.setAllPages(false); 
verifyOptions.setPageNumber(1);
```
**คำอธิบาย**:ตัวเลือกการตรวจยืนยันจะระบุประเภท QR Code และข้อความที่ต้องค้นหา เพื่อให้แน่ใจว่าลายเซ็นตรงตามความคาดหวังของคุณ

##### ขั้นตอนที่ 2: ดำเนินการตรวจสอบ
```java
boolean isValid = signature2.verify(verifyOptions).isValid();
System.out.println("Is Signature Valid? " + isValid);
```
**คำอธิบาย**:การดำเนินการนี้จะตรวจสอบว่าเอกสารมี QR Code ที่ถูกต้องตรงตามเกณฑ์ของคุณหรือไม่

### ค้นหาเอกสารสำหรับลายเซ็น QR-Code
#### ภาพรวม
บางครั้งการค้นหาลายเซ็นที่มีอยู่แล้วภายในเอกสารก็เป็นสิ่งจำเป็น คุณสามารถค้นหาลายเซ็นเหล่านั้นได้โดยใช้ GroupDocs.Signature ดังต่อไปนี้

##### ขั้นตอนที่ 1: กำหนดค่าตัวเลือกการค้นหา
```java
import com.groupdocs.signature.domain.signatures.QrCodeSignature;
import com.groupdocs.signature.options.search.QrCodeSearchOptions;

Signature signature2 = new Signature("YOUR_OUTPUT_PATH");
QrCodeSearchOptions searchOptions = new QrCodeSearchOptions();
searchOptions.setAllPages(true);
```
**คำอธิบาย**:การตั้งค่าเครื่องมือนี้จะสแกนทุกหน้าเพื่อหาลายเซ็น QR Code

##### ขั้นตอนที่ 2: ดำเนินการค้นหา
```java
List<QrCodeSignature> signatures = signature2.search(QrCodeSignature.class, searchOptions);

for (QrCodeSignature qrSignature : signatures) {
    System.out.println("Found Signature ID: " + qrSignature.getSignatureId());
}
```
**คำอธิบาย**:การดำเนินการนี้จะดึงลายเซ็น QR Code ทั้งหมดที่พบในเอกสาร

### อัปเดตเอกสารลายเซ็น QR-Code
#### ภาพรวม
การอัปเดตลายเซ็นเกี่ยวข้องกับการเปลี่ยนแปลงคุณสมบัติ เช่น ตำแหน่งหรือขนาด วิธีการมีดังนี้:

##### ขั้นตอนที่ 1: เตรียมลายเซ็นสำหรับการอัปเดต
```java
import com.groupdocs.signature.domain.signatures.QrCodeSignature;
import java.io.ByteArrayOutputStream;

Signature signature2 = new Signature("YOUR_OUTPUT_PATH");
List<QrCodeSignature> signaturesToUpdate = new ArrayList<>();

// โดยถือว่า 'ลายเซ็น' เป็นรายการของวัตถุ QrCodeSignature ที่ได้รับจากการค้นหา
for (QrCodeSignature qrSignature : signatures) {
    qrSignature.setLeft(qrSignature.getLeft() + 100);
    qrSignature.setTop(qrSignature.getTop() + 100);
    qrSignature.setWidth(200);
    qrSignature.setHeight(50);
    signaturesToUpdate.add(qrSignature);
}
```
**คำอธิบาย**:การปรับตำแหน่งและขนาดของลายเซ็นแต่ละรายการ

##### ขั้นตอนที่ 2: อัปเดตเอกสาร
```java
ByteArrayOutputStream outputStream = new ByteArrayOutputStream();
signature2.update(outputStream, signaturesToUpdate);
```
**คำอธิบาย**:เอกสารได้รับการอัปเดตด้วยลายเซ็น QR Code ที่แก้ไขแล้ว

### ลบลายเซ็น QR-Code ของเอกสารด้วย ID
#### ภาพรวม
การลบลายเซ็นอาจจำเป็นหากไม่จำเป็นอีกต่อไปหรือถูกเพิ่มเข้ามาโดยไม่ได้ตั้งใจ นี่คือวิธีที่คุณสามารถลบลายเซ็นโดยใช้รหัสเฉพาะของลายเซ็น

##### ขั้นตอนที่ 1: ระบุลายเซ็นที่จะลบ
```java
import com.groupdocs.signature.domain.SignatureCollection;
import java.util.Arrays;

SignatureCollection signaturesToDelete = signature2.search(QrCodeSignature.class);
Arrays.stream(signaturesToDelete).forEach(signature -> {
    if (signature.getSignatureId().equals("YOUR_SIGNATURE_ID")) {
        signature.delete();
    }
});
```
**คำอธิบาย**:การดำเนินการนี้จะค้นหาและลบลายเซ็น QR Code ตาม ID เฉพาะตัว

## บทสรุป
คู่มือนี้จะแนะนำคุณเกี่ยวกับการรักษาความปลอดภัยเอกสารโดยใช้ลายเซ็น QR code ใน Java ด้วย GroupDocs.Signature เพียงทำตามขั้นตอนเหล่านี้ คุณจะมั่นใจได้ว่าเอกสารของคุณได้รับการลงนามอย่างปลอดภัยและตรวจสอบความถูกต้องได้อย่างง่ายดาย