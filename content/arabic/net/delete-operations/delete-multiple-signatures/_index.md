---
title: حذف التوقيعات المتعددة من المستند
linktitle: حذف التوقيعات المتعددة من المستند
second_title: GroupDocs.Signature .NET API
description: قم بحذف التوقيعات المتعددة من المستندات بسهولة باستخدام GroupDocs.Signature لـ .NET. تبسيط سير عمل إدارة المستندات الخاصة بك.
weight: 15
url: /ar/net/delete-operations/delete-multiple-signatures/
---

# حذف التوقيعات المتعددة من المستند

## مقدمة
في العالم الرقمي، غالبًا ما تتضمن إدارة المستندات التعامل مع التوقيعات المختلفة. يمكن أن يؤدي حذف التوقيعات المتعددة من المستند برمجياً إلى تبسيط سير العمل وتعزيز الكفاءة. باستخدام GroupDocs.Signature for .NET، تصبح هذه المهمة سلسة ومباشرة. سيرشدك هذا البرنامج التعليمي خلال عملية حذف التوقيعات المتعددة من المستند خطوة بخطوة.
## المتطلبات الأساسية
قبل الغوص في البرنامج التعليمي، تأكد من أن لديك المتطلبات الأساسية التالية:
- الفهم الأساسي للغة البرمجة C#.
- تم تثبيت GroupDocs.Signature لمكتبة .NET.
- نموذج مستند يحتوي على توقيعات متعددة للاختبار.

## استيراد مساحات الأسماء
ابدأ باستيراد مساحات الأسماء الضرورية للوصول إلى وظائف GroupDocs.Signature لـ .NET:
```csharp
using System;
using System.IO;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## الخطوة 1: تحديد مسار المستند واسم الملف
قم بتعيين مسار ملف المستند الذي يحتوي على توقيعات متعددة. تأكد من أن لديك مسار الملف واسم الملف المناسبين:
```csharp
string filePath = "sample_multiple_signatures.docx";
string fileName = Path.GetFileName(filePath);
```
## الخطوة 2: انسخ المستند للمعالجة
لتجنب تعديل المستند الأصلي، قم بإنشاء نسخة للمعالجة:
```csharp
string outputFilePath = Path.Combine("Your Document Directory", "DeleteMultiple", fileName);
File.Copy(filePath, outputFilePath, true);
```
## الخطوة 3: تهيئة كائن التوقيع
إنشاء مثيل لكائن التوقيع باستخدام مسار ملف الإخراج:
```csharp
using (Signature signature = new Signature(outputFilePath))
{
    // رمز معالجة التوقيع يظهر هنا
}
```
## الخطوة 4: تحديد خيارات البحث
حدد خيارات بحث متنوعة لتحديد التوقيعات داخل المستند. تتضمن الخيارات البحث عن النص والبحث عن الصور والبحث عن الرمز الشريطي والبحث عن رمز الاستجابة السريعة:
```csharp
TextSearchOptions textSearchOptions = new TextSearchOptions();
ImageSearchOptions imageSearchOptions = new ImageSearchOptions();
BarcodeSearchOptions barcodeOptions = new BarcodeSearchOptions();
QrCodeSearchOptions qrCodeOptions = new QrCodeSearchOptions();
// إضافة خيارات إلى القائمة
List<SearchOptions> listOptions = new List<SearchOptions>();
listOptions.Add(textSearchOptions);
listOptions.Add(imageSearchOptions);
listOptions.Add(barcodeOptions);
listOptions.Add(qrCodeOptions);
```
## الخطوة 5: البحث عن التوقيعات
قم بتنفيذ عملية بحث للعثور على جميع التوقيعات داخل المستند بناءً على خيارات البحث المحددة:
```csharp
SearchResult result = signature.Search(listOptions);
```
## الخطوة 6: حذف التوقيعات
إذا تم العثور على التوقيعات، تابع لحذفها:
```csharp
if (result.Signatures.Count > 0)
{
    // محاولة حذف كافة التوقيعات
    DeleteResult deleteResult = signature.Delete(result.Signatures);
    //تحقق مما إذا كان الحذف ناجحًا
    if(deleteResult.Succeeded.Count == result.Signatures.Count)
    {
        Console.WriteLine("\nAll signatures were successfully deleted!");                        
    }
    else
    {
        Console.WriteLine($"Successfully deleted signatures : {deleteResult.Succeeded.Count}");
        Helper.WriteError($"Not deleted signatures : {deleteResult.Failed.Count}");
    }
    // عرض معلومات حول التوقيعات المحذوفة
    Console.WriteLine("\nList of deleted signatures:");
    int number = 1;
    foreach(BaseSignature temp in deleteResult.Succeeded)
    {
        Console.WriteLine($"Signature #{number++}: Type: {temp.SignatureType} Id:{temp.SignatureId}, Location: {temp.Left}x{temp.Top}. Size: {temp.Width}x{temp.Height}");
    }
}
else
{
    Helper.WriteError("No one signature was found.");
}
```

## خاتمة
يعد حذف التوقيعات المتعددة من المستند برمجياً مهمة حاسمة في إدارة المستندات. باستخدام GroupDocs.Signature for .NET، تصبح هذه العملية فعالة وموثوقة. باتباع الخطوات الموضحة في هذا البرنامج التعليمي، يمكنك بسهولة دمج وظيفة حذف التوقيع في تطبيقات .NET الخاصة بك.
## الأسئلة الشائعة
### هل يمكن لـ GroupDocs.Signature لـ .NET التعامل مع تنسيقات المستندات المختلفة؟
نعم، يدعم GroupDocs.Signature for .NET نطاقًا واسعًا من تنسيقات المستندات، بما في ذلك DOCX وPDF وPPTX وXLSX والمزيد.
### هل من الممكن تخصيص خيارات البحث للكشف عن التوقيع؟
بالتأكيد، يمكنك تخصيص خيارات البحث مثل البحث عن النص، والبحث عن الصور، والبحث عن الرمز الشريطي، والبحث عن رمز الاستجابة السريعة لتلبية متطلباتك المحددة.
### هل يوفر GroupDocs.Signature for .NET آليات لمعالجة الأخطاء؟
نعم، توفر المكتبة إمكانات قوية لمعالجة الأخطاء لضمان التنفيذ السلس لمهام معالجة المستندات.
### هل يمكنني دمج GroupDocs.Signature لـ .NET مع مكتبات الجهات الخارجية الأخرى؟
ومن المؤكد أن GroupDocs.Signature for .NET مصمم للتكامل بسلاسة مع مكتبات .NET الأخرى، مما يوفر المرونة وقابلية التوسعة.
### أين يمكنني العثور على دعم وموارد إضافية لـ GroupDocs.Signature لـ .NET؟
 يمكنك زيارة GroupDocs[المنتدى](https://forum.groupdocs.com/c/signature/13) مخصصة للمناقشات المتعلقة بالتوقيع وطلب المساعدة من المجتمع والخبراء.