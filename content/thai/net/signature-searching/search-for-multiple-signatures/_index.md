---
title: ค้นหาลายเซ็นหลายรายการ
linktitle: ค้นหาลายเซ็นหลายรายการ
second_title: GroupDocs.Signature .NET API
description: เรียนรู้วิธีค้นหาลายเซ็นหลายรายการในเอกสาร .NET โดยใช้ GroupDocs.Signature เพื่อความปลอดภัยและความสมบูรณ์ของเอกสารที่มีประสิทธิภาพ
weight: 14
url: /th/net/signature-searching/search-for-multiple-signatures/
---
## การแนะนำ
GroupDocs.Signature สำหรับ .NET เป็นไลบรารีที่มีประสิทธิภาพซึ่งช่วยให้นักพัฒนาสามารถเพิ่ม ค้นหา และลบลายเซ็นประเภทต่างๆ ในรูปแบบเอกสารยอดนิยมโดยใช้แอปพลิเคชัน .NET ในบทช่วยสอนนี้ เราจะเน้นที่การค้นหาลายเซ็นหลายรายการภายในเอกสารโดยใช้ GroupDocs.Signature สำหรับ .NET
## ข้อกำหนดเบื้องต้น
ก่อนที่เราจะเริ่มต้น ตรวจสอบให้แน่ใจว่าคุณมีข้อกำหนดเบื้องต้นดังต่อไปนี้:
- ติดตั้ง Visual Studio บนระบบของคุณแล้ว
- ความเข้าใจพื้นฐานเกี่ยวกับภาษาการเขียนโปรแกรม C#
- GroupDocs.Signature สำหรับไลบรารี .NET ที่ติดตั้งในโครงการของคุณ คุณสามารถดาวน์โหลดได้จาก[ที่นี่](https://releases.groupdocs.com/signature/net/).

## นำเข้าเนมสเปซ
ขั้นแรก คุณต้องนำเข้าเนมสเปซที่จำเป็นเพื่อเข้าถึงคลาสและวิธีการที่ได้รับจาก GroupDocs.Signature สำหรับ .NET
```csharp
using System;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## ขั้นตอนที่ 1: โหลดเอกสาร
โหลดเอกสารที่คุณต้องการค้นหาลายเซ็นหลายรายการ ตรวจสอบให้แน่ใจว่าคุณระบุเส้นทางไฟล์ที่ถูกต้อง
```csharp
string filePath = "sample_multiple_signatures.docx";
using (Signature signature = new Signature(filePath))
{
    // รหัสของคุณอยู่ที่นี่
}
```
## ขั้นตอนที่ 2: กำหนดตัวเลือกการค้นหา
กำหนดตัวเลือกการค้นหาสำหรับลายเซ็นประเภทต่างๆ เช่น ข้อความ ดิจิทัล บาร์โค้ด รหัส QR และข้อมูลเมตา คุณสามารถระบุเกณฑ์การค้นหา เช่น ข้อความที่จะจับคู่ ประเภทการจับคู่ และการค้นหาในทุกหน้า
```csharp
// กำหนดตัวเลือกการค้นหา
TextSearchOptions textOptions = new TextSearchOptions()
{
    AllPages = true
};
DigitalSearchOptions digitalOptions = new DigitalSearchOptions()
{
    AllPages = true
};
BarcodeSearchOptions barcodeOptions = new BarcodeSearchOptions()
{
    AllPages = true,
    Text = "123456",
    MatchType = TextMatchType.Exact
};
QrCodeSearchOptions qrCodeOptions = new QrCodeSearchOptions()
{
    AllPages = true,
    Text = "John",
    MatchType = TextMatchType.Contains
};
MetadataSearchOptions metadataOptions = new MetadataSearchOptions();
```
## ขั้นตอนที่ 3: เพิ่มตัวเลือกการค้นหาลงในรายการ
เพิ่มตัวเลือกการค้นหาที่กำหนดไว้ในรายการ
```csharp
// เพิ่มตัวเลือกในรายการ
List<SearchOptions> listOptions = new List<SearchOptions>();
listOptions.Add(textOptions);
listOptions.Add(barcodeOptions);
listOptions.Add(qrCodeOptions);
listOptions.Add(metadataOptions);
listOptions.Add(digitalOptions);
```
## ขั้นตอนที่ 4: ค้นหาลายเซ็น
ค้นหาลายเซ็นในเอกสารโดยใช้ตัวเลือกการค้นหาที่กำหนดไว้
```csharp
// ค้นหาลายเซ็นในเอกสาร
SearchResult result = signature.Search(listOptions);
if (result.Signatures.Count > 0)
{
    Console.WriteLine($"\nSource document ['{filePath}'] contains following signatures.");
    foreach (var resSignature in result.Signatures)
    {
        Console.WriteLine($"Signature found at page {resSignature.PageNumber} with type {resSignature.SignatureType} and Id#: {resSignature.SignatureId}");
    }
}
else
{
    Helper.WriteError("No one signature was found.");
}
```

## บทสรุป
ในบทช่วยสอนนี้ เราได้เรียนรู้วิธีค้นหาลายเซ็นหลายรายการภายในเอกสารโดยใช้ GroupDocs.Signature สำหรับ .NET ด้วยการทำตามขั้นตอนที่ให้ไว้ คุณสามารถค้นหาลายเซ็นประเภทต่างๆ ในเอกสารของคุณได้อย่างมีประสิทธิภาพ เพิ่มความปลอดภัยและความสมบูรณ์ของเอกสาร
## คำถามที่พบบ่อย
### ฉันสามารถค้นหาลายเซ็นในรูปแบบเอกสารต่างๆ ได้หรือไม่
ใช่ GroupDocs.Signature สำหรับ .NET รองรับรูปแบบเอกสารที่หลากหลาย รวมถึง Word, PDF, Excel และอื่นๆ
### สามารถปรับเกณฑ์การค้นหาลายเซ็นได้หรือไม่?
แน่นอน คุณสามารถปรับแต่งเกณฑ์การค้นหาตามความต้องการของคุณได้ เช่น การระบุข้อความที่ตรงกันทุกประการ หรือการค้นหาในทุกหน้า
### GroupDocs.Signature สำหรับ .NET รองรับลายเซ็นดิจิทัลหรือไม่
ใช่ คุณสามารถค้นหาลายเซ็นดิจิทัลได้ เช่นเดียวกับลายเซ็นประเภทอื่นๆ เช่น ข้อความ บาร์โค้ด และลายเซ็นรหัส QR
### ฉันสามารถรวมฟังก์ชันการค้นหาลายเซ็นเข้ากับแอปพลิเคชัน .NET ของฉันได้อย่างง่ายดายหรือไม่
ใช่ GroupDocs.Signature สำหรับ .NET มี API ที่ไม่ซับซ้อนซึ่งทำให้กระบวนการบูรณาการง่ายขึ้น
### ฉันจะรับการสนับสนุนหรือความช่วยเหลือเพิ่มเติมได้จากที่ไหน?
 คุณสามารถเยี่ยมชมฟอรัม GroupDocs.Signature[ที่นี่](https://forum.groupdocs.com/c/signature/13) หากมีข้อสงสัยหรือความช่วยเหลือ