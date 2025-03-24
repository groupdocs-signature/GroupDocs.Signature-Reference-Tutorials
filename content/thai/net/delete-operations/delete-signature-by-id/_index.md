---
title: ลบลายเซ็นด้วย ID
linktitle: ลบลายเซ็นด้วย ID
second_title: GroupDocs.Signature .NET API
description: เรียนรู้วิธีลบลายเซ็นด้วย ID ในเอกสาร .NET โดยใช้ไลบรารี GroupDocs.Signature คำแนะนำทีละขั้นตอนง่าย ๆ
weight: 11
url: /th/net/delete-operations/delete-signature-by-id/
---
## การแนะนำ
ในบทช่วยสอนนี้ เราจะสำรวจวิธีลบลายเซ็นด้วย ID โดยใช้ GroupDocs.Signature สำหรับ .NET GroupDocs.Signature สำหรับ .NET เป็นไลบรารีที่มีประสิทธิภาพซึ่งช่วยให้นักพัฒนาสามารถเพิ่ม ลบ หรือตรวจสอบลายเซ็นดิจิทัลในรูปแบบเอกสารต่างๆ โดยใช้แอปพลิเคชัน .NET
## ข้อกำหนดเบื้องต้น
ก่อนที่เราจะเริ่มต้น ตรวจสอบให้แน่ใจว่าคุณมีข้อกำหนดเบื้องต้นดังต่อไปนี้:
1.  GroupDocs.Signature สำหรับ .NET Library: ดาวน์โหลดและติดตั้งไลบรารีจาก[ที่นี่](https://releases.groupdocs.com/signature/net/).
2. .NET Framework: ตรวจสอบให้แน่ใจว่าคุณได้ติดตั้ง .NET Framework บนระบบของคุณ
3. เอกสารที่มีลายเซ็น: เตรียมเอกสาร (เช่น DOCX, PDF) พร้อมลายเซ็นที่คุณต้องการลบ

## นำเข้าเนมสเปซ
```csharp
using System;
using System.IO;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## ขั้นตอนที่ 1: กำหนดเส้นทางไฟล์
ขั้นแรก ระบุเส้นทางไฟล์สำหรับเอกสารที่มีลายเซ็น และเส้นทางไฟล์เอาต์พุตที่จะบันทึกเอกสารที่แก้ไข
```csharp
string filePath = "sample_multiple_signatures.docx";
string fileName = Path.GetFileName(filePath);
string outputFilePath = Path.Combine("Your Document Directory", "DeleteById", fileName);
```
## ขั้นตอนที่ 2: คัดลอกเอกสาร
 ตั้งแต่วันที่`Delete` วิธีการแก้ไขเอกสารที่มีอยู่ วิธีที่ดีที่สุดคือสร้างสำเนาของเอกสารต้นฉบับ
```csharp
File.Copy(filePath, outputFilePath, true);
```
## ขั้นตอนที่ 3: ลบลายเซ็นด้วย ID
 เริ่มต้น`Signature` object ด้วยเส้นทางไฟล์เอกสารและใช้`Delete` วิธีการลบลายเซ็นด้วย ID
```csharp
using (Signature signature = new Signature(outputFilePath))
{
    string id = @"eff64a14-dad9-47b0-88e5-2ee4e3604e71";
    bool result = signature.Delete(id);
    if (result)
    {
        Console.WriteLine($"Signature with Id# '{id}' was deleted from document ['{fileName}'].");
    }
    else
    {
        Helper.WriteError($"Signature was not deleted from the document! Signature with id# '{id}' was not found!");
    }
}
```

## บทสรุป
ในบทช่วยสอนนี้ เราได้เรียนรู้วิธีลบลายเซ็นด้วย ID โดยใช้ GroupDocs.Signature สำหรับ .NET ไลบรารีนี้มอบวิธีที่สะดวกในการจัดการลายเซ็นดิจิทัลในรูปแบบเอกสารต่างๆ โดยทางโปรแกรม
## คำถามที่พบบ่อย
### ฉันสามารถลบลายเซ็นหลายรายการพร้อมกันได้หรือไม่
 ใช่ คุณสามารถลบลายเซ็นหลายรายการได้ด้วยการวนซ้ำ ID ของลายเซ็นเหล่านั้นแล้วเรียก`Delete` วิธีการสำหรับแต่ละ ID
### GroupDocs.Signature สำหรับ .NET เข้ากันได้กับเอกสารทุกรูปแบบหรือไม่
GroupDocs.Signature สำหรับ .NET รองรับรูปแบบเอกสารที่หลากหลาย รวมถึง PDF, DOCX, XLSX และอื่นๆ
### ฉันสามารถปรับแต่งลักษณะที่ปรากฏของลายเซ็นได้หรือไม่
ใช่ คุณสามารถปรับแต่งลักษณะที่ปรากฏของลายเซ็น รวมถึงตำแหน่ง ขนาด แบบอักษร และสีได้
### มีรุ่นทดลองใช้งานหรือไม่?
 ใช่ คุณสามารถดาวน์โหลดเวอร์ชันทดลองใช้ฟรีได้จาก[ที่นี่](https://releases.groupdocs.com/).
### ฉันจะขอความช่วยเหลือหรือสนับสนุน GroupDocs.Signature สำหรับ .NET ได้ที่ไหน
 คุณสามารถเยี่ยมชมฟอรั่มการสนับสนุน[ที่นี่](https://forum.groupdocs.com/c/signature/13) สำหรับความช่วยเหลือ.