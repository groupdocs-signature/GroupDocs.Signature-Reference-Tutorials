---
"description": "เรียนรู้วิธีลงนามและฝังข้อมูลเมตาลงในรูปภาพโดยใช้ GroupDocs.Signature สำหรับ .NET เพิ่มข้อมูลผู้เขียน ประทับเวลา และข้อมูลที่กำหนดเอง เพื่อปรับปรุงความถูกต้องและการตรวจสอบย้อนกลับของรูปภาพ"
"linktitle": "ภาพลายเซ็นพร้อมข้อมูลเมตา"
"second_title": "API ของ GroupDocs.Signature .NET"
"title": "ลงนามภาพด้วยข้อมูลเมตาใน C# .NET"
"url": "/th/net/document-signing/sign-image-with-metadata/"
"weight": 10
---

## การแนะนำ

การลงนามภาพดิจิทัลด้วยเมตาดาต้ากำลังมีความสำคัญเพิ่มมากขึ้นเรื่อยๆ ในการสร้างความน่าเชื่อถือ ความเป็นเจ้าของ และการตรวจสอบย้อนกลับ GroupDocs.Signature สำหรับ .NET มอบโซลูชันที่ทรงพลังแต่ใช้งานง่ายสำหรับการเพิ่มลายเซ็นเมตาดาต้าให้กับรูปแบบภาพต่างๆ บทช่วยสอนนี้จะแนะนำคุณตลอดกระบวนการลงนามภาพด้วยเมตาดาต้าโดยใช้ C#

ลายเซ็นเมตาเดตาช่วยให้คุณฝังข้อมูลสำคัญลงในไฟล์ภาพได้โดยตรง เช่น ข้อมูลผู้เขียน ตราประทับเวลาที่สร้าง รหัสประจำตัวเฉพาะ และอื่นๆ ข้อมูลนี้จะเป็นส่วนหนึ่งของไฟล์ภาพเอง ซึ่งเป็นวิธีการที่เชื่อถือได้ในการติดตามและตรวจสอบความถูกต้องของภาพ

## ข้อกำหนดเบื้องต้น

ก่อนที่จะดำเนินการตามบทช่วยสอนนี้ โปรดแน่ใจว่าคุณมีสิ่งต่อไปนี้:

1. [GroupDocs.Signature สำหรับ .NET](https://releases.groupdocs.com/signature/net/) - ดาวน์โหลดและติดตั้งไลบรารี
2. สภาพแวดล้อมการพัฒนา - Visual Studio หรือ IDE ใดๆ ที่เข้ากันได้กับการรองรับ .NET
3. ไฟล์รูปภาพ - ไฟล์รูปภาพตัวอย่างในรูปแบบที่รองรับ (PNG, JPG, TIFF เป็นต้น)
4. ความรู้พื้นฐานเกี่ยวกับการเขียนโปรแกรม C# - ความคุ้นเคยกับแนวคิดการเขียนโปรแกรม C#

## นำเข้าเนมสเปซ

เริ่มต้นด้วยการนำเข้าเนมสเปซที่จำเป็นเพื่อเข้าถึงฟังก์ชันการทำงานของ GroupDocs.Signature:

```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

## ขั้นตอนที่ 1: ตั้งค่าเส้นทางไฟล์

กำหนดเส้นทางสำหรับภาพต้นฉบับของคุณและตำแหน่งที่จะบันทึกเอาต์พุตที่ลงนาม:

```csharp
// ระบุเส้นทางไปยังไฟล์ภาพต้นฉบับของคุณ
string filePath = "sample.png";

// กำหนดไดเรกทอรีเอาต์พุตและชื่อไฟล์สำหรับภาพที่ลงนาม
string outputDirectory = "Your Document Directory";
string outputFilePath = Path.Combine(outputDirectory, "SignImageWithMetadata", "SignedWithMetadata.png");

// ตรวจสอบให้แน่ใจว่ามีไดเร็กทอรีเอาท์พุตอยู่
Directory.CreateDirectory(Path.GetDirectoryName(outputFilePath));
```

## ขั้นตอนที่ 2: เริ่มต้นวัตถุลายเซ็น

สร้างอินสแตนซ์ของคลาส Signature ด้วยไฟล์ภาพต้นฉบับของคุณ:

```csharp
using (Signature signature = new Signature(filePath))
{
    // ส่วนที่เหลือของโค้ดจะอยู่ที่นี่
}
```

## ขั้นตอนที่ 3: สร้างและกำหนดค่าลายเซ็นข้อมูลเมตา

ขั้นต่อไป ให้กำหนดเมตาดาต้าที่คุณต้องการฝังลงในรูปภาพ GroupDocs.Signature รองรับประเภทข้อมูลเมตาดาต้าหลากหลายประเภท:

```csharp
// เริ่มต้น ID เมตาข้อมูล (เฉพาะกับรูปแบบภาพ)
ushort imgsMetadataId = 41996;

// สร้างวัตถุตัวเลือกเมตาข้อมูล
MetadataSignOptions options = new MetadataSignOptions();

// เพิ่มลายเซ็นข้อมูลเมตาประเภทต่างๆ
options
    .Add(new ImageMetadataSignature(imgsMetadataId++, "Mr.Sherlock Holmes"))  // ค่าสตริง
    .Add(new ImageMetadataSignature(imgsMetadataId++, DateTime.Now))          // ค่าวันที่และเวลา
    .Add(new ImageMetadataSignature(imgsMetadataId++, 123456))                // ค่าจำนวนเต็ม
    .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456D))              // ค่าสองเท่า
    .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456M))              // ค่าทศนิยม
    .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456F));             // ค่าลอยตัว
```

## ขั้นตอนที่ 4: ลงนามภาพด้วยข้อมูลเมตา

ใช้ลายเซ็นข้อมูลเมตากับรูปภาพและบันทึกผลลัพธ์:

```csharp
// ลงนามในเอกสารและบันทึกลงในเส้นทางไฟล์เอาต์พุต
SignResult result = signature.Sign(outputFilePath, options);

// แสดงข้อความแสดงความสำเร็จ
Console.WriteLine($"\nSource image signed successfully with {result.Succeeded.Count} metadata signature(s).");
Console.WriteLine($"Signed image saved at: {outputFilePath}");
```

## ตัวอย่างที่สมบูรณ์

นี่คือตัวอย่างโค้ดที่สมบูรณ์ซึ่งรวบรวมขั้นตอนทั้งหมดเข้าด้วยกัน:

```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;

namespace SignImageWithMetadataExample
{
    class Program
    {
        static void Main(string[] args)
        {
            // ระบุเส้นทางไฟล์
            string filePath = "sample.png";            
            string outputFilePath = Path.Combine("Your Document Directory", "SignImageWithMetadata", "SignedWithMetadata.png");
            
            // ตรวจสอบให้แน่ใจว่ามีไดเร็กทอรีเอาท์พุตอยู่
            Directory.CreateDirectory(Path.GetDirectoryName(outputFilePath));

            // ลงนามภาพด้วยข้อมูลเมตา
            using (Signature signature = new Signature(filePath))
            {
                // เริ่มต้น ID เมตาข้อมูล (เฉพาะกับรูปแบบภาพ)
                ushort imgsMetadataId = 41996;
                
                // สร้างตัวเลือกข้อมูลเมตา
                MetadataSignOptions options = new MetadataSignOptions();
                
                // เพิ่มลายเซ็นข้อมูลเมตาประเภทต่างๆ
                options
                    .Add(new ImageMetadataSignature(imgsMetadataId++, "Mr.Sherlock Holmes")) // ค่าสตริง
                    .Add(new ImageMetadataSignature(imgsMetadataId++, DateTime.Now))          // ค่าวันที่และเวลา
                    .Add(new ImageMetadataSignature(imgsMetadataId++, 123456))                // ค่าจำนวนเต็ม
                    .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456D))              // ค่าสองเท่า
                    .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456M))              // ค่าทศนิยม
                    .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456F));             // ค่าลอยตัว
                
                // ลงนามเอกสารและบันทึกลงในไฟล์
                SignResult result = signature.Sign(outputFilePath, options);
                
                // แสดงผลลัพธ์
                Console.WriteLine($"\nSource image signed successfully with {result.Succeeded.Count} signature(s).");
                Console.WriteLine($"File saved at {outputFilePath}.");
            }
        }
    }
}
```

## เทคนิคการลงนามข้อมูลเมตาขั้นสูง

### การทำงานกับข้อมูลเมตาที่กำหนดเอง

คุณสามารถสร้างฟิลด์เมตาข้อมูลที่กำหนดเองด้วย ID เฉพาะได้:

```csharp
// สร้างข้อมูลเมตาที่กำหนดเองด้วย ID เฉพาะ
options.Add(new ImageMetadataSignature(42000, "CustomValue"));
```

### การตรวจสอบลายเซ็นข้อมูลเมตา

หลังจากลงนามแล้ว คุณอาจต้องการตรวจสอบลายเซ็นข้อมูลเมตา:

```csharp
// สร้างตัวเลือกการตรวจสอบ
MetadataSearchOptions searchOptions = new MetadataSearchOptions();

// ค้นหาลายเซ็นข้อมูลเมตา
SearchResult result = signature.Search(searchOptions);

// แสดงลายเซ็นที่พบ
Console.WriteLine($"Found {result.Signatures.Count} metadata signatures:");
foreach(var metadataSignature in result.Signatures)
{
    Console.WriteLine($"- {metadataSignature.Name}: {metadataSignature.Value}");
}
```

## บทสรุป

ในบทช่วยสอนนี้ คุณได้เรียนรู้วิธีการลงนามรูปภาพด้วยข้อมูลเมตาโดยใช้ GroupDocs.Signature สำหรับ .NET การฝังข้อมูลเมตาลงในรูปภาพเป็นวิธีที่ยอดเยี่ยมในการเพิ่มความน่าเชื่อถือของรูปภาพ เพิ่มข้อมูลสำคัญ และปรับปรุงเวิร์กโฟลว์การจัดการเอกสาร กระบวนการนี้ตรงไปตรงมาแต่ทรงพลัง ช่วยให้สามารถปรับแต่งตามความต้องการเฉพาะของคุณได้

เมตาดาต้าที่ฝังอยู่ในไฟล์ภาพสามารถนำไปใช้ประโยชน์ได้หลากหลาย เช่น การคุ้มครองลิขสิทธิ์ การติดตามแหล่งที่มาของภาพ การเพิ่มข้อมูลเชิงบรรยาย และการสร้างห่วงโซ่อุปทานดิจิทัล การใช้ลายเซ็นเมตาดาต้าจะช่วยให้คุณมั่นใจได้ว่ารูปภาพของคุณจะคงความสมบูรณ์และความถูกต้องตลอดวงจรชีวิตของภาพ

## คำถามที่พบบ่อย

### ฉันสามารถเพิ่มข้อมูลเมตาลงในรูปภาพที่ลงนามที่มีอยู่ได้หรือไม่

ใช่ คุณสามารถเพิ่มเมตาดาต้าเพิ่มเติมลงในรูปภาพที่มีลายเซ็นเมตาดาต้าอยู่แล้วได้ เมตาดาต้าที่มีอยู่จะถูกเก็บรักษาไว้ และเมตาดาต้าใหม่จะถูกเพิ่มเข้าไปตามนั้น

### รูปแบบภาพใดบ้างที่ได้รับการรองรับสำหรับการลงนามเมตาข้อมูล?

GroupDocs.Signature สำหรับ .NET รองรับการลงนามเมตาดาต้าสำหรับรูปแบบภาพต่างๆ รวมถึง PNG, JPEG, TIFF, BMP, GIF และอื่นๆ สำหรับรายการทั้งหมด โปรดดูที่ [เอกสารอย่างเป็นทางการ](https://docs-groupdocs.com/signature/net/).

### สามารถเข้ารหัสข้อมูลเมตาในภาพได้หรือไม่

ใช่ GroupDocs.Signature มีตัวเลือกสำหรับการเข้ารหัสข้อมูลเมตาเพื่อเพิ่มความปลอดภัย คุณสามารถใช้ตัวเลือกการเข้ารหัสที่ไลบรารีจัดเตรียมไว้เพื่อปกป้องข้อมูลเมตาที่ละเอียดอ่อนได้

### ฉันสามารถตรวจสอบความถูกต้องของรูปภาพที่ลงนามโดยใช้โปรแกรมได้หรือไม่

แน่นอน คุณสามารถใช้วิธีการตรวจสอบใน GroupDocs.Signature เพื่อตรวจสอบลายเซ็นเมตาดาต้าและยืนยันความถูกต้องของรูปภาพที่ลงนามได้

### มีข้อจำกัดขนาดไฟล์เมื่อลงนามรูปภาพที่มีข้อมูลเมตาหรือไม่

ไลบรารีไม่ได้กำหนดขนาดไฟล์ที่เจาะจง แต่ไฟล์ขนาดใหญ่มากอาจต้องใช้เวลาประมวลผลและหน่วยความจำมากขึ้น ขอแนะนำให้คำนึงถึงทรัพยากรระบบเมื่อทำงานกับรูปภาพขนาดใหญ่มาก

### ฉันจะได้รับใบอนุญาตชั่วคราวเพื่อวัตถุประสงค์การทดสอบได้อย่างไร

คุณสามารถรับได้ [ใบอนุญาตชั่วคราว](https://purchase.groupdocs.com/temporary-license/) เพื่อทดสอบ GroupDocs.Signature ก่อนตัดสินใจซื้อ

### ฉันสามารถหาทรัพยากรและการสนับสนุนเพิ่มเติมได้ที่ไหน

- [ข้อมูลอ้างอิง API](https://reference.groupdocs.com/signature/net/)
- [ดาวน์โหลด](https://releases.groupdocs.com/signature/net/)
- [ตัวอย่าง](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
- [เอกสารประกอบ](https://docs.groupdocs.com/signature/net/)
- [หน้าผลิตภัณฑ์](https://products.groupdocs.com/signature/net/)
- [บล็อก](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
- [ฟอรั่มสนับสนุน](https://forum.groupdocs.com/c/signature/13)