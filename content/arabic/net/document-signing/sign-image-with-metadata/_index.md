---
title: توقيع الصورة مع البيانات الوصفية
linktitle: توقيع الصورة مع البيانات الوصفية
second_title: GroupDocs.Signature .NET API
description: تعرف على كيفية توقيع الصور باستخدام بيانات التعريف في .NET باستخدام GroupDocs.Signature. حل توقيع البيانات الوصفية سهل وفعال وقابل للتخصيص.
type: docs
weight: 10
url: /ar/net/document-signing/sign-image-with-metadata/
---
## مقدمة
يمكّن GroupDocs.Signature for .NET المطورين من توقيع الصور باستخدام بيانات التعريف بكفاءة. يرشدك هذا البرنامج التعليمي خلال العملية خطوة بخطوة.
## المتطلبات الأساسية
قبل أن تبدأ، تأكد من أن لديك ما يلي:
1. GroupDocs.Signature لـ .NET: قم بتثبيت حزمة GroupDocs.Signature في مشروع .NET الخاص بك. يمكنك تنزيله من[هنا](https://releases.groupdocs.com/signature/net/).   
2. ملف الصورة: قم بإعداد ملف الصورة الذي تريد توقيعه باستخدام البيانات التعريفية.

## استيراد مساحات الأسماء
تأكد من استيراد مساحات الأسماء الضرورية في كود C# الخاص بك:
```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## الخطوة 1: تحميل ملف الصورة
أولاً، حدد المسار إلى ملف الصورة الخاص بك ودليل الإخراج للصورة الموقعة مع البيانات الوصفية:
```csharp
string filePath = "sample.png";            
string outputFilePath = Path.Combine("Your Document Directory", "SignImageWithMetadata", "SignedWithMetadata.png");
```
## الخطوة 2: إنشاء تواقيع البيانات التعريفية
بعد ذلك، قم بإنشاء توقيعات بيانات تعريف مختلفة وأضفها إلى مجموعة توقيع الخيارات:
```csharp
using (Signature signature = new Signature(filePath))
{
    ushort imgsMetadataId = 41996;
    MetadataSignOptions options = new MetadataSignOptions();
    options
        .Add(new ImageMetadataSignature(imgsMetadataId++, "Mr.Scherlock Holmes")) // قيمة السلسلة
        .Add(new ImageMetadataSignature(imgsMetadataId++, DateTime.Now))          // قيمة التاريخ والوقت
        .Add(new ImageMetadataSignature(imgsMetadataId++, 123456))                // قيمة عدد صحيح
        .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456D))              // قيمة مزدوجة
        .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456M))              // القيمة العشرية
        .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456F));             // تعويم القيمة
    
    // التوقيع على وثيقة للملف
    SignResult result = signature.Sign(outputFilePath, options);
    Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).\nFile saved at {outputFilePath}.");
}
```

## خاتمة
في هذا البرنامج التعليمي، تعلمت كيفية توقيع صورة باستخدام بيانات التعريف باستخدام GroupDocs.Signature لـ .NET. باتباع هذه الخطوات، يمكنك بسهولة دمج توقيعات بيانات التعريف في تطبيقات .NET الخاصة بك.

## الأسئلة الشائعة
### هل يمكنني توقيع صور متعددة باستخدام بيانات التعريف باستخدام GroupDocs.Signature لـ .NET؟
نعم، يمكنك توقيع صور متعددة باستخدام البيانات التعريفية من خلال التكرار خلال كل ملف صورة وتطبيق توقيعات البيانات التعريفية.
### هل هناك إصدار تجريبي متاح لـ GroupDocs.Signature لـ .NET؟
 نعم يمكنك تحميل النسخة التجريبية من[هنا](https://releases.groupdocs.com/).
### هل يدعم GroupDocs.Signature for .NET تنسيقات الملفات الأخرى إلى جانب الصور؟
نعم، يدعم GroupDocs.Signature تنسيقات ملفات متنوعة، بما في ذلك PDF وWord وExcel والمزيد.
### هل يمكنني تخصيص مظهر توقيع البيانات التعريفية؟
نعم، يمكنك تخصيص مظهر توقيع البيانات التعريفية، مثل حجم الخط واللون والموضع.
### أين يمكنني الحصول على دعم GroupDocs.Signature لـ .NET؟
 يمكنك الحصول على الدعم من منتدى GroupDocs.Signature[هنا](https://forum.groupdocs.com/c/signature/13).