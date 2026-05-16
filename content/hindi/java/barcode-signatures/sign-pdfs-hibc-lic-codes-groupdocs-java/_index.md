---
categories:
- Document Signing
- Healthcare Integration
date: '2026-05-16'
description: GroupDocs.Signature for Java का उपयोग करके data matrix PDF बनाना और QR
  code PDF जोड़ना सीखें। स्वास्थ्य देखभाल दस्तावेज़ साइनिंग के लिए स्टेप‑बाय‑स्टेप
  गाइड।
keywords:
- create data matrix pdf
- add qr code pdf
- HIBC barcode Java
lastmod: '2026-05-16'
linktitle: HIBC PDF साइनिंग Java गाइड
schemas:
- author: GroupDocs
  dateModified: '2026-05-16'
  description: Learn how to create data matrix PDF and add QR code PDF using GroupDocs.Signature
    for Java. Step‑by‑step guide for healthcare document signing.
  headline: Create Data Matrix PDF with HIBC Barcode in Java
  type: TechArticle
- description: Learn how to create data matrix PDF and add QR code PDF using GroupDocs.Signature
    for Java. Step‑by‑step guide for healthcare document signing.
  name: Create Data Matrix PDF with HIBC Barcode in Java
  steps:
  - name: '**Import the required classes** – these give you access to the signature
      engine and Data Matrix options.'
    text: '**Import the required classes** – these give you access to the signature
      engine and Data Matrix options.'
  - name: '**Instantiate the `Signature` object** with absolute paths for source and
      destination files.'
    text: '**Instantiate the `Signature` object** with absolute paths for source and
      destination files.'
  - name: '**Configure the Data Matrix options** – set the HIBC string, choose `QrCodeTypes.HIBCLICDataMatrix`,
      and define placement coordinates. `QrCodeTypes` enumerates the supported barcode
      formats for HIBC signatures.'
    text: '**Configure the Data Matrix options** – set the HIBC string, choose `QrCodeTypes.HIBCLICDataMatrix`,
      and define placement coordinates. `QrCodeTypes` enumerates the supported barcode
      formats for HIBC signatures.'
  - name: '**Apply the signature** to the PDF.'
    text: '**Apply the signature** to the PDF.'
  - name: '**Dispose of resources** to free file handles and avoid memory leaks.'
    text: '**Dispose of resources** to free file handles and avoid memory leaks.'
  - name: '**Import QR‑specific classes**'
    text: '**Import QR‑specific classes**'
  - name: '**Create and configure QR options** – note the use of `QrCodeTypes.HIBCLICQR`.'
    text: '**Create and configure QR options** – note the use of `QrCodeTypes.HIBCLICQR`.'
  - name: '**Sign the document**'
    text: '**Sign the document**'
  type: HowTo
- questions:
  - answer: Yes, it also supports DOCX, XLSX, PPTX, PNG, JPEG, and TIFF with the same
      barcode‑signing API.
    question: Can GroupDocs.Signature sign file types other than PDF?
  - answer: Verify that your HIBC string follows the exact HIBCC syntax, use the online
      validator, and ensure you’re using the correct `QrCodeTypes` constant for the
      chosen format.
    question: How do I troubleshoot “Invalid barcode content” errors?
  - answer: QR ≈ 4,296 alphanumeric characters, Aztec ≈ 3,832 numeric / 3,067 alphanumeric,
      Data Matrix ≈ 3,116 numeric / 2,335 alphanumeric. Keep codes under 200 characters
      for optimal scan reliability.
    question: What is the maximum data capacity for each HIBC format?
  - answer: Absolutely. Create separate `QrCodeSignOptions` objects with different
      positions and call `signature.sign()` for each. Just ensure they don’t overlap.
    question: Is it possible to embed multiple barcode types in one PDF?
  - answer: No. After the JAR is on the classpath and the license is activated, all
      operations are performed locally.
    question: Do I need an internet connection for signing at runtime?
  type: FAQPage
tags:
- java
- pdf-signing
- hibc
- healthcare
- barcode
- pharmaceutical
title: Java में HIBC बारकोड के साथ Data Matrix PDF बनाएं
type: docs
url: /hi/java/barcode-signatures/sign-pdfs-hibc-lic-codes-groupdocs-java/
weight: 1
---

# HIBC बारकोड के साथ जावा में डेटा मैट्रिक्स PDF बनाएं

यदि आप फ़ार्मास्यूटिकल या हेल्थकेयर लॉजिस्टिक्स सॉफ़्टवेयर बना रहे हैं, तो आप संभवतः कागज़-आधारित ट्रैकिंग, खोए हुए हस्ताक्षर, और ऑडिट की दुविधाओं से जूझ रहे होंगे। **Creating a Data Matrix PDF** जो HIBC LIC बारकोड को एम्बेड करता है, इन समस्याओं को हल करता है क्योंकि यह आपको एक छेड़छाड़-प्रूफ़, मशीन‑रीडेबल ट्रेल देता है जो प्रिंटिंग, स्कैनिंग और नियामक समीक्षा में भी टिकता है। इस ट्यूटोरियल में आप देखेंगे कि **add QR code PDF** समर्थन कैसे जोड़ें, साथ ही Aztec और Data Matrix फ़ॉर्मेट, GroupDocs.Signature for Java का उपयोग करके।

## त्वरित उत्तर
- **Java में HIBC बारकोड को संभालने वाली लाइब्रेरी कौन सी है?** GroupDocs.Signature for Java.  
- **कौन सा बारकोड फ़ॉर्मेट सबसे कॉम्पैक्ट है?** Data Matrix – छोटे लेबल के लिए आदर्श।  
- **क्या मैं एक ही PDF में QR और Data Matrix दोनों जोड़ सकता हूँ?** हाँ, बस अलग `QrCodeSignOptions` बनाएं।  
- **क्या रनटाइम पर मुझे इंटरनेट कनेक्शन की आवश्यकता है?** नहीं, लाइब्रेरी इंस्टॉल होने के बाद पूरी तरह ऑफ़लाइन काम करती है।  
- **कौन सा Java संस्करण अनुशंसित है?** उत्पादन‑ग्रेड प्रदर्शन के लिए Java 11+।

## HIBC बारकोड PDF साइनिंग क्या है?
`Signature` क्लास GroupDocs.Signature for Java में एक PDF दस्तावेज़ का प्रतिनिधित्व करता है और HIBC बारकोड को डिजिटल सिग्नेचर के रूप में एम्बेड करने के लिए मेथड प्रदान करता है। HIBC बारकोड के साथ PDF पर साइन करके आप एक सत्यापन योग्य, छेड़छाड़‑प्रूफ़ रिकॉर्ड बनाते हैं जिसे आपूर्ति श्रृंखला के किसी भी बिंदु पर स्कैन किया जा सकता है।

## Data Matrix और QR कोड को साथ में क्यों उपयोग करें?
GroupDocs.Signature **50+ इनपुट और आउटपुट फ़ॉर्मेट** का समर्थन करता है और पूरी फ़ाइल को मेमोरी में लोड किए बिना कई‑सौ पृष्ठों वाले PDF को प्रोसेस कर सकता है। घने, छोटे‑क्षेत्र लेबल के लिए Data Matrix और अधिक विस्तृत दस्तावेज़ों के लिए QR का उपयोग करने से आपको पठनीयता, डेटा क्षमता (QR के लिए अधिकतम 4,296 अक्षर) और प्रिंट‑स्पेस दक्षता का सर्वोत्तम संतुलन मिलता है।

## पूर्वापेक्षाएँ
- **JDK 11 या उससे ऊपर** (Java 8 काम करता है लेकिन इष्टतम प्रदर्शन के लिए Java 11+ अनुशंसित है)।  
- **IDE** जैसे IntelliJ IDEA, Eclipse, या VS Code Java एक्सटेंशन के साथ।  
- **Maven या Gradle** डिपेंडेंसी मैनेजमेंट के लिए (नीचे उदाहरण)।  
- **Sample PDF** (जैसे `sample.pdf`) कार्यान्वयन का परीक्षण करने के लिए।  
- **Valid GroupDocs.Signature license** (विकास के लिए फ्री ट्रायल, उत्पादन के लिए पेड लाइसेंस)।

## GroupDocs.Signature for Java सेटअप करना

### Maven कॉन्फ़िगरेशन
`pom.xml` में डिपेंडेंसी जोड़ें:

```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

### Gradle कॉन्फ़िगरेशन
Gradle प्रोजेक्ट्स के लिए, इसे अपने `build.gradle` में जोड़ें:

```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

### डायरेक्ट डाउनलोड विकल्प
आप [GroupDocs.Signature for Java releases](https://releases.groupdocs.com/signature/java/) से JAR फ़ाइल सीधे डाउनलोड कर सकते हैं और इसे मैन्युअली अपने प्रोजेक्ट की क्लासपाथ में जोड़ सकते हैं। यह तरीका प्रतिबंधित‑नेटवर्क वातावरण में अच्छी तरह काम करता है।

### लाइसेंस प्राप्त करना
वॉटरमार्क हटाने और सभी फीचर अनलॉक करने के लिए GroupDocs से फ्री ट्रायल या टेम्पररी लाइसेंस का अनुरोध करें। प्रोडक्शन डिप्लॉयमेंट के लिए खरीदा हुआ लाइसेंस आवश्यक है।

### बेसिक इनिशियलाइज़ेशन
`Signature` क्लास सभी साइनिंग ऑपरेशन्स का एंट्री पॉइंट है। यह PDF को लोड करता है, बारकोड लागू करता है, और साइन किया हुआ फ़ाइल लिखता है।

```java
import com.groupdocs.signature.Signature;

class InitializeSignature {
    public static void main(String[] args) {
        Signature signature = new Signature("sample.pdf");
        // Proceed with signing operations...
    }
}
```

## HIBC बारकोड के साथ Data Matrix PDF कैसे बनाएं?
अपना स्रोत PDF लोड करें, Data Matrix फ़ॉर्मेट के लिए `QrCodeSignOptions` ऑब्जेक्ट कॉन्फ़िगर करें, और `sign()` कॉल करें – यह वह सब है जो एक अनुपालन योग्य HIBC Data Matrix बारकोड एम्बेड करने के लिए आवश्यक है। नीचे दिए गए चरण आपको आवश्यक सटीक कोड दिखाते हैं। `QrCodeSignOptions` बारकोड सिग्नेचर की सेटिंग्स निर्धारित करता है, जैसे प्रकार, सामग्री, आकार, और स्थिति।

1. **Import the required classes** – ये आपको सिग्नेचर इंजन और Data Matrix विकल्पों तक पहुंच प्रदान करते हैं।  

```java
import com.groupdocs.signature.Signature;
import com.groupdocs.signature.options.sign.QrCodeSignOptions;
import com.groupdocs.signature.domain.qrcodes.QrCodeTypes;
```

2. **`Signature` ऑब्जेक्ट को इंस्टैंसिएट करें** स्रोत और गंतव्य फ़ाइलों के पूर्ण पाथ के साथ।  

```java
String sourceFilePath = "YOUR_DOCUMENT_DIRECTORY";
String destinFilePath = "YOUR_OUTPUT_DIRECTORY/SignWithHIBCLICQR.pdf";

final Signature signature = new Signature(sourceFilePath);
```

3. **Configure the Data Matrix options** – HIBC स्ट्रिंग सेट करें, `QrCodeTypes.HIBCLICDataMatrix` चुनें, और प्लेसमेंट कोऑर्डिनेट्स निर्धारित करें। `QrCodeTypes` HIBC सिग्नेचर के लिए समर्थित बारकोड फ़ॉर्मेट को सूचीबद्ध करता है।  

```java
QrCodeSignOptions hibcLic_QR = new QrCodeSignOptions("A123PROD30917/75#422011907#GP293", QrCodeTypes.HIBCLICQR);
hibcLic_QR.setLeft(1); // Set the position from left
hibcLic_QR.setTop(1);   // Set the position from top
hibcLic_QR.setReturnContent(true); // Return content after signing
hibcLic_QR.setReturnContentType(FileType.PNG); // Specify return content type as PNG
```

4. **PDF पर सिग्नेचर लागू करें**।  

```java
signature.sign(destinFilePath, hibcLic_QR);
```

5. **संसाधनों को डिस्पोज़ करें** ताकि फ़ाइल हैंडल मुक्त हों और मेमोरी लीक्स न हों।  

```java
finally {
    if (signature != null) signature.dispose();
}
```

### पूर्ण कार्यशील उदाहरण
यहाँ एकल ब्लॉक में पूरा फ्लो दिया गया है (प्लेसहोल्डर पहले के स्निपेट्स से आप जो कोड पेस्ट करेंगे, उसे दर्शाते हैं):

```java
import com.groupdocs.signature.Signature;
import com.groupdocs.signature.options.sign.QrCodeSignOptions;
import com.groupdocs.signature.domain.qrcodes.QrCodeTypes;

public class HibcQrSigning {
    public static void main(String[] args) {
        String sourceFilePath = "sample.pdf";
        String destinFilePath = "output/SignWithHIBCLICQR.pdf";
        
        Signature signature = null;
        try {
            signature = new Signature(sourceFilePath);
            
            QrCodeSignOptions hibcLic_QR = new QrCodeSignOptions(
                "A123PROD30917/75#422011907#GP293", 
                QrCodeTypes.HIBCLICQR
            );
            hibcLic_QR.setLeft(1);
            hibcLic_QR.setTop(1);
            hibcLic_QR.setReturnContent(true);
            hibcLic_QR.setReturnContentType(FileType.PNG);
            
            signature.sign(destinFilePath, hibcLic_QR);
            System.out.println("PDF signed successfully with HIBC QR code");
            
        } catch (Exception e) {
            System.err.println("Error signing PDF: " + e.getMessage());
            e.printStackTrace();
        } finally {
            if (signature != null) signature.dispose();
        }
    }
}
```

#### सीधा उत्तर (40–70 शब्द)
एक **Data Matrix PDF** बनाने के लिए, अपने स्रोत PDF के साथ `Signature` को इंस्टैंसिएट करें, `QrCodeSignOptions` को `QrCodeTypes.HIBCLICDataMatrix` सेट करें और सही फ़ॉर्मेटेड HIBC स्ट्रिंग प्रदान करें, फिर `signature.sign(outputPath, options)` कॉल करें। लाइब्रेरी साइन किया हुआ PDF गंतव्य पर लिखती है, लेआउट को संरक्षित रखती है और बारकोड को छेड़छाड़‑प्रूफ़ सिग्नेचर के रूप में एम्बेड करती है।

## GroupDocs.Signature का उपयोग करके QR कोड PDF कैसे जोड़ें?
PDF लोड करें, QR फ़ॉर्मेट के लिए `QrCodeSignOptions` कॉन्फ़िगर करें, और `sign()` को कॉल करें। यह दो‑लाइन पैटर्न किसी भी PDF आकार के लिए काम करता है और स्वचालित रूप से QR इमेज को सर्वोत्तम पठनीयता के लिए स्केल करता है। `QrCodeSignOptions` QR बारकोड सिग्नेचर को कॉन्फ़िगर करता है, जिसमें उसकी सामग्री और दृश्य गुण शामिल हैं। यह कोड को सेट किए गए कोऑर्डिनेट्स के आधार पर स्थित करता है, यह सुनिश्चित करता है कि यह मौजूदा सामग्री के साथ ओवरलैप न हो और प्रिंटिंग के बाद स्कैन करने योग्य बना रहे।

1. **QR‑विशिष्ट क्लासेस इम्पोर्ट करें**  

```java
QrCodeSignOptions hibcLic_AZ = new QrCodeSignOptions("A123PROD30917/75#422011907#GP293", QrCodeTypes.HIBCLICAztec);
hibcLic_AZ.setLeft(1); // Set the position from left
hibcLic_AZ.setTop(200); // Set the position from top
hibcLic_AZ.setReturnContent(true); // Return content after signing
hibcLic_AZ.setReturnContentType(FileType.PNG); // Specify return content type as PNG
```

2. **QR विकल्प बनाएं और कॉन्फ़िगर करें** – `QrCodeTypes.HIBCLICQR` के उपयोग पर ध्यान दें।  

```java
signature.sign(destinFilePath, hibcLic_AZ);
```

3. **दस्तावेज़ पर साइन करें**  

```java
QrCodeSignOptions hibcLic_DM = new QrCodeSignOptions("A123PROD30917/75#422011907#GP293", QrCodeTypes.HIBCLICDataMatrix);
hibcLic_DM.setLeft(1); // Set the position from left
hibcLic_DM.setTop(400); // Set the position from top
hibcLic_DM.setReturnContent(true); // Return content after signing
hibcLic_DM.setReturnContentType(FileType.PNG); // Specify return content type as PNG
```

> **Direct answer:** `QrCodeSignOptions` में `QrCodeTypes.HIBCLICQR` का उपयोग करें, HIBC कंटेंट स्ट्रिंग सेट करें, कोड को `setLeft()` और `setTop()` से पोजिशन करें, फिर `signature.sign(outputPath, options)` कॉल करें। QR बारकोड तुरंत एम्बेड हो जाता है, स्मार्टफ़ोन या स्कैनर कैप्चर के लिए तैयार।

## सामान्य गलतियों से बचें

### 1. संसाधन डिस्पोज़ करना भूलना
**गलत:**  
```java
Signature signature = new Signature("sample.pdf");
signature.sign(destinFilePath, options);
// Oops, no dispose() call
```  

**सही:** `Signature` उपयोग को try‑with‑resources ब्लॉक में रैप करें या finally क्लॉज़ में स्पष्ट रूप से `close()` कॉल करें।

### 2. गलत HIBC फ़ॉर्मेट स्ट्रिंग्स का उपयोग करना
**गलत:** “12345” जैसी सामान्य स्ट्रिंग्स का उपयोग करना।  
**सही:** HIBCC मानक का पालन करें (उदाहरण: `A123PROD30917/75#422011907#GP293`)। [HIBCC ऑनलाइन वैलिडेटर](https://www.hibcc.org/) से वैलिडेट करें।

### 3. फ़ाइल पाथ हार्ड‑कोड करना
**गलत:**  
```java
String sourceFilePath = "C:/Users/John/Documents/test.pdf";
```  

**सही:** पाथ को कॉन्फ़िगरेशन फ़ाइल या एनवायरनमेंट वैरिएबल में रखें और रनटाइम पर पढ़ें।

### 4. बारकोड पोजिशन कॉन्फ्लिक्ट को अनदेखा करना
बारकोड को मौजूदा टेक्स्ट या सिग्नेचर से दूर रखें। PDF कोऑर्डिनेट्स (origin नीचे‑बाएँ) का उपयोग करें और प्रिंटेड सैंपल से टेस्ट करें।

### 5. वास्तविक स्कैनर के साथ टेस्ट न करना
साइन किया हुआ PDF प्रिंट करें और अपने वर्कफ़्लो में उपयोग किए जाने वाले सटीक हार्डवेयर से स्कैन करें। विभिन्न प्रिंट क्वालिटी पर पठनीयता सत्यापित करें।

## स्वास्थ्य देखभाल में व्यावहारिक अनुप्रयोग

| परिदृश्य | सिफ़ारिश किया गया बारकोड | क्यों उपयुक्त है |
|----------|--------------------|--------------|
| **फ़ार्मास्यूटिकल वितरण** | QR Code | उच्च डेटा क्षमता, स्मार्टफ़ोन द्वारा व्यापक रूप से स्कैन किया जाता है। |
| **इन्वेंटरी प्रबंधन** | Data Matrix | छोटा फुटप्रिंट, घने शेल्फ लेबल के लिए आदर्श। |
| **नियामक अनुपालन (FDA 21 CFR Part 11)** | QR + Data Matrix | ड्यूल‑फ़ॉर्मेट रिडंडेंसी और ऑडिटेबिलिटी प्रदान करता है। |
| **मेडिकल डिवाइस ट्रैकिंग** | Aztec Code | कॉम्पैक्ट साइज सीमित‑स्पेस पैकेजिंग पर काम करता है। |

## प्रदर्शन विचार और सर्वोत्तम प्रथाएँ

### बैच प्रोसेसिंग पैटर्न
```java
List<String> filesToSign = getFileList();
for (String filePath : filesToSign) {
    Signature signature = null;
    try {
        signature = new Signature(filePath);
        // Sign and save
    } finally {
        if (signature != null) signature.dispose();
    }
}
```

- प्रत्येक फ़ाइल के लिए नया `Signature` इंस्टेंस बनाएं ताकि मेमोरी उपयोग कम रहे।  
- पैरेलल प्रोसेसिंग के लिए फिक्स्ड थ्रेड पूल (`Executors.newFixedThreadPool(Runtime.getRuntime().availableProcessors() - 1)`) का उपयोग करें, लेकिन हीप साइज मॉनिटर करें क्योंकि प्रत्येक `Signature` पूरी PDF को मेमोरी में रखता है।

### लाइब्रेरीज़ को अपडेट रखें
GroupDocs रिलीज़ प्रोसेसिंग स्पीड को **20 %** तक बढ़ाते हैं और नए HIBC कम्प्लायंस फीचर जोड़ते हैं। त्रैमासिक डिपेंडेंसी चेक शेड्यूल करें।

### टेम्प्लेट कैशिंग
PDF टेम्प्लेट को एक बार लोड करें, प्रत्येक बारकोड वैरिएंट के लिए क्लोन बनाएं, और क्लोन पर साइन करें। इससे I/O कम होता है और हाई‑वॉल्यूम वर्कफ़्लो तेज़ होते हैं।

## अक्सर पूछे जाने वाले प्रश्न

**Q: क्या GroupDocs.Signature PDF के अलावा अन्य फ़ाइल प्रकारों को साइन कर सकता है?**  
A: हाँ, यह DOCX, XLSX, PPTX, PNG, JPEG, और TIFF को भी उसी बारकोड‑साइनिंग API के साथ सपोर्ट करता है।

**Q: “Invalid barcode content” त्रुटियों को कैसे ट्रबलशूट करें?**  
A: सुनिश्चित करें कि आपका HIBC स्ट्रिंग सटीक HIBCC सिंटैक्स का पालन करता है, ऑनलाइन वैलिडेटर का उपयोग करें, और चुने हुए फ़ॉर्मेट के लिए सही `QrCodeTypes` कॉन्स्टेंट उपयोग कर रहे हैं।

**Q: प्रत्येक HIBC फ़ॉर्मेट की अधिकतम डेटा क्षमता क्या है?**  
A: QR ≈ 4,296 अल्फ़ान्यूमेरिक कैरेक्टर्स, Aztec ≈ 3,832 न्यूमेरिक / 3,067 अल्फ़ान्यूमेरिक, Data Matrix ≈ 3,116 न्यूमेरिक / 2,335 अल्फ़ान्यूमेरिक। इष्टतम स्कैन विश्वसनीयता के लिए कोड को 200 कैरेक्टर्स से कम रखें।

**Q: क्या एक PDF में कई बारकोड प्रकार एम्बेड करना संभव है?**  
A: बिल्कुल। विभिन्न पोजिशन के साथ अलग `QrCodeSignOptions` ऑब्जेक्ट बनाएं और प्रत्येक के लिए `signature.sign()` कॉल करें। बस यह सुनिश्चित करें कि वे ओवरलैप न हों।

**Q: रनटाइम पर साइन करने के लिए क्या इंटरनेट कनेक्शन आवश्यक है?**  
A: नहीं। JAR क्लासपाथ में होने और लाइसेंस एक्टिवेट होने के बाद सभी ऑपरेशन स्थानीय रूप से किए जाते हैं।

## अतिरिक्त संसाधन

- [GroupDocs.Signature for Java दस्तावेज़ीकरण](https://docs.groupdocs.com/signature/java/)  
- [API रेफ़रेंस गाइड](https://reference.groupdocs.com/signature/java/)  
- [नवीनतम रिलीज़ डाउनलोड्स](https://releases.groupdocs.com/signature/java/)  
- [लाइसेंस खरीदें](https://purchase.groupdocs.com/buy)  
- [फ़्री ट्रायल प्राप्त करें](https://releases.groupdocs.com/signature/java/)  
- [टेम्पररी लाइसेंस का अनुरोध करें](https://purchase.groupdocs.com/temporary-license/)  
- [GroupDocs फ़ोरम](https://forum.groupdocs.com/c/signature/)

---

**अंतिम अपडेट:** 2026-05-16  
**परीक्षित संस्करण:** GroupDocs.Signature 23.12 for Java  
**लेखक:** GroupDocs  

---

```java
signature.sign(destinFilePath, hibcLic_DM);
```

## संबंधित ट्यूटोरियल

- [जावा में बारकोड सिग्नेचर PDF बनाएं – GroupDocs गाइड](/signature/java/barcode-signatures/create-sign-pdfs-groupdocs-barcode-java/)
- [जावा में बारकोड सिग्नेचर बनाएं – PDF बारकोड अपडेट करें](/signature/java/barcode-signatures/java-groupdocs-signature-barcode-initialize-update/)
- [जावा और GroupDocs.Signature का उपयोग करके QR कोड PDF कैसे पढ़ें](/signature/java/barcode-signatures/java-pdf-barcode-search-groupdocs-signature-api/)