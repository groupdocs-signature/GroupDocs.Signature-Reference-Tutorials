---
"date": "2025-05-08"
"description": "تعرّف على كيفية تنفيذ توقيع رمز الاستجابة السريعة (QR) في جافا باستخدام GroupDocs.Signature. حسّن أمان المستندات، وضبط خيارات التوقيع، وطبّق تشفيرًا مخصصًا في تطبيقات جافا."
"title": "دليل توقيع رمز الاستجابة السريعة بلغة Java - تأمين مستنداتك باستخدام GroupDocs.Signature"
"url": "/ar/java/qr-code-signatures/java-qr-code-signing-groupdocs-signature/"
"weight": 1
---

# تنفيذ توقيع رمز الاستجابة السريعة Java باستخدام GroupDocs.Signature لـ Java

## مقدمة

عزز أمان مستنداتك الرقمية بتضمين رموز الاستجابة السريعة (QR codes) في تطبيقات جافا. يتيح لك استخدام GroupDocs.Signature لجافا ضمان صحة المستندات وإمكانية تتبعها بفعالية. سيرشدك هذا الدليل إلى كيفية إنشاء توقيعات بيانات مخصصة، وتكوين خيارات توقيع رموز الاستجابة السريعة (QR code)، وتأمين مستنداتك بتشفير قوي.

**ما سوف تتعلمه:**
- كيفية إنشاء فئة توقيع بيانات مخصصة باستخدام GroupDocs.Signature
- تكوين خيارات إشارة رمز الاستجابة السريعة في تطبيقات Java
- توقيع المستندات باستخدام رموز الاستجابة السريعة وتطبيق التشفير المخصص

دعنا نتعمق في المتطلبات الأساسية ونبدأ في دمج هذه الوظيفة في مشاريعك!

## المتطلبات الأساسية

قبل أن نبدأ، تأكد من إعداد المكتبات والتبعيات الضرورية في بيئة التطوير الخاصة بك.

### المكتبات والإصدارات المطلوبة

لتنفيذ GroupDocs.Signature لـ Java، قم بتضمين التبعية التالية:

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
implementation 'com.groupdocs:groupdocs-signation:23.12'
```

يمكنك أيضًا تنزيل الإصدار الأحدث مباشرةً من [GroupDocs.Signature لإصدارات Java](https://releases.groupdocs.com/signature/java/).

### متطلبات إعداد البيئة

- تأكد من تثبيت Java Development Kit (JDK) العامل.
- قم بإعداد بيئة التطوير المتكاملة (IDE)، مثل IntelliJ IDEA أو Eclipse.

### متطلبات المعرفة الأساسية

- فهم أساسي لبرمجة جافا والمفاهيم الموجهة للكائنات.
- المعرفة بكيفية التعامل مع التبعيات باستخدام Maven أو Gradle.

## إعداد GroupDocs.Signature لـ Java

للبدء، قم بإعداد GroupDocs.Signature في مشروعك من خلال اتباع تعليمات التثبيت أعلاه لتضمينه في تكوين البناء الخاص بك.

### خطوات الحصول على الترخيص

توفر GroupDocs خيارات ترخيص مختلفة:
- **نسخة تجريبية مجانية**:اختبار كافة الميزات دون قيود.
- **رخصة مؤقتة**:الحصول على ترخيص لأغراض التقييم.
- **شراء**:احصل على ترخيص كامل للاستخدام التجاري.

بعد التنزيل، قم بتهيئة GroupDocs.Signature على النحو التالي:

```java
import com.groupdocs.signature.Signature;

class InitializeGroupDocs {
    public static void main(String[] args) {
        Signature signature = new Signature("path/to/your/document");
        // بإمكانك الآن البدء في استخدام كائن التوقيع للعمل مع المستندات.
    }
}
```

## دليل التنفيذ

دعونا نقسم عملية التنفيذ إلى أقسام قابلة للإدارة، مع التركيز على الميزات الرئيسية.

### فئة توقيع البيانات المخصصة

#### ملخص
أنشئ فئة مخصصة لتخزين بيانات التوقيع، مثل المعرف، والمؤلف، وتاريخ التوقيع، وعوامل أخرى. هذا يضمن لك تضمين جميع البيانات الوصفية الضرورية في توقيعاتك.

#### التنفيذ خطوة بخطوة

**تعريف فئة DocumentSignatureData**

```java
import com.groupdocs.signature.domain.extensions.serialization.FormatAttribute;
import java.util.Date;
import java.math.BigDecimal;

class DocumentSignatureData {
    @FormatAttribute(propertyName = "SignID")
    public String ID; // معرف فريد للتوقيع
    
    public String getID() { return ID; }
    public void setID(String value) { ID = value; }
    
    @FormatAttribute(propertyName = "SAuth")
    public final String Author; // مؤلف الوثيقة
    
    public final String getAuthor() { return Author; }
    public final void setAuthor(String value) { Author = value; }
    
    @FormatAttribute(propertyName = "SDate", propertyFormat = "yyyy-MM-dd")
    public final Date Signed = new Date(); // تاريخ ووقت التوقيع
    
    public final Date getSigned() { return Signed; }
    public final void setSigned(Date value) { Signed = value; }
    
    @FormatAttribute(propertyName = "SDFact", propertyFormat = "N2")
    public final BigDecimal DataFactor = new BigDecimal(0.01); // عامل بيانات إضافي للتوقيع
    
    public final BigDecimal getDataFactor() { return DataFactor; }
    public final void setDataFactor(BigDecimal value) { DataFactor = value; }
}
```

**توضيح:**
- **سمة التنسيق**:يضيف تعليقات توضيحية إلى الخصائص لتخصيص التسلسل.
- **ملكيات**:التقط التفاصيل الأساسية مثل المعرف الفريد واسم المؤلف وتاريخ التوقيع وعامل البيانات.

### تكوين خيارات علامة رمز الاستجابة السريعة

#### ملخص
قم بتكوين خيارات علامة رمز الاستجابة السريعة QR لتحديد كيفية ظهور رموز QR الخاصة بك على المستندات، بما في ذلك الحجم والمحاذاة والحشو.

#### التنفيذ خطوة بخطوة

**تعريف فئة QrCodeSignOptionsConfig**

```java
import com.groupdocs.signature.domain.enums.HorizontalAlignment;
import com.groupdocs.signature.domain.enums.VerticalAlignment;
import com.groupdocs.signature.domain.qrcodes.QrCodeTypes;
import com.groupdocs.signature.domain.Padding;
import com.groupdocs.signature.options.sign.QrCodeSignOptions;

class QrCodeSignOptionsConfig {
    public static QrCodeSignOptions setupQrCodeSignOptions(DocumentSignatureData documentSignature) {
        QrCodeSignOptions options = new QrCodeSignOptions();
        
        // تسلسل كائن البيانات المخصص إلى رمز الاستجابة السريعة
        options.setData(documentSignature);
        
        // تحديد نوع رمز الاستجابة السريعة
        options.setEncodeType(QrCodeTypes.QR);
        
        // تكوين الحشو للمحاذاة
        Padding padding = new Padding();
        padding.setRight(10); // الحشو الأيمن بالبكسل
        padding.setBottom(10); // الحشو السفلي بالبكسل
        options.setMargin(padding);
        
        // تحديد حجم وموضع رمز الاستجابة السريعة
        options.setHeight(100);
        options.setWidth(100);
        options.setVerticalAlignment(VerticalAlignment.Bottom);
        options.setHorizontalAlignment(HorizontalAlignment.Right);
        
        return options;
    }
}
```

**توضيح:**
- **خيارات توقيع رمز الاستجابة السريعة**:تقوم بإدارة كيفية عرض رمز الاستجابة السريعة (QR)، بما في ذلك حجمه وموقعه.
- **حشوة**:ضبط المحاذاة داخل المستند.

### توقيع المستندات باستخدام رمز الاستجابة السريعة والتشفير المخصص

#### ملخص
اجمع بين رموز الاستجابة السريعة (QR) والتشفير المُخصّص لتوقيع المستندات بأمان. هذا يضمن سلامة البيانات وسريتها.

#### التنفيذ خطوة بخطوة

**توقيع مستند باستخدام رمز الاستجابة السريعة**

```java
import com.groupdocs.signature.Signature;
import com.groupdocs.signature.domain.extensions.encryption.IDataEncryption;
import com.groupdocs.signature.exception.GroupDocsSignatureException;

import java.util.UUID;

class SignDocumentWithQRCode {
    public static void signDocument(String filePath, String outputFilePath) throws Exception {
        try {
            Signature signature = new Signature(filePath);

            // استراتيجية تشفير XOR المخصصة
            IDataEncryption encryption = new CustomXOREncryption();

            // تكوين كائن بيانات توقيع المستند المخصص
            DocumentSignatureData documentSignature = new DocumentSignatureData();
            documentSignature.setID(UUID.randomUUID().toString());
            documentSignature.setAuthor(System.getenv("USERNAME"));
            documentSignature.setSigned(new Date());
            documentSignature.setDataFactor(new BigDecimal("11.22"));

            // إعداد خيارات رمز الاستجابة السريعة
            QrCodeSignOptions options = QrCodeSignOptionsConfig.setupQrCodeSignOptions(documentSignature);

            // تطبيق التشفير على البيانات داخل رمز الاستجابة السريعة
            options.setDataEncryption(encryption);

            // التوقيع على الوثيقة وحفظها
            signature.sign(outputFilePath, options);
        } catch (Exception e) {
            throw new GroupDocsSignatureException(e.getMessage());
        }
    }
}
```

**توضيح:**
- **تشفير XOR المخصص**:تنفيذ استراتيجية تشفير مخصصة لتأمين بيانات رمز الاستجابة السريعة.
- **معرف UUID**:يُنشئ معرفًا فريدًا لكل توقيع.