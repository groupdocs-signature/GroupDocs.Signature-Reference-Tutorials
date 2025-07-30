---
"date": "2025-05-07"
"description": "تعلّم كيفية التوقيع والتحقق والبحث وتحديث وحذف تواقيع النصوص في المستندات بكفاءة باستخدام GroupDocs.Signature لـ .NET. بسّط عملية التوقيع الرقمي لديك اليوم."
"title": "توقيع المستندات الرئيسية والتحقق منها باستخدام GroupDocs.Signature لـ .NET"
"url": "/ar/net/digital-signatures/master-document-signing-groupdocs-signature-net/"
"weight": 1
---

# توقيع المستندات الرئيسية والتحقق منها باستخدام GroupDocs.Signature لـ .NET

## كيفية إتقان توقيع المستندات والتحقق منها باستخدام GroupDocs.Signature لـ .NET

في ظلّ العالم الرقميّ الحالي، تُعدّ حلول توقيع المستندات الفعّالة أمرًا بالغ الأهمية لإدارة العقود والاتفاقيات وأي وثائق قانونية. أتمتة هذه العملية تُوفّر الوقت وتُقلّل الأخطاء. **GroupDocs.Signature لـ .NET** يقدم حلاً فعالاً لتبسيط إدارة توقيعات النصوص في تطبيقاتك. سيشرح لك هذا الدليل الشامل ميزات GroupDocs.Signature لـ .NET، بما في ذلك التوقيع والتحقق والبحث والتحديث وحذف توقيعات النصوص.

## ما سوف تتعلمه

- كيفية توقيع المستندات باستخدام توقيعات نصية قابلة للتخصيص
- تقنيات للتحقق الفعال من الوثائق الموقعة
- طرق البحث عن التوقيعات النصية الموجودة في المستندات
- خطوات تحديث وحذف التوقيعات النصية حسب الحاجة
- أفضل الممارسات لتحسين الأداء وإدارة الذاكرة

دعونا نبدأ بمراجعة المتطلبات الأساسية.

## المتطلبات الأساسية

قبل أن تبدأ، تأكد من إعداد بيئة التطوير الخاصة بك بالأدوات اللازمة:

### المكتبات والتبعيات المطلوبة

- **GroupDocs.Signature لـ .NET**:تمكنك هذه المكتبة من إضافة وظائف التوقيع في تطبيقاتك.
- **.NET Framework 4.6.1 أو أعلى** (أو .NET Core 2.x+)

### متطلبات إعداد البيئة

سوف تحتاج إلى بيئة تطوير C#، مثل Visual Studio، واتصال بالإنترنت لتنزيل الحزم الضرورية.

### متطلبات المعرفة الأساسية

يُنصح بالإلمام بمفاهيم برمجة C# الأساسية. إذا كنت جديدًا على GroupDocs.Signature لـ .NET، فلا تقلق، فهذا الدليل سيرشدك خلال كل خطوة.

## إعداد GroupDocs.Signature لـ .NET

للبدء، ستحتاج إلى تثبيت مكتبة GroupDocs.Signature في مشروعك. إليك الطريقة:

### التثبيت عبر .NET CLI
```bash
dotnet add package GroupDocs.Signature
```

### وحدة تحكم مدير الحزم
```powershell
Install-Package GroupDocs.Signature
```

### واجهة مستخدم مدير الحزم NuGet
1. افتح مشروعك في Visual Studio.
2. انتقل إلى **أدوات** > **مدير الحزم NuGet** > **إدارة حزم NuGet للحل**.
3. ابحث عن "GroupDocs.Signature" وقم بتثبيت الإصدار الأحدث.

#### خطوات الحصول على الترخيص
- **نسخة تجريبية مجانية**:ابدأ بتجربة مجانية عن طريق التنزيل من [تجارب مجانية لـ GroupDocs](https://releases.groupdocs.com/signature/net/).
- **رخصة مؤقتة**:الحصول على ترخيص مؤقت لتقييم الميزات الكاملة في [رخصة مؤقتة](https://purchase.groupdocs.com/temporary-license/).
- **شراء**:للاستمرار في الاستخدام، قم بشراء ترخيص من [صفحة شراء GroupDocs](https://purchase.groupdocs.com/buy).

#### التهيئة والإعداد الأساسي

بعد التثبيت، قم بتهيئة GroupDocs.Signature في مشروعك على النحو التالي:

```csharp
using GroupDocs.Signature;

// قم بتهيئة مثيل التوقيع باستخدام مسار المستند.
Signature signature = new Signature("path/to/your/document.pdf");
```

الآن بعد أن قمت بالإعداد، دعنا نستكشف كيفية الاستفادة من GroupDocs.Signature للعديد من الوظائف.

## دليل التنفيذ

### توقيع المستند باستخدام توقيع النص

تتيح لك هذه الميزة إضافة توقيعات نصية إلى مستند. لنبدأ بشرحها:

#### ملخص
يمكنك تخصيص مظهر وموضع توقيع النص الخاص بك باستخدام خيارات مختلفة مثل حجم الخط واللون والمحاذاة وما إلى ذلك.

#### التنفيذ خطوة بخطوة

**الخطوة 1**:قم بتحديد مسار الملف وموقع الإخراج.
```csharp
string filePath = "YOUR_DOCUMENT_DIRECTORY"; // المسار إلى المستند الأصلي
string outputFilePath = Path.Combine("YOUR_OUTPUT_DIRECTORY", "SignedDocument.docx");
```

**الخطوة 2**:إنشاء توقيع نصي باستخدام `TextSignOptions`.
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

**الخطوة 3**:توقيع الوثيقة وإخراج النتائج.
```csharp
    SignResult signResult = signature.Sign(outputFilePath, signOptions);
    foreach (BaseSignature temp in signResult.Succeeded)
    {
        Console.WriteLine($"Signed Text Signature: Id:{temp.SignatureId}, Location: {temp.Left}x{temp.Top}. Size: {temp.Width}x{temp.Height}");
    }
}
```

#### خيارات تكوين المفاتيح
- **المحاذاة الرأسية والمحاذاة الأفقية**:التحكم في مكان ظهور التوقيع على الصفحة.
- **الخط**:تخصيص حجم الخط ونمطه لتوقيع النص الخاص بك.

### التحقق من المستند للحصول على توقيع نصي

يضمن التحقق توقيع المستند كما هو مقصود. إليك كيفية تنفيذه:

#### ملخص
قم بالتحقق من التوقيعات النصية الموجودة في مستنداتك للتأكد من صحتها وسلامتها.

#### التنفيذ خطوة بخطوة

**الخطوة 1**:حدد مسار الملف للمستند الموقع.
```csharp
string filePath = "YOUR_OUTPUT_DIRECTORY"; // المسار إلى الوثيقة الموقعة
```

**الخطوة 2**:إنشاء خيارات التحقق باستخدام `TextVerifyOptions`.
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

**الخطوة 3**:التحقق من الوثيقة.
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

#### نصائح استكشاف الأخطاء وإصلاحها
- تأكد من `Text` تتطابق الخاصية تمامًا مع ما هو موجود في المستند.
- تأكد من ذلك `PageNumber` يتوافق مع الصفحة الصحيحة التي تحتوي على التوقيع.

### البحث عن توقيع النص في المستند

استخدم هذه الميزة للعثور على توقيعات النصوص داخل مستنداتك بكفاءة.

#### ملخص
ابحث في جميع الصفحات أو صفحات محددة من المستند للعثور على توقيعات نصية محددة.

#### التنفيذ خطوة بخطوة

**الخطوة 1**:تحديد مسار الملف.
```csharp
string filePath = "YOUR_OUTPUT_DIRECTORY"; // المسار إلى الوثيقة الموقعة
```

**الخطوة 2**: يستخدم `TextSearchOptions` للبحث.
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

**الخطوة 3**:تنفيذ البحث.
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

### تحديث توقيع نص المستند

تعديل التوقيعات النصية الموجودة في المستند عند الحاجة إلى ذلك.

#### ملخص
ضبط خصائص التوقيعات النصية الموجودة، مثل الحجم والموقع.

#### التنفيذ خطوة بخطوة

**الخطوة 1**:حدد مسار الملف ومعرفات التوقيع.
```csharp
string filePath = "YOUR_OUTPUT_DIRECTORY"; // المسار إلى الوثيقة الموقعة
List<string> signatureIds = new List<string>(); // افترض أن هذه القائمة مملوءة بمعرفات التوقيع الصالحة
```

**الخطوة 2**: يخلق `TextSignature` الأشياء للتحديثات.
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

**الخطوة 3**:تحديث المستند.
```csharp
        SignResult signResult = signature.UpdateSignatures(temp);
        if (signResult.Succeeded.Count > 0)
        {
            Console.WriteLine($"Updated Text Signature: Id:{temp.SignatureId}");
        }
    }
}
```

#### خيارات تكوين المفاتيح
- **العرض والارتفاع**:ضبط حجم التوقيع.
- **المحاذاة الأفقية**:التحكم في مكان ظهور التوقيع المحدث على الصفحة.

## خاتمة

باتباع هذا الدليل، ستتعلم كيفية توقيع التوقيعات النصية في المستندات، والتحقق منها، والبحث عنها، وتحديثها، وحذفها باستخدام GroupDocs.Signature لـ .NET. تُعد هذه الإمكانيات أساسية لأتمتة عمليات التوقيع الرقمي في تطبيقاتك. لمزيد من المعلومات التفصيلية والخيارات المتقدمة، راجع [الوثائق الرسمية](https://docs.groupdocs.com/signature/net/).