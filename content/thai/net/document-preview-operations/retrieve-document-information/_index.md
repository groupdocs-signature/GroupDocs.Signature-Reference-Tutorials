---
title: ดึงข้อมูลเอกสาร
linktitle: ดึงข้อมูลเอกสาร
second_title: GroupDocs.Signature .NET API
description: ปรับปรุงการจัดการเอกสารใน .NET ด้วย GroupDocs.Signature ดึงข้อมูลเอกสารทีละขั้นตอน รองรับรูปแบบต่างๆ
weight: 11
url: /th/net/document-preview-operations/retrieve-document-information/
---
## การแนะนำ
ในขอบเขตของเอกสารดิจิทัล การรับรองความถูกต้องและความสมบูรณ์เป็นสิ่งสำคัญยิ่ง GroupDocs.Signature สำหรับ .NET มอบโซลูชันที่มีประสิทธิภาพสำหรับการจัดการลายเซ็นเอกสารภายในสภาพแวดล้อม .NET ในบทช่วยสอนนี้ เราจะเจาะลึกกระบวนการเรียกข้อมูลเอกสารโดยใช้ GroupDocs.Signature สำหรับ .NET โดยแจกแจงแต่ละขั้นตอนเพื่อความเข้าใจที่ครอบคลุม
## ข้อกำหนดเบื้องต้น
ก่อนที่จะเข้าสู่บทช่วยสอน ตรวจสอบให้แน่ใจว่าคุณมีข้อกำหนดเบื้องต้นต่อไปนี้:
1.  การติดตั้ง: ติดตั้ง GroupDocs.Signature สำหรับ .NET โดยดาวน์โหลดจาก[ที่นี่](https://releases.groupdocs.com/signature/net/).
2. .NET Environment: มีความรู้ในการทำงานของ .NET Framework
3. เอกสาร: เตรียมเอกสารตัวอย่าง (เช่น "sample_multiple_signatures.docx") เพื่อการทดสอบ

## การนำเข้าเนมสเปซ
ก่อนดำเนินการกระบวนการดึงลายเซ็นเอกสาร ให้นำเข้าเนมสเปซที่จำเป็น:
```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
```

## ขั้นตอนที่ 1: ตั้งค่าเส้นทางไฟล์เอกสาร:
กำหนดเส้นทางของไฟล์สำหรับเอกสารที่คุณต้องการดึงข้อมูล
```csharp
string filePath = "sample_multiple_signatures.docx";
```
## ขั้นตอนที่ 2: สร้างอินสแตนซ์ของวัตถุลายเซ็น:
 สร้างอินสแตนซ์ของ`Signature` คลาสโดยผ่านเส้นทางไฟล์เอกสาร
```csharp
using (Signature signature = new Signature(filePath))
{

}
```
## ขั้นตอนที่ 3: ดึงข้อมูลเอกสาร:
 ใช้`GetDocumentInfo()` วิธีการดึงข้อมูลที่ครอบคลุมเกี่ยวกับเอกสาร
```csharp
IDocumentInfo documentInfo = signature.GetDocumentInfo();
```
## ขั้นตอนที่ 4: แสดงคุณสมบัติเอกสาร:
แสดงคุณสมบัติต่างๆ ของเอกสาร เช่น รูปแบบ นามสกุล ขนาด จำนวนหน้า เป็นต้น
```csharp
Console.WriteLine($"Document properties {Path.GetFileName(filePath)}:");
Console.WriteLine($" - format : {documentInfo.FileType.FileFormat}");
Console.WriteLine($" - extension : {documentInfo.FileType.Extension}");
Console.WriteLine($" - size : {documentInfo.Size}");
Console.WriteLine($" - page count : {documentInfo.PageCount}");
Console.WriteLine($" - Form Fields count : {documentInfo.FormFields.Count}");
Console.WriteLine($" - Text signatures count : {documentInfo.TextSignatures.Count}");
Console.WriteLine($" - Image signatures count : {documentInfo.ImageSignatures.Count}");
Console.WriteLine($" - Digital signatures count : {documentInfo.DigitalSignatures.Count}");
Console.WriteLine($" - Barcode signatures count : {documentInfo.BarcodeSignatures.Count}");
Console.WriteLine($" - QrCode signatures count : {documentInfo.QrCodeSignatures.Count}");
Console.WriteLine($" - FormField signatures count : {documentInfo.FormFieldSignatures.Count}");
foreach (PageInfo pageInfo in documentInfo.Pages)
{
   Console.WriteLine($" - page-{pageInfo.PageNumber} Width {pageInfo.Width}, Height {pageInfo.Height}");
}
```


## บทสรุป
GroupDocs.Signature สำหรับ .NET นำเสนอชุดเครื่องมืออันทรงพลังสำหรับการจัดการลายเซ็นเอกสารภายในกรอบงาน .NET ได้อย่างราบรื่น เมื่อทำตามขั้นตอนที่ระบุไว้ในคู่มือนี้ คุณจะสามารถเรียกข้อมูลที่ครอบคลุมเกี่ยวกับเอกสารของคุณได้อย่างมีประสิทธิภาพ ซึ่งช่วยอำนวยความสะดวกในการจัดการเอกสารที่ได้รับการปรับปรุง

## คำถามที่พบบ่อย
### GroupDocs.Signature สำหรับ .NET สามารถจัดการเอกสารหลายรูปแบบได้หรือไม่
ใช่ GroupDocs.Signature รองรับรูปแบบเอกสารที่หลากหลาย รวมถึงแต่ไม่จำกัดเพียง DOCX, PDF, PNG และ JPEG
### มีรุ่นทดลองใช้สำหรับ GroupDocs.Signature สำหรับ .NET หรือไม่
 ใช่ คุณสามารถเข้าถึงเวอร์ชันทดลองได้จาก[ที่นี่](https://releases.groupdocs.com/).
### GroupDocs.Signature สำหรับ .NET ให้การสนับสนุนลายเซ็นดิจิทัลหรือไม่
GroupDocs.Signature ให้การสนับสนุนลายเซ็นดิจิทัลอย่างมีประสิทธิภาพ ช่วยให้มั่นใจในความถูกต้องและความสมบูรณ์ของเอกสาร
### ฉันจะหาเอกสารและการสนับสนุนเพิ่มเติมสำหรับ GroupDocs.Signature สำหรับ .NET ได้ที่ไหน
 คุณสามารถดูเอกสารประกอบที่ครอบคลุมได้[ที่นี่](https://tutorials.groupdocs.com/signature/net/) และหากต้องการการสนับสนุน โปรดไปที่ฟอรัม GroupDocs[ที่นี่](https://forum.groupdocs.com/c/signature/13).
### สามารถรับใบอนุญาตชั่วคราวสำหรับ GroupDocs.Signature สำหรับ .NET ได้หรือไม่
 ใช่ ใบอนุญาตชั่วคราวพร้อมสำหรับการซื้อ[ที่นี่](https://purchase.groupdocs.com/temporary-license/).