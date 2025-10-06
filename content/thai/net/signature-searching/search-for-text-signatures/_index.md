---
"description": "เรียนรู้วิธีค้นหาลายเซ็นข้อความในเอกสารอย่างมีประสิทธิภาพโดยใช้ GroupDocs.Signature สำหรับ .NET ด้วยคำแนะนำทีละขั้นตอนที่ครอบคลุมและตัวอย่างโค้ดของเรา"
"linktitle": "ค้นหาลายเซ็นข้อความ"
"second_title": "API ของ GroupDocs.Signature .NET"
"title": "ค้นหาลายเซ็นข้อความในเอกสาร"
"url": "/th/net/signature-searching/search-for-text-signatures/"
"weight": 16
type: docs
---
## การแนะนำ

ลายเซ็นข้อความเป็นวิธีการทั่วไปในการระบุผู้แต่ง การอนุมัติ หรือการตรวจสอบเอกสาร ในการจัดการเอกสารดิจิทัล ความสามารถในการค้นหาและดึงลายเซ็นข้อความผ่านโปรแกรมเป็นสิ่งสำคัญอย่างยิ่งสำหรับการตรวจสอบความถูกต้องของเอกสาร การทำงานอัตโนมัติ และการตรวจสอบการปฏิบัติตามข้อกำหนด GroupDocs.Signature for .NET นำเสนอโซลูชันที่ครอบคลุมสำหรับการนำฟังก์ชันการค้นหาลายเซ็นข้อความไปใช้ในแอปพลิเคชัน .NET ของคุณ รองรับรูปแบบเอกสารที่หลากหลายและความสามารถในการค้นหาขั้นสูง

บทช่วยสอนนี้จะแนะนำคุณเกี่ยวกับกระบวนการค้นหาลายเซ็นข้อความในเอกสารโดยใช้ GroupDocs.Signature สำหรับ .NET พร้อมทั้งมีคำอธิบายโดยละเอียด คำแนะนำทีละขั้นตอน และตัวอย่างโค้ดในทางปฏิบัติ

## ข้อกำหนดเบื้องต้น

ก่อนที่จะดำเนินการค้นหาลายเซ็นข้อความ ให้แน่ใจว่าคุณมีข้อกำหนดเบื้องต้นดังต่อไปนี้:

1. GroupDocs.Signature สำหรับไลบรารี .NET: ดาวน์โหลดและติดตั้งไลบรารีจาก [หน้าเผยแพร่](https://releases-groupdocs.com/signature/net/).

2. สภาพแวดล้อมการพัฒนา: ตั้งค่าสภาพแวดล้อมการพัฒนาที่เหมาะสม เช่น Visual Studio หรือ IDE ที่เข้ากันได้ที่รองรับ .NET

3. เอกสารตัวอย่าง: เตรียมเอกสารทดสอบที่มีลายเซ็นข้อความเพื่อการตรวจสอบและการทดสอบ

4. ความรู้พื้นฐานเกี่ยวกับ C#: ความคุ้นเคยกับภาษาการเขียนโปรแกรม C# และแนวคิดของกรอบงาน .NET

## นำเข้าเนมสเปซ

เริ่มต้นด้วยการนำเข้าเนมสเปซที่จำเป็นเพื่อเข้าถึงฟังก์ชันการทำงานของ GroupDocs.Signature:

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

ตอนนี้มาแบ่งกระบวนการค้นหาลายเซ็นข้อความออกเป็นขั้นตอนที่ชัดเจนและจัดการได้:

## ขั้นตอนที่ 1: โหลดเอกสาร

ขั้นแรก ให้กำหนดเส้นทางเอกสารและเริ่มต้นใช้งาน `Signature` วัตถุ:

```csharp
string filePath = "sample_multiple_signatures.docx";
string fileName = Path.GetFileName(filePath);

using (Signature signature = new Signature(filePath))
{
    // จะเพิ่มรหัสค้นหาลายเซ็นข้อความไว้ที่นี่
}
```

## ขั้นตอนที่ 2: กำหนดค่าตัวเลือกการค้นหา

สร้างและกำหนดค่า `TextSearchOptions` เพื่อระบุวิธีการค้นหาลายเซ็นข้อความ:

```csharp
// กำหนดค่าตัวเลือกการค้นหาข้อความ
TextSearchOptions options = new TextSearchOptions
{
    // ค้นหาในทุกหน้า
    AllPages = true,
    
    // ตัวเลือก: ระบุข้อความที่ต้องการจับคู่
    // ข้อความ = "อนุมัติ"
    
    // ตัวเลือก: ระบุประเภทการจับคู่
    // MatchType = TextMatchType.ประกอบด้วย
};
```

## ขั้นตอนที่ 3: ดำเนินการค้นหาลายเซ็นข้อความ

ดำเนินการค้นหาโดยใช้ตัวเลือกที่กำหนดค่าไว้:

```csharp
// ค้นหาลายเซ็นข้อความ
List<TextSignature> signatures = signature.Search<TextSignature>(options);
```

## ขั้นตอนที่ 4: ประมวลผลและแสดงผลลัพธ์

ทำซ้ำผ่านลายเซ็นข้อความที่พบและแสดงรายละเอียด:

```csharp
// แสดงผลการค้นหา
Console.WriteLine($"\nSource document '{fileName}' contains {signatures.Count} text signature(s):");

foreach (TextSignature textSignature in signatures)
{
    Console.WriteLine($"Text signature found at page {textSignature.PageNumber} with text '{textSignature.Text}'");
    Console.WriteLine($"Location: X={textSignature.Left}, Y={textSignature.Top}, Width={textSignature.Width}, Height={textSignature.Height}");
    Console.WriteLine($"Signature type: {textSignature.SignatureImplementation}");
    Console.WriteLine();
}
```

## ตัวอย่างที่สมบูรณ์

นี่คือตัวอย่างการทำงานที่สมบูรณ์ซึ่งสาธิตวิธีการค้นหาลายเซ็นข้อความในเอกสาร:

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;

namespace TextSignatureSearch
{
    class Program
    {
        static void Main(string[] args)
        {
            // เส้นทางเอกสาร - อัปเดตด้วยเส้นทางไฟล์ของคุณ
            string filePath = "sample_multiple_signatures.docx";
            string fileName = Path.GetFileName(filePath);
            
            // เริ่มต้นอินสแตนซ์ลายเซ็น
            using (Signature signature = new Signature(filePath))
            {
                try
                {
                    // กำหนดค่าตัวเลือกการค้นหาข้อความ
                    TextSearchOptions options = new TextSearchOptions
                    {
                        // ค้นหาในทุกหน้า
                        AllPages = true
                    };
                    
                    // ค้นหาลายเซ็นข้อความ
                    List<TextSignature> signatures = signature.Search<TextSignature>(options);
                    
                    // แสดงผลการค้นหา
                    Console.WriteLine($"\nSource document '{fileName}' contains {signatures.Count} text signature(s):");
                    
                    foreach (TextSignature textSignature in signatures)
                    {
                        Console.WriteLine($"Text signature found at page {textSignature.PageNumber} with text '{textSignature.Text}'");
                        Console.WriteLine($"Location: X={textSignature.Left}, Y={textSignature.Top}, Width={textSignature.Width}, Height={textSignature.Height}");
                        Console.WriteLine($"Signature type: {textSignature.SignatureImplementation}");
                        Console.WriteLine();
                    }
                }
                catch (Exception ex)
                {
                    Console.WriteLine($"Error occurred: {ex.Message}");
                }
            }
            
            Console.WriteLine("Press any key to exit...");
            Console.ReadKey();
        }
    }
}
```

## เทคนิคการค้นหาลายเซ็นข้อความขั้นสูง

### การค้นหาด้วยเกณฑ์ข้อความเฉพาะ

สำหรับการค้นหาที่ตรงเป้าหมายมากขึ้น คุณสามารถปรับแต่งได้ `TextSearchOptions` เพื่อกรองตามเนื้อหาข้อความที่เฉพาะเจาะจง:

```csharp
// สร้างตัวเลือกการค้นหาด้วยเกณฑ์ข้อความที่เฉพาะเจาะจง
TextSearchOptions options = new TextSearchOptions
{
    // ค้นหาในทุกหน้า
    AllPages = true,
    
    // ค้นหาข้อความเฉพาะ
    Text = "Approved",
    
    // ระบุประเภทการจับคู่ (ประกอบด้วย, ตรงกัน, เริ่มต้นด้วย, สิ้นสุดด้วย)
    MatchType = TextMatchType.Contains,
    
    // การค้นหาแบบแยกแยะตัวพิมพ์ใหญ่-เล็ก
    MatchCase = true
};
```

### การค้นหาในพื้นที่เอกสารเฉพาะ

คุณสามารถจำกัดการค้นหาให้เฉพาะพื้นที่เฉพาะของเอกสารได้:

```csharp
// สร้างตัวเลือกการค้นหาสำหรับพื้นที่เอกสารเฉพาะ
TextSearchOptions options = new TextSearchOptions
{
    // ค้นหาเฉพาะหน้าที่ระบุเท่านั้น
    AllPages = false,
    PageNumber = 1,
    
    // หรือระบุหลายหน้า
    PagesSetup = new PagesSetup { Pages = new List<int> { 1, 3, 5 } },
    
    // กำหนดพื้นที่เฉพาะที่จะค้นหาภายใน
    Rectangle = new Rectangle(100, 100, 400, 200)
};
```

### การกรองข้อความขั้นสูง

นำตรรกะการกรองแบบกำหนดเองมาใช้กับข้อกำหนดการค้นหาที่ซับซ้อนยิ่งขึ้น:

```csharp
// สร้างตัวเลือกการค้นหาด้วยการประมวลผลแบบกำหนดเอง
TextSearchOptions options = new TextSearchOptions
{
    AllPages = true,
    
    // กำหนดการประมวลผลแบบกำหนดเองโดยใช้ตัวแทน
    ProcessCompleted = (TextSignature signature) =>
    {
        // ตรรกะการตรวจสอบแบบกำหนดเอง
        bool isValid = signature.Text.Length > 5 && 
                      (signature.Text.Contains("Approved") || signature.Text.Contains("Verified"));
        
        return isValid;
    }
};
```

### การค้นหารูปแบบข้อความที่แตกต่างกัน

ใช้คุณสมบัติแบบอักษรและรูปแบบเพื่อกรองลายเซ็นข้อความ:

```csharp
// สร้างตัวเลือกการค้นหาที่กำหนดเป้าหมายการปรากฏข้อความที่เฉพาะเจาะจง
TextSearchOptions options = new TextSearchOptions
{
    // กรองตามชื่อแบบอักษร
    FontName = "Arial",
    
    // กรองตามช่วงขนาดตัวอักษร
    MinFontSize = 10,
    MaxFontSize = 14,
    
    // กรองตามสีตัวอักษร
    ForeColor = System.Drawing.Color.Blue
};
```

### การแยกข้อมูลเมตาของลายเซ็น

แยกและประมวลผลข้อมูลเมตาที่เกี่ยวข้องกับลายเซ็นข้อความ:

```csharp
foreach (TextSignature signature in signatures)
{
    // การเข้าถึงข้อมูลเมตาลายเซ็น
    if (signature.Metadata != null && signature.Metadata.Count > 0)
    {
        Console.WriteLine("Signature Metadata:");
        
        foreach (var item in signature.Metadata)
        {
            Console.WriteLine($"  {item.Key}: {item.Value}");
        }
    }
    
    // ตรวจสอบวันที่สร้างและแก้ไขลายเซ็น
    if (signature.CreatedOn.HasValue)
    {
        Console.WriteLine($"Created on: {signature.CreatedOn.Value}");
    }
    
    if (signature.ModifiedOn.HasValue)
    {
        Console.WriteLine($"Modified on: {signature.ModifiedOn.Value}");
    }
}
```

## บทสรุป

ในคู่มือฉบับสมบูรณ์นี้ เราได้สำรวจวิธีการค้นหาลายเซ็นข้อความในเอกสารโดยใช้ GroupDocs.Signature สำหรับ .NET ตั้งแต่การค้นหาขั้นพื้นฐานไปจนถึงเทคนิคขั้นสูง ตอนนี้คุณมีความรู้ในการนำฟังก์ชันลายเซ็นข้อความที่มีประสิทธิภาพไปใช้ในแอปพลิเคชัน .NET ของคุณแล้ว

GroupDocs.Signature มอบกรอบงานอันทรงพลังและยืดหยุ่นสำหรับการทำงานกับลายเซ็นข้อความ ช่วยให้คุณสร้างระบบการตรวจสอบเอกสารที่ซับซ้อน โซลูชันเวิร์กโฟลว์อัตโนมัติ และเครื่องมือตรวจสอบการปฏิบัติตามข้อกำหนด

## คำถามที่พบบ่อย

### ฉันสามารถค้นหาลายเซ็นข้อความในเอกสารที่ป้องกันด้วยรหัสผ่านได้หรือไม่

ใช่ GroupDocs.Signature รองรับการค้นหาลายเซ็นข้อความในเอกสารที่ป้องกันด้วยรหัสผ่าน คุณสามารถระบุรหัสผ่านเมื่อเริ่มต้นใช้งาน `Signature` วัตถุ:

```csharp
LoadOptions loadOptions = new LoadOptions { Password = "your_password" };
using (Signature signature = new Signature(filePath, loadOptions))
{
    // ค้นหาลายเซ็นข้อความ
}
```

### รูปแบบเอกสารใดบ้างที่รองรับการค้นหาลายเซ็นข้อความ?

GroupDocs.Signature รองรับรูปแบบเอกสารที่หลากหลาย รวมถึง PDF, เอกสาร Microsoft Office (Word, Excel, PowerPoint), รูปแบบ OpenOffice, รูปภาพ และอื่นๆ อีกมากมาย

### ฉันสามารถค้นหาลายเซ็นข้อความที่มีการจัดรูปแบบเฉพาะ เช่น ตัวหนา หรือ ตัวเอียง ได้หรือไม่

ใช่ คุณสามารถค้นหาลายเซ็นข้อความที่มีการจัดรูปแบบเฉพาะได้โดยใช้ `FontBold` และ `FontItalic` คุณสมบัติใน `TextSearchOptions`-

```csharp
TextSearchOptions options = new TextSearchOptions
{
    FontBold = true,
    FontItalic = true
};
```

### ฉันจะปรับปรุงประสิทธิภาพการค้นหาเอกสารขนาดใหญ่ได้อย่างไร

สำหรับเอกสารขนาดใหญ่ คุณสามารถเพิ่มประสิทธิภาพการค้นหาได้โดย:

1. จำกัดการค้นหาให้เฉพาะหน้าที่ระบุแทนที่จะค้นหาทั้งเอกสาร
2. การใช้เกณฑ์การค้นหาที่เฉพาะเจาะจงมากขึ้นเพื่อลดจำนวนการจับคู่
3. การระบุพื้นที่ค้นหาโดยใช้ `Rectangle` ทรัพย์สินหากคุณรู้ว่าลายเซ็นมักอยู่ที่ไหน
4. การนำการแบ่งหน้าไปใช้ในแอปพลิเคชันของคุณเพื่อประมวลผลผลการค้นหาเป็นชุด

### ฉันสามารถตรวจจับได้หรือไม่ว่ามีการเพิ่มลายเซ็นข้อความทางอิเล็กทรอนิกส์หรือเป็นส่วนหนึ่งของเนื้อหาเอกสารต้นฉบับหรือไม่

GroupDocs.Signature สามารถแยกแยะความแตกต่างระหว่างองค์ประกอบข้อความประเภทต่างๆ ในเอกสารได้ `SignatureImplementation` ทรัพย์สินของ `TextSignature` ระบุว่าข้อความนั้นเป็นลายเซ็นอย่างเป็นทางการหรือเนื้อหาเอกสารทั่วไป อย่างไรก็ตาม การตัดสินใจขั้นสุดท้ายอาจขึ้นอยู่กับวิธีการเพิ่มข้อความลงในเอกสารเดิม

## ดูเพิ่มเติม

* [ข้อมูลอ้างอิง API](https://reference.groupdocs.com/signature/net/)
* [ตัวอย่างโค้ดบน GitHub](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
* [เอกสารประกอบผลิตภัณฑ์](https://docs.groupdocs.com/signature/net/)
* [หน้าผลิตภัณฑ์](https://products.groupdocs.com/signature/net/)
* [ดาวน์โหลดเวอร์ชันล่าสุด](https://releases.groupdocs.com/signature/net/)
* [บทความบล็อก](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
* [ฟอรั่มสนับสนุนฟรี](https://forum.groupdocs.com/c/signature/13)
* [ใบอนุญาตชั่วคราว](https://purchase.groupdocs.com/temporary-license/)