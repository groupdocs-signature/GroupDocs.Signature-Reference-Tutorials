---
title: ลงนาม PDF ด้วยข้อมูลเมตา
linktitle: ลงนาม PDF ด้วยข้อมูลเมตา
second_title: GroupDocs.Signature .NET API
description: เรียนรู้วิธีลงนามในเอกสาร PDF ด้วยข้อมูลเมตาโดยใช้ GroupDocs.Signature สำหรับ .NET เพิ่มความสามารถในการตรวจสอบย้อนกลับและความถูกต้องของเอกสารได้อย่างง่ายดาย
type: docs
weight: 11
url: /th/net/document-signing/sign-pdf-with-metadata/
---
## การแนะนำ
ในบทช่วยสอนนี้ เราจะเรียนรู้วิธีลงนามในเอกสาร PDF ด้วยข้อมูลเมตาโดยใช้ GroupDocs.Signature สำหรับ .NET การเพิ่มข้อมูลเมตาลงใน PDF สามารถให้ข้อมูลเพิ่มเติมเกี่ยวกับเอกสาร เช่น ผู้เขียน วันที่สร้าง รหัสเอกสาร และอื่นๆ
## ข้อกำหนดเบื้องต้น
ก่อนที่เราจะเริ่ม ตรวจสอบให้แน่ใจว่าคุณมีสิ่งต่อไปนี้:
1.  GroupDocs.Signature สำหรับ .NET: คุณสามารถดาวน์โหลดได้จาก[ที่นี่](https://releases.groupdocs.com/signature/net/).
2. เอกสาร PDF: เตรียมไฟล์ PDF ตัวอย่างให้พร้อมสำหรับการลงนาม
3. ความรู้พื้นฐานเกี่ยวกับการเขียนโปรแกรม C#: จำเป็นต้องมีความคุ้นเคยกับไวยากรณ์ C# เพื่อทำความเข้าใจตัวอย่างโค้ด
## นำเข้าเนมสเปซ
ขั้นแรก ตรวจสอบให้แน่ใจว่าคุณนำเข้าเนมสเปซที่จำเป็นเพื่อเข้าถึงคลาสและวิธีการที่จำเป็น:
```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## ขั้นตอนที่ 1: โหลดเอกสาร PDF
โหลดเอกสาร PDF ที่คุณต้องการลงนาม:
```csharp
string filePath = "sample.pdf";
```
## ขั้นตอนที่ 2: ระบุเส้นทางไฟล์เอาต์พุต
กำหนดเส้นทางของไฟล์เอาต์พุตที่จะบันทึก PDF ที่ลงนามพร้อมข้อมูลเมตา:
```csharp
string outputFilePath = Path.Combine("Your Document Directory", "SignPdfWithMetadata", "SignedWithMetadata.pdf");
```
## ขั้นตอนที่ 3: สร้างอินสแตนซ์ลายเซ็น
เริ่มต้นอินสแตนซ์ลายเซ็นโดยระบุเส้นทางไปยังเอกสาร PDF:
```csharp
using (Signature signature = new Signature(filePath))
{
    // รหัสที่เกี่ยวข้องกับลายเซ็นจะอยู่ที่นี่
}
```
## ขั้นตอนที่ 4: กำหนดตัวเลือกข้อมูลเมตา
สร้าง MetadataSignOptions และเพิ่มฟิลด์ข้อมูลเมตาด้วยค่าที่เกี่ยวข้อง:
```csharp
MetadataSignOptions options = new MetadataSignOptions();
options
    .Add(new PdfMetadataSignature("Author", "Mr.Sherlock Holmes")) // ค่าสตริง
    .Add(new PdfMetadataSignature("CreatedOn", DateTime.Now))       // ค่าวันที่และเวลา
    .Add(new PdfMetadataSignature("DocumentId", 123456))            // ค่าจำนวนเต็ม
    .Add(new PdfMetadataSignature("SignatureId", 123.456D))         // ค่าสองเท่า
    .Add(new PdfMetadataSignature("Amount", 123.456M))              // ค่าทศนิยม
    .Add(new PdfMetadataSignature("Total", 123.456F));              // มูลค่าลอยตัว
```
## ขั้นตอนที่ 5: ลงนามในเอกสาร
ลงนามในเอกสาร PDF ด้วยตัวเลือกข้อมูลเมตาที่ระบุ และบันทึกเอกสารที่ลงนาม:
```csharp
SignResult result = signature.Sign(outputFilePath, options);
Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).\nFile saved at {outputFilePath}.");
```

## บทสรุป
ในบทช่วยสอนนี้ เราได้กล่าวถึงวิธีการลงนามในเอกสาร PDF ด้วยข้อมูลเมตาโดยใช้ GroupDocs.Signature สำหรับ .NET ด้วยการทำตามคำแนะนำทีละขั้นตอน คุณสามารถเพิ่มข้อมูลเมตาดาต้า เช่น ผู้เขียน วันที่สร้าง และอื่นๆ ลงในไฟล์ PDF ของคุณได้อย่างง่ายดาย ซึ่งช่วยเพิ่มอรรถประโยชน์และความสามารถในการตรวจสอบย้อนกลับ
## คำถามที่พบบ่อย
### ฉันสามารถเพิ่มฟิลด์ข้อมูลเมตาที่กำหนดเองลงในเอกสาร PDF ของฉันได้หรือไม่
ได้ คุณสามารถเพิ่มฟิลด์ข้อมูลเมตาที่กำหนดเองได้โดยการระบุชื่อฟิลด์และค่าที่เกี่ยวข้องโดยใช้ GroupDocs.Signature สำหรับ .NET
### GroupDocs.Signature สำหรับ .NET เข้ากันได้กับ .NET Framework ทุกเวอร์ชันหรือไม่
GroupDocs.Signature สำหรับ .NET เข้ากันได้กับ .NET Framework เวอร์ชันต่างๆ ทำให้มั่นใจได้ถึงความยืดหยุ่นและความสะดวกในการบูรณาการ
### GroupDocs.Signature รองรับการเซ็นเอกสารรูปแบบอื่นนอกเหนือจาก PDF หรือไม่
ใช่ GroupDocs.Signature รองรับรูปแบบเอกสารที่หลากหลาย รวมถึง Word, Excel, PowerPoint และอื่นๆ
### ฉันสามารถเซ็นเอกสารหลายฉบับพร้อมกันโดยใช้ GroupDocs.Signature สำหรับ .NET ได้หรือไม่
ได้ คุณสามารถลงนามในเอกสารหลายฉบับพร้อมกันได้โดยการวนซ้ำรายการไฟล์และใช้กระบวนการลายเซ็นโดยทางโปรแกรม
### มีการสนับสนุนทางเทคนิคสำหรับผู้ใช้ GroupDocs.Signature หรือไม่
 ใช่ GroupDocs ให้การสนับสนุนด้านเทคนิคโดยเฉพาะผ่านทางฟอรัม คุณสามารถเข้าถึงฟอรั่มการสนับสนุน[ที่นี่](https://forum.groupdocs.com/c/signature/13).