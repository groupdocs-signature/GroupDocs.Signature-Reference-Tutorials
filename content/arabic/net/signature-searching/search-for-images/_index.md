---
"description": "تعرف على كيفية البحث بكفاءة عن توقيعات الصور في المستندات باستخدام GroupDocs.Signature لـ .NET مع أمثلة خطوة بخطوة وإرشادات التنفيذ الشاملة."
"linktitle": "البحث عن الصور"
"second_title": "واجهة برمجة تطبيقات GroupDocs.Signature .NET"
"title": "البحث عن توقيعات الصور في المستندات"
"url": "/ar/net/signature-searching/search-for-images/"
"weight": 13
---

## مقدمة

في بيئة المستندات الرقمية الحالية، تُعدّ تواقيع الصور بمثابة علامات بصرية فعّالة للعلامات التجارية والتفويض والتحقق من صحة المستندات. يوفر GroupDocs.Signature لـ .NET إطار عمل شاملًا للمطورين للبحث عن تواقيع الصور وتحديدها ومعالجتها بسلاسة داخل المستندات بمختلف تنسيقاتها. تُعد هذه الإمكانية أساسية للتطبيقات التي تتطلب التحقق من المستندات، أو تحليل محتواها، أو المعالجة الآلية للمستندات الموقعة.

سوف يرشدك هذا البرنامج التعليمي خلال عملية تنفيذ وظيفة البحث عن توقيع الصورة في تطبيقات .NET الخاصة بك باستخدام GroupDocs.Signature، مع تفسيرات واضحة وأمثلة عملية للكود.

## المتطلبات الأساسية

قبل الغوص في البحث عن توقيع الصورة باستخدام GroupDocs.Signature لـ .NET، تأكد من أن لديك المتطلبات الأساسية التالية:

1. بيئة تطوير .NET: بيئة تطوير .NET فعالة، مثل Visual Studio.

2. GroupDocs.Signature لمكتبة .NET: قم بتنزيل وتثبيت مكتبة GroupDocs.Signature لمكتبة .NET من [هنا](https://releases.groupdocs.com/signature/net/).

3. عينات المستندات: قم بإعداد مستندات الاختبار مع توقيعات الصور للتحقق منها واختبارها.

4. المعرفة الأساسية بلغة C#: فهم أساسيات برمجة C#.

## استيراد مساحات الأسماء

ابدأ باستيراد المساحات الأساسية اللازمة للوصول إلى وظيفة GroupDocs.Signature:

```csharp
using System;
using System.IO;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

الآن، دعنا نقسم عملية البحث عن توقيعات الصور إلى خطوات واضحة وسهلة المتابعة:

## الخطوة 1: تحديد مسار المستند ومعلومات الملف

أولاً، حدد المسار إلى المستند الذي يحتوي على توقيعات الصور واستخرج اسم الملف الخاص به للرجوع إليه:

```csharp
string filePath = "sample_multiple_signatures.docx";
string fileName = Path.GetFileName(filePath);
```

## الخطوة 2: تهيئة كائن التوقيع

إنشاء مثيل لـ `Signature` الفئة عن طريق تمرير مسار الملف إلى المنشئ:

```csharp
using (Signature signature = new Signature(filePath))
{
    // سيتم إضافة كود البحث عن توقيع الصورة هنا
}
```

## الخطوة 3: البحث عن توقيعات الصور

استخدم `Search` الطريقة مع نوع التوقيع المناسب للعثور على توقيعات الصور في المستند:

```csharp
// البحث عن توقيعات الصور داخل المستند
List<ImageSignature> signatures = signature.Search<ImageSignature>(SignatureType.Image);
```

## الخطوة 4: معالجة النتائج وعرضها

قم بالتكرار خلال توقيعات الصور التي تم العثور عليها والوصول إلى خصائصها:

```csharp
// عرض معلومات حول توقيعات الصور التي تم العثور عليها
Console.WriteLine($"\nSource document '{fileName}' contains {signatures.Count} image signature(s).");

foreach (ImageSignature imageSignature in signatures)
{
    Console.WriteLine($"Found image signature at page {imageSignature.PageNumber} with size {imageSignature.Size}.");
    Console.WriteLine($"Location: X={imageSignature.Left}, Y={imageSignature.Top}");
    Console.WriteLine($"Dimensions: Width={imageSignature.Width}, Height={imageSignature.Height}");
}
```

## مثال كامل

فيما يلي مثال شامل وعملي يوضح كيفية البحث عن توقيعات الصور في مستند:

```csharp
using System;
using System.IO;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;

namespace ImageSignatureSearch
{
    class Program
    {
        static void Main(string[] args)
        {
            // مسار المستند
            string filePath = "sample_multiple_signatures.docx";
            string fileName = Path.GetFileName(filePath);
            
            // تهيئة مثيل التوقيع
            using (Signature signature = new Signature(filePath))
            {
                try
                {
                    // البحث عن توقيعات الصور في المستند
                    List<ImageSignature> signatures = signature.Search<ImageSignature>(SignatureType.Image);
                    
                    // عرض نتائج البحث
                    Console.WriteLine($"\nSource document '{fileName}' contains {signatures.Count} image signature(s).");
                    
                    foreach (ImageSignature imageSignature in signatures)
                    {
                        Console.WriteLine($"Found image signature at page {imageSignature.PageNumber} with size {imageSignature.Size}.");
                        Console.WriteLine($"Location: X={imageSignature.Left}, Y={imageSignature.Top}");
                        Console.WriteLine($"Dimensions: Width={imageSignature.Width}, Height={imageSignature.Height}");
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

## تقنيات البحث المتقدمة عن توقيع الصورة

### استخدام خيارات البحث المخصصة

لإجراء عمليات بحث أكثر استهدافًا، يمكنك استخدام `ImageSearchOptions` لتخصيص معايير البحث الخاصة بك:

```csharp
// إنشاء خيارات البحث عن الصور
ImageSearchOptions options = new ImageSearchOptions
{
    // البحث في صفحات محددة
    AllPages = false,
    PageNumber = 1,
    PagesSetup = new PagesSetup { Pages = new List<int> { 1, 3, 5 } },
    
    // البحث فقط في مناطق محددة من الصفحة
    Rectangle = new Rectangle(100, 100, 400, 200),
    
    // تعيين الحد الأدنى والحد الأقصى لأبعاد الصورة لتصفية النتائج
    MinWidth = 50,
    MinHeight = 50,
    MaxWidth = 300,
    MaxHeight = 300
};

// البحث باستخدام خيارات مخصصة
List<ImageSignature> filteredSignatures = signature.Search<ImageSignature>(options);
```

### معالجة بيانات توقيع الصورة

يمكنك معالجة توقيعات الصور التي تم العثور عليها بشكل أكبر، مثل حفظها كملفات منفصلة أو تحليل محتواها:

```csharp
foreach (ImageSignature imageSignature in signatures)
{
    // الوصول إلى بيانات الصورة
    byte[] imageData = imageSignature.ImageData;
    
    // حفظ الصورة في ملف
    string outputPath = $"extracted_image_{imageSignature.PageNumber}_{Guid.NewGuid()}.png";
    File.WriteAllBytes(outputPath, imageData);
    
    Console.WriteLine($"Saved image signature to {outputPath}");
    
    // يمكنك أيضًا تحليل الصورة باستخدام مكتبات الطرف الثالث
    // تحليل الصورة(بيانات الصورة)؛
}
```

### مقارنة توقيعات الصور

يمكنك تنفيذ منطق المقارنة لمطابقة توقيعات الصور مع القوالب المعروفة:

```csharp
// تحميل صورة مرجعية للمقارنة
byte[] referenceImage = File.ReadAllBytes("reference_signature.png");

foreach (ImageSignature foundSignature in signatures)
{
    // قارن التوقيع الموجود مع الصورة المرجعية
    // هذا مثال مبسط - التنفيذ الحقيقي سيستخدم خوارزميات معالجة الصور
    bool isMatch = CompareImages(foundSignature.ImageData, referenceImage);
    
    if (isMatch)
    {
        Console.WriteLine($"Found matching signature at page {foundSignature.PageNumber}!");
    }
}

// دالة المقارنة البسيطة (لأغراض التوضيح)
static bool CompareImages(byte[] image1, byte[] image2)
{
    // في تطبيق حقيقي، سوف تقوم بتنفيذ مقارنة الصور المناسبة
    // باستخدام تقنيات مثل مطابقة الميزات ومقارنة الهيستوجرام وما إلى ذلك.
    
    // عنصر نائب لمنطق مقارنة الصور الفعلية
    return image1.Length == image2.Length;
}
```

## خاتمة

في هذا البرنامج التعليمي، استكشفنا كيفية البحث بفعالية عن توقيعات الصور داخل المستندات باستخدام GroupDocs.Signature لـ .NET. بدءًا من عمليات البحث الأساسية ووصولًا إلى التقنيات المتقدمة، بما في ذلك معايير البحث المخصصة والمعالجة الإضافية للتوقيعات التي تم العثور عليها، أصبحت لديك الآن المعرفة اللازمة لتطبيق وظيفة شاملة لتوقيعات الصور في تطبيقات .NET الخاصة بك.

يوفر GroupDocs.Signature واجهة برمجة تطبيقات قوية ومرنة للعمل مع أنواع مختلفة من التوقيعات، مما يجعله خيارًا ممتازًا لتطبيقات معالجة المستندات التي تتطلب تحليل التوقيع أو التحقق منه أو قدرات الاستخراج.

## الأسئلة الشائعة

### هل يمكن لـ GroupDocs.Signature اكتشاف جميع تنسيقات الصور باعتبارها توقيعات؟

يمكن لـ GroupDocs.Signature اكتشاف تنسيقات الصور المختلفة بما في ذلك PNG وJPEG وBMP وGIF كتوقيعات داخل المستندات، بشرط إضافتها بشكل صحيح كعناصر توقيع بدلاً من صور المحتوى العادية.

### هل من الممكن البحث عن توقيعات الصور في مناطق محددة من المستند؟

نعم، باستخدام `Rectangle` الممتلكات في `ImageSearchOptions`يمكنك تقييد البحث على مناطق محددة من صفحة المستند، وهو أمر مفيد للمستندات التي تحتوي على مناطق توقيع محددة مسبقًا.

### هل يمكنني البحث عن توقيعات الصور في المستندات المحمية بكلمة مرور؟

نعم، يدعم GroupDocs.Signature البحث في المستندات المحمية بكلمة مرور من خلال توفير كلمة المرور في `LoadOptions` عند تهيئة `Signature` هدف:

```csharp
LoadOptions loadOptions = new LoadOptions { Password = "your_password" };
using (Signature signature = new Signature(filePath, loadOptions))
{
    // البحث عن توقيعات الصور
}
```

### كيف يمكنني تحديد ما إذا كانت الصورة الموجودة في المستند عبارة عن توقيع أم مجرد صورة عادية؟

يُركز GroupDocs.Signature على العثور على الصور المُضافة كعناصر توقيع. للتمييز بين الصور العادية وصور التوقيع، يُمكنك استخدام خصائص مثل موضع الصورة (عادةً ما تظهر التوقيعات في مناطق مُحددة) أو تطبيق عملية تحقق مُخصصة بناءً على منطق عملك.

### هل يمكنني تصفية توقيعات الصور بناءً على حجمها أو أبعادها؟

نعم، `ImageSearchOptions` يوفر خصائص مثل `MinWidth`، `MinHeight`، `MaxWidth`، و `MaxHeight` التي تسمح لك بتصفية التوقيعات استنادًا إلى أبعادها، مما يجعل من الأسهل التمييز بين أنواع مختلفة من عناصر الصورة.

## انظر أيضا

* [مرجع واجهة برمجة التطبيقات](https://reference.groupdocs.com/signature/net/)
* [أمثلة التعليمات البرمجية](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
* [وثائق المنتج](https://docs.groupdocs.com/signature/net/)
* [صفحة المنتج](https://products.groupdocs.com/signature/net/)
* [تنزيل أحدث إصدار](https://releases.groupdocs.com/signature/net/)
* [مقالات المدونة](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
* [منتدى الدعم المجاني](https://forum.groupdocs.com/c/signature/13)
* [رخصة مؤقتة](https://purchase.groupdocs.com/temporary-license/)