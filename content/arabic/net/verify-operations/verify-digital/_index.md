---
"description": "طبّق عملية التحقق الآمن من التوقيع الرقمي في تطبيقات .NET باستخدام GroupDocs.Signature. دليل خطوة بخطوة مع أمثلة برمجية شاملة لمصادقة المستندات."
"linktitle": "التحقق من التوقيع الرقمي"
"second_title": "واجهة برمجة تطبيقات GroupDocs.Signature .NET"
"title": "التحقق من التوقيعات الرقمية في المستندات"
"url": "/ar/net/verify-operations/verify-digital/"
"weight": 11
type: docs
---
## مقدمة

تلعب التوقيعات الرقمية دورًا حاسمًا في ضمان صحة المستندات وسلامتها وعدم نقضها في عمليات الأعمال الحديثة. وخلافًا للتوقيعات اليدوية التقليدية، تستخدم التوقيعات الرقمية تقنيات تشفير للتحقق من هوية المُوقّع وضمان عدم تعديل المستند منذ توقيعه.

يوفر GroupDocs.Signature لـ .NET مجموعة أدوات شاملة تُمكّن المطورين من تطبيق عملية تحقق فعّالة من التوقيعات الرقمية في تطبيقات .NET. سيرشدك هذا البرنامج التعليمي المُفصّل خلال عملية التحقق من التوقيعات الرقمية داخل المستندات باستخدام GroupDocs.Signature لـ .NET.

## المتطلبات الأساسية

قبل تنفيذ وظيفة التحقق من التوقيع الرقمي، تأكد من توفر المتطلبات الأساسية التالية:

1. GroupDocs.Signature لـ .NET: قم بتنزيل المكتبة وتثبيتها من [GroupDocs.Signature لإصدارات .NET](https://releases.groupdocs.com/signature/net/).
2. بيئة تطوير .NET: Visual Studio أو أي بيئة تطوير .NET متوافقة.
3. الشهادة الرقمية: ملف شهادة رقمية (على سبيل المثال، .pfx) تم استخدامه لتوقيع المستند أو شهادة تنتمي إلى السلسلة الموثوقة.
4. وثيقة للتحقق: وثيقة تحتوي على توقيعات رقمية تحتاج إلى التحقق.

## استيراد مساحات الأسماء المطلوبة

ابدأ باستيراد مساحات الأسماء الضرورية للوصول إلى وظيفة GroupDocs.Signature:

```csharp
using System;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

دعونا نقسم عملية التحقق من التوقيعات الرقمية إلى خطوات واضحة وقابلة للإدارة:

## الخطوة 1: تحديد مسار المستند

```csharp
// المسار إلى المستند الذي يحتوي على التوقيعات الرقمية
string filePath = "sample_multiple_signatures.docx";
```

استبدل مسار المثال بالمسار الفعلي للمستند الذي يحتوي على التوقيعات الرقمية.

## الخطوة 2: تهيئة كائن التوقيع

```csharp
// إنشاء مثيل لفئة التوقيع عن طريق تمرير مسار المستند
using (Signature signature = new Signature(filePath))
{
    // سيتم تنفيذ رمز التحقق هنا
}
```

فئة التوقيع هي نقطة الدخول الرئيسية لجميع العمليات في واجهة برمجة التطبيقات GroupDocs.Signature.

## الخطوة 3: تكوين خيارات التحقق الرقمي

```csharp
// إعداد خيارات التحقق
DigitalVerifyOptions options = new DigitalVerifyOptions("YourSignature.pfx")
{
    Contact = "Mr.Smith",     // جهة اتصال التوقيع المتوقعة
    Password = "1234567890",  // كلمة مرور الشهادة إذا لزم الأمر
    AllPages = true           // التحقق من جميع الصفحات بحثًا عن التوقيعات
};
```

تتيح لك خيارات التحقق تحديد:
- مسار ملف الشهادة الرقمية
- معلومات الاتصال بالموقع المتوقع
- كلمة المرور للشهادة إذا كانت محمية بكلمة مرور
- نطاق الصفحات المطلوب التحقق منها (كل الصفحات بشكل افتراضي)

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
    Console.WriteLine($"Document {filePath} contains valid digital signatures!");
    
    // عرض تفاصيل التوقيعات الصالحة
    foreach (DigitalSignature digitalSignature in result.Succeeded)
    {
        Console.WriteLine($"\nValid signature found:");
        Console.WriteLine($"Signer: {digitalSignature.Subject}");
        Console.WriteLine($"Issuer: {digitalSignature.Issuer}");
        Console.WriteLine($"Valid From: {digitalSignature.ValidFrom}");
        Console.WriteLine($"Valid To: {digitalSignature.ValidTo}");
    }
}
else
{
    Console.WriteLine($"Document {filePath} failed verification process.");
    
    // عرض معلومات حول التوقيعات الفاشلة إذا لزم الأمر
    foreach (DigitalSignature failedSignature in result.Failed)
    {
        Console.WriteLine($"Failed signature reason: {failedSignature.Comments}");
    }
}
```

يتحقق هذا الرمز من نجاح التحقق ويوفر معلومات مفصلة حول التوقيعات التي تم التحقق منها.

## مثال كامل

فيما يلي مثال عملي كامل يوضح التحقق من التوقيع الرقمي:

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
                    DigitalVerifyOptions options = new DigitalVerifyOptions("YourSignature.pfx")
                    {
                        Contact = "Mr.Smith",
                        Password = "1234567890"
                    };
                    
                    // التحقق من توقيعات المستندات
                    VerificationResult result = signature.Verify(options);
                    
                    // نتائج التحقق من العملية
                    if (result.IsValid)
                    {
                        Console.WriteLine($"Document {filePath} contains valid digital signatures!");
                        
                        foreach (DigitalSignature item in result.Succeeded)
                        {
                            Console.WriteLine($"\nValid signature found.");
                            Console.WriteLine($"Subject: {item.Subject}");
                            Console.WriteLine($"Comments: {item.Comments}");
                            Console.WriteLine($"Sign Time: {item.SignTime}");
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

### التحقق من التوقيعات الرقمية المتعددة

```csharp
// إنشاء قائمة بخيارات التحقق
List<VerifyOptions> listOptions = new List<VerifyOptions>();

// إضافة خيارات التحقق من الشهادة الأولى
listOptions.Add(new DigitalVerifyOptions("Certificate1.pfx")
{
    Contact = "John Smith"
});

// إضافة خيارات التحقق من الشهادة الثانية
listOptions.Add(new DigitalVerifyOptions("Certificate2.pfx")
{
    Contact = "Jane Doe"
});

// التحقق باستخدام خيارات متعددة
VerificationResult result = signature.Verify(listOptions);
```

### التحقق من التوقيعات على صفحات محددة

```csharp
// التحقق من التوقيعات الرقمية فقط في الصفحة الأولى
DigitalVerifyOptions options = new DigitalVerifyOptions("YourSignature.pfx")
{
    AllPages = false,
    PageNumber = 1
};
```

### استخدام الطابع الزمني والتحقق من صحة هيئة الشهادة

```csharp
DigitalVerifyOptions options = new DigitalVerifyOptions("YourSignature.pfx")
{
    ValidateTimeStampOnly = true,   // التحقق من صحة الطابع الزمني فقط
    CertificateAuth = CertificateAuthType.Standard  // التحقق من صحة شهادة الموقع
};
```

## أفضل الممارسات للتحقق من التوقيع الرقمي

1. إدارة الشهادات المناسبة: قم بتخزين ملفات الشهادات بشكل آمن وإدارة كلمات المرور بشكل مناسب.
2. التحقق من صحة الشهادة: تنفيذ التحقق من صحة سلسلة الشهادات للتأكد من أن الشهادة نفسها صالحة.
3. معالجة الأخطاء: تنفيذ معالجة قوية للأخطاء لإدارة حالات فشل التحقق بسلاسة.
4. التسجيل: تسجيل محاولات التحقق والنتائج لأغراض التدقيق والامتثال.
5. تحديثات الشهادات بانتظام: تأكد من تحديث الشهادات قبل انتهاء صلاحيتها.

## استكشاف الأخطاء وإصلاحها

### شهادة غير صالحة
- تأكد من أن مسار ملف الشهادة صحيح
- تأكد من صحة كلمة مرور الشهادة
- التحقق مما إذا كانت الشهادة قد انتهت صلاحيتها

### لم يتم العثور على التوقيع
- تأكد من أن المستند يحتوي بالفعل على توقيعات رقمية
- تأكد من أنك تقوم بفحص الصفحات الصحيحة

### فشل التحقق
- التحقق مما إذا كان قد تم تعديل المستند بعد التوقيع
- التحقق من أن شهادة المُوقِّع موجودة في سلسلة الشهادات الموثوقة

## خاتمة

يوفر GroupDocs.Signature لـ .NET حلاً فعالاً ومرنًا للتحقق من التوقيعات الرقمية داخل المستندات. باتباع هذا الدليل المفصل، يمكنك تطبيق عملية تحقق قوية من التوقيعات الرقمية في تطبيقات .NET، مما يضمن صحة المستندات وسلامتها.

يُعدّ التحقق من التوقيع الرقمي عنصرًا أساسيًا في سير عمل المستندات الآمنة في بيئات الأعمال الحديثة. مع GroupDocs.Signature، يمكنك تنفيذ هذه الوظيفة بثقة وبأقل جهد، مستفيدًا من واجهة برمجة التطبيقات الشاملة للتعامل مع سيناريوهات التحقق المختلفة.

## الأسئلة الشائعة

### هل يمكن لـ GroupDocs.Signature التحقق من التوقيعات في مستندات PDF التي تم توقيعها باستخدام Adobe Acrobat؟
نعم، يمكن لـ GroupDocs.Signature التحقق من التوقيعات الرقمية القياسية في مستندات PDF التي تم إنشاؤها بواسطة Adobe Acrobat وبرامج PDF المتوافقة الأخرى.

### هل يدعم GroupDocs.Signature التحقق من الطوابع الزمنية للمستندات؟
نعم، توفر واجهة برمجة التطبيقات خيارات للتحقق من طوابع زمنية للمستندات كجزء من عملية التحقق من التوقيع الرقمي.

### هل يمكنني التحقق من التوقيعات على صفحات معينة من مستند متعدد الصفحات؟
نعم، يمكنك تكوين خيارات التحقق للتحقق من التوقيعات على صفحات محددة بدلاً من المستند بأكمله.

### هل يدعم GroupDocs.Signature التحقق من التوقيعات المتعددة ضمن مستند واحد؟
نعم، يمكن لـ GroupDocs.Signature التحقق من التوقيعات الرقمية المتعددة ضمن مستند واحد وتوفير نتائج مفصلة لكل توقيع.

### هل من الممكن التحقق من التوقيعات التي تم إنشاؤها باستخدام شهادات من هيئات شهادات مختلفة؟
نعم، يدعم GroupDocs.Signature التحقق من التوقيعات التي تم إنشاؤها باستخدام شهادات من هيئات شهادات مختلفة، طالما أنها موجودة في سلسلة الشهادات الموثوقة.

### الموارد ذات الصلة
* [مرجع API لـ GroupDocs.Signature](https://reference.groupdocs.com/signature/net/)
* [تنزيلات GroupDocs.Signature](https://releases.groupdocs.com/signature/net/)
* [أمثلة التعليمات البرمجية على GitHub](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
* [التوثيق](https://docs.groupdocs.com/signature/net/)
* [صفحة المنتج](https://products.groupdocs.com/signature/net/)
* [مقالات المدونة](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
* [منتدى الدعم](https://forum.groupdocs.com/c/signature/13)
* [رخصة مؤقتة](https://purchase.groupdocs.com/temporary-license/)