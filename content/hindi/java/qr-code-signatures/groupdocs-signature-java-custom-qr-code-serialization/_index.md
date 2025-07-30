---
"date": "2025-05-08"
"description": "Java के लिए GroupDocs.Signature का उपयोग करके PDF में एन्क्रिप्शन के साथ कस्टम QR-कोड क्रमांकन लागू करना सीखें। अपने दस्तावेज़ों को कुशलतापूर्वक सुरक्षित करें।"
"title": "Java के लिए GroupDocs.Signature का उपयोग करके PDF में कस्टम QR-कोड क्रमांकन और एन्क्रिप्शन लागू करें"
"url": "/hi/java/qr-code-signatures/groupdocs-signature-java-custom-qr-code-serialization/"
"weight": 1
---

# Java के लिए GroupDocs.Signature का उपयोग करके PDF में कस्टम QR-कोड क्रमांकन और एन्क्रिप्शन कैसे लागू करें

## परिचय

डिजिटल युग में, डेटा की अखंडता और प्रामाणिकता बनाए रखने के लिए सुरक्षित दस्तावेज़ हस्ताक्षर आवश्यक हैं। GroupDocs.Signature for Java—दस्तावेज़ों में हस्ताक्षर जोड़ना आसान बनाने के लिए डिज़ाइन की गई एक शक्तिशाली लाइब्रेरी—का उपयोग करें। यह ट्यूटोरियल आपको GroupDocs.Signature for Java का उपयोग करके PDF में एन्क्रिप्शन के साथ कस्टम QR-कोड क्रमांकन लागू करने में मार्गदर्शन करेगा।

**आप क्या सीखेंगे:**
- Java के लिए GroupDocs.Signature को कैसे सेट अप और कॉन्फ़िगर करें
- क्यूआर-कोड हस्ताक्षरों के लिए कस्टम क्रमांकन का कार्यान्वयन
- QR कोड के भीतर क्रमबद्ध डेटा को एन्क्रिप्ट करना
- अपने दस्तावेज़ों को सुरक्षित करने के लिए इन सुविधाओं का उपयोग करें

इससे पहले कि हम कार्यान्वयन में उतरें, आइए यह सुनिश्चित कर लें कि आपके पास अनुसरण करने के लिए आवश्यक सभी चीजें मौजूद हैं।

### आवश्यक शर्तें

इस ट्यूटोरियल का प्रभावी ढंग से उपयोग करने के लिए, सुनिश्चित करें कि आप निम्नलिखित पूर्वापेक्षाएँ पूरी करते हैं:

1. **आवश्यक लाइब्रेरी और निर्भरताएँ:**
   - Java संस्करण 23.12 या उच्चतर के लिए GroupDocs.Signature
   - निर्भरता प्रबंधन के लिए Maven या Gradle (वैकल्पिक)

2. **पर्यावरण सेटअप आवश्यकताएँ:**
   - आपकी मशीन पर जावा डेवलपमेंट किट (JDK) स्थापित है
   - जावा प्रोग्रामिंग की बुनियादी समझ

3. **ज्ञान पूर्वापेक्षाएँ:**
   - जावा और ऑब्जेक्ट-ओरिएंटेड प्रोग्रामिंग अवधारणाओं से परिचित होना
   - जावा में PDF के साथ काम करने का बुनियादी ज्ञान

## Java के लिए GroupDocs.Signature सेट अप करना

आरंभ करने के लिए, आपको अपने प्रोजेक्ट परिवेश में GroupDocs.Signature लाइब्रेरी सेट अप करनी होगी।

### मावेन स्थापना

यदि आप Maven का उपयोग कर रहे हैं, तो अपने में निम्नलिखित निर्भरता जोड़ें `pom.xml` फ़ाइल:

```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

### ग्रेडल स्थापना

Gradle उपयोगकर्ताओं के लिए, इस पंक्ति को अपने में शामिल करें `build.gradle` फ़ाइल:

```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

### प्रत्यक्षत: डाउनलोड

वैकल्पिक रूप से, आप नवीनतम संस्करण को सीधे यहां से डाउनलोड कर सकते हैं [Java रिलीज़ के लिए GroupDocs.Signature](https://releases.groupdocs.com/signature/java/).

#### लाइसेंस प्राप्ति चरण
- **मुफ्त परीक्षण:** इसकी विशेषताओं का परीक्षण करने के लिए परीक्षण संस्करण डाउनलोड करके शुरुआत करें।
- **अस्थायी लाइसेंस:** यदि आवश्यक हो तो आप अस्थायी लाइसेंस का अनुरोध कर सकते हैं, जो आपको बिना किसी प्रतिबंध के उत्पाद का मूल्यांकन करने की अनुमति देता है।
- **खरीदना:** दीर्घकालिक उपयोग के लिए, पूर्ण लाइसेंस खरीदने पर विचार करें।

एक बार इंस्टॉल हो जाने पर, अपने प्रोजेक्ट में GroupDocs.Signature को आरंभ करें:

```java
import com.groupdocs.signature.Signature;

public class SetupGroupDocs {
    public static void main(String[] args) {
        Signature signature = new Signature("YOUR_DOCUMENT_DIRECTORY/sample.pdf");
        // आपका कोड यहां...
    }
}
```

## कार्यान्वयन मार्गदर्शिका

अब, आइए Java के लिए GroupDocs.Signature के साथ कस्टम QR-कोड क्रमांकन और एन्क्रिप्शन को लागू करने पर गौर करें।

### क्यूआर-कोड हस्ताक्षरों के लिए कस्टम क्रमांकन वर्ग

#### अवलोकन

इस सुविधा में एक ऐसा वर्ग बनाना शामिल है जो मेटाडेटा को क्यूआर-कोड हस्ताक्षर में क्रमबद्ध करने का काम संभालता है। `DocumentSignatureData` क्लास आईडी, लेखक, हस्ताक्षरित तिथि और डेटा फैक्टर जैसी विशेषताओं को संग्रहीत करता है।

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

#### स्पष्टीकरण
- **गुण:** The `@FormatAttribute` एनोटेशन यह निर्दिष्ट करते हैं कि प्रत्येक विशेषता को क्यूआर कोड में कैसे क्रमबद्ध किया जाता है।
  - **पहचान**हस्ताक्षर के लिए एक अद्वितीय पहचानकर्ता.
  - **लेखक**: वह व्यक्ति जिसने दस्तावेज़ पर हस्ताक्षर किये हैं।
  - **हस्ताक्षरित तिथि**: दस्तावेज़ पर हस्ताक्षर किए जाने का टाइमस्टैम्प.
  - **डेटा फैक्टर**: हस्ताक्षर से संबद्ध अतिरिक्त संख्यात्मक डेटा.

### कस्टम डेटा क्रमांकन और एन्क्रिप्शन के साथ क्यूआर-कोड हस्ताक्षर

#### अवलोकन

यह अनुभाग दर्शाता है कि क्यूआर-कोड का उपयोग करके किसी दस्तावेज़ पर हस्ताक्षर कैसे किया जाता है, जिसमें कस्टम क्रमबद्ध डेटा और एन्क्रिप्शन शामिल होता है।

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

        // अपना कस्टम एन्क्रिप्शन तर्क यहां लागू करें
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

        // संरेखण और उपस्थिति कॉन्फ़िगर करें
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

#### स्पष्टीकरण
- **कस्टम एन्क्रिप्शन:** अपना स्वयं का एन्क्रिप्शन तर्क लागू करें `CustomXOREncryption` या किसी अन्य विधि का उपयोग करें `IDataEncryption`.
- **हस्ताक्षर विकल्प:** ऊंचाई, चौड़ाई, पैडिंग आदि जैसे विकल्पों के साथ QR-कोड की उपस्थिति और संरेखण को कॉन्फ़िगर करें।
- **हस्ताक्षर प्रक्रिया:** The `signature.sign()` विधि दस्तावेज़ पर क्यूआर-कोड हस्ताक्षर लागू करती है।

### समस्या निवारण युक्तियों

- सुनिश्चित करें कि आपके बिल्ड टूल (Maven/Gradle) में सभी निर्भरताएं सही ढंग से कॉन्फ़िगर की गई हैं।
- सत्यापित करें कि इनपुट और आउटपुट दस्तावेज़ों के लिए फ़ाइल पथ सटीक हैं।
- पुष्टि करें कि आपका कस्टम एन्क्रिप्शन तर्क उचित रूप से क्रियान्वित और एकीकृत है।

## व्यावहारिक अनुप्रयोगों

इस सुविधा के कुछ वास्तविक अनुप्रयोग इस प्रकार हैं:

1. **कानूनी दस्तावेज़ पर हस्ताक्षर:** प्रामाणिकता सुनिश्चित करने के लिए क्यूआर कोड में एम्बेडेड मेटाडेटा के साथ अनुबंधों पर सुरक्षित रूप से हस्ताक्षर करें।
2. **बीजक संसाधित करना:** अतिरिक्त सुरक्षा और पता लगाने की क्षमता के लिए चालान में स्वचालित रूप से एन्क्रिप्टेड हस्ताक्षर जोड़ें।
3. **रसद ट्रैकिंग:** शिपमेंट ट्रैकिंग के लिए हस्ताक्षरित दस्तावेजों का उपयोग करें, क्यूआर कोड के भीतर अद्वितीय पहचानकर्ता और टाइमस्टैम्प एम्बेड करें।
4. **शैक्षणिक प्रमाणपत्र:** क्यूआर-कोड हस्ताक्षर का उपयोग करके छात्र की जानकारी को डिजिटल प्रमाणपत्रों में सुरक्षित रूप से एम्बेड करें