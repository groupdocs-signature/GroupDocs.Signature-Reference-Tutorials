---
title: ลบลายเซ็นรูปภาพ
linktitle: ลบลายเซ็นรูปภาพ
second_title: GroupDocs.Signature .NET API
description: เรียนรู้วิธีลบลายเซ็นรูปภาพออกจากเอกสารโดยใช้ GroupDocs.Signature สำหรับ .NET ปฏิบัติตามคำแนะนำทีละขั้นตอนของเราเพื่อการจัดการลายเซ็นที่มีประสิทธิภาพ
weight: 14
url: /th/net/delete-operations/delete-image-signature/
---

# ลบลายเซ็นรูปภาพ

## การแนะนำ
ในบทช่วยสอนนี้ เราจะสำรวจวิธีลบลายเซ็นรูปภาพออกจากเอกสารโดยใช้ GroupDocs.Signature สำหรับ .NET GroupDocs.Signature เป็นไลบรารีอันทรงพลังที่ช่วยให้นักพัฒนาสามารถทำงานกับลายเซ็นดิจิทัล ตราประทับ และฟิลด์แบบฟอร์มภายในรูปแบบเอกสารที่หลากหลาย
## ข้อกำหนดเบื้องต้น
ก่อนที่เราจะเริ่ม ตรวจสอบให้แน่ใจว่าคุณมีสิ่งต่อไปนี้:
### 1. GroupDocs.Signature สำหรับ .NET
 ดาวน์โหลดและติดตั้ง GroupDocs.Signature สำหรับ .NET จาก[เว็บไซต์](https://releases.groupdocs.com/signature/net/)- ปฏิบัติตามคำแนะนำในการติดตั้งที่ให้ไว้ในเอกสารประกอบ
### 2. .NET Framework
ตรวจสอบให้แน่ใจว่าคุณได้ติดตั้ง .NET Framework บนเครื่องของคุณแล้ว
## นำเข้าเนมสเปซ
รวมเนมสเปซที่จำเป็นในโครงการของคุณ:
```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
แบ่งขั้นตอนการลบลายเซ็นรูปภาพออกเป็นหลายขั้นตอน:
## ขั้นตอนที่ 1: กำหนดเส้นทางไฟล์
ขั้นแรก ให้ระบุเส้นทางสำหรับเอกสารอินพุตและเอกสารเอาต์พุตหลังจากลบลายเซ็น:
```csharp
string filePath = "sample_multiple_signatures.docx";
string fileName = Path.GetFileName(filePath);
string outputFilePath = Path.Combine("Your Document Directory", "DeleteImage", fileName);
```
## ขั้นตอนที่ 2: คัดลอกไฟล์ต้นฉบับ
 ตั้งแต่วันที่`Delete`วิธีการนี้ใช้ได้กับเอกสารเดียวกัน จำเป็นต้องคัดลอกไฟล์ต้นฉบับไปยังตำแหน่งอื่น:
```csharp
File.Copy(filePath, outputFilePath, true);
```
## ขั้นตอนที่ 3: เริ่มต้นวัตถุลายเซ็น
 สร้างอินสแตนซ์ของ`Signature` คลาสและระบุเส้นทางไปยังเอกสารเอาต์พุต:
```csharp
using (Signature signature = new Signature(outputFilePath))
{
    // รหัสไปที่นี่
}
```
## ขั้นตอนที่ 4: ค้นหาลายเซ็นรูปภาพ
กำหนดตัวเลือกการค้นหาและค้นหาลายเซ็นรูปภาพภายในเอกสาร:
```csharp
ImageSearchOptions options = new ImageSearchOptions();
List<ImageSignature> signatures = signature.Search<ImageSignature>(options);
```
## ขั้นตอนที่ 5: ลบลายเซ็นรูปภาพ
หากพบลายเซ็นรูปภาพ ให้ลบอันแรก:
```csharp
if (signatures.Count > 0)
{
    ImageSignature imageSignature = signatures[0];
    bool result = signature.Delete(imageSignature);
    if (result)
    {
        Console.WriteLine($"Image signature at location {imageSignature.Left}x{imageSignature.Top} and Size {imageSignature.Size} was deleted from document ['{fileName}'].");
    }
    else
    {
        Helper.WriteError($"Signature was not deleted from the document! Signature at location {imageSignature.Left}x{imageSignature.Top} and Size {imageSignature.Size} was not found!");
    }
}
```
## บทสรุป
ในบทช่วยสอนนี้ เราได้เรียนรู้วิธีลบลายเซ็นรูปภาพออกจากเอกสารโดยใช้ GroupDocs.Signature สำหรับ .NET ด้วยการทำตามคำแนะนำทีละขั้นตอน นักพัฒนาสามารถจัดการลายเซ็นดิจิทัลภายในแอปพลิเคชันของตนได้อย่างมีประสิทธิภาพ
## คำถามที่พบบ่อย
### ฉันสามารถลบลายเซ็นรูปภาพหลายรูปออกจากเอกสารได้หรือไม่
 ได้ คุณสามารถแก้ไขโค้ดเพื่อลบลายเซ็นรูปภาพหลายรูปได้โดยการวนซ้ำ`signatures` รายการ.
### GroupDocs.Signature รองรับรูปแบบเอกสารอื่นนอกเหนือจาก DOCX หรือไม่
ใช่ GroupDocs.Signature รองรับรูปแบบเอกสารที่หลากหลาย รวมถึง PDF, PPT, XLS และอื่นๆ
### มีรุ่นทดลองใช้สำหรับ GroupDocs.Signature สำหรับ .NET หรือไม่
 ใช่ คุณสามารถดาวน์โหลดเวอร์ชันทดลองใช้ฟรีได้จาก[เว็บไซต์](https://releases.groupdocs.com/).
### ฉันจะรับการสนับสนุนสำหรับ GroupDocs.Signature ได้อย่างไร
 ท่านสามารถเยี่ยมชมได้ที่[ฟอรัม GroupDocs.Signature](https://forum.groupdocs.com/c/signature/13) เพื่อขอความช่วยเหลือและสนับสนุน
### ฉันสามารถซื้อใบอนุญาตชั่วคราวสำหรับ GroupDocs.Signature ได้หรือไม่
 ใช่ คุณสามารถซื้อใบอนุญาตชั่วคราวได้จาก[หน้าซื้อ](https://purchase.groupdocs.com/temporary-license/).