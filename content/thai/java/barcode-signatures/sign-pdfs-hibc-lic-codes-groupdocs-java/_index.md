---
categories:
- Document Signing
- Healthcare Integration
date: '2026-05-16'
description: เรียนรู้วิธีสร้าง Data Matrix PDF และเพิ่ม QR code PDF ด้วย GroupDocs.Signature
  สำหรับ Java. คู่มือขั้นตอนโดยละเอียดสำหรับการลงนามเอกสารด้านสุขภาพ
keywords:
- create data matrix pdf
- add qr code pdf
- HIBC barcode Java
lastmod: '2026-05-16'
linktitle: คู่มือ HIBC PDF Signing Java
schemas:
- author: GroupDocs
  dateModified: '2026-05-16'
  description: Learn how to create data matrix PDF and add QR code PDF using GroupDocs.Signature
    for Java. Step‑by‑step guide for healthcare document signing.
  headline: Create Data Matrix PDF with HIBC Barcode in Java
  type: TechArticle
- description: Learn how to create data matrix PDF and add QR code PDF using GroupDocs.Signature
    for Java. Step‑by‑step guide for healthcare document signing.
  name: Create Data Matrix PDF with HIBC Barcode in Java
  steps:
  - name: '**Import the required classes** – these give you access to the signature
      engine and Data Matrix options.'
    text: '**Import the required classes** – these give you access to the signature
      engine and Data Matrix options.'
  - name: '**Instantiate the `Signature` object** with absolute paths for source and
      destination files.'
    text: '**Instantiate the `Signature` object** with absolute paths for source and
      destination files.'
  - name: '**Configure the Data Matrix options** – set the HIBC string, choose `QrCodeTypes.HIBCLICDataMatrix`,
      and define placement coordinates. `QrCodeTypes` enumerates the supported barcode
      formats for HIBC signatures.'
    text: '**Configure the Data Matrix options** – set the HIBC string, choose `QrCodeTypes.HIBCLICDataMatrix`,
      and define placement coordinates. `QrCodeTypes` enumerates the supported barcode
      formats for HIBC signatures.'
  - name: '**Apply the signature** to the PDF.'
    text: '**Apply the signature** to the PDF.'
  - name: '**Dispose of resources** to free file handles and avoid memory leaks.'
    text: '**Dispose of resources** to free file handles and avoid memory leaks.'
  - name: '**Import QR‑specific classes**'
    text: '**Import QR‑specific classes**'
  - name: '**Create and configure QR options** – note the use of `QrCodeTypes.HIBCLICQR`.'
    text: '**Create and configure QR options** – note the use of `QrCodeTypes.HIBCLICQR`.'
  - name: '**Sign the document**'
    text: '**Sign the document**'
  type: HowTo
- questions:
  - answer: Yes, it also supports DOCX, XLSX, PPTX, PNG, JPEG, and TIFF with the same
      barcode‑signing API.
    question: Can GroupDocs.Signature sign file types other than PDF?
  - answer: Verify that your HIBC string follows the exact HIBCC syntax, use the online
      validator, and ensure you’re using the correct `QrCodeTypes` constant for the
      chosen format.
    question: How do I troubleshoot “Invalid barcode content” errors?
  - answer: QR ≈ 4,296 alphanumeric characters, Aztec ≈ 3,832 numeric / 3,067 alphanumeric,
      Data Matrix ≈ 3,116 numeric / 2,335 alphanumeric. Keep codes under 200 characters
      for optimal scan reliability.
    question: What is the maximum data capacity for each HIBC format?
  - answer: Absolutely. Create separate `QrCodeSignOptions` objects with different
      positions and call `signature.sign()` for each. Just ensure they don’t overlap.
    question: Is it possible to embed multiple barcode types in one PDF?
  - answer: No. After the JAR is on the classpath and the license is activated, all
      operations are performed locally.
    question: Do I need an internet connection for signing at runtime?
  type: FAQPage
tags:
- java
- pdf-signing
- hibc
- healthcare
- barcode
- pharmaceutical
title: สร้าง Data Matrix PDF ด้วย HIBC Barcode ใน Java
type: docs
url: /th/java/barcode-signatures/sign-pdfs-hibc-lic-codes-groupdocs-java/
weight: 1
---

# สร้างไฟล์ PDF Data Matrix พร้อมบาร์โค้ด HIBC ใน Java

หากคุณกำลังพัฒนาซอฟต์แวร์โลจิสติกส์ด้านเภสัชกรรมหรือสุขภาพ คุณอาจเคยเจอปัญหาการติดตามด้วยกระดาษ การสูญเสียลายเซ็น และความยุ่งยากในการตรวจสอบ **สร้าง PDF Data Matrix** ที่ฝังบาร์โค้ด HIBC LIC จะช่วยแก้ปัญหาเหล่านี้โดยให้เส้นทางการตรวจสอบที่ทนต่อการดัดแปลงและอ่านด้วยเครื่องจักรซึ่งคงอยู่หลังการพิมพ์ การสแกน และการตรวจสอบตามกฎระเบียบ ในบทแนะนำนี้คุณจะได้เห็นวิธี **เพิ่ม QR code PDF** รวมถึงรูปแบบ Aztec และ Data Matrix โดยใช้ GroupDocs.Signature for Java

## คำตอบด่วน
- **ไลบรารีใดที่จัดการบาร์โค้ด HIBC ใน Java?** GroupDocs.Signature for Java.  
- **รูปแบบบาร์โค้ดใดที่กะทัดรัดที่สุด?** Data Matrix – เหมาะสำหรับป้ายขนาดเล็ก.  
- **ฉันสามารถเพิ่ม QR และ Data Matrix ทั้งสองลงใน PDF เดียวได้หรือไม่?** ได้ เพียงสร้าง `QrCodeSignOptions` แยกกัน.  
- **ฉันต้องการการเชื่อมต่ออินเทอร์เน็ตขณะรันไทม์หรือไม่?** ไม่ ไลบรารีทำงานแบบออฟไลน์เต็มรูปแบบหลังการติดตั้ง.  
- **แนะนำเวอร์ชัน Java ใด?** Java 11+ สำหรับประสิทธิภาพระดับการผลิต.

## การลงเซ็น PDF ด้วยบาร์โค้ด HIBC คืออะไร?
`Signature` class ใน GroupDocs.Signature for Java แทนเอกสาร PDF และให้เมธอดสำหรับฝังบาร์โค้ด HIBC เป็นลายเซ็นดิจิทัล. โดยการลงลายเซ็น PDF ด้วยบาร์โค้ด HIBC คุณจะสร้างบันทึกที่ตรวจสอบได้และแสดงการดัดแปลงที่สามารถสแกนได้ตลอดห่วงโซ่อุปทาน

## ทำไมต้องใช้ Data Matrix และ QR code ร่วมกัน?
GroupDocs.Signature รองรับ **รูปแบบการนำเข้าและส่งออกกว่า 50+** และสามารถประมวลผล PDF หลายร้อยหน้าโดยไม่ต้องโหลดไฟล์ทั้งหมดเข้าสู่หน่วยความจำ. การใช้ Data Matrix สำหรับป้ายที่หนาแน่นและพื้นที่เล็ก และ QR สำหรับเอกสารที่มีพื้นที่กว้างกว่า จะให้ความสมดุลที่ดีที่สุดระหว่างความอ่านง่าย ความจุข้อมูล (สูงสุด 4,296 ตัวอักษรสำหรับ QR) และประสิทธิภาพการใช้พื้นที่พิมพ์

## ข้อกำหนดเบื้องต้น
- **JDK 11 หรือสูงกว่า** (Java 8 ทำงานได้แต่แนะนำให้ใช้ Java 11+ เพื่อประสิทธิภาพที่ดีที่สุด).  
- **IDE** เช่น IntelliJ IDEA, Eclipse หรือ VS Code พร้อมส่วนขยาย Java.  
- **Maven หรือ Gradle** สำหรับการจัดการ dependencies (ตัวอย่างด้านล่าง).  
- **Sample PDF** (เช่น `sample.pdf`) เพื่อทดสอบการใช้งาน  
- **ใบอนุญาต GroupDocs.Signature ที่ถูกต้อง** (ทดลองใช้ฟรีสำหรับการพัฒนา, ใบอนุญาตแบบชำระเงินสำหรับการผลิต)

## การตั้งค่า GroupDocs.Signature สำหรับ Java

### การกำหนดค่า Maven
เพิ่ม dependency ลงใน `pom.xml` ของคุณ:

```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

### การกำหนดค่า Gradle
สำหรับโครงการ Gradle ให้เพิ่มสิ่งนี้ลงใน `build.gradle` ของคุณ:

```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

### ตัวเลือกการดาวน์โหลดโดยตรง
คุณสามารถดาวน์โหลดไฟล์ JAR โดยตรงจาก [GroupDocs.Signature for Java releases](https://releases.groupdocs.com/signature/java/) และเพิ่มลงใน classpath ของโครงการด้วยตนเอง วิธีนี้ทำงานได้ดีในสภาพแวดล้อมที่มีเครือข่ายจำกัด

### การรับใบอนุญาต
ขอรับการทดลองใช้ฟรีหรือใบอนุญาตชั่วคราวจาก GroupDocs เพื่อลบลายน้ำและเปิดใช้งานคุณสมบัติทั้งหมด การใช้งานในสภาพแวดล้อมการผลิตต้องมีใบอนุญาตที่ซื้อแล้ว

### การเริ่มต้นพื้นฐาน
`Signature` class เป็นจุดเริ่มต้นสำหรับการดำเนินการลงลายเซ็นทั้งหมด มันโหลด PDF, ใส่บาร์โค้ด, และเขียนไฟล์ที่ลงลายเซ็นแล้ว

```java
import com.groupdocs.signature.Signature;

class InitializeSignature {
    public static void main(String[] args) {
        Signature signature = new Signature("sample.pdf");
        // Proceed with signing operations...
    }
}
```

## วิธีสร้าง PDF Data Matrix พร้อมบาร์โค้ด HIBC?
โหลด PDF ต้นฉบับของคุณ, กำหนดอ็อบเจกต์ `QrCodeSignOptions` สำหรับรูปแบบ Data Matrix, และเรียก `sign()` – นั่นคือทั้งหมดที่คุณต้องทำเพื่อฝังบาร์โค้ด HIBC Data Matrix ที่สอดคล้อง ขั้นตอนต่อไปนี้จะพาคุณผ่านโค้ดที่จำเป็น `QrCodeSignOptions` กำหนดการตั้งค่าสำหรับลายเซ็นบาร์โค้ด เช่น ประเภท, เนื้อหา, ขนาด, และตำแหน่ง.

1. **นำเข้าคลาสที่จำเป็น** – ซึ่งให้คุณเข้าถึงเอนจินลายเซ็นและตัวเลือก Data Matrix.  

```java
import com.groupdocs.signature.Signature;
import com.groupdocs.signature.options.sign.QrCodeSignOptions;
import com.groupdocs.signature.domain.qrcodes.QrCodeTypes;
```

2. **สร้างอ็อบเจกต์ `Signature`** ด้วยเส้นทางแบบ absolute สำหรับไฟล์ต้นฉบับและไฟล์ปลายทาง.  

```java
String sourceFilePath = "YOUR_DOCUMENT_DIRECTORY";
String destinFilePath = "YOUR_OUTPUT_DIRECTORY/SignWithHIBCLICQR.pdf";

final Signature signature = new Signature(sourceFilePath);
```

3. **กำหนดค่าตัวเลือก Data Matrix** – ตั้งสตริง HIBC, เลือก `QrCodeTypes.HIBCLICDataMatrix`, และกำหนดพิกัดการวาง `QrCodeTypes` แสดงรายการรูปแบบบาร์โค้ดที่รองรับสำหรับลายเซ็น HIBC.  

```java
QrCodeSignOptions hibcLic_QR = new QrCodeSignOptions("A123PROD30917/75#422011907#GP293", QrCodeTypes.HIBCLICQR);
hibcLic_QR.setLeft(1); // Set the position from left
hibcLic_QR.setTop(1);   // Set the position from top
hibcLic_QR.setReturnContent(true); // Return content after signing
hibcLic_QR.setReturnContentType(FileType.PNG); // Specify return content type as PNG
```

4. **นำลายเซ็นไปใช้** กับ PDF.  

```java
signature.sign(destinFilePath, hibcLic_QR);
```

5. **ปล่อยทรัพยากร** เพื่อปลดปล่อยไฟล์แฮนด์เดิลและหลีกเลี่ยงการรั่วของหน่วยความจำ.  

```java
finally {
    if (signature != null) signature.dispose();
}
```

### ตัวอย่างการทำงานที่สมบูรณ์
นี่คือกระบวนการทั้งหมดในบล็อกเดียว (ตัวแทน placeholders แสดงโค้ดที่คุณจะวางจาก snippet ก่อนหน้า):

```java
import com.groupdocs.signature.Signature;
import com.groupdocs.signature.options.sign.QrCodeSignOptions;
import com.groupdocs.signature.domain.qrcodes.QrCodeTypes;

public class HibcQrSigning {
    public static void main(String[] args) {
        String sourceFilePath = "sample.pdf";
        String destinFilePath = "output/SignWithHIBCLICQR.pdf";
        
        Signature signature = null;
        try {
            signature = new Signature(sourceFilePath);
            
            QrCodeSignOptions hibcLic_QR = new QrCodeSignOptions(
                "A123PROD30917/75#422011907#GP293", 
                QrCodeTypes.HIBCLICQR
            );
            hibcLic_QR.setLeft(1);
            hibcLic_QR.setTop(1);
            hibcLic_QR.setReturnContent(true);
            hibcLic_QR.setReturnContentType(FileType.PNG);
            
            signature.sign(destinFilePath, hibcLic_QR);
            System.out.println("PDF signed successfully with HIBC QR code");
            
        } catch (Exception e) {
            System.err.println("Error signing PDF: " + e.getMessage());
            e.printStackTrace();
        } finally {
            if (signature != null) signature.dispose();
        }
    }
}
```

#### คำตอบโดยตรง (40–70 คำ)
เพื่อ **สร้าง PDF Data Matrix**, สร้างอ็อบเจกต์ `Signature` ด้วย PDF ต้นฉบับของคุณ, ตั้ง `QrCodeSignOptions` เป็น `QrCodeTypes.HIBCLICDataMatrix` และให้สตริง HIBC ที่ฟอร์แมตถูกต้อง, จากนั้นเรียก `signature.sign(outputPath, options)`. ไลบรารีจะเขียน PDF ที่ลงลายเซ็นไปยังปลายทาง, รักษาเลเอาต์และฝังบาร์โค้ดเป็นลายเซ็นที่แสดงการดัดแปลง

## วิธีเพิ่ม QR code PDF ด้วย GroupDocs.Signature?
โหลด PDF, กำหนด `QrCodeSignOptions` สำหรับรูปแบบ QR, และเรียก `sign()` รูปแบบสองบรรทัดนี้ทำงานกับ PDF ขนาดใดก็ได้และปรับขนาดภาพ QR อัตโนมัติเพื่อความอ่านง่ายสูงสุด `QrCodeSignOptions` กำหนดค่าลายเซ็นบาร์โค้ด QR รวมถึงเนื้อหาและคุณสมบัติภาพ มันวางตำแหน่งโค้ดตามพิกัดที่คุณตั้งค่า เพื่อให้ไม่ทับซ้อนกับเนื้อหาที่มีอยู่และยังคงสแกนได้หลังการพิมพ์

1. **นำเข้าคลาสที่เฉพาะเจาะจงสำหรับ QR**  

```java
QrCodeSignOptions hibcLic_AZ = new QrCodeSignOptions("A123PROD30917/75#422011907#GP293", QrCodeTypes.HIBCLICAztec);
hibcLic_AZ.setLeft(1); // Set the position from left
hibcLic_AZ.setTop(200); // Set the position from top
hibcLic_AZ.setReturnContent(true); // Return content after signing
hibcLic_AZ.setReturnContentType(FileType.PNG); // Specify return content type as PNG
```

2. **สร้างและกำหนดค่า QR options** – โปรดสังเกตการใช้ `QrCodeTypes.HIBCLICQR`.  

```java
signature.sign(destinFilePath, hibcLic_AZ);
```

3. **ลงลายเซ็นเอกสาร**  

```java
QrCodeSignOptions hibcLic_DM = new QrCodeSignOptions("A123PROD30917/75#422011907#GP293", QrCodeTypes.HIBCLICDataMatrix);
hibcLic_DM.setLeft(1); // Set the position from left
hibcLic_DM.setTop(400); // Set the position from top
hibcLic_DM.setReturnContent(true); // Return content after signing
hibcLic_DM.setReturnContentType(FileType.PNG); // Specify return content type as PNG
```

> **คำตอบโดยตรง:** ใช้ `QrCodeTypes.HIBCLICQR` ใน `QrCodeSignOptions`, ตั้งสตริงเนื้อหา HIBC, กำหนดตำแหน่งโค้ดด้วย `setLeft()` และ `setTop()`, จากนั้นเรียก `signature.sign(outputPath, options)`. บาร์โค้ด QR จะถูกฝังทันที พร้อมสำหรับการจับภาพด้วยสมาร์ทโฟนหรือสแกนเนอร์

## ข้อผิดพลาดทั่วไปที่ควรหลีกเลี่ยง

### 1. ลืมปล่อยทรัพยากร
**Wrong:**  
```java
Signature signature = new Signature("sample.pdf");
signature.sign(destinFilePath, options);
// Oops, no dispose() call
```  

**Fix:** ห่อการใช้ `Signature` ด้วย try‑with‑resources block หรือเรียก `close()` อย่างชัดเจนใน finally clause.

### 2. ใช้สตริงรูปแบบ HIBC ไม่ถูกต้อง
**Wrong:** ใช้สตริงทั่วไปเช่น “12345”.  
**Fix:** ปฏิบัติตามมาตรฐาน HIBCC (เช่น `A123PROD30917/75#422011907#GP293`). ตรวจสอบด้วย [HIBCC online validator](https://www.hibcc.org/).

### 3. กำหนดเส้นทางไฟล์แบบฮาร์ดโค้ด
**Wrong:**  
```java
String sourceFilePath = "C:/Users/John/Documents/test.pdf";
```  

**Fix:** เก็บเส้นทางในไฟล์กำหนดค่า หรือ ตัวแปรสภาพแวดล้อมและอ่านในเวลารัน

### 4. ไม่สนใจความขัดแย้งของตำแหน่งบาร์โค้ด
วางบาร์โค้ดห่างจากข้อความหรือลายเซ็นที่มีอยู่ ใช้พิกัด PDF (จุดกำเนิดที่ด้านล่างซ้าย) และทดสอบด้วยตัวอย่างที่พิมพ์ออกมา.

### 5. ไม่ทดสอบกับสแกนเนอร์จริง
พิมพ์ PDF ที่ลงลายเซ็นและสแกนด้วยฮาร์ดแวร์เดียวกับที่ใช้ในกระบวนการของคุณ ตรวจสอบความอ่านได้ที่คุณภาพการพิมพ์ต่าง ๆ.

## การประยุกต์ใช้ในด้านสุขภาพ

| สถานการณ์ | บาร์โค้ดที่แนะนำ | เหตุผลที่เหมาะสม |
|----------|--------------------|--------------|
| **การจัดจำหน่ายยา** | QR Code | ความจุข้อมูลสูง, สแกนได้ง่ายโดยสมาร์ทโฟน |
| **การจัดการสินค้าคงคลัง** | Data Matrix | พื้นที่ใช้สอยเล็ก, เหมาะสำหรับป้ายชั้นวางที่หนาแน่น |
| **การปฏิบัติตามกฎระเบียบ (FDA 21 CFR Part 11)** | QR + Data Matrix | รูปแบบคู่ให้ความซ้ำซ้อนและความสามารถในการตรวจสอบ |
| **การติดตามอุปกรณ์ทางการแพทย์** | Aztec Code | ขนาดกะทัดรัดทำงานได้บนบรรจุภัณฑ์ที่มีพื้นที่จำกัด |

## ข้อควรพิจารณาด้านประสิทธิภาพและแนวปฏิบัติที่ดีที่สุด

### รูปแบบการประมวลผลแบบแบตช์
```java
List<String> filesToSign = getFileList();
for (String filePath : filesToSign) {
    Signature signature = null;
    try {
        signature = new Signature(filePath);
        // Sign and save
    } finally {
        if (signature != null) signature.dispose();
    }
}
```

- สร้างอินสแตนซ์ `Signature` ใหม่ต่อไฟล์เพื่อรักษาการใช้หน่วยความจำให้ต่ำ  
- ใช้ thread pool คงที่ (`Executors.newFixedThreadPool(Runtime.getRuntime().availableProcessors() - 1)`) สำหรับการประมวลผลแบบขนาน แต่ควรตรวจสอบขนาด heap เนื่องจากแต่ละ `Signature` เก็บ PDF ทั้งหมดในหน่วยความจำ

### อัปเดตไลบรารีอย่างสม่ำเสมอ
การอัปเดต GroupDocs ปรับปรุงความเร็วการประมวลผลได้ถึง **20 %** และเพิ่มคุณสมบัติการปฏิบัติตาม HIBC ใหม่. กำหนดการตรวจสอบ dependencies ทุกไตรมาส.

### แคชเทมเพลต
โหลดเทมเพลต PDF ครั้งเดียว, คัดลอกสำหรับแต่ละรูปแบบบาร์โค้ด, และลงลายเซ็นในสำเนา การทำเช่นนี้ลด I/O และเร่งความเร็วของกระบวนการทำงานปริมาณมาก

## คำถามที่พบบ่อย

**Q: GroupDocs.Signature สามารถลงลายเซ็นไฟล์ประเภทอื่นนอกจาก PDF ได้หรือไม่?**  
A: ได้ รองรับ DOCX, XLSX, PPTX, PNG, JPEG, และ TIFF ด้วย API การลงลายเซ็นบาร์โค้ดเดียวกัน

**Q: ฉันจะแก้ไขข้อผิดพลาด “Invalid barcode content” อย่างไร?**  
A: ตรวจสอบว่าสตริง HIBC ของคุณตรงตามไวยากรณ์ HIBCC อย่างเคร่งครัด ใช้ตัวตรวจสอบออนไลน์ และตรวจให้แน่ใจว่าคุณใช้ค่าคงที่ `QrCodeTypes` ที่ถูกต้องสำหรับรูปแบบที่เลือก

**Q: ความจุข้อมูลสูงสุดของแต่ละรูปแบบ HIBC คือเท่าไหร่?**  
A: QR ≈ 4,296 ตัวอักษรอัลฟานูเมอริก, Aztec ≈ 3,832 ตัวเลข / 3,067 ตัวอักษรอัลฟานูเมอริก, Data Matrix ≈ 3,116 ตัวเลข / 2,335 ตัวอักษรอัลฟานูเมอริก. ควรทำบาร์โค้ดไม่เกิน 200 ตัวอักษรเพื่อความน่าเชื่อถือในการสแกนสูงสุด

**Q: สามารถฝังหลายประเภทบาร์โค้ดใน PDF เดียวได้หรือไม่?**  
A: ได้แน่นอน สร้างอ็อบเจกต์ `QrCodeSignOptions` แยกกันด้วยตำแหน่งต่าง ๆ แล้วเรียก `signature.sign()` สำหรับแต่ละอ็อบเจกต์ เพียงตรวจสอบให้แน่ใจว่าไม่ทับซ้อนกัน

**Q: ฉันต้องการการเชื่อมต่ออินเทอร์เน็ตสำหรับการลงลายเซ็นขณะรันไทม์หรือไม่?**  
A: ไม่ หลังจากที่ JAR อยู่ใน classpath และใบอนุญาตถูกเปิดใช้งาน การดำเนินการทั้งหมดจะทำในเครื่อง

## แหล่งข้อมูลเพิ่มเติม

- [เอกสาร GroupDocs.Signature for Java](https://docs.groupdocs.com/signature/java/)  
- [คู่มืออ้างอิง API](https://reference.groupdocs.com/signature/java/)  
- [ดาวน์โหลดรุ่นล่าสุด](https://releases.groupdocs.com/signature/java/)  
- [ซื้อใบอนุญาต](https://purchase.groupdocs.com/buy)  
- [รับการทดลองใช้ฟรี](https://releases.groupdocs.com/signature/java/)  
- [ขอใบอนุญาตชั่วคราว](https://purchase.groupdocs.com/temporary-license/)  
- [ฟอรั่ม GroupDocs](https://forum.groupdocs.com/c/signature/)

**อัปเดตล่าสุด:** 2026-05-16  
**ทดสอบด้วย:** GroupDocs.Signature 23.12 for Java  
**ผู้เขียน:** GroupDocs  

```java
signature.sign(destinFilePath, hibcLic_DM);
```

## บทแนะนำที่เกี่ยวข้อง

- [สร้างลายเซ็นบาร์โค้ด PDF ใน Java – คู่มือ GroupDocs](/signature/java/barcode-signatures/create-sign-pdfs-groupdocs-barcode-java/)
- [สร้างลายเซ็นบาร์โค้ดใน Java – อัปเดตบาร์โค้ด PDF](/signature/java/barcode-signatures/java-groupdocs-signature-barcode-initialize-update/)
- [วิธีอ่าน QR code PDF ด้วย Java และ GroupDocs.Signature](/signature/java/barcode-signatures/java-pdf-barcode-search-groupdocs-signature-api/)