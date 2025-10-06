---
"date": "2025-05-08"
"description": "เรียนรู้วิธีสร้างลายเซ็น QR Code แบบไดนามิกและปลอดภัยใน Java โดยใช้ GroupDocs.Signature เพิ่มประสิทธิภาพการลงนามเอกสารได้อย่างง่ายดาย"
"title": "สร้างลายเซ็น QR Code ด้วย GroupDocs.Signature สำหรับ Java - คู่มือฉบับสมบูรณ์"
"url": "/th/java/qr-code-signatures/generate-qr-code-signatures-groupdocs-java/"
"weight": 1
type: docs
---
# สร้างลายเซ็น QR Code ด้วย GroupDocs.Signature สำหรับ Java

## การแนะนำ

ในยุคดิจิทัลทุกวันนี้ ความปลอดภัยของเอกสารถือเป็นสิ่งสำคัญยิ่ง ไม่ว่าคุณจะจัดการสัญญา ใบแจ้งหนี้ หรือข้อตกลง การรับรองลายเซ็นที่ถูกต้องและปลอดภัยอาจเป็นเรื่องท้าทาย **GroupDocs.Signature สำหรับ Java** นำเสนอโซลูชันที่แข็งแกร่งเพื่อลดความยุ่งยากในการเพิ่มลายเซ็นดิจิทัลลงในเอกสารของคุณ

บทช่วยสอนนี้จะแนะนำคุณเกี่ยวกับการสร้างลายเซ็น QR Code โดยใช้ GroupDocs.Signature สำหรับ Java ซึ่งช่วยเพิ่มทั้งความปลอดภัยและความยืดหยุ่นในการฝังข้อมูลเพิ่มเติมลงในเอกสารของคุณ เมื่อทำตามนี้ คุณจะได้เรียนรู้:

- การตั้งค่าและกำหนดค่า GroupDocs.Signature สำหรับ Java
- เทคนิคการสร้างลายเซ็น QR code ด้วยการตั้งค่าการจัดตำแหน่งที่แม่นยำ
- การกำหนดค่าตัวเลือกการแสดงตัวอย่างลายเซ็นเพื่อให้มองเห็นเอกสารที่ลงนามได้อย่างครอบคลุม
- การสร้างสตรีมลายเซ็นเพื่อให้แน่ใจว่าการจัดการไฟล์จะราบรื่น

มาเจาะลึกการใช้งานฟังก์ชันเหล่านี้ในแอปพลิเคชัน Java ของคุณกันก่อน ก่อนอื่น มาดูข้อกำหนดเบื้องต้นบางประการเพื่อเริ่มต้นใช้งานได้อย่างราบรื่น

## ข้อกำหนดเบื้องต้น

ก่อนใช้ GroupDocs.Signature สำหรับ Java โปรดตรวจสอบให้แน่ใจว่าคุณปฏิบัติตามข้อกำหนดต่อไปนี้:

- **ห้องสมุดและแหล่งอ้างอิง**: ติดตั้งไลบรารีที่จำเป็น ใช้ Maven หรือ Gradle เพื่อจัดการการอ้างอิง
  
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

- **การตั้งค่าสภาพแวดล้อม**ตรวจสอบให้แน่ใจว่าคุณมีสภาพแวดล้อมการพัฒนา Java ที่มี JDK และ IDE เช่น IntelliJ IDEA หรือ Eclipse

- **ข้อกำหนดเบื้องต้นของความรู้**:ความคุ้นเคยกับแนวคิดการเขียนโปรแกรม Java ถือเป็นสิ่งสำคัญ เช่นเดียวกับการทำความเข้าใจลายเซ็นดิจิทัล

ต่อไปเราจะแนะนำคุณเกี่ยวกับการตั้งค่า GroupDocs.Signature สำหรับ Java ในสภาพแวดล้อมโครงการของคุณ

## การตั้งค่า GroupDocs.Signature สำหรับ Java

หากต้องการเริ่มใช้ GroupDocs.Signature สำหรับ Java ให้ทำตามขั้นตอนเหล่านี้:

1. **เพิ่มการพึ่งพา**:ใช้ Maven หรือ Gradle เพื่อรวมการอ้างอิงดังที่แสดงด้านบน
2. **การได้มาซึ่งใบอนุญาต**-
   - เริ่มต้นด้วยเวอร์ชันทดลองใช้ฟรีโดยดาวน์โหลดจาก [การเปิดตัว GroupDocs](https://releases-groupdocs.com/signature/java/).
   - หากต้องการใช้เป็นเวลานาน ควรพิจารณาซื้อใบอนุญาตหรือสมัครใบอนุญาตชั่วคราวผ่าน [หน้าการซื้อ](https://purchase-groupdocs.com/buy).
3. **การเริ่มต้นขั้นพื้นฐาน**-
   เริ่มต้นไลบรารีในแอปพลิเคชัน Java ของคุณเพื่อเริ่มใช้คุณลักษณะต่างๆ ของมัน

   ```java
   import com.groupdocs.signature.Signature;
   
   // เริ่มต้นวัตถุลายเซ็น
   Signature signature = new Signature("sample.pdf");
   ```

เมื่อตั้งค่า GroupDocs.Signature สำหรับ Java เรียบร้อยแล้ว คุณก็พร้อมที่จะสร้างลายเซ็น QR Code ได้เลย มาดูรายละเอียดกัน

## คู่มือการใช้งาน

### การสร้างลายเซ็น QR Code

การสร้างลายเซ็น QR Code มีหลายขั้นตอนสำคัญ แต่ละขั้นตอนจะช่วยปรับแต่งวิธีการฝังและแสดงข้อมูลในเอกสารของคุณ

#### ภาพรวม
ลายเซ็น QR Code มีความหลากหลาย ช่วยให้คุณสามารถฝังข้อมูลที่ซับซ้อน เช่น ที่อยู่ URL หรือข้อมูลไบนารีลงในเอกสารของคุณได้โดยตรง มาดูวิธีการสร้างลายเซ็นเหล่านี้ด้วยการตั้งค่าการจัดตำแหน่งเฉพาะโดยใช้ GroupDocs.Signature สำหรับ Java กัน

#### การดำเนินการแบบทีละขั้นตอน

##### 1. กำหนดค่าตัวเลือก QR Code
เริ่มต้นด้วยการตั้งค่า `QrCodeSignOptions` วัตถุ ที่นี่คุณจะระบุประเภทของรหัส QR และข้อมูลที่ควรมี

```java
import com.groupdocs.signature.domain.enums.HorizontalAlignment;
import com.groupdocs.signature.domain.enums.VerticalAlignment;
import com.groupdocs.signature.domain.extensions.serialization.Address;
import com.groupdocs.signature.domain.qrcodes.QrCodeTypes;
import com.groupdocs.signature.options.sign.QrCodeSignOptions;

QrCodeSignOptions signOptions = new QrCodeSignOptions();
signOptions.setEncodeType(QrCodeTypes.QR);

// ตั้งค่าข้อมูลด้วยวัตถุที่อยู่
Address address = new Address();
address.setStreet("221B Baker Street");
address.setCity("London");
address.setState("NW");
address.setZIP("NW16XE");
address.setCountry("England");

signOptions.setData(address);
```
**คำอธิบาย**:ที่นี่เราตั้งค่าประเภท QR code ให้เป็นมาตรฐาน `QR` และกรอกข้อมูลที่อยู่ การห่อหุ้มข้อมูลนี้ช่วยให้มั่นใจได้ว่ารายละเอียดสำคัญต่างๆ จะพร้อมใช้งานในเอกสารของคุณ

##### 2. จัดตำแหน่ง QR Code
ปรับการตั้งค่าการจัดตำแหน่งเพื่อควบคุมว่ารหัส QR จะปรากฏที่ใดบนหน้าเอกสาร

```java
signOptions.setHorizontalAlignment(HorizontalAlignment.Left);
signOptions.setVerticalAlignment(VerticalAlignment.Center);
signOptions.setWidth(100);
signOptions.setHeight(100);
```
**คำอธิบาย**: ตัวเลือกการจัดตำแหน่ง (`HorizontalAlignment` และ `VerticalAlignment`) ช่วยให้คุณวางตำแหน่ง QR Code ได้อย่างแม่นยำ ขั้นตอนนี้ช่วยให้มั่นใจได้ว่า QR Code จะสวยงามและจัดวางอย่างมีกลยุทธ์เพื่อการสแกนที่ดีที่สุด

##### 3. กำหนดระยะขอบ
กำหนดระยะขอบรอบรหัส QR เพื่อให้แน่ใจว่าจะไม่สัมผัสกับขอบเอกสาร ซึ่งอาจมีความสำคัญต่อความน่าเชื่อถือในการสแกน

```java
signOptions.setMargin(new Padding(10));
```
**คำอธิบาย**: มีการกำหนดระยะขอบไว้ที่นี่โดยใช้ `Padding`เพื่อให้แน่ใจว่ามีพื้นที่ว่างระหว่างรหัส QR และขอบเอกสาร ช่วยให้สแกนได้ง่ายขึ้น

### การกำหนดค่าตัวเลือกการแสดงตัวอย่างลายเซ็น

การตั้งค่าตัวเลือกการดูตัวอย่างช่วยให้คุณเห็นภาพว่าลายเซ็นจะปรากฏอย่างไรก่อนที่จะสรุปผล ทำได้ดังนี้:

#### ภาพรวม
การตั้งค่าการแสดงตัวอย่างเป็นสิ่งสำคัญสำหรับการตรวจยืนยันลักษณะที่ปรากฏของลายเซ็นของคุณภายในเอกสาร

#### การดำเนินการแบบทีละขั้นตอน

##### 1. สร้างและกำหนดค่า PreviewOptions
ใช้ประโยชน์ `PreviewSignatureOptions` เพื่อกำหนดว่าจะแสดงตัวอย่างลายเซ็นอย่างไร

```java
import com.groupdocs.signature.options.PreviewSignatureOptions;
import com.groupdocs.signature.options.preview.PreviewFormats;
import java.util.UUID;

PreviewSignatureOptions previewOption = new PreviewSignatureOptions(signOptions);
previewOption.setSignatureId(UUID.randomUUID().toString());
previewOption.setPreviewFormat(PreviewFormats.JPEG);
```
**คำอธิบาย**: เดอะ `PreviewSignatureOptions` วัตถุได้รับการกำหนดค่าให้สร้างตัวอย่าง JPEG ของรหัส QR ตัวระบุเฉพาะสำหรับลายเซ็นแต่ละรายการ (`UUID`) ช่วยให้คุณสามารถติดตามและจัดการลายเซ็นหลายรายการได้อย่างมีประสิทธิภาพ

### การสร้างสตรีมลายเซ็น

การสร้างสตรีมช่วยให้แน่ใจว่าเอกสารที่คุณลงนามได้รับการบันทึกหรือส่งอย่างถูกต้อง

#### ภาพรวม
การสร้างสตรีมไฟล์ทำให้สามารถจัดการเอกสารที่ลงนามได้อย่างราบรื่น และรับประกันว่าเอกสารจะถูกจัดเก็บอย่างถูกต้องในไดเร็กทอรีที่ระบุ

#### การดำเนินการแบบทีละขั้นตอน

##### 1. กำหนดไดเรกทอรีเอาต์พุตและสร้างสตรีม
ตรวจสอบให้แน่ใจว่าไดเร็กทอรีเอาต์พุตมีอยู่ก่อนที่จะสร้างสตรีมเพื่อหลีกเลี่ยงข้อผิดพลาดในระหว่างการเขียนไฟล์

```java
import java.io.FileOutputStream;
import java.io.OutputStream;
import java.nio.file.Files;
import java.nio.file.Path;
import java.nio.file.Paths;

public OutputStream generateSignatureStream(PreviewSignatureOptions previewOptions) {
    try {
        Path path = Paths.get("YOUR_OUTPUT_DIRECTORY");
        if (!Files.exists(path)) {
            Files.createDirectories(path);
        }
        
        // สร้างสตรีมเอาท์พุตเพื่อบันทึกเอกสารที่ลงนามแล้ว
        return new FileOutputStream(path.resolve("signedDocument.pdf"));
    } catch (Exception e) {
        e.printStackTrace();
        return null;
    }
}
```
**คำอธิบาย**วิธีการนี้จะตรวจสอบว่ามีไดเรกทอรีที่ระบุอยู่หรือไม่ และสร้างขึ้นหากจำเป็น จากนั้นจะส่งคืนสตรีมเอาต์พุตของไฟล์สำหรับบันทึกเอกสารของคุณ การจัดการไดเรกทอรีช่วยให้มั่นใจได้ว่าเอกสารที่ลงนามแล้วจะถูกจัดเก็บอย่างเป็นระเบียบ

## บทสรุป

เมื่อทำตามคำแนะนำนี้ คุณจะได้เรียนรู้วิธีสร้างลายเซ็น QR Code โดยใช้ GroupDocs.Signature สำหรับ Java ซึ่งช่วยเพิ่มทั้งความปลอดภัยและความยืดหยุ่นในการฝังข้อมูลเพิ่มเติมลงในเอกสารของคุณ ด้วยขั้นตอนเหล่านี้ คุณสามารถนำฟังก์ชันลายเซ็นดิจิทัลไปใช้งานในแอปพลิเคชัน Java ของคุณได้อย่างมั่นใจ

หากต้องการสำรวจเพิ่มเติม โปรดพิจารณาทดลองใช้ลายเซ็นประเภทต่างๆ หรือสำรวจฟีเจอร์อื่นๆ ที่นำเสนอโดย GroupDocs.Signature สำหรับ Java