---
"date": "2025-05-08"
"description": "تعلّم كيفية إنشاء توقيعات رمز الاستجابة السريعة (QR) آمنة وديناميكية في جافا باستخدام GroupDocs.Signature. سهّل توقيع المستندات."
"title": "إنشاء توقيعات رمز الاستجابة السريعة (QR Code) باستخدام GroupDocs.Signature for Java - دليل شامل"
"url": "/ar/java/qr-code-signatures/generate-qr-code-signatures-groupdocs-java/"
"weight": 1
---

# إنشاء توقيعات رمز الاستجابة السريعة (QR Code) باستخدام GroupDocs.Signature لـ Java

## مقدمة

في عصرنا الرقمي، يُعدّ تأمين المستندات أمرًا بالغ الأهمية. سواء كنت تتعامل مع عقود أو فواتير أو اتفاقيات، فإن ضمان دقة التوقيعات وأمانها قد يكون أمرًا صعبًا. **GroupDocs.Signature لـ Java** يقدم حلاً قويًا لتبسيط إضافة التوقيعات الرقمية إلى مستنداتك.

سيرشدك هذا البرنامج التعليمي إلى كيفية إنشاء توقيعات رمز الاستجابة السريعة (QR Code) باستخدام GroupDocs.Signature لجافا، مما يعزز الأمان والمرونة في تضمين بيانات إضافية في مستنداتك. باتباعك لهذا الدليل، ستتعلم:

- إعداد وتكوين GroupDocs.Signature لـ Java.
- تقنيات لإنشاء توقيعات رمز الاستجابة السريعة (QR) بإعدادات محاذاة دقيقة.
- تكوين خيارات معاينة التوقيع للحصول على عرض شامل للمستند الموقع.
- إنشاء تدفقات التوقيع لضمان التعامل السلس مع الملفات.

لنبدأ بتطبيق هذه الوظائف في تطبيقات جافا. أولاً، لنتناول بعض المتطلبات الأساسية للبدء بسلاسة.

## المتطلبات الأساسية

قبل استخدام GroupDocs.Signature لـ Java، تأكد من استيفاء المتطلبات التالية:

- **المكتبات والتبعيات**: ثبّت المكتبات اللازمة. استخدم Maven أو Gradle لإدارة التبعيات.
  
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

- **إعداد البيئة**:تأكد من أن لديك بيئة تطوير Java مع JDK و IDE مثل IntelliJ IDEA أو Eclipse.

- **متطلبات المعرفة الأساسية**:إن المعرفة بمفاهيم برمجة Java أمر ضروري، بالإضافة إلى فهم التوقيعات الرقمية.

بعد ذلك، سنقوم بإرشادك خلال إعداد GroupDocs.Signature لـ Java في بيئة مشروعك.

## إعداد GroupDocs.Signature لـ Java

لبدء استخدام GroupDocs.Signature لـ Java، اتبع الخطوات التالية:

1. **إضافة التبعية**:استخدم Maven أو Gradle لتضمين التبعية كما هو موضح أعلاه.
2. **الحصول على الترخيص**:
   - ابدأ بإصدار تجريبي مجاني عن طريق تنزيله من [إصدارات GroupDocs](https://releases.groupdocs.com/signature/java/).
   - للاستخدام الموسع، فكر في شراء ترخيص أو التقدم بطلب للحصول على ترخيص مؤقت من خلالهم [صفحة الشراء](https://purchase.groupdocs.com/buy).
3. **التهيئة الأساسية**:
   قم بتهيئة المكتبة في تطبيق Java الخاص بك لبدء استخدام ميزاتها.

   ```java
   import com.groupdocs.signature.Signature;
   
   // تهيئة كائن التوقيع
   Signature signature = new Signature("sample.pdf");
   ```

بعد تهيئة GroupDocs.Signature لجافا، أصبحتَ جاهزًا لإنشاء توقيعات رموز الاستجابة السريعة. لنبدأ بالتفاصيل.

## دليل التنفيذ

### إنشاء توقيع رمز الاستجابة السريعة

يتضمن إنشاء توقيعات رمز الاستجابة السريعة (QR Code) عدة خطوات رئيسية. تساعد كل خطوة على تخصيص كيفية تضمين البيانات وعرضها في مستنداتك.

#### ملخص
تُعد توقيعات رموز الاستجابة السريعة (QR Code) متعددة الاستخدامات؛ فهي تتيح لك تضمين معلومات معقدة، مثل العناوين وعناوين URL والبيانات الثنائية، مباشرةً في مستنداتك. لنرَ كيفية إنشاء هذه التوقيعات بإعدادات محاذاة محددة باستخدام GroupDocs.Signature لـ Java.

#### التنفيذ خطوة بخطوة

##### 1. تكوين خيارات رمز الاستجابة السريعة
ابدأ بإعداد `QrCodeSignOptions` الكائن. هنا يمكنك تحديد نوع رمز الاستجابة السريعة والبيانات التي يجب أن يحتوي عليها.

```java
import com.groupdocs.signature.domain.enums.HorizontalAlignment;
import com.groupdocs.signature.domain.enums.VerticalAlignment;
import com.groupdocs.signature.domain.extensions.serialization.Address;
import com.groupdocs.signature.domain.qrcodes.QrCodeTypes;
import com.groupdocs.signature.options.sign.QrCodeSignOptions;

QrCodeSignOptions signOptions = new QrCodeSignOptions();
signOptions.setEncodeType(QrCodeTypes.QR);

// إعداد البيانات باستخدام كائن العنوان
Address address = new Address();
address.setStreet("221B Baker Street");
address.setCity("London");
address.setState("NW");
address.setZIP("NW16XE");
address.setCountry("England");

signOptions.setData(address);
```
**توضيح**:هنا، قمنا بتعيين نوع رمز الاستجابة السريعة إلى قياسي `QR` واملأه بمعلومات العنوان. يضمن هذا التغليف للبيانات توافر التفاصيل المهمة بسهولة داخل مستندك.

##### 2. محاذاة رمز الاستجابة السريعة
اضبط إعدادات المحاذاة للتحكم في مكان ظهور رمز الاستجابة السريعة (QR) على صفحة المستند.

```java
signOptions.setHorizontalAlignment(HorizontalAlignment.Left);
signOptions.setVerticalAlignment(VerticalAlignment.Center);
signOptions.setWidth(100);
signOptions.setHeight(100);
```
**توضيح**:خيارات المحاذاة (`HorizontalAlignment` و `VerticalAlignment`) يسمح لك بتحديد موضع رمز الاستجابة السريعة بدقة. تضمن هذه الخطوة أن يكون رمز الاستجابة السريعة جميلاً من الناحية الجمالية وموضعاً استراتيجياً لمسح مثالي.

##### 3. تعيين الهوامش
قم بتحديد الهوامش حول رمز الاستجابة السريعة (QR) للتأكد من أنه لا يلامس حواف المستند، وهو أمر قد يكون مهمًا لموثوقية المسح الضوئي.

```java
signOptions.setMargin(new Padding(10));
```
**توضيح**:يتم تعيين الهامش هنا باستخدام `Padding`، مما يضمن وجود مسافة بين رمز الاستجابة السريعة (QR) وحافة المستند، مما يحسن إمكانية المسح الضوئي.

### تكوين خيارات معاينة التوقيع

يتيح لك إعداد خيارات المعاينة تصوّر شكل التوقيع قبل إتمامه. إليك الطريقة:

#### ملخص
تعد إعدادات المعاينة ضرورية للتحقق من مظهر توقيعاتك داخل المستندات.

#### التنفيذ خطوة بخطوة

##### 1. إنشاء وتكوين خيارات المعاينة
يستخدم `PreviewSignatureOptions` لتحديد كيفية معاينة التوقيع.

```java
import com.groupdocs.signature.options.PreviewSignatureOptions;
import com.groupdocs.signature.options.preview.PreviewFormats;
import java.util.UUID;

PreviewSignatureOptions previewOption = new PreviewSignatureOptions(signOptions);
previewOption.setSignatureId(UUID.randomUUID().toString());
previewOption.setPreviewFormat(PreviewFormats.JPEG);
```
**توضيح**: ال `PreviewSignatureOptions` تم تكوين الكائن لإنشاء معاينة JPEG لرمز الاستجابة السريعة. مُعرِّف فريد لكل توقيع (`UUID`) يضمن لك إمكانية تتبع وإدارة التوقيعات المتعددة بكفاءة.

### إنشاء تدفق التوقيع

يضمن إنشاء تدفق حفظ المستند الموقع أو إرساله بشكل صحيح.

#### ملخص
يتيح إنشاء مجرى ملف التعامل بسلاسة مع المستند الموقع، مما يضمن تخزينه بشكل صحيح في الدلائل المحددة.

#### التنفيذ خطوة بخطوة

##### 1. تحديد دليل الإخراج وإنشاء التدفق
تأكد من وجود دليل الإخراج قبل إنشاء التدفق لتجنب الأخطاء أثناء كتابة الملف.

```java
import java.io.FileOutputStream;
import java.io.OutputStream;
import java.nio.file.Files;
import java.nio.file.Path;
import java.nio.file.Paths;

public OutputStream generateSignatureStream(PreviewSignatureOptions previewOptions) {
    try {
        Path path = Paths.get("YOUR_OUTPUT_DIRECTORY");
        if (!Files.exists(path)) {
            Files.createDirectories(path);
        }
        
        // إنشاء مجرى إخراج لحفظ المستند الموقّع
        return new FileOutputStream(path.resolve("signedDocument.pdf"));
    } catch (Exception e) {
        e.printStackTrace();
        return null;
    }
}
```
**توضيح**تتحقق هذه الطريقة من وجود الدليل المحدد، وتُنشئه عند الحاجة، ثم تُرجع تدفق إخراج ملف لحفظ مستندك. تضمن معالجة الأدلة تخزين المستندات الموقعة بشكل منظم.

## خاتمة

باتباع هذا الدليل، ستتعلم كيفية إنشاء توقيعات رمز الاستجابة السريعة (QR) باستخدام GroupDocs.Signature لجافا، مما يعزز الأمان والمرونة في تضمين بيانات إضافية في مستنداتك. باتباع هذه الخطوات، يمكنك تطبيق وظائف التوقيع الرقمي بثقة في تطبيقات جافا.

لمزيد من الاستكشاف، فكر في تجربة أنواع مختلفة من التوقيعات أو استكشاف الميزات الأخرى التي تقدمها GroupDocs.Signature لـ Java.