---
title: मेटाडेटा के साथ प्रस्तुतिकरण पर हस्ताक्षर करें
linktitle: मेटाडेटा के साथ प्रस्तुतिकरण पर हस्ताक्षर करें
second_title: GroupDocs.Signature .NET API
description: .NET के लिए GroupDocs.Signature का उपयोग करके मेटाडेटा के साथ प्रेजेंटेशन फ़ाइलों पर हस्ताक्षर करना सीखें। दस्तावेज़ की अखंडता बढ़ाएँ और बहुमूल्य जानकारी जोड़ें।
type: docs
weight: 12
url: /hi/net/document-signing/sign-presentation-with-metadata/
---
## परिचय
इस ट्यूटोरियल में, हम सीखेंगे कि .NET लाइब्रेरी के लिए GroupDocs.Signature का उपयोग करके मेटाडेटा के साथ प्रेजेंटेशन फ़ाइल (PPTX) पर हस्ताक्षर कैसे करें। मेटाडेटा के साथ प्रस्तुतियों पर हस्ताक्षर करने से दस्तावेज़ में मूल्यवान जानकारी जुड़ जाती है, जैसे लेखक का नाम, निर्माण तिथि, दस्तावेज़ आईडी, हस्ताक्षर आईडी और विभिन्न संख्यात्मक मान।
## आवश्यक शर्तें
शुरू करने से पहले, सुनिश्चित करें कि आपके पास निम्नलिखित हैं:
1.  .NET लाइब्रेरी के लिए GroupDocs.Signature: यहां से लाइब्रेरी डाउनलोड और इंस्टॉल करें[यहाँ](https://releases.groupdocs.com/signature/net/).
2. विकास परिवेश: सुनिश्चित करें कि आपके पास एक .NET विकास परिवेश स्थापित है।
3. प्रस्तुति फ़ाइल: हस्ताक्षर के लिए एक नमूना प्रस्तुति फ़ाइल (पीपीटीएक्स प्रारूप) तैयार रखें।
4. C# की बुनियादी समझ: C# प्रोग्रामिंग भाषा से परिचित होना फायदेमंद होगा।

## नामस्थान आयात करें
कोड में गोता लगाने से पहले, आइए आवश्यक नामस्थान आयात करें:
```csharp
using System;
using System.IO;
    using GroupDocs.Signature;
    using GroupDocs.Signature.Domain;
    using GroupDocs.Signature.Options;
```
## चरण 1: प्रस्तुति फ़ाइल लोड करें
```csharp
string filePath = "sample.pptx";
```
 प्रतिस्थापित करें`"sample.pptx"` आपकी प्रस्तुति फ़ाइल के पथ के साथ।
## चरण 2: आउटपुट फ़ाइल पथ निर्दिष्ट करें
```csharp
string outputFilePath = Path.Combine("Your Document Directory", "SignPresentationWithMetadata", "SignedWithMetadata.pptx");
```
वह निर्देशिका निर्दिष्ट करें जहाँ आप हस्ताक्षरित प्रस्तुति फ़ाइल को फ़ाइल नाम के साथ सहेजना चाहते हैं।
## चरण 3: हस्ताक्षर वस्तु को आरंभ करें
```csharp
using (Signature signature = new Signature(filePath))
```
प्रेजेंटेशन फ़ाइल के लिए पथ प्रदान करके सिग्नेचर ऑब्जेक्ट को प्रारंभ करें।
## चरण 4: मेटाडेटा साइन विकल्प परिभाषित करें
```csharp
MetadataSignOptions options = new MetadataSignOptions();
```
मेटाडेटा हस्ताक्षर विकल्पों को परिभाषित करने के लिए MetadataSignOptions का एक उदाहरण बनाएं।
## चरण 5: मेटाडेटा हस्ताक्षर बनाएं
```csharp
PresentationMetadataSignature[] signatures = new PresentationMetadataSignature[]
{
    new PresentationMetadataSignature("Author", "Mr.Scherlock Holmes"),
    new PresentationMetadataSignature("CreatedOn", DateTime.Now),
    new PresentationMetadataSignature("DocumentId", 123456),
    new PresentationMetadataSignature("SignatureId", 123.456D),
    new PresentationMetadataSignature("Amount", 123.456M),
    new PresentationMetadataSignature("Total", 123.456F)
};
```
प्रेजेंटेशनमेटाडेटासिग्नेचर ऑब्जेक्ट की एक सरणी बनाएं, प्रत्येक मेटाडेटा हस्ताक्षर का प्रतिनिधित्व करता है। आप स्ट्रिंग, डेटटाइम, पूर्णांक, डबल, दशमलव और फ्लोट सहित विभिन्न प्रकार के मेटाडेटा जोड़ सकते हैं।
## चरण 6: विकल्पों में हस्ताक्षर जोड़ें
```csharp
options.Signatures.AddRange(signatures);
```
बनाए गए मेटाडेटा हस्ताक्षरों को MetadataSignOptions ऑब्जेक्ट में जोड़ें।
## चरण 7: दस्तावेज़ पर हस्ताक्षर करें
```csharp
SignResult result = signature.Sign(outputFilePath, options);
```
निर्दिष्ट विकल्पों का उपयोग करके मेटाडेटा के साथ प्रेजेंटेशन फ़ाइल पर हस्ताक्षर करें और हस्ताक्षरित फ़ाइल को आउटपुट पथ पर सहेजें।
## चरण 8: परिणाम प्रदर्शित करें
```csharp
Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).\nFile saved at {outputFilePath}.");
```
लागू किए गए हस्ताक्षरों की संख्या और उस पथ के साथ एक सफलता संदेश प्रदर्शित करें जहां हस्ताक्षरित फ़ाइल सहेजी गई है।

## निष्कर्ष
इस ट्यूटोरियल में, हमने सीखा कि .NET लाइब्रेरी के लिए GroupDocs.Signature का उपयोग करके मेटाडेटा के साथ प्रेजेंटेशन फ़ाइल पर हस्ताक्षर कैसे करें। मेटाडेटा हस्ताक्षर जोड़ने से दस्तावेज़ की अखंडता बढ़ती है और इसकी सामग्री के बारे में बहुमूल्य जानकारी मिलती है।

## अक्सर पूछे जाने वाले प्रश्न
### क्या मैं .NET के लिए GroupDocs.Signature का उपयोग करके मेटाडेटा के साथ PPTX के अलावा अन्य दस्तावेज़ प्रारूपों पर हस्ताक्षर कर सकता हूँ?
हाँ, GroupDocs.Signature मेटाडेटा के साथ हस्ताक्षर करने के लिए वर्ड, एक्सेल, पीडीएफ और अन्य सहित विभिन्न दस्तावेज़ प्रारूपों का समर्थन करता है।
### क्या .NET के लिए GroupDocs.Signature .NET कोर के साथ संगत है?
हां, लाइब्रेरी .NET फ्रेमवर्क और .NET कोर दोनों के साथ संगत है।
### क्या मैं मेटाडेटा हस्ताक्षरों के स्वरूप को अनुकूलित कर सकता हूँ?
हाँ, आप अपनी आवश्यकताओं के अनुसार मेटाडेटा हस्ताक्षरों की उपस्थिति, स्थिति और अन्य गुणों को अनुकूलित कर सकते हैं।
### क्या .NET के लिए GroupDocs.Signature हस्ताक्षरित दस्तावेज़ों के लिए एन्क्रिप्शन प्रदान करता है?
हां, GroupDocs.Signature हस्ताक्षरित दस्तावेज़ों को अनधिकृत पहुंच से सुरक्षित करने के लिए एन्क्रिप्शन विकल्प प्रदान करता है।
### क्या खरीदने से पहले परीक्षण के लिए कोई परीक्षण संस्करण उपलब्ध है?
 हां, आप .NET के लिए GroupDocs.Signature के निःशुल्क परीक्षण का लाभ उठा सकते हैं[यहाँ](https://releases.groupdocs.com/).