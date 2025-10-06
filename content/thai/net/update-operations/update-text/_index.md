---
"description": "เรียนรู้วิธีอัปเดตลายเซ็นข้อความในรูปแบบเอกสารต่างๆ อย่างมีประสิทธิภาพด้วย GroupDocs.Signature สำหรับ .NET รับรองความถูกต้องของเอกสารอย่างมืออาชีพด้วยบทช่วยสอนที่ครอบคลุมนี้"
"linktitle": "อัปเดตข้อความ"
"second_title": "API ของ GroupDocs.Signature .NET"
"title": "อัปเดตลายเซ็นข้อความในเอกสาร"
"url": "/th/net/update-operations/update-text/"
"weight": 13
type: docs
---
## การแนะนำ
GroupDocs.Signature สำหรับ .NET คือโซลูชันการลงนามในเอกสารที่ครอบคลุม ช่วยให้นักพัฒนาสามารถผสานรวมฟังก์ชันลายเซ็นอันทรงพลังเข้ากับแอปพลิเคชัน .NET ของพวกเขาได้ ด้วยไลบรารีอเนกประสงค์นี้ คุณสามารถเพิ่ม ค้นหา ตรวจสอบ และอัปเดตลายเซ็นประเภทต่างๆ ได้อย่างง่ายดาย รวมถึงลายเซ็นข้อความ ในรูปแบบเอกสารที่หลากหลาย บทช่วยสอนนี้มุ่งเน้นที่การอัปเดตลายเซ็นข้อความในเอกสารโดยเฉพาะ พร้อมให้คำแนะนำทีละขั้นตอนเพื่อการใช้งานที่ราบรื่น

## ข้อกำหนดเบื้องต้น
ก่อนที่จะดำเนินการอัปเดตลายเซ็นข้อความด้วย GroupDocs.Signature สำหรับ .NET ตรวจสอบให้แน่ใจว่าคุณมีข้อกำหนดเบื้องต้นดังต่อไปนี้:

1. Visual Studio: ติดตั้ง Visual Studio IDE เวอร์ชันล่าสุดบนระบบของคุณ
2. GroupDocs.Signature สำหรับ .NET: ดาวน์โหลดและติดตั้งไลบรารี GroupDocs.Signature สำหรับ .NET จาก [หน้าดาวน์โหลด](https://releases-groupdocs.com/signature/net/).
3. .NET Framework หรือ .NET Core: ตรวจสอบให้แน่ใจว่าคุณได้ติดตั้ง .NET Framework หรือ .NET Core ไว้ในเครื่องพัฒนาของคุณแล้ว
4. ความรู้พื้นฐานเกี่ยวกับ C#: ความคุ้นเคยกับพื้นฐานการเขียนโปรแกรม C#

## นำเข้าเนมสเปซ
ก่อนที่คุณจะเริ่มอัปเดตลายเซ็นข้อความในเอกสาร คุณต้องนำเข้าเนมสเปซที่จำเป็นเข้าสู่โปรเจ็กต์ของคุณก่อน เนมสเปซเหล่านี้ให้สิทธิ์เข้าถึงคลาสและเมธอด GroupDocs.Signature

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

## ขั้นตอนที่ 1: ตั้งค่าเส้นทางเอกสาร
ขั้นแรก ให้กำหนดเส้นทางไปยังเอกสารที่มีลายเซ็นข้อความที่คุณต้องการอัปเดต

```csharp
string filePath = "sample_multiple_signatures.docx";
```

บรรทัดนี้ระบุเส้นทางไปยังเอกสารต้นฉบับของคุณ แทนที่ `"sample_multiple_signatures.docx"` พร้อมเส้นทางจริงไปยังเอกสารของคุณ

## ขั้นตอนที่ 2: คัดลอกเอกสาร
ตั้งแต่ `Update` วิธีการนี้ใช้ได้กับเอกสารเดียวกัน ดังนั้นจึงถือเป็นแนวทางปฏิบัติที่ดีที่จะสร้างสำเนาสำรองของเอกสารต้นฉบับของคุณ

```csharp
string fileName = Path.GetFileName(filePath);
string outputFilePath = Path.Combine("Your Document Directory", "UpdateText", fileName);
File.Copy(filePath, outputFilePath, true);
```

โค้ดสั้นๆ นี้จะสร้างสำเนาเอกสารต้นฉบับของคุณในไดเร็กทอรีที่ระบุ แทนที่ `"Your Document Directory"` พร้อมเส้นทางจริงที่คุณต้องการบันทึกเอกสารอัพเดต

## ขั้นตอนที่ 3: เริ่มต้นวัตถุลายเซ็น
ตอนนี้เริ่มต้น `Signature` วัตถุที่มีเส้นทางไปยังสำเนาเอกสารของคุณ

```csharp
using (Signature signature = new Signature(outputFilePath))
{
    // รหัสของคุณที่นี่
}
```

การ `Signature` คลาสเป็นจุดเข้าหลักสำหรับฟังก์ชัน GroupDocs.Signature `using` คำชี้แจงเพื่อให้แน่ใจว่าทรัพยากรได้รับการกำจัดอย่างถูกต้องหลังการใช้งาน

## ขั้นตอนที่ 4: ค้นหาลายเซ็นข้อความ
ก่อนที่จะอัปเดตลายเซ็นข้อความ คุณต้องค้นหาลายเซ็นนั้นในเอกสารเสียก่อน

```csharp
TextSearchOptions options = new TextSearchOptions();
List<TextSignature> signatures = signature.Search<TextSignature>(options);
```

โค้ดนี้จะค้นหาลายเซ็นข้อความทั้งหมดในเอกสารโดยใช้ตัวเลือกการค้นหาเริ่มต้น คุณสามารถปรับแต่งการค้นหาได้โดยการกำหนดค่าคุณสมบัติเพิ่มเติมของ `TextSearchOptions` ระดับ.

## ขั้นตอนที่ 5: อัปเดตลายเซ็นข้อความ
เมื่อคุณพบลายเซ็นข้อความแล้ว คุณสามารถเลือกลายเซ็นหนึ่งรายการและอัปเดตคุณสมบัติได้

```csharp
if (signatures.Count > 0)
{
    TextSignature textSignature = signatures[0];
    textSignature.Text = "John Walkman";
    textSignature.Left = textSignature.Left + 10;
    textSignature.Top = textSignature.Top + 10;
    textSignature.Width = 200;
    textSignature.Height = 100;
    bool result = signature.Update(textSignature);
    if (result)
    {
        Console.WriteLine($"Signature with Text '{textSignature.Text}' was updated in the document ['{fileName}'].");
    }
    else
    {
        Console.WriteLine($"Signature was not updated in the document! Signature with Text '{textSignature.Text}' was not found!");
    }
}
```

โค้ดนี้:
1. ตรวจสอบว่าพบลายเซ็นข้อความใด ๆ หรือไม่
2. รับลายเซ็นแรกจากรายการ
3. แก้ไขเนื้อหาข้อความ ตำแหน่ง (ซ้าย, บน) และขนาด (กว้าง, สูง)
4. เรียกหา `Update` วิธีการใช้การเปลี่ยนแปลง
5. แสดงข้อความความสำเร็จหรือความล้มเหลวตามผลลัพธ์

## ตัวอย่างที่สมบูรณ์
นี่คือตัวอย่างที่สมบูรณ์ซึ่งสาธิตวิธีการอัปเดตลายเซ็นข้อความในเอกสาร:

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;

namespace UpdateTextSignature
{
    class Program
    {
        static void Main(string[] args)
        {
            // เส้นทางเอกสาร
            string filePath = "sample_multiple_signatures.docx";
            
            // คัดลอกเอกสาร
            string fileName = Path.GetFileName(filePath);
            string outputFilePath = Path.Combine("OutputDirectory", "UpdateText", fileName);
            Directory.CreateDirectory(Path.GetDirectoryName(outputFilePath));
            File.Copy(filePath, outputFilePath, true);
            
            // เริ่มต้นวัตถุลายเซ็น
            using (Signature signature = new Signature(outputFilePath))
            {
                // ค้นหาลายเซ็นข้อความ
                TextSearchOptions options = new TextSearchOptions();
                List<TextSignature> signatures = signature.Search<TextSignature>(options);
                
                // อัปเดตลายเซ็นข้อความ
                if (signatures.Count > 0)
                {
                    TextSignature textSignature = signatures[0];
                    textSignature.Text = "John Walkman";
                    textSignature.Left = textSignature.Left + 10;
                    textSignature.Top = textSignature.Top + 10;
                    textSignature.Width = 200;
                    textSignature.Height = 100;
                    
                    // ใช้การเปลี่ยนแปลง
                    bool result = signature.Update(textSignature);
                    
                    // ตรวจสอบผลลัพธ์
                    if (result)
                    {
                        Console.WriteLine($"Signature with Text '{textSignature.Text}' was updated in the document ['{fileName}'].");
                    }
                    else
                    {
                        Console.WriteLine($"Signature was not updated in the document! Signature with Text '{textSignature.Text}' was not found!");
                    }
                }
                else
                {
                    Console.WriteLine("No text signatures found in the document.");
                }
            }
        }
    }
}
```

## การปรับแต่งลายเซ็นข้อความขั้นสูง
GroupDocs.Signature มีตัวเลือกการปรับแต่งลายเซ็นข้อความที่หลากหลาย คุณสามารถปรับเปลี่ยนคุณสมบัติต่างๆ ได้ เช่น:

- แบบอักษร: เปลี่ยนแบบอักษร ขนาด สไตล์ และสี
- ขอบ: เพิ่มหรือปรับเปลี่ยนรูปแบบและสีของขอบ
- พื้นหลัง: ตั้งค่าสีพื้นหลังหรือความโปร่งใส
- การหมุน: หมุนลายเซ็นข้อความไปยังมุมที่กำหนด
- ความโปร่งใส: ปรับความทึบของลายเซ็น

นี่คือตัวอย่างวิธีการปรับแต่งคุณสมบัติของแบบอักษร:

```csharp
textSignature.ForeColor = System.Drawing.Color.Blue;
textSignature.Font.FontFamily = "Arial";
textSignature.Font.FontSize = 16;
textSignature.Font.Bold = true;
textSignature.Font.Italic = true;
textSignature.Font.Underline = true;
```

## บทสรุป
GroupDocs.Signature สำหรับ .NET มอบโซลูชันที่แข็งแกร่งและยืดหยุ่นสำหรับการอัปเดตลายเซ็นข้อความในเอกสารผ่านโปรแกรม ด้วยการทำตามขั้นตอนที่ระบุไว้ในบทช่วยสอนนี้ นักพัฒนาสามารถผสานรวมฟังก์ชันการอัปเดตลายเซ็นข้อความเข้ากับแอปพลิเคชัน .NET ได้อย่างมีประสิทธิภาพ ซึ่งจะช่วยเพิ่มประสิทธิภาพในการจัดการเอกสารและกระบวนการตรวจสอบสิทธิ์

ด้วยชุดคุณลักษณะที่ครอบคลุมและ API ที่ใช้งานง่าย GroupDocs.Signature ช่วยให้นักพัฒนาสามารถสร้างโซลูชันการลงนามเอกสารที่ซับซ้อนซึ่งตรงตามข้อกำหนดของแอปพลิเคชันธุรกิจสมัยใหม่

## คำถามที่พบบ่อย
### ฉันสามารถอัปเดตลายเซ็นข้อความหลายรายการในเอกสารเดียวได้หรือไม่
ใช่ คุณสามารถอัปเดตลายเซ็นข้อความหลายรายการได้โดยการวนซ้ำผ่านรายการลายเซ็นที่พบและนำการเปลี่ยนแปลงที่จำเป็นไปใช้กับแต่ละรายการทีละรายการ

### GroupDocs.Signature รองรับลายเซ็นประเภทอื่นนอกเหนือจากข้อความหรือไม่
แน่นอน! GroupDocs.Signature รองรับลายเซ็นหลากหลายประเภท ทั้งลายเซ็นรูปภาพ ลายเซ็นดิจิทัล ลายเซ็นบาร์โค้ด ลายเซ็นคิวอาร์โค้ด และลายเซ็นแสตมป์ แต่ละประเภทมีคุณสมบัติและวิธีการสร้าง ค้นหา และอัปเดตที่แตกต่างกัน

### มีเวอร์ชันทดลองใช้สำหรับ GroupDocs.Signature สำหรับ .NET หรือไม่
ใช่ คุณสามารถดาวน์โหลดเวอร์ชันทดลองใช้ฟรีได้จาก [ที่นี่](https://releases.groupdocs.com/) เพื่อประเมินคุณลักษณะของห้องสมุดก่อนตัดสินใจซื้อ

### ฉันสามารถปรับแต่งลักษณะที่ปรากฏของลายเซ็นข้อความได้หรือไม่
ใช่ GroupDocs.Signature มีตัวเลือกการปรับแต่งมากมายสำหรับลายเซ็นข้อความ รวมถึงคุณสมบัติของแบบอักษร (ตระกูล ขนาด สไตล์) สี ขอบ พื้นหลัง การหมุน และความโปร่งใส

### GroupDocs.Signature สำหรับ .NET ทำงานกับรูปแบบเอกสารทั้งหมดหรือไม่
GroupDocs.Signature รองรับไฟล์เอกสารหลากหลายรูปแบบ รวมถึง PDF, Microsoft Office (Word, Excel, PowerPoint), OpenDocument, รูปภาพ และอื่นๆ อีกมากมาย สำหรับรายการทั้งหมด โปรดดูที่ [เอกสารประกอบ](https://docs-groupdocs.com/signature/net/).

### ฉันจะได้รับการสนับสนุนด้านเทคนิคสำหรับ GroupDocs.Signature ได้อย่างไร
คุณสามารถรับการสนับสนุนด้านเทคนิคได้ผ่านช่องทางต่อไปนี้:
- [ฟอรั่ม](https://forum.groupdocs.com/c/signature/13)
- [เอกสารประกอบ](https://docs.groupdocs.com/signature/net/)
- [ข้อมูลอ้างอิง API](https://reference.groupdocs.com/signature/net/)
- [ตัวอย่างบน GitHub](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
- [บล็อก](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)