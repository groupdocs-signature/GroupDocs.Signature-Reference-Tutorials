---
title: حذف الباركود من المستند
linktitle: حذف الباركود من المستند
second_title: GroupDocs.Signature .NET API
description: تعرف على كيفية حذف الرمز الشريطي من مستند باستخدام GroupDocs.Signature لـ .NET. دليل خطوة بخطوة مع أمثلة التعليمات البرمجية.
type: docs
weight: 10
url: /ar/net/delete-operations/delete-barcode/
---
## مقدمة
تعد GroupDocs.Signature for .NET مكتبة قوية تمكن المطورين من العمل بسلاسة مع التوقيعات الرقمية والطوابع والرموز الشريطية داخل تطبيقات .NET. في هذا البرنامج التعليمي، سنرشدك خلال عملية حذف الرمز الشريطي من مستند باستخدام GroupDocs.Signature لـ .NET.
## المتطلبات الأساسية
قبل أن نبدأ، تأكد من توفر المتطلبات الأساسية التالية:
- المعرفة الأساسية بلغة البرمجة C#.
- تم تثبيت Visual Studio على نظامك.
-  تم تثبيت GroupDocs.Signature لمكتبة .NET. يمكنك تنزيله من[هنا](https://releases.groupdocs.com/signature/net/).
- نموذج مستند يحتوي على رمز شريطي تريد حذفه.

## استيراد مساحات الأسماء
أولاً، تأكد من استيراد مساحات الأسماء الضرورية إلى كود C# الخاص بك:
```csharp
using System;
using System.IO;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

دعنا نقسم عملية حذف الباركود من المستند إلى خطوات بسيطة:
## الخطوة 1: تحديد مسارات الملفات
```csharp
string filePath = "sample_multiple_signatures.docx";
string fileName = Path.GetFileName(filePath);
string outputFilePath = Path.Combine("Your Document Directory", "DeleteBarcode", fileName);
```
 تأكد من الاستبدال`"sample_multiple_signatures.docx"` مع المسار إلى المستند الخاص بك الذي يحتوي على الرمز الشريطي.
## الخطوة 2: انسخ الملف المصدر
```csharp
File.Copy(filePath, outputFilePath, true);
```
تضمن هذه الخطوة أننا نعمل على نسخة من المستند الأصلي للحفاظ على الملف الأصلي.
## الخطوة 3: تهيئة GroupDocs.Signature
```csharp
using (Signature signature = new Signature(outputFilePath))
{
    // الكود الخاص بك يذهب هنا
}
```
قم بتهيئة كائن التوقيع عن طريق تمرير المسار إلى نسخة المستند التي تم إنشاؤها في الخطوة السابقة.
## الخطوة 4: البحث عن توقيعات الباركود
```csharp
BarcodeSearchOptions options = new BarcodeSearchOptions();
List<BarcodeSignature> signatures = signature.Search<BarcodeSignature>(options);
```
قم بإنشاء مثيل BarcodeSearchOptions واستخدمه للبحث عن توقيعات الرمز الشريطي داخل المستند.
## الخطوة 5: حذف توقيع الباركود
```csharp
if (signatures.Count > 0)
{
    BarcodeSignature barcodeSignature = signatures[0];
    bool result = signature.Delete(barcodeSignature);
    if (result)
    {
        Console.WriteLine($"Signature with Barcode '{barcodeSignature.Text}' and encode type '{barcodeSignature.EncodeType.TypeName}' was deleted from document ['{fileName}'].");
    }
    else
    {
        Helper.WriteError($"Signature was not deleted from the document! Signature with Barcode '{barcodeSignature.Text}' and encode type '{barcodeSignature.EncodeType.TypeName}' was not found!");
    }
}
```
تحقق من العثور على توقيعات الباركود في المستند. إذا وجد، قم بحذف توقيع الباركود الأول الذي تم العثور عليه.

## خاتمة
في هذا البرنامج التعليمي، تعلمنا كيفية حذف الرمز الشريطي من مستند باستخدام GroupDocs.Signature لـ .NET. باتباع الدليل الموضح خطوة بخطوة، يمكنك دمج وظيفة حذف الرمز الشريطي بسلاسة في تطبيقات .NET الخاصة بك.
## الأسئلة الشائعة
### هل يمكنني حذف توقيعات باركود متعددة من مستند؟
نعم، يمكنك تعديل الرمز لحذف توقيعات باركود متعددة من خلال التكرار على قائمة التوقيعات.
### هل يدعم GroupDocs.Signature for .NET أنواعًا أخرى من التوقيعات؟
نعم، يدعم GroupDocs.Signature for .NET أنواعًا مختلفة من التوقيعات، بما في ذلك التوقيعات الرقمية والطوابع والتوقيعات النصية.
### هل يمكنني تخصيص خيارات البحث لتوقيعات الباركود؟
نعم، يمكنك تخصيص خيارات البحث حسب متطلباتك، مثل تحديد أنواع الباركود أو مناطق البحث داخل الوثيقة.
### هل يتوافق GroupDocs.Signature for .NET مع تنسيقات المستندات المختلفة؟
نعم، يدعم GroupDocs.Signature for .NET نطاقًا واسعًا من تنسيقات المستندات، بما في ذلك Word وExcel وPDF والمزيد.
### أين يمكنني العثور على دعم أو موارد إضافية لـ GroupDocs.Signature لـ .NET؟
 يمكنك زيارة منتدى GroupDocs.Signature[هنا](https://forum.groupdocs.com/c/signature/13) لأية استفسارات أو مساعدة بخصوص المكتبة.