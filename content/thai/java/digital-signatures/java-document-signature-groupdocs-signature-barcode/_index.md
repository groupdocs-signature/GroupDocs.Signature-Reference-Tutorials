---
date: '2026-07-15'
description: เรียนรู้วิธีเพิ่ม Barcode PDF Java ด้วย GroupDocs.Signature – คู่มือขั้นตอนต่อขั้นตอนในการลงนาม,
  ตรวจสอบ, ค้นหา, อัปเดตและลบลายเซ็นบาร์โค้ดในเอกสาร Java
keywords:
- add barcode pdf java
- groupdocs barcode signature
- java document signing
lastmod: '2026-07-15'
linktitle: คู่มือ Barcode Signature Java
og_description: เรียนรู้วิธีเพิ่ม Barcode PDF Java ด้วย GroupDocs.Signature – คู่มือขั้นตอนต่อขั้นตอนในการลงนาม,
  ตรวจสอบ, ค้นหา, อัปเดตและลบลายเซ็นบาร์โค้ดในเอกสาร Java
og_image_alt: Guide showing how to add barcode PDF Java using GroupDocs.Signature
og_title: เพิ่ม Barcode PDF Java – ลงนามและตรวจสอบด้วย GroupDocs
schemas:
- author: GroupDocs
  dateModified: '2026-07-15'
  description: Learn how to add barcode PDF Java using GroupDocs.Signature – step‑by‑step
    guide to sign, verify, search, update and delete barcode signatures in Java documents.
  headline: Add Barcode PDF Java – Sign & Verify with GroupDocs
  type: TechArticle
- description: Learn how to add barcode PDF Java using GroupDocs.Signature – step‑by‑step
    guide to sign, verify, search, update and delete barcode signatures in Java documents.
  name: Add Barcode PDF Java – Sign & Verify with GroupDocs
  steps:
  - name: Case mismatch (e.g., “John Smith” vs. “john smith”).
    text: Case mismatch (e.g., “John Smith” vs. “john smith”).
  - name: Extra whitespace in the encoded text.
    text: Extra whitespace in the encoded text.
  - name: Wrong barcode type specified in the verification options.
    text: Wrong barcode type specified in the verification options.
  - name: Searching the wrong page number.
    text: Searching the wrong page number.
  - name: '**Reuse Signature Instances** – Create a single `Signature` object per
      document and reuse it for multiple operations.'
    text: '**Reuse Signature Instances** – Create a single `Signature` object per
      document and reuse it for multiple operations.'
  - name: '**Search Specific Pages Only** – Limit the page range to where barcodes
      are expected.'
    text: '**Search Specific Pages Only** – Limit the page range to where barcodes
      are expected.'
  - name: '**Choose the Simplest Barcode Type** – Simpler barcodes generate faster;
      only use QR or Data Matrix when you truly need the extra capacity.'
    text: '**Choose the Simplest Barcode Type** – Simpler barcodes generate faster;
      only use QR or Data Matrix when you truly need the extra capacity.'
  - name: '**Never Encode Sensitive Personal Data** – Barcodes are easily readable;
      avoid PII such as SSNs or passwords.'
    text: '**Never Encode Sensitive Personal Data** – Barcodes are easily readable;
      avoid PII such as SSNs or passwords.'
  - name: '**Validate Server‑Side** – Never trust client‑side verification alone;
      always re‑verify on a trusted backend.'
    text: '**Validate Server‑Side** – Never trust client‑side verification alone;
      always re‑verify on a trusted backend.'
  - name: '**Add Timestamps** – Include a timestamp in the barcode payload to prevent
      replay attacks.'
    text: '**Add Timestamps** – Include a timestamp in the barcode payload to prevent
      replay attacks.'
  type: HowTo
- questions:
  - answer: Yes – the library is fully compatible with JDK 8, 11, and 17.
    question: Can I use GroupDocs.Signature with Java 17?
  - answer: When you use Code128 or QR with sufficient size and contrast, the barcode
      remains scannable after printing and scanning.
    question: Does the barcode survive a print‑scan cycle?
  - answer: There is no hard limit; however, for optimal performance keep the total
      count below **200** per document.
    question: How many barcodes can a single document contain?
  - answer: A temporary license removes evaluation watermarks; a full license is mandatory
      for any production deployment.
    question: Is a license required for development builds?
  - answer: Yes – provide the password when creating the `Signature` object; the API
      will unlock the file internally.
    question: Can I sign password‑protected PDFs?
  type: FAQPage
tags:
- barcode signature
- groupdocs
- java
- pdf
- document signing
title: เพิ่ม Barcode PDF Java – ลงนามและตรวจสอบด้วย GroupDocs
type: docs
url: /th/java/digital-signatures/java-document-signature-groupdocs-signature-barcode/
weight: 1
---

# เพิ่ม Barcode PDF Java – ลงชื่อและตรวจสอบด้วย GroupDocs

หากคุณต้องการวิธีที่รวดเร็วและเห็นภาพเพื่อทำเครื่องหมายเอกสารสำหรับกระบวนการทำงานภายใน การเพิ่ม barcode ลงใน PDF ด้วย Java เป็นวิธีที่สมบูรณ์แบบ ด้วย **GroupDocs.Signature** คุณสามารถฝัง, ตรวจสอบ, ค้นหา, อัปเดตและลบลายเซ็น barcode ได้โดยไม่ต้องใช้ลายเซ็นดิจิทัลแบบ PKI‑based ที่ซับซ้อน บทเรียนนี้จะพาคุณผ่านทุกขั้นตอน ตั้งแต่การตั้งค่าสภาพแวดล้อมจนถึงแนวปฏิบัติที่พร้อมใช้งานในการผลิต

## คำตอบเร็ว
- **ไลบรารีอะไรที่เพิ่ม barcode ให้กับ PDF ใน Java?** GroupDocs.Signature for Java.  
- **ฉันสามารถลงนาม PDF, Word และรูปภาพได้หรือไม่?** ใช่ – API รองรับกว่า 30 รูปแบบ.  
- **ฉันต้องการไลเซนส์สำหรับการพัฒนาหรือไม่?** ไลเซนส์ชั่วคราว 30‑วันฟรี; ต้องมีไลเซนส์เต็มสำหรับการใช้งานจริง.  
- **ต้องใช้บรรทัดโค้ดกี่บรรทัดเพื่อลงนาม PDF?** เพียงสองบรรทัด: สร้างอ็อบเจ็กต์ `Signature` แล้วเรียก `sign`.  
- **การตรวจสอบ barcode มีความไวต่อกรณีอักษรหรือไม่?** ใช่ – ข้อความต้องตรงกันอย่างสมบูรณ์ รวมถึงตัวพิมพ์ใหญ่‑เล็กและช่องว่าง.

## add barcode pdf java คืออะไร
`add barcode pdf java` หมายถึงกระบวนการใช้โค้ด Java เพื่อฝัง barcode (เช่น Code128, QR หรือ Data Matrix) ลงในไฟล์ PDF เทคนิคนี้ให้แท็กที่เครื่องอ่านได้ซึ่งสามารถสแกนหรือยืนยันโดยโปรแกรมได้ ช่วยให้การติดตามเอกสารภายในระบบทำได้อย่างรวดเร็ว

## ทำไมต้องใช้ลายเซ็น barcode แทนลายเซ็นดิจิทัลเต็มรูปแบบ?
ลายเซ็น barcode **เร็วกว่า 30‑50 %** ในการสร้างและตรวจสอบเมื่อเทียบกับลายเซ็นดิจิทัลแบบ PKI‑based และทำงานได้อย่างเชื่อถือได้หลังการพิมพ์‑สแกน ไม่ต้องจัดการใบรับรอง ทำให้เหมาะกับกระบวนการทำงานภายในที่ต้องการปริมาณสูงและไม่จำเป็นต้องมีหลักฐานเชิงคริปโต

## ข้อกำหนดเบื้องต้น

- **Java Development Kit (JDK) 8+** – แนะนำให้ใช้ Java 11 หรือ 17 เพื่อประสิทธิภาพที่ดีกว่า.  
- **IDE** – IntelliJ IDEA หรือ Eclipse (ตัวอย่างใช้ไวยากรณ์ของ IntelliJ).  
- **เครื่องมือสร้าง** – Maven หรือ Gradle สำหรับการจัดการ dependencies.  

### การเพิ่ม GroupDocs.Signature ไปยังโปรเจกต์ของคุณ

วิธีที่ง่ายที่สุดคือเพิ่มไลบรารีผ่านเครื่องมือสร้างของคุณ ตัวอย่างเช่น:

**ผู้ใช้ Maven** – เพิ่มบรรทัดต่อไปนี้ใน `pom.xml` ของคุณ:

```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

**ผู้ใช้ Gradle** – เพิ่มบรรทัดต่อไปนี้ใน `build.gradle`:

```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

**Direct JAR Download** – หากคุณต้องการตั้งค่าด้วยตนเอง ให้ดาวน์โหลด JAR จาก [การปล่อย GroupDocs.Signature](https://releases.groupdocs.com/signature/java/) แล้วเพิ่มลงใน classpath ของคุณ

### การจัดการไลเซนส์ของคุณ

GroupDocs.Signature ไม่ฟรีสำหรับการใช้งานจริง แต่คุณมีตัวเลือกยืดหยุ่น:

- **ทดลองใช้ฟรี** – ดาวน์โหลดจาก [หน้าดาวน์โหลดของ GroupDocs](https://releases.groupdocs.com/signature/java/) เพื่อทดสอบฟีเจอร์ (จะมีลายน้ำการประเมินผล).  
- **ไลเซนส์ชั่วคราว** – รับการเข้าถึงเต็มรูปแบบเป็นเวลา 30 วันผ่าน [หน้าลิขสิทธิ์ชั่วคราวของ GroupDocs](https://purchase.groupdocs.com/temporary-license/) – เหมาะสำหรับการพิสูจน์แนวคิด.  
- **ไลเซนส์เต็ม** – สำหรับการใช้งานจริง ตรวจสอบ [ตัวเลือกการซื้อของ GroupDocs](https://purchase.groupdocs.com/buy).  

**Pro tip:** เริ่มต้นด้วยไลเซนส์ชั่วคราวสำหรับการพัฒนา; จะลบลายน้ำเมื่อคุณเปลี่ยนเป็นคีย์ถาวร

### การตรวจสอบสภาพแวดล้อมอย่างรวดเร็ว

หลังจากเพิ่ม dependency แล้ว ให้รันการทดสอบง่าย ๆ:

```java
import com.groupdocs.signature.Signature;

public class SignatureTest {
    public static void main(String[] args) {
        try {
            Signature signature = new Signature("test.pdf");
            System.out.println("GroupDocs.Signature initialized successfully!");
            signature.dispose();
        } catch (Exception e) {
            System.err.println("Setup issue: " + e.getMessage());
        }
    }
}
```

หากโปรแกรมทำงานโดยไม่มีข้อผิดพลาด สภาพแวดล้อมของคุณพร้อมใช้งาน หากพบปัญหา ให้ตรวจสอบเวอร์ชัน JDK และเวอร์ชันไลบรารีที่คุณเพิ่ม

## เมื่อใดควรใช้ลายเซ็น Barcode

ลายเซ็น barcode มีประโยชน์ในสถานการณ์เฉพาะ:

- **กระบวนการทำงานเอกสารภายใน** – ติดตามใบแจ้งหนี้, ใบสั่งซื้อ หรือบันทึกข้อความผ่านสายการอนุมัติ.  
- **การประมวลผลปริมาณมาก** – ลงนามเอกสารหลายพันฉบับอย่างรวดเร็ว; การสร้าง barcode เร็วกว่า **2×** เท่ากว่าการลงนามดิจิทัลเต็มรูปแบบ.  
- **สะพานการพิมพ์‑สแกน** – barcode ยังอ่านได้หลังการพิมพ์‑สแกน ทำให้เหมาะกับกระบวนการผสมกระดาษ‑ดิจิทัล.  
- **การบูรณาการระบบเก่า** – เครื่องสแกน barcode ที่มีอยู่สามารถอ่านแท็กได้โดยไม่ต้องซอฟต์แวร์เพิ่มเติม.  
- **ร่องรอยการตรวจสอบ** – ฝังรหัสธุรกรรมหรือเวลาที่ตรวจสอบได้ทันทีโดยผู้ตรวจสอบ.  

หลีกเลี่ยงการใช้ลายเซ็น barcode สำหรับสัญญากฎหมาย, เอกสารที่ต้องการความปลอดภัยสูง, หรือการแลกเปลี่ยนกับพันธมิตรภายนอกที่ต้องการลายเซ็นดิจิทัลแบบ PKI

## การตั้งค่า GroupDocs.Signature สำหรับ Java

### คำจำกัดความของคลาสหลัก

คลาส `Signature` เป็นจุดเริ่มต้นสำหรับการลงนาม, ตรวจสอบ, ค้นหา, อัปเดตและลบลายเซ็นใน GroupDocs.Signature

```java
import com.groupdocs.signature.Signature;
```

### การเริ่มต้นพื้นฐาน

สร้างอ็อบเจ็กต์ `Signature` ที่ชี้ไปยังไฟล์เป้าหมาย:

```java
Signature signature = new Signature("path/to/your/document.pdf");
```

**Important notes**
- เส้นทางสามารถเป็นแบบเต็มหรือแบบสัมพันธ์; ใช้ `System.getProperty("user.home")` เพื่อความเข้ากันได้ข้ามแพลตฟอร์ม.  
- GroupDocs รองรับ **กว่า 30 รูปแบบอินพุตและเอาต์พุต**, รวมถึง PDF, DOCX, XLSX, PPTX, และ PNG.  
- ควรปล่อยทรัพยากรเสมอด้วย `signature.dispose()` หรือบล็อก try‑with‑resources:

```java
try (Signature signature = new Signature("path/to/your/document.pdf")) {
    // Your signing operations here
} catch (Exception e) {
    System.err.println("Error working with document: " + e.getMessage());
}
```

ตอนนี้คุณพร้อมที่จะเพิ่ม barcode แล้ว

## ฉันจะเพิ่ม barcode ลงใน PDF ด้วย Java อย่างไร

การโหลด PDF ต้นฉบับด้วย `new Signature("input.pdf")`, กำหนดอ็อบเจ็กต์ `BarcodeSignature` (เช่น Code128 พร้อมข้อความ “John Smith”) แล้วเรียก `sign` เพื่อสร้างไฟล์ที่ลงนาม – ทั้งหมดในสามบรรทัดสั้น ๆ วิธีนี้ทำให้คุณฝังแท็กที่เครื่องอ่านได้โดยไม่กระทบต่อเลย์เอาต์เอกสารเดิมและใช้ได้กับรูปแบบที่รองรับทั้งหมด ไม่จำกัดแค่ PDF

### การดำเนินการตามขั้นตอน

#### 1. กำหนดเส้นทางไฟล์

ตั้งค่าตำแหน่งของไฟล์ต้นฉบับและไฟล์ผลลัพธ์:

```java
String filePath = "YOUR_DOCUMENT_DIRECTORY/sample.docx";
String outputFilePath = "YOUR_OUTPUT_DIRECTORY/signed_sample.docx";
```

#### 2. สร้างตัวจัดการ Signature

เริ่มต้นตัวจัดการด้วยเอกสารต้นฉบับ:

```java
Signature signature = new Signature(filePath);
```

#### 3. กำหนดค่าตัวเลือก Barcode

อ็อบเจ็กต์ `BarcodeSignature` กำหนดคุณสมบัติเชิงภาพและข้อมูลของ barcode ที่จะฝัง ตั้งค่าชนิด barcode, ข้อความที่เข้ารหัส, ตำแหน่ง, ขนาด, สีและฟอนต์ที่อ่านได้ (ถ้ามี):

```java
BarcodeSignOptions signOptions = new BarcodeSignOptions("John Smith", BarcodeTypes.Code128);
signOptions.setVerticalAlignment(VerticalAlignment.Top);
signOptions.setHorizontalAlignment(HorizontalAlignment.Center);
signOptions.setWidth(100);
signOptions.setHeight(40);
signOptions.setMargin(new java.awt.Rectangle(20, 20, 0, 0));
signOptions.setForeColor(Color.RED);

SignatureFont signatureFont = new SignatureFont();
signatureFont.setSize(12);
signatureFont.setFamilyName("Comic Sans MS");
signOptions.setFont(signatureFont);
```

> **Pro tip:** หากสตริงที่เข้ารหัสยาวเกิน 20 ตัวอักษร ให้เพิ่มความกว้างของ barcode เพื่อหลีกเลี่ยงข้อผิดพลาดในการสแกน

#### 4. ใช้ลายเซ็น

ดำเนินการลงนามและสร้างไฟล์ผลลัพธ์:

```java
signature.sign(outputFilePath, signOptions);
```

#### 5. ตัวอย่างจากโลกจริง

ในระบบอนุมัติใบแจ้งหนี้ คุณอาจฝังรหัสพนักงานผู้อนุมัติและเวลาประทับ:

```java
String invoiceId = "INV-2025-0042";
String approver = "john.smith@company.com";
String timestamp = LocalDateTime.now().toString();

// Combine into barcode data
String barcodeData = invoiceId + "|" + approver + "|" + timestamp;

BarcodeSignOptions signOptions = new BarcodeSignOptions(barcodeData, BarcodeTypes.QR);
signOptions.setVerticalAlignment(VerticalAlignment.Bottom);
signOptions.setHorizontalAlignment(HorizontalAlignment.Right);

signature.sign(outputFilePath, signOptions);
```

ผลลัพธ์ PDF จะมี barcode ที่สแกนได้ซึ่งเข้ารหัสข้อมูลเมตาดาต้าในการอนุมัติทั้งหมด

## ฉันจะตรวจสอบลายเซ็น barcode ในเอกสาร Java อย่างไร

เมธอด `Signature.verify` ตรวจสอบเอกสารสำหรับลายเซ็น barcode ที่ตรงกับตัวเลือกที่กำหนด คืนค่า boolean ที่บ่งบอกว่ามี barcode ที่คาดหวังอยู่หรือไม่ การตรวจสอบนี้มีประโยชน์สำหรับกระบวนการอัตโนมัติที่ต้องยืนยันว่าเอกสารถูกประมวลผลโดยฝ่ายที่ถูกต้องก่อนทำขั้นตอนต่อไป

### ขั้นตอนการตรวจสอบ

#### 1. โหลดเอกสารที่ลงนามแล้ว

```java
Signature signature = new Signature("YOUR_OUTPUT_DIRECTORY/signed_sample.docx");
```

#### 2. ตั้งเกณฑ์การตรวจสอบ

กำหนดข้อความ, รูปแบบ barcode และหมายเลขหน้าที่คาดหวัง:

```java
BarcodeVerifyOptions verifyOptions = new BarcodeVerifyOptions();
verifyOptions.setAllPages(false); // Only check the first page
verifyOptions.setPageNumber(1);
verifyOptions.setEncodeType(BarcodeTypes.Code128);
verifyOptions.setText("John Smith");
```

#### 3. เรียกการตรวจสอบ

ดำเนินการตรวจสอบและจัดการผลลัพธ์:

```java
boolean isValid = signature.verify(verifyOptions) != null;

if (isValid) {
    System.out.println("Document signature verified successfully!");
} else {
    System.out.println("Warning: Signature verification failed!");
}
```

**Common pattern:** เพื่อยืนยันว่า *any* barcode ของชนิดที่กำหนดมีอยู่ เพียงละเว้นฟิลเตอร์ `setText`:

```java
BarcodeVerifyOptions flexibleOptions = new BarcodeVerifyOptions();
flexibleOptions.setAllPages(true);
flexibleOptions.setEncodeType(BarcodeTypes.Code128);
// No setText() call = accept any text with this barcode type

boolean hasAnySignature = signature.verify(flexibleOptions) != null;
```

หรือยืนยันเฉพาะรูปแบบ barcode โดยไม่สนใจเนื้อหา:

```java
BarcodeVerifyOptions formatOnly = new BarcodeVerifyOptions();
formatOnly.setEncodeType(BarcodeTypes.QR);
// Confirms a QR code exists, regardless of content
```

> **Warning:** การตรวจสอบไวต่อตัวพิมพ์ใหญ่‑เล็กและช่องว่าง; ควรตัดและทำให้ข้อมูลเป็นมาตรฐานก่อนลงนาม

## ฉันจะค้นหาลายเซ็น barcode ภายในเอกสารอย่างไร

เมธอด `Signature.search` สแกนเอกสารเพื่อหา barcode ที่ตรงกับ `BarcodeSearchOptions` ที่ให้มา คืนค่าชุดข้อมูลที่รวมตำแหน่งของแต่ละ barcode, หมายเลขหน้าและค่าที่เข้ารหัสไว้ ความสามารถนี้ช่วยให้ดึงเมตาดาต้าเป็นชุดได้โดยไม่ต้องเปิดไฟล์ทีละไฟล์

### ขั้นตอนการค้นหา

#### 1. เริ่มต้นการค้นหา

```java
Signature signature = new Signature("YOUR_OUTPUT_DIRECTORY/signed_sample.docx");
```

#### 2. กำหนดค่าพารามิเตอร์การค้นหา

ระบุช่วงหน้า, ชนิด barcode หรือฟิลเตอร์ข้อความ:

```java
BarcodeSearchOptions searchOptions = new BarcodeSearchOptions();
searchOptions.setAllPages(true); // Search the entire document
```

โดยอาจจำกัดการค้นหาเพื่อเพิ่มประสิทธิภาพ:

```java
BarcodeSearchOptions narrowSearch = new BarcodeSearchOptions();
narrowSearch.setAllPages(false);
narrowSearch.setPageNumber(1); // Only search page 1
narrowSearch.setEncodeType(BarcodeTypes.Code128); // Only find Code128 barcodes
```

#### 3. ดำเนินการค้นหา

```java
java.util.List<BarcodeSignature> signatures = signature.search(BarcodeSignature.class, searchOptions);

System.out.println("Found " + signatures.size() + " barcode signature(s)");

for (BarcodeSignature bcSignature : signatures) {
    System.out.println("Barcode Type: " + bcSignature.getEncodeType().getTypeName());
    System.out.println("Text: " + bcSignature.getText());
    System.out.println("Position: (" + bcSignature.getLeft() + ", " + bcSignature.getTop() + ")");
    System.out.println("Size: " + bcSignature.getWidth() + "x" + bcSignature.getHeight());
    System.out.println("---");
}
```

#### 4. ตัวอย่างการดึงข้อมูล

ดึงข้อมูลการอนุมัติจากทุก barcode ในชุดใบแจ้งหนี้:

```java
List<BarcodeSignature> foundSignatures = signature.search(BarcodeSignature.class, searchOptions);

for (BarcodeSignature sig : foundSignatures) {
    String barcodeData = sig.getText();
    
    // Parse your custom format (remember our invoice example?)
    String[] parts = barcodeData.split("\\|");
    if (parts.length == 3) {
        String invoiceId = parts[0];
        String approver = parts[1];
        String timestamp = parts[2];
        
        System.out.println("Invoice " + invoiceId + " approved by " + approver + " at " + timestamp);
    }
}
```

> **Performance tip:** สำหรับเอกสารที่มีมากกว่า 100 หน้า ควรจำกัดการค้นหาให้เฉพาะหน้าที่มี barcode เท่านั้น; จะลดเวลาในการทำงานได้ถึง **70 %**

## ฉันจะอัปเดตลายเซ็น barcode ที่มีอยู่ได้อย่างไร

เมธอด `Signature.update` แก้ไขคุณลักษณะเชิงภาพของลายเซ็น barcode ที่มีอยู่—เช่น ตำแหน่ง, ขนาดหรือสี—โดยไม่เปลี่ยนข้อมูลที่เข้ารหัส ซึ่งเป็นประโยชน์เมื่อจำเป็นต้องปรับเลย์เอาต์หลังจากเอกสารถูกลงนามแล้ว

### ขั้นตอนการอัปเดต

#### 1. ค้นหาลายเซ็นที่ต้องการอัปเดต

```java
Signature signature = new Signature("YOUR_OUTPUT_DIRECTORY/signed_sample.docx");

BarcodeSearchOptions searchOptions = new BarcodeSearchOptions();
searchOptions.setAllPages(true);

List<BarcodeSignature> signatures = signature.search(BarcodeSignature.class, searchOptions);
```

#### 2. แก้ไขคุณสมบัติที่ต้องการ

```java
List<BarcodeSignature> signaturesToUpdate = new ArrayList<>();

if (!signatures.isEmpty()) {
    BarcodeSignature bcSignature = signatures.get(0); // Update the first found signature
    
    // Move it 100px right and 100px down
    bcSignature.setLeft(bcSignature.getLeft() + 100);
    bcSignature.setTop(bcSignature.getTop() + 100);
    
    // Make it bigger
    bcSignature.setWidth(200);
    bcSignature.setHeight(50);
    
    signaturesToUpdate.add(bcSignature);
}
```

คุณสามารถเปลี่ยนหลายคุณลักษณะพร้อมกัน:

```java
bcSignature.setLeft(50);
bcSignature.setTop(50);
bcSignature.setWidth(150);
bcSignature.setHeight(45);
// Note: You can't change the encoded text or barcode type with update
// For that, you'd need to delete and re-sign
```

#### 3. บันทึกการเปลี่ยนแปลง

```java
ByteArrayOutputStream outputStream = new ByteArrayOutputStream();
signature.update(outputStream, signaturesToUpdate);

// If you want to save to a file instead:
// signature.update("path/to/updated_document.docx", signaturesToUpdate);
```

#### 4. สถานการณ์จากโลกจริง

ย้ายตำแหน่งลายเซ็นทั้งหมดเพื่อหลีกเลี่ยงการทับกับโลโก้บริษัทที่เพิ่มใหม่:

```java
List<BarcodeSignature> allSignatures = signature.search(BarcodeSignature.class, searchOptions);
List<BarcodeSignature> toUpdate = new ArrayList<>();

for (BarcodeSignature sig : allSignatures) {
    // Move all signatures down by 50px to clear space for new logo
    if (sig.getTop() < 100) {
        sig.setTop(sig.getTop() + 50);
        toUpdate.add(sig);
    }
}

if (!toUpdate.isEmpty()) {
    signature.update(outputStream, toUpdate);
    System.out.println("Repositioned " + toUpdate.size() + " signature(s)");
}
```

> **Limitation:** การเปลี่ยนข้อความที่เข้ารหัสต้องลบและแทรกลายเซ็นใหม่

## ฉันจะลบลายเซ็น barcode จากเอกสารได้อย่างไร

เมธอด `Signature.delete` ลบลายเซ็น barcode ที่เลือกออกจากเอกสารอย่างถาวร ทั้งส่วนภาพและข้อมูลที่เข้ารหัส ใช้เมธอดนี้เมื่อต้องทำความสะอาดลายเซ็นทดสอบหรือเมื่อ barcode ไม่เกี่ยวข้องอีกต่อไป

### ขั้นตอนการลบ

#### 1. ค้นหาลายเซ็น

```java
Signature signature = new Signature("YOUR_OUTPUT_DIRECTORY/signed_sample.docx");

BarcodeSearchOptions searchOptions = new BarcodeSearchOptions();
searchOptions.setAllPages(true);

List<BarcodeSignature> signatures = signature.search(BarcodeSignature.class, searchOptions);
```

#### 2. ลบลายเซ็นที่เลือก

```java
List<BarcodeSignature> signaturesToDelete = new ArrayList<>();

// Delete all Code128 signatures (for example)
for (BarcodeSignature sig : signatures) {
    if (sig.getEncodeType().equals(BarcodeTypes.Code128)) {
        signaturesToDelete.add(sig);
    }
}

if (!signaturesToDelete.isEmpty()) {
    boolean result = signature.delete(signaturesToDelete);
    
    if (result) {
        System.out.println("Successfully deleted " + signaturesToDelete.size() + " signature(s)");
    } else {
        System.err.println("Failed to delete signatures");
    }
}
```

#### 3. ตัวอย่างการลบแบบมีเงื่อนไข

ลบเฉพาะ barcode ที่เก่ากว่าตัวแสดงเวลาเฉพาะ (สมมติว่าตัวแสดงเวลาถูกฝังในข้อความที่เข้ารหัส):

```java
LocalDateTime cutoffDate = LocalDateTime.now().minusDays(30);
List<BarcodeSignature> outdatedSignatures = new ArrayList<>();

for (BarcodeSignature sig : signatures) {
    try {
        String text = sig.getText();
        // Assuming format like "data|timestamp"
        String[] parts = text.split("\\|");
        if (parts.length > 1) {
            LocalDateTime sigDate = LocalDateTime.parse(parts[1]);
            if (sigDate.isBefore(cutoffDate)) {
                outdatedSignatures.add(sig);
            }
        }
    } catch (Exception e) {
        // Skip signatures that don't match our format
        continue;
    }
}

if (!outdatedSignatures.isEmpty()) {
    signature.delete(outdatedSignatures);
    System.out.println("Removed " + outdatedSignatures.size() + " outdated signature(s)");
}
```

> **Caution:** การลบไม่สามารถย้อนกลับได้; ควรทำงานบนสำเนาไฟล์ผลิตจริงระหว่างการทดสอบ

#### 4. รูปแบบการลบเป็นชุด

ทำความสะอาดลายเซ็นทดสอบก่อนการปล่อย:

```java
// Remove all signatures containing "TEST" in their text
List<BarcodeSignature> testSignatures = signatures.stream()
    .filter(sig -> sig.getText().toUpperCase().contains("TEST"))
    .collect(Collectors.toList());

if (!testSignatures.isEmpty()) {
    signature.delete(testSignatures);
    System.out.println("Cleaned up " + testSignatures.size() + " test signature(s)");
}
```

## ประเภท Barcode: คู่มือปฏิบัติ

การเลือก barcode ที่เหมาะสมส่งผลต่อความน่าเชื่อถือของการสแกน, ความจุข้อมูลและความเข้ากันได้ของเครื่องพิมพ์

### Code128 (ตัวเลือกที่พบบ่อยที่สุด)

- **เมื่อใช้:** ข้อมูลอักขระและตัวเลข, ความหนาแน่นสูง, เอกสารที่พิมพ์.  
- **ข้อดี:** กะทัดรัด, ทำงานกับสแกนเนอร์มาตรฐาน, พิมพ์ชัดที่ขนาดเล็ก.  
- **ข้อเสีย:** จำกัดที่ ASCII, ความทนต่อข้อผิดพลาดน้อยกว่าโค้ด 2‑D.

```java
BarcodeSignOptions code128 = new BarcodeSignOptions("INV-2025-042", BarcodeTypes.Code128);
```

### QR Code (ดีที่สุดสำหรับมือถือ)

- **เมื่อใช้:** สแกนด้วยมือถือ, ข้อมูลขนาดใหญ่ (URL, JSON ฯลฯ), เอกสารที่อาจเสียหาย.  
- **ข้อดี:** สูงสุด 4 000 ตัวอักษร, มีการแก้ไขข้อผิดพลาดในตัว, รองรับสมาร์ทโฟน.  
- **ข้อเสีย:** มีขนาดภาพใหญ่กว่า, ต้องการความละเอียดสูงสำหรับขนาดเล็ก.

```java
String jsonData = "{\"invoice\":\"INV-042\",\"amount\":1500.00,\"approver\":\"john@company.com\"}";
BarcodeSignOptions qrCode = new BarcodeSignOptions(jsonData, BarcodeTypes.QR);
```

### Code39 (คลาสสิกที่เชื่อถือได้)

- **เมื่อใช้:** สภาพแวดล้อมสแกนเนอร์เก่า, ต้องการข้อความที่มนุษย์อ่านได้.  
- **ข้อดี:** รองรับระบบเก่าอย่างกว้างขวาง, รูปแบบง่าย, ไม่ต้องเช็คซัม.  
- **ข้อเสีย:** ความหนาแน่นข้อมูลต่ำ, ชุดอักขระจำกัด, ใช้พื้นที่มากกว่า.

### Data Matrix (พลังงานกะทัดรัด)

- **เมื่อใช้:** พื้นที่จำกัดมาก, ทำเครื่องหมายชิ้นส่วนขนาดเล็ก, ข้อมูลความหนาแน่นสูง.  
- **ข้อดี:** กะทัดรัดมาก, การแก้ไขข้อผิดพลาดแข็งแรง, ทำงานบนพื้นผิวโค้ง.  
- **ข้อเสีย:** ต้องการการพิมพ์คุณภาพสูง, การสนับสนุนสแกนเนอร์น้อยกว่า.

#### การเปรียบเทียบอย่างรวดเร็ว

| ประเภท Barcode | ความจุข้อมูล | เหมาะสำหรับ | ขนาดทั่วไป |
|----------------|---------------|--------------|------------|
| Code128        | ~100 ตัวอักษร | การแท็กทั่วไป | เล็ก |
| QR Code        | ~4 000 ตัวอักษร | สแกนมือถือ, ข้อมูลหลากหลาย | ปานกลาง |
| Code39         | ~43 ตัวอักษร | ฮาร์ดแวร์เก่า | ใหญ่ |
| Data Matrix    | ~3 000 ตัวอักษร | พื้นที่เล็กมาก, แท็กอุตสาหกรรม | เล็กมาก |

**Recommendation:** เริ่มต้นด้วย **Code128** สำหรับ ID ง่าย ๆ; เปลี่ยนเป็น **QR** เมื่อจำเป็นต้องฝัง URL หรือข้อมูลขนาดใหญ่; ใช้ **Code39** เฉพาะเมื่อรวมกับระบบเก่า

## ปัญหาทั่วไปและวิธีแก้

### Problem: “ไม่พบ Barcode ระหว่างการตรวจสอบ”

**Symptoms:** การตรวจสอบคืนค่า `false` แม้ว่า barcode จะมองเห็นได้.

**Typical causes**
1. ความแตกต่างของตัวพิมพ์ (เช่น “John Smith” vs. “john smith”).  
2. ช่องว่างเพิ่มในข้อความที่เข้ารหัส.  
3. ระบุชนิด barcode ผิดในตัวเลือกการตรวจสอบ.  
4. ค้นหาหน้าผิดหมายเลข.

**Solution:** ทำให้ข้อความเป็นมาตรฐานก่อนการลงนามและตรวจสอบ, และให้ `setEncodeType` ตรงกับชนิดเดิม.

```java
// Always normalize your data
String signatureText = originalText.trim().toLowerCase();

// When signing:
BarcodeSignOptions signOptions = new BarcodeSignOptions(signatureText, BarcodeTypes.Code128);

// When verifying:
BarcodeVerifyOptions verifyOptions = new BarcodeVerifyOptions();
verifyOptions.setText(signatureText); // Use the same normalized text
verifyOptions.setEncodeType(BarcodeTypes.Code128);
```

### Problem: “Barcode เบลอหรือไม่สามารถอ่านได้”

**Symptoms:** barcode ที่พิมพ์ออกมาสแกนไม่ได้.

**Causes**
- ขนาด barcode เล็กเกินกว่าข้อมูลที่เข้ารหัส.  
- การตั้งค่าพรินเตอร์ความละเอียดต่ำ.  
- คอนทราสต์สี barcode กับพื้นหลังไม่เพียงพอ.

**Solution:** เพิ่มความกว้าง/ความสูงของ barcode, ใช้สีคอนทราสต์สูง (ดำบนพื้นขาว), ตั้งค่า DPI ของพรินเตอร์อย่างน้อย 300 dpi.

```java
// Increase size for longer strings
int dataLength = barcodeText.length();
int minWidth = Math.max(100, dataLength * 10); // 10px per character minimum

BarcodeSignOptions signOptions = new BarcodeSignOptions(barcodeText, BarcodeTypes.Code128);
signOptions.setWidth(minWidth);
signOptions.setHeight(60); // Taller = easier to scan

// Use high-contrast colors
signOptions.setForeColor(Color.BLACK); // Black on white is most reliable
signOptions.setBackColor(Color.WHITE);
```

### Problem: “OutOfMemoryError กับเอกสารขนาดใหญ่”

**Symptoms:** แอปพลิเคชันพังเมื่อประมวลผล PDF หลายร้อยหน้า.

**Cause:** ไลบรารีโหลดเอกสารทั้งหมดเข้าสู่หน่วยความจำ.

**Solution:** เปิดโหมดสตรีมมิ่งและประมวลผลหน้าแบบต่อหน้า.

```java
// Process pages in batches instead of all at once
BarcodeSearchOptions searchOptions = new BarcodeSearchOptions();
searchOptions.setAllPages(false);

List<BarcodeSignature> allSignatures = new ArrayList<>();

for (int page = 1; page <= totalPages; page++) {
    searchOptions.setPageNumber(page);
    List<BarcodeSignature> pageSignatures = signature.search(BarcodeSignature.class, searchOptions);
    allSignatures.addAll(pageSignatures);
    
    // Process and clear as you go
    if (page % 10 == 0) {
        System.gc(); // Suggest garbage collection every 10 pages
    }
}
```

### Problem: “ตำแหน่งลายเซ็นไม่สอดคล้องระหว่างประเภทเอกสาร”

**Symptoms:** barcode ปรากฏในตำแหน่งต่างกันเมื่อลงนาม PDF กับ Word.

**Cause:** PDF ใช้จุดกำเนิดที่มุมล่างซ้าย, ส่วน Word ใช้มุมบนซ้าย.

**Solution:** ตรวจจับประเภทเอกสารและปรับการแปลงพิกัดให้เหมาะสม.

```java
// Use relative positioning instead of absolute
signOptions.setVerticalAlignment(VerticalAlignment.Bottom);
signOptions.setHorizontalAlignment(HorizontalAlignment.Right);

// Then use margins for fine-tuning
Padding margin = new Padding();
margin.setRight(50); // 50px from right edge
margin.setBottom(50); // 50px from bottom
signOptions.setMargin(margin);

// This works consistently across PDF, DOCX, XLSX, etc.
```

### Problem: “ลายเซ็นที่อัปเดตสูญเสียการจัดรูปแบบ”

**Symptoms:** หลังเรียก `update` สีหรือฟอนต์ของ barcode เปลี่ยนโดยไม่คาดคิด.

**Cause:** ไม่ได้บันทึกคุณสมบัติเชิงภาพทั้งหมดระหว่างการอัปเดต.

**Solution:** ตั้งค่าการแสดงผลใหม่หลังจากเรียก `update`.

```java
// When updating, explicitly set all visual properties
bcSignature.setLeft(newLeft);
bcSignature.setTop(newTop);
bcSignature.setWidth(originalWidth); // Don't forget these!
bcSignature.setHeight(originalHeight);
// Note: Color and font can't be updated - you'd need to delete and re-sign
```

## แนวทางปฏิบัติที่ดีที่สุดสำหรับการผลิต

### การเพิ่มประสิทธิภาพ

1. **ใช้ตัวอย่าง Signature ซ้ำ** – สร้างอ็อบเจ็กต์ `Signature` หนึ่งตัวต่อเอกสารและใช้ซ้ำสำหรับหลายการดำเนินการ.

```java
// Bad - Creates new instance each time
public void processDocument(String path) {
    Signature sig1 = new Signature(path);
    sig1.search(/* ... */);
    
    Signature sig2 = new Signature(path); // Unnecessary reload
    sig2.verify(/* ... */);
}

// Good - Reuse the same instance
public void processDocument(String path) {
    try (Signature signature = new Signature(path)) {
        signature.search(/* ... */);
        signature.verify(/* ... */);
        signature.update(/* ... */);
    }
}
```

2. **ค้นหาเฉพาะหน้าที่ต้องการ** – จำกัดช่วงหน้าให้ตรงกับที่คาดว่าจะมี barcode.

```java
// Slow for 100+ page documents
BarcodeSearchOptions slowSearch = new BarcodeSearchOptions();
slowSearch.setAllPages(true);

// Fast - only check where signatures actually are
BarcodeSearchOptions fastSearch = new BarcodeSearchOptions();
fastSearch.setAllPages(false);
fastSearch.setPageNumber(1); // Only check cover page
```

3. **เลือกประเภท Barcode ที่ง่ายที่สุด** – Barcode ที่ง่ายกว่าจะสร้างได้เร็วกว่า; ใช้ QR หรือ Data Matrix เฉพาะเมื่อจำเป็นต้องการความจุเพิ่ม.

```java
// Overkill for simple IDs
BarcodeSignOptions slow = new BarcodeSignOptions("12345", BarcodeTypes.QR);

// Faster and more appropriate
BarcodeSignOptions fast = new BarcodeSignOptions("12345", BarcodeTypes.Code128);
```

### ข้อควรระวังด้านความปลอดภัย

- **ห้ามเข้ารหัสข้อมูลส่วนบุคคลที่สำคัญ** – Barcode สามารถอ่านได้ง่าย; หลีกเลี่ยงข้อมูลส่วนบุคคลเช่น SSN หรือรหัสผ่าน.

```java
// Bad - exposes sensitive data
String barcodeData = "SSN:123-45-6789|Password:hunter2";

// Good - use reference IDs
String barcodeData = "USER-REF-7721X"; // Look up sensitive data server-side
```

- **ตรวจสอบบนเซิร์ฟเวอร์** – อย่าเชื่อถือการตรวจสอบจากฝั่งไคลเอนต์อย่างเดียว; ควรตรวจสอบซ้ำบนแบ็กเอนด์ที่เชื่อถือได้.

```java
// Client scans barcode and extracts "APPROVED-BY-ADMIN"
// Always verify server-side:
public boolean verifyApproval(String documentId, String scannedData) {
    // Load document from secure storage
    Signature signature = new Signature(getSecureDocument(documentId));
    
    BarcodeVerifyOptions verifyOptions = new BarcodeVerifyOptions();
    verifyOptions.setText(scannedData);
    
    boolean isValid = signature.verify(verifyOptions) != null;
    
    // Also check against your database
    boolean isInDatabase = checkApprovalDatabase(documentId, scannedData);
    
    return isValid && isInDatabase;
}
```

- **เพิ่มเวลาประทับ** – ใส่เวลาประทับในข้อมูลของ barcode เพื่อป้องกันการโจมตีแบบรีเพลย์.

```java
import java.time.LocalDateTime;
import java.time.temporal.ChronoUnit;

String timestamp = LocalDateTime.now().truncatedTo(ChronoUnit.SECONDS).toString();
String barcodeData = "APPROVAL|" + userId + "|" + timestamp;

// When verifying, check the timestamp isn't too old
public boolean isSignatureRecent(String barcodeData, int maxAgeHours) {
    String[] parts = barcodeData.split("\\|");
    if (parts.length < 3) return false;
    
    LocalDateTime signatureTime = LocalDateTime.parse(parts[2]);
    LocalDateTime now = LocalDateTime.now();
    
    long hoursSince = ChronoUnit.HOURS.between(signatureTime, now);
    return hoursSince <= maxAgeHours;
}
```

### รูปแบบการจัดการข้อผิดพลาด

- **ใช้ Try‑With‑Resources เสมอ** เพื่อให้แน่ใจว่าอ็อบเจ็กต์ `Signature` ถูกปล่อย.

```java
try (Signature signature = new Signature(documentPath)) {
    // Your operations here
    signature.sign(outputPath, signOptions);
} catch (Exception e) {
    logger.error("Failed to sign document: " + documentPath, e);
    throw new DocumentSigningException("Could not process document", e);
}
```

- **ตรวจสอบการเข้าถึงไฟล์** ก่อนทำการลงนาม.

```java
public void signDocument(String inputPath, String outputPath) {
    File inputFile = new File(inputPath);
    
    if (!inputFile.exists()) {
        throw new IllegalArgumentException("Input file not found: " + inputPath);
    }
    
    if (!inputFile.canRead()) {
        throw new SecurityException("Cannot read input file: " + inputPath);
    }
    
    File outputDir = new File(outputPath).getParentFile();
    if (outputDir != null && !outputDir.exists()) {
        outputDir.mkdirs();
    }
    
    try (Signature signature = new Signature(inputPath)) {
        signature.sign(outputPath, signOptions);
    }
}
```

- **ซิงโครไนซ์การเข้าถึง** หากหลายเธรดอาจทำงานกับไฟล์เดียวกัน.

```java
import java.util.concurrent.locks.ReentrantLock;
import java.util.concurrent.ConcurrentHashMap;

public class SignatureManager {
    private final ConcurrentHashMap<String, ReentrantLock> documentLocks = new ConcurrentHashMap<>();
    
    public void signDocument(String documentPath, BarcodeSignOptions options) {
        ReentrantLock lock = documentLocks.computeIfAbsent(documentPath, k -> new ReentrantLock());
        
        lock.lock();
        try (Signature signature = new Signature(documentPath)) {
            signature.sign(documentPath + ".signed", options);
        } finally {
            lock.unlock();
        }
    }
}
```

### การทดสอบการใช้งานของคุณ

**เทมเพลต Unit Test**

```java
import org.junit.jupiter.api.Test;
import org.junit.jupiter.api.io.TempDir;
import static org.junit.jupiter.api.Assertions.*;

public class BarcodeSignatureTest {
    
    @TempDir
    Path tempDir;
    
    @Test
    public void testSignAndVerify() throws Exception {
        // Setup
        String testDoc = "test-document.pdf";
        String outputDoc = tempDir.resolve("signed-test.pdf").toString();
        String testData = "TEST-USER-12345";
        
        // Sign
        try (Signature signature = new Signature(testDoc)) {
            BarcodeSignOptions signOptions = new BarcodeSignOptions(testData, BarcodeTypes.Code128);
            signature.sign(outputDoc, signOptions);
        }
        
        // Verify
        try (Signature signature = new Signature(outputDoc)) {
            BarcodeVerifyOptions verifyOptions = new BarcodeVerifyOptions();
            verifyOptions.setText(testData);
            verifyOptions.setEncodeType(BarcodeTypes.Code128);
            
            boolean isValid = signature.verify(verifyOptions) != null;
            assertTrue(isValid, "Signature should be valid");
        }
    }
    
    @Test
    public void testSearchFindsSignature() throws Exception {
        String signedDoc = "signed-document.pdf";
        
        try (Signature signature = new Signature(signedDoc)) {
            BarcodeSearchOptions searchOptions = new BarcodeSearchOptions();
            searchOptions.setAllPages(true);
            
            List<BarcodeSignature> signatures = signature.search(BarcodeSignature.class, searchOptions);
            
            assertFalse(signatures.isEmpty(), "Should find at least one signature");
            assertEquals("TEST-USER-12345", signatures.get(0).getText());
        }
    }
}
```

**รายการตรวจสอบการบูรณาการ**

- ✅ ทดสอบทุกรูปแบบที่รองรับ (PDF, DOCX, XLSX, PPTX, PNG).  
- ✅ ตรวจสอบว่า barcode ยังคงอ่านได้หลังการพิมพ์‑สแกน.  
- ✅ ทำการทดสอบความทนทานด้วยสตริงข้อมูลยาวที่สุด.  
- ✅ ยืนยันตำแหน่งบนขนาดหน้า A4, Letter, และขนาดหน้าที่กำหนดเอง.  
- ✅ รันการลงนามพร้อมกันบนหลายเอกสาร.  
- ✅ ตรวจสอบการใช้หน่วยความจำสำหรับเอกสาร > 500 หน้า.  
- ✅ ตรวจสอบให้แน่ใจว่าสแกนเนอร์ barcode สามารถอ่านผลลัพธ์ได้อย่างน่าเชื่อถือ.

### การบันทึกและการเฝ้าติดตาม

เพิ่มบันทึกที่มีความหมายรอบแต่ละการดำเนินการ:

```java
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

public class DocumentSigningService {
    private static final Logger logger = LoggerFactory.getLogger(DocumentSigningService.class);
    
    public void signDocument(String docPath, String barcodeData) {
        logger.info("Starting signature process for document: {}", docPath);
        logger.debug("Barcode data length: {} characters", barcodeData.length());
        
        try (Signature signature = new Signature(docPath)) {
            BarcodeSignOptions options = new BarcodeSignOptions(barcodeData, BarcodeTypes.Code128);
            
            long startTime = System.currentTimeMillis();
            signature.sign(docPath + ".signed", options);
            long duration = System.currentTimeMillis() - startTime;
            
            logger.info("Successfully signed document in {}ms", duration);
        } catch (Exception e) {
            logger.error("Failed to sign document: {}", docPath, e);
            throw new RuntimeException("Signature operation failed", e);
        }
    }
}
```

ติดตามเมตริกสำคัญ เช่น เวลาในการประมวลผล, การใช้หน่วยความจำและอัตราข้อผิดพลาด:

```java
// Track success/failure rates
metricsService.incrementCounter("signature.sign.success");
metricsService.incrementCounter("signature.verify.failure");

// Track performance
metricsService.recordTimer("signature.sign.duration", duration);

// Track document sizes
metricsService.recordHistogram("signature.document.pages", pageCount);
```

## เคล็ดลับจากการใช้งานจริง

**กลยุทธ์การประมวลผลเป็นชุด**

เมื่อจัดการไฟล์หลายร้อยไฟล์ ให้ประมวลผลเป็นชุดและรายงานความคืบหน้า:

```java
public void signBatch(List<String> documents, String barcodePrefix) {
    int total = documents.size();
    int completed = 0;
    int failed = 0;
    
    for (String docPath : documents) {
        try {
            String barcodeData = barcodePrefix + "-" + UUID.randomUUID().toString();
            signDocument(docPath, barcodeData);
            completed++;
            
            if (completed % 10 == 0) {
                logger.info("Progress: {}/{} documents signed", completed, total);
            }
        } catch (Exception e) {
            failed++;
            logger.warn("Failed to sign: {}", docPath, e);
        }
    }
    
    logger.info("Batch complete: {} succeeded, {} failed", completed, failed);
}
```

**แยกการตั้งค่าออกเป็นไฟล์ภายนอก**

เก็บการตั้งค่า barcode (ชนิด, ขนาด, สี) ในไฟล์ properties เพื่อปรับแต่งได้ง่ายโดยไม่ต้องคอมไพล์ใหม่:

```java
public class BarcodeConfig {
    private int defaultWidth = 100;
    private int defaultHeight = 40;
    private String defaultBarcodeType = "Code128";
    private String defaultColor = "BLACK";
    
    // Load from properties file or environment variables
    public BarcodeConfig() {
        this.defaultWidth = Integer.parseInt(
            System.getProperty("barcode.width", "100")
        );
        // ... load other properties
    }
    
    public BarcodeSignOptions createDefaultOptions(String text) {
        BarcodeSignOptions options = new BarcodeSignOptions(text, getBarcodeType());
        options.setWidth(defaultWidth);
        options.setHeight(defaultHeight);
        options.setForeColor(getColor());
        return options;
    }
}
```

**มาตรฐาน Payload ของ Barcode**

ใช้รูปแบบที่คั่นด้วย `|` เช่น `EMPID|TIMESTAMP|DOCID` เพื่อให้การแยกข้อมูลง่ายและสอดคล้องกัน:

```java
public class BarcodeDataBuilder {
    private String userId;
    private String action;
    private LocalDateTime timestamp;
    private String documentId;
    
    public BarcodeDataBuilder setUserId(String userId) {
        this.userId = userId;
        return this;
    }
    
    public BarcodeDataBuilder setAction(String action) {
        this.action = action;
        return this;
    }
    
    public BarcodeDataBuilder setDocumentId(String documentId) {
        this.documentId = documentId;
        return this;
    }
    
    public String build() {
        this.timestamp = LocalDateTime.now();
        
        // Format: VERSION|USER|ACTION|DOC_ID|TIMESTAMP|CHECKSUM
        String data = String.join("|",
            "v1",
            userId,
            action,
            documentId,
            timestamp.toString()
        );
        
        // Add simple checksum
        int checksum = data.hashCode();
        return data + "|" + checksum;
    }
    
    public static ParsedBarcodeData parse(String barcodeData) {
        String[] parts = barcodeData.split("\\|");
        if (parts.length != 6 || !parts[0].equals("v1")) {
            throw new IllegalArgumentException("Invalid barcode format");
        }
        
        return new ParsedBarcodeData(parts[1], parts[2], parts[3], 
                                     LocalDateTime.parse(parts[4]));
    }
}

// Usage:
String barcodeData = new BarcodeDataBuilder()
    .setUserId("john.smith")
    .setAction("APPROVED")
    .setDocumentId("INV-2025-042")
    .build();
```

**ตรวจจับประเภทเอกสารโดยอัตโนมัติ**

ปรับขนาด barcode ตามว่าเป้าหมายเป็น PDF, Word หรือภาพ:

```java
public BarcodeSignOptions getOptimalOptions(String documentPath, String text) {
    String extension = documentPath.substring(documentPath.lastIndexOf(".") + 1).toLowerCase();
    
    BarcodeSignOptions options = new BarcodeSignOptions(text, BarcodeTypes.Code128);
    
    switch (extension) {
        case "pdf":
            // PDFs can handle larger, detailed barcodes
            options.setWidth(150);
            options.setHeight(50);
            break;
        case "docx":
        case "doc":
            // Word docs need compact signatures that don't disrupt flow
            options.setWidth(100);
            options.setHeight(35);
            options.setVerticalAlignment(VerticalAlignment.Bottom);
            break;
        case "xlsx":
        case "xls":
            // Excel needs signatures that don't obscure data
            options.setWidth(80);
            options.setHeight(30);
            options.setHorizontalAlignment(HorizontalAlignment.Right);
            break;
        default:
            // Safe defaults
            options.setWidth(100);
            options.setHeight(40);
    }
    
    return options;
}
```

## แหล่งข้อมูลเพิ่มเติม

- [เอกสาร GroupDocs.Signature](https://docs.groupdocs.com/signature/java/) – คู่มือ API เต็มรูปแบบและตัวอย่างการใช้งาน.  
- [ฟอรั่มสนับสนุน GroupDocs](https://forum.groupdocs.com/c/signature/13) – ความช่วยเหลือจากชุมชนและการแก้ปัญหา.  
- [อ้างอิง API](https://apireference.groupdocs.com/signature/java) – รายละเอียดลายเซ็นเมธอดและคำอธิบายพารามิเตอร์.  

## คำถามที่พบบ่อย

**ถาม: ฉันสามารถใช้ GroupDocs.Signature กับ Java 17 ได้หรือไม่?**  
**ตอบ:** ใช่ – ไลบรารีเข้ากันได้เต็มที่กับ JDK 8, 11, และ 17.

**ถาม: Barcode ยังคงอ่านได้หลังการพิมพ์‑สแกนหรือไม่?**  
**ตอบ:** เมื่อใช้ Code128 หรือ QR ที่มีขนาดและคอนทราสต์เพียงพอ, barcode จะยังคงสแกนได้หลังการพิมพ์และสแกน.

**ถาม: เอกสารหนึ่งสามารถมี barcode ได้กี่อัน?**  
**ตอบ:** ไม่มีขีดจำกัดที่แน่นอน; อย่างไรก็ตามเพื่อประสิทธิภาพที่ดีที่สุด ควรรักษาจำนวนทั้งหมดไม่เกิน **200** ต่อเอกสาร.

**ถาม: จำเป็นต้องมีไลเซนส์สำหรับการสร้างเวอร์ชันพัฒนาไหม?**  
**ตอบ:** ไลเซนส์ชั่วคราวจะลบลายน้ำการประเมินผล; ไลเซนส์เต็มเป็นสิ่งจำเป็นสำหรับการใช้งานจริงใด ๆ.

**ถาม: ฉันสามารถลงนาม PDF ที่มีการป้องกันด้วยรหัสผ่านได้หรือไม่?**  
**ตอบ:** ใช่ – ให้รหัสผ่านเมื่อสร้างอ็อบเจ็กต์ `Signature`; API จะปลดล็อกไฟล์ภายใน.

---

**อัปเดตล่าสุด:** 2026-07-15  
**ทดสอบด้วย:** GroupDocs.Signature 23.9 for Java  
**ผู้เขียน:** GroupDocs

{< /blocks/products/pf/tutorial-page-section >}
{< /blocks/products/pf/main-container >}
{< /blocks/products/pf/main-wrap-class >}
{< blocks/products/products-backtop-button >}

## บทแนะนำที่เกี่ยวข้อง

- [วิธีตรวจสอบลายเซ็น Barcode ใน Java ด้วย GroupDocs.Signature](/signature/java/search-verification/groupdocs-signature-java-document-verification/)
- [วิธีค้นหาลายเซ็นดิจิทัลในเอกสาร Java ด้วย GroupDocs](/signature/java/search-verification/groupdocs-signature-java-digital-search-tutorial/)
- [บทแนะนำลายเซ็น Barcode Java - เพิ่ม, ตรวจสอบ & จัดการ Barcode ใน PDF](/signature/java/barcode-signatures/)