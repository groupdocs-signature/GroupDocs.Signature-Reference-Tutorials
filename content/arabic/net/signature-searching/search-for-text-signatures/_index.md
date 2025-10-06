---
"description": "تعرف على كيفية البحث بكفاءة عن التوقيعات النصية في المستندات باستخدام GroupDocs.Signature لـ .NET باستخدام دليلنا الشامل خطوة بخطوة وأمثلة التعليمات البرمجية."
"linktitle": "البحث عن توقيعات النص"
"second_title": "واجهة برمجة تطبيقات GroupDocs.Signature .NET"
"title": "البحث عن التوقيعات النصية في المستندات"
"url": "/ar/net/signature-searching/search-for-text-signatures/"
"weight": 16
type: docs
---
## مقدمة

تُعد التوقيعات النصية وسيلة شائعة للإشارة إلى تأليف المستندات أو الموافقة عليها أو التحقق منها. في إدارة المستندات الرقمية، تُعد القدرة على البحث البرمجي عن التوقيعات النصية واستخراجها أمرًا بالغ الأهمية للتحقق من صحة المستندات، وأتمتة سير العمل، والتحقق من الامتثال. يوفر GroupDocs.Signature لـ .NET حلاً شاملاً لتطبيق وظيفة البحث عن التوقيعات النصية في تطبيقات .NET، مع دعم تنسيقات مستندات متنوعة وإمكانيات بحث متقدمة.

سوف يرشدك هذا البرنامج التعليمي خلال عملية البحث عن التوقيعات النصية في المستندات باستخدام GroupDocs.Signature لـ .NET، مع توفير تفسيرات مفصلة وتعليمات خطوة بخطوة وأمثلة عملية للكود.

## المتطلبات الأساسية

قبل الغوص في البحث عن توقيع النص، تأكد من أن لديك المتطلبات الأساسية التالية:

1. GroupDocs.Signature لمكتبة .NET: قم بتنزيل المكتبة وتثبيتها من [صفحة الإصدارات](https://releases.groupdocs.com/signature/net/).

2. بيئة التطوير: قم بإعداد بيئة تطوير مناسبة مثل Visual Studio أو أي IDE متوافق مع دعم .NET.

3. المستندات النموذجية: إعداد مستندات الاختبار التي تحتوي على توقيعات نصية للتحقق والاختبار.

4. المعرفة الأساسية بلغة C#: المعرفة بلغة البرمجة C# ومفاهيم إطار عمل .NET.

## استيراد مساحات الأسماء

ابدأ باستيراد مساحات الأسماء الضرورية للوصول إلى وظيفة GroupDocs.Signature:

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

الآن، دعونا نقسم عملية البحث عن توقيعات النص إلى خطوات واضحة وقابلة للإدارة:

## الخطوة 1: تحميل المستند

أولاً، قم بتحديد مسار المستند وتهيئة `Signature` هدف:

```csharp
string filePath = "sample_multiple_signatures.docx";
string fileName = Path.GetFileName(filePath);

using (Signature signature = new Signature(filePath))
{
    // سيتم إضافة كود البحث عن توقيع النص هنا
}
```

## الخطوة 2: تكوين خيارات البحث

إنشاء وتكوين `TextSearchOptions` لتحديد كيفية البحث عن توقيعات النص:

```csharp
// تكوين خيارات البحث النصي
TextSearchOptions options = new TextSearchOptions
{
    // البحث في جميع الصفحات
    AllPages = true,
    
    // اختياري: حدد النص المطابق
    // النص = "موافق عليه"،
    
    // اختياري: حدد نوع المطابقة
    // MatchType = TextMatchType.يحتوي على
};
```

## الخطوة 3: إجراء بحث عن توقيع النص

قم بتنفيذ عملية البحث باستخدام الخيارات المحددة:

```csharp
// البحث عن توقيعات النص
List<TextSignature> signatures = signature.Search<TextSignature>(options);
```

## الخطوة 4: معالجة النتائج وعرضها

قم بالتكرار خلال توقيعات النص الموجودة وعرض تفاصيلها:

```csharp
// عرض نتائج البحث
Console.WriteLine($"\nSource document '{fileName}' contains {signatures.Count} text signature(s):");

foreach (TextSignature textSignature in signatures)
{
    Console.WriteLine($"Text signature found at page {textSignature.PageNumber} with text '{textSignature.Text}'");
    Console.WriteLine($"Location: X={textSignature.Left}, Y={textSignature.Top}, Width={textSignature.Width}, Height={textSignature.Height}");
    Console.WriteLine($"Signature type: {textSignature.SignatureImplementation}");
    Console.WriteLine();
}
```

## مثال كامل

فيما يلي مثال عملي كامل يوضح كيفية البحث عن توقيعات النص في مستند:

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;

namespace TextSignatureSearch
{
    class Program
    {
        static void Main(string[] args)
        {
            // مسار المستند - التحديث باستخدام مسار الملف الخاص بك
            string filePath = "sample_multiple_signatures.docx";
            string fileName = Path.GetFileName(filePath);
            
            // تهيئة مثيل التوقيع
            using (Signature signature = new Signature(filePath))
            {
                try
                {
                    // تكوين خيارات البحث النصي
                    TextSearchOptions options = new TextSearchOptions
                    {
                        // البحث في جميع الصفحات
                        AllPages = true
                    };
                    
                    // البحث عن توقيعات النص
                    List<TextSignature> signatures = signature.Search<TextSignature>(options);
                    
                    // عرض نتائج البحث
                    Console.WriteLine($"\nSource document '{fileName}' contains {signatures.Count} text signature(s):");
                    
                    foreach (TextSignature textSignature in signatures)
                    {
                        Console.WriteLine($"Text signature found at page {textSignature.PageNumber} with text '{textSignature.Text}'");
                        Console.WriteLine($"Location: X={textSignature.Left}, Y={textSignature.Top}, Width={textSignature.Width}, Height={textSignature.Height}");
                        Console.WriteLine($"Signature type: {textSignature.SignatureImplementation}");
                        Console.WriteLine();
                    }
                }
                catch (Exception ex)
                {
                    Console.WriteLine($"Error occurred: {ex.Message}");
                }
            }
            
            Console.WriteLine("Press any key to exit...");
            Console.ReadKey();
        }
    }
}
```

## تقنيات البحث المتقدمة عن توقيع النص

### البحث باستخدام معايير نصية محددة

لإجراء عمليات بحث أكثر استهدافًا، يمكنك تخصيص `TextSearchOptions` للتصفية حسب محتوى نص معين:

```csharp
// إنشاء خيارات البحث باستخدام معايير نصية محددة
TextSearchOptions options = new TextSearchOptions
{
    // البحث في جميع الصفحات
    AllPages = true,
    
    // البحث عن نص محدد
    Text = "Approved",
    
    // حدد نوع المطابقة (يحتوي على، دقيق، يبدأ بـ، ينتهي بـ)
    MatchType = TextMatchType.Contains,
    
    // البحث الحساس لحالة الأحرف
    MatchCase = true
};
```

### البحث في مناطق محددة من المستندات

يمكنك تقييد البحث على مناطق محددة من المستند:

```csharp
// إنشاء خيارات البحث لمنطقة مستند محددة
TextSearchOptions options = new TextSearchOptions
{
    // البحث فقط في صفحات محددة
    AllPages = false,
    PageNumber = 1,
    
    // أو حدد صفحات متعددة
    PagesSetup = new PagesSetup { Pages = new List<int> { 1, 3, 5 } },
    
    // تحديد منطقة محددة للبحث داخلها
    Rectangle = new Rectangle(100, 100, 400, 200)
};
```

### تصفية النصوص المتقدمة

تنفيذ منطق التصفية المخصص لمتطلبات البحث الأكثر تعقيدًا:

```csharp
// إنشاء خيارات البحث باستخدام المعالجة المخصصة
TextSearchOptions options = new TextSearchOptions
{
    AllPages = true,
    
    // تعريف المعالجة المخصصة باستخدام المندوب
    ProcessCompleted = (TextSignature signature) =>
    {
        // منطق التحقق المخصص
        bool isValid = signature.Text.Length > 5 && 
                      (signature.Text.Contains("Approved") || signature.Text.Contains("Verified"));
        
        return isValid;
    }
};
```

### البحث عن أنماط نصية مختلفة

استخدم خصائص الخط والنمط لتصفية توقيعات النص:

```csharp
// إنشاء خيارات بحث تستهدف مظهر نص معين
TextSearchOptions options = new TextSearchOptions
{
    // تصفية حسب اسم الخط
    FontName = "Arial",
    
    // تصفية حسب نطاق حجم الخط
    MinFontSize = 10,
    MaxFontSize = 14,
    
    // تصفية حسب لون الخط
    ForeColor = System.Drawing.Color.Blue
};
```

### استخراج بيانات التعريف الخاصة بالتوقيع

استخراج ومعالجة البيانات الوصفية المرتبطة بتوقيعات النصوص:

```csharp
foreach (TextSignature signature in signatures)
{
    // بيانات تعريف توقيع الوصول
    if (signature.Metadata != null && signature.Metadata.Count > 0)
    {
        Console.WriteLine("Signature Metadata:");
        
        foreach (var item in signature.Metadata)
        {
            Console.WriteLine($"  {item.Key}: {item.Value}");
        }
    }
    
    // التحقق من تواريخ إنشاء التوقيع وتعديله
    if (signature.CreatedOn.HasValue)
    {
        Console.WriteLine($"Created on: {signature.CreatedOn.Value}");
    }
    
    if (signature.ModifiedOn.HasValue)
    {
        Console.WriteLine($"Modified on: {signature.ModifiedOn.Value}");
    }
}
```

## خاتمة

في هذا الدليل الشامل، استكشفنا كيفية البحث عن توقيعات النصوص في المستندات باستخدام GroupDocs.Signature لـ .NET. من عمليات البحث الأساسية إلى التقنيات المتقدمة، أصبحت لديك الآن المعرفة اللازمة لتطبيق وظيفة توقيع نصي فعّالة في تطبيقات .NET الخاصة بك.

يوفر GroupDocs.Signature إطار عمل قويًا ومرنًا للعمل مع توقيعات النصوص، مما يتيح لك إنشاء أنظمة متطورة للتحقق من المستندات، وحلول سير العمل الآلية، وأدوات التحقق من الامتثال.

## الأسئلة الشائعة

### هل يمكنني البحث عن التوقيعات النصية في المستندات المحمية بكلمة مرور؟

نعم، يدعم GroupDocs.Signature البحث عن التوقيعات النصية في المستندات المحمية بكلمة مرور. يمكنك إدخال كلمة المرور عند تهيئة `Signature` هدف:

```csharp
LoadOptions loadOptions = new LoadOptions { Password = "your_password" };
using (Signature signature = new Signature(filePath, loadOptions))
{
    // البحث عن توقيعات النص
}
```

### ما هي تنسيقات المستندات المدعومة للبحث عن توقيع النص؟

يدعم GroupDocs.Signature مجموعة واسعة من تنسيقات المستندات بما في ذلك PDF، ومستندات Microsoft Office (Word، Excel، PowerPoint)، وتنسيقات OpenOffice، والصور، والمزيد.

### هل يمكنني البحث عن توقيعات نصية بتنسيق محدد مثل غامق أو مائل؟

نعم، يمكنك البحث عن توقيعات نصية بتنسيق محدد باستخدام `FontBold` و `FontItalic` العقارات في `TextSearchOptions`:

```csharp
TextSearchOptions options = new TextSearchOptions
{
    FontBold = true,
    FontItalic = true
};
```

### كيف يمكنني تحسين أداء البحث للمستندات الكبيرة؟

بالنسبة للمستندات الكبيرة، يمكنك تحسين أداء البحث من خلال:

1. تقييد البحث على صفحات محددة بدلاً من البحث في المستند بأكمله
2. استخدام معايير بحث أكثر تحديدًا لتقليل عدد المطابقات
3. تحديد منطقة البحث باستخدام `Rectangle` الممتلكات إذا كنت تعرف مكان وجود التوقيعات عادةً
4. تنفيذ الترقيم الصفحي في تطبيقك لمعالجة نتائج البحث على دفعات

### هل يمكنني معرفة ما إذا كان التوقيع النصي قد تمت إضافته إلكترونيًا أو أنه جزء من محتوى المستند الأصلي؟

يمكن لـ GroupDocs.Signature التمييز بين أنواع مختلفة من عناصر النص في المستندات. `SignatureImplementation` ممتلكات `TextSignature` يُشير إلى ما إذا كان النص توقيعًا رسميًا أم محتوىً عاديًا في مستند. مع ذلك، قد يعتمد التحديد النهائي على كيفية إضافة النص إلى المستند في الأصل.

## انظر أيضا

* [مرجع واجهة برمجة التطبيقات](https://reference.groupdocs.com/signature/net/)
* [أمثلة التعليمات البرمجية على GitHub](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
* [وثائق المنتج](https://docs.groupdocs.com/signature/net/)
* [صفحة المنتج](https://products.groupdocs.com/signature/net/)
* [تنزيل أحدث إصدار](https://releases.groupdocs.com/signature/net/)
* [مقالات المدونة](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
* [منتدى الدعم المجاني](https://forum.groupdocs.com/c/signature/13)
* [رخصة مؤقتة](https://purchase.groupdocs.com/temporary-license/)