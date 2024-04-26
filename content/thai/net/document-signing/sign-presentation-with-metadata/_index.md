---
title: ลงนามการนำเสนอด้วยข้อมูลเมตา
linktitle: ลงนามการนำเสนอด้วยข้อมูลเมตา
second_title: GroupDocs.Signature .NET API
description: เรียนรู้วิธีเซ็นชื่อไฟล์งานนำเสนอด้วยข้อมูลเมตาโดยใช้ GroupDocs.Signature สำหรับ .NET ปรับปรุงความสมบูรณ์ของเอกสารและเพิ่มข้อมูลอันมีค่า
type: docs
weight: 12
url: /th/net/document-signing/sign-presentation-with-metadata/
---
## การแนะนำ
ในบทช่วยสอนนี้ เราจะเรียนรู้วิธีเซ็นชื่อไฟล์งานนำเสนอ (PPTX) ด้วยข้อมูลเมตาโดยใช้ GroupDocs.Signature สำหรับไลบรารี .NET การลงนามในงานนำเสนอด้วยข้อมูลเมตาจะเพิ่มข้อมูลที่เป็นประโยชน์ให้กับเอกสาร เช่น ชื่อผู้เขียน วันที่สร้าง รหัสเอกสาร รหัสลายเซ็น และค่าตัวเลขต่างๆ
## ข้อกำหนดเบื้องต้น
ก่อนที่เราจะเริ่ม ตรวจสอบให้แน่ใจว่าคุณมีสิ่งต่อไปนี้:
1.  GroupDocs.Signature สำหรับ .NET Library: ดาวน์โหลดและติดตั้งไลบรารีจาก[ที่นี่](https://releases.groupdocs.com/signature/net/).
2. สภาพแวดล้อมการพัฒนา: ตรวจสอบให้แน่ใจว่าคุณได้ตั้งค่าสภาพแวดล้อมการพัฒนา .NET แล้ว
3. ไฟล์การนำเสนอ: เตรียมไฟล์การนำเสนอตัวอย่าง (รูปแบบ PPTX) พร้อมสำหรับการลงนาม
4. ความเข้าใจพื้นฐานของ C#: ความคุ้นเคยกับภาษาการเขียนโปรแกรม C# จะเป็นประโยชน์

## นำเข้าเนมสเปซ
ก่อนที่จะเจาะลึกโค้ด มานำเข้าเนมสเปซที่จำเป็นก่อน:
```csharp
using System;
using System.IO;
    using GroupDocs.Signature;
    using GroupDocs.Signature.Domain;
    using GroupDocs.Signature.Options;
```
## ขั้นตอนที่ 1: โหลดไฟล์การนำเสนอ
```csharp
string filePath = "sample.pptx";
```
 แทนที่`"sample.pptx"` พร้อมเส้นทางไปยังไฟล์การนำเสนอของคุณ
## ขั้นตอนที่ 2: ระบุเส้นทางไฟล์เอาต์พุต
```csharp
string outputFilePath = Path.Combine("Your Document Directory", "SignPresentationWithMetadata", "SignedWithMetadata.pptx");
```
ระบุไดเร็กทอรีที่คุณต้องการบันทึกไฟล์งานนำเสนอที่ลงนามพร้อมกับชื่อไฟล์
## ขั้นตอนที่ 3: เริ่มต้นวัตถุลายเซ็น
```csharp
using (Signature signature = new Signature(filePath))
```
เริ่มต้นออบเจ็กต์ลายเซ็นโดยระบุเส้นทางไปยังไฟล์งานนำเสนอ
## ขั้นตอนที่ 4: กำหนดตัวเลือกเครื่องหมายข้อมูลเมตา
```csharp
MetadataSignOptions options = new MetadataSignOptions();
```
สร้างอินสแตนซ์ของ MetadataSignOptions เพื่อกำหนดตัวเลือกการลงนามข้อมูลเมตา
## ขั้นตอนที่ 5: สร้างลายเซ็นข้อมูลเมตา
```csharp
PresentationMetadataSignature[] signatures = new PresentationMetadataSignature[]
{
    new PresentationMetadataSignature("Author", "Mr.Scherlock Holmes"),
    new PresentationMetadataSignature("CreatedOn", DateTime.Now),
    new PresentationMetadataSignature("DocumentId", 123456),
    new PresentationMetadataSignature("SignatureId", 123.456D),
    new PresentationMetadataSignature("Amount", 123.456M),
    new PresentationMetadataSignature("Total", 123.456F)
};
```
สร้างอาร์เรย์ของออบเจ็กต์ PresentationMetadataSignature ซึ่งแต่ละออบเจ็กต์จะแสดงลายเซ็นข้อมูลเมตา คุณสามารถเพิ่มข้อมูลเมตาประเภทต่างๆ ได้ รวมถึงสตริง DateTime จำนวนเต็ม สองเท่า ทศนิยม และทศนิยม
## ขั้นตอนที่ 6: เพิ่มลายเซ็นให้กับตัวเลือก
```csharp
options.Signatures.AddRange(signatures);
```
เพิ่มลายเซ็นข้อมูลเมตาที่สร้างขึ้นไปยังวัตถุ MetadataSignOptions
## ขั้นตอนที่ 7: ลงนามในเอกสาร
```csharp
SignResult result = signature.Sign(outputFilePath, options);
```
เซ็นชื่อไฟล์งานนำเสนอด้วยข้อมูลเมตาโดยใช้ตัวเลือกที่ระบุ และบันทึกไฟล์ที่เซ็นชื่อลงในพาธเอาต์พุต
## ขั้นตอนที่ 8: แสดงผล
```csharp
Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).\nFile saved at {outputFilePath}.");
```
แสดงข้อความแสดงความสำเร็จพร้อมกับจำนวนลายเซ็นที่ใช้และเส้นทางที่บันทึกไฟล์ที่เซ็นชื่อ

## บทสรุป
ในบทช่วยสอนนี้ เราได้เรียนรู้วิธีลงนามไฟล์งานนำเสนอด้วยข้อมูลเมตาโดยใช้ไลบรารี GroupDocs.Signature สำหรับ .NET การเพิ่มลายเซ็นเมตาดาต้าช่วยปรับปรุงความสมบูรณ์ของเอกสารและให้ข้อมูลอันมีค่าเกี่ยวกับเนื้อหาในเอกสาร

## คำถามที่พบบ่อย
### ฉันสามารถเซ็นเอกสารรูปแบบอื่นนอกเหนือจาก PPTX ด้วยข้อมูลเมตาโดยใช้ GroupDocs.Signature สำหรับ .NET ได้หรือไม่
ใช่ GroupDocs.Signature รองรับรูปแบบเอกสารที่หลากหลาย รวมถึง Word, Excel, PDF และอื่นๆ สำหรับการเซ็นชื่อด้วยเมตาดาต้า
### GroupDocs.Signature สำหรับ .NET เข้ากันได้กับ .NET Core หรือไม่
ใช่ ไลบรารีเข้ากันได้กับทั้ง .NET Framework และ .NET Core
### ฉันสามารถปรับแต่งลักษณะที่ปรากฏของลายเซ็นข้อมูลเมตาได้หรือไม่
ได้ คุณสามารถปรับแต่งลักษณะที่ปรากฏ ตำแหน่ง และคุณสมบัติอื่นๆ ของลายเซ็นเมทาดาทาได้ตามความต้องการของคุณ
### GroupDocs.Signature สำหรับ .NET มีการเข้ารหัสสำหรับเอกสารที่ลงนามหรือไม่
ใช่ GroupDocs.Signature มีตัวเลือกการเข้ารหัสเพื่อรักษาความปลอดภัยเอกสารที่ลงนามจากการเข้าถึงโดยไม่ได้รับอนุญาต
### มีรุ่นทดลองให้ทดสอบก่อนซื้อหรือไม่?
 ใช่ คุณสามารถทดลองใช้ GroupDocs.Signature สำหรับ .NET ได้ฟรีจาก[ที่นี่](https://releases.groupdocs.com/).