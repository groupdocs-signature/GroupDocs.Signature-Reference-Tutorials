---
title: ลบลายเซ็นดิจิทัลออกจากเอกสาร
linktitle: ลบลายเซ็นดิจิทัลออกจากเอกสาร
second_title: GroupDocs.Signature .NET API
description: เรียนรู้วิธีลบลายเซ็นดิจิทัลออกจากเอกสารโดยใช้ GroupDocs.Signature สำหรับ .NET ปฏิบัติตามคำแนะนำทีละขั้นตอนของเราเพื่อการจัดการที่มีประสิทธิภาพ
type: docs
weight: 13
url: /th/net/delete-operations/delete-digital-signature/
---
## การแนะนำ
ในโลกของเอกสารดิจิทัล การรับรองความถูกต้องและความปลอดภัยเป็นสิ่งสำคัญยิ่ง ลายเซ็นดิจิทัลมีบทบาทสำคัญในการตรวจสอบความสมบูรณ์ของเอกสารอิเล็กทรอนิกส์ GroupDocs.Signature สำหรับ .NET นำเสนอเครื่องมือที่มีประสิทธิภาพในการจัดการลายเซ็นดิจิทัลภายในแอปพลิเคชัน .NET ได้อย่างมีประสิทธิภาพ
## ข้อกำหนดเบื้องต้น
ก่อนที่จะเริ่มใช้ GroupDocs.Signature สำหรับ .NET เพื่อลบลายเซ็นดิจิทัลออกจากเอกสาร ตรวจสอบให้แน่ใจว่าคุณมีสิ่งต่อไปนี้:
1. Visual Studio: ติดตั้ง Visual Studio IDE บนระบบของคุณ
2.  GroupDocs.Signature สำหรับ .NET: ดาวน์โหลดและติดตั้ง GroupDocs.Signature สำหรับ .NET จาก[หน้าดาวน์โหลด](https://releases.groupdocs.com/signature/net/).
3. เอกสารตัวอย่าง: เตรียมเอกสารตัวอย่างที่มีลายเซ็นดิจิทัลสำหรับการทดสอบ

## นำเข้าเนมสเปซ
ในการเริ่มต้น ตรวจสอบให้แน่ใจว่าได้นำเข้าเนมสเปซที่จำเป็นในโปรเจ็กต์ .NET ของคุณ:
```csharp
using System;
using System.IO;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
```
## ขั้นตอนที่ 1: กำหนดเส้นทางไฟล์
เริ่มต้นด้วยการกำหนดเส้นทางของไฟล์สำหรับเอกสารต้นฉบับและเอกสารเอาต์พุต:
```csharp
string filePath = "sample.pdf"_SIGNED_DIGITAL;
string fileName = Path.GetFileName(filePath);
string outputFilePath = Path.Combine("Your Document Directory", "DeleteDigital", fileName);
```
## ขั้นตอนที่ 2: คัดลอกเอกสารต้นฉบับ
 ตั้งแต่วันที่`Delete` วิธีการทำงานกับเอกสารเดียวกัน จำเป็นต้องคัดลอกไฟล์ต้นฉบับไปยังตำแหน่งใหม่:
```csharp
File.Copy(filePath, outputFilePath, true);
```
## ขั้นตอนที่ 3: เริ่มต้นวัตถุลายเซ็น
 เริ่มต้นก`Signature` วัตถุที่มีเส้นทางไฟล์เอาต์พุต:
```csharp
using (Signature signature = new Signature(outputFilePath))
{
    // รหัสของคุณอยู่ที่นี่
}
```
## ขั้นตอนที่ 4: ค้นหาลายเซ็นดิจิทัล
ค้นหาลายเซ็นดิจิทัลอิเล็กทรอนิกส์ภายในเอกสาร:
```csharp
List<DigitalSignature> signatures = signature.Search<DigitalSignature>(SignatureType.Digital);
```
## ขั้นตอนที่ 5: ลบลายเซ็นดิจิทัล
หากพบลายเซ็นดิจิทัล ให้ลบลายเซ็นแรกที่พบ:
```csharp
if (signatures.Count > 0)
{
    DigitalSignature digitalSignature = signatures[0];
    bool result = signature.Delete(digitalSignature);
    if (result)
    {
        Console.WriteLine($"Digital signature #{digitalSignature.Thumbprint} from {digitalSignature.SignTime.ToShortDateString()} was deleted from document ['{fileName}'].");
    }
    else
    {
        Helper.WriteError($"Signature was not deleted from the document! Signature# {digitalSignature.Thumbprint} was not found!");
    }
}
```

## บทสรุป
การจัดการลายเซ็นดิจิทัลในแอปพลิเคชัน .NET จะกลายเป็นเรื่องง่ายดายด้วย GroupDocs.Signature ด้วยการทำตามขั้นตอนง่ายๆ ที่อธิบายไว้ข้างต้น คุณสามารถลบลายเซ็นดิจิทัลออกจากเอกสารของคุณได้อย่างราบรื่น รับประกันความสมบูรณ์และความปลอดภัยของข้อมูล
## คำถามที่พบบ่อย
### ฉันสามารถลบลายเซ็นดิจิทัลหลายฉบับจากเอกสารฉบับเดียวได้หรือไม่
ได้ คุณสามารถแก้ไขโค้ดเพื่อวนซ้ำลายเซ็นดิจิทัลทั้งหมดที่พบ และลบออกตามลำดับ
### GroupDocs.Signature รองรับลายเซ็นประเภทอื่นนอกเหนือจากดิจิทัลหรือไม่
ใช่ GroupDocs.Signature รองรับลายเซ็นหลายประเภท รวมถึงลายเซ็นอิเล็กทรอนิกส์ ดิจิทัล และลายมือเขียน
### GroupDocs.Signature เหมาะสำหรับการจัดการเอกสารระดับองค์กรหรือไม่
GroupDocs.Signature ได้รับการออกแบบมาเพื่อตอบสนองความต้องการของนักพัฒนารายบุคคลและแอปพลิเคชันระดับองค์กร โดยนำเสนอฟีเจอร์ที่แข็งแกร่งและความสามารถในการปรับขนาดได้
### ฉันสามารถปรับแต่งกระบวนการลบลายเซ็นดิจิทัลได้หรือไม่
ใช่ GroupDocs.Signature มีตัวเลือกและการตั้งค่ามากมายเพื่อปรับแต่งกระบวนการลบลายเซ็นตามความต้องการเฉพาะของคุณ
### มีเวอร์ชันทดลองใช้สำหรับการทดสอบ GroupDocs.Signature หรือไม่
 ใช่ คุณสามารถดาวน์โหลดเวอร์ชันทดลองใช้ฟรีได้จาก[หน้าเผยแพร่](https://releases.groupdocs.com/).