---
title: मेटाडेटा के साथ छवि पर हस्ताक्षर करें
linktitle: मेटाडेटा के साथ छवि पर हस्ताक्षर करें
second_title: GroupDocs.Signature .NET API
description: GroupDocs.Signature का उपयोग करके .NET में मेटाडेटा के साथ छवियों पर हस्ताक्षर करना सीखें। आसान, कुशल और अनुकूलन योग्य मेटाडेटा हस्ताक्षर समाधान।
type: docs
weight: 10
url: /hi/net/document-signing/sign-image-with-metadata/
---
## परिचय
.NET के लिए GroupDocs.Signature डेवलपर्स को मेटाडेटा के साथ छवियों पर कुशलतापूर्वक हस्ताक्षर करने में सक्षम बनाता है। यह ट्यूटोरियल चरण दर चरण प्रक्रिया में आपका मार्गदर्शन करता है।
## आवश्यक शर्तें
शुरू करने से पहले, सुनिश्चित करें कि आपके पास निम्नलिखित हैं:
1. .NET के लिए GroupDocs.Signature: अपने .NET प्रोजेक्ट में GroupDocs.Signature पैकेज स्थापित करें। आप इसे यहां से डाउनलोड कर सकते हैं[यहाँ](https://releases.groupdocs.com/signature/net/).   
2. छवि फ़ाइल: वह छवि फ़ाइल तैयार करें जिस पर आप मेटाडेटा के साथ हस्ताक्षर करना चाहते हैं।

## नामस्थान आयात करें
अपने C# कोड में आवश्यक नामस्थान आयात करना सुनिश्चित करें:
```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## चरण 1: छवि फ़ाइल लोड करें
सबसे पहले, अपनी छवि फ़ाइल का पथ और मेटाडेटा के साथ हस्ताक्षरित छवि के लिए आउटपुट निर्देशिका निर्दिष्ट करें:
```csharp
string filePath = "sample.png";            
string outputFilePath = Path.Combine("Your Document Directory", "SignImageWithMetadata", "SignedWithMetadata.png");
```
## चरण 2: मेटाडेटा हस्ताक्षर बनाएं
इसके बाद, अलग-अलग मेटाडेटा हस्ताक्षर बनाएं और उन्हें विकल्प हस्ताक्षर संग्रह में जोड़ें:
```csharp
using (Signature signature = new Signature(filePath))
{
    ushort imgsMetadataId = 41996;
    MetadataSignOptions options = new MetadataSignOptions();
    options
        .Add(new ImageMetadataSignature(imgsMetadataId++, "Mr.Scherlock Holmes")) // स्ट्रिंग वैल्यू
        .Add(new ImageMetadataSignature(imgsMetadataId++, DateTime.Now))          // दिनांक समय मान
        .Add(new ImageMetadataSignature(imgsMetadataId++, 123456))                // पूर्णांक मूल्य
        .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456D))              // दोगुना मूल्य
        .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456M))              // दशमलव मान
        .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456F));             // फ़्लोट मान
    
    // फ़ाइल करने के लिए दस्तावेज़ पर हस्ताक्षर करें
    SignResult result = signature.Sign(outputFilePath, options);
    Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).\nFile saved at {outputFilePath}.");
}
```

## निष्कर्ष
इस ट्यूटोरियल में, आपने सीखा कि .NET के लिए GroupDocs.Signature का उपयोग करके मेटाडेटा के साथ एक छवि पर हस्ताक्षर कैसे करें। इन चरणों का पालन करके, आप आसानी से अपने .NET अनुप्रयोगों में मेटाडेटा हस्ताक्षर शामिल कर सकते हैं।

## अक्सर पूछे जाने वाले प्रश्न
### क्या मैं .NET के लिए GroupDocs.Signature का उपयोग करके मेटाडेटा के साथ एकाधिक छवियों पर हस्ताक्षर कर सकता हूँ?
हां, आप प्रत्येक छवि फ़ाइल के माध्यम से पुनरावृत्ति करके और मेटाडेटा हस्ताक्षर लागू करके मेटाडेटा के साथ एकाधिक छवियों पर हस्ताक्षर कर सकते हैं।
### क्या .NET के लिए GroupDocs.Signature का कोई परीक्षण संस्करण उपलब्ध है?
 हां, आप यहां से परीक्षण संस्करण डाउनलोड कर सकते हैं[यहाँ](https://releases.groupdocs.com/).
### क्या .NET के लिए GroupDocs.Signature छवियों के अलावा अन्य फ़ाइल स्वरूपों का समर्थन करता है?
हाँ, GroupDocs.Signature पीडीएफ, वर्ड, एक्सेल और अन्य सहित विभिन्न फ़ाइल स्वरूपों का समर्थन करता है।
### क्या मैं मेटाडेटा हस्ताक्षर के स्वरूप को अनुकूलित कर सकता हूँ?
हां, आप मेटाडेटा हस्ताक्षर के स्वरूप को अनुकूलित कर सकते हैं, जैसे फ़ॉन्ट आकार, रंग और स्थिति।
### मुझे .NET के लिए GroupDocs.Signature के लिए समर्थन कहाँ से मिल सकता है?
 आप GroupDocs.Signature फोरम से समर्थन प्राप्त कर सकते हैं[यहाँ](https://forum.groupdocs.com/c/signature/13).