---
"description": "ใช้งานการตรวจสอบลายเซ็นดิจิทัลอย่างปลอดภัยในแอปพลิเคชัน .NET ด้วย GroupDocs.Signature คู่มือทีละขั้นตอนพร้อมตัวอย่างโค้ดที่ครบถ้วนสำหรับการตรวจสอบสิทธิ์เอกสาร"
"linktitle": "ตรวจสอบลายเซ็นดิจิทัล"
"second_title": "API ของ GroupDocs.Signature .NET"
"title": "ตรวจสอบลายเซ็นดิจิทัลในเอกสาร"
"url": "/th/net/verify-operations/verify-digital/"
"weight": 11
---

## การแนะนำ

ลายเซ็นดิจิทัลมีบทบาทสำคัญในการรับรองความถูกต้อง ความสมบูรณ์ และการป้องกันการปฏิเสธความรับผิดชอบของเอกสารในกระบวนการทางธุรกิจสมัยใหม่ ลายเซ็นดิจิทัลแตกต่างจากลายเซ็นลายมือแบบดั้งเดิมตรงที่ใช้เทคนิคการเข้ารหัสเพื่อยืนยันตัวตนของผู้ลงนาม และเพื่อให้แน่ใจว่าเอกสารไม่ได้ถูกเปลี่ยนแปลงตั้งแต่ลงนาม

GroupDocs.Signature สำหรับ .NET มอบชุดเครื่องมือที่ครอบคลุมซึ่งช่วยให้นักพัฒนาสามารถนำการตรวจสอบลายเซ็นดิจิทัลที่มีประสิทธิภาพไปใช้ในแอปพลิเคชัน .NET ของพวกเขาได้ บทช่วยสอนโดยละเอียดนี้จะแนะนำคุณตลอดกระบวนการตรวจสอบลายเซ็นดิจิทัลภายในเอกสารโดยใช้ GroupDocs.Signature สำหรับ .NET

## ข้อกำหนดเบื้องต้น

ก่อนที่จะใช้งานฟังก์ชันการตรวจสอบลายเซ็นดิจิทัล ให้แน่ใจว่าคุณมีข้อกำหนดเบื้องต้นดังต่อไปนี้:

1. GroupDocs.Signature สำหรับ .NET: ดาวน์โหลดและติดตั้งไลบรารีจาก [GroupDocs.Signature สำหรับรุ่น .NET](https://releases-groupdocs.com/signature/net/).
2. สภาพแวดล้อมการพัฒนา .NET: Visual Studio หรือสภาพแวดล้อมการพัฒนา .NET ที่เข้ากันได้
3. ใบรับรองดิจิทัล: ไฟล์ใบรับรองดิจิทัล (เช่น .pfx) ที่ใช้ในการลงนามในเอกสารหรือใบรับรองที่อยู่ในเครือข่ายที่เชื่อถือได้
4. เอกสารสำหรับการตรวจสอบ: เอกสารที่มีลายเซ็นดิจิทัลที่ต้องมีการตรวจสอบ

## นำเข้าเนมสเปซที่จำเป็น

เริ่มต้นด้วยการนำเข้าเนมสเปซที่จำเป็นเพื่อเข้าถึงฟังก์ชันการทำงานของ GroupDocs.Signature:

```csharp
using System;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

มาแบ่งกระบวนการตรวจสอบลายเซ็นดิจิทัลออกเป็นขั้นตอนที่ชัดเจนและจัดการได้ดังนี้:

## ขั้นตอนที่ 1: ระบุเส้นทางเอกสาร

```csharp
// เส้นทางไปยังเอกสารที่มีลายเซ็นดิจิทัล
string filePath = "sample_multiple_signatures.docx";
```

แทนที่เส้นทางตัวอย่างด้วยเส้นทางจริงไปยังเอกสารของคุณที่มีลายเซ็นดิจิทัล

## ขั้นตอนที่ 2: เริ่มต้นวัตถุลายเซ็น

```csharp
// สร้างอินสแตนซ์ของคลาส Signature โดยส่งเส้นทางเอกสาร
using (Signature signature = new Signature(filePath))
{
    // รหัสยืนยันจะถูกนำมาใช้ที่นี่
}
```

คลาส Signature เป็นจุดเข้าหลักสำหรับการดำเนินการทั้งหมดใน GroupDocs.Signature API

## ขั้นตอนที่ 3: กำหนดค่าตัวเลือกการยืนยันแบบดิจิทัล

```csharp
// ตั้งค่าตัวเลือกการยืนยัน
DigitalVerifyOptions options = new DigitalVerifyOptions("YourSignature.pfx")
{
    Contact = "Mr.Smith",     // คาดว่าจะมีการติดต่อผู้ลงนาม
    Password = "1234567890",  // รหัสผ่านใบรับรองหากจำเป็น
    AllPages = true           // ตรวจสอบลายเซ็นทุกหน้า
};
```

ตัวเลือกการตรวจสอบช่วยให้คุณระบุ:
- เส้นทางไฟล์ใบรับรองดิจิทัล
- ข้อมูลติดต่อผู้ลงนามที่คาดหวัง
- รหัสผ่านสำหรับใบรับรองหากมีการป้องกันด้วยรหัสผ่าน
- ช่วงหน้าที่จะตรวจสอบ (ทุกหน้าตามค่าเริ่มต้น)

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
    Console.WriteLine($"Document {filePath} contains valid digital signatures!");
    
    // แสดงรายละเอียดของลายเซ็นที่ถูกต้อง
    foreach (DigitalSignature digitalSignature in result.Succeeded)
    {
        Console.WriteLine($"\nValid signature found:");
        Console.WriteLine($"Signer: {digitalSignature.Subject}");
        Console.WriteLine($"Issuer: {digitalSignature.Issuer}");
        Console.WriteLine($"Valid From: {digitalSignature.ValidFrom}");
        Console.WriteLine($"Valid To: {digitalSignature.ValidTo}");
    }
}
else
{
    Console.WriteLine($"Document {filePath} failed verification process.");
    
    // แสดงข้อมูลเกี่ยวกับลายเซ็นที่ล้มเหลวหากจำเป็น
    foreach (DigitalSignature failedSignature in result.Failed)
    {
        Console.WriteLine($"Failed signature reason: {failedSignature.Comments}");
    }
}
```

โค้ดนี้จะตรวจสอบว่าการตรวจสอบสำเร็จหรือไม่ และให้ข้อมูลโดยละเอียดเกี่ยวกับลายเซ็นที่ได้รับการตรวจสอบ

## ตัวอย่างที่สมบูรณ์

นี่คือตัวอย่างการทำงานที่สมบูรณ์ซึ่งสาธิตการตรวจสอบลายเซ็นดิจิทัล:

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
                    DigitalVerifyOptions options = new DigitalVerifyOptions("YourSignature.pfx")
                    {
                        Contact = "Mr.Smith",
                        Password = "1234567890"
                    };
                    
                    // ตรวจสอบลายเซ็นเอกสาร
                    VerificationResult result = signature.Verify(options);
                    
                    // ผลการตรวจสอบกระบวนการ
                    if (result.IsValid)
                    {
                        Console.WriteLine($"Document {filePath} contains valid digital signatures!");
                        
                        foreach (DigitalSignature item in result.Succeeded)
                        {
                            Console.WriteLine($"\nValid signature found.");
                            Console.WriteLine($"Subject: {item.Subject}");
                            Console.WriteLine($"Comments: {item.Comments}");
                            Console.WriteLine($"Sign Time: {item.SignTime}");
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

### การตรวจสอบลายเซ็นดิจิทัลหลายรายการ

```csharp
// สร้างรายการตัวเลือกการตรวจสอบ
List<VerifyOptions> listOptions = new List<VerifyOptions>();

// เพิ่มตัวเลือกการตรวจสอบใบรับรองแรก
listOptions.Add(new DigitalVerifyOptions("Certificate1.pfx")
{
    Contact = "John Smith"
});

// เพิ่มตัวเลือกการตรวจสอบใบรับรองที่สอง
listOptions.Add(new DigitalVerifyOptions("Certificate2.pfx")
{
    Contact = "Jane Doe"
});

// ยืนยันด้วยตัวเลือกหลายตัว
VerificationResult result = signature.Verify(listOptions);
```

### การตรวจสอบลายเซ็นบนหน้าเฉพาะ

```csharp
// ตรวจสอบลายเซ็นดิจิทัลเฉพาะในหน้าแรกเท่านั้น
DigitalVerifyOptions options = new DigitalVerifyOptions("YourSignature.pfx")
{
    AllPages = false,
    PageNumber = 1
};
```

### การใช้ Timestamp และการตรวจสอบผู้มีอำนาจออกใบรับรอง

```csharp
DigitalVerifyOptions options = new DigitalVerifyOptions("YourSignature.pfx")
{
    ValidateTimeStampOnly = true,   // ตรวจสอบเฉพาะวันที่และเวลาเท่านั้น
    CertificateAuth = CertificateAuthType.Standard  // ตรวจสอบใบรับรองผู้ลงนาม
};
```

## แนวทางปฏิบัติที่ดีที่สุดสำหรับการตรวจสอบลายเซ็นดิจิทัล

1. การจัดการใบรับรองที่เหมาะสม: จัดเก็บไฟล์ใบรับรองอย่างปลอดภัยและจัดการรหัสผ่านอย่างเหมาะสม
2. การตรวจสอบใบรับรอง: นำการตรวจสอบใบรับรองแบบโซ่มาใช้เพื่อให้แน่ใจว่าใบรับรองนั้นถูกต้อง
3. การจัดการข้อผิดพลาด: นำการจัดการข้อผิดพลาดที่แข็งแกร่งมาใช้เพื่อจัดการกับความล้มเหลวในการตรวจสอบอย่างเหมาะสม
4. การบันทึก: ความพยายามและผลลัพธ์การตรวจสอบบันทึกเพื่อวัตถุประสงค์ในการตรวจสอบและการปฏิบัติตาม
5. การอัปเดตใบรับรองปกติ: ตรวจสอบให้แน่ใจว่าใบรับรองได้รับการอัปเดตก่อนที่จะหมดอายุ

## การแก้ไขปัญหาทั่วไป

### ใบรับรองไม่ถูกต้อง
- ตรวจสอบว่าเส้นทางไฟล์ใบรับรองถูกต้อง
- ตรวจสอบให้แน่ใจว่ารหัสผ่านใบรับรองถูกต้อง
- ตรวจสอบว่าใบรับรองหมดอายุหรือไม่

### ไม่พบลายเซ็น
- ยืนยันว่าเอกสารมีลายเซ็นดิจิทัลจริง
- ตรวจสอบว่าคุณกำลังตรวจสอบหน้าที่ถูกต้อง

### ความล้มเหลวในการตรวจสอบ
- ตรวจสอบว่าเอกสารได้รับการแก้ไขหลังจากการลงนามหรือไม่
- ตรวจสอบว่าใบรับรองของผู้ลงนามอยู่ในห่วงโซ่ใบรับรองที่เชื่อถือได้

## บทสรุป

GroupDocs.Signature สำหรับ .NET มอบโซลูชันที่ทรงพลังและยืดหยุ่นสำหรับการตรวจสอบลายเซ็นดิจิทัลภายในเอกสาร การปฏิบัติตามคำแนะนำทีละขั้นตอนนี้จะช่วยให้คุณสามารถนำการตรวจสอบลายเซ็นดิจิทัลที่มีประสิทธิภาพไปใช้กับแอปพลิเคชัน .NET ของคุณ รับรองความถูกต้องและความสมบูรณ์ของเอกสาร

การตรวจสอบลายเซ็นดิจิทัลเป็นองค์ประกอบสำคัญของเวิร์กโฟลว์เอกสารที่ปลอดภัยในสภาพแวดล้อมทางธุรกิจสมัยใหม่ ด้วย GroupDocs.Signature คุณสามารถใช้งานฟังก์ชันนี้ได้อย่างมั่นใจด้วยความพยายามเพียงเล็กน้อย ด้วย API ที่ครอบคลุมเพื่อจัดการสถานการณ์การตรวจสอบที่หลากหลาย

## คำถามที่พบบ่อย

### GroupDocs.Signature สามารถตรวจสอบลายเซ็นในเอกสาร PDF ที่ลงนามโดยใช้ Adobe Acrobat ได้หรือไม่
ใช่ GroupDocs.Signature สามารถตรวจสอบลายเซ็นดิจิทัลมาตรฐานในเอกสาร PDF ที่สร้างโดย Adobe Acrobat และซอฟต์แวร์ PDF ที่รองรับอื่นๆ ได้

### GroupDocs.Signature รองรับการตรวจสอบความถูกต้องของเวลาในเอกสารหรือไม่
ใช่ API ให้ตัวเลือกในการยืนยันเวลาของเอกสารเป็นส่วนหนึ่งของกระบวนการยืนยันลายเซ็นดิจิทัล

### ฉันสามารถตรวจสอบลายเซ็นบนหน้าเฉพาะของเอกสารหลายหน้าได้หรือไม่
ใช่ คุณสามารถกำหนดค่าตัวเลือกการตรวจสอบเพื่อตรวจสอบลายเซ็นบนหน้าเฉพาะแทนที่จะตรวจสอบทั้งเอกสารได้

### GroupDocs.Signature รองรับการตรวจสอบลายเซ็นหลายรายการภายในเอกสารเดียวหรือไม่
ใช่ GroupDocs.Signature สามารถตรวจสอบลายเซ็นดิจิทัลหลายรายการภายในเอกสารเดียว และให้ผลลัพธ์โดยละเอียดสำหรับลายเซ็นแต่ละรายการได้

### เป็นไปได้หรือไม่ที่จะตรวจสอบลายเซ็นที่สร้างด้วยใบรับรองจากผู้มีอำนาจออกใบรับรองที่แตกต่างกัน
ใช่ GroupDocs.Signature รองรับการตรวจสอบลายเซ็นที่สร้างด้วยใบรับรองจากผู้มีอำนาจออกใบรับรองที่แตกต่างกัน ตราบใดที่ลายเซ็นเหล่านั้นอยู่ในห่วงโซ่ใบรับรองที่เชื่อถือได้

### แหล่งข้อมูลที่เกี่ยวข้อง
* [เอกสารอ้างอิง API GroupDocs.Signature](https://reference.groupdocs.com/signature/net/)
* [ดาวน์โหลด GroupDocs.Signature](https://releases.groupdocs.com/signature/net/)
* [ตัวอย่างโค้ดบน GitHub](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
* [เอกสารประกอบ](https://docs.groupdocs.com/signature/net/)
* [หน้าผลิตภัณฑ์](https://products.groupdocs.com/signature/net/)
* [บทความบล็อก](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
* [ฟอรั่มสนับสนุน](https://forum.groupdocs.com/c/signature/13)
* [ใบอนุญาตชั่วคราว](https://purchase.groupdocs.com/temporary-license/)