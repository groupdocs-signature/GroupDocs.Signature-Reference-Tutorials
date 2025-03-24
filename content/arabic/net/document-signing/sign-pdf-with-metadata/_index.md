---
title: قم بتوقيع ملف PDF باستخدام البيانات الوصفية
linktitle: قم بتوقيع ملف PDF باستخدام البيانات الوصفية
second_title: GroupDocs.Signature .NET API
description: تعرف على كيفية توقيع مستندات PDF باستخدام بيانات التعريف باستخدام GroupDocs.Signature لـ .NET. تعزيز إمكانية تتبع المستندات وأصالتها بسهولة.
weight: 11
url: /ar/net/document-signing/sign-pdf-with-metadata/
---

# قم بتوقيع ملف PDF باستخدام البيانات الوصفية

## مقدمة
في هذا البرنامج التعليمي، سنتعلم كيفية توقيع مستند PDF يحتوي على بيانات التعريف باستخدام GroupDocs.Signature for .NET. يمكن أن تؤدي إضافة البيانات الأولية إلى ملف PDF إلى توفير معلومات إضافية حول المستند، مثل التأليف وتاريخ الإنشاء ومعرف المستند والمزيد.
## المتطلبات الأساسية
قبل أن نبدأ، تأكد من أن لديك ما يلي:
1.  GroupDocs.Signature لـ .NET: يمكنك تنزيله من[هنا](https://releases.groupdocs.com/signature/net/).
2. مستند PDF: احصل على نموذج ملف PDF جاهز للتوقيع.
3. المعرفة الأساسية ببرمجة C#: الإلمام بتركيب جملة C# مطلوب لفهم أمثلة التعليمات البرمجية.
## استيراد مساحات الأسماء
أولاً، تأكد من استيراد مساحات الأسماء الضرورية للوصول إلى الفئات والتوابع المطلوبة:
```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## الخطوة 1: قم بتحميل مستند PDF
قم بتحميل مستند PDF الذي تريد التوقيع عليه:
```csharp
string filePath = "sample.pdf";
```
## الخطوة 2: تحديد مسار ملف الإخراج
حدد مسار ملف الإخراج حيث سيتم حفظ ملف PDF الموقع مع البيانات التعريفية:
```csharp
string outputFilePath = Path.Combine("Your Document Directory", "SignPdfWithMetadata", "SignedWithMetadata.pdf");
```
## الخطوة 3: إنشاء مثيل التوقيع
قم بتهيئة مثيل التوقيع من خلال توفير المسار إلى مستند PDF:
```csharp
using (Signature signature = new Signature(filePath))
{
    // سيتم وضع الرمز المتعلق بالتوقيع هنا
}
```
## الخطوة 4: تحديد خيارات البيانات التعريفية
قم بإنشاء MetadataSignOptions وأضف حقول البيانات التعريفية بالقيم الخاصة بها:
```csharp
MetadataSignOptions options = new MetadataSignOptions();
options
    .Add(new PdfMetadataSignature("Author", "Mr.Sherlock Holmes")) // قيمة السلسلة
    .Add(new PdfMetadataSignature("CreatedOn", DateTime.Now))       // قيم التاريخ والوقت
    .Add(new PdfMetadataSignature("DocumentId", 123456))            // قيمة عدد صحيح
    .Add(new PdfMetadataSignature("SignatureId", 123.456D))         // قيمة مزدوجة
    .Add(new PdfMetadataSignature("Amount", 123.456M))              // القيمة العشرية
    .Add(new PdfMetadataSignature("Total", 123.456F));              // تعويم القيمة
```
## الخطوة 5: قم بالتوقيع على الوثيقة
قم بتوقيع مستند PDF باستخدام خيارات البيانات التعريفية المحددة واحفظ المستند الموقع:
```csharp
SignResult result = signature.Sign(outputFilePath, options);
Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).\nFile saved at {outputFilePath}.");
```

## خاتمة
في هذا البرنامج التعليمي، تناولنا كيفية توقيع مستند PDF يحتوي على بيانات التعريف باستخدام GroupDocs.Signature لـ .NET. باتباع الدليل الموضح خطوة بخطوة، يمكنك بسهولة إضافة معلومات البيانات التعريفية مثل التأليف وتاريخ الإنشاء والمزيد إلى ملفات PDF الخاصة بك، مما يعزز فائدتها وإمكانية تتبعها.
## الأسئلة الشائعة
### هل يمكنني إضافة حقول بيانات تعريف مخصصة إلى مستندات PDF الخاصة بي؟
نعم، يمكنك إضافة حقول بيانات التعريف المخصصة عن طريق تحديد اسم الحقل والقيمة المقابلة له باستخدام GroupDocs.Signature لـ .NET.
### هل يتوافق GroupDocs.Signature for .NET مع كافة إصدارات .NET Framework؟
يتوافق GroupDocs.Signature for .NET مع إصدارات مختلفة من .NET Framework، مما يضمن المرونة وسهولة التكامل.
### هل يدعم GroupDocs.Signature توقيع تنسيقات المستندات الأخرى بخلاف PDF؟
نعم، يدعم GroupDocs.Signature نطاقًا واسعًا من تنسيقات المستندات، بما في ذلك Word وExcel وPowerPoint والمزيد.
### هل يمكنني توقيع مستندات متعددة بشكل مجمّع باستخدام GroupDocs.Signature لـ .NET؟
نعم، يمكنك توقيع مستندات متعددة بشكل مجمّع من خلال تكرار قائمة الملفات وتطبيق عملية التوقيع برمجيًا.
### هل يتوفر الدعم الفني لمستخدمي GroupDocs.Signature؟
 نعم، توفر GroupDocs دعمًا فنيًا مخصصًا من خلال منتدياتها. يمكنك الوصول إلى منتدى الدعم[هنا](https://forum.groupdocs.com/c/signature/13).