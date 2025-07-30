---
"description": "تعرّف على كيفية توقيع البيانات الوصفية وتضمينها في الصور باستخدام GroupDocs.Signature لـ .NET. أضف معلومات المؤلف، والطوابع الزمنية، والبيانات المخصصة لتحسين مصداقية الصور وإمكانية تتبعها."
"linktitle": "توقيع الصورة مع البيانات الوصفية"
"second_title": "واجهة برمجة تطبيقات GroupDocs.Signature .NET"
"title": "توقيع الصور باستخدام البيانات الوصفية في C# .NET"
"url": "/ar/net/document-signing/sign-image-with-metadata/"
"weight": 10
---

## مقدمة

يتزايد أهمية توقيع الصور الرقمية باستخدام البيانات الوصفية لإثبات مصداقيتها وملكيتها وإمكانية تتبعها. يوفر GroupDocs.Signature لـ .NET حلاً فعالاً وسهل الاستخدام لإضافة توقيعات البيانات الوصفية إلى مختلف تنسيقات الصور. يرشدك هذا البرنامج التعليمي خلال العملية الكاملة لتوقيع الصور باستخدام البيانات الوصفية باستخدام لغة C#.

تتيح لك توقيعات البيانات الوصفية تضمين معلومات قيّمة مباشرةً في ملفات الصور، مثل معلومات المؤلف، وتواريخ الإنشاء، والمعرفات الفريدة، وغيرها. تُدمج هذه المعلومات في ملف الصورة نفسه، مما يوفر طريقة موثوقة لتتبع صحة الصورة والتحقق منها.

## المتطلبات الأساسية

قبل المتابعة بهذا البرنامج التعليمي، تأكد من أن لديك ما يلي:

1. [GroupDocs.Signature لـ .NET](https://releases.groupdocs.com/signature/net/) - تنزيل المكتبة وتثبيتها
2. بيئة التطوير - Visual Studio أو أي بيئة تطوير متكاملة متوافقة مع دعم .NET
3. ملف الصورة - ملف صورة نموذجي بتنسيق مدعوم (PNG، JPG، TIFF، وما إلى ذلك)
4. المعرفة الأساسية ببرمجة C# - الإلمام بمفاهيم برمجة C#

## استيراد مساحات الأسماء

ابدأ باستيراد المساحات الأساسية اللازمة للوصول إلى وظيفة GroupDocs.Signature:

```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

## الخطوة 1: إعداد مسارات الملفات

قم بتحديد المسارات لصورة المصدر والمكان الذي يجب حفظ الإخراج الموقع فيه:

```csharp
// حدد المسار إلى ملف الصورة المصدر الخاص بك
string filePath = "sample.png";

// قم بتحديد دليل الإخراج واسم الملف للصورة الموقعة
string outputDirectory = "Your Document Directory";
string outputFilePath = Path.Combine(outputDirectory, "SignImageWithMetadata", "SignedWithMetadata.png");

// تأكد من وجود دليل الإخراج
Directory.CreateDirectory(Path.GetDirectoryName(outputFilePath));
```

## الخطوة 2: تهيئة كائن التوقيع

قم بإنشاء مثيل لفئة التوقيع باستخدام ملف الصورة المصدر الخاص بك:

```csharp
using (Signature signature = new Signature(filePath))
{
    // سيتم وضع باقي الكود هنا
}
```

## الخطوة 3: إنشاء وتكوين توقيعات البيانات الوصفية

بعد ذلك، حدد البيانات الوصفية التي تريد تضمينها في الصورة. يدعم GroupDocs.Signature أنواعًا مختلفة من البيانات الوصفية:

```csharp
// تهيئة معرف البيانات الوصفية (خاص بتنسيق الصورة)
ushort imgsMetadataId = 41996;

// إنشاء كائن خيارات البيانات الوصفية
MetadataSignOptions options = new MetadataSignOptions();

// إضافة أنواع مختلفة من توقيعات البيانات الوصفية
options
    .Add(new ImageMetadataSignature(imgsMetadataId++, "Mr.Sherlock Holmes"))  // قيمة السلسلة
    .Add(new ImageMetadataSignature(imgsMetadataId++, DateTime.Now))          // التاريخ والوقت والقيمة
    .Add(new ImageMetadataSignature(imgsMetadataId++, 123456))                // قيمة صحيحة
    .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456D))              // قيمة مزدوجة
    .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456M))              // القيمة العشرية
    .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456F));             // قيمة التعويم
```

## الخطوة 4: توقيع الصورة باستخدام البيانات الوصفية

قم بتطبيق توقيعات البيانات الوصفية على الصورة واحفظ النتيجة:

```csharp
// توقيع المستند وحفظه في مسار ملف الإخراج
SignResult result = signature.Sign(outputFilePath, options);

// عرض رسالة النجاح
Console.WriteLine($"\nSource image signed successfully with {result.Succeeded.Count} metadata signature(s).");
Console.WriteLine($"Signed image saved at: {outputFilePath}");
```

## مثال كامل

فيما يلي مثال الكود الكامل الذي يجمع كل الخطوات معًا:

```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;

namespace SignImageWithMetadataExample
{
    class Program
    {
        static void Main(string[] args)
        {
            // تحديد مسارات الملفات
            string filePath = "sample.png";            
            string outputFilePath = Path.Combine("Your Document Directory", "SignImageWithMetadata", "SignedWithMetadata.png");
            
            // تأكد من وجود دليل الإخراج
            Directory.CreateDirectory(Path.GetDirectoryName(outputFilePath));

            // توقيع الصورة باستخدام البيانات الوصفية
            using (Signature signature = new Signature(filePath))
            {
                // تهيئة معرف البيانات الوصفية (خاص بتنسيق الصورة)
                ushort imgsMetadataId = 41996;
                
                // خيارات إنشاء البيانات الوصفية
                MetadataSignOptions options = new MetadataSignOptions();
                
                // إضافة أنواع مختلفة من توقيعات البيانات الوصفية
                options
                    .Add(new ImageMetadataSignature(imgsMetadataId++, "Mr.Sherlock Holmes")) // قيمة السلسلة
                    .Add(new ImageMetadataSignature(imgsMetadataId++, DateTime.Now))          // التاريخ والوقت والقيمة
                    .Add(new ImageMetadataSignature(imgsMetadataId++, 123456))                // قيمة صحيحة
                    .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456D))              // قيمة مزدوجة
                    .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456M))              // القيمة العشرية
                    .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456F));             // قيمة التعويم
                
                // توقيع المستند وحفظه في الملف
                SignResult result = signature.Sign(outputFilePath, options);
                
                // عرض النتائج
                Console.WriteLine($"\nSource image signed successfully with {result.Succeeded.Count} signature(s).");
                Console.WriteLine($"File saved at {outputFilePath}.");
            }
        }
    }
}
```

## تقنيات توقيع البيانات الوصفية المتقدمة

### العمل مع البيانات الوصفية المخصصة

يمكنك أيضًا إنشاء حقول بيانات تعريفية مخصصة باستخدام معرفات محددة:

```csharp
// إنشاء بيانات تعريفية مخصصة باستخدام معرف محدد
options.Add(new ImageMetadataSignature(42000, "CustomValue"));
```

### التحقق من توقيعات البيانات الوصفية

بعد التوقيع، قد ترغب في التحقق من توقيعات البيانات الوصفية:

```csharp
// إنشاء خيارات التحقق
MetadataSearchOptions searchOptions = new MetadataSearchOptions();

// البحث عن توقيعات البيانات الوصفية
SearchResult result = signature.Search(searchOptions);

// عرض التوقيعات التي تم العثور عليها
Console.WriteLine($"Found {result.Signatures.Count} metadata signatures:");
foreach(var metadataSignature in result.Signatures)
{
    Console.WriteLine($"- {metadataSignature.Name}: {metadataSignature.Value}");
}
```

## خاتمة

في هذا البرنامج التعليمي، تعلمتَ كيفية توقيع الصور باستخدام البيانات الوصفية باستخدام GroupDocs.Signature لـ .NET. يُعدّ تضمين البيانات الوصفية في الصور طريقةً ممتازةً لتعزيز مصداقية الصور، وإضافة معلومات مهمة، وتحسين سير عمل إدارة المستندات. العملية بسيطة وفعّالة، وتتيح لك تخصيصها وفقًا لاحتياجاتك الخاصة.

يمكن استخدام البيانات الوصفية المُضمَّنة في ملف الصورة لأغراض مُختلفة، مثل حماية حقوق النشر، وتتبُّع أصل الصورة، وإضافة معلومات وصفية، وإنشاء سلسلة رقمية للحفظ. بتطبيق توقيعات البيانات الوصفية، يُمكنك ضمان الحفاظ على سلامة صورك وأصالتها طوال دورة حياتها.

## الأسئلة الشائعة

### هل يمكنني إضافة بيانات وصفية للصور الموقعة الموجودة؟

نعم، يمكنك إضافة بيانات وصفية إضافية إلى الصور التي تحتوي بالفعل على توقيعات وصفية. سيتم حفظ البيانات الوصفية الحالية، وستتم إضافة بيانات وصفية جديدة وفقًا لذلك.

### ما هي تنسيقات الصور المدعومة لتوقيع البيانات الوصفية؟

يدعم GroupDocs.Signature لـ .NET توقيع البيانات الوصفية لمختلف صيغ الصور، بما في ذلك PNG وJPEG وTIFF وBMP وGIF وغيرها. للاطلاع على القائمة الكاملة، يُرجى مراجعة [الوثائق الرسمية](https://docs.groupdocs.com/signature/net/).

### هل من الممكن تشفير البيانات الوصفية الموجودة في الصور؟

نعم، يوفر GroupDocs.Signature خيارات لتشفير البيانات الوصفية لتعزيز الأمان. يمكنك استخدام خيارات التشفير التي توفرها المكتبة لحماية معلومات البيانات الوصفية الحساسة.

### هل يمكنني التحقق برمجيًا من صحة الصور الموقعة؟

بالتأكيد. يمكنك استخدام طرق التحقق في GroupDocs.Signature للتحقق من صحة توقيعات البيانات الوصفية والتأكد من صحة الصور الموقعة.

### هل هناك حد لحجم الملف عند توقيع الصور باستخدام البيانات الوصفية؟

لا يوجد حدّ أقصى لحجم الملف تفرضه المكتبة نفسها، ولكن الملفات الكبيرة جدًا قد تتطلب وقتًا أطول للمعالجة وذاكرة أكبر. يُنصح بمراعاة موارد النظام عند العمل مع صور كبيرة جدًا.

### كيف يمكنني الحصول على ترخيص مؤقت لأغراض الاختبار؟

يمكنك الحصول على [رخصة مؤقتة](https://purchase.groupdocs.com/temporary-license/) لاختبار GroupDocs.Signature قبل إجراء عملية شراء.

### أين يمكنني العثور على المزيد من الموارد والدعم؟

- [مرجع واجهة برمجة التطبيقات](https://reference.groupdocs.com/signature/net/)
- [التنزيلات](https://releases.groupdocs.com/signature/net/)
- [أمثلة](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
- [التوثيق](https://docs.groupdocs.com/signature/net/)
- [صفحة المنتج](https://products.groupdocs.com/signature/net/)
- [مدونة](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
- [منتدى الدعم](https://forum.groupdocs.com/c/signature/13)