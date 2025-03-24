---
title: ลบลายเซ็นหลายรายการออกจากเอกสาร
linktitle: ลบลายเซ็นหลายรายการออกจากเอกสาร
second_title: GroupDocs.Signature .NET API
description: ลบลายเซ็นหลายรายการจากเอกสารได้อย่างง่ายดายโดยใช้ GroupDocs.Signature สำหรับ .NET ปรับปรุงขั้นตอนการทำงานการจัดการเอกสารของคุณ
weight: 15
url: /th/net/delete-operations/delete-multiple-signatures/
---
## การแนะนำ
ในโลกดิจิทัล การจัดการเอกสารมักเกี่ยวข้องกับการจัดการลายเซ็นต่างๆ การลบลายเซ็นหลายรายการออกจากเอกสารโดยทางโปรแกรมสามารถปรับปรุงขั้นตอนการทำงานและเพิ่มประสิทธิภาพได้ ด้วย GroupDocs.Signature สำหรับ .NET งานนี้จึงราบรื่นและตรงไปตรงมา บทช่วยสอนนี้จะแนะนำคุณตลอดกระบวนการลบลายเซ็นหลายรายการออกจากเอกสารทีละขั้นตอน
## ข้อกำหนดเบื้องต้น
ก่อนที่จะเข้าสู่บทช่วยสอน ตรวจสอบให้แน่ใจว่าคุณมีข้อกำหนดเบื้องต้นต่อไปนี้:
- ความเข้าใจพื้นฐานเกี่ยวกับภาษาการเขียนโปรแกรม C#
- ติดตั้ง GroupDocs.Signature สำหรับไลบรารี .NET แล้ว
- ตัวอย่างเอกสารที่มีลายเซ็นหลายลายเซ็นสำหรับการทดสอบ

## นำเข้าเนมสเปซ
เริ่มต้นด้วยการนำเข้าเนมสเปซที่จำเป็นเพื่อเข้าถึงฟังก์ชันการทำงานของ GroupDocs.Signature สำหรับ .NET:
```csharp
using System;
using System.IO;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## ขั้นตอนที่ 1: กำหนดเส้นทางเอกสารและชื่อไฟล์
กำหนดเส้นทางไฟล์ของเอกสารที่มีลายเซ็นหลายรายการ ตรวจสอบให้แน่ใจว่าคุณมีพาธไฟล์และชื่อไฟล์ที่เหมาะสม:
```csharp
string filePath = "sample_multiple_signatures.docx";
string fileName = Path.GetFileName(filePath);
```
## ขั้นตอนที่ 2: คัดลอกเอกสารเพื่อการประมวลผล
เพื่อหลีกเลี่ยงการแก้ไขเอกสารต้นฉบับ ให้สร้างสำเนาสำหรับการประมวลผล:
```csharp
string outputFilePath = Path.Combine("Your Document Directory", "DeleteMultiple", fileName);
File.Copy(filePath, outputFilePath, true);
```
## ขั้นตอนที่ 3: เริ่มต้นวัตถุลายเซ็น
สร้างอินสแตนซ์ของวัตถุ Signature โดยใช้เส้นทางไฟล์เอาต์พุต:
```csharp
using (Signature signature = new Signature(outputFilePath))
{
    // รหัสประมวลผลลายเซ็นอยู่ที่นี่
}
```
## ขั้นตอนที่ 4: กำหนดตัวเลือกการค้นหา
กำหนดตัวเลือกการค้นหาต่างๆ เพื่อระบุลายเซ็นภายในเอกสาร ตัวเลือกต่างๆ ได้แก่ การค้นหาข้อความ การค้นหารูปภาพ การค้นหาบาร์โค้ด และการค้นหาโค้ด QR:
```csharp
TextSearchOptions textSearchOptions = new TextSearchOptions();
ImageSearchOptions imageSearchOptions = new ImageSearchOptions();
BarcodeSearchOptions barcodeOptions = new BarcodeSearchOptions();
QrCodeSearchOptions qrCodeOptions = new QrCodeSearchOptions();
// เพิ่มตัวเลือกในรายการ
List<SearchOptions> listOptions = new List<SearchOptions>();
listOptions.Add(textSearchOptions);
listOptions.Add(imageSearchOptions);
listOptions.Add(barcodeOptions);
listOptions.Add(qrCodeOptions);
```
## ขั้นตอนที่ 5: ค้นหาลายเซ็น
ดำเนินการค้นหาเพื่อค้นหาลายเซ็นทั้งหมดภายในเอกสารตามตัวเลือกการค้นหาที่กำหนดไว้:
```csharp
SearchResult result = signature.Search(listOptions);
```
## ขั้นตอนที่ 6: ลบลายเซ็น
หากพบลายเซ็น ให้ดำเนินการลบต่อไป:
```csharp
if (result.Signatures.Count > 0)
{
    // พยายามลบลายเซ็นทั้งหมด
    DeleteResult deleteResult = signature.Delete(result.Signatures);
    //ตรวจสอบว่าการลบสำเร็จหรือไม่
    if(deleteResult.Succeeded.Count == result.Signatures.Count)
    {
        Console.WriteLine("\nAll signatures were successfully deleted!");                        
    }
    else
    {
        Console.WriteLine($"Successfully deleted signatures : {deleteResult.Succeeded.Count}");
        Helper.WriteError($"Not deleted signatures : {deleteResult.Failed.Count}");
    }
    // แสดงข้อมูลเกี่ยวกับลายเซ็นที่ถูกลบ
    Console.WriteLine("\nList of deleted signatures:");
    int number = 1;
    foreach(BaseSignature temp in deleteResult.Succeeded)
    {
        Console.WriteLine($"Signature #{number++}: Type: {temp.SignatureType} Id:{temp.SignatureId}, Location: {temp.Left}x{temp.Top}. Size: {temp.Width}x{temp.Height}");
    }
}
else
{
    Helper.WriteError("No one signature was found.");
}
```

## บทสรุป
การลบลายเซ็นหลายรายการออกจากเอกสารโดยทางโปรแกรมถือเป็นงานสำคัญในการจัดการเอกสาร ด้วย GroupDocs.Signature สำหรับ .NET กระบวนการนี้จะมีประสิทธิภาพและเชื่อถือได้ ด้วยการทำตามขั้นตอนที่อธิบายไว้ในบทช่วยสอนนี้ คุณสามารถรวมฟังก์ชันการลบลายเซ็นเข้ากับแอปพลิเคชัน .NET ของคุณได้อย่างง่ายดาย
## คำถามที่พบบ่อย
### GroupDocs.Signature สำหรับ .NET สามารถจัดการรูปแบบเอกสารต่าง ๆ ได้หรือไม่
ใช่ GroupDocs.Signature สำหรับ .NET รองรับรูปแบบเอกสารที่หลากหลาย รวมถึง DOCX, PDF, PPTX, XLSX และอื่นๆ
### เป็นไปได้หรือไม่ที่จะปรับแต่งตัวเลือกการค้นหาสำหรับการตรวจจับลายเซ็น?
แน่นอน คุณสามารถปรับแต่งตัวเลือกการค้นหา เช่น การค้นหาข้อความ การค้นหารูปภาพ การค้นหาบาร์โค้ด และการค้นหาโค้ด QR เพื่อให้ตรงตามความต้องการเฉพาะของคุณ
### GroupDocs.Signature สำหรับ .NET มีกลไกการจัดการข้อผิดพลาดหรือไม่
ใช่ ไลบรารีมีความสามารถในการจัดการข้อผิดพลาดที่มีประสิทธิภาพเพื่อให้มั่นใจว่าการดำเนินงานการประมวลผลเอกสารเป็นไปอย่างราบรื่น
### ฉันสามารถรวม GroupDocs.Signature สำหรับ .NET เข้ากับไลบรารีของบริษัทอื่นได้หรือไม่
แน่นอนว่า GroupDocs.Signature สำหรับ .NET ได้รับการออกแบบมาเพื่อผสานรวมกับไลบรารี .NET อื่นๆ ได้อย่างราบรื่น โดยให้ความยืดหยุ่นและความสามารถในการขยายได้
### ฉันจะค้นหาการสนับสนุนและทรัพยากรเพิ่มเติมสำหรับ GroupDocs.Signature สำหรับ .NET ได้ที่ไหน
 คุณสามารถเยี่ยมชม GroupDocs[ฟอรั่ม](https://forum.groupdocs.com/c/signature/13) ทุ่มเทให้กับการอภิปรายที่เกี่ยวข้องกับลายเซ็นและขอความช่วยเหลือจากชุมชนและผู้เชี่ยวชาญ