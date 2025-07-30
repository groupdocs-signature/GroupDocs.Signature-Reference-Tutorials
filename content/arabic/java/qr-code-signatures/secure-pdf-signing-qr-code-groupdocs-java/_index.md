---
"date": "2025-05-08"
"description": "تعرّف على كيفية تأمين ملفات PDF باستخدام تشفير رمز الاستجابة السريعة والتوقيعات الرقمية مع GroupDocs.Signature لجافا. عزّز أمان مستنداتك بفعالية."
"title": "تنفيذ توقيع PDF آمن باستخدام تشفير رمز الاستجابة السريعة في Java باستخدام GroupDocs.Signature"
"url": "/ar/java/qr-code-signatures/secure-pdf-signing-qr-code-groupdocs-java/"
"weight": 1
---

# كيفية تنفيذ توقيع PDF آمن باستخدام تشفير رمز الاستجابة السريعة في Java باستخدام GroupDocs.Signature

في عصرنا الرقمي، يُعدّ تأمين المعلومات الحساسة في المستندات أمرًا بالغ الأهمية. وقد جعل تزايد التهديدات الإلكترونية تشفير البيانات جزءًا أساسيًا من إدارة المستندات. يرشدك هذا الدليل إلى كيفية تنفيذ توقيع PDF آمن باستخدام تشفير رمز الاستجابة السريعة (QR code) مع GroupDocs.Signature لـ Java. بنهاية هذه المقالة، ستكون جاهزًا لدمج ميزات أمان قوية في تطبيقاتك.

## ما سوف تتعلمه:
- فهم تشفير البيانات المتماثل في جافا
- إنشاء فئة توقيع مخصصة
- تكوين توقيعات رمز الاستجابة السريعة (QR) باستخدام البيانات المخصصة والمحاذاة
- دمج GroupDocs.Signature لتوقيع PDF بشكل آمن

هل أنت مستعد للبدء؟ لنبدأ!

## المتطلبات الأساسية
قبل أن نبدأ، تأكد من أن لديك ما يلي:
- **مجموعة تطوير Java (JDK):** الإصدار 8 أو أعلى.
- **Maven أو Gradle:** لإدارة التبعيات. اختر بناءً على إعدادات مشروعك.
- **معرفة برمجة جافا:** فهم أساسي للبرمجة الكائنية التوجه في جافا.

## إعداد GroupDocs.Signature لـ Java
لبدء استخدام GroupDocs.Signature، ستحتاج إلى إضافتها كاعتمادية لمشروعك. توفر هذه المكتبة أدوات فعّالة لإدارة التوقيعات الرقمية وتشفير المستندات.

### إعداد Maven
أضف التبعية التالية إلى ملفك `pom.xml` ملف:
```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

### إعداد Gradle
بالنسبة لمستخدمي Gradle، قم بتضمين هذا في `build.gradle` ملف:
```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

### التحميل المباشر
بدلاً من ذلك، قم بتنزيل الإصدار الأحدث من [GroupDocs.Signature لإصدارات Java](https://releases.groupdocs.com/signature/java/).

### الحصول على الترخيص
يمكنك البدء بفترة تجريبية مجانية من GroupDocs.Signature لتقييم ميزاته. للاستخدام الممتد، يمكنك شراء ترخيص أو التقدم بطلب ترخيص مؤقت عبر موقعهم الإلكتروني.

## دليل التنفيذ
ينقسم هذا الدليل إلى أقسام رئيسية تتناول تشفير البيانات وإنشاء التوقيع المخصص وتكوين توقيع رمز الاستجابة السريعة QR.

### تشفير البيانات باستخدام خوارزمية متماثلة
يضمن تشفير بياناتك بقائها آمنة أثناء النقل والتخزين. إليك كيفية إعداد التشفير المتماثل باستخدام GroupDocs.Signature:

#### إعداد التشفير المتماثل
1. **استيراد الحزم الضرورية:**
   ```java
   import com.groupdocs.signature.domain.extensions.encryption.IDataEncryption;
   import com.groupdocs.signature.domain.extensions.encryption.SymmetricAlgorithmType;
   import com.groupdocs.signature.domain.extensions.encryption.SymmetricEncryption;
   ```
2. **تهيئة كائن التشفير:**
   استخدم مفتاحًا آمنًا وملحًا للتشفير. استبدل `"YOUR_SECURE_KEY"` مع مفاتيحك الخاصة.
   ```java
   String key = "YOUR_SECURE_KEY";
   String salt = "YOUR_SECURE_SALT";

   IDataEncryption encryption = new SymmetricEncryption(
       SymmetricAlgorithmType.Rijndael, 
       key, 
       salt
   );
   ```
   - **SymmetricAlgorithmType.Rijndael:** يحدد هذا نوع الخوارزمية المتماثلة التي يجب استخدامها.
   - **المفتاح والملح:** تأكد من أن هذه العناصر فريدة وآمنة لتطبيقك.

### فئة توقيع البيانات المخصصة
إنشاء فئة مخصصة يُمكّنك من إدارة خصائص التوقيع بفعالية. إليك الطريقة:

#### تعريف `DocumentSignatureData` فصل
```java
class DocumentSignatureData {
    private String ID;
    private String Author;
    private Date Signed = new Date();
    private BigDecimal DataFactor = new BigDecimal(0.01);

    public String getID() { return ID; }
    public void setID(String value) { ID = value; }

    public final String getAuthor() { return Author; }
    public final void setAuthor(String value) { Author = value; }

    public final Date getSigned() { return Signed; }
    public final void setSigned(Date value) { Signed = value; }

    public final BigDecimal getDataFactor() { return DataFactor; }
    public final void setDataFactor(BigDecimal value) { DataFactor = value; }
}
```
- **الهوية، المؤلف، التوقيع:** تخزن هذه الحقول بيانات التعريف الخاصة بالتوقيع.
- **عامل البيانات:** تحتوي على قيمة عددية ذات صلة بمنطق تطبيقك.

### خيارات توقيع رمز الاستجابة السريعة
تُقدّم رموز الاستجابة السريعة (QR) طريقةً مُدمجةً لتضمين المعلومات. جهّزها ببيانات مُخصّصة وتشفير مُخصّص.

#### إعداد توقيعات رمز الاستجابة السريعة (QR)
1. **تهيئة `Signature` هدف:**
   ```java
   import com.groupdocs.signature.Signature;
   
   Signature signature = new Signature("YOUR_DOCUMENT_DIRECTORY");
   ```
2. **تكوين خيارات رمز الاستجابة السريعة:**
   ```java
   import com.groupdocs.signature.domain.qrcodes.QrCodeTypes;
   import com.groupdocs.signature.options.sign.QrCodeSignOptions;
   import java.util.UUID;

   DocumentSignatureData documentSignature = new DocumentSignatureData();
   documentSignature.setID(UUID.randomUUID().toString());
   documentSignature.setAuthor(System.getenv("USERNAME"));
   documentSignature.setDataFactor(new BigDecimal("11.22"));

   QrCodeSignOptions options = new QrCodeSignOptions();
   options.setData(documentSignature);
   options.setEncodeType(QrCodeTypes.QR);
   options.setDataEncryption(encryption); // استخدم كائن التشفير
   options.setHeight(100);
   options.setWidth(100);
   options.setVerticalAlignment(com.groupdocs.signature.domain.enums.VerticalAlignment.Bottom);
   options.setHorizontalAlignment(com.groupdocs.signature.domain.enums.HorizontalAlignment.Right);

   import com.groupdocs.signature.domain.Padding;
   Padding padding = new Padding();
   padding.setRight(10);
   padding.setBottom(10);
   options.setMargin(padding);
   ```
   - **نوع الترميز:** يحدد تنسيق رمز الاستجابة السريعة.
   - **المحاذاة والهامش:** تخصيص كيفية ظهور رمز الاستجابة السريعة (QR) على المستند.

### مثال للاستخدام
لتوقيع مستند باستخدام الخيارات التي قمت بتكوينها:
```java
signature.sign("YOUR_OUTPUT_DIRECTORY/QRCodeEncryptedObject.pdf\