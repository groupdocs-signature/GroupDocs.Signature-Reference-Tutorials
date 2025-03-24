---
title: توقيع المستندات باستخدام رمز الاستجابة السريعة باستخدام GroupDocs.Signature
linktitle: التوقيع باستخدام رمز الاستجابة السريعة
second_title: GroupDocs.Signature .NET API
description: تعرف على كيفية إضافة توقيعات رمز الاستجابة السريعة إلى مستنداتك باستخدام GroupDocs.Signature لـ .NET. تعزيز الأمن والمصادقة دون عناء.
weight: 15
url: /ar/net/advanced-signature-techniques/sign-with-qr-code/
---
## مقدمة
في هذا البرنامج التعليمي، سنتعرف على عملية توقيع المستندات باستخدام رمز الاستجابة السريعة باستخدام GroupDocs.Signature for .NET. GroupDocs.Signature for .NET عبارة عن واجهة برمجة تطبيقات قوية تتيح للمطورين إضافة أنواع مختلفة من التوقيعات إلى المستندات الرقمية برمجيًا. يمكن أن يوفر توقيع المستندات باستخدام رموز QR طبقة إضافية من الأمان والمصادقة لمستنداتك.
## المتطلبات الأساسية
قبل أن نبدأ، تأكد من تثبيت المتطلبات الأساسية التالية:
1.  GroupDocs.Signature لـ .NET: يمكنك تنزيل المكتبة من[موقع إلكتروني](https://releases.groupdocs.com/signature/net/).
2. بيئة التطوير: تأكد من إعداد بيئة تطوير .NET على جهازك.
3. مستند نموذجي: قم بإعداد مستند نموذجي (على سبيل المثال، PDF) الذي تريد التوقيع عليه باستخدام رمز الاستجابة السريعة.

## استيراد مساحات الأسماء الضرورية
قبل الغوص في الكود، فلنستورد مساحات الأسماء الضرورية:
```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

## الخطوة 1: تحديد مسارات الملفات
```csharp
string filePath = "sample.pdf";
string fileName = Path.GetFileName(filePath);
string outputFilePath = Path.Combine("Your Document Directory", "SignWithQRCode", fileName);
```
 تأكد من الاستبدال`"Your Document Directory"` بالمسار إلى الدليل الذي تريد حفظ المستند الموقع فيه.
## الخطوة 2: تهيئة كائن التوقيع
```csharp
using (Signature signature = new Signature(filePath))
{
    //رمز التوقيع يذهب هنا
}
```
 تهيئة أ`Signature` الكائن الذي يحتوي على المسار إلى المستند الذي تريد التوقيع عليه.
## الخطوة 3: إنشاء QRCodeSignOptions
```csharp
QrCodeSignOptions options = new QrCodeSignOptions("JohnSmith")
{
    EncodeType = QrCodeTypes.QR,
    Left = 50,
    Top = 150,
    Width = 200,
    Height = 200
};
```
 إنشاء`QrCodeSignOptions` الكائن بالإعدادات المطلوبة لتوقيع رمز الاستجابة السريعة. يمكنك تخصيص المعلمات مثل النص لتشفير رمز الاستجابة السريعة وموضعه وأبعاده.
## الخطوة 4: قم بالتوقيع على الوثيقة
```csharp
SignResult result = signature.Sign(outputFilePath, options);
```
 استخدم ال`Sign` طريقة`Signature` كائن لتوقيع المستند بالخيارات المحددة. ترجع هذه الطريقة أ`SignResult` كائن يحتوي على معلومات حول عملية التوقيع.
## الخطوة 5: عرض النتيجة
```csharp
Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).\nFile saved at {outputFilePath}.");
```
عرض رسالة تشير إلى نجاح عملية التوقيع ومكان حفظ الوثيقة الموقعة.

## خاتمة
في هذا البرنامج التعليمي، تعلمنا كيفية توقيع المستندات باستخدام رمز الاستجابة السريعة باستخدام GroupDocs.Signature لـ .NET. باتباع هذه الخطوات البسيطة، يمكنك إضافة توقيعات رمز الاستجابة السريعة إلى مستنداتك الرقمية، مما يعزز الأمان والمصادقة.

## الأسئلة الشائعة
### هل يمكنني تخصيص مظهر رمز الاستجابة السريعة؟
نعم، يمكنك تخصيص معلمات مختلفة مثل الحجم والموضع ونوع تشفير رمز الاستجابة السريعة وفقًا لمتطلباتك.
### ما هي تنسيقات المستندات المدعومة للتوقيع باستخدام رموز QR؟
يدعم GroupDocs.Signature for .NET نطاقًا واسعًا من تنسيقات المستندات، بما في ذلك PDF وWord وExcel وPowerPoint والمزيد.
### هل من الممكن التوقيع على مستندات متعددة في عملية مجمعة؟
بالتأكيد، يمكنك استخدام GroupDocs.Signature for .NET لتوقيع مستندات متعددة في وقت واحد، مما يؤدي إلى تبسيط سير عملك.
### هل يمكنني التحقق من صحة مستند موقع برمز QR؟
نعم، يوفر GroupDocs.Signature for .NET آليات التحقق لضمان سلامة وصحة المستندات الموقعة.
### هل هناك نسخة تجريبية متاحة لاختبار الوظيفة قبل الشراء؟
 نعم، يمكنك تنزيل نسخة تجريبية مجانية من[موقع إلكتروني](https://releases.groupdocs.com/) لتقييم ميزات وإمكانيات GroupDocs.Signature لـ .NET.