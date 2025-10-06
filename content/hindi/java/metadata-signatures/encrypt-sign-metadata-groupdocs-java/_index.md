---
"date": "2025-05-08"
"description": "Java के लिए GroupDocs.Signature के साथ दस्तावेज़ मेटाडेटा को एन्क्रिप्ट और हस्ताक्षरित करके सुरक्षित करने का तरीका जानें। यह मार्गदर्शिका कस्टम डेटा हस्ताक्षर, XOR एन्क्रिप्शन, और इन सुविधाओं को आपके Java अनुप्रयोगों में एकीकृत करने के बारे में बताती है।"
"title": "GroupDocs का उपयोग करके दस्तावेज़ मेटाडेटा को एन्क्रिप्ट और हस्ताक्षरित कैसे करें. Java के लिए हस्ताक्षर एक व्यापक गाइड"
"url": "/hi/java/metadata-signatures/encrypt-sign-metadata-groupdocs-java/"
"weight": 1
type: docs
---
# Java के लिए GroupDocs.Signature का उपयोग करके दस्तावेज़ मेटाडेटा को एन्क्रिप्ट और हस्ताक्षरित कैसे करें: एक व्यापक मार्गदर्शिका

## परिचय
आज के डिजिटल युग में, व्यावसायिक वातावरण में गोपनीयता और प्रामाणिकता बनाए रखने के लिए दस्तावेज़ मेटाडेटा की सुरक्षा अत्यंत महत्वपूर्ण है। चाहे आप संवेदनशील अनुबंधों का प्रबंधन कर रहे हों या व्यक्तिगत डेटा का, अनधिकृत पहुँच का जोखिम गंभीर सुरक्षा उल्लंघनों का कारण बन सकता है। यह ट्यूटोरियल आपको इसके उपयोग के बारे में मार्गदर्शन करेगा। **Java के लिए GroupDocs.Signature** दस्तावेज़ मेटाडेटा को कुशलतापूर्वक एन्क्रिप्ट और हस्ताक्षरित करना, उद्योग मानकों के अनुपालन को सुनिश्चित करते हुए डेटा सुरक्षा को बढ़ाना।

इस व्यापक मार्गदर्शिका में, हम यह जानेंगे कि:
- एक कस्टम डेटा हस्ताक्षर वर्ग बनाएँ.
- डेटा सुरक्षा के लिए XOR एन्क्रिप्शन लागू करें।
- मेटाडेटा हस्ताक्षर सेट करें और उन्हें GroupDocs.Signature का उपयोग करके दस्तावेज़ों पर लागू करें।

इस ट्यूटोरियल के अंत तक आप यह सीख चुके होंगे कि:
- प्रमुख विशेषताओं के साथ एक कस्टम डेटा हस्ताक्षर संरचना विकसित करें।
- XOR एल्गोरिदम का उपयोग करके दस्तावेज़ डेटा को एन्क्रिप्ट और डिक्रिप्ट करें।
- दस्तावेज़ मेटाडेटा को सुरक्षित करने के लिए इन सुविधाओं को अपने जावा अनुप्रयोगों में एकीकृत करें।

### आवश्यक शर्तें
कार्यान्वयन में उतरने से पहले, सुनिश्चित करें कि आप निम्नलिखित पूर्वापेक्षाएँ पूरी करते हैं:

#### आवश्यक लाइब्रेरी और निर्भरताएँ
- **Java के लिए GroupDocs.Signature**: सुनिश्चित करें कि आपके पास संस्करण 23.12 या बाद का संस्करण स्थापित है।
- **जावा डेवलपमेंट किट (JDK)**: संस्करण 8 या उच्चतर अनुशंसित है।

#### पर्यावरण सेटअप आवश्यकताएँ
- एक उपयुक्त IDE जैसे कि IntelliJ IDEA या Eclipse.
- आपके प्रोजेक्ट वातावरण में कॉन्फ़िगर किया गया Maven या Gradle.

#### ज्ञान पूर्वापेक्षाएँ
- जावा प्रोग्रामिंग की बुनियादी समझ.
- एन्क्रिप्शन और डिजिटल हस्ताक्षर जैसी अवधारणाओं से परिचित होना।

## Java के लिए GroupDocs.Signature सेट अप करना
आरंभ करने के लिए, आपको GroupDocs.Signature को अपने जावा प्रोजेक्ट में एकीकृत करना होगा। विभिन्न बिल्ड टूल्स का उपयोग करके इंस्टॉलेशन के चरण नीचे दिए गए हैं:

### मावेन स्थापना
अपने में निम्नलिखित निर्भरता जोड़ें `pom.xml` फ़ाइल:
```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

### ग्रेडल स्थापना
इस पंक्ति को अपने में शामिल करें `build.gradle` फ़ाइल:
```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

### प्रत्यक्षत: डाउनलोड
वैकल्पिक रूप से, आप नवीनतम संस्करण को यहां से डाउनलोड कर सकते हैं [Java रिलीज़ के लिए GroupDocs.Signature](https://releases.groupdocs.com/signature/java/).

#### लाइसेंस प्राप्ति चरण
- **मुफ्त परीक्षण**: सुविधाओं का मूल्यांकन करने के लिए परीक्षण से शुरुआत करें।
- **अस्थायी लाइसेंस**: बिना किसी प्रतिबंध के विस्तारित परीक्षण के लिए इसे प्राप्त करें।
- **खरीदना**: दीर्घकालिक उपयोग के लिए, के माध्यम से लाइसेंस खरीदें [ग्रुपडॉक्स खरीदारी पृष्ठ](https://purchase.groupdocs.com/buy).

### बुनियादी आरंभीकरण और सेटअप
एक बार इंस्टॉल हो जाने पर, अपने जावा एप्लिकेशन में GroupDocs.Signature को प्रारंभ करें:
```java
Signature signature = new Signature("YOUR_DOCUMENT_PATH");
```

## कार्यान्वयन मार्गदर्शिका
हम कार्यान्वयन को अलग-अलग विशेषताओं में विभाजित करेंगे: कस्टम डेटा हस्ताक्षर वर्ग निर्माण, XOR एन्क्रिप्शन सेटअप, और मेटाडेटा हस्ताक्षर।

### विशेषता 1: कस्टम डेटा हस्ताक्षर वर्ग
यह सुविधा आपको दस्तावेज़ हस्ताक्षरों के लिए विशिष्ट विशेषताओं जैसे साइन आईडी, लेखक, हस्ताक्षर तिथि और डेटा फैक्टर के साथ एक संरचित प्रारूप परिभाषित करने की अनुमति देती है।

#### चरण 1: DocumentSignatureData वर्ग को परिभाषित करें
```java
import com.groupdocs.signature.domain.extensions.serialization.FormatAttribute;
import java.math.BigDecimal;
import java.util.Date;

public static class DocumentSignatureData {
    @FormatAttribute(propertyName = "SignID")
    public String ID;

    public String getID() { return ID; }
    public void setID(String value) { ID = value; }

    @FormatAttribute(propertyName = "SAuth")
    public final String Author;

    public final String getAuthor() { return Author; }
    public final void setAuthor(String value) { Author = value; }

    @FormatAttribute(propertyName = "SDate", propertyFormat = "yyyy-MM-dd")
    public final Date Signed = new Date();

    public final Date getSigned() { return Signed; }
    public final void setSigned(Date value) { Signed = value; }

    @FormatAttribute(propertyName = "SDFact", propertyFormat = "N2")
    public final BigDecimal DataFactor = new BigDecimal(0.01);

    public final BigDecimal getDataFactor() { return DataFactor; }
    public final void setDataFactor(BigDecimal value) { DataFactor = value; }
}
```
**स्पष्टीकरण**: 
- यह वर्ग प्रत्येक विशेषता को प्रारूपित करने के लिए एनोटेशन का उपयोग करता है, जो क्रमबद्धीकरण में सहायता करता है।
- विशेषताओं में अपरिवर्तनीय फ़ील्ड शामिल हैं `Author` और `Signed`, मेटाडेटा की अखंडता सुनिश्चित करना।

### फ़ीचर 2: कस्टम XOR एन्क्रिप्शन
एक सरल किन्तु प्रभावी एन्क्रिप्शन विधि को क्रियान्वित करते हुए, यह सुविधा आपको XOR तर्क का उपयोग करके दस्तावेज़ डेटा को सुरक्षित करने की अनुमति देती है।

#### चरण 2: CustomXOREncryption क्लास लागू करें
```java
import com.groupdocs.signature.domain.extensions.encryption.IDataEncryption;

class CustomXOREncryption implements IDataEncryption {
    @Override
    public byte[] encrypt(byte[] data) {
        byte[] result = new byte[data.length];
        for (int i = 0; i < data.length; i++) {
            result[i] = (byte)(data[i] ^ 0x5A); // एक कुंजी के साथ XOR
        }
        return result;
    }

    @Override
    public byte[] decrypt(byte[] data) {
        return encrypt(data); // XOR गुणों के कारण डिक्रिप्शन के लिए समान ऑपरेशन
    }
}
```
**स्पष्टीकरण**: 
- The `encrypt` और `decrypt` विधियाँ सममित होती हैं, क्योंकि समान कुंजी वाले XOR ऑपरेशन स्वयं को उलट सकते हैं।

### विशेषता 3: मेटाडेटा हस्ताक्षर सेटअप और हस्ताक्षर
यह सुविधा दर्शाती है कि GroupDocs.Signature का उपयोग करके अपने दस्तावेज़ों में मेटाडेटा हस्ताक्षरों को कैसे कॉन्फ़िगर और लागू किया जाए।

#### चरण 3: कस्टम मेटाडेटा के साथ दस्तावेज़ पर हस्ताक्षर करें
```java
import com.groupdocs.signature.Signature;
import com.groupdocs.signature.domain.signatures.metadata.WordProcessingMetadataSignature;
import com.groupdocs.signature.options.sign.MetadataSignOptions;

import java.io.File;
import java.util.UUID;

public static void signDocumentWithMetadata() throws Exception {
    String filePath = "YOUR_DOCUMENT_DIRECTORY";
    String outputFilePath = new File("YOUR_OUTPUT_DIRECTORY", "SignedDocument.docx").getPath();

    Signature signature = new Signature(filePath);
    IDataEncryption encryption = new CustomXOREncryption();

    MetadataSignOptions options = new MetadataSignOptions();
    options.setDataEncryption(encryption);

    DocumentSignatureData documentSignature = new DocumentSignatureData();
    documentSignature.setID(UUID.randomUUID().toString());
    documentSignature.setAuthor("YourUsername");
    documentSignature.setSigned(new Date());
    documentSignature.setDataFactor(new BigDecimal("11.22"));

    WordProcessingMetadataSignature mdSignature = new WordProcessingMetadataSignature("Signature", documentSignature);
    WordProcessingMetadataSignature mdAuthor = new WordProcessingMetadataSignature("Author", "Mr.Scherlock Holmes");
    mdAuthor.setDataEncryption(encryption);
    WordProcessingMetadataSignature mdDocId = new WordProcessingMetadataSignature("DocumentId", UUID.randomUUID().toString());

    options.getSignatures().add(mdSignature);
    options.getSignatures().add(mdAuthor);
    options.getSignatures().add(mdDocId);

    signature.sign(outputFilePath, options);
}
```
**स्पष्टीकरण**: 
- यह विधि एन्क्रिप्शन के साथ मेटाडेटा हस्ताक्षर सेट करती है और उन्हें दस्तावेज़ पर लागू करती है।
- यह दर्शाता है कि GroupDocs.Signature का उपयोग करके दस्तावेजों को कैसे अनुकूलित और सुरक्षित रूप से हस्ताक्षरित किया जाए।

## व्यावहारिक अनुप्रयोगों
दस्तावेज़ मेटाडेटा को एन्क्रिप्ट करने और हस्ताक्षर करने के लिए यहां कुछ वास्तविक उपयोग के मामले दिए गए हैं:
1. **कानूनी अनुबंध**: अनधिकृत पहुंच को रोकने के लिए मेटाडेटा को एन्क्रिप्ट करके संवेदनशील अनुबंध विवरण को सुरक्षित करें।
2. **स्वास्थ्य सेवा रिकॉर्ड**: एन्क्रिप्टेड हस्ताक्षरों के साथ चिकित्सा दस्तावेजों में रोगी डेटा अखंडता की रक्षा करें।
3. **वित्तीय दस्तावेज़**मेटाडेटा हस्ताक्षर लागू करके वित्तीय लेनदेन की प्रामाणिकता सुनिश्चित करें।
4. **कॉर्पोरेट दस्तावेज़ीकरण**: मजबूत मेटाडेटा सुरक्षा के माध्यम से दस्तावेज़ सुरक्षा और अनुपालन बनाए रखें।

## निष्कर्ष
इस गाइड का पालन करके, आपने सीखा है कि GroupDocs.Signature for Java का उपयोग करके दस्तावेज़ मेटाडेटा को एन्क्रिप्ट और हस्ताक्षरित करके अपने Java अनुप्रयोगों की सुरक्षा कैसे बढ़ाएँ। यह प्रक्रिया न केवल संवेदनशील जानकारी की सुरक्षा करती है, बल्कि विभिन्न व्यावसायिक परिस्थितियों में दस्तावेज़ों की प्रामाणिकता भी सुनिश्चित करती है।