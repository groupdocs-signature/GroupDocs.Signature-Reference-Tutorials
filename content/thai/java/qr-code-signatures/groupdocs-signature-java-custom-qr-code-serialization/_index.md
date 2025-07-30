---
"date": "2025-05-08"
"description": "เรียนรู้วิธีการใช้งานการจัดลำดับรหัส QR แบบกำหนดเองพร้อมการเข้ารหัสในไฟล์ PDF ด้วย GroupDocs.Signature สำหรับ Java รักษาความปลอดภัยเอกสารของคุณอย่างมีประสิทธิภาพ"
"title": "นำการสร้างรหัส QR แบบกำหนดเองและการเข้ารหัสไปใช้ใน PDF โดยใช้ GroupDocs.Signature สำหรับ Java"
"url": "/th/java/qr-code-signatures/groupdocs-signature-java-custom-qr-code-serialization/"
"weight": 1
---

# วิธีการนำ QR-Code แบบกำหนดเองและการเข้ารหัสไปใช้ใน PDF โดยใช้ GroupDocs.Signature สำหรับ Java

## การแนะนำ

ในยุคดิจิทัล การลงนามในเอกสารอย่างปลอดภัยเป็นสิ่งสำคัญอย่างยิ่งต่อการรักษาความสมบูรณ์และความถูกต้องของข้อมูล พบกับ GroupDocs.Signature สำหรับ Java ซึ่งเป็นไลบรารีอันทรงพลังที่ออกแบบมาเพื่อเพิ่มลายเซ็นลงในเอกสารได้อย่างง่ายดาย บทช่วยสอนนี้จะแนะนำคุณเกี่ยวกับการใช้งานการจัดลำดับรหัส QR แบบกำหนดเองพร้อมการเข้ารหัสในไฟล์ PDF โดยใช้ GroupDocs.Signature สำหรับ Java

**สิ่งที่คุณจะได้เรียนรู้:**
- วิธีตั้งค่าและกำหนดค่า GroupDocs.Signature สำหรับ Java
- การนำการสร้างซีเรียลไลเซชันแบบกำหนดเองมาใช้กับลายเซ็น QR-code
- การเข้ารหัสข้อมูลแบบอนุกรมภายในรหัส QR
- การใช้คุณสมบัติเหล่านี้เพื่อรักษาความปลอดภัยเอกสารของคุณ

ก่อนที่เราจะเจาะลึกถึงการใช้งานจริง เรามาแน่ใจกันก่อนว่าคุณมีทุกอย่างที่จำเป็นสำหรับการปฏิบัติตาม

### ข้อกำหนดเบื้องต้น

หากต้องการใช้บทช่วยสอนนี้อย่างมีประสิทธิผล โปรดตรวจสอบให้แน่ใจว่าคุณปฏิบัติตามข้อกำหนดเบื้องต้นต่อไปนี้:

1. **ไลบรารีและการอ้างอิงที่จำเป็น:**
   - GroupDocs.Signature สำหรับ Java เวอร์ชัน 23.12 ขึ้นไป
   - Maven หรือ Gradle สำหรับการจัดการการอ้างอิง (ทางเลือก)

2. **ข้อกำหนดการตั้งค่าสภาพแวดล้อม:**
   - ติดตั้ง Java Development Kit (JDK) บนเครื่องของคุณ
   - ความเข้าใจพื้นฐานเกี่ยวกับการเขียนโปรแกรม Java

3. **ความรู้เบื้องต้นที่จำเป็น:**
   - ความคุ้นเคยกับ Java และแนวคิดการเขียนโปรแกรมเชิงวัตถุ
   - ความรู้พื้นฐานในการทำงานกับ PDF ใน Java

## การตั้งค่า GroupDocs.Signature สำหรับ Java

ในการเริ่มต้น คุณต้องตั้งค่าไลบรารี GroupDocs.Signature ในสภาพแวดล้อมโครงการของคุณ

### การติดตั้ง Maven

หากคุณใช้ Maven ให้เพิ่มการอ้างอิงต่อไปนี้ลงในของคุณ `pom.xml` ไฟล์:

```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

### การติดตั้ง Gradle

สำหรับผู้ใช้ Gradle ให้รวมบรรทัดนี้ไว้ใน `build.gradle` ไฟล์:

```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

### ดาวน์โหลดโดยตรง

หรือคุณสามารถดาวน์โหลดเวอร์ชันล่าสุดได้โดยตรงจาก [GroupDocs.Signature สำหรับรุ่น Java](https://releases-groupdocs.com/signature/java/).

#### ขั้นตอนการขอใบอนุญาต
- **ทดลองใช้ฟรี:** เริ่มต้นด้วยการดาวน์โหลดเวอร์ชันทดลองใช้เพื่อทดสอบคุณสมบัติต่างๆ
- **ใบอนุญาตชั่วคราว:** คุณสามารถขอใบอนุญาตชั่วคราวได้หากจำเป็น ซึ่งจะทำให้คุณสามารถประเมินผลิตภัณฑ์ได้โดยไม่มีข้อจำกัดใดๆ
- **ซื้อ:** หากต้องการใช้ในระยะยาว ควรพิจารณาซื้อใบอนุญาตแบบเต็มรูปแบบ

เมื่อติดตั้งแล้ว ให้เริ่มต้น GroupDocs.Signature ในโครงการของคุณ:

```java
import com.groupdocs.signature.Signature;

public class SetupGroupDocs {
    public static void main(String[] args) {
        Signature signature = new Signature("YOUR_DOCUMENT_DIRECTORY/sample.pdf");
        // โค้ดของคุณที่นี่...
    }
}
```

## คู่มือการใช้งาน

ตอนนี้ มาลองดูการใช้งานการสร้างรหัส QR และการเข้ารหัสแบบกำหนดเองด้วย GroupDocs.Signature สำหรับ Java กัน

### คลาสการสร้างซีเรียลไลเซชันแบบกำหนดเองสำหรับลายเซ็น QR-Code

#### ภาพรวม

คุณลักษณะนี้เกี่ยวข้องกับการสร้างคลาสที่จัดการการแปลงข้อมูลเมตาเป็นลายเซ็น QR-code `DocumentSignatureData` คลาสจะเก็บแอตทริบิวต์ต่างๆ เช่น ID, ผู้เขียน, วันที่ลงนาม และปัจจัยข้อมูล

```java
import com.groupdocs.signature.domain.extensions.serialization.FormatAttribute;
import java.math.BigDecimal;
import java.util.Date;

class DocumentSignatureData {
    @FormatAttribute(propertyName = "SignID")
    public String ID;

    public void setID(String value) { 
        this.ID = value; 
    }

    @FormatAttribute(propertyName = "SAuth")
    public String author;

    public void setAuthor(String value) {
        this.author = value;
    }

    @FormatAttribute(propertyName = "SDate", propertyFormat = "yyyy-MM-dd")
    public Date signed = new Date();

    public void setSigned(Date value) {
        this.signed = value;
    }

    @FormatAttribute(propertyName = "SDFact", propertyFormat = "N2")
    public BigDecimal dataFactor = new BigDecimal(0.01);

    public void setDataFactor(BigDecimal value) {
        this.dataFactor = value;
    }
}
```

#### คำอธิบาย
- **คุณสมบัติ:** การ `@FormatAttribute` คำอธิบายประกอบระบุว่าแอตทริบิวต์แต่ละรายการจะถูกแปลงเป็นรหัส QR อย่างไร
  - **บัตรประจำตัว**:ตัวระบุเฉพาะสำหรับลายเซ็น
  - **ผู้เขียน**: ผู้ที่ลงนามในเอกสาร
  - **วันที่ลงนาม**: ประทับเวลาเมื่อลงนามเอกสาร
  - **ปัจจัยข้อมูล**:ข้อมูลตัวเลขเพิ่มเติมที่เชื่อมโยงกับลายเซ็น

### ลายเซ็น QR-Code พร้อมการเข้ารหัสและการจัดลำดับข้อมูลแบบกำหนดเอง

#### ภาพรวม

หัวข้อนี้สาธิตวิธีการลงนามในเอกสารโดยใช้รหัส QR ที่มีข้อมูลอนุกรมที่กำหนดเองและการเข้ารหัส

```java
import com.groupdocs.signature.Signature;
import com.groupdocs.signature.domain.Padding;
import com.groupdocs.signature.domain.enums.HorizontalAlignment;
import com.groupdocs.signature.domain.enums.VerticalAlignment;
import com.groupdocs.signature.domain.extensions.encryption.IDataEncryption;
import com.groupdocs.signature.domain.qrcodes.QrCodeTypes;
import com.groupdocs.signature.exception.GroupDocsSignatureException;
import com.groupdocs.signature.options.sign.QrCodeSignOptions;
import java.io.File;
import java.math.BigDecimal;
import java.util.Date;
import java.util.UUID;

class SignWithQRCodeCustomSerialization {
    String filePath = "YOUR_DOCUMENT_DIRECTORY/sample.pdf"; 
    String outputFilePath = new File("YOUR_OUTPUT_DIRECTORY", "SignedQRCodeCustomSerialization.pdf").getPath();

    public void signDocument() throws Exception {
        Signature signature = new Signature(filePath);

        // นำตรรกะการเข้ารหัสแบบกำหนดเองของคุณไปใช้ที่นี่
        IDataEncryption encryption = new CustomXOREncryption();

        DocumentSignatureData documentSignature = new DocumentSignatureData();
        documentSignature.setID(UUID.randomUUID().toString());
        documentSignature.setAuthor(System.getenv("USERNAME")); 
        documentSignature.setSigned(new Date());
        documentSignature.setDataFactor(new BigDecimal("11.22"));

        QrCodeSignOptions options = new QrCodeSignOptions();
        options.setData(documentSignature);
        options.setEncodeType(QrCodeTypes.QR);
        options.setDataEncryption(encryption);

        // กำหนดค่าการจัดตำแหน่งและลักษณะที่ปรากฏ
        options.setHeight(100);
        options.setWidth(100);
        options.setVerticalAlignment(VerticalAlignment.Bottom);
        options.setHorizontalAlignment(HorizontalAlignment.Right);
        
        Padding padding = new Padding();
        padding.setRight(10);
        padding.setBottom(10);
        options.setMargin(padding);

        signature.sign(outputFilePath, options);
    }
}
```

#### คำอธิบาย
- **การเข้ารหัสแบบกำหนดเอง:** นำตรรกะการเข้ารหัสของคุณเองไปใช้ใน `CustomXOREncryption` หรือใช้วิธีการอื่นใดในการดำเนินการ `IDataEncryption`-
- **ตัวเลือกลายเซ็น:** กำหนดค่าลักษณะและการจัดตำแหน่งของรหัส QR ด้วยตัวเลือกเช่น ความสูง ความกว้าง การเติม ฯลฯ
- **ขั้นตอนการลงนาม:** การ `signature.sign()` วิธีนี้ใช้ลายเซ็น QR-code กับเอกสาร

### เคล็ดลับการแก้ไขปัญหา

- ตรวจสอบให้แน่ใจว่าการอ้างอิงทั้งหมดได้รับการกำหนดค่าอย่างถูกต้องในเครื่องมือสร้างของคุณ (Maven/Gradle)
- ตรวจสอบว่าเส้นทางไฟล์สำหรับเอกสารอินพุตและเอาต์พุตถูกต้อง
- ยืนยันว่าตรรกะการเข้ารหัสแบบกำหนดเองของคุณได้รับการใช้งานและบูรณาการอย่างถูกต้อง

## การประยุกต์ใช้งานจริง

ต่อไปนี้เป็นการใช้งานฟีเจอร์นี้ในโลกแห่งความเป็นจริง:

1. **การลงนามเอกสารทางกฎหมาย:** ลงนามในสัญญาอย่างปลอดภัยโดยมีข้อมูลเมตาฝังอยู่ในรหัส QR เพื่อรับรองความถูกต้อง
2. **การประมวลผลใบแจ้งหนี้:** เพิ่มลายเซ็นเข้ารหัสลงในใบแจ้งหนี้โดยอัตโนมัติเพื่อความปลอดภัยและการติดตามที่เพิ่มขึ้น
3. **การติดตามโลจิสติกส์:** ใช้เอกสารที่ลงนามเพื่อติดตามการจัดส่งโดยฝังตัวระบุเฉพาะและวันที่เวลาภายในรหัส QR
4. **ใบรับรองทางวิชาการ:** ฝังข้อมูลนักเรียนอย่างปลอดภัยลงในใบรับรองดิจิทัลโดยใช้ลายเซ็น QR-code