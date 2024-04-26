---
title: आईडी के आधार पर हस्ताक्षर हटाएं
linktitle: आईडी के आधार पर हस्ताक्षर हटाएं
second_title: GroupDocs.Signature .NET API
description: GroupDocs.Signature लाइब्रेरी का उपयोग करके .NET दस्तावेज़ों में आईडी द्वारा हस्ताक्षर को हटाने का तरीका जानें। आसान चरण-दर-चरण मार्गदर्शिका.
type: docs
weight: 11
url: /hi/net/delete-operations/delete-signature-by-id/
---
## परिचय
इस ट्यूटोरियल में, हम जानेंगे कि .NET के लिए GroupDocs.Signature का उपयोग करके किसी हस्ताक्षर को उसकी आईडी से कैसे हटाया जाए। .NET के लिए GroupDocs.Signature एक शक्तिशाली लाइब्रेरी है जो डेवलपर्स को .NET अनुप्रयोगों का उपयोग करके विभिन्न दस्तावेज़ प्रारूपों में डिजिटल हस्ताक्षर जोड़ने, हटाने या सत्यापित करने की अनुमति देता है।
## आवश्यक शर्तें
शुरू करने से पहले, सुनिश्चित करें कि आपके पास निम्नलिखित शर्तें हैं:
1.  .NET लाइब्रेरी के लिए GroupDocs.Signature: यहां से लाइब्रेरी डाउनलोड और इंस्टॉल करें[यहाँ](https://releases.groupdocs.com/signature/net/).
2. .NET फ्रेमवर्क: सुनिश्चित करें कि आपके सिस्टम पर .NET फ्रेमवर्क स्थापित है।
3. हस्ताक्षर वाला दस्तावेज़: जिस हस्ताक्षर को आप हटाना चाहते हैं, उसके साथ एक दस्तावेज़ (उदाहरण के लिए, DOCX, PDF) तैयार करें।

## नामस्थान आयात करें
```csharp
using System;
using System.IO;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## चरण 1: फ़ाइल पथ परिभाषित करें
सबसे पहले, हस्ताक्षर वाले दस्तावेज़ के लिए फ़ाइल पथ और आउटपुट फ़ाइल पथ निर्दिष्ट करें जहां संशोधित दस्तावेज़ सहेजा जाएगा।
```csharp
string filePath = "sample_multiple_signatures.docx";
string fileName = Path.GetFileName(filePath);
string outputFilePath = Path.Combine("Your Document Directory", "DeleteById", fileName);
```
## चरण 2: दस्तावेज़ की प्रतिलिपि बनाएँ
 के बाद से`Delete` विधि दस्तावेज़ को उसी स्थान पर संशोधित करती है, मूल दस्तावेज़ की एक प्रति बनाना सबसे अच्छा है।
```csharp
File.Copy(filePath, outputFilePath, true);
```
## चरण 3: आईडी द्वारा हस्ताक्षर हटाएं
 को आरंभ करें`Signature` दस्तावेज़ फ़ाइल पथ के साथ ऑब्जेक्ट करें और इसका उपयोग करें`Delete` इसकी आईडी द्वारा हस्ताक्षर हटाने की विधि।
```csharp
using (Signature signature = new Signature(outputFilePath))
{
    string id = @"eff64a14-dad9-47b0-88e5-2ee4e3604e71";
    bool result = signature.Delete(id);
    if (result)
    {
        Console.WriteLine($"Signature with Id# '{id}' was deleted from document ['{fileName}'].");
    }
    else
    {
        Helper.WriteError($"Signature was not deleted from the document! Signature with id# '{id}' was not found!");
    }
}
```

## निष्कर्ष
इस ट्यूटोरियल में, हमने सीखा कि .NET के लिए GroupDocs.Signature का उपयोग करके किसी हस्ताक्षर को उसकी आईडी से कैसे हटाया जाए। यह लाइब्रेरी विभिन्न दस्तावेज़ प्रारूपों में डिजिटल हस्ताक्षरों को प्रोग्रामेटिक रूप से प्रबंधित करने का एक सुविधाजनक तरीका प्रदान करती है।
## अक्सर पूछे जाने वाले प्रश्न
### क्या मैं एक साथ अनेक हस्ताक्षर हटा सकता हूँ?
 हाँ, आप एकाधिक हस्ताक्षरों को उनकी आईडी के माध्यम से दोहराकर और कॉल करके हटा सकते हैं`Delete` प्रत्येक आईडी के लिए विधि.
### क्या .NET के लिए GroupDocs.Signature सभी दस्तावेज़ प्रारूपों के साथ संगत है?
.NET के लिए GroupDocs.Signature PDF, DOCX, XLSX और अन्य सहित दस्तावेज़ प्रारूपों की एक विस्तृत श्रृंखला का समर्थन करता है।
### क्या मैं हस्ताक्षर का स्वरूप अनुकूलित कर सकता हूँ?
हाँ, आप हस्ताक्षर की स्थिति, आकार, फ़ॉन्ट और रंग सहित उसके स्वरूप को अनुकूलित कर सकते हैं।
### क्या कोई परीक्षण संस्करण उपलब्ध है?
 हां, आप यहां से नि:शुल्क परीक्षण संस्करण डाउनलोड कर सकते हैं[यहाँ](https://releases.groupdocs.com/).
### मुझे .NET के लिए GroupDocs.Signature के लिए सहायता या समर्थन कहां मिल सकता है?
 आप सहायता मंच पर जा सकते हैं[यहाँ](https://forum.groupdocs.com/c/signature/13) सहायता के लिए।