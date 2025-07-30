---
"description": "ปกป้องและปรับปรุงสเปรดชีต Excel ด้วยการฝังลายเซ็นเมตาดาต้าโดยใช้ GroupDocs.Signature สำหรับ .NET เพิ่มข้อมูลผู้เขียน ประทับเวลา และข้อมูลที่กำหนดเองเพื่อปรับปรุงการตรวจสอบย้อนกลับและความถูกต้องของเอกสาร"
"linktitle": "ลงนามในสเปรดชีตพร้อมข้อมูลเมตา"
"second_title": "API ของ GroupDocs.Signature .NET"
"title": "เพิ่มลายเซ็นข้อมูลเมตาลงในสเปรดชีต Excel ใน C# .NET"
"url": "/th/net/document-signing/sign-spreadsheet-with-metadata/"
"weight": 13
---

## การแนะนำ

สเปรดชีต Excel มักประกอบด้วยข้อมูลทางธุรกิจที่สำคัญ ข้อมูลทางการเงิน และการคำนวณที่สำคัญ การตรวจสอบความถูกต้อง การติดตามแหล่งที่มา และการปกป้องความสมบูรณ์ของข้อมูลเป็นสิ่งสำคัญอย่างยิ่งในสภาพแวดล้อมการทำงานที่หลากหลาย แนวทางหนึ่งที่มีประสิทธิภาพในการเพิ่มความปลอดภัยและความสามารถในการตรวจสอบย้อนกลับของสเปรดชีตคือการฝังลายเซ็นเมตาเดตา

บทช่วยสอนที่ครอบคลุมนี้จะแนะนำคุณตลอดกระบวนการลงนามในสเปรดชีต Excel ด้วยข้อมูลเมตาโดยใช้ GroupDocs.Signature สำหรับ .NET การเพิ่มลายเซ็นข้อมูลเมตาช่วยให้คุณสามารถฝังข้อมูลสำคัญ เช่น รายละเอียดผู้เขียน ตราประทับเวลาที่สร้าง รหัสประจำตัวเอกสาร และคุณสมบัติแบบกำหนดเองอื่นๆ ลงในโครงสร้างไฟล์สเปรดชีตได้โดยตรง

## ข้อกำหนดเบื้องต้น

ก่อนที่จะดำเนินการตามบทช่วยสอนนี้ โปรดแน่ใจว่าคุณมีสิ่งต่อไปนี้:

1. [GroupDocs.Signature สำหรับ .NET](https://releases.groupdocs.com/signature/net/) - ดาวน์โหลดและติดตั้งไลบรารี
2. สภาพแวดล้อมการพัฒนา - Visual Studio หรือ IDE อื่นๆ ที่เข้ากันได้กับ .NET
3. Excel Spreadsheet - ไฟล์ตัวอย่างสเปรดชีต (XLSX, XLS เป็นต้น)
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

กำหนดเส้นทางสำหรับสเปรดชีตแหล่งที่มาของคุณและตำแหน่งที่จะบันทึกเอาต์พุตที่ลงนาม:

```csharp
// ระบุเส้นทางไปยังไฟล์ Excel ของคุณ
string filePath = "sample.xlsx";

// กำหนดไดเรกทอรีเอาต์พุตและชื่อไฟล์สำหรับสเปรดชีตที่ลงนาม
string outputDirectory = "Your Document Directory";
string outputFilePath = Path.Combine(outputDirectory, "SignSpreadsheetWithMetadata", "SignedWithMetadata.xlsx");

// ตรวจสอบให้แน่ใจว่ามีไดเร็กทอรีเอาท์พุตอยู่
Directory.CreateDirectory(Path.GetDirectoryName(outputFilePath));
```

## ขั้นตอนที่ 2: เริ่มต้นวัตถุลายเซ็น

สร้างอินสแตนซ์ของคลาส Signature ด้วยไฟล์สเปรดชีตต้นฉบับของคุณ:

```csharp
using (Signature signature = new Signature(filePath))
{
    // ส่วนที่เหลือของโค้ดจะอยู่ที่นี่
}
```

## ขั้นตอนที่ 3: สร้างและกำหนดค่าลายเซ็นข้อมูลเมตา

ขั้นตอนต่อไป กำหนดตัวเลือกเมตาข้อมูลและสร้างอาร์เรย์ของลายเซ็นเมตาข้อมูลของสเปรดชีต:

```csharp
// สร้างวัตถุตัวเลือกเมตาข้อมูล
MetadataSignOptions options = new MetadataSignOptions();

// สร้างอาร์เรย์ของลายเซ็นข้อมูลเมตาของสเปรดชีตที่มีประเภทข้อมูลที่แตกต่างกัน
SpreadsheetMetadataSignature[] signatures = new SpreadsheetMetadataSignature[]
{
    new SpreadsheetMetadataSignature("Author", "Mr.Sherlock Holmes"), // ค่าสตริง
    new SpreadsheetMetadataSignature("CreatedOn", DateTime.Now),      // ค่าวันที่และเวลา
    new SpreadsheetMetadataSignature("DocumentId", 123456),           // ค่าจำนวนเต็ม
    new SpreadsheetMetadataSignature("SignatureId", 123.456D),        // ค่าสองเท่า
    new SpreadsheetMetadataSignature("Amount", 123.456M),             // ค่าทศนิยม
    new SpreadsheetMetadataSignature("Total", 123.456F)               // ค่าลอยตัว
};

// เพิ่มคอลเลกชันลายเซ็นให้กับตัวเลือก
options.Signatures.AddRange(signatures);
```

## ขั้นตอนที่ 4: ลงนามในสเปรดชีตด้วยข้อมูลเมตา

ใช้ลายเซ็นข้อมูลเมตาลงในสเปรดชีตและบันทึกผลลัพธ์:

```csharp
// ลงนามในเอกสารและบันทึกลงในเส้นทางไฟล์เอาต์พุต
SignResult result = signature.Sign(outputFilePath, options);

// แสดงข้อความแสดงความสำเร็จ
Console.WriteLine($"\nSource spreadsheet signed successfully with {result.Succeeded.Count} metadata signature(s).");
Console.WriteLine($"Signed spreadsheet saved at: {outputFilePath}");
```

## ตัวอย่างที่สมบูรณ์

นี่คือตัวอย่างโค้ดที่สมบูรณ์ซึ่งรวบรวมขั้นตอนทั้งหมดเข้าด้วยกัน:

```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;

namespace SignSpreadsheetWithMetadataExample
{
    class Program
    {
        static void Main(string[] args)
        {
            // ระบุเส้นทางไฟล์
            string filePath = "sample.xlsx";
            string outputFilePath = Path.Combine("Your Document Directory", "SignSpreadsheetWithMetadata", "SignedWithMetadata.xlsx");
            
            // ตรวจสอบให้แน่ใจว่ามีไดเร็กทอรีเอาท์พุตอยู่
            Directory.CreateDirectory(Path.GetDirectoryName(outputFilePath));

            // ลงนามในสเปรดชีตด้วยข้อมูลเมตา
            using (Signature signature = new Signature(filePath))
            {
                // สร้างวัตถุตัวเลือกเมตาข้อมูล
                MetadataSignOptions options = new MetadataSignOptions();
                
                // สร้างอาร์เรย์ของลายเซ็นข้อมูลเมตาของสเปรดชีตที่มีประเภทข้อมูลที่แตกต่างกัน
                SpreadsheetMetadataSignature[] signatures = new SpreadsheetMetadataSignature[]
                {
                    new SpreadsheetMetadataSignature("Author", "Mr.Sherlock Holmes"), // ค่าสตริง
                    new SpreadsheetMetadataSignature("CreatedOn", DateTime.Now),      // ค่าวันที่และเวลา
                    new SpreadsheetMetadataSignature("DocumentId", 123456),           // ค่าจำนวนเต็ม
                    new SpreadsheetMetadataSignature("SignatureId", 123.456D),        // ค่าสองเท่า
                    new SpreadsheetMetadataSignature("Amount", 123.456M),             // ค่าทศนิยม
                    new SpreadsheetMetadataSignature("Total", 123.456F)               // ค่าลอยตัว
                };
                
                // เพิ่มคอลเลกชันลายเซ็นให้กับตัวเลือก
                options.Signatures.AddRange(signatures);
                
                // ลงนามเอกสารและบันทึกลงในไฟล์
                SignResult result = signature.Sign(outputFilePath, options);
                
                // แสดงผลลัพธ์
                Console.WriteLine($"\nSource spreadsheet signed successfully with {result.Succeeded.Count} signature(s).");
                Console.WriteLine($"File saved at {outputFilePath}.");
            }
        }
    }
}
```

## เทคนิคเมตาดาต้าสเปรดชีตขั้นสูง

### การทำงานกับคุณสมบัติสเปรดชีตแบบกำหนดเองและแบบในตัว

สเปรดชีต Excel มีทั้งคุณสมบัติในตัวและคุณสมบัติแบบกำหนดเอง ซึ่งสามารถเข้าถึงได้ผ่านกล่องโต้ตอบคุณสมบัติไฟล์ GroupDocs.Signature ช่วยให้คุณทำงานกับทั้งสองอย่าง:

```csharp
// เพิ่มคุณสมบัติในตัว
signatures = new SpreadsheetMetadataSignature[]
{
    new SpreadsheetMetadataSignature("Company", "Sherlock Holmes Consulting"),
    new SpreadsheetMetadataSignature("Category", "Financial"),
    new SpreadsheetMetadataSignature("Keywords", "budget,forecast,analysis"),
    new SpreadsheetMetadataSignature("Comments", "This spreadsheet contains confidential information"),
    new SpreadsheetMetadataSignature("Manager", "John Watson")
};
options.Signatures.AddRange(signatures);

// เพิ่มคุณสมบัติที่กำหนดเอง
options.Signatures.Add(new SpreadsheetMetadataSignature("Department", "Finance"));
options.Signatures.Add(new SpreadsheetMetadataSignature("SecurityLevel", "Confidential"));
```

### การค้นหาข้อมูลเมตาในสเปรดชีตที่ลงนาม

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

คุณสามารถอัปเดตข้อมูลเมตาที่มีอยู่ในสเปรดชีตได้โดยใช้ชื่อคุณสมบัติเดียวกัน:

```csharp
// อัปเดตข้อมูลเมตาที่มีอยู่
options.Signatures.Add(new SpreadsheetMetadataSignature("Author", "Updated Author Name"));
```

## บทสรุป

ในบทช่วยสอนที่ครอบคลุมนี้ คุณจะได้เรียนรู้วิธีการลงนามในสเปรดชีต Excel ด้วยข้อมูลเมตาโดยใช้ GroupDocs.Signature สำหรับ .NET การฝังข้อมูลเมตาลงในไฟล์สเปรดชีตช่วยเพิ่มความสามารถในการติดตามเอกสาร ให้บริบทที่มีคุณค่า และช่วยยืนยันความถูกต้อง

ลายเซ็นเมตาดาต้าในสเปรดชีตมีประโยชน์อย่างยิ่งในสภาพแวดล้อมทางธุรกิจที่แหล่งที่มาของเอกสาร ผู้เขียน และการติดตามเวอร์ชันมีความสำคัญ เมตาดาต้าที่ฝังไว้สามารถประกอบด้วยข้อมูลเกี่ยวกับผู้เขียน เวลาที่สร้าง รหัสประจำตัวเอกสาร และคุณสมบัติแบบกำหนดเองที่เกี่ยวข้องกับความต้องการขององค์กรของคุณ

การนำลายเซ็นเมตาข้อมูลมาใช้กับ GroupDocs.Signature จะช่วยให้คุณมั่นใจได้ว่าสเปรดชีต Excel ของคุณยังคงความสมบูรณ์และให้ข้อมูลที่ตรวจสอบได้ตลอดวงจรชีวิต

## คำถามที่พบบ่อย

### ฉันสามารถเพิ่มข้อมูลเมตาลงในสเปรดชีตที่มีคุณสมบัติบางอย่างที่กำหนดไว้แล้วได้หรือไม่

ใช่ คุณสามารถเพิ่มเมตาดาต้าใหม่หรืออัปเดตเมตาดาต้าที่มีอยู่ในสเปรดชีตได้ GroupDocs.Signature จะจัดการการผสานรวม ไม่ว่าจะโดยการเพิ่มคุณสมบัติใหม่หรืออัปเดตคุณสมบัติที่มีอยู่แล้วด้วยชื่อเดียวกัน

### รูปแบบสเปรดชีตใดบ้างที่รองรับการลงนามเมตาเดตา?

GroupDocs.Signature สำหรับ .NET รองรับการลงนามเมตาดาต้าสำหรับรูปแบบสเปรดชีตต่างๆ รวมถึง XLSX, XLS, XLSM, ODS และอื่นๆ สำหรับรายการทั้งหมด โปรดดูที่ [เอกสารอย่างเป็นทางการ](https://docs-groupdocs.com/signature/net/).

### ลายเซ็นเมตาข้อมูลในสเปรดชีตจะมองเห็นได้โดยผู้ใช้หรือไม่

ลายเซ็นเมตาดาต้าจะไม่ปรากฏในเนื้อหาของสเปรดชีต อย่างไรก็ตาม สามารถดูได้ผ่านแผงคุณสมบัติเอกสารใน Excel หรือแอปพลิเคชันอื่นๆ ที่เข้ากันได้

### ฉันสามารถตรวจสอบด้วยโปรแกรมได้หรือไม่ว่าสเปรดชีตถูกเปลี่ยนแปลงหรือไม่หลังจากเพิ่มข้อมูลเมตาแล้ว

ใช่ GroupDocs.Signature มีความสามารถในการตรวจสอบที่ช่วยตรวจจับว่าเอกสารได้รับการแก้ไขหรือไม่หลังจากการลงนาม รวมถึงการเปลี่ยนแปลงข้อมูลเมตา

### การเพิ่มข้อมูลเมตาจะส่งผลต่อการทำงานของสเปรดชีตหรือไม่

การเพิ่มเมตาดาต้ามีผลกระทบต่อขนาดไฟล์เพียงเล็กน้อยและไม่มีผลกระทบต่อฟังก์ชันการทำงานของสเปรดชีต เป็นวิธีง่ายๆ ในการปรับปรุงคุณสมบัติของเอกสารโดยไม่กระทบต่อการคำนวณ สูตร หรือฟีเจอร์อื่นๆ ของ Excel

### ฉันสามารถหาทรัพยากรและการสนับสนุนเพิ่มเติมได้ที่ไหน

- [ข้อมูลอ้างอิง API](https://reference.groupdocs.com/signature/net/)
- [ดาวน์โหลด](https://releases.groupdocs.com/signature/net/)
- [ตัวอย่าง](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
- [เอกสารประกอบ](https://docs.groupdocs.com/signature/net/)
- [หน้าผลิตภัณฑ์](https://products.groupdocs.com/signature/net/)
- [บล็อก](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
- [ฟอรั่มสนับสนุน](https://forum.groupdocs.com/c/signature/13)
- [ใบอนุญาตชั่วคราว](https://purchase.groupdocs.com/temporary-license/)