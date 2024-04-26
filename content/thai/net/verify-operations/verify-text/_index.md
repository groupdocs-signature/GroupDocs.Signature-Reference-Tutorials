---
title: ยืนยันข้อความ
linktitle: ยืนยันข้อความ
second_title: GroupDocs.Signature .NET API
description: เรียนรู้วิธีตรวจสอบข้อความในเอกสารโดยใช้ GroupDocs.Signature สำหรับ .NET ปฏิบัติตามบทช่วยสอนทีละขั้นตอนของเราเพื่อการบูรณาการที่ราบรื่น
type: docs
weight: 13
url: /th/net/verify-operations/verify-text/
---
## การแนะนำ
ในบทช่วยสอนนี้ เราจะแนะนำคุณตลอดขั้นตอนการตรวจสอบข้อความในเอกสารโดยใช้ GroupDocs.Signature สำหรับ .NET ไลบรารีอันทรงพลังนี้ช่วยให้คุณสามารถรวมฟังก์ชันการตรวจสอบข้อความเข้ากับแอปพลิเคชัน .NET ของคุณได้อย่างราบรื่น ช่วยให้มั่นใจในความสมบูรณ์และความถูกต้องของเอกสารของคุณ
## ข้อกำหนดเบื้องต้น
ก่อนที่เราจะเริ่ม ตรวจสอบให้แน่ใจว่าคุณมีข้อกำหนดเบื้องต้นดังต่อไปนี้:
1.  GroupDocs.Signature สำหรับ .NET: ตรวจสอบให้แน่ใจว่าคุณได้ติดตั้งและกำหนดค่า GroupDocs.Signature สำหรับ .NET แล้ว คุณสามารถดาวน์โหลดห้องสมุดได้จาก[ที่นี่](https://releases.groupdocs.com/signature/net/).
2. ไฟล์เอกสาร: เตรียมไฟล์เอกสาร (เช่น example_multiple_signatures.docx) ที่คุณต้องการตรวจสอบ

## นำเข้าเนมสเปซ
ขั้นแรก คุณต้องนำเข้าเนมสเปซที่จำเป็นลงในโปรเจ็กต์ของคุณ:
```csharp
using System;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## ขั้นตอนที่ 1: ตั้งค่าเส้นทางไฟล์เอกสาร
 กำหนดเส้นทางไฟล์ของเอกสารที่คุณต้องการตรวจสอบ แทนที่`"sample_multiple_signatures.docx"` พร้อมเส้นทางไปยังไฟล์เอกสารของคุณ
```csharp
string filePath = "sample_multiple_signatures.docx";
```
## ขั้นตอนที่ 2: เริ่มต้นวัตถุลายเซ็น
 สร้างอินสแตนซ์ของ`Signature` คลาสและส่งเส้นทางไฟล์ไปยังตัวสร้าง
```csharp
using (Signature signature = new Signature(filePath))
{
    // รหัสยืนยันจะถูกเขียนไว้ที่นี่
}
```
## ขั้นตอนที่ 3: ระบุตัวเลือกการยืนยันข้อความ
กำหนดตัวเลือกการยืนยันข้อความ รวมถึงข้อความที่จะยืนยัน ประเภทการจับคู่ และพารามิเตอร์อื่นๆ
```csharp
TextVerifyOptions options = new TextVerifyOptions()
{
    AllPages = true, // ตรวจสอบข้อความในทุกหน้า
    SignatureImplementation = TextSignatureImplementation.Native,
    Text = "signature", // ข้อความที่จะตรวจสอบ
    MatchType = TextMatchType.Contains // ระบุประเภทการจับคู่
};
```
## ขั้นตอนที่ 4: ตรวจสอบลายเซ็นเอกสาร
 เรียกใช้`Verify` วิธีการบน`Signature` คัดค้านและส่งตัวเลือกการตรวจสอบ
```csharp
VerificationResult result = signature.Verify(options);
```
## ขั้นตอนที่ 5: จัดการผลการตรวจสอบ
ตรวจสอบความถูกต้องของผลการตรวจสอบและดำเนินการตามนั้น
```csharp
if(result.IsValid)
{
    Console.WriteLine($"\nDocument {filePath} was verified successfully!");
    foreach (TextSignature item in result.Succeeded)
    {
        Console.WriteLine($"\nValid signature is found with text: {item.Text}");
    }
}
else
{
    Helper.WriteError($"\nDocument {filePath} failed verification process.");
}
```

## บทสรุป
โดยสรุป GroupDocs.Signature สำหรับ .NET มอบวิธีที่ราบรื่นในการตรวจสอบข้อความในเอกสาร ช่วยให้มั่นใจในความสมบูรณ์และความถูกต้องของเอกสาร ด้วยการทำตามขั้นตอนที่ระบุไว้ในบทช่วยสอนนี้ คุณสามารถรวมฟังก์ชันการตรวจสอบข้อความเข้ากับแอปพลิเคชัน .NET ของคุณได้อย่างง่ายดาย
## คำถามที่พบบ่อย
### GroupDocs.Signature สำหรับ .NET เข้ากันได้กับเอกสารทุกรูปแบบหรือไม่
ใช่ GroupDocs.Signature สำหรับ .NET รองรับรูปแบบเอกสารที่หลากหลาย รวมถึง DOCX, PDF, XLSX และอื่นๆ
### ฉันสามารถปรับแต่งเกณฑ์การตรวจสอบข้อความได้หรือไม่
แน่นอน คุณสามารถปรับแต่งพารามิเตอร์ต่างๆ ได้ เช่น ประเภทการจับคู่ ช่วงหน้า และอื่นๆ เพื่อให้เหมาะกับข้อกำหนดในการยืนยันของคุณ
### GroupDocs.Signature สำหรับ .NET ให้การสนับสนุนลายเซ็นดิจิทัลหรือไม่
ใช่ GroupDocs.Signature สำหรับ .NET รองรับทั้งลายเซ็นข้อความและลายเซ็นดิจิทัล ให้ความสามารถในการตรวจสอบเอกสารที่ครอบคลุม
### GroupDocs.Signature สำหรับ .NET มีรุ่นทดลองใช้ฟรีหรือไม่
 ใช่ คุณสามารถทดลองใช้ฟรีได้จาก[ที่นี่](https://releases.groupdocs.com/).
### ฉันจะขอความช่วยเหลือหรือสนับสนุน GroupDocs.Signature สำหรับ .NET ได้ที่ไหน
 ท่านสามารถเยี่ยมชมได้ที่[ฟอรัม GroupDocs.Signature](https://forum.groupdocs.com/c/signature/13) เพื่อขอความช่วยเหลือและการสนับสนุนจากชุมชน