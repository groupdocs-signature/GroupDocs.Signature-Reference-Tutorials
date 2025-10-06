---
"date": "2025-05-07"
"description": "เรียนรู้วิธีลงนามดิจิทัลในไฟล์ PDF ด้วย GroupDocs.Signature สำหรับ .NET ปรับแต่งรูปลักษณ์ ใส่ฟอนต์และรูปภาพ รับรองความปลอดภัยและความถูกต้องของเอกสาร"
"title": "การลงนาม PDF แบบดิจิทัลใน .NET พร้อมคู่มือการใช้ GroupDocs.Signature"
"url": "/th/net/digital-signatures/sign-pdf-digital-signature-groupdocs-dotnet/"
"weight": 1
type: docs
---
# การลงนาม PDF แบบดิจิทัลใน .NET: คู่มือการใช้ GroupDocs.Signature

## การแนะนำ

ลายเซ็นดิจิทัลบนเอกสาร PDF ช่วยให้มั่นใจได้ถึงความถูกต้อง ปลอดภัย และสมบูรณ์ ซึ่งถือเป็นสิ่งสำคัญสำหรับสัญญาทางกฎหมาย ใบแจ้งหนี้ และบันทึกอย่างเป็นทางการ **GroupDocs.Signature สำหรับ .NET** ช่วยให้คุณเพิ่มลายเซ็นดิจิทัลลงในไฟล์ PDF ได้อย่างง่ายดาย พร้อมปรับแต่งรูปลักษณ์ของลายเซ็นเพื่อเพิ่มความสวยงาม บทช่วยสอนนี้จะแนะนำคุณตลอดกระบวนการลงนามในเอกสาร PDF โดยใช้ GroupDocs ลายเซ็นจะเน้นที่การตั้งค่ารูปภาพและแบบอักษรเป็นพิเศษ

### สิ่งที่คุณจะได้เรียนรู้:
- วิธีการลงนามดิจิทัลในเอกสาร PDF โดยใช้ .NET
- ใช้การตั้งค่าลักษณะที่กำหนดเอง เช่น รูปภาพและแบบอักษรกับลายเซ็นดิจิทัลของคุณ
- ตั้งค่าและเริ่มต้น GroupDocs.Signature สำหรับ .NET ในโครงการของคุณ

เริ่มต้นด้วยการครอบคลุมข้อกำหนดเบื้องต้นที่จำเป็นเพื่อเริ่มต้น

## ข้อกำหนดเบื้องต้น (H2)

หากต้องการทำตามบทช่วยสอนนี้ คุณจะต้องมี:

- **GroupDocs.Signature สำหรับ .NET** ไลบรารี: ตรวจสอบให้แน่ใจว่าติดตั้งผ่าน .NET CLI หรือ NuGet Package Manager
  - **.NET CLI**- `dotnet add package GroupDocs.Signature`
  - **ตัวจัดการแพ็คเกจ**- `Install-Package GroupDocs.Signature`

- ใบรับรองดิจิทัลที่ถูกต้องในรูปแบบ PFX
- ความรู้พื้นฐานเกี่ยวกับ C# และการตั้งค่าสภาพแวดล้อม .NET

## การตั้งค่า GroupDocs.Signature สำหรับ .NET (H2)

เริ่มต้นด้วยการติดตั้งไลบรารี GroupDocs.Signature:

**.NET CLI**
```shell
dotnet add package GroupDocs.Signature
```

**ตัวจัดการแพ็คเกจ**
```shell
Install-Package GroupDocs.Signature
```

หรือใช้ UI ของตัวจัดการแพ็คเกจ NuGet เพื่อค้นหาและติดตั้ง "GroupDocs.Signature"

### การได้มาซึ่งใบอนุญาต

- **ทดลองใช้ฟรี**:สำรวจคุณสมบัติทั้งหมดด้วยใบอนุญาตประเมินชั่วคราว
- **ใบอนุญาตชั่วคราว**: รับได้จาก [ที่นี่](https://purchase-groupdocs.com/temporary-license/).
- **ซื้อ**:สำหรับการใช้งานในระยะยาว ให้ซื้อการสมัครสมาชิกได้ที่ [ลิงค์นี้](https://purchase-groupdocs.com/buy).

### การเริ่มต้นและการตั้งค่าขั้นพื้นฐาน

ในการเริ่มต้น GroupDocs.Signature ในโครงการ .NET ของคุณ:

```csharp
using GroupDocs.Signature;

// สร้างการเริ่มต้นวัตถุลายเซ็นด้วยไฟล์ PDF ต้นฉบับ
using (Signature signature = new Signature("YOUR_DOCUMENT_DIRECTORY/SAMPLE_PDF.pdf")) {
    // รหัสของคุณในการลงนามเอกสารอยู่ที่นี่
}
```

## คู่มือการใช้งาน

### ลงนามในเอกสาร PDF ด้วยลายเซ็นดิจิทัล (H2)

คุณลักษณะนี้ช่วยให้คุณสามารถเพิ่มลายเซ็นดิจิทัลลงในเอกสาร PDF ของคุณได้ เพื่อรับรองความถูกต้องและความสมบูรณ์ของเอกสาร

#### ภาพรวมของคุณสมบัติ
การนำฟีเจอร์นี้ไปใช้ช่วยให้คุณสามารถลงนามดิจิทัลในไฟล์ PDF ใดๆ ก็ได้โดยใช้ GroupDocs.Signature สำหรับ .NET คุณยังสามารถใช้การตั้งค่าแบบกำหนดเองเพื่อปรับแต่งรูปลักษณ์ของลายเซ็นของคุณ รวมถึงรูปภาพและแบบอักษรได้อีกด้วย

#### ขั้นตอนการดำเนินการ (H3)

##### ขั้นตอนที่ 1: ตั้งค่าสภาพแวดล้อมของคุณ

ตรวจสอบให้แน่ใจว่าโครงการของคุณได้รับการกำหนดค่าด้วยการอ้างอิงที่จำเป็น:

```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Options;
using GroupDocs.Signature.Domain;

namespace DigitalSignatureExample {
    public class SignPdfWithDigitalSignature {
        // กำหนดเส้นทางสำหรับแหล่งที่มาของ PDF และใบรับรองดิจิทัล
        private static string sourceFile = "YOUR_DOCUMENT_DIRECTORY/SAMPLE_PDF.pdf";
        private static string outputFile = Path.Combine("YOUR_OUTPUT_DIRECTORY", "SignWithPdfDigitalAdvanced_Signed.pdf");
        private static string certificatePath = "YOUR_DOCUMENT_DIRECTORY/CertificatePfx.pfx";

        public static void Run() {
            // เริ่มต้นวัตถุลายเซ็น
            using (Signature signature = new Signature(sourceFile)) {
                // ตั้งค่าตัวเลือกการลงนามแบบดิจิทัล
                DigitalSignOptions options = new DigitalSignOptions(certificatePath) {
                    Password = "1234567890",  // รหัสผ่านใบรับรอง
                    Reason = "Sign",          // เหตุผลในการลงนาม
                    Contact = "JohnSmith",    // ข้อมูลการติดต่อ
                    Location = "Office1",     // สถานที่ลงนาม
                    Visible = true,            // ทำให้ลายเซ็นมองเห็นได้
                    Left = 400,                // ตำแหน่งแนวนอน
                    Top = 20,                  // ตำแหน่งแนวตั้ง
                    Height = 70,               // ความสูงของลายเซ็น
                    Width = 200,               // ความกว้างของลายเซ็น
                    ImageFilePath = "YOUR_DOCUMENT_DIRECTORY/ImageHandwrite.png", // รูปลักษณ์ภายนอก
                    Appearance = new PdfDigitalSignatureAppearance() {
                        Foreground = System.Drawing.Color.FromArgb(50, System.Drawing.Color.Gray),
                        FontFamilyName = "TimesNewRoman",
                        FontSize = 12
                    }
                };

                // ลงนามในเอกสารและบันทึกลงในเส้นทางเอาต์พุต
                SignResult signResult = signature.Sign(outputFile, options);
                Console.WriteLine($"Document signed successfully with {signResult.Succeeded.Count} signature(s). File saved at {outputFile}.");
            }
        }
    }
}
```

##### ขั้นตอนที่ 2: ปรับแต่งลักษณะลายเซ็น

ปรับแต่งลักษณะลายเซ็นดิจิทัลของคุณโดยใช้การตั้งค่าแบบอักษรและรูปภาพ:

```csharp
using System;
using GroupDocs.Signature.Options;
using GroupDocs.Signature.Domain;
using System.Drawing;

namespace DigitalSignatureAppearanceExample {
    public class CustomizeDigitalSignatureAppearance {
        public static void Run() {
            // เริ่มต้นการตั้งค่าลักษณะที่ปรากฏสำหรับลายเซ็นดิจิทัล
            PdfDigitalSignatureAppearance appearance = new PdfDigitalSignatureAppearance() {
                Foreground = Color.FromArgb(50, Color.Gray),  // ตั้งค่าสีตัวอักษรที่กำหนดเอง
                FontFamilyName = "TimesNewRoman",          // ระบุตระกูลแบบอักษร
                FontSize = 12                               // กำหนดขนาดตัวอักษร
            };

            Console.WriteLine("Custom appearance settings for digital signature have been applied.");
        }
    }
}
```

#### ตัวเลือกการกำหนดค่าคีย์
- **เส้นทางใบรับรอง**: ตรวจสอบให้แน่ใจว่าคุณระบุเส้นทางที่ถูกต้องไปยังไฟล์ PFX ของคุณ
- **รหัสผ่าน**:ใช้รหัสผ่านที่เชื่อมโยงกับใบรับรองดิจิทัลของคุณ
- **การตั้งค่ารูปลักษณ์**:ปรับแต่งแบบอักษรและสีให้ตรงกับความต้องการของแบรนด์

##### เคล็ดลับการแก้ไขปัญหา
- ตรวจสอบว่าใบรับรองดิจิทัลของคุณถูกต้องและได้รับการกำหนดค่าอย่างถูกต้อง
- ตรวจสอบให้แน่ใจว่าเส้นทางทั้งหมด (PDF, เอาท์พุต, รูปภาพ) สามารถเข้าถึงได้จากสภาพแวดล้อมแอปพลิเคชันของคุณ

### ใช้การตั้งค่าลักษณะที่ปรากฏแบบกำหนดเองกับลายเซ็นดิจิทัล (H2)

ปรับปรุงความน่าสนใจทางภาพของลายเซ็นดิจิทัลของคุณด้วยการตั้งค่าแบบอักษรและรูปภาพที่กำหนดเองโดยใช้ GroupDocs.Signature สำหรับ .NET

#### ภาพรวม
การปรับแต่งรูปลักษณ์ของลายเซ็นดิจิทัลสามารถทำให้ดูน่าสนใจและสอดคล้องกับมาตรฐานการสร้างแบรนด์มากขึ้น ฟีเจอร์นี้ช่วยให้คุณตั้งค่าแบบอักษร สี และรูปภาพเฉพาะได้

#### ขั้นตอนการดำเนินการ (H3)

##### ขั้นตอนที่ 1: เริ่มต้นการตั้งค่ารูปลักษณ์

สร้างอินสแตนซ์ของ `PdfDigitalSignatureAppearance`-

```csharp
using System.Drawing;

// กำหนดค่าลักษณะที่ปรากฏแบบกำหนดเองสำหรับลายเซ็นดิจิทัล
PdfDigitalSignatureAppearance appearance = new PdfDigitalSignatureAppearance() {
    Foreground = Color.FromArgb(50, Color.Gray),  // สีตัวอักษรที่กำหนดเอง
    FontFamilyName = "TimesNewRoman",            // ฟอนต์ตระกูล
    FontSize = 12                                // ขนาดตัวอักษร
};
```

##### ขั้นตอนที่ 2: ใช้การตั้งค่ารูปลักษณ์

รวมการตั้งค่าเหล่านี้ลงในตัวเลือกลายเซ็นดิจิทัลของคุณ:

```csharp
DigitalSignOptions options = new DigitalSignOptions(certificatePath) {
    ImageFilePath = "YOUR_DOCUMENT_DIRECTORY/ImageHandwrite.png",
    Appearance = appearance
};
```

## การประยุกต์ใช้งานจริง (H2)

ต่อไปนี้เป็นสถานการณ์จริงบางกรณีที่การลงนาม PDF ด้วย GroupDocs.Signature อาจเป็นประโยชน์ได้:
1. **การลงนามสัญญา**:ให้แน่ใจว่าข้อตกลงทางกฎหมายได้รับการลงนามและตรวจสอบแบบดิจิทัล
2. **การอนุมัติใบแจ้งหนี้**:ลงนามใบแจ้งหนี้แบบดิจิทัลเพื่อการประมวลผลที่รวดเร็วยิ่งขึ้นในแผนกการเงิน
3. **การตรวจสอบเอกสาร**:รับรองเอกสารราชการเพื่อป้องกันการแก้ไขโดยไม่ได้รับอนุญาต

เมื่อปฏิบัติตามคู่มือนี้ คุณจะบูรณาการการลงนามดิจิทัลเข้ากับแอปพลิเคชัน .NET ได้อย่างมีประสิทธิภาพโดยใช้ GroupDocs.Signature ซึ่งช่วยเพิ่มความปลอดภัยและความเป็นมืออาชีพ