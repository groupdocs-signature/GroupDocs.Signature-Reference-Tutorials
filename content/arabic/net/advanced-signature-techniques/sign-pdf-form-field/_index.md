---
title: توقيع PDF مع حقل النموذج
linktitle: توقيع PDF مع حقل النموذج
second_title: GroupDocs.Signature .NET API
description: تعرف على كيفية توقيع مستندات PDF مع حقول النموذج باستخدام GroupDocs.Signature لـ .NET. ضمان صحة الوثيقة وسلامتها دون عناء.
type: docs
weight: 10
url: /ar/net/advanced-signature-techniques/sign-pdf-form-field/
---
## مقدمة
توفر التوقيعات الرقمية طريقة آمنة وملزمة قانونًا لتوقيع المستندات إلكترونيًا، مما يضمن صحتها وسلامتها. في هذا البرنامج التعليمي، سوف نتعلم كيفية توقيع مستند PDF يحتوي على حقول النموذج باستخدام GroupDocs.Signature لمكتبة .NET.
## المتطلبات الأساسية
قبل أن نبدأ، تأكد من توفر المتطلبات الأساسية التالية:
1.  GroupDocs.Signature لمكتبة .NET: قم بتنزيل المكتبة وتثبيتها من[هنا](https://releases.groupdocs.com/signature/net/).
2. بيئة التطوير: قم بإعداد بيئة تطوير .NET.
3. مستند PDF: احصل على مستند PDF يحتوي على حقول نموذج جاهزة للتوقيع.

## استيراد مساحات الأسماء
تأكد من استيراد مساحات الأسماء الضرورية إلى مشروعك:
```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## الخطوة 1: قم بتحميل مستند PDF
أولاً، حدد المسار إلى مستند PDF الخاص بك:
```csharp
string filePath = "sample.pdf";
```
## الخطوة 2: تحديد مسار الإخراج
حدد المسار الذي سيتم فيه حفظ المستند الموقع:
```csharp
string outputFilePath = Path.Combine("Your Document Directory", "SignPdfWithFormField", "SignedWithFormField.pdf");
```
## الخطوة 3: تهيئة كائن التوقيع
 إنشاء مثيل لـ`Signature` class وتمرير مسار ملف PDF إليه:
```csharp
using (Signature signature = new Signature(filePath))
{
    // سيتم وضع رمز التوقيع هنا
}
```
## الخطوة 4: إنشاء مثيل لتوقيع حقل النموذج
بعد ذلك، قم بإنشاء توقيع حقل نموذج نصي باسم الحقل المطلوب وقيمته:
```csharp
FormFieldSignature textSignature = new TextFormFieldSignature("FieldText", "Value1");
```
## الخطوة 5: تكوين خيارات التوقيع
قم بإنشاء خيارات للتوقيع بناءً على توقيع حقل النموذج النصي. يمكنك تحديد موضع وحجم التوقيع:
```csharp
FormFieldSignOptions options = new FormFieldSignOptions(textSignature)
{
    Top = 150,
    Left = 50,
    Height = 50,
    Width = 200
};
```
## الخطوة 6: قم بالتوقيع على الوثيقة
قم بتوقيع المستند باستخدام الخيارات المحددة واحفظ المستند الموقع في مسار الإخراج:
```csharp
SignResult result = signature.Sign(outputFilePath, options);
```

## خاتمة
في هذا البرنامج التعليمي، تعلمنا كيفية توقيع مستند PDF يحتوي على حقول النموذج باستخدام GroupDocs.Signature لـ .NET. تعد التوقيعات الرقمية ضرورية لضمان صحة المستندات وسلامتها في مختلف الصناعات.
## الأسئلة الشائعة
### هل يمكنني توقيع مستندات PDF برمجيًا باستخدام GroupDocs.Signature لـ .NET؟
نعم، يمكنك توقيع مستندات PDF برمجيًا باستخدام GroupDocs.Signature لـ .NET كما هو موضح في هذا البرنامج التعليمي.
### هل GroupDocs.Signature for .NET مناسب للتطبيقات على مستوى المؤسسة؟
قطعاً! يتميز GroupDocs.Signature for .NET بالقوة والقابلية للتطوير، مما يجعله مناسبًا للتطبيقات على مستوى المؤسسة.
### هل يدعم GroupDocs.Signature for .NET تنسيقات المستندات الأخرى إلى جانب PDF؟
نعم، يدعم GroupDocs.Signature for .NET نطاقًا واسعًا من تنسيقات المستندات، بما في ذلك Word وExcel وPowerPoint والمزيد.
### هل يمكنني تخصيص مظهر التوقيع؟
نعم، يمكنك تخصيص مظهر التوقيع عن طريق ضبط المعلمات المختلفة مثل اللون والخط والحجم والموضع.
### هل هناك إصدار تجريبي متاح لـ GroupDocs.Signature لـ .NET؟
 نعم، يمكنك تنزيل نسخة تجريبية مجانية من GroupDocs.Signature لـ .NET من[هنا](https://releases.groupdocs.com/).