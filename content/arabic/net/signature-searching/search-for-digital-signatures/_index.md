---
"description": "أتقن البحث عن التوقيعات الرقمية في المستندات باستخدام GroupDocs.Signature لـ .NET. عزز أمان المستندات والتحقق منها باستخدام دليلنا المفصل خطوة بخطوة."
"linktitle": "البحث عن التوقيعات الرقمية"
"second_title": "واجهة برمجة تطبيقات GroupDocs.Signature .NET"
"title": "البحث عن التوقيعات الرقمية في المستندات"
"url": "/ar/net/signature-searching/search-for-digital-signatures/"
"weight": 11
---

## مقدمة

في ظلّ المشهد الرقميّ الحالي، يُعدّ ضمان صحة المستندات وسلامتها أمرًا بالغ الأهمية للشركات والمؤسسات. تُوفّر التوقيعات الرقمية آليةً فعّالة للتحقق من صحة المستندات واكتشاف التعديلات غير المُصرّح بها. يُقدّم GroupDocs.Signature لـ .NET حلاًّ شاملاً للتعامل مع التوقيعات الرقمية في مختلف تنسيقات المستندات، ممّا يُمكّن المُطوّرين من دمج وظائف التوقيع بسلاسة في تطبيقات .NET الخاصة بهم.

سوف يرشدك هذا البرنامج التعليمي خلال عملية البحث عن التوقيعات الرقمية داخل المستندات باستخدام GroupDocs.Signature لـ .NET، مع توفير تفسيرات مفصلة وأمثلة عملية للكود.

## المتطلبات الأساسية

قبل الخوض في تفاصيل التنفيذ، تأكد من أن لديك المتطلبات الأساسية التالية:

1. GroupDocs.Signature لـ .NET: قم بتنزيل المكتبة وتثبيتها من [هنا](https://releases.groupdocs.com/signature/net/).
   
2. بيئة التطوير: قم بإعداد بيئة تطوير .NET باستخدام Visual Studio أو IDE المفضل لديك.
   
3. المستندات النموذجية: قم بإعداد مستندات نموذجية تحتوي على توقيعات رقمية لأغراض الاختبار.

4. المعرفة الأساسية: المعرفة بلغة البرمجة C# وأساسيات إطار عمل .NET.

## استيراد مساحات الأسماء

ابدأ باستيراد مساحات الأسماء المطلوبة للوصول إلى الوظائف التي توفرها GroupDocs.Signature لـ .NET:

```csharp
using System;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

الآن، دعونا نقسم عملية البحث عن التوقيعات الرقمية إلى خطوات واضحة وقابلة للإدارة:

## الخطوة 1: تهيئة كائن التوقيع

ابدأ بإنشاء مثيل لـ `Signature` الفئة، تمرير المسار إلى مستندك:

```csharp
string filePath = "sample_multiple_signatures.docx";
using (Signature signature = new Signature(filePath))
{
    // سيتم إضافة الكود الخاص بالبحث عن التوقيعات الرقمية هنا
}
```

## الخطوة 2: البحث عن التوقيعات الرقمية

بعد ذلك، استخدم `Search` الطريقة مع `SignatureType.Digital` المعلمة للبحث عن التوقيعات الرقمية في المستند:

```csharp
// البحث عن التوقيعات الرقمية في المستند
List<DigitalSignature> signatures = signature.Search<DigitalSignature>(SignatureType.Digital);
```

## الخطوة 3: معالجة النتائج وعرضها

أخيرًا، قم بمعالجة نتائج البحث وعرض المعلومات ذات الصلة بالتوقيعات الرقمية التي تم العثور عليها:

```csharp
Console.WriteLine($"\nSource document ['{filePath}'] contains the following digital signatures:");
foreach (var digitalSignature in signatures)
{
    Console.WriteLine($"Digital signature found from {digitalSignature.SignTime} with validation status: {digitalSignature.IsValid}");
    Console.WriteLine($"Certificate: Subject: {digitalSignature.Certificate?.SubjectName}");
    Console.WriteLine($"Certificate: Issuer: {digitalSignature.Certificate?.IssuerName}");
    Console.WriteLine($"Certificate: Serial Number: {digitalSignature.Certificate?.SerialNumber}");
    Console.WriteLine();
}
```

## مثال كامل

فيما يلي مثال عملي كامل يوضح كيفية البحث عن التوقيعات الرقمية في مستند:

```csharp
using System;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;

namespace SearchDigitalSignatures
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
                // البحث عن التوقيعات الرقمية في المستند
                List<DigitalSignature> signatures = signature.Search<DigitalSignature>(SignatureType.Digital);
                
                // عرض نتائج البحث
                Console.WriteLine($"\nSource document ['{filePath}'] contains the following digital signatures:");
                
                if (signatures.Count > 0)
                {
                    foreach (var digitalSignature in signatures)
                    {
                        Console.WriteLine($"Digital signature found from {digitalSignature.SignTime} with validation status: {digitalSignature.IsValid}");
                        Console.WriteLine($"Certificate: Subject: {digitalSignature.Certificate?.SubjectName}");
                        Console.WriteLine($"Certificate: Issuer: {digitalSignature.Certificate?.IssuerName}");
                        Console.WriteLine($"Certificate: Serial Number: {digitalSignature.Certificate?.SerialNumber}");
                        Console.WriteLine();
                    }
                }
                else
                {
                    Console.WriteLine("No digital signatures found in the document.");
                }
            }
        }
    }
}
```

## خيارات البحث المتقدمة

لإجراء عمليات بحث أكثر استهدافًا، يمكنك استخدام `DigitalSearchOptions` لتخصيص معايير البحث:

```csharp
// إنشاء خيارات البحث الرقمية
DigitalSearchOptions options = new DigitalSearchOptions()
{
    // البحث فقط في صفحات محددة (على سبيل المثال، الصفحتين 1 و2)
    PageNumber = 1,
    PagesSetup = new PagesSetup() { Pages = new List<int> { 1, 2 } },
    
    // تصفية حسب التعليقات في التوقيعات الرقمية
    Comments = "Approved",
    
    // تعيين التاريخ ونطاق الوقت للبحث
    SignDateTimeFrom = new DateTime(2022, 1, 1),
    SignDateTimeTo = DateTime.Now
};

// البحث باستخدام خيارات محددة
List<DigitalSignature> signatures = signature.Search<DigitalSignature>(options);
```

## العمل مع معلومات الشهادة

تحتوي التوقيعات الرقمية على معلومات شهادة قيمة يمكنك الوصول إليها والتحقق من صحتها:

```csharp
foreach (var digitalSignature in signatures)
{
    if (digitalSignature.Certificate != null)
    {
        // خصائص شهادة الوصول
        Console.WriteLine($"Certificate Valid From: {digitalSignature.Certificate.NotBefore}");
        Console.WriteLine($"Certificate Valid To: {digitalSignature.Certificate.NotAfter}");
        
        // التحقق مما إذا كانت الشهادة ضمن نطاق تاريخ صالح
        bool isDateValid = DateTime.Now >= digitalSignature.Certificate.NotBefore && 
                          DateTime.Now <= digitalSignature.Certificate.NotAfter;
        
        Console.WriteLine($"Certificate Date Validity: {isDateValid}");
        
        // تفاصيل جهة إصدار شهادة الوصول
        Console.WriteLine($"Certificate Issuer: {digitalSignature.Certificate.IssuerName}");
    }
}
```

## خاتمة

يوفر GroupDocs.Signature لـ .NET حلاً فعالاً ومرنًا للبحث عن التوقيعات الرقمية والتحقق منها داخل المستندات. في هذا البرنامج التعليمي، استكشفنا خطوة بخطوة عملية تطبيق وظيفة البحث عن التوقيعات الرقمية في تطبيقات .NET، مما يزودك بالمعرفة اللازمة لتعزيز أمان المستندات والتحقق من سلامتها.

من خلال الاستفادة من GroupDocs.Signature، يمكنك إنشاء أنظمة قوية لإدارة المستندات تضمن صحة وسلامة مستنداتك الرقمية، مما يعزز الثقة والامتثال في عمليات عملك.

## الأسئلة الشائعة

### هل يمكن لـ GroupDocs.Signature التحقق من صحة التوقيعات الرقمية؟

نعم، يقوم GroupDocs.Signature تلقائيًا بالتحقق من صحة التوقيعات الرقمية أثناء عملية البحث ويوفر حالة التحقق من خلال `IsValid` ممتلكات `DigitalSignature` فصل.

### ما هي تنسيقات المستندات التي تدعم البحث بالتوقيع الرقمي؟

يدعم GroupDocs.Signature البحث عن التوقيع الرقمي في تنسيقات مختلفة، بما في ذلك PDF، ومستندات Microsoft Office (Word، Excel، PowerPoint)، وتنسيقات OpenOffice، والمزيد.

### هل يمكنني البحث عن التوقيعات الرقمية في المستندات المحمية بكلمة مرور؟

نعم، يمكنك البحث عن التوقيعات الرقمية في المستندات المحمية بكلمة مرور من خلال تقديم كلمة المرور عند تهيئة `Signature` هدف:

```csharp
LoadOptions loadOptions = new LoadOptions() { Password = "your_password" };
using (Signature signature = new Signature(filePath, loadOptions))
{
    // البحث عن التوقيعات الرقمية
}
```

### كيف يمكنني التحقق من أن التوقيع الرقمي تم إنشاؤه بواسطة شخص معين؟

يمكنك فحص اسم موضوع الشهادة والخصائص الأخرى للتحقق من هوية الموقع:

```csharp
foreach (var signature in signatures)
{
    if (signature.Certificate?.SubjectName?.Contains("John Doe") == true)
    {
        Console.WriteLine("Found signature by John Doe");
    }
}
```

### هل يمكنني استخراج المفتاح العام من شهادة التوقيع الرقمي؟

نعم، يمكنك الوصول إلى معلومات المفتاح العام من خلال خصائص الشهادة:

```csharp
if (signature.Certificate != null)
{
    // الوصول إلى معلومات المفتاح العام
    Console.WriteLine($"Public Key: {signature.Certificate.GetPublicKeyString()}");
}
```

## انظر أيضا

* [مرجع واجهة برمجة التطبيقات](https://reference.groupdocs.com/signature/net/)
* [أمثلة التعليمات البرمجية](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
* [وثائق المنتج](https://docs.groupdocs.com/signature/net/)
* [صفحة المنتج](https://products.groupdocs.com/signature/net/)
* [تنزيل أحدث إصدار](https://releases.groupdocs.com/signature/net/)
* [مقالات المدونة](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
* [منتدى الدعم](https://forum.groupdocs.com/c/signature/13)
* [رخصة مؤقتة](https://purchase.groupdocs.com/temporary-license/)