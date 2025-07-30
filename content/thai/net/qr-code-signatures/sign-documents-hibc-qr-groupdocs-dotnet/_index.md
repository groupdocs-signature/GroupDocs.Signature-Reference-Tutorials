---
"date": "2025-05-07"
"description": "เรียนรู้วิธีลงนามในเอกสาร PDF ด้วยรหัส QR ของ HIBC โดยใช้ GroupDocs.Signature สำหรับ .NET คู่มือนี้ครอบคลุมรหัส LIC และ PAS รวมถึงรหัส QR, Aztec Code และ DataMatrix"
"title": "วิธีการลงนามในเอกสารด้วยรหัส QR ของ HIBC โดยใช้ GroupDocs.Signature สำหรับ .NET คู่มือฉบับสมบูรณ์"
"url": "/th/net/qr-code-signatures/sign-documents-hibc-qr-groupdocs-dotnet/"
"weight": 1
---

# วิธีการลงนามในเอกสารด้วยรหัส QR ของ HIBC โดยใช้ GroupDocs.Signature สำหรับ .NET

## การแนะนำ

ในสภาพแวดล้อมทางธุรกิจที่เปลี่ยนแปลงอย่างรวดเร็วในปัจจุบัน การรับรองความถูกต้องและความสมบูรณ์ของเอกสารถือเป็นสิ่งสำคัญยิ่ง ไม่ว่าคุณจะจัดการกับยา ผลิตภัณฑ์ดูแลสุขภาพ หรือโลจิสติกส์ การมีวิธีการลงนามและติดตามเอกสารที่ปลอดภัยจะช่วยประหยัดเวลาและป้องกันข้อผิดพลาดได้ ป้อน **GroupDocs.Signature สำหรับ .NET**ไลบรารีอันทรงพลังที่ออกแบบมาเพื่อปรับปรุงกระบวนการจัดการเอกสารโดยเปิดใช้งานการผสานรวมรหัส QR ของ HIBC เข้ากับเอกสารของคุณได้อย่างราบรื่น

ในบทช่วยสอนนี้ เราจะสำรวจว่าคุณสามารถใช้ GroupDocs.Signature สำหรับ .NET เพื่อลงนามในเอกสาร PDF ด้วยรหัส QR HIBC หลากหลายประเภท ได้แก่ LIC (License) และ PAS (Product Authentication System) ซึ่งรวมถึง QR Code, Aztec Code และ DataMatrix ได้อย่างไร เมื่อจบบทนี้ คุณจะมีความเข้าใจอย่างถ่องแท้เกี่ยวกับการนำโซลูชันเหล่านี้ไปใช้งานในแอปพลิเคชัน .NET ของคุณ

**สิ่งที่คุณจะได้เรียนรู้:**
- วิธีตั้งค่า GroupDocs.Signature สำหรับ .NET
- การนำรหัส QR ของ HIBC LIC, รหัส Aztec และ DataMatrix มาใช้
- การเพิ่มรหัส QR ของ HIBC PAS, รหัส Aztec และ DataMatrix
- กรณีการใช้งานจริงและความเป็นไปได้ในการบูรณาการ

มาเจาะลึกข้อกำหนดเบื้องต้นก่อนที่เราจะเริ่มนำฟีเจอร์เหล่านี้ไปใช้

## ข้อกำหนดเบื้องต้น

ก่อนที่เราจะเริ่มเขียนโค้ด ให้แน่ใจว่าคุณมีสิ่งต่อไปนี้:

- **สภาพแวดล้อม .NET**: ตรวจสอบให้แน่ใจว่าคุณได้ติดตั้ง .NET ไว้ในระบบของคุณแล้ว (ควรเป็น .NET Core หรือ .NET 5/6+)
- **GroupDocs.Signature สำหรับ .NET**:ไลบรารีนี้จะเป็นเครื่องมือหลักของเรา คุณสามารถติดตั้งได้ผ่าน NuGet
- **ความรู้พื้นฐานด้านการเขียนโปรแกรม**: ขอแนะนำให้มีความคุ้นเคยกับ C# และการจัดการไฟล์ใน .NET

### ห้องสมุดที่จำเป็น

ในการใช้ GroupDocs.Signature สำหรับ .NET คุณจะต้องเพิ่มแพ็คเกจโดยใช้หนึ่งในวิธีต่อไปนี้:

**.NET CLI**
```bash
dotnet add package GroupDocs.Signature
```

**ตัวจัดการแพ็คเกจ**
```powershell
Install-Package GroupDocs.Signature
```

**UI ตัวจัดการแพ็คเกจ NuGet**
ค้นหา "GroupDocs.Signature" และติดตั้งเวอร์ชันล่าสุด

### การได้มาซึ่งใบอนุญาต

เพื่อวัตถุประสงค์ในการทดสอบ คุณสามารถขอรับใบอนุญาตทดลองใช้ฟรีได้ สำหรับการใช้งานเพิ่มเติม โปรดพิจารณาซื้อการสมัครสมาชิกหรือขอใบอนุญาตชั่วคราว:

- **ทดลองใช้ฟรี**: เข้าถึง [ที่นี่](https://releases.groupdocs.com/signature/net/)
- **ใบอนุญาตชั่วคราว**: ขอได้ที่ [ลิงค์นี้](https://purchase.groupdocs.com/temporary-license/)

### การตั้งค่าสภาพแวดล้อม

ตั้งค่าสภาพแวดล้อมของคุณโดยตรวจสอบให้แน่ใจว่าโครงการของคุณกำหนดเป้าหมายเป็นเวอร์ชัน .NET ที่เหมาะสม และสามารถเข้าถึง GroupDocs.Signature ได้ ตั้งค่าเริ่มต้นในแอปพลิเคชันของคุณดังที่แสดง:

```csharp
using GroupDocs.Signature;
```

## การตั้งค่า GroupDocs.Signature สำหรับ .NET

หากต้องการเริ่มใช้ GroupDocs.Signature สำหรับ .NET คุณจะต้องติดตั้งไลบรารีและกำหนดค่าการตั้งค่าพื้นฐานภายในโครงการของคุณ

### การติดตั้ง

ทำตามวิธีใดวิธีหนึ่งที่กล่าวถึงข้างต้นเพื่อเพิ่ม GroupDocs.Signature ลงในโปรเจกต์ของคุณ เมื่อติดตั้งแล้ว โปรดตรวจสอบให้แน่ใจว่าโปรเจกต์ของคุณได้รับการกำหนดค่าให้ใช้งาน GroupDocs.Signature โดยอ้างอิงถึงไฟล์โค้ดของคุณ

### การเริ่มต้นใบอนุญาต

หลังจากได้รับใบอนุญาตแล้ว ให้ตั้งค่าเริ่มต้นดังต่อไปนี้:

```csharp
SignatureConfig signConfig = new SignatureConfig();
signConfig.LicensePath = "path/to/your/license.lic";
Signature signature = new Signature("Sample.pdf", signConfig);
```

การตั้งค่านี้จะช่วยให้คุณสามารถเข้าถึงฟีเจอร์ทั้งหมดของ GroupDocs.Signature โดยไม่มีข้อจำกัด

## คู่มือการใช้งาน

ตอนนี้เรามาดูการใช้งานฟีเจอร์แต่ละอย่างโดยใช้รหัส QR ของ HIBC กับ GroupDocs.Signature สำหรับ .NET กัน

### ลงนามเอกสารด้วยรหัส QR ของ HIBC LIC

#### ภาพรวม

การลงนามในเอกสารด้วยรหัส QR ของ HIBC LIC ช่วยให้มั่นใจได้ถึงการปฏิบัติตามข้อกำหนดและการตรวจสอบย้อนกลับในสถานการณ์การออกใบอนุญาต ส่วนนี้จะแนะนำคุณเกี่ยวกับการสร้างและฝังรหัส QR ลงในเอกสาร PDF ของคุณ

#### ขั้นตอนการดำเนินการ

##### ขั้นตอนที่ 1: กำหนดค่าเส้นทางต้นทางและปลายทาง

กำหนดว่าเอกสารต้นฉบับของคุณอยู่ที่ใด และควรบันทึกเอาต์พุตที่ลงนามไว้ที่ใด:

```csharp
string sourceFilePath = Path.Combine("YOUR_DOCUMENT_DIRECTORY", "Sample.pdf");
string outputPath = Path.Combine("YOUR_OUTPUT_DIRECTORY", "SignWithHIBCLICQR");
string destinFilePath = Path.Combine(outputPath, "SignedDocumentWithHIBCLICQR.pdf");
```

##### ขั้นตอนที่ 2: สร้างตัวเลือกการลงชื่อ QR Code

กำหนดค่ารหัส QR ของคุณด้วยข้อความและการตั้งค่าเฉพาะ:

```csharp
using (Signature signature = new Signature(sourceFilePath))
{
    var hibcLic_QR_Options = new QrCodeSignOptions("A123PROD30917/75#422011907#GP293", QrCodeTypes.HIBCLICQR)
    {
        Left = 1,
        Top = 1,
        ReturnContent = true,
        ReturnContentType = FileType.PNG
    };

    // ลงนามในเอกสารด้วยตัวเลือกเหล่านี้
    signature.Sign(destinFilePath, hibcLic_QR_Options);
}
```

**คำอธิบาย**- 
- `QrCodeSignOptions` ตั้งค่าลักษณะและเนื้อหาของรหัส QR ที่นี่ เราจะระบุประเภทรหัส QR ของ HIBC LIC และวางไว้ในเอกสาร
- `ReturnContent` ตั้งค่าเป็นจริงช่วยให้คุณสามารถดึงภาพที่แสดงผลของเอกสารที่ลงนามได้

#### เคล็ดลับการแก้ไขปัญหา

- ตรวจสอบให้แน่ใจว่าเส้นทางเอกสารได้รับการระบุอย่างถูกต้อง
- ตรวจสอบว่า GroupDocs.Signature ได้รับอนุญาตการใช้งานอย่างถูกต้องเพื่อให้ใช้งานได้เต็มรูปแบบ

### ลงนามในเอกสารด้วยรหัส Aztec ของ HIBC LIC

#### ภาพรวม

รหัสแอซเท็กนำเสนอรูปแบบการเข้ารหัสอีกรูปแบบหนึ่ง ซึ่งเหมาะสำหรับการจัดเก็บข้อมูลความหนาแน่นสูง หัวข้อนี้เน้นการฝังรหัสแอซเท็กลงในเอกสารของคุณโดยใช้ GroupDocs.Signature

#### ขั้นตอนการดำเนินการ

##### ขั้นตอนที่ 1: กำหนดค่าเส้นทาง

คล้ายกับฟีเจอร์ก่อนหน้านี้ กำหนดเส้นทางไฟล์ของคุณ:

```csharp
string sourceFilePath = Path.Combine("YOUR_DOCUMENT_DIRECTORY", "Sample.pdf");
string outputPath = Path.Combine("YOUR_OUTPUT_DIRECTORY", "SignWithHIBCLICAztec");
string destinFilePath = Path.Combine(outputPath, "SignedDocumentWithHIBCLICAztec.pdf");
```

##### ขั้นตอนที่ 2: กำหนดค่าตัวเลือก Aztec Code

ตั้งค่ารหัส Aztec ของคุณโดยใช้ GroupDocs.Signature:

```csharp
using (Signature signature = new Signature(sourceFilePath))
{
    var hibcLic_AZ_Options = new QrCodeSignOptions("A123PROD30917/75#422011907#GP293", QrCodeTypes.HIBCLICAztec)
    {
        Left = 1,
        Top = 200,
        ReturnContent = true,
        ReturnContentType = FileType.PNG
    };

    signature.Sign(destinFilePath, hibcLic_AZ_Options);
}
```

**คำอธิบาย**- 
- การ `QrCodeSignOptions` ถูกนำมาใช้ที่นี่อีกครั้งแต่กับประเภทรหัสแอซเท็ก
- การวางตำแหน่ง (`Top`- `Left`) และการตั้งค่าการดึงเนื้อหาจะคล้ายกับรหัส QR

#### เคล็ดลับการแก้ไขปัญหา

- ยืนยันว่าเส้นทางไฟล์ถูกต้อง
- ตรวจสอบให้แน่ใจว่าเวอร์ชัน GroupDocs.Signature รองรับประเภทรหัส Aztec

### ลงนามเอกสารด้วย HIBC LIC DataMatrix

#### ภาพรวม

โค้ด DataMatrix เป็นอีกหนึ่งวิธีที่มีประสิทธิภาพในการจัดเก็บข้อมูล ส่วนนี้จะสาธิตวิธีการผสาน DataMatrix เข้ากับเอกสาร PDF ของคุณ

#### ขั้นตอนการดำเนินการ

##### ขั้นตอนที่ 1: ตั้งค่าเส้นทางไฟล์

เช่นเดียวกับก่อนหน้านี้ ให้ระบุว่าไฟล์ของคุณอยู่ที่ไหน:

```csharp
string sourceFilePath = Path.Combine("YOUR_DOCUMENT_DIRECTORY", "Sample.pdf");
string outputPath = Path.Combine("YOUR_OUTPUT_DIRECTORY", "SignWithHIBCLICDataMatrix");
string destinFilePath = Path.Combine(outputPath, "SignedDocumentWithHIBCLICDataMatrix.pdf");
```

##### ขั้นตอนที่ 2: สร้างตัวเลือกเครื่องหมาย DataMatrix

กำหนดค่าและใช้โค้ด DataMatrix:

```csharp
using (Signature signature = new Signature(sourceFilePath))
{
    var hibcLic_DM_Options = new QrCodeSignOptions("A123PROD30917/75#422011907#GP293", QrCodeTypes.HIBCLICDataMatrix)
    {
        Left = 1,
        Top = 400,
        ReturnContent = true,
        ReturnContentType = FileType.PNG
    };

    signature.Sign(destinFilePath, hibcLic_DM_Options);
}
```

**คำอธิบาย**- 
- `QrCodeSignOptions` ใช้ในการตั้งค่าลักษณะและเนื้อหาของโค้ด DataMatrix
- การวางตำแหน่ง (`Top`- `Left`) และการตั้งค่าการเรียกค้นจะปฏิบัติตามรูปแบบเดียวกันกับโค้ดก่อนหน้า

#### เคล็ดลับการแก้ไขปัญหา

- ตรวจสอบให้แน่ใจว่าเส้นทางไฟล์ทั้งหมดได้รับการระบุอย่างถูกต้อง
- ตรวจสอบว่า GroupDocs.Signature รองรับประเภทรหัส DataMatrix ในเวอร์ชันของคุณ

### ลงนามในเอกสารด้วยรหัส QR ของ HIBC PAS

#### ภาพรวม

การลงนามในเอกสารด้วยรหัส QR ของ HIBC PAS ช่วยเพิ่มประสิทธิภาพในการติดตามและตรวจสอบย้อนกลับผลิตภัณฑ์ หัวข้อนี้จะแนะนำวิธีการฝังรหัส QR ของ PAS ลงในไฟล์ PDF โดยใช้ GroupDocs.Signature

#### ขั้นตอนการดำเนินการ

##### ขั้นตอนที่ 1: กำหนดค่าเส้นทางต้นทางและปลายทาง

กำหนดว่าเอกสารต้นฉบับของคุณอยู่ที่ใด และควรบันทึกเอาต์พุตที่ลงนามไว้ที่ใด:

```csharp
string sourceFilePath = Path.Combine("YOUR_DOCUMENT_DIRECTORY", "Sample.pdf");
string outputPath = Path.Combine("YOUR_OUTPUT_DIRECTORY", "SignWithHIBCPASQR");
string destinFilePath = Path.Combine(outputPath, "SignedDocumentWithHIBCPASQR.pdf");
```

##### ขั้นตอนที่ 2: สร้างตัวเลือกการลงชื่อ QR Code

กำหนดค่ารหัส QR PAS ของคุณด้วยข้อความและการตั้งค่าเฉพาะ:

```csharp
using (Signature signature = new Signature(sourceFilePath))
{
    var hibcPas_QR_Options = new QrCodeSignOptions("PAS123456789012", QrCodeTypes.HIBCPASQR)
    {
        Left = 1,
        Top = 500,
        ReturnContent = true,
        ReturnContentType = FileType.PNG
    };

    // ลงนามในเอกสารด้วยตัวเลือกเหล่านี้
    signature.Sign(destinFilePath, hibcPas_QR_Options);
}
```

**คำอธิบาย**- 
- `QrCodeSignOptions` ได้รับการกำหนดค่าสำหรับประเภท QR Code ของ HIBC PAS และวางไว้บนเอกสาร
- `ReturnContent` ตั้งค่าเป็นจริงเพื่อดึงภาพที่แสดงผลของเอกสารที่ลงนาม

#### เคล็ดลับการแก้ไขปัญหา

- ตรวจสอบให้แน่ใจว่าเส้นทางทั้งหมดได้รับการระบุอย่างถูกต้อง
- ตรวจสอบว่า GroupDocs.Signature รองรับประเภท PAS QR Code ในเวอร์ชันของคุณ

### บทสรุป

การปฏิบัติตามคู่มือนี้จะช่วยให้คุณผสานรวมรหัส QR ของ HIBC LIC และ PAS ลงในเอกสาร PDF ได้อย่างมีประสิทธิภาพโดยใช้ GroupDocs.Signature สำหรับ .NET กระบวนการนี้ช่วยเพิ่มความปลอดภัยของเอกสาร ความสามารถในการตรวจสอบย้อนกลับ และการปฏิบัติตามข้อกำหนดในหลากหลายอุตสาหกรรม สำหรับการปรับแต่งเพิ่มเติมและฟีเจอร์ขั้นสูง โปรดดูที่ [เอกสาร GroupDocs](https://docs-groupdocs.com/signature/net/).