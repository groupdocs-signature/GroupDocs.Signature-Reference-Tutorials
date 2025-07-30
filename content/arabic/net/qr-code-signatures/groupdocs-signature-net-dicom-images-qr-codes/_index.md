---
"date": "2025-05-07"
"description": "تعرّف على كيفية توقيع صور DICOM برموز الاستجابة السريعة (QR codes) باستخدام GroupDocs.Signature لـ .NET. يغطي هذا الدليل إعداد وتنفيذ والتحقق من توقيعات رموز الاستجابة السريعة في التصوير الطبي."
"title": "كيفية توقيع صور DICOM باستخدام رموز الاستجابة السريعة (QR Codes) باستخدام GroupDocs.Signature لـ .NET - دليل شامل"
"url": "/ar/net/qr-code-signatures/groupdocs-signature-net-dicom-images-qr-codes/"
"weight": 1
---

# كيفية توقيع صور DICOM باستخدام رموز QR باستخدام GroupDocs.Signature لـ .NET: دليل شامل

هل تبحث عن طريقة آمنة لمصادقة ملفات DICOM؟ سيوضح لك هذا الدليل المفصل كيفية استخدام GroupDocs.Signature لـ .NET لدمج توقيعات رمز الاستجابة السريعة (QR) في صور DICOM. يُعد هذا الدليل مثاليًا لمتخصصي الرعاية الصحية والمطورين وأي شخص يتعامل مع المستندات الطبية الرقمية، حيث يغطي البرنامج التعليمي من الإعداد إلى التنفيذ.

## ما سوف تتعلمه:
- إعداد بيئة التطوير الخاصة بك باستخدام GroupDocs.Signature لـ .NET.
- تعليمات خطوة بخطوة حول كيفية توقيع صور DICOM باستخدام رموز QR.
- طرق التحقق والبحث عن توقيعات رمز الاستجابة السريعة QR في ملفات DICOM.
- تقنيات لإنشاء معاينات للمستندات الموقعة لأغراض المراجعة.
- أفضل الممارسات لتحسين الأداء وإدارة الموارد بشكل فعال.

دعونا نبدأ بالمتطلبات الأساسية!

## المتطلبات الأساسية

لاستخدام GroupDocs.Signature لـ .NET، تأكد من جاهزية بيئتك. إليك ما ستحتاجه:

### المكتبات والإصدارات المطلوبة
- **GroupDocs.Signature لـ .NET**:تأكد من التوافق مع إطار عمل .NET الخاص بك.

### متطلبات إعداد البيئة
- بيئة تطوير على Windows أو Linux.
- تم تثبيت Visual Studio أو أي IDE آخر متوافق مع .NET.

### متطلبات المعرفة الأساسية
- فهم أساسي لبرمجة C#.
- المعرفة بإدخال وإخراج الملفات في تطبيقات .NET.

## إعداد GroupDocs.Signature لـ .NET

قم بتثبيت مكتبة GroupDocs.Signature باستخدام طريقتك المفضلة:

**استخدام .NET CLI:**
```bash
dotnet add package GroupDocs.Signature
```

**مدير الحزمة:**
```powershell
Install-Package GroupDocs.Signature
```

**واجهة مستخدم مدير حزمة NuGet:**
- ابحث عن "GroupDocs.Signature" وقم بتثبيت الإصدار الأحدث.

### الحصول على الترخيص

ابدأ بفترة تجريبية مجانية لاستكشاف الإمكانيات. للاستخدام الممتد، فكّر في الحصول على ترخيص مؤقت أو كامل من [مجموعة المستندات](https://purchase.groupdocs.com/buy).

بمجرد التثبيت، قم بتشغيل المكتبة:

```csharp
using GroupDocs.Signature;
// قم بتهيئة كائن التوقيع باستخدام مسار ملف DICOM الخاص بك.
Signature signature = new Signature("YOUR_DOCUMENT_DIRECTORY\\sample.dicom");
```

## دليل التنفيذ

### توقيع صورة DICOM باستخدام رمز الاستجابة السريعة

#### ملخص
أضف توقيعات رمز الاستجابة السريعة (QR Code) لضمان صحة المستندات الطبية وإمكانية تتبعها.

**الخطوة 1: تهيئة كائن التوقيع**

```csharp
string filePath = "YOUR_DOCUMENT_DIRECTORY\\sample.dicom";
using (Signature signature = new Signature(filePath))
{
    // متابعة عمليات التوقيع...
}
```

**الخطوة 2: إنشاء خيارات إشارة رمز الاستجابة السريعة**

قم بتكوين خصائص مثل النص والحجم والمحاذاة.

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

**الخطوة 3: إضافة بيانات تعريف XMP**

قم بتعزيز المستند باستخدام بيانات تعريفية إضافية.

```csharp
DicomSaveOptions dicomSaveOptions = new DicomSaveOptions()
{
    XmpEntries = new List<DicomXmpEntry>() { new DicomXmpEntry(DicomXmpType.PatientName, "Patient #4") }
};
```

**الخطوة 4: توقيع الوثيقة**

تنفيذ التوقيع والحفظ.

```csharp
SignResult signResult = signature.Sign("YOUR_OUTPUT_DIRECTORY\\SignedDicom", options, dicomSaveOptions);
```

### الحصول على معلومات المستند

استرداد البيانات الوصفية من ملفات DICOM الموقعة لضمان سلامة البيانات.

**ملخص:**
الوصول إلى معلومات المستند وتوقيعات بيانات XMP للتحقق منها.

**الخطوة 1: استرداد معلومات المستند**

```csharp
using (Signature signature = new Signature("YOUR_DOCUMENT_DIRECTORY\\sample_signed.dicom"))
{
    IDocumentInfo signedDocumentInfo = signature.GetDocumentInfo();
}
```

**الخطوة 2: تكرار وطباعة بيانات XMP**

عرض تفاصيل البيانات الوصفية.

```csharp
foreach (var item in signedDocumentInfo.MetadataSignatures)
{
    Console.WriteLine(item.ToString());
}
```

### التحقق من توقيعات DICOM

التحقق من صحة توقيعات رمز الاستجابة السريعة (QR Code) داخل صور DICOM.

**ملخص:**
تأكد من أن التوقيعات صحيحة وأصيلة.

**الخطوة 1: إنشاء خيارات التحقق من رمز الاستجابة السريعة**

تعيين الخيارات المطابقة للنص المحدد في رموز QR.

```csharp
QrCodeVerifyOptions options = new QrCodeVerifyOptions()
{
    AllPages = true,
    Text = "Patient #36363393",
    MatchType = TextMatchType.Contains
};
```

**الخطوة 2: التحقق من التوقيعات**

التحقق مما إذا كانت التوقيعات تلبي المعايير.

```csharp
VerificationResult result = signature.Verify(options);

if (result.IsValid)
{
    Console.WriteLine($"DICOM {filePath} has {result.Succeeded.Count} successfully verified signatures!");
}
```

### البحث عن التوقيعات في DICOM

حدد توقيعات رمز الاستجابة السريعة (QR) داخل صور DICOM الموقعة.

**ملخص:**
ابحث بكفاءة عن جميع توقيعات رمز الاستجابة السريعة لإدارة صحة المستندات.

**الخطوة 1: البحث عن توقيعات رمز الاستجابة السريعة**

```csharp
List<QrCodeSignature> signatures = signature.Search<QrCodeSignature>(SignatureType.QrCode);
```

**الخطوة 2: تكرار وطباعة تفاصيل التوقيع**

قم بمراجعة تفاصيل كل توقيع تم العثور عليه.

```csharp
foreach (var QrCodeSignature in signatures)
{
    Console.WriteLine($"QRCode signature found at page {QrCodeSignature.PageNumber} with type {QrCodeSignature.EncodeType.TypeName} and text {QrCodeSignature.Text}");
}
```

### إنشاء معاينة لـ DICOM الموقع

إنشاء معاينات مرئية للتحقق.

**ملخص:**
إنشاء معاينات للصور للتحقق من المحتوى دون الحاجة إلى برامج متخصصة.

**الخطوة 1: تحديد طرق التدفق**

إعداد طرق لإدارة تدفق الملفات أثناء إنشاء المعاينة.

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

**الخطوة 2: إنشاء المعاينات**

تنفيذ عملية إنشاء المعاينة.

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

## التطبيقات العملية

1. **إدارة السجلات الطبية**:التحقق من صحة سجلات المرضى باستخدام توقيعات رمز الاستجابة السريعة (QR Code) لضمان الامتثال.
2. **مسارات التدقيق في أنظمة الرعاية الصحية**:تتبع تغييرات المستندات والتحقق من صحتها باستخدام رموز الاستجابة السريعة (QR).
3. **مشاركة البيانات بشكل آمن**:ضمان المشاركة الآمنة للصور الطبية من خلال تضمين التوقيعات الرقمية.
4. **التحقق من الامتثال**:تحقق بانتظام من سلامة ملف DICOM لتلبية المتطلبات القانونية.
5. **التكامل مع أنظمة السجلات الصحية الإلكترونية**:دمج ملفات DICOM الموقعة بسلاسة في أنظمة السجلات الصحية الإلكترونية (EHR) لتبسيط العمليات.