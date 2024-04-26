---
title: توقيع المستندات بالصورة باستخدام GroupDocs.Signature
linktitle: التوقيع بالصورة
second_title: GroupDocs.Signature .NET API
description: تعرف على كيفية توقيع المستندات باستخدام الصور في تطبيقات .NET باستخدام Groupdocs.Signature لـ .NET. تعزيز أمان المستندات وأصالتها دون عناء.
type: docs
weight: 13
url: /ar/net/advanced-signature-techniques/sign-with-image/
---
## مقدمة
في هذا البرنامج التعليمي، سوف نستكشف كيفية توقيع المستندات باستخدام الصور باستخدام Groupdocs.Signature for .NET. يضيف توقيع المستندات طبقة إضافية من الأصالة والأمان إلى ملفاتك، مما يجعلها مقاومة للتلاعب وملزمة قانونًا. بمساعدة Groupdocs.Signature for .NET، يمكنك دمج وظيفة توقيع المستندات بسلاسة في تطبيقات .NET الخاصة بك.
## المتطلبات الأساسية
قبل الغوص في البرنامج التعليمي، تأكد من أن لديك المتطلبات الأساسية التالية:
1.  Groupdocs.Signature لـ .NET: تأكد من تثبيت Groupdocs.Signature لـ .NET في بيئة التطوير الخاصة بك. يمكنك تنزيله من[موقع إلكتروني](https://releases.groupdocs.com/signature/net/).
2. بيئة تطوير .NET: تأكد من أن لديك بيئة تطوير .NET عاملة تم إعدادها على جهازك.

## استيراد مساحات الأسماء
قبل البدء بجزء الترميز، قم باستيراد مساحات الأسماء الضرورية للوصول إلى الفئات والطرق المطلوبة:
```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## الخطوة 1: قم بتحميل المستند
الخطوة الأولى هي تحميل المستند الذي تريد التوقيع عليه. قم بتوفير مسار ملف المستند الذي ترغب في التوقيع عليه:
```csharp
string filePath = "sample.pdf";
```
## الخطوة 2: تحديد صورة التوقيع
بعد ذلك، حدد المسار إلى صورة التوقيع التي تريد استخدامها للتوقيع:
```csharp
string imagePath = "signature_handwrite.jpg";
```
## الخطوة 3: تعيين مسار ملف الإخراج
حدد المسار الذي تريد حفظ المستند الموقع فيه:
```csharp
string outputFilePath = Path.Combine("Your Document Directory", "SignWithImage", fileName);
```
## الخطوة 4: تهيئة كائن التوقيع
قم بتهيئة كائن التوقيع عن طريق تمرير مسار ملف المستند:
```csharp
using (Signature signature = new Signature(filePath))
```
## الخطوة 5: ضبط خيارات توقيع الصورة
قم بتعيين خيارات توقيع الصورة، بما في ذلك موضع التوقيع، وما إذا كنت تريد التوقيع على جميع الصفحات، وما إلى ذلك:
```csharp
ImageSignOptions options = new ImageSignOptions(imagePath)
{
    Left = 50,
    Top = 50,
    AllPages = true
};
```
## الخطوة 6: قم بالتوقيع على الوثيقة
قم بتوقيع المستند باستخدام الصورة والخيارات المحددة:
```csharp
SignResult result = signature.Sign(outputFilePath, options);
```
## الخطوة 7: عرض النتيجة
وأخيراً عرض النتيجة التي تشير إلى نجاح عملية التوقيع ومكان الوثيقة الموقعة:
```csharp
Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).\nFile saved at {outputFilePath}.");
```

## خاتمة
في هذا البرنامج التعليمي، تعلمنا كيفية توقيع المستندات باستخدام الصور في تطبيقات .NET باستخدام Groupdocs.Signature لـ .NET. يعد توقيع المستندات جانبًا مهمًا في إدارة المستندات، حيث يوفر الأصالة والأمان لملفاتك.
## الأسئلة الشائعة
### هل يمكنني استخدام صور توقيع متعددة في مستند واحد؟
نعم، يمكنك توقيع مستند يحتوي على صور متعددة باستخدام Groupdocs.Signature لـ .NET. ما عليك سوى تكرار عملية التوقيع لكل صورة.
### هل Groupdocs.Signature for .NET متوافق مع كافة أنواع المستندات؟
يدعم Groupdocs.Signature for .NET نطاقًا واسعًا من تنسيقات المستندات، بما في ذلك PDF وWord وExcel والمزيد.
### هل يمكنني تخصيص مظهر التوقيع؟
نعم، يمكنك تخصيص جوانب مختلفة من مظهر التوقيع مثل الحجم والموضع والشفافية والمزيد.
### هل هناك نسخة تجريبية متاحة للاختبار؟
نعم، يمكنك تنزيل نسخة تجريبية مجانية من الموقع الإلكتروني لاختبار الوظيفة قبل إجراء عملية الشراء.
### كيف يمكنني الحصول على الدعم الفني لـ Groupdocs.Signature لـ .NET؟
 يمكنك الحصول على الدعم الفني من خلال زيارة منتدى Groupdocs.Signature[هنا](https://forum.groupdocs.com/c/signature/13).