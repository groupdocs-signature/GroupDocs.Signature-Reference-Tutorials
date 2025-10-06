---
"description": "การตรวจสอบลายเซ็นข้อความระดับปรมาจารย์ในแอปพลิเคชัน .NET ด้วย GroupDocs.Signature คู่มือการใช้งานแบบทีละขั้นตอน พร้อมตัวอย่างโค้ดที่สมบูรณ์และแนวทางปฏิบัติที่ดีที่สุด"
"linktitle": "ตรวจสอบข้อความ"
"second_title": "API ของ GroupDocs.Signature .NET"
"title": "ตรวจสอบลายเซ็นข้อความในเอกสาร"
"url": "/th/net/verify-operations/verify-text/"
"weight": 13
type: docs
---
## การแนะนำ

ลายเซ็นข้อความ ถึงแม้จะเรียบง่ายกว่าลายเซ็นดิจิทัลหรืออิเล็กทรอนิกส์ แต่ก็มีบทบาทสำคัญในการจัดการและการตรวจสอบเอกสาร ไม่ว่าจะเป็นลายน้ำ ข้อความท้ายกระดาษ หรือรูปแบบเนื้อหาเฉพาะ การตรวจสอบการมีอยู่และความสมบูรณ์ของลายเซ็นข้อความถือเป็นส่วนสำคัญของกระบวนการตรวจสอบเอกสาร

GroupDocs.Signature สำหรับ .NET มอบ API อันทรงพลังสำหรับการตรวจสอบลายเซ็นข้อความภายในเอกสารในรูปแบบที่หลากหลาย บทช่วยสอนที่ครอบคลุมนี้จะแนะนำคุณเกี่ยวกับการใช้งานฟังก์ชันการตรวจสอบข้อความในแอปพลิเคชัน .NET ของคุณ เพื่อให้มั่นใจว่าเอกสารของคุณยังคงความสมบูรณ์และความถูกต้อง

## ข้อกำหนดเบื้องต้น

ก่อนที่จะใช้งานฟังก์ชันการตรวจสอบข้อความ ให้แน่ใจว่าคุณมีข้อกำหนดเบื้องต้นดังต่อไปนี้:

1. GroupDocs.Signature สำหรับ .NET: ดาวน์โหลดและติดตั้งไลบรารีจาก [หน้าดาวน์โหลด](https://releases-groupdocs.com/signature/net/).
2. สภาพแวดล้อมการพัฒนา .NET: Visual Studio หรือสภาพแวดล้อมการพัฒนา .NET ที่เข้ากันได้
3. ความรู้พื้นฐาน: ความคุ้นเคยกับการเขียนโปรแกรม C# และแนวคิดของกรอบงาน .NET
4. เอกสารทดสอบ: เอกสารที่มีลายเซ็นข้อความเพื่อวัตถุประสงค์ในการตรวจสอบ

## นำเข้าเนมสเปซที่จำเป็น

เริ่มต้นด้วยการนำเข้าเนมสเปซที่จำเป็นเพื่อเข้าถึงฟังก์ชันการทำงานของ GroupDocs.Signature:

```csharp
using System;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

มาแบ่งกระบวนการยืนยันข้อความออกเป็นขั้นตอนที่ชัดเจนและจัดการได้:

## ขั้นตอนที่ 1: ระบุเส้นทางเอกสาร

```csharp
// เส้นทางไปยังเอกสารที่มีลายเซ็นข้อความ
string filePath = "sample_multiple_signatures.docx";
```

ตรวจสอบให้แน่ใจว่าคุณได้แทนที่เส้นทางตัวอย่างด้วยเส้นทางจริงไปยังเอกสารของคุณที่มีลายเซ็นข้อความ

## ขั้นตอนที่ 2: เริ่มต้นวัตถุลายเซ็น

```csharp
// สร้างอินสแตนซ์ของคลาส Signature โดยส่งเส้นทางเอกสาร
using (Signature signature = new Signature(filePath))
{
    // รหัสยืนยันจะถูกนำมาใช้ที่นี่
}
```

คลาส Signature เป็นจุดเข้าหลักสำหรับการดำเนินการทั้งหมดใน GroupDocs.Signature API

## ขั้นตอนที่ 3: กำหนดค่าตัวเลือกการตรวจสอบข้อความ

```csharp
// กำหนดตัวเลือกการตรวจสอบข้อความ
TextVerifyOptions options = new TextVerifyOptions()
{
    AllPages = true,                               // ตรวจสอบทุกหน้าของเอกสาร
    SignatureImplementation = TextSignatureImplementation.Native,
    Text = "signature",                            // ข้อความที่ต้องตรวจสอบ
    MatchType = TextMatchType.Contains             // ระบุเกณฑ์การจับคู่
};
```

ตัวเลือกการตรวจสอบช่วยให้คุณกำหนดเกณฑ์เฉพาะสำหรับกระบวนการตรวจสอบได้:
- `AllPages`: ตั้งค่าเป็นจริงเพื่อตรวจสอบหน้าเอกสารทั้งหมด
- `SignatureImplementation`: ระบุวิธีการนำข้อความไปใช้ (แบบเนทีฟหรือแบบสติ๊กเกอร์)
- `Text`: เนื้อหาข้อความที่จะจับคู่ภายในเอกสาร
- `MatchType`:วิธีการจับคู่ข้อความ (มี, ชัดเจน, เริ่มต้นด้วย ฯลฯ)

## ขั้นตอนที่ 4: ดำเนินการกระบวนการตรวจสอบ

```csharp
// ดำเนินการตรวจสอบ
VerificationResult result = signature.Verify(options);
```

การดำเนินการนี้จะดำเนินการตรวจสอบตามตัวเลือกที่คุณระบุ

## ขั้นตอนที่ 5: ดำเนินการตรวจสอบผลลัพธ์

```csharp
// ตรวจสอบผลการตรวจสอบและดำเนินการตามนั้น
if (result.IsValid)
{
    Console.WriteLine($"Document {filePath} contains valid text signatures!");
    
    // แสดงข้อมูลเกี่ยวกับลายเซ็นที่ประสบความสำเร็จ
    foreach (TextSignature textSignature in result.Succeeded)
    {
        Console.WriteLine($"\nFound valid text signature:");
        Console.WriteLine($"Text: {textSignature.Text}");
        Console.WriteLine($"Location: Page {textSignature.PageNumber}, {textSignature.Left}x{textSignature.Top}");
    }
}
else
{
    Console.WriteLine($"Document {filePath} failed verification process.");
    Console.WriteLine($"Number of failed signatures: {result.Failed.Count}");
}
```

โค้ดนี้จะตรวจสอบว่าการตรวจสอบสำเร็จหรือไม่ และให้ข้อมูลโดยละเอียดเกี่ยวกับลายเซ็นข้อความที่ได้รับการตรวจสอบ

## ตัวอย่างที่สมบูรณ์

นี่คือตัวอย่างการทำงานที่สมบูรณ์ซึ่งสาธิตการตรวจสอบลายเซ็นข้อความ:

```csharp
using System;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;

namespace GroupDocs.Signature.Examples
{
    class Program
    {
        static void Main(string[] args)
        {
            // เส้นทางเอกสาร
            string filePath = "sample_multiple_signatures.docx";
            
            try
            {
                // เริ่มต้นอินสแตนซ์ลายเซ็น
                using (Signature signature = new Signature(filePath))
                {
                    // ตั้งค่าตัวเลือกการยืนยัน
                    TextVerifyOptions options = new TextVerifyOptions()
                    {
                        AllPages = true,
                        SignatureImplementation = TextSignatureImplementation.Native,
                        Text = "signature",
                        MatchType = TextMatchType.Contains
                    };
                    
                    // ตรวจสอบลายเซ็นเอกสาร
                    VerificationResult result = signature.Verify(options);
                    
                    // ผลการตรวจสอบกระบวนการ
                    if(result.IsValid)
                    {
                        Console.WriteLine($"\nDocument {filePath} was verified successfully!");
                        foreach (TextSignature item in result.Succeeded)
                        {
                            Console.WriteLine($"\nValid signature is found with text: {item.Text}");
                            Console.WriteLine($"Location: Page {item.PageNumber}, position {item.Left}x{item.Top}");
                        }
                    }
                    else
                    {
                        Console.WriteLine($"\nDocument {filePath} failed verification process.");
                    }
                }
            }
            catch (Exception ex)
            {
                Console.WriteLine($"Error: {ex.Message}");
            }
        }
    }
}
```

## สถานการณ์การตรวจสอบขั้นสูง

GroupDocs.Signature มอบตัวเลือกเพิ่มเติมสำหรับสถานการณ์การตรวจสอบที่ซับซ้อนมากขึ้น:

### การใช้นิพจน์ทั่วไปสำหรับการตรวจสอบ

หากต้องการจับคู่รูปแบบที่ยืดหยุ่นยิ่งขึ้น คุณสามารถใช้นิพจน์ทั่วไปได้:

```csharp
TextVerifyOptions options = new TextVerifyOptions()
{
    Text = "Invoice\\s+#\\d{5,6}",  // จับคู่รูปแบบเช่น "ใบแจ้งหนี้ #12345"
    MatchType = TextMatchType.Regex
};
```

### การตรวจสอบข้อความในพื้นที่เอกสารเฉพาะ

คุณสามารถจำกัดการตรวจสอบเฉพาะบางพื้นที่ของเอกสารได้:

```csharp
TextVerifyOptions options = new TextVerifyOptions()
{
    AllPages = false,
    PageNumber = 1,  // ตรวจสอบเฉพาะหน้าแรกเท่านั้น
    
    // กำหนดพื้นที่ที่จะค้นหา (พิกัดเป็นจุด)
    PagesSetup = new PagesSetup() 
    { 
        FirstPage = true,
        LastPage = false,
        OddPages = false,
        EvenPages = false 
    },
    
    // พื้นที่สี่เหลี่ยมผืนผ้าเป็นมิลลิเมตร
    Rectangle = new Rectangle(10, 10, 100, 30),
    
    Text = "Confidential"
};
```

### การตรวจสอบรูปแบบข้อความหลายรายการพร้อมกัน

คุณสามารถสร้างตัวเลือกการตรวจยืนยันหลายรายการเพื่อตรวจสอบรูปแบบข้อความที่แตกต่างกันได้:

```csharp
// สร้างรายการตัวเลือกการตรวจสอบ
List<VerifyOptions> listOptions = new List<VerifyOptions>();

// เพิ่มการยืนยันข้อความแรก
listOptions.Add(new TextVerifyOptions()
{
    Text = "Confidential",
    MatchType = TextMatchType.Exact
});

// เพิ่มการยืนยันข้อความที่สอง
listOptions.Add(new TextVerifyOptions()
{
    Text = "Do not copy",
    MatchType = TextMatchType.Contains
});

// ยืนยันด้วยตัวเลือกหลายตัว
VerificationResult result = signature.Verify(listOptions);
```

### การตรวจสอบข้อความด้วยลักษณะเฉพาะ

คุณยังสามารถตรวจสอบข้อความด้วยลักษณะการจัดรูปแบบเฉพาะได้อีกด้วย:

```csharp
TextVerifyOptions options = new TextVerifyOptions()
{
    Text = "APPROVED",
    MatchType = TextMatchType.Exact,
    
    // ตรวจสอบคุณสมบัติลักษณะเฉพาะ
    ForegroundColorRGB = System.Drawing.Color.Green,
    Font = new SignatureFont() { FontFamily = "Arial", FontSize = 12, Bold = true }
};
```

## แนวทางปฏิบัติที่ดีที่สุดสำหรับการยืนยันข้อความ

1. เลือกประเภทการจับคู่ที่เหมาะสม: เลือกประเภทการจับคู่ที่ถูกต้อง (มี, ตรงกัน, Regex) ตามความต้องการในการตรวจยืนยันของคุณ
2. ปรับให้เหมาะสมเพื่อประสิทธิภาพการทำงาน: สำหรับเอกสารขนาดใหญ่ ควรพิจารณาตรวจสอบหน้าเฉพาะเจาะจงแทนที่จะตรวจสอบทั้งเอกสาร
3. การจัดการข้อผิดพลาด: นำการจัดการข้อผิดพลาดที่เหมาะสมมาใช้เพื่อจัดการกับสถานการณ์ที่ไม่คาดคิดได้อย่างเหมาะสม
4. พิจารณาความละเอียดอ่อนของตัวพิมพ์ใหญ่-เล็ก: คำนึงถึงความละเอียดอ่อนของตัวพิมพ์ใหญ่-เล็กในการจับคู่ข้อความ โดยเฉพาะอย่างยิ่งสำหรับการตรวจสอบที่สำคัญ
5. ทดสอบอย่างละเอียด: ทดสอบการยืนยันด้วยรูปแบบเอกสารและรูปแบบข้อความต่างๆ เพื่อให้แน่ใจว่ามีความเข้ากันได้

## การแก้ไขปัญหาทั่วไป

### ไม่พบข้อความ
- ตรวจสอบว่าการจัดรูปแบบหรือการเข้ารหัสข้อความส่งผลต่อการตรวจจับหรือไม่
- ตรวจสอบให้แน่ใจว่าข้อความปรากฏอยู่ในเอกสารเป็นข้อความปกติ (ไม่ใช่รูปภาพ)
- ลองใช้เกณฑ์การจับคู่ที่แตกต่างกัน (ประกอบด้วย แทนที่จะเป็น ตรงกัน)

### ปัญหาประสิทธิภาพการทำงาน
- เพิ่มประสิทธิภาพการตรวจสอบโดยกำหนดเป้าหมายไปที่หน้าหรือพื้นที่เฉพาะ
- ใช้รูปแบบข้อความที่เฉพาะเจาะจงมากขึ้นเพื่อลดผลบวกปลอม

### ความล้มเหลวในการตรวจสอบ
- ตรวจสอบว่าช่องว่าง อักขระพิเศษ หรือการจัดรูปแบบส่งผลต่อการจับคู่หรือไม่
- ตรวจสอบว่าข้อความไม่ใช่ส่วนหนึ่งของภาพที่สแกน (ซึ่งต้องใช้ OCR)
- ตรวจสอบให้แน่ใจว่าเอกสารไม่ได้ถูกแก้ไขตั้งแต่มีการเพิ่มข้อความ

## บทสรุป

การยืนยันข้อความเป็นวิธีการที่หลากหลายและใช้งานได้จริงสำหรับการตรวจสอบความถูกต้องของเอกสาร ซึ่งสามารถใช้เพียงอย่างเดียวหรือใช้ร่วมกับวิธีการยืนยันอื่นๆ ได้ GroupDocs.Signature สำหรับ .NET มอบ API ที่ครอบคลุมและใช้งานง่ายสำหรับการนำฟังก์ชันการยืนยันข้อความที่มีประสิทธิภาพไปใช้ในแอปพลิเคชัน .NET ของคุณ

เมื่อทำตามคำแนะนำทีละขั้นตอนนี้ คุณจะได้เรียนรู้วิธีการดังต่อไปนี้:
- กำหนดค่าและเริ่มต้นกระบวนการตรวจสอบข้อความ
- ระบุเกณฑ์การตรวจสอบต่างๆ
- ประมวลผลและตีความผลการตรวจสอบ
- การนำสถานการณ์การตรวจสอบขั้นสูงมาใช้

ความสามารถเหล่านี้ช่วยให้คุณสร้างระบบประมวลผลเอกสารที่ปลอดภัยและเชื่อถือได้ซึ่งสามารถตรวจสอบความถูกต้องของข้อความในรูปแบบเอกสารต่างๆ ได้

## คำถามที่พบบ่อย

### GroupDocs.Signature สามารถตรวจสอบข้อความในเอกสารที่สแกนได้หรือไม่
GroupDocs.Signature ออกแบบมาเพื่อการตรวจสอบข้อความดิจิทัลเป็นหลัก สำหรับเอกสารที่สแกน คุณจะต้องใช้เทคโนโลยี OCR (Optical Character Recognition) ก่อนเพื่อแปลงรูปภาพที่สแกนเป็นข้อความ

### รูปแบบเอกสารใดบ้างที่รองรับการตรวจสอบข้อความ?
GroupDocs.Signature รองรับรูปแบบเอกสารที่หลากหลาย รวมถึง PDF, เอกสาร Word (DOC, DOCX), สเปรดชีต Excel (XLS, XLSX), งานนำเสนอ PowerPoint (PPT, PPTX), รูปภาพ และอื่นๆ อีกมากมาย

### ฉันสามารถตรวจสอบข้อความที่จัดรูปแบบ (ตัวหนา ตัวเอียง แบบอักษรเฉพาะ) ได้หรือไม่
ใช่ GroupDocs.Signature มีตัวเลือกสำหรับตรวจสอบข้อความด้วยลักษณะการจัดรูปแบบเฉพาะ รวมถึงแบบอักษร ขนาด สไตล์ (ตัวหนา ตัวเอียง) และสี

### เป็นไปได้หรือไม่ที่จะตรวจสอบข้อความในเอกสารที่ป้องกันด้วยรหัสผ่าน?
ใช่ GroupDocs.Signature ให้ตัวเลือกในการระบุรหัสผ่านเอกสารเมื่อเปิดเอกสารที่ได้รับการป้องกันเพื่อการตรวจยืนยัน

### ฉันสามารถตรวจสอบลายน้ำและข้อความพื้นหลังได้หรือไม่
ใช่ GroupDocs.Signature สามารถตรวจสอบลายเซ็นข้อความประเภทต่างๆ รวมถึงลายน้ำและข้อความพื้นหลัง ขึ้นอยู่กับว่านำไปใช้ในเอกสารอย่างไร

### แหล่งข้อมูลที่เกี่ยวข้อง
* [เอกสารอ้างอิง API GroupDocs.Signature](https://reference.groupdocs.com/signature/net/)
* [ดาวน์โหลด GroupDocs.Signature](https://releases.groupdocs.com/signature/net/)
* [ตัวอย่างโค้ดบน GitHub](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
* [เอกสารประกอบ](https://docs.groupdocs.com/signature/net/)
* [หน้าผลิตภัณฑ์](https://products.groupdocs.com/signature/net/)
* [บทความบล็อก](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
* [ฟอรั่มสนับสนุน](https://forum.groupdocs.com/c/signature/13)
* [ใบอนุญาตชั่วคราว](https://purchase.groupdocs.com/temporary-license/)