---
title: التوقيع مع خيارات متعددة
linktitle: التوقيع مع خيارات متعددة
second_title: GroupDocs.Signature .NET API
description: تعرف على كيفية توقيع المستندات ذات الخيارات المتعددة باستخدام GroupDocs.Signature لـ .NET. تعزيز أمان المستندات باستخدام النص والرمز الشريطي ورمز الاستجابة السريعة والرقمي والصورة.
type: docs
weight: 14
url: /ar/net/advanced-signature-techniques/sign-with-multiple-options/
---
## مقدمة
في هذا البرنامج التعليمي، سوف نستكشف كيفية توقيع مستند باستخدام خيارات التوقيع المتعددة باستخدام مكتبة GroupDocs.Signature لـ .NET. يمكن أن يؤدي توقيع المستندات بخيارات متنوعة مثل التوقيعات النصية والرمز الشريطي ورمز الاستجابة السريعة والتوقيعات الرقمية والصور وبيانات التعريف إلى توفير تعدد الاستخدامات وتعزيز أمان المستندات.
## المتطلبات الأساسية
قبل البدء، تأكد من توفر المتطلبات الأساسية التالية:
1.  GroupDocs.Signature لمكتبة .NET: قم بتنزيل وتثبيت GroupDocs.Signature لمكتبة .NET من[هنا](https://releases.groupdocs.com/signature/net/).
2. بيئة التطوير: قم بإعداد بيئة تطوير مع تثبيت .NET Framework.
3. المستند المراد التوقيع عليه: قم بإعداد المستند (على سبيل المثال، Sample.docx) الذي تريد التوقيع عليه.
4. الشهادات والصور: قم بإعداد أي شهادات وصور مطلوبة للتوقيعات الرقمية والصورية.

## استيراد مساحات الأسماء
أولاً، قم باستيراد مساحات الأسماء الضرورية لاستخدام مكتبة GroupDocs.Signature في تطبيق .NET الخاص بك:
```csharp
using System;
using System.IO;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## الخطوة 1: قم بتحميل المستند
```csharp
string filePath = "sample.docx";
string outputFilePath = Path.Combine("Your Document Directory", "SignWithMultiple", "SignWithMultiple.docx");
using (Signature signature = new Signature(filePath))
{
    // يستمر الرمز الخاص بك ...
}
```
## الخطوة 2: تحديد خيارات التوقيع
تحديد عدة خيارات للتوقيع بأنواع وإعدادات مختلفة، مثل التوقيع النصي والرمز الشريطي ورمز الاستجابة السريعة والتوقيع الرقمي والصورة وبيانات التعريف:
```csharp
TextSignOptions textOptions = new TextSignOptions("Text signature")
{
    VerticalAlignment = VerticalAlignment.Top,
    HorizontalAlignment = HorizontalAlignment.Left
};
BarcodeSignOptions barcodeOptions = new BarcodeSignOptions("123456")
{
    EncodeType = BarcodeTypes.Code128,
    Left = 0,
    Top = 150,
    Height = 50,
    Width = 200
};
// تحديد خيارات التوقيع الأخرى (على سبيل المثال، رمز الاستجابة السريعة، الرقمي، الصورة، البيانات الوصفية)...
```
## الخطوة 3: إنشاء قائمة بخيارات التوقيع
حدد قائمة خيارات التوقيع التي تحتوي على جميع الخيارات المحددة مسبقًا:
```csharp
List<SignOptions> listOptions = new List<SignOptions>();
listOptions.Add(textOptions);
listOptions.Add(barcodeOptions);
// أضف خيارات التوقيع الأخرى إلى القائمة...
```
## الخطوة 4: قم بالتوقيع على الوثيقة
قم بتوقيع المستند بقائمة خيارات التوقيع واحفظ المستند الموقع:
```csharp
SignResult result = signature.Sign(outputFilePath, listOptions);
Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).\nFile saved at {outputFilePath}.");
```

## خاتمة
يوفر توقيع المستندات ذات الخيارات المتعددة باستخدام GroupDocs.Signature for .NET حلاً قويًا لتعزيز أمان المستندات وتعدد استخداماتها. باتباع الخطوات الموضحة في هذا البرنامج التعليمي، يمكنك دمج أنواع التوقيع المختلفة بسلاسة في تطبيقات .NET الخاصة بك.
## الأسئلة الشائعة
### هل يمكنني استخدام صور مخصصة للتوقيعات الرقمية؟
نعم، يمكنك تحديد صور مخصصة للتوقيعات الرقمية باستخدام مكتبة GroupDocs.Signature.
### هل GroupDocs.Signature متوافق مع تنسيقات المستندات المختلفة؟
نعم، يدعم GroupDocs.Signature تنسيقات المستندات المختلفة، بما في ذلك DOCX وPDF وPPTX والمزيد.
### هل يمكنني تخصيص مظهر التوقيعات النصية؟
بالتأكيد، يمكنك تخصيص مظهر التوقيعات النصية، بما في ذلك حجم الخط واللون والنمط.
### هل يوفر GroupDocs.Signature التشفير للتوقيعات الرقمية؟
نعم، يوفر GroupDocs.Signature خيارات تشفير للتوقيعات الرقمية لضمان أمان المستند.
### هل هناك إصدار تجريبي متاح لـ GroupDocs.Signature لـ .NET؟
 نعم، يمكنك تنزيل نسخة تجريبية مجانية من GroupDocs.Signature لـ .NET من[هنا](https://releases.groupdocs.com/).