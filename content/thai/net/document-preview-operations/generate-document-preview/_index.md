---
title: สร้างการแสดงตัวอย่างเอกสาร
linktitle: สร้างการแสดงตัวอย่างเอกสาร
second_title: GroupDocs.Signature .NET API
description: เรียนรู้วิธีสร้างหน้าตัวอย่างเอกสารโดยใช้ GroupDocs.Signature สำหรับ .NET ลดความซับซ้อนในการจัดการเอกสารในแอปพลิเคชัน .NET ของคุณ
weight: 10
url: /th/net/document-preview-operations/generate-document-preview/
---

# สร้างการแสดงตัวอย่างเอกสาร

## การแนะนำ
ในยุคดิจิทัลปัจจุบัน ที่เอกสารถือเป็นหัวใจสำคัญของการสื่อสารและการทำธุรกรรม การรับรองความสมบูรณ์และความถูกต้องของเอกสารเป็นสิ่งสำคัญยิ่ง GroupDocs.Signature สำหรับ .NET ช่วยให้นักพัฒนาสามารถรวมความสามารถในการลงนามเอกสารเข้ากับแอปพลิเคชัน .NET ของตนได้อย่างราบรื่น ในบทช่วยสอนนี้ เราจะเจาะลึกการสร้างหน้าตัวอย่างเอกสารโดยใช้ GroupDocs.Signature สำหรับ .NET โดยให้คำแนะนำทีละขั้นตอนสำหรับนักพัฒนา
## ข้อกำหนดเบื้องต้น
ก่อนที่จะเข้าสู่บทช่วยสอน ตรวจสอบให้แน่ใจว่าคุณมีข้อกำหนดเบื้องต้นต่อไปนี้:
1.  การติดตั้ง: ตรวจสอบให้แน่ใจว่าคุณได้ติดตั้ง GroupDocs.Signature สำหรับ .NET ในสภาพแวดล้อมการพัฒนาของคุณ หากไม่ใช่คุณสามารถดาวน์โหลดได้จาก[ที่นี่](https://releases.groupdocs.com/signature/net/).
2. .NET Framework: บทช่วยสอนนี้ถือว่ามีความคุ้นเคยกับ .NET Framework และภาษาการเขียนโปรแกรม C#

## การนำเข้าเนมสเปซ
ในการเริ่มต้น ให้นำเข้าเนมสเปซที่จำเป็นลงในโปรเจ็กต์ของคุณ:
```csharp
using System;
using System.IO;
    using GroupDocs.Signature;
    using GroupDocs.Signature.Options;
```
## ขั้นตอนที่ 1: โหลดเอกสาร
 ขั้นตอนแรกเกี่ยวข้องกับการโหลดเอกสารที่คุณต้องการสร้างการแสดงตัวอย่าง แทนที่`"sample.pdf"` พร้อมเส้นทางไปยังเอกสารที่คุณต้องการ
```csharp
string filePath = "sample.pdf";
using (Signature signature = new Signature(filePath))
{
    // รหัสไปที่นี่
}
```
## ขั้นตอนที่ 2: กำหนดตัวเลือกการแสดงตัวอย่าง
ถัดไป กำหนดตัวเลือกสำหรับการสร้างการแสดงตัวอย่างเอกสาร ระบุรูปแบบการแสดงตัวอย่างและวิธีการสร้างและปล่อยสตรีมเพจ
```csharp
PreviewOptions previewOption = new PreviewOptions(GeneratePreview.CreatePageStream, GeneratePreview.ReleasePageStream)
{
    PreviewFormat = PreviewOptions.PreviewFormats.JPEG,
};
```
## ขั้นตอนที่ 3: สร้างการแสดงตัวอย่าง
 ใช้`GeneratePreview()` วิธีการสร้างการแสดงตัวอย่างเอกสารตามตัวเลือกที่กำหนดไว้
```csharp
signature.GeneratePreview(previewOption);
```
## ขั้นตอนที่ 4: ใช้วิธี CreatePageStream
 ดำเนินการ`CreatePageStream` วิธีการสร้างเพจสตรีมสำหรับการสร้างตัวอย่าง
```csharp
private static Stream CreatePageStream(int pageNumber)
{
    string imageFilePath = Path.Combine("Your Document Directory", "GeneratePreviewFolder", "image-" + pageNumber.ToString() + ".jpg");
    var folder = Path.GetDirectoryName(imageFilePath);
    if (!Directory.Exists(folder))
    {
        Directory.CreateDirectory(folder);
    }
    return new FileStream(imageFilePath, FileMode.Create);
}
```
## ขั้นตอนที่ 5: ใช้วิธี ReleasePageStream
 ดำเนินการ`ReleasePageStream` วิธีการเผยแพร่สตรีมเพจหลังจากการสร้างตัวอย่าง
```csharp
private static void ReleasePageStream(int pageNumber, Stream pageStream)
{
    pageStream.Dispose();
    string imageFilePath = Path.Combine("Your Document Directory", "GeneratePreviewFolder", "image-" + pageNumber.ToString() + ".jpg");
    Console.WriteLine($"Image file {imageFilePath} is ready for preview");
}
```

## บทสรุป
โดยสรุป GroupDocs.Signature สำหรับ .NET ช่วยลดความยุ่งยากในการสร้างการแสดงตัวอย่างเอกสาร เพิ่มประสิทธิภาพการจัดการเอกสารและประสิทธิภาพเวิร์กโฟลว์ ด้วยการทำตามขั้นตอนที่ระบุไว้ในบทช่วยสอนนี้ นักพัฒนาสามารถรวมการสร้างหน้าตัวอย่างเอกสารเข้ากับแอปพลิเคชัน .NET ของตนได้อย่างราบรื่น เพื่อให้มั่นใจว่าผู้ใช้จะได้รับประสบการณ์ที่ราบรื่น
## คำถามที่พบบ่อย
### ฉันสามารถสร้างตัวอย่างสำหรับเอกสารอื่นที่ไม่ใช่ PDF ได้หรือไม่
ใช่ GroupDocs.Signature สำหรับ .NET รองรับรูปแบบเอกสารที่หลากหลาย รวมถึง Word, Excel, PowerPoint และอื่นๆ
### มีรุ่นทดลองใช้สำหรับ GroupDocs.Signature สำหรับ .NET หรือไม่
ใช่ คุณสามารถเข้าถึงเวอร์ชันทดลองใช้ฟรีได้จาก[ที่นี่](https://releases.groupdocs.com/).
### ฉันจะรับใบอนุญาตชั่วคราวเพื่อการทดสอบได้อย่างไร
 สามารถรับใบอนุญาตชั่วคราวได้จาก[ที่นี่](https://purchase.groupdocs.com/temporary-license/).
### ฉันจะรับการสนับสนุนสำหรับ GroupDocs.Signature สำหรับ .NET ได้ที่ไหน
 คุณสามารถขอการสนับสนุนและความช่วยเหลือได้จากฟอรัมชุมชน GroupDocs[ที่นี่](https://forum.groupdocs.com/c/signature/13).
### GroupDocs.Signature สำหรับ .NET เหมาะสำหรับแอปพลิเคชันระดับองค์กรหรือไม่
แน่นอนว่า GroupDocs.Signature สำหรับ .NET นั้นแข็งแกร่งและปรับขนาดได้ ทำให้เหมาะอย่างยิ่งสำหรับโซลูชันการจัดการเอกสารระดับองค์กร