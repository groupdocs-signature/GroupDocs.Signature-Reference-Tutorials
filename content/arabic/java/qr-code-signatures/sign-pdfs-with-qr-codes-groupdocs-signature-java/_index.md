---
"date": "2025-05-08"
"description": "تعرّف على كيفية توقيع مستندات PDF بأمان باستخدام رموز الاستجابة السريعة (QR codes) باستخدام GroupDocs.Signature لجافا. يغطي هذا البرنامج التعليمي الإعداد والتنفيذ والتطبيقات العملية."
"title": "كيفية توقيع ملفات PDF باستخدام رموز الاستجابة السريعة (QR Codes) باستخدام GroupDocs.Signature لـ Java"
"url": "/ar/java/qr-code-signatures/sign-pdfs-with-qr-codes-groupdocs-signature-java/"
"weight": 1
type: docs
---
# كيفية توقيع مستندات PDF باستخدام رموز الاستجابة السريعة (QR Codes) باستخدام GroupDocs.Signature لـ Java

في عصرنا الرقمي، أصبح التوقيع الآمن على المستندات أكثر أهمية من أي وقت مضى. سواء كنتَ خبيرًا في مجال الأعمال أو فردًا يبحث عن مصادقة ملفاتك، فإن الأدوات المناسبة تُحدث فرقًا كبيرًا. سيرشدك هذا البرنامج التعليمي خلال استخدام **GroupDocs.Signature لـ Java** لتوقيع مستندات PDF باستخدام رموز QR التي تحتوي على بيانات معقدة، مثل كائنات Mailmark2D. سنغطي كل شيء، من إعداد بيئتك إلى تطبيق الميزات المتقدمة.

## ما سوف تتعلمه
- كيفية إعداد GroupDocs.Signature لـ Java
- إنشاء وتكوين رمز الاستجابة السريعة لتوقيع ملفات PDF
- استخدام كائن Mailmark2D لترميز البيانات المعقدة
- التطبيقات العملية لهذه الميزة في سيناريوهات العالم الحقيقي

هل أنت مستعد للبدء؟ لنبدأ بالمتطلبات الأساسية أولاً.

## المتطلبات الأساسية
قبل أن تبدأ، تأكد من أن لديك:
- **مجموعة تطوير جافا (JDK)**:الإصدار 8 أو أعلى.
- **بيئة التطوير المتكاملة (IDE)** مثل IntelliJ IDEA أو Eclipse.
- فهم أساسي لبرمجة Java وأدوات بناء Maven/Gradle.

### المكتبات والتبعيات المطلوبة
لاستخدام GroupDocs.Signature في Java، عليك تضمين المكتبة في مشروعك. إليك الطريقة:

**مافن:**
```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

**جرادل:**
```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

**التحميل المباشر:**  
بالنسبة لأولئك الذين لا يستخدمون مدير البناء، قم بتنزيل الإصدار الأحدث من [GroupDocs.Signature لإصدارات Java](https://releases.groupdocs.com/signature/java/).

### الحصول على الترخيص
توفر GroupDocs خيارات ترخيص مختلفة:
- **نسخة تجريبية مجانية**:ابدأ بإصدار تجريبي لاستكشاف الميزات.
- **رخصة مؤقتة**:الحصول على ترخيص مؤقت للاختبار الموسع.
- **شراء**:شراء ترخيص كامل للاستخدام الإنتاجي.

## إعداد GroupDocs.Signature لـ Java
بعد تجهيز بيئتك والمكتبة المُضمنة، شغّل GroupDocs.Signature. هذا الإعداد أساسي للوصول إلى جميع وظائفه:

```java
import com.groupdocs.signature.Signature;

class SetupGroupDocs {
    public static void main(String[] args) {
        Signature signature = new Signature("YOUR_DOCUMENT_DIRECTORY");
        // بإمكانك الآن استخدام "التوقيع" لتوقيع المستندات.
    }
}
```

## دليل التنفيذ
### توقيع المستند باستخدام رمز الاستجابة السريعة
#### ملخص
تتيح لك هذه الميزة إضافة رمز الاستجابة السريعة (QR) كتوقيع رقمي على مستندات PDF. سيحتوي رمز الاستجابة السريعة على بيانات معقدة مُرمَّزة في كائن Mailmark2D.

**الخطوة 1: استيراد الحزم المطلوبة**

```java
import com.groupdocs.signature.Signature;
import com.groupdocs.signature.domain.qrcodes.QrCodeTypes;
import com.groupdocs.signature.options.sign.QrCodeSignOptions;
```

**الخطوة 2: تعيين مسارات الملفات وتهيئة كائن التوقيع**
عيّن مسارات مستندك المصدر وملف الإخراج. قم بتهيئة `Signature` الكائن الذي يحتوي على المسار إلى ملف PDF الخاص بك:

```java
String filePath = "YOUR_DOCUMENT_DIRECTORY";
String outputFilePath = "YOUR_OUTPUT_DIRECTORY/SignWithQRCodeMailmark2DObject.pdf";

final Signature signature = new Signature(filePath);
```

**الخطوة 3: إنشاء خيارات إشارة رمز الاستجابة السريعة**
قم بتكوين رمز الاستجابة السريعة (QR) بإعدادات محددة مثل النوع والموضع والبيانات:

```java
QrCodeSignOptions options = new QrCodeSignOptions();
options.setEncodeType(QrCodeTypes.QR); // تعيين نوع رمز الاستجابة السريعة
options.setLeft(100); // إحداثيات X للوضع
options.setTop(100);  // إحداثيات Y للوضع
```

**الخطوة 4: توقيع الوثيقة**
تنفيذ عملية التوقيع وحفظ المستند الموقع:

```java
try {
    signature.sign(outputFilePath, options);
} finally {
    if (signature != null) signature.dispose();
}
```

### إنشاء كائن بيانات Mailmark2D
#### ملخص
يُستخدم كائن Mailmark2D لتشفير البيانات المعقدة داخل رمز الاستجابة السريعة. يوضح هذا القسم كيفية تكوين هذا الكائن.

**الخطوة 1: استيراد الحزم المطلوبة**

```java
import com.groupdocs.signature.domain.extensions.mailmark2d.Mailmark2D;
import com.groupdocs.signature.domain.extensions.mailmark2d.Mailmark2DType;
import com.groupdocs.signature.domain.extensions.serialization.DataMatrixEncodeMode;
```

**الخطوة 2: تهيئة وتكوين كائن Mailmark2D**
تعيين خصائص مختلفة لكائن Mailmark2D لتحديد البيانات المعقدة:

```java
Mailmark2D mailmark2D = new Mailmark2D();
mailmark2D.setUPUCountryID("JGB "); // معرف بلد الخدمة البريدية
mailmark2D.setInformationTypeID("0"); // معرف نوع المعلومات
mailmark2D.setClass("1"); // فئة معالجة البريد
mailmark2D.setSupplyChainID(123); // معرف سلسلة التوريد
mailmark2D.setItemID(1234); // معرف العنصر الفريد
mailmark2D.setDestinationPostCodeAndDPS("QWE1"); // الرمز البريدي للوجهة
mailmark2D.setRTSFlag("0"); // العودة إلى علم المرسل
mailmark2D.setReturnToSenderPostCode("QWE2"); // الرمز البريدي للعودة
mailmark2D.setDataMatrixType(Mailmark2DType.Type_7); // نوع مصفوفة البيانات
mailmark2D.setCustomerContentEncodeMode(DataMatrixEncodeMode.C40); // وضع الترميز
mailmark2D.setCustomerContent("CUSTOM"); // محتوى مخصص
```

## التطبيقات العملية
1. **المصادقة على الوثائق القانونية**:تأكد من توقيع المستندات القانونية والتحقق منها باستخدام رموز الاستجابة السريعة (QR).
2. **معالجة الفواتير**:قم بإرفاق رموز الاستجابة السريعة (QR) بالفواتير لتسهيل التتبع والتحقق.
3. **ملصقات الشحن**:استخدم رموز الاستجابة السريعة (QR code) الموجودة على ملصقات الشحن لتشفير معلومات التتبع التفصيلية.
4. **تذاكر الفعاليات**:تعزيز الأمان من خلال تضمين تفاصيل الحدث في رموز الاستجابة السريعة الموجودة على التذاكر.
5. **إدارة سلسلة التوريد**:تبسيط العمليات اللوجستية باستخدام بيانات Mailmark2D المرمزة برمز الاستجابة السريعة.

## اعتبارات الأداء
- قم بتحسين الأداء من خلال إدارة استخدام الذاكرة بشكل فعال، وخاصة عند التعامل مع ملفات PDF كبيرة الحجم.
- استخدم المعالجة غير المتزامنة إذا كنت تريد التكامل في تطبيقات الويب لتجنب عمليات الحظر.
- قم بتحديث GroupDocs.Signature بشكل منتظم للاستفادة من التحسينات وإصلاحات الأخطاء.

## خاتمة
باتباع هذا الدليل، ستتعلم كيفية توقيع مستندات PDF باستخدام رموز الاستجابة السريعة (QR codes) باستخدام GroupDocs.Signature لجافا. يمكن دمج هذه الميزة الفعّالة في مختلف مهام سير العمل لتعزيز أمان المستندات وتبسيط العمليات. لاستكشاف إمكانيات GroupDocs.Signature بشكل أكبر، جرّب تكوينات مختلفة أو دمجها مع أنظمة أخرى.

## قسم الأسئلة الشائعة
1. **هل يمكنني استخدام GroupDocs.Signature مجانًا؟**  
   نعم، يمكنك البدء بفترة تجريبية مجانية لاختبار ميزاته.
2. **ما هي أنواع المستندات التي يمكن توقيعها باستخدام هذه المكتبة؟**  
   بالإضافة إلى ملفات PDF، يمكنك توقيع الصور، ومستندات Word، وجداول بيانات Excel، والمزيد.
3. **كيف يمكنني استكشاف أخطاء التوقيع وإصلاحها؟**  
   تحقق من سجلات الأخطاء بحثًا عن رسائل محددة وتأكد من تكوين جميع التبعيات بشكل صحيح.
4. **هل يمكنني تخصيص مظهر رمز الاستجابة السريعة؟**  
   نعم، يمكنك تعديل الحجم والموضع والخصائص الأخرى باستخدام `QrCodeSignOptions`.
5. **هل من الممكن التوقيع على عدة مستندات في وقت واحد؟**  
   على الرغم من أن GroupDocs.Signature يتعامل مع مستند واحد في كل مرة، يمكنك برمجة معالجة الدفعات لتحقيق الكفاءة.

## موارد
- **التوثيق**: [GroupDocs.Signature Java Docs](https://docs.groupdocs.com/signature/java/)
- **مرجع واجهة برمجة التطبيقات**: [مرجع API لتوقيع GroupDocs](https://reference.groupdocs.com/signature/java/)
- **تحميل**: [إصدارات GroupDocs.Signature](https://releases.groupdocs.com/signature/java/)
- **شراء**: [شراء ترخيص GroupDocs](https://purchase.groupdocs.com/buy)
- **نسخة تجريبية مجانية**: [ابدأ تجربتك المجانية](https://releases.groupdocs.com/signature/java/)
- **رخصة مؤقتة**: [التقدم بطلب للحصول على رخصة مؤقتة](https://purchase.groupdocs.com/temporary-license/)
- **يدعم**: [منتدى GroupDocs](https://forum.groupdocs.com/c/signature/)

باستخدام هذه الموارد، يمكنك تعميق فهمك وتوسيع وظائف GroupDocs.Signature في تطبيقاتك. برمجة ممتعة!