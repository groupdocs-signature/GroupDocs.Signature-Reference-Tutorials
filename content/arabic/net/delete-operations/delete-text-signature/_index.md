---
title: حذف التوقيع النصي
linktitle: حذف التوقيع النصي
second_title: GroupDocs.Signature .NET API
description: يمكنك حذف التوقيعات النصية من المستندات بسهولة باستخدام GroupDocs.Signature لـ .NET. تبسيط مهام إدارة المستندات الخاصة بك.
type: docs
weight: 17
url: /ar/net/delete-operations/delete-text-signature/
---
## مقدمة
تعد GroupDocs.Signature for .NET مكتبة قوية تمكن المطورين من دمج وظائف التوقيع الإلكتروني بسلاسة في تطبيقات .NET الخاصة بهم. سواء كنت تقوم بإنشاء نظام لإدارة المستندات، أو نظام أساسي لتوقيع العقود، أو أي تطبيق آخر يتطلب وظيفة التوقيع، فإن GroupDocs.Signature for .NET يوفر مجموعة شاملة من الأدوات لتبسيط العملية.
## المتطلبات الأساسية
قبل الغوص في استخدام GroupDocs.Signature لـ .NET، تأكد من توفر المتطلبات الأساسية التالية:
### 1. بيئة تطوير .NET
تأكد من إعداد بيئة تطوير .NET على جهازك. يمكنك تنزيل وتثبيت .NET SDK من موقع Microsoft على الويب.
### 2. GroupDocs.Signature لـ .NET
 قم بتنزيل وتثبيت GroupDocs.Signature لـ .NET من الرابط المقدم:[قم بتنزيل GroupDocs.Signature لـ .NET](https://releases.groupdocs.com/signature/net/)
### 3. وثيقة للاختبار
قم بإعداد مستند نموذجي (على سبيل المثال، مستند Word أو PDF وما إلى ذلك) الذي ستستخدمه لاختبار وظيفة حذف التوقيع.

## استيراد مساحات الأسماء
لبدء استخدام GroupDocs.Signature لـ .NET في مشروعك، قم باستيراد مساحات الأسماء الضرورية:
```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

الآن، دعنا نقسم عملية حذف التوقيع النصي من المستند إلى خطوات متعددة:
## الخطوة 1: تحديد مسارات الملفات
أولاً، حدد المسارات لمستند الإدخال، ومستند الإخراج، واسم الملف.
```csharp
string filePath = "sample_multiple_signatures.docx";
string fileName = Path.GetFileName(filePath);
string outputFilePath = Path.Combine("Your Document Directory", "DeleteText", fileName);
```
## الخطوة 2: نسخ الملف المصدر
 منذ`Delete` تعمل الطريقة مع نفس المستند، انسخ الملف المصدر إلى موقع جديد.
```csharp
File.Copy(filePath, outputFilePath, true);
```
## الخطوة 3: تهيئة كائن التوقيع
 تهيئة أ`Signature` الكائن باستخدام مسار ملف الإخراج.
```csharp
using (Signature signature = new Signature(outputFilePath))
{
    // سيتم وضع رمز حذف التوقيع النصي هنا
}
```
## الخطوة 4: البحث عن التوقيعات النصية
 ابحث عن التوقيعات النصية داخل المستند باستخدام`TextSearchOptions`.
```csharp
TextSearchOptions options = new TextSearchOptions();
List<TextSignature> signatures = signature.Search<TextSignature>(options);
```
## الخطوة 5: حذف التوقيع النصي
إذا تم العثور على توقيعات نصية، فاحذف التوقيع الأول.
```csharp
if (signatures.Count > 0)
{
    TextSignature textSignature = signatures[0];
    bool result = signature.Delete(textSignature);
    if (result)
    {
        Console.WriteLine($"Signature with Text '{textSignature.Text}' was deleted from document ['{fileName}'].");
    }
    else
    {
        Helper.WriteError($"Signature was not deleted from the document! Signature with Text '{textSignature.Text}' was not found!");
    }
}
```

## خاتمة
في الختام، يقدم GroupDocs.Signature for .NET أسلوبًا مباشرًا لحذف التوقيعات النصية من المستندات برمجيًا. باتباع الخطوات الموضحة في هذا البرنامج التعليمي، يمكن للمطورين دمج وظيفة حذف التوقيع بسلاسة في تطبيقات .NET الخاصة بهم، مما يعزز عمليات إدارة المستندات ويضمن الامتثال لمعايير التوقيع الإلكتروني.
## الأسئلة الشائعة
### هل يمكن لـ GroupDocs.Signature لـ .NET التعامل مع توقيعات متعددة داخل مستند واحد؟
نعم، يدعم GroupDocs.Signature for .NET اكتشاف وحذف التوقيعات المتعددة داخل المستند.
### هل هناك نسخة تجريبية متاحة لأغراض الاختبار؟
 نعم، يمكنك الوصول إلى النسخة التجريبية من الرابط المقدم:[تجربة مجانية](https://releases.groupdocs.com/)
### هل يقدم GroupDocs.Signature for .NET الدعم لتنسيقات المستندات المختلفة؟
نعم، يدعم GroupDocs.Signature for .NET نطاقًا واسعًا من تنسيقات المستندات، بما في ذلك Word وPDF وExcel والمزيد.
### هل يمكنني تخصيص خيارات البحث عند البحث عن التوقيعات؟
بالتأكيد، يوفر GroupDocs.Signature for .NET خيارات بحث متنوعة، مما يسمح للمطورين بتخصيص معايير البحث وفقًا لمتطلباتهم.
### أين يمكنني الحصول على المساعدة إذا واجهت مشاكل أثناء التنفيذ؟
 يمكنك طلب الدعم من منتدى مجتمع GroupDocs:[منتدى الدعم](https://forum.groupdocs.com/c/signature/13)