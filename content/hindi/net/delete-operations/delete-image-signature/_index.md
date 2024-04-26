---
title: छवि हस्ताक्षर हटाएँ
linktitle: छवि हस्ताक्षर हटाएँ
second_title: GroupDocs.Signature .NET API
description: .NET के लिए GroupDocs.Signature का उपयोग करके दस्तावेज़ों से छवि हस्ताक्षर हटाने का तरीका जानें। कुशल हस्ताक्षर प्रबंधन के लिए हमारी चरण-दर-चरण मार्गदर्शिका का पालन करें।
type: docs
weight: 14
url: /hi/net/delete-operations/delete-image-signature/
---
## परिचय
इस ट्यूटोरियल में, हम जानेंगे कि .NET के लिए GroupDocs.Signature का उपयोग करके दस्तावेज़ों से छवि हस्ताक्षर कैसे हटाएं। GroupDocs.Signature एक शक्तिशाली लाइब्रेरी है जो डेवलपर्स को विभिन्न दस्तावेज़ प्रारूपों के भीतर डिजिटल हस्ताक्षर, टिकट और फॉर्म फ़ील्ड के साथ काम करने की अनुमति देती है।
## आवश्यक शर्तें
शुरू करने से पहले, सुनिश्चित करें कि आपके पास निम्नलिखित हैं:
### 1. .NET के लिए GroupDocs.Signature
 .NET के लिए GroupDocs.Signature को डाउनलोड और इंस्टॉल करें[वेबसाइट](https://releases.groupdocs.com/signature/net/). दस्तावेज़ में दिए गए इंस्टॉलेशन निर्देशों का पालन करें।
### 2. .NET फ्रेमवर्क
सुनिश्चित करें कि आपकी मशीन पर .NET फ्रेमवर्क स्थापित है।
## नामस्थान आयात करें
अपने प्रोजेक्ट में आवश्यक नामस्थान शामिल करें:
```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
आइए छवि हस्ताक्षरों को हटाने की प्रक्रिया को कई चरणों में विभाजित करें:
## चरण 1: फ़ाइल पथ परिभाषित करें
सबसे पहले, हस्ताक्षर हटाने के बाद इनपुट दस्तावेज़ और आउटपुट दस्तावेज़ के लिए पथ निर्दिष्ट करें:
```csharp
string filePath = "sample_multiple_signatures.docx";
string fileName = Path.GetFileName(filePath);
string outputFilePath = Path.Combine("Your Document Directory", "DeleteImage", fileName);
```
## चरण 2: स्रोत फ़ाइल की प्रतिलिपि बनाएँ
 के बाद से`Delete`विधि समान दस्तावेज़ के साथ काम करती है, स्रोत फ़ाइल को किसी अन्य स्थान पर कॉपी करना आवश्यक है:
```csharp
File.Copy(filePath, outputFilePath, true);
```
## चरण 3: हस्ताक्षर वस्तु को आरंभ करें
 का एक उदाहरण बनाएं`Signature` क्लास बनाएं और आउटपुट दस्तावेज़ का पथ निर्दिष्ट करें:
```csharp
using (Signature signature = new Signature(outputFilePath))
{
    // कोड यहाँ जाता है
}
```
## चरण 4: छवि हस्ताक्षर खोजें
खोज विकल्पों को परिभाषित करें और दस्तावेज़ के भीतर छवि हस्ताक्षर खोजें:
```csharp
ImageSearchOptions options = new ImageSearchOptions();
List<ImageSignature> signatures = signature.Search<ImageSignature>(options);
```
## चरण 5: छवि हस्ताक्षर हटाएँ
यदि छवि हस्ताक्षर पाए जाते हैं, तो पहले वाले को हटा दें:
```csharp
if (signatures.Count > 0)
{
    ImageSignature imageSignature = signatures[0];
    bool result = signature.Delete(imageSignature);
    if (result)
    {
        Console.WriteLine($"Image signature at location {imageSignature.Left}x{imageSignature.Top} and Size {imageSignature.Size} was deleted from document ['{fileName}'].");
    }
    else
    {
        Helper.WriteError($"Signature was not deleted from the document! Signature at location {imageSignature.Left}x{imageSignature.Top} and Size {imageSignature.Size} was not found!");
    }
}
```
## निष्कर्ष
इस ट्यूटोरियल में, हमने सीखा कि .NET के लिए GroupDocs.Signature का उपयोग करके दस्तावेज़ों से छवि हस्ताक्षर कैसे हटाएं। चरण-दर-चरण मार्गदर्शिका का पालन करके, डेवलपर्स अपने अनुप्रयोगों के भीतर डिजिटल हस्ताक्षरों को कुशलतापूर्वक प्रबंधित कर सकते हैं।
## अक्सर पूछे जाने वाले प्रश्न
### क्या मैं किसी दस्तावेज़ से एकाधिक छवि हस्ताक्षर हटा सकता हूँ?
 हां, आप बार-बार दोहराकर एकाधिक छवि हस्ताक्षरों को हटाने के लिए कोड को संशोधित कर सकते हैं`signatures` सूची।
### क्या GroupDocs.Signature DOCX के अलावा अन्य दस्तावेज़ प्रारूपों का समर्थन करता है?
हां, GroupDocs.Signature पीडीएफ, पीपीटी, एक्सएलएस और अन्य सहित दस्तावेज़ प्रारूपों की एक विस्तृत श्रृंखला का समर्थन करता है।
### क्या .NET के लिए GroupDocs.Signature का कोई परीक्षण संस्करण उपलब्ध है?
 हाँ, आप नि:शुल्क परीक्षण संस्करण डाउनलोड कर सकते हैं[वेबसाइट](https://releases.groupdocs.com/).
### मैं GroupDocs.Signature के लिए समर्थन कैसे प्राप्त कर सकता हूँ?
 आप विजिट कर सकते हैं[GroupDocs.हस्ताक्षर मंच](https://forum.groupdocs.com/c/signature/13) सहायता और समर्थन के लिए.
### क्या मैं GroupDocs.Signature के लिए अस्थायी लाइसेंस खरीद सकता हूँ?
 हां, आप यहां से अस्थायी लाइसेंस खरीद सकते हैं[खरीद पृष्ठ](https://purchase.groupdocs.com/temporary-license/).