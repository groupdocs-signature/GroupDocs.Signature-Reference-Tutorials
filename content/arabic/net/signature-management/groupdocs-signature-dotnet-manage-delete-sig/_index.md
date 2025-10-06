---
"date": "2025-05-07"
"description": "تعرّف على كيفية إدارة وحذف توقيعات المستندات بكفاءة باستخدام GroupDocs.Signature لـ .NET. مثالي لضمان الامتثال وتبسيط إدارة العقود."
"title": "Master GroupDocs.Signature لـ .NET - إدارة وحذف توقيعات المستندات"
"url": "/ar/net/signature-management/groupdocs-signature-dotnet-manage-delete-sig/"
"weight": 1
type: docs
---
# إتقان إدارة التوقيع في .NET باستخدام GroupDocs.Signature

## مقدمة
في ظلّ العالم الرقميّ الحالي، تُعدّ إدارة توقيعات المستندات بكفاءة أمرًا بالغ الأهمية للشركات والأفراد على حدّ سواء. سواءً كنتَ تُحقّق من صحة العقود أو تضمن الامتثال، فإنّ الأدوات المناسبة تُحدث فرقًا كبيرًا. سيُرشدك هذا البرنامج التعليمي خلال استخدام **GroupDocs.Signature لـ .NET** لإدارة وحذف التوقيعات في المستندات بسلاسة.

**ما سوف تتعلمه:**
- كيفية تهيئة مثيل التوقيع.
- إضافة خيارات بحث متنوعة لاكتشاف التوقيعات.
- البحث عن أنواع مختلفة من التوقيعات داخل المستندات.
- حذف التوقيعات المتعددة بكفاءة.

هل أنت مستعد للبدء؟ لنستكشف المتطلبات الأساسية أولًا.

## المتطلبات الأساسية
قبل أن نبدأ، تأكد من أن لديك ما يلي:

- **المكتبات المطلوبة**: GroupDocs.Signature لـ .NET
- **إعداد البيئة**:Visual Studio 2019 أو إصدار أحدث مع تثبيت .NET Framework أو .NET Core.
- **متطلبات المعرفة الأساسية**:فهم أساسي لتطوير C# و.NET.

## إعداد GroupDocs.Signature لـ .NET
للبدء، عليك تثبيت مكتبة GroupDocs.Signature. إليك الطريقة:

### تعليمات التثبيت
**استخدام .NET CLI:**
```bash
dotnet add package GroupDocs.Signature
```

**وحدة تحكم مدير الحزمة:**
```powershell
Install-Package GroupDocs.Signature
```

**واجهة مستخدم مدير حزمة NuGet:** 
ابحث عن "GroupDocs.Signature" وقم بتثبيت الإصدار الأحدث.

### الحصول على الترخيص
يمكنك البدء بفترة تجريبية مجانية لاستكشاف الميزات. للاستخدام الممتد، فكّر في الحصول على ترخيص مؤقت أو شراء ترخيص من [مجموعة المستندات](https://purchase.groupdocs.com/buy).

## دليل التنفيذ
دعونا نقوم بتقسيم كل ميزة خطوة بخطوة.

### الميزة 1: تهيئة مثيل التوقيع
توضح هذه الميزة كيفية إعداد البيئة الخاصة بك لإدارة التوقيعات في المستندات باستخدام GroupDocs.Signature لـ .NET. 

#### ملخص
تهيئة `Signature` تعتبر المثيلة بالغة الأهمية لأنها تقوم بإعداد المستند لعمليات التوقيع مثل البحث والحذف.

#### تنفيذ الكود
```csharp
using System.IO;
using GroupDocs.Signature;

var filePath = Path.Combine("YOUR_DOCUMENT_DIRECTORY", "Sample_Signed_Multi_Document");
Directory.CreateDirectory(Path.GetDirectoryName(filePath)); // تأكد من وجود الدليل.
File.Copy(filePath, outputFilePath, true);

// تهيئة مثيل التوقيع باستخدام مسار المستند
using (Signature signature = new Signature(outputFilePath))
{
    // أصبحت الآن نسخة التوقيع جاهزة للعمليات.
}
```

#### توضيح
- `filePath`:المسار إلى المستند المصدر.
- `Directory.CreateDirectory(...)`:يتأكد من وجود الدليل قبل محاولة إجراء عمليات على الملف.
- `signature`:الكائن الأساسي الذي يسهل كافة المهام المتعلقة بالتوقيع.

### الميزة 2: إضافة خيارات البحث
يتطلب اكتشاف التوقيعات بكفاءة تحديد نوع التوقيعات التي تبحث عنها في مستنداتك.

#### ملخص
تتيح لك إضافة خيارات البحث استهداف أنواع معينة من التوقيعات مثل النص أو الرمز الشريطي أو رمز الاستجابة السريعة أو التوقيعات القائمة على الصور داخل مستند.

#### تنفيذ الكود
```csharp
using System.Collections.Generic;
using GroupDocs.Signature.Options;

List<SearchOptions> listOptions = new List<SearchOptions>();
listOptions.Add(new TextSearchOptions()); // البحث عن التوقيعات النصية.
listOptions.Add(new BarcodeSearchOptions()); // البحث عن توقيعات الباركود.
listOptions.Add(new QrCodeSearchOptions()); // البحث عن توقيعات رمز الاستجابة السريعة QR.
listOptions.Add(new ImageSearchOptions()); // البحث عن التوقيعات القائمة على الصور.

// تحتوي listOptions الآن على جميع خيارات البحث اللازمة للعثور على أنواع مختلفة من التوقيعات في مستند.
```

#### توضيح
- `TextSearchOptions`:يستهدف توقيعات النص داخل المستند.
- `BarcodeSearchOptions`، `QrCodeSearchOptions`، و `ImageSearchOptions`:تمكين الكشف عن الباركود، ورمز الاستجابة السريعة، والتوقيعات القائمة على الصور على التوالي.

### الميزة 3: البحث عن التوقيعات في المستند
بعد إعداد خيارات البحث، يمكنك الآن العثور على هذه التوقيعات في مستنداتك.

#### ملخص
تسلط هذه الميزة الضوء على كيفية البحث عن مستند باستخدام خيارات التوقيع المحددة ومعالجة النتائج وفقًا لذلك.

#### تنفيذ الكود
```csharp
using System.Collections.Generic;
using GroupDocs.Signature.Domain;

string filePath = Path.Combine("YOUR_DOCUMENT_DIRECTORY", "Sample_Signed_Multi_Document");
Directory.CreateDirectory(Path.GetDirectoryName(filePath)); // تأكد من وجود الدليل.
File.Copy(filePath, outputFilePath, true);

using (Signature signature = new Signature(outputFilePath))
{
    List<SearchOptions> listOptions = new List<SearchOptions>();
    listOptions.Add(new TextSearchOptions());
    listOptions.Add(new BarcodeSearchOptions());
    listOptions.Add(new QrCodeSearchOptions());
    listOptions.Add(new ImageSearchOptions());

    // ابحث عن التوقيعات باستخدام الخيارات المحددة.
    SearchResult result = signature.Search(listOptions);

    if (result.Signatures.Count > 0)
    {
        // التوقيعات الموجودة في الوثيقة.
    }
    else
    {
        // لم يتم العثور على أي توقيعات في الوثيقة.
    }
}
```

#### توضيح
- `SearchResult`:يحتوي على تفاصيل جميع التوقيعات المكتشفة، مما يسمح بالمعالجة الإضافية مثل الحذف.

### الميزة 4: حذف التوقيعات من المستند
بمجرد تحديد التوقيعات غير المرغوب فيها، فإن الخطوة التالية هي إزالتها بكفاءة.

#### ملخص
توضح هذه الميزة كيفية حذف أنواع متعددة من التوقيعات من مستند باستخدام GroupDocs.Signature لـ .NET.

#### تنفيذ الكود
```csharp
using System.Collections.Generic;
using GroupDocs.Signature.Domain;

string filePath = Path.Combine("YOUR_DOCUMENT_DIRECTORY", "Sample_Signed_Multi_Document");
Directory.CreateDirectory(Path.GetDirectoryName(filePath)); // تأكد من وجود الدليل.
File.Copy(filePath, outputFilePath, true);

using (Signature signature = new Signature(outputFilePath))
{
    List<SearchOptions> listOptions = new List<SearchOptions>();
    listOptions.Add(new TextSearchOptions());
    listOptions.Add(new BarcodeSearchOptions());
    listOptions.Add(new QrCodeSearchOptions());
    listOptions.Add(new ImageSearchOptions());

    // البحث عن التوقيعات.
    SearchResult result = signature.Search(listOptions);

    if (result.Signatures.Count > 0)
    {
        List<BaseSignature> signaturesToDelete = new List<BaseSignature>();

        // جمع التوقيعات للحذف.
        foreach (BaseSignature temp in result.Signatures)
        {
            signaturesToDelete.Add(temp);
        }

        // حذف التوقيعات المجمعة من المستند.
        DeleteResult deleteResult = signature.Delete(signaturesToDelete);
    }
}
```

#### توضيح
- `signaturesToDelete`:مجموعة من التوقيعات المحددة للحذف.
- `DeleteResult`:يوفر ملاحظات حول نجاح أو فشل عملية الحذف.

## التطبيقات العملية
1. **إدارة العقود**:أتمتة التحقق من التوقيعات القديمة وإزالتها في العقود.
2. **عمليات تدقيق الامتثال**:التأكد من امتثال جميع المستندات للمتطلبات التنظيمية من خلال التدقيق وتنظيف التوقيعات.
3. **إدارة دورة حياة المستندات**:إدارة توقيعات المستندات طوال دورة حياتها، من إنشائها إلى أرشفتها.

## اعتبارات الأداء
- قم بتحسين الأداء عن طريق معالجة الأجزاء الضرورية فقط من المستند عند البحث عن التوقيعات أو حذفها.
- راقب استخدام الموارد للتأكد من أن تطبيقك يظل فعالاً وسريع الاستجابة أثناء عمليات التوقيع.