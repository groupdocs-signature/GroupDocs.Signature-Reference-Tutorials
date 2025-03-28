---
title: เซ็นชื่อรูปภาพด้วยข้อมูลเมตา
linktitle: เซ็นชื่อรูปภาพด้วยข้อมูลเมตา
second_title: GroupDocs.Signature .NET API
description: เรียนรู้วิธีเซ็นชื่อรูปภาพด้วยข้อมูลเมตาใน .NET โดยใช้ GroupDocs.Signature โซลูชันการเซ็นชื่อเมตาดาต้าที่ง่าย มีประสิทธิภาพ และปรับแต่งได้
weight: 10
url: /th/net/document-signing/sign-image-with-metadata/
---

# เซ็นชื่อรูปภาพด้วยข้อมูลเมตา

## การแนะนำ
GroupDocs.Signature สำหรับ .NET ช่วยให้นักพัฒนาสามารถเซ็นชื่อรูปภาพด้วยเมตาดาต้าได้อย่างมีประสิทธิภาพ บทช่วยสอนนี้จะแนะนำคุณตลอดกระบวนการทีละขั้นตอน
## ข้อกำหนดเบื้องต้น
ก่อนที่คุณจะเริ่มต้น ตรวจสอบให้แน่ใจว่าคุณมีสิ่งต่อไปนี้:
1. GroupDocs.Signature สำหรับ .NET: ติดตั้งแพ็คเกจ GroupDocs.Signature ในโครงการ .NET ของคุณ คุณสามารถดาวน์โหลดได้จาก[ที่นี่](https://releases.groupdocs.com/signature/net/).   
2. ไฟล์รูปภาพ: เตรียมไฟล์รูปภาพที่คุณต้องการเซ็นชื่อด้วยข้อมูลเมตา

## นำเข้าเนมสเปซ
ตรวจสอบให้แน่ใจว่าได้นำเข้าเนมสเปซที่จำเป็นในโค้ด C# ของคุณ:
```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## ขั้นตอนที่ 1: โหลดไฟล์รูปภาพ
ขั้นแรก ให้ระบุเส้นทางไปยังไฟล์รูปภาพของคุณและไดเร็กทอรีเอาต์พุตสำหรับรูปภาพที่เซ็นชื่อด้วยข้อมูลเมตา:
```csharp
string filePath = "sample.png";            
string outputFilePath = Path.Combine("Your Document Directory", "SignImageWithMetadata", "SignedWithMetadata.png");
```
## ขั้นตอนที่ 2: สร้างลายเซ็นข้อมูลเมตา
ถัดไป สร้างลายเซ็นข้อมูลเมตาที่แตกต่างกัน และเพิ่มลงในคอลเลกชันลายเซ็นตัวเลือก:
```csharp
using (Signature signature = new Signature(filePath))
{
    ushort imgsMetadataId = 41996;
    MetadataSignOptions options = new MetadataSignOptions();
    options
        .Add(new ImageMetadataSignature(imgsMetadataId++, "Mr.Scherlock Holmes")) // ค่าสตริง
        .Add(new ImageMetadataSignature(imgsMetadataId++, DateTime.Now))          // ค่าวันที่ เวลา
        .Add(new ImageMetadataSignature(imgsMetadataId++, 123456))                // ค่าจำนวนเต็ม
        .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456D))              // ค่าสองเท่า
        .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456M))              // ค่าทศนิยม
        .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456F));             // มูลค่าลอยตัว
    
    // ลงนามในเอกสารเพื่อยื่น
    SignResult result = signature.Sign(outputFilePath, options);
    Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).\nFile saved at {outputFilePath}.");
}
```

## บทสรุป
ในบทช่วยสอนนี้ คุณได้เรียนรู้วิธีเซ็นชื่อรูปภาพด้วยข้อมูลเมตาโดยใช้ GroupDocs.Signature สำหรับ .NET ด้วยการทำตามขั้นตอนเหล่านี้ คุณสามารถรวมลายเซ็นข้อมูลเมตาลงในแอปพลิเคชัน .NET ของคุณได้อย่างง่ายดาย

## คำถามที่พบบ่อย
### ฉันสามารถเซ็นชื่อหลายภาพด้วยข้อมูลเมตาโดยใช้ GroupDocs.Signature สำหรับ .NET ได้หรือไม่
ได้ คุณสามารถเซ็นชื่อรูปภาพหลายรูปด้วยเมทาดาทาได้โดยการวนซ้ำไฟล์รูปภาพแต่ละไฟล์และใช้ลายเซ็นเมทาดาทา
### มีรุ่นทดลองใช้สำหรับ GroupDocs.Signature สำหรับ .NET หรือไม่
 ใช่ คุณสามารถดาวน์โหลดเวอร์ชันทดลองได้จาก[ที่นี่](https://releases.groupdocs.com/).
### GroupDocs.Signature สำหรับ .NET รองรับไฟล์รูปแบบอื่นนอกเหนือจากรูปภาพหรือไม่
ใช่ GroupDocs.Signature รองรับไฟล์ได้หลากหลายรูปแบบ รวมถึง PDF, Word, Excel และอื่นๆ
### ฉันสามารถปรับแต่งลักษณะที่ปรากฏของลายเซ็นข้อมูลเมตาได้หรือไม่
ได้ คุณสามารถปรับแต่งลักษณะที่ปรากฏของลายเซ็นข้อมูลเมตาได้ เช่น ขนาดตัวอักษร สี และตำแหน่ง
### ฉันจะรับการสนับสนุนสำหรับ GroupDocs.Signature สำหรับ .NET ได้ที่ไหน
 คุณสามารถรับการสนับสนุนจากฟอรัม GroupDocs.Signature[ที่นี่](https://forum.groupdocs.com/c/signature/13).