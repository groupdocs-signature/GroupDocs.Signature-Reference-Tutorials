---
"description": "เรียนรู้วิธีฝังลายเซ็นเมตาเดตาลงในงานนำเสนอ PowerPoint โดยใช้ GroupDocs.Signature สำหรับ .NET เพิ่มรายละเอียดผู้เขียน ประทับเวลา และคุณสมบัติแบบกำหนดเอง เพื่อปรับปรุงความถูกต้องและการตรวจสอบย้อนกลับของงานนำเสนอ"
"linktitle": "การนำเสนอลายเซ็นพร้อมข้อมูลเมตา"
"second_title": "API ของ GroupDocs.Signature .NET"
"title": "ปรับปรุงการนำเสนอ PowerPoint ด้วยลายเซ็นข้อมูลเมตาใน C# .NET"
"url": "/th/net/document-signing/sign-presentation-with-metadata/"
"weight": 12
type: docs
---
## การแนะนำ

ในสถานที่ทำงานดิจิทัลในปัจจุบัน การนำเสนอถือเป็นเครื่องมือสำคัญสำหรับการสื่อสารและการแบ่งปันข้อมูล การรับรองความถูกต้องและความสมบูรณ์ของไฟล์งานนำเสนอเหล่านี้กำลังมีความสำคัญเพิ่มมากขึ้น โดยเฉพาะอย่างยิ่งในสภาพแวดล้อมขององค์กรและการศึกษา วิธีหนึ่งที่มีประสิทธิภาพในการเพิ่มความปลอดภัยและการตรวจสอบย้อนกลับของงานนำเสนอคือการฝังลายเซ็นเมตาเดตา

บทช่วยสอนที่ครอบคลุมนี้จะแนะนำคุณตลอดกระบวนการลงนามในงานนำเสนอ PowerPoint (PPTX, PPT) ด้วยข้อมูลเมตาโดยใช้ GroupDocs.Signature สำหรับ .NET การเพิ่มลายเซ็นข้อมูลเมตาช่วยให้คุณสามารถฝังข้อมูลสำคัญ เช่น รายละเอียดผู้เขียน ตราประทับเวลาที่สร้าง รหัสประจำตัวเอกสาร และคุณสมบัติแบบกำหนดเองอื่นๆ ลงในโครงสร้างไฟล์งานนำเสนอได้โดยตรง

## ข้อกำหนดเบื้องต้น

ก่อนที่จะดำเนินการตามบทช่วยสอนนี้ โปรดแน่ใจว่าคุณมีสิ่งต่อไปนี้:

1. [GroupDocs.Signature สำหรับ .NET](https://releases.groupdocs.com/signature/net/) - ดาวน์โหลดและติดตั้งไลบรารี
2. สภาพแวดล้อมการพัฒนา - Visual Studio หรือ IDE อื่นๆ ที่เข้ากันได้กับ .NET
3. การนำเสนอ PowerPoint - ไฟล์ตัวอย่างการนำเสนอ (รูปแบบ PPTX หรือ PPT)
4. ความรู้พื้นฐานเกี่ยวกับ C# - ความคุ้นเคยกับภาษาการเขียนโปรแกรม C#

## นำเข้าเนมสเปซ

เริ่มต้นด้วยการนำเข้าเนมสเปซที่จำเป็นเพื่อเข้าถึงฟังก์ชันการทำงานของ GroupDocs.Signature:

```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

## ขั้นตอนที่ 1: ตั้งค่าเส้นทางไฟล์

กำหนดเส้นทางสำหรับการนำเสนอแหล่งที่มาของคุณและตำแหน่งที่จะบันทึกเอาต์พุตที่ลงนาม:

```csharp
// ระบุเส้นทางไปยังไฟล์การนำเสนอของคุณ
string filePath = "sample.pptx";

// กำหนดไดเรกทอรีเอาต์พุตและชื่อไฟล์สำหรับการนำเสนอที่ลงนาม
string outputDirectory = "Your Document Directory";
string outputFilePath = Path.Combine(outputDirectory, "SignPresentationWithMetadata", "SignedWithMetadata.pptx");

// ตรวจสอบให้แน่ใจว่ามีไดเร็กทอรีเอาท์พุตอยู่
Directory.CreateDirectory(Path.GetDirectoryName(outputFilePath));
```

## ขั้นตอนที่ 2: เริ่มต้นวัตถุลายเซ็น

สร้างอินสแตนซ์ของคลาส Signature ด้วยไฟล์การนำเสนอต้นฉบับของคุณ:

```csharp
using (Signature signature = new Signature(filePath))
{
    // ส่วนที่เหลือของโค้ดจะอยู่ที่นี่
}
```

## ขั้นตอนที่ 3: สร้างและกำหนดค่าลายเซ็นข้อมูลเมตา

ขั้นตอนต่อไป กำหนดตัวเลือกเมตาข้อมูลและสร้างอาร์เรย์ของลายเซ็นเมตาข้อมูลการนำเสนอ:

```csharp
// สร้างวัตถุตัวเลือกเมตาข้อมูล
MetadataSignOptions options = new MetadataSignOptions();

// สร้างอาร์เรย์ของลายเซ็นข้อมูลเมตาการนำเสนอที่มีประเภทข้อมูลที่แตกต่างกัน
PresentationMetadataSignature[] signatures = new PresentationMetadataSignature[]
{
    new PresentationMetadataSignature("Author", "Mr.Sherlock Holmes"), // ค่าสตริง
    new PresentationMetadataSignature("CreatedOn", DateTime.Now),      // ค่าวันที่และเวลา
    new PresentationMetadataSignature("DocumentId", 123456),           // ค่าจำนวนเต็ม
    new PresentationMetadataSignature("SignatureId", 123.456D),        // ค่าสองเท่า
    new PresentationMetadataSignature("Amount", 123.456M),             // ค่าทศนิยม
    new PresentationMetadataSignature("Total", 123.456F)               // ค่าลอยตัว
};

// เพิ่มคอลเลกชันลายเซ็นให้กับตัวเลือก
options.Signatures.AddRange(signatures);
```

## ขั้นตอนที่ 4: ลงนามในงานนำเสนอพร้อมข้อมูลเมตา

ใช้ลายเซ็นข้อมูลเมตาในการนำเสนอและบันทึกผลลัพธ์:

```csharp
// ลงนามในเอกสารและบันทึกลงในเส้นทางไฟล์เอาต์พุต
SignResult result = signature.Sign(outputFilePath, options);

// แสดงข้อความแสดงความสำเร็จ
Console.WriteLine($"\nSource presentation signed successfully with {result.Succeeded.Count} metadata signature(s).");
Console.WriteLine($"Signed presentation saved at: {outputFilePath}");
```

## ตัวอย่างที่สมบูรณ์

นี่คือตัวอย่างโค้ดที่สมบูรณ์ซึ่งรวบรวมขั้นตอนทั้งหมดเข้าด้วยกัน:

```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;

namespace SignPresentationWithMetadataExample
{
    class Program
    {
        static void Main(string[] args)
        {
            // ระบุเส้นทางไฟล์
            string filePath = "sample.pptx";
            string outputFilePath = Path.Combine("Your Document Directory", "SignPresentationWithMetadata", "SignedWithMetadata.pptx");
            
            // ตรวจสอบให้แน่ใจว่ามีไดเร็กทอรีเอาท์พุตอยู่
            Directory.CreateDirectory(Path.GetDirectoryName(outputFilePath));

            // ลงนามในงานนำเสนอพร้อมข้อมูลเมตา
            using (Signature signature = new Signature(filePath))
            {
                // สร้างวัตถุตัวเลือกเมตาข้อมูล
                MetadataSignOptions options = new MetadataSignOptions();
                
                // สร้างอาร์เรย์ของลายเซ็นข้อมูลเมตาการนำเสนอที่มีประเภทข้อมูลที่แตกต่างกัน
                PresentationMetadataSignature[] signatures = new PresentationMetadataSignature[]
                {
                    new PresentationMetadataSignature("Author", "Mr.Sherlock Holmes"), // ค่าสตริง
                    new PresentationMetadataSignature("CreatedOn", DateTime.Now),      // ค่าวันที่และเวลา
                    new PresentationMetadataSignature("DocumentId", 123456),           // ค่าจำนวนเต็ม
                    new PresentationMetadataSignature("SignatureId", 123.456D),        // ค่าสองเท่า
                    new PresentationMetadataSignature("Amount", 123.456M),             // ค่าทศนิยม
                    new PresentationMetadataSignature("Total", 123.456F)               // ค่าลอยตัว
                };
                
                // เพิ่มคอลเลกชันลายเซ็นให้กับตัวเลือก
                options.Signatures.AddRange(signatures);
                
                // ลงนามเอกสารและบันทึกลงในไฟล์
                SignResult result = signature.Sign(outputFilePath, options);
                
                // แสดงผลลัพธ์
                Console.WriteLine($"\nSource presentation signed successfully with {result.Succeeded.Count} signature(s).");
                Console.WriteLine($"File saved at {outputFilePath}.");
            }
        }
    }
}
```

## เทคนิคการนำเสนอข้อมูลเมตาขั้นสูง

### การทำงานกับคุณสมบัติการนำเสนอแบบกำหนดเองและแบบในตัว

งานนำเสนอ PowerPoint มีทั้งคุณสมบัติในตัวและคุณสมบัติแบบกำหนดเอง ซึ่งสามารถเข้าถึงได้ผ่านกล่องโต้ตอบคุณสมบัติไฟล์ GroupDocs.Signature ช่วยให้คุณทำงานกับทั้งสองอย่าง:

```csharp
// เพิ่มคุณสมบัติในตัว
signatures = new PresentationMetadataSignature[]
{
    new PresentationMetadataSignature("Company", "Sherlock Holmes Consulting"),
    new PresentationMetadataSignature("Category", "Presentation"),
    new PresentationMetadataSignature("Keywords", "metadata,signing,groupdocs"),
    new PresentationMetadataSignature("Comments", "This document was signed with GroupDocs.Signature"),
    new PresentationMetadataSignature("Manager", "John Watson")
};
options.Signatures.AddRange(signatures);

// เพิ่มคุณสมบัติที่กำหนดเอง
options.Signatures.Add(new PresentationMetadataSignature("CustomProperty1", "Custom Value 1"));
options.Signatures.Add(new PresentationMetadataSignature("CustomProperty2", "Custom Value 2"));
```

### การค้นหาข้อมูลเมตาในงานนำเสนอที่ลงนาม

หลังจากลงนามแล้ว คุณอาจต้องการตรวจสอบหรือแยกข้อมูลเมตา:

```csharp
// สร้างตัวเลือกการค้นหาสำหรับข้อมูลเมตา
MetadataSearchOptions searchOptions = new MetadataSearchOptions();

// ค้นหาลายเซ็นข้อมูลเมตา
SearchResult searchResult = signature.Search(searchOptions);

// แสดงลายเซ็นที่พบ
Console.WriteLine($"Found {searchResult.Signatures.Count} metadata signatures:");
foreach (var foundSignature in searchResult.Signatures)
{
    MetadataSignature metadataSignature = foundSignature as MetadataSignature;
    if (metadataSignature != null)
    {
        Console.WriteLine($"- {metadataSignature.Name}: {metadataSignature.Value} ({metadataSignature.Value.GetType().Name})");
    }
}
```

### การอัปเดตข้อมูลเมตาที่มีอยู่

คุณสามารถอัปเดตข้อมูลเมตาที่มีอยู่ในงานนำเสนอได้โดยใช้ชื่อคุณสมบัติเดียวกัน:

```csharp
// อัปเดตข้อมูลเมตาที่มีอยู่
options.Signatures.Add(new PresentationMetadataSignature("Author", "Updated Author Name"));
```

## บทสรุป

ในบทช่วยสอนที่ครอบคลุมนี้ คุณจะได้เรียนรู้วิธีการลงนามในงานนำเสนอ PowerPoint ด้วยข้อมูลเมตาโดยใช้ GroupDocs.Signature สำหรับ .NET การฝังข้อมูลเมตาลงในไฟล์งานนำเสนอช่วยเพิ่มความสามารถในการติดตามเอกสาร ให้บริบทที่มีคุณค่า และช่วยยืนยันความถูกต้อง

ลายเซ็นเมตาเดตาในงานนำเสนอมีประโยชน์อย่างยิ่งในสภาพแวดล้อมทางธุรกิจและการศึกษาที่ให้ความสำคัญกับแหล่งที่มาของเอกสาร ผู้เขียน และการติดตามเวอร์ชัน เมตาเดตาที่ฝังไว้สามารถประกอบด้วยข้อมูลเกี่ยวกับผู้เขียน เวลาที่สร้าง รหัสประจำตัวเอกสาร และคุณสมบัติแบบกำหนดเองที่เกี่ยวข้องกับความต้องการขององค์กรของคุณ

การนำลายเซ็นเมตาข้อมูลมาใช้กับ GroupDocs.Signature จะช่วยให้คุณมั่นใจได้ว่าการนำเสนอ PowerPoint ของคุณจะยังคงความสมบูรณ์และให้ข้อมูลที่สามารถตรวจยืนยันได้ตลอดวงจรชีวิต

## คำถามที่พบบ่อย

### ฉันสามารถเพิ่มข้อมูลเมตาให้กับงานนำเสนอที่ได้กำหนดคุณสมบัติบางประการไว้แล้วได้หรือไม่

ใช่ คุณสามารถเพิ่มเมตาดาต้าใหม่หรืออัปเดตเมตาดาต้าที่มีอยู่ในงานนำเสนอได้ GroupDocs.Signature จะจัดการการผสานรวม ไม่ว่าจะโดยการเพิ่มคุณสมบัติใหม่หรืออัปเดตคุณสมบัติที่มีอยู่แล้วด้วยชื่อเดียวกัน

### รูปแบบการนำเสนอใดบ้างที่รองรับการลงนามข้อมูลเมตา?

GroupDocs.Signature สำหรับ .NET รองรับการลงนามเมตาดาต้าสำหรับงานนำเสนอ PowerPoint ในรูปแบบ PPT, PPTX, PPTM, PPS, PPSX และรูปแบบ PowerPoint อื่นๆ สำหรับรายการทั้งหมด โปรดดูที่ [เอกสารอย่างเป็นทางการ](https://docs-groupdocs.com/signature/net/).

### ลายเซ็นเมตาข้อมูลในงานนำเสนอจะมองเห็นได้จากผู้ดูหรือไม่

ลายเซ็นเมตาดาต้าจะไม่ปรากฏในสไลด์การนำเสนอ อย่างไรก็ตาม คุณสามารถดูได้ผ่านแผงคุณสมบัติเอกสารใน PowerPoint หรือแอปพลิเคชันอื่นๆ ที่เข้ากันได้

### ฉันสามารถเข้ารหัสข้อมูลเมตาที่ละเอียดอ่อนในงานนำเสนอได้หรือไม่

แม้ว่าคุณสมบัติเมตาดาต้าแต่ละรายการจะไม่สามารถเข้ารหัสได้ แต่ GroupDocs.Signature มีตัวเลือกสำหรับการรักษาความปลอดภัยเอกสารทั้งหมด คุณสามารถใช้การป้องกันด้วยรหัสผ่านเพื่อจำกัดการเข้าถึงงานนำเสนอและเมตาดาต้าได้

### การเพิ่มข้อมูลเมตาส่งผลต่อประสิทธิภาพการนำเสนอหรือไม่

การเพิ่มเมตาดาต้ามีผลกระทบต่อขนาดไฟล์เพียงเล็กน้อยและไม่มีผลกระทบต่อประสิทธิภาพการนำเสนอ ถือเป็นวิธีง่ายๆ ในการปรับปรุงคุณสมบัติของเอกสารโดยไม่กระทบต่อประสบการณ์ของผู้ใช้

### ฉันสามารถหาทรัพยากรและการสนับสนุนเพิ่มเติมได้ที่ไหน

- [ข้อมูลอ้างอิง API](https://reference.groupdocs.com/signature/net/)
- [ดาวน์โหลด](https://releases.groupdocs.com/signature/net/)
- [ตัวอย่าง](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
- [เอกสารประกอบ](https://docs.groupdocs.com/signature/net/)
- [หน้าผลิตภัณฑ์](https://products.groupdocs.com/signature/net/)
- [บล็อก](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
- [ฟอรั่มสนับสนุน](https://forum.groupdocs.com/c/signature/13)
- [ใบอนุญาตชั่วคราว](https://purchase.groupdocs.com/temporary-license/)