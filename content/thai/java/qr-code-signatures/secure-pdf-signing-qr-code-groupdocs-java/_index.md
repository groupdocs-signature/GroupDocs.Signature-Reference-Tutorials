---
"date": "2025-05-08"
"description": "เรียนรู้วิธีรักษาความปลอดภัยไฟล์ PDF ด้วยการเข้ารหัส QR Code และลายเซ็นดิจิทัลด้วย GroupDocs.Signature สำหรับ Java ยกระดับความปลอดภัยเอกสารของคุณอย่างมีประสิทธิภาพ"
"title": "ใช้งานการลงนาม PDF ที่ปลอดภัยพร้อมการเข้ารหัส QR Code ใน Java โดยใช้ GroupDocs.Signature"
"url": "/th/java/qr-code-signatures/secure-pdf-signing-qr-code-groupdocs-java/"
"weight": 1
---

# วิธีการใช้การลงนาม PDF ที่ปลอดภัยพร้อมการเข้ารหัส QR Code ใน Java โดยใช้ GroupDocs.Signature

ในยุคดิจิทัลปัจจุบัน การรักษาความปลอดภัยของข้อมูลสำคัญในเอกสารถือเป็นสิ่งสำคัญยิ่ง ภัยคุกคามทางไซเบอร์ที่เพิ่มขึ้นทำให้การเข้ารหัสข้อมูลกลายเป็นส่วนสำคัญในการจัดการเอกสาร บทช่วยสอนนี้จะแนะนำคุณเกี่ยวกับการใช้งานการลงนาม PDF อย่างปลอดภัยโดยใช้การเข้ารหัส QR code ด้วย GroupDocs.Signature สำหรับ Java เมื่ออ่านบทความนี้จบ คุณจะพร้อมผสานรวมฟีเจอร์ความปลอดภัยที่แข็งแกร่งเข้ากับแอปพลิเคชันของคุณ

## สิ่งที่คุณจะได้เรียนรู้:
- ทำความเข้าใจการเข้ารหัสข้อมูลแบบสมมาตรใน Java
- การสร้างคลาสลายเซ็นแบบกำหนดเอง
- การกำหนดค่าลายเซ็น QR-code ด้วยข้อมูลที่กำหนดเองและการจัดตำแหน่ง
- การรวม GroupDocs.Signature เพื่อการลงนาม PDF ที่ปลอดภัย

พร้อมจะดำดิ่งลงไปหรือยัง? มาเริ่มกันเลย!

## ข้อกำหนดเบื้องต้น
ก่อนที่เราจะเริ่ม ให้แน่ใจว่าคุณมีสิ่งต่อไปนี้:
- **ชุดพัฒนา Java (JDK):** เวอร์ชัน 8 ขึ้นไป
- **Maven หรือ Gradle:** สำหรับการจัดการการพึ่งพา เลือกตามการตั้งค่าโครงการของคุณ
- **ความรู้เกี่ยวกับการเขียนโปรแกรม Java:** ความเข้าใจพื้นฐานเกี่ยวกับการเขียนโปรแกรมเชิงวัตถุใน Java

## การตั้งค่า GroupDocs.Signature สำหรับ Java
ในการเริ่มใช้ GroupDocs.Signature คุณจะต้องเพิ่ม GroupDocs.Signature เป็นส่วนอ้างอิงในโปรเจกต์ของคุณ ไลบรารีนี้มีเครื่องมืออันทรงพลังสำหรับการจัดการลายเซ็นดิจิทัลและการเข้ารหัสเอกสาร

### การตั้งค่า Maven
เพิ่มการอ้างอิงต่อไปนี้ให้กับของคุณ `pom.xml` ไฟล์:
```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

### การตั้งค่า Gradle
สำหรับผู้ใช้ Gradle ให้รวมสิ่งนี้ไว้ใน `build.gradle` ไฟล์:
```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

### ดาวน์โหลดโดยตรง
หรือดาวน์โหลดเวอร์ชันล่าสุดได้จาก [GroupDocs.Signature สำหรับรุ่น Java](https://releases-groupdocs.com/signature/java/).

### การได้มาซึ่งใบอนุญาต
คุณสามารถเริ่มต้นด้วยการทดลองใช้ GroupDocs.Signature ฟรีเพื่อประเมินคุณสมบัติต่างๆ หากต้องการใช้งานแบบขยายเวลา โปรดพิจารณาซื้อใบอนุญาตหรือสมัครใบอนุญาตชั่วคราวผ่านเว็บไซต์

## คู่มือการใช้งาน
คู่มือนี้แบ่งออกเป็นส่วนสำคัญๆ ที่ครอบคลุมถึงการเข้ารหัสข้อมูล การสร้างลายเซ็นแบบกำหนดเอง และการกำหนดค่าลายเซ็น QR-code

### การเข้ารหัสข้อมูลด้วยอัลกอริทึมแบบสมมาตร
การเข้ารหัสข้อมูลของคุณช่วยให้มั่นใจได้ว่าข้อมูลจะปลอดภัยในระหว่างการส่งและจัดเก็บ วิธีตั้งค่าการเข้ารหัสแบบสมมาตรโดยใช้ GroupDocs.Signature มีดังนี้

#### การตั้งค่าการเข้ารหัสแบบสมมาตร
1. **แพ็คเกจที่จำเป็นในการนำเข้า:**
   ```java
   import com.groupdocs.signature.domain.extensions.encryption.IDataEncryption;
   import com.groupdocs.signature.domain.extensions.encryption.SymmetricAlgorithmType;
   import com.groupdocs.signature.domain.extensions.encryption.SymmetricEncryption;
   ```
2. **เริ่มต้นวัตถุการเข้ารหัส:**
   ใช้คีย์ที่ปลอดภัยและเกลือเพื่อเข้ารหัส แทนที่ `"YOUR_SECURE_KEY"` ด้วยกุญแจของคุณเอง
   ```java
   String key = "YOUR_SECURE_KEY";
   String salt = "YOUR_SECURE_SALT";

   IDataEncryption encryption = new SymmetricEncryption(
       SymmetricAlgorithmType.Rijndael, 
       key, 
       salt
   );
   ```
   - **SymmetricAlgorithmType.Rijndael:** สิ่งนี้ระบุประเภทของอัลกอริทึมสมมาตรที่จะใช้
   - **คีย์และเกลือ:** ตรวจสอบให้แน่ใจว่าสิ่งเหล่านี้ไม่ซ้ำกันและปลอดภัยสำหรับการใช้งานของคุณ

### คลาสลายเซ็นข้อมูลที่กำหนดเอง
การสร้างคลาสแบบกำหนดเองช่วยให้คุณจัดการคุณสมบัติลายเซ็นได้อย่างมีประสิทธิภาพ ดังต่อไปนี้:

#### การกำหนด `DocumentSignatureData` ระดับ
```java
class DocumentSignatureData {
    private String ID;
    private String Author;
    private Date Signed = new Date();
    private BigDecimal DataFactor = new BigDecimal(0.01);

    public String getID() { return ID; }
    public void setID(String value) { ID = value; }

    public final String getAuthor() { return Author; }
    public final void setAuthor(String value) { Author = value; }

    public final Date getSigned() { return Signed; }
    public final void setSigned(Date value) { Signed = value; }

    public final BigDecimal getDataFactor() { return DataFactor; }
    public final void setDataFactor(BigDecimal value) { DataFactor = value; }
}
```
- **บัตรประจำตัวผู้แต่ง ลงชื่อ :** ฟิลด์เหล่านี้จะเก็บข้อมูลเมตาของลายเซ็น
- **ปัจจัยข้อมูล:** เก็บค่าตัวเลขที่เกี่ยวข้องกับตรรกะของแอปพลิเคชันของคุณ

### ตัวเลือกลายเซ็น QR-Code
รหัส QR นำเสนอวิธีการฝังข้อมูลแบบกะทัดรัด กำหนดค่าด้วยข้อมูลและการเข้ารหัสแบบกำหนดเอง:

#### การตั้งค่าลายเซ็น QR-Code
1. **เริ่มต้น `Signature` วัตถุ:**
   ```java
   import com.groupdocs.signature.Signature;
   
   Signature signature = new Signature("YOUR_DOCUMENT_DIRECTORY");
   ```
2. **กำหนดค่าตัวเลือกรหัส QR:**
   ```java
   import com.groupdocs.signature.domain.qrcodes.QrCodeTypes;
   import com.groupdocs.signature.options.sign.QrCodeSignOptions;
   import java.util.UUID;

   DocumentSignatureData documentSignature = new DocumentSignatureData();
   documentSignature.setID(UUID.randomUUID().toString());
   documentSignature.setAuthor(System.getenv("USERNAME"));
   documentSignature.setDataFactor(new BigDecimal("11.22"));

   QrCodeSignOptions options = new QrCodeSignOptions();
   options.setData(documentSignature);
   options.setEncodeType(QrCodeTypes.QR);
   options.setDataEncryption(encryption); // ใช้การเข้ารหัสวัตถุ
   options.setHeight(100);
   options.setWidth(100);
   options.setVerticalAlignment(com.groupdocs.signature.domain.enums.VerticalAlignment.Bottom);
   options.setHorizontalAlignment(com.groupdocs.signature.domain.enums.HorizontalAlignment.Right);

   import com.groupdocs.signature.domain.Padding;
   Padding padding = new Padding();
   padding.setRight(10);
   padding.setBottom(10);
   options.setMargin(padding);
   ```
   - **ประเภทการเข้ารหัส:** ระบุรูปแบบรหัส QR
   - **การจัดตำแหน่งและระยะขอบ:** ปรับแต่งวิธีการแสดงรหัส QR บนเอกสาร

### ตัวอย่างการใช้งาน
หากต้องการลงนามในเอกสารด้วยตัวเลือกที่กำหนดค่าไว้ ให้ทำดังนี้:
```java
signature.sign("YOUR_OUTPUT_DIRECTORY/QRCodeEncryptedObject.pdf\