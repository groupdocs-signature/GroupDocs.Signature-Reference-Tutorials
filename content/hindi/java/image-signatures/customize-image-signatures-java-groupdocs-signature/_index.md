---
"date": "2025-05-08"
"description": "GroupDocs.Signature के साथ जावा में कस्टमाइज़्ड इमेज सिग्नेचर लागू करने का तरीका जानें। यह गाइड पोज़िशनिंग, अलाइनमेंट, अपीयरेंस एडजस्टमेंट और बॉर्डर कस्टमाइज़ेशन को कवर करती है।"
"title": "GroupDocs.Signature का उपयोग करके जावा में छवि हस्ताक्षरों को कैसे अनुकूलित करें"
"url": "/hi/java/image-signatures/customize-image-signatures-java-groupdocs-signature/"
"weight": 1
type: docs
---
# Java के लिए GroupDocs.Signature का उपयोग करके अनुकूलित छवि हस्ताक्षर कैसे लागू करें

## परिचय

आज की डिजिटल दुनिया में, कई व्यावसायिक प्रक्रियाओं के लिए इलेक्ट्रॉनिक दस्तावेज़ हस्ताक्षर आवश्यक हैं। यह सुनिश्चित करना कि आपका हस्ताक्षर दस्तावेज़ पर ठीक उसी जगह दिखाई दे जहाँ आप चाहते हैं, और साथ ही एक पेशेवर रूप बनाए रखना चुनौतीपूर्ण हो सकता है। **Java के लिए GroupDocs.Signature** अनुप्रयोगों में इलेक्ट्रॉनिक हस्ताक्षरों को सहजता से एकीकृत करने के लिए शक्तिशाली अनुकूलन विकल्प प्रदान करता है।

यह ट्यूटोरियल आपको Java के लिए GroupDocs.Signature सेटअप करने में मार्गदर्शन करता है और आकार, संरेखण, रूप समायोजन और बॉर्डर अनुकूलन जैसे विभिन्न कॉन्फ़िगरेशन का उपयोग करके इमेज सिग्नेचर की स्थिति, संरेखण और स्टाइलिंग जैसी प्रमुख विशेषताओं का अन्वेषण करता है। इस लेख के अंत तक, आप जानेंगे कि कैसे:
- हस्ताक्षर की स्थिति और आकार निर्धारित करें
- हस्ताक्षर को हाशिये के साथ संरेखित करें
- छवि उपस्थिति सेटिंग्स समायोजित करें
- छवि बॉर्डर अनुकूलित करें

आइये इसमें गोता लगाएँ!

## आवश्यक शर्तें

आरंभ करने से पहले, सुनिश्चित करें कि आपके पास निम्नलिखित पूर्वापेक्षाएँ तैयार हैं:
1. **जावा डेवलपमेंट किट (JDK)**सुनिश्चित करें कि आपके सिस्टम पर JDK 8 या उच्चतर संस्करण स्थापित है।
2. **एकीकृत विकास वातावरण (IDE)**जावा विकास के लिए IntelliJ IDEA या Eclipse जैसे IDE का उपयोग करें।
3. **GroupDocs.Signature लाइब्रेरी**: अपने प्रोजेक्ट में निर्भरता के रूप में GroupDocs.Signature जोड़ें।

### आवश्यक लाइब्रेरी और निर्भरताएँ

GroupDocs.Signature को शामिल करने के लिए, आप Maven या Gradle का उपयोग कर सकते हैं:

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

वैकल्पिक रूप से, नवीनतम संस्करण को सीधे यहां से डाउनलोड करें [Java रिलीज़ के लिए GroupDocs.Signature](https://releases.groupdocs.com/signature/java/).

### पर्यावरण सेटअप

सुनिश्चित करें कि आपका IDE बाह्य लाइब्रेरीज़ को शामिल करने के लिए कॉन्फ़िगर किया गया है और इनपुट दस्तावेज़ों, हस्ताक्षर छवियों और आउटपुट हस्ताक्षरित दस्तावेज़ों के लिए निर्देशिकाओं के साथ एक प्रोजेक्ट सेट अप करें।

### ज्ञान पूर्वापेक्षाएँ

- जावा प्रोग्रामिंग की बुनियादी समझ.
- जावा अनुप्रयोगों में फ़ाइल पथों को संभालने की जानकारी।

## Java के लिए GroupDocs.Signature सेट अप करना

GroupDocs.Signature का उपयोग शुरू करने के लिए, इन सेटअप चरणों का पालन करें:
1. **निर्भरता जोड़ें**: लाइब्रेरी को शामिल करने के लिए प्रदान किए गए Maven या Gradle कॉन्फ़िगरेशन का उपयोग करें।
2. **लाइसेंस अधिग्रहण**: से एक निःशुल्क परीक्षण डाउनलोड करके प्रारंभ करें [ग्रुपडॉक्स](https://releases.groupdocs.com/signature/java/) और यदि आवश्यक हो तो लाइसेंस खरीदने पर विचार करें।

### मूल आरंभीकरण

यहां बताया गया है कि आप अपने जावा एप्लिकेशन में GroupDocs.Signature को कैसे आरंभ करते हैं:

```java
import com.groupdocs.signature.Signature;

public class Main {
    public static void main(String[] args) throws Exception {
        String filePath = "path/to/your/document.docx";
        Signature signature = new Signature(filePath);
        
        // अतिरिक्त सेटअप और उपयोग के लिए यहां जाएं
    }
}
```

## कार्यान्वयन मार्गदर्शिका

आइए, छवि हस्ताक्षरों को अनुकूलित करने के लिए विभिन्न सुविधाओं के कार्यान्वयन पर नजर डालें।

### हस्ताक्षर की स्थिति और आकार निर्धारित करें

**अवलोकन**यह सुविधा आपको यह निर्दिष्ट करने की अनुमति देती है कि आपका हस्ताक्षर किसी दस्तावेज़ पर कहां दिखाई देगा और उसका आकार क्या होगा, जिससे दस्तावेज़ों में एकरूपता सुनिश्चित होती है।

#### चरण-दर-चरण कार्यान्वयन

1. **हस्ताक्षर ऑब्जेक्ट आरंभ करें**: का एक उदाहरण बनाएँ `Signature` अपने दस्तावेज़ पथ के साथ class.
2. **ImageSignOptions कॉन्फ़िगर करें**: आकार और स्थिति सहित छवि हस्ताक्षर के लिए विकल्प सेट करें।

```java
import com.groupdocs.signature.Signature;
import com.groupdocs.signature.options.sign.ImageSignOptions;

public class SignWithImagePosition {
    public static void run() throws Exception {
        String filePath = "YOUR_DOCUMENT_DIRECTORY/document.docx";
        String imagePath = "YOUR_DOCUMENT_DIRECTORY/signature.png";
        String outputFilePath = "YOUR_OUTPUT_DIRECTORY/SignaturePosition.docx";

        Signature signature = new Signature(filePath);
        ImageSignOptions options = new ImageSignOptions(imagePath);

        // दस्तावेज़ पर हस्ताक्षर की स्थिति निर्धारित करें
        options.setLeft(100);  // पिक्सेल में X-निर्देशांक
        options.setTop(100);   // पिक्सेल में Y-निर्देशांक

        // हस्ताक्षर आयत का आकार निर्धारित करें
        options.setWidth(100);  // पिक्सेल में चौड़ाई
        options.setHeight(30);  // पिक्सेल में ऊँचाई
        
        // दस्तावेज़ पर हस्ताक्षर करें और उसे सहेजें
        signature.sign(outputFilePath, options);
    }
}
```

### हस्ताक्षर संरेखण और मार्जिन सेट करें

**अवलोकन**संरेखण समायोजन दस्तावेज़ के विभिन्न अनुभागों में एकसमान स्थान सुनिश्चित करता है। हाशिये अन्य सामग्री के साथ क्लिपिंग या ओवरलैपिंग से बचने में मदद करते हैं।

#### चरण-दर-चरण कार्यान्वयन

1. **ऊर्ध्वाधर और क्षैतिज संरेखण को परिभाषित करें**: वांछित संरेखण के लिए गणना मानों का उपयोग करें।
2. **पैडिंग का उपयोग करके मार्जिन कॉन्फ़िगर करें**: सटीक स्थिति के लिए मार्जिन निर्दिष्ट करें.

```java
import com.groupdocs.signature.Signature;
import com.groupdocs.signature.options.sign.ImageSignOptions;
import com.groupdocs.signature.domain.enums.HorizontalAlignment;
import com.groupdocs.signature.domain.enums.VerticalAlignment;
import com.groupdocs.signature.domain.Padding;

public class SignWithImageAlignment {
    public static void run() throws Exception {
        String filePath = "YOUR_DOCUMENT_DIRECTORY/document.docx";
        String imagePath = "YOUR_DOCUMENT_DIRECTORY/signature.png";
        String outputFilePath = "YOUR_OUTPUT_DIRECTORY/SignatureAlignment.docx";

        Signature signature = new Signature(filePath);
        ImageSignOptions options = new ImageSignOptions(imagePath);

        // हस्ताक्षर का ऊर्ध्वाधर संरेखण सेट करें
        options.setVerticalAlignment(VerticalAlignment.Bottom);
        
        // हस्ताक्षर का क्षैतिज संरेखण सेट करें
        options.setHorizontalAlignment(HorizontalAlignment.Right);
        
        // हस्ताक्षर स्थिति के लिए मार्जिन पैडिंग कॉन्फ़िगर करें
        Padding padding = new Padding();
        padding.setBottom(20);  // पिक्सेल में निचला मार्जिन
        padding.setRight(20);   // पिक्सेल में दायाँ मार्जिन
        options.setMargin(padding);

        // दस्तावेज़ पर हस्ताक्षर करें और उसे सहेजें
        signature.sign(outputFilePath, options);
    }
}
```

### ग्रेस्केल और चमक समायोजन के साथ छवि का स्वरूप सेट करें

**अवलोकन**छवि के स्वरूप को अनुकूलित करके दृश्य अपील को बढ़ाया जा सकता है। विकल्पों में ग्रेस्केल लागू करना या चमक समायोजित करना शामिल है।

#### चरण-दर-चरण कार्यान्वयन

1. **छवि प्रकटन सेटिंग्स कॉन्फ़िगर करें**: उपयोग `ImageAppearance` दस्तावेज़ पर छवि कैसी दिखेगी इसे समायोजित करने के लिए.

```java
import com.groupdocs.signature.Signature;
import com.groupdocs.signature.options.sign.ImageSignOptions;
import com.groupdocs.signature.domain.appearances.ImageAppearance;

public class SignWithImageAppearance {
    public static void run() throws Exception {
        String filePath = "YOUR_DOCUMENT_DIRECTORY/document.docx";
        String imagePath = "YOUR_DOCUMENT_DIRECTORY/signature.png";
        String outputFilePath = "YOUR_OUTPUT_DIRECTORY/SignatureAppearance.docx";

        Signature signature = new Signature(filePath);
        ImageSignOptions options = new ImageSignOptions(imagePath);

        // छवि उपस्थिति सेटिंग्स बनाएँ और कॉन्फ़िगर करें
        ImageAppearance imageAppearance = new ImageAppearance();
        
        // छवि पर ग्रेस्केल प्रभाव लागू करें
        imageAppearance.setGrayscale(true);
        
        // छवि का चमक स्तर समायोजित करें
        imageAppearance.setBrightness(0.9f);  // चमक स्तर (रेंज: 0.0 - 1.0)
        
        options.setAppearance(imageAppearance);

        // दस्तावेज़ पर हस्ताक्षर करें और उसे सहेजें
        signature.sign(outputFilePath, options);
    }
}
```

### शैली और पारदर्शिता के साथ छवि बॉर्डर सेट करें

**अवलोकन**: सीमाओं को अनुकूलित करने से आपके हस्ताक्षरों की व्यावसायिकता बढ़ सकती है।

#### चरण-दर-चरण कार्यान्वयन

1. **बॉर्डर विकल्प कॉन्फ़िगर करें**: उपयोग `Border` शैली और पारदर्शिता को परिभाषित करने के लिए सेटिंग्स.

```java
import com.groupdocs.signature.Signature;
import com.groupdocs.signature.options.sign.ImageSignOptions;
import com.groupdocs.signature.domain.Border;

public class SignWithImageBorder {
    public static void run() throws Exception {
        String filePath = "YOUR_DOCUMENT_DIRECTORY/document.docx";
        String imagePath = "YOUR_DOCUMENT_DIRECTORY/signature.png";
        String outputFilePath = "YOUR_OUTPUT_DIRECTORY/SignatureBorder.docx";

        Signature signature = new Signature(filePath);
        ImageSignOptions options = new ImageSignOptions(imagePath);

        // छवि के लिए बॉर्डर सेटिंग बनाएँ और कॉन्फ़िगर करें
        Border border = new Border();
        border.setColor(java.awt.Color.BLACK);  // बॉर्डर का रंग सेट करें
        border.setWidth(2);                    // पिक्सेल में बॉर्डर की चौड़ाई सेट करें
        border.setDashStyle(com.groupdocs.signature.domain.enums.DashStyle.DashDot);
        
        options.setBorder(border);

        // दस्तावेज़ पर हस्ताक्षर करें और उसे सहेजें
        signature.sign(outputFilePath, options);
    }
}
```