---
"description": "دمج توقيعات البيانات الوصفية في مستندات PDF باستخدام GroupDocs.Signature لـ .NET. تعلم كيفية تضمين معلومات المؤلف، والطوابع الزمنية، والبيانات المخصصة لتعزيز مصداقية ملفات PDF وإمكانية تتبعها."
"linktitle": "توقيع ملف PDF باستخدام البيانات الوصفية"
"second_title": "واجهة برمجة تطبيقات GroupDocs.Signature .NET"
"title": "إضافة توقيعات البيانات الوصفية إلى مستندات PDF في C# .NET"
"url": "/ar/net/document-signing/sign-pdf-with-metadata/"
"weight": 11
type: docs
---
## مقدمة

تُستخدم مستندات PDF (تنسيق المستندات المحمولة) على نطاق واسع في مختلف القطاعات بفضل اتساقها واستقلاليتها عن المنصات. يُعد ضمان صحة هذه المستندات وإمكانية تتبعها أمرًا بالغ الأهمية في العديد من البيئات المهنية. ومن الطرق الفعالة لتحقيق ذلك تضمين البيانات الوصفية في ملفات PDF نفسها.

في هذا البرنامج التعليمي الشامل، سنستكشف كيفية توقيع مستندات PDF باستخدام البيانات الوصفية باستخدام GroupDocs.Signature لـ .NET. تتيح لك توقيعات البيانات الوصفية تضمين معلومات إضافية داخل المستند، مثل تفاصيل المؤلف، وتواريخ الإنشاء، ومعرفات المستند، والقيم المخصصة، دون تغيير مظهره بشكل واضح.

## المتطلبات الأساسية

قبل أن نبدأ، تأكد من أن لديك ما يلي:

1. [GroupDocs.Signature لـ .NET](https://releases.groupdocs.com/signature/net/) - تنزيل المكتبة وتثبيتها
2. بيئة التطوير - Visual Studio أو أي بيئة تطوير متكاملة أخرى متوافقة مع .NET
3. مستند PDF - ملف PDF نموذجي للتوقيع
4. المعرفة الأساسية بلغة C# - الإلمام بلغة البرمجة C#

## استيراد مساحات الأسماء

ابدأ باستيراد مساحات الأسماء الضرورية للوصول إلى وظيفة GroupDocs.Signature:

```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

## الخطوة 1: إعداد مسارات الملفات

أولاً، قم بتحديد المسار إلى مستند PDF الخاص بك وحدد المكان الذي تريد حفظ الإخراج الموقع فيه:

```csharp
// حدد المسار إلى مستند PDF الخاص بك
string filePath = "sample.pdf";

// تحديد دليل الإخراج ومسار الملف
string outputDirectory = "Your Document Directory";
string outputFilePath = Path.Combine(outputDirectory, "SignPdfWithMetadata", "SignedWithMetadata.pdf");

// تأكد من وجود دليل الإخراج
Directory.CreateDirectory(Path.GetDirectoryName(outputFilePath));
```

## الخطوة 2: تهيئة كائن التوقيع

قم بإنشاء مثيل لفئة التوقيع باستخدام مستند PDF المصدر الخاص بك:

```csharp
using (Signature signature = new Signature(filePath))
{
    // سيتم وضع الكود الخاص بالتوقيع هنا
}
```

## الخطوة 3: تحديد خيارات البيانات الوصفية

إنشاء وتكوين خيارات البيانات الوصفية، وإضافة أنواع مختلفة من توقيعات البيانات الوصفية:

```csharp
// إنشاء كائن خيارات البيانات الوصفية
MetadataSignOptions options = new MetadataSignOptions();

// أضف أنواعًا مختلفة من البيانات الوصفية باستخدام الواجهة السلسة
options
    .Add(new PdfMetadataSignature("Author", "Mr.Sherlock Holmes")) // قيمة السلسلة
    .Add(new PdfMetadataSignature("CreatedOn", DateTime.Now))       // قيمة التاريخ والوقت
    .Add(new PdfMetadataSignature("DocumentId", 123456))            // قيمة صحيحة
    .Add(new PdfMetadataSignature("SignatureId", 123.456D))         // قيمة مزدوجة
    .Add(new PdfMetadataSignature("Amount", 123.456M))              // القيمة العشرية
    .Add(new PdfMetadataSignature("Total", 123.456F));              // قيمة التعويم
```

## الخطوة 4: توقيع ملف PDF باستخدام البيانات الوصفية

قم بتطبيق توقيعات البيانات الوصفية على مستند PDF واحفظ النتيجة:

```csharp
// توقيع المستند وحفظه في مسار الإخراج
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

namespace SignPdfWithMetadataExample
{
    class Program
    {
        static void Main(string[] args)
        {
            // تحديد مسارات الملفات
            string filePath = "sample.pdf";
            string outputFilePath = Path.Combine("Your Document Directory", "SignPdfWithMetadata", "SignedWithMetadata.pdf");
            
            // تأكد من وجود دليل الإخراج
            Directory.CreateDirectory(Path.GetDirectoryName(outputFilePath));

            // توقيع ملف PDF باستخدام البيانات الوصفية
            using (Signature signature = new Signature(filePath))
            {
                // إنشاء كائن خيارات البيانات الوصفية
                MetadataSignOptions options = new MetadataSignOptions();
                
                // إضافة أنواع مختلفة من توقيعات البيانات الوصفية
                options
                    .Add(new PdfMetadataSignature("Author", "Mr.Sherlock Holmes")) // قيمة السلسلة
                    .Add(new PdfMetadataSignature("CreatedOn", DateTime.Now))       // قيمة التاريخ والوقت
                    .Add(new PdfMetadataSignature("DocumentId", 123456))            // قيمة صحيحة
                    .Add(new PdfMetadataSignature("SignatureId", 123.456D))         // قيمة مزدوجة
                    .Add(new PdfMetadataSignature("Amount", 123.456M))              // القيمة العشرية
                    .Add(new PdfMetadataSignature("Total", 123.456F));              // قيمة التعويم
                
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

## عمليات البيانات الوصفية المتقدمة لملفات PDF

### إضافة بيانات تعريفية مخصصة مع دعم مساحة الأسماء

تدعم مستندات PDF البيانات الوصفية المخصصة مع دعم مساحة اسم XML:

```csharp
// إضافة بيانات تعريفية مخصصة باستخدام مساحة الاسم
options.Add(new PdfMetadataSignature("CustomProperty", "Custom Value")
{
    NamespaceUri = "http://your-namespace.com/schema"
});
```

### البحث عن البيانات الوصفية في ملفات PDF الموقعة

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

### العمل مع بيانات التعريف القياسية لملف PDF

تحتوي مستندات PDF على حقول بيانات وصفية قياسية يمكن الوصول إليها وتعديلها:

```csharp
// تعيين حقول بيانات PDF القياسية
options
    .Add(new PdfMetadataSignature("Title", "Important Contract"))
    .Add(new PdfMetadataSignature("Subject", "Legal Agreement"))
    .Add(new PdfMetadataSignature("Keywords", "contract, agreement, legal, binding"))
    .Add(new PdfMetadataSignature("Creator", "Legal Department"))
    .Add(new PdfMetadataSignature("Producer", "GroupDocs.Signature"));
```

## خاتمة

في هذا البرنامج التعليمي، تعلمت كيفية توقيع مستندات PDF باستخدام البيانات الوصفية باستخدام GroupDocs.Signature لـ .NET. يُعد تضمين البيانات الوصفية في ملفات PDF طريقة ممتازة لتعزيز مصداقية المستندات، وإضافة معلومات مهمة، وتحسين سير عمل إدارة المستندات.

تُعد توقيعات البيانات الوصفية في ملفات PDF قيّمة بشكل خاص في بيئات العمل التي تُعد فيها إمكانية تتبع المستندات والتحقق من صحتها أمرًا بالغ الأهمية. يمكن أن تتضمن البيانات الوصفية المضمنة معلومات حول أصل المستند، ومؤلفه، ووقت إنشائه، وإصداره، والخصائص المخصصة ذات الصلة بسير عمل مؤسستك.

من خلال تنفيذ توقيعات البيانات الوصفية مع GroupDocs.Signature، يمكنك التأكد من أن مستندات PDF الخاصة بك تحافظ على سلامتها وتوفر معلومات يمكن التحقق منها طوال دورة حياتها.

## الأسئلة الشائعة

### هل يمكنني تعديل البيانات الوصفية الموجودة في مستند PDF؟

نعم، يمكنك تعديل البيانات الوصفية الموجودة في مستندات PDF. عند تطبيق توقيعات بيانات وصفية جديدة بنفس أسماء التوقيعات الحالية، سيتم تحديث القيم وفقًا لذلك.

### هل تكون توقيعات البيانات الوصفية في مستندات PDF مرئية للمستخدم النهائي؟

لا تظهر توقيعات البيانات الوصفية في محتوى المستند نفسه. مع ذلك، يُمكن عرضها من خلال لوحة خصائص المستند في برامج قراءة ملفات PDF مثل Adobe Acrobat أو باستخدام أدوات مُخصصة لعرض البيانات الوصفية.

### هل يمكنني تشفير أو حماية البيانات الوصفية في ملفات PDF؟

يوفر GroupDocs.Signature خيارات لتأمين المستندات، بما في ذلك التشفير. يمكنك تطبيق تشفير على مستوى المستند لحماية ملف PDF بأكمله، بما في ذلك بياناته الوصفية.

### هل هناك حد لكمية البيانات الوصفية التي يمكنني إضافتها إلى ملف PDF؟

على الرغم من عدم وجود حد أقصى لملفات PDF، إلا أن إضافة كميات زائدة من البيانات الوصفية قد يزيد من حجم الملف. يُنصح بتضمين المعلومات ذات الصلة والضرورية فقط في البيانات الوصفية.

### هل يمكنني التحقق برمجيًا من أن ملف PDF قد تم العبث به بعد إضافة البيانات الوصفية؟

نعم، يوفر GroupDocs.Signature إمكانيات التحقق التي يمكن أن تساعد في اكتشاف ما إذا كان قد تم تعديل المستند بعد التوقيع، بما في ذلك التغييرات في البيانات الوصفية.

### أين يمكنني العثور على المزيد من الموارد والدعم؟

- [مرجع واجهة برمجة التطبيقات](https://reference.groupdocs.com/signature/net/)
- [التنزيلات](https://releases.groupdocs.com/signature/net/)
- [أمثلة](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
- [التوثيق](https://docs.groupdocs.com/signature/net/)
- [صفحة المنتج](https://products.groupdocs.com/signature/net/)
- [مدونة](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
- [منتدى الدعم](https://forum.groupdocs.com/c/signature/13)
- [رخصة مؤقتة](https://purchase.groupdocs.com/temporary-license/)