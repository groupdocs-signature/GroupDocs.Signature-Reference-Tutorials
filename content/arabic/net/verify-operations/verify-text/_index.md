---
"description": "إتقان التحقق من توقيع النص في تطبيقات .NET باستخدام GroupDocs.Signature. دليل تنفيذ خطوة بخطوة مع أمثلة برمجية كاملة وأفضل الممارسات."
"linktitle": "التحقق من النص"
"second_title": "واجهة برمجة تطبيقات GroupDocs.Signature .NET"
"title": "التحقق من التوقيعات النصية في المستندات"
"url": "/ar/net/verify-operations/verify-text/"
"weight": 13
type: docs
---
## مقدمة

رغم أن التوقيعات النصية غالبًا ما تكون أبسط من التوقيعات الرقمية أو الإلكترونية، إلا أنها تلعب دورًا محوريًا في إدارة المستندات والتحقق منها. سواءً كانت علامات مائية، أو نصًا في التذييل، أو أنماط محتوى محددة، فإن التحقق من وجود التوقيعات النصية وسلامتها يُعد جانبًا مهمًا في عمليات التحقق من المستندات.

يوفر GroupDocs.Signature لـ .NET واجهة برمجة تطبيقات فعّالة للتحقق من تواقيع النصوص داخل المستندات عبر مجموعة واسعة من التنسيقات. سيرشدك هذا البرنامج التعليمي الشامل خلال عملية تطبيق وظيفة التحقق من النصوص في تطبيقات .NET، مما يضمن الحفاظ على سلامة مستنداتك وأصالتها.

## المتطلبات الأساسية

قبل تنفيذ وظيفة التحقق من النص، تأكد من توفر المتطلبات الأساسية التالية:

1. GroupDocs.Signature لـ .NET: قم بتنزيل المكتبة وتثبيتها من [صفحة التحميل](https://releases.groupdocs.com/signature/net/).
2. بيئة تطوير .NET: Visual Studio أو أي بيئة تطوير .NET متوافقة.
3. المعرفة الأساسية: المعرفة ببرمجة C# ومفاهيم إطار عمل .NET.
4. مستند الاختبار: مستند يحتوي على توقيعات نصية لأغراض التحقق.

## استيراد مساحات الأسماء المطلوبة

ابدأ باستيراد مساحات الأسماء الضرورية للوصول إلى وظيفة GroupDocs.Signature:

```csharp
using System;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

دعونا نقسم عملية التحقق من النص إلى خطوات واضحة وقابلة للإدارة:

## الخطوة 1: تحديد مسار المستند

```csharp
// المسار إلى المستند الذي يحتوي على توقيعات نصية
string filePath = "sample_multiple_signatures.docx";
```

تأكد من استبدال مسار المثال بالمسار الفعلي للمستند الذي يحتوي على توقيعات نصية.

## الخطوة 2: تهيئة كائن التوقيع

```csharp
// إنشاء مثيل لفئة التوقيع عن طريق تمرير مسار المستند
using (Signature signature = new Signature(filePath))
{
    // سيتم تنفيذ رمز التحقق هنا
}
```

فئة التوقيع هي نقطة الدخول الرئيسية لجميع العمليات في واجهة برمجة التطبيقات GroupDocs.Signature.

## الخطوة 3: تكوين خيارات التحقق من النص

```csharp
// تحديد خيارات التحقق من النص
TextVerifyOptions options = new TextVerifyOptions()
{
    AllPages = true,                               // التحقق من جميع صفحات الوثيقة
    SignatureImplementation = TextSignatureImplementation.Native,
    Text = "signature",                            // النص المراد التحقق منه
    MatchType = TextMatchType.Contains             // تحديد معايير المطابقة
};
```

تتيح لك خيارات التحقق تحديد معايير محددة لعملية التحقق:
- `AllPages`:اضبط على "صحيح" للتحقق من جميع صفحات المستند
- `SignatureImplementation`:حدد كيفية تنفيذ النص (أصلي أو ملصق)
- `Text`:محتوى النص الذي يجب مطابقته داخل المستند
- `MatchType`:طريقة مطابقة النص (يحتوي على، دقيق، يبدأ بـ، إلخ.)

## الخطوة 4: تنفيذ عملية التحقق

```csharp
// إجراء التحقق
VerificationResult result = signature.Verify(options);
```

يؤدي هذا إلى تنفيذ عملية التحقق استنادًا إلى الخيارات التي حددتها.

## الخطوة 5: نتائج التحقق من العملية

```csharp
// التحقق من نتيجة التحقق والمعالجة وفقًا لذلك
if (result.IsValid)
{
    Console.WriteLine($"Document {filePath} contains valid text signatures!");
    
    // عرض معلومات حول التوقيعات الناجحة
    foreach (TextSignature textSignature in result.Succeeded)
    {
        Console.WriteLine($"\nFound valid text signature:");
        Console.WriteLine($"Text: {textSignature.Text}");
        Console.WriteLine($"Location: Page {textSignature.PageNumber}, {textSignature.Left}x{textSignature.Top}");
    }
}
else
{
    Console.WriteLine($"Document {filePath} failed verification process.");
    Console.WriteLine($"Number of failed signatures: {result.Failed.Count}");
}
```

يتحقق هذا الرمز من نجاح التحقق ويوفر معلومات مفصلة حول التوقيعات النصية التي تم التحقق منها.

## مثال كامل

فيما يلي مثال عملي كامل يوضح كيفية التحقق من توقيع النص:

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
            
            try
            {
                // تهيئة مثيل التوقيع
                using (Signature signature = new Signature(filePath))
                {
                    // إعداد خيارات التحقق
                    TextVerifyOptions options = new TextVerifyOptions()
                    {
                        AllPages = true,
                        SignatureImplementation = TextSignatureImplementation.Native,
                        Text = "signature",
                        MatchType = TextMatchType.Contains
                    };
                    
                    // التحقق من توقيعات المستندات
                    VerificationResult result = signature.Verify(options);
                    
                    // نتائج التحقق من العملية
                    if(result.IsValid)
                    {
                        Console.WriteLine($"\nDocument {filePath} was verified successfully!");
                        foreach (TextSignature item in result.Succeeded)
                        {
                            Console.WriteLine($"\nValid signature is found with text: {item.Text}");
                            Console.WriteLine($"Location: Page {item.PageNumber}, position {item.Left}x{item.Top}");
                        }
                    }
                    else
                    {
                        Console.WriteLine($"\nDocument {filePath} failed verification process.");
                    }
                }
            }
            catch (Exception ex)
            {
                Console.WriteLine($"Error: {ex.Message}");
            }
        }
    }
}
```

## سيناريوهات التحقق المتقدمة

يوفر GroupDocs.Signature خيارات إضافية لسيناريوهات التحقق الأكثر تعقيدًا:

### استخدام التعبيرات العادية للتحقق

للحصول على مطابقة نمطية أكثر مرونة، يمكنك استخدام التعبيرات العادية:

```csharp
TextVerifyOptions options = new TextVerifyOptions()
{
    Text = "Invoice\\s+#\\d{5,6}",  // تطابق الأنماط مثل "الفاتورة رقم 12345"
    MatchType = TextMatchType.Regex
};
```

### التحقق من النص في مناطق محددة من المستند

يمكنك تقييد التحقق على مناطق محددة من المستند:

```csharp
TextVerifyOptions options = new TextVerifyOptions()
{
    AllPages = false,
    PageNumber = 1,  // التحقق فقط من الصفحة الأولى
    
    // تحديد المنطقة التي سيتم البحث فيها (الإحداثيات بالنقاط)
    PagesSetup = new PagesSetup() 
    { 
        FirstPage = true,
        LastPage = false,
        OddPages = false,
        EvenPages = false 
    },
    
    // مساحة المستطيل بالملليمتر
    Rectangle = new Rectangle(10, 10, 100, 30),
    
    Text = "Confidential"
};
```

### التحقق من أنماط نصية متعددة في وقت واحد

يمكنك إنشاء خيارات تحقق متعددة للتحقق من أنماط النص المختلفة:

```csharp
// إنشاء قائمة بخيارات التحقق
List<VerifyOptions> listOptions = new List<VerifyOptions>();

// إضافة التحقق من النص الأول
listOptions.Add(new TextVerifyOptions()
{
    Text = "Confidential",
    MatchType = TextMatchType.Exact
});

// إضافة التحقق من النص الثاني
listOptions.Add(new TextVerifyOptions()
{
    Text = "Do not copy",
    MatchType = TextMatchType.Contains
});

// التحقق باستخدام خيارات متعددة
VerificationResult result = signature.Verify(listOptions);
```

### التحقق من النص من خلال المظهر المحدد

يمكنك أيضًا التحقق من النص باستخدام خصائص التنسيق المحددة:

```csharp
TextVerifyOptions options = new TextVerifyOptions()
{
    Text = "APPROVED",
    MatchType = TextMatchType.Exact,
    
    // التحقق من خصائص المظهر المحددة
    ForegroundColorRGB = System.Drawing.Color.Green,
    Font = new SignatureFont() { FontFamily = "Arial", FontSize = 12, Bold = true }
};
```

## أفضل الممارسات للتحقق من النص

1. اختر أنواع المطابقة المناسبة: حدد نوع المطابقة الصحيح (يحتوي على، دقيق، Regex) استنادًا إلى متطلبات التحقق الخاصة بك.
2. تحسين الأداء: بالنسبة للمستندات الكبيرة، فكر في التحقق من صفحات محددة بدلاً من المستند بأكمله.
3. معالجة الأخطاء: تنفيذ معالجة الأخطاء بشكل صحيح لإدارة السيناريوهات غير المتوقعة بسلاسة.
4. ضع حساسية الحالة في الاعتبار: ضع حساسية الحالة في الاعتبار عند مطابقة النص، وخاصةً للتحققات الحرجة.
5. اختبار شامل: اختبار التحقق باستخدام تنسيقات المستندات المختلفة وأنماط النص لضمان التوافق.

## استكشاف الأخطاء وإصلاحها

### لم يتم اكتشاف النص
- تحقق مما إذا كان تنسيق النص أو ترميزه يؤثر على الكشف
- تأكد من أن النص موجود فعليًا في المستند كنص عادي (وليس صورة)
- جرب معايير مطابقة مختلفة (يحتوي على بدلاً من مطابق تمامًا)

### مشاكل الأداء
- تحسين التحقق من خلال استهداف صفحات أو مناطق محددة
- استخدم أنماط نصية أكثر تحديدًا لتقليل النتائج الإيجابية الخاطئة

### فشل التحقق
- تحقق مما إذا كانت المسافات أو الأحرف الخاصة أو التنسيق تؤثر على المطابقة
- التحقق من أن النص ليس جزءًا من الصورة الممسوحة ضوئيًا (التي تتطلب التعرف الضوئي على الحروف)
- تأكد من عدم تعديل المستند منذ إضافة النص

## خاتمة

يُعد التحقق من النصوص أسلوبًا عمليًا ومتعدد الاستخدامات لمصادقة المستندات، ويمكن استخدامه بمفرده أو مع طرق تحقق أخرى. يوفر GroupDocs.Signature لـ .NET واجهة برمجة تطبيقات شاملة وسهلة الاستخدام لتطبيق وظائف تحقق نصوص فعّالة في تطبيقات .NET.

من خلال اتباع هذا الدليل خطوة بخطوة، ستتعلم كيفية:
- تكوين وتفعيل عملية التحقق من النص
- تحديد معايير التحقق المختلفة
- معالجة وتفسير نتائج التحقق
- تنفيذ سيناريوهات التحقق المتقدمة

تتيح لك هذه الإمكانيات إنشاء أنظمة معالجة مستندات آمنة وموثوقة يمكنها التحقق من صحة النص عبر تنسيقات المستندات المختلفة.

## الأسئلة الشائعة

### هل يمكن لـ GroupDocs.Signature التحقق من النص في المستندات الممسوحة ضوئيًا؟
صُمم GroupDocs.Signature أساسًا للتحقق من النصوص الرقمية. بالنسبة للمستندات الممسوحة ضوئيًا، ستحتاج أولًا إلى استخدام تقنية التعرف الضوئي على الحروف (OCR) لتحويل الصور الممسوحة ضوئيًا إلى نص.

### ما هي تنسيقات المستندات المدعومة للتحقق من النص؟
يدعم GroupDocs.Signature مجموعة واسعة من تنسيقات المستندات بما في ذلك PDF، ومستندات Word (DOC، DOCX)، وجداول بيانات Excel (XLS، XLSX)، وعروض PowerPoint (PPT، PPTX)، والصور، والمزيد.

### هل يمكنني التحقق من تنسيق النص (غامق، مائل، خطوط محددة)؟
نعم، يوفر GroupDocs.Signature خيارات للتحقق من النص باستخدام خصائص تنسيق محددة بما في ذلك عائلة الخط والحجم والنمط (غامق، مائل) واللون.

### هل من الممكن التحقق من النص في المستندات المحمية بكلمة مرور؟
نعم، يوفر GroupDocs.Signature خيارات لتحديد كلمات مرور المستندات عند فتح المستندات المحمية للتحقق منها.

### هل يمكنني التحقق من العلامات المائية والنص الخلفي؟
نعم، يمكن لـ GroupDocs.Signature التحقق من أنواع مختلفة من توقيعات النصوص بما في ذلك العلامات المائية والنص الخلفي، اعتمادًا على كيفية تنفيذها في المستند.

### الموارد ذات الصلة
* [مرجع API لـ GroupDocs.Signature](https://reference.groupdocs.com/signature/net/)
* [تنزيلات GroupDocs.Signature](https://releases.groupdocs.com/signature/net/)
* [أمثلة التعليمات البرمجية على GitHub](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
* [التوثيق](https://docs.groupdocs.com/signature/net/)
* [صفحة المنتج](https://products.groupdocs.com/signature/net/)
* [مقالات المدونة](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
* [منتدى الدعم](https://forum.groupdocs.com/c/signature/13)
* [رخصة مؤقتة](https://purchase.groupdocs.com/temporary-license/)