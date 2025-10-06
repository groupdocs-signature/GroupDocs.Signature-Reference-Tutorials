---
"date": "2025-05-08"
"description": "Java के लिए GroupDocs.Signature का उपयोग करके छवियों पर सुरक्षित रूप से हस्ताक्षर करना सीखें, जिसमें QR कोड हस्ताक्षर और उन्नत छवि सहेजने के विकल्प शामिल हैं। व्यावसायिक पेशेवरों और डेवलपर्स के लिए आदर्श।"
"title": "Java के लिए GroupDocs.Signature के साथ मास्टर इमेज साइनिंग और ऑप्टिमाइज़ेशन"
"url": "/hi/java/image-signatures/groupdocs-signature-java-image-optimization/"
"weight": 1
type: docs
---
# जावा के लिए GroupDocs.Signature के साथ छवि हस्ताक्षर और अनुकूलन में निपुणता

आज के डिजिटल दौर में, दस्तावेज़ों पर सुरक्षित हस्ताक्षर करना बेहद ज़रूरी है। चाहे आप अनुबंधों को प्रमाणित करने वाले व्यावसायिक पेशेवर हों या तस्वीरों की सुरक्षा करने वाले व्यक्ति, मज़बूत हस्ताक्षर क्षमताएँ बेहद ज़रूरी हैं। **Java के लिए GroupDocs.Signature** क्यूआर कोड सिग्नेचर बनाने और इमेज सेव विकल्पों को सहजता से ऑप्टिमाइज़ करने के लिए शक्तिशाली सुविधाएँ प्रदान करता है। यह ट्यूटोरियल आपको प्रभावी दस्तावेज़ प्रबंधन के लिए इन कार्यात्मकताओं का उपयोग करने में मार्गदर्शन करेगा।

### आप क्या सीखेंगे:
- छवियों पर क्यूआर कोड हस्ताक्षर उत्पन्न करना।
- उन्नत BMP, GIF, JPEG, PNG, और TIFF सेव विकल्पों को कॉन्फ़िगर करना।
- अपनी परियोजनाओं में Java के लिए GroupDocs.Signature का कार्यान्वयन करना।
- इन सुविधाओं के वास्तविक दुनिया अनुप्रयोग।

आइए सुनिश्चित करें कि आपने सब कुछ सही ढंग से सेट किया है!

## आवश्यक शर्तें

कार्यान्वयन विवरण में जाने से पहले, सुनिश्चित करें कि आपके पास:

### आवश्यक लाइब्रेरी और निर्भरताएँ
Java के लिए GroupDocs.Signature का उपयोग करने के लिए, इसकी लाइब्रेरी को अपने प्रोजेक्ट में एकीकृत करें। अपने बिल्ड सिस्टम के आधार पर इसे शामिल करने का तरीका यहां दिया गया है:

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

वैकल्पिक रूप से, आप [नवीनतम संस्करण को सीधे डाउनलोड करें](https://releases.groupdocs.com/signature/java/) यदि आपके प्रोजेक्ट सेटअप को इसकी आवश्यकता है।

### पर्यावरण सेटअप आवश्यकताएँ
- जावा डेवलपमेंट किट (JDK) स्थापित और उचित रूप से कॉन्फ़िगर किया गया।
- कोड विकास के लिए IntelliJ IDEA या Eclipse जैसा IDE.

### ज्ञान पूर्वापेक्षाएँ
जावा प्रोग्रामिंग की बुनियादी समझ होना ज़रूरी है। Maven/Gradle बिल्ड टूल्स से परिचित होना फ़ायदेमंद होगा, लेकिन ज़रूरी नहीं क्योंकि हम आपको सेटअप प्रक्रिया में मार्गदर्शन करेंगे।

## Java के लिए GroupDocs.Signature सेट अप करना

GroupDocs.Signature के साथ काम करना शुरू करने के लिए, इन चरणों का पालन करें:

1. **निर्भरता स्थापित करें**: अपने में उपयुक्त निर्भरता जोड़ें `pom.xml` या `build.gradle` फ़ाइल जैसा कि ऊपर दिखाया गया है.
2. **लाइसेंस अधिग्रहण**:
   - प्राप्त करें [मुफ्त परीक्षण](https://releases.groupdocs.com/signature/java/) पुस्तकालय की सम्पूर्ण क्षमताओं का पता लगाने के लिए।
   - विस्तारित उपयोग के लिए, लाइसेंस खरीदने या उनके माध्यम से अस्थायी लाइसेंस के लिए आवेदन करने पर विचार करें। [खरीद पृष्ठ](https://purchase.groupdocs.com/buy).

### बुनियादी आरंभीकरण और सेटअप
अपना परिवेश सेट अप करने के बाद, GroupDocs.Signature का एक उदाहरण बनाकर उसे आरंभ करें. `Signature` कक्षा। यहाँ बताया गया है कि कैसे:

```java
import com.groupdocs.signature.Signature;

public class SignatureSetup {
    public static void main(String[] args) throws Exception {
        // अपने दस्तावेज़ निर्देशिका के फ़ाइल पथ के साथ आरंभ करें
        String filePath = "YOUR_DOCUMENT_DIRECTORY/sampleImage.jpg";
        Signature signature = new Signature(filePath);
        
        System.out.println("GroupDocs.Signature initialized successfully!");
    }
}
```

## कार्यान्वयन मार्गदर्शिका

अब जब आपके पास आवश्यक सेटअप है, तो आइए Java के लिए GroupDocs.Signature का उपयोग करके विशिष्ट सुविधाओं को लागू करने में गोता लगाएँ।

### छवियों पर QR कोड हस्ताक्षर बनाना

#### अवलोकन
यह अनुभाग आपको किसी इमेज दस्तावेज़ पर QR कोड हस्ताक्षर बनाने की प्रक्रिया बताता है। यह मेटाडेटा या जानकारी को सीधे इमेज में बिना किसी बाधा के एम्बेड करने के लिए विशेष रूप से उपयोगी है।

##### चरण 1: हस्ताक्षर ऑब्जेक्ट को आरंभ करें
सबसे पहले, एक बनाएं `Signature` ऑब्जेक्ट आपकी लक्ष्य फ़ाइल की ओर इशारा करता है।
```java
String filePath = "YOUR_DOCUMENT_DIRECTORY/sampleImage.jpg";
Signature signature = new Signature(filePath);
```

##### चरण 2: QR कोड साइन विकल्प सेट करें
QR कोड से हस्ताक्षर करने के विकल्प कॉन्फ़िगर करें। आप सामग्री और स्थिति जैसे विवरण निर्दिष्ट करेंगे।

```java
import com.groupdocs.signature.domain.qrcodes.QrCodeTypes;
import com.groupdocs.signature.options.sign.QrCodeSignOptions;

QrCodeSignOptions signOptions = new QrCodeSignOptions("JohnSmith");
signOptions.setEncodeType(QrCodeTypes.QR);
signOptions.setLeft(100);  // बाएं हाशिये से स्थिति
signOptions.setTop(100);   // शीर्ष मार्जिन से स्थिति
```

##### चरण 3: दस्तावेज़ पर हस्ताक्षर करें
अंत में, अपने दस्तावेज़ पर QR कोड हस्ताक्षर लागू करें।

```java
signature.sign("output/imageWithQR.jpg", signOptions);
System.out.println("QR Code Signature Applied Successfully!");
```

### उन्नत छवि सहेजने के विकल्प कॉन्फ़िगर करना

#### BMP सहेजें विकल्प कॉन्फ़िगरेशन
यह कॉन्फ़िगरेशन आपको BMP फ़ॉर्मैट में इमेज सेव करने के तरीके को कस्टमाइज़ करने की सुविधा देता है। आवश्यकतानुसार कम्प्रेशन, रिज़ॉल्यूशन और अन्य पैरामीटर समायोजित करें।

```java
import com.groupdocs.signature.options.saveoptions.imagessaveoptions.BmpSaveOptions;
import com.groupdocs.signature.domain.enums.BitmapCompression;

BmpSaveOptions bmpSaveOptions = new BmpSaveOptions();
bmpSaveOptions.setAddMissingExtenstion(true);
bmpSaveOptions.setCompression(BitmapCompression.Rgb);
bmpSaveOptions.setHorizontalResolution(7);
bmpSaveOptions.setVerticalResolution(7);
bmpSaveOptions.setBitsPerPixel(16);
bmpSaveOptions.setOverwriteExistingFiles(true);
```

#### GIF सहेजें विकल्प कॉन्फ़िगरेशन
छवियों को GIF के रूप में सहेजते समय, आप पृष्ठभूमि रंग और पैलेट सॉर्टिंग जैसे पहलुओं को नियंत्रित कर सकते हैं।

```java
import com.groupdocs.signature.options.saveoptions.imagessaveoptions.GifSaveOptions;

GifSaveOptions gifSaveOptions = new GifSaveOptions();
gifSaveOptions.setBackgroundColorIndex((byte) 2);
gifSaveOptions.setColorResolution((byte) 7);
gifSaveOptions.setDoPaletteCorrection(true);
gifSaveOptions.setTrailer(true);
gifSaveOptions.setInterlaced(false);
gifSaveOptions.setPaletteSorted(true);
gifSaveOptions.setPixelAspectRatio((byte) 24);
gifSaveOptions.setAddMissingExtenstion(true);
```

#### JPEG सहेजें विकल्प कॉन्फ़िगरेशन
गुणवत्ता, रंग प्रकार और संपीड़न मोड के लिए सेटिंग्स के साथ अपनी JPEG छवि को अनुकूलित करें।

```java
import com.groupdocs.signature.options.saveoptions.imagessaveoptions.JpegSaveOptions;
import com.groupdocs.signature.domain.enums.JpegCompressionColorMode;
import com.groupdocs.signature.domain.enums.JpegCompressionMode;
import com.groupdocs.signature.domain.enums.JpegRoundingMode;

JpegSaveOptions jpegSaveOptions = new JpegSaveOptions();
jpegSaveOptions.setAddMissingExtenstion(true);
jpegSaveOptions.setBitsPerChannel((byte) 8);
jpegSaveOptions.setColorType(JpegCompressionColorMode.Rgb);
jpegSaveOptions.setComment("signed jpeg file");
jpegSaveOptions.setCompressionType(JpegCompressionMode.Lossless);
jpegSaveOptions.setQuality(100);
jpegSaveOptions.setSampleRoundingMode(JpegRoundingMode.Extrapolate);
```

#### PNG सहेजें विकल्प कॉन्फ़िगरेशन
PNG के साथ, आप अपनी आवश्यकताओं के अनुरूप बिट गहराई और संपीड़न स्तर निर्धारित कर सकते हैं।

```java
import com.groupdocs.signature.options.saveoptions.imagessaveoptions.PngSaveOptions;
import com.groupdocs.signature.domain.enums.PngColorType;
import com.groupdocs.signature.domain.enums.PngFilterType;

PngSaveOptions pngSaveOptions = new PngSaveOptions();
pngSaveOptions.setBitDepth((byte) 8);
pngSaveOptions.setColorType(PngColorType.Grayscale);
pngSaveOptions.setCompressionLevel(9);
pngSaveOptions.setFilterType(PngFilterType.Adaptive);
pngSaveOptions.setProgressive(true);
pngSaveOptions.setAddMissingExtenstion(true);
```

#### TIFF सहेजें विकल्प कॉन्फ़िगरेशन
TIFF छवियों के लिए, आप प्रारूप और अन्य प्रासंगिक सेटिंग्स निर्दिष्ट कर सकते हैं।

```java
import com.groupdocs.signature.options.saveoptions.imagessaveoptions.TiffSaveOptions;
import com.groupdocs.signature.domain.enums.TiffFormat;

TiffSaveOptions tiffSaveOptions = new TiffSaveOptions();
tiffSaveOptions.setExpectedTiffFormat(TiffFormat.TiffNoCompressionBw);
tiffSaveOptions.setAddMissingExtenstion(true);
```

## व्यावहारिक अनुप्रयोगों

### वास्तविक दुनिया के उपयोग के मामले
1. **अनुबंध पर हस्ताक्षर**: त्वरित सत्यापन के लिए अनुबंध छवियों में क्यूआर कोड एम्बेड करें।
2. **विपणन की चीजे**: क्यूआर कोड का उपयोग करके प्रचार सामग्री पर सीधे ब्रांडेड जानकारी जोड़ें।
3. **छवि संग्रहण**: संग्रहण के दौरान गुणवत्ता बनाए रखने और फ़ाइल आकार को कम करने के लिए छवि सहेजने की सेटिंग्स को अनुकूलित करें।