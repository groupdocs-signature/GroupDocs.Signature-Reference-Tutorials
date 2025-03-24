---
title: मेटाडेटा के साथ वर्ड प्रोसेसिंग पर हस्ताक्षर करें
linktitle: मेटाडेटा के साथ वर्ड प्रोसेसिंग पर हस्ताक्षर करें
second_title: GroupDocs.Signature .NET API
description: .NET के लिए GroupDocs.Signature का उपयोग करके मेटाडेटा के साथ Word Processing दस्तावेज़ों पर हस्ताक्षर करना सीखें। दस्तावेज़ की प्रामाणिकता और पता लगाने की क्षमता बढ़ाएँ।
weight: 14
url: /hi/net/document-signing/sign-word-processing-with-metadata/
---
## परिचय
इस ट्यूटोरियल में, हम आपको GroupDocs.Signature for .NET का उपयोग करके मेटाडेटा के साथ वर्ड प्रोसेसिंग दस्तावेज़ पर हस्ताक्षर करने की प्रक्रिया के बारे में बताएंगे। मेटाडेटा हस्ताक्षर आपको अपने दस्तावेज़ में अतिरिक्त जानकारी एम्बेड करने की अनुमति देता है, जैसे कि लेखक का नाम, निर्माण तिथि, दस्तावेज़ आईडी, और बहुत कुछ।
## आवश्यक शर्तें
शुरू करने से पहले, सुनिश्चित करें कि आपके पास निम्नलिखित हैं:
- .NET पुस्तकालय के लिए GroupDocs.Signature स्थापित किया गया।
- वर्ड प्रोसेसिंग दस्तावेज़ (जैसे, .docx) तक पहुंच.
- C# प्रोग्रामिंग भाषा का बुनियादी ज्ञान।

## नामस्थान आयात करें
सबसे पहले, आपको अपने C# प्रोजेक्ट में आवश्यक नेमस्पेस आयात करने होंगे:
```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## चरण 1: फ़ाइल पथ सेट करें
उस वर्ड प्रोसेसिंग दस्तावेज़ का फ़ाइल पथ परिभाषित करें जिस पर आप हस्ताक्षर करना चाहते हैं तथा आउटपुट फ़ाइल पथ जहाँ हस्ताक्षरित दस्तावेज़ सहेजा जाएगा।
```csharp
string filePath = "sample.docx";
string outputFilePath = Path.Combine("Your Document Directory", "SignWordProcessingWithMetadata", "SignedWithMetadata.docx");
```
## चरण 2: हस्ताक्षर वस्तु को आरंभ करें
जिस दस्तावेज़ पर आप हस्ताक्षर करना चाहते हैं उसका फ़ाइल पथ पास करके एक हस्ताक्षर ऑब्जेक्ट बनाएँ।
```csharp
using (Signature signature = new Signature(filePath))
{
    // हस्ताक्षर संबंधी कार्य यहां किए जाएंगे
}
```
## चरण 3: मेटाडेटा साइन विकल्प परिभाषित करें
अब, आइए मेटाडेटा संकेत विकल्प बनाएं और विभिन्न प्रकार के मेटाडेटा हस्ताक्षर जोड़ें।
```csharp
MetadataSignOptions options = new MetadataSignOptions();
// मेटाडेटा हस्ताक्षर जोड़ें
options
    .Add(new WordProcessingMetadataSignature("Author", "Mr.Sherlock Holmes")) // स्ट्रिंग वैल्यू
    .Add(new WordProcessingMetadataSignature("CreatedOn", DateTime.Now))      // दिनांकसमय मान
    .Add(new WordProcessingMetadataSignature("DocumentId", 123456))           // पूर्णांक मूल्य
    .Add(new WordProcessingMetadataSignature("SignatureId", 123.456D))        // दोगुना मूल्य
    .Add(new WordProcessingMetadataSignature("Amount", 123.456M))             // दशमलव मान
    .Add(new WordProcessingMetadataSignature("Total", 123.456F));             // फ़्लोट मान
```
## चरण 4: दस्तावेज़ पर हस्ताक्षर करें
अब, आइए निर्धारित मेटाडेटा विकल्पों के साथ दस्तावेज़ पर हस्ताक्षर करें और हस्ताक्षरित दस्तावेज़ को आउटपुट फ़ाइल पथ पर सहेजें।
```csharp
SignResult result = signature.Sign(outputFilePath, options);
Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).\nFile saved at {outputFilePath}.");
```
यह .NET के लिए GroupDocs.Signature का उपयोग करके मेटाडेटा के साथ Word प्रसंस्करण दस्तावेज़ पर हस्ताक्षर करने की प्रक्रिया को समाप्त करता है।

## निष्कर्ष
इस ट्यूटोरियल में, हमने सीखा कि .NET के लिए GroupDocs.Signature का उपयोग करके मेटाडेटा के साथ वर्ड प्रोसेसिंग दस्तावेज़ पर हस्ताक्षर कैसे करें। मेटाडेटा हस्ताक्षर आपके दस्तावेज़ों में बहुमूल्य जानकारी जोड़ता है, जिससे उनकी प्रामाणिकता और पता लगाने की क्षमता बढ़ती है।
## अक्सर पूछे जाने वाले प्रश्न
### क्या मैं .NET के लिए GroupDocs.Signature का उपयोग करके कस्टम मेटाडेटा के साथ दस्तावेज़ों पर हस्ताक्षर कर सकता हूँ?
हाँ, आप कस्टम मेटाडेटा फ़ील्ड परिभाषित कर सकते हैं और उनके साथ दस्तावेज़ों पर हस्ताक्षर कर सकते हैं।
### क्या GroupDocs.Signature for .NET विभिन्न दस्तावेज़ प्रारूपों के साथ संगत है?
हां, GroupDocs.Signature वर्ड प्रोसेसिंग, पीडीएफ और अन्य सहित दस्तावेज़ प्रारूपों की एक विस्तृत श्रृंखला का समर्थन करता है।
### क्या मैं उपयोगकर्ता की सहभागिता के बिना दस्तावेज़ों पर प्रोग्रामेटिक रूप से हस्ताक्षर कर सकता हूँ?
बिल्कुल, GroupDocs.Signature आपको अपने एप्लिकेशन के भीतर दस्तावेज़ पर हस्ताक्षर करने की प्रक्रिया को स्वचालित करने की अनुमति देता है।
### क्या .NET के लिए GroupDocs.Signature का कोई परीक्षण संस्करण उपलब्ध है?
हाँ, आप GroupDocs वेबसाइट से निःशुल्क परीक्षण संस्करण प्राप्त कर सकते हैं।
### क्या .NET के लिए GroupDocs.Signature डिजिटल हस्ताक्षरों का समर्थन करता है?
हाँ, GroupDocs.Signature दस्तावेज़ों के लिए डिजिटल और मेटाडेटा हस्ताक्षर दोनों का समर्थन करता है।