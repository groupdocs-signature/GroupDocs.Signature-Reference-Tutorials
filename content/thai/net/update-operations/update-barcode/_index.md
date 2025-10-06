---
"description": "เรียนรู้วิธีอัปเดตลายเซ็นบาร์โค้ดในรูปแบบเอกสารต่างๆ ด้วยโปรแกรม GroupDocs.Signature สำหรับ .NET บทช่วยสอนที่ครอบคลุมสำหรับนักพัฒนาที่สร้างโซลูชันการจัดการเอกสาร"
"linktitle": "อัปเดตบาร์โค้ด"
"second_title": "API ของ GroupDocs.Signature .NET"
"title": "อัปเดตลายเซ็นบาร์โค้ดในเอกสาร"
"url": "/th/net/update-operations/update-barcode/"
"weight": 10
type: docs
---
## การแนะนำ
ลายเซ็นบาร์โค้ดถูกนำมาใช้อย่างแพร่หลายในเวิร์กโฟลว์เอกสารดิจิทัลเพื่อเข้ารหัสข้อมูลที่มีโครงสร้าง ช่วยให้สามารถติดตาม ระบุตัวตน และตรวจสอบความถูกต้องได้อย่างมีประสิทธิภาพ GroupDocs.Signature สำหรับ .NET เป็นโซลูชันการลงนามในเอกสารที่ครอบคลุม ช่วยให้นักพัฒนาสามารถผสานรวมฟังก์ชันลายเซ็นขั้นสูงเข้ากับแอปพลิเคชันของตน รวมถึงความสามารถในการอัปเดตลายเซ็นบาร์โค้ดที่มีอยู่ในเอกสาร

บทช่วยสอนนี้มุ่งเน้นเฉพาะการอัปเดตลายเซ็นบาร์โค้ดในเอกสารโดยใช้ GroupDocs.Signature สำหรับ .NET ไม่ว่าคุณจะต้องแก้ไขตำแหน่ง ขนาด หรือข้อมูลที่เข้ารหัสของบาร์โค้ดที่มีอยู่ คู่มือนี้จะแนะนำคุณตลอดกระบวนการพร้อมตัวอย่างโค้ดและคำอธิบายที่ชัดเจน

## ข้อกำหนดเบื้องต้น
ก่อนที่จะดำเนินการอัปเดตลายเซ็นบาร์โค้ดด้วย GroupDocs.Signature สำหรับ .NET โปรดตรวจสอบให้แน่ใจว่าคุณมีข้อกำหนดเบื้องต้นดังต่อไปนี้:

1. สภาพแวดล้อมการพัฒนา: สภาพแวดล้อมการพัฒนา .NET ที่ใช้งานได้ เช่น Visual Studio 2017 หรือใหม่กว่า
2. ไลบรารี GroupDocs.Signature: ไลบรารี GroupDocs.Signature สำหรับ .NET ซึ่งคุณสามารถดาวน์โหลดได้จาก [หน้าดาวน์โหลด](https://releases-groupdocs.com/signature/net/).
3. ความรู้พื้นฐานเกี่ยวกับ C#: ความคุ้นเคยกับแนวคิดการเขียนโปรแกรม C#
4. เอกสารตัวอย่าง: เอกสารที่มีลายเซ็นบาร์โค้ดที่คุณต้องการอัปเดต

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

ตอนนี้มาแบ่งกระบวนการอัปเดตลายเซ็นบาร์โค้ดออกเป็นขั้นตอนที่จัดการได้ดังนี้:

## ขั้นตอนที่ 1: ตั้งค่าเส้นทางเอกสาร
ขั้นแรก ให้กำหนดเส้นทางสำหรับเอกสารต้นฉบับของคุณและตำแหน่งที่จะบันทึกเอกสารที่อัปเดต:

```csharp
// เส้นทางไปยังเอกสารต้นฉบับพร้อมลายเซ็นบาร์โค้ด
string filePath = "sample_multiple_signatures.docx";

// รับชื่อไฟล์สำหรับเอาท์พุต
string fileName = Path.GetFileName(filePath);

// กำหนดไดเรกทอรีเอาต์พุตและเส้นทางไฟล์
string outputDirectory = Path.Combine("Your Document Directory", "UpdateBarcode");
string outputFilePath = Path.Combine(outputDirectory, fileName);

// ตรวจสอบให้แน่ใจว่ามีไดเร็กทอรีเอาท์พุตอยู่
Directory.CreateDirectory(outputDirectory);
```

## ขั้นตอนที่ 2: คัดลอกเอกสารต้นฉบับ
เนื่องจากการดำเนินการอัปเดตจะแก้ไขเอกสารโดยตรง ดังนั้นให้สร้างสำเนาของเอกสารต้นฉบับเพื่อเก็บรักษาไว้:

```csharp
// สร้างสำเนาของเอกสารต้นฉบับ
File.Copy(filePath, outputFilePath, true);
```

## ขั้นตอนที่ 3: เริ่มต้นอินสแตนซ์ลายเซ็น
สร้างอินสแตนซ์ของ `Signature` คลาสที่จะทำงานกับเอกสาร:

```csharp
// เริ่มต้นอินสแตนซ์ลายเซ็นด้วยเส้นทางไฟล์เอาต์พุต
using (Signature signature = new Signature(outputFilePath))
{
    // การดำเนินการลงนามจะดำเนินการที่นี่
}
```

## ขั้นตอนที่ 4: กำหนดค่าตัวเลือกการค้นหาบาร์โค้ด
ตั้งค่าตัวเลือกการค้นหาเพื่อค้นหาลายเซ็นบาร์โค้ดที่มีอยู่ในเอกสาร:

```csharp
// กำหนดค่าตัวเลือกการค้นหาสำหรับลายเซ็นบาร์โค้ด
BarcodeSearchOptions options = new BarcodeSearchOptions()
{
    // คุณสามารถกรองตามเนื้อหาข้อความได้
    Text = "12345",
    MatchType = TextMatchType.Contains
    
    // ยกเลิกการแสดงความเห็นเพื่อค้นหาในทุกหน้า
    // AllPages = จริง
};
```

## ขั้นตอนที่ 5: ค้นหาลายเซ็นบาร์โค้ด
ใช้ตัวเลือกการค้นหาที่กำหนดค่าเพื่อค้นหาลายเซ็นบาร์โค้ดในเอกสาร:

```csharp
// ค้นหาลายเซ็นบาร์โค้ด
List<BarcodeSignature> signatures = signature.Search<BarcodeSignature>(options);
```

## ขั้นตอนที่ 6: อัปเดตคุณสมบัติลายเซ็นบาร์โค้ด
หากพบลายเซ็นบาร์โค้ด ให้ปรับปรุงคุณสมบัติตามความจำเป็น:

```csharp
// ตรวจสอบว่าพบลายเซ็นหรือไม่
if (signatures.Count > 0)
{
    // รับลายเซ็นบาร์โค้ดแรก
    BarcodeSignature barcodeSignature = signatures[0];
    
    // อัปเดตตำแหน่ง
    barcodeSignature.Left = 100;
    barcodeSignature.Top = 100;
    
    // อัปเดตขนาด
    barcodeSignature.Width = 400;
    barcodeSignature.Height = 100;
    
    // ใช้การอัปเดต
    bool result = signature.Update(barcodeSignature);
    
    // ตรวจสอบผลลัพธ์
    if (result)
    {
        Console.WriteLine($"Signature with Barcode '{barcodeSignature.Text}' and encode type '{barcodeSignature.EncodeType.TypeName}' was updated in the document ['{fileName}'].");
    }
    else
    {
        Console.WriteLine($"Signature was not updated in the document! Signature with Barcode '{barcodeSignature.Text}' and encode type '{barcodeSignature.EncodeType.TypeName}' was not found!");
    }
}
else
{
    Console.WriteLine("No barcode signatures found in the document.");
}
```

## ตัวอย่างที่สมบูรณ์
นี่คือตัวอย่างการใช้งานที่สมบูรณ์ซึ่งสาธิตวิธีการอัปเดตลายเซ็นบาร์โค้ดในเอกสาร:

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;

namespace UpdateBarcodeSignatureExample
{
    class Program
    {
        static void Main(string[] args)
        {
            // เส้นทางเอกสาร
            string filePath = "sample_multiple_signatures.docx";
            
            // กำหนดเส้นทางเอาต์พุต
            string fileName = Path.GetFileName(filePath);
            string outputDirectory = Path.Combine(Environment.CurrentDirectory, "UpdateBarcode");
            string outputFilePath = Path.Combine(outputDirectory, fileName);
            
            // ตรวจสอบให้แน่ใจว่ามีไดเร็กทอรีเอาท์พุตอยู่
            Directory.CreateDirectory(outputDirectory);
            
            // สร้างสำเนาของเอกสารต้นฉบับ
            File.Copy(filePath, outputFilePath, true);
            
            // เริ่มต้นอินสแตนซ์ลายเซ็น
            using (Signature signature = new Signature(outputFilePath))
            {
                // กำหนดค่าตัวเลือกการค้นหา
                BarcodeSearchOptions options = new BarcodeSearchOptions
                {
                    Text = "12345",
                    MatchType = TextMatchType.Contains
                };
                
                // ค้นหาลายเซ็นบาร์โค้ด
                List<BarcodeSignature> signatures = signature.Search<BarcodeSignature>(options);
                
                // ตรวจสอบว่าพบลายเซ็นหรือไม่
                if (signatures.Count > 0)
                {
                    // รับลายเซ็นคนแรก
                    BarcodeSignature barcodeSignature = signatures[0];
                    
                    // อัปเดตตำแหน่งและขนาด
                    barcodeSignature.Left = 100;
                    barcodeSignature.Top = 100;
                    barcodeSignature.Width = 400;
                    barcodeSignature.Height = 100;
                    
                    // ใช้การอัปเดต
                    bool result = signature.Update(barcodeSignature);
                    
                    // ตรวจสอบผลลัพธ์
                    if (result)
                    {
                        Console.WriteLine($"Barcode signature was successfully updated in document '{fileName}'.");
                        Console.WriteLine($"Barcode text: {barcodeSignature.Text}");
                        Console.WriteLine($"Encode type: {barcodeSignature.EncodeType.TypeName}");
                        Console.WriteLine($"New position: {barcodeSignature.Left}x{barcodeSignature.Top}");
                        Console.WriteLine($"New size: {barcodeSignature.Width}x{barcodeSignature.Height}");
                        Console.WriteLine($"Output file path: {outputFilePath}");
                    }
                    else
                    {
                        Console.WriteLine("Failed to update barcode signature!");
                    }
                }
                else
                {
                    Console.WriteLine("No barcode signatures found in the document.");
                }
            }
            
            Console.WriteLine("\nPress any key to exit...");
            Console.ReadKey();
        }
    }
}
```

## การปรับแต่งลายเซ็นบาร์โค้ดขั้นสูง
GroupDocs.Signature มอบตัวเลือกเพิ่มเติมสำหรับการปรับแต่งลายเซ็นบาร์โค้ดนอกเหนือจากตำแหน่งและขนาดพื้นฐาน:

### การปรับคุณสมบัติรูปลักษณ์
ปรับแต่งลักษณะภาพของบาร์โค้ด:

```csharp
// ตั้งค่าสีพื้นหน้า (สีบาร์โค้ด)
barcodeSignature.ForeColor = System.Drawing.Color.Blue;

// ตั้งค่าสีพื้นหลัง
barcodeSignature.BackgroundColor = System.Drawing.Color.LightYellow;

// ปรับความโปร่งใส
barcodeSignature.Opacity = 0.8;
```

### การเพิ่มขอบ
ปรับปรุงบาร์โค้ดด้วยขอบที่กำหนดเอง:

```csharp
barcodeSignature.Border.Color = System.Drawing.Color.Red;
barcodeSignature.Border.DashStyle = System.Drawing.Drawing2D.DashStyle.Dash;
barcodeSignature.Border.Weight = 2;
barcodeSignature.Border.Visible = true;
```

### การหมุนบาร์โค้ด
หมุนลายเซ็นบาร์โค้ดไปยังมุมที่กำหนด:

```csharp
barcodeSignature.Angle = 30; // หมุน 30 องศา
```

## บทสรุป
GroupDocs.Signature สำหรับ .NET มอบโซลูชันที่ทรงพลังและยืดหยุ่นสำหรับการอัปเดตลายเซ็นบาร์โค้ดภายในเอกสาร ด้วยการทำตามขั้นตอนที่ระบุไว้ในบทช่วยสอนนี้ นักพัฒนาสามารถนำฟังก์ชันการอัปเดตลายเซ็นบาร์โค้ดไปใช้ในแอปพลิเคชัน .NET ได้อย่างมีประสิทธิภาพ ซึ่งจะช่วยยกระดับความสามารถในการจัดการเอกสารและการทำงานอัตโนมัติ

ด้วยชุดคุณลักษณะที่ครอบคลุมและ API ที่ใช้งานง่าย GroupDocs.Signature ช่วยให้นักพัฒนาสามารถสร้างโซลูชันการลงนามเอกสารที่ซับซ้อนซึ่งตรงตามข้อกำหนดของแอปพลิเคชันธุรกิจสมัยใหม่ พร้อมทั้งรับประกันความสมบูรณ์และการเข้าถึงเอกสาร

## คำถามที่พบบ่อย
### ฉันสามารถอัปเดตลายเซ็นบาร์โค้ดหลายรายการภายในเอกสารเดียวได้หรือไม่
ใช่ GroupDocs.Signature ช่วยให้คุณอัปเดตลายเซ็นบาร์โค้ดหลายรายการภายในเอกสารเดียวกันได้ หลังจากค้นหาลายเซ็นแล้ว คุณสามารถวนซ้ำผ่านรายการผลลัพธ์และอัปเดตลายเซ็นบาร์โค้ดแต่ละรายการได้

### GroupDocs.Signature รองรับรูปแบบบาร์โค้ดที่แตกต่างกันหรือไม่
ใช่ GroupDocs.Signature รองรับรูปแบบบาร์โค้ดที่หลากหลาย รวมถึงบาร์โค้ดเชิงเส้น (รหัส 128, รหัส 39, EAN, UPC เป็นต้น) และบาร์โค้ด 2 มิติ (QR Code, Data Matrix, PDF417 เป็นต้น)

### มีเวอร์ชันทดลองใช้สำหรับ GroupDocs.Signature สำหรับ .NET หรือไม่
ใช่ คุณสามารถดาวน์โหลดเวอร์ชันทดลองใช้ฟรีได้จาก [เว็บไซต์ GroupDocs](https://releases.groupdocs.com/signature/net/) เพื่อประเมินคุณลักษณะของห้องสมุดก่อนตัดสินใจซื้อ

### ฉันสามารถแปลงบาร์โค้ดประเภทหนึ่งเป็นอีกประเภทหนึ่งเมื่อทำการอัพเดตได้หรือไม่
ไม่รองรับการแปลงบาร์โค้ดระหว่างประเภทต่างๆ โดยตรงระหว่างการอัปเดต อย่างไรก็ตาม คุณสามารถทำได้โดยการลบบาร์โค้ดที่มีอยู่แล้วและเพิ่มบาร์โค้ดใหม่ที่มีรูปแบบที่ต้องการ

### การอัปเดตบาร์โค้ดส่งผลต่อความสามารถในการสแกนหรือไม่?
เมื่ออัปเดตคุณสมบัติบาร์โค้ด เช่น ขนาดและตำแหน่ง GroupDocs.Signature จะรักษาความสมบูรณ์ของการสแกนบาร์โค้ดไว้ อย่างไรก็ตาม ขนาดที่เล็กมากหรือมุมหมุนที่มากอาจส่งผลต่อประสิทธิภาพการสแกนของเครื่องอ่านบางรุ่น

### ฉันสามารถค้นหาการสนับสนุนเพิ่มเติมสำหรับ GroupDocs.Signature สำหรับ .NET ได้ที่ไหน
คุณสามารถค้นหาการสนับสนุนที่ครอบคลุมได้จากแหล่งข้อมูลต่อไปนี้:
- [เอกสารประกอบ API](https://docs.groupdocs.com/signature/net/)
- [ข้อมูลอ้างอิง API](https://reference.groupdocs.com/signature/net/)
- [ตัวอย่าง GitHub](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
- [ฟอรั่มสนับสนุน](https://forum.groupdocs.com/c/signature/13)
- [บล็อก](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
- [การสนับสนุนฟรี](https://forum.groupdocs.com/c/signature)
- [ใบอนุญาตชั่วคราว](https://purchase.groupdocs.com/temporary-license/)