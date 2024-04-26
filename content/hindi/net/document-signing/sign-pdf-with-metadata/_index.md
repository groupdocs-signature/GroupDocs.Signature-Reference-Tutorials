---
title: मेटाडेटा के साथ पीडीएफ पर हस्ताक्षर करें
linktitle: मेटाडेटा के साथ पीडीएफ पर हस्ताक्षर करें
second_title: GroupDocs.Signature .NET API
description: .NET के लिए GroupDocs.Signature का उपयोग करके मेटाडेटा के साथ PDF दस्तावेज़ों पर हस्ताक्षर करना सीखें। दस्तावेज़ ट्रैसेबिलिटी और प्रामाणिकता को आसानी से बढ़ाएं।
type: docs
weight: 11
url: /hi/net/document-signing/sign-pdf-with-metadata/
---
## परिचय
इस ट्यूटोरियल में, हम सीखेंगे कि .NET के लिए GroupDocs.Signature का उपयोग करके मेटाडेटा के साथ एक पीडीएफ दस्तावेज़ पर हस्ताक्षर कैसे करें। पीडीएफ में मेटाडेटा जोड़ने से दस्तावेज़ के बारे में अतिरिक्त जानकारी मिल सकती है, जैसे लेखकत्व, निर्माण तिथि, दस्तावेज़ आईडी, और बहुत कुछ।
## आवश्यक शर्तें
शुरू करने से पहले, सुनिश्चित करें कि आपके पास निम्नलिखित हैं:
1.  .NET के लिए GroupDocs.Signature: आप इसे यहां से डाउनलोड कर सकते हैं[यहाँ](https://releases.groupdocs.com/signature/net/).
2. एक पीडीएफ दस्तावेज़: हस्ताक्षर के लिए एक नमूना पीडीएफ फ़ाइल तैयार रखें।
3. C# प्रोग्रामिंग का बुनियादी ज्ञान: कोड उदाहरणों को समझने के लिए C# सिंटैक्स से परिचित होना आवश्यक है।
## नामस्थान आयात करें
सबसे पहले, सुनिश्चित करें कि आप आवश्यक कक्षाओं और विधियों तक पहुँचने के लिए आवश्यक नामस्थान आयात करें:
```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## चरण 1: पीडीएफ दस्तावेज़ लोड करें
वह पीडीएफ दस्तावेज़ लोड करें जिस पर आप हस्ताक्षर करना चाहते हैं:
```csharp
string filePath = "sample.pdf";
```
## चरण 2: आउटपुट फ़ाइल पथ निर्दिष्ट करें
आउटपुट फ़ाइल पथ को परिभाषित करें जहां मेटाडेटा के साथ हस्ताक्षरित पीडीएफ सहेजा जाएगा:
```csharp
string outputFilePath = Path.Combine("Your Document Directory", "SignPdfWithMetadata", "SignedWithMetadata.pdf");
```
## चरण 3: हस्ताक्षर उदाहरण बनाएं
पीडीएफ दस्तावेज़ के लिए पथ प्रदान करके एक हस्ताक्षर उदाहरण प्रारंभ करें:
```csharp
using (Signature signature = new Signature(filePath))
{
    // यहां हस्ताक्षर संबंधी कोड जाएगा
}
```
## चरण 4: मेटाडेटा विकल्प परिभाषित करें
MetadataSignOptions बनाएं और मेटाडेटा फ़ील्ड को उनके संबंधित मानों के साथ जोड़ें:
```csharp
MetadataSignOptions options = new MetadataSignOptions();
options
    .Add(new PdfMetadataSignature("Author", "Mr.Sherlock Holmes")) // स्ट्रिंग वैल्यू
    .Add(new PdfMetadataSignature("CreatedOn", DateTime.Now))       // दिनांकसमय मान
    .Add(new PdfMetadataSignature("DocumentId", 123456))            // पूर्णांक मूल्य
    .Add(new PdfMetadataSignature("SignatureId", 123.456D))         // दोगुना मूल्य
    .Add(new PdfMetadataSignature("Amount", 123.456M))              // दशमलव मान
    .Add(new PdfMetadataSignature("Total", 123.456F));              // फ़्लोट मान
```
## चरण 5: दस्तावेज़ पर हस्ताक्षर करें
निर्दिष्ट मेटाडेटा विकल्पों के साथ पीडीएफ दस्तावेज़ पर हस्ताक्षर करें और हस्ताक्षरित दस्तावेज़ को सहेजें:
```csharp
SignResult result = signature.Sign(outputFilePath, options);
Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).\nFile saved at {outputFilePath}.");
```

## निष्कर्ष
इस ट्यूटोरियल में, हमने .NET के लिए GroupDocs.Signature का उपयोग करके मेटाडेटा के साथ एक पीडीएफ दस्तावेज़ पर हस्ताक्षर करने का तरीका बताया है। चरण-दर-चरण मार्गदर्शिका का पालन करके, आप आसानी से अपनी पीडीएफ फाइलों में मेटाडेटा जानकारी जैसे लेखकत्व, निर्माण तिथि और बहुत कुछ जोड़ सकते हैं, जिससे उनकी उपयोगिता और पता लगाने की क्षमता बढ़ जाती है।
## अक्सर पूछे जाने वाले प्रश्न
### क्या मैं अपने पीडीएफ दस्तावेज़ों में कस्टम मेटाडेटा फ़ील्ड जोड़ सकता हूँ?
हां, आप .NET के लिए GroupDocs.Signature का उपयोग करके फ़ील्ड नाम और उसके संबंधित मान को निर्दिष्ट करके कस्टम मेटाडेटा फ़ील्ड जोड़ सकते हैं।
### क्या .NET के लिए GroupDocs.Signature, .NET फ्रेमवर्क के सभी संस्करणों के साथ संगत है?
.NET के लिए GroupDocs.Signature, .NET फ्रेमवर्क के विभिन्न संस्करणों के साथ संगत है, जो लचीलापन और एकीकरण में आसानी सुनिश्चित करता है।
### क्या GroupDocs.Signature पीडीएफ के अलावा अन्य दस्तावेज़ प्रारूपों पर हस्ताक्षर करने का समर्थन करता है?
हाँ, GroupDocs.Signature Word, Excel, PowerPoint और अन्य सहित दस्तावेज़ स्वरूपों की एक विस्तृत श्रृंखला का समर्थन करता है।
### क्या मैं .NET के लिए GroupDocs.Signature का उपयोग करके एक साथ कई दस्तावेज़ों पर हस्ताक्षर कर सकता हूँ?
हाँ, आप फ़ाइलों की सूची को दोहराकर और हस्ताक्षर प्रक्रिया को प्रोग्रामेटिक रूप से लागू करके एक साथ कई दस्तावेज़ों पर हस्ताक्षर कर सकते हैं।
### क्या GroupDocs.Signature उपयोगकर्ताओं के लिए तकनीकी सहायता उपलब्ध है?
 हाँ, GroupDocs अपने मंचों के माध्यम से समर्पित तकनीकी सहायता प्रदान करता है। आप सहायता फ़ोरम तक पहुंच सकते हैं[यहाँ](https://forum.groupdocs.com/c/signature/13).