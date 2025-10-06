---
"date": "2025-05-08"
"description": "تعرّف على كيفية توقيع الصور بأمان باستخدام GroupDocs.Signature لجافا، بما في ذلك توقيع رمز الاستجابة السريعة وخيارات حفظ الصور المتقدمة. مثالي لرجال الأعمال والمطورين."
"title": "إتقان توقيع الصور وتحسينها باستخدام GroupDocs.Signature لـ Java"
"url": "/ar/java/image-signatures/groupdocs-signature-java-image-optimization/"
"weight": 1
type: docs
---
# إتقان توقيع الصور وتحسينها باستخدام GroupDocs.Signature لـ Java

في عالمنا الرقمي اليوم، يُعدّ التوقيع الآمن للمستندات أمرًا بالغ الأهمية. سواءً كنتَ خبيرًا في مجال الأعمال تُوثّق العقود أو فردًا يحمي الصور، فإنّ امتلاك إمكانيات توقيع فعّالة أمرٌ بالغ الأهمية. **GroupDocs.Signature لـ Java** يوفر ميزات فعّالة لإنشاء توقيعات رموز الاستجابة السريعة (QR) وتحسين خيارات حفظ الصور بسلاسة. سيرشدك هذا البرنامج التعليمي إلى كيفية استخدام هذه الوظائف لإدارة مستندات فعّالة.

### ما سوف تتعلمه:
- إنشاء توقيعات رمز الاستجابة السريعة على الصور.
- تكوين خيارات الحفظ المتقدمة بالتنسيقات BMP، وGIF، وJPEG، وPNG، وTIFF.
- تنفيذ GroupDocs.Signature لـ Java في مشاريعك.
- التطبيقات الواقعية لهذه الميزات.

دعونا نتأكد من إعداد كل شيء بشكل صحيح!

## المتطلبات الأساسية

قبل الخوض في تفاصيل التنفيذ، تأكد من أن لديك:

### المكتبات والتبعيات المطلوبة
لاستخدام GroupDocs.Signature في Java، قم بدمج مكتبتها في مشروعك. إليك كيفية تضمينها بناءً على نظام البناء الخاص بك:

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

بدلا من ذلك، يمكنك [تنزيل أحدث إصدار مباشرة](https://releases.groupdocs.com/signature/java/) إذا كان إعداد مشروعك يتطلب ذلك.

### متطلبات إعداد البيئة
- تم تثبيت Java Development Kit (JDK) وتكوينه بشكل صحيح.
- بيئة تطوير متكاملة مثل IntelliJ IDEA أو Eclipse لتطوير التعليمات البرمجية.

### متطلبات المعرفة الأساسية
يُنصح بفهم أساسيات برمجة جافا. ستكون معرفة أدوات بناء Maven/Gradle مفيدة، ولكنها ليست ضرورية، حيث سنرشدك خلال عملية الإعداد.

## إعداد GroupDocs.Signature لـ Java

لبدء العمل مع GroupDocs.Signature، اتبع الخطوات التالية:

1. **تثبيت التبعية**:أضف التبعية المناسبة إلى `pom.xml` أو `build.gradle` الملف كما هو موضح أعلاه.
2. **الحصول على الترخيص**:
   - احصل على [نسخة تجريبية مجانية](https://releases.groupdocs.com/signature/java/) لاستكشاف كامل قدرات المكتبة.
   - للاستخدام الموسع، فكر في شراء ترخيص أو التقدم بطلب للحصول على ترخيص مؤقت من خلال [صفحة الشراء](https://purchase.groupdocs.com/buy).

### التهيئة والإعداد الأساسي
بعد إعداد بيئتك، قم بتهيئة GroupDocs.Signature عن طريق إنشاء مثيل لـ `Signature` الصف. إليك الطريقة:

```java
import com.groupdocs.signature.Signature;

public class SignatureSetup {
    public static void main(String[] args) throws Exception {
        // قم بالتهيئة باستخدام مسار الملف إلى دليل المستند الخاص بك
        String filePath = "YOUR_DOCUMENT_DIRECTORY/sampleImage.jpg";
        Signature signature = new Signature(filePath);
        
        System.out.println("GroupDocs.Signature initialized successfully!");
    }
}
```

## دليل التنفيذ

الآن بعد أن حصلت على الإعداد اللازم، دعنا ننتقل إلى تنفيذ ميزات محددة باستخدام GroupDocs.Signature لـ Java.

### إنشاء توقيعات رمز الاستجابة السريعة على الصور

#### ملخص
يرشدك هذا القسم إلى كيفية إنشاء توقيع رمز الاستجابة السريعة (QR) على مستند صورة. وهو مفيد بشكل خاص لتضمين البيانات الوصفية أو المعلومات مباشرةً على الصور بطريقة آمنة.

##### الخطوة 1: تهيئة كائن التوقيع
أولاً، قم بإنشاء `Signature` كائن يشير إلى ملفك المستهدف.
```java
String filePath = "YOUR_DOCUMENT_DIRECTORY/sampleImage.jpg";
Signature signature = new Signature(filePath);
```

##### الخطوة 2: إعداد خيارات إشارة رمز الاستجابة السريعة
حدّد خيارات التوقيع باستخدام رمز الاستجابة السريعة. ستُحدّد تفاصيل مثل المحتوى والموقع.

```java
import com.groupdocs.signature.domain.qrcodes.QrCodeTypes;
import com.groupdocs.signature.options.sign.QrCodeSignOptions;

QrCodeSignOptions signOptions = new QrCodeSignOptions("JohnSmith");
signOptions.setEncodeType(QrCodeTypes.QR);
signOptions.setLeft(100);  // الموضع من الهامش الأيسر
signOptions.setTop(100);   // الموضع من الهامش العلوي
```

##### الخطوة 3: توقيع الوثيقة
وأخيرًا، قم بتطبيق توقيع رمز الاستجابة السريعة (QR) على مستندك.

```java
signature.sign("output/imageWithQR.jpg", signOptions);
System.out.println("QR Code Signature Applied Successfully!");
```

### تكوين خيارات حفظ الصورة المتقدمة

#### تكوين خيارات حفظ BMP
يتيح لك هذا التكوين تخصيص كيفية حفظ الصور بتنسيق BMP. اضبط مستوى الضغط والدقة والمعلمات الأخرى حسب الحاجة.

```java
import com.groupdocs.signature.options.saveoptions.imagessaveoptions.BmpSaveOptions;
import com.groupdocs.signature.domain.enums.BitmapCompression;

BmpSaveOptions bmpSaveOptions = new BmpSaveOptions();
bmpSaveOptions.setAddMissingExtenstion(true);
bmpSaveOptions.setCompression(BitmapCompression.Rgb);
bmpSaveOptions.setHorizontalResolution(7);
bmpSaveOptions.setVerticalResolution(7);
bmpSaveOptions.setBitsPerPixel(16);
bmpSaveOptions.setOverwriteExistingFiles(true);
```

#### تكوين خيارات حفظ GIF
عند حفظ الصور بتنسيق GIF، يمكنك التحكم في جوانب مثل لون الخلفية وفرز الألوان.

```java
import com.groupdocs.signature.options.saveoptions.imagessaveoptions.GifSaveOptions;

GifSaveOptions gifSaveOptions = new GifSaveOptions();
gifSaveOptions.setBackgroundColorIndex((byte) 2);
gifSaveOptions.setColorResolution((byte) 7);
gifSaveOptions.setDoPaletteCorrection(true);
gifSaveOptions.setTrailer(true);
gifSaveOptions.setInterlaced(false);
gifSaveOptions.setPaletteSorted(true);
gifSaveOptions.setPixelAspectRatio((byte) 24);
gifSaveOptions.setAddMissingExtenstion(true);
```

#### تكوين خيارات حفظ JPEG
قم بتحسين حفظ صور JPEG الخاصة بك باستخدام الإعدادات الخاصة بالجودة ونوع اللون ووضع الضغط.

```java
import com.groupdocs.signature.options.saveoptions.imagessaveoptions.JpegSaveOptions;
import com.groupdocs.signature.domain.enums.JpegCompressionColorMode;
import com.groupdocs.signature.domain.enums.JpegCompressionMode;
import com.groupdocs.signature.domain.enums.JpegRoundingMode;

JpegSaveOptions jpegSaveOptions = new JpegSaveOptions();
jpegSaveOptions.setAddMissingExtenstion(true);
jpegSaveOptions.setBitsPerChannel((byte) 8);
jpegSaveOptions.setColorType(JpegCompressionColorMode.Rgb);
jpegSaveOptions.setComment("signed jpeg file");
jpegSaveOptions.setCompressionType(JpegCompressionMode.Lossless);
jpegSaveOptions.setQuality(100);
jpegSaveOptions.setSampleRoundingMode(JpegRoundingMode.Extrapolate);
```

#### تكوين خيارات حفظ PNG
مع PNG، يمكنك تحديد عمق البت ومستويات الضغط لتناسب احتياجاتك.

```java
import com.groupdocs.signature.options.saveoptions.imagessaveoptions.PngSaveOptions;
import com.groupdocs.signature.domain.enums.PngColorType;
import com.groupdocs.signature.domain.enums.PngFilterType;

PngSaveOptions pngSaveOptions = new PngSaveOptions();
pngSaveOptions.setBitDepth((byte) 8);
pngSaveOptions.setColorType(PngColorType.Grayscale);
pngSaveOptions.setCompressionLevel(9);
pngSaveOptions.setFilterType(PngFilterType.Adaptive);
pngSaveOptions.setProgressive(true);
pngSaveOptions.setAddMissingExtenstion(true);
```

#### تكوين خيارات حفظ TIFF
بالنسبة لصور TIFF، يمكنك تحديد التنسيق والإعدادات الأخرى ذات الصلة.

```java
import com.groupdocs.signature.options.saveoptions.imagessaveoptions.TiffSaveOptions;
import com.groupdocs.signature.domain.enums.TiffFormat;

TiffSaveOptions tiffSaveOptions = new TiffSaveOptions();
tiffSaveOptions.setExpectedTiffFormat(TiffFormat.TiffNoCompressionBw);
tiffSaveOptions.setAddMissingExtenstion(true);
```

## التطبيقات العملية

### حالات الاستخدام في العالم الحقيقي
1. **توقيع العقد**:قم بتضمين رموز الاستجابة السريعة (QR code) في صور العقد للتحقق السريع.
2. **مواد التسويق**:أضف المعلومات الخاصة بالعلامة التجارية مباشرةً على المواد الترويجية باستخدام رموز الاستجابة السريعة (QR code).
3. **أرشفة الصور**:تحسين إعدادات حفظ الصورة للحفاظ على الجودة وتقليل حجم الملف أثناء الأرشفة.