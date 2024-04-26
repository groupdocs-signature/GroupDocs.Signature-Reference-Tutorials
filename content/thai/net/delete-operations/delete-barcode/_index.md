---
title: ลบบาร์โค้ดออกจากเอกสาร
linktitle: ลบบาร์โค้ดออกจากเอกสาร
second_title: GroupDocs.Signature .NET API
description: เรียนรู้วิธีลบบาร์โค้ดออกจากเอกสารโดยใช้ GroupDocs.Signature สำหรับ .NET คำแนะนำทีละขั้นตอนพร้อมตัวอย่างโค้ด
type: docs
weight: 10
url: /th/net/delete-operations/delete-barcode/
---
## การแนะนำ
GroupDocs.Signature สำหรับ .NET เป็นไลบรารีที่มีประสิทธิภาพซึ่งช่วยให้นักพัฒนาสามารถทำงานกับลายเซ็นดิจิทัล ตราประทับ และบาร์โค้ดภายในแอปพลิเคชัน .NET ได้อย่างราบรื่น ในบทช่วยสอนนี้ เราจะแนะนำคุณตลอดขั้นตอนการลบบาร์โค้ดออกจากเอกสารโดยใช้ GroupDocs.Signature สำหรับ .NET
## ข้อกำหนดเบื้องต้น
ก่อนที่เราจะเริ่ม ตรวจสอบให้แน่ใจว่าคุณมีข้อกำหนดเบื้องต้นดังต่อไปนี้:
- ความรู้พื้นฐานเกี่ยวกับภาษาการเขียนโปรแกรม C#
- ติดตั้ง Visual Studio บนระบบของคุณแล้ว
-  ติดตั้ง GroupDocs.Signature สำหรับไลบรารี .NET แล้ว คุณสามารถดาวน์โหลดได้จาก[ที่นี่](https://releases.groupdocs.com/signature/net/).
- ตัวอย่างเอกสารที่มีบาร์โค้ดที่คุณต้องการลบ

## นำเข้าเนมสเปซ
ขั้นแรก ตรวจสอบให้แน่ใจว่าได้นำเข้าเนมสเปซที่จำเป็นลงในโค้ด C# ของคุณ:
```csharp
using System;
using System.IO;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

เรามาแจกแจงขั้นตอนการลบบาร์โค้ดออกจากเอกสารเป็นขั้นตอนง่ายๆ:
## ขั้นตอนที่ 1: กำหนดเส้นทางไฟล์
```csharp
string filePath = "sample_multiple_signatures.docx";
string fileName = Path.GetFileName(filePath);
string outputFilePath = Path.Combine("Your Document Directory", "DeleteBarcode", fileName);
```
 ให้แน่ใจว่าจะเปลี่ยน`"sample_multiple_signatures.docx"` พร้อมเส้นทางไปยังเอกสารของคุณที่มีบาร์โค้ด
## ขั้นตอนที่ 2: คัดลอกไฟล์ต้นฉบับ
```csharp
File.Copy(filePath, outputFilePath, true);
```
ขั้นตอนนี้ช่วยให้แน่ใจว่าเรากำลังทำงานกับสำเนาของเอกสารต้นฉบับเพื่อรักษาไฟล์ต้นฉบับ
## ขั้นตอนที่ 3: เริ่มต้น GroupDocs.Signature
```csharp
using (Signature signature = new Signature(outputFilePath))
{
    // รหัสของคุณอยู่ที่นี่
}
```
เตรียมใช้งานออบเจ็กต์ลายเซ็นโดยส่งเส้นทางไปยังสำเนาเอกสารที่สร้างขึ้นในขั้นตอนก่อนหน้า
## ขั้นตอนที่ 4: ค้นหาลายเซ็นบาร์โค้ด
```csharp
BarcodeSearchOptions options = new BarcodeSearchOptions();
List<BarcodeSignature> signatures = signature.Search<BarcodeSignature>(options);
```
สร้างอินสแตนซ์ของ BarcodeSearchOptions และใช้เพื่อค้นหาลายเซ็นบาร์โค้ดภายในเอกสาร
## ขั้นตอนที่ 5: ลบลายเซ็นบาร์โค้ด
```csharp
if (signatures.Count > 0)
{
    BarcodeSignature barcodeSignature = signatures[0];
    bool result = signature.Delete(barcodeSignature);
    if (result)
    {
        Console.WriteLine($"Signature with Barcode '{barcodeSignature.Text}' and encode type '{barcodeSignature.EncodeType.TypeName}' was deleted from document ['{fileName}'].");
    }
    else
    {
        Helper.WriteError($"Signature was not deleted from the document! Signature with Barcode '{barcodeSignature.Text}' and encode type '{barcodeSignature.EncodeType.TypeName}' was not found!");
    }
}
```
ตรวจสอบว่าพบลายเซ็นบาร์โค้ดในเอกสารหรือไม่ หากพบให้ลบลายเซ็นบาร์โค้ดแรกที่พบ

## บทสรุป
ในบทช่วยสอนนี้ เราได้เรียนรู้วิธีลบบาร์โค้ดออกจากเอกสารโดยใช้ GroupDocs.Signature สำหรับ .NET ด้วยการทำตามคำแนะนำทีละขั้นตอน คุณสามารถรวมฟังก์ชันการลบบาร์โค้ดเข้ากับแอปพลิเคชัน .NET ของคุณได้อย่างราบรื่น
## คำถามที่พบบ่อย
### ฉันสามารถลบลายเซ็นบาร์โค้ดหลายลายเซ็นออกจากเอกสารได้หรือไม่
ได้ คุณสามารถแก้ไขโค้ดเพื่อลบลายเซ็นบาร์โค้ดหลายรายการได้โดยการวนซ้ำรายการลายเซ็น
### GroupDocs.Signature สำหรับ .NET รองรับลายเซ็นประเภทอื่นหรือไม่
ใช่ GroupDocs.Signature สำหรับ .NET รองรับลายเซ็นหลายประเภท รวมถึงลายเซ็นดิจิทัล ตราประทับ และลายเซ็นข้อความ
### ฉันสามารถปรับแต่งตัวเลือกการค้นหาสำหรับลายเซ็นบาร์โค้ดได้หรือไม่
ได้ คุณสามารถปรับแต่งตัวเลือกการค้นหาได้ตามความต้องการของคุณ เช่น การระบุประเภทบาร์โค้ดหรือพื้นที่การค้นหาภายในเอกสาร
### GroupDocs.Signature สำหรับ .NET เข้ากันได้กับรูปแบบเอกสารที่แตกต่างกันหรือไม่
ใช่ GroupDocs.Signature สำหรับ .NET รองรับรูปแบบเอกสารที่หลากหลาย รวมถึง Word, Excel, PDF และอื่นๆ
### ฉันจะค้นหาการสนับสนุนหรือแหล่งข้อมูลเพิ่มเติมสำหรับ GroupDocs.Signature สำหรับ .NET ได้ที่ไหน
 คุณสามารถเยี่ยมชมฟอรัม GroupDocs.Signature[ที่นี่](https://forum.groupdocs.com/c/signature/13) หากมีข้อสงสัยหรือความช่วยเหลือเกี่ยวกับห้องสมุด