---
title: ลบลายเซ็นข้อความ
linktitle: ลบลายเซ็นข้อความ
second_title: GroupDocs.Signature .NET API
description: ลบลายเซ็นข้อความออกจากเอกสารได้อย่างง่ายดายโดยใช้ GroupDocs.Signature สำหรับ .NET ลดความซับซ้อนของงานการจัดการเอกสารของคุณ
weight: 17
url: /th/net/delete-operations/delete-text-signature/
---

# ลบลายเซ็นข้อความ

## การแนะนำ
GroupDocs.Signature สำหรับ .NET เป็นไลบรารีที่มีประสิทธิภาพซึ่งช่วยให้นักพัฒนาสามารถรวมฟังก์ชันลายเซ็นอิเล็กทรอนิกส์เข้ากับแอปพลิเคชัน .NET ของตนได้อย่างราบรื่น ไม่ว่าคุณกำลังสร้างระบบการจัดการเอกสาร แพลตฟอร์มการลงนามในสัญญา หรือแอปพลิเคชันอื่นๆ ที่ต้องใช้ฟังก์ชันลายเซ็น GroupDocs.Signature สำหรับ .NET ก็มีชุดเครื่องมือที่ครอบคลุมเพื่อทำให้กระบวนการง่ายขึ้น
## ข้อกำหนดเบื้องต้น
ก่อนที่จะเริ่มใช้ GroupDocs.Signature สำหรับ .NET ตรวจสอบให้แน่ใจว่าคุณมีข้อกำหนดเบื้องต้นต่อไปนี้:
### 1. สภาพแวดล้อมการพัฒนา .NET
ตรวจสอบให้แน่ใจว่าคุณได้ตั้งค่าสภาพแวดล้อมการพัฒนา .NET บนเครื่องของคุณ คุณสามารถดาวน์โหลดและติดตั้ง .NET SDK ได้จากเว็บไซต์ Microsoft
### 2. GroupDocs.Signature สำหรับ .NET
 ดาวน์โหลดและติดตั้ง GroupDocs.Signature สำหรับ .NET จากลิงก์ที่ให้มา:[ดาวน์โหลด GroupDocs.Signature สำหรับ .NET](https://releases.groupdocs.com/signature/net/)
### 3. เอกสารสำหรับการทดสอบ
เตรียมเอกสารตัวอย่าง (เช่น เอกสาร Word, PDF ฯลฯ) ที่คุณจะใช้ในการทดสอบฟังก์ชันการลบลายเซ็น

## นำเข้าเนมสเปซ
หากต้องการเริ่มใช้ GroupDocs.Signature สำหรับ .NET ในโปรเจ็กต์ของคุณ ให้นำเข้าเนมสเปซที่จำเป็น:
```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

ตอนนี้ เรามาแบ่งขั้นตอนการลบลายเซ็นข้อความออกจากเอกสารออกเป็นหลายขั้นตอน:
## ขั้นตอนที่ 1: กำหนดเส้นทางไฟล์
ขั้นแรก กำหนดเส้นทางสำหรับเอกสารอินพุต เอกสารเอาต์พุต และชื่อไฟล์
```csharp
string filePath = "sample_multiple_signatures.docx";
string fileName = Path.GetFileName(filePath);
string outputFilePath = Path.Combine("Your Document Directory", "DeleteText", fileName);
```
## ขั้นตอนที่ 2: คัดลอกไฟล์ต้นฉบับ
 ตั้งแต่วันที่`Delete` วิธีการทำงานกับเอกสารเดียวกัน ให้คัดลอกไฟล์ต้นฉบับไปยังตำแหน่งใหม่
```csharp
File.Copy(filePath, outputFilePath, true);
```
## ขั้นตอนที่ 3: เริ่มต้นวัตถุลายเซ็น
 เริ่มต้นก`Signature` วัตถุโดยใช้เส้นทางไฟล์เอาต์พุต
```csharp
using (Signature signature = new Signature(outputFilePath))
{
    // รหัสสำหรับการลบลายเซ็นข้อความจะอยู่ที่นี่
}
```
## ขั้นตอนที่ 4: ค้นหาลายเซ็นข้อความ
 ค้นหาลายเซ็นข้อความภายในเอกสารโดยใช้`TextSearchOptions`.
```csharp
TextSearchOptions options = new TextSearchOptions();
List<TextSignature> signatures = signature.Search<TextSignature>(options);
```
## ขั้นตอนที่ 5: ลบลายเซ็นข้อความ
หากพบลายเซ็นข้อความ ให้ลบอันแรกออก
```csharp
if (signatures.Count > 0)
{
    TextSignature textSignature = signatures[0];
    bool result = signature.Delete(textSignature);
    if (result)
    {
        Console.WriteLine($"Signature with Text '{textSignature.Text}' was deleted from document ['{fileName}'].");
    }
    else
    {
        Helper.WriteError($"Signature was not deleted from the document! Signature with Text '{textSignature.Text}' was not found!");
    }
}
```

## บทสรุป
โดยสรุป GroupDocs.Signature สำหรับ .NET นำเสนอวิธีการที่ตรงไปตรงมาในการลบลายเซ็นข้อความออกจากเอกสารโดยทางโปรแกรม ด้วยการทำตามขั้นตอนที่ระบุไว้ในบทช่วยสอนนี้ นักพัฒนาสามารถรวมฟังก์ชันการลบลายเซ็นเข้ากับแอปพลิเคชัน .NET ของตนได้อย่างราบรื่น ปรับปรุงกระบวนการจัดการเอกสาร และรับรองการปฏิบัติตามมาตรฐานลายเซ็นอิเล็กทรอนิกส์
## คำถามที่พบบ่อย
### GroupDocs.Signature สำหรับ .NET สามารถจัดการลายเซ็นหลายรายการภายในเอกสารเดียวได้หรือไม่
ใช่ GroupDocs.Signature สำหรับ .NET รองรับการตรวจจับและการลบลายเซ็นหลายรายการภายในเอกสาร
### มีรุ่นทดลองใช้สำหรับการทดสอบหรือไม่?
 ใช่ คุณสามารถเข้าถึงเวอร์ชันทดลองได้จากลิงก์ที่ให้มา:[ทดลองฟรี](https://releases.groupdocs.com/)
### GroupDocs.Signature สำหรับ .NET รองรับรูปแบบเอกสารที่แตกต่างกันหรือไม่
ใช่ GroupDocs.Signature สำหรับ .NET รองรับรูปแบบเอกสารที่หลากหลาย รวมถึง Word, PDF, Excel และอื่นๆ
### ฉันสามารถปรับแต่งตัวเลือกการค้นหาเมื่อค้นหาลายเซ็นได้หรือไม่
แน่นอนว่า GroupDocs.Signature สำหรับ .NET มีตัวเลือกการค้นหาที่หลากหลาย ช่วยให้นักพัฒนาสามารถปรับแต่งเกณฑ์การค้นหาตามความต้องการของพวกเขาได้
### ฉันจะขอความช่วยเหลือได้ที่ไหนหากฉันประสบปัญหาระหว่างการใช้งาน
 คุณสามารถขอการสนับสนุนจากฟอรัมชุมชน GroupDocs:[ฟอรั่มการสนับสนุน](https://forum.groupdocs.com/c/signature/13)