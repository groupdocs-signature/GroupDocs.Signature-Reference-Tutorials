---
title: حذف التوقيع الرقمي من المستند
linktitle: حذف التوقيع الرقمي من المستند
second_title: GroupDocs.Signature .NET API
description: تعرف على كيفية حذف التوقيعات الرقمية من المستندات باستخدام GroupDocs.Signature لـ .NET. اتبع دليلنا خطوة بخطوة للإدارة الفعالة.
weight: 13
url: /ar/net/delete-operations/delete-digital-signature/
---

# حذف التوقيع الرقمي من المستند

## مقدمة
في عالم المستندات الرقمية، يعد ضمان الأصالة والأمان أمرًا بالغ الأهمية. تلعب التوقيعات الرقمية دورًا حاسمًا في التحقق من سلامة المستندات الإلكترونية. يوفر GroupDocs.Signature for .NET أدوات قوية لإدارة التوقيعات الرقمية داخل تطبيقات .NET بكفاءة.
## المتطلبات الأساسية
قبل الغوص في استخدام GroupDocs.Signature لـ .NET لحذف التوقيعات الرقمية من المستندات، تأكد من أن لديك ما يلي:
1. Visual Studio: قم بتثبيت Visual Studio IDE على نظامك.
2.  GroupDocs.Signature لـ .NET: قم بتنزيل وتثبيت GroupDocs.Signature لـ .NET من[صفحة التحميل](https://releases.groupdocs.com/signature/net/).
3. نموذج المستند: قم بإعداد نموذج مستند يحتوي على التوقيعات الرقمية للاختبار.

## استيراد مساحات الأسماء
للبدء، تأكد من استيراد مساحات الأسماء الضرورية في مشروع .NET الخاص بك:
```csharp
using System;
using System.IO;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
```
## الخطوة 1: تحديد مسارات الملفات
ابدأ بتحديد مسارات الملفات للمستند المصدر والمستند الناتج:
```csharp
string filePath = "sample.pdf"_SIGNED_DIGITAL;
string fileName = Path.GetFileName(filePath);
string outputFilePath = Path.Combine("Your Document Directory", "DeleteDigital", fileName);
```
## الخطوة 2: انسخ المستند المصدر
 منذ`Delete` تعمل الطريقة مع نفس المستند، فمن الضروري نسخ الملف المصدر إلى موقع جديد:
```csharp
File.Copy(filePath, outputFilePath, true);
```
## الخطوة 3: تهيئة كائن التوقيع
 تهيئة أ`Signature` كائن بمسار ملف الإخراج:
```csharp
using (Signature signature = new Signature(outputFilePath))
{
    // الكود الخاص بك يذهب هنا
}
```
## الخطوة 4: البحث عن التوقيعات الرقمية
ابحث عن التوقيعات الرقمية الإلكترونية داخل المستند:
```csharp
List<DigitalSignature> signatures = signature.Search<DigitalSignature>(SignatureType.Digital);
```
## الخطوة 5: حذف التوقيع الرقمي
إذا تم العثور على التوقيعات الرقمية، فاحذف التوقيع الأول الذي تم العثور عليه:
```csharp
if (signatures.Count > 0)
{
    DigitalSignature digitalSignature = signatures[0];
    bool result = signature.Delete(digitalSignature);
    if (result)
    {
        Console.WriteLine($"Digital signature #{digitalSignature.Thumbprint} from {digitalSignature.SignTime.ToShortDateString()} was deleted from document ['{fileName}'].");
    }
    else
    {
        Helper.WriteError($"Signature was not deleted from the document! Signature# {digitalSignature.Thumbprint} was not found!");
    }
}
```

## خاتمة
أصبحت إدارة التوقيعات الرقمية في تطبيقات .NET أمرًا سهلاً مع GroupDocs.Signature. باتباع الخطوات البسيطة الموضحة أعلاه، يمكنك حذف التوقيعات الرقمية من مستنداتك بسلاسة، مما يضمن سلامة البيانات وأمنها.
## الأسئلة الشائعة
### هل يمكنني حذف عدة توقيعات رقمية من مستند واحد؟
نعم، يمكنك تعديل الكود لتكرار جميع التوقيعات الرقمية التي تم العثور عليها وحذفها وفقًا لذلك.
### هل يدعم GroupDocs.Signature أنواعًا أخرى من التوقيعات إلى جانب التوقيع الرقمي؟
نعم، يدعم GroupDocs.Signature أنواعًا مختلفة من التوقيعات، بما في ذلك التوقيعات الإلكترونية والرقمية والمكتوبة بخط اليد.
### هل GroupDocs.Signature مناسب لإدارة المستندات على مستوى المؤسسة؟
بالتأكيد، تم تصميم GroupDocs.Signature لتلبية احتياجات كل من المطورين الأفراد والتطبيقات على مستوى المؤسسات، مما يوفر ميزات قوية وقابلية للتوسع.
### هل يمكنني تخصيص عملية الحذف للتوقيعات الرقمية؟
نعم، يوفر GroupDocs.Signature نطاقًا واسعًا من الخيارات والإعدادات لتخصيص عملية حذف التوقيع وفقًا لمتطلباتك المحددة.
### هل هناك إصدار تجريبي متاح لاختبار GroupDocs.Signature؟
 نعم، يمكنك تنزيل نسخة تجريبية مجانية من[صفحة الإصدارات](https://releases.groupdocs.com/).