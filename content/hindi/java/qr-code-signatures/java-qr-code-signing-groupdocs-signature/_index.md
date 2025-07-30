---
"date": "2025-05-08"
"description": "GroupDocs.Signature का उपयोग करके Java QR कोड साइनिंग को लागू करने का तरीका जानें। अपने Java अनुप्रयोगों में दस्तावेज़ सुरक्षा बढ़ाएँ, साइन विकल्प कॉन्फ़िगर करें, और कस्टम एन्क्रिप्शन लागू करें।"
"title": "जावा क्यूआर कोड हस्ताक्षर गाइड - GroupDocs.Signature के साथ अपने दस्तावेज़ सुरक्षित करें"
"url": "/hi/java/qr-code-signatures/java-qr-code-signing-groupdocs-signature/"
"weight": 1
---

# Java के लिए GroupDocs.Signature के साथ Java QR कोड हस्ताक्षर को कार्यान्वित करना

## परिचय

अपने जावा एप्लिकेशन में क्यूआर कोड एम्बेड करके अपने डिजिटल दस्तावेज़ों की सुरक्षा बढ़ाएँ। जावा के लिए GroupDocs.Signature का उपयोग करके आप दस्तावेज़ों की प्रामाणिकता और ट्रेसबिलिटी को प्रभावी ढंग से सुनिश्चित कर सकते हैं। यह मार्गदर्शिका आपको कस्टम डेटा सिग्नेचर बनाने, क्यूआर कोड साइनिंग विकल्पों को कॉन्फ़िगर करने और अपने दस्तावेज़ों को मज़बूत एन्क्रिप्शन से सुरक्षित करने में मदद करेगी।

**आप क्या सीखेंगे:**
- GroupDocs.Signature का उपयोग करके कस्टम डेटा हस्ताक्षर वर्ग कैसे बनाएँ
- जावा अनुप्रयोगों में QR कोड चिह्न विकल्पों को कॉन्फ़िगर करना
- क्यूआर कोड के साथ दस्तावेज़ों पर हस्ताक्षर करना और कस्टम एन्क्रिप्शन लागू करना

आइए पूर्वापेक्षाओं पर गौर करें और इस कार्यक्षमता को अपनी परियोजनाओं में एकीकृत करना शुरू करें!

## आवश्यक शर्तें

आरंभ करने से पहले, सुनिश्चित करें कि आपने अपने विकास परिवेश में आवश्यक लाइब्रेरीज़ और निर्भरताएं स्थापित कर ली हैं।

### आवश्यक लाइब्रेरी और संस्करण

Java के लिए GroupDocs.Signature को क्रियान्वित करने के लिए, निम्नलिखित निर्भरता शामिल करें:

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
implementation 'com.groupdocs:groupdocs-signation:23.12'
```

आप नवीनतम संस्करण को सीधे यहां से भी डाउनलोड कर सकते हैं [Java रिलीज़ के लिए GroupDocs.Signature](https://releases.groupdocs.com/signature/java/).

### पर्यावरण सेटअप आवश्यकताएँ

- सुनिश्चित करें कि आपके पास कार्यशील जावा डेवलपमेंट किट (JDK) स्थापित है।
- अपना एकीकृत विकास वातावरण (IDE) सेट करें, जैसे कि IntelliJ IDEA या Eclipse.

### ज्ञान पूर्वापेक्षाएँ

- जावा प्रोग्रामिंग और ऑब्जेक्ट-ओरिएंटेड अवधारणाओं की बुनियादी समझ।
- मावेन या ग्रेडेल का उपयोग करके निर्भरताओं को संभालने की जानकारी।

## Java के लिए GroupDocs.Signature सेट अप करना

आरंभ करने के लिए, अपने बिल्ड कॉन्फ़िगरेशन में इसे शामिल करने के लिए ऊपर दिए गए इंस्टॉलेशन निर्देशों का पालन करके अपने प्रोजेक्ट में GroupDocs.Signature सेट अप करें।

### लाइसेंस प्राप्ति चरण

ग्रुपडॉक्स विभिन्न लाइसेंसिंग विकल्प प्रदान करता है:
- **मुफ्त परीक्षण**: बिना किसी सीमा के सभी सुविधाओं का परीक्षण करें।
- **अस्थायी लाइसेंस**: मूल्यांकन प्रयोजनों के लिए लाइसेंस प्राप्त करें।
- **खरीदना**: वाणिज्यिक उपयोग के लिए पूर्ण लाइसेंस प्राप्त करें।

डाउनलोड करने के बाद, GroupDocs.Signature को इस प्रकार प्रारंभ करें:

```java
import com.groupdocs.signature.Signature;

class InitializeGroupDocs {
    public static void main(String[] args) {
        Signature signature = new Signature("path/to/your/document");
        // अब आप दस्तावेज़ों के साथ काम करने के लिए हस्ताक्षर ऑब्जेक्ट का उपयोग शुरू कर सकते हैं।
    }
}
```

## कार्यान्वयन मार्गदर्शिका

आइए कार्यान्वयन प्रक्रिया को प्रबंधनीय खंडों में विभाजित करें, तथा प्रमुख विशेषताओं पर ध्यान केंद्रित करें।

### कस्टम डेटा हस्ताक्षर वर्ग

#### अवलोकन
हस्ताक्षर डेटा, जैसे आईडी, लेखक, हस्ताक्षर तिथि, और अन्य कारक, संग्रहीत करने के लिए एक कस्टम क्लास बनाएँ। इससे यह सुनिश्चित होता है कि आपके हस्ताक्षरों में सभी आवश्यक मेटाडेटा समाहित हैं।

#### चरण-दर-चरण कार्यान्वयन

**DocumentSignatureData वर्ग को परिभाषित करें**

```java
import com.groupdocs.signature.domain.extensions.serialization.FormatAttribute;
import java.util.Date;
import java.math.BigDecimal;

class DocumentSignatureData {
    @FormatAttribute(propertyName = "SignID")
    public String ID; // हस्ताक्षर के लिए विशिष्ट पहचानकर्ता
    
    public String getID() { return ID; }
    public void setID(String value) { ID = value; }
    
    @FormatAttribute(propertyName = "SAuth")
    public final String Author; // दस्तावेज़ के लेखक
    
    public final String getAuthor() { return Author; }
    public final void setAuthor(String value) { Author = value; }
    
    @FormatAttribute(propertyName = "SDate", propertyFormat = "yyyy-MM-dd")
    public final Date Signed = new Date(); // हस्ताक्षर की तिथि और समय
    
    public final Date getSigned() { return Signed; }
    public final void setSigned(Date value) { Signed = value; }
    
    @FormatAttribute(propertyName = "SDFact", propertyFormat = "N2")
    public final BigDecimal DataFactor = new BigDecimal(0.01); // हस्ताक्षर के लिए अतिरिक्त डेटा कारक
    
    public final BigDecimal getDataFactor() { return DataFactor; }
    public final void setDataFactor(BigDecimal value) { DataFactor = value; }
}
```

**स्पष्टीकरण:**
- **प्रारूप विशेषता**: क्रमांकन को अनुकूलित करने के लिए गुणों पर टिप्पणी करता है।
- **गुण**: विशिष्ट आईडी, लेखक का नाम, हस्ताक्षर तिथि और डेटा फैक्टर जैसे आवश्यक विवरण कैप्चर करें।

### QR कोड साइन विकल्प कॉन्फ़िगरेशन

#### अवलोकन
अपने QR कोड को दस्तावेज़ों पर कैसे प्रदर्शित किया जाएगा, यह निर्धारित करने के लिए QR कोड चिह्न विकल्पों को कॉन्फ़िगर करें, जिसमें आकार, संरेखण और पैडिंग शामिल हैं।

#### चरण-दर-चरण कार्यान्वयन

**QrCodeSignOptionsConfig वर्ग को परिभाषित करें**

```java
import com.groupdocs.signature.domain.enums.HorizontalAlignment;
import com.groupdocs.signature.domain.enums.VerticalAlignment;
import com.groupdocs.signature.domain.qrcodes.QrCodeTypes;
import com.groupdocs.signature.domain.Padding;
import com.groupdocs.signature.options.sign.QrCodeSignOptions;

class QrCodeSignOptionsConfig {
    public static QrCodeSignOptions setupQrCodeSignOptions(DocumentSignatureData documentSignature) {
        QrCodeSignOptions options = new QrCodeSignOptions();
        
        // कस्टम डेटा ऑब्जेक्ट को QR कोड में क्रमबद्ध करें
        options.setData(documentSignature);
        
        // QR कोड प्रकार निर्दिष्ट करें
        options.setEncodeType(QrCodeTypes.QR);
        
        // संरेखण के लिए पैडिंग कॉन्फ़िगर करें
        Padding padding = new Padding();
        padding.setRight(10); // पिक्सेल में दायाँ पैडिंग
        padding.setBottom(10); // पिक्सेल में निचला पैडिंग
        options.setMargin(padding);
        
        // QR कोड का आकार और स्थिति निर्धारित करें
        options.setHeight(100);
        options.setWidth(100);
        options.setVerticalAlignment(VerticalAlignment.Bottom);
        options.setHorizontalAlignment(HorizontalAlignment.Right);
        
        return options;
    }
}
```

**स्पष्टीकरण:**
- **QrCodeSignOptions**: यह प्रबंधित करता है कि QR कोड कैसे प्रदर्शित किया जाए, जिसमें उसका आकार और स्थिति शामिल है.
- **पैडिंग**दस्तावेज़ के भीतर संरेखण समायोजित करता है.

### क्यूआर कोड और कस्टम एन्क्रिप्शन के साथ दस्तावेज़ पर हस्ताक्षर

#### अवलोकन
दस्तावेज़ों पर सुरक्षित रूप से हस्ताक्षर करने के लिए क्यूआर कोड और कस्टम एन्क्रिप्शन का संयोजन करें। यह डेटा की अखंडता और गोपनीयता सुनिश्चित करता है।

#### चरण-दर-चरण कार्यान्वयन

**QR कोड से दस्तावेज़ पर हस्ताक्षर करें**

```java
import com.groupdocs.signature.Signature;
import com.groupdocs.signature.domain.extensions.encryption.IDataEncryption;
import com.groupdocs.signature.exception.GroupDocsSignatureException;

import java.util.UUID;

class SignDocumentWithQRCode {
    public static void signDocument(String filePath, String outputFilePath) throws Exception {
        try {
            Signature signature = new Signature(filePath);

            // कस्टम XOR एन्क्रिप्शन रणनीति
            IDataEncryption encryption = new CustomXOREncryption();

            // कस्टम दस्तावेज़ हस्ताक्षर डेटा ऑब्जेक्ट कॉन्फ़िगर करें
            DocumentSignatureData documentSignature = new DocumentSignatureData();
            documentSignature.setID(UUID.randomUUID().toString());
            documentSignature.setAuthor(System.getenv("USERNAME"));
            documentSignature.setSigned(new Date());
            documentSignature.setDataFactor(new BigDecimal("11.22"));

            // QR-कोड विकल्प सेटअप करें
            QrCodeSignOptions options = QrCodeSignOptionsConfig.setupQrCodeSignOptions(documentSignature);

            // QR कोड के भीतर डेटा पर एन्क्रिप्शन लागू करें
            options.setDataEncryption(encryption);

            // दस्तावेज़ पर हस्ताक्षर करें और उसे सहेजें
            signature.sign(outputFilePath, options);
        } catch (Exception e) {
            throw new GroupDocsSignatureException(e.getMessage());
        }
    }
}
```

**स्पष्टीकरण:**
- **कस्टमXORE एन्क्रिप्शन**: क्यूआर कोड डेटा को सुरक्षित करने के लिए एक कस्टम एन्क्रिप्शन रणनीति लागू करता है।
- **यूयूआईडी**: प्रत्येक हस्ताक्षर के लिए एक अद्वितीय पहचानकर्ता उत्पन्न करता है।