---
"date": "2025-05-08"
"description": "GroupDocs.Signature की मदद से Java में QR कोड हस्ताक्षरों को लागू और सत्यापित करके दस्तावेज़ सुरक्षा बढ़ाने का तरीका जानें। सुरक्षित हस्ताक्षर प्रक्रिया के लिए इस चरण-दर-चरण मार्गदर्शिका का पालन करें।"
"title": "अपने दस्तावेज़ों को सुरक्षित करें&#58; GroupDocs.Signature का उपयोग करके जावा में QR कोड हस्ताक्षर लागू करें"
"url": "/hi/java/qr-code-signatures/qr-code-signatures-java-groupdocs/"
"weight": 1
---

# अपने दस्तावेज़ सुरक्षित करें: GroupDocs.Signature का उपयोग करके जावा में QR कोड हस्ताक्षर लागू करें

आज के डिजिटल परिदृश्य में, अनुबंधों, चालानों या संवेदनशील व्यक्तिगत जानकारी जैसे दस्तावेज़ों की सुरक्षा सुनिश्चित करना अत्यंत महत्वपूर्ण है। दस्तावेज़ सुरक्षा बढ़ाने और सत्यापन प्रक्रियाओं को सरल बनाने का एक अभिनव तरीका क्यूआर कोड हस्ताक्षरों का उपयोग करना है। यह ट्यूटोरियल आपको GroupDocs.Signature का उपयोग करके जावा में अपने दस्तावेज़ों के लिए क्यूआर कोड हस्ताक्षरों को लागू करने और सत्यापित करने में मार्गदर्शन करेगा।

## आप क्या सीखेंगे
- क्यूआर कोड का उपयोग करके दस्तावेज़ों पर हस्ताक्षर कैसे करें
- क्यूआर कोड के साथ हस्ताक्षरित दस्तावेजों का सत्यापन
- किसी दस्तावेज़ में मौजूदा QR कोड हस्ताक्षरों की खोज करना
- अपने दस्तावेज़ों से QR कोड हस्ताक्षर अपडेट करना और हटाना

आइये अपना वातावरण तैयार करें और शुरू करें!

### आवश्यक शर्तें
आरंभ करने से पहले, सुनिश्चित करें कि आपके पास निम्नलिखित पूर्वापेक्षाएँ हैं:

#### आवश्यक लाइब्रेरी और निर्भरताएँ
आपको Java के लिए GroupDocs.Signature की आवश्यकता होगी। आप इसे Maven या Gradle के माध्यम से शामिल कर सकते हैं, या सीधे डाउनलोड कर सकते हैं।

**मावेन**
```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

**ग्रैडल**
```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

**प्रत्यक्षत: डाउनलोड**
नवीनतम संस्करण यहां से डाउनलोड करें [Java रिलीज़ के लिए GroupDocs.Signature](https://releases.groupdocs.com/signature/java/).

#### पर्यावरण सेटअप आवश्यकताएँ
- सुनिश्चित करें कि आपके पास जावा डेवलपमेंट किट (JDK) 8 या उच्चतर संस्करण स्थापित है।
- IntelliJ IDEA, Eclipse, या NetBeans जैसे IDE का उपयोग करें।

#### ज्ञान पूर्वापेक्षाएँ
जावा प्रोग्रामिंग और दस्तावेज़ प्रसंस्करण की बुनियादी समझ लाभदायक है।

## Java के लिए GroupDocs.Signature सेट अप करना
अपने प्रोजेक्ट में GroupDocs.Signature का उपयोग करने के लिए, इन चरणों का पालन करें:
1. **इंस्टालेशन**: अपने सेटअप के आधार पर Maven, Gradle, या सीधे डाउनलोड के बीच चुनें।
2. **लाइसेंस अधिग्रहण**:
   - पर उपलब्ध निःशुल्क परीक्षण के साथ शुरुआत करें [ग्रुपडॉक्स वेबसाइट](https://releases.groupdocs.com/signature/java/).
   - विस्तारित परीक्षण और विकास के लिए अस्थायी लाइसेंस प्राप्त करने पर विचार करें [यहाँ](https://purchase.groupdocs.com/temporary-license/).
3. **मूल आरंभीकरण**: 
    GroupDocs.Signature को आरंभ करने का तरीका यहां दिया गया है:

    ```java
    Signature signature = new Signature("YOUR_DOCUMENT_PATH");
    ```

यह आपको QR कोड हस्ताक्षर लागू करने के लिए तैयार करता है।

## कार्यान्वयन मार्गदर्शिका

### क्यूआर-कोड हस्ताक्षर के साथ दस्तावेज़ पर हस्ताक्षर करें
#### अवलोकन
क्यूआर कोड का उपयोग करके किसी दस्तावेज़ पर हस्ताक्षर करने में एक विशिष्ट कोड शामिल होता है जो आपके डिजिटल हस्ताक्षर का प्रतिनिधित्व करता है। यह प्रक्रिया दस्तावेज़ को सुरक्षित बनाती है और बाद में उसकी प्रामाणिकता की आसान पुष्टि की अनुमति देती है।

##### चरण 1: अपने हस्ताक्षर विकल्प सेट करें
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
**स्पष्टीकरण**: `QrCodeSignOptions` विशिष्ट टेक्स्ट और संरेखण के साथ एक QR कोड बनाने के लिए कॉन्फ़िगर किया गया है। आवश्यकतानुसार चौड़ाई और ऊँचाई समायोजित करें।

##### चरण 2: हस्ताक्षर का स्वरूप अनुकूलित करें
```java
import java.awt.Color;

signOptions.setForeColor(Color.RED); // QR कोड का रंग सेट करें
com.groupdocs.signature.domain.SignatureFont signatureFont = new com.groupdocs.signature.domain.SignatureFont();
signatureFont.setSize(12);
signatureFont.setFamilyName("Comic Sans MS");
signOptions.setFont(signatureFont);
```
**स्पष्टीकरण**फ़ॉन्ट और रंग को अनुकूलित करने से दृश्य पहचान बढ़ जाती है।

##### चरण 3: दस्तावेज़ पर हस्ताक्षर करें
```java
import java.util.ArrayList;
import java.util.List;

List<String> signatureIds = new ArrayList<>();
List<com.groupdocs.signature.domain.BaseSignature> signedSignatures = signature.sign("YOUR_OUTPUT_PATH", signOptions).getSucceeded();

for (com.groupdocs.signature.domain.BaseSignature temp : signedSignatures) {
    signatureIds.add(temp.getSignatureId());
}
```
**स्पष्टीकरण**: यह चरण दस्तावेज़ पर हस्ताक्षर करता है और भविष्य के संदर्भ के लिए हस्ताक्षर आईडी संग्रहीत करता है।

### क्यूआर-कोड हस्ताक्षर के साथ दस्तावेज़ सत्यापित करें
#### अवलोकन
सत्यापन यह सुनिश्चित करता है कि दस्तावेज़ पर वैध हस्ताक्षर किए गए हैं। यहाँ बताया गया है कि आप दस्तावेज़ में QR कोड हस्ताक्षर कैसे सत्यापित कर सकते हैं।

##### चरण 1: सत्यापन विकल्प सेट करें
```java
import com.groupdocs.signature.Signature;
import com.groupdocs.signature.options.verify.QrCodeVerifyOptions;

Signature signature2 = new Signature("YOUR_OUTPUT_PATH");
QrCodeVerifyOptions verifyOptions = new QrCodeVerifyOptions();

verifyOptions.setEncodeType(QrCodeTypes.QR);
verifyOptions.setText("John Smith"); // सत्यापित करने के लिए पाठ
verifyOptions.setAllPages(false); 
verifyOptions.setPageNumber(1);
```
**स्पष्टीकरण**सत्यापन विकल्प निर्दिष्ट करते हैं कि किस QR कोड प्रकार और पाठ को देखना है, यह सुनिश्चित करते हुए कि हस्ताक्षर आपकी अपेक्षाओं से मेल खाता है।

##### चरण 2: सत्यापन करें
```java
boolean isValid = signature2.verify(verifyOptions).isValid();
System.out.println("Is Signature Valid? " + isValid);
```
**स्पष्टीकरण**: यह जाँचता है कि दस्तावेज़ में आपके मानदंड से मेल खाता वैध QR कोड है या नहीं।

### क्यूआर-कोड हस्ताक्षर के लिए दस्तावेज़ खोजें
#### अवलोकन
किसी दस्तावेज़ में मौजूदा हस्ताक्षरों को ढूँढना कभी-कभी ज़रूरी होता है। यहाँ बताया गया है कि आप GroupDocs.Signature का इस्तेमाल करके उन्हें कैसे खोज सकते हैं।

##### चरण 1: खोज विकल्प कॉन्फ़िगर करें
```java
import com.groupdocs.signature.domain.signatures.QrCodeSignature;
import com.groupdocs.signature.options.search.QrCodeSearchOptions;

Signature signature2 = new Signature("YOUR_OUTPUT_PATH");
QrCodeSearchOptions searchOptions = new QrCodeSearchOptions();
searchOptions.setAllPages(true);
```
**स्पष्टीकरण**: यह टूल को QR कोड हस्ताक्षरों के लिए सभी पृष्ठों को स्कैन करने के लिए सेट करता है।

##### चरण 2: खोज निष्पादित करें
```java
List<QrCodeSignature> signatures = signature2.search(QrCodeSignature.class, searchOptions);

for (QrCodeSignature qrSignature : signatures) {
    System.out.println("Found Signature ID: " + qrSignature.getSignatureId());
}
```
**स्पष्टीकरण**: यह दस्तावेज़ में पाए गए सभी QR कोड हस्ताक्षरों को पुनः प्राप्त करता है।

### दस्तावेज़ QR-कोड हस्ताक्षर अपडेट करें
#### अवलोकन
हस्ताक्षर को अपडेट करने के लिए उसकी स्थिति या आकार जैसे गुणों को बदलना पड़ता है। यह कैसे करें, यहाँ बताया गया है:

##### चरण 1: अद्यतन के लिए हस्ताक्षर तैयार करें
```java
import com.groupdocs.signature.domain.signatures.QrCodeSignature;
import java.io.ByteArrayOutputStream;

Signature signature2 = new Signature("YOUR_OUTPUT_PATH");
List<QrCodeSignature> signaturesToUpdate = new ArrayList<>();

// मान लें कि 'हस्ताक्षर' खोज से प्राप्त QrCodeSignature ऑब्जेक्ट्स की एक सूची है
for (QrCodeSignature qrSignature : signatures) {
    qrSignature.setLeft(qrSignature.getLeft() + 100);
    qrSignature.setTop(qrSignature.getTop() + 100);
    qrSignature.setWidth(200);
    qrSignature.setHeight(50);
    signaturesToUpdate.add(qrSignature);
}
```
**स्पष्टीकरण**: यह प्रत्येक हस्ताक्षर की स्थिति और आकार को समायोजित करता है।

##### चरण 2: दस्तावेज़ अपडेट करें
```java
ByteArrayOutputStream outputStream = new ByteArrayOutputStream();
signature2.update(outputStream, signaturesToUpdate);
```
**स्पष्टीकरण**: दस्तावेज़ को संशोधित क्यूआर कोड हस्ताक्षरों के साथ अद्यतन किया गया है।

### आईडी द्वारा दस्तावेज़ क्यूआर-कोड हस्ताक्षर हटाएं
#### अवलोकन
अगर किसी हस्ताक्षर की अब ज़रूरत नहीं है या वह गलती से जोड़ा गया है, तो उसे हटाना ज़रूरी हो सकता है। यहाँ बताया गया है कि आप उसकी विशिष्ट आईडी का इस्तेमाल करके उसे कैसे हटा सकते हैं।

##### चरण 1: हटाने के लिए हस्ताक्षरों की पहचान करें
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
**स्पष्टीकरण**: यह QR कोड हस्ताक्षर को उसकी विशिष्ट आईडी द्वारा ढूंढता है और हटा देता है।

## निष्कर्ष
इस गाइड में आपको GroupDocs.Signature के साथ जावा में क्यूआर कोड हस्ताक्षरों का उपयोग करके दस्तावेज़ों को सुरक्षित करने का तरीका बताया गया है। इन चरणों का पालन करके, आप यह सुनिश्चित कर सकते हैं कि आपके दस्तावेज़ सुरक्षित रूप से हस्ताक्षरित हैं और उनकी प्रामाणिकता आसानी से सत्यापित की जा सकती है।