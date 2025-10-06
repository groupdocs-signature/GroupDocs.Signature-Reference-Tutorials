---
"date": "2025-05-08"
"description": "เรียนรู้วิธีลงนามในรูปภาพอย่างปลอดภัยโดยใช้ GroupDocs.Signature สำหรับ Java รวมถึงการลงนาม QR Code และตัวเลือกการบันทึกรูปภาพขั้นสูง เหมาะสำหรับมืออาชีพทางธุรกิจและนักพัฒนา"
"title": "การลงนามและเพิ่มประสิทธิภาพภาพหลักด้วย GroupDocs.Signature สำหรับ Java"
"url": "/th/java/image-signatures/groupdocs-signature-java-image-optimization/"
"weight": 1
type: docs
---
# การเรียนรู้การลงนามและการเพิ่มประสิทธิภาพภาพด้วย GroupDocs.Signature สำหรับ Java

ในภูมิทัศน์ดิจิทัลปัจจุบัน การลงนามในเอกสารอย่างปลอดภัยถือเป็นสิ่งสำคัญ ไม่ว่าคุณจะเป็นมืออาชีพทางธุรกิจที่รับรองความถูกต้องของสัญญา หรือเป็นบุคคลธรรมดาที่ปกป้องรูปภาพ ความสามารถในการลงนามที่แข็งแกร่งจึงเป็นสิ่งสำคัญอย่างยิ่ง **GroupDocs.Signature สำหรับ Java** นำเสนอฟีเจอร์อันทรงพลังสำหรับการสร้างลายเซ็น QR Code และปรับแต่งตัวเลือกการบันทึกภาพได้อย่างราบรื่น บทช่วยสอนนี้จะแนะนำคุณเกี่ยวกับการใช้ประโยชน์จากฟังก์ชันเหล่านี้เพื่อการจัดการเอกสารอย่างมีประสิทธิภาพ

### สิ่งที่คุณจะได้เรียนรู้:
- การสร้างลายเซ็น QR code บนรูปภาพ
- การกำหนดค่าตัวเลือกการบันทึก BMP, GIF, JPEG, PNG และ TIFF ขั้นสูง
- การนำ GroupDocs.Signature สำหรับ Java ไปใช้ในโครงการของคุณ
- การนำคุณลักษณะเหล่านี้ไปใช้ในโลกแห่งความเป็นจริง

มาแน่ใจว่าคุณได้ตั้งค่าทุกอย่างถูกต้อง!

## ข้อกำหนดเบื้องต้น

ก่อนที่จะเจาะลึกรายละเอียดการใช้งาน ให้แน่ใจว่าคุณมี:

### ไลบรารีและการอ้างอิงที่จำเป็น
ในการใช้ GroupDocs.Signature สำหรับ Java ให้รวมไลบรารีของ GroupDocs.Signature เข้ากับโปรเจกต์ของคุณ นี่คือวิธีการรวมไลบรารีนี้ตามระบบบิลด์ของคุณ:

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

อีกทางเลือกหนึ่งคุณสามารถทำได้ [ดาวน์โหลดเวอร์ชันล่าสุดได้โดยตรง](https://releases.groupdocs.com/signature/java/) หากการตั้งค่าโครงการของคุณต้องการ

### ข้อกำหนดการตั้งค่าสภาพแวดล้อม
- ติดตั้งและกำหนดค่า Java Development Kit (JDK) อย่างถูกต้อง
- IDE เช่น IntelliJ IDEA หรือ Eclipse สำหรับการพัฒนาโค้ด

### ข้อกำหนดเบื้องต้นของความรู้
ขอแนะนำให้มีความเข้าใจพื้นฐานเกี่ยวกับการเขียนโปรแกรม Java ความคุ้นเคยกับเครื่องมือสร้าง Maven/Gradle จะเป็นประโยชน์ แต่ไม่จำเป็น เพราะเราจะแนะนำคุณตลอดขั้นตอนการตั้งค่า

## การตั้งค่า GroupDocs.Signature สำหรับ Java

หากต้องการเริ่มทำงานกับ GroupDocs.Signature ให้ทำตามขั้นตอนเหล่านี้:

1. **ติดตั้งการพึ่งพา**: เพิ่มการอ้างอิงที่เหมาะสมให้กับคุณ `pom.xml` หรือ `build.gradle` ไฟล์ดังแสดงด้านบน
2. **การได้มาซึ่งใบอนุญาต**-
   - รับ [ทดลองใช้ฟรี](https://releases.groupdocs.com/signature/java/) เพื่อสำรวจศักยภาพทั้งหมดของห้องสมุด
   - หากต้องการใช้เป็นเวลานาน โปรดพิจารณาซื้อใบอนุญาตหรือสมัครใบอนุญาตชั่วคราวผ่าน [หน้าการซื้อ](https://purchase-groupdocs.com/buy).

### การเริ่มต้นและการตั้งค่าขั้นพื้นฐาน
หลังจากตั้งค่าสภาพแวดล้อมของคุณแล้ว ให้เริ่มต้น GroupDocs.Signature โดยการสร้างอินสแตนซ์ของ `Signature` ชั้นเรียน นี่คือวิธีการ:

```java
import com.groupdocs.signature.Signature;

public class SignatureSetup {
    public static void main(String[] args) throws Exception {
        // เริ่มต้นด้วยเส้นทางไฟล์ไปยังไดเร็กทอรีเอกสารของคุณ
        String filePath = "YOUR_DOCUMENT_DIRECTORY/sampleImage.jpg";
        Signature signature = new Signature(filePath);
        
        System.out.println("GroupDocs.Signature initialized successfully!");
    }
}
```

## คู่มือการใช้งาน

ตอนนี้คุณมีการตั้งค่าที่จำเป็นแล้ว มาเจาะลึกการใช้งานฟีเจอร์เฉพาะต่างๆ โดยใช้ GroupDocs.Signature สำหรับ Java กัน

### การสร้างลายเซ็น QR Code บนรูปภาพ

#### ภาพรวม
ส่วนนี้จะแนะนำคุณเกี่ยวกับการสร้างลายเซ็น QR Code บนเอกสารรูปภาพ ซึ่งมีประโยชน์อย่างยิ่งสำหรับการฝังข้อมูลเมตาหรือข้อมูลลงในรูปภาพโดยตรงโดยไม่รบกวนผู้อื่น

##### ขั้นตอนที่ 1: เริ่มต้นวัตถุลายเซ็น
ขั้นแรกให้สร้าง `Signature` วัตถุที่ชี้ไปยังไฟล์เป้าหมายของคุณ
```java
String filePath = "YOUR_DOCUMENT_DIRECTORY/sampleImage.jpg";
Signature signature = new Signature(filePath);
```

##### ขั้นตอนที่ 2: ตั้งค่าตัวเลือกการลงนามรหัส QR
กำหนดค่าตัวเลือกสำหรับการลงนามด้วยรหัส QR คุณจะระบุรายละเอียด เช่น เนื้อหาและตำแหน่ง

```java
import com.groupdocs.signature.domain.qrcodes.QrCodeTypes;
import com.groupdocs.signature.options.sign.QrCodeSignOptions;

QrCodeSignOptions signOptions = new QrCodeSignOptions("JohnSmith");
signOptions.setEncodeType(QrCodeTypes.QR);
signOptions.setLeft(100);  // ตำแหน่งจากระยะขอบซ้าย
signOptions.setTop(100);   // ตำแหน่งจากระยะขอบบน
```

##### ขั้นตอนที่ 3: ลงนามในเอกสาร
สุดท้ายนี้ ให้ใช้ลายเซ็น QR code ลงในเอกสารของคุณ

```java
signature.sign("output/imageWithQR.jpg", signOptions);
System.out.println("QR Code Signature Applied Successfully!");
```

### การกำหนดค่าตัวเลือกการบันทึกภาพขั้นสูง

#### การกำหนดค่าตัวเลือกการบันทึก BMP
การกำหนดค่านี้ช่วยให้คุณปรับแต่งวิธีการบันทึกรูปภาพในรูปแบบ BMP ได้ สามารถปรับการบีบอัด ความละเอียด และพารามิเตอร์อื่นๆ ได้ตามต้องการ

```java
import com.groupdocs.signature.options.saveoptions.imagessaveoptions.BmpSaveOptions;
import com.groupdocs.signature.domain.enums.BitmapCompression;

BmpSaveOptions bmpSaveOptions = new BmpSaveOptions();
bmpSaveOptions.setAddMissingExtenstion(true);
bmpSaveOptions.setCompression(BitmapCompression.Rgb);
bmpSaveOptions.setHorizontalResolution(7);
bmpSaveOptions.setVerticalResolution(7);
bmpSaveOptions.setBitsPerPixel(16);
bmpSaveOptions.setOverwriteExistingFiles(true);
```

#### การกำหนดค่าตัวเลือกการบันทึก GIF
เมื่อบันทึกรูปภาพเป็น GIF คุณสามารถควบคุมลักษณะต่างๆ เช่น สีพื้นหลังและการเรียงลำดับจานสีได้

```java
import com.groupdocs.signature.options.saveoptions.imagessaveoptions.GifSaveOptions;

GifSaveOptions gifSaveOptions = new GifSaveOptions();
gifSaveOptions.setBackgroundColorIndex((byte) 2);
gifSaveOptions.setColorResolution((byte) 7);
gifSaveOptions.setDoPaletteCorrection(true);
gifSaveOptions.setTrailer(true);
gifSaveOptions.setInterlaced(false);
gifSaveOptions.setPaletteSorted(true);
gifSaveOptions.setPixelAspectRatio((byte) 24);
gifSaveOptions.setAddMissingExtenstion(true);
```

#### การกำหนดค่าตัวเลือกการบันทึก JPEG
เพิ่มประสิทธิภาพการบันทึกภาพ JPEG ของคุณด้วยการตั้งค่าคุณภาพ ประเภทสี และโหมดการบีบอัด

```java
import com.groupdocs.signature.options.saveoptions.imagessaveoptions.JpegSaveOptions;
import com.groupdocs.signature.domain.enums.JpegCompressionColorMode;
import com.groupdocs.signature.domain.enums.JpegCompressionMode;
import com.groupdocs.signature.domain.enums.JpegRoundingMode;

JpegSaveOptions jpegSaveOptions = new JpegSaveOptions();
jpegSaveOptions.setAddMissingExtenstion(true);
jpegSaveOptions.setBitsPerChannel((byte) 8);
jpegSaveOptions.setColorType(JpegCompressionColorMode.Rgb);
jpegSaveOptions.setComment("signed jpeg file");
jpegSaveOptions.setCompressionType(JpegCompressionMode.Lossless);
jpegSaveOptions.setQuality(100);
jpegSaveOptions.setSampleRoundingMode(JpegRoundingMode.Extrapolate);
```

#### การกำหนดค่าตัวเลือกการบันทึก PNG
ด้วย PNG คุณสามารถกำหนดความลึกของบิตและระดับการบีบอัดให้เหมาะกับความต้องการของคุณได้

```java
import com.groupdocs.signature.options.saveoptions.imagessaveoptions.PngSaveOptions;
import com.groupdocs.signature.domain.enums.PngColorType;
import com.groupdocs.signature.domain.enums.PngFilterType;

PngSaveOptions pngSaveOptions = new PngSaveOptions();
pngSaveOptions.setBitDepth((byte) 8);
pngSaveOptions.setColorType(PngColorType.Grayscale);
pngSaveOptions.setCompressionLevel(9);
pngSaveOptions.setFilterType(PngFilterType.Adaptive);
pngSaveOptions.setProgressive(true);
pngSaveOptions.setAddMissingExtenstion(true);
```

#### การกำหนดค่าตัวเลือกการบันทึก TIFF
สำหรับภาพ TIFF คุณสามารถระบุรูปแบบและการตั้งค่าอื่นๆ ที่เกี่ยวข้องได้

```java
import com.groupdocs.signature.options.saveoptions.imagessaveoptions.TiffSaveOptions;
import com.groupdocs.signature.domain.enums.TiffFormat;

TiffSaveOptions tiffSaveOptions = new TiffSaveOptions();
tiffSaveOptions.setExpectedTiffFormat(TiffFormat.TiffNoCompressionBw);
tiffSaveOptions.setAddMissingExtenstion(true);
```

## การประยุกต์ใช้งานจริง

### กรณีการใช้งานในโลกแห่งความเป็นจริง
1. **การลงนามสัญญา**:ฝังรหัส QR ในภาพสัญญาเพื่อการตรวจยืนยันอย่างรวดเร็ว
2. **สื่อการตลาด**:เพิ่มข้อมูลแบรนด์โดยตรงลงในสื่อส่งเสริมการขายโดยใช้รหัส QR
3. **การเก็บถาวรรูปภาพ**:เพิ่มประสิทธิภาพการตั้งค่าการบันทึกภาพเพื่อรักษาคุณภาพและลดขนาดไฟล์ในระหว่างการเก็บถาวร