---
categories:
- Java Document Processing
date: '2026-01-16'
description: जावा में बारकोड सिग्नेचर बनाना सीखें और GroupDocs.Signature API का उपयोग
  करके PDFs के लिए उसकी स्थिति, आकार और गुण अपडेट करें।
keywords: update barcode signature Java, Java barcode signature management, modify
  barcode in PDF Java, GroupDocs Signature Java, Java document signature automation
lastmod: '2026-01-16'
linktitle: Update Barcode Signatures in Java
tags:
- barcode-signatures
- pdf-automation
- groupdocs-java
- document-management
title: जावा में बारकोड सिग्नेचर बनाएं – PDF बारकोड अपडेट करें
type: docs
url: /hi/java/barcode-signatures/java-groupdocs-signature-barcode-initialize-update/
weight: 1
---

# जावा में बारकोड सिग्नेचर बनाएं – PDF बारकोड अपडेट करें

## परिचय

क्या आपको कभी पैकेजिंग री‑डिज़ाइन के बाद हजारों शिपिंग लेबल पर बारकोड को पुनः स्थित करने की आवश्यकता पड़ी है? या जब आपकी लीगल टीम दस्तावेज़ लेआउट बदलती है, तो कॉन्ट्रैक्ट टेम्पलेट्स में बारकोड स्थान अपडेट करने पड़े हैं? आप अकेले नहीं हैं—ऐसे परिदृश्य दस्तावेज़ ऑटोमेशन वर्कफ़्लो में लगातार सामने आते रहते हैं।

हाथ से **बारकोड सिग्नेचर** को अपडेट करना थकाऊ और त्रुटिप्रवण होता है। GroupDocs.Signature for Java के साथ, आप **बारकोड सिग्नेचर** ऑब्जेक्ट बना सकते हैं और फिर उन्हें कुछ ही कोड लाइनों में संशोधित कर सकते हैं। चाहे आप इन्वेंटरी सिस्टम बना रहे हों, लॉजिस्टिक्स दस्तावेज़ों को ऑटोमेट कर रहे हों, या लीगल कॉन्ट्रैक्ट्स का प्रबंधन कर रहे हों, प्रोग्रामेटिक रूप से बारकोड सिग्नेचर अपडेट करने से घंटों का मैन्युअल काम बचता है।

**इस ट्यूटोरियल में आप क्या सीखेंगे:**
- अपने दस्तावेज़ों के साथ Signature API को सेट अप और इनिशियलाइज़ करना
- मौजूदा बारकोड सिग्नेचर को प्रभावी ढंग से खोजना
- बारकोड की पोजीशन, आकार और अन्य प्रॉपर्टीज़ को अपडेट करना (जिसमें **बारकोड आकार बदलना** भी शामिल है)
- सामान्य त्रुटियों और किनारे के मामलों को संभालना
- बैच ऑपरेशन्स के लिए प्रदर्शन को ऑप्टिमाइज़ करना

कोड लिखने से पहले यह सुनिश्चित करके शुरू करते हैं कि आपके पास सभी आवश्यक चीज़ें हैं।

## पूर्वापेक्षाएँ

अपने प्रोजेक्ट में बारकोड सिग्नेचर जावा कोड अपडेट करने से पहले, सुनिश्चित करें कि आपके पास ये आवश्यक चीज़ें हैं:

### आवश्यक लाइब्रेरीज़

- **GroupDocs.Signature for Java**: संस्करण 23.12 या बाद का (पहले के संस्करणों में वह अपडेट मेथड्स नहीं हो सकते जो हम उपयोग करेंगे)।

### पर्यावरण सेटअप

- एक कार्यशील **Java Development Kit (JDK)** (JDK 8 या उससे ऊपर की सिफारिश की जाती है)
- एक **IDE** जैसे IntelliJ IDEA, Eclipse, या VS Code

### ज्ञान पूर्वापेक्षाएँ

- बेसिक जावा (क्लासेज़, ऑब्जेक्ट्स, एक्सेप्शन हैंडलिंग)
- जावा में फ़ाइल हैंडलिंग (पाथ्स, डायरेक्टरीज़)
- वैकल्पिक: PDF संरचना और बारकोड अवधारणाओं की समझ

सब कुछ तैयार है? बढ़िया! चलिए लाइब्रेरी इंस्टॉल करते हैं।

## जावा के लिए GroupDocs.Signature सेट अप करना

अपने जावा प्रोजेक्ट में GroupDocs.Signature जोड़ना सरल है। आप जो भी बिल्ड टूल उपयोग कर रहे हैं, उसे चुनें:

**Maven**
```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

**Gradle**
```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

**Direct Download**: यदि आप कोई बिल्ड टूल उपयोग नहीं कर रहे हैं, तो नवीनतम JAR फ़ाइल को [GroupDocs.Signature for Java releases](https://releases.groupdocs.com/signature/java/) से डाउनलोड करें और इसे मैन्युअली अपने प्रोजेक्ट की क्लासपाथ में जोड़ें।

### लाइसेंस प्राप्ति

GroupDocs.Signature ट्रायल और फुल दोनों लाइसेंस के साथ काम करता है:

- **Free Trial** – परीक्षण और प्रूफ़‑ऑफ़‑कॉन्सेप्ट कार्य के लिए उपयुक्त
- **Temporary License** – किसी विशिष्ट प्रोजेक्ट पर विस्तारित मूल्यांकन के लिए
- **Full License** – प्रोडक्शन के लिए वाटरमार्क और उपयोग सीमाओं को हटाता है

**Pro Tip**: पहले फ्री ट्रायल से शुरू करें ताकि आप देख सकें कि API आपकी जरूरतों को पूरा करता है या नहीं, फिर जब आप लाइव जाने के लिए तैयार हों तो अपग्रेड करें।

अब लाइब्रेरी इंस्टॉल हो गई है, चलिए वास्तविक इम्प्लीमेंटेशन में डुबकी लगाते हैं।

## त्वरित उत्तर

- **“create barcode signature” का क्या अर्थ है?** इसका मतलब है एक बारकोड ऑब्जेक्ट बनाना जिसे API के माध्यम से दस्तावेज़ के भीतर रखा, स्थानांतरित या संपादित किया जा सकता है।  
- **क्या मैं बारकोड का आकार बन जाने के बाद बदल सकता हूँ?** हाँ – `setWidth` और `setHeight` मेथड्स का उपयोग करें या उसके `Left`/`Top` कॉर्डिनेट्स को समायोजित करें।  
- **क्या बारकोड अपडेट करने के लिए लाइसेंस चाहिए?** विकास के लिए ट्रायल काम करता है; प्रोडक्शन के लिए फुल लाइसेंस आवश्यक है।  
- **क्या यह केवल PDFs के साथ काम करता है?** नहीं – वही कोड Word, Excel, PowerPoint और इमेज फ़ाइलों के साथ भी काम करता है।  
- **मैं एक साथ कितनी दस्तावेज़ प्रोसेस कर सकता हूँ?** बैच प्रोसेसिंग समर्थित है; बस मेमोरी को try‑with‑resources के साथ मैनेज करें।

## जावा में बारकोड सिग्नेचर कैसे बनाएं

### चरण 1: Signature इंस्टेंस को इनिशियलाइज़ करें

#### क्यों यह महत्वपूर्ण है

`Signature` ऑब्जेक्ट को अपने दस्तावेज़ के गेटवे के रूप में सोचें। यह PDF (या कोई भी समर्थित फ़ॉर्मेट) को मेमोरी में लोड करता है और आपको सभी सिग्नेचर‑संबंधित ऑपरेशन्स तक पहुँच देता है। इस इनिशियलाइज़ेशन के बिना, आप कुछ भी खोज या संशोधित नहीं कर सकते।

#### इम्प्लीमेंटेशन

पहले, आवश्यक क्लास इम्पोर्ट करें और फ़ाइल पाथ को परिभाषित करें:

```java
import com.groupdocs.signature.Signature;
import java.nio.file.Paths;
```

```java
String filePath = "YOUR_DOCUMENT_DIRECTORY/your_document.pdf";
```

```java
Signature signature = new Signature(filePath);
```

**क्या हो रहा है?** कंस्ट्रक्टर फ़ाइल को पढ़ता है और उसे संशोधन के लिए तैयार करता है। पाथ एब्सोल्यूट या रिलेटिव हो सकता है—सिर्फ यह सुनिश्चित करें कि जावा प्रोसेस के पास रीड परमिशन हो।

> **Pro tip:** `Signature` इंस्टेंस बनाने से पहले पाथ को वैलिडेट करें ताकि `FileNotFoundException` से बचा जा सके।

### चरण 2: बारकोड सिग्नेचर खोजें

#### क्यों पहले खोज करना आवश्यक है

आप वह अपडेट नहीं कर सकते जो आप नहीं पा सकते। GroupDocs.Signature एक शक्तिशाली सर्च API प्रदान करता है जो सिग्नेचर को प्रकार के आधार पर फ़िल्टर करता है।

#### इम्प्लीमेंटेशन

सर्च‑से संबंधित क्लासेज़ इम्पोर्ट करें:

```java
import com.groupdocs.signature.options.search.BarcodeSearchOptions;
import com.groupdocs.signature.domain.signatures.BarcodeSignature;
import java.util.List;
```

सर्च ऑप्शन्स को कॉन्फ़िगर करें (डिफ़ॉल्ट सभी पेज़ खोजता है):

```java
BarcodeSearchOptions options = new BarcodeSearchOptions();
```

सर्च चलाएँ:

```java
List<BarcodeSignature> signatures = signature.search(BarcodeSignature.class, options);
```

अब आपके पास `BarcodeSignature` ऑब्जेक्ट्स की एक लिस्ट है, जिनमें `Left`, `Top`, `Width`, `Height`, `Text`, और `EncodeType` जैसी प्रॉपर्टीज़ उपलब्ध हैं।

> **Performance note:** बहुत बड़े PDFs के लिए, सर्च को विशिष्ट पेज़ या बारकोड प्रकार तक सीमित करने पर विचार करें ताकि गति बढ़े।

### चरण 3: बारकोड प्रॉपर्टीज़ अपडेट करें

#### मुख्य इवेंट: बारकोड सिग्नेचर संशोधित करना

अब आप **बारकोड आकार बदल** सकते हैं या इसे जहाँ भी चाहिए, पुनः स्थित कर सकते हैं।

#### इम्प्लीमेंटेशन

पहले, एक्सेप्शन हैंडलिंग क्लासेज़ इम्पोर्ट करें:

```java
import java.io.File;
import com.groupdocs.signature.exception.GroupDocsSignatureException;
```

आउटपुट पाथ सेट करें जहाँ संशोधित दस्तावेज़ सेव होगा:

```java
String fileName = Paths.get(filePath).getFileName().toString();
String outputFilePath = new File("YOUR_OUTPUT_DIRECTORY/UpdateBarcode/" + fileName).getPath();
checkDir(outputFilePath);
```

अब, पहला बारकोड खोजें (या लिस्ट पर इटररेट करें) और बदलाव लागू करें:

```java
if (signatures.size() > 0) {
    BarcodeSignature barcodeSignature = signatures.get(0);
    
    // Update the barcode's position and size
    barcodeSignature.setLeft(100);
    barcodeSignature.setTop(100);
    
    // Apply the changes to the document
    boolean result = signature.update(outputFilePath, barcodeSignature);
    
    if (result) {
        System.out.println("Signature with Barcode '" +
            barcodeSignature.getText() + "' and encode type '"+
            barcodeSignature.getEncodeType().getTypeName() + "' was updated in the document ['" +
            fileName + "'].");
    }
} catch (GroupDocsSignatureException e) {
    System.err.println("Error updating signature: " + e.getMessage());
}
```

**मुख्य बिंदु:**
- `setLeft` / `setTop` बारकोड को मूव करते हैं (कोऑर्डिनेट्स टॉप‑लेफ़्ट कोने से मापे जाते हैं)।
- `update` मेथड एक नई फ़ाइल लिखता है; मूल फ़ाइल अपरिवर्तित रहती है।
- संभावित `GroupDocsSignatureException` को हैंडल करने के लिए कॉल को `try‑catch` ब्लॉक में रैप करें।

## आपको कब बारकोड सिग्नेचर अपडेट करना चाहिए?

सही परिदृश्यों को समझना आपको प्रभावी वर्कफ़्लो डिज़ाइन करने में मदद करता है।

### दस्तावेज़ रीब्रांडिंग और टेम्पलेट अपडेट्स

एक नया लेटरहेड या लेबल लेआउट अक्सर बारकोड को पुनः स्थित करने की आवश्यकता रखता है। जावा के साथ इसे ऑटोमेट करना सैकड़ों फ़ाइलों को मैन्युअली एडिट करने से बेहतर है।

### डेटा माइग्रेशन के बाद बैच प्रोसेसिंग

माइग्रेटेड PDFs आपके वर्तमान बारकोड प्लेसमेंट मानकों का पालन नहीं कर सकते। एक बुल्क अपडेट प्रत्येक दस्तावेज़ को फिर से बनाने के बिना संगति बहाल करता है।

### नियामक अनुपालन समायोजन

लॉजिस्टिक्स या हेल्थकेयर जैसी इंडस्ट्रीज़ बारकोड प्लेसमेंट नियम बदल सकती हैं। एक तेज़ स्क्रिप्ट आपको अनुपालन में रखती है।

### डायनामिक दस्तावेज़ जनरेशन

यदि दस्तावेज़ की सामग्री की लंबाई बदलती है, तो आपको बारकोड कोऑर्डिनेट्स को तुरंत समायोजित करने की आवश्यकता हो सकती है।

**कब अपडेट नहीं करना चाहिए:** यदि आप एक बिल्कुल नया दस्तावेज़ बना रहे हैं, तो शुरू से ही बारकोड को सही जगह रखें, बाद में जोड़कर अपडेट करने के बजाय।

## सामान्य समस्याएँ और समाधान

### समस्या 1: “No Barcode Signatures Found”

**लक्षण:** सर्च एक खाली लिस्ट रिटर्न करता है जबकि आप PDF में बारकोड देख रहे हैं।

**संभावित कारण**
- बारकोड इमेज या फॉर्म फ़ील्ड के रूप में एम्बेडेड हैं, सिग्नेचर ऑब्जेक्ट नहीं।
- दस्तावेज़ पासवर्ड‑प्रोटेक्टेड है।
- आप एक विशिष्ट बारकोड प्रकार के लिए फ़िल्टर कर रहे हैं जो मेल नहीं खाता।

**समाधान**
```java
BarcodeSearchOptions options = new BarcodeSearchOptions();
options.setAllPages(true); // Search all pages, not just the first
List<BarcodeSignature> signatures = signature.search(BarcodeSignature.class, options);

if (signatures.isEmpty()) {
    System.out.println("No barcode signatures found. The barcodes might be images, not signature objects.");
}
```

### समस्या 2: अपडेटेड दस्तावेज़ भ्रष्ट दिखता है

**लक्षण:** अपडेट के बाद PDF नहीं खुल रहा है।

**संभावित कारण**
- डिस्क स्पेस अपर्याप्त है।
- आउटपुट डायरेक्टरी मौजूद नहीं है।
- फ़ाइल‑सिस्टम परमिशन लिखने से रोक रहे हैं।

**समाधान**
```java
File outputDir = new File("YOUR_OUTPUT_DIRECTORY/UpdateBarcode/");
if (!outputDir.exists()) {
    outputDir.mkdirs(); // Create directories if they don't exist
}

// Check write permissions
if (!outputDir.canWrite()) {
    throw new IOException("Cannot write to output directory: " + outputDir.getAbsolutePath());
}
```

### समस्या 3: बड़े दस्तावेज़ों में प्रदर्शन गिरावट

**लक्षण:** ~50 पेज़ से अधिक PDFs के लिए प्रोसेसिंग बहुत धीमी हो जाती है।

**समाधान**
```java
BarcodeSearchOptions options = new BarcodeSearchOptions();
options.setPageNumber(1); // Start with page 1
options.setPagesSetup(new PagesSetup());
options.getPagesSetup().setFirstPage(true);
options.getPagesSetup().setLastPage(false);
```

## प्रदर्शन अनुकूलन टिप्स

### बैच ऑपरेशन्स के लिए मेमोरी मैनेजमेंट

एक समय में एक दस्तावेज़ प्रोसेस करें और जावा को संसाधनों को स्वचालित रूप से साफ़ करने दें:
```java
List<String> documentPaths = getDocumentList();
for (String path : documentPaths) {
    try (Signature sig = new Signature(path)) {
        // Process one document at a time
        // Signature instance is auto‑closed after each iteration
    }
}
```

### सर्च परिणामों को कैश करना

यदि आपको एक ही बारकोड पर कई प्रॉपर्टीज़ बदलनी हैं, तो एक बार सर्च करें और लिस्ट को पुन: उपयोग करें:
```java
List<BarcodeSignature> signatures = signature.search(BarcodeSignature.class, options);

// Update multiple properties
for (BarcodeSignature barcode : signatures) {
    barcode.setLeft(100);
    barcode.setTop(100);
    barcode.setWidth(200);
    barcode.setHeight(50);
}

// Single update call with all changes
signature.update(outputPath, signatures);
```

### बड़े बैच के लिए पैरलल प्रोसेसिंग

हजारों दस्तावेज़ों को तेज़ करने के लिए जावा स्ट्रीम्स का उपयोग करें:
```java
documentPaths.parallelStream().forEach(path -> {
    try (Signature sig = new Signature(path)) {
        List<BarcodeSignature> barcodes = sig.search(BarcodeSignature.class, new BarcodeSearchOptions());
        if (!barcodes.isEmpty()) {
            BarcodeSignature barcode = barcodes.get(0);
            barcode.setLeft(50);  // New position for smaller boxes
            barcode.setTop(10);
            sig.update(generateOutputPath(path), barcode);
        }
    } catch (Exception e) {
        logError(path, e);
    }
});
```

## व्यावहारिक अनुप्रयोग

### उपयोग केस 1: ऑटोमेटेड लॉजिस्टिक्स लेबल अपडेट्स

एक शिपिंग कंपनी ने बॉक्स के आयाम बदल दिए, जिससे 50,000 मौजूदा लेबल्स पर बारकोड को पुनः स्थित करना पड़ा। ऊपर दिया गया पैरलल‑प्रोसेसिंग स्निपेट काम को दिनों से कुछ घंटों में बदल दिया।

### उपयोग केस 2: कॉन्ट्रैक्ट टेम्पलेट मानकीकरण

लीगल काउंसल ने स्कैनिंग के लिए एक निश्चित बारकोड लोकेशन निर्धारित किया। सभी कॉन्ट्रैक्ट PDFs को एक ही बैच में खोजकर और अपडेट करके टीम ने महंगे मैन्युअल री‑प्रिंटिंग से बची।

### उपयोग केस 3: इन्वेंटरी सिस्टम इंटीग्रेशन

ERP अपग्रेड के बाद, प्रोडक्ट बारकोड को नए लेबल प्रिंटर के साथ संरेखित करना पड़ा। प्रोग्रामेटिक रूप से बारकोड आकार और पोजीशन अपडेट करने से समय और सामग्री लागत दोनों बची।

## ट्रबलशूटिंग चेकलिस्ट

सपोर्ट से संपर्क करने से पहले इस चेकलिस्ट को देखें:

- [ ] **फ़ाइल पाथ सही है** और फ़ाइल मौजूद है
- [ ] **रीड/राइट परमिशन** स्रोत और गंतव्य दोनों के लिए प्रदान किए गए हैं
- [ ] **GroupDocs.Signature संस्करण** 23.12 या बाद का है
- [ ] **लाइसेंस सही तरीके से कॉन्फ़िगर किया गया है** (यदि फुल लाइसेंस उपयोग कर रहे हैं)
- [ ] **आउटपुट डायरेक्टरी मौजूद है** या प्रोग्रामेटिक रूप से बनाई गई है
- [ ] **आउटपुट फ़ाइलों के लिए पर्याप्त डिस्क स्पेस** है
- [ ] **कोई अन्य प्रोसेस** स्रोत फ़ाइल को लॉक नहीं कर रहा है
- [ ] **एक्सेप्शन हैंडलिंग** त्रुटियों को कैप्चर करने के लिए मौजूद है

## अक्सर पूछे जाने वाले प्रश्न

**Q: क्या मैं एक ही दस्तावेज़ में कई बारकोड सिग्नेचर जावा कोड को अपडेट कर सकता हूँ?**  
A: बिल्कुल। सर्च द्वारा लौटाए गए `List<BarcodeSignature>` पर इटररेट करें और प्रत्येक के लिए `signature.update()` कॉल करें, या पूरी लिस्ट को एक ही `update` कॉल में पास करें।

**Q: GroupDocs.Signature कौन‑से बारकोड प्रकार समर्थन करता है?**  
A: दर्जनों प्रकार, जैसे Code 128, QR Code, EAN‑13, UPC‑A, DataMatrix, PDF417, आदि। प्रकार देखने के लिए `barcodeSignature.getEncodeType()` का उपयोग करें।

**Q: क्या मैं बारकोड की वास्तविक सामग्री (एन्कोडेड डेटा) बदल सकता हूँ?**  
A: हाँ, `setText()` के माध्यम से, लेकिन स्कैनर सही पढ़ें, इसके लिए विज़ुअल बारकोड को पुनः जनरेट करना याद रखें।

**Q: कई पेज़ पर बारकोड वाले दस्तावेज़ों को कैसे हैंडल करूँ?**  
A: प्रत्येक `BarcodeSignature` में `getPageNumber()` शामिल है। आवश्यकतानुसार पेज‑स्पेसिफिक बारकोड को फ़िल्टर या प्रोसेस करें।

**Q: अपडेट के बाद मूल दस्तावेज़ का क्या होता है?**  
A: स्रोत फ़ाइल अपरिवर्तित रहती है। GroupDocs आपके द्वारा निर्दिष्ट आउटपुट पाथ पर बदलाव लिखता है, जिससे मूल सुरक्षित रहता है।

**Q: क्या मैं पासवर्ड‑प्रोटेक्टेड PDFs में बारकोड अपडेट कर सकता हूँ?**  
A: हाँ। `Signature` कंस्ट्रक्टर के `LoadOptions` ओवरलोड का उपयोग करके पासवर्ड प्रदान करें।

**Q: हजारों दस्तावेज़ों को कुशलतापूर्वक बैच प्रोसेस कैसे करूँ?**  
A: पैरलल स्ट्रीम्स को try‑with‑resources के साथ मिलाएँ (जैसा कि पैरलल‑प्रोसेसिंग उदाहरण में दिखाया गया है) और मेमोरी उपयोग पर नज़र रखें।

**Q: क्या यह PDF के अलावा अन्य फ़ॉर्मेट्स के साथ काम करता है?**  
A: हाँ। वही API Word, Excel, PowerPoint, इमेजेज़ और GroupDocs.Signature द्वारा समर्थित कई अन्य फ़ॉर्मेट्स के साथ काम करता है।

## निष्कर्ष

अब आपके पास जावा में **बारकोड सिग्नेचर** ऑब्जेक्ट बनाने और उनकी पोजीशन, आकार और अन्य प्रॉपर्टीज़ को अपडेट करने के लिए एक पूर्ण, प्रोडक्शन‑रेडी गाइड है। हमने इनिशियलाइज़ेशन, सर्च, मॉडिफिकेशन, ट्रबलशूटिंग और प्रदर्शन ट्यूनिंग को कवर किया है, चाहे वह सिंगल‑डॉक्यूमेंट हो या बड़े बैच परिदृश्य।

### अगले कदम

- एक ही पास में कई प्रॉपर्टीज़ (जैसे रोटेशन, अपारदर्शिता) को अपडेट करने का प्रयोग करें।  
- इस कोड के चारों ओर एक REST सर्विस बनाएं ताकि बारकोड अपडेट्स को API के रूप में एक्सपोज़ किया जा सके।  
- उसी पैटर्न का उपयोग करके अन्य सिग्नेचर प्रकार (टेक्स्ट, इमेज, डिजिटल) का अन्वेषण करें।

GroupDocs.Signature API बारकोड अपडेट्स से कहीं अधिक प्रदान करता है—वेरिफिकेशन, मेटाडाटा हैंडलिंग और मल्टी‑फ़ॉर्मेट सपोर्ट में गहराई से जाएँ ताकि आप अपने दस्तावेज़ वर्कफ़्लो को पूरी तरह ऑटोमेट कर सकें।

**Resources**
- [GroupDocs.Signature for Java Documentation](https://docs.groupdocs.com/signature/java/)
- [API Reference](https://reference.groupdocs.com/signature/java/)
- [Support Forum](https://forum.groupdocs.com/c/signature)
- [Free Trial Download](https://releases.groupdocs.com/signature/java/)

---

**Last Updated:** 2026-01-16  
**Tested With:** GroupDocs.Signature 23.12  
**Author:** GroupDocs  
