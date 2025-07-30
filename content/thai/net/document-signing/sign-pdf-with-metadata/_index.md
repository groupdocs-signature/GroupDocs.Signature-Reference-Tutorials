---
"description": "รวมลายเซ็นเมตาดาต้าลงในเอกสาร PDF โดยใช้ GroupDocs.Signature สำหรับ .NET เรียนรู้การฝังข้อมูลผู้เขียน ประทับเวลา และข้อมูลที่กำหนดเอง เพื่อปรับปรุงความถูกต้องและการตรวจสอบย้อนกลับของ PDF"
"linktitle": "ลงนาม PDF ด้วยข้อมูลเมตา"
"second_title": "API ของ GroupDocs.Signature .NET"
"title": "เพิ่มลายเซ็นข้อมูลเมตาลงในเอกสาร PDF ใน C# .NET"
"url": "/th/net/document-signing/sign-pdf-with-metadata/"
"weight": 11
---

## การแนะนำ

เอกสาร PDF (Portable Document Format) ถูกใช้กันอย่างแพร่หลายในอุตสาหกรรมต่างๆ เนื่องจากความสอดคล้องและความเป็นอิสระของแพลตฟอร์ม การรับรองความถูกต้องและการตรวจสอบย้อนกลับของเอกสารเหล่านี้เป็นสิ่งสำคัญอย่างยิ่งในสภาพแวดล้อมการทำงานที่หลากหลาย วิธีหนึ่งที่มีประสิทธิภาพในการบรรลุเป้าหมายนี้คือการฝังข้อมูลเมตาลงในไฟล์ PDF

ในบทช่วยสอนที่ครอบคลุมนี้ เราจะสำรวจวิธีการลงนามในเอกสาร PDF ด้วยข้อมูลเมตาโดยใช้ GroupDocs.Signature สำหรับ .NET ลายเซ็นข้อมูลเมตาช่วยให้คุณสามารถฝังข้อมูลเพิ่มเติมลงในเอกสาร เช่น รายละเอียดผู้เขียน ตราประทับเวลาที่สร้าง รหัสประจำตัวเอกสาร และค่าที่กำหนดเอง โดยไม่ทำให้รูปลักษณ์ของเอกสารเปลี่ยนแปลงไปอย่างเห็นได้ชัด

## ข้อกำหนดเบื้องต้น

ก่อนที่เราจะเริ่ม โปรดตรวจสอบให้แน่ใจว่าคุณมีสิ่งต่อไปนี้:

1. [GroupDocs.Signature สำหรับ .NET](https://releases.groupdocs.com/signature/net/) - ดาวน์โหลดและติดตั้งไลบรารี
2. สภาพแวดล้อมการพัฒนา - Visual Studio หรือ IDE อื่นๆ ที่เข้ากันได้กับ .NET
3. เอกสาร PDF - ตัวอย่างไฟล์ PDF สำหรับการลงนาม
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

ขั้นแรก ให้กำหนดเส้นทางไปยังเอกสาร PDF ของคุณ และระบุตำแหน่งที่คุณต้องการบันทึกเอาต์พุตที่ลงนาม:

```csharp
// ระบุเส้นทางไปยังเอกสาร PDF ของคุณ
string filePath = "sample.pdf";

// กำหนดไดเรกทอรีเอาต์พุตและเส้นทางไฟล์
string outputDirectory = "Your Document Directory";
string outputFilePath = Path.Combine(outputDirectory, "SignPdfWithMetadata", "SignedWithMetadata.pdf");

// ตรวจสอบให้แน่ใจว่ามีไดเร็กทอรีเอาท์พุตอยู่
Directory.CreateDirectory(Path.GetDirectoryName(outputFilePath));
```

## ขั้นตอนที่ 2: เริ่มต้นวัตถุลายเซ็น

สร้างอินสแตนซ์ของคลาส Signature ด้วยเอกสาร PDF ต้นฉบับของคุณ:

```csharp
using (Signature signature = new Signature(filePath))
{
    // รหัสสำหรับการลงนามจะอยู่ที่นี่
}
```

## ขั้นตอนที่ 3: กำหนดตัวเลือกข้อมูลเมตา

สร้างและกำหนดค่าตัวเลือกเมตาข้อมูล เพิ่มลายเซ็นเมตาข้อมูลประเภทต่างๆ:

```csharp
// สร้างวัตถุตัวเลือกเมตาข้อมูล
MetadataSignOptions options = new MetadataSignOptions();

// เพิ่มข้อมูลเมตาประเภทต่างๆ โดยใช้อินเทอร์เฟซที่คล่องแคล่ว
options
    .Add(new PdfMetadataSignature("Author", "Mr.Sherlock Holmes")) // ค่าสตริง
    .Add(new PdfMetadataSignature("CreatedOn", DateTime.Now))       // ค่าวันที่และเวลา
    .Add(new PdfMetadataSignature("DocumentId", 123456))            // ค่าจำนวนเต็ม
    .Add(new PdfMetadataSignature("SignatureId", 123.456D))         // ค่าสองเท่า
    .Add(new PdfMetadataSignature("Amount", 123.456M))              // ค่าทศนิยม
    .Add(new PdfMetadataSignature("Total", 123.456F));              // ค่าลอยตัว
```

## ขั้นตอนที่ 4: ลงนาม PDF ด้วยข้อมูลเมตา

ใช้ลายเซ็นเมตาข้อมูลกับเอกสาร PDF และบันทึกผลลัพธ์:

```csharp
// ลงนามในเอกสารและบันทึกลงในเส้นทางเอาต์พุต
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

namespace SignPdfWithMetadataExample
{
    class Program
    {
        static void Main(string[] args)
        {
            // ระบุเส้นทางไฟล์
            string filePath = "sample.pdf";
            string outputFilePath = Path.Combine("Your Document Directory", "SignPdfWithMetadata", "SignedWithMetadata.pdf");
            
            // ตรวจสอบให้แน่ใจว่ามีไดเร็กทอรีเอาท์พุตอยู่
            Directory.CreateDirectory(Path.GetDirectoryName(outputFilePath));

            // ลงนามใน PDF ด้วยข้อมูลเมตา
            using (Signature signature = new Signature(filePath))
            {
                // สร้างวัตถุตัวเลือกเมตาข้อมูล
                MetadataSignOptions options = new MetadataSignOptions();
                
                // เพิ่มลายเซ็นข้อมูลเมตาประเภทต่างๆ
                options
                    .Add(new PdfMetadataSignature("Author", "Mr.Sherlock Holmes")) // ค่าสตริง
                    .Add(new PdfMetadataSignature("CreatedOn", DateTime.Now))       // ค่าวันที่และเวลา
                    .Add(new PdfMetadataSignature("DocumentId", 123456))            // ค่าจำนวนเต็ม
                    .Add(new PdfMetadataSignature("SignatureId", 123.456D))         // ค่าสองเท่า
                    .Add(new PdfMetadataSignature("Amount", 123.456M))              // ค่าทศนิยม
                    .Add(new PdfMetadataSignature("Total", 123.456F));              // ค่าลอยตัว
                
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

## การดำเนินการเมตาข้อมูล PDF ขั้นสูง

### การเพิ่มข้อมูลเมตาแบบกำหนดเองพร้อมการรองรับเนมสเปซ

เอกสาร PDF รองรับข้อมูลเมตาแบบกำหนดเองพร้อมการรองรับเนมสเปซ XML:

```csharp
// เพิ่มข้อมูลเมตาที่กำหนดเองด้วยเนมสเปซ
options.Add(new PdfMetadataSignature("CustomProperty", "Custom Value")
{
    NamespaceUri = "http://your-namespace.com/schema"
});
```

### การค้นหาข้อมูลเมตาใน PDF ที่ลงนาม

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

### การทำงานกับข้อมูลเมตา PDF มาตรฐาน

เอกสาร PDF มีฟิลด์เมตาข้อมูลมาตรฐานที่สามารถเข้าถึงและแก้ไขได้:

```csharp
// ตั้งค่าฟิลด์เมตาข้อมูล PDF มาตรฐาน
options
    .Add(new PdfMetadataSignature("Title", "Important Contract"))
    .Add(new PdfMetadataSignature("Subject", "Legal Agreement"))
    .Add(new PdfMetadataSignature("Keywords", "contract, agreement, legal, binding"))
    .Add(new PdfMetadataSignature("Creator", "Legal Department"))
    .Add(new PdfMetadataSignature("Producer", "GroupDocs.Signature"));
```

## บทสรุป

ในบทช่วยสอนนี้ คุณได้เรียนรู้วิธีการลงนามในเอกสาร PDF ด้วยข้อมูลเมตาโดยใช้ GroupDocs.Signature สำหรับ .NET การฝังข้อมูลเมตาลงในไฟล์ PDF ถือเป็นวิธีที่ยอดเยี่ยมในการเพิ่มความถูกต้องของเอกสาร เพิ่มข้อมูลสำคัญ และปรับปรุงเวิร์กโฟลว์การจัดการเอกสาร

ลายเซ็นเมตาเดตาในไฟล์ PDF มีประโยชน์อย่างยิ่งในสภาพแวดล้อมทางธุรกิจที่การตรวจสอบย้อนกลับและความถูกต้องของเอกสารเป็นสิ่งสำคัญ เมตาเดตาที่ฝังไว้สามารถประกอบด้วยข้อมูลเกี่ยวกับแหล่งที่มาของเอกสาร ผู้เขียน เวลาที่สร้าง เวอร์ชัน และคุณสมบัติที่กำหนดเองที่เกี่ยวข้องกับเวิร์กโฟลว์ขององค์กรของคุณ

การนำลายเซ็นเมตาข้อมูลมาใช้กับ GroupDocs.Signature จะช่วยให้คุณมั่นใจได้ว่าเอกสาร PDF ของคุณยังคงความสมบูรณ์และมีข้อมูลที่ตรวจสอบได้ตลอดวงจรชีวิต

## คำถามที่พบบ่อย

### ฉันสามารถแก้ไขข้อมูลเมตาที่มีอยู่แล้วในเอกสาร PDF ได้หรือไม่

ใช่ คุณสามารถแก้ไขข้อมูลเมตาที่มีอยู่ในเอกสาร PDF ได้ เมื่อคุณใช้ลายเซ็นข้อมูลเมตาใหม่ที่มีชื่อเดียวกับลายเซ็นที่มีอยู่ ค่าต่างๆ จะได้รับการอัปเดตตามไปด้วย

### ลายเซ็นเมตาข้อมูลในเอกสาร PDF จะปรากฏให้ผู้ใช้ปลายทางเห็นหรือไม่

ลายเซ็นเมตาดาต้าจะไม่ปรากฏในเนื้อหาของเอกสารโดยตรง อย่างไรก็ตาม คุณสามารถดูได้ผ่านแผงคุณสมบัติเอกสารในโปรแกรมอ่าน PDF เช่น Adobe Acrobat หรือใช้เครื่องมือเฉพาะทางสำหรับการดูข้อมูลเมตา

### ฉันสามารถเข้ารหัสหรือปกป้องข้อมูลเมตาใน PDF ได้หรือไม่

GroupDocs.Signature มีตัวเลือกสำหรับการรักษาความปลอดภัยเอกสาร รวมถึงการเข้ารหัส คุณสามารถใช้การเข้ารหัสระดับเอกสารเพื่อปกป้องไฟล์ PDF ทั้งหมด รวมถึงข้อมูลเมตาด้วย

### มีข้อจำกัดเกี่ยวกับจำนวนข้อมูลเมตาที่ฉันสามารถเพิ่มลงใน PDF ได้หรือไม่

แม้ว่าข้อกำหนด PDF จะไม่มีข้อจำกัดที่เข้มงวด แต่การเพิ่มข้อมูลเมตาดาต้ามากเกินไปอาจทำให้ขนาดไฟล์เพิ่มขึ้น ขอแนะนำให้ใส่เฉพาะข้อมูลที่เกี่ยวข้องและจำเป็นลงในข้อมูลเมตาดาต้าเท่านั้น

### ฉันสามารถตรวจสอบด้วยโปรแกรมได้หรือไม่ว่า PDF ถูกเปลี่ยนแปลงหรือไม่หลังจากเพิ่มข้อมูลเมตาแล้ว

ใช่ GroupDocs.Signature มีความสามารถในการตรวจสอบที่ช่วยตรวจจับว่าเอกสารได้รับการแก้ไขหรือไม่หลังจากการลงนาม รวมถึงการเปลี่ยนแปลงข้อมูลเมตา

### ฉันสามารถหาทรัพยากรและการสนับสนุนเพิ่มเติมได้ที่ไหน

- [ข้อมูลอ้างอิง API](https://reference.groupdocs.com/signature/net/)
- [ดาวน์โหลด](https://releases.groupdocs.com/signature/net/)
- [ตัวอย่าง](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
- [เอกสารประกอบ](https://docs.groupdocs.com/signature/net/)
- [หน้าผลิตภัณฑ์](https://products.groupdocs.com/signature/net/)
- [บล็อก](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
- [ฟอรั่มสนับสนุน](https://forum.groupdocs.com/c/signature/13)
- [ใบอนุญาตชั่วคราว](https://purchase.groupdocs.com/temporary-license/)