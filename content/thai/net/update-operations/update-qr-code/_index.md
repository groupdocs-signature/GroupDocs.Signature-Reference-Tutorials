---
"description": "เรียนรู้วิธีอัปเดตลายเซ็น QR code แบบไดนามิกในรูปแบบเอกสารต่างๆ ด้วย GroupDocs.Signature สำหรับ .NET คู่มือนักพัฒนาที่ครอบคลุมสำหรับโซลูชันการจัดการเอกสารสมัยใหม่"
"linktitle": "อัปเดต QR Code"
"second_title": "API ของ GroupDocs.Signature .NET"
"title": "อัปเดตลายเซ็น QR Code ในเอกสาร"
"url": "/th/net/update-operations/update-qr-code/"
"weight": 12
type: docs
---
## การแนะนำ
ในสภาพแวดล้อมทางธุรกิจที่ให้ความสำคัญกับดิจิทัลในปัจจุบัน รหัส QR ได้กลายเป็นองค์ประกอบสำคัญในระบบจัดการและยืนยันตัวตนเอกสาร รหัส QR ช่วยให้การเข้ารหัสและเข้าถึงข้อมูลได้อย่างสะดวก ตั้งแต่ URL ธรรมดาไปจนถึงข้อมูลที่มีโครงสร้างซับซ้อน GroupDocs.Signature สำหรับ .NET นำเสนอชุดเครื่องมือที่ครอบคลุมซึ่งช่วยให้นักพัฒนาสามารถผสานรวมความสามารถด้านลายเซ็นอิเล็กทรอนิกส์ขั้นสูงเข้ากับแอปพลิเคชันของตน รวมถึงความสามารถในการอัปเดตลายเซ็น QR ที่มีอยู่ในเอกสาร

บทช่วยสอนนี้มุ่งเน้นเฉพาะการอัปเดตลายเซ็น QR code ในเอกสารโดยใช้ GroupDocs.Signature สำหรับ .NET ไม่ว่าคุณจะต้องแก้ไขตำแหน่ง ขนาด หรือข้อมูลที่เข้ารหัสของ QR code ที่มีอยู่ คู่มือนี้จะแนะนำคุณตลอดกระบวนการทีละขั้นตอน พร้อมตัวอย่างโค้ดและคำอธิบายที่ชัดเจน

## ข้อกำหนดเบื้องต้น
ก่อนที่จะดำเนินการอัปเดตลายเซ็น QR โค้ดด้วย GroupDocs.Signature สำหรับ .NET ตรวจสอบให้แน่ใจว่าคุณมีข้อกำหนดเบื้องต้นดังต่อไปนี้:

1. สภาพแวดล้อมการพัฒนา: สภาพแวดล้อมการพัฒนา .NET ที่ใช้งานได้ เช่น Visual Studio 2017 หรือใหม่กว่า
2. ไลบรารี GroupDocs.Signature: ดาวน์โหลดและติดตั้งไลบรารี GroupDocs.Signature สำหรับ .NET จาก [หน้าดาวน์โหลด](https://releases-groupdocs.com/signature/net/).
3. ใบอนุญาต (ไม่บังคับ): สำหรับการใช้งานจริง คุณจะต้องมีใบอนุญาตที่ถูกต้อง สำหรับการทดสอบ คุณสามารถใช้ [ใบอนุญาตชั่วคราว](https://purchase-groupdocs.com/temporary-license/).
4. เอกสารตัวอย่าง: เอกสารที่มีลายเซ็น QR code ที่คุณต้องการอัปเดต
5. ความรู้พื้นฐานเกี่ยวกับ C#: ความคุ้นเคยกับแนวคิดการเขียนโปรแกรม C#

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

มาแบ่งกระบวนการอัปเดตลายเซ็นโค้ด QR ออกเป็นขั้นตอนที่ชัดเจนและจัดการได้:

## ขั้นตอนที่ 1: ตั้งค่าเส้นทางเอกสาร
ขั้นแรก ให้กำหนดเส้นทางสำหรับเอกสารต้นฉบับของคุณและตำแหน่งที่จะบันทึกเอกสารที่อัปเดต:

```csharp
// เส้นทางไปยังเอกสารต้นฉบับพร้อมลายเซ็น QR code
string filePath = "sample_multiple_signatures.docx";

// รับชื่อไฟล์สำหรับเอาท์พุต
string fileName = Path.GetFileName(filePath);

// กำหนดไดเรกทอรีเอาต์พุตและเส้นทางไฟล์
string outputDirectory = Path.Combine("Your Document Directory", "UpdateQRCode");
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

## ขั้นตอนที่ 4: กำหนดค่าตัวเลือกการค้นหารหัส QR
ตั้งค่าตัวเลือกการค้นหาเพื่อค้นหาลายเซ็น QR code ที่มีอยู่ในเอกสาร:

```csharp
// กำหนดค่าตัวเลือกการค้นหาสำหรับลายเซ็นรหัส QR
QrCodeSearchOptions options = new QrCodeSearchOptions();

// คุณสามารถปรับแต่งตัวเลือกการค้นหาได้หากจำเป็น
// options.AllPages = true; // ค้นหาในทุกหน้า
// options.PageNumber = 1; // ค้นหาในหน้าที่ระบุ
// options.EncodeType = QrCodeTypes.QR; // ค้นหาประเภท QR code ที่ต้องการ
```

## ขั้นตอนที่ 5: ค้นหาลายเซ็น QR Code
ใช้ตัวเลือกการค้นหาที่กำหนดค่าเพื่อค้นหาลายเซ็นรหัส QR ในเอกสาร:

```csharp
// ค้นหาลายเซ็น QR code
List<QrCodeSignature> signatures = signature.Search<QrCodeSignature>(options);
```

## ขั้นตอนที่ 6: อัปเดตคุณสมบัติลายเซ็น QR Code
หากพบลายเซ็นรหัส QR ให้ปรับปรุงคุณสมบัติตามความจำเป็น:

```csharp
// ตรวจสอบว่าพบลายเซ็นหรือไม่
if (signatures.Count > 0)
{
    // รับลายเซ็น QR code แรก
    QrCodeSignature qrCodeSignature = signatures[0];
    
    // อัปเดตตำแหน่ง
    qrCodeSignature.Left = 200;
    qrCodeSignature.Top = 250;
    
    // อัปเดตขนาด
    qrCodeSignature.Width = 200;
    qrCodeSignature.Height = 200;
    
    // คุณยังสามารถอัปเดตข้อมูลรหัส QR ได้หากจำเป็น
    // qrCodeSignature.Text = "อัปเดตข้อมูล QR Code";
    
    // ใช้การอัปเดต
    bool result = signature.Update(qrCodeSignature);
    
    // ตรวจสอบผลลัพธ์
    if (result)
    {
        Console.WriteLine($"QR Code signature was successfully updated in the document '{fileName}'.");
        Console.WriteLine($"New position: {qrCodeSignature.Left}x{qrCodeSignature.Top}");
        Console.WriteLine($"New size: {qrCodeSignature.Width}x{qrCodeSignature.Height}");
    }
    else
    {
        Console.WriteLine($"Failed to update QR Code signature in the document!");
    }
}
else
{
    Console.WriteLine("No QR Code signatures found in the document.");
}
```

## ตัวอย่างที่สมบูรณ์
นี่คือตัวอย่างการใช้งานที่สมบูรณ์ซึ่งสาธิตวิธีการอัปเดตลายเซ็นโค้ด QR ในเอกสาร:

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;

namespace UpdateQRCodeSignatureExample
{
    class Program
    {
        static void Main(string[] args)
        {
            // เส้นทางเอกสาร
            string filePath = "sample_multiple_signatures.docx";
            
            // กำหนดเส้นทางเอาต์พุต
            string fileName = Path.GetFileName(filePath);
            string outputDirectory = Path.Combine(Environment.CurrentDirectory, "UpdateQRCode");
            string outputFilePath = Path.Combine(outputDirectory, fileName);
            
            // ตรวจสอบให้แน่ใจว่ามีไดเร็กทอรีเอาท์พุตอยู่
            Directory.CreateDirectory(outputDirectory);
            
            // สร้างสำเนาของเอกสารต้นฉบับ
            File.Copy(filePath, outputFilePath, true);
            
            // เริ่มต้นอินสแตนซ์ลายเซ็น
            using (Signature signature = new Signature(outputFilePath))
            {
                // กำหนดค่าตัวเลือกการค้นหา
                QrCodeSearchOptions options = new QrCodeSearchOptions();
                
                // ค้นหาลายเซ็น QR code
                List<QrCodeSignature> signatures = signature.Search<QrCodeSignature>(options);
                
                // ตรวจสอบว่าพบลายเซ็นหรือไม่
                if (signatures.Count > 0)
                {
                    // รับลายเซ็นคนแรก
                    QrCodeSignature qrCodeSignature = signatures[0];
                    
                    // อัปเดตตำแหน่งและขนาด
                    qrCodeSignature.Left = 200;
                    qrCodeSignature.Top = 250;
                    qrCodeSignature.Width = 200;
                    qrCodeSignature.Height = 200;
                    
                    // ใช้การอัปเดต
                    bool result = signature.Update(qrCodeSignature);
                    
                    // ตรวจสอบผลลัพธ์
                    if (result)
                    {
                        Console.WriteLine($"QR Code signature was successfully updated in document '{fileName}'.");
                        Console.WriteLine($"New position: {qrCodeSignature.Left}x{qrCodeSignature.Top}");
                        Console.WriteLine($"New size: {qrCodeSignature.Width}x{qrCodeSignature.Height}");
                        Console.WriteLine($"Output file path: {outputFilePath}");
                    }
                    else
                    {
                        Console.WriteLine("Failed to update QR Code signature!");
                    }
                }
                else
                {
                    Console.WriteLine("No QR Code signatures found in the document.");
                }
            }
            
            Console.WriteLine("\nPress any key to exit...");
            Console.ReadKey();
        }
    }
}
```

## การปรับแต่งลายเซ็น QR Code ขั้นสูง
GroupDocs.Signature มอบตัวเลือกเพิ่มเติมสำหรับการปรับแต่งลายเซ็นโค้ด QR นอกเหนือจากตำแหน่งและขนาดพื้นฐาน:

### การอัปเดตข้อมูลที่เข้ารหัส
คุณสามารถอัปเดตข้อมูลจริงที่เข้ารหัสในรหัส QR ได้:

```csharp
// อัพเดตข้อมูลเข้ารหัส
qrCodeSignature.Text = "https://www.updated-website.com";
```

### การปรับคุณสมบัติรูปลักษณ์
ปรับแต่งลักษณะภาพของรหัส QR:

```csharp
// ตั้งค่าสีพื้นหน้า (สี QR code)
qrCodeSignature.ForeColor = System.Drawing.Color.Blue;

// ตั้งค่าสีพื้นหลัง
qrCodeSignature.BackgroundColor = System.Drawing.Color.LightYellow;

// ปรับความโปร่งใส
qrCodeSignature.Opacity = 0.8;
```

### การเพิ่มขอบ
ปรับปรุงรหัส QR ด้วยเส้นขอบที่กำหนดเอง:

```csharp
qrCodeSignature.Border.Color = System.Drawing.Color.Red;
qrCodeSignature.Border.DashStyle = System.Drawing.Drawing2D.DashStyle.Dash;
qrCodeSignature.Border.Weight = 2;
qrCodeSignature.Border.Visible = true;
```

### การหมุนรหัส QR
หมุนลายเซ็น QR code ไปที่มุมที่ต้องการ:

```csharp
qrCodeSignature.Angle = 30; // หมุน 30 องศา
```

## การทำงานกับรูปแบบเอกสารที่แตกต่างกัน
GroupDocs.Signature รองรับการอัปเดตลายเซ็น QR code ในรูปแบบเอกสารต่างๆ:

- เอกสาร PDF
- เอกสาร Microsoft Word (DOC, DOCX)
- สเปรดชีต Microsoft Excel (XLS, XLSX)
- การนำเสนอ Microsoft PowerPoint (PPT, PPTX)
- รูปแบบ OpenDocument
- รูปแบบภาพ

สามารถใช้โค้ดเดียวกันได้กับรูปแบบเหล่านี้โดยมีการปรับเปลี่ยนเล็กน้อย

## บทสรุป
GroupDocs.Signature สำหรับ .NET มอบโซลูชันที่ทรงพลังและยืดหยุ่นสำหรับการอัปเดตลายเซ็น QR Code ภายในเอกสาร ด้วยการทำตามขั้นตอนที่ระบุไว้ในบทช่วยสอนนี้ นักพัฒนาสามารถนำฟังก์ชันการอัปเดตลายเซ็น QR Code ไปใช้ในแอปพลิเคชัน .NET ได้อย่างมีประสิทธิภาพ ซึ่งจะช่วยยกระดับความสามารถในการจัดการเอกสารและการตรวจสอบสิทธิ์

ด้วยชุดคุณลักษณะที่ครอบคลุมและ API ที่ใช้งานง่าย GroupDocs.Signature ช่วยให้นักพัฒนาสามารถสร้างโซลูชันการลงนามเอกสารที่ซับซ้อนซึ่งตรงตามข้อกำหนดของแอปพลิเคชันธุรกิจสมัยใหม่ พร้อมทั้งรับประกันความสมบูรณ์และการเข้าถึงเอกสาร

## คำถามที่พบบ่อย
### ฉันสามารถอัปเดตลายเซ็น QR code หลายรายการภายในเอกสารเดียวได้หรือไม่
ใช่ GroupDocs.Signature ช่วยให้คุณอัปเดตลายเซ็น QR code หลายรายการภายในเอกสารเดียวกันได้ หลังจากค้นหาลายเซ็นแล้ว คุณสามารถวนซ้ำผ่านรายการผลลัพธ์และอัปเดตลายเซ็น QR code แต่ละรายการได้

### GroupDocs.Signature รองรับประเภท QR code ที่แตกต่างกันหรือไม่
ใช่ GroupDocs.Signature รองรับ QR code หลากหลายประเภท รวมถึง QR มาตรฐาน, Micro QR และอื่นๆ คุณสามารถระบุประเภท QR code ได้โดยใช้ `EncodeType` คุณสมบัติ.

### มีเวอร์ชันทดลองใช้สำหรับ GroupDocs.Signature สำหรับ .NET หรือไม่
ใช่ คุณสามารถดาวน์โหลดเวอร์ชันทดลองใช้ฟรีได้จาก [เว็บไซต์ GroupDocs](https://releases.groupdocs.com/signature/net/) เพื่อประเมินคุณลักษณะของห้องสมุดก่อนตัดสินใจซื้อ

### ฉันสามารถเปลี่ยนระดับการแก้ไขข้อผิดพลาดรหัส QR โดยใช้โปรแกรมได้หรือไม่
ใช่ คุณสามารถเปลี่ยนระดับการแก้ไขข้อผิดพลาดได้เมื่อเพิ่มรหัส QR ใหม่ แต่การอัปเดตคุณสมบัติสำหรับรหัส QR ที่มีอยู่นี้อาจไม่ได้รับการรองรับในรูปแบบเอกสารทั้งหมด

### ฉันสามารถค้นหาการสนับสนุนเพิ่มเติมสำหรับ GroupDocs.Signature สำหรับ .NET ได้ที่ไหน
คุณสามารถค้นหาการสนับสนุนที่ครอบคลุมได้จากแหล่งข้อมูลต่อไปนี้:
- [เอกสารประกอบ API](https://docs.groupdocs.com/signature/net/)
- [ข้อมูลอ้างอิง API](https://reference.groupdocs.com/signature/net/)
- [ตัวอย่าง GitHub](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
- [ฟอรั่มสนับสนุน](https://forum.groupdocs.com/c/signature/13)
- [บล็อก](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)