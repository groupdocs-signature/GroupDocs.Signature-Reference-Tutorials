---
categories:
- Document Processing
date: '2026-06-21'
description: เรียนรู้วิธีการค้นหาหน้าบาร์โค้ด java ด้วย GroupDocs.Signature คู่มือขั้นตอนต่อขั้นตอน
  การค้นหาบาร์โค้ดแบบเรียลไทม์ และการตรวจสอบลายเซ็นบาร์โค้ดใน Java
keywords:
- search barcode pages java
- real time barcode search
- barcode verification documents
lastmod: '2026-06-21'
linktitle: ค้นหาหน้าบาร์โค้ดเฉพาะ Java
schemas:
- author: GroupDocs
  dateModified: '2026-06-21'
  description: Learn how to search barcode pages java using GroupDocs.Signature. Step-by-step
    guide, real‑time barcode search, and verification of barcode signatures in Java.
  headline: search barcode pages java – Search Barcode Specific Pages in Documents
  type: TechArticle
- questions:
  - answer: Yes. `BarcodeSearchOptions` searches all supported formats by default.
      Filter results by `getEncodeType()` if you need only specific types.
    question: Can I search for multiple barcode formats in one call?
  - answer: Run separate searches—use `BarcodeSignature.class` for barcodes and `ImageSignature.class`
      for image signatures, then combine the results as needed.
    question: How do I handle documents that contain both barcode and image signatures?
  - answer: Scanning every page of a 50‑page PDF can take 3–5 seconds. Limiting to
      first + last pages usually finishes under 1 second.
    question: What’s the performance impact of searching all pages vs. specific pages?
  - answer: Only if the barcode was added as a digital signature object. For raster‑only
      barcodes, you’ll need an image‑based barcode recognizer (e.g., GroupDocs.Barcode).
    question: Does this work with scanned PDFs (raster images)?
  - answer: Embed a hash or digital signature inside the barcode payload, then recompute
      the hash on the original data and compare. This requires the original signing
      key or certificate.
    question: How can I verify that a barcode signature hasn’t been tampered with?
  type: FAQPage
tags:
- java
- barcode-signatures
- document-verification
- groupdocs
title: ค้นหาหน้าบาร์โค้ด java – ค้นหาหน้าบาร์โค้ดเฉพาะในเอกสาร
type: docs
url: /th/java/barcode-signatures/implement-barcode-signature-search-groupdocs-signature-java/
weight: 1
---

# ค้นหาหน้าที่มีบาร์โค้ดเฉพาะในเอกสารโดยใช้ Java

## บทนำ

เคยใช้เวลาหลายชั่วโมงในการตรวจสอบลายเซ็นด้วยตนเองในเอกสารหลายร้อยฉบับหรือไม่? คุณไม่ได้เป็นคนเดียว ไม่ว่าคุณจะกำลังสร้างระบบจัดการสัญญา, ทำระบบอัตโนมัติการประมวลผลใบแจ้งหนี้, หรือรักษาความปลอดภัยของบันทึกสุขภาพ การติดตามและตรวจสอบลายเซ็นบาร์โค้ดด้วยตนเองนั้นน่าเบื่อและเสี่ยงต่อข้อผิดพลาด **ในบทแนะนำนี้คุณจะได้เรียนรู้วิธีการค้นหาหน้าบาร์โค้ดด้วย Java และ GroupDocs.Signature** เพื่อให้คุณสามารถกำหนดเป้าหมายเฉพาะหน้าที่สำคัญได้โดยโปรแกรม, ตรวจสอบความคืบหน้าแบบเรียลไทม์, และจัดการกับรูปแบบบาร์โค้ดหลายประเภทด้วยเพียงไม่กี่บรรทัดของโค้ด Java.

สิ่งที่คุณจะได้เรียนรู้  
- ตั้งค่า GroupDocs.Signature ในโครงการ Java (≈5 นาที)  
- สมัครรับเหตุการณ์การค้นหาเพื่อการติดตามความคืบหน้าแบบเรียลไทม์  
- กำหนดค่าตัวเลือกการค้นอัจฉริยะเพื่อกำหนดเป้าหมายหน้าที่เฉพาะ  
- ดำเนินการค้นหาและประมวลผลผลลัพธ์อย่างมีประสิทธิภาพ  

## คำตอบอย่างรวดเร็ว
- **ไลบรารีใดที่ช่วยคุณค้นหาหนบาร์โค้ดเฉพาะ?** GroupDocs.Signature for Java  
- **เวลาในการตั้งค่าปกติ?** ประมาณ 5 นาทีเพื่อเพิ่มการพึ่งพา Maven/Gradle และใบอนุญาต  
- **ฉันสามารถจำกัดการค้นหาให้เฉพาะหน้าหนึ่งและหน้าสุดท้ายได้หรือไม่?** ใช่ – ใช้ `PagesSetup` เพื่อระบุหน้าที่ต้องการ  
- **รูปแบบบาร์โค้ดที่รองรับคืออะไร?** QR Code, Code128, Code39, DataMatrix, EAN/UPC, และอื่น ๆ  
- **ต้องการใบอนุญาตแบบจ่ายเงินสำหรับการใช้งานจริงหรือไม่?** จำเป็นต้องมีใบอนุญาตเต็มสำหรับการใช้งานจริง; เวอร์ชันทดลองใช้ได้สำหรับการประเมินผล  

## “การค้นหาหนบาร์โค้ดเฉพาะ” คืออะไร

การค้นหาหนบาร์โค้ดเฉพาะหมายถึงการสั่งให้เอนจินลายเซ็นค้นหาลายเซ็นบาร์โค้ดเฉพาะบนหน้าที่คุณสนใจเท่านั้น—เช่น หน้าแรก, หน้าสุดท้าย, หรือช่วงที่กำหนดเอง วิธีการที่มุ่งเน้นนี้ช่วยเร่งการประมวลผล, ลดการใช้หน่วยความจำ, และทำให้คุณสร้างฟีดแบ็ก UI ที่ตอบสนองได้  

## ทำไมต้องใช้ GroupDocs.Signature สำหรับงานนี้

GroupDocs.Signature ให้ API ระดับสูงที่ซ่อนรายละเอียดการถอดรหัสบาร์โค้ดระดับต่ำ, การเรนเดอร์หน้า, และการจัดการรูปแบบเอกสาร มันรองรับ **มากกว่า 20 รูปแบบบาร์โค้ด** และสามารถประมวลผล **เอกสารหลายร้อยหน้าโดยไม่ต้องโหลดไฟล์ทั้งหมดเข้าสู่หน่วยความจำ** ทำให้คุณมุ่งเน้นที่ตรรกะธุรกิจแทนการแยกวิเคราะห์ไฟล์  

## ข้อกำหนดเบื้องต้น

- **JDK 8+** ติดตั้งแล้ว  
- **Maven** หรือ **Gradle** สำหรับการจัดการการพึ่งพา  
- ความคุ้นเคยพื้นฐานกับคลาส, เมธอด, และการจัดการข้อยกเว้นของ Java  
- เข้าถึงใบอนุญาต GroupDocs.Signature (ทดลองหรือเต็ม)  

## การตั้งค่า GroupDocs.Signature สำหรับ Java

### การตั้งค่า Maven

Add the dependency to your `pom.xml`:

```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

### การตั้งค่า Gradle

Or include it in `build.gradle`:

```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

Prefer manual downloads? You can grab the latest release directly from the [GroupDocs download page](https://releases.groupdocs.com/signature/java/).

### การรับใบอนุญาตของคุณ

- **Free Trial** – เริ่มได้ทันที, ไม่มีข้อผูกมัด  
- **Temporary License** – เข้าถึงคุณสมบัติเต็มสำหรับการประเมิน  
- **Full License** – พร้อมใช้งานในการผลิต, ไม่จำกัดการใช้  

Verify the installation with a quick initialization snippet:

```java
import com.groupdocs.signature.Signature;

public class SignatureSetup {
    public static void main(String[] args) {
        // Initialize the Signature instance with the document path
        Signature signature = new Signature("YOUR_DOCUMENT_PATH");
        
        System.out.println("GroupDocs.Signature for Java initialized successfully.");
    }
}
```

> **เคล็ดลับมืออาชีพ:** แทนที่ `"YOUR_DOCUMENT_PATH"` ด้วยไฟล์ PDF, DOCX, หรือ XLSX จริง หากคอนโซลพิมพ์ข้อความสำเร็จ, คุณพร้อมเริ่มใช้งานแล้ว.

## ทำความเข้าใจประเภทลายเซ็นบาร์โค้ด

Barcodes embed machine‑readable data inside a document. Unlike handwritten signatures, they can store IDs, timestamps, URLs, or JSON payloads, making them ideal for automated verification.

| ประเภทบาร์โค้ด | การใช้งานที่ดีที่สุด | ความยาวข้อมูลทั่วไป |
|----------------|----------------------|----------------------|
| QR Code | ข้อมูลความหนาแน่นสูง, URL, ข้อความหลายบรรทัด | สูงสุด 4,296 ตัวอักษร |
| Code128 | หมายเลขติดตามแบบอัลฟานูเมอริก | ตัวแปร |
| Code39 | รหัสเก่าแบบง่าย | สูงสุด 43 ตัวอักษร |
| DataMatrix | ป้ายเล็ก, บันทึกสุขภาพ | สูงสุด 2,335 ตัวอักษร |
| EAN/UPC | การระบุสินค้า, การค้าปลีก | 8‑13 หลัก |

คุณมักใช้บาร์โค้ดเมื่อจำเป็นต้องอ่านด้วยเครื่องอย่างรวดเร็ว, ข้อมูลโครงสร้าง, หรือการลงลายเซ็นที่ตรวจจับการดัดแปลงได้.  

## วิธีการค้นหาหนบาร์โค้ดด้วย Java

`Signature` เป็นคลาสหลักที่แทนเอกสารที่จะประมวลผล โหลดเอกสารของคุณด้วย `new Signature("file.pdf")`, `BarcodeSearchOptions` กำหนดพารามิเตอร์สำหรับการค้นหาลายเซ็นบาร์โค้ด, และกำหนดให้มุ่งเป้าหมายหน้าที่ต้องการ, จากนั้นเรียก `signature.search(options)`. เมธอด `search` จะดำเนินการค้นหาโดยใช้ตัวเลือกที่ให้ไว้. เอนจินจะคืนรายการของอ็อบเจ็กต์ `BarcodeSignature` ที่มีหมายเลขหน้า, ข้อความที่ถอดรหัส, และพิกัดเรขาคณิต—ทั้งหมดในหนึ่งการเรียก. รูปแบบขั้นตอนเดียวนี้ลบความจำเป็นในการแยกการสกัดภาพหรือการถอดรหัสแบบกำหนดเอง.

เมื่อคุณเข้าใจกระบวนการโดยรวมแล้ว, มาเจาะลึกสามคุณลักษณะหลักที่คุณจะทำการใช้งาน.

### คุณลักษณะ 1: สมัครรับเหตุการณ์การค้นหาเอกสาร

#### ทำไมสิ่งนี้สำคัญ  
เมื่อประมวลผลชุดใหญ่, ฟีดแบ็กแบบเรียลไทม์ (เช่น แถบความคืบหน้า) ปรับปรุง UX และช่วยให้คุณตรวจจับการหยุดชะงักได้เร็ว.

#### คำอธิบาย  
`Signature` แทนเอกสารและให้ความสามารถในการสมัครรับเหตุการณ์.

Implementation

```java
Signature signature = new Signature("YOUR_DOCUMENT_PATH");
```

```java
signature.SearchStarted.add(new ProcessStartEventHandler() {
    public void invoke(Signature sender, ProcessStartEventArgs args) {
        System.out.println("Search process started at " + args.getStarted()
            + " with " + args.getTotalSignatures() + " total signatures to be put in document");
    }
});

signature.SearchProgress.add(new ProcessProgressEventHandler() {
    public void invoke(Signature sender, ProcessProgressEventArgs args) {
        System.out.println("Search progress. Processed " + args.getProcessedSignatures()
            + " signatures. Time spent " + args.getTicks() + " mlsec");
    }
});

signature.SearchCompleted.add(new ProcessCompleteEventHandler() {
    public void invoke(Signature sender, ProcessCompleteEventArgs args) {
        System.out.println("Search process completed at " + args.getCompleted()
            + " with " + args.getTotalSignatures() + " total signatures. Process took "
            + args.getTicks() + " mlsec");
    }
});
```

These three handlers give you start time, live progress, and final statistics—perfect for logging or UI updates.

### คุณลักษณะ 2: กำหนดค่าตัวเลือกการค้นหาบาร์โค้ดสำหรับหน้าที่เฉพาะ

#### ทำไมการควบคุมแบบละเอียดสำคัญ  
การสแกนทุกหน้าของสัญญา 200 หน้าใช้ทรัพยากร CPU อย่างไม่จำเป็น การมุ่งเป้าเฉพาะหน้าแรกและหน้าสุดท้ายสามารถลดเวลาทำงานได้ **สูงสุด 80 %**.

#### คำอธิบาย  
`PagesSetup` ระบุว่าหน้าใดบ้างที่จะรวมในการดำเนินการค้นหา.

Implementation

```java
import com.groupdocs.signature.domain.enums.TextMatchType;
import com.groupdocs.signature.options.search.BarcodeSearchOptions;

BarcodeSearchOptions options = new BarcodeSearchOptions();
```

```java
options.setAllPages(false); // Opt‑in selective page searching
options.setPageNumber(1);   // Starting page (optional)
```

```java
import com.groupdocs.signature.options.PagesSetup;

PagesSetup pagesSetup = new PagesSetup();
pagesSetup.setFirstPage(true);   // Include first page
pagesSetup.setLastPage(true);    // Include last page
pagesSetup.setOddPages(false);   // Skip odd pages
pagesSetup.setEvenPages(false);  // Skip even pages
options.setPagesSetup(pagesSetup);
```

```java
options.setMatchType(TextMatchType.Contains);
options.setText("12345");
```

- **Match types** ให้คุณปรับการค้นหาข้อความอย่างละเอียด (`Contains`, `Exact`, `StartsWith`, `EndsWith`).  
- ปรับ `setAllPages` และ `PagesSetup` เพื่อ **ค้นหาหนบาร์โค้ดเฉพาะ** เท่านั้น.

### คุณลักษณะ 3: ดำเนินการค้นหาและประมวลผลผลลัพธ์

#### ทำไมขั้นตอนนี้สำคัญ  
การค้นหาบาร์โค้ดเป็นเพียงครึ่งหนึ่งของเรื่อง—คุณต้องดำเนินการกับข้อมูล (เช่น ตรวจสอบ, เก็บ, หรือเรียกใช้เวิร์กโฟลว์).

#### คำอธิบาย  
`BarcodeSignature` แทนบาร์โค้ดที่ตรวจพบและมีคุณสมบัติต่าง ๆ เช่น หมายเลขหน้าและข้อความที่ถอดรหัส.

Implementation

```java
import java.util.List;
import com.groupdocs.signature.domain.signatures.BarcodeSignature;

try {
    List<BarcodeSignature> signatures = signature.search(BarcodeSignature.class, options);
    System.out.println("Source document contains following signatures.");
    
    for (BarcodeSignature barcodeSignature : signatures) {
        System.out.println("Barcode signature found at page " + barcodeSignature.getPageNumber()
            + " with type " + barcodeSignature.getEncodeType() + " and text " + barcodeSignature.getText());
    }
} catch (Exception e) {
    throw new RuntimeException(e.getMessage(), e);
}
```

You now have a list of `BarcodeSignature` objects, each exposing:

- `getPageNumber()` – ตำแหน่งหน้าที่บาร์โค้ดอยู่  
- `getEncodeType()` – QR, Code128, ฯลฯ  
- `getText()` – ข้อมูลที่ถอดรหัส  
- ตำแหน่ง (`getLeft()`, `getTop()`) และขนาด (`getWidth()`, `getHeight()`)

**ตัวอย่าง: ประมวลผลเฉพาะ QR code บนหน้าสุดท้าย**

```java
for (BarcodeSignature barcodeSignature : signatures) {
    if (barcodeSignature.getPageNumber() == lastPageNumber 
        && barcodeSignature.getEncodeType().equals("QRCode")) {
        // Process only QR codes from the final page
        processApprovalCode(barcodeSignature.getText());
    }
}
```

## การประยุกต์ใช้ในโลกจริง

| สถานการณ์ | วิธีที่การค้นหาหนบาร์โค้ดเฉพาะช่วยได้ |
|------------|------------------------------------------|
| การตรวจสอบสัญญากฎหมาย | ตรวจสอบอัตโนมัติแฮชใบรับรองที่เข้ารหัสด้วย QR บนหน้าลายเซ็น |
| การติดตามห่วงโซ่อุปทาน | ค้นหา ID การจัดส่ง Code128 บนหน้าแรก/สุดท้ายของรายการสินค้า |
| แบบฟอร์มยินยอมด้านสุขภาพ | ดึง DataMatrix ID ผู้ป่วยจากหน้ายินยอมสุดท้าย |
| การอัตโนมัติใบแจ้งหนี้ | ค้นหาบาร์โค้ดที่ขึ้นต้นด้วย “APPR‑” ใด ๆ บนใบแจ้งหนี้, จากนั้นส่งต่อ |

## ปัญหาที่พบบ่อยและวิธีแก้

### ปัญหา 1 – ไม่พบผลลัพธ์แม้ว่าจะเห็นบาร์โค้ด

```java
// Ensure you are not limiting pages too aggressively
options.setAllPages(true);
```  
If the barcode is embedded as a raster image, consider using GroupDocs.Image for image‑based detection.

หากบาร์โค้ดฝังเป็นภาพราสเตอร์, พิจารณาใช้ GroupDocs.Image สำหรับการตรวจจับแบบภาพ.

### ปัญหา 2 – ประสิทธิภาพช้าในไฟล์ขนาดใหญ่

```java
PagesSetup pagesSetup = new PagesSetup();
pagesSetup.setLastPage(true);  // Most signatures are on the last page
pagesSetup.setFirstPage(true);
options.setPagesSetup(pagesSetup);
```  
Targeted pages dramatically reduce processing time; a 150‑page PDF drops from ~4 seconds to <1 second when you limit the search to two pages.

การจำกัดหน้าช่วยลดเวลาประมวลผลอย่างมาก; PDF 150 หน้า ลดจาก ~4 วินาทีเป็น <1 วินาทีเมื่อจำกัดการค้นหาเพียงสองหน้า.

### ปัญหา 3 – TextMatchType ไม่พบบาร์โค้ดที่คาดหวัง

```java
String searchText = "12345".trim().toLowerCase();
options.setText(searchText);
options.setMatchType(TextMatchType.StartsWith); // Try a more permissive mode
```

### ปัญหา 4 – การรั่วของหน่วยความจำในลูปที่ทำงานนาน

```java
try (Signature signature = new Signature("document.pdf")) {
    List<BarcodeSignature> signatures = signature.search(BarcodeSignature.class, options);
    // Process signatures
}
```  
The try‑with‑resources block disposes the `Signature` instance automatically.

บล็อก try‑with‑resources จะทำลายอินสแตนซ์ `Signature` โดยอัตโนมัติ.

## แนวทางปฏิบัติที่ดีที่สุดสำหรับการใช้งานจริง

### การจัดการข้อผิดพลาดที่แข็งแรง

```java
try {
    List<BarcodeSignature> signatures = signature.search(BarcodeSignature.class, options);
} catch (com.groupdocs.signature.exception.GroupDocsSignatureException e) {
    logger.error("GroupDocs error: " + e.getMessage());
} catch (Exception e) {
    logger.error("Unexpected error: " + e.getMessage(), e);
}
```

### แคชผลลัพธ์เมื่อเอกสารไม่เปลี่ยนแปลง

```java
Map<String, List<BarcodeSignature>> cache = new ConcurrentHashMap<>();

public List<BarcodeSignature> getCachedSignatures(String docId) {
    return cache.computeIfAbsent(docId, id -> performSearch(id));
}
```

### ใช้เหตุการณ์ความคืบหน้าเพื่อฟีดแบ็ก UI

```java
signature.SearchProgress.add(new ProcessProgressEventHandler() {
    public void invoke(Signature sender, ProcessProgressEventArgs args) {
        int percent = (args.getProcessedSignatures() * 100) / args.getTotalSignatures();
        updateProgressBar(percent);
    }
});
```

### ตรวจสอบ payload ของบาร์โค้ด

```java
for (BarcodeSignature barcodeSignature : signatures) {
    String text = barcodeSignature.getText();
    if (!text.matches("APPR-\\d{4}-\\d{3}")) {
        logger.warn("Invalid format: " + text);
        continue;
    }
    if (!validateChecksum(text)) {
        logger.error("Checksum failed for: " + text);
        flagForManualReview(document);
    }
}
```

### ปรับแต่งการเลือกหน้าให้เหมาะกับประเภทเอกสาร

```java
PagesSetup contractsSetup = new PagesSetup();
contractsSetup.setLastPage(true); // Contracts usually signed on last page
options.setPagesSetup(contractsSetup);
```

### กรองตามประเภทบาร์โค้ดหลังการค้นหา (หากต้องการเฉพาะ QR code)

```java
for (BarcodeSignature sig : signatures) {
    if ("QRCode".equals(sig.getEncodeType())) {
        // Process QR code
    }
}
```

### ดึงขนาดภาพบาร์โค้ด (หากต้องการสำหรับการเรนเดอร์)

```java
for (BarcodeSignature sig : signatures) {
    int width = sig.getWidth();
    int height = sig.getHeight();
    // Use dimensions for overlay or thumbnail generation
}
```

## คำถามที่พบบ่อย

**ถาม: ฉันสามารถค้นหาหลายรูปแบบบาร์โค้ดในหนึ่งการเรียกได้หรือไม่?**  
**ตอบ:** ใช่. `BarcodeSearchOptions` จะค้นหาทุกรูปแบบที่รองรับโดยค่าเริ่มต้น. กรองผลลัพธ์โดย `getEncodeType()` หากคุณต้องการเฉพาะประเภทบางอย่าง.

**ถาม: ฉันจะจัดการกับเอกสารที่มีบาร์โค้ดและลายเซ็นภาพพร้อมกันอย่างไร?**  
**ตอบ:** ทำการค้นหาแยกกัน—ใช้ `BarcodeSignature.class` สำหรับบาร์โค้ดและ `ImageSignature.class` สำหรับลายเซ็นภาพ, จากนั้นรวมผลลัพธ์ตามต้องการ.

**ถาม: ผลกระทบต่อประสิทธิภาพของการค้นหาทุกหน้ากับการค้นหาเฉพาะหน้ามีอย่างไร?**  
**ตอบ:** การสแกนทุกหน้าของ PDF 50 หน้าอาจใช้ 3–5 วินาที. การจำกัดเฉพาะหน้าแรก + หน้าสุดท้ายมักเสร็จภายใน <1 วินาที.

**ถาม: วิธีนี้ทำงานกับ PDF ที่สแกน (ภาพราสเตอร์) หรือไม่?**  
**ตอบ:** ทำได้เฉพาะเมื่อบาร์โค้ดถูกเพิ่มเป็นอ็อบเจ็กต์ลายเซ็นดิจิทัล. สำหรับบาร์โค้ดที่เป็นภาพราสเตอร์เท่านั้น, คุณจะต้องใช้ตัวตรวจจับบาร์โค้ดแบบภาพ (เช่น GroupDocs.Barcode).

**ถาม: ฉันจะตรวจสอบว่าลายเซ็นบาร์โค้ดไม่ได้ถูกดัดแปลงได้อย่างไร?**  
**ตอบ:** ฝังแฮชหรือลายเซ็นดิจิทัลใน payload ของบาร์โค้ด, จากนั้นคำนวณแฮชใหม่จากข้อมูลต้นฉบับและเปรียบเทียบ. วิธีนี้ต้องใช้คีย์หรือใบรับรองการลงลายเซ็นต้นฉบับ.

**อัปเดตล่าสุด:** 2026-06-21  
**ทดสอบด้วย:** GroupDocs.Signature 23.12 for Java  
**ผู้เขียน:** GroupDocs  

## บทแนะนำที่เกี่ยวข้อง

- [วิธีเพิ่มบาร์โค้ดลงใน PDF ด้วย Java และ GroupDocs.Signature](/signature/java/barcode-signatures/sign-pdf-barcode-groupdocs-signature-java/)
- [วิธีตรวจสอบลายเซ็นบาร์โค้ดใน Java ด้วย GroupDocs.Signature](/signature/java/search-verification/groupdocs-signature-java-document-verification/)
- [การสมัครรับเหตุการณ์ GroupDocs Signature Java - ติดตามการตรวจสอบแบบเรียลไทม์](/signature/java/event-handling/implement-document-verification-events-groupdocs-java/)