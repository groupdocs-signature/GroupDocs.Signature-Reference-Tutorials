---
"date": "2025-05-07"
"description": "تعرّف على كيفية استخدام GroupDocs.Signature لـ .NET لاستخراج معلومات مُفصّلة عن المستندات، بما في ذلك التوقيعات والبيانات الوصفية وغيرها. يُغطي هذا الدليل الإعداد والتنفيذ وأفضل الممارسات."
"title": "Master GroupDocs.Signature لـ .NET - استخراج معلومات المستند وعرضها بكفاءة"
"url": "/ar/net/preview-info/groupdocs-signature-net-document-info-extraction/"
"weight": 1
---

# إتقان GroupDocs.Signature لـ .NET: استخراج معلومات المستند وعرضها بكفاءة

## مقدمة

هل تبحث عن استخراج تفاصيل شاملة بكفاءة من مستندات تطبيقاتك؟ سواءً كنتَ تُدير عقودًا أو اتفاقيات أو ملفات PDF متعددة الصفحات، فإنّ وجود حلٍّ فعّال أمرٌ أساسي. **GroupDocs.Signature لـ .NET** يقدم ميزات فعّالة مصممة لتبسيط تحليل المستندات من خلال استرجاع وعرض عناصر مثل حقول النماذج والتوقيعات والبيانات الوصفية وغيرها. سيرشدك هذا البرنامج التعليمي إلى كيفية استخدام هذه الإمكانيات لتحسين وظائف تطبيقك.

**ما سوف تتعلمه:**
- كيفية استرداد معلومات المستند التفصيلية باستخدام GroupDocs.Signature لـ .NET
- عرض أنواع مختلفة من التوقيعات وتفاصيل حقل النموذج
- استخراج البيانات الوصفية والسمات الخاصة بالصفحة

دعونا نراجع المتطلبات الأساسية قبل أن نتعمق في التنفيذ.

## المتطلبات الأساسية

قبل استخدام GroupDocs.Signature لـ .NET، تأكد من إعداد بيئتك بشكل صحيح. يتطلب هذا البرنامج التعليمي إلمامًا بلغة C# ومعرفة أساسية بمفاهيم معالجة المستندات.

### المكتبات والتبعيات المطلوبة
- **GroupDocs.Signature لـ .NET**:المكتبة الأساسية التي سنستخدمها.
- **.NET Framework أو .NET Core**:اعتمادًا على إعداد مشروعك.

### إعداد البيئة
تأكد من أن لديك بيئة تطوير جاهزة باستخدام Visual Studio أو أي بيئة تطوير متكاملة مناسبة أخرى تدعم مشاريع .NET.

### متطلبات المعرفة الأساسية
- فهم أساسي لبرمجة C#.
- التعرف على أنواع المستندات (PDF، Word، Excel) وخصائصها.

## إعداد GroupDocs.Signature لـ .NET

لاستخدام GroupDocs.Signature لـ .NET، عليك تثبيت المكتبة. إليك عدة طرق:

### تعليمات التثبيت

**استخدام .NET CLI:**
```bash
dotnet add package GroupDocs.Signature
```

**استخدام وحدة تحكم إدارة الحزم:**
```powershell
Install-Package GroupDocs.Signature
```

**واجهة مستخدم مدير حزمة NuGet:**
ابحث عن "GroupDocs.Signature" في NuGet Package Manager وقم بتثبيت الإصدار الأحدث.

### الحصول على الترخيص
للاستفادة الكاملة من GroupDocs.Signature، فكر في الحصول على ترخيص:
- **نسخة تجريبية مجانية**:ابدأ بإصدار تجريبي مجاني لاستكشاف الميزات.
- **رخصة مؤقتة**:الحصول على ترخيص مؤقت للاختبار الموسع.
- **شراء**:شراء ترخيص كامل للاستخدام الإنتاجي.

بمجرد التثبيت والترخيص، قم بتهيئة مشروعك عن طريق إعداد بيئة GroupDocs.Signature كما هو موضح أدناه:

```csharp
using System;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;

public class GetDocumentInfoFeature
{
    public static void Run()
    {
        // قم بتحديد مسار الملف للمستند الذي تريد تحليله
        string filePath = "YOUR_DOCUMENT_DIRECTORY\Sample_Signed_Multi_Document.pdf";  // استبدل بمسار المستند الفعلي الخاص بك
        
        SignatureSettings signatureSettings = new SignatureSettings
        {
            IncludeStandardMetadataSignatures = true
        };

        using (Signature signature = new Signature(filePath, signatureSettings))
        {
            IDocumentInfo documentInfo = signature.GetDocumentInfo();
            // سيتم إجراء عمليات أخرى هنا...
        }
    }
}
```

## دليل التنفيذ

بعد اكتمال عملية الإعداد، دعنا نستكشف كيفية تنفيذ الميزات المختلفة لـ GroupDocs.Signature لـ .NET.

### استرداد وعرض خصائص المستند الأساسية

**ملخص**:استخراج الخصائص الأساسية مثل تنسيق الملف والحجم وعدد الصفحات.

#### التنفيذ خطوة بخطوة:
1. **تهيئة كائن التوقيع**:إنشاء مثيل لـ `Signature` الفئة مع مسار المستند الخاص بك.
2. **طريقة الحصول على معلومات المستند**:استخدم `GetDocumentInfo()` طريقة لاسترجاع معلومات مفصلة حول المستند.
3. **عرض خصائص المستند**:إخراج الخصائص الأساسية مثل التنسيق والامتداد والحجم باستخدام `Console.WriteLine` لأغراض التصحيح أو التسجيل.

```csharp
IDocumentInfo documentInfo = signature.GetDocumentInfo();
Console.WriteLine($"Document properties {Path.GetFileName(filePath)}:");
Console.WriteLine($" - format : {documentInfo.FileType.FileFormat}");
Console.WriteLine($" - extension : {documentInfo.FileType.Extension}");
Console.WriteLine($" - size : {documentInfo.Size}");
Console.WriteLine($" - page count : {documentInfo.PageCount}");
```

### عرض معلومات حول كل صفحة مستند

**ملخص**:قم بالتعمق أكثر من خلال استرداد المعلومات وعرضها حول كل صفحة داخل المستند.

#### التنفيذ خطوة بخطوة:
1. **التكرار عبر الصفحات**:تكرار من خلال `documentInfo.Pages` للوصول إلى تفاصيل الصفحة الفردية مثل العرض والارتفاع.

```csharp
foreach (PageInfo pageInfo in documentInfo.Pages)
{
    Console.WriteLine($" - page-{pageInfo.PageNumber} Width {pageInfo.Width}, Height {pageInfo.Height}");
}
```

### عرض معلومات توقيعات حقول النموذج

**ملخص**:استخراج وعرض المعلومات المتعلقة بحقول النموذج داخل المستند.

#### التنفيذ خطوة بخطوة:
1. **حقول نموذج الوصول**: يستخدم `documentInfo.FormFields` لاسترجاع كافة توقيعات حقول النموذج الموجودة في المستند.
2. **عرض تفاصيل كل حقل نموذج**:تكرار كل حقل نموذج وإخراج نوعه واسمه وقيمته.

```csharp
Console.WriteLine($"Document Form Fields information: count = {documentInfo.FormFields.Count}");
foreach (FormFieldSignature formField in documentInfo.FormFields)
{
    Console.WriteLine($" - type #{formField.Type}: Name: {formField.Name} Value: {formField.Value}");
}
```

### عرض معلومات التوقيعات المختلفة

**ملخص**:استرجاع وعرض المعلومات الخاصة بالنصوص والصور والبيانات الرقمية والرمز الشريطي ورمز الاستجابة السريعة وحقول النموذج وتوقيعات البيانات الوصفية.

#### خطوات التنفيذ:
- **توقيعات النص**: وصول `documentInfo.TextSignatures` للحصول على تفاصيل حول كل توقيع نصي بما في ذلك معرفه وموقعه وحجمه وتاريخ إنشائه.

```csharp
Console.WriteLine($"Document Text signatures: {documentInfo.TextSignatures.Count}");
foreach (TextSignature textSignature in documentInfo.TextSignatures)
{
    Console.WriteLine($" - #{textSignature.SignatureId}: Text: {textSignature.Text} Location: {textSignature.Left}x{textSignature.Top}. Size: {textSignature.Width}x{textSignature.Height}. CreatedOn/ModifiedOn: {textSignature.CreatedOn.ToShortDateString()} / {textSignature.ModifiedOn.ToShortDateString()}");
}
```

- **توقيعات الصور**:على غرار توقيعات النص، استخدم `documentInfo.ImageSignatures` للحصول على تفاصيل مثل حجم وتنسيق توقيعات الصور.

```csharp
Console.WriteLine($"Document Image signatures: {documentInfo.ImageSignatures.Count}");
foreach (ImageSignature imageSignature in documentInfo.ImageSignatures)
{
    Console.WriteLine($" - #{imageSignature.SignatureId}: Size: {imageSignature.Size} bytes, Format: {imageSignature.Format}. CreatedOn/ModifiedOn: {imageSignature.CreatedOn.ToShortDateString()} / {imageSignature.ModifiedOn.ToShortDateString()}");
}
```

- **التوقيعات الرقمية**:للتوقيعات الرقمية، استخدم `documentInfo.DigitalSignatures` لاستخراج معرفات التوقيع والطوابع الزمنية.

```csharp
Console.WriteLine($"Document Digital signatures: {documentInfo.DigitalSignatures.Count}");
foreach (DigitalSignature digitalSignature in documentInfo.DigitalSignatures)
{
    Console.WriteLine($" - #{digitalSignature.SignatureId}. CreatedOn/ModifiedOn: {digitalSignature.CreatedOn.ToShortDateString()} / {digitalSignature.ModifiedOn.ToShortDateString()}");
}
```

- **توقيعات الباركود ورمز الاستجابة السريعة**: يستخدم `documentInfo.BarcodeSignatures` و `documentInfo.QrCodeSignatures` لجمع تفاصيل الباركود ورمز الاستجابة السريعة على التوالي.

```csharp
Console.WriteLine($"Document Barcode signatures: {documentInfo.BarcodeSignatures.Count}");
foreach (BarcodeSignature barcodeSignature in documentInfo.BarcodeSignatures)
{
    Console.WriteLine($" - #{barcodeSignature.SignatureId}: Type: {barcodeSignature.EncodeType?.TypeName}. Text: {barcodeSignature.Text}");
}

Console.WriteLine($"Document QR Code signatures: {documentInfo.QrCodeSignatures.Count}");
foreach (QrCodeSignature qrCodeSignature in documentInfo.QrCodeSignatures)
{
    Console.WriteLine($" - #{qrCodeSignature.SignatureId}: Type: {qrCodeSignature.EncodeType?.TypeName}. Text: {qrCodeSignature.Text}");
}
```

### خاتمة

باتباع هذا البرنامج التعليمي، ستتعلم كيفية استخدام GroupDocs.Signature لـ .NET لاستخراج وعرض معلومات شاملة من المستندات بكفاءة. ستعزز هذه المهارات قدرة تطبيقك على إدارة المستندات بدقة وسهولة.

**الخطوات التالية:**
- استكشف الميزات الإضافية لـ GroupDocs.Signature.
- تنفيذ التحقق من صحة التوقيع داخل تطبيقاتك.
- دمج هذه الوظيفة في سير عمل أكبر لمعالجة المستندات تلقائيًا.