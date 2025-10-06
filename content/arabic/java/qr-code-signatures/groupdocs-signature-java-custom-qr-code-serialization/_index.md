---
"date": "2025-05-08"
"description": "تعرّف على كيفية تنفيذ تسلسل رمز الاستجابة السريعة (QR) المخصص مع التشفير في ملفات PDF باستخدام GroupDocs.Signature لجافا. وفّر الحماية لمستنداتك بكفاءة."
"title": "تنفيذ التسلسل والتشفير المخصص لرمز الاستجابة السريعة في ملفات PDF باستخدام GroupDocs.Signature لـ Java"
"url": "/ar/java/qr-code-signatures/groupdocs-signature-java-custom-qr-code-serialization/"
"weight": 1
type: docs
---
# كيفية تنفيذ تسلسل رمز الاستجابة السريعة (QR-Code) المخصص والتشفير في ملفات PDF باستخدام GroupDocs.Signature لـ Java

## مقدمة

في العصر الرقمي، يُعدّ التوقيع الآمن للمستندات أمرًا بالغ الأهمية للحفاظ على سلامة البيانات وصحتها. استخدم GroupDocs.Signature لجافا، وهي مكتبة فعّالة مصممة لتبسيط إضافة التوقيعات إلى المستندات. سيرشدك هذا البرنامج التعليمي إلى كيفية تنفيذ تسلسل رمز الاستجابة السريعة (QR) المخصص مع التشفير في ملفات PDF باستخدام GroupDocs.Signature لجافا.

**ما سوف تتعلمه:**
- كيفية إعداد وتكوين GroupDocs.Signature لـ Java
- تنفيذ التسلسل المخصص لتوقيعات رمز الاستجابة السريعة (QR Code)
- تشفير البيانات التسلسلية داخل رمز الاستجابة السريعة
- تطبيق هذه الميزات لتأمين مستنداتك

قبل أن نتعمق في التنفيذ، دعونا نتأكد من أن لديك كل ما تحتاجه للمتابعة.

### المتطلبات الأساسية

لاستخدام هذا البرنامج التعليمي بشكل فعال، تأكد من تلبية المتطلبات الأساسية التالية:

1. **المكتبات والتبعيات المطلوبة:**
   - GroupDocs.Signature لإصدار Java 23.12 أو أعلى
   - Maven أو Gradle لإدارة التبعيات (اختياري)

2. **متطلبات إعداد البيئة:**
   - مجموعة تطوير Java (JDK) مثبتة على جهازك
   - فهم أساسي لبرمجة جافا

3. **المتطلبات المعرفية:**
   - المعرفة بلغة جافا ومفاهيم البرمجة الموجهة للكائنات
   - المعرفة الأساسية للعمل مع ملفات PDF في Java

## إعداد GroupDocs.Signature لـ Java

للبدء، تحتاج إلى إعداد مكتبة GroupDocs.Signature في بيئة مشروعك.

### تثبيت Maven

إذا كنت تستخدم Maven، فأضف التبعية التالية إلى ملفك `pom.xml` ملف:

```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

### تثبيت Gradle

بالنسبة لمستخدمي Gradle، قم بتضمين هذا السطر في `build.gradle` ملف:

```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

### التحميل المباشر

بدلاً من ذلك، يمكنك تنزيل الإصدار الأحدث مباشرةً من [GroupDocs.Signature لإصدارات Java](https://releases.groupdocs.com/signature/java/).

#### خطوات الحصول على الترخيص
- **نسخة تجريبية مجانية:** ابدأ بتنزيل النسخة التجريبية لاختبار ميزاتها.
- **رخصة مؤقتة:** يمكنك طلب ترخيص مؤقت إذا لزم الأمر، مما يسمح لك بتقييم المنتج دون أي قيود.
- **شراء:** للاستخدام طويل الأمد، فكر في شراء ترخيص كامل.

بمجرد التثبيت، قم بتشغيل GroupDocs.Signature في مشروعك:

```java
import com.groupdocs.signature.Signature;

public class SetupGroupDocs {
    public static void main(String[] args) {
        Signature signature = new Signature("YOUR_DOCUMENT_DIRECTORY/sample.pdf");
        // الكود الخاص بك هنا...
    }
}
```

## دليل التنفيذ

الآن، دعنا نتعمق في تنفيذ التسلسل والتشفير المخصص لرمز الاستجابة السريعة (QR) باستخدام GroupDocs.Signature لـ Java.

### فئة التسلسل المخصصة لتوقيعات رمز الاستجابة السريعة (QR)

#### ملخص

تتضمن هذه الميزة إنشاء فئة تتولى تسلسل البيانات الوصفية في توقيع رمز الاستجابة السريعة. `DocumentSignatureData` تخزن الفئة السمات مثل المعرف والمؤلف وتاريخ التوقيع وعامل البيانات.

```java
import com.groupdocs.signature.domain.extensions.serialization.FormatAttribute;
import java.math.BigDecimal;
import java.util.Date;

class DocumentSignatureData {
    @FormatAttribute(propertyName = "SignID")
    public String ID;

    public void setID(String value) { 
        this.ID = value; 
    }

    @FormatAttribute(propertyName = "SAuth")
    public String author;

    public void setAuthor(String value) {
        this.author = value;
    }

    @FormatAttribute(propertyName = "SDate", propertyFormat = "yyyy-MM-dd")
    public Date signed = new Date();

    public void setSigned(Date value) {
        this.signed = value;
    }

    @FormatAttribute(propertyName = "SDFact", propertyFormat = "N2")
    public BigDecimal dataFactor = new BigDecimal(0.01);

    public void setDataFactor(BigDecimal value) {
        this.dataFactor = value;
    }
}
```

#### توضيح
- **صفات:** ال `@FormatAttribute` تشير التعليقات التوضيحية إلى كيفية تسلسل كل سمة في رمز الاستجابة السريعة QR.
  - **بطاقة تعريف**:معرف فريد للتوقيع.
  - **مؤلف**:الشخص الذي وقع على الوثيقة.
  - **تاريخ التوقيع**:العلامة الزمنية لتوقيع المستند.
  - **عامل البيانات**:البيانات الرقمية الإضافية المرتبطة بالتوقيع.

### توقيع رمز الاستجابة السريعة (QR) مع التسلسل والتشفير المخصصين للبيانات

#### ملخص

يوضح هذا القسم كيفية توقيع مستند باستخدام رمز الاستجابة السريعة QR الذي يتضمن بيانات تسلسلية مخصصة وتشفيرًا.

```java
import com.groupdocs.signature.Signature;
import com.groupdocs.signature.domain.Padding;
import com.groupdocs.signature.domain.enums.HorizontalAlignment;
import com.groupdocs.signature.domain.enums.VerticalAlignment;
import com.groupdocs.signature.domain.extensions.encryption.IDataEncryption;
import com.groupdocs.signature.domain.qrcodes.QrCodeTypes;
import com.groupdocs.signature.exception.GroupDocsSignatureException;
import com.groupdocs.signature.options.sign.QrCodeSignOptions;
import java.io.File;
import java.math.BigDecimal;
import java.util.Date;
import java.util.UUID;

class SignWithQRCodeCustomSerialization {
    String filePath = "YOUR_DOCUMENT_DIRECTORY/sample.pdf"; 
    String outputFilePath = new File("YOUR_OUTPUT_DIRECTORY", "SignedQRCodeCustomSerialization.pdf").getPath();

    public void signDocument() throws Exception {
        Signature signature = new Signature(filePath);

        // قم بتنفيذ منطق التشفير المخصص لك هنا
        IDataEncryption encryption = new CustomXOREncryption();

        DocumentSignatureData documentSignature = new DocumentSignatureData();
        documentSignature.setID(UUID.randomUUID().toString());
        documentSignature.setAuthor(System.getenv("USERNAME")); 
        documentSignature.setSigned(new Date());
        documentSignature.setDataFactor(new BigDecimal("11.22"));

        QrCodeSignOptions options = new QrCodeSignOptions();
        options.setData(documentSignature);
        options.setEncodeType(QrCodeTypes.QR);
        options.setDataEncryption(encryption);

        // تكوين المحاذاة والمظهر
        options.setHeight(100);
        options.setWidth(100);
        options.setVerticalAlignment(VerticalAlignment.Bottom);
        options.setHorizontalAlignment(HorizontalAlignment.Right);
        
        Padding padding = new Padding();
        padding.setRight(10);
        padding.setBottom(10);
        options.setMargin(padding);

        signature.sign(outputFilePath, options);
    }
}
```

#### توضيح
- **التشفير المخصص:** قم بتنفيذ منطق التشفير الخاص بك في `CustomXOREncryption` أو استخدم أي طريقة أخرى للتنفيذ `IDataEncryption`.
- **خيارات التوقيع:** قم بتكوين مظهر رمز الاستجابة السريعة (QR) ومحاذاته باستخدام خيارات مثل الارتفاع والعرض والحشو وما إلى ذلك.
- **عملية التوقيع:** ال `signature.sign()` تطبق الطريقة توقيع رمز الاستجابة السريعة QR على المستند.

### نصائح استكشاف الأخطاء وإصلاحها

- تأكد من تكوين جميع التبعيات بشكل صحيح في أداة البناء الخاصة بك (Maven/Gradle).
- تأكد من أن مسارات الملفات الخاصة بمستندات الإدخال والإخراج دقيقة.
- تأكد من أن منطق التشفير المخصص الخاص بك تم تنفيذه ودمجه بشكل صحيح.

## التطبيقات العملية

وفيما يلي بعض التطبيقات الواقعية لهذه الميزة:

1. **توقيع الوثيقة القانونية:** قم بتوقيع العقود بشكل آمن مع البيانات الوصفية المضمنة في رموز الاستجابة السريعة لضمان صحتها.
2. **معالجة الفواتير:** قم بإضافة التوقيعات المشفرة تلقائيًا إلى الفواتير لمزيد من الأمان وإمكانية التتبع.
3. **تتبع الخدمات اللوجستية:** استخدم المستندات الموقعة لتتبع الشحنات، وتضمين معرفات فريدة وطوابع زمنية داخل رموز الاستجابة السريعة (QR).
4. **الشهادات الأكاديمية:** تضمين معلومات الطالب بشكل آمن في الشهادات الرقمية باستخدام توقيع رمز الاستجابة السريعة