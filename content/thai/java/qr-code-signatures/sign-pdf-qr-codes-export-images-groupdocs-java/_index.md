---
"date": "2025-05-08"
"description": "เรียนรู้วิธีเพิ่มความปลอดภัยให้กับเอกสารด้วยการลงนามใน PDF ด้วยรหัส QR และส่งออกเป็นรูปภาพโดยใช้ GroupDocs.Signature สำหรับ Java"
"title": "ลงนาม PDF ด้วยลายเซ็น QR Code และส่งออกเป็นรูปภาพโดยใช้ GroupDocs สำหรับ Java"
"url": "/th/java/qr-code-signatures/sign-pdf-qr-codes-export-images-groupdocs-java/"
"weight": 1
---

# คู่มือครอบคลุมในการลงนามและส่งออก PDF เป็นรูปภาพที่มีรหัส QR โดยใช้ GroupDocs.Signature สำหรับ Java

## การแนะนำ

ในยุคดิจิทัล การรับรองความถูกต้องของเอกสารเป็นสิ่งสำคัญอย่างยิ่งสำหรับทุกภาคส่วน ไม่ว่าจะเป็นภาคการเงิน กฎหมาย และสาธารณสุข การรวมลายเซ็นอิเล็กทรอนิกส์เข้ากับเอกสารจะช่วยประหยัดเวลาและเพิ่มความปลอดภัย บทช่วยสอนนี้จะแนะนำคุณเกี่ยวกับการใช้ GroupDocs.Signature สำหรับ Java เพื่อเพิ่มลายเซ็น QR Code ลงในไฟล์ PDF และส่งออกเป็นรูปภาพพร้อมเส้นขอบแบบกำหนดเอง

**สิ่งที่คุณจะได้เรียนรู้:**
- วิธีการลงนามเอกสารด้วยลายเซ็นรหัส QR โดยใช้ GroupDocs.Signature
- วิธีการส่งออกเอกสารที่ลงนามเป็นรูปภาพด้วยการกำหนดค่าแบบกำหนดเอง
- แนวทางปฏิบัติที่ดีที่สุดสำหรับการเพิ่มประสิทธิภาพการทำงานเมื่อทำงานกับลายเซ็นดิจิทัลใน Java

เริ่มต้นด้วยการตรวจสอบข้อกำหนดเบื้องต้นก่อนที่จะนำฟีเจอร์เหล่านี้ไปใช้!

## ข้อกำหนดเบื้องต้น

ก่อนเริ่มต้น โปรดตรวจสอบให้แน่ใจว่าสภาพแวดล้อมการพัฒนาของคุณได้รับการตั้งค่าอย่างถูกต้อง ในส่วนนี้จะสรุปสิ่งที่คุณจำเป็นต้องรู้และติดตั้งไว้:

### ห้องสมุดที่จำเป็น
คุณจะต้องมีไลบรารี GroupDocs.Signature สำหรับ Java ซึ่งสามารถเพิ่มลงในโปรเจกต์ของคุณโดยใช้ Maven หรือ Gradle ได้ ตรวจสอบให้แน่ใจว่าคุณกำลังใช้งานไลบรารีเวอร์ชัน 23.12

#### การพึ่งพา Maven
```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

#### การนำ Gradle ไปใช้
```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

### ดาวน์โหลดโดยตรง
สำหรับผู้ที่ไม่ต้องการใช้เครื่องมือสร้าง ให้ดาวน์โหลดเวอร์ชันล่าสุดได้จาก [GroupDocs.Signature สำหรับรุ่น Java](https://releases-groupdocs.com/signature/java/).

### ข้อกำหนดการตั้งค่าสภาพแวดล้อม
ตรวจสอบให้แน่ใจว่าสภาพแวดล้อมการพัฒนาของคุณมี:
- JDK 8 ขึ้นไป
- IDE เช่น IntelliJ IDEA หรือ Eclipse

### ข้อกำหนดเบื้องต้นของความรู้
ความคุ้นเคยกับการเขียนโปรแกรม Java และความรู้พื้นฐานเกี่ยวกับการจัดการไฟล์ใน Java จะเป็นประโยชน์ แต่ไม่ใช่ข้อผูกมัด เราจะแนะนำคุณในแต่ละขั้นตอนเพื่อความชัดเจน

## การตั้งค่า GroupDocs.Signature สำหรับ Java

การตั้งค่าโครงการของคุณด้วย GroupDocs.Signature นั้นตรงไปตรงมา:

1. **เพิ่มการพึ่งพา:**
   หากใช้ Maven หรือ Gradle ให้เพิ่มการอ้างอิงตามที่แสดงด้านบนในส่วนข้อกำหนดเบื้องต้น

2. **ขั้นตอนการรับใบอนุญาต:**
   - **ทดลองใช้ฟรี:** เริ่มต้นด้วยการดาวน์โหลดรุ่นทดลองใช้ฟรีจาก [เอกสารกลุ่ม](https://releases-groupdocs.com/signature/java/).
   - **ใบอนุญาตชั่วคราว:** สำหรับการทดสอบแบบขยายเวลาโดยไม่มีข้อจำกัดในการประเมิน ให้ขอใบอนุญาตชั่วคราวได้ที่ [ใบอนุญาตชั่วคราว](https://purchase-groupdocs.com/temporary-license/).
   - **ซื้อ:** หากต้องการใช้ในการผลิต โปรดพิจารณาซื้อใบอนุญาตจาก [ซื้อ GroupDocs](https://purchase-groupdocs.com/buy).

3. **การเริ่มต้นและการตั้งค่าขั้นพื้นฐาน:**

นี่คือตัวอย่างของการเริ่มต้น:
```java
import com.groupdocs.signature.Signature;

public class InitializeSignature {
    public static void main(String[] args) throws Exception {
        // สร้างวัตถุลายเซ็นด้วยเส้นทางไปยังเอกสารของคุณ
        Signature signature = new Signature("YOUR_DOCUMENT_DIRECTORY/sample.pdf");
        
        // ใช้ 'ลายเซ็น' วัตถุนี้เพื่อดำเนินการต่างๆ
    }
}
```

## คู่มือการใช้งาน

### ลายเซ็น QR Code บนเอกสาร

#### ภาพรวม:
การเพิ่มลายเซ็น QR Code ช่วยเพิ่มความปลอดภัยและยืนยันความถูกต้อง ส่วนนี้จะแสดงวิธีการลงนาม PDF ด้วย QR Code โดยใช้ GroupDocs.Signature

##### นำเข้าคลาสที่จำเป็น
```java
import com.groupdocs.signature.Signature;
import com.groupdocs.signature.domain.enums.QrCodeTypes;
import com.groupdocs.signature.options.sign.QrCodeSignOptions;
```

##### ตั้งค่าวัตถุลายเซ็น
เริ่มต้นของคุณ `Signature` วัตถุที่มีเส้นทางไปยังเอกสาร PDF ของคุณ:
```java
Signature signature = new Signature("YOUR_DOCUMENT_DIRECTORY/sample.pdf");
```

##### กำหนดค่าตัวเลือกรหัส QR
สร้างและกำหนดค่า `QrCodeSignOptions` ตัวอย่าง ซึ่งรวมถึงการกำหนดเนื้อหาของรหัส QR ตำแหน่งบนหน้า และระบุเป็นประเภทรหัส QR
```java
QrCodeSignOptions signOptions = new QrCodeSignOptions("JohnSmith"); // ตั้งค่าเนื้อหารหัส QR

signOptions.setEncodeType(QrCodeTypes.QR); // ระบุประเภทรหัส QR
signOptions.setLeft(100); // พิกัด X สำหรับตำแหน่งลายเซ็น
signOptions.setTop(100); // พิกัด Y สำหรับตำแหน่งลายเซ็น
```

##### ลงนามและบันทึกเอกสาร
ใช้ `sign` วิธีการใช้ลายเซ็น QR code และบันทึก:
```java
signature.sign("YOUR_OUTPUT_DIRECTORY/signedWithQRCode.png", signOptions);
```

#### เคล็ดลับการแก้ไขปัญหา:
- ตรวจสอบให้แน่ใจว่าเส้นทางเอกสารของคุณถูกต้อง
- ตรวจสอบว่ามีการเพิ่มการอ้างอิงทั้งหมดอย่างถูกต้อง

### ส่งออกเอกสารเป็นรูปภาพพร้อมการตั้งค่าขอบและหน้าแบบกำหนดเอง

#### ภาพรวม:
ฟีเจอร์นี้สาธิตการส่งออกไฟล์ PDF ที่ลงนามแล้วเป็นรูปภาพ พร้อมกำหนดขอบและการกำหนดค่าหน้าแบบกำหนดเอง เหมาะอย่างยิ่งสำหรับการนำเสนอเอกสารในรูปแบบภาพ

##### นำเข้าคลาสที่จำเป็น
```java
import com.groupdocs.signature.Signature;
import com.groupdocs.signature.domain.Border;
import com.groupdocs.signature.domain.enums.DashStyle;
import com.groupdocs.signature.domain.ImageSaveFileFormat;
import com.groupdocs.signature.options.saveoptions.ExportImageSaveOptions;
import java.awt.Color;
```

##### ตั้งค่าวัตถุลายเซ็น
เช่นเดียวกับก่อนหน้านี้ ให้เริ่มต้นใช้งานของคุณ `Signature` วัตถุที่มีเส้นทางเอกสาร:
```java
Signature signature = new Signature("YOUR_DOCUMENT_DIRECTORY/sample.pdf");
```

##### กำหนดค่าตัวเลือกการส่งออก
สร้างอินสแตนซ์ของ `ExportImageSaveOptions`คุณสามารถกำหนดรูปแบบภาพ คุณสมบัติขอบ และการตั้งค่าหน้าได้ที่นี่
```java
ExportImageSaveOptions exportImageSaveOptions = new ExportImageSaveOptions(ImageSaveFileFormat.Png);

Border border = new Border();
border.setColor(Color.BLUE); // ตั้งค่าสีเส้นขอบเป็นสีน้ำเงิน
border.setWeight(5); // ตั้งค่าความกว้างของเส้นขอบ
border.setDashStyle(DashStyle.Solid); // ตั้งค่ารูปแบบเส้นประสำหรับขอบ
border.setTransparency(0.5); // ตั้งค่าความโปร่งใสของขอบ

exportImageSaveOptions.setBorder(border);
exportImageSaveOptions.setPagesSetup(new PagesSetup());
exportImageSaveOptions.getPagesSetup().setFirstPage(true); // ส่งออกเฉพาะหน้าแรกเท่านั้น
exportImageSaveOptions.setPageColumns(2); // กำหนดจำนวนคอลัมน์สำหรับเค้าโครง
```

##### ลงชื่อและบันทึกเป็นรูปภาพ
ใช้ตัวเลือกการส่งออกเพื่อบันทึกเอกสารของคุณเป็นรูปภาพ:
```java
signature.sign("YOUR_OUTPUT_DIRECTORY/signedAndSavedAsImage.png", null, exportImageSaveOptions);
```

#### เคล็ดลับการแก้ไขปัญหา:
- ตรวจสอบความเข้ากันได้ของรูปแบบไฟล์เอาต์พุต
- ตรวจสอบให้แน่ใจว่าการปรับแต่งทั้งหมดพอดีกับขนาดของหน้า

## การประยุกต์ใช้งานจริง

1. **เอกสารทางกฎหมาย:** ปรับปรุงสัญญาทางกฎหมายด้วยลายเซ็น QR Code เพื่อให้ง่ายต่อการตรวจสอบและจัดเก็บในรูปแบบดิจิทัล
2. **ภาคการศึกษา:** การลงนามใบรับรองทางวิชาการในรูปแบบดิจิทัลและส่งออกเป็นรูปภาพเพื่อเผยแพร่
3. **สัญญาทางธุรกิจ:** ปรับปรุงกระบวนการทำสัญญาให้มีประสิทธิภาพยิ่งขึ้นด้วยการอนุญาตให้มีลายเซ็นอิเล็กทรอนิกส์และสร้างเวอร์ชันรูปภาพที่สามารถแชร์ได้

## การพิจารณาประสิทธิภาพ

เมื่อทำงานกับเอกสารขนาดใหญ่หรือรูปภาพที่มีความละเอียดสูง ควรพิจารณาสิ่งต่อไปนี้:
- เพิ่มประสิทธิภาพการใช้งานหน่วยความจำโดยจัดการทรัพยากรอย่างมีประสิทธิภาพใน Java
- ใช้โครงสร้างข้อมูลที่เหมาะสมเพื่อจัดการงานการประมวลผลเอกสาร
- สร้างโปรไฟล์แอปพลิเคชันของคุณเป็นประจำเพื่อระบุปัญหาคอขวด

## บทสรุป

การปฏิบัติตามคู่มือนี้จะช่วยให้คุณเรียนรู้วิธีการเซ็นชื่อไฟล์ PDF ด้วยรหัส QR และส่งออกเป็นรูปภาพอย่างมีประสิทธิภาพโดยใช้ GroupDocs.Signature สำหรับ Java เครื่องมือเหล่านี้สามารถปรับปรุงความปลอดภัยและการนำเสนอเอกสารของคุณได้อย่างมาก

ขั้นตอนต่อไป ได้แก่ การทดลองใช้ฟีเจอร์เพิ่มเติมที่นำเสนอโดย GroupDocs.Signature หรือการรวมเข้ากับระบบที่ใหญ่กว่า เช่น แพลตฟอร์มการจัดการเอกสาร

## ส่วนคำถามที่พบบ่อย

1. **GroupDocs.Signature คืออะไร?**
   - ไลบรารีที่ครอบคลุมสำหรับการเพิ่มลายเซ็นอิเล็กทรอนิกส์ลงในรูปแบบเอกสารต่างๆ ใน Java เพื่อเพิ่มความปลอดภัยและความถูกต้องของเอกสาร