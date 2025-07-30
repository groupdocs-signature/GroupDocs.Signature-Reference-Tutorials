---
"date": "2025-05-08"
"description": "تعرّف على كيفية تأمين بيانات تعريف الصور باستخدام التشفير باستخدام GroupDocs.Signature لجافا. تأكّد من سلامة البيانات وصحتها من خلال إرشادات خطوة بخطوة."
"title": "تنفيذ توقيع وتشفير بيانات الصورة في Java باستخدام GroupDocs.Signature"
"url": "/ar/java/metadata-signatures/groupdocs-signature-java-image-metadata-encryption/"
"weight": 1
---

# تنفيذ توقيع بيانات الصورة باستخدام التشفير في Java باستخدام GroupDocs.Signature

## مقدمة

في عالمنا الرقمي اليوم، يُعدّ تأمين المعلومات الحساسة ضمن بيانات تعريف المستندات أمرًا بالغ الأهمية. سواءً تعلق الأمر بعقود عمل سرية أو صور هوية شخصية، فإن الحفاظ على سلامة بيانات تعريف الصور ودقتها يُساعد على منع الوصول غير المصرح به والتلاعب بها. **GroupDocs.Signature لـ Java** يوفر حلاً قويًا لتوقيع وتشفير بيانات الصورة بشكل آمن.

يرشدك هذا البرنامج التعليمي إلى كيفية تنفيذ توقيع بيانات تعريف الصور مع التشفير في جافا باستخدام ميزات GroupDocs.Signature الفعّالة. باتباع هذه الخطوات، ستتمكن من دمج هذه الوظيفة بفعالية في تطبيقات جافا.

**ما سوف تتعلمه:**
- توقيع بيانات تعريف المستند باستخدام GroupDocs.Signature لـ Java
- تنفيذ توقيعات الكائنات المخصصة باستخدام التشفير
- إعداد بيئة آمنة باستخدام التشفير بالمفتاح المتماثل

## المتطلبات الأساسية

قبل البدء، تأكد من استيفاء المتطلبات الأساسية التالية:

### المكتبات والتبعيات المطلوبة:
- **GroupDocs.Signature لـ Java**:تأكد من أن لديك الإصدار 23.12 أو إصدار أحدث.

### متطلبات إعداد البيئة:
- قم بتثبيت Java Development Kit (JDK) على جهازك.
- استخدم بيئة التطوير المتكاملة (IDE) مثل IntelliJ IDEA، أو Eclipse، أو NetBeans.

### المتطلبات المعرفية:
- فهم أساسيات برمجة جافا.
- المعرفة بـ Maven أو Gradle لإدارة التبعيات.

## إعداد GroupDocs.Signature لـ Java

لاستخدام GroupDocs.Signature في مشروعك، قم بتضمين التبعيات الضرورية على النحو التالي:

### استخدام Maven
أضف هذا إلى `pom.xml` ملف:
```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

### استخدام Gradle
قم بتضمين هذا في `build.gradle` ملف:
```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

### التحميل المباشر
بدلاً من ذلك، قم بتنزيل الإصدار الأحدث من [GroupDocs.Signature لإصدارات Java](https://releases.groupdocs.com/signature/java/).

#### خطوات الحصول على الترخيص
- **نسخة تجريبية مجانية**:ابدأ بإصدار تجريبي لاستكشاف الميزات.
- **رخصة مؤقتة**:تقدم بطلب لإجراء اختبارات مكثفة إذا لزم الأمر.
- **شراء**:الحصول على ترخيص للاستخدام الإنتاجي من [مجموعة المستندات](https://purchase.groupdocs.com/buy).

## التهيئة والإعداد الأساسي

إليك كيفية تهيئة GroupDocs.Signature في تطبيق Java الخاص بك:

```java
import com.groupdocs.signature.Signature;

public class InitializeSignature {
    public static void main(String[] args) {
        // المسار إلى المستند
        String filePath = "path/to/your/document.jpg";
        
        // إنشاء مثيل جديد للتوقيع
        Signature signature = new Signature(filePath);

        System.out.println("GroupDocs.Signature initialized successfully.");
    }
}
```

## دليل التنفيذ

### الميزة: توقيع البيانات الوصفية مع الكائن المخصص

#### ملخص
تتيح هذه الميزة توقيع بيانات التعريف الخاصة بالصورة باستخدام كائن مخصص وتشفيرها لمزيد من الأمان، مما يضمن أن الأطراف المصرح لها فقط يمكنها الوصول إلى البيانات التعريفية أو تعديلها.

#### التنفيذ خطوة بخطوة

##### 1. قم بتحديد فئة بيانات توقيع المستند الخاص بك
إنشاء فئة لتخزين معلومات البيانات الوصفية الخاصة بك:

```java
import java.math.BigDecimal;
import java.util.Date;

class DocumentSignatureData {
    private String ID;
    private String Author;
    private Date Signed = new Date();
    private BigDecimal DataFactor = new BigDecimal(0.01);

    public String getID() { return ID; }
    public void setID(String value) { ID = value; }

    @FormatAttribute(propertyName = "SignID")
    public final String getAuthor() { return Author; }
    public final void setAuthor(String value) { Author = value; }

    @FormatAttribute(propertyName = "SAuth")
    public final Date getSigned() { return Signed; }
    public final void setSigned(Date value) { Signed = value; }

    @FormatAttribute(propertyName = "SDate", propertyFormat = "yyyy-MM-dd")
    public final BigDecimal getDataFactor() { return DataFactor; }
    public final void setDataFactor(BigDecimal value) { DataFactor = value; }
}
```

##### 2. تنفيذ منطق التوقيع
إليك كيفية توقيع البيانات الوصفية باستخدام التشفير:

```java
import com.groupdocs.signature.Signature;
import com.groupdocs.signature.domain.extensions.encryption.IDataEncryption;
import com.groupdocs.signature.domain.extensions.encryption.SymmetricAlgorithmType;
import com.groupdocs.signature.domain.extensions.encryption.SymmetricEncryption;
import com.groupdocs.signature.domain.signatures.metadata.ImageMetadataSignature;
import com.groupdocs.signature.exception.GroupDocsSignatureException;
import com.groupdocs.signature.options.sign.MetadataSignOptions;

import java.io.File;
import java.nio.file.Paths;
import java.util.UUID;

public class SignMetadataWithCustomObject {
    // تهيئة مسارات الملفات باستخدام العناصر النائبة
    String filePath = "YOUR_DOCUMENT_DIRECTORY/SampleImage.jpg";
    String outputFilePath = new File("YOUR_OUTPUT_DIRECTORY", 
                                       "SignedImageWithCustomMetadata/SampleImage_signed.jpg").getPath();

    public void run() throws Exception {
        Signature signature = new Signature(filePath);

        // إعداد المفتاح وعبارة المرور للتشفير
        String key = "1234567890";
        String salt = "1234567890";
        IDataEncryption encryption = new SymmetricEncryption(
            SymmetricAlgorithmType.Rijndael, key, salt);

        MetadataSignOptions options = new MetadataSignOptions();
        DocumentSignatureData documentSignature = new DocumentSignatureData();
        
        // تعيين خصائص البيانات الوصفية المخصصة
        documentSignature.setID(UUID.randomUUID().toString());
        documentSignature.setAuthor(System.getenv("USERNAME"));
        documentSignature.setSigned(new Date());
        documentSignature.setDataFactor(new BigDecimal("11.22"));

        ImageMetadataSignature mdDocument = new ImageMetadataSignature(41996, documentSignature);
        mdDocument.setDataEncryption(encryption);

        // إضافة توقيعات البيانات الوصفية إلى الخيارات
        options.getSignatures().add(mdDocument);

        signature.sign(outputFilePath, options);
    }
}
```

#### خيارات تكوين المفاتيح
- **التشفير المتماثل**:يستخدم خوارزمية Rijndael للتشفير.
- **خيارات توقيع البيانات الوصفية**:يقوم بتكوين عملية التوقيع ويحدد البيانات الوصفية التي سيتم التوقيع عليها.

##### نصائح استكشاف الأخطاء وإصلاحها
- تأكد من أن مسارات الملفات الخاصة بك صحيحة ويمكن الوصول إليها.
- تأكد من أن متغير البيئة `USERNAME` تم ضبطه بشكل صحيح.
- تأكد من أن إصدار مكتبة GroupDocs.Signature يتطابق مع تبعيات الكود لديك.

### الميزة: توقيع البيانات الوصفية مع التشفير

#### ملخص
ترتكز هذه الميزة على تشفير توقيعات البيانات الوصفية لحماية المعلومات الحساسة داخل ملفات الصور.

#### التنفيذ خطوة بخطوة
##### 1. تنفيذ منطق التشفير
إليك كيفية توقيع البيانات الوصفية باستخدام التشفير:
```java
import com.groupdocs.signature.Signature;
import com.groupdocs.signature.domain.extensions.encryption.IDataEncryption;
import com.groupdocs.signature.domain.extensions.encryption.SymmetricAlgorithmType;
import com.groupdocs.signature.domain.extensions.encryption.SymmetricEncryption;
import com.groupdocs.signature.exception.GroupDocsSignatureException;
import com.groupdocs.signature.options.sign.MetadataSignOptions;

import java.io.File;
import java.nio.file.Paths;
import java.util.UUID;

public class SignMetadataWithEncryption {
    // تهيئة مسارات الملفات باستخدام العناصر النائبة
    String filePath = "YOUR_DOCUMENT_DIRECTORY/SampleImage.jpg";
    String outputFilePath = new File("YOUR_OUTPUT_DIRECTORY", 
                                       "SignedImageWithEncryption/SampleImage_signed.jpg").getPath();

    public void run() throws Exception {
        Signature signature = new Signature(filePath);

        // إعداد المفتاح وعبارة المرور للتشفير
        String key = "1234567890";
        String salt = "1234567890";
        IDataEncryption encryption = new SymmetricEncryption(
            SymmetricAlgorithmType.Rijndael, key, salt);

        MetadataSignOptions options = new MetadataSignOptions();
        DocumentSignatureData documentSignature = new DocumentSignatureData();
        
        // تعيين خصائص البيانات الوصفية المخصصة
        documentSignature.setID(UUID.randomUUID().toString());
        documentSignature.setAuthor(System.getenv("USERNAME"));
        documentSignature.setSigned(new Date());
        documentSignature.setDataFactor(new BigDecimal("11.22"));

        ImageMetadataSignature mdDocument = new ImageMetadataSignature(41996, documentSignature);
        mdDocument.setDataEncryption(encryption);

        // إضافة توقيعات البيانات الوصفية إلى الخيارات
        options.getSignatures().add(mdDocument);

        signature.sign(outputFilePath, options);
    }
}
```