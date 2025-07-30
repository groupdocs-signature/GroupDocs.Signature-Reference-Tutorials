---
"description": "أضف توقيعات البيانات الوصفية إلى مستندات Word باستخدام GroupDocs.Signature لـ .NET. أدرج تفاصيل المؤلف، والطوابع الزمنية، والخصائص المخصصة لتعزيز أمان المستندات وإمكانية تتبعها."
"linktitle": "معالجة النصوص باستخدام البيانات الوصفية"
"second_title": "واجهة برمجة تطبيقات GroupDocs.Signature .NET"
"title": "تعزيز مستندات Word باستخدام توقيعات البيانات الوصفية في C# .NET"
"url": "/ar/net/document-signing/sign-word-processing-with-metadata/"
"weight": 14
---

## مقدمة

تُعد مستندات معالجة النصوص من أكثر أنواع الملفات شيوعًا في الأعمال والتعليم والتواصل الشخصي. يُعد ضمان صحة هذه المستندات، وتتبع مصدرها، والحفاظ على سلامتها أمرًا بالغ الأهمية في العديد من البيئات المهنية. ومن الطرق الفعالة لتعزيز أمان المستندات وإمكانية تتبعها تضمين توقيعات البيانات الوصفية.

سيرشدك هذا البرنامج التعليمي الشامل خلال عملية توقيع مستندات معالجة النصوص باستخدام البيانات الوصفية باستخدام GroupDocs.Signature لـ .NET. بإضافة توقيعات البيانات الوصفية، يمكنك تضمين معلومات قيّمة، مثل تفاصيل المؤلف، وتواريخ الإنشاء، ومعرفات المستندات، وخصائص مخصصة أخرى، مباشرةً في بنية ملف المستند.

## المتطلبات الأساسية

قبل المتابعة بهذا البرنامج التعليمي، تأكد من أن لديك ما يلي:

1. [GroupDocs.Signature لـ .NET](https://releases.groupdocs.com/signature/net/) - تنزيل المكتبة وتثبيتها
2. بيئة التطوير - Visual Studio أو أي بيئة تطوير متكاملة أخرى متوافقة مع .NET
3. مستند Word - ملف مستند نموذجي (DOCX، DOC، وما إلى ذلك)
4. المعرفة الأساسية بلغة C# - الإلمام بلغة البرمجة C#

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

قم بتحديد المسارات لمستند Word المصدر والمكان الذي يجب حفظ الإخراج الموقع فيه:

```csharp
// حدد المسار إلى مستند Word الخاص بك
string filePath = "sample.docx";

// تحديد دليل الإخراج واسم الملف للمستند الموقع
string outputDirectory = "Your Document Directory";
string outputFilePath = Path.Combine(outputDirectory, "SignWordProcessingWithMetadata", "SignedWithMetadata.docx");

// تأكد من وجود دليل الإخراج
Directory.CreateDirectory(Path.GetDirectoryName(outputFilePath));
```

## الخطوة 2: تهيئة كائن التوقيع

قم بإنشاء مثيل لفئة التوقيع باستخدام مستند Word المصدر الخاص بك:

```csharp
using (Signature signature = new Signature(filePath))
{
    // سيتم وضع باقي الكود هنا
}
```

## الخطوة 3: إنشاء وتكوين توقيعات البيانات الوصفية

بعد ذلك، قم بتحديد خيارات البيانات الوصفية وأضف أنواعًا مختلفة من توقيعات البيانات الوصفية:

```csharp
// إنشاء كائن خيارات البيانات الوصفية
MetadataSignOptions options = new MetadataSignOptions();

// أضف أنواعًا مختلفة من البيانات الوصفية باستخدام الواجهة السلسة
options
    .Add(new WordProcessingMetadataSignature("Author", "Mr.Sherlock Holmes")) // قيمة السلسلة
    .Add(new WordProcessingMetadataSignature("CreatedOn", DateTime.Now))      // قيمة التاريخ والوقت
    .Add(new WordProcessingMetadataSignature("DocumentId", 123456))           // قيمة صحيحة
    .Add(new WordProcessingMetadataSignature("SignatureId", 123.456D))        // قيمة مزدوجة
    .Add(new WordProcessingMetadataSignature("Amount", 123.456M))             // القيمة العشرية
    .Add(new WordProcessingMetadataSignature("Total", 123.456F));             // قيمة التعويم
```

## الخطوة 4: توقيع المستند باستخدام البيانات الوصفية

قم بتطبيق توقيعات البيانات الوصفية على مستند Word واحفظ النتيجة:

```csharp
// توقيع المستند وحفظه في مسار ملف الإخراج
SignResult result = signature.Sign(outputFilePath, options);

// عرض رسالة النجاح
Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} metadata signature(s).");
Console.WriteLine($"Signed document saved at: {outputFilePath}");
```

## مثال كامل

فيما يلي مثال الكود الكامل الذي يجمع كل الخطوات معًا:

```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;

namespace SignWordProcessingWithMetadataExample
{
    class Program
    {
        static void Main(string[] args)
        {
            // تحديد مسارات الملفات
            string filePath = "sample.docx";
            string outputFilePath = Path.Combine("Your Document Directory", "SignWordProcessingWithMetadata", "SignedWithMetadata.docx");
            
            // تأكد من وجود دليل الإخراج
            Directory.CreateDirectory(Path.GetDirectoryName(outputFilePath));

            // توقيع مستند Word باستخدام البيانات الوصفية
            using (Signature signature = new Signature(filePath))
            {
                // إنشاء كائن خيارات البيانات الوصفية
                MetadataSignOptions options = new MetadataSignOptions();
                
                // إضافة أنواع مختلفة من توقيعات البيانات الوصفية
                options
                    .Add(new WordProcessingMetadataSignature("Author", "Mr.Sherlock Holmes")) // قيمة السلسلة
                    .Add(new WordProcessingMetadataSignature("CreatedOn", DateTime.Now))      // قيمة التاريخ والوقت
                    .Add(new WordProcessingMetadataSignature("DocumentId", 123456))           // قيمة صحيحة
                    .Add(new WordProcessingMetadataSignature("SignatureId", 123.456D))        // قيمة مزدوجة
                    .Add(new WordProcessingMetadataSignature("Amount", 123.456M))             // القيمة العشرية
                    .Add(new WordProcessingMetadataSignature("Total", 123.456F));             // قيمة التعويم
                
                // توقيع المستند وحفظه في الملف
                SignResult result = signature.Sign(outputFilePath, options);
                
                // عرض النتائج
                Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).");
                Console.WriteLine($"File saved at {outputFilePath}.");
            }
        }
    }
}
```

## تقنيات متقدمة لبيانات مستندات Word

### العمل مع خصائص المستندات المخصصة والمضمنة

تحتوي مستندات Word على خصائص مدمجة ومخصصة، ويمكن الوصول إليها من خلال لوحة خصائص المستند. يتيح لك GroupDocs.Signature العمل مع كليهما:

```csharp
// إضافة خصائص مدمجة
options
    .Add(new WordProcessingMetadataSignature("Company", "Sherlock Holmes Consulting"))
    .Add(new WordProcessingMetadataSignature("Category", "Legal Document"))
    .Add(new WordProcessingMetadataSignature("Keywords", "contract,agreement,legal"))
    .Add(new WordProcessingMetadataSignature("Comments", "This document is confidential"))
    .Add(new WordProcessingMetadataSignature("Manager", "John Watson"));

// إضافة خصائص مخصصة
options.Add(new WordProcessingMetadataSignature("Department", "Legal"));
options.Add(new WordProcessingMetadataSignature("SecurityLevel", "Confidential"));
```

### البحث عن البيانات الوصفية في مستندات Word الموقعة

بعد التوقيع، قد ترغب في التحقق من البيانات الوصفية أو استخراجها:

```csharp
// إنشاء خيارات البحث للبيانات الوصفية
MetadataSearchOptions searchOptions = new MetadataSearchOptions();

// البحث عن توقيعات البيانات الوصفية
SearchResult searchResult = signature.Search(searchOptions);

// عرض التوقيعات التي تم العثور عليها
Console.WriteLine($"Found {searchResult.Signatures.Count} metadata signatures:");
foreach (var foundSignature in searchResult.Signatures)
{
    MetadataSignature metadataSignature = foundSignature as MetadataSignature;
    if (metadataSignature != null)
    {
        Console.WriteLine($"- {metadataSignature.Name}: {metadataSignature.Value} ({metadataSignature.Value.GetType().Name})");
    }
}
```

### العمل مع متغيرات المستند

تدعم مستندات Word أيضًا متغيرات المستند، وهي شكل آخر من أشكال البيانات الوصفية:

```csharp
// إضافة متغيرات المستند
options.Add(new WordProcessingMetadataSignature("DocVariable1", "Custom Value 1", true));
options.Add(new WordProcessingMetadataSignature("DocVariable2", DateTime.Now, true));
```

## خاتمة

في هذا البرنامج التعليمي الشامل، تعلمت كيفية توقيع مستندات Word باستخدام البيانات الوصفية باستخدام GroupDocs.Signature لـ .NET. يُحسّن تضمين البيانات الوصفية في مستندات Word إمكانية تتبع المستندات، ويوفر سياقًا قيّمًا، ويساعد في ضمان مصداقيتها.

تُعد توقيعات البيانات الوصفية في مستندات Word مفيدة بشكل خاص في بيئات الأعمال والقانون حيث يكون أصل المستند ومؤلفه وتتبع الإصدارات أمرًا بالغ الأهمية. يمكن أن تتضمن البيانات الوصفية المضمنة معلومات حول المؤلف ووقت الإنشاء ومعرفات المستند والخصائص المخصصة المناسبة لاحتياجات مؤسستك.

من خلال تنفيذ توقيعات البيانات الوصفية مع GroupDocs.Signature، يمكنك التأكد من أن مستندات Word الخاصة بك تحافظ على سلامتها وتوفر معلومات يمكن التحقق منها طوال دورة حياتها.

## الأسئلة الشائعة

### هل يمكنني إضافة بيانات وصفية إلى مستندات Word التي تحتوي بالفعل على بعض الخصائص المحددة؟

نعم، يمكنك إضافة بيانات تعريفية جديدة أو تحديث بيانات تعريفية موجودة في مستندات Word. سيتولى GroupDocs.Signature عملية التكامل، إما بإضافة خصائص جديدة أو تحديث خصائص موجودة بنفس الأسماء.

### ما هي تنسيقات معالجة الكلمات المدعومة لتوقيع البيانات الوصفية؟

يدعم GroupDocs.Signature لـ .NET توقيع البيانات الوصفية لمختلف صيغ معالجة النصوص، بما في ذلك DOCX وDOC وRTF وODT وغيرها. للاطلاع على القائمة الكاملة، يُرجى مراجعة [التوثيق](https://docs.groupdocs.com/signature/net/).

### هل تكون توقيعات البيانات الوصفية في مستندات Word مرئية للقراء؟

لا تظهر توقيعات البيانات الوصفية في محتوى المستند نفسه. مع ذلك، يُمكن عرضها من خلال لوحة خصائص المستند في Microsoft Word أو أي تطبيقات أخرى متوافقة.

### هل يمكنني التحقق برمجيًا من أن مستند Word قد تم العبث به بعد إضافة البيانات الوصفية؟

نعم، يوفر GroupDocs.Signature إمكانيات التحقق التي يمكن أن تساعد في اكتشاف ما إذا كان قد تم تعديل المستند بعد التوقيع، بما في ذلك التغييرات في البيانات الوصفية.

### هل من الممكن إزالة البيانات الوصفية من مستند Word؟

نعم، يوفر GroupDocs.Signature خيارات لإزالة توقيعات البيانات الوصفية من المستندات عند الحاجة. قد يكون هذا مفيدًا لتنظيف المعلومات الحساسة قبل مشاركة المستندات خارجيًا.

### أين يمكنني العثور على المزيد من الموارد والدعم؟

- [مرجع واجهة برمجة التطبيقات](https://reference.groupdocs.com/signature/net/)
- [التنزيلات](https://releases.groupdocs.com/signature/net/)
- [أمثلة](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
- [التوثيق](https://docs.groupdocs.com/signature/net/)
- [صفحة المنتج](https://products.groupdocs.com/signature/net/)
- [مدونة](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
- [منتدى الدعم](https://forum.groupdocs.com/c/signature/13)
- [رخصة مؤقتة](https://purchase.groupdocs.com/temporary-license/)