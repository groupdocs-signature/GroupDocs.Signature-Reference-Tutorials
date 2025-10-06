---
"date": "2025-05-07"
"description": "เรียนรู้วิธีลงนาม ตรวจสอบ ค้นหา อัปเดต และลบลายเซ็นข้อความในเอกสารอย่างมีประสิทธิภาพด้วย GroupDocs.Signature สำหรับ .NET ปรับปรุงกระบวนการลงนามดิจิทัลของคุณวันนี้"
"title": "การลงนามและการยืนยันเอกสารหลักด้วย GroupDocs.Signature สำหรับ .NET"
"url": "/th/net/digital-signatures/master-document-signing-groupdocs-signature-net/"
"weight": 1
type: docs
---
# การลงนามและการยืนยันเอกสารหลักด้วย GroupDocs.Signature สำหรับ .NET

## วิธีการลงนามและยืนยันเอกสารอย่างเชี่ยวชาญด้วย GroupDocs.Signature สำหรับ .NET

ในโลกดิจิทัลปัจจุบัน โซลูชันการลงนามเอกสารที่มีประสิทธิภาพมีความสำคัญอย่างยิ่งต่อการจัดการสัญญา ข้อตกลง หรือเอกสารทางกฎหมายใดๆ การทำให้กระบวนการนี้เป็นระบบอัตโนมัติช่วยประหยัดเวลาและลดข้อผิดพลาด **GroupDocs.Signature สำหรับ .NET** นำเสนอโซลูชันอันทรงพลังเพื่อเพิ่มประสิทธิภาพการจัดการลายเซ็นข้อความในแอปพลิเคชันของคุณ คู่มือฉบับสมบูรณ์นี้จะแนะนำฟีเจอร์ต่างๆ ของ GroupDocs.Signature สำหรับ .NET รวมถึงการลงนาม การตรวจสอบ การค้นหา การอัปเดต และการลบลายเซ็นข้อความ

## สิ่งที่คุณจะได้เรียนรู้

- วิธีการลงนามเอกสารด้วยลายเซ็นข้อความที่ปรับแต่งได้
- เทคนิคการตรวจสอบเอกสารที่ลงนามอย่างมีประสิทธิภาพ
- วิธีการค้นหาลายเซ็นข้อความที่มีอยู่ในเอกสาร
- ขั้นตอนการอัปเดตและลบลายเซ็นข้อความตามต้องการ
- แนวทางปฏิบัติที่ดีที่สุดสำหรับการเพิ่มประสิทธิภาพการทำงานและการจัดการหน่วยความจำ

มาเริ่มกันด้วยการดูข้อกำหนดเบื้องต้นกันก่อน

## ข้อกำหนดเบื้องต้น

ก่อนที่คุณจะเริ่มต้น โปรดตรวจสอบให้แน่ใจว่าสภาพแวดล้อมการพัฒนาของคุณได้รับการตั้งค่าด้วยเครื่องมือที่จำเป็น:

### ไลบรารีและการอ้างอิงที่จำเป็น

- **GroupDocs.Signature สำหรับ .NET**:ไลบรารีนี้ช่วยให้คุณสามารถเพิ่มฟังก์ชันลายเซ็นในแอปพลิเคชันของคุณได้
- **.NET Framework 4.6.1 หรือสูงกว่า** (หรือ .NET Core 2.x+)

### ข้อกำหนดการตั้งค่าสภาพแวดล้อม

คุณจะต้องมีสภาพแวดล้อมการพัฒนา C# เช่น Visual Studio และการเชื่อมต่ออินเทอร์เน็ตเพื่อดาวน์โหลดแพ็คเกจที่จำเป็น

### ข้อกำหนดเบื้องต้นของความรู้

ขอแนะนำให้คุณคุ้นเคยกับแนวคิดการเขียนโปรแกรม C# ขั้นพื้นฐาน หากคุณยังใหม่กับ GroupDocs.Signature สำหรับ .NET ไม่ต้องกังวล เพราะคู่มือนี้จะแนะนำคุณทุกขั้นตอน

## การตั้งค่า GroupDocs.Signature สำหรับ .NET

ในการเริ่มต้น คุณจะต้องติดตั้งไลบรารี GroupDocs.Signature ในโปรเจ็กต์ของคุณ ทำตามขั้นตอนดังนี้:

### การติดตั้งผ่าน .NET CLI
```bash
dotnet add package GroupDocs.Signature
```

### คอนโซลตัวจัดการแพ็คเกจ
```powershell
Install-Package GroupDocs.Signature
```

### UI ตัวจัดการแพ็คเกจ NuGet
1. เปิดโปรเจ็กต์ของคุณใน Visual Studio
2. นำทางไปที่ **เครื่องมือ** - **ตัวจัดการแพ็กเกจ NuGet** - **จัดการแพ็กเกจ NuGet สำหรับโซลูชัน**-
3. ค้นหา "GroupDocs.Signature" และติดตั้งเวอร์ชันล่าสุด

#### ขั้นตอนการขอใบอนุญาต
- **ทดลองใช้ฟรี**:เริ่มต้นด้วยการทดลองใช้ฟรีโดยดาวน์โหลดจาก [ทดลองใช้ GroupDocs ฟรี](https://releases-groupdocs.com/signature/net/).
- **ใบอนุญาตชั่วคราว**:รับใบอนุญาตชั่วคราวเพื่อประเมินคุณสมบัติเต็มรูปแบบได้ที่ [ใบอนุญาตชั่วคราว](https://purchase-groupdocs.com/temporary-license/).
- **ซื้อ**:เพื่อการใช้งานต่อเนื่อง กรุณาซื้อใบอนุญาตจาก [หน้าการซื้อ GroupDocs](https://purchase-groupdocs.com/buy).

#### การเริ่มต้นและการตั้งค่าขั้นพื้นฐาน

หลังจากการติดตั้ง ให้เริ่มต้น GroupDocs.Signature ในโครงการของคุณดังต่อไปนี้:

```csharp
using GroupDocs.Signature;

// เริ่มต้นอินสแตนซ์ลายเซ็นด้วยเส้นทางเอกสาร
Signature signature = new Signature("path/to/your/document.pdf");
```

ตอนนี้คุณตั้งค่าเรียบร้อยแล้ว เรามาดูวิธีใช้ประโยชน์จาก GroupDocs.Signature สำหรับฟังก์ชันต่างๆ กัน

## คู่มือการใช้งาน

### ลงนามเอกสารพร้อมลายเซ็นข้อความ

ฟีเจอร์นี้ช่วยให้คุณเพิ่มลายเซ็นข้อความลงในเอกสารได้ ลองมาดูกัน:

#### ภาพรวม
คุณสามารถปรับแต่งลักษณะและตำแหน่งของลายเซ็นข้อความของคุณได้โดยใช้ตัวเลือกต่างๆ เช่น ขนาดตัวอักษร สี การจัดตำแหน่ง ฯลฯ

#### การดำเนินการแบบทีละขั้นตอน

**ขั้นตอนที่ 1**: กำหนดเส้นทางไฟล์และตำแหน่งเอาต์พุต
```csharp
string filePath = "YOUR_DOCUMENT_DIRECTORY"; // เส้นทางไปยังเอกสารต้นฉบับ
string outputFilePath = Path.Combine("YOUR_OUTPUT_DIRECTORY", "SignedDocument.docx");
```

**ขั้นตอนที่ 2**: สร้างลายเซ็นข้อความโดยใช้ `TextSignOptions`-
```csharp
using (Signature signature = new Signature(filePath))
{
    TextSignOptions signOptions = new TextSignOptions("John Smith")
    {
        VerticalAlignment = GroupDocs.Signature.Options.VerticalAlignment.Top,
        HorizontalAlignment = GroupDocs.Signature.Options.HorizontalAlignment.Center,
        Width = 100,
        Height = 40,
        Margin = new Padding(20),
        ForeColor = Color.Red,
        Font = new SignatureFont { Size = 12, FamilyName = "Comic Sans MS" }
    };
```

**ขั้นตอนที่ 3**:ลงนามในเอกสารและออกผลลัพธ์
```csharp
    SignResult signResult = signature.Sign(outputFilePath, signOptions);
    foreach (BaseSignature temp in signResult.Succeeded)
    {
        Console.WriteLine($"Signed Text Signature: Id:{temp.SignatureId}, Location: {temp.Left}x{temp.Top}. Size: {temp.Width}x{temp.Height}");
    }
}
```

#### ตัวเลือกการกำหนดค่าคีย์
- **การจัดแนวแนวตั้งและการจัดแนวแนวนอน**ควบคุมว่าลายเซ็นจะปรากฏบนหน้าไหน
- **แบบอักษร**:ปรับแต่งขนาดและรูปแบบตัวอักษรสำหรับลายเซ็นข้อความของคุณ

### ตรวจสอบเอกสารสำหรับลายเซ็นข้อความ

การตรวจสอบช่วยให้มั่นใจว่าเอกสารได้รับการลงนามตามที่ตั้งใจไว้ ต่อไปนี้คือวิธีการดำเนินการ:

#### ภาพรวม
ตรวจสอบลายเซ็นข้อความที่มีอยู่ในเอกสารของคุณเพื่อยืนยันความถูกต้องและความสมบูรณ์

#### การดำเนินการแบบทีละขั้นตอน

**ขั้นตอนที่ 1**: ระบุเส้นทางไฟล์ของเอกสารที่ลงนาม
```csharp
string filePath = "YOUR_OUTPUT_DIRECTORY"; // เส้นทางไปยังเอกสารที่ลงนาม
```

**ขั้นตอนที่ 2**: สร้างตัวเลือกการตรวจสอบโดยใช้ `TextVerifyOptions`-
```csharp
using (Signature signature = new Signature(filePath))
{
    TextVerifyOptions verifyOptions = new TextVerifyOptions()
    {
        AllPages = false,
        PageNumber = 1,
        Text = "John Smith",
        MatchType = GroupDocs.Signature.Options.TextMatchType.Exact
    };
```

**ขั้นตอนที่ 3**: ตรวจสอบเอกสาร.
```csharp
    VerificationResult verifyResult = signature.Verify(verifyOptions);
    if (verifyResult.IsValid)
    {
        Console.WriteLine("Document was verified successfully!");
    }
    else
    {
        Console.WriteLine("Document failed verification process.");
    }
}
```

#### เคล็ดลับการแก้ไขปัญหา
- ให้แน่ใจว่า `Text` คุณสมบัติตรงกับสิ่งที่อยู่ในเอกสารอย่างแน่นอน
- ตรวจสอบว่า `PageNumber` ตรงตามหน้าที่มีลายเซ็นถูกต้อง

### ค้นหาเอกสารสำหรับลายเซ็นข้อความ

ค้นหาลายเซ็นข้อความภายในเอกสารของคุณอย่างมีประสิทธิภาพโดยใช้ฟีเจอร์นี้

#### ภาพรวม
ค้นหาผ่านหน้าทั้งหมดหรือที่เลือกของเอกสารเพื่อค้นหาลายเซ็นข้อความที่ต้องการ

#### การดำเนินการแบบทีละขั้นตอน

**ขั้นตอนที่ 1**: กำหนดเส้นทางของไฟล์
```csharp
string filePath = "YOUR_OUTPUT_DIRECTORY"; // เส้นทางไปยังเอกสารที่ลงนาม
```

**ขั้นตอนที่ 2**: ใช้ `TextSearchOptions` เพื่อการค้นหา
```csharp
using (Signature signature = new Signature(filePath))
{
    TextSearchOptions searchOptions = new TextSearchOptions()
    {
        AllPages = true,
        MatchType = GroupDocs.Signature.Options.TextMatchType.Exact,
        Text = "John Smith"
    };
```

**ขั้นตอนที่ 3**: ดำเนินการค้นหา
```csharp
    List<TextSignature> signatures = signature.Search<TextSignature>(searchOptions);
    foreach (TextSignature textSignature in signatures)
    {
        if (textSignature != null)
        {
            Console.WriteLine($"Found Text signature at page {textSignature.PageNumber} with type [{textSignature.SignatureImplementation}] and text '{textSignature.Text}'. Location: {textSignature.Left}-{textSignature.Top}. Size is {textSignature.Width}x{textSignature.Height}.");
        }
    }
}
```

### อัปเดตลายเซ็นข้อความเอกสาร

แก้ไขลายเซ็นข้อความที่มีอยู่ในเอกสารเมื่อจำเป็น

#### ภาพรวม
ปรับแต่งคุณสมบัติของลายเซ็นข้อความที่มีอยู่ เช่น ขนาดและตำแหน่ง

#### การดำเนินการแบบทีละขั้นตอน

**ขั้นตอนที่ 1**: ระบุเส้นทางไฟล์และ ID ลายเซ็น
```csharp
string filePath = "YOUR_OUTPUT_DIRECTORY"; // เส้นทางไปยังเอกสารที่ลงนาม
List<string> signatureIds = new List<string>(); // ถือว่ารายการนี้ถูกเติมด้วย ID ลายเซ็นที่ถูกต้อง
```

**ขั้นตอนที่ 2**: สร้าง `TextSignature` วัตถุสำหรับการอัปเดต
```csharp
using (Signature signature = new Signature(filePath))
{
    foreach (var item in signatureIds)
    {
        TextSignature temp = new TextSignature(item)
        {
            Width = 150,
            Height = 50,
            HorizontalAlignment = GroupDocs.Signature.Options.HorizontalAlignment.Right
        };
```

**ขั้นตอนที่ 3**: อัปเดตเอกสาร
```csharp
        SignResult signResult = signature.UpdateSignatures(temp);
        if (signResult.Succeeded.Count > 0)
        {
            Console.WriteLine($"Updated Text Signature: Id:{temp.SignatureId}");
        }
    }
}
```

#### ตัวเลือกการกำหนดค่าคีย์
- **ความกว้างและความสูง**: ปรับขนาดลายเซ็น
- **การจัดแนวแนวนอน**: ควบคุมว่าลายเซ็นที่อัปเดตจะปรากฏบนเพจอย่างไร

## บทสรุป

เมื่อทำตามคำแนะนำนี้ คุณจะได้เรียนรู้วิธีลงนาม ตรวจสอบ ค้นหา อัปเดต และลบลายเซ็นข้อความในเอกสารโดยใช้ GroupDocs.Signature สำหรับ .NET ความสามารถเหล่านี้จำเป็นสำหรับการทำให้กระบวนการลงนามดิจิทัลเป็นอัตโนมัติในแอปพลิเคชันของคุณ สำหรับข้อมูลเพิ่มเติมโดยละเอียดและตัวเลือกขั้นสูง โปรดดูที่ [เอกสารอย่างเป็นทางการ](https://docs-groupdocs.com/signature/net/).