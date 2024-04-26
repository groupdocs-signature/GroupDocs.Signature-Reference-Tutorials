---
title: البحث عن التوقيعات المتعددة
linktitle: البحث عن التوقيعات المتعددة
second_title: GroupDocs.Signature .NET API
description: تعرف على كيفية البحث عن توقيعات متعددة في مستندات .NET باستخدام GroupDocs.Signature لضمان أمان المستندات وسلامتها بشكل فعال.
type: docs
weight: 14
url: /ar/net/signature-searching/search-for-multiple-signatures/
---
## مقدمة
تعد GroupDocs.Signature for .NET مكتبة قوية تمكن المطورين من إضافة أنواع مختلفة من التوقيعات والبحث فيها وإزالتها بتنسيقات المستندات الشائعة باستخدام تطبيقات .NET. في هذا البرنامج التعليمي، سنركز على البحث عن توقيعات متعددة داخل مستند باستخدام GroupDocs.Signature لـ .NET.
## المتطلبات الأساسية
قبل أن نبدأ، تأكد من توفر المتطلبات الأساسية التالية:
- تم تثبيت Visual Studio على نظامك.
- الفهم الأساسي للغة البرمجة C#.
- GroupDocs.Signature لمكتبة .NET المثبتة في مشروعك. يمكنك تنزيله من[هنا](https://releases.groupdocs.com/signature/net/).

## استيراد مساحات الأسماء
أولاً، تحتاج إلى استيراد مساحات الأسماء الضرورية للوصول إلى الفئات والأساليب التي يوفرها GroupDocs.Signature لـ .NET.
```csharp
using System;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## الخطوة 1: قم بتحميل المستند
قم بتحميل المستند حيث تريد البحث عن توقيعات متعددة. تأكد من توفير مسار الملف الصحيح.
```csharp
string filePath = "sample_multiple_signatures.docx";
using (Signature signature = new Signature(filePath))
{
    // الكود الخاص بك يذهب هنا
}
```
## الخطوة 2: تحديد خيارات البحث
تحديد خيارات البحث لأنواع مختلفة من التوقيعات مثل التوقيعات النصية والرقمية والباركود ورمز الاستجابة السريعة والبيانات التعريفية. يمكنك تحديد معايير البحث مثل النص المراد مطابقته، ونوع المطابقة، والبحث عبر جميع الصفحات.
```csharp
// تحديد خيارات البحث
TextSearchOptions textOptions = new TextSearchOptions()
{
    AllPages = true
};
DigitalSearchOptions digitalOptions = new DigitalSearchOptions()
{
    AllPages = true
};
BarcodeSearchOptions barcodeOptions = new BarcodeSearchOptions()
{
    AllPages = true,
    Text = "123456",
    MatchType = TextMatchType.Exact
};
QrCodeSearchOptions qrCodeOptions = new QrCodeSearchOptions()
{
    AllPages = true,
    Text = "John",
    MatchType = TextMatchType.Contains
};
MetadataSearchOptions metadataOptions = new MetadataSearchOptions();
```
## الخطوة 3: إضافة خيارات البحث إلى القائمة
أضف خيارات البحث المحددة إلى القائمة.
```csharp
// إضافة خيارات إلى القائمة
List<SearchOptions> listOptions = new List<SearchOptions>();
listOptions.Add(textOptions);
listOptions.Add(barcodeOptions);
listOptions.Add(qrCodeOptions);
listOptions.Add(metadataOptions);
listOptions.Add(digitalOptions);
```
## الخطوة 4: البحث عن التوقيعات
ابحث عن التوقيعات في المستند باستخدام خيارات البحث المحددة.
```csharp
// البحث عن التوقيعات في الوثيقة
SearchResult result = signature.Search(listOptions);
if (result.Signatures.Count > 0)
{
    Console.WriteLine($"\nSource document ['{filePath}'] contains following signatures.");
    foreach (var resSignature in result.Signatures)
    {
        Console.WriteLine($"Signature found at page {resSignature.PageNumber} with type {resSignature.SignatureType} and Id#: {resSignature.SignatureId}");
    }
}
else
{
    Helper.WriteError("No one signature was found.");
}
```

## خاتمة
في هذا البرنامج التعليمي، تعلمنا كيفية البحث عن توقيعات متعددة داخل مستند باستخدام GroupDocs.Signature لـ .NET. باتباع الخطوات المقدمة، يمكنك تحديد أنواع مختلفة من التوقيعات في مستنداتك بكفاءة، مما يعزز أمان المستندات وسلامتها.
## الأسئلة الشائعة
### هل يمكنني البحث عن التوقيعات بتنسيقات مستندات مختلفة؟
نعم، يدعم GroupDocs.Signature for .NET نطاقًا واسعًا من تنسيقات المستندات بما في ذلك Word وPDF وExcel والمزيد.
### هل من الممكن تخصيص معايير البحث للتوقيعات؟
بالتأكيد، يمكنك تخصيص معايير البحث وفقًا لمتطلباتك، مثل تحديد التطابقات الدقيقة للنص أو البحث عبر جميع الصفحات.
### هل يقدم GroupDocs.Signature for .NET دعمًا للتوقيعات الرقمية؟
نعم، يمكنك البحث عن التوقيعات الرقمية بالإضافة إلى أنواع أخرى مثل التوقيعات النصية والباركود ورمز الاستجابة السريعة.
### هل يمكنني دمج وظيفة البحث عن التوقيع في تطبيقات .NET الخاصة بي بسهولة؟
نعم، يوفر GroupDocs.Signature for .NET واجهة برمجة تطبيقات مباشرة تعمل على تبسيط عملية التكامل.
### أين يمكنني العثور على دعم أو مساعدة إضافية؟
 يمكنك زيارة منتدى GroupDocs.Signature[هنا](https://forum.groupdocs.com/c/signature/13) لأية استفسارات أو مساعدة.