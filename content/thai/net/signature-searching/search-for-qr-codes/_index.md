---
"description": "เรียนรู้วิธีค้นหารหัส QR ในเอกสารอย่างมีประสิทธิภาพโดยใช้ GroupDocs.Signature สำหรับ .NET ด้วยคำแนะนำทีละขั้นตอนและตัวอย่างโค้ดที่ครอบคลุมนี้"
"linktitle": "ค้นหา QR Code"
"second_title": "API ของ GroupDocs.Signature .NET"
"title": "ค้นหาลายเซ็น QR Code ในเอกสาร"
"url": "/th/net/signature-searching/search-for-qr-codes/"
"weight": 15
type: docs
---
## การแนะนำ

ในระบบนิเวศเอกสารดิจิทัลปัจจุบัน ลายเซ็น QR code ได้กลายเป็นเครื่องมืออันทรงคุณค่าสำหรับการฝังข้อมูล การรับรองความถูกต้อง และการเพิ่มความปลอดภัยของเอกสาร GroupDocs.Signature สำหรับ .NET มอบ API อันทรงพลังสำหรับนักพัฒนาในการค้นหาและดึง QR code จากรูปแบบเอกสารต่างๆ ช่วยให้สามารถวิเคราะห์และตรวจสอบเอกสารขั้นสูงในแอปพลิเคชัน .NET ได้

บทช่วยสอนที่ครอบคลุมนี้จะแนะนำคุณตลอดกระบวนการการใช้งานฟังก์ชันการค้นหารหัส QR โดยใช้ GroupDocs.Signature สำหรับ .NET พร้อมทั้งให้คำอธิบายที่ชัดเจน คำแนะนำทีละขั้นตอน และตัวอย่างโค้ดเชิงปฏิบัติที่คุณสามารถนำไปผสานรวมเข้ากับแอปพลิเคชันของคุณเองได้

## ข้อกำหนดเบื้องต้น

ก่อนที่จะดำเนินการค้นหาลายเซ็นรหัส QR โปรดตรวจสอบให้แน่ใจว่าคุณมีข้อกำหนดเบื้องต้นดังต่อไปนี้:

1. GroupDocs.Signature สำหรับ .NET SDK: ดาวน์โหลดและติดตั้ง SDK จาก [หน้าดาวน์โหลด](https://releases-groupdocs.com/signature/net/).

2. สภาพแวดล้อมการพัฒนา: ตั้งค่าสภาพแวดล้อมการพัฒนา .NET เช่น Visual Studio พร้อมติดตั้ง .NET Framework หรือ .NET Core

3. ความรู้พื้นฐาน: ความคุ้นเคยกับการเขียนโปรแกรม C# และแนวคิดการพัฒนา .NET

4. เอกสารตัวอย่าง: เตรียมเอกสารทดสอบที่มีรหัส QR สำหรับการตรวจสอบและการทดสอบ

## นำเข้าเนมสเปซ

เริ่มต้นด้วยการนำเข้าเนมสเปซที่จำเป็นเพื่อเข้าถึงฟังก์ชันการทำงานของ GroupDocs.Signature:

```csharp
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
using System;
using System.Collections.Generic;
```

ตอนนี้มาแบ่งกระบวนการค้นหารหัส QR ออกเป็นขั้นตอนที่ชัดเจนและง่ายต่อการปฏิบัติตาม:

## ขั้นตอนที่ 1: กำหนดเส้นทางเอกสาร

ขั้นแรกระบุเส้นทางไปยังเอกสารที่มีรหัส QR ที่คุณต้องการค้นหา:

```csharp
string filePath = "sample_multiple_signatures.docx";
```

## ขั้นตอนที่ 2: เริ่มต้นวัตถุลายเซ็น

สร้างอินสแตนซ์ของ `Signature` คลาสโดยผ่านเส้นทางเอกสาร:

```csharp
using (Signature signature = new Signature(filePath))
{
    // จะเพิ่มรหัสค้นหา QR code ไว้ที่นี่
}
```

## ขั้นตอนที่ 3: ค้นหาลายเซ็น QR Code

ใช้ `Search` วิธีการที่มีประเภทลายเซ็นที่เหมาะสมเพื่อค้นหารหัส QR ในเอกสาร:

```csharp
// ค้นหาลายเซ็น QR code ภายในเอกสาร
List<QrCodeSignature> signatures = signature.Search<QrCodeSignature>(SignatureType.QrCode);
```

## ขั้นตอนที่ 4: ประมวลผลและแสดงผลลัพธ์

ทำซ้ำผ่านลายเซ็น QR code ที่พบและเข้าถึงคุณสมบัติของลายเซ็นเหล่านี้:

```csharp
// แสดงข้อมูลเกี่ยวกับรหัส QR ที่พบ
Console.WriteLine($"\nSource document contains {signatures.Count} QR code signature(s):");

foreach (var qrCodeSignature in signatures)
{
    Console.WriteLine($"QR Code found at page {qrCodeSignature.PageNumber} with type {qrCodeSignature.EncodeType.TypeName}");
    Console.WriteLine($"Content: {qrCodeSignature.Text}");
    Console.WriteLine($"Location: X={qrCodeSignature.Left}, Y={qrCodeSignature.Top}, Width={qrCodeSignature.Width}, Height={qrCodeSignature.Height}");
    Console.WriteLine();
}
```

## ตัวอย่างที่สมบูรณ์

นี่คือตัวอย่างการทำงานที่ครอบคลุมซึ่งสาธิตกระบวนการทั้งหมดของการค้นหารหัส QR ในเอกสาร:

```csharp
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
using System;
using System.Collections.Generic;

namespace QrCodeSignatureSearch
{
    class Program
    {
        static void Main(string[] args)
        {
            // เส้นทางเอกสาร - อัปเดตด้วยเส้นทางไฟล์ของคุณ
            string filePath = "sample_multiple_signatures.docx";
            
            // เริ่มต้นอินสแตนซ์ลายเซ็น
            using (Signature signature = new Signature(filePath))
            {
                try
                {
                    // ค้นหาลายเซ็น QR code ในเอกสาร
                    List<QrCodeSignature> signatures = signature.Search<QrCodeSignature>(SignatureType.QrCode);
                    
                    // แสดงผลการค้นหา
                    Console.WriteLine($"\nSource document ['{filePath}'] contains {signatures.Count} QR code signature(s):");
                    
                    foreach (var qrCodeSignature in signatures)
                    {
                        Console.WriteLine($"QR Code found at page {qrCodeSignature.PageNumber} with type {qrCodeSignature.EncodeType.TypeName}");
                        Console.WriteLine($"Content: {qrCodeSignature.Text}");
                        Console.WriteLine($"Location: X={qrCodeSignature.Left}, Y={qrCodeSignature.Top}, Width={qrCodeSignature.Width}, Height={qrCodeSignature.Height}");
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

## เทคนิคการค้นหา QR Code ขั้นสูง

### การค้นหาด้วยเกณฑ์เฉพาะ

สำหรับการค้นหาที่ตรงเป้าหมายมากขึ้นคุณสามารถใช้ `QrCodeSearchOptions` เพื่อปรับแต่งเกณฑ์การค้นหาของคุณ:

```csharp
// สร้างตัวเลือกการค้นหารหัส QR ด้วยเกณฑ์เฉพาะ
QrCodeSearchOptions options = new QrCodeSearchOptions
{
    // ค้นหาเฉพาะหน้าที่ระบุเท่านั้น
    AllPages = false,
    PageNumber = 1,
    PagesSetup = new PagesSetup { Pages = new List<int> { 1, 3, 5 } },
    
    // กรองตามเนื้อหารหัส QR
    Text = "Invoice",
    MatchType = TextMatchType.Contains,
    
    // กรองตามประเภทรหัส QR เฉพาะ
    EncodeType = QrCodeTypes.QR,
    
    // กำหนดพื้นที่เฉพาะที่จะค้นหาภายใน
    Rectangle = new Rectangle(100, 100, 400, 400)
};

// ค้นหาด้วยตัวเลือกเฉพาะ
List<QrCodeSignature> filteredSignatures = signature.Search<QrCodeSignature>(options);
```

### การประมวลผลข้อมูลรหัส QR

คุณสามารถนำการประมวลผลแบบกำหนดเองไปใช้กับข้อมูลรหัส QR ตามความต้องการของแอปพลิเคชันของคุณได้:

```csharp
foreach (var qrCode in signatures)
{
    // สกัดและประมวลผลข้อมูลรหัส QR ตามเนื้อหา
    string qrContent = qrCode.Text;
    
    if (qrContent.StartsWith("URL:"))
    {
        // ประมวลผลข้อมูล URL
        string url = qrContent.Substring(4);
        Console.WriteLine($"Found URL in QR code: {url}");
    }
    else if (qrContent.StartsWith("CONTACT:"))
    {
        // ข้อมูลการติดต่อกระบวนการ
        string contact = qrContent.Substring(8);
        Console.WriteLine($"Found contact information in QR code: {contact}");
    }
    else if (qrContent.StartsWith("INVOICE:"))
    {
        // ดำเนินการข้อมูลใบแจ้งหนี้
        string invoiceData = qrContent.Substring(8);
        Console.WriteLine($"Found invoice information in QR code: {invoiceData}");
        
        // แยกวิเคราะห์และตรวจสอบข้อมูลใบแจ้งหนี้
        if (ValidateInvoiceData(invoiceData))
        {
            Console.WriteLine("Invoice data is valid!");
        }
        else
        {
            Console.WriteLine("Warning: Invalid invoice data detected!");
        }
    }
}

// ตัวอย่างวิธีการตรวจสอบ
static bool ValidateInvoiceData(string data)
{
    // นำตรรกะการตรวจสอบของคุณไปใช้
    return !string.IsNullOrEmpty(data) && data.Contains("ID") && data.Contains("Amount");
}
```

### การดำเนินการตรวจสอบความปลอดภัย

คิวอาร์โค้ดมักใช้เพื่อวัตถุประสงค์ในการยืนยันตัวตน ต่อไปนี้คือวิธีการตรวจสอบความปลอดภัยขั้นพื้นฐาน:

```csharp
// ตรวจสอบว่าเอกสารมีรหัส QR ยืนยันตัวตนที่ถูกต้องหรือไม่
bool hasValidAuthQrCode = false;

foreach (var qrCode in signatures)
{
    if (qrCode.Text.StartsWith("AUTH:"))
    {
        string authCode = qrCode.Text.Substring(5);
        
        // ตรวจสอบรหัสยืนยัน (เช่น กับฐานข้อมูลหรือรายการที่กำหนดไว้ล่วงหน้า)
        if (VerifyAuthCode(authCode))
        {
            hasValidAuthQrCode = true;
            Console.WriteLine("Document contains valid authentication QR code!");
            break;
        }
    }
}

if (!hasValidAuthQrCode)
{
    Console.WriteLine("Warning: Document does not contain a valid authentication QR code!");
}

// ตัวอย่างวิธีการตรวจสอบ
static bool VerifyAuthCode(string code)
{
    // นำตรรกะการตรวจสอบของคุณไปใช้
    // นี่อาจเป็นการค้นหาฐานข้อมูล การเรียก API หรือการเปรียบเทียบกับค่าที่กำหนดไว้ล่วงหน้า
    return code == "A7B82C3D" || code == "X9Y8Z7W6";
}
```

### การแยกภาพ QR Code

คุณสามารถดึงภาพ QR code จากเอกสารเพื่อประมวลผลหรือแสดงเพิ่มเติมได้:

```csharp
// บันทึกภาพ QR code ลงในดิสก์
foreach (var qrCode in signatures)
{
    if (qrCode.Content != null)
    {
        // สร้างชื่อไฟล์ที่ไม่ซ้ำกันตามหมายเลขหน้าและตำแหน่ง
        string outputPath = $"QrCode_P{qrCode.PageNumber}_X{qrCode.Left}_Y{qrCode.Top}.png";
        
        // บันทึกข้อมูลภาพ
        File.WriteAllBytes(outputPath, qrCode.Content);
        Console.WriteLine($"Saved QR code image to {outputPath}");
    }
}
```

## บทสรุป

ในคู่มือฉบับสมบูรณ์นี้ เราได้สำรวจวิธีการค้นหาลายเซ็น QR โค้ดในเอกสารโดยใช้ GroupDocs.Signature สำหรับ .NET ตั้งแต่การค้นหาขั้นพื้นฐานไปจนถึงเทคนิคขั้นสูง ตอนนี้คุณมีความรู้ในการนำการจัดการ QR โค้ดที่มีประสิทธิภาพไปใช้ในแอปพลิเคชัน .NET ของคุณแล้ว GroupDocs.Signature API มอบกรอบการทำงานที่ทรงพลังและยืดหยุ่นสำหรับการทำงานกับลายเซ็นประเภทต่างๆ รวมถึง QR โค้ด ในรูปแบบเอกสารที่แตกต่างกัน

การใช้ประโยชน์จากความสามารถเหล่านี้ ช่วยให้คุณสามารถปรับปรุงกระบวนการตรวจสอบเอกสาร ใช้งานระบบการตรวจสอบสิทธิ์ และดึงข้อมูลอันมีค่าที่ฝังอยู่ในรหัส QR ออกมาได้ ทั้งหมดนี้ทำได้ภายในแอปพลิเคชัน .NET ของคุณ

## คำถามที่พบบ่อย

### GroupDocs.Signature รองรับรูปแบบ QR code ใดบ้าง?

GroupDocs.Signature รองรับรูปแบบ QR Code หลากหลายรูปแบบ รวมถึง QR Code มาตรฐาน, Micro QR Code และมาตรฐาน QR Code ทั่วไปอื่นๆ สามารถเข้าถึงรูปแบบเฉพาะได้ผ่าน `EncodeType` ทรัพย์สินของ `QrCodeSignature` วัตถุ.

### ฉันสามารถค้นหารหัส QR ในเอกสารที่ป้องกันด้วยรหัสผ่านได้หรือไม่

ใช่ GroupDocs.Signature รองรับการค้นหารหัส QR ในเอกสารที่ป้องกันด้วยรหัสผ่านโดยระบุรหัสผ่านเมื่อเริ่มต้นใช้งาน `Signature` วัตถุ:

```csharp
LoadOptions loadOptions = new LoadOptions { Password = "your_password" };
using (Signature signature = new Signature(filePath, loadOptions))
{
    // ค้นหารหัส QR
}
```

### ฉันจะกรองรหัส QR ตามเนื้อหาได้อย่างไร

คุณสามารถกรองรหัส QR ตามเนื้อหาได้โดยใช้ `Text` และ `MatchType` คุณสมบัติของ `QrCodeSearchOptions`-

```csharp
QrCodeSearchOptions options = new QrCodeSearchOptions
{
    Text = "Invoice",
    MatchType = TextMatchType.Contains // ตัวเลือกอื่นๆ: Exact, StartsWith, EndsWith
};
```

### GroupDocs.Signature สามารถตรวจจับรหัส QR ที่เสียหายหรือมองเห็นได้เพียงบางส่วนได้หรือไม่

GroupDocs.Signature มีความสามารถในการตรวจจับคิวอาร์โค้ดที่มองเห็นได้เพียงบางส่วน แต่คิวอาร์โค้ดที่เสียหายอย่างหนักอาจไม่สามารถตรวจจับได้ ความแม่นยำในการตรวจจับขึ้นอยู่กับคุณภาพและการมองเห็นของคิวอาร์โค้ดในเอกสาร

### รูปแบบเอกสารใดบ้างที่รองรับการค้นหารหัส QR?

GroupDocs.Signature รองรับการค้นหารหัส QR ในรูปแบบเอกสารต่างๆ รวมถึง PDF, เอกสาร Microsoft Office (Word, Excel, PowerPoint), รูปภาพ (JPEG, PNG, TIFF) และอื่นๆ อีกมากมาย

## ดูเพิ่มเติม

* [ข้อมูลอ้างอิง API](https://reference.groupdocs.com/signature/net/)
* [ตัวอย่างโค้ดบน GitHub](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
* [เอกสารประกอบผลิตภัณฑ์](https://docs.groupdocs.com/signature/net/)
* [หน้าผลิตภัณฑ์](https://products.groupdocs.com/signature/net/)
* [ดาวน์โหลดเวอร์ชันล่าสุด](https://releases.groupdocs.com/signature/net/)
* [บทความบล็อก](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
* [ฟอรั่มสนับสนุนฟรี](https://forum.groupdocs.com/c/signature/13)
* [ใบอนุญาตชั่วคราว](https://purchase.groupdocs.com/temporary-license/)