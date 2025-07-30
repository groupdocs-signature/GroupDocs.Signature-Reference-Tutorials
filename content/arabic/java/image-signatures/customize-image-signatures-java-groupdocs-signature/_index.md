---
"date": "2025-05-08"
"description": "تعرّف على كيفية تنفيذ توقيعات الصور المُخصّصة في جافا باستخدام GroupDocs.Signature. يتناول هذا الدليل تحديد المواقع، والمحاذاة، وتعديلات المظهر، وتخصيصات الحدود."
"title": "كيفية تخصيص توقيعات الصور في Java باستخدام GroupDocs.Signature"
"url": "/ar/java/image-signatures/customize-image-signatures-java-groupdocs-signature/"
"weight": 1
---

# كيفية تنفيذ توقيعات الصور المخصصة باستخدام GroupDocs.Signature لـ Java

## مقدمة

في عالمنا الرقمي اليوم، يُعدّ التوقيع الإلكتروني للمستندات أمرًا بالغ الأهمية للعديد من العمليات التجارية. قد يكون من الصعب ضمان ظهور توقيعك في المكان المطلوب على المستند مع الحفاظ على مظهر احترافي. **GroupDocs.Signature لـ Java** يقدم خيارات تخصيص قوية لدمج التوقيعات الإلكترونية بسلاسة في التطبيقات.

يرشدك هذا البرنامج التعليمي خلال إعداد GroupDocs.Signature لجافا، ويستكشف ميزات رئيسية مثل تحديد موضع الصور ومحاذاتها وتصميمها باستخدام إعدادات متنوعة مثل الحجم والمحاذاة وتعديلات المظهر وتخصيصات الحدود. بنهاية هذه المقالة، ستعرف كيفية:
- تعيين موضع التوقيع وحجمه
- محاذاة التوقيع مع الهوامش
- ضبط إعدادات مظهر الصورة
- تخصيص حدود الصورة

دعونا نغوص في ذلك!

## المتطلبات الأساسية

قبل أن نبدأ، تأكد من أن لديك المتطلبات الأساسية التالية جاهزة:
1. **مجموعة تطوير جافا (JDK)**:تأكد من تثبيت JDK 8 أو أعلى على نظامك.
2. **بيئة التطوير المتكاملة (IDE)**:استخدم IDE مثل IntelliJ IDEA أو Eclipse لتطوير Java.
3. **مكتبة GroupDocs.Signature**:أضف GroupDocs.Signature كتبعية في مشروعك.

### المكتبات والتبعيات المطلوبة

لتضمين GroupDocs.Signature، يمكنك استخدام Maven أو Gradle:

**مافن**
```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

**جرادل**
```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

بدلاً من ذلك، قم بتنزيل الإصدار الأحدث مباشرةً من [GroupDocs.Signature لإصدارات Java](https://releases.groupdocs.com/signature/java/).

### إعداد البيئة

تأكد من تكوين بيئة التطوير المتكاملة لديك لتضمين مكتبات خارجية وإعداد مشروع يحتوي على أدلة للمستندات المدخلة وصور التوقيع والمستندات الموقعة الناتجة.

### متطلبات المعرفة الأساسية

- فهم أساسيات برمجة جافا.
- المعرفة بكيفية التعامل مع مسارات الملفات في تطبيقات Java.

## إعداد GroupDocs.Signature لـ Java

لبدء استخدام GroupDocs.Signature، اتبع خطوات الإعداد التالية:
1. **إضافة التبعية**:استخدم تكوين Maven أو Gradle المقدم لتضمين المكتبة.
2. **الحصول على الترخيص**:ابدأ بتنزيل نسخة تجريبية مجانية من [مجموعة المستندات](https://releases.groupdocs.com/signature/java/) وفكر في شراء ترخيص إذا لزم الأمر.

### التهيئة الأساسية

فيما يلي كيفية تهيئة GroupDocs.Signature في تطبيق Java الخاص بك:

```java
import com.groupdocs.signature.Signature;

public class Main {
    public static void main(String[] args) throws Exception {
        String filePath = "path/to/your/document.docx";
        Signature signature = new Signature(filePath);
        
        // الإعدادات الإضافية والاستخدامات تذهب هنا
    }
}
```

## دليل التنفيذ

دعونا نلقي نظرة على كيفية تنفيذ الميزات المختلفة لتخصيص توقيعات الصور.

### تعيين موضع التوقيع والحجم

**ملخص**:تتيح لك هذه الميزة تحديد مكان ظهور توقيعك على المستند وأبعاده، مما يضمن الاتساق عبر المستندات.

#### التنفيذ خطوة بخطوة

1. **تهيئة كائن التوقيع**:إنشاء مثيل لـ `Signature` الفئة مع مسار المستند الخاص بك.
2. **تكوين ImageSignOptions**:قم بتعيين خيارات توقيع الصورة بما في ذلك الحجم والموضع.

```java
import com.groupdocs.signature.Signature;
import com.groupdocs.signature.options.sign.ImageSignOptions;

public class SignWithImagePosition {
    public static void run() throws Exception {
        String filePath = "YOUR_DOCUMENT_DIRECTORY/document.docx";
        String imagePath = "YOUR_DOCUMENT_DIRECTORY/signature.png";
        String outputFilePath = "YOUR_OUTPUT_DIRECTORY/SignaturePosition.docx";

        Signature signature = new Signature(filePath);
        ImageSignOptions options = new ImageSignOptions(imagePath);

        // تعيين موضع التوقيع على المستند
        options.setLeft(100);  // إحداثيات X بالبكسل
        options.setTop(100);   // إحداثيات Y بالبكسل

        // تعيين حجم مستطيل التوقيع
        options.setWidth(100);  // العرض بالبكسل
        options.setHeight(30);  // الارتفاع بالبكسل
        
        // التوقيع على الوثيقة وحفظها
        signature.sign(outputFilePath, options);
    }
}
```

### تعيين محاذاة التوقيع والهامش

**ملخص**يضمن ضبط المحاذاة تناسقًا في توزيع النصوص في مختلف أقسام المستند. تساعد الهوامش على تجنب الاقتصاص أو التداخل مع محتوى آخر.

#### التنفيذ خطوة بخطوة

1. **تحديد المحاذاة الرأسية والأفقية**:استخدم قيم التعداد للمحاذاة المطلوبة.
2. **تكوين الهوامش باستخدام الحشو**:حدد الهوامش لتحديد الموضع الدقيق.

```java
import com.groupdocs.signature.Signature;
import com.groupdocs.signature.options.sign.ImageSignOptions;
import com.groupdocs.signature.domain.enums.HorizontalAlignment;
import com.groupdocs.signature.domain.enums.VerticalAlignment;
import com.groupdocs.signature.domain.Padding;

public class SignWithImageAlignment {
    public static void run() throws Exception {
        String filePath = "YOUR_DOCUMENT_DIRECTORY/document.docx";
        String imagePath = "YOUR_DOCUMENT_DIRECTORY/signature.png";
        String outputFilePath = "YOUR_OUTPUT_DIRECTORY/SignatureAlignment.docx";

        Signature signature = new Signature(filePath);
        ImageSignOptions options = new ImageSignOptions(imagePath);

        // ضبط المحاذاة الرأسية للتوقيع
        options.setVerticalAlignment(VerticalAlignment.Bottom);
        
        // ضبط المحاذاة الأفقية للتوقيع
        options.setHorizontalAlignment(HorizontalAlignment.Right);
        
        // تكوين الحشو الهامشي لتحديد موضع التوقيع
        Padding padding = new Padding();
        padding.setBottom(20);  // الهامش السفلي بالبكسل
        padding.setRight(20);   // الهامش الأيمن بالبكسل
        options.setMargin(padding);

        // التوقيع على الوثيقة وحفظها
        signature.sign(outputFilePath, options);
    }
}
```

### ضبط مظهر الصورة باستخدام ضبط التدرج الرمادي والسطوع

**ملخص**تخصيص مظهر الصورة يُحسّن من جاذبيتها البصرية. من الخيارات المتاحة تطبيق تدرجات الرمادي أو تعديل السطوع.

#### التنفيذ خطوة بخطوة

1. **تكوين إعدادات مظهر الصورة**: يستخدم `ImageAppearance` لضبط كيفية ظهور الصورة على المستند.

```java
import com.groupdocs.signature.Signature;
import com.groupdocs.signature.options.sign.ImageSignOptions;
import com.groupdocs.signature.domain.appearances.ImageAppearance;

public class SignWithImageAppearance {
    public static void run() throws Exception {
        String filePath = "YOUR_DOCUMENT_DIRECTORY/document.docx";
        String imagePath = "YOUR_DOCUMENT_DIRECTORY/signature.png";
        String outputFilePath = "YOUR_OUTPUT_DIRECTORY/SignatureAppearance.docx";

        Signature signature = new Signature(filePath);
        ImageSignOptions options = new ImageSignOptions(imagePath);

        // إنشاء وتكوين إعدادات مظهر الصورة
        ImageAppearance imageAppearance = new ImageAppearance();
        
        // تطبيق تأثير التدرج الرمادي على الصورة
        imageAppearance.setGrayscale(true);
        
        // ضبط مستوى سطوع الصورة
        imageAppearance.setBrightness(0.9f);  // مستوى السطوع (المدى: 0.0 - 1.0)
        
        options.setAppearance(imageAppearance);

        // التوقيع على الوثيقة وحفظها
        signature.sign(outputFilePath, options);
    }
}
```

### تعيين حدود الصورة باستخدام الأسلوب والشفافية

**ملخص**:يمكن أن يؤدي تخصيص الحدود إلى تعزيز احترافية توقيعاتك.

#### التنفيذ خطوة بخطوة

1. **تكوين خيارات الحدود**: يستخدم `Border` الإعدادات لتحديد الأسلوب والشفافية.

```java
import com.groupdocs.signature.Signature;
import com.groupdocs.signature.options.sign.ImageSignOptions;
import com.groupdocs.signature.domain.Border;

public class SignWithImageBorder {
    public static void run() throws Exception {
        String filePath = "YOUR_DOCUMENT_DIRECTORY/document.docx";
        String imagePath = "YOUR_DOCUMENT_DIRECTORY/signature.png";
        String outputFilePath = "YOUR_OUTPUT_DIRECTORY/SignatureBorder.docx";

        Signature signature = new Signature(filePath);
        ImageSignOptions options = new ImageSignOptions(imagePath);

        // إنشاء وتكوين إعدادات الحدود للصورة
        Border border = new Border();
        border.setColor(java.awt.Color.BLACK);  // تعيين لون الحدود
        border.setWidth(2);                    // تعيين عرض الحدود بالبكسل
        border.setDashStyle(com.groupdocs.signature.domain.enums.DashStyle.DashDot);
        
        options.setBorder(border);

        // التوقيع على الوثيقة وحفظها
        signature.sign(outputFilePath, options);
    }
}
```