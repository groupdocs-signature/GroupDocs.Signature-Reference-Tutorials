---
"date": "2025-05-08"
"description": "تعرّف على كيفية تعزيز أمان المستندات من خلال تطبيق توقيعات رمز الاستجابة السريعة (QR) والتحقق منها في جافا باستخدام GroupDocs.Signature. اتبع هذا الدليل خطوة بخطوة لعملية توقيع آمنة."
"title": "تأمين مستنداتك - تنفيذ توقيعات رمز الاستجابة السريعة في Java باستخدام GroupDocs.Signature"
"url": "/ar/java/qr-code-signatures/qr-code-signatures-java-groupdocs/"
"weight": 1
---

# تأمين مستنداتك: تنفيذ توقيعات رمز الاستجابة السريعة في Java باستخدام GroupDocs.Signature

في ظلّ العالم الرقميّ الحالي، يُعدّ ضمان أمن المستندات، كالعقود والفواتير والمعلومات الشخصية الحساسة، أمرًا بالغ الأهمية. ومن الأساليب المبتكرة لتعزيز أمن المستندات وتبسيط عمليات التحقق، استخدام توقيعات رمز الاستجابة السريعة (QR). سيرشدك هذا البرنامج التعليمي إلى كيفية تطبيق توقيعات رمز الاستجابة السريعة (QR) والتحقق منها في مستنداتك بلغة جافا باستخدام GroupDocs.Signature.

## ما سوف تتعلمه
- كيفية توقيع المستندات باستخدام رموز الاستجابة السريعة (QR Codes)
- التحقق من المستندات الموقعة باستخدام رموز الاستجابة السريعة (QR Codes)
- البحث عن توقيعات رمز الاستجابة السريعة (QR Code) الموجودة داخل مستند
- تحديث وحذف توقيعات رمز الاستجابة السريعة من مستنداتك

دعنا ننشئ بيئتك ونبدأ!

### المتطلبات الأساسية
قبل البدء، تأكد من أن لديك المتطلبات الأساسية التالية:

#### المكتبات والتبعيات المطلوبة
ستحتاج إلى GroupDocs.Signature لجافا. يمكنك تضمينه عبر Maven أو Gradle، أو تنزيله مباشرةً.

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

**التحميل المباشر**
قم بتنزيل أحدث إصدار من [GroupDocs.Signature لإصدارات Java](https://releases.groupdocs.com/signature/java/).

#### متطلبات إعداد البيئة
- تأكد من تثبيت Java Development Kit (JDK) 8 أو أعلى.
- استخدم IDE مثل IntelliJ IDEA، أو Eclipse، أو NetBeans.

#### متطلبات المعرفة الأساسية
من المفيد أن يكون لديك فهم أساسي لبرمجة Java ومعالجة المستندات.

## إعداد GroupDocs.Signature لـ Java
لاستخدام GroupDocs.Signature في مشروعك، اتبع الخطوات التالية:
1. **تثبيت**:اختر بين Maven أو Gradle أو التنزيل المباشر بناءً على إعدادك.
2. **الحصول على الترخيص**:
   - ابدأ بالتجربة المجانية المتاحة على [موقع GroupDocs](https://releases.groupdocs.com/signature/java/).
   - فكر في الحصول على ترخيص مؤقت للاختبار والتطوير الموسع من [هنا](https://purchase.groupdocs.com/temporary-license/).
3. **التهيئة الأساسية**: 
    فيما يلي كيفية تهيئة GroupDocs.Signature:

    ```java
    Signature signature = new Signature("YOUR_DOCUMENT_PATH");
    ```

يُعد هذا بمثابة إعداد لك لتنفيذ توقيعات رمز الاستجابة السريعة (QR Code).

## دليل التنفيذ

### توقيع المستند باستخدام رمز الاستجابة السريعة (QR-Code)
#### ملخص
يتضمن توقيع مستند باستخدام رمز الاستجابة السريعة تضمين رمز فريد يمثل توقيعك الرقمي. هذه العملية تضمن أمان المستند وتتيح التحقق من صحته بسهولة لاحقًا.

##### الخطوة 1: إعداد خيارات التوقيع الخاصة بك
```java
import com.groupdocs.signature.Signature;
import com.groupdocs.signature.domain.enums.HorizontalAlignment;
import com.groupdocs.signature.domain.enums.VerticalAlignment;
import com.groupdocs.signature.options.sign.QrCodeSignOptions;

Signature signature = new Signature("YOUR_DOCUMENT_PATH");
QrCodeSignOptions signOptions = new QrCodeSignOptions("John Smith", com.groupdocs.signature.domain.qrcodes.QrCodeTypes.QR);

signOptions.setVerticalAlignment(VerticalAlignment.Top);
signOptions.setHorizontalAlignment(HorizontalAlignment.Center);
signOptions.setWidth(100);
signOptions.setHeight(40);
```
**توضيح**: `QrCodeSignOptions` مُهيأ لإنشاء رمز استجابة سريعة (QR) بنص ومحاذاة مُحددين. اضبط العرض والارتفاع حسب الحاجة.

##### الخطوة 2: تخصيص مظهر التوقيع
```java
import java.awt.Color;

signOptions.setForeColor(Color.RED); // تعيين لون رمز الاستجابة السريعة
com.groupdocs.signature.domain.SignatureFont signatureFont = new com.groupdocs.signature.domain.SignatureFont();
signatureFont.setSize(12);
signatureFont.setFamilyName("Comic Sans MS");
signOptions.setFont(signatureFont);
```
**توضيح**:يساعد تخصيص الخط واللون على تعزيز التعرف البصري.

##### الخطوة 3: توقيع الوثيقة
```java
import java.util.ArrayList;
import java.util.List;

List<String> signatureIds = new ArrayList<>();
List<com.groupdocs.signature.domain.BaseSignature> signedSignatures = signature.sign("YOUR_OUTPUT_PATH", signOptions).getSucceeded();

for (com.groupdocs.signature.domain.BaseSignature temp : signedSignatures) {
    signatureIds.add(temp.getSignatureId());
}
```
**توضيح**:تقوم هذه الخطوة بتوقيع المستند وتخزين معرفات التوقيع للرجوع إليها في المستقبل.

### التحقق من المستند باستخدام توقيع رمز الاستجابة السريعة
#### ملخص
يضمن التحقق صحة توقيع المستند. إليك كيفية التحقق من توقيع رمز الاستجابة السريعة في مستند.

##### الخطوة 1: إعداد خيارات التحقق
```java
import com.groupdocs.signature.Signature;
import com.groupdocs.signature.options.verify.QrCodeVerifyOptions;

Signature signature2 = new Signature("YOUR_OUTPUT_PATH");
QrCodeVerifyOptions verifyOptions = new QrCodeVerifyOptions();

verifyOptions.setEncodeType(QrCodeTypes.QR);
verifyOptions.setText("John Smith"); // نص للتحقق
verifyOptions.setAllPages(false); 
verifyOptions.setPageNumber(1);
```
**توضيح**:تحدد خيارات التحقق نوع رمز الاستجابة السريعة والنص الذي يجب البحث عنه، مما يضمن أن التوقيع يطابق توقعاتك.

##### الخطوة 2: إجراء التحقق
```java
boolean isValid = signature2.verify(verifyOptions).isValid();
System.out.println("Is Signature Valid? " + isValid);
```
**توضيح**:يتحقق هذا مما إذا كانت الوثيقة تحتوي على رمز QR صالح يطابق معاييرك.

### البحث عن مستند لتوقيع رمز الاستجابة السريعة
#### ملخص
من الضروري أحيانًا العثور على التوقيعات الموجودة في مستند. إليك كيفية البحث عنها باستخدام GroupDocs.Signature.

##### الخطوة 1: تكوين خيارات البحث
```java
import com.groupdocs.signature.domain.signatures.QrCodeSignature;
import com.groupdocs.signature.options.search.QrCodeSearchOptions;

Signature signature2 = new Signature("YOUR_OUTPUT_PATH");
QrCodeSearchOptions searchOptions = new QrCodeSearchOptions();
searchOptions.setAllPages(true);
```
**توضيح**:يؤدي هذا إلى إعداد الأداة لمسح جميع الصفحات بحثًا عن توقيعات رمز الاستجابة السريعة QR.

##### الخطوة 2: تنفيذ البحث
```java
List<QrCodeSignature> signatures = signature2.search(QrCodeSignature.class, searchOptions);

for (QrCodeSignature qrSignature : signatures) {
    System.out.println("Found Signature ID: " + qrSignature.getSignatureId());
}
```
**توضيح**:يؤدي هذا إلى استرداد جميع توقيعات رمز الاستجابة السريعة QR الموجودة في المستند.

### تحديث توقيع رمز الاستجابة السريعة للمستند
#### ملخص
يتضمن تحديث التوقيع تغيير خصائصه، مثل الموقع أو الحجم. إليك كيفية القيام بذلك:

##### الخطوة 1: تحضير التوقيعات للتحديث
```java
import com.groupdocs.signature.domain.signatures.QrCodeSignature;
import java.io.ByteArrayOutputStream;

Signature signature2 = new Signature("YOUR_OUTPUT_PATH");
List<QrCodeSignature> signaturesToUpdate = new ArrayList<>();

// بافتراض أن "التوقيعات" عبارة عن قائمة من كائنات QrCodeSignature التي تم الحصول عليها من البحث
for (QrCodeSignature qrSignature : signatures) {
    qrSignature.setLeft(qrSignature.getLeft() + 100);
    qrSignature.setTop(qrSignature.getTop() + 100);
    qrSignature.setWidth(200);
    qrSignature.setHeight(50);
    signaturesToUpdate.add(qrSignature);
}
```
**توضيح**:يؤدي هذا إلى ضبط موضع وحجم كل توقيع.

##### الخطوة 2: تحديث المستند
```java
ByteArrayOutputStream outputStream = new ByteArrayOutputStream();
signature2.update(outputStream, signaturesToUpdate);
```
**توضيح**:تم تحديث المستند باستخدام توقيعات رمز الاستجابة السريعة المعدلة.

### حذف توقيع رمز الاستجابة السريعة للمستند بواسطة المعرف
#### ملخص
قد يكون حذف التوقيع ضروريًا إذا لم يعد ضروريًا أو أُضيف بالخطأ. إليك كيفية إزالته باستخدام مُعرِّفه الفريد.

##### الخطوة 1: تحديد التوقيعات المراد حذفها
```java
import com.groupdocs.signature.domain.SignatureCollection;
import java.util.Arrays;

SignatureCollection signaturesToDelete = signature2.search(QrCodeSignature.class);
Arrays.stream(signaturesToDelete).forEach(signature -> {
    if (signature.getSignatureId().equals("YOUR_SIGNATURE_ID")) {
        signature.delete();
    }
});
```
**توضيح**:يؤدي هذا إلى العثور على توقيع رمز الاستجابة السريعة (QR Code) وحذفه من خلال معرفه الفريد.

## خاتمة
يشرح هذا الدليل كيفية تأمين مستنداتك باستخدام توقيعات رمز الاستجابة السريعة (QR) في جافا باستخدام GroupDocs.Signature. باتباع هذه الخطوات، يمكنك ضمان توقيع مستنداتك بأمان والتحقق من صحتها بسهولة.