---
title: ยืนยันรหัส QR
linktitle: ยืนยันรหัส QR
second_title: GroupDocs.Signature .NET API
description: เรียนรู้วิธีตรวจสอบรหัส QR ภายในเอกสารโดยใช้ GroupDocs.Signature สำหรับ .NET บทช่วยสอนที่ครอบคลุมพร้อมคำแนะนำทีละขั้นตอน
type: docs
weight: 12
url: /th/net/verify-operations/verify-qr-code/
---
## การแนะนำ
ในขอบเขตของการจัดการเอกสารและการรับรองความถูกต้อง การรับรองความสมบูรณ์และความถูกต้องของลายเซ็นเป็นสิ่งสำคัญยิ่ง GroupDocs.Signature สำหรับ .NET มอบโซลูชันที่ครอบคลุมสำหรับการตรวจสอบรหัส QR ที่ฝังอยู่ภายในเอกสาร ในบทช่วยสอนนี้ เราจะเจาะลึกกระบวนการทีละขั้นตอนในการตรวจสอบรหัส QR โดยใช้ GroupDocs.Signature สำหรับ .NET
## ข้อกำหนดเบื้องต้น
ก่อนที่จะเข้าสู่กระบวนการตรวจสอบ ตรวจสอบให้แน่ใจว่าคุณมีข้อกำหนดเบื้องต้นต่อไปนี้:
1.  การติดตั้ง GroupDocs.Signature สำหรับ .NET: ดาวน์โหลดและติดตั้ง GroupDocs.Signature สำหรับ .NET จาก[ลิ้งค์ดาวน์โหลด](https://releases.groupdocs.com/signature/net/).
2. การเข้าถึงเอกสารที่มีรหัส QR: เตรียมเอกสารตัวอย่างที่มีรหัส QR เพื่อการตรวจสอบ 

## นำเข้าเนมสเปซ
ประการแรก คุณต้องนำเข้าเนมสเปซที่จำเป็นเพื่อใช้ฟังก์ชันการทำงานที่ GroupDocs.Signature สำหรับ .NET มอบให้ ทำตามขั้นตอนเหล่านี้:

```csharp
using System;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```


ตอนนี้ เรามาแจกแจงขั้นตอนการตรวจสอบรหัส QR ที่ฝังอยู่ภายในเอกสารโดยใช้ GroupDocs.Signature สำหรับ .NET:
## ขั้นตอนที่ 1: ระบุเส้นทางเอกสาร
```csharp
string filePath = "sample_multiple_signatures.docx";
```
 ให้แน่ใจว่าจะเปลี่ยน`"sample_multiple_signatures.docx"` พร้อมเส้นทางไปยังเอกสารของคุณ
## ขั้นตอนที่ 2: เริ่มต้นวัตถุลายเซ็น
```csharp
using (Signature signature = new Signature(filePath))
{
    //รหัสยืนยันอยู่ที่นี่
}
```
 เริ่มต้นก`Signature` วัตถุโดยระบุเส้นทางไปยังเอกสาร
## ขั้นตอนที่ 3: ระบุตัวเลือกการยืนยัน
```csharp
QrCodeVerifyOptions options = new QrCodeVerifyOptions()
{
    AllPages = true, // ค่านี้ถูกกำหนดไว้ตามค่าเริ่มต้น
    Text = "John",
    MatchType = TextMatchType.Contains
};
```
 กำหนดตัวเลือกการยืนยัน เช่น`AllPages` เพื่อตรวจสอบทุกหน้า`Text` เพื่อระบุข้อความที่จะจับคู่ภายในรหัส QR และ`MatchType` เพื่อกำหนดเกณฑ์การจับคู่
## ขั้นตอนที่ 4: ตรวจสอบลายเซ็นเอกสาร
```csharp
VerificationResult result = signature.Verify(options);
```
 เรียกใช้`Verify` วิธีการของ`Signature` วัตถุผ่านตัวเลือกการตรวจสอบ
## ขั้นตอนที่ 5: จัดการผลการตรวจสอบ
```csharp
if (result.IsValid)
{
    // พบลายเซ็นที่ถูกต้อง
}
else
{
    // พบลายเซ็นที่ไม่ถูกต้อง
}
```
ขึ้นอยู่กับผลการตรวจสอบ ให้จัดการกับสถานการณ์ความสำเร็จหรือความล้มเหลวตามลำดับ

## บทสรุป
ในบทช่วยสอนนี้ เราได้สำรวจกระบวนการตรวจสอบรหัส QR ภายในเอกสารโดยใช้ GroupDocs.Signature สำหรับ .NET ด้วยการทำตามขั้นตอนเหล่านี้ คุณจะสามารถรวมฟังก์ชันการตรวจสอบโค้ด QR เข้ากับแอปพลิเคชัน .NET ของคุณได้อย่างราบรื่น ช่วยให้มั่นใจในความสมบูรณ์และความถูกต้องของเอกสาร
## คำถามที่พบบ่อย
### GroupDocs.Signature สำหรับ .NET สามารถตรวจสอบรหัส QR ในรูปแบบเอกสารต่างๆ ได้หรือไม่
ใช่ GroupDocs.Signature สำหรับ .NET รองรับรูปแบบเอกสารที่หลากหลาย รวมถึง DOCX, PDF และอื่นๆ สำหรับการตรวจสอบรหัส QR
### GroupDocs.Signature สำหรับ .NET มีรุ่นทดลองใช้ฟรีหรือไม่
 ใช่ คุณสามารถทดลองใช้ฟรีได้จาก[หน้าเผยแพร่](https://releases.groupdocs.com/).
### ตัวเลือกการสนับสนุนใดบ้างสำหรับ GroupDocs.Signature สำหรับผู้ใช้ .NET
 ผู้ใช้สามารถเข้าถึงการสนับสนุนผ่านทาง[ฟอรั่ม](https://forum.groupdocs.com/c/signature/13) สำหรับ GroupDocs.Signature
### ฉันสามารถซื้อใบอนุญาตชั่วคราวสำหรับ GroupDocs.Signature สำหรับ .NET ได้หรือไม่
 ใช่ ใบอนุญาตชั่วคราวสามารถซื้อได้จาก[หน้าการซื้อ GroupDocs](https://purchase.groupdocs.com/temporary-license/).
### มีเอกสารประกอบมากมายสำหรับ GroupDocs.Signature สำหรับ .NET หรือไม่
 แน่นอนคุณสามารถดูเอกสารรายละเอียดที่ให้ไว้ได้[ที่นี่](https://reference.groupdocs.com/signature/net/) สำหรับคำแนะนำที่ครอบคลุมเกี่ยวกับการใช้ฟังก์ชันของ GroupDocs.Signature สำหรับ .NET