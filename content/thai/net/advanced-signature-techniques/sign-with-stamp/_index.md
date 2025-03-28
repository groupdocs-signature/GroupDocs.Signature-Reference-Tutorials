---
title: การลงนามด้วย Stamp โดยใช้ GroupDocs.Signature
linktitle: ลงนามกับแสตมป์
second_title: GroupDocs.Signature .NET API
description: เรียนรู้วิธีเพิ่มลายเซ็นตราประทับลงในเอกสาร .NET ของคุณอย่างง่ายดายด้วย GroupDocs.Signature สำหรับ .NET เพิ่มความปลอดภัยให้กับเอกสาร
weight: 16
url: /th/net/advanced-signature-techniques/sign-with-stamp/
---

# การลงนามด้วย Stamp โดยใช้ GroupDocs.Signature

## การแนะนำ
ในบทช่วยสอนนี้ เราจะแนะนำคุณตลอดขั้นตอนการลงนามเอกสารพร้อมตราประทับโดยใช้ GroupDocs.Signature สำหรับ .NET เมื่อปฏิบัติตามคำแนะนำทีละขั้นตอนเหล่านี้ คุณจะสามารถเพิ่มลายเซ็นแสตมป์ลงในเอกสารของคุณได้อย่างง่ายดาย
## ข้อกำหนดเบื้องต้น
ก่อนที่เราจะเริ่มต้น ตรวจสอบให้แน่ใจว่าคุณมีข้อกำหนดเบื้องต้นดังต่อไปนี้:
1.  GroupDocs.Signature สำหรับ .NET SDK: ดาวน์โหลดและติดตั้ง SDK จาก[เว็บไซต์](https://releases.groupdocs.com/signature/net/).
2. สภาพแวดล้อมการพัฒนา: ตรวจสอบให้แน่ใจว่าคุณมีสภาพแวดล้อมการพัฒนาที่เหมาะสมสำหรับการพัฒนา .NET
3. เอกสารที่จะลงนาม: เตรียมเอกสาร (เช่น PDF) ที่คุณต้องการลงนามด้วยตราประทับ

## การนำเข้าเนมสเปซ
เริ่มต้นด้วยการนำเข้าเนมสเปซที่จำเป็นในโครงการของคุณ:
```csharp
using System;
using System.IO;
using System.Drawing;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## ขั้นตอนที่ 1: โหลดเอกสาร
```csharp
string filePath = "sample.pdf";
using (Signature signature = new Signature(filePath))
{
    // รหัสของคุณอยู่ที่นี่
}
```
## ขั้นตอนที่ 2: ตั้งค่าตัวเลือกเครื่องหมายประทับตรา
```csharp
StampSignOptions options = new StampSignOptions()
{
    Left = 50,
    Top = 150,                    
    Width = 200,
    Height = 200
};
```
## ขั้นตอนที่ 3: กำหนดค่าลักษณะที่ปรากฏของแสตมป์
```csharp
StampLine outerLine = new StampLine();
outerLine.Text = " * European Union ";
outerLine.TextRepeatType = StampTextRepeatType.FullTextRepeat;
outerLine.Font.Size = 12;
outerLine.Height = 22;
outerLine.TextBottomIntent = 6;
outerLine.TextColor = Color.WhiteSmoke;
outerLine.BackgroundColor = Color.DarkSlateBlue;
options.OuterLines.Add(outerLine);
StampLine innerLine = new StampLine();
innerLine.Text = "John Smith";
innerLine.TextColor = Color.MediumVioletRed;
innerLine.Font.Size = 20;
innerLine.Font.Bold = true;
innerLine.Height = 40;
options.InnerLines.Add(innerLine);
```
## ขั้นตอนที่ 4: ลงนามในเอกสาร
```csharp
string outputFilePath = Path.Combine("Your Document Directory", "SignWithStamp", fileName);
SignResult result = signature.Sign(outputFilePath, options);
Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).\nFile saved at {outputFilePath}.");
```

## บทสรุป
การเพิ่มลายเซ็นตราประทับให้กับเอกสารของคุณโดยใช้ GroupDocs.Signature สำหรับ .NET เป็นกระบวนการที่ไม่ซับซ้อน ดังที่แสดงในบทช่วยสอนนี้ ด้วยขั้นตอนที่ให้มา คุณสามารถเพิ่มความปลอดภัยและความถูกต้องของเอกสารของคุณได้อย่างง่ายดาย
## คำถามที่พบบ่อย
### ฉันสามารถปรับแต่งลักษณะที่ปรากฏของลายเซ็นแสตมป์ได้หรือไม่
ใช่ คุณสามารถปรับแต่งลักษณะต่างๆ เช่น ข้อความ แบบอักษร สี และตำแหน่งของลายเซ็นแสตมป์ได้ตามความต้องการของคุณ
### GroupDocs.Signature รองรับการเซ็นเอกสารหลายรูปแบบหรือไม่
ใช่ GroupDocs.Signature รองรับรูปแบบเอกสารที่หลากหลาย รวมถึง PDF, Microsoft Word, Excel, PowerPoint และอื่นๆ
### GroupDocs.Signature มีเวอร์ชันทดลองใช้งานหรือไม่
 ใช่ คุณสามารถเข้าถึงเวอร์ชันทดลองใช้ฟรีได้จาก[เว็บไซต์](https://releases.groupdocs.com/).
### ฉันสามารถเพิ่มลายเซ็นหลายรายการในเอกสารเดียวได้หรือไม่
GroupDocs.Signature ช่วยให้คุณสามารถเพิ่มลายเซ็นได้หลายแบบ รวมถึงตราประทับ ข้อความ รูปภาพ และลายเซ็นดิจิทัล ลงในเอกสารฉบับเดียว
### ฉันจะขอรับการสนับสนุนได้ที่ไหน หากฉันประสบปัญหาใดๆ ระหว่างการใช้งาน
 คุณสามารถค้นหาการสนับสนุนและความช่วยเหลือได้จากฟอรัมชุมชน GroupDocs.Signature[ที่นี่](https://forum.groupdocs.com/c/signature/13).