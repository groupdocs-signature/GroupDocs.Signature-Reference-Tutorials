---
"description": "เรียนรู้วิธีค้นหาลายเซ็นหลายประเภทในเอกสารโดยใช้ GroupDocs.Signature สำหรับ .NET คู่มือฉบับสมบูรณ์พร้อมตัวอย่างโค้ดเพื่อยกระดับความปลอดภัยของเอกสาร"
"linktitle": "ค้นหาลายเซ็นหลายรายการ"
"second_title": "API ของ GroupDocs.Signature .NET"
"title": "ค้นหาประเภทลายเซ็นหลายประเภทในเอกสาร"
"url": "/th/net/signature-searching/search-for-multiple-signatures/"
"weight": 14
type: docs
---
## การแนะนำ

ในระบบการจัดการเอกสารสมัยใหม่ ความสามารถในการค้นหาและตรวจสอบลายเซ็นหลายประเภทภายในเอกสารเดียวมีความสำคัญเพิ่มมากขึ้น องค์กรต่างๆ มักใช้ลายเซ็นหลายประเภท เช่น ลายเซ็นดิจิทัล ลายเซ็นข้อความ บาร์โค้ด คิวอาร์โค้ด และอื่นๆ เพื่อยกระดับความปลอดภัยของเอกสารและเพิ่มประสิทธิภาพกระบวนการตรวจสอบ GroupDocs.Signature สำหรับ .NET มอบเฟรมเวิร์กอันทรงพลังที่ช่วยให้นักพัฒนาสามารถใช้งานฟังก์ชันการค้นหาลายเซ็นที่ครอบคลุมในเอกสารหลากหลายรูปแบบได้

บทช่วยสอนนี้จะแนะนำคุณเกี่ยวกับกระบวนการค้นหาลายเซ็นประเภทต่างๆ ภายในเอกสารโดยใช้ GroupDocs.Signature สำหรับ .NET พร้อมทั้งมีคำอธิบายโดยละเอียดและตัวอย่างโค้ดที่เป็นประโยชน์

## ข้อกำหนดเบื้องต้น

ก่อนที่จะดำเนินการใช้งานฟังก์ชันการค้นหาลายเซ็นหลายรายการ ให้แน่ใจว่าคุณมีข้อกำหนดเบื้องต้นดังต่อไปนี้:

1. สภาพแวดล้อมการพัฒนา: Visual Studio หรือสภาพแวดล้อมการพัฒนา .NET อื่น ๆ ที่ต้องการติดตั้งบนระบบของคุณ
  
2. GroupDocs.Signature สำหรับ .NET: ดาวน์โหลดและติดตั้งไลบรารี GroupDocs.Signature สำหรับ .NET จาก [ที่นี่](https://releases-groupdocs.com/signature/net/).

3. ความรู้พื้นฐานเกี่ยวกับ C#: ความคุ้นเคยกับภาษาการเขียนโปรแกรม C# และแนวคิดของกรอบงาน .NET

4. เอกสารตัวอย่าง: เตรียมเอกสารทดสอบที่มีลายเซ็นประเภทต่างๆ เพื่อจุดประสงค์ในการทดสอบ

## นำเข้าเนมสเปซ

เริ่มต้นด้วยการนำเข้าเนมสเปซที่จำเป็นเพื่อเข้าถึงฟังก์ชันการทำงานของ GroupDocs.Signature:

```csharp
using System;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

ตอนนี้มาแบ่งกระบวนการค้นหาประเภทลายเซ็นหลายประเภทออกเป็นขั้นตอนที่ชัดเจนและจัดการได้:

## ขั้นตอนที่ 1: โหลดเอกสาร

ขั้นแรกโหลดเอกสารที่มีลายเซ็นที่คุณต้องการค้นหา:

```csharp
string filePath = "sample_multiple_signatures.docx";
using (Signature signature = new Signature(filePath))
{
    // จะเพิ่มรหัสการค้นหาลายเซ็นหลายรายการไว้ที่นี่
}
```

## ขั้นตอนที่ 2: กำหนดตัวเลือกการค้นหาสำหรับประเภทลายเซ็นที่แตกต่างกัน

สร้างตัวเลือกการค้นหาสำหรับประเภทลายเซ็นแต่ละประเภทที่คุณต้องการค้นหา:

```csharp
// กำหนดตัวเลือกการค้นหาสำหรับลายเซ็นข้อความ
TextSearchOptions textOptions = new TextSearchOptions
{
    AllPages = true,  // ค้นหาในทุกหน้า
    Text = "Signature",  // ตัวเลือก: ข้อความที่ต้องการค้นหา
    MatchType = TextMatchType.Contains  // เกณฑ์การจับคู่
};

// กำหนดตัวเลือกการค้นหาสำหรับลายเซ็นดิจิทัล
DigitalSearchOptions digitalOptions = new DigitalSearchOptions
{
    AllPages = true
};

// กำหนดตัวเลือกการค้นหาสำหรับลายเซ็นบาร์โค้ด
BarcodeSearchOptions barcodeOptions = new BarcodeSearchOptions
{
    AllPages = true,
    Text = "123456",  // ตัวเลือก: ข้อความบาร์โค้ดที่จะตรงกัน
    MatchType = TextMatchType.Exact  // เกณฑ์การจับคู่
};

// กำหนดตัวเลือกการค้นหาสำหรับลายเซ็น QR code
QrCodeSearchOptions qrCodeOptions = new QrCodeSearchOptions
{
    AllPages = true,
    Text = "John",  // ตัวเลือก: ข้อความ QR code ที่จะจับคู่
    MatchType = TextMatchType.Contains  // เกณฑ์การจับคู่
};

// กำหนดตัวเลือกการค้นหาสำหรับลายเซ็นข้อมูลเมตา
MetadataSearchOptions metadataOptions = new MetadataSearchOptions();
```

## ขั้นตอนที่ 3: เพิ่มตัวเลือกให้กับคอลเลกชัน

เพิ่มตัวเลือกการค้นหาทั้งหมดลงในคอลเลกชัน:

```csharp
// สร้างรายการเพื่อเก็บตัวเลือกการค้นหาทั้งหมด
List<SearchOptions> searchOptions = new List<SearchOptions>
{
    textOptions,
    digitalOptions,
    barcodeOptions,
    qrCodeOptions,
    metadataOptions
};
```

## ขั้นตอนที่ 4: ดำเนินการค้นหาและประมวลผลผลลัพธ์

ดำเนินการค้นหาโดยใช้ตัวเลือกการค้นหาแบบรวมและประมวลผลผลลัพธ์:

```csharp
// ค้นหาประเภทลายเซ็นทั้งหมดโดยใช้ตัวเลือกที่กำหนด
SearchResult result = signature.Search(searchOptions);

// ตรวจสอบว่าพบลายเซ็นหรือไม่
if (result.Signatures.Count > 0)
{
    Console.WriteLine($"\nSource document ['{filePath}'] contains {result.Signatures.Count} signature(s):");
    
    // ทำซ้ำผ่านลายเซ็นที่พบ
    foreach (var foundSignature in result.Signatures)
    {
        Console.WriteLine($"Signature found: Type: {foundSignature.SignatureType}, Page: {foundSignature.PageNumber}, ID: {foundSignature.SignatureId}");
        
        // ประเภทลายเซ็นเฉพาะกระบวนการ
        if (foundSignature is TextSignature textSignature)
        {
            Console.WriteLine($"Text: '{textSignature.Text}'");
        }
        else if (foundSignature is BarcodeSignature barcodeSignature)
        {
            Console.WriteLine($"Barcode Type: {barcodeSignature.EncodeType.TypeName}, Text: '{barcodeSignature.Text}'");
        }
        else if (foundSignature is QrCodeSignature qrCodeSignature)
        {
            Console.WriteLine($"QR Code Type: {qrCodeSignature.EncodeType.TypeName}, Text: '{qrCodeSignature.Text}'");
        }
        else if (foundSignature is DigitalSignature digitalSignature)
        {
            Console.WriteLine($"Certificate: {digitalSignature.Certificate?.SubjectName}, Valid: {digitalSignature.IsValid}");
        }
        else if (foundSignature is MetadataSignature metadataSignature)
        {
            Console.WriteLine($"Metadata: Name: {metadataSignature.Name}, Value: {metadataSignature.Value}");
        }
    }
}
else
{
    Console.WriteLine("No signatures were found in the document.");
}
```

## ตัวอย่างที่สมบูรณ์

นี่คือตัวอย่างการทำงานที่สมบูรณ์ซึ่งสาธิตการค้นหาลายเซ็นหลายประเภทในเอกสาร:

```csharp
using System;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;

namespace MultiSignatureSearch
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
                try
                {
                    // กำหนดตัวเลือกการค้นหาสำหรับลายเซ็นข้อความ
                    TextSearchOptions textOptions = new TextSearchOptions
                    {
                        AllPages = true,
                        MatchType = TextMatchType.Contains
                    };

                    // กำหนดตัวเลือกการค้นหาสำหรับลายเซ็นดิจิทัล
                    DigitalSearchOptions digitalOptions = new DigitalSearchOptions
                    {
                        AllPages = true
                    };

                    // กำหนดตัวเลือกการค้นหาสำหรับลายเซ็นบาร์โค้ด
                    BarcodeSearchOptions barcodeOptions = new BarcodeSearchOptions
                    {
                        AllPages = true
                    };

                    // กำหนดตัวเลือกการค้นหาสำหรับลายเซ็น QR code
                    QrCodeSearchOptions qrCodeOptions = new QrCodeSearchOptions
                    {
                        AllPages = true
                    };

                    // กำหนดตัวเลือกการค้นหาสำหรับลายเซ็นข้อมูลเมตา
                    MetadataSearchOptions metadataOptions = new MetadataSearchOptions();

                    // สร้างรายการเพื่อเก็บตัวเลือกการค้นหาทั้งหมด
                    List<SearchOptions> searchOptions = new List<SearchOptions>
                    {
                        textOptions,
                        digitalOptions,
                        barcodeOptions,
                        qrCodeOptions,
                        metadataOptions
                    };

                    // ค้นหาประเภทลายเซ็นทั้งหมด
                    SearchResult result = signature.Search(searchOptions);

                    // ตรวจสอบว่าพบลายเซ็นหรือไม่
                    if (result.Signatures.Count > 0)
                    {
                        Console.WriteLine($"\nSource document ['{filePath}'] contains {result.Signatures.Count} signature(s):");
                        
                        // ผลลัพธ์การประมวลผลตามประเภทลายเซ็น
                        foreach (var foundSignature in result.Signatures)
                        {
                            Console.WriteLine($"Signature found: Type: {foundSignature.SignatureType}, Page: {foundSignature.PageNumber}");
                            
                            // ประเภทลายเซ็นเฉพาะกระบวนการ
                            switch (foundSignature.SignatureType)
                            {
                                case SignatureType.Text:
                                    var textSignature = foundSignature as TextSignature;
                                    Console.WriteLine($"Text: '{textSignature.Text}'");
                                    break;
                                    
                                case SignatureType.Barcode:
                                    var barcodeSignature = foundSignature as BarcodeSignature;
                                    Console.WriteLine($"Barcode Type: {barcodeSignature.EncodeType.TypeName}, Text: '{barcodeSignature.Text}'");
                                    break;
                                    
                                case SignatureType.QrCode:
                                    var qrCodeSignature = foundSignature as QrCodeSignature;
                                    Console.WriteLine($"QR Code Type: {qrCodeSignature.EncodeType.TypeName}, Text: '{qrCodeSignature.Text}'");
                                    break;
                                    
                                case SignatureType.Digital:
                                    var digitalSignature = foundSignature as DigitalSignature;
                                    Console.WriteLine($"Certificate: {digitalSignature.Certificate?.SubjectName}, Valid: {digitalSignature.IsValid}");
                                    break;
                                    
                                case SignatureType.Metadata:
                                    var metadataSignature = foundSignature as MetadataSignature;
                                    Console.WriteLine($"Metadata: Name: {metadataSignature.Name}, Value: {metadataSignature.Value}");
                                    break;
                            }
                            
                            Console.WriteLine(); // เพิ่มการแบ่งบรรทัดระหว่างลายเซ็น
                        }
                    }
                    else
                    {
                        Console.WriteLine("No signatures were found in the document.");
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

## เทคนิคการค้นหาลายเซ็นหลายรายการขั้นสูง

### การกรองผลการค้นหา

คุณสามารถใช้การกรองขั้นสูงเพื่อจำกัดผลการค้นหาได้:

```csharp
// กรองผลลัพธ์ตามหมายเลขหน้า
var signaturesOnFirstPage = result.Signatures.FindAll(s => s.PageNumber == 1);

// กรองผลลัพธ์ตามประเภทลายเซ็น
var digitalSignatures = result.Signatures.FindAll(s => s.SignatureType == SignatureType.Digital);
var qrCodeSignatures = result.Signatures.FindAll(s => s.SignatureType == SignatureType.QrCode);

// กรองลายเซ็นข้อความที่มีเนื้อหาเฉพาะ
var approvalSignatures = result.Signatures
    .FindAll(s => s is TextSignature && ((TextSignature)s).Text.Contains("Approved"));
```

### การตรวจสอบลายเซ็นหลายรายการ

นำตรรกะการตรวจสอบไปใช้กับประเภทลายเซ็นที่แตกต่างกัน:

```csharp
bool ValidateAllSignatures(SearchResult result)
{
    bool isDocumentValid = true;
    
    // ตรวจสอบว่าเอกสารมีลายเซ็นดิจิทัลที่ถูกต้องหรือไม่
    bool hasValidDigitalSignature = result.Signatures
        .Any(s => s is DigitalSignature && ((DigitalSignature)s).IsValid);
    
    if (!hasValidDigitalSignature)
    {
        Console.WriteLine("Warning: Document does not contain a valid digital signature");
        isDocumentValid = false;
    }
    
    // ตรวจสอบว่าเอกสารมีรหัส QR ที่จำเป็นหรือไม่
    bool hasRequiredQRCode = result.Signatures
        .Any(s => s is QrCodeSignature && ((QrCodeSignature)s).Text.Contains("Auth-Code"));
    
    if (!hasRequiredQRCode)
    {
        Console.WriteLine("Warning: Document does not contain the required authentication QR code");
        isDocumentValid = false;
    }
    
    return isDocumentValid;
}
```

### การค้นหาด้วยการประมวลผลแบบกำหนดเอง

คุณสามารถกำหนดตรรกะการประมวลผลแบบกำหนดเองสำหรับการดำเนินการค้นหาได้:

```csharp
// สร้างตัวเลือกการค้นหาด้วยการประมวลผลแบบกำหนดเอง
TextSearchOptions textOptions = new TextSearchOptions
{
    AllPages = true,
    
    // กำหนดการประมวลผลแบบกำหนดเองโดยใช้ตัวแทน
    ProcessCompleted = (signature) =>
    {
        // ตรรกะการตรวจสอบแบบกำหนดเอง - ยอมรับเฉพาะลายเซ็นในหน้าที่ระบุเท่านั้น
        TextSignature textSignature = signature as TextSignature;
        return textSignature != null && (textSignature.PageNumber == 1 || textSignature.PageNumber == 2);
    }
};
```

## บทสรุป

ในคู่มือฉบับสมบูรณ์นี้ เราได้สำรวจวิธีการค้นหาลายเซ็นประเภทต่างๆ ภายในเอกสารโดยใช้ GroupDocs.Signature สำหรับ .NET ตั้งแต่การตั้งค่าตัวเลือกการค้นหาสำหรับลายเซ็นประเภทต่างๆ ไปจนถึงการประมวลผลและการตรวจสอบผลลัพธ์ ตอนนี้คุณมีความรู้ในการใช้ฟังก์ชันการค้นหาลายเซ็นที่มีประสิทธิภาพในแอปพลิเคชัน .NET ของคุณแล้ว

ความสามารถในการค้นหาลายเซ็นหลายประเภทพร้อมกัน ช่วยเพิ่มประสิทธิภาพกระบวนการตรวจสอบเอกสาร เสริมสร้างมาตรการรักษาความปลอดภัย และปรับปรุงขั้นตอนการตรวจสอบเอกสารให้มีประสิทธิภาพยิ่งขึ้น GroupDocs.Signature มอบกรอบการทำงานที่ทรงพลังและยืดหยุ่นสำหรับการทำงานกับลายเซ็นประเภทต่างๆ ในรูปแบบเอกสารที่หลากหลาย ทำให้เป็นตัวเลือกที่ยอดเยี่ยมสำหรับการใช้งานด้านการประมวลผลเอกสาร

## คำถามที่พบบ่อย

### ฉันสามารถค้นหาลายเซ็นในเอกสารที่ป้องกันด้วยรหัสผ่านได้หรือไม่

ใช่ GroupDocs.Signature รองรับการค้นหาลายเซ็นในเอกสารที่ป้องกันด้วยรหัสผ่าน คุณสามารถระบุรหัสผ่านเมื่อเริ่มต้นใช้งาน `Signature` วัตถุ:

```csharp
LoadOptions loadOptions = new LoadOptions { Password = "your_password" };
using (Signature signature = new Signature(filePath, loadOptions))
{
    // ค้นหาลายเซ็น
}
```

### รูปแบบเอกสารใดบ้างที่รองรับการค้นหาลายเซ็น?

GroupDocs.Signature รองรับรูปแบบเอกสารที่หลากหลาย รวมถึง PDF, เอกสาร Microsoft Office (Word, Excel, PowerPoint), รูปแบบ OpenOffice, รูปภาพ และอื่นๆ อีกมากมาย

### ฉันสามารถจำกัดการค้นหาให้เฉพาะเฉพาะหน้าในเอกสารได้หรือไม่

ใช่ ตัวเลือกการค้นหาแต่ละประเภทมีคุณสมบัติที่ให้คุณระบุหน้าที่ต้องการค้นหาได้:

```csharp
TextSearchOptions options = new TextSearchOptions
{
    AllPages = false,  // อย่าค้นหาทุกหน้า
    PageNumber = 1,    // ค้นหาเฉพาะหน้า 1
    
    // หรือระบุหลายหน้า
    PagesSetup = new PagesSetup { Pages = new List<int> { 1, 3, 5 } }
};
```

### ฉันจะเพิ่มประสิทธิภาพการทำงานเมื่อค้นหาเอกสารขนาดใหญ่ได้อย่างไร

สำหรับเอกสารขนาดใหญ่ คุณสามารถเพิ่มประสิทธิภาพได้โดย:

1. การจำกัดการค้นหาให้เฉพาะหน้าหรือช่วงหน้าที่เฉพาะเจาะจง
2. การใช้เกณฑ์การค้นหาที่เฉพาะเจาะจงมากขึ้นเพื่อลดจำนวนการจับคู่ที่เป็นไปได้
3. การนำการแบ่งหน้าไปใช้ในการแสดงผลผลลัพธ์ของคุณ
4. ค้นหาประเภทลายเซ็นครั้งละหนึ่งรายการหากคุณไม่ต้องการผลลัพธ์พร้อมกัน

### ฉันสามารถขยาย GroupDocs.Signature เพื่อรองรับประเภทลายเซ็นแบบกำหนดเองได้หรือไม่

แม้ว่า GroupDocs.Signature จะมีการสนับสนุนในตัวสำหรับประเภทลายเซ็นทั่วไป แต่คุณสามารถขยายการทำงานของมันได้โดย:

1. การสร้างคลาสตัวเลือกการค้นหาแบบกำหนดเองที่ได้รับมาจาก `SearchOptions`
2. การนำตรรกะการประมวลผลแบบกำหนดเองมาใช้โดยใช้ `ProcessCompleted` ผู้แทน
3. การพัฒนาคลาส wrapper ที่รวมการค้นหาลายเซ็นหลายรายการเข้ากับตรรกะทางธุรกิจขั้นสูง

## ดูเพิ่มเติม

* [ข้อมูลอ้างอิง API](https://reference.groupdocs.com/signature/net/)
* [ตัวอย่างโค้ดบน GitHub](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
* [เอกสารประกอบผลิตภัณฑ์](https://docs.groupdocs.com/signature/net/)
* [หน้าผลิตภัณฑ์](https://products.groupdocs.com/signature/net/)
* [ดาวน์โหลดเวอร์ชันล่าสุด](https://releases.groupdocs.com/signature/net/)
* [บทความบล็อก](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
* [ฟอรั่มสนับสนุนฟรี](https://forum.groupdocs.com/c/signature/13)
* [ใบอนุญาตชั่วคราว](https://purchase.groupdocs.com/temporary-license/)