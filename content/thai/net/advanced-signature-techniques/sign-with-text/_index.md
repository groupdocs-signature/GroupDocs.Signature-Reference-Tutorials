---
title: การลงนามด้วยข้อความโดยใช้ GroupDocs.Signature สำหรับ .NET
linktitle: การลงนามด้วยข้อความ
second_title: GroupDocs.Signature .NET API
description: เรียนรู้วิธีเซ็นเอกสารด้วยข้อความโดยใช้ GroupDocs.Signature สำหรับ .NET คำแนะนำทีละขั้นตอนสำหรับการเพิ่มลายเซ็นข้อความโดยทางโปรแกรม
weight: 17
url: /th/net/advanced-signature-techniques/sign-with-text/
---
## การแนะนำ
ในยุคดิจิทัล การลงนามในเอกสารทางอิเล็กทรอนิกส์กลายเป็นแนวทางปฏิบัติมาตรฐาน ซึ่งช่วยประหยัดเวลาและทรัพยากร GroupDocs.Signature สำหรับ .NET นำเสนอโซลูชันที่ครอบคลุมสำหรับการเพิ่มลายเซ็นข้อความให้กับรูปแบบเอกสารต่างๆ โดยทางโปรแกรม ในบทช่วยสอนนี้ เราจะแนะนำคุณตลอดขั้นตอนการลงนามเอกสารด้วยข้อความโดยใช้ GroupDocs.Signature สำหรับ .NET
## ข้อกำหนดเบื้องต้น
ก่อนที่เราจะเจาะลึกบทช่วยสอน ตรวจสอบให้แน่ใจว่าคุณมีข้อกำหนดเบื้องต้นดังต่อไปนี้:
1.  GroupDocs.Signature for .NET: ตรวจสอบให้แน่ใจว่าคุณได้ติดตั้งไลบรารี GroupDocs.Signature for .NET แล้ว คุณสามารถดาวน์โหลดได้จาก[ที่นี่](https://releases.groupdocs.com/signature/net/).
2. สภาพแวดล้อมการพัฒนา: มีสภาพแวดล้อมการทำงานที่ตั้งค่าไว้สำหรับการพัฒนา .NET
3. เอกสาร: เตรียมเอกสาร (เช่น PDF, Word) ที่คุณต้องการเซ็นชื่อด้วยข้อความ

## นำเข้าเนมสเปซ
ขั้นแรก คุณต้องนำเข้าเนมสเปซที่จำเป็นลงในโปรเจ็กต์ .NET ของคุณเพื่อใช้ฟังก์ชัน GroupDocs.Signature
```csharp
using System;
using System.IO;
using System.Drawing;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

แบ่งขั้นตอนการเซ็นเอกสารด้วยข้อความออกเป็นหลายขั้นตอน:
## ขั้นตอนที่ 1: โหลดเอกสาร
โหลดเอกสารที่คุณต้องการลงนามด้วยข้อความ
```csharp
string filePath = "sample.pdf"; // เส้นทางไปยังเอกสาร
string fileName = Path.GetFileName(filePath);
```
## ขั้นตอนที่ 2: ตั้งค่าเส้นทางไฟล์เอาต์พุต
กำหนดเส้นทางไฟล์เอาต์พุตที่จะบันทึกเอกสารที่เซ็นชื่อ
```csharp
string outputFilePath = Path.Combine("Your Document Directory", "SignWithText", fileName);
```
## ขั้นตอนที่ 3: สร้างตัวเลือกลายเซ็น
ตั้งค่าตัวเลือกสำหรับลายเซ็นข้อความ รวมถึงเนื้อหาข้อความ ตำแหน่ง ขนาด สี และแบบอักษร
```csharp
TextSignOptions options = new TextSignOptions("John Smith")
{
    Left = 50, // กำหนดตำแหน่งลายเซ็น
    Top = 200,
    Width = 100, // ตั้งค่าสี่เหลี่ยมลายเซ็น
    Height = 30,
    ForeColor = Color.Red, // ตั้งค่าสีข้อความ
    Font = new SignatureFont { Size = 14, FamilyName = "Comic Sans MS" } // ตั้งค่าแบบอักษร
};
```
## ขั้นตอนที่ 4: ลงนามในเอกสาร
ใช้ GroupDocs.Signature เพื่อลงนามเอกสารด้วยตัวเลือกที่ระบุ และบันทึกเอกสารที่ลงนามไปยังเส้นทางไฟล์เอาต์พุต
```csharp
using (Signature signature = new Signature(filePath))
{
    SignResult result = signature.Sign(outputFilePath, options); // เซ็นเอกสาร
    Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).\nFile saved at {outputFilePath}.");
}
```

## บทสรุป
ในบทช่วยสอนนี้ เราได้เรียนรู้วิธีลงนามเอกสารด้วยข้อความโดยใช้ GroupDocs.Signature สำหรับ .NET เมื่อทำตามขั้นตอนเหล่านี้ คุณจะสามารถเพิ่มลายเซ็นข้อความลงในเอกสารของคุณได้อย่างมีประสิทธิภาพโดยทางโปรแกรม ซึ่งช่วยเพิ่มความปลอดภัยและความถูกต้อง
## คำถามที่พบบ่อย
### ฉันสามารถปรับแต่งลักษณะที่ปรากฏของลายเซ็นข้อความได้หรือไม่
ใช่ คุณสามารถปรับแต่งพารามิเตอร์ต่างๆ เช่น สี แบบอักษร ขนาด และตำแหน่งของลายเซ็นข้อความได้ตามความต้องการของคุณ
### GroupDocs.Signature เข้ากันได้กับเอกสารหลายรูปแบบหรือไม่
ใช่ GroupDocs.Signature รองรับรูปแบบเอกสารที่หลากหลาย รวมถึง PDF, Word, Excel, PowerPoint และอื่นๆ
### ฉันสามารถเพิ่มลายเซ็นข้อความหลายรายการลงในเอกสารเดียวได้หรือไม่
แน่นอน คุณสามารถเพิ่มลายเซ็นข้อความหลายรายการลงในเอกสารได้ โดยแต่ละลายเซ็นมีตัวเลือกการปรับแต่งของตัวเอง
### GroupDocs.Signature รับประกันความสมบูรณ์ของเอกสารหลังจากการลงนามหรือไม่
ใช่ GroupDocs.Signature ใช้อัลกอริธึมการเข้ารหัสที่มีประสิทธิภาพเพื่อรับรองความสมบูรณ์ของเอกสารและป้องกันการปลอมแปลงหลังจากการลงนาม
### มีรุ่นทดลองให้ทดสอบก่อนซื้อหรือไม่?
 ใช่ คุณสามารถดาวน์โหลดเวอร์ชันทดลองใช้ฟรีได้จาก[ที่นี่](https://releases.groupdocs.com/) เพื่อสำรวจคุณสมบัติก่อนตัดสินใจซื้อ