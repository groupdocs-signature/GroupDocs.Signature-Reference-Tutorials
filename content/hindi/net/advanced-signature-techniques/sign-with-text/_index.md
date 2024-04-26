---
title: .NET के लिए GroupDocs.Signature का उपयोग करके पाठ के साथ हस्ताक्षर करना
linktitle: पाठ के साथ हस्ताक्षर करना
second_title: GroupDocs.Signature .NET API
description: .NET के लिए GroupDocs.Signature का उपयोग करके टेक्स्ट के साथ दस्तावेज़ों पर हस्ताक्षर करना सीखें। प्रोग्रामेटिक रूप से टेक्स्ट हस्ताक्षर जोड़ने के लिए चरण-दर-चरण मार्गदर्शिका।
type: docs
weight: 17
url: /hi/net/advanced-signature-techniques/sign-with-text/
---
## परिचय
डिजिटल युग में, इलेक्ट्रॉनिक रूप से दस्तावेज़ों पर हस्ताक्षर करना एक मानक अभ्यास बन गया है, जिससे समय और संसाधनों की बचत होती है। GroupDocs.Signature for .NET प्रोग्रामेटिक रूप से विभिन्न दस्तावेज़ स्वरूपों में टेक्स्ट हस्ताक्षर जोड़ने के लिए एक व्यापक समाधान प्रदान करता है। इस ट्यूटोरियल में, हम आपको GroupDocs.Signature for .NET का उपयोग करके टेक्स्ट के साथ दस्तावेज़ पर हस्ताक्षर करने की प्रक्रिया के माध्यम से मार्गदर्शन करेंगे।
## आवश्यक शर्तें
इससे पहले कि हम ट्यूटोरियल में आगे बढ़ें, सुनिश्चित करें कि आपके पास निम्नलिखित पूर्वापेक्षाएँ हैं:
1.  .NET के लिए GroupDocs.Signature: सुनिश्चित करें कि आपके पास GroupDocs.Signature for .NET लाइब्रेरी स्थापित है। आप इसे यहाँ से डाउनलोड कर सकते हैं[यहाँ](https://releases.groupdocs.com/signature/net/).
2. विकास वातावरण: .NET विकास के लिए एक कार्य वातावरण स्थापित करें।
3. दस्तावेज़: वह दस्तावेज़ तैयार करें (उदाहरण के लिए, पीडीएफ, वर्ड) जिस पर आप टेक्स्ट के साथ हस्ताक्षर करना चाहते हैं।

## नामस्थान आयात करें
सबसे पहले, आपको GroupDocs.Signature कार्यात्मकताओं का उपयोग करने के लिए अपने .NET प्रोजेक्ट में आवश्यक नेमस्पेस आयात करने की आवश्यकता है।
```csharp
using System;
using System.IO;
using System.Drawing;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

आइए किसी दस्तावेज़ पर टेक्स्ट के साथ हस्ताक्षर करने की प्रक्रिया को कई चरणों में विभाजित करें:
## चरण 1: दस्तावेज़ लोड करें
जिस दस्तावेज़ पर आप हस्ताक्षर करना चाहते हैं उसे टेक्स्ट के साथ लोड करें।
```csharp
string filePath = "sample.pdf"; // दस्तावेज़ का पथ
string fileName = Path.GetFileName(filePath);
```
## चरण 2: आउटपुट फ़ाइल पथ सेट करें
आउटपुट फ़ाइल पथ को परिभाषित करें जहां हस्ताक्षरित दस्तावेज़ सहेजा जाएगा।
```csharp
string outputFilePath = Path.Combine("Your Document Directory", "SignWithText", fileName);
```
## चरण 3: हस्ताक्षर विकल्प बनाएं
पाठ सामग्री, स्थिति, आकार, रंग और फ़ॉन्ट सहित पाठ हस्ताक्षर के लिए विकल्प सेट करें।
```csharp
TextSignOptions options = new TextSignOptions("John Smith")
{
    Left = 50, // हस्ताक्षर की स्थिति निर्धारित करें
    Top = 200,
    Width = 100, // हस्ताक्षर आयत सेट करें
    Height = 30,
    ForeColor = Color.Red, // टेक्स्ट का रंग सेट करें
    Font = new SignatureFont { Size = 14, FamilyName = "Comic Sans MS" } // फ़ॉन्ट सेट करें
};
```
## चरण 4: दस्तावेज़ पर हस्ताक्षर करें
निर्दिष्ट विकल्पों के साथ दस्तावेज़ पर हस्ताक्षर करने और हस्ताक्षरित दस्तावेज़ को आउटपुट फ़ाइल पथ पर सहेजने के लिए GroupDocs.Signature का उपयोग करें।
```csharp
using (Signature signature = new Signature(filePath))
{
    SignResult result = signature.Sign(outputFilePath, options); // दस्तावेज़ पर हस्ताक्षर करें
    Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).\nFile saved at {outputFilePath}.");
}
```

## निष्कर्ष
इस ट्यूटोरियल में, हमने सीखा कि .NET के लिए GroupDocs.Signature का उपयोग करके टेक्स्ट के साथ दस्तावेज़ पर हस्ताक्षर कैसे करें। इन चरणों का पालन करके, आप सुरक्षा और प्रामाणिकता को बढ़ाते हुए कुशलतापूर्वक अपने दस्तावेज़ों में प्रोग्रामेटिक रूप से टेक्स्ट हस्ताक्षर जोड़ सकते हैं।
## अक्सर पूछे जाने वाले प्रश्न
### क्या मैं टेक्स्ट हस्ताक्षर के स्वरूप को अनुकूलित कर सकता हूँ?
हां, आप अपनी पसंद के अनुसार रंग, फ़ॉन्ट, आकार और टेक्स्ट हस्ताक्षर की स्थिति जैसे विभिन्न मापदंडों को अनुकूलित कर सकते हैं।
### क्या GroupDocs.Signature कई दस्तावेज़ प्रारूपों के साथ संगत है?
हां, GroupDocs.Signature पीडीएफ, वर्ड, एक्सेल, पावरपॉइंट और अन्य सहित विभिन्न दस्तावेज़ प्रारूपों का समर्थन करता है।
### क्या मैं एक ही दस्तावेज़ में एकाधिक टेक्स्ट हस्ताक्षर जोड़ सकता हूँ?
बिल्कुल, आप किसी दस्तावेज़ में एकाधिक टेक्स्ट हस्ताक्षर जोड़ सकते हैं, प्रत्येक के पास अनुकूलन विकल्पों का अपना सेट होता है।
### क्या GroupDocs.Signature हस्ताक्षर करने के बाद दस्तावेज़ की अखंडता सुनिश्चित करता है?
हाँ, GroupDocs.Signature दस्तावेज़ की अखंडता सुनिश्चित करने और हस्ताक्षर करने के बाद छेड़छाड़ को रोकने के लिए मजबूत क्रिप्टोग्राफ़िक एल्गोरिदम का उपयोग करता है।
### क्या खरीदने से पहले परीक्षण के लिए कोई परीक्षण संस्करण उपलब्ध है?
 हां, आप यहां से नि:शुल्क परीक्षण संस्करण डाउनलोड कर सकते हैं[यहाँ](https://releases.groupdocs.com/) खरीदारी करने से पहले सुविधाओं का पता लगाएं।