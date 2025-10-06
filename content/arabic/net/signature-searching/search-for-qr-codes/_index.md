---
"description": "تعرف على كيفية البحث بكفاءة عن رموز QR في المستندات باستخدام GroupDocs.Signature لـ .NET باستخدام هذا الدليل الشامل خطوة بخطوة وأمثلة التعليمات البرمجية."
"linktitle": "البحث عن رموز الاستجابة السريعة"
"second_title": "واجهة برمجة تطبيقات GroupDocs.Signature .NET"
"title": "البحث عن توقيعات رمز الاستجابة السريعة في المستندات"
"url": "/ar/net/signature-searching/search-for-qr-codes/"
"weight": 15
type: docs
---
## مقدمة

في بيئة المستندات الرقمية الحالية، أصبحت توقيعات رموز الاستجابة السريعة (QR Codes) أداةً قيّمةً لتضمين المعلومات والمصادقة وتعزيز أمان المستندات. يوفر GroupDocs.Signature لـ .NET للمطورين واجهة برمجة تطبيقات فعّالة للبحث عن رموز الاستجابة السريعة (QR Codes) واستخراجها من مختلف تنسيقات المستندات، مما يتيح إمكانيات متقدمة لتحليل المستندات والتحقق منها في تطبيقات .NET.

سوف يرشدك هذا البرنامج التعليمي الشامل خلال عملية تنفيذ وظيفة البحث عن رمز الاستجابة السريعة باستخدام GroupDocs.Signature لـ .NET، مع توفير تفسيرات واضحة وتعليمات خطوة بخطوة وأمثلة أكواد عملية يمكنك دمجها في تطبيقاتك الخاصة.

## المتطلبات الأساسية

قبل الغوص في البحث عن توقيع رمز الاستجابة السريعة، تأكد من أن لديك المتطلبات الأساسية التالية:

1. GroupDocs.Signature لـ .NET SDK: قم بتنزيل SDK وتثبيته من [صفحة التحميل](https://releases.groupdocs.com/signature/net/).

2. بيئة التطوير: قم بإعداد بيئة تطوير .NET، مثل Visual Studio، مع تثبيت .NET Framework أو .NET Core.

3. المعرفة الأساسية: المعرفة ببرمجة C# ومفاهيم تطوير .NET.

4. المستندات النموذجية: قم بإعداد مستندات الاختبار التي تحتوي على رموز QR للتحقق والاختبار.

## استيراد مساحات الأسماء

ابدأ باستيراد المساحات الأساسية اللازمة للوصول إلى وظيفة GroupDocs.Signature:

```csharp
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
using System;
using System.Collections.Generic;
```

الآن، دعونا نقوم بتقسيم عملية البحث عن رموز الاستجابة السريعة (QR code) إلى خطوات واضحة وسهلة المتابعة:

## الخطوة 1: تحديد مسار المستند

أولاً، حدد المسار إلى المستند الذي يحتوي على رموز QR التي تريد البحث عنها:

```csharp
string filePath = "sample_multiple_signatures.docx";
```

## الخطوة 2: تهيئة كائن التوقيع

إنشاء مثيل لـ `Signature` الفئة عن طريق تمرير مسار المستند:

```csharp
using (Signature signature = new Signature(filePath))
{
    // سيتم إضافة رمز البحث عن رمز الاستجابة السريعة هنا
}
```

## الخطوة 3: البحث عن توقيعات رمز الاستجابة السريعة

استخدم `Search` الطريقة مع نوع التوقيع المناسب للعثور على رموز الاستجابة السريعة في المستند:

```csharp
// ابحث عن توقيعات رمز الاستجابة السريعة (QR) داخل المستند
List<QrCodeSignature> signatures = signature.Search<QrCodeSignature>(SignatureType.QrCode);
```

## الخطوة 4: معالجة النتائج وعرضها

قم بالتكرار من خلال توقيعات رمز الاستجابة السريعة التي تم العثور عليها والوصول إلى خصائصها:

```csharp
// عرض معلومات حول رموز الاستجابة السريعة التي تم العثور عليها
Console.WriteLine($"\nSource document contains {signatures.Count} QR code signature(s):");

foreach (var qrCodeSignature in signatures)
{
    Console.WriteLine($"QR Code found at page {qrCodeSignature.PageNumber} with type {qrCodeSignature.EncodeType.TypeName}");
    Console.WriteLine($"Content: {qrCodeSignature.Text}");
    Console.WriteLine($"Location: X={qrCodeSignature.Left}, Y={qrCodeSignature.Top}, Width={qrCodeSignature.Width}, Height={qrCodeSignature.Height}");
    Console.WriteLine();
}
```

## مثال كامل

فيما يلي مثال عملي شامل يوضح العملية الكاملة للبحث عن رموز الاستجابة السريعة في مستند:

```csharp
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
using System;
using System.Collections.Generic;

namespace QrCodeSignatureSearch
{
    class Program
    {
        static void Main(string[] args)
        {
            // مسار المستند - التحديث باستخدام مسار الملف الخاص بك
            string filePath = "sample_multiple_signatures.docx";
            
            // تهيئة مثيل التوقيع
            using (Signature signature = new Signature(filePath))
            {
                try
                {
                    // ابحث عن توقيعات رمز الاستجابة السريعة في المستند
                    List<QrCodeSignature> signatures = signature.Search<QrCodeSignature>(SignatureType.QrCode);
                    
                    // عرض نتائج البحث
                    Console.WriteLine($"\nSource document ['{filePath}'] contains {signatures.Count} QR code signature(s):");
                    
                    foreach (var qrCodeSignature in signatures)
                    {
                        Console.WriteLine($"QR Code found at page {qrCodeSignature.PageNumber} with type {qrCodeSignature.EncodeType.TypeName}");
                        Console.WriteLine($"Content: {qrCodeSignature.Text}");
                        Console.WriteLine($"Location: X={qrCodeSignature.Left}, Y={qrCodeSignature.Top}, Width={qrCodeSignature.Width}, Height={qrCodeSignature.Height}");
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

## تقنيات البحث المتقدمة عن رمز الاستجابة السريعة

### البحث باستخدام معايير محددة

لإجراء عمليات بحث أكثر استهدافًا، يمكنك استخدام `QrCodeSearchOptions` لتخصيص معايير البحث الخاصة بك:

```csharp
// إنشاء خيارات بحث رمز الاستجابة السريعة باستخدام معايير محددة
QrCodeSearchOptions options = new QrCodeSearchOptions
{
    // البحث فقط في صفحات محددة
    AllPages = false,
    PageNumber = 1,
    PagesSetup = new PagesSetup { Pages = new List<int> { 1, 3, 5 } },
    
    // تصفية حسب محتوى رمز الاستجابة السريعة
    Text = "Invoice",
    MatchType = TextMatchType.Contains,
    
    // تصفية حسب أنواع رمز الاستجابة السريعة المحددة
    EncodeType = QrCodeTypes.QR,
    
    // تحديد منطقة محددة للبحث داخلها
    Rectangle = new Rectangle(100, 100, 400, 400)
};

// البحث باستخدام خيارات محددة
List<QrCodeSignature> filteredSignatures = signature.Search<QrCodeSignature>(options);
```

### معالجة بيانات رمز الاستجابة السريعة

يمكنك تنفيذ معالجة مخصصة لبيانات رمز الاستجابة السريعة استنادًا إلى متطلبات تطبيقك:

```csharp
foreach (var qrCode in signatures)
{
    // استخراج ومعالجة بيانات رمز الاستجابة السريعة بناءً على المحتوى
    string qrContent = qrCode.Text;
    
    if (qrContent.StartsWith("URL:"))
    {
        // معالجة بيانات عنوان URL
        string url = qrContent.Substring(4);
        Console.WriteLine($"Found URL in QR code: {url}");
    }
    else if (qrContent.StartsWith("CONTACT:"))
    {
        // معلومات الاتصال بالعملية
        string contact = qrContent.Substring(8);
        Console.WriteLine($"Found contact information in QR code: {contact}");
    }
    else if (qrContent.StartsWith("INVOICE:"))
    {
        // معالجة معلومات الفاتورة
        string invoiceData = qrContent.Substring(8);
        Console.WriteLine($"Found invoice information in QR code: {invoiceData}");
        
        // تحليل بيانات الفاتورة والتحقق من صحتها
        if (ValidateInvoiceData(invoiceData))
        {
            Console.WriteLine("Invoice data is valid!");
        }
        else
        {
            Console.WriteLine("Warning: Invalid invoice data detected!");
        }
    }
}

// مثال على طريقة التحقق
static bool ValidateInvoiceData(string data)
{
    // تنفيذ منطق التحقق الخاص بك
    return !string.IsNullOrEmpty(data) && data.Contains("ID") && data.Contains("Amount");
}
```

### تنفيذ التحقق الأمني

تُستخدم رموز الاستجابة السريعة (QR codes) غالبًا لأغراض المصادقة. إليك كيفية تطبيق إجراءات التحقق الأمني الأساسية:

```csharp
// تحقق مما إذا كان المستند يحتوي على رمز QR صالح للمصادقة
bool hasValidAuthQrCode = false;

foreach (var qrCode in signatures)
{
    if (qrCode.Text.StartsWith("AUTH:"))
    {
        string authCode = qrCode.Text.Substring(5);
        
        // التحقق من رمز المصادقة (على سبيل المثال، مقابل قاعدة بيانات أو قائمة محددة مسبقًا)
        if (VerifyAuthCode(authCode))
        {
            hasValidAuthQrCode = true;
            Console.WriteLine("Document contains valid authentication QR code!");
            break;
        }
    }
}

if (!hasValidAuthQrCode)
{
    Console.WriteLine("Warning: Document does not contain a valid authentication QR code!");
}

// مثال على طريقة التحقق
static bool VerifyAuthCode(string code)
{
    // تنفيذ منطق التحقق الخاص بك
    // قد يكون هذا بحثًا في قاعدة البيانات، أو استدعاء واجهة برمجة التطبيقات، أو مقارنة بالقيم المحددة مسبقًا
    return code == "A7B82C3D" || code == "X9Y8Z7W6";
}
```

### استخراج صور رمز الاستجابة السريعة

يمكنك استخراج صور رمز الاستجابة السريعة من المستندات لمزيد من المعالجة أو العرض:

```csharp
// حفظ صور رمز الاستجابة السريعة على القرص
foreach (var qrCode in signatures)
{
    if (qrCode.Content != null)
    {
        // إنشاء اسم ملف فريد بناءً على رقم الصفحة وموضعها
        string outputPath = $"QrCode_P{qrCode.PageNumber}_X{qrCode.Left}_Y{qrCode.Top}.png";
        
        // حفظ بيانات الصورة
        File.WriteAllBytes(outputPath, qrCode.Content);
        Console.WriteLine($"Saved QR code image to {outputPath}");
    }
}
```

## خاتمة

في هذا الدليل الشامل، استكشفنا كيفية البحث عن توقيعات رموز الاستجابة السريعة (QR) في المستندات باستخدام GroupDocs.Signature لـ .NET. من البحث الأساسي إلى التقنيات المتقدمة، أصبحت لديك الآن المعرفة اللازمة لتطبيق معالجة فعّالة لرموز الاستجابة السريعة في تطبيقات .NET. توفر واجهة برمجة التطبيقات GroupDocs.Signature إطار عمل قويًا ومرنًا للعمل مع أنواع مختلفة من التوقيعات، بما في ذلك رموز الاستجابة السريعة، عبر تنسيقات مستندات مختلفة.

من خلال الاستفادة من هذه الإمكانات، يمكنك تحسين عمليات التحقق من المستندات، وتنفيذ أنظمة المصادقة، واستخراج معلومات قيمة مضمنة في رموز QR، كل ذلك داخل تطبيقات .NET الخاصة بك.

## الأسئلة الشائعة

### ما هي تنسيقات رمز الاستجابة السريعة (QR Code) التي يدعمها GroupDocs.Signature؟

يدعم GroupDocs.Signature تنسيقات مختلفة لرموز الاستجابة السريعة، بما في ذلك رموز الاستجابة السريعة القياسية، ورموز الاستجابة السريعة المصغرة، وغيرها من معايير رموز الاستجابة السريعة الشائعة. يمكن الوصول إلى التنسيق المحدد من خلال `EncodeType` ممتلكات `QrCodeSignature` هدف.

### هل يمكنني البحث عن رموز الاستجابة السريعة (QR code) في المستندات المحمية بكلمة مرور؟

نعم، يدعم GroupDocs.Signature البحث عن رموز الاستجابة السريعة (QR code) في المستندات المحمية بكلمة مرور من خلال توفير كلمة المرور عند تهيئة `Signature` هدف:

```csharp
LoadOptions loadOptions = new LoadOptions { Password = "your_password" };
using (Signature signature = new Signature(filePath, loadOptions))
{
    // البحث عن رموز الاستجابة السريعة
}
```

### كيف يمكنني تصفية رموز الاستجابة السريعة (QR) استنادًا إلى محتواها؟

يمكنك تصفية رموز الاستجابة السريعة (QR Codes) استنادًا إلى محتواها باستخدام `Text` و `MatchType` خصائص `QrCodeSearchOptions`:

```csharp
QrCodeSearchOptions options = new QrCodeSearchOptions
{
    Text = "Invoice",
    MatchType = TextMatchType.Contains // خيارات أخرى: Exact، StartsWith، EndsWith
};
```

### هل يمكن لـ GroupDocs.Signature اكتشاف رموز QR التالفة أو المرئية جزئيًا؟

يتمتع GroupDocs.Signature بقدرة جزئية على اكتشاف رموز الاستجابة السريعة (QR) المرئية جزئيًا، ولكن قد لا يتم التعرف على رموز الاستجابة السريعة التالفة بشدة. تعتمد دقة الكشف على جودة رمز الاستجابة السريعة ووضوحه في المستند.

### ما هي تنسيقات المستندات المدعومة للبحث عن رمز الاستجابة السريعة؟

يدعم GroupDocs.Signature البحث عن رمز الاستجابة السريعة في تنسيقات المستندات المختلفة بما في ذلك PDF، ومستندات Microsoft Office (Word، Excel، PowerPoint)، والصور (JPEG، PNG، TIFF)، وغيرها الكثير.

## انظر أيضا

* [مرجع واجهة برمجة التطبيقات](https://reference.groupdocs.com/signature/net/)
* [أمثلة التعليمات البرمجية على GitHub](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
* [وثائق المنتج](https://docs.groupdocs.com/signature/net/)
* [صفحة المنتج](https://products.groupdocs.com/signature/net/)
* [تنزيل أحدث إصدار](https://releases.groupdocs.com/signature/net/)
* [مقالات المدونة](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
* [منتدى الدعم المجاني](https://forum.groupdocs.com/c/signature/13)
* [رخصة مؤقتة](https://purchase.groupdocs.com/temporary-license/)