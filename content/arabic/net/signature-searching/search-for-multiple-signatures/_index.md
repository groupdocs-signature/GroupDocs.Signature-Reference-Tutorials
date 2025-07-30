---
"description": "تعرّف على كيفية البحث عن أنواع متعددة من التوقيعات في المستندات باستخدام GroupDocs.Signature لـ .NET. دليل شامل مع أمثلة برمجية لتعزيز أمان المستندات."
"linktitle": "البحث عن توقيعات متعددة"
"second_title": "واجهة برمجة تطبيقات GroupDocs.Signature .NET"
"title": "البحث عن أنواع متعددة من التوقيعات في المستندات"
"url": "/ar/net/signature-searching/search-for-multiple-signatures/"
"weight": 14
---

## مقدمة

في أنظمة إدارة المستندات الحديثة، تتزايد أهمية إمكانية البحث عن أنواع متعددة من التوقيعات والتحقق منها ضمن مستند واحد. غالبًا ما تستخدم المؤسسات أنواعًا مختلفة من التوقيعات - مثل التوقيعات الرقمية، والتوقيعات النصية، والرموز الشريطية، ورموز الاستجابة السريعة، وغيرها - لتعزيز أمان المستندات وتبسيط عمليات التحقق. يوفر GroupDocs.Signature لـ .NET إطار عمل قويًا يُمكّن المطورين من تطبيق وظيفة بحث شاملة عن التوقيعات عبر تنسيقات المستندات المختلفة.

سوف يرشدك هذا البرنامج التعليمي خلال عملية البحث عن أنواع متعددة من التوقيعات داخل المستندات باستخدام GroupDocs.Signature لـ .NET، مع تقديم تفسيرات مفصلة وأمثلة عملية للكود.

## المتطلبات الأساسية

قبل الغوص في تنفيذ وظيفة البحث عن التوقيعات المتعددة، تأكد من أن لديك المتطلبات الأساسية التالية:

1. بيئة التطوير: Visual Studio أو أي بيئة تطوير .NET مفضلة مثبتة على نظامك.
  
2. GroupDocs.Signature لـ .NET: قم بتنزيل وتثبيت مكتبة GroupDocs.Signature لـ .NET من [هنا](https://releases.groupdocs.com/signature/net/).

3. المعرفة الأساسية بلغة C#: المعرفة بلغة البرمجة C# ومفاهيم إطار عمل .NET.

4. المستندات النموذجية: قم بإعداد مستندات اختبار تحتوي على أنواع مختلفة من التوقيعات لأغراض الاختبار.

## استيراد مساحات الأسماء

ابدأ باستيراد مساحات الأسماء الضرورية للوصول إلى وظيفة GroupDocs.Signature:

```csharp
using System;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

الآن، دعنا نقسم عملية البحث عن أنواع متعددة من التوقيعات إلى خطوات واضحة وقابلة للإدارة:

## الخطوة 1: تحميل المستند

أولاً، قم بتحميل المستند الذي يحتوي على التوقيعات التي تريد البحث عنها:

```csharp
string filePath = "sample_multiple_signatures.docx";
using (Signature signature = new Signature(filePath))
{
    // سيتم إضافة رمز البحث متعدد التوقيعات هنا
}
```

## الخطوة 2: تحديد خيارات البحث لأنواع التوقيع المختلفة

إنشاء خيارات بحث لكل نوع توقيع تريد البحث عنه:

```csharp
// تحديد خيارات البحث للتوقيعات النصية
TextSearchOptions textOptions = new TextSearchOptions
{
    AllPages = true,  // البحث في جميع الصفحات
    Text = "Signature",  // اختياري: النص للبحث عنه
    MatchType = TextMatchType.Contains  // معايير المطابقة
};

// تحديد خيارات البحث للتوقيعات الرقمية
DigitalSearchOptions digitalOptions = new DigitalSearchOptions
{
    AllPages = true
};

// تحديد خيارات البحث لتوقيعات الباركود
BarcodeSearchOptions barcodeOptions = new BarcodeSearchOptions
{
    AllPages = true,
    Text = "123456",  // اختياري: نص الباركود المطابق
    MatchType = TextMatchType.Exact  // معايير المطابقة
};

// تحديد خيارات البحث لتوقيعات رمز الاستجابة السريعة
QrCodeSearchOptions qrCodeOptions = new QrCodeSearchOptions
{
    AllPages = true,
    Text = "John",  // اختياري: نص رمز الاستجابة السريعة للمطابقة
    MatchType = TextMatchType.Contains  // معايير المطابقة
};

// تحديد خيارات البحث لتوقيعات البيانات الوصفية
MetadataSearchOptions metadataOptions = new MetadataSearchOptions();
```

## الخطوة 3: إضافة خيارات إلى المجموعة

إضافة كافة خيارات البحث إلى المجموعة:

```csharp
// إنشاء قائمة لاحتواء جميع خيارات البحث
List<SearchOptions> searchOptions = new List<SearchOptions>
{
    textOptions,
    digitalOptions,
    barcodeOptions,
    qrCodeOptions,
    metadataOptions
};
```

## الخطوة 4: إجراء البحث ومعالجة النتائج

قم بتنفيذ البحث باستخدام خيارات البحث المجمعة ومعالجة النتائج:

```csharp
// ابحث عن جميع أنواع التوقيع باستخدام الخيارات المحددة
SearchResult result = signature.Search(searchOptions);

// التحقق من وجود توقيعات
if (result.Signatures.Count > 0)
{
    Console.WriteLine($"\nSource document ['{filePath}'] contains {result.Signatures.Count} signature(s):");
    
    // التكرار من خلال التوقيعات التي تم العثور عليها
    foreach (var foundSignature in result.Signatures)
    {
        Console.WriteLine($"Signature found: Type: {foundSignature.SignatureType}, Page: {foundSignature.PageNumber}, ID: {foundSignature.SignatureId}");
        
        // أنواع التوقيعات الخاصة بالعملية
        if (foundSignature is TextSignature textSignature)
        {
            Console.WriteLine($"Text: '{textSignature.Text}'");
        }
        else if (foundSignature is BarcodeSignature barcodeSignature)
        {
            Console.WriteLine($"Barcode Type: {barcodeSignature.EncodeType.TypeName}, Text: '{barcodeSignature.Text}'");
        }
        else if (foundSignature is QrCodeSignature qrCodeSignature)
        {
            Console.WriteLine($"QR Code Type: {qrCodeSignature.EncodeType.TypeName}, Text: '{qrCodeSignature.Text}'");
        }
        else if (foundSignature is DigitalSignature digitalSignature)
        {
            Console.WriteLine($"Certificate: {digitalSignature.Certificate?.SubjectName}, Valid: {digitalSignature.IsValid}");
        }
        else if (foundSignature is MetadataSignature metadataSignature)
        {
            Console.WriteLine($"Metadata: Name: {metadataSignature.Name}, Value: {metadataSignature.Value}");
        }
    }
}
else
{
    Console.WriteLine("No signatures were found in the document.");
}
```

## مثال كامل

فيما يلي مثال عملي كامل يوضح كيفية البحث عن أنواع متعددة من التوقيعات في مستند:

```csharp
using System;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;

namespace MultiSignatureSearch
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
                try
                {
                    // تحديد خيارات البحث للتوقيعات النصية
                    TextSearchOptions textOptions = new TextSearchOptions
                    {
                        AllPages = true,
                        MatchType = TextMatchType.Contains
                    };

                    // تحديد خيارات البحث للتوقيعات الرقمية
                    DigitalSearchOptions digitalOptions = new DigitalSearchOptions
                    {
                        AllPages = true
                    };

                    // تحديد خيارات البحث لتوقيعات الباركود
                    BarcodeSearchOptions barcodeOptions = new BarcodeSearchOptions
                    {
                        AllPages = true
                    };

                    // تحديد خيارات البحث لتوقيعات رمز الاستجابة السريعة
                    QrCodeSearchOptions qrCodeOptions = new QrCodeSearchOptions
                    {
                        AllPages = true
                    };

                    // تحديد خيارات البحث لتوقيعات البيانات الوصفية
                    MetadataSearchOptions metadataOptions = new MetadataSearchOptions();

                    // إنشاء قائمة لاحتواء جميع خيارات البحث
                    List<SearchOptions> searchOptions = new List<SearchOptions>
                    {
                        textOptions,
                        digitalOptions,
                        barcodeOptions,
                        qrCodeOptions,
                        metadataOptions
                    };

                    // البحث عن جميع أنواع التوقيع
                    SearchResult result = signature.Search(searchOptions);

                    // التحقق من وجود توقيعات
                    if (result.Signatures.Count > 0)
                    {
                        Console.WriteLine($"\nSource document ['{filePath}'] contains {result.Signatures.Count} signature(s):");
                        
                        // نتائج العملية حسب نوع التوقيع
                        foreach (var foundSignature in result.Signatures)
                        {
                            Console.WriteLine($"Signature found: Type: {foundSignature.SignatureType}, Page: {foundSignature.PageNumber}");
                            
                            // أنواع التوقيعات الخاصة بالعملية
                            switch (foundSignature.SignatureType)
                            {
                                case SignatureType.Text:
                                    var textSignature = foundSignature as TextSignature;
                                    Console.WriteLine($"Text: '{textSignature.Text}'");
                                    break;
                                    
                                case SignatureType.Barcode:
                                    var barcodeSignature = foundSignature as BarcodeSignature;
                                    Console.WriteLine($"Barcode Type: {barcodeSignature.EncodeType.TypeName}, Text: '{barcodeSignature.Text}'");
                                    break;
                                    
                                case SignatureType.QrCode:
                                    var qrCodeSignature = foundSignature as QrCodeSignature;
                                    Console.WriteLine($"QR Code Type: {qrCodeSignature.EncodeType.TypeName}, Text: '{qrCodeSignature.Text}'");
                                    break;
                                    
                                case SignatureType.Digital:
                                    var digitalSignature = foundSignature as DigitalSignature;
                                    Console.WriteLine($"Certificate: {digitalSignature.Certificate?.SubjectName}, Valid: {digitalSignature.IsValid}");
                                    break;
                                    
                                case SignatureType.Metadata:
                                    var metadataSignature = foundSignature as MetadataSignature;
                                    Console.WriteLine($"Metadata: Name: {metadataSignature.Name}, Value: {metadataSignature.Value}");
                                    break;
                            }
                            
                            Console.WriteLine(); // إضافة فاصل للأسطر بين التوقيعات
                        }
                    }
                    else
                    {
                        Console.WriteLine("No signatures were found in the document.");
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

## تقنيات البحث المتقدمة متعددة التوقيعات

### تصفية نتائج البحث

يمكنك تنفيذ التصفية المتقدمة لتضييق نتائج البحث:

```csharp
// تصفية النتائج حسب رقم الصفحة
var signaturesOnFirstPage = result.Signatures.FindAll(s => s.PageNumber == 1);

// تصفية النتائج حسب نوع التوقيع
var digitalSignatures = result.Signatures.FindAll(s => s.SignatureType == SignatureType.Digital);
var qrCodeSignatures = result.Signatures.FindAll(s => s.SignatureType == SignatureType.QrCode);

// تصفية توقيعات النصوص التي تحتوي على محتوى محدد
var approvalSignatures = result.Signatures
    .FindAll(s => s is TextSignature && ((TextSignature)s).Text.Contains("Approved"));
```

### التحقق من صحة التوقيعات المتعددة

تنفيذ منطق التحقق لأنواع التوقيع المختلفة:

```csharp
bool ValidateAllSignatures(SearchResult result)
{
    bool isDocumentValid = true;
    
    // التحقق مما إذا كان المستند يحتوي على توقيع رقمي صالح
    bool hasValidDigitalSignature = result.Signatures
        .Any(s => s is DigitalSignature && ((DigitalSignature)s).IsValid);
    
    if (!hasValidDigitalSignature)
    {
        Console.WriteLine("Warning: Document does not contain a valid digital signature");
        isDocumentValid = false;
    }
    
    // تحقق مما إذا كان المستند يحتوي على رمز الاستجابة السريعة المطلوب
    bool hasRequiredQRCode = result.Signatures
        .Any(s => s is QrCodeSignature && ((QrCodeSignature)s).Text.Contains("Auth-Code"));
    
    if (!hasRequiredQRCode)
    {
        Console.WriteLine("Warning: Document does not contain the required authentication QR code");
        isDocumentValid = false;
    }
    
    return isDocumentValid;
}
```

### البحث باستخدام المعالجة المخصصة

يمكنك تحديد منطق المعالجة المخصص لعمليات البحث:

```csharp
// إنشاء خيارات البحث باستخدام المعالجة المخصصة
TextSearchOptions textOptions = new TextSearchOptions
{
    AllPages = true,
    
    // تعريف المعالجة المخصصة باستخدام المندوب
    ProcessCompleted = (signature) =>
    {
        // منطق التحقق المخصص - قبول التوقيعات فقط على الصفحات المحددة
        TextSignature textSignature = signature as TextSignature;
        return textSignature != null && (textSignature.PageNumber == 1 || textSignature.PageNumber == 2);
    }
};
```

## خاتمة

في هذا الدليل الشامل، استكشفنا كيفية البحث عن أنواع متعددة من التوقيعات داخل المستندات باستخدام GroupDocs.Signature لـ .NET. بدءًا من إعداد خيارات البحث لأنواع التوقيعات المختلفة، وصولًا إلى معالجة النتائج والتحقق من صحتها، أصبحت لديك الآن المعرفة اللازمة لتطبيق وظيفة بحث فعّالة عن التوقيعات في تطبيقات .NET الخاصة بك.

تُحسّن إمكانية البحث عن أنواع متعددة من التوقيعات في آنٍ واحد عمليات التحقق من المستندات، وتُعزز إجراءات الأمان، وتُبسّط سير عمل التحقق من صحة المستندات. يُوفّر GroupDocs.Signature إطار عمل قويًا ومرنًا للعمل مع أنواع توقيعات مُختلفة عبر تنسيقات مستندات مُختلفة، مما يجعله خيارًا ممتازًا لتطبيقات معالجة المستندات.

## الأسئلة الشائعة

### هل يمكنني البحث عن التوقيعات في المستندات المحمية بكلمة مرور؟

نعم، يدعم GroupDocs.Signature البحث عن التوقيعات في المستندات المحمية بكلمة مرور. يمكنك إدخال كلمة المرور عند تهيئة `Signature` هدف:

```csharp
LoadOptions loadOptions = new LoadOptions { Password = "your_password" };
using (Signature signature = new Signature(filePath, loadOptions))
{
    // البحث عن التوقيعات
}
```

### ما هي تنسيقات المستندات المدعومة للبحث عن التوقيع؟

يدعم GroupDocs.Signature مجموعة واسعة من تنسيقات المستندات، بما في ذلك PDF، ومستندات Microsoft Office (Word، Excel، PowerPoint)، وتنسيقات OpenOffice، والصور، والمزيد.

### هل يمكنني تقييد البحث على صفحات محددة في مستند؟

نعم، يحتوي كل نوع من خيارات البحث على خصائص تسمح لك بتحديد الصفحات التي تريد البحث فيها:

```csharp
TextSearchOptions options = new TextSearchOptions
{
    AllPages = false,  // لا تبحث في كل الصفحات
    PageNumber = 1,    // البحث فقط في الصفحة 1
    
    // أو حدد صفحات متعددة
    PagesSetup = new PagesSetup { Pages = new List<int> { 1, 3, 5 } }
};
```

### كيف يمكنني تحسين الأداء عند البحث في مستندات كبيرة؟

بالنسبة للمستندات الكبيرة، يمكنك تحسين الأداء من خلال:

1. تقييد البحث على صفحات أو نطاقات صفحات محددة
2. استخدام معايير بحث أكثر تحديدًا لتقليل عدد المطابقات المحتملة
3. تنفيذ الترقيم الصفحي في عرض النتائج
4. البحث عن نوع توقيع واحد في كل مرة إذا كنت لا تحتاج إلى نتائج متزامنة

### هل يمكنني توسيع GroupDocs.Signature لدعم أنواع التوقيع المخصصة؟

على الرغم من أن GroupDocs.Signature يوفر دعمًا مدمجًا لأنواع التوقيع الشائعة، يمكنك توسيع وظائفه من خلال:

1. إنشاء خيارات بحث مخصصة للفئات المشتقة من `SearchOptions`
2. تنفيذ منطق المعالجة المخصص باستخدام `ProcessCompleted` مندوب
3. تطوير فئات التغليف التي تجمع بين عمليات البحث المتعددة عن التوقيعات ومنطق الأعمال المتقدم

## انظر أيضا

* [مرجع واجهة برمجة التطبيقات](https://reference.groupdocs.com/signature/net/)
* [أمثلة التعليمات البرمجية على GitHub](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
* [وثائق المنتج](https://docs.groupdocs.com/signature/net/)
* [صفحة المنتج](https://products.groupdocs.com/signature/net/)
* [تنزيل أحدث إصدار](https://releases.groupdocs.com/signature/net/)
* [مقالات المدونة](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
* [منتدى الدعم المجاني](https://forum.groupdocs.com/c/signature/13)
* [رخصة مؤقتة](https://purchase.groupdocs.com/temporary-license/)