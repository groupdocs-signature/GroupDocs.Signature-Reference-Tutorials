---
title: التوقيع بالتوقيع الرقمي
linktitle: التوقيع بالتوقيع الرقمي
second_title: GroupDocs.Signature .NET API
description: تعرف على كيفية توقيع المستندات رقميًا في .NET باستخدام GroupDocs.Signature. عزز الأمان والأصالة من خلال هذا البرنامج التعليمي الشامل.
weight: 12
url: /ar/net/advanced-signature-techniques/sign-with-digital/
---
## مقدمة
تلعب التوقيعات الرقمية دورًا حاسمًا في ضمان صحة وسلامة المستندات الإلكترونية. في مجال تطوير .NET، يقدم GroupDocs.Signature حلاً قويًا لدمج التوقيعات الرقمية بسلاسة في تطبيقاتك. سيرشدك هذا البرنامج التعليمي خلال عملية توقيع مستند باستخدام التوقيع الرقمي باستخدام GroupDocs.Signature لـ .NET.
## المتطلبات الأساسية
قبل أن نتعمق في التنفيذ، تأكد من توفر المتطلبات الأساسية التالية:
1.  GroupDocs.Signature لـ .NET: قم بتنزيل وتثبيت GroupDocs.Signature لـ .NET من[صفحة التحميل](https://releases.groupdocs.com/signature/net/).
2. الشهادة الرقمية: احصل على الشهادة الرقمية (.pfx) التي سيتم استخدامها لتوقيع المستند. إذا لم يكن لديك شهادة، يمكنك إنشاء شهادة موقعة ذاتيًا أو الحصول عليها من مرجع مصدق موثوق به.
3. المستند المراد التوقيع عليه: قم بإعداد المستند (على سبيل المثال، PDF) الذي تريد توقيعه رقميًا. تأكد من أن لديك الأذونات اللازمة للوصول إلى المستند وتعديله.
4. صورة التوقيع: اختياريًا، يمكنك تقديم صورة لتوقيعك والتي سيتم تضمينها في المستند. وهذا يضيف لمسة شخصية إلى التوقيع الرقمي.

## استيراد مساحات الأسماء
أولاً، لنستورد مساحات الأسماء الضرورية إلى كود C# الخاص بنا:
```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## الخطوة 1: تحديد مسارات الملفات وخياراتها
حدد مسارات الملفات للمستند الذي سيتم توقيعه، وصورة التوقيع (إن أمكن)، والشهادة الرقمية.
```csharp
string filePath = "sample.pdf";
string fileName = Path.GetFileName(filePath);
string imagePath = "signature_handwrite.jpg";
string certificatePath = "YourSignature.pfx";
string outputFilePath = Path.Combine("Your Document Directory", "SignWithDigital", fileName);
```
## الخطوة 2: تهيئة كائن التوقيع
 إنشاء مثيل لـ`Signature` فئة عن طريق تمرير مسار الوثيقة للتوقيع.
```csharp
using (Signature signature = new Signature(filePath))
{
    // تحديد خيارات التوقيع الرقمي
    DigitalSignOptions options = new DigitalSignOptions(certificatePath)
    {
        ImageFilePath = imagePath, // تعيين مسار ملف الصورة (اختياري)
        Left = 50,                 //قم بتعيين إحداثي X لموضع التوقيع
        Top = 50,                  // قم بتعيين إحداثي Y لموضع التوقيع
        PageNumber = 1,            // حدد رقم الصفحة للتوقيع
        Password = "1234567890"    // تعيين كلمة المرور للشهادة (إذا لزم الأمر)
    };
    // الخطوة 3: قم بالتوقيع على الوثيقة
    SignResult result = signature.Sign(outputFilePath, options);
    // الخطوة 4: عرض النتيجة
    Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).\nFile saved at {outputFilePath}.");
}
```

## خاتمة
في هذا البرنامج التعليمي، اكتشفنا كيفية توقيع مستند باستخدام التوقيع الرقمي باستخدام GroupDocs.Signature لـ .NET. باتباع هذه الخطوات البسيطة، يمكنك تعزيز أمان وصحة مستنداتك الإلكترونية، مما يضمن أنها تظل مقاومة للتلاعب وملزمة قانونًا.
## الأسئلة الشائعة
### ما هو التوقيع الرقمي؟
التوقيع الرقمي هو أسلوب تشفير يستخدم للتحقق من صحة وسلامة المستندات أو الرسائل الرقمية.
### هل يمكنني توقيع المستندات باستخدام GroupDocs.Signature باستخدام شهادة موقعة ذاتيًا؟
نعم، يمكنك توقيع المستندات باستخدام شهادة موقعة ذاتيًا تم إنشاؤها بواسطة أدوات مثل OpenSSL أو MakeCert من Microsoft.
### هل GroupDocs.Signature متوافق مع تنسيقات المستندات المختلفة؟
نعم، يدعم GroupDocs.Signature نطاقًا واسعًا من تنسيقات المستندات، بما في ذلك PDF وWord وExcel وPowerPoint والمزيد.
### هل يمكنني تخصيص مظهر توقيعي الرقمي؟
قطعاً! يسمح لك GroupDocs.Signature بتخصيص جوانب مختلفة من توقيعك الرقمي، مثل موضعه وحجمه ومظهره.
### هل GroupDocs.Signature مناسب للتطبيقات على مستوى المؤسسة؟
نعم، يوفر GroupDocs.Signature ميزات قوية وقابلية للتوسع، مما يجعله خيارًا مثاليًا لتطبيقات توقيع المستندات على مستوى المؤسسة.