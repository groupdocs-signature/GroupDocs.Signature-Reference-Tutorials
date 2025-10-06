---
"date": "2025-05-08"
"description": "GroupDocs.Signature का उपयोग करके जावा में QR कोड के साथ दस्तावेज़ों पर इलेक्ट्रॉनिक रूप से हस्ताक्षर करना सीखें। अपने दस्तावेज़ प्रबंधन सिस्टम में सुरक्षा और दक्षता बढ़ाएँ।"
"title": "जावा और ग्रुपडॉक्स का उपयोग करके क्यूआर कोड से दस्तावेज़ों पर हस्ताक्षर करें। हस्ताक्षर की एक व्यापक मार्गदर्शिका"
"url": "/hi/java/qr-code-signatures/sign-documents-with-qr-code-java-groupdocs-signature/"
"weight": 1
type: docs
---
# Java और GroupDocs.Signature का उपयोग करके QR कोड से दस्तावेज़ों पर हस्ताक्षर करें

क्या आप अपने दस्तावेज़ प्रबंधन सिस्टम में सुरक्षा और दक्षता का एक अतिरिक्त स्तर जोड़ना चाहते हैं? आज के डिजिटल युग में दस्तावेज़ों पर इलेक्ट्रॉनिक रूप से हस्ताक्षर करना एक ज़रूरी सुविधा है, और क्यूआर-कोड हस्ताक्षर सुविधा और मज़बूती दोनों प्रदान करते हैं। इस विस्तृत गाइड में, हम Java के लिए GroupDocs.Signature का उपयोग करके क्यूआर कोड के साथ छवि दस्तावेज़ों पर हस्ताक्षर करने का तरीका जानेंगे। इस ट्यूटोरियल के अंत तक, आप इन सुविधाओं को आसानी से लागू कर पाएँगे।

## आप क्या सीखेंगे
- अपने प्रोजेक्ट में Java के लिए GroupDocs.Signature सेट अप करना
- QR-कोड हस्ताक्षर विकल्प बनाना और कॉन्फ़िगर करना
- विभिन्न आउटपुट स्वरूपों के लिए छवि सहेजने के विकल्प कॉन्फ़िगर करना
- क्यूआर कोड के साथ दस्तावेजों पर हस्ताक्षर करने के वास्तविक-विश्व अनुप्रयोग

आइये इस रोमांचक यात्रा की शुरुआत करें!

### आवश्यक शर्तें
कार्यान्वयन में उतरने से पहले, सुनिश्चित करें कि आपने निम्नलिखित बातों को शामिल कर लिया है:

- **लाइब्रेरी और निर्भरताएँ:** आपको GroupDocs.Signature लाइब्रेरी की आवश्यकता होगी। सुनिश्चित करें कि आप संगतता के लिए संस्करण 23.12 का उपयोग करते हैं।
- **पर्यावरण सेटअप:** यह मार्गदर्शिका जावा विकास वातावरण जैसे मावेन या ग्रैडल की बुनियादी समझ पर आधारित है।
- **ज्ञान पूर्वापेक्षाएँ:** जावा प्रोग्रामिंग, जावा में फ़ाइल हैंडलिंग, और XML/Gradle बिल्ड फ़ाइलों का बुनियादी ज्ञान लाभदायक है।

### Java के लिए GroupDocs.Signature सेट अप करना
Java के लिए GroupDocs.Signature का उपयोग शुरू करने के लिए, Maven या Gradle के माध्यम से अपने प्रोजेक्ट में निर्भरता जोड़ें:

**मावेन:**
```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

**ग्रेडेल:**
```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

वैकल्पिक रूप से, नवीनतम संस्करण को सीधे यहां से डाउनलोड करें [Java रिलीज़ के लिए GroupDocs.Signature](https://releases.groupdocs.com/signature/java/).

परीक्षण या खरीदारी शुरू करने के लिए:
- **निःशुल्क परीक्षण और लाइसेंस प्राप्ति:** मिलने जाना [ग्रुपडॉक्स के निःशुल्क परीक्षण](https://releases.groupdocs.com/signature/java/) लाइब्रेरी को डाउनलोड करने के लिए.
- **अस्थायी लाइसेंस:** यदि आपको मूल्यांकन के लिए अधिक समय चाहिए, तो अस्थायी लाइसेंस के लिए अनुरोध करें [ग्रुपडॉक्स अस्थायी लाइसेंस](https://purchase.groupdocs.com/temporary-license/).
- **खरीदना:** पूर्ण सुविधाओं और समर्थन के लिए, लाइसेंस खरीदें [ग्रुपडॉक्स खरीदारी](https://purchase.groupdocs.com/buy).

#### मूल आरंभीकरण
एक बार जब लाइब्रेरी आपके प्रोजेक्ट में स्थापित हो जाए, तो इसे निम्न प्रकार से आरंभ करें:
```java
import com.groupdocs.signature.Signature;

public class InitializeSignature {
    public void setup() {
        Signature signature = new Signature("SampleImage.jpg");
        // आपका आरंभीकरण कोड यहां...
    }
}
```

### कार्यान्वयन मार्गदर्शिका
अब जब आपने सब कुछ सेट कर लिया है, तो चलिए QR-कोड हस्ताक्षर सुविधा को क्रियान्वित करते हैं।

#### क्यूआर-कोड हस्ताक्षर के साथ दस्तावेज़ पर हस्ताक्षर करें
यह अनुभाग आपको Java के लिए GroupDocs.Signature का उपयोग करके एक छवि दस्तावेज़ में एक QR-कोड हस्ताक्षर जोड़ने के माध्यम से मार्गदर्शन करेगा।

**चरण:**
1. **हस्ताक्षर इंस्टेंस बनाएँ:** आरंभ करें `Signature` अपने दस्तावेज़ के पथ के साथ class जोड़ें.
   ```java
   String filePath = "YOUR_DOCUMENT_DIRECTORY/SampleImage.jpg";
   Signature signature = new Signature(filePath);
   ```

2. **QR-कोड साइन विकल्प कॉन्फ़िगर करें:** पाठ और स्थिति निर्दिष्ट करते हुए QR-कोड विकल्प सेट करें।
   ```java
   import com.groupdocs.signature.options.sign.QrCodeSignOptions;
   import com.groupdocs.signature.domain.qrcodes.QrCodeTypes;

   QrCodeSignOptions signOptions = new QrCodeSignOptions("JohnSmith");
   signOptions.setEncodeType(QrCodeTypes.QR);
   signOptions.setLeft(100);  // बाईं ओर से स्थिति
   signOptions.setTop(100);   // ऊपर की ओर से स्थिति
   ```

3. **छवि सहेजें विकल्प सेट करें:** परिभाषित करें कि हस्ताक्षरित दस्तावेज़ कैसे और कहाँ सहेजा जाएगा.
   ```java
   import com.groupdocs.signature.options.saveoptions.imagessaveoptions.ImageSaveOptions;
   import com.groupdocs.signature.domain.enums.ImageSaveFileFormat;

   String outputFilePath = "YOUR_OUTPUT_DIRECTORY/SaveSignedOutputType/SampleJPG.svg";
   ImageSaveOptions saveOptions = new ImageSaveOptions();
   saveOptions.setFileFormat(ImageSaveFileFormat.Svg);
   saveOptions.setOverwriteExistingFiles(true);
   ```

4. **दस्तावेज़ पर हस्ताक्षर करें और उसे सहेजें:** कॉन्फ़िगर किए गए विकल्पों का उपयोग करके QR-कोड हस्ताक्षर लागू करें।
   ```java
   try {
       signature.sign(outputFilePath, signOptions, saveOptions);
   } catch (Exception e) {
       throw new GroupDocsSignatureException(e.getMessage());
   }
   ```

#### हस्ताक्षर के लिए QR-कोड विकल्प कॉन्फ़िगर करें
अपने दस्तावेज़ के QR-कोड हस्ताक्षरों पर अधिक नियंत्रण के लिए:

**चरण:**
1. **QR-कोड विकल्प बनाएं और अनुकूलित करें:**
    ```java
    public QrCodeSignOptions createQRCodeOptions() {
        QrCodeSignOptions signOptions = new QrCodeSignOptions("JohnSmith");
        signOptions.setEncodeType(QrCodeTypes.QR);
        signOptions.setLeft(100);  // आवश्यकतानुसार स्थिति अनुकूलित करें
        signOptions.setTop(100);
        
        return signOptions;
    }
    ```
   - `QrCodeSignOptions(String text)`: निर्दिष्ट पाठ के साथ QR-कोड विकल्पों को आरंभ करता है।
   - `setEncodeType(QrCodeTypes type)`: QR कोड प्रकार को परिभाषित करता है.
   - `setLeft(int left)` और `setTop(int top)`: दस्तावेज़ पर QR कोड को स्थान देता है.

#### आउटपुट स्वरूप के लिए छवि सहेजने के विकल्प कॉन्फ़िगर करें
नियंत्रित करें कि आपके हस्ताक्षरित दस्तावेज़ कहाँ संग्रहीत हैं और वे किस प्रारूप में सहेजे गए हैं:

**चरण:**
1. **छवि सहेजें विकल्प बनाएँ और सेट करें:**
    ```java
    public ImageSaveOptions createImageSaveOptions() {
        ImageSaveOptions saveOptions = new ImageSaveOptions();
        saveOptions.setFileFormat(ImageSaveFileFormat.Svg);  // इसे PNG, JPG जैसे अन्य प्रारूपों में बदला जा सकता है।
        saveOptions.setOverwriteExistingFiles(true);
        
        return saveOptions;
    }
    ```
   - `setFileFormat(ImageSaveFileFormat format)`आउटपुट फ़ाइल का प्रारूप निर्धारित करता है.
   - `setOverwriteExistingFiles(boolean overwrite)`: यह निर्णय लेता है कि मौजूदा फ़ाइलों को अधिलेखित करना है या नहीं।

### व्यावहारिक अनुप्रयोगों
क्यूआर-कोड हस्ताक्षर बहुमुखी हैं और विभिन्न वास्तविक दुनिया परिदृश्यों में उपयोग किए जा सकते हैं:
1. **अनुबंध पर हस्ताक्षर:** डिजिटल सत्यापन प्रणालियों से जुड़े क्यूआर कोड के साथ सुरक्षित रूप से अनुबंधों पर हस्ताक्षर करें।
2. **दस्तावेज़ प्रमाणीकरण:** दस्तावेजों को प्रमाणित करने के लिए छेड़छाड़-रोधी विधि के रूप में क्यूआर कोड का उपयोग करें।
3. **सूची प्रबंधन:** इन्वेंट्री आइटमों पर क्यूआर कोड संलग्न करें, जिससे शिपमेंट की ट्रैकिंग और हस्ताक्षर करना आसान हो जाएगा।

### प्रदर्शन संबंधी विचार
जावा अनुप्रयोगों में GroupDocs.Signature को क्रियान्वित करते समय:
- **संसाधन उपयोग को अनुकूलित करें:** प्रसंस्करण के बाद स्ट्रीम्स को बंद करके कुशल मेमोरी प्रबंधन सुनिश्चित करें।
- **प्रदर्शन सुझाव:** यदि आवश्यक हो तो दस्तावेजों के बड़े बैच को संभालने के लिए मल्टी-थ्रेडिंग का उपयोग करें।
- **सर्वोत्तम प्रथाएं:** बेहतर प्रदर्शन और नई सुविधाओं के लिए GroupDocs.Signature के नवीनतम संस्करण को नियमित रूप से अपडेट करें।

### निष्कर्ष
इस ट्यूटोरियल में, आपने GroupDocs.Signature का उपयोग करके अपने Java अनुप्रयोगों में QR-कोड हस्ताक्षरों को एकीकृत करना सीखा। यह सुविधा न केवल दस्तावेज़ सुरक्षा को बढ़ाती है, बल्कि डिजिटल वर्कफ़्लो को भी सरल बनाती है। यहाँ प्राप्त ज्ञान के साथ, आप अपनी परियोजनाओं में इन शक्तिशाली उपकरणों को लागू करने के लिए पूरी तरह से तैयार हैं। और भी मज़बूत समाधानों के लिए GroupDocs.Signature की अतिरिक्त सुविधाओं का अन्वेषण करें।

### कीवर्ड अनुशंसाएँ
- "जावा के साथ क्यूआर कोड हस्ताक्षर"
- "ग्रुपडॉक्स हस्ताक्षर कार्यान्वयन"
- "इलेक्ट्रॉनिक दस्तावेज़ हस्ताक्षर"