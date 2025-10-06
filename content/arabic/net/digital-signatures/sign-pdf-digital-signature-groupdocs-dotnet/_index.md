---
"date": "2025-05-07"
"description": "تعرّف على كيفية التوقيع الرقمي لملفات PDF باستخدام GroupDocs.Signature لـ .NET. خصّص المظهر، واضف الخطوط والصور، لضمان أمان المستندات ومصداقيتها."
"title": "التوقيع الرقمي على ملفات PDF في .NET - دليل استخدام GroupDocs.Signature"
"url": "/ar/net/digital-signatures/sign-pdf-digital-signature-groupdocs-dotnet/"
"weight": 1
type: docs
---
# التوقيع الرقمي على ملفات PDF في .NET: دليل باستخدام GroupDocs.Signature

## مقدمة

تضمن التوقيعات الرقمية على مستندات PDF صحتها وأمانها وسلامتها - وهو أمر ضروري للعقود القانونية والفواتير والسجلات الرسمية. **GroupDocs.Signature لـ .NET** يُبسّط إضافة التوقيعات الرقمية إلى ملفات PDF، مع إمكانية تخصيص مظهرها لتحسين جاذبيتها البصرية. سيرشدك هذا البرنامج التعليمي خلال عملية توقيع مستند PDF باستخدام GroupDocs.Signature، مع التركيز بشكل خاص على إعدادات الصور والخطوط.

### ما سوف تتعلمه:
- كيفية التوقيع رقميًا على مستند PDF باستخدام .NET
- تطبيق إعدادات المظهر المخصصة مثل الصور والخطوط على توقيعك الرقمي
- إعداد GroupDocs.Signature وتشغيله لـ .NET في مشروعك

دعونا نبدأ بتغطية المتطلبات الأساسية اللازمة للبدء.

## المتطلبات الأساسية (H2)

لمتابعة هذا البرنامج التعليمي، ستحتاج إلى:

- **GroupDocs.Signature لـ .NET** المكتبة: تأكد من تثبيتها عبر .NET CLI أو NuGet Package Manager.
  - **.NET CLI**: `dotnet add package GroupDocs.Signature`
  - **مدير الحزم**: `Install-Package GroupDocs.Signature`

- شهادة رقمية صالحة بتنسيق PFX
- المعرفة الأساسية بلغة C# وإعداد بيئة .NET

## إعداد GroupDocs.Signature لـ .NET (H2)

ابدأ بتثبيت مكتبة GroupDocs.Signature:

**.NET CLI**
```shell
dotnet add package GroupDocs.Signature
```

**مدير الحزم**
```shell
Install-Package GroupDocs.Signature
```

أو استخدم واجهة مستخدم NuGet Package Manager للبحث عن "GroupDocs.Signature" وتثبيته.

### الحصول على الترخيص

- **نسخة تجريبية مجانية**:استكشف الميزات الكاملة باستخدام ترخيص التقييم المؤقت.
- **رخصة مؤقتة**:الحصول عليها من [هنا](https://purchase.groupdocs.com/temporary-license/).
- **شراء**:للاستخدام طويل الأمد، قم بشراء اشتراك في [هذا الرابط](https://purchase.groupdocs.com/buy).

### التهيئة والإعداد الأساسي

لتهيئة GroupDocs.Signature في مشروع .NET الخاص بك:

```csharp
using GroupDocs.Signature;

// قم بتهيئة كائن التوقيع باستخدام ملف PDF المصدر.
using (Signature signature = new Signature("YOUR_DOCUMENT_DIRECTORY/SAMPLE_PDF.pdf")) {
    // يوجد هنا رمزك لتوقيع المستند.
}
```

## دليل التنفيذ

### توقيع مستند PDF باستخدام التوقيع الرقمي (H2)

تتيح لك هذه الميزة إضافة توقيع رقمي إلى مستندات PDF الخاصة بك، مما يضمن صحتها وسلامتها.

#### نظرة عامة على الميزة
بتطبيق هذه الميزة، يمكنك التوقيع رقميًا على أي ملف PDF باستخدام GroupDocs.Signature لـ .NET. كما يمكنك تطبيق إعدادات مخصصة لتخصيص مظهر توقيعك، بما في ذلك الصور والخطوط.

#### خطوات التنفيذ (H3)

##### الخطوة 1: إعداد البيئة الخاصة بك

تأكد من تكوين مشروعك بالمراجع الضرورية:

```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Options;
using GroupDocs.Signature.Domain;

namespace DigitalSignatureExample {
    public class SignPdfWithDigitalSignature {
        // تحديد المسارات لملف PDF المصدر والشهادة الرقمية
        private static string sourceFile = "YOUR_DOCUMENT_DIRECTORY/SAMPLE_PDF.pdf";
        private static string outputFile = Path.Combine("YOUR_OUTPUT_DIRECTORY", "SignWithPdfDigitalAdvanced_Signed.pdf");
        private static string certificatePath = "YOUR_DOCUMENT_DIRECTORY/CertificatePfx.pfx";

        public static void Run() {
            // تهيئة كائن التوقيع
            using (Signature signature = new Signature(sourceFile)) {
                // إعداد خيارات التوقيع الرقمي
                DigitalSignOptions options = new DigitalSignOptions(certificatePath) {
                    Password = "1234567890",  // كلمة مرور الشهادة
                    Reason = "Sign",          // سبب التوقيع
                    Contact = "JohnSmith",    // معلومات الاتصال
                    Location = "Office1",     // مكان التوقيع
                    Visible = true,            // جعل التوقيع مرئيًا
                    Left = 400,                // الوضع الأفقي
                    Top = 20,                  // الوضع الرأسي
                    Height = 70,               // ارتفاع التوقيع
                    Width = 200,               // عرض التوقيع
                    ImageFilePath = "YOUR_DOCUMENT_DIRECTORY/ImageHandwrite.png", // صورة المظهر
                    Appearance = new PdfDigitalSignatureAppearance() {
                        Foreground = System.Drawing.Color.FromArgb(50, System.Drawing.Color.Gray),
                        FontFamilyName = "TimesNewRoman",
                        FontSize = 12
                    }
                };

                // قم بتوقيع المستند وحفظه في مسار الإخراج.
                SignResult signResult = signature.Sign(outputFile, options);
                Console.WriteLine($"Document signed successfully with {signResult.Succeeded.Count} signature(s). File saved at {outputFile}.");
            }
        }
    }
}
```

##### الخطوة 2: تخصيص مظهر التوقيع

قم بتخصيص مظهر توقيعك الرقمي باستخدام إعدادات الخط والصورة:

```csharp
using System;
using GroupDocs.Signature.Options;
using GroupDocs.Signature.Domain;
using System.Drawing;

namespace DigitalSignatureAppearanceExample {
    public class CustomizeDigitalSignatureAppearance {
        public static void Run() {
            // تهيئة إعدادات المظهر للتوقيع الرقمي.
            PdfDigitalSignatureAppearance appearance = new PdfDigitalSignatureAppearance() {
                Foreground = Color.FromArgb(50, Color.Gray),  // تعيين لون الخط المخصص
                FontFamilyName = "TimesNewRoman",          // حدد عائلة الخط
                FontSize = 12                               // تحديد حجم الخط
            };

            Console.WriteLine("Custom appearance settings for digital signature have been applied.");
        }
    }
}
```

#### خيارات تكوين المفاتيح
- **مسار الشهادة**:تأكد من توفير المسار الصحيح لملف PFX الخاص بك.
- **كلمة المرور**:استخدم كلمة المرور المرتبطة بشهادتك الرقمية.
- **إعدادات المظهر**:تخصيص الخط واللون لتتناسب مع متطلبات العلامة التجارية.

##### نصائح استكشاف الأخطاء وإصلاحها
- تأكد من أن الشهادة الرقمية الخاصة بك صالحة ومُهيأة بشكل صحيح.
- تأكد من إمكانية الوصول إلى جميع المسارات (ملف PDF، الإخراج، الصورة) من بيئة تطبيقك.

### تطبيق إعدادات المظهر المخصصة على التوقيع الرقمي (H2)

قم بتعزيز المظهر المرئي لتوقيعك الرقمي باستخدام إعدادات الخط والصورة المخصصة باستخدام GroupDocs.Signature لـ .NET.

#### ملخص
تخصيص مظهر التوقيع الرقمي يجعله أكثر جاذبية بصريًا ومتوافقًا مع معايير العلامة التجارية. تتيح لك هذه الميزة تحديد خطوط وألوان وصور محددة.

#### خطوات التنفيذ (H3)

##### الخطوة 1: تهيئة إعدادات المظهر

إنشاء مثيل لـ `PdfDigitalSignatureAppearance`:

```csharp
using System.Drawing;

// قم بتحديد إعدادات المظهر المخصصة للتوقيع الرقمي.
PdfDigitalSignatureAppearance appearance = new PdfDigitalSignatureAppearance() {
    Foreground = Color.FromArgb(50, Color.Gray),  // لون الخط المخصص
    FontFamilyName = "TimesNewRoman",            // عائلة الخطوط
    FontSize = 12                                // حجم الخط
};
```

##### الخطوة 2: تطبيق إعدادات المظهر

دمج هذه الإعدادات في خيارات التوقيع الرقمي لديك:

```csharp
DigitalSignOptions options = new DigitalSignOptions(certificatePath) {
    ImageFilePath = "YOUR_DOCUMENT_DIRECTORY/ImageHandwrite.png",
    Appearance = appearance
};
```

## التطبيقات العملية (H2)

فيما يلي بعض السيناريوهات الواقعية حيث قد يكون توقيع ملفات PDF باستخدام GroupDocs.Signature مفيدًا:
1. **توقيع العقد**:تأكد من توقيع الاتفاقيات القانونية والتحقق منها رقميًا.
2. **الموافقة على الفاتورة**:قم بتوقيع الفواتير رقميًا لتسهيل معالجتها بشكل أسرع في الأقسام المالية.
3. **مصادقة المستندات**:التحقق من صحة الوثائق الرسمية لمنع التغييرات غير المصرح بها.

من خلال اتباع هذا الدليل، ستتمكن من دمج التوقيع الرقمي بفعالية في تطبيقات .NET الخاصة بك باستخدام GroupDocs.Signature، مما يعزز الأمان والاحترافية.