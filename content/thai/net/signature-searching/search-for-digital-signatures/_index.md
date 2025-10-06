---
"description": "เชี่ยวชาญการค้นหาลายเซ็นดิจิทัลในเอกสารด้วย GroupDocs.Signature สำหรับ .NET เพิ่มความปลอดภัยและการตรวจสอบเอกสารด้วยคู่มือทีละขั้นตอนโดยละเอียดของเรา"
"linktitle": "ค้นหาลายเซ็นดิจิทัล"
"second_title": "API ของ GroupDocs.Signature .NET"
"title": "ค้นหาลายเซ็นดิจิทัลในเอกสาร"
"url": "/th/net/signature-searching/search-for-digital-signatures/"
"weight": 11
type: docs
---
## การแนะนำ

ในภูมิทัศน์ดิจิทัลปัจจุบัน การรับรองความถูกต้องและความสมบูรณ์ของเอกสารเป็นสิ่งสำคัญอย่างยิ่งสำหรับธุรกิจและองค์กรต่างๆ ลายเซ็นดิจิทัลเป็นกลไกที่แข็งแกร่งสำหรับการตรวจสอบความถูกต้องของเอกสารและการตรวจจับการแก้ไขที่ไม่ได้รับอนุญาต GroupDocs.Signature สำหรับ .NET นำเสนอโซลูชันที่ครอบคลุมสำหรับการทำงานกับลายเซ็นดิจิทัลในรูปแบบเอกสารต่างๆ ช่วยให้นักพัฒนาสามารถผสานรวมฟังก์ชันลายเซ็นเข้ากับแอปพลิเคชัน .NET ได้อย่างราบรื่น

บทช่วยสอนนี้จะแนะนำคุณเกี่ยวกับกระบวนการค้นหาลายเซ็นดิจิทัลภายในเอกสารโดยใช้ GroupDocs.Signature สำหรับ .NET พร้อมทั้งมีคำอธิบายโดยละเอียดและตัวอย่างโค้ดในทางปฏิบัติ

## ข้อกำหนดเบื้องต้น

ก่อนที่จะเจาะลึกรายละเอียดการใช้งาน ให้แน่ใจว่าคุณมีข้อกำหนดเบื้องต้นดังต่อไปนี้:

1. GroupDocs.Signature สำหรับ .NET: ดาวน์โหลดและติดตั้งไลบรารีจาก [ที่นี่](https://releases-groupdocs.com/signature/net/).
   
2. สภาพแวดล้อมการพัฒนา: ตั้งค่าสภาพแวดล้อมการพัฒนา .NET ด้วย Visual Studio หรือ IDE ที่คุณต้องการ
   
3. เอกสารตัวอย่าง: เตรียมเอกสารตัวอย่างที่มีลายเซ็นดิจิทัลเพื่อวัตถุประสงค์ในการทดสอบ

4. ความรู้พื้นฐาน: ความคุ้นเคยกับภาษาการเขียนโปรแกรม C# และพื้นฐานของกรอบงาน .NET

## นำเข้าเนมสเปซ

เริ่มต้นด้วยการนำเข้าเนมสเปซที่จำเป็นเพื่อเข้าถึงฟังก์ชันการทำงานที่ GroupDocs.Signature จัดทำไว้สำหรับ .NET:

```csharp
using System;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

ตอนนี้มาแบ่งกระบวนการค้นหาลายเซ็นดิจิทัลออกเป็นขั้นตอนที่ชัดเจนและจัดการได้:

## ขั้นตอนที่ 1: เริ่มต้นวัตถุลายเซ็น

เริ่มต้นด้วยการสร้างอินสแตนซ์ของ `Signature` คลาส ส่งผ่านเส้นทางไปยังเอกสารของคุณ:

```csharp
string filePath = "sample_multiple_signatures.docx";
using (Signature signature = new Signature(filePath))
{
    // จะเพิ่มโค้ดสำหรับค้นหาลายเซ็นดิจิทัลไว้ที่นี่
}
```

## ขั้นตอนที่ 2: ค้นหาลายเซ็นดิจิทัล

ต่อไปใช้ `Search` วิธีการด้วย `SignatureType.Digital` พารามิเตอร์ในการค้นหาลายเซ็นดิจิทัลในเอกสาร:

```csharp
// ค้นหาลายเซ็นดิจิทัลในเอกสาร
List<DigitalSignature> signatures = signature.Search<DigitalSignature>(SignatureType.Digital);
```

## ขั้นตอนที่ 3: ประมวลผลและแสดงผลลัพธ์

สุดท้ายประมวลผลผลการค้นหาและแสดงข้อมูลที่เกี่ยวข้องเกี่ยวกับลายเซ็นดิจิทัลที่พบ:

```csharp
Console.WriteLine($"\nSource document ['{filePath}'] contains the following digital signatures:");
foreach (var digitalSignature in signatures)
{
    Console.WriteLine($"Digital signature found from {digitalSignature.SignTime} with validation status: {digitalSignature.IsValid}");
    Console.WriteLine($"Certificate: Subject: {digitalSignature.Certificate?.SubjectName}");
    Console.WriteLine($"Certificate: Issuer: {digitalSignature.Certificate?.IssuerName}");
    Console.WriteLine($"Certificate: Serial Number: {digitalSignature.Certificate?.SerialNumber}");
    Console.WriteLine();
}
```

## ตัวอย่างที่สมบูรณ์

นี่คือตัวอย่างการทำงานที่สมบูรณ์ซึ่งสาธิตวิธีการค้นหาลายเซ็นดิจิทัลในเอกสาร:

```csharp
using System;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;

namespace SearchDigitalSignatures
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
                // ค้นหาลายเซ็นดิจิทัลในเอกสาร
                List<DigitalSignature> signatures = signature.Search<DigitalSignature>(SignatureType.Digital);
                
                // แสดงผลการค้นหา
                Console.WriteLine($"\nSource document ['{filePath}'] contains the following digital signatures:");
                
                if (signatures.Count > 0)
                {
                    foreach (var digitalSignature in signatures)
                    {
                        Console.WriteLine($"Digital signature found from {digitalSignature.SignTime} with validation status: {digitalSignature.IsValid}");
                        Console.WriteLine($"Certificate: Subject: {digitalSignature.Certificate?.SubjectName}");
                        Console.WriteLine($"Certificate: Issuer: {digitalSignature.Certificate?.IssuerName}");
                        Console.WriteLine($"Certificate: Serial Number: {digitalSignature.Certificate?.SerialNumber}");
                        Console.WriteLine();
                    }
                }
                else
                {
                    Console.WriteLine("No digital signatures found in the document.");
                }
            }
        }
    }
}
```

## ตัวเลือกการค้นหาขั้นสูง

สำหรับการค้นหาที่ตรงเป้าหมายมากขึ้นคุณสามารถใช้ `DigitalSearchOptions` เพื่อปรับแต่งเกณฑ์การค้นหา:

```csharp
// สร้างตัวเลือกการค้นหาแบบดิจิทัล
DigitalSearchOptions options = new DigitalSearchOptions()
{
    // ค้นหาเฉพาะหน้าที่ระบุ (เช่น หน้า 1 และ 2)
    PageNumber = 1,
    PagesSetup = new PagesSetup() { Pages = new List<int> { 1, 2 } },
    
    // กรองตามความคิดเห็นในลายเซ็นดิจิทัล
    Comments = "Approved",
    
    // กำหนดช่วงวันที่และเวลาสำหรับการค้นหา
    SignDateTimeFrom = new DateTime(2022, 1, 1),
    SignDateTimeTo = DateTime.Now
};

// ค้นหาด้วยตัวเลือกเฉพาะ
List<DigitalSignature> signatures = signature.Search<DigitalSignature>(options);
```

## การทำงานกับข้อมูลใบรับรอง

ลายเซ็นดิจิทัลมีข้อมูลใบรับรองที่มีค่าที่คุณสามารถเข้าถึงและตรวจสอบได้:

```csharp
foreach (var digitalSignature in signatures)
{
    if (digitalSignature.Certificate != null)
    {
        // คุณสมบัติใบรับรองการเข้าถึง
        Console.WriteLine($"Certificate Valid From: {digitalSignature.Certificate.NotBefore}");
        Console.WriteLine($"Certificate Valid To: {digitalSignature.Certificate.NotAfter}");
        
        // ตรวจสอบว่าใบรับรองอยู่ในช่วงวันที่ถูกต้องหรือไม่
        bool isDateValid = DateTime.Now >= digitalSignature.Certificate.NotBefore && 
                          DateTime.Now <= digitalSignature.Certificate.NotAfter;
        
        Console.WriteLine($"Certificate Date Validity: {isDateValid}");
        
        // รายละเอียดผู้ออกใบรับรองการเข้าถึง
        Console.WriteLine($"Certificate Issuer: {digitalSignature.Certificate.IssuerName}");
    }
}
```

## บทสรุป

GroupDocs.Signature สำหรับ .NET มอบโซลูชันที่ทรงพลังและยืดหยุ่นสำหรับการค้นหาและตรวจสอบลายเซ็นดิจิทัลภายในเอกสาร ในบทช่วยสอนนี้ เราได้สำรวจกระบวนการทีละขั้นตอนในการนำฟังก์ชันการค้นหาลายเซ็นดิจิทัลไปใช้ในแอปพลิเคชัน .NET เพื่อให้คุณมีความรู้ในการยกระดับความปลอดภัยและการตรวจสอบความถูกต้องของเอกสาร

การใช้ประโยชน์จาก GroupDocs.Signature จะช่วยให้คุณสร้างระบบการจัดการเอกสารที่แข็งแกร่งซึ่งรับรองความถูกต้องและความสมบูรณ์ของเอกสารดิจิทัลของคุณ ส่งเสริมความน่าเชื่อถือและการปฏิบัติตามข้อกำหนดในกระบวนการทางธุรกิจของคุณ

## คำถามที่พบบ่อย

### GroupDocs.Signature สามารถตรวจสอบความถูกต้องของลายเซ็นดิจิทัลได้หรือไม่

ใช่ GroupDocs.Signature จะตรวจสอบลายเซ็นดิจิทัลโดยอัตโนมัติในระหว่างกระบวนการค้นหา และให้สถานะการตรวจสอบผ่านทาง `IsValid` ทรัพย์สินของ `DigitalSignature` ระดับ.

### รูปแบบเอกสารใดบ้างที่รองรับการค้นหาลายเซ็นดิจิทัล?

GroupDocs.Signature รองรับการค้นหาลายเซ็นดิจิทัลในรูปแบบต่างๆ รวมถึง PDF, เอกสาร Microsoft Office (Word, Excel, PowerPoint), รูปแบบ OpenOffice และอื่นๆ อีกมากมาย

### ฉันสามารถค้นหาลายเซ็นดิจิทัลในเอกสารที่ป้องกันด้วยรหัสผ่านได้หรือไม่

ใช่ คุณสามารถค้นหาลายเซ็นดิจิทัลในเอกสารที่ได้รับการป้องกันด้วยรหัสผ่านโดยระบุรหัสผ่านเมื่อเริ่มต้นใช้งาน `Signature` วัตถุ:

```csharp
LoadOptions loadOptions = new LoadOptions() { Password = "your_password" };
using (Signature signature = new Signature(filePath, loadOptions))
{
    // ค้นหาลายเซ็นดิจิทัล
}
```

### ฉันจะตรวจสอบได้อย่างไรว่าลายเซ็นดิจิทัลถูกสร้างโดยบุคคลใดบุคคลหนึ่งหรือไม่

คุณสามารถตรวจสอบชื่อเรื่องของใบรับรองและคุณสมบัติอื่น ๆ เพื่อยืนยันตัวตนของผู้ลงนามได้:

```csharp
foreach (var signature in signatures)
{
    if (signature.Certificate?.SubjectName?.Contains("John Doe") == true)
    {
        Console.WriteLine("Found signature by John Doe");
    }
}
```

### ฉันสามารถดึงคีย์สาธารณะจากใบรับรองลายเซ็นดิจิทัลได้หรือไม่

ใช่ คุณสามารถเข้าถึงข้อมูลคีย์สาธารณะได้ผ่านคุณสมบัติใบรับรอง:

```csharp
if (signature.Certificate != null)
{
    // เข้าถึงข้อมูลคีย์สาธารณะ
    Console.WriteLine($"Public Key: {signature.Certificate.GetPublicKeyString()}");
}
```

## ดูเพิ่มเติม

* [ข้อมูลอ้างอิง API](https://reference.groupdocs.com/signature/net/)
* [ตัวอย่างโค้ด](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
* [เอกสารประกอบผลิตภัณฑ์](https://docs.groupdocs.com/signature/net/)
* [หน้าผลิตภัณฑ์](https://products.groupdocs.com/signature/net/)
* [ดาวน์โหลดเวอร์ชันล่าสุด](https://releases.groupdocs.com/signature/net/)
* [บทความบล็อก](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
* [ฟอรั่มสนับสนุน](https://forum.groupdocs.com/c/signature/13)
* [ใบอนุญาตชั่วคราว](https://purchase.groupdocs.com/temporary-license/)