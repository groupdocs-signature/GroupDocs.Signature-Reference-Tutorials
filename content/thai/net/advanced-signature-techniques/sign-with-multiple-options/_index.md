---
title: การลงนามด้วยหลายตัวเลือก
linktitle: การลงนามด้วยหลายตัวเลือก
second_title: GroupDocs.Signature .NET API
description: เรียนรู้วิธีเซ็นเอกสารด้วยหลายตัวเลือกโดยใช้ GroupDocs.Signature สำหรับ .NET เพิ่มความปลอดภัยให้กับเอกสารด้วยข้อความ บาร์โค้ด รหัส QR ดิจิทัล และรูปภาพ
type: docs
weight: 14
url: /th/net/advanced-signature-techniques/sign-with-multiple-options/
---
## การแนะนำ
ในบทช่วยสอนนี้ เราจะสำรวจวิธีการลงนามในเอกสารโดยใช้ตัวเลือกลายเซ็นหลายรายการโดยใช้ไลบรารี GroupDocs.Signature สำหรับ .NET การลงนามในเอกสารด้วยตัวเลือกต่างๆ เช่น ข้อความ บาร์โค้ด รหัส QR ลายเซ็นดิจิทัล รูปภาพ และเมตาดาต้า สามารถให้ความคล่องตัวและเพิ่มความปลอดภัยของเอกสาร
## ข้อกำหนดเบื้องต้น
ก่อนที่จะเริ่มต้น ตรวจสอบให้แน่ใจว่าคุณมีข้อกำหนดเบื้องต้นต่อไปนี้:
1.  GroupDocs.Signature สำหรับ .NET Library: ดาวน์โหลดและติดตั้ง GroupDocs.Signature สำหรับ .NET Library จาก[ที่นี่](https://releases.groupdocs.com/signature/net/).
2. สภาพแวดล้อมการพัฒนา: ตั้งค่าสภาพแวดล้อมการพัฒนาโดยติดตั้ง .NET Framework
3. เอกสารที่จะลงนาม: เตรียมเอกสาร (เช่น example.docx) ที่คุณต้องการลงนาม
4. ใบรับรองและรูปภาพ: เตรียมใบรับรองและรูปภาพที่จำเป็นสำหรับลายเซ็นดิจิทัลและรูปภาพ

## นำเข้าเนมสเปซ
ขั้นแรก นำเข้าเนมสเปซที่จำเป็นเพื่อใช้ไลบรารี GroupDocs.Signature ในแอปพลิเคชัน .NET ของคุณ:
```csharp
using System;
using System.IO;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## ขั้นตอนที่ 1: โหลดเอกสาร
```csharp
string filePath = "sample.docx";
string outputFilePath = Path.Combine("Your Document Directory", "SignWithMultiple", "SignWithMultiple.docx");
using (Signature signature = new Signature(filePath))
{
    // รหัสของคุณดำเนินต่อไป...
}
```
## ขั้นตอนที่ 2: กำหนดตัวเลือกลายเซ็น
กำหนดตัวเลือกลายเซ็นหลายประเภทและการตั้งค่าต่างๆ เช่น ลายเซ็นข้อความ บาร์โค้ด รหัส QR ลายเซ็นดิจิทัล รูปภาพ และเมตาดาต้า:
```csharp
TextSignOptions textOptions = new TextSignOptions("Text signature")
{
    VerticalAlignment = VerticalAlignment.Top,
    HorizontalAlignment = HorizontalAlignment.Left
};
BarcodeSignOptions barcodeOptions = new BarcodeSignOptions("123456")
{
    EncodeType = BarcodeTypes.Code128,
    Left = 0,
    Top = 150,
    Height = 50,
    Width = 200
};
// กำหนดตัวเลือกลายเซ็นอื่นๆ (เช่น โค้ด QR, ดิจิทัล, รูปภาพ, ข้อมูลเมตา)...
```
## ขั้นตอนที่ 3: สร้างรายการตัวเลือกลายเซ็น
กำหนดรายการตัวเลือกลายเซ็นที่มีตัวเลือกที่กำหนดไว้ก่อนหน้านี้ทั้งหมด:
```csharp
List<SignOptions> listOptions = new List<SignOptions>();
listOptions.Add(textOptions);
listOptions.Add(barcodeOptions);
// เพิ่มตัวเลือกลายเซ็นอื่นๆ ลงในรายการ...
```
## ขั้นตอนที่ 4: ลงนามในเอกสาร
ลงนามในเอกสารด้วยรายการตัวเลือกลายเซ็นและบันทึกเอกสารที่ลงนาม:
```csharp
SignResult result = signature.Sign(outputFilePath, listOptions);
Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).\nFile saved at {outputFilePath}.");
```

## บทสรุป
การลงนามเอกสารด้วยตัวเลือกที่หลากหลายโดยใช้ GroupDocs.Signature สำหรับ .NET มอบโซลูชันที่มีประสิทธิภาพในการเพิ่มความปลอดภัยและความคล่องตัวของเอกสาร ด้วยการทำตามขั้นตอนที่ระบุไว้ในบทช่วยสอนนี้ คุณสามารถรวมลายเซ็นประเภทต่างๆ เข้ากับแอปพลิเคชัน .NET ของคุณได้อย่างราบรื่น
## คำถามที่พบบ่อย
### ฉันสามารถใช้รูปภาพที่กำหนดเองสำหรับลายเซ็นดิจิทัลได้หรือไม่
ได้ คุณสามารถระบุรูปภาพที่กำหนดเองสำหรับลายเซ็นดิจิทัลได้โดยใช้ไลบรารี GroupDocs.Signature
### GroupDocs.Signature เข้ากันได้กับรูปแบบเอกสารที่แตกต่างกันหรือไม่
ใช่ GroupDocs.Signature รองรับรูปแบบเอกสารที่หลากหลาย รวมถึง DOCX, PDF, PPTX และอื่นๆ
### ฉันสามารถปรับแต่งลักษณะที่ปรากฏของลายเซ็นข้อความได้หรือไม่
คุณสามารถปรับแต่งลักษณะที่ปรากฏของลายเซ็นข้อความ รวมถึงขนาดตัวอักษร สี และสไตล์ได้อย่างแน่นอน
### GroupDocs.Signature มีการเข้ารหัสสำหรับลายเซ็นดิจิทัลหรือไม่
ใช่ GroupDocs.Signature มีตัวเลือกการเข้ารหัสสำหรับลายเซ็นดิจิทัลเพื่อให้มั่นใจในความปลอดภัยของเอกสาร
### มีรุ่นทดลองใช้สำหรับ GroupDocs.Signature สำหรับ .NET หรือไม่
 ใช่ คุณสามารถดาวน์โหลด GroupDocs.Signature สำหรับ .NET เวอร์ชันทดลองใช้ฟรีได้จาก[ที่นี่](https://releases.groupdocs.com/).