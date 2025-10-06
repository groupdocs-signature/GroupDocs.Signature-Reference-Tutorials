---
"date": "2025-05-08"
"description": "Java के लिए GroupDocs.Signature के साथ एन्क्रिप्शन का उपयोग करके इमेज मेटाडेटा को सुरक्षित करने का तरीका जानें। चरण-दर-चरण मार्गदर्शन के साथ डेटा की अखंडता और प्रामाणिकता सुनिश्चित करें।"
"title": "GroupDocs.Signature के साथ जावा में छवि मेटाडेटा हस्ताक्षर और एन्क्रिप्शन लागू करें"
"url": "/hi/java/metadata-signatures/groupdocs-signature-java-image-metadata-encryption/"
"weight": 1
type: docs
---
# GroupDocs.Signature का उपयोग करके जावा में एन्क्रिप्शन के साथ छवि मेटाडेटा हस्ताक्षर को कार्यान्वित करें

## परिचय

आज के डिजिटल परिदृश्य में, दस्तावेज़ मेटाडेटा में संवेदनशील जानकारी की सुरक्षा अत्यंत महत्वपूर्ण है। चाहे गोपनीय व्यावसायिक अनुबंधों से संबंधित हो या व्यक्तिगत पहचान वाली तस्वीरों से, छवि मेटाडेटा की अखंडता और प्रामाणिकता बनाए रखने से अनधिकृत पहुँच और छेड़छाड़ को रोकने में मदद मिलती है। **Java के लिए GroupDocs.Signature** छवि मेटाडेटा को सुरक्षित रूप से हस्ताक्षरित और एन्क्रिप्ट करने के लिए एक मजबूत समाधान प्रदान करता है।

यह ट्यूटोरियल आपको GroupDocs.Signature की शक्तिशाली सुविधाओं का उपयोग करके जावा में एन्क्रिप्शन के साथ इमेज मेटाडेटा साइनिंग को लागू करने में मार्गदर्शन करता है। इन चरणों का पालन करके, आप इस कार्यक्षमता को अपने जावा अनुप्रयोगों में प्रभावी ढंग से एकीकृत कर पाएँगे।

**आप क्या सीखेंगे:**
- Java के लिए GroupDocs.Signature का उपयोग करके दस्तावेज़ मेटाडेटा पर हस्ताक्षर करना
- एन्क्रिप्शन के साथ कस्टम ऑब्जेक्ट हस्ताक्षरों को कार्यान्वित करना
- सममित कुंजी एन्क्रिप्शन का उपयोग करके एक सुरक्षित वातावरण स्थापित करना

## आवश्यक शर्तें

आरंभ करने से पहले, सुनिश्चित करें कि निम्नलिखित पूर्वापेक्षाएँ पूरी हों:

### आवश्यक लाइब्रेरी और निर्भरताएँ:
- **Java के लिए GroupDocs.Signature**सुनिश्चित करें कि आपके पास संस्करण 23.12 या बाद का संस्करण है।

### पर्यावरण सेटअप आवश्यकताएँ:
- अपनी मशीन पर जावा डेवलपमेंट किट (JDK) स्थापित करें।
- IntelliJ IDEA, Eclipse, या NetBeans जैसे एकीकृत विकास वातावरण (IDE) का उपयोग करें।

### ज्ञान पूर्वापेक्षाएँ:
- जावा प्रोग्रामिंग की बुनियादी समझ.
- निर्भरता प्रबंधन के लिए मावेन या ग्रेडेल से परिचित होना।

## Java के लिए GroupDocs.Signature सेट अप करना

अपने प्रोजेक्ट में GroupDocs.Signature का उपयोग करने के लिए, आवश्यक निर्भरताएँ निम्नानुसार शामिल करें:

### मावेन का उपयोग करना
इसे अपने में जोड़ें `pom.xml` फ़ाइल:
```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

### ग्रैडल का उपयोग करना
इसे अपने में शामिल करें `build.gradle` फ़ाइल:
```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

### प्रत्यक्षत: डाउनलोड
वैकल्पिक रूप से, नवीनतम संस्करण यहां से डाउनलोड करें [Java रिलीज़ के लिए GroupDocs.Signature](https://releases.groupdocs.com/signature/java/).

#### लाइसेंस प्राप्ति चरण
- **मुफ्त परीक्षण**: सुविधाओं का पता लगाने के लिए परीक्षण से शुरुआत करें।
- **अस्थायी लाइसेंस**यदि आवश्यक हो तो व्यापक परीक्षण के लिए आवेदन करें।
- **खरीदना**: उत्पादन उपयोग के लिए लाइसेंस प्राप्त करें [ग्रुपडॉक्स](https://purchase.groupdocs.com/buy).

## बुनियादी आरंभीकरण और सेटअप

यहां बताया गया है कि आप अपने जावा एप्लिकेशन में GroupDocs.Signature को कैसे आरंभ कर सकते हैं:

```java
import com.groupdocs.signature.Signature;

public class InitializeSignature {
    public static void main(String[] args) {
        // दस्तावेज़ का पथ
        String filePath = "path/to/your/document.jpg";
        
        // हस्ताक्षर का एक नया उदाहरण बनाएँ
        Signature signature = new Signature(filePath);

        System.out.println("GroupDocs.Signature initialized successfully.");
    }
}
```

## कार्यान्वयन मार्गदर्शिका

### विशेषता: कस्टम ऑब्जेक्ट के साथ मेटाडेटा हस्ताक्षर

#### अवलोकन
यह सुविधा कस्टम ऑब्जेक्ट का उपयोग करके छवि मेटाडेटा पर हस्ताक्षर करने और अतिरिक्त सुरक्षा के लिए इसे एन्क्रिप्ट करने की अनुमति देती है, जिससे यह सुनिश्चित होता है कि केवल अधिकृत पक्ष ही मेटाडेटा तक पहुंच या उसे संशोधित कर सकते हैं।

#### चरण-दर-चरण कार्यान्वयन

##### 1. अपने दस्तावेज़ हस्ताक्षर डेटा वर्ग को परिभाषित करें
अपनी मेटाडेटा जानकारी रखने के लिए एक क्लास बनाएं:

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

##### 2. हस्ताक्षर तर्क को लागू करें
एन्क्रिप्शन का उपयोग करके मेटाडेटा पर हस्ताक्षर करने का तरीका यहां दिया गया है:

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
    // प्लेसहोल्डर्स के साथ फ़ाइल पथ आरंभ करें
    String filePath = "YOUR_DOCUMENT_DIRECTORY/SampleImage.jpg";
    String outputFilePath = new File("YOUR_OUTPUT_DIRECTORY", 
                                       "SignedImageWithCustomMetadata/SampleImage_signed.jpg").getPath();

    public void run() throws Exception {
        Signature signature = new Signature(filePath);

        // एन्क्रिप्शन के लिए कुंजी और पासफ़्रेज़ सेट करें
        String key = "1234567890";
        String salt = "1234567890";
        IDataEncryption encryption = new SymmetricEncryption(
            SymmetricAlgorithmType.Rijndael, key, salt);

        MetadataSignOptions options = new MetadataSignOptions();
        DocumentSignatureData documentSignature = new DocumentSignatureData();
        
        // कस्टम मेटाडेटा गुण सेट करें
        documentSignature.setID(UUID.randomUUID().toString());
        documentSignature.setAuthor(System.getenv("USERNAME"));
        documentSignature.setSigned(new Date());
        documentSignature.setDataFactor(new BigDecimal("11.22"));

        ImageMetadataSignature mdDocument = new ImageMetadataSignature(41996, documentSignature);
        mdDocument.setDataEncryption(encryption);

        // विकल्पों में मेटाडेटा हस्ताक्षर जोड़ें
        options.getSignatures().add(mdDocument);

        signature.sign(outputFilePath, options);
    }
}
```

#### कुंजी कॉन्फ़िगरेशन विकल्प
- **सममित एन्क्रिप्शन**: एन्क्रिप्शन के लिए रिजेंडेल एल्गोरिथ्म का उपयोग करता है।
- **मेटाडेटा साइनऑप्शन**: हस्ताक्षर प्रक्रिया को कॉन्फ़िगर करता है और निर्दिष्ट करता है कि किस मेटाडेटा पर हस्ताक्षर करना है।

##### समस्या निवारण युक्तियों
- सुनिश्चित करें कि आपके फ़ाइल पथ सही और सुलभ हैं।
- जाँच करें कि पर्यावरण चर `USERNAME` ठीक से सेट किया गया है.
- सत्यापित करें कि GroupDocs.Signature लाइब्रेरी संस्करण आपके कोड निर्भरताओं से मेल खाता है।

### विशेषता: एन्क्रिप्शन के साथ मेटाडेटा हस्ताक्षर

#### अवलोकन
यह सुविधा छवि फ़ाइलों के भीतर संवेदनशील जानकारी की सुरक्षा के लिए मेटाडेटा हस्ताक्षरों को एन्क्रिप्ट करने पर केंद्रित है।

#### चरण-दर-चरण कार्यान्वयन
##### 1. एन्क्रिप्शन लॉजिक को लागू करें
एन्क्रिप्शन का उपयोग करके मेटाडेटा पर हस्ताक्षर करने का तरीका यहां दिया गया है:
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
    // प्लेसहोल्डर्स के साथ फ़ाइल पथ आरंभ करें
    String filePath = "YOUR_DOCUMENT_DIRECTORY/SampleImage.jpg";
    String outputFilePath = new File("YOUR_OUTPUT_DIRECTORY", 
                                       "SignedImageWithEncryption/SampleImage_signed.jpg").getPath();

    public void run() throws Exception {
        Signature signature = new Signature(filePath);

        // एन्क्रिप्शन के लिए कुंजी और पासफ़्रेज़ सेट करें
        String key = "1234567890";
        String salt = "1234567890";
        IDataEncryption encryption = new SymmetricEncryption(
            SymmetricAlgorithmType.Rijndael, key, salt);

        MetadataSignOptions options = new MetadataSignOptions();
        DocumentSignatureData documentSignature = new DocumentSignatureData();
        
        // कस्टम मेटाडेटा गुण सेट करें
        documentSignature.setID(UUID.randomUUID().toString());
        documentSignature.setAuthor(System.getenv("USERNAME"));
        documentSignature.setSigned(new Date());
        documentSignature.setDataFactor(new BigDecimal("11.22"));

        ImageMetadataSignature mdDocument = new ImageMetadataSignature(41996, documentSignature);
        mdDocument.setDataEncryption(encryption);

        // विकल्पों में मेटाडेटा हस्ताक्षर जोड़ें
        options.getSignatures().add(mdDocument);

        signature.sign(outputFilePath, options);
    }
}
```