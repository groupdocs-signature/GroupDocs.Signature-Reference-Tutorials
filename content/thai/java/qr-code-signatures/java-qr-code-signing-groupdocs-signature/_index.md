---
"date": "2025-05-08"
"description": "เรียนรู้วิธีการใช้งานการลงนามโค้ด QR ของ Java โดยใช้ GroupDocs.Signature ยกระดับความปลอดภัยของเอกสาร กำหนดค่าตัวเลือกการลงนาม และใช้การเข้ารหัสแบบกำหนดเองในแอปพลิเคชัน Java ของคุณ"
"title": "คู่มือการลงนามรหัส QR ของ Java และรักษาความปลอดภัยเอกสารของคุณด้วย GroupDocs.Signature"
"url": "/th/java/qr-code-signatures/java-qr-code-signing-groupdocs-signature/"
"weight": 1
type: docs
---
# การนำ Java QR Code Signing ไปใช้กับ GroupDocs.Signature สำหรับ Java

## การแนะนำ

เพิ่มความปลอดภัยให้กับเอกสารดิจิทัลของคุณด้วยการฝังรหัส QR ลงในแอปพลิเคชัน Java ของคุณ การใช้ประโยชน์จาก GroupDocs.Signature สำหรับ Java ช่วยให้คุณมั่นใจได้ถึงความถูกต้องของเอกสารและการตรวจสอบย้อนกลับได้อย่างมีประสิทธิภาพ คู่มือนี้จะแนะนำคุณเกี่ยวกับการสร้างลายเซ็นข้อมูลแบบกำหนดเอง การกำหนดค่าตัวเลือกการลงนามรหัส QR และการรักษาความปลอดภัยของเอกสารของคุณด้วยการเข้ารหัสที่แข็งแกร่ง

**สิ่งที่คุณจะได้เรียนรู้:**
- วิธีการสร้างคลาสลายเซ็นข้อมูลแบบกำหนดเองโดยใช้ GroupDocs.Signature
- การกำหนดค่าตัวเลือกการลงนามรหัส QR ในแอปพลิเคชัน Java
- การลงนามเอกสารด้วยรหัส QR และใช้การเข้ารหัสแบบกำหนดเอง

มาเจาะลึกถึงข้อกำหนดเบื้องต้นและเริ่มผสานฟังก์ชันนี้เข้ากับโปรเจ็กต์ของคุณกันเลย!

## ข้อกำหนดเบื้องต้น

ก่อนที่เราจะเริ่มต้น ให้แน่ใจว่าคุณได้ตั้งค่าไลบรารีและการอ้างอิงที่จำเป็นในสภาพแวดล้อมการพัฒนาของคุณแล้ว

### ไลบรารีและเวอร์ชันที่จำเป็น

ในการใช้งาน GroupDocs.Signature สำหรับ Java ให้รวมการอ้างอิงต่อไปนี้:

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
implementation 'com.groupdocs:groupdocs-signation:23.12'
```

คุณสามารถดาวน์โหลดเวอร์ชันล่าสุดได้โดยตรงจาก [GroupDocs.Signature สำหรับรุ่น Java](https://releases-groupdocs.com/signature/java/).

### ข้อกำหนดการตั้งค่าสภาพแวดล้อม

- ตรวจสอบให้แน่ใจว่าคุณได้ติดตั้ง Java Development Kit (JDK) ที่ใช้งานได้
- ตั้งค่าสภาพแวดล้อมการพัฒนาแบบบูรณาการ (IDE) เช่น IntelliJ IDEA หรือ Eclipse

### ข้อกำหนดเบื้องต้นของความรู้

- ความเข้าใจพื้นฐานเกี่ยวกับการเขียนโปรแกรม Java และแนวคิดเชิงวัตถุ
- ความคุ้นเคยกับการจัดการการอ้างอิงโดยใช้ Maven หรือ Gradle

## การตั้งค่า GroupDocs.Signature สำหรับ Java

ในการเริ่มต้น ให้ตั้งค่า GroupDocs.Signature ในโครงการของคุณโดยปฏิบัติตามคำแนะนำในการติดตั้งด้านบนเพื่อรวมไว้ในการกำหนดค่าการสร้างของคุณ

### ขั้นตอนการขอใบอนุญาต

GroupDocs นำเสนอตัวเลือกการออกใบอนุญาตที่แตกต่างกัน:
- **ทดลองใช้ฟรี**:ทดสอบฟีเจอร์ทั้งหมดโดยไม่มีข้อจำกัด
- **ใบอนุญาตชั่วคราว**:การขอใบอนุญาตเพื่อการประเมินผล
- **ซื้อ**:รับใบอนุญาตเต็มรูปแบบเพื่อใช้งานเชิงพาณิชย์

หลังจากดาวน์โหลดแล้ว ให้เริ่มต้น GroupDocs.Signature ดังต่อไปนี้:

```java
import com.groupdocs.signature.Signature;

class InitializeGroupDocs {
    public static void main(String[] args) {
        Signature signature = new Signature("path/to/your/document");
        // ตอนนี้คุณสามารถเริ่มใช้ลายเซ็นวัตถุเพื่อทำงานกับเอกสารได้แล้ว
    }
}
```

## คู่มือการใช้งาน

มาแบ่งกระบวนการใช้งานออกเป็นส่วนๆ ที่จัดการได้ โดยเน้นที่คุณสมบัติหลัก

### คลาสลายเซ็นข้อมูลที่กำหนดเอง

#### ภาพรวม
สร้างคลาสแบบกำหนดเองเพื่อเก็บข้อมูลลายเซ็น เช่น ID ผู้เขียน วันที่ลงนาม และปัจจัยเพิ่มเติม วิธีนี้ช่วยให้คุณมีข้อมูลเมตาที่จำเป็นทั้งหมดรวมอยู่ในลายเซ็นของคุณ

#### การดำเนินการแบบทีละขั้นตอน

**กำหนดคลาส DocumentSignatureData**

```java
import com.groupdocs.signature.domain.extensions.serialization.FormatAttribute;
import java.util.Date;
import java.math.BigDecimal;

class DocumentSignatureData {
    @FormatAttribute(propertyName = "SignID")
    public String ID; // ตัวระบุเฉพาะสำหรับลายเซ็น
    
    public String getID() { return ID; }
    public void setID(String value) { ID = value; }
    
    @FormatAttribute(propertyName = "SAuth")
    public final String Author; // ผู้เขียนเอกสาร
    
    public final String getAuthor() { return Author; }
    public final void setAuthor(String value) { Author = value; }
    
    @FormatAttribute(propertyName = "SDate", propertyFormat = "yyyy-MM-dd")
    public final Date Signed = new Date(); // วันที่และเวลาในการลงนาม
    
    public final Date getSigned() { return Signed; }
    public final void setSigned(Date value) { Signed = value; }
    
    @FormatAttribute(propertyName = "SDFact", propertyFormat = "N2")
    public final BigDecimal DataFactor = new BigDecimal(0.01); // ปัจจัยข้อมูลเพิ่มเติมสำหรับลายเซ็น
    
    public final BigDecimal getDataFactor() { return DataFactor; }
    public final void setDataFactor(BigDecimal value) { DataFactor = value; }
}
```

**คำอธิบาย:**
- **รูปแบบแอตทริบิวต์**: ใส่คำอธิบายคุณสมบัติเพื่อปรับแต่งการจัดลำดับ
- **คุณสมบัติ**:บันทึกรายละเอียดที่สำคัญ เช่น รหัสเฉพาะ ชื่อผู้เขียน วันที่ลงนาม และปัจจัยข้อมูล

### การกำหนดค่าตัวเลือกการลงนามรหัส QR

#### ภาพรวม
กำหนดค่าตัวเลือกการลงนามรหัส QR เพื่อกำหนดว่ารหัส QR ของคุณจะปรากฏบนเอกสารอย่างไร รวมถึงขนาด การจัดตำแหน่ง และการเติม

#### การดำเนินการแบบทีละขั้นตอน

**กำหนดคลาส QrCodeSignOptionsConfig**

```java
import com.groupdocs.signature.domain.enums.HorizontalAlignment;
import com.groupdocs.signature.domain.enums.VerticalAlignment;
import com.groupdocs.signature.domain.qrcodes.QrCodeTypes;
import com.groupdocs.signature.domain.Padding;
import com.groupdocs.signature.options.sign.QrCodeSignOptions;

class QrCodeSignOptionsConfig {
    public static QrCodeSignOptions setupQrCodeSignOptions(DocumentSignatureData documentSignature) {
        QrCodeSignOptions options = new QrCodeSignOptions();
        
        // แปลงวัตถุข้อมูลที่กำหนดเองเป็นรหัส QR
        options.setData(documentSignature);
        
        // ระบุประเภทรหัส QR
        options.setEncodeType(QrCodeTypes.QR);
        
        // กำหนดค่าการเติมสำหรับการจัดตำแหน่ง
        Padding padding = new Padding();
        padding.setRight(10); // การเติมด้านขวาเป็นพิกเซล
        padding.setBottom(10); // การเติมด้านล่างเป็นพิกเซล
        options.setMargin(padding);
        
        // กำหนดขนาดและตำแหน่งของรหัส QR
        options.setHeight(100);
        options.setWidth(100);
        options.setVerticalAlignment(VerticalAlignment.Bottom);
        options.setHorizontalAlignment(HorizontalAlignment.Right);
        
        return options;
    }
}
```

**คำอธิบาย:**
- **ตัวเลือกลายเซ็น QRCode**:จัดการวิธีการแสดงรหัส QR รวมถึงขนาดและตำแหน่ง
- **การบุนวม**ปรับการจัดตำแหน่งภายในเอกสาร

### การลงนามเอกสารด้วยรหัส QR และการเข้ารหัสแบบกำหนดเอง

#### ภาพรวม
ผสานรวมรหัส QR และการเข้ารหัสแบบกำหนดเองเพื่อลงนามในเอกสารอย่างปลอดภัย รับรองความสมบูรณ์และความลับของข้อมูล

#### การดำเนินการแบบทีละขั้นตอน

**ลงนามในเอกสารด้วยรหัส QR**

```java
import com.groupdocs.signature.Signature;
import com.groupdocs.signature.domain.extensions.encryption.IDataEncryption;
import com.groupdocs.signature.exception.GroupDocsSignatureException;

import java.util.UUID;

class SignDocumentWithQRCode {
    public static void signDocument(String filePath, String outputFilePath) throws Exception {
        try {
            Signature signature = new Signature(filePath);

            // กลยุทธ์การเข้ารหัส XOR แบบกำหนดเอง
            IDataEncryption encryption = new CustomXOREncryption();

            // กำหนดค่าวัตถุข้อมูลลายเซ็นเอกสารที่กำหนดเอง
            DocumentSignatureData documentSignature = new DocumentSignatureData();
            documentSignature.setID(UUID.randomUUID().toString());
            documentSignature.setAuthor(System.getenv("USERNAME"));
            documentSignature.setSigned(new Date());
            documentSignature.setDataFactor(new BigDecimal("11.22"));

            // ตั้งค่าตัวเลือก QR-Code
            QrCodeSignOptions options = QrCodeSignOptionsConfig.setupQrCodeSignOptions(documentSignature);

            // ใช้การเข้ารหัสข้อมูลภายในรหัส QR
            options.setDataEncryption(encryption);

            // ลงนามและบันทึกเอกสาร
            signature.sign(outputFilePath, options);
        } catch (Exception e) {
            throw new GroupDocsSignatureException(e.getMessage());
        }
    }
}
```

**คำอธิบาย:**
- **การเข้ารหัส XORE แบบกำหนดเอง**:นำกลยุทธ์การเข้ารหัสแบบกำหนดเองมาใช้เพื่อรักษาความปลอดภัยข้อมูลรหัส QR
- **รหัสประจำตัว**:สร้างตัวระบุเฉพาะสำหรับลายเซ็นแต่ละรายการ