---
title: حذف التوقيع عن طريق الهوية
linktitle: حذف التوقيع عن طريق الهوية
second_title: GroupDocs.Signature .NET API
description: تعرف على كيفية حذف التوقيع بواسطة المعرف في مستندات .NET باستخدام مكتبة GroupDocs.Signature. دليل سهل خطوة بخطوة.
weight: 11
url: /ar/net/delete-operations/delete-signature-by-id/
---

# حذف التوقيع عن طريق الهوية

## مقدمة
في هذا البرنامج التعليمي، سوف نستكشف كيفية حذف التوقيع بواسطة المعرف الخاص به باستخدام GroupDocs.Signature لـ .NET. تعد GroupDocs.Signature for .NET مكتبة قوية تسمح للمطورين بإضافة التوقيعات الرقمية أو إزالتها أو التحقق منها في تنسيقات المستندات المختلفة باستخدام تطبيقات .NET.
## المتطلبات الأساسية
قبل أن نبدأ، تأكد من توفر المتطلبات الأساسية التالية:
1.  GroupDocs.Signature لمكتبة .NET: قم بتنزيل المكتبة وتثبيتها من[هنا](https://releases.groupdocs.com/signature/net/).
2. .NET Framework: تأكد من تثبيت .NET Framework على نظامك.
3. مستند بتوقيع: قم بإعداد مستند (على سبيل المثال، DOCX، PDF) بالتوقيع الذي تريد حذفه.

## استيراد مساحات الأسماء
```csharp
using System;
using System.IO;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## الخطوة 1: تحديد مسارات الملفات
أولاً، حدد مسار الملف للمستند الذي يحتوي على التوقيع، ومسار ملف الإخراج حيث سيتم حفظ المستند المعدل.
```csharp
string filePath = "sample_multiple_signatures.docx";
string fileName = Path.GetFileName(filePath);
string outputFilePath = Path.Combine("Your Document Directory", "DeleteById", fileName);
```
## الخطوة 2: انسخ المستند
 منذ`Delete` الطريقة تعدل المستند في مكانه، فمن الأفضل إنشاء نسخة من المستند الأصلي.
```csharp
File.Copy(filePath, outputFilePath, true);
```
## الخطوة 3: حذف التوقيع عن طريق الهوية
 تهيئة`Signature` الكائن بمسار ملف المستند واستخدم ملف`Delete` طريقة إزالة التوقيع بواسطة المعرف الخاص به.
```csharp
using (Signature signature = new Signature(outputFilePath))
{
    string id = @"eff64a14-dad9-47b0-88e5-2ee4e3604e71";
    bool result = signature.Delete(id);
    if (result)
    {
        Console.WriteLine($"Signature with Id# '{id}' was deleted from document ['{fileName}'].");
    }
    else
    {
        Helper.WriteError($"Signature was not deleted from the document! Signature with id# '{id}' was not found!");
    }
}
```

## خاتمة
في هذا البرنامج التعليمي، تعلمنا كيفية حذف التوقيع بواسطة معرفه باستخدام GroupDocs.Signature لـ .NET. توفر هذه المكتبة طريقة ملائمة لإدارة التوقيعات الرقمية بتنسيقات المستندات المختلفة برمجيًا.
## الأسئلة الشائعة
### هل يمكنني حذف توقيعات متعددة في وقت واحد؟
 نعم، يمكنك حذف توقيعات متعددة عن طريق تكرار معرفاتهم واستدعاء`Delete` طريقة لكل معرف
### هل يتوافق GroupDocs.Signature for .NET مع كافة تنسيقات المستندات؟
يدعم GroupDocs.Signature for .NET نطاقًا واسعًا من تنسيقات المستندات، بما في ذلك PDF وDOCX وXLSX والمزيد.
### هل يمكنني تخصيص مظهر التوقيع؟
نعم، يمكنك تخصيص مظهر التوقيع، بما في ذلك موضعه وحجمه وخطه ولونه.
### هل هناك نسخة تجريبية متاحة؟
 نعم، يمكنك تنزيل نسخة تجريبية مجانية من[هنا](https://releases.groupdocs.com/).
### أين يمكنني العثور على مساعدة أو دعم بخصوص GroupDocs.Signature لـ .NET؟
 يمكنك زيارة منتدى الدعم[هنا](https://forum.groupdocs.com/c/signature/13) للمساعدة.