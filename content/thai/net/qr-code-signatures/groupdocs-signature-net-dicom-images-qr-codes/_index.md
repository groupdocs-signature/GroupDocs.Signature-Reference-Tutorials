---
"date": "2025-05-07"
"description": "เรียนรู้วิธีการลงนามภาพ DICOM ด้วยรหัส QR โดยใช้ GroupDocs.Signature สำหรับ .NET คู่มือนี้ครอบคลุมการตั้งค่า การนำไปใช้งาน และการตรวจสอบลายเซ็น QR code ในระบบถ่ายภาพทางการแพทย์"
"title": "วิธีการลงนามภาพ DICOM ด้วยรหัส QR โดยใช้ GroupDocs.Signature สำหรับ .NET คู่มือฉบับสมบูรณ์"
"url": "/th/net/qr-code-signatures/groupdocs-signature-net-dicom-images-qr-codes/"
"weight": 1
type: docs
---
# วิธีการลงนามภาพ DICOM ด้วยรหัส QR โดยใช้ GroupDocs.Signature สำหรับ .NET: คู่มือที่ครอบคลุม

คุณกำลังมองหาวิธีที่ปลอดภัยในการตรวจสอบสิทธิ์ไฟล์ DICOM ของคุณอยู่ใช่ไหม? คู่มือโดยละเอียดนี้จะแสดงวิธีใช้ GroupDocs.Signature สำหรับ .NET เพื่อผสานลายเซ็น QR Code เข้ากับรูปภาพ DICOM เหมาะสำหรับบุคลากรทางการแพทย์ นักพัฒนา และผู้ที่ทำงานกับเอกสารทางการแพทย์ดิจิทัล บทช่วยสอนนี้ครอบคลุมตั้งแต่การตั้งค่าไปจนถึงการใช้งานจริง

## สิ่งที่คุณจะได้เรียนรู้:
- การตั้งค่าสภาพแวดล้อมการพัฒนาของคุณด้วย GroupDocs.Signature สำหรับ .NET
- คำแนะนำทีละขั้นตอนในการลงนามภาพ DICOM โดยใช้รหัส QR
- วิธีการตรวจสอบและค้นหาลายเซ็นรหัส QR ในไฟล์ DICOM
- เทคนิคการสร้างตัวอย่างเอกสารที่ลงนามเพื่อจุดประสงค์ในการตรวจสอบ
- แนวทางปฏิบัติที่ดีที่สุดสำหรับการเพิ่มประสิทธิภาพการทำงานและการจัดการทรัพยากรอย่างมีประสิทธิผล

มาเริ่มกันด้วยข้อกำหนดเบื้องต้นก่อนเลยดีกว่า!

## ข้อกำหนดเบื้องต้น

ในการใช้ GroupDocs.Signature สำหรับ .NET โปรดตรวจสอบให้แน่ใจว่าสภาพแวดล้อมของคุณพร้อมใช้งานแล้ว นี่คือสิ่งที่คุณต้องมี:

### ไลบรารีและเวอร์ชันที่จำเป็น
- **GroupDocs.Signature สำหรับ .NET**:ให้แน่ใจว่ามีความเข้ากันได้กับกรอบงาน .NET ของคุณ

### ข้อกำหนดการตั้งค่าสภาพแวดล้อม
- สภาพแวดล้อมการพัฒนาบน Windows หรือ Linux
- มีการติดตั้ง Visual Studio หรือ IDE อื่นที่เข้ากันได้กับ .NET

### ข้อกำหนดเบื้องต้นของความรู้
- ความเข้าใจพื้นฐานเกี่ยวกับการเขียนโปรแกรม C#
- ความคุ้นเคยกับไฟล์ I/O ในแอปพลิเคชัน .NET

## การตั้งค่า GroupDocs.Signature สำหรับ .NET

ติดตั้งไลบรารี GroupDocs.Signature โดยใช้วิธีการที่คุณต้องการ:

**การใช้ .NET CLI:**
```bash
dotnet add package GroupDocs.Signature
```

**ตัวจัดการแพ็คเกจ:**
```powershell
Install-Package GroupDocs.Signature
```

**UI ตัวจัดการแพ็กเกจ NuGet:**
- ค้นหา "GroupDocs.Signature" และติดตั้งเวอร์ชันล่าสุด

### การได้มาซึ่งใบอนุญาต

เริ่มต้นด้วยการทดลองใช้ฟรีเพื่อสำรวจความสามารถต่างๆ สำหรับการใช้งานแบบขยายเวลา โปรดพิจารณาซื้อใบอนุญาตชั่วคราวหรือใบอนุญาตฉบับเต็มจาก [เอกสารกลุ่ม](https://purchase-groupdocs.com/buy).

เมื่อติดตั้งแล้ว ให้เริ่มต้นไลบรารี:

```csharp
using GroupDocs.Signature;
// เริ่มต้นวัตถุลายเซ็นด้วยเส้นทางไฟล์ DICOM ของคุณ
Signature signature = new Signature("YOUR_DOCUMENT_DIRECTORY\\sample.dicom");
```

## คู่มือการใช้งาน

### ลงชื่อภาพ DICOM ด้วยรหัส QR

#### ภาพรวม
เพิ่มลายเซ็น QR Code เพื่อรับรองความถูกต้องและสามารถตรวจสอบย้อนกลับของเอกสารทางการแพทย์ได้

**ขั้นตอนที่ 1: เริ่มต้นวัตถุลายเซ็น**

```csharp
string filePath = "YOUR_DOCUMENT_DIRECTORY\\sample.dicom";
using (Signature signature = new Signature(filePath))
{
    // ดำเนินการลงนามต่อไป...
}
```

**ขั้นตอนที่ 2: สร้างตัวเลือกการลงชื่อ QR Code**

กำหนดค่าคุณสมบัติเช่นข้อความ ขนาด และการจัดตำแหน่ง

```csharp
QrCodeSignOptions options = new QrCodeSignOptions("Patient #36363393. R: No-Issues")
{
    AllPages = true,
    Width = 100,
    Height = 100,
    VerticalAlignment = VerticalAlignment.Bottom,
    HorizontalAlignment = HorizontalAlignment.Right,
    Margin = new Padding() { Right = 5, Left = 5 }
};
```

**ขั้นตอนที่ 3: เพิ่มข้อมูลเมตา XMP**

ปรับปรุงเอกสารด้วยข้อมูลเมตาเพิ่มเติม

```csharp
DicomSaveOptions dicomSaveOptions = new DicomSaveOptions()
{
    XmpEntries = new List<DicomXmpEntry>() { new DicomXmpEntry(DicomXmpType.PatientName, "Patient #4") }
};
```

**ขั้นตอนที่ 4: ลงนามในเอกสาร**

ดำเนินการลงนามและบันทึก

```csharp
SignResult signResult = signature.Sign("YOUR_OUTPUT_DIRECTORY\\SignedDicom", options, dicomSaveOptions);
```

### รับข้อมูลเอกสาร

ดึงข้อมูลเมตาจากไฟล์ DICOM ที่ลงนามเพื่อให้แน่ใจว่าข้อมูลมีความสมบูรณ์

**ภาพรวม:**
เข้าถึงข้อมูลเอกสารและลายเซ็นเมตาข้อมูล XMP เพื่อการตรวจยืนยัน

**ขั้นตอนที่ 1: ดึงข้อมูลเอกสาร**

```csharp
using (Signature signature = new Signature("YOUR_DOCUMENT_DIRECTORY\\sample_signed.dicom"))
{
    IDocumentInfo signedDocumentInfo = signature.GetDocumentInfo();
}
```

**ขั้นตอนที่ 2: ทำซ้ำและพิมพ์ข้อมูล XMP**

แสดงรายละเอียดข้อมูลเมตา

```csharp
foreach (var item in signedDocumentInfo.MetadataSignatures)
{
    Console.WriteLine(item.ToString());
}
```

### ตรวจสอบลายเซ็น DICOM

ตรวจสอบความถูกต้องของลายเซ็นรหัส QR ภายในภาพ DICOM

**ภาพรวม:**
ตรวจสอบให้แน่ใจว่าลายเซ็นถูกต้องและแท้จริง

**ขั้นตอนที่ 1: สร้างตัวเลือกการยืนยันรหัส QR**

ตั้งค่าตัวเลือกที่ตรงกับข้อความเฉพาะในรหัส QR

```csharp
QrCodeVerifyOptions options = new QrCodeVerifyOptions()
{
    AllPages = true,
    Text = "Patient #36363393",
    MatchType = TextMatchType.Contains
};
```

**ขั้นตอนที่ 2: ตรวจสอบลายเซ็น**

ตรวจสอบว่าลายเซ็นตรงตามเกณฑ์หรือไม่

```csharp
VerificationResult result = signature.Verify(options);

if (result.IsValid)
{
    Console.WriteLine($"DICOM {filePath} has {result.Succeeded.Count} successfully verified signatures!");
}
```

### ค้นหาลายเซ็นใน DICOM

ค้นหาลายเซ็นโค้ด QR ภายในภาพ DICOM ที่ลงนามแล้ว

**ภาพรวม:**
ค้นหาลายเซ็น QR code ทั้งหมดอย่างมีประสิทธิภาพเพื่อจัดการความถูกต้องของเอกสาร

**ขั้นตอนที่ 1: ค้นหาลายเซ็น QR Code**

```csharp
List<QrCodeSignature> signatures = signature.Search<QrCodeSignature>(SignatureType.QrCode);
```

**ขั้นตอนที่ 2: ทำซ้ำและพิมพ์รายละเอียดลายเซ็น**

ตรวจสอบรายละเอียดลายเซ็นที่พบแต่ละรายการ

```csharp
foreach (var QrCodeSignature in signatures)
{
    Console.WriteLine($"QRCode signature found at page {QrCodeSignature.PageNumber} with type {QrCodeSignature.EncodeType.TypeName} and text {QrCodeSignature.Text}");
}
```

### สร้างตัวอย่างของ DICOM ที่ลงนาม

สร้างการแสดงตัวอย่างภาพเพื่อการตรวจยืนยัน

**ภาพรวม:**
สร้างภาพตัวอย่างเพื่อตรวจสอบเนื้อหาโดยไม่ต้องใช้ซอฟต์แวร์เฉพาะทาง

**ขั้นตอนที่ 1: กำหนดวิธีการสตรีม**

ตั้งค่าวิธีการจัดการสตรีมไฟล์ในระหว่างการสร้างตัวอย่าง

```csharp
Stream CreatePageStream(PreviewPageData pageData)
{
    string imageFilePath = Path.Combine("YOUR_OUTPUT_DIRECTORY", "SignDicomImageAdvanced", $"preview-{pageData.PageNumber}.jpg");
    var folder = Path.GetDirectoryName(imageFilePath);
    if (!Directory.Exists(folder))
    {
        Directory.CreateDirectory(folder);
    }
    return new FileStream(imageFilePath, FileMode.Create);
}

void ReleasePageStream(PreviewPageData pageData, Stream pageStream)
{
    pageStream.Dispose();
}
```

**ขั้นตอนที่ 2: สร้างตัวอย่าง**

ดำเนินการตามกระบวนการสร้างตัวอย่าง

```csharp
using (Signature signature = new Signature("YOUR_DOCUMENT_DIRECTORY\\sample_signed.dicom"))
{
    PreviewOptions previewOption = new PreviewOptions(CreatePageStream, ReleasePageStream)
    {
        PreviewFormat = PreviewOptions.PreviewFormats.PNG,
    };

    signature.GeneratePreview(previewOption);
}
```

## การประยุกต์ใช้งานจริง

1. **การจัดการบันทึกทางการแพทย์**:ตรวจสอบข้อมูลประวัติผู้ป่วยโดยใช้ลายเซ็นรหัส QR เพื่อการปฏิบัติตาม
2. **เส้นทางการตรวจสอบในระบบการดูแลสุขภาพ**ติดตามการเปลี่ยนแปลงเอกสารและตรวจสอบความถูกต้องด้วยรหัส QR
3. **การแบ่งปันข้อมูลที่ปลอดภัย**:รับรองการแบ่งปันภาพทางการแพทย์อย่างปลอดภัยด้วยการฝังลายเซ็นดิจิทัล
4. **การตรวจสอบการปฏิบัติตาม**:ตรวจสอบความสมบูรณ์ของไฟล์ DICOM เป็นประจำเพื่อให้เป็นไปตามข้อกำหนดทางกฎหมาย
5. **การบูรณาการกับระบบ EHR**:บูรณาการไฟล์ DICOM ที่ลงนามแล้วเข้ากับระบบบันทึกสุขภาพอิเล็กทรอนิกส์ (EHR) ได้อย่างราบรื่นเพื่อการดำเนินงานที่มีประสิทธิภาพ