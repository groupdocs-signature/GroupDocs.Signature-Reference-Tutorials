---
"description": "ใช้งานการตรวจสอบบาร์โค้ดที่มีประสิทธิภาพในแอปพลิเคชัน .NET ด้วย GroupDocs.Signature ตัวอย่างโค้ดที่สมบูรณ์และแนวทางปฏิบัติที่ดีที่สุดเพื่อรับรองความถูกต้องของเอกสาร"
"linktitle": "ตรวจสอบบาร์โค้ด"
"second_title": "API ของ GroupDocs.Signature .NET"
"title": "ตรวจสอบลายเซ็นบาร์โค้ดในเอกสาร"
"url": "/th/net/verify-operations/verify-barcode/"
"weight": 10
---

## การแนะนำ

บาร์โค้ดกลายเป็นส่วนสำคัญของระบบการจัดการเอกสารสมัยใหม่ ช่วยให้เข้าถึงข้อมูลที่เข้ารหัสได้อย่างรวดเร็ว และยังทำหน้าที่เป็นคุณลักษณะด้านความปลอดภัยอีกด้วย GroupDocs.Signature สำหรับ .NET มอบ API อันทรงพลังสำหรับการตรวจสอบลายเซ็นบาร์โค้ดภายในเอกสาร เพื่อรับรองความถูกต้องและความสมบูรณ์ของเอกสาร

บทช่วยสอนที่ครอบคลุมนี้จะอธิบายกระบวนการนำการตรวจสอบบาร์โค้ดไปใช้ในแอปพลิเคชัน .NET โดยใช้ GroupDocs.Signature ไม่ว่าคุณจะทำงานกับเอกสารธุรกิจ ใบรับรอง สัญญา หรือเอกสารประเภทใดก็ตามที่ใช้บาร์โค้ดเพื่อการตรวจสอบสิทธิ์ คู่มือนี้จะช่วยให้คุณนำฟังก์ชันการตรวจสอบที่มีประสิทธิภาพมาใช้ได้

## ข้อกำหนดเบื้องต้น

ก่อนที่จะใช้งานฟังก์ชันการตรวจสอบบาร์โค้ด ให้แน่ใจว่าคุณมีข้อกำหนดเบื้องต้นดังต่อไปนี้:

1. GroupDocs.Signature สำหรับ .NET: ดาวน์โหลดและติดตั้งไลบรารีจาก [หน้าดาวน์โหลด](https://releases-groupdocs.com/signature/net/).
2. สภาพแวดล้อมการพัฒนา .NET: Visual Studio หรือสภาพแวดล้อมการพัฒนา .NET ที่เข้ากันได้
3. ความรู้พื้นฐาน: ความคุ้นเคยกับการเขียนโปรแกรม C# และแนวคิดของกรอบงาน .NET
4. เอกสารทดสอบ: เอกสารที่มีลายเซ็นบาร์โค้ดเพื่อวัตถุประสงค์ในการตรวจสอบ

## นำเข้าเนมสเปซที่จำเป็น

เริ่มต้นด้วยการนำเข้าเนมสเปซที่จำเป็นเพื่อเข้าถึงฟังก์ชันการทำงานของ GroupDocs.Signature:

```csharp
using System;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

มาแบ่งกระบวนการตรวจสอบบาร์โค้ดออกเป็นขั้นตอนที่ชัดเจนและจัดการได้ดังนี้:

## ขั้นตอนที่ 1: ระบุเส้นทางเอกสาร

```csharp
// เส้นทางไปยังเอกสารที่มีลายเซ็นบาร์โค้ด
string filePath = "sample_multiple_signatures.docx";
```

ตรวจสอบให้แน่ใจว่าคุณได้แทนที่เส้นทางตัวอย่างด้วยเส้นทางจริงไปยังเอกสารของคุณที่มีลายเซ็นบาร์โค้ด

## ขั้นตอนที่ 2: เริ่มต้นวัตถุลายเซ็น

```csharp
// สร้างอินสแตนซ์ของคลาส Signature โดยส่งเส้นทางเอกสาร
using (Signature signature = new Signature(filePath))
{
    // รหัสยืนยันจะถูกนำมาใช้ที่นี่
}
```

คลาส Signature เป็นจุดเข้าหลักสำหรับการดำเนินการทั้งหมดใน GroupDocs.Signature API

## ขั้นตอนที่ 3: กำหนดค่าตัวเลือกการตรวจสอบบาร์โค้ด

```csharp
// กำหนดตัวเลือกการตรวจสอบบาร์โค้ด
BarcodeVerifyOptions options = new BarcodeVerifyOptions()
{
    AllPages = true,           // ตรวจสอบทุกหน้าของเอกสาร
    Text = "12345",            // ข้อความที่จะจับคู่ภายในบาร์โค้ด
    MatchType = TextMatchType.Contains // ระบุเกณฑ์การจับคู่ข้อความ
};
```

ตัวเลือกการตรวจสอบช่วยให้คุณกำหนดเกณฑ์เฉพาะสำหรับกระบวนการตรวจสอบได้:
- `AllPages`: ตั้งค่าเป็นจริงเพื่อตรวจสอบหน้าเอกสารทั้งหมด
- `Text`: เนื้อหาข้อความที่จะจับคู่ภายในบาร์โค้ด
- `MatchType`: วิธีการจับคู่ข้อความ (ประกอบด้วย, ตรงกัน, เริ่มต้นด้วย, สิ้นสุดด้วย)

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
    Console.WriteLine($"Document {filePath} contains valid barcode signatures!");
    
    // แสดงข้อมูลเกี่ยวกับลายเซ็นที่ประสบความสำเร็จ
    foreach (BarcodeSignature barcodeSignature in result.Succeeded)
    {
        Console.WriteLine($"\nFound valid barcode signature:");
        Console.WriteLine($"Text: {barcodeSignature.Text}");
        Console.WriteLine($"Type: {barcodeSignature.EncodeType.TypeName}");
        Console.WriteLine($"Location: Page {barcodeSignature.PageNumber}, {barcodeSignature.Left}x{barcodeSignature.Top}");
    }
}
else
{
    Console.WriteLine($"Document {filePath} failed verification process.");
    Console.WriteLine($"Number of failed signatures: {result.Failed.Count}");
}
```

โค้ดนี้จะตรวจสอบว่าการตรวจสอบสำเร็จหรือไม่ และให้ข้อมูลโดยละเอียดเกี่ยวกับลายเซ็นบาร์โค้ดที่ได้รับการตรวจสอบ

## ตัวอย่างที่สมบูรณ์

นี่คือตัวอย่างการทำงานที่สมบูรณ์ซึ่งสาธิตการตรวจสอบบาร์โค้ด:

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
                    BarcodeVerifyOptions options = new BarcodeVerifyOptions()
                    {
                        AllPages = true,
                        Text = "12345",
                        MatchType = TextMatchType.Contains
                    };
                    
                    // ตรวจสอบลายเซ็นเอกสาร
                    VerificationResult result = signature.Verify(options);
                    
                    // ผลการตรวจสอบกระบวนการ
                    if (result.IsValid)
                    {
                        Console.WriteLine($"Document {filePath} contains valid barcode signatures!");
                        
                        foreach (BarcodeSignature item in result.Succeeded)
                        {
                            Console.WriteLine($"\nValid signature found with text: {item.Text}");
                            Console.WriteLine($"Barcode type: {item.EncodeType.TypeName}");
                            Console.WriteLine($"Page: {item.PageNumber}");
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

### การตรวจสอบประเภทบาร์โค้ดเฉพาะ

หากคุณทราบประเภทบาร์โค้ดเฉพาะที่คุณกำลังมองหา คุณสามารถจำกัดการตรวจยืนยันให้เฉพาะประเภทนั้นได้:

```csharp
BarcodeVerifyOptions options = new BarcodeVerifyOptions()
{
    EncodeType = BarcodeTypes.Code128,  // ตรวจสอบเฉพาะบาร์โค้ด Code128 เท่านั้น
    Text = "PROD-12345",
    MatchType = TextMatchType.Exact
};
```

### การตรวจสอบบาร์โค้ดบนหน้าเฉพาะ

สำหรับเอกสารหลายหน้า คุณสามารถจำกัดการตรวจยืนยันให้เฉพาะหน้าที่ระบุได้:

```csharp
BarcodeVerifyOptions options = new BarcodeVerifyOptions()
{
    AllPages = false,
    PageNumber = 2,  // ตรวจสอบเฉพาะหน้า 2 เท่านั้น
    Text = "INV-2023"
};
```

### การใช้นิพจน์ทั่วไปสำหรับการตรวจสอบ

หากต้องการจับคู่รูปแบบที่ยืดหยุ่นยิ่งขึ้น คุณสามารถใช้นิพจน์ทั่วไปได้:

```csharp
BarcodeVerifyOptions options = new BarcodeVerifyOptions()
{
    Text = "INV-\\d{4}-\\d{2}",  // จับคู่หมายเลขใบแจ้งหนี้ เช่น INV-2023-01
    MatchType = TextMatchType.Regex
};
```

### การตรวจสอบบาร์โค้ดหลายประเภทพร้อมกัน

คุณสามารถสร้างตัวเลือกการตรวจสอบหลายรายการเพื่อตรวจสอบประเภทบาร์โค้ดที่แตกต่างกัน:

```csharp
// สร้างรายการตัวเลือกการตรวจสอบ
List<VerifyOptions> listOptions = new List<VerifyOptions>();

// เพิ่มการยืนยัน QR Code
listOptions.Add(new BarcodeVerifyOptions()
{
    EncodeType = BarcodeTypes.QR,
    Text = "Security"
});

// เพิ่มการยืนยัน Code128
listOptions.Add(new BarcodeVerifyOptions()
{
    EncodeType = BarcodeTypes.Code128,
    Text = "12345"
});

// ยืนยันด้วยตัวเลือกหลายตัว
VerificationResult result = signature.Verify(listOptions);
```

## แนวทางปฏิบัติที่ดีที่สุดสำหรับการตรวจสอบบาร์โค้ด

1. การจัดการข้อผิดพลาด: ใช้การจัดการข้อผิดพลาดที่เหมาะสมอยู่เสมอเพื่อจัดการกับสถานการณ์ที่ไม่คาดคิดได้อย่างเหมาะสม
2. การเพิ่มประสิทธิภาพการทำงาน: สำหรับเอกสารขนาดใหญ่ ควรพิจารณาตรวจสอบเฉพาะหน้าที่เฉพาะเจาะจงแทนที่จะตรวจสอบทั้งเอกสาร
3. การบันทึกข้อมูล: นำการบันทึกข้อมูลไปใช้งานเพื่อติดตามความพยายามและผลลัพธ์การตรวจสอบเพื่อวัตถุประสงค์ในการตรวจสอบ
4. ข้อควรพิจารณาด้านความปลอดภัย: จัดเก็บเกณฑ์การยืนยันอย่างปลอดภัย โดยเฉพาะอย่างยิ่งหากเป็นส่วนหนึ่งของโครงสร้างพื้นฐานด้านความปลอดภัยของคุณ
5. การทดสอบ: ทดสอบการยืนยันด้วยรูปแบบเอกสารและประเภทบาร์โค้ดต่างๆ เพื่อให้แน่ใจถึงความเข้ากันได้

## การแก้ไขปัญหาทั่วไป

### ไม่พบบาร์โค้ด
- ตรวจสอบให้แน่ใจว่าบาร์โค้ดสามารถมองเห็นได้ชัดเจนในเอกสาร
- ตรวจสอบว่าประเภทบาร์โค้ดได้รับการรองรับโดย GroupDocs.Signature หรือไม่
- ตรวจสอบว่าบาร์โค้ดไม่บิดเบี้ยวหรือเสียหาย

### ความล้มเหลวในการตรวจสอบ
- ยืนยันว่าเกณฑ์การตรวจสอบ (ข้อความ, ประเภทบาร์โค้ด) ถูกต้อง
- ตรวจสอบว่า MatchType เหมาะสมกับกรณีการใช้งานของคุณหรือไม่
- ตรวจสอบว่าเอกสารไม่ได้รับการแก้ไขตั้งแต่มีการใช้บาร์โค้ด

### ปัญหาประสิทธิภาพการทำงาน
- เพิ่มประสิทธิภาพการตรวจสอบโดยกำหนดเป้าหมายไปที่หน้าเฉพาะที่คาดว่าจะมีบาร์โค้ด
- จำกัดการตรวจสอบให้เฉพาะประเภทบาร์โค้ดเท่านั้นหากทราบล่วงหน้า

## บทสรุป

การตรวจสอบบาร์โค้ดเป็นเครื่องมือสำคัญในการรับรองความถูกต้องและความสมบูรณ์ของเอกสารในระบบจัดการเอกสารสมัยใหม่ GroupDocs.Signature สำหรับ .NET มอบ API ที่ครอบคลุมและใช้งานง่ายสำหรับการนำฟังก์ชันการตรวจสอบบาร์โค้ดที่มีประสิทธิภาพไปใช้งานในแอปพลิเคชัน .NET ของคุณ

เมื่อทำตามคำแนะนำทีละขั้นตอนนี้ คุณจะได้เรียนรู้วิธีการดังต่อไปนี้:
- กำหนดค่าและเริ่มต้นกระบวนการตรวจสอบ
- ระบุเกณฑ์การตรวจสอบต่างๆ
- ประมวลผลและตีความผลการตรวจสอบ
- การนำสถานการณ์การตรวจสอบขั้นสูงมาใช้

ความสามารถเหล่านี้ช่วยให้คุณสร้างระบบประมวลผลเอกสารที่ปลอดภัยและเชื่อถือได้ซึ่งสามารถตรวจสอบความถูกต้องของบาร์โค้ดในรูปแบบเอกสารต่างๆ ได้

## คำถามที่พบบ่อย

### รูปแบบเอกสารใดบ้างที่รองรับการตรวจสอบบาร์โค้ด?
GroupDocs.Signature รองรับรูปแบบเอกสารที่หลากหลาย รวมถึง PDF, เอกสาร Word (DOC, DOCX), สเปรดชีต Excel (XLS, XLSX), งานนำเสนอ PowerPoint (PPT, PPTX), รูปภาพ และอื่นๆ อีกมากมาย

### GroupDocs.Signature สามารถตรวจสอบบาร์โค้ดหลายอันในเอกสารเดียวได้หรือไม่
ใช่ GroupDocs.Signature สามารถตรวจสอบบาร์โค้ดหลายรายการภายในเอกสารเดียวได้ ผลการตรวจสอบจะรวมบาร์โค้ดที่ตรงกันทั้งหมด

### ประเภทบาร์โค้ดใดบ้างที่รองรับสำหรับการตรวจสอบ?
GroupDocs.Signature รองรับบาร์โค้ดหลายประเภท รวมถึง Code39, Code128, EAN13, EAN8, QR Code, DataMatrix, PDF417 และอื่นๆ อีกมากมาย

### ฉันสามารถตรวจสอบบาร์โค้ดในเอกสารที่ป้องกันด้วยรหัสผ่านได้หรือไม่
ใช่ GroupDocs.Signature ให้ตัวเลือกในการระบุรหัสผ่านเอกสารเมื่อเปิดเอกสารที่ได้รับการป้องกันเพื่อการตรวจยืนยัน

### เป็นไปได้ไหมที่จะตรวจสอบบาร์โค้ดที่มีข้อมูลไบนารีแทนข้อความ?
ใช่ GroupDocs.Signature มีตัวเลือกสำหรับการตรวจสอบบาร์โค้ดด้วยข้อมูลไบนารีผ่านทาง `BinaryData` คุณสมบัติของตัวเลือกการตรวจสอบ

### แหล่งข้อมูลที่เกี่ยวข้อง
* [เอกสารอ้างอิง API GroupDocs.Signature](https://reference.groupdocs.com/signature/net/)
* [ดาวน์โหลด GroupDocs.Signature](https://releases.groupdocs.com/signature/net/)
* [ตัวอย่างโค้ดบน GitHub](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
* [เอกสารประกอบ](https://docs.groupdocs.com/signature/net/)
* [หน้าผลิตภัณฑ์](https://products.groupdocs.com/signature/net/)
* [บทความบล็อก](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
* [ฟอรั่มสนับสนุน](https://forum.groupdocs.com/c/signature/13)
* [ใบอนุญาตชั่วคราว](https://purchase.groupdocs.com/temporary-license/)