---
title: حذف توقيع رمز الاستجابة السريعة من المستند
linktitle: حذف توقيع رمز الاستجابة السريعة من المستند
second_title: GroupDocs.Signature .NET API
description: تعرف على كيفية حذف توقيعات رمز الاستجابة السريعة من المستندات باستخدام GroupDocs.Signature لـ .NET. اتبع دليلنا خطوة بخطوة لإدارة التوقيع بكفاءة.
weight: 16
url: /ar/net/delete-operations/delete-qr-code-signature/
---

# حذف توقيع رمز الاستجابة السريعة من المستند

## مقدمة
في هذا البرنامج التعليمي، سنرشدك خلال عملية إزالة توقيع رمز الاستجابة السريعة من مستند باستخدام GroupDocs.Signature لـ .NET. اتبع هذه التعليمات خطوة بخطوة لحذف توقيعات رمز QR بشكل فعال.
## المتطلبات الأساسية
قبل البدء، تأكد من توفر المتطلبات الأساسية التالية:
-  GroupDocs.Signature لـ .NET: تأكد من تثبيت مكتبة GroupDocs.Signature في مشروع .NET الخاص بك. يمكنك تنزيله من[هنا](https://releases.groupdocs.com/signature/net/).
- مستند بتوقيع رمز الاستجابة السريعة: قم بإعداد مستند يحتوي على توقيعات رمز الاستجابة السريعة التي تريد حذفها.
- المعرفة الأساسية بـ C#: تعرف على أساسيات لغة البرمجة C#.

## استيراد مساحات الأسماء
قبل الغوص في التعليمات البرمجية، قم باستيراد مساحات الأسماء الضرورية إلى ملف C# الخاص بك:
```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## الخطوة 1: تحديد مسارات الملفات
```csharp
// المسار إلى دليل المستندات.
string filePath = "sample_multiple_signatures.docx";
string fileName = Path.GetFileName(filePath);
// تحديد مسار ملف الإخراج للمستند المعدل.
string outputFilePath = Path.Combine("Your Document Directory", "DeleteQRCode", fileName);
// انسخ الملف المصدر لأن طريقة الحذف تعمل مع نفس المستند.
File.Copy(filePath, outputFilePath, true);
```
## الخطوة 2: تهيئة كائن التوقيع
```csharp
using (Signature signature = new Signature(outputFilePath))
{
    // إنشاء خيارات للبحث في توقيعات رمز الاستجابة السريعة.
    QrCodeSearchOptions options = new QrCodeSearchOptions();
    // ابحث عن توقيعات رمز الاستجابة السريعة في المستند.
    List<QrCodeSignature> signatures = signature.Search<QrCodeSignature>(options);
```
## الخطوة 3: التحقق من وجود توقيع رمز الاستجابة السريعة
```csharp
    if (signatures.Count > 0)
    {
        // احصل على أول توقيع لرمز الاستجابة السريعة الموجود في المستند.
        QrCodeSignature qrCodeSignature = signatures[0];
```
## الخطوة 4: حذف توقيع رمز الاستجابة السريعة
```csharp
        // احذف توقيع رمز الاستجابة السريعة من المستند.
        bool result = signature.Delete(qrCodeSignature);
        if (result)
        {
            Console.WriteLine($"Signature with QR-Code '{qrCodeSignature.Text}' and encode type '{qrCodeSignature.EncodeType.TypeName}' was deleted from document ['{fileName}'].");
        }
        else
        {
            Helper.WriteError($"Signature was not deleted from the document! Signature with Barcode '{qrCodeSignature.Text}' and encode type '{qrCodeSignature.EncodeType.TypeName}' was not found!");
        }
    }
}
```
تهانينا! لقد نجحت في إزالة توقيع رمز الاستجابة السريعة من المستند باستخدام GroupDocs.Signature لـ .NET.

## خاتمة
في هذا البرنامج التعليمي، تعلمنا كيفية حذف توقيع رمز QR من مستند باستخدام GroupDocs.Signature لـ .NET. باتباع الخطوات المتوفرة، يمكنك إدارة التوقيعات ومعالجتها بكفاءة داخل تطبيقات .NET الخاصة بك.
## الأسئلة الشائعة
### هل يمكنني حذف توقيعات رمز الاستجابة السريعة المتعددة من مستند؟
نعم، يمكنك تعديل الرمز للتكرار عبر جميع توقيعات رمز الاستجابة السريعة وحذفها وفقًا لذلك.
### هل يدعم GroupDocs.Signature أنواعًا أخرى من التوقيعات إلى جانب رموز QR؟
نعم، يدعم GroupDocs.Signature أنواع التوقيع المختلفة مثل النص والصورة والرمز الشريطي والمزيد.
### هل GroupDocs.Signature متوافق مع جميع تنسيقات المستندات؟
يدعم GroupDocs.Signature مجموعة واسعة من تنسيقات المستندات بما في ذلك PDF وMicrosoft Word وExcel وPowerPoint والمزيد.
### هل يمكنني تخصيص خيارات البحث للتوقيعات؟
نعم، يمكنك تخصيص خيارات البحث وفقًا لمتطلباتك لتحديد موقع توقيعات معينة داخل المستند.
### هل هناك إصدار تجريبي متاح لـ GroupDocs.Signature؟
 نعم، يمكنك الوصول إلى الإصدار التجريبي المجاني من GroupDocs.Signature من[هنا](https://releases.groupdocs.com/).