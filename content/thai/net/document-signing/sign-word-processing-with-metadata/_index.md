---
"description": "เพิ่มลายเซ็นเมตาดาต้าลงในเอกสาร Word โดยใช้ GroupDocs.Signature สำหรับ .NET ฝังรายละเอียดผู้เขียน ประทับเวลา และคุณสมบัติที่กำหนดเองเพื่อเพิ่มความปลอดภัยและความสามารถในการตรวจสอบย้อนกลับของเอกสาร"
"linktitle": "การประมวลผลคำลงนามด้วยข้อมูลเมตา"
"second_title": "API ของ GroupDocs.Signature .NET"
"title": "ปรับปรุงเอกสาร Word ด้วยลายเซ็นเมตาข้อมูลใน C# .NET"
"url": "/th/net/document-signing/sign-word-processing-with-metadata/"
"weight": 14
---

## การแนะนำ

เอกสารประมวลผลคำเป็นประเภทไฟล์ที่นิยมใช้มากที่สุดในธุรกิจ การศึกษา และการสื่อสารส่วนบุคคล การตรวจสอบความถูกต้อง การติดตามแหล่งที่มา และการรักษาความสมบูรณ์ของเอกสารเหล่านี้เป็นสิ่งสำคัญอย่างยิ่งในสภาพแวดล้อมการทำงานที่หลากหลาย แนวทางหนึ่งที่มีประสิทธิภาพในการเพิ่มความปลอดภัยและความสามารถในการตรวจสอบย้อนกลับของเอกสารคือการฝังลายเซ็นเมตาเดตา

บทช่วยสอนที่ครอบคลุมนี้จะแนะนำคุณตลอดกระบวนการลงนามในเอกสารประมวลผลคำด้วยข้อมูลเมตาโดยใช้ GroupDocs.Signature สำหรับ .NET การเพิ่มลายเซ็นข้อมูลเมตาช่วยให้คุณสามารถฝังข้อมูลสำคัญ เช่น รายละเอียดผู้เขียน ตราประทับเวลาที่สร้าง รหัสประจำตัวเอกสาร และคุณสมบัติแบบกำหนดเองอื่นๆ ลงในโครงสร้างไฟล์เอกสารได้โดยตรง

## ข้อกำหนดเบื้องต้น

ก่อนที่จะดำเนินการตามบทช่วยสอนนี้ โปรดแน่ใจว่าคุณมีสิ่งต่อไปนี้:

1. [GroupDocs.Signature สำหรับ .NET](https://releases.groupdocs.com/signature/net/) - ดาวน์โหลดและติดตั้งไลบรารี
2. สภาพแวดล้อมการพัฒนา - Visual Studio หรือ IDE อื่นๆ ที่เข้ากันได้กับ .NET
3. เอกสาร Word - ไฟล์เอกสารตัวอย่าง (DOCX, DOC เป็นต้น)
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

กำหนดเส้นทางสำหรับเอกสาร Word ต้นทางของคุณและตำแหน่งที่จะบันทึกเอาต์พุตที่ลงนาม:

```csharp
// ระบุเส้นทางไปยังเอกสาร Word ของคุณ
string filePath = "sample.docx";

// กำหนดไดเรกทอรีเอาต์พุตและชื่อไฟล์สำหรับเอกสารที่ลงนาม
string outputDirectory = "Your Document Directory";
string outputFilePath = Path.Combine(outputDirectory, "SignWordProcessingWithMetadata", "SignedWithMetadata.docx");

// ตรวจสอบให้แน่ใจว่ามีไดเร็กทอรีเอาท์พุตอยู่
Directory.CreateDirectory(Path.GetDirectoryName(outputFilePath));
```

## ขั้นตอนที่ 2: เริ่มต้นวัตถุลายเซ็น

สร้างอินสแตนซ์ของคลาส Signature ด้วยเอกสาร Word ต้นทางของคุณ:

```csharp
using (Signature signature = new Signature(filePath))
{
    // ส่วนที่เหลือของโค้ดจะอยู่ที่นี่
}
```

## ขั้นตอนที่ 3: สร้างและกำหนดค่าลายเซ็นข้อมูลเมตา

ขั้นตอนต่อไป กำหนดตัวเลือกเมตาข้อมูลและเพิ่มลายเซ็นเมตาข้อมูลประเภทต่างๆ:

```csharp
// สร้างวัตถุตัวเลือกเมตาข้อมูล
MetadataSignOptions options = new MetadataSignOptions();

// เพิ่มข้อมูลเมตาประเภทต่างๆ โดยใช้อินเทอร์เฟซที่คล่องแคล่ว
options
    .Add(new WordProcessingMetadataSignature("Author", "Mr.Sherlock Holmes")) // ค่าสตริง
    .Add(new WordProcessingMetadataSignature("CreatedOn", DateTime.Now))      // ค่าวันที่และเวลา
    .Add(new WordProcessingMetadataSignature("DocumentId", 123456))           // ค่าจำนวนเต็ม
    .Add(new WordProcessingMetadataSignature("SignatureId", 123.456D))        // ค่าสองเท่า
    .Add(new WordProcessingMetadataSignature("Amount", 123.456M))             // ค่าทศนิยม
    .Add(new WordProcessingMetadataSignature("Total", 123.456F));             // ค่าลอยตัว
```

## ขั้นตอนที่ 4: ลงนามในเอกสารด้วยข้อมูลเมตา

ใช้ลายเซ็นข้อมูลเมตากับเอกสาร Word และบันทึกผลลัพธ์:

```csharp
// ลงนามในเอกสารและบันทึกลงในเส้นทางไฟล์เอาต์พุต
SignResult result = signature.Sign(outputFilePath, options);

// แสดงข้อความแสดงความสำเร็จ
Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} metadata signature(s).");
Console.WriteLine($"Signed document saved at: {outputFilePath}");
```

## ตัวอย่างที่สมบูรณ์

นี่คือตัวอย่างโค้ดที่สมบูรณ์ซึ่งรวบรวมขั้นตอนทั้งหมดเข้าด้วยกัน:

```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;

namespace SignWordProcessingWithMetadataExample
{
    class Program
    {
        static void Main(string[] args)
        {
            // ระบุเส้นทางไฟล์
            string filePath = "sample.docx";
            string outputFilePath = Path.Combine("Your Document Directory", "SignWordProcessingWithMetadata", "SignedWithMetadata.docx");
            
            // ตรวจสอบให้แน่ใจว่ามีไดเร็กทอรีเอาท์พุตอยู่
            Directory.CreateDirectory(Path.GetDirectoryName(outputFilePath));

            // ลงนามในเอกสาร Word ด้วยข้อมูลเมตา
            using (Signature signature = new Signature(filePath))
            {
                // สร้างวัตถุตัวเลือกเมตาข้อมูล
                MetadataSignOptions options = new MetadataSignOptions();
                
                // เพิ่มลายเซ็นข้อมูลเมตาประเภทต่างๆ
                options
                    .Add(new WordProcessingMetadataSignature("Author", "Mr.Sherlock Holmes")) // ค่าสตริง
                    .Add(new WordProcessingMetadataSignature("CreatedOn", DateTime.Now))      // ค่าวันที่และเวลา
                    .Add(new WordProcessingMetadataSignature("DocumentId", 123456))           // ค่าจำนวนเต็ม
                    .Add(new WordProcessingMetadataSignature("SignatureId", 123.456D))        // ค่าสองเท่า
                    .Add(new WordProcessingMetadataSignature("Amount", 123.456M))             // ค่าทศนิยม
                    .Add(new WordProcessingMetadataSignature("Total", 123.456F));             // ค่าลอยตัว
                
                // ลงนามเอกสารและบันทึกลงในไฟล์
                SignResult result = signature.Sign(outputFilePath, options);
                
                // แสดงผลลัพธ์
                Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).");
                Console.WriteLine($"File saved at {outputFilePath}.");
            }
        }
    }
}
```

## เทคนิคเมตาข้อมูลเอกสาร Word ขั้นสูง

### การทำงานกับคุณสมบัติเอกสารที่กำหนดเองและในตัว

เอกสาร Word มีทั้งคุณสมบัติในตัวและคุณสมบัติแบบกำหนดเอง ซึ่งสามารถเข้าถึงได้ผ่านแผงคุณสมบัติเอกสาร GroupDocs.Signature ช่วยให้คุณทำงานกับทั้งสองอย่าง:

```csharp
// เพิ่มคุณสมบัติในตัว
options
    .Add(new WordProcessingMetadataSignature("Company", "Sherlock Holmes Consulting"))
    .Add(new WordProcessingMetadataSignature("Category", "Legal Document"))
    .Add(new WordProcessingMetadataSignature("Keywords", "contract,agreement,legal"))
    .Add(new WordProcessingMetadataSignature("Comments", "This document is confidential"))
    .Add(new WordProcessingMetadataSignature("Manager", "John Watson"));

// เพิ่มคุณสมบัติที่กำหนดเอง
options.Add(new WordProcessingMetadataSignature("Department", "Legal"));
options.Add(new WordProcessingMetadataSignature("SecurityLevel", "Confidential"));
```

### การค้นหาข้อมูลเมตาในเอกสาร Word ที่มีลายเซ็น

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

### การทำงานกับตัวแปรเอกสาร

เอกสาร Word ยังรองรับตัวแปรเอกสาร ซึ่งเป็นรูปแบบอื่นของข้อมูลเมตา:

```csharp
// เพิ่มตัวแปรเอกสาร
options.Add(new WordProcessingMetadataSignature("DocVariable1", "Custom Value 1", true));
options.Add(new WordProcessingMetadataSignature("DocVariable2", DateTime.Now, true));
```

## บทสรุป

ในบทช่วยสอนที่ครอบคลุมนี้ คุณจะได้เรียนรู้วิธีการลงนามเอกสารประมวลผลคำด้วยข้อมูลเมตาโดยใช้ GroupDocs.Signature สำหรับ .NET การฝังข้อมูลเมตาลงในเอกสาร Word ช่วยเพิ่มความสามารถในการติดตามเอกสาร ให้บริบทที่มีคุณค่า และช่วยยืนยันความถูกต้อง

ลายเซ็นเมตาดาต้าในเอกสาร Word มีประโยชน์อย่างยิ่งในสภาพแวดล้อมทางธุรกิจและกฎหมายที่ให้ความสำคัญกับแหล่งที่มาของเอกสาร ผู้เขียน และการติดตามเวอร์ชัน เมตาดาต้าที่ฝังไว้สามารถประกอบด้วยข้อมูลเกี่ยวกับผู้เขียน เวลาที่สร้าง รหัสประจำตัวเอกสาร และคุณสมบัติแบบกำหนดเองที่เกี่ยวข้องกับความต้องการขององค์กรของคุณ

การนำลายเซ็นเมตาข้อมูลมาใช้กับ GroupDocs.Signature จะช่วยให้คุณมั่นใจได้ว่าเอกสาร Word ของคุณยังคงความสมบูรณ์และมีข้อมูลที่ตรวจสอบได้ตลอดวงจรชีวิต

## คำถามที่พบบ่อย

### ฉันสามารถเพิ่มข้อมูลเมตาลงในเอกสาร Word ที่ได้กำหนดคุณสมบัติบางประการไว้แล้วได้หรือไม่

ใช่ คุณสามารถเพิ่มเมตาดาต้าใหม่หรืออัปเดตเมตาดาต้าที่มีอยู่ในเอกสาร Word ได้ GroupDocs.Signature จะจัดการการผสานรวม ไม่ว่าจะโดยการเพิ่มคุณสมบัติใหม่หรืออัปเดตคุณสมบัติที่มีอยู่แล้วด้วยชื่อเดียวกัน

### รูปแบบการประมวลผลคำใดบ้างที่รองรับการลงนามข้อมูลเมตา?

GroupDocs.Signature สำหรับ .NET รองรับการลงนามเมตาดาต้าสำหรับรูปแบบการประมวลผลคำต่างๆ รวมถึง DOCX, DOC, RTF, ODT และอื่นๆ สำหรับรายการทั้งหมด โปรดดูที่ [เอกสารประกอบ](https://docs-groupdocs.com/signature/net/).

### ลายเซ็นเมตาข้อมูลในเอกสาร Word จะให้ผู้อ่านมองเห็นได้หรือไม่

ลายเซ็นเมตาดาต้าจะไม่ปรากฏในเนื้อหาของเอกสารโดยตรง อย่างไรก็ตาม คุณสามารถดูได้ผ่านแผงคุณสมบัติเอกสารใน Microsoft Word หรือแอปพลิเคชันอื่นๆ ที่เข้ากันได้

### ฉันสามารถตรวจสอบด้วยโปรแกรมได้หรือไม่ว่าเอกสาร Word ถูกเปลี่ยนแปลงหลังจากเพิ่มข้อมูลเมตาหรือไม่

ใช่ GroupDocs.Signature มีความสามารถในการตรวจสอบที่ช่วยตรวจจับว่าเอกสารได้รับการแก้ไขหรือไม่หลังจากการลงนาม รวมถึงการเปลี่ยนแปลงข้อมูลเมตา

### เป็นไปได้ไหมที่จะลบข้อมูลเมตาออกจากเอกสาร Word?

ใช่ GroupDocs.Signature มีตัวเลือกสำหรับลบลายเซ็นเมตาดาต้าออกจากเอกสารหากจำเป็น วิธีนี้มีประโยชน์สำหรับการทำความสะอาดข้อมูลสำคัญก่อนแชร์เอกสารกับภายนอก

### ฉันสามารถหาทรัพยากรและการสนับสนุนเพิ่มเติมได้ที่ไหน

- [ข้อมูลอ้างอิง API](https://reference.groupdocs.com/signature/net/)
- [ดาวน์โหลด](https://releases.groupdocs.com/signature/net/)
- [ตัวอย่าง](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
- [เอกสารประกอบ](https://docs.groupdocs.com/signature/net/)
- [หน้าผลิตภัณฑ์](https://products.groupdocs.com/signature/net/)
- [บล็อก](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
- [ฟอรั่มสนับสนุน](https://forum.groupdocs.com/c/signature/13)
- [ใบอนุญาตชั่วคราว](https://purchase.groupdocs.com/temporary-license/)