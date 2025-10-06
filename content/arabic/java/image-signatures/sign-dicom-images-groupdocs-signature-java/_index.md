---
"date": "2025-05-08"
"description": "تعرّف على كيفية توقيع صور DICOM بأمان باستخدام GroupDocs.Signature لـ Java. عزّز أمان المستندات بتضمين رموز الاستجابة السريعة (QR) والبيانات الوصفية."
"title": "توقيع صور DICOM باستخدام رموز QR والبيانات الوصفية باستخدام GroupDocs.Signature لـ Java"
"url": "/ar/java/image-signatures/sign-dicom-images-groupdocs-signature-java/"
"weight": 1
type: docs
---
# كيفية توقيع صور DICOM باستخدام رموز الاستجابة السريعة والبيانات الوصفية باستخدام GroupDocs.Signature لـ Java

## مقدمة

في ظل التطور السريع لقطاع الرعاية الصحية الرقمية، تُعدّ إدارة بيانات المرضى بأمان أمرًا بالغ الأهمية. يرشدك هذا البرنامج التعليمي إلى كيفية تطبيق حل فعّال باستخدام GroupDocs.Signature لجافا لتوقيع صور التصوير الرقمي والاتصالات في الطب (DICOM) باستخدام رموز الاستجابة السريعة والبيانات الوصفية. تضمن هذه الميزات الموثوقية، وتُحسّن إمكانية التتبع، وتحافظ على الامتثال من خلال تضمين معلومات حيوية مباشرةً في الصور الطبية.

### ما سوف تتعلمه:
- كيفية دمج GroupDocs.Signature لـ Java في مشروعك.
- عملية توقيع صور DICOM باستخدام رموز QR.
- إضافة بيانات تعريف XMP لتعزيز أمان المستندات.
- استرجاع التوقيعات والتحقق منها والبحث عنها داخل ملفات DICOM.
- إنشاء معاينات لصور DICOM الموقعة.

لنبدأ! قبل أن نبدأ، تأكد من تجهيز كل ما يلزم لمتابعتنا بسلاسة.

## المتطلبات الأساسية

لتنفيذ ميزات GroupDocs.Signature بشكل فعال، تأكد من تلبية المتطلبات الأساسية التالية:

### المكتبات والتبعيات المطلوبة
- **GroupDocs.Signature لـ Java**:ستحتاج إلى الإصدار 23.12 أو إصدار أحدث من هذه المكتبة.

### متطلبات إعداد البيئة
- **مجموعة تطوير جافا (JDK)**:تأكد من تثبيت JDK على نظامك.
- **بيئة تطوير متكاملة**:استخدم بيئة تطوير متكاملة مثل IntelliJ IDEA أو Eclipse.

### متطلبات المعرفة الأساسية
فهم أساسي لـ:
- برمجة جافا ومبادئ البرمجة الكائنية التوجه.
- أدوات بناء Maven أو Gradle لإدارة التبعيات.

## إعداد GroupDocs.Signature لـ Java

لبدء استخدام GroupDocs.Signature، عليك إضافتها كاعتمادية في مشروعك. إليك كيفية القيام بذلك باستخدام أدوات بناء مختلفة:

### مافن
أضف المقطع التالي إلى ملفك `pom.xml` ملف:
```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

### جرادل
قم بتضمين هذا في `build.gradle` ملف:
```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

### التحميل المباشر
بدلاً من ذلك، يمكنك تنزيل الإصدار الأحدث من [GroupDocs.Signature لإصدارات Java](https://releases.groupdocs.com/signature/java/).

#### خطوات الحصول على الترخيص
1. **نسخة تجريبية مجانية**:اختبر الميزات من خلال الإصدار التجريبي المجاني لمدة محدودة.
2. **رخصة مؤقتة**:احصل على ترخيص مؤقت لاستكشاف الإمكانيات الكاملة.
3. **شراء**:قم بشراء اشتراك إذا كنت بحاجة إلى وصول طويل الأمد.

#### التهيئة والإعداد الأساسي

لتهيئة GroupDocs.Signature، قم بإنشاء مثيل لـ `Signature` فصل:
```java
import com.groupdocs.signature.Signature;

// تهيئة كائن التوقيع باستخدام المسار إلى ملف DICOM الخاص بك
Signature signature = new Signature(filePath);
```

## دليل التنفيذ

### توقيع صورة DICOM باستخدام رمز الاستجابة السريعة والبيانات الوصفية

#### ملخص
تتيح لك هذه الميزة توقيع صور DICOM باستخدام رمز الاستجابة السريعة QR وإضافة بيانات تعريف XMP، مما يعزز أمان المستندات.

#### الخطوة 1: إعداد خيارات إشارة رمز الاستجابة السريعة
```java
import com.groupdocs.signature.domain.Padding;
import com.groupdocs.signature.domain.enums.HorizontalAlignment;
import com.groupdocs.signature.domain.enums.VerticalAlignment;
import com.groupdocs.signature.domain.signatures.QrCodeSignOptions;

Padding padding = new Padding();
padding.setRight(5);
padding.setLeft(5);

QrCodeSignOptions options = new QrCodeSignOptions("Patient #36363393. R: No-Issues");
options.setAllPages(true);
options.setWidth(100);
options.setHeight(100);
options.setVerticalAlignment(VerticalAlignment.Bottom);
options.setHorizontalAlignment(HorizontalAlignment.Right);
options.setMargin(padding);
```
هنا، نقوم بتكوين مظهر رمز الاستجابة السريعة وموقعه على صورة DICOM.

#### الخطوة 2: إضافة بيانات تعريف XMP
```java
import com.groupdocs.signature.options.saveoptions.imagessaveoptions.DicomSaveOptions;
import com.groupdocs.signature.options.saveoptions.imagessaveoptions.DicomXmpEntry;
import com.groupdocs.signature.options.saveoptions.imagessaveoptions.DicomXmpType;

DicomSaveOptions dicomSaveOptions = new DicomSaveOptions();
List<DicomXmpEntry> xmpEntries = new ArrayList<>();
xmpEntries.add(new DicomXmpEntry(DicomXmpType.PatientName, "Patient #4"));
dicomSaveOptions.setXmpEntries(xmpEntries);
```
تضيف هذه القطعة بيانات وصفية إلى ملف DICOM، وتتضمن معلومات إضافية للمريض.

#### الخطوة 3: توقيع الوثيقة
```java
String outputFilePath = YOUR_OUTPUT_DIRECTORY + "/SignDicomImageAdvanced/" + fileName;
signature.sign(outputFilePath, options, dicomSaveOptions);
```
ال `sign` تكتب الطريقة رمز الاستجابة السريعة والبيانات الوصفية في ملف DICOM الخاص بك، وتحفظه في الموقع المحدد.

### استرداد معلومات صورة DICOM الموقعة

#### ملخص
استخراج بيانات XMP من صورة DICOM موقعة لأغراض التحقق أو التدقيق.
```java
import com.groupdocs.signature.domain.IDocumentInfo;
import com.groupdocs.signature.domain.signatures.MetadataSignature;

IDocumentInfo documentInfo = signature.getDocumentInfo();
for (MetadataSignature item : documentInfo.getMetadataSignatures()) {
    System.out.println(item.toString());
}
```
يسترجع هذا الكود ويطبع جميع توقيعات البيانات الوصفية المرتبطة بملف DICOM.

### التحقق من توقيع DICOM

#### ملخص
تأكد من وجود توقيع رمز الاستجابة السريعة QR في صورة DICOM الموقعة للتأكد من صحتها.
```java
import com.groupdocs.signature.domain.VerificationResult;
import com.groupdocs.signature.options.verify.QrCodeVerifyOptions;
import com.groupdocs.signature.domain.enums.TextMatchType;

QrCodeVerifyOptions verifyOptions = new QrCodeVerifyOptions();
verifyOptions.setAllPages(true);
verifyOptions.setText("Patient #36363393");
verifyOptions.setMatchType(TextMatchType.Contains);

VerificationResult result = signature.verify(verifyOptions);
if (result.isValid()) {
    System.out.println(filePath + " has successfully verified signatures!");
} else {
    System.out.println(filePath + " failed verification process.");
}
```
تضمن خطوة التحقق هذه أن رمز الاستجابة السريعة يتطابق مع المعايير المتوقعة، مما يؤكد سلامة المستند.

### البحث عن التوقيعات في DICOM الموقع

#### ملخص
قم بتحديد جميع توقيعات رمز الاستجابة السريعة (QR) داخل صورة DICOM الموقعة لمراجعتها أو تدقيقها.
```java
import com.groupdocs.signature.domain.signatures.QrCodeSignature;
import java.util.List;

List<QrCodeSignature> signatures = signature.search(QrCodeSignature.class);
for (QrCodeSignature qrCodeSignature : signatures) {
    System.out.println("QRCode signature found at page " +
        qrCodeSignature.getPageNumber() + ": " +
        qrCodeSignature.getEncodeType().getTypeName() + ": " +
        qrCodeSignature.getText());
}
```
تعتبر هذه الميزة مفيدة لمسح جميع توقيعات رمز الاستجابة السريعة (QR) داخل المستند، مما يوفر رؤية شاملة.

### إنشاء معاينة لـ DICOM الموقّع

#### ملخص
إنشاء معاينات لكل صفحة من صورة DICOM الموقعة، مما يسمح بالفحص البصري السريع دون فتح الملف بالكامل.
```java
import com.groupdocs.signature.options.PreviewOptions;
import java.io.File;
import java.io.FileOutputStream;
import java.nio.file.Paths;

PreviewOptions previewOption = new PreviewOptions(pageNumber -> {
    try {
        String pageFilePath = YOUR_OUTPUT_DIRECTORY + "/SignDicomImageAdvanced/image-" + pageNumber + ".jpg";
        return new FileOutputStream(Paths.get(pageFilePath).toFile());
    } catch (Exception e) {
        throw new RuntimeException(e.getMessage());
    }
});

signature.generatePreview(previewOption);
```
يؤدي هذا المقطع إلى إنشاء معاينات صور لكل صفحة، مما قد يكون مفيدًا للتحقق السريع أو المشاركة.

## التطبيقات العملية

يوفر GroupDocs.Signature for Java العديد من التطبيقات الواقعية:
- **التصوير الطبي**:قم بتوقيع وإدارة صور DICOM الخاصة بالمريض بشكل آمن باستخدام رموز QR والبيانات الوصفية.
- **إدارة الوثائق القانونية**:تعزيز صحة الوثائق والامتثال لها في الإجراءات القانونية.
- **الخدمات المالية**:تنفيذ التوقيعات الإلكترونية الآمنة على المستندات المالية الحساسة.