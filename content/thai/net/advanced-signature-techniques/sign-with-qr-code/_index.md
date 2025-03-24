---
title: การลงนามเอกสารด้วย QR Code โดยใช้ GroupDocs.Signature
linktitle: การลงนามด้วยรหัส QR
second_title: GroupDocs.Signature .NET API
description: เรียนรู้วิธีเพิ่มลายเซ็นโค้ด QR ลงในเอกสารของคุณด้วย GroupDocs.Signature สำหรับ .NET ปรับปรุงความปลอดภัยและการรับรองความถูกต้องได้อย่างง่ายดาย
weight: 15
url: /th/net/advanced-signature-techniques/sign-with-qr-code/
---
## การแนะนำ
ในบทช่วยสอนนี้ เราจะอธิบายขั้นตอนการลงนามเอกสารด้วยโค้ด QR โดยใช้ GroupDocs.Signature สำหรับ .NET GroupDocs.Signature สำหรับ .NET เป็น API ที่ทรงพลังซึ่งช่วยให้นักพัฒนาสามารถเพิ่มลายเซ็นประเภทต่างๆ ลงในเอกสารดิจิทัลโดยทางโปรแกรม การลงนามเอกสารด้วยรหัส QR ช่วยเพิ่มระดับความปลอดภัยและการตรวจสอบสิทธิ์ให้กับเอกสารของคุณ
## ข้อกำหนดเบื้องต้น
ก่อนที่เราจะเริ่มต้น ตรวจสอบให้แน่ใจว่าคุณได้ติดตั้งข้อกำหนดเบื้องต้นต่อไปนี้:
1.  GroupDocs.Signature สำหรับ .NET: คุณสามารถดาวน์โหลดไลบรารี่ได้จาก[เว็บไซต์](https://releases.groupdocs.com/signature/net/).
2. สภาพแวดล้อมการพัฒนา: ตรวจสอบให้แน่ใจว่าคุณได้ตั้งค่าสภาพแวดล้อมการพัฒนา .NET บนเครื่องของคุณ
3. เอกสารตัวอย่าง: เตรียมเอกสารตัวอย่าง (เช่น PDF) ที่คุณต้องการลงนามด้วยรหัส QR

## การนำเข้าเนมสเปซที่จำเป็น
ก่อนที่จะเจาะลึกโค้ด มานำเข้าเนมสเปซที่จำเป็นก่อน:
```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

## ขั้นตอนที่ 1: กำหนดเส้นทางไฟล์
```csharp
string filePath = "sample.pdf";
string fileName = Path.GetFileName(filePath);
string outputFilePath = Path.Combine("Your Document Directory", "SignWithQRCode", fileName);
```
 ให้แน่ใจว่าจะเปลี่ยน`"Your Document Directory"` พร้อมพาธไปยังไดเร็กทอรีที่คุณต้องการบันทึกเอกสารที่เซ็นชื่อ
## ขั้นตอนที่ 2: เริ่มต้นวัตถุลายเซ็น
```csharp
using (Signature signature = new Signature(filePath))
{
    //รหัสสำหรับการลงนามอยู่ที่นี่
}
```
 เริ่มต้นก`Signature` วัตถุที่มีเส้นทางไปยังเอกสารที่คุณต้องการลงนาม
## ขั้นตอนที่ 3: สร้าง QRCodeSignOptions
```csharp
QrCodeSignOptions options = new QrCodeSignOptions("JohnSmith")
{
    EncodeType = QrCodeTypes.QR,
    Left = 50,
    Top = 150,
    Width = 200,
    Height = 200
};
```
 สร้างก`QrCodeSignOptions` วัตถุด้วยการตั้งค่าที่ต้องการสำหรับลายเซ็นรหัส QR คุณสามารถปรับแต่งพารามิเตอร์ เช่น ข้อความที่จะเข้ารหัส ตำแหน่ง และขนาดของโค้ด QR ได้
## ขั้นตอนที่ 4: ลงนามในเอกสาร
```csharp
SignResult result = signature.Sign(outputFilePath, options);
```
 ใช้`Sign` วิธีการของ`Signature` วัตถุเพื่อลงนามในเอกสารด้วยตัวเลือกที่ระบุ วิธีการนี้จะคืนค่า a`SignResult` วัตถุที่มีข้อมูลเกี่ยวกับกระบวนการลงนาม
## ขั้นตอนที่ 5: แสดงผล
```csharp
Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).\nFile saved at {outputFilePath}.");
```
แสดงข้อความระบุความสำเร็จของกระบวนการลงนามและตำแหน่งที่บันทึกเอกสารที่ลงนาม

## บทสรุป
ในบทช่วยสอนนี้ เราได้เรียนรู้วิธีลงนามเอกสารด้วยโค้ด QR โดยใช้ GroupDocs.Signature สำหรับ .NET ด้วยการทำตามขั้นตอนง่ายๆ เหล่านี้ คุณจะสามารถเพิ่มลายเซ็นรหัส QR ลงในเอกสารดิจิทัลของคุณได้ ซึ่งช่วยเพิ่มความปลอดภัยและการรับรองความถูกต้อง

## คำถามที่พบบ่อย
### ฉันสามารถปรับแต่งลักษณะที่ปรากฏของโค้ด QR ได้หรือไม่
ได้ คุณสามารถปรับแต่งพารามิเตอร์ต่างๆ ได้ เช่น ขนาด ตำแหน่ง และประเภทการเข้ารหัสของโค้ด QR ตามความต้องการของคุณ
### เอกสารรูปแบบใดบ้างที่รองรับการลงนามด้วยรหัส QR
GroupDocs.Signature สำหรับ .NET รองรับรูปแบบเอกสารที่หลากหลาย รวมถึง PDF, Word, Excel, PowerPoint และอื่นๆ
### เป็นไปได้ไหมที่จะเซ็นเอกสารหลายฉบับในกระบวนการเป็นชุด?
แน่นอน คุณสามารถใช้ GroupDocs.Signature สำหรับ .NET เพื่อเซ็นเอกสารหลายฉบับพร้อมกันได้ ซึ่งจะทำให้ขั้นตอนการทำงานของคุณคล่องตัวขึ้น
### ฉันสามารถตรวจสอบความถูกต้องของเอกสารที่ลงนามด้วยรหัส QR ได้หรือไม่
ใช่ GroupDocs.Signature สำหรับ .NET มีกลไกการตรวจสอบเพื่อให้มั่นใจในความสมบูรณ์และความถูกต้องของเอกสารที่ลงนาม
### มีเวอร์ชันทดลองให้ทดสอบฟังก์ชันการทำงานก่อนซื้อหรือไม่
 ใช่ คุณสามารถดาวน์โหลดเวอร์ชันทดลองใช้ฟรีได้จาก[เว็บไซต์](https://releases.groupdocs.com/) เพื่อประเมินคุณสมบัติและความสามารถของ GroupDocs.Signature สำหรับ .NET