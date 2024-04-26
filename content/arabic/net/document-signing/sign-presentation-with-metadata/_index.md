---
title: قم بالتوقيع على العرض التقديمي باستخدام البيانات الوصفية
linktitle: قم بالتوقيع على العرض التقديمي باستخدام البيانات الوصفية
second_title: GroupDocs.Signature .NET API
description: تعرف على كيفية توقيع ملفات العرض التقديمي باستخدام بيانات التعريف باستخدام GroupDocs.Signature لـ .NET. تعزيز سلامة الوثيقة وإضافة معلومات قيمة.
type: docs
weight: 12
url: /ar/net/document-signing/sign-presentation-with-metadata/
---
## مقدمة
في هذا البرنامج التعليمي، سوف نتعلم كيفية توقيع ملف العرض التقديمي (PPTX) مع بيانات التعريف باستخدام GroupDocs.Signature لمكتبة .NET. يؤدي توقيع العروض التقديمية باستخدام بيانات التعريف إلى إضافة معلومات قيمة إلى المستند، مثل اسم المؤلف وتاريخ الإنشاء ومعرف المستند ومعرف التوقيع وقيم رقمية متنوعة.
## المتطلبات الأساسية
قبل أن نبدأ، تأكد من أن لديك ما يلي:
1.  GroupDocs.Signature لمكتبة .NET: قم بتنزيل المكتبة وتثبيتها من[هنا](https://releases.groupdocs.com/signature/net/).
2. بيئة التطوير: تأكد من إعداد بيئة تطوير .NET.
3. ملف العرض التقديمي: احصل على نموذج ملف عرض تقديمي (تنسيق PPTX) جاهز للتوقيع.
4. الفهم الأساسي لـ C#: الإلمام بلغة البرمجة C# سيكون مفيدًا.

## استيراد مساحات الأسماء
قبل الغوص في الكود، فلنستورد مساحات الأسماء الضرورية:
```csharp
using System;
using System.IO;
    using GroupDocs.Signature;
    using GroupDocs.Signature.Domain;
    using GroupDocs.Signature.Options;
```
## الخطوة 1: تحميل ملف العرض التقديمي
```csharp
string filePath = "sample.pptx";
```
 يستبدل`"sample.pptx"` مع المسار إلى ملف العرض التقديمي الخاص بك.
## الخطوة 2: تحديد مسار ملف الإخراج
```csharp
string outputFilePath = Path.Combine("Your Document Directory", "SignPresentationWithMetadata", "SignedWithMetadata.pptx");
```
حدد الدليل الذي تريد حفظ ملف العرض التقديمي الموقع به مع اسم الملف.
## الخطوة 3: تهيئة كائن التوقيع
```csharp
using (Signature signature = new Signature(filePath))
```
قم بتهيئة كائن التوقيع من خلال توفير المسار إلى ملف العرض التقديمي.
## الخطوة 4: تحديد خيارات تسجيل البيانات التعريفية
```csharp
MetadataSignOptions options = new MetadataSignOptions();
```
قم بإنشاء مثيل لـ MetadataSignOptions لتحديد خيارات توقيع البيانات التعريفية.
## الخطوة 5: إنشاء تواقيع البيانات التعريفية
```csharp
PresentationMetadataSignature[] signatures = new PresentationMetadataSignature[]
{
    new PresentationMetadataSignature("Author", "Mr.Scherlock Holmes"),
    new PresentationMetadataSignature("CreatedOn", DateTime.Now),
    new PresentationMetadataSignature("DocumentId", 123456),
    new PresentationMetadataSignature("SignatureId", 123.456D),
    new PresentationMetadataSignature("Amount", 123.456M),
    new PresentationMetadataSignature("Total", 123.456F)
};
```
قم بإنشاء مصفوفة من كائنات PresentationMetadataSignature، يمثل كل منها توقيع بيانات التعريف. يمكنك إضافة أنواع مختلفة من البيانات التعريفية، بما في ذلك السلسلة والتاريخ والوقت والعدد الصحيح والمزدوج والعشري والعائم.
## الخطوة 6: إضافة التوقيعات إلى الخيارات
```csharp
options.Signatures.AddRange(signatures);
```
أضف توقيعات بيانات التعريف التي تم إنشاؤها إلى كائن MetadataSignOptions.
## الخطوة 7: قم بتوقيع الوثيقة
```csharp
SignResult result = signature.Sign(outputFilePath, options);
```
قم بتوقيع ملف العرض التقديمي باستخدام البيانات التعريفية باستخدام الخيارات المحددة واحفظ الملف الموقع في مسار الإخراج.
## الخطوة 8: عرض النتيجة
```csharp
Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).\nFile saved at {outputFilePath}.");
```
اعرض رسالة نجاح مع عدد التوقيعات المطبقة والمسار الذي تم حفظ الملف الموقع به.

## خاتمة
في هذا البرنامج التعليمي، تعلمنا كيفية توقيع ملف العرض التقديمي باستخدام بيانات التعريف باستخدام GroupDocs.Signature لمكتبة .NET. تعمل إضافة توقيعات البيانات التعريفية على تحسين سلامة المستند وتوفير معلومات قيمة حول محتواه.

## الأسئلة الشائعة
### هل يمكنني التوقيع على تنسيقات مستندات أخرى إلى جانب PPTX باستخدام بيانات التعريف باستخدام GroupDocs.Signature لـ .NET؟
نعم، يدعم GroupDocs.Signature تنسيقات المستندات المختلفة، بما في ذلك Word وExcel وPDF والمزيد، للتوقيع باستخدام بيانات التعريف.
### هل GroupDocs.Signature لـ .NET متوافق مع .NET Core؟
نعم، المكتبة متوافقة مع كل من .NET Framework و .NET Core.
### هل يمكنني تخصيص مظهر توقيعات البيانات التعريفية؟
نعم، يمكنك تخصيص المظهر والموضع والخصائص الأخرى لتوقيعات بيانات التعريف وفقًا لمتطلباتك.
### هل يوفر GroupDocs.Signature for .NET تشفيرًا للمستندات الموقعة؟
نعم، يوفر GroupDocs.Signature خيارات تشفير لتأمين المستندات الموقعة من الوصول غير المصرح به.
### هل هناك نسخة تجريبية متاحة للاختبار قبل الشراء؟
 نعم، يمكنك الاستفادة من النسخة التجريبية المجانية من GroupDocs.Signature لـ .NET من[هنا](https://releases.groupdocs.com/).