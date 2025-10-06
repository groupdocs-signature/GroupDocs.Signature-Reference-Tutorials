---
"date": "2025-05-08"
"description": "Java के लिए GroupDocs.Signature के साथ QR कोड एन्क्रिप्शन और डिजिटल हस्ताक्षर का उपयोग करके PDF फ़ाइलों को सुरक्षित करना सीखें। अपने दस्तावेज़ों की सुरक्षा को प्रभावी ढंग से बढ़ाएँ।"
"title": "GroupDocs.Signature का उपयोग करके जावा में QR कोड एन्क्रिप्शन के साथ सुरक्षित PDF हस्ताक्षर लागू करें"
"url": "/hi/java/qr-code-signatures/secure-pdf-signing-qr-code-groupdocs-java/"
"weight": 1
type: docs
---
# GroupDocs.Signature का उपयोग करके जावा में QR कोड एन्क्रिप्शन के साथ सुरक्षित PDF हस्ताक्षर कैसे लागू करें

आज के डिजिटल युग में, दस्तावेज़ों में संवेदनशील जानकारी की सुरक्षा अत्यंत महत्वपूर्ण है। साइबर खतरों के बढ़ते मामलों ने डेटा एन्क्रिप्शन को दस्तावेज़ प्रबंधन का एक अनिवार्य हिस्सा बना दिया है। यह ट्यूटोरियल आपको GroupDocs.Signature for Java के साथ QR कोड एन्क्रिप्शन का उपयोग करके सुरक्षित PDF हस्ताक्षर लागू करने में मार्गदर्शन करता है। इस लेख के अंत तक, आप अपने एप्लिकेशन में मज़बूत सुरक्षा सुविधाओं को एकीकृत करने में सक्षम हो जाएँगे।

## आप क्या सीखेंगे:
- जावा में सममित डेटा एन्क्रिप्शन को समझना
- एक कस्टम हस्ताक्षर वर्ग बनाना
- कस्टम डेटा और संरेखण के साथ QR-कोड हस्ताक्षर कॉन्फ़िगर करना
- सुरक्षित PDF हस्ताक्षर के लिए GroupDocs.Signature को एकीकृत करना

क्या आप इसमें शामिल होने के लिए तैयार हैं? चलिए शुरू करते हैं!

## आवश्यक शर्तें
शुरू करने से पहले, सुनिश्चित करें कि आपके पास निम्नलिखित हैं:
- **जावा डेवलपमेंट किट (JDK):** संस्करण 8 या उच्चतर.
- **मावेन या ग्रेडेल:** निर्भरता प्रबंधन के लिए। अपने प्रोजेक्ट सेटअप के आधार पर चुनें।
- **जावा प्रोग्रामिंग का ज्ञान:** जावा में ऑब्जेक्ट-ओरिएंटेड प्रोग्रामिंग की बुनियादी समझ।

## Java के लिए GroupDocs.Signature सेट अप करना
GroupDocs.Signature का उपयोग शुरू करने के लिए, आपको इसे अपनी परियोजना में एक निर्भरता के रूप में जोड़ना होगा। यह लाइब्रेरी डिजिटल हस्ताक्षर और दस्तावेज़ एन्क्रिप्शन के प्रबंधन के लिए शक्तिशाली उपकरण प्रदान करती है।

### मावेन सेटअप
अपने में निम्नलिखित निर्भरता जोड़ें `pom.xml` फ़ाइल:
```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

### ग्रेडल सेटअप
Gradle उपयोगकर्ताओं के लिए, इसे अपने में शामिल करें `build.gradle` फ़ाइल:
```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

### प्रत्यक्षत: डाउनलोड
वैकल्पिक रूप से, नवीनतम संस्करण यहां से डाउनलोड करें [Java रिलीज़ के लिए GroupDocs.Signature](https://releases.groupdocs.com/signature/java/).

### लाइसेंस अधिग्रहण
आप GroupDocs.Signature की सुविधाओं का मूल्यांकन करने के लिए इसका निःशुल्क परीक्षण शुरू कर सकते हैं। विस्तारित उपयोग के लिए, लाइसेंस खरीदने या उनकी वेबसाइट के माध्यम से अस्थायी लाइसेंस के लिए आवेदन करने पर विचार करें।

## कार्यान्वयन मार्गदर्शिका
यह मार्गदर्शिका प्रमुख खंडों में विभाजित है जो डेटा एन्क्रिप्शन, कस्टम हस्ताक्षर निर्माण और क्यूआर-कोड हस्ताक्षर कॉन्फ़िगरेशन को कवर करते हैं।

### सममित एल्गोरिथ्म के साथ डेटा एन्क्रिप्शन
अपने डेटा को एन्क्रिप्ट करने से यह सुनिश्चित होता है कि ट्रांसमिशन और स्टोरेज के दौरान यह सुरक्षित रहे। GroupDocs.Signature का उपयोग करके सममित एन्क्रिप्शन सेट अप करने का तरीका यहां दिया गया है:

#### सममित एन्क्रिप्शन सेट अप करना
1. **आवश्यक पैकेज आयात करें:**
   ```java
   import com.groupdocs.signature.domain.extensions.encryption.IDataEncryption;
   import com.groupdocs.signature.domain.extensions.encryption.SymmetricAlgorithmType;
   import com.groupdocs.signature.domain.extensions.encryption.SymmetricEncryption;
   ```
2. **एन्क्रिप्शन ऑब्जेक्ट को आरंभ करें:**
   एन्क्रिप्शन के लिए सुरक्षित कुंजी और सॉल्ट का इस्तेमाल करें। `"YOUR_SECURE_KEY"` अपनी स्वयं की चाबियों के साथ.
   ```java
   String key = "YOUR_SECURE_KEY";
   String salt = "YOUR_SECURE_SALT";

   IDataEncryption encryption = new SymmetricEncryption(
       SymmetricAlgorithmType.Rijndael, 
       key, 
       salt
   );
   ```
   - **सममितएल्गोरिदमप्रकार.रिजंडेल:** यह उपयोग किये जाने वाले सममित एल्गोरिथ्म के प्रकार को निर्दिष्ट करता है।
   - **कुंजी और नमक:** सुनिश्चित करें कि ये आपके अनुप्रयोग के लिए अद्वितीय और सुरक्षित हैं।

### कस्टम डेटा हस्ताक्षर वर्ग
एक कस्टम क्लास बनाने से आप सिग्नेचर प्रॉपर्टीज़ को प्रभावी ढंग से प्रबंधित कर सकते हैं। यह कैसे करें:

#### परिभाषित करना `DocumentSignatureData` कक्षा
```java
class DocumentSignatureData {
    private String ID;
    private String Author;
    private Date Signed = new Date();
    private BigDecimal DataFactor = new BigDecimal(0.01);

    public String getID() { return ID; }
    public void setID(String value) { ID = value; }

    public final String getAuthor() { return Author; }
    public final void setAuthor(String value) { Author = value; }

    public final Date getSigned() { return Signed; }
    public final void setSigned(Date value) { Signed = value; }

    public final BigDecimal getDataFactor() { return DataFactor; }
    public final void setDataFactor(BigDecimal value) { DataFactor = value; }
}
```
- **आईडी, लेखक, हस्ताक्षर:** ये फ़ील्ड हस्ताक्षर का मेटाडेटा संग्रहीत करते हैं.
- **डेटाफ़ैक्टर:** आपके अनुप्रयोग के तर्क से संबंधित एक संख्यात्मक मान रखता है।

### क्यूआर-कोड हस्ताक्षर विकल्प
क्यूआर कोड जानकारी को एम्बेड करने का एक संक्षिप्त तरीका प्रदान करते हैं। इन्हें कस्टम डेटा और एन्क्रिप्शन के साथ कॉन्फ़िगर करें:

#### क्यूआर-कोड हस्ताक्षर सेट अप करना
1. **प्रारंभ `Signature` वस्तु:**
   ```java
   import com.groupdocs.signature.Signature;
   
   Signature signature = new Signature("YOUR_DOCUMENT_DIRECTORY");
   ```
2. **QR कोड विकल्प कॉन्फ़िगर करें:**
   ```java
   import com.groupdocs.signature.domain.qrcodes.QrCodeTypes;
   import com.groupdocs.signature.options.sign.QrCodeSignOptions;
   import java.util.UUID;

   DocumentSignatureData documentSignature = new DocumentSignatureData();
   documentSignature.setID(UUID.randomUUID().toString());
   documentSignature.setAuthor(System.getenv("USERNAME"));
   documentSignature.setDataFactor(new BigDecimal("11.22"));

   QrCodeSignOptions options = new QrCodeSignOptions();
   options.setData(documentSignature);
   options.setEncodeType(QrCodeTypes.QR);
   options.setDataEncryption(encryption); // एन्क्रिप्शन ऑब्जेक्ट का उपयोग करें
   options.setHeight(100);
   options.setWidth(100);
   options.setVerticalAlignment(com.groupdocs.signature.domain.enums.VerticalAlignment.Bottom);
   options.setHorizontalAlignment(com.groupdocs.signature.domain.enums.HorizontalAlignment.Right);

   import com.groupdocs.signature.domain.Padding;
   Padding padding = new Padding();
   padding.setRight(10);
   padding.setBottom(10);
   options.setMargin(padding);
   ```
   - **एन्कोडिंग प्रकार:** QR कोड प्रारूप निर्दिष्ट करता है.
   - **संरेखण और मार्जिन:** दस्तावेज़ पर QR कोड कैसे दिखाई दे, इसे अनुकूलित करें.

### उदाहरण उपयोग
अपने कॉन्फ़िगर किए गए विकल्पों के साथ दस्तावेज़ पर हस्ताक्षर करने के लिए:
```java
signature.sign("YOUR_OUTPUT_DIRECTORY/QRCodeEncryptedObject.pdf\