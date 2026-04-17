---
categories:
- Java PDF Processing
date: '2026-03-06'
description: تعلم كيفية إنشاء توقيع باركود في مستندات PDF باستخدام Java وGroupDocs.Signature.
  دليل خطوة بخطوة مع أمثلة على الشيفرة وأفضل الممارسات.
keywords: sign PDF with barcode Java, Java barcode signature, GroupDocs PDF signing,
  Code128 barcode PDF, add barcode to PDF programmatically
lastmod: '2026-03-06'
linktitle: Create Barcode Signature Java
tags:
- pdf-signing
- barcode-signature
- document-security
- groupdocs
title: كيفية إنشاء توقيع الباركود في ملف PDF باستخدام Java
type: docs
url: /ar/java/barcode-signatures/java-pdf-signing-barcode-groupdocs/
weight: 1
---

# كيفية إنشاء توقيع الباركود في PDF باستخدام Java

في هذا البرنامج التعليمي، ستتعلم كيفية **إنشاء توقيع باركود** في ملفات PDF باستخدام Java وGroupDocs.Signature. تضمن توقيعات الباركود معرّفات قابلة للقراءة آليًا تكون مقاومة للعبث وسهلة المسح—مناسبة للعقود، الشهادات، الفواتير، وأي مستند يحتاج إلى تحقق موثوق.

## إجابات سريعة
- **ما هو توقيع الباركود؟** باركود مدمج في PDF يخزن بيانات منظمة ويمكن قراءتها بواسطة الماسحات الضوئية أو البرمجيات.  
- **ما نوع الباركود الموصى به؟** Code128، لأنه يتعامل مع البيانات الحرفية الرقمية بشكل مضغوط.  
- **هل أحتاج إلى ترخيص؟** نسخة تجريبية مجانية تكفي للاختبار؛ يتطلب الترخيص الكامل للإنتاج.  
- **هل يمكنني وضع الباركود على أي حجم صفحة؟** نعم—استخدم التموضع القائم على النسبة المئوية للتوسيع التلقائي.  
- **هل الباركود قائم على المتجهات؟** نعم، يضيف فقط بضع كيلوبايت إلى PDF ويبقى واضحًا بأي دقة.  

## لماذا توقيعات الباركود مهمة لملفات PDF الخاصة بك

إليك تحديًا ربما واجهته: تحتاج إلى إضافة معرّفات فريدة إلى ملفات PDF تكون قابلة للقراءة آليًا ومقاومة للعبث. ربما تعمل على نظام إدارة مستندات، أو تعالج شهادات، أو تتعامل مع عقود تحتاج إلى تحقق لاحقًا.

هنا يأتي دور توقيعات الباركود. على عكس الطوابع النصية البسيطة، تسمح لك الباركودات بدمج بيانات منظمة يمكن للماسحات (وبرمجياتك) قراءتها فورًا. بالإضافة إلى ذلك، عندما تجمعها مع توقيع PDF عبر GroupDocs.Signature for Java، تحصل على طريقة قوية لتتبع والتحقق من المستندات دون الحاجة إلى عمليات بحث معقدة في قواعد البيانات.

في هذا الدليل، ستتعلم بالضبط كيفية تنفيذ توقيعات الباركود في ملفات PDF الخاصة بك — من الإعداد الأساسي إلى الكود الجاهز للإنتاج مع تموضع مرن. سواء كنت تبني نظام فواتير، مولد شهادات، أو منصة إدارة عقود، ستحصل على كل ما تحتاجه بحلول النهاية.

**ما ستتقنه:**
- إعداد GroupDocs.Signature for Java في دقائق
- إنشاء توقيعات باركود Code128 (ولماذا غالبًا ما تكون اختيارك الأفضل)
- تموضع الباركود باستخدام تخطيطات قائمة على النسبة المئوية تعمل عبر أي حجم PDF
- تجنب الأخطاء الشائعة التي تعيق المطورين
- اختبار تنفيذك بشكل صحيح

## ما الذي ستحتاجه قبل البدء

تأكد من أن لديك هذه الأساسيات جاهزة:

**المكتبات المطلوبة:**
- GroupDocs.Signature for Java (الإصدار 23.12 أو أحدث يُنصح به)

**بيئة التطوير:**
- JDK 8 أو أعلى مثبت
- بيئة التطوير المتكاملة المفضلة لديك (IntelliJ IDEA، Eclipse، أو VS Code مع امتدادات Java)
- Maven أو Gradle لإدارة التبعيات

**مستوى مهارتك:**
يجب أن تكون مرتاحًا مع بنية Java الأساسية وتعرف كيفية التعامل مع عمليات الملفات. إذا كنت تستطيع إنشاء فئة Java بسيطة ومعالجة الاستثناءات، فأنت جاهز للانطلاق.

## إعداد GroupDocs.Signature في مشروعك

إدخال المكتبة إلى مشروعك سهل. اختر أداة البناء التي تستخدمها:

**لمستخدمي Maven**، أضف هذا إلى ملف `pom.xml` الخاص بك:
```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

**تستخدم Gradle؟** أضف هذا السطر إلى ملف `build.gradle`:
```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

**تفضل الإعداد اليدوي؟** حمّل ملف JAR مباشرة من [GroupDocs.Signature for Java releases](https://releases.groupdocs.com/signature/java/) وأضفه إلى مسار الفئة (classpath).

### الحصول على الترخيص

قبل الانتقال إلى الإنتاج الكامل، ستحتاج إلى معالجة الترخيص:

- **نسخة تجريبية مجانية:** مثالية للاختبار — احصل عليها من موقع GroupDocs لاستكشاف الميزات الأساسية  
- **ترخيص مؤقت:** تحتاج وقتًا أطول للتقييم؟ قدّم طلبًا للحصول على ترخيص مؤقت لمدة 30 يومًا  
- **ترخيص كامل:** جاهز للإنتاج؟ اشترِ ترخيصًا للاستخدام غير المحدود  

إليك فحص سريع للتأكد من أن كل شيء يعمل:
```java
import com.groupdocs.signature.Signature;

public class QuickTest {
    public static void main(String[] args) {
        try {
            Signature signature = new Signature("test-document.pdf");
            System.out.println("GroupDocs.Signature is ready to go!");
        } catch (Exception e) {
            System.err.println("Setup issue: " + e.getMessage());
        }
    }
}
```

إذا تم تشغيله دون أخطاء، فأنت جاهز!

## كيفية إنشاء توقيع باركود في Java

الآن للجزء الممتع — لنوقع PDF بباركود. سنقسم العملية إلى خطوات صغيرة حتى تفهم تمامًا ما يحدث في كل مرحلة.

### الخطوة 1: تهيئة كائن Signature

أولًا، عليك إخبار GroupDocs بملف PDF الذي تعمل عليه:

```java
String filePath = "YOUR_DOCUMENT_DIRECTORY/sample.pdf";
Signature signature = new Signature(filePath);
```

**ما يحدث هنا:** كائن `Signature` يحمل ملف PDF في الذاكرة ويجهزه للتعديلات. تأكد من أن مسار الملف صحيح — أحد الأخطاء الشائعة هو استخدام شرطات مائلة عكسية على Windows دون الهروب منها (استخدم `\\` أو استعمل الشرطات المائلة الأمامية، التي تعمل عبر الأنظمة).

### الخطوة 2: تكوين خيارات الباركود (كيفية إضافة الباركود)

الآن لننشئ توقيع الباركود ببياناتك:

```java
import com.groupdocs.signature.options.sign.BarcodeSignOptions;
import com.groupdocs.signature.domain.barcodes.BarcodeTypes;

BarcodeSignOptions options = new BarcodeSignOptions("12345678");
options.setEncodeType(BarcodeTypes.Code128);
```

**تفصيل ذلك:**
- `"12345678"` هي بيانات الباركود — يمكن أن تكون رقم طلب، رقم شهادة، أو أي معرّف تحتاجه  
- `Code128` هو نوع الترميز (المزيد حول اختيار النوع المناسب أدناه)  

**نصيحة احترافية:** يدعم Code128 كلًا من الأرقام والحروف، مما يجعله متعدد الاستخدامات لمعظم السيناريوهات. إذا كنت تحتاج أرقامًا فقط، قد يكون `Code39` أبسط، لكن Code128 يمنحك مرونة أكبر.

### الخطوة 3: تموضع الباركود (كيفية توقيع PDF بالباركود)

هنا يتألق GroupDocs — التموضع القائم على النسبة المئوية يعني أن الباركود يبدو جيدًا على أي حجم PDF:

```java
import com.groupdocs.signature.domain.enums.MeasureType;
import com.groupdocs.signature.domain.Padding;

// Use percentages instead of fixed pixels
options.setLocationMeasureType(MeasureType.Percents);
options.setLeft(5);  // 5% from the left edge
options.setTop(5);   // 5% from the top

// Size it proportionally too
options.setSizeMeasureType(MeasureType.Percents);
options.setWidth(10);  // 10% of page width
options.setHeight(5);  // 5% of page height

// Add some breathing room with margins
Padding margins = new Padding();
margins.setLeft(1);
margins.setTop(1);
margins.setRight(1);
options.setMargin(margins);
```

**لماذا النسب المئوية مهمة:** تخيّل أنك توقع مستندات A4 ونماذج بحجم قانوني. باستخدام التموضع القائم على النسبة، يتوسع الباركود تلقائيًا ليظهر متناسقًا في كلا الحالتين. استخدام قيم بكسل ثابتة سيجعل الباركود صغيرًا جدًا على المستندات الكبيرة أو كبيرًا جدًا على الصغيرة.

**مثال واقعي:** على صفحة A4 (595 × 842 نقطة)، سيكون الباركود بعرض 10% حوالي 60 نقطة. على صفحة قانونية (612 × 1008 نقطة)، سيكون العرض ~61 نقطة — متناسق تلقائيًا.

### الخطوة 4: توقيع وحفظ المستند (كيفية إضافة الباركود إلى PDF)

حان الوقت لتطبيق التوقيع وحفظ العمل:

```java
String outputFilePath = "YOUR_OUTPUT_DIRECTORY/SignWithPercents/sample_signed.pdf";
signature.sign(outputFilePath, options);
```

**ملاحظة هامة:** يجب أن يكون دليل الإخراج موجودًا قبل تشغيل الكود. لا يقوم GroupDocs بإنشاء الأدلة المتداخلة تلقائيًا، لذا أنشئها مسبقًا أو تعامل مع ذلك في الكود:

```java
Path outputPath = Paths.get(outputFilePath);
Files.createDirectories(outputPath.getParent());
signature.sign(outputFilePath, options);
```

**ماذا لو حدث خطأ؟** غلف الكود بكتلة try‑catch:

```java
try {
    signature.sign(outputFilePath, options);
    System.out.println("PDF signed successfully at: " + outputFilePath);
} catch (Exception e) {
    System.err.println("Signing failed: " + e.getMessage());
    e.printStackTrace();
}
```

## اختيار نوع الباركود المناسب لاحتياجاتك (code128 pdf barcode)

يدعم GroupDocs عدة صيغ للباركود، واختيار الصيغة الصحيحة مهم. إليك مقارنة عملية:

**Code128 (اختيارنا الافتراضي):**
- **الأفضل لـ:** بيانات مختلطة حرفية رقمية (مثل "INV2024-001")  
- **السعة:** حتى 128 حرف ASCII  
- **لماذا يفوز:** مدمج، مدعوم على نطاق واسع، يتعامل مع الحروف والأرقام  
- **متى تستخدمه:** عندما تحتاج إلى مرونة ولا تعرف نوع البيانات التي ستشفّرها  

**Code39:**
- **الأفضل لـ:** رموز حرفية رقمية بسيطة  
- **السعة:** 43 حرفًا (A‑Z، 0‑9، وبعض الرموز)  
- **لماذا تفكر فيه:** غالبًا ما تدعم الماسحات القديمة هذا النوع بشكل أفضل  
- **متى تستخدمه:** عند العمل مع أنظمة قديمة أو عندما تكون البساطة أهم من كثافة البيانات  

**QR Code:**
- **الأفضل لـ:** كميات كبيرة من البيانات (روابط URL، JSON)  
- **السعة:** حتى 3 KB من البيانات  
- **لماذا هو قوي:** يمكنه تخزين هياكل بيانات معقدة، ويتضمن تصحيح الأخطاء  
- **متى تستخدمه:** عندما تحتاج إلى تضمين بيانات منظمة أو روابط URL  

**EAN/UPC:**
- **الأفضل لـ:** تعريف المنتجات  
- **السعة:** رموز رقمية ثابتة الطول (8‑13 رقمًا)  
- **متى تستخدمه:** إذا كنت تعمل في مجال التجزئة أو أنظمة المخزون  

**دليل اتخاذ القرار السريع:**  
- تحتاج حروفًا وأرقامًا؟ → Code128  
- أرقام فقط، أبسط؟ → Code39  
- بيانات كثيرة أو روابط؟ → QR Code  
- رموز منتجات تجزئة؟ → EAN/UPC  

## الأخطاء الشائعة وكيفية تجنبها

إليك المشكلات التي يواجهها المطورون غالبًا (لتجنبها):

### المشكلة 1: تموضع الباركود غير صحيح

**العَرَض:** يظهر الباركود في مواقع غير متوقعة أو يُقَصّ.

**الأسباب الشائعة:**
- استخدام قيم بكسل على أحجام صفحات مختلفة  
- نسيان أن إحداثيات PDF تبدأ من الزاوية السفلية اليسرى، وليس العلوية اليسرى  
- الهوامش تدفع المحتوى خارج المنطقة المرئية  

**الحل:**  
استخدم دائمًا التموضع القائم على النسبة المئوية للاتساق:
```java
options.setLocationMeasureType(MeasureType.Percents);
options.setLeft(5);  // 5% from left works on any page width
```

### المشكلة 2: نص الباركود غير قابل للقراءة

**العَرَض:** يظهر النص المشفر لكن الماسحات لا تستطيع قراءته.

**الأسباب:**  
- باركود صغير جدًا بالنسبة لطول البيانات  
- نوع الترميز غير مناسب للبيانات  
- دقة منخفضة أو تباين ضعيف  

**الحل:**  
طابق حجم الباركود مع طول البيانات. بالنسبة لـ Code128 مع 10‑15 حرفًا، استهدف على الأقل 8‑10% من عرض الصفحة:
```java
options.setWidth(10);  // Give it room to breathe
options.setHeight(5);  // Maintain proper aspect ratio
```

### المشكلة 3: استثناءات مسار الملف

**العَرَض:** `FileNotFoundException` أو أخطاء مماثلة.

**الأسباب:**  
- مسارات Windows ثابتة بشرطة مائلة عكسية واحدة  
- دليل الإخراج غير موجود  
- مشاكل أذونات الملف  

**الحل:**  
استخدم الشرطات المائلة الأمامية (تعمل في كل مكان) وأنشئ الأدلة مسبقًا:
```java
String filePath = "documents/sample.pdf";  // Works on Windows, Mac, Linux
Files.createDirectories(Paths.get("output/signed"));
```

### المشكلة 4: مشاكل الذاكرة مع ملفات PDF الكبيرة

**العَرَض:** أخطاء نفاد الذاكرة عند معالجة مستندات ضخمة.

**الحل:**  
أغلق كائن `Signature` عند الانتهاء لتحرير الموارد:
```java
try (Signature signature = new Signature(filePath)) {
    signature.sign(outputFilePath, options);
} // Automatically closes and releases memory
```

## اختبار تنفيذ الباركود الخاص بك

قبل النشر، تأكد من أن الباركود يعمل فعليًا. إليك قائمة فحص عملية:

### 1. اختبار الفحص البصري
افتح PDF الموقع وتحقق من:
- هل الباركود مرئي ومتموضع بشكل صحيح؟  
- هل يبدو حادًا (ليس ضبابيًا أو بكسليًا)؟  
- هل هناك مساحة بيضاء كافية حوله؟

### 2. اختبار المسح
استخدم تطبيق ماسح باركود على هاتفك (مثل “Barcode Scanner” أو “QR & Barcode Reader”) للتحقق من:
- قدرة الماسح على قراءة الباركود  
- تطابق البيانات المفكوكة مع ما تم تشفيره  
- عمله من زوايا ومسافات مختلفة

### 3. اختبار عبر الأنظمة
افتح PDF على أجهزة مختلفة:
- Windows (Adobe Reader، Chrome)  
- macOS (Preview، Chrome)  
- الأجهزة المحمولة (iOS، Android)  

تأكد من أن الباركود يُعرض بشكل صحيح في جميع الحالات.

### 4. اختبار آلي
إليك كود اختبار بسيط يمكنك تشغيله:

```java
import org.junit.Test;
import static org.junit.Assert.*;

public class BarcodeSignatureTest {
    
    @Test
    public void testBarcodeSigning() {
        String testPdf = "test-data/sample.pdf";
        String output = "test-output/signed.pdf";
        
        try (Signature signature = new Signature(testPdf)) {
            BarcodeSignOptions options = new BarcodeSignOptions("TEST123");
            options.setEncodeType(BarcodeTypes.Code128);
            
            signature.sign(output, options);
            
            // Verify output file exists
            assertTrue(new File(output).exists());
            
            // Verify file size increased (signature was added)
            long originalSize = new File(testPdf).length();
            long signedSize = new File(output).length();
            assertTrue(signedSize > originalSize);
            
        } catch (Exception e) {
            fail("Signing should not throw exception: " + e.getMessage());
        }
    }
}
```

## حالات الاستخدام الواقعية لتوقيعات الباركود

نستعرض أين يبرز هذا الأسلوب في الأنظمة الإنتاجية:

### 1. توليد الشهادات والتحقق منها
**السيناريو:** تبني منصة تدريب تصدر شهادات إكمال.  
**التنفيذ:** أنشئ معرف شهادة فريد (مثل “CERT‑2024‑00123”) وادمجه كباركود Code128 في الزاوية السفلية اليمنى. يتيح مسح الباركود لواجهة API استرجاع تفاصيل الشهادة فورًا، مما يلغي الحاجة للإدخال اليدوي.

### 2. أنظمة تتبع الفواتير
**السيناريو:** شركتك تعالج آلاف الفواتير شهريًا.  
**التنفيذ:** أضف رقم الفاتورة وتاريخ الاستحقاق كرمز QR موضعًا بحيث يمكن لمعدات المسح قراءته بسهولة. يمكن للأنظمة الآلية فرز الفواتير دون تدخل بشري، مما يقلل الوقت من ساعات إلى دقائق.

### 3. إدارة العقود القانونية
**السيناريو:** مكتب محاماة يحتاج لتتبع إصدارات العقود وتعديلاتهم.  
**التنفيذ:** كل نسخة من العقد تحصل على معرف باركود فريد يتضمن رقم العقد، رقم الإصدار، وتاريخ التوقيع. يتيح المسح أثناء عمليات التدقيق استرجاع تاريخ الإصدار الكامل تلقائيًا.

### 4. أمان السجلات الطبية
**السيناريو:** مستشفى يرغب بمنع الوصول غير المصرح به إلى السجلات.  
**التنفيذ:** دمج معرف المريض وتوقيت إنشاء السجل في باركود. لا يمكن للأجهزة غير الموثوقة فك تشفيره، وكل عملية مسح تُسجل في سجل تدقيق للامتثال.

## نصائح تحسين الأداء

عند توقيع عدد كبير من ملفات PDF، يصبح الأداء مهمًا. إليك بعض النصائح للحفاظ على السلاسة:

### استراتيجية المعالجة الدفعية
بدلاً من توقيع مستند واحد في كل مرة، عالجها دفعةً:

```java
List<String> pdfFiles = Arrays.asList("doc1.pdf", "doc2.pdf", "doc3.pdf");

for (String pdfFile : pdfFiles) {
    try (Signature signature = new Signature(pdfFile)) {
        BarcodeSignOptions options = createBarcodeOptions(); // Reuse options
        signature.sign(getOutputPath(pdfFile), options);
    }
}
```

**لماذا يساعد ذلك:** إعادة استخدام كائن الخيارات وإغلاق الموارد بشكل صحيح يمنع تسرب الذاكرة.

### إدارة الذاكرة
لملفات PDF ضخمة (أكثر من 50 MB):
- عالجها تسلسليًا بدلاً من تحميل عدة ملفات في آنٍ واحد  
- استخدم try‑with‑resources لضمان التنظيف  
- راقب حجم الكومة واضبط معلمات JVM إذا لزم الأمر: `-Xmx2g`

### استراتيجية التخزين المؤقت
إذا كنت توقع بنفس الباركود مرارًا:

```java
// Create options once, reuse many times
BarcodeSignOptions templateOptions = createStandardBarcodeOptions();

// For each document, clone and customize
BarcodeSignOptions documentOptions = templateOptions.clone();
documentOptions.setText(uniqueDocumentId);
```

## متى تستخدم توقيعات الباركود (ومتى لا تستخدمها)

**السيناريوهات المثالية:**
- تحتاج إلى معرّفات مستندات قابلة للقراءة آليًا  
- سيتم مسح المستندات أو معالجتها تلقائيًا  
- تريد تتبعًا مقاومًا للعبث دون شهادات رقمية  
- لديك بنية تحتية للباركود موجودة مسبقًا  

**ليس مثاليًا عندما:**
- تحتاج إلى توقيعات رقمية قانونية (استخدم الشهادات الرقمية بدلاً منها)  
- سيُعرض المستند فقط على البشر (قد يكفي علامة مائية نصية)  
- تعمل على مستندات صغيرة جدًا حيث سيهيمن الباركود على الصفحة  
- تتطلب المتطلبات الأمنية تشفيرًا (الباركود مرئي وقابل للمسح من قبل أي شخص)  

**هل يمكن دمج الأسلوبين؟** بالتأكيد! تستخدم العديد من الأنظمة كلًا من توقيعات الباركود للتتبع وتوقيعات رقمية للشرعية القانونية.

## الأسئلة المتكررة

**س: هل يمكنني استخدام أنواع باركود مختلفة في نفس PDF؟**  
ج: نعم! استدعِ `signature.sign()` عدة مرات مع `BarcodeSignOptions` مختلفة لكل نوع باركود. فقط تأكد من عدم تداخلها.

**س: كيف أتعامل مع الباركود الذي يحتوي على أحرف خاصة؟**  
ج: يدعم Code128 معظم أحرف ASCII. للبيانات Unicode أو المعقدة، انتقل إلى QR Code—فهو يدعم ترميز UTF‑8.

**س: ما الحد الأقصى للبيانات التي يمكن تخزينها في باركود Code128؟**  
ج: نظريًا حتى 128 حرفًا، لكن قابلية القراءة تتدهور بشكل كبير فوق 30‑40 حرفًا. للحمولات الأكبر، استخدم QR Code.

**س: هل سيزيد حجم ملف PDF بشكل ملحوظ بإضافة الباركود؟**  
ج: لا بشكل ملحوظ—الباركودات رسومات متجهية، عادةً تضيف 5‑20 KB فقط لكل باركود حسب الحجم والتعقيد.

**س: هل يمكنني تدوير الباركود أو وضعه عموديًا؟**  
ج: نعم! استخدم `options.setRotationAngle(90)` لتدوير الباركود، وهو مفيد للتموضع على الهوامش.

**س: كيف أجعل الباركود يظهر في كل صفحة من PDF متعدد الصفحات؟**  
ج: كرّر العملية عبر الصفحات باستخدام `PagesSetup` لتحديد الصفحات التي تريد توقيعها.

**س: ماذا أفعل إذا لم يستطع ماسح الباركود قراءة الباركود المُولد؟**  
ج: أولًا، تأكد من أن الماسح يدعم نوع الباركود المختار. ثم زِد حجم الباركود—معظم مشاكل القراءة تنجم عن أشرطة صغيرة جدًا. استهدف عرضًا لا يقل عن 1 إنش (2.54 سم) لضمان قراءة موثوقة.

## موارد إضافية

**التوثيق:**  
- [GroupDocs.Signature for Java Docs](https://docs.groupdocs.com/signature/java/)  
- [API Reference Guide](https://reference.groupdocs.com/signature/java/)  

**التنزيلات والترخيص:**  
- [Download Latest Version](https://releases.groupdocs.com/signature/java/)  
- [Free Trial Access](https://releases.groupdocs.com/signature/java/)  
- [Get Temporary License](https://purchase.groupdocs.com/temporary-license/)  
- [Purchase Full License](https://purchase.groupdocs.com/buy)  

**المجتمع والدعم:**  
- [Support Forum](https://forum.groupdocs.com/c/signature/) - مجتمع نشط مع مهندسي GroupDocs  

---

**آخر تحديث:** 2026-03-06  
**تم الاختبار مع:** GroupDocs.Signature 23.12 (Java)  
**المؤلف:** GroupDocs