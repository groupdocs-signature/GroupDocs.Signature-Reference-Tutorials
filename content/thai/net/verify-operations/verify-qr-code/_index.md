---
"description": "เรียนรู้วิธีการตรวจสอบรหัส QR ในเอกสารโดยใช้ GroupDocs.Signature สำหรับ .NET คู่มือฉบับสมบูรณ์พร้อมตัวอย่างโค้ดและแนวทางปฏิบัติที่ดีที่สุดสำหรับการตรวจสอบสิทธิ์เอกสาร"
"linktitle": "ยืนยันรหัส QR"
"second_title": "API ของ GroupDocs.Signature .NET"
"title": "ตรวจสอบ QR Code ในเอกสาร"
"url": "/th/net/verify-operations/verify-qr-code/"
"weight": 12
type: docs
---
## การแนะนำ

ความปลอดภัยของเอกสารถือเป็นปัจจัยสำคัญอย่างยิ่งต่อการดำเนินธุรกิจยุคใหม่ รหัส QR กลายเป็นวิธีที่ได้รับความนิยมเพิ่มขึ้นเรื่อยๆ สำหรับการฝังข้อมูลลงในเอกสาร ซึ่งสามารถตรวจสอบความถูกต้องได้ GroupDocs.Signature สำหรับ .NET มอบโซลูชันที่ทรงพลังและยืดหยุ่นสำหรับการตรวจสอบรหัส QR ที่ฝังอยู่ในเอกสารในรูปแบบต่างๆ

บทช่วยสอนที่ครอบคลุมนี้จะแนะนำคุณตลอดกระบวนการในการนำการตรวจสอบรหัส QR ไปใช้ในแอปพลิเคชัน .NET ของคุณ เพื่อให้แน่ใจว่าเอกสารของคุณยังคงความสมบูรณ์และถูกต้อง

## ข้อกำหนดเบื้องต้น

ก่อนที่จะใช้งานฟังก์ชันการตรวจสอบรหัส QR โปรดแน่ใจว่าคุณมีข้อกำหนดเบื้องต้นดังต่อไปนี้:

1. GroupDocs.Signature สำหรับ .NET: ดาวน์โหลดและติดตั้งไลบรารีจาก [หน้าดาวน์โหลด](https://releases-groupdocs.com/signature/net/).
2. สภาพแวดล้อมการพัฒนา: Visual Studio หรือสภาพแวดล้อมการพัฒนา .NET ที่เข้ากันได้
3. เอกสารทดสอบ: เอกสารที่มีลายเซ็น QR code เพื่อวัตถุประสงค์ในการตรวจสอบ
4. ความรู้พื้นฐาน: ความคุ้นเคยกับการเขียนโปรแกรม C# และแนวคิดของกรอบงาน .NET

## นำเข้าเนมสเปซ

เริ่มต้นด้วยการนำเข้าเนมสเปซที่จำเป็นเพื่อเข้าถึงฟังก์ชันการทำงานของ GroupDocs.Signature:

```csharp
using System;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

## ขั้นตอนการยืนยันรหัส QR ทีละขั้นตอน

ปฏิบัติตามขั้นตอนโดยละเอียดเหล่านี้เพื่อยืนยันรหัส QR ในเอกสารของคุณ:

### ขั้นตอนที่ 1: ระบุเส้นทางเอกสาร

```csharp
// ระบุเส้นทางไปยังเอกสารที่มีลายเซ็น QR code
string filePath = "sample_multiple_signatures.docx";
```

ตรวจสอบให้แน่ใจว่าคุณได้แทนที่เส้นทางตัวอย่างด้วยเส้นทางจริงไปยังเอกสารของคุณ

### ขั้นตอนที่ 2: เริ่มต้นวัตถุลายเซ็น

```csharp
// สร้างอินสแตนซ์ลายเซ็นโดยส่งเส้นทางเอกสาร
using (Signature signature = new Signature(filePath))
{
    // รหัสยืนยันจะถูกนำมาใช้ที่นี่
}
```

คลาส Signature เป็นจุดเข้าหลักสำหรับการดำเนินการทั้งหมดใน GroupDocs.Signature API

### ขั้นตอนที่ 3: กำหนดค่าตัวเลือกการตรวจสอบรหัส QR

```csharp
// กำหนดตัวเลือกการตรวจสอบรหัส QR
QrCodeVerifyOptions options = new QrCodeVerifyOptions()
{
    AllPages = true, // ตรวจสอบทุกหน้าของเอกสาร
    Text = "John",   // ข้อความที่ต้องยืนยันภายในรหัส QR
    MatchType = TextMatchType.Contains // ระบุเกณฑ์การจับคู่ข้อความ
};
```

ตัวเลือกการตรวจสอบช่วยให้คุณกำหนดเกณฑ์เฉพาะสำหรับกระบวนการตรวจสอบได้:
- `AllPages`: ตั้งค่าเป็นจริงเพื่อตรวจสอบหน้าเอกสารทั้งหมด (พฤติกรรมเริ่มต้น)
- `Text`: เนื้อหาข้อความที่จะจับคู่ภายในรหัส QR
- `MatchType`:วิธีการจับคู่ข้อความ (มี, ชัดเจน, เริ่มต้นด้วย ฯลฯ)

### ขั้นตอนที่ 4: ดำเนินการกระบวนการตรวจสอบ

```csharp
// ดำเนินการตรวจสอบ
VerificationResult result = signature.Verify(options);
```

การดำเนินการนี้จะดำเนินการตรวจสอบตามตัวเลือกที่คุณระบุ

### ขั้นตอนที่ 5: ดำเนินการตรวจสอบผลลัพธ์

```csharp
// ตรวจสอบผลการตรวจสอบและดำเนินการตามนั้น
if (result.IsValid)
{
    Console.WriteLine($"Document {filePath} contains valid QR code signature!");
    
    // แสดงข้อมูลเกี่ยวกับลายเซ็นที่ประสบความสำเร็จ
    foreach (QrCodeSignature signature in result.Succeeded)
    {
        Console.WriteLine($"Found valid QR Code signature with text: {signature.Text}");
        Console.WriteLine($"QR Code type: {signature.EncodeType.TypeName}");
        Console.WriteLine($"Location: Page {signature.PageNumber}, {signature.Left}x{signature.Top}");
    }
}
else
{
    Console.WriteLine($"Document {filePath} failed verification process.");
    Console.WriteLine($"Number of failed signatures: {result.Failed.Count}");
}
```

การจัดการผลการตรวจสอบอย่างถูกต้องจะทำให้แอปพลิเคชันของคุณดำเนินการที่เหมาะสมตามผลการตรวจสอบได้

## ตัวอย่างที่สมบูรณ์

นี่คือตัวอย่างการทำงานที่สมบูรณ์ซึ่งสาธิตการตรวจสอบรหัส QR:

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
            
            // เริ่มต้นอินสแตนซ์ลายเซ็น
            using (Signature signature = new Signature(filePath))
            {
                // ตั้งค่าตัวเลือกการยืนยัน
                QrCodeVerifyOptions options = new QrCodeVerifyOptions()
                {
                    AllPages = true,
                    Text = "John",
                    MatchType = TextMatchType.Contains
                };
                
                // ตรวจสอบลายเซ็นเอกสาร
                VerificationResult result = signature.Verify(options);
                
                // ผลการตรวจสอบกระบวนการ
                if (result.IsValid)
                {
                    Console.WriteLine($"Document {filePath} contains valid QR code signature!");
                    
                    foreach (QrCodeSignature qrSignature in result.Succeeded)
                    {
                        Console.WriteLine($"Found valid QR Code with text: {qrSignature.Text}");
                    }
                }
                else
                {
                    Console.WriteLine($"Document {filePath} failed verification process.");
                }
            }
        }
    }
}
```

## ตัวเลือกการยืนยันขั้นสูง

GroupDocs.Signature มอบตัวเลือกเพิ่มเติมสำหรับสถานการณ์การตรวจสอบที่ซับซ้อนมากขึ้น:

### การตรวจสอบประเภท QR Code เฉพาะ

```csharp
QrCodeVerifyOptions options = new QrCodeVerifyOptions()
{
    EncodeType = QrCodeTypes.QR,  // ตรวจสอบเฉพาะรหัส QR มาตรฐานเท่านั้น
    Text = "Confidential",
    MatchType = TextMatchType.Exact
};
```

### การตรวจสอบบนหน้าเฉพาะ

```csharp
QrCodeVerifyOptions options = new QrCodeVerifyOptions()
{
    AllPages = false,
    PageNumber = 2,  // ตรวจสอบเฉพาะหน้า 2 เท่านั้น
    Text = "Approved"
};
```

### การใช้นิพจน์ทั่วไปสำหรับการตรวจสอบ

```csharp
QrCodeVerifyOptions options = new QrCodeVerifyOptions()
{
    Text = "INV-\\d{6}",  // ตรงกับหมายเลขใบแจ้งหนี้ (เช่น INV-123456)
    MatchType = TextMatchType.Regex
};
```

## แนวทางปฏิบัติที่ดีที่สุดสำหรับการยืนยันรหัส QR

1. ตรวจสอบข้อมูลอินพุตเสมอ: ตรวจสอบให้แน่ใจว่าเส้นทางเอกสารและเกณฑ์การตรวจสอบถูกต้องก่อนดำเนินการประมวลผล
2. ใช้งานการจัดการข้อผิดพลาด: ใช้บล็อค try-catch เพื่อจัดการข้อยกเว้นที่อาจเกิดขึ้นระหว่างการตรวจสอบ
3. พิจารณาประสิทธิภาพ: สำหรับเอกสารขนาดใหญ่ ควรพิจารณาตรวจสอบหน้าเฉพาะเจาะจงแทนที่จะตรวจสอบทั้งเอกสาร
4. ผลการตรวจสอบบันทึก: จัดทำบันทึกกระบวนการตรวจสอบเพื่อวัตถุประสงค์ในการตรวจสอบ
5. ทดสอบกับรูปแบบเอกสารต่างๆ: ตรวจสอบให้แน่ใจว่าการตรวจยืนยันของคุณใช้ได้กับรูปแบบเอกสารที่จำเป็นทั้งหมด

## บทสรุป

การตรวจสอบรหัส QR ในเอกสารเป็นสิ่งสำคัญอย่างยิ่งในการรับรองความถูกต้องและความสมบูรณ์ของเอกสาร GroupDocs.Signature สำหรับ .NET มอบ API ที่ครอบคลุมและใช้งานง่ายสำหรับการนำการตรวจสอบรหัส QR ไปใช้งานในแอปพลิเคชัน .NET ของคุณ

เมื่อทำตามบทช่วยสอนนี้ คุณจะได้เรียนรู้วิธีการดังต่อไปนี้:
- กำหนดค่าและเริ่มต้นกระบวนการตรวจสอบ
- ระบุเกณฑ์การตรวจสอบต่างๆ
- ประมวลผลและตีความผลการตรวจสอบ
- ใช้ตัวเลือกการตรวจสอบขั้นสูง

ความรู้ดังกล่าวจะช่วยให้คุณสามารถปรับปรุงความปลอดภัยและความน่าเชื่อถือของระบบการจัดการเอกสารของคุณได้

## คำถามที่พบบ่อย

### GroupDocs.Signature สามารถตรวจสอบรหัส QR หลายรหัสในเอกสารเดียวได้หรือไม่
ใช่ GroupDocs.Signature สามารถตรวจสอบรหัส QR หลายรหัสภายในเอกสารเดียวได้ ผลการตรวจสอบจะรวมรหัส QR ทั้งหมดที่ตรงกัน

### รูปแบบเอกสารใดบ้างที่รองรับการยืนยันรหัส QR?
GroupDocs.Signature รองรับรูปแบบเอกสารที่หลากหลาย รวมถึง PDF, Word (DOC, DOCX), Excel (XLS, XLSX), PowerPoint (PPT, PPTX), รูปภาพ และอื่นๆ

### ฉันสามารถตรวจสอบรหัส QR ด้วยการเข้ารหัสหรือการจัดรูปแบบเฉพาะได้หรือไม่
ใช่ GroupDocs.Signature ให้ตัวเลือกในการยืนยันรหัส QR ด้วยประเภทการเข้ารหัสและรูปแบบการจัดรูปแบบเนื้อหาที่เฉพาะเจาะจง

### เป็นไปได้หรือไม่ที่จะตรวจสอบรหัส QR ที่สร้างโดยแอพพลิเคชั่นของบริษัทอื่น?
ใช่ GroupDocs.Signature สามารถตรวจสอบรหัส QR มาตรฐานที่สร้างขึ้นโดยแอปพลิเคชันส่วนใหญ่ได้ ตราบใดที่รหัสเหล่านั้นปฏิบัติตามรูปแบบรหัส QR มาตรฐาน

### ฉันจะจัดการรหัส QR ที่มีข้อมูลไบนารีแทนข้อความได้อย่างไร
GroupDocs.Signature ให้ตัวเลือกสำหรับการตรวจสอบรหัส QR ด้วยข้อมูลไบนารีผ่านทาง `BinaryData` คุณสมบัติของตัวเลือกการตรวจสอบ

### แหล่งข้อมูลที่เกี่ยวข้อง
* [เอกสารอ้างอิง API GroupDocs.Signature](https://reference.groupdocs.com/signature/net/)
* [ดาวน์โหลด GroupDocs.Signature](https://releases.groupdocs.com/signature/net/)
* [ตัวอย่างโค้ดบน GitHub](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
* [เอกสารประกอบ](https://docs.groupdocs.com/signature/net/)
* [หน้าผลิตภัณฑ์](https://products.groupdocs.com/signature/net/)
* [บทความบล็อก](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
* [ฟอรั่มสนับสนุน](https://forum.groupdocs.com/c/signature/13)
* [ใบอนุญาตชั่วคราว](https://purchase.groupdocs.com/temporary-license/)