---
"description": "احمِ جداول بيانات Excel وحسّنها بتضمين توقيعات البيانات الوصفية باستخدام GroupDocs.Signature لـ .NET. أضف معلومات المؤلف، والطوابع الزمنية، والبيانات المخصصة لتحسين إمكانية تتبع المستندات ومصداقيتها."
"linktitle": "توقيع جدول بيانات مع البيانات الوصفية"
"second_title": "واجهة برمجة تطبيقات GroupDocs.Signature .NET"
"title": "إضافة توقيعات البيانات الوصفية إلى جداول بيانات Excel في C# .NET"
"url": "/ar/net/document-signing/sign-spreadsheet-with-metadata/"
"weight": 13
---

## مقدمة

غالبًا ما تحتوي جداول بيانات Excel على بيانات أعمال مهمة، ومعلومات مالية، وحسابات مهمة. يُعدّ ضمان صحتها، وتتبع مصدرها، وحماية سلامتها أمرًا بالغ الأهمية في العديد من البيئات المهنية. ومن الطرق الفعّالة لتعزيز أمان جداول البيانات وإمكانية تتبعها تضمين توقيعات البيانات الوصفية.

سيرشدك هذا البرنامج التعليمي الشامل خلال عملية توقيع جداول بيانات Excel بالبيانات الوصفية باستخدام GroupDocs.Signature لـ .NET. بإضافة توقيعات البيانات الوصفية، يمكنك تضمين معلومات قيّمة، مثل تفاصيل المؤلف، وتواريخ الإنشاء، ومعرفات المستندات، وخصائص مخصصة أخرى، مباشرةً في بنية ملف جدول البيانات.

## المتطلبات الأساسية

قبل المتابعة بهذا البرنامج التعليمي، تأكد من أن لديك ما يلي:

1. [GroupDocs.Signature لـ .NET](https://releases.groupdocs.com/signature/net/) - تنزيل المكتبة وتثبيتها
2. بيئة التطوير - Visual Studio أو أي بيئة تطوير متكاملة أخرى متوافقة مع .NET
3. جدول بيانات Excel - ملف جدول بيانات نموذجي (XLSX، XLS، وما إلى ذلك)
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

قم بتحديد المسارات الخاصة بجدول البيانات المصدر والمكان الذي يجب حفظ الإخراج الموقع فيه:

```csharp
// حدد المسار إلى ملف Excel الخاص بك
string filePath = "sample.xlsx";

// قم بتحديد دليل الإخراج واسم الملف للجدول الموقع
string outputDirectory = "Your Document Directory";
string outputFilePath = Path.Combine(outputDirectory, "SignSpreadsheetWithMetadata", "SignedWithMetadata.xlsx");

// تأكد من وجود دليل الإخراج
Directory.CreateDirectory(Path.GetDirectoryName(outputFilePath));
```

## الخطوة 2: تهيئة كائن التوقيع

قم بإنشاء مثيل لفئة التوقيع باستخدام ملف جدول البيانات المصدر الخاص بك:

```csharp
using (Signature signature = new Signature(filePath))
{
    // سيتم وضع باقي الكود هنا
}
```

## الخطوة 3: إنشاء وتكوين توقيعات البيانات الوصفية

بعد ذلك، قم بتحديد خيارات البيانات الوصفية وإنشاء مجموعة من توقيعات البيانات الوصفية في جدول البيانات:

```csharp
// إنشاء كائن خيارات البيانات الوصفية
MetadataSignOptions options = new MetadataSignOptions();

// إنشاء مجموعة من توقيعات بيانات جدول البيانات باستخدام أنواع بيانات مختلفة
SpreadsheetMetadataSignature[] signatures = new SpreadsheetMetadataSignature[]
{
    new SpreadsheetMetadataSignature("Author", "Mr.Sherlock Holmes"), // قيمة السلسلة
    new SpreadsheetMetadataSignature("CreatedOn", DateTime.Now),      // قيمة التاريخ والوقت
    new SpreadsheetMetadataSignature("DocumentId", 123456),           // قيمة صحيحة
    new SpreadsheetMetadataSignature("SignatureId", 123.456D),        // قيمة مزدوجة
    new SpreadsheetMetadataSignature("Amount", 123.456M),             // القيمة العشرية
    new SpreadsheetMetadataSignature("Total", 123.456F)               // قيمة التعويم
};

// إضافة مجموعة التوقيعات إلى الخيارات
options.Signatures.AddRange(signatures);
```

## الخطوة 4: توقيع جدول البيانات باستخدام البيانات الوصفية

قم بتطبيق توقيعات البيانات الوصفية على جدول البيانات واحفظ النتيجة:

```csharp
// توقيع المستند وحفظه في مسار ملف الإخراج
SignResult result = signature.Sign(outputFilePath, options);

// عرض رسالة النجاح
Console.WriteLine($"\nSource spreadsheet signed successfully with {result.Succeeded.Count} metadata signature(s).");
Console.WriteLine($"Signed spreadsheet saved at: {outputFilePath}");
```

## مثال كامل

فيما يلي مثال الكود الكامل الذي يجمع كل الخطوات معًا:

```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;

namespace SignSpreadsheetWithMetadataExample
{
    class Program
    {
        static void Main(string[] args)
        {
            // تحديد مسارات الملفات
            string filePath = "sample.xlsx";
            string outputFilePath = Path.Combine("Your Document Directory", "SignSpreadsheetWithMetadata", "SignedWithMetadata.xlsx");
            
            // تأكد من وجود دليل الإخراج
            Directory.CreateDirectory(Path.GetDirectoryName(outputFilePath));

            // توقيع جدول البيانات باستخدام البيانات الوصفية
            using (Signature signature = new Signature(filePath))
            {
                // إنشاء كائن خيارات البيانات الوصفية
                MetadataSignOptions options = new MetadataSignOptions();
                
                // إنشاء مجموعة من توقيعات بيانات جدول البيانات باستخدام أنواع بيانات مختلفة
                SpreadsheetMetadataSignature[] signatures = new SpreadsheetMetadataSignature[]
                {
                    new SpreadsheetMetadataSignature("Author", "Mr.Sherlock Holmes"), // قيمة السلسلة
                    new SpreadsheetMetadataSignature("CreatedOn", DateTime.Now),      // قيمة التاريخ والوقت
                    new SpreadsheetMetadataSignature("DocumentId", 123456),           // قيمة صحيحة
                    new SpreadsheetMetadataSignature("SignatureId", 123.456D),        // قيمة مزدوجة
                    new SpreadsheetMetadataSignature("Amount", 123.456M),             // القيمة العشرية
                    new SpreadsheetMetadataSignature("Total", 123.456F)               // قيمة التعويم
                };
                
                // إضافة مجموعة التوقيعات إلى الخيارات
                options.Signatures.AddRange(signatures);
                
                // توقيع المستند وحفظه في الملف
                SignResult result = signature.Sign(outputFilePath, options);
                
                // عرض النتائج
                Console.WriteLine($"\nSource spreadsheet signed successfully with {result.Succeeded.Count} signature(s).");
                Console.WriteLine($"File saved at {outputFilePath}.");
            }
        }
    }
}
```

## تقنيات البيانات الوصفية المتقدمة لجداول البيانات

### العمل مع خصائص جدول البيانات المخصصة والمضمنة

تحتوي جداول بيانات Excel على خصائص مدمجة ومخصصة، ويمكن الوصول إليها من خلال مربع حوار خصائص الملف. يتيح لك GroupDocs.Signature العمل مع كليهما:

```csharp
// إضافة خصائص مدمجة
signatures = new SpreadsheetMetadataSignature[]
{
    new SpreadsheetMetadataSignature("Company", "Sherlock Holmes Consulting"),
    new SpreadsheetMetadataSignature("Category", "Financial"),
    new SpreadsheetMetadataSignature("Keywords", "budget,forecast,analysis"),
    new SpreadsheetMetadataSignature("Comments", "This spreadsheet contains confidential information"),
    new SpreadsheetMetadataSignature("Manager", "John Watson")
};
options.Signatures.AddRange(signatures);

// إضافة خصائص مخصصة
options.Signatures.Add(new SpreadsheetMetadataSignature("Department", "Finance"));
options.Signatures.Add(new SpreadsheetMetadataSignature("SecurityLevel", "Confidential"));
```

### البحث عن البيانات الوصفية في جداول البيانات الموقعة

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

### تحديث البيانات الوصفية الموجودة

يمكنك تحديث البيانات الوصفية الموجودة في جداول البيانات باستخدام أسماء الخصائص نفسها:

```csharp
// تحديث البيانات الوصفية الموجودة
options.Signatures.Add(new SpreadsheetMetadataSignature("Author", "Updated Author Name"));
```

## خاتمة

في هذا البرنامج التعليمي الشامل، تعلمت كيفية توقيع جداول بيانات Excel باستخدام البيانات الوصفية باستخدام GroupDocs.Signature لـ .NET. يُحسّن تضمين البيانات الوصفية في ملفات جداول البيانات إمكانية تتبع المستندات، ويوفر سياقًا قيّمًا، ويساعد في إثبات صحتها.

تُعد توقيعات البيانات الوصفية في جداول البيانات مفيدةً بشكل خاص في بيئات العمل التي تُعد فيها معرفة أصل المستند ومؤلفه وتتبع إصداراته أمرًا بالغ الأهمية. يمكن أن تتضمن البيانات الوصفية المضمنة معلومات حول المؤلف ووقت الإنشاء ومعرفات المستند والخصائص المخصصة المناسبة لاحتياجات مؤسستك.

من خلال تنفيذ توقيعات البيانات الوصفية مع GroupDocs.Signature، يمكنك التأكد من أن جداول بيانات Excel الخاصة بك تحافظ على سلامتها وتوفر معلومات يمكن التحقق منها طوال دورة حياتها.

## الأسئلة الشائعة

### هل يمكنني إضافة بيانات وصفية إلى جداول البيانات التي تحتوي بالفعل على بعض الخصائص المحددة؟

نعم، يمكنك إضافة بيانات تعريفية جديدة أو تحديث بيانات تعريفية موجودة في جداول البيانات. سيتولى GroupDocs.Signature عملية التكامل، إما بإضافة خصائص جديدة أو تحديث خصائص موجودة بنفس الأسماء.

### ما هي تنسيقات جداول البيانات المدعومة لتوقيع البيانات الوصفية؟

يدعم GroupDocs.Signature لـ .NET توقيع البيانات الوصفية لمختلف تنسيقات جداول البيانات، بما في ذلك XLSX وXLS وXLSM وODS وغيرها. للاطلاع على القائمة الكاملة، يُرجى مراجعة [الوثائق الرسمية](https://docs.groupdocs.com/signature/net/).

### هل تكون توقيعات البيانات الوصفية في جداول البيانات مرئية للمستخدمين؟

لا تظهر توقيعات البيانات الوصفية في محتوى جدول البيانات نفسه. مع ذلك، يُمكن عرضها من خلال لوحة خصائص المستند في Excel أو أي تطبيقات أخرى متوافقة.

### هل يمكنني التحقق برمجيًا من أن جدول البيانات قد تم العبث به بعد إضافة البيانات الوصفية؟

نعم، يوفر GroupDocs.Signature إمكانيات التحقق التي يمكن أن تساعد في اكتشاف ما إذا كان قد تم تعديل المستند بعد التوقيع، بما في ذلك التغييرات في البيانات الوصفية.

### هل تؤثر إضافة البيانات الوصفية على وظيفة جدول البيانات؟

إضافة البيانات الوصفية لها تأثير ضئيل على حجم الملف، ولا تؤثر على وظائف جدول البيانات. إنها طريقة سهلة لتحسين خصائص المستند دون التأثير على العمليات الحسابية أو الصيغ أو ميزات Excel الأخرى.

### أين يمكنني العثور على المزيد من الموارد والدعم؟

- [مرجع واجهة برمجة التطبيقات](https://reference.groupdocs.com/signature/net/)
- [التنزيلات](https://releases.groupdocs.com/signature/net/)
- [أمثلة](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
- [التوثيق](https://docs.groupdocs.com/signature/net/)
- [صفحة المنتج](https://products.groupdocs.com/signature/net/)
- [مدونة](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
- [منتدى الدعم](https://forum.groupdocs.com/c/signature/13)
- [رخصة مؤقتة](https://purchase.groupdocs.com/temporary-license/)