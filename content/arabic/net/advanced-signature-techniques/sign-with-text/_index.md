---
title: التوقيع بالنص باستخدام GroupDocs.Signature لـ .NET
linktitle: التوقيع بالنص
second_title: GroupDocs.Signature .NET API
description: تعرف على كيفية توقيع المستندات التي تحتوي على نص باستخدام GroupDocs.Signature لـ .NET. دليل خطوة بخطوة لإضافة التوقيعات النصية برمجياً.
weight: 17
url: /ar/net/advanced-signature-techniques/sign-with-text/
---
## مقدمة
في العصر الرقمي، أصبح توقيع المستندات إلكترونيًا ممارسة قياسية، مما يوفر الوقت والموارد. يقدم GroupDocs.Signature for .NET حلاً شاملاً لإضافة التوقيعات النصية إلى تنسيقات المستندات المختلفة برمجيًا. في هذا البرنامج التعليمي، سنرشدك خلال عملية توقيع مستند يحتوي على نص باستخدام GroupDocs.Signature لـ .NET.
## المتطلبات الأساسية
قبل أن نتعمق في البرنامج التعليمي، تأكد من أن لديك المتطلبات الأساسية التالية:
1.  GroupDocs.Signature لـ .NET: تأكد من تثبيت GroupDocs.Signature لمكتبة .NET. يمكنك تنزيله من[هنا](https://releases.groupdocs.com/signature/net/).
2. بيئة التطوير: تمتع ببيئة عمل معدة لتطوير .NET.
3. المستند: قم بإعداد المستند (على سبيل المثال، PDF وWord) الذي تريد التوقيع عليه بالنص.

## استيراد مساحات الأسماء
أولاً، تحتاج إلى استيراد مساحات الأسماء الضرورية إلى مشروع .NET الخاص بك لاستخدام وظائف GroupDocs.Signature.
```csharp
using System;
using System.IO;
using System.Drawing;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

دعنا نقسم عملية توقيع مستند يحتوي على نص إلى خطوات متعددة:
## الخطوة 1: تحميل المستند
قم بتحميل المستند الذي تريد التوقيع عليه بالنص.
```csharp
string filePath = "sample.pdf"; // المسار إلى الوثيقة
string fileName = Path.GetFileName(filePath);
```
## الخطوة 2: تعيين مسار ملف الإخراج
حدد مسار ملف الإخراج حيث سيتم حفظ المستند الموقع.
```csharp
string outputFilePath = Path.Combine("Your Document Directory", "SignWithText", fileName);
```
## الخطوة 3: إنشاء خيارات التوقيع
قم بإعداد خيارات توقيع النص، بما في ذلك محتوى النص والموضع والحجم واللون والخط.
```csharp
TextSignOptions options = new TextSignOptions("John Smith")
{
    Left = 50, // تعيين موقف التوقيع
    Top = 200,
    Width = 100, // تعيين مستطيل التوقيع
    Height = 30,
    ForeColor = Color.Red, // ضبط لون النص
    Font = new SignatureFont { Size = 14, FamilyName = "Comic Sans MS" } // تعيين الخط
};
```
## الخطوة 4: التوقيع على الوثيقة
استخدم GroupDocs.Signature لتوقيع المستند بالخيارات المحددة وحفظ المستند الموقع في مسار ملف الإخراج.
```csharp
using (Signature signature = new Signature(filePath))
{
    SignResult result = signature.Sign(outputFilePath, options); // وثيقة التوقيع
    Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).\nFile saved at {outputFilePath}.");
}
```

## خاتمة
في هذا البرنامج التعليمي، تعلمنا كيفية توقيع مستند يحتوي على نص باستخدام GroupDocs.Signature لـ .NET. باتباع هذه الخطوات، يمكنك إضافة التوقيعات النصية بكفاءة إلى مستنداتك برمجيًا، مما يعزز الأمان والأصالة.
## الأسئلة الشائعة
### هل يمكنني تخصيص مظهر توقيع النص؟
نعم، يمكنك تخصيص معلمات مختلفة مثل اللون والخط والحجم وموضع توقيع النص وفقًا لتفضيلاتك.
### هل GroupDocs.Signature متوافق مع تنسيقات المستندات المتعددة؟
نعم، يدعم GroupDocs.Signature تنسيقات المستندات المختلفة بما في ذلك PDF وWord وExcel وPowerPoint والمزيد.
### هل يمكنني إضافة توقيعات نصية متعددة إلى مستند واحد؟
بالتأكيد، يمكنك إضافة توقيعات نصية متعددة إلى المستند، ولكل منها مجموعة خاصة به من خيارات التخصيص.
### هل يضمن GroupDocs.Signature سلامة المستند بعد التوقيع؟
نعم، يستخدم GroupDocs.Signature خوارزميات تشفير قوية لضمان سلامة المستند ومنع التلاعب به بعد التوقيع.
### هل هناك نسخة تجريبية متاحة للاختبار قبل الشراء؟
 نعم، يمكنك تنزيل نسخة تجريبية مجانية من[هنا](https://releases.groupdocs.com/) لاستكشاف الميزات قبل إجراء عملية الشراء.