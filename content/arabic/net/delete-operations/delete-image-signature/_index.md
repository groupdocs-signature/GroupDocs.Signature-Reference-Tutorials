---
title: حذف توقيع الصورة
linktitle: حذف توقيع الصورة
second_title: GroupDocs.Signature .NET API
description: تعرف على كيفية حذف توقيعات الصور من المستندات باستخدام GroupDocs.Signature لـ .NET. اتبع دليلنا خطوة بخطوة لإدارة التوقيع بكفاءة.
type: docs
weight: 14
url: /ar/net/delete-operations/delete-image-signature/
---
## مقدمة
في هذا البرنامج التعليمي، سوف نستكشف كيفية حذف توقيعات الصور من المستندات باستخدام GroupDocs.Signature لـ .NET. GroupDocs.Signature هي مكتبة قوية تتيح للمطورين العمل مع التوقيعات الرقمية والطوابع وحقول النماذج ضمن تنسيقات المستندات المختلفة.
## المتطلبات الأساسية
قبل أن نبدأ، تأكد من أن لديك ما يلي:
### 1. GroupDocs.Signature لـ .NET
 قم بتنزيل وتثبيت GroupDocs.Signature لـ .NET من[موقع إلكتروني](https://releases.groupdocs.com/signature/net/). اتبع تعليمات التثبيت المتوفرة في الوثائق.
### 2. صافي الإطار
تأكد من تثبيت .NET Framework على جهازك.
## استيراد مساحات الأسماء
قم بتضمين مساحات الأسماء الضرورية في مشروعك:
```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
دعنا نقسم عملية حذف توقيعات الصور إلى خطوات متعددة:
## الخطوة 1: تحديد مسارات الملفات
أولاً، قم بتحديد مسارات مستند الإدخال ومستند الإخراج بعد حذف التوقيع:
```csharp
string filePath = "sample_multiple_signatures.docx";
string fileName = Path.GetFileName(filePath);
string outputFilePath = Path.Combine("Your Document Directory", "DeleteImage", fileName);
```
## الخطوة 2: انسخ الملف المصدر
 منذ`Delete`تعمل الطريقة مع نفس المستند، فمن الضروري نسخ الملف المصدر إلى موقع آخر:
```csharp
File.Copy(filePath, outputFilePath, true);
```
## الخطوة 3: تهيئة كائن التوقيع
 إنشاء مثيل لـ`Signature` فئة وحدد المسار إلى مستند الإخراج:
```csharp
using (Signature signature = new Signature(outputFilePath))
{
    // الكود يذهب هنا
}
```
## الخطوة 4: البحث عن توقيعات الصور
حدد خيارات البحث وابحث عن توقيعات الصور داخل المستند:
```csharp
ImageSearchOptions options = new ImageSearchOptions();
List<ImageSignature> signatures = signature.Search<ImageSignature>(options);
```
## الخطوة 5: حذف توقيع الصورة
إذا تم العثور على توقيعات الصورة، فاحذف التوقيع الأول:
```csharp
if (signatures.Count > 0)
{
    ImageSignature imageSignature = signatures[0];
    bool result = signature.Delete(imageSignature);
    if (result)
    {
        Console.WriteLine($"Image signature at location {imageSignature.Left}x{imageSignature.Top} and Size {imageSignature.Size} was deleted from document ['{fileName}'].");
    }
    else
    {
        Helper.WriteError($"Signature was not deleted from the document! Signature at location {imageSignature.Left}x{imageSignature.Top} and Size {imageSignature.Size} was not found!");
    }
}
```
## خاتمة
في هذا البرنامج التعليمي، تعلمنا كيفية حذف توقيعات الصور من المستندات باستخدام GroupDocs.Signature لـ .NET. ومن خلال اتباع الدليل الموضح خطوة بخطوة، يمكن للمطورين إدارة التوقيعات الرقمية بكفاءة داخل تطبيقاتهم.
## الأسئلة الشائعة
### هل يمكنني حذف توقيعات صور متعددة من مستند؟
 نعم، يمكنك تعديل الكود لحذف توقيعات صور متعددة عن طريق التكرار فوق ملف`signatures` قائمة.
### هل يدعم GroupDocs.Signature تنسيقات المستندات الأخرى إلى جانب DOCX؟
نعم، يدعم GroupDocs.Signature نطاقًا واسعًا من تنسيقات المستندات، بما في ذلك PDF وPPT وXLS والمزيد.
### هل هناك إصدار تجريبي متاح لـ GroupDocs.Signature لـ .NET؟
 نعم، يمكنك تنزيل نسخة تجريبية مجانية من[موقع إلكتروني](https://releases.groupdocs.com/).
### كيف يمكنني الحصول على الدعم لـ GroupDocs.Signature؟
 يمكنك زيارة[منتدى GroupDocs.Signature](https://forum.groupdocs.com/c/signature/13) للحصول على المساعدة والدعم.
### هل يمكنني شراء ترخيص مؤقت لـ GroupDocs.Signature؟
 نعم، يمكنك شراء ترخيص مؤقت من[صفحة الشراء](https://purchase.groupdocs.com/temporary-license/).