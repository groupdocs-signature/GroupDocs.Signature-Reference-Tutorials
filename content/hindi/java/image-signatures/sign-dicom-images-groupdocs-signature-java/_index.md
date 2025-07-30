---
"date": "2025-05-08"
"description": "Java के लिए GroupDocs.Signature का उपयोग करके DICOM छवियों पर सुरक्षित रूप से हस्ताक्षर करना सीखें। QR कोड और मेटाडेटा एम्बेड करके दस्तावेज़ सुरक्षा बढ़ाएँ।"
"title": "Java के लिए GroupDocs.Signature का उपयोग करके QR कोड और मेटाडेटा के साथ DICOM छवियों पर हस्ताक्षर करें"
"url": "/hi/java/image-signatures/sign-dicom-images-groupdocs-signature-java/"
"weight": 1
---

# Java के लिए GroupDocs.Signature का उपयोग करके QR कोड और मेटाडेटा के साथ DICOM छवियों पर हस्ताक्षर कैसे करें

## परिचय

तेज़ी से विकसित हो रहे डिजिटल स्वास्थ्य सेवा परिदृश्य में, रोगी डेटा का सुरक्षित प्रबंधन अत्यंत महत्वपूर्ण है। यह ट्यूटोरियल आपको GroupDocs.Signature for Java का उपयोग करके डिजिटल इमेजिंग एंड कम्युनिकेशंस इन मेडिसिन (DICOM) छवियों पर QR कोड और मेटाडेटा के साथ हस्ताक्षर करने के लिए एक मज़बूत समाधान लागू करने में मार्गदर्शन करता है। ये सुविधाएँ प्रामाणिकता सुनिश्चित करती हैं, ट्रेसबिलिटी बढ़ाती हैं, और महत्वपूर्ण जानकारी को सीधे चिकित्सा छवियों में एम्बेड करके अनुपालन बनाए रखती हैं।

### आप क्या सीखेंगे:
- अपने प्रोजेक्ट में GroupDocs.Signature for Java को कैसे एकीकृत करें।
- क्यूआर कोड के साथ DICOM छवियों पर हस्ताक्षर करने की प्रक्रिया।
- दस्तावेज़ सुरक्षा बढ़ाने के लिए XMP मेटाडेटा जोड़ना।
- DICOM फ़ाइलों के भीतर हस्ताक्षरों को पुनः प्राप्त करना, सत्यापित करना और खोजना।
- हस्ताक्षरित DICOM छवियों का पूर्वावलोकन तैयार करना।

चलिए शुरू करते हैं! शुरू करने से पहले, आइए यह सुनिश्चित कर लें कि आपके पास इसे आसानी से फॉलो करने के लिए ज़रूरी सभी चीज़ें मौजूद हैं।

## आवश्यक शर्तें

GroupDocs.Signature सुविधाओं को प्रभावी ढंग से क्रियान्वित करने के लिए, सुनिश्चित करें कि आप निम्नलिखित पूर्वापेक्षाएँ पूरी करते हैं:

### आवश्यक लाइब्रेरी और निर्भरताएँ
- **Java के लिए GroupDocs.Signature**आपको इस लाइब्रेरी के संस्करण 23.12 या बाद के संस्करण की आवश्यकता होगी।

### पर्यावरण सेटअप आवश्यकताएँ
- **जावा डेवलपमेंट किट (JDK)**: सुनिश्चित करें कि आपके सिस्टम पर JDK स्थापित है।
- **आईडीई**: IntelliJ IDEA या Eclipse जैसे एकीकृत विकास वातावरण का उपयोग करें।

### ज्ञान पूर्वापेक्षाएँ
इसकी बुनियादी समझ:
- जावा प्रोग्रामिंग और ऑब्जेक्ट-ओरिएंटेड सिद्धांत।
- निर्भरता प्रबंधन के लिए मावेन या ग्रेडेल निर्मित उपकरण।

## Java के लिए GroupDocs.Signature सेट अप करना

GroupDocs.Signature का उपयोग शुरू करने के लिए, आपको इसे अपने प्रोजेक्ट में एक निर्भरता के रूप में जोड़ना होगा। विभिन्न बिल्ड टूल्स का उपयोग करके आप ऐसा कैसे कर सकते हैं, यहाँ बताया गया है:

### मावेन
अपने में निम्नलिखित स्निपेट जोड़ें `pom.xml` फ़ाइल:
```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

### ग्रैडल
इसे अपने में शामिल करें `build.gradle` फ़ाइल:
```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

### प्रत्यक्षत: डाउनलोड
वैकल्पिक रूप से, आप नवीनतम संस्करण यहां से डाउनलोड कर सकते हैं [Java रिलीज़ के लिए GroupDocs.Signature](https://releases.groupdocs.com/signature/java/).

#### लाइसेंस प्राप्ति चरण
1. **मुफ्त परीक्षण**: सीमित समय के निःशुल्क परीक्षण के साथ सुविधाओं का परीक्षण करें।
2. **अस्थायी लाइसेंस**पूर्ण क्षमताओं का पता लगाने के लिए एक अस्थायी लाइसेंस प्राप्त करें।
3. **खरीदना**यदि आपको दीर्घकालिक पहुंच की आवश्यकता है तो सदस्यता खरीदें।

#### बुनियादी आरंभीकरण और सेटअप

GroupDocs.Signature को आरंभ करने के लिए, इसका एक उदाहरण बनाएं `Signature` कक्षा:
```java
import com.groupdocs.signature.Signature;

// अपनी DICOM फ़ाइल के पथ के साथ हस्ताक्षर ऑब्जेक्ट को आरंभ करें
Signature signature = new Signature(filePath);
```

## कार्यान्वयन मार्गदर्शिका

### QR कोड और मेटाडेटा के साथ DICOM छवि पर हस्ताक्षर करना

#### अवलोकन
यह सुविधा आपको DICOM छवियों पर QR कोड के साथ हस्ताक्षर करने और XMP मेटाडेटा जोड़ने की अनुमति देती है, जिससे दस्तावेज़ सुरक्षा बढ़ जाती है।

#### चरण 1: QR कोड साइन विकल्प सेट करें
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
यहां, हम DICOM छवि पर QR कोड की उपस्थिति और स्थिति को कॉन्फ़िगर करते हैं।

#### चरण 2: XMP मेटाडेटा जोड़ें
```java
import com.groupdocs.signature.options.saveoptions.imagessaveoptions.DicomSaveOptions;
import com.groupdocs.signature.options.saveoptions.imagessaveoptions.DicomXmpEntry;
import com.groupdocs.signature.options.saveoptions.imagessaveoptions.DicomXmpType;

DicomSaveOptions dicomSaveOptions = new DicomSaveOptions();
List<DicomXmpEntry> xmpEntries = new ArrayList<>();
xmpEntries.add(new DicomXmpEntry(DicomXmpType.PatientName, "Patient #4"));
dicomSaveOptions.setXmpEntries(xmpEntries);
```
यह स्निपेट DICOM फ़ाइल में मेटाडेटा जोड़ता है, तथा अतिरिक्त रोगी जानकारी एम्बेड करता है।

#### चरण 3: दस्तावेज़ पर हस्ताक्षर करें
```java
String outputFilePath = YOUR_OUTPUT_DIRECTORY + "/SignDicomImageAdvanced/" + fileName;
signature.sign(outputFilePath, options, dicomSaveOptions);
```
The `sign` विधि आपके DICOM फ़ाइल में QR कोड और मेटाडेटा लिखती है, तथा उसे निर्दिष्ट स्थान पर सहेजती है।

### हस्ताक्षरित DICOM छवि जानकारी प्राप्त करना

#### अवलोकन
सत्यापन या ऑडिट प्रयोजनों के लिए हस्ताक्षरित DICOM छवि से XMP मेटाडेटा निकालें।
```java
import com.groupdocs.signature.domain.IDocumentInfo;
import com.groupdocs.signature.domain.signatures.MetadataSignature;

IDocumentInfo documentInfo = signature.getDocumentInfo();
for (MetadataSignature item : documentInfo.getMetadataSignatures()) {
    System.out.println(item.toString());
}
```
यह कोड DICOM फ़ाइल से संबद्ध सभी मेटाडेटा हस्ताक्षरों को पुनः प्राप्त करता है और प्रिंट करता है।

### हस्ताक्षरित DICOM का सत्यापन

#### अवलोकन
इसकी प्रामाणिकता की पुष्टि करने के लिए सत्यापित करें कि हस्ताक्षरित DICOM छवि में QR कोड हस्ताक्षर मौजूद है।
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
यह सत्यापन चरण सुनिश्चित करता है कि क्यूआर कोड अपेक्षित मानदंडों से मेल खाता है, तथा दस्तावेज़ की अखंडता की पुष्टि करता है।

### हस्ताक्षरित DICOM में हस्ताक्षरों की खोज

#### अवलोकन
सभी QR कोड हस्ताक्षरों को हस्ताक्षरित DICOM छवि के भीतर खोजें और उनकी समीक्षा या ऑडिट करें।
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
यह सुविधा दस्तावेज़ के भीतर सभी क्यूआर कोड हस्ताक्षरों को स्कैन करने के लिए उपयोगी है, जो व्यापक दृश्यता प्रदान करती है।

### हस्ताक्षरित DICOM का पूर्वावलोकन तैयार करना

#### अवलोकन
हस्ताक्षरित DICOM छवि के प्रत्येक पृष्ठ के लिए पूर्वावलोकन बनाएं, जिससे पूरी फ़ाइल को खोले बिना त्वरित दृश्य निरीक्षण की सुविधा मिल सके।
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
यह स्निपेट प्रत्येक पृष्ठ के लिए छवि पूर्वावलोकन तैयार करता है, जो त्वरित सत्यापन या साझाकरण के लिए उपयोगी हो सकता है।

## व्यावहारिक अनुप्रयोगों

GroupDocs.Signature for Java कई वास्तविक-विश्व अनुप्रयोग प्रदान करता है:
- **मेडिकल इमेजिंग**: QR कोड और मेटाडेटा के साथ रोगी DICOM छवियों पर सुरक्षित रूप से हस्ताक्षर करें और उनका प्रबंधन करें।
- **कानूनी दस्तावेज़ प्रबंधन**कानूनी कार्यवाही में दस्तावेज़ की प्रामाणिकता और अनुपालन को बढ़ाना।
- **वित्तीय सेवाएं**संवेदनशील वित्तीय दस्तावेजों पर सुरक्षित इलेक्ट्रॉनिक हस्ताक्षर लागू करें।