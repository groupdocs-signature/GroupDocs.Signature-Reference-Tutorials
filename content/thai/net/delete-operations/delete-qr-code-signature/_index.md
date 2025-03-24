---
title: ลบลายเซ็น QR Code จากเอกสาร
linktitle: ลบลายเซ็น QR Code จากเอกสาร
second_title: GroupDocs.Signature .NET API
description: เรียนรู้วิธีลบลายเซ็นโค้ด QR ออกจากเอกสารโดยใช้ GroupDocs.Signature สำหรับ .NET ปฏิบัติตามคำแนะนำทีละขั้นตอนของเราเพื่อการจัดการลายเซ็นที่มีประสิทธิภาพ
weight: 16
url: /th/net/delete-operations/delete-qr-code-signature/
---
## การแนะนำ
ในบทช่วยสอนนี้ เราจะแนะนำคุณตลอดขั้นตอนการลบลายเซ็นโค้ด QR ออกจากเอกสารโดยใช้ GroupDocs.Signature สำหรับ .NET ทำตามคำแนะนำทีละขั้นตอนเหล่านี้เพื่อลบลายเซ็นโค้ด QR ได้อย่างมีประสิทธิภาพ
## ข้อกำหนดเบื้องต้น
ก่อนที่คุณจะเริ่มต้น ตรวจสอบให้แน่ใจว่าคุณมีข้อกำหนดเบื้องต้นต่อไปนี้:
-  GroupDocs.Signature สำหรับ .NET: ตรวจสอบให้แน่ใจว่าคุณได้ติดตั้งไลบรารี GroupDocs.Signature ในโครงการ .NET ของคุณ คุณสามารถดาวน์โหลดได้จาก[ที่นี่](https://releases.groupdocs.com/signature/net/).
- เอกสารที่มีลายเซ็น QR Code: เตรียมเอกสารที่มีลายเซ็น QR Code ที่คุณต้องการลบ
- ความรู้พื้นฐานของ C#: ทำความคุ้นเคยกับพื้นฐานภาษาการเขียนโปรแกรม C#

## การนำเข้าเนมสเปซ
ก่อนที่จะเจาะลึกโค้ด ให้นำเข้าเนมสเปซที่จำเป็นไปยังไฟล์ C# ของคุณ:
```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## ขั้นตอนที่ 1: กำหนดเส้นทางไฟล์
```csharp
// เส้นทางไปยังไดเร็กทอรีเอกสาร
string filePath = "sample_multiple_signatures.docx";
string fileName = Path.GetFileName(filePath);
// กำหนดเส้นทางไฟล์เอาต์พุตสำหรับเอกสารที่แก้ไข
string outputFilePath = Path.Combine("Your Document Directory", "DeleteQRCode", fileName);
// คัดลอกไฟล์ต้นฉบับเนื่องจากวิธีการลบใช้งานได้กับเอกสารเดียวกัน
File.Copy(filePath, outputFilePath, true);
```
## ขั้นตอนที่ 2: เริ่มต้นวัตถุลายเซ็น
```csharp
using (Signature signature = new Signature(outputFilePath))
{
    // สร้างตัวเลือกสำหรับการค้นหาลายเซ็นรหัส QR
    QrCodeSearchOptions options = new QrCodeSearchOptions();
    // ค้นหาลายเซ็นรหัส QR ในเอกสาร
    List<QrCodeSignature> signatures = signature.Search<QrCodeSignature>(options);
```
## ขั้นตอนที่ 3: ตรวจสอบการมีอยู่ของลายเซ็น QR Code
```csharp
    if (signatures.Count > 0)
    {
        // รับลายเซ็นรหัส QR แรกที่พบในเอกสาร
        QrCodeSignature qrCodeSignature = signatures[0];
```
## ขั้นตอนที่ 4: ลบลายเซ็น QR Code
```csharp
        // ลบลายเซ็นรหัส QR ออกจากเอกสาร
        bool result = signature.Delete(qrCodeSignature);
        if (result)
        {
            Console.WriteLine($"Signature with QR-Code '{qrCodeSignature.Text}' and encode type '{qrCodeSignature.EncodeType.TypeName}' was deleted from document ['{fileName}'].");
        }
        else
        {
            Helper.WriteError($"Signature was not deleted from the document! Signature with Barcode '{qrCodeSignature.Text}' and encode type '{qrCodeSignature.EncodeType.TypeName}' was not found!");
        }
    }
}
```
ยินดีด้วย! คุณได้ลบลายเซ็นโค้ด QR ออกจากเอกสารเรียบร้อยแล้วโดยใช้ GroupDocs.Signature สำหรับ .NET

## บทสรุป
ในบทช่วยสอนนี้ เราได้เรียนรู้วิธีลบลายเซ็นโค้ด QR ออกจากเอกสารโดยใช้ GroupDocs.Signature สำหรับ .NET ด้วยการทำตามขั้นตอนที่ให้ไว้ คุณสามารถจัดการและจัดการลายเซ็นภายในแอปพลิเคชัน .NET ของคุณได้อย่างมีประสิทธิภาพ
## คำถามที่พบบ่อย
### ฉันสามารถลบลายเซ็น QR Code หลายลายเซ็นออกจากเอกสารได้หรือไม่
ได้ คุณสามารถแก้ไขโค้ดเพื่อวนซ้ำลายเซ็นโค้ด QR ทั้งหมดและลบออกตามลำดับ
### GroupDocs.Signature รองรับลายเซ็นประเภทอื่นนอกเหนือจากรหัส QR หรือไม่
ใช่ GroupDocs.Signature รองรับลายเซ็นหลายประเภท เช่น ข้อความ รูปภาพ บาร์โค้ด และอื่นๆ
### GroupDocs.Signature เข้ากันได้กับเอกสารทุกรูปแบบหรือไม่
GroupDocs.Signature รองรับรูปแบบเอกสารที่หลากหลาย รวมถึง PDF, Microsoft Word, Excel, PowerPoint และอื่นๆ
### ฉันสามารถปรับแต่งตัวเลือกการค้นหาสำหรับลายเซ็นได้หรือไม่
ได้ คุณสามารถปรับแต่งตัวเลือกการค้นหาตามความต้องการของคุณเพื่อค้นหาลายเซ็นเฉพาะภายในเอกสารได้
### GroupDocs.Signature มีเวอร์ชันทดลองใช้งานหรือไม่
 ใช่ คุณสามารถเข้าถึง GroupDocs.Signature เวอร์ชันทดลองใช้ฟรีได้จาก[ที่นี่](https://releases.groupdocs.com/).