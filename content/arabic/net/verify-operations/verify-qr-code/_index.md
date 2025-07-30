---
"description": "تعرّف على كيفية التحقق من رموز الاستجابة السريعة (QR) في المستندات باستخدام GroupDocs.Signature لـ .NET. دليل شامل يتضمن أمثلة برمجية وأفضل الممارسات لمصادقة المستندات."
"linktitle": "التحقق من رمز الاستجابة السريعة"
"second_title": "واجهة برمجة تطبيقات GroupDocs.Signature .NET"
"title": "التحقق من رمز الاستجابة السريعة في المستندات"
"url": "/ar/net/verify-operations/verify-qr-code/"
"weight": 12
---

## مقدمة

يُعدّ أمن المستندات جانبًا بالغ الأهمية في العمليات التجارية الحديثة. وقد أصبحت رموز الاستجابة السريعة (QR codes) وسيلةً شائعةً بشكل متزايد لتضمين المعلومات في المستندات التي يُمكن التحقق من صحتها. يُوفّر GroupDocs.Signature for .NET حلاً فعّالاً ومرنًا للتحقق من رموز الاستجابة السريعة (QR codes) المُضمّنة في المستندات بمختلف التنسيقات.

سوف يرشدك هذا البرنامج التعليمي الشامل خلال عملية تنفيذ التحقق من رمز الاستجابة السريعة في تطبيقات .NET الخاصة بك، مما يضمن الحفاظ على سلامة مستنداتك وأصالتها.

## المتطلبات الأساسية

قبل تنفيذ وظيفة التحقق من رمز الاستجابة السريعة، تأكد من توفر المتطلبات الأساسية التالية:

1. GroupDocs.Signature لـ .NET: قم بتنزيل المكتبة وتثبيتها من [صفحة التحميل](https://releases.groupdocs.com/signature/net/).
2. بيئة التطوير: Visual Studio أو أي بيئة تطوير .NET متوافقة.
3. مستند الاختبار: مستند يحتوي على توقيعات رمز الاستجابة السريعة لأغراض التحقق.
4. المعرفة الأساسية: المعرفة ببرمجة C# ومفاهيم إطار عمل .NET.

## استيراد مساحات الأسماء

ابدأ باستيراد مساحات الأسماء المطلوبة للوصول إلى وظيفة GroupDocs.Signature:

```csharp
using System;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

## عملية التحقق من رمز الاستجابة السريعة (QR Code) خطوة بخطوة

اتبع الخطوات التفصيلية التالية للتحقق من رموز الاستجابة السريعة (QR) الموجودة في مستنداتك:

### الخطوة 1: تحديد مسار المستند

```csharp
// توفير المسار إلى المستند الذي يحتوي على توقيعات رمز الاستجابة السريعة
string filePath = "sample_multiple_signatures.docx";
```

تأكد من استبدال مسار المثال بالمسار الفعلي للمستند الخاص بك.

### الخطوة 2: تهيئة كائن التوقيع

```csharp
// إنشاء مثيل توقيع عن طريق تمرير مسار المستند
using (Signature signature = new Signature(filePath))
{
    // سيتم تنفيذ رمز التحقق هنا
}
```

فئة التوقيع هي نقطة الدخول الرئيسية لجميع العمليات في واجهة برمجة التطبيقات GroupDocs.Signature.

### الخطوة 3: تكوين خيارات التحقق من رمز الاستجابة السريعة

```csharp
// تحديد خيارات التحقق من رمز الاستجابة السريعة
QrCodeVerifyOptions options = new QrCodeVerifyOptions()
{
    AllPages = true, // التحقق من جميع صفحات الوثيقة
    Text = "John",   // نص للتحقق داخل رمز الاستجابة السريعة
    MatchType = TextMatchType.Contains // حدد معايير مطابقة النص
};
```

تتيح لك خيارات التحقق تحديد معايير محددة لعملية التحقق:
- `AllPages`:تم ضبطه على "صحيح" للتحقق من جميع صفحات المستند (السلوك الافتراضي)
- `Text`:محتوى النص الذي يجب مطابقته داخل رمز الاستجابة السريعة
- `MatchType`:طريقة مطابقة النص (يحتوي على، دقيق، يبدأ بـ، إلخ.)

### الخطوة 4: تنفيذ عملية التحقق

```csharp
// إجراء التحقق
VerificationResult result = signature.Verify(options);
```

يؤدي هذا إلى تنفيذ عملية التحقق استنادًا إلى الخيارات التي حددتها.

### الخطوة 5: نتائج التحقق من العملية

```csharp
// التحقق من نتيجة التحقق والمعالجة وفقًا لذلك
if (result.IsValid)
{
    Console.WriteLine($"Document {filePath} contains valid QR code signature!");
    
    // عرض معلومات حول التوقيعات الناجحة
    foreach (QrCodeSignature signature in result.Succeeded)
    {
        Console.WriteLine($"Found valid QR Code signature with text: {signature.Text}");
        Console.WriteLine($"QR Code type: {signature.EncodeType.TypeName}");
        Console.WriteLine($"Location: Page {signature.PageNumber}, {signature.Left}x{signature.Top}");
    }
}
else
{
    Console.WriteLine($"Document {filePath} failed verification process.");
    Console.WriteLine($"Number of failed signatures: {result.Failed.Count}");
}
```

إن التعامل الصحيح مع نتيجة التحقق يسمح لتطبيقك باتخاذ الإجراءات المناسبة بناءً على نتيجة التحقق.

## مثال كامل

فيما يلي مثال كامل وعملي يوضح عملية التحقق من رمز الاستجابة السريعة (QR code):

```csharp
using System;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;

namespace GroupDocs.Signature.Examples
{
    class Program
    {
        static void Main(string[] args)
        {
            // مسار المستند
            string filePath = "sample_multiple_signatures.docx";
            
            // تهيئة مثيل التوقيع
            using (Signature signature = new Signature(filePath))
            {
                // إعداد خيارات التحقق
                QrCodeVerifyOptions options = new QrCodeVerifyOptions()
                {
                    AllPages = true,
                    Text = "John",
                    MatchType = TextMatchType.Contains
                };
                
                // التحقق من توقيعات المستندات
                VerificationResult result = signature.Verify(options);
                
                // نتائج التحقق من العملية
                if (result.IsValid)
                {
                    Console.WriteLine($"Document {filePath} contains valid QR code signature!");
                    
                    foreach (QrCodeSignature qrSignature in result.Succeeded)
                    {
                        Console.WriteLine($"Found valid QR Code with text: {qrSignature.Text}");
                    }
                }
                else
                {
                    Console.WriteLine($"Document {filePath} failed verification process.");
                }
            }
        }
    }
}
```

## خيارات التحقق المتقدمة

يوفر GroupDocs.Signature خيارات إضافية لسيناريوهات التحقق الأكثر تعقيدًا:

### التحقق من أنواع رموز الاستجابة السريعة المحددة

```csharp
QrCodeVerifyOptions options = new QrCodeVerifyOptions()
{
    EncodeType = QrCodeTypes.QR,  // التحقق من رموز الاستجابة السريعة القياسية فقط
    Text = "Confidential",
    MatchType = TextMatchType.Exact
};
```

### التحقق من صفحات محددة

```csharp
QrCodeVerifyOptions options = new QrCodeVerifyOptions()
{
    AllPages = false,
    PageNumber = 2,  // التحقق فقط في الصفحة 2
    Text = "Approved"
};
```

### استخدام التعبيرات العادية للتحقق

```csharp
QrCodeVerifyOptions options = new QrCodeVerifyOptions()
{
    Text = "INV-\\d{6}",  // مطابقة أرقام الفاتورة (على سبيل المثال، INV-123456)
    MatchType = TextMatchType.Regex
};
```

## أفضل الممارسات للتحقق من رمز الاستجابة السريعة

1. التحقق دائمًا من صحة المدخلات: تأكد من صحة مسارات المستندات ومعايير التحقق قبل المعالجة.
2. تنفيذ معالجة الأخطاء: استخدم كتل try-catch للتعامل مع الاستثناءات المحتملة أثناء التحقق.
3. خذ الأداء في الاعتبار: بالنسبة للمستندات الكبيرة، فكر في التحقق من صفحات محددة بدلاً من المستند بأكمله.
4. نتائج التحقق من السجل: الاحتفاظ بسجلات عمليات التحقق لأغراض التدقيق.
5. الاختبار باستخدام تنسيقات المستندات المختلفة: تأكد من أن عملية التحقق الخاصة بك تعمل عبر جميع تنسيقات المستندات المطلوبة.

## خاتمة

يُعدّ التحقق من رموز الاستجابة السريعة (QR Codes) في المستندات جانبًا أساسيًا لضمان مصداقيتها وسلامتها. يوفر GroupDocs.Signature for .NET واجهة برمجة تطبيقات شاملة وسهلة الاستخدام لتطبيق التحقق من رموز الاستجابة السريعة في تطبيقات .NET.

من خلال اتباع هذا البرنامج التعليمي، تعلمت كيفية:
- تكوين عملية التحقق وبدء تشغيلها
- تحديد معايير التحقق المختلفة
- معالجة وتفسير نتائج التحقق
- تنفيذ خيارات التحقق المتقدمة

تمكنك هذه المعرفة من تعزيز أمان وموثوقية أنظمة إدارة المستندات الخاصة بك.

## الأسئلة الشائعة

### هل يمكن لـ GroupDocs.Signature التحقق من رموز QR المتعددة في مستند واحد؟
نعم، يُمكن لـ GroupDocs.Signature التحقق من رموز QR متعددة في مستند واحد. ستتضمن نتائج التحقق جميع رموز QR المطابقة.

### ما هي تنسيقات المستندات المدعومة للتحقق من رمز الاستجابة السريعة؟
يدعم GroupDocs.Signature مجموعة واسعة من تنسيقات المستندات بما في ذلك PDF، وWord (DOC، DOCX)، وExcel (XLS، XLSX)، وPowerPoint (PPT، PPTX)، والصور، والمزيد.

### هل يمكنني التحقق من رموز الاستجابة السريعة QR باستخدام تشفير أو تنسيق محدد؟
نعم، يوفر GroupDocs.Signature خيارات للتحقق من رموز QR باستخدام أنواع ترميز محددة وأنماط تنسيق المحتوى.

### هل من الممكن التحقق من رموز الاستجابة السريعة QR التي تم إنشاؤها بواسطة تطبيقات الطرف الثالث؟
نعم، يمكن لـ GroupDocs.Signature التحقق من رموز QR القياسية التي تم إنشاؤها بواسطة معظم التطبيقات، طالما أنها تتبع تنسيقات رموز QR القياسية.

### كيف أتعامل مع رموز الاستجابة السريعة QR التي تحتوي على بيانات ثنائية بدلاً من النص؟
يوفر GroupDocs.Signature خيارات للتحقق من رموز QR باستخدام البيانات الثنائية من خلال `BinaryData` خاصية خيارات التحقق.

### الموارد ذات الصلة
* [مرجع API لـ GroupDocs.Signature](https://reference.groupdocs.com/signature/net/)
* [تنزيلات GroupDocs.Signature](https://releases.groupdocs.com/signature/net/)
* [أمثلة التعليمات البرمجية على GitHub](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
* [التوثيق](https://docs.groupdocs.com/signature/net/)
* [صفحة المنتج](https://products.groupdocs.com/signature/net/)
* [مقالات المدونة](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
* [منتدى الدعم](https://forum.groupdocs.com/c/signature/13)
* [رخصة مؤقتة](https://purchase.groupdocs.com/temporary-license/)