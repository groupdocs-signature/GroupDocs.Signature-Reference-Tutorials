---
"date": "2025-05-07"
"description": "تعرّف على كيفية توقيع مستندات PDF باستخدام رموز الاستجابة السريعة HIBC باستخدام GroupDocs.Signature لـ .NET. يغطي هذا الدليل رموز LIC وPAS، بما في ذلك رموز الاستجابة السريعة، ورموز Aztec، وDataMatrix."
"title": "كيفية توقيع المستندات باستخدام رموز الاستجابة السريعة HIBC باستخدام GroupDocs.Signature لـ .NET - دليل شامل"
"url": "/ar/net/qr-code-signatures/sign-documents-hibc-qr-groupdocs-dotnet/"
"weight": 1
type: docs
---
# كيفية توقيع المستندات باستخدام رموز QR الخاصة بـ HIBC باستخدام GroupDocs.Signature لـ .NET

## مقدمة

في بيئة الأعمال المتسارعة اليوم، يُعدّ ضمان صحة وسلامة المستندات أمرًا بالغ الأهمية. سواء كنت تتعامل مع الأدوية، أو منتجات الرعاية الصحية، أو الخدمات اللوجستية، فإن وجود طريقة آمنة لتوقيع المستندات وتتبعها يُوفّر الوقت ويمنع الأخطاء. **GroupDocs.Signature لـ .NET**، وهي مكتبة قوية مصممة لتبسيط عمليات إدارة المستندات من خلال تمكين التكامل السلس لرموز HIBC QR في مستنداتك.

في هذا البرنامج التعليمي، سنستكشف كيفية الاستفادة من GroupDocs.Signature لـ .NET لتوقيع مستندات PDF باستخدام أنواع مختلفة من رموز الاستجابة السريعة (QR code) الخاصة بـ HIBC - LIC (الترخيص) وPAS (نظام مصادقة المنتج) - بما في ذلك رموز الاستجابة السريعة (QR code) وAztec Code وDataMatrix. في النهاية، ستكتسب فهمًا متينًا لتطبيق هذه الحلول في تطبيقات .NET الخاصة بك.

**ما سوف تتعلمه:**
- كيفية إعداد GroupDocs.Signature لـ .NET
- تنفيذ رموز الاستجابة السريعة (QR Codes) ورموز Aztec وDataMatrix الخاصة بـ HIBC LIC
- إضافة رموز QR الخاصة بـ HIBC PAS ورموز Aztec وDataMatrix
- حالات الاستخدام العملية وإمكانيات التكامل

دعونا نلقي نظرة على المتطلبات الأساسية قبل أن نبدأ في تنفيذ هذه الميزات.

## المتطلبات الأساسية

قبل أن نبدأ في الترميز، تأكد من أن لديك ما يلي:

- **بيئة .NET**:تأكد من تثبيت .NET على نظامك (يفضل .NET Core أو .NET 5/6+).
- **GroupDocs.Signature لـ .NET**ستكون هذه المكتبة أداتنا الرئيسية. يمكنك تثبيتها عبر NuGet.
- **المعرفة الأساسية بالبرمجة**:يوصى بالإلمام بلغة C# والتعامل مع الملفات في .NET.

### المكتبات المطلوبة

لاستخدام GroupDocs.Signature لـ .NET، تحتاج إلى إضافة الحزمة باستخدام إحدى الطرق التالية:

**.NET CLI**
```bash
dotnet add package GroupDocs.Signature
```

**مدير الحزم**
```powershell
Install-Package GroupDocs.Signature
```

**واجهة مستخدم مدير الحزم NuGet**
ابحث عن "GroupDocs.Signature" وقم بتثبيت الإصدار الأحدث.

### الحصول على الترخيص

لأغراض الاختبار، يمكنك الحصول على ترخيص تجريبي مجاني. للاستخدام الممتد، يمكنك شراء اشتراك أو طلب ترخيص مؤقت.

- **نسخة تجريبية مجانية**: وصول [هنا](https://releases.groupdocs.com/signature/net/)
- **رخصة مؤقتة**:طلب في [هذا الرابط](https://purchase.groupdocs.com/temporary-license/)

### إعداد البيئة

قم بإعداد بيئتك بالتأكد من أن مشروعك يستهدف إصدار .NET المناسب ويتمتع بإمكانية الوصول إلى GroupDocs.Signature. قم بتشغيله في تطبيقك كما هو موضح:

```csharp
using GroupDocs.Signature;
```

## إعداد GroupDocs.Signature لـ .NET

لبدء استخدام GroupDocs.Signature لـ .NET، تحتاج إلى تثبيت المكتبة وتكوين إعداد أساسي ضمن مشروعك.

### تثبيت

اتبع إحدى الطرق المذكورة أعلاه لإضافة GroupDocs.Signature إلى مشروعك. بعد التثبيت، تأكد من تهيئة مشروعك لاستخدامه من خلال الإشارة إليه في ملفات التعليمات البرمجية.

### تهيئة الترخيص

بعد الحصول على الترخيص، قم بتهيئته على النحو التالي:

```csharp
SignatureConfig signConfig = new SignatureConfig();
signConfig.LicensePath = "path/to/your/license.lic";
Signature signature = new Signature("Sample.pdf", signConfig);
```

سيسمح لك هذا الإعداد بالوصول إلى كافة ميزات GroupDocs.Signature دون قيود.

## دليل التنفيذ

الآن، دعنا نتعمق في تنفيذ كل ميزة باستخدام رموز QR الخاصة بـ HIBC مع GroupDocs.Signature لـ .NET.

### توقيع المستند باستخدام رمز الاستجابة السريعة HIBC LIC

#### ملخص

يضمن توقيع مستند باستخدام رمز الاستجابة السريعة HIBC LIC الامتثال وإمكانية التتبع في حالات الترخيص. سيرشدك هذا القسم إلى كيفية إنشاء رمز الاستجابة السريعة وتضمينه في مستندات PDF الخاصة بك.

#### خطوات التنفيذ

##### الخطوة 1: تكوين مسارات المصدر والإخراج

قم بتحديد مكان وجود مستند المصدر والمكان الذي يجب حفظ الإخراج الموقع فيه:

```csharp
string sourceFilePath = Path.Combine("YOUR_DOCUMENT_DIRECTORY", "Sample.pdf");
string outputPath = Path.Combine("YOUR_OUTPUT_DIRECTORY", "SignWithHIBCLICQR");
string destinFilePath = Path.Combine(outputPath, "SignedDocumentWithHIBCLICQR.pdf");
```

##### الخطوة 2: إنشاء خيارات إشارة رمز الاستجابة السريعة

قم بتكوين رمز الاستجابة السريعة الخاص بك باستخدام نص وإعدادات محددة:

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

    // قم بتوقيع المستند باستخدام هذه الخيارات.
    signature.Sign(destinFilePath, hibcLic_QR_Options);
}
```

**توضيح**: 
- `QrCodeSignOptions` يُهيئ مظهر رمز الاستجابة السريعة ومحتواه. هنا، نُحدد نوع رمز الاستجابة السريعة HIBC LIC ونضعه في المستند.
- `ReturnContent` يسمح لك تعيين هذا الخيار على "صحيح" باسترجاع صورة مقدمة من المستند الموقع.

#### نصائح استكشاف الأخطاء وإصلاحها

- تأكد من تحديد مسار المستند بشكل صحيح.
- تأكد من أن GroupDocs.Signature مرخص بشكل صحيح للوظائف الكاملة.

### توقيع المستند باستخدام رمز HIBC LIC Aztec

#### ملخص

يُقدّم رمز Aztec شكلاً آخر من الترميز، مناسبًا لتخزين المعلومات عالية الكثافة. يُركّز هذا القسم على تضمين رمز Aztec في مستنداتك باستخدام GroupDocs.Signature.

#### خطوات التنفيذ

##### الخطوة 1: تكوين المسارات

على غرار الميزة السابقة، قم بتحديد مسارات ملفاتك:

```csharp
string sourceFilePath = Path.Combine("YOUR_DOCUMENT_DIRECTORY", "Sample.pdf");
string outputPath = Path.Combine("YOUR_OUTPUT_DIRECTORY", "SignWithHIBCLICAztec");
string destinFilePath = Path.Combine(outputPath, "SignedDocumentWithHIBCLICAztec.pdf");
```

##### الخطوة 2: تكوين خيارات الكود الأزتكي

قم بإعداد كود Aztec الخاص بك باستخدام GroupDocs.التوقيع:

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

**توضيح**: 
- ال `QrCodeSignOptions` يتم استخدامه مرة أخرى هنا ولكن مع نوع الكود الأزتكي.
- التمركز (`Top`، `Left`) وإعدادات استرجاع المحتوى مشابهة لرموز QR.

#### نصائح استكشاف الأخطاء وإصلاحها

- تأكد من أن مسارات الملف دقيقة.
- تأكد من أن إصدار GroupDocs.Signature يدعم أنواع Aztec Code.

### توقيع المستند باستخدام HIBC LIC DataMatrix

#### ملخص

يوفر كود DataMatrix طريقةً فعّالة أخرى لتخزين البيانات. يوضح هذا القسم كيفية دمج DataMatrix في مستندات PDF.

#### خطوات التنفيذ

##### الخطوة 1: تعيين مسارات الملفات

كما في السابق، حدد مكان وجود ملفاتك:

```csharp
string sourceFilePath = Path.Combine("YOUR_DOCUMENT_DIRECTORY", "Sample.pdf");
string outputPath = Path.Combine("YOUR_OUTPUT_DIRECTORY", "SignWithHIBCLICDataMatrix");
string destinFilePath = Path.Combine(outputPath, "SignedDocumentWithHIBCLICDataMatrix.pdf");
```

##### الخطوة 2: إنشاء خيارات علامة DataMatrix

تكوين وتطبيق كود DataMatrix:

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

**توضيح**: 
- `QrCodeSignOptions` يتم استخدامه لإعداد مظهر ومحتوى كود DataMatrix.
- التمركز (`Top`، `Left`) وتتبع إعدادات الاسترجاع نفس النمط مثل الرموز السابقة.

#### نصائح استكشاف الأخطاء وإصلاحها

- تأكد من تحديد جميع مسارات الملفات بشكل صحيح.
- تأكد من أن GroupDocs.Signature يدعم أنواع DataMatrix Code في الإصدار الخاص بك.

### توقيع المستند باستخدام رمز الاستجابة السريعة HIBC PAS

#### ملخص

يُحسّن توقيع المستندات باستخدام رمز الاستجابة السريعة HIBC PAS إمكانية تتبّع المنتجات وتتبعها. يرشدك هذا القسم إلى كيفية تضمين رمز الاستجابة السريعة PAS في ملفات PDF باستخدام GroupDocs.Signature.

#### خطوات التنفيذ

##### الخطوة 1: تكوين مسارات المصدر والإخراج

قم بتحديد مكان وجود مستند المصدر والمكان الذي يجب حفظ الإخراج الموقع فيه:

```csharp
string sourceFilePath = Path.Combine("YOUR_DOCUMENT_DIRECTORY", "Sample.pdf");
string outputPath = Path.Combine("YOUR_OUTPUT_DIRECTORY", "SignWithHIBCPASQR");
string destinFilePath = Path.Combine(outputPath, "SignedDocumentWithHIBCPASQR.pdf");
```

##### الخطوة 2: إنشاء خيارات إشارة رمز الاستجابة السريعة

قم بتكوين رمز الاستجابة السريعة PAS الخاص بك باستخدام نص وإعدادات محددة:

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

    // قم بتوقيع المستند باستخدام هذه الخيارات.
    signature.Sign(destinFilePath, hibcPas_QR_Options);
}
```

**توضيح**: 
- `QrCodeSignOptions` تم تكوينه لنوع رمز الاستجابة السريعة HIBC PAS ووضعه على المستند.
- `ReturnContent` يؤدي تعيينه على true إلى استرداد صورة مقدمة للمستند الموقع.

#### نصائح استكشاف الأخطاء وإصلاحها

- تأكد من تحديد جميع المسارات بشكل صحيح.
- تأكد من أن GroupDocs.Signature يدعم أنواع رمز الاستجابة السريعة PAS في الإصدار الخاص بك.

### خاتمة

باتباع هذا الدليل، يمكنك دمج رموز الاستجابة السريعة HIBC LIC وPAS بكفاءة في مستندات PDF باستخدام GroupDocs.Signature لـ .NET. تُحسّن هذه العملية أمان المستندات وإمكانية تتبعها والامتثال في مختلف القطاعات. لمزيد من التخصيص والميزات المتقدمة، يُرجى مراجعة [توثيق GroupDocs](https://docs.groupdocs.com/signature/net/).