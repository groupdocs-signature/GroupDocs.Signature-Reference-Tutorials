---
"date": "2025-05-08"
"description": "เรียนรู้วิธีรักษาความปลอดภัยข้อมูลเมตาของรูปภาพด้วยการเข้ารหัสด้วย GroupDocs.Signature สำหรับ Java รับรองความสมบูรณ์และความถูกต้องของข้อมูลด้วยคำแนะนำทีละขั้นตอน"
"title": "ใช้งานการลงนามและเข้ารหัสข้อมูลเมตาของภาพใน Java ด้วย GroupDocs.Signature"
"url": "/th/java/metadata-signatures/groupdocs-signature-java-image-metadata-encryption/"
"weight": 1
type: docs
---
# ใช้งานการลงนามข้อมูลเมตาของภาพพร้อมการเข้ารหัสใน Java โดยใช้ GroupDocs.Signature

## การแนะนำ

ในโลกดิจิทัลปัจจุบัน การรักษาความปลอดภัยของข้อมูลสำคัญในข้อมูลเมตาของเอกสารถือเป็นสิ่งสำคัญยิ่ง ไม่ว่าจะเป็นการจัดการกับสัญญาทางธุรกิจที่เป็นความลับหรือภาพถ่ายติดบัตรประจำตัว การรักษาความสมบูรณ์และความถูกต้องของข้อมูลเมตาของภาพจะช่วยป้องกันการเข้าถึงและการปลอมแปลงโดยไม่ได้รับอนุญาต **GroupDocs.Signature สำหรับ Java** มอบโซลูชันที่แข็งแกร่งในการลงนามและเข้ารหัสข้อมูลเมตาของภาพอย่างปลอดภัย

บทช่วยสอนนี้จะแนะนำคุณเกี่ยวกับการใช้งานการลงนามเมตาดาต้าของรูปภาพพร้อมการเข้ารหัสใน Java โดยใช้ฟีเจอร์อันทรงพลังของ GroupDocs.Signature การทำตามขั้นตอนเหล่านี้จะช่วยให้คุณผสานฟังก์ชันนี้เข้ากับแอปพลิเคชัน Java ของคุณได้อย่างมีประสิทธิภาพ

**สิ่งที่คุณจะได้เรียนรู้:**
- การลงนามข้อมูลเมตาของเอกสารโดยใช้ GroupDocs.Signature สำหรับ Java
- การนำลายเซ็นวัตถุที่กำหนดเองไปใช้งานพร้อมการเข้ารหัส
- การตั้งค่าสภาพแวดล้อมที่ปลอดภัยโดยใช้การเข้ารหัสคีย์สมมาตร

## ข้อกำหนดเบื้องต้น

ก่อนที่จะเริ่มต้น โปรดตรวจสอบให้แน่ใจว่าได้ปฏิบัติตามข้อกำหนดเบื้องต้นต่อไปนี้:

### ไลบรารีและการอ้างอิงที่จำเป็น:
- **GroupDocs.Signature สำหรับ Java**: ตรวจสอบให้แน่ใจว่าคุณมีเวอร์ชัน 23.12 หรือใหม่กว่า

### ข้อกำหนดการตั้งค่าสภาพแวดล้อม:
- ติดตั้ง Java Development Kit (JDK) บนเครื่องของคุณ
- ใช้ Integrated Development Environment (IDE) เช่น IntelliJ IDEA, Eclipse หรือ NetBeans

### ความรู้เบื้องต้นที่จำเป็น:
- ความเข้าใจพื้นฐานเกี่ยวกับการเขียนโปรแกรม Java
- ความคุ้นเคยกับ Maven หรือ Gradle สำหรับการจัดการการอ้างอิง

## การตั้งค่า GroupDocs.Signature สำหรับ Java

ในการใช้ GroupDocs.Signature ในโครงการของคุณ ให้รวมการอ้างอิงที่จำเป็นดังต่อไปนี้:

### การใช้ Maven
เพิ่มสิ่งนี้ลงในของคุณ `pom.xml` ไฟล์:
```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

### การใช้ Gradle
รวมสิ่งนี้ไว้ในของคุณ `build.gradle` ไฟล์:
```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

### ดาวน์โหลดโดยตรง
หรือดาวน์โหลดเวอร์ชันล่าสุดได้จาก [GroupDocs.Signature สำหรับรุ่น Java](https://releases-groupdocs.com/signature/java/).

#### ขั้นตอนการขอใบอนุญาต
- **ทดลองใช้ฟรี**:เริ่มต้นด้วยการทดลองใช้เพื่อสำรวจคุณสมบัติต่างๆ
- **ใบอนุญาตชั่วคราว**:สมัครเข้ารับการทดสอบอย่างละเอียดหากจำเป็น
- **ซื้อ**:ขอใบอนุญาตใช้ผลิตได้จาก [เอกสารกลุ่ม](https://purchase-groupdocs.com/buy).

## การเริ่มต้นและการตั้งค่าขั้นพื้นฐาน

นี่คือวิธีที่คุณสามารถเริ่มต้น GroupDocs.Signature ในแอปพลิเคชัน Java ของคุณได้:

```java
import com.groupdocs.signature.Signature;

public class InitializeSignature {
    public static void main(String[] args) {
        // เส้นทางไปยังเอกสาร
        String filePath = "path/to/your/document.jpg";
        
        // สร้างอินสแตนซ์ใหม่ของลายเซ็น
        Signature signature = new Signature(filePath);

        System.out.println("GroupDocs.Signature initialized successfully.");
    }
}
```

## คู่มือการใช้งาน

### คุณสมบัติ: ลายเซ็นข้อมูลเมตาพร้อมวัตถุที่กำหนดเอง

#### ภาพรวม
คุณลักษณะนี้ช่วยให้สามารถลงนามข้อมูลเมตาของภาพโดยใช้วัตถุที่กำหนดเองและเข้ารหัสเพื่อความปลอดภัยยิ่งขึ้น โดยรับรองว่าเฉพาะบุคคลที่ได้รับอนุญาตเท่านั้นที่สามารถเข้าถึงหรือแก้ไขข้อมูลเมตาได้

#### การดำเนินการแบบทีละขั้นตอน

##### 1. กำหนดคลาสข้อมูลลายเซ็นเอกสารของคุณ
สร้างคลาสเพื่อเก็บข้อมูลเมตาข้อมูลของคุณ:

```java
import java.math.BigDecimal;
import java.util.Date;

class DocumentSignatureData {
    private String ID;
    private String Author;
    private Date Signed = new Date();
    private BigDecimal DataFactor = new BigDecimal(0.01);

    public String getID() { return ID; }
    public void setID(String value) { ID = value; }

    @FormatAttribute(propertyName = "SignID")
    public final String getAuthor() { return Author; }
    public final void setAuthor(String value) { Author = value; }

    @FormatAttribute(propertyName = "SAuth")
    public final Date getSigned() { return Signed; }
    public final void setSigned(Date value) { Signed = value; }

    @FormatAttribute(propertyName = "SDate", propertyFormat = "yyyy-MM-dd")
    public final BigDecimal getDataFactor() { return DataFactor; }
    public final void setDataFactor(BigDecimal value) { DataFactor = value; }
}
```

##### 2. การนำตรรกะลายเซ็นมาใช้
วิธีการลงนามข้อมูลเมตาโดยใช้การเข้ารหัสมีดังนี้:

```java
import com.groupdocs.signature.Signature;
import com.groupdocs.signature.domain.extensions.encryption.IDataEncryption;
import com.groupdocs.signature.domain.extensions.encryption.SymmetricAlgorithmType;
import com.groupdocs.signature.domain.extensions.encryption.SymmetricEncryption;
import com.groupdocs.signature.domain.signatures.metadata.ImageMetadataSignature;
import com.groupdocs.signature.exception.GroupDocsSignatureException;
import com.groupdocs.signature.options.sign.MetadataSignOptions;

import java.io.File;
import java.nio.file.Paths;
import java.util.UUID;

public class SignMetadataWithCustomObject {
    // กำหนดเส้นทางไฟล์ด้วยตัวแทน
    String filePath = "YOUR_DOCUMENT_DIRECTORY/SampleImage.jpg";
    String outputFilePath = new File("YOUR_OUTPUT_DIRECTORY", 
                                       "SignedImageWithCustomMetadata/SampleImage_signed.jpg").getPath();

    public void run() throws Exception {
        Signature signature = new Signature(filePath);

        // ตั้งค่าคีย์และรหัสผ่านสำหรับการเข้ารหัส
        String key = "1234567890";
        String salt = "1234567890";
        IDataEncryption encryption = new SymmetricEncryption(
            SymmetricAlgorithmType.Rijndael, key, salt);

        MetadataSignOptions options = new MetadataSignOptions();
        DocumentSignatureData documentSignature = new DocumentSignatureData();
        
        // ตั้งค่าคุณสมบัติเมตาข้อมูลที่กำหนดเอง
        documentSignature.setID(UUID.randomUUID().toString());
        documentSignature.setAuthor(System.getenv("USERNAME"));
        documentSignature.setSigned(new Date());
        documentSignature.setDataFactor(new BigDecimal("11.22"));

        ImageMetadataSignature mdDocument = new ImageMetadataSignature(41996, documentSignature);
        mdDocument.setDataEncryption(encryption);

        // เพิ่มลายเซ็นข้อมูลเมตาลงในตัวเลือก
        options.getSignatures().add(mdDocument);

        signature.sign(outputFilePath, options);
    }
}
```

#### ตัวเลือกการกำหนดค่าคีย์
- **การเข้ารหัสแบบสมมาตร**:ใช้อัลกอริทึม Rijndael สำหรับการเข้ารหัส
- **ตัวเลือกการลงชื่อเมตาข้อมูล**: กำหนดค่ากระบวนการลงนามและระบุข้อมูลเมตาที่ต้องการลงนาม

##### เคล็ดลับการแก้ไขปัญหา
- ตรวจสอบให้แน่ใจว่าเส้นทางไฟล์ของคุณถูกต้องและสามารถเข้าถึงได้
- ตรวจสอบว่าตัวแปรสภาพแวดล้อม `USERNAME` ถูกตั้งค่าไว้ถูกต้องแล้ว
- ตรวจสอบว่าเวอร์ชันไลบรารี GroupDocs.Signature ตรงกับการอ้างอิงโค้ดของคุณ

### คุณสมบัติ: ลายเซ็นข้อมูลเมตาพร้อมการเข้ารหัส

#### ภาพรวม
คุณลักษณะนี้มุ่งเน้นไปที่การเข้ารหัสลายเซ็นข้อมูลเมตาเพื่อปกป้องข้อมูลที่ละเอียดอ่อนภายในไฟล์รูปภาพ

#### การดำเนินการแบบทีละขั้นตอน
##### 1. การนำตรรกะการเข้ารหัสมาใช้
วิธีการลงนามข้อมูลเมตาโดยใช้การเข้ารหัสมีดังนี้:
```java
import com.groupdocs.signature.Signature;
import com.groupdocs.signature.domain.extensions.encryption.IDataEncryption;
import com.groupdocs.signature.domain.extensions.encryption.SymmetricAlgorithmType;
import com.groupdocs.signature.domain.extensions.encryption.SymmetricEncryption;
import com.groupdocs.signature.exception.GroupDocsSignatureException;
import com.groupdocs.signature.options.sign.MetadataSignOptions;

import java.io.File;
import java.nio.file.Paths;
import java.util.UUID;

public class SignMetadataWithEncryption {
    // กำหนดเส้นทางไฟล์ด้วยตัวแทน
    String filePath = "YOUR_DOCUMENT_DIRECTORY/SampleImage.jpg";
    String outputFilePath = new File("YOUR_OUTPUT_DIRECTORY", 
                                       "SignedImageWithEncryption/SampleImage_signed.jpg").getPath();

    public void run() throws Exception {
        Signature signature = new Signature(filePath);

        // ตั้งค่าคีย์และรหัสผ่านสำหรับการเข้ารหัส
        String key = "1234567890";
        String salt = "1234567890";
        IDataEncryption encryption = new SymmetricEncryption(
            SymmetricAlgorithmType.Rijndael, key, salt);

        MetadataSignOptions options = new MetadataSignOptions();
        DocumentSignatureData documentSignature = new DocumentSignatureData();
        
        // ตั้งค่าคุณสมบัติเมตาข้อมูลที่กำหนดเอง
        documentSignature.setID(UUID.randomUUID().toString());
        documentSignature.setAuthor(System.getenv("USERNAME"));
        documentSignature.setSigned(new Date());
        documentSignature.setDataFactor(new BigDecimal("11.22"));

        ImageMetadataSignature mdDocument = new ImageMetadataSignature(41996, documentSignature);
        mdDocument.setDataEncryption(encryption);

        // เพิ่มลายเซ็นข้อมูลเมตาลงในตัวเลือก
        options.getSignatures().add(mdDocument);

        signature.sign(outputFilePath, options);
    }
}
```