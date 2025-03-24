---
title: दस्तावेज़ से QR कोड हस्ताक्षर हटाएँ
linktitle: दस्तावेज़ से QR कोड हस्ताक्षर हटाएँ
second_title: GroupDocs.Signature .NET API
description: .NET के लिए GroupDocs.Signature का उपयोग करके दस्तावेज़ों से QR कोड हस्ताक्षर हटाने का तरीका जानें। कुशल हस्ताक्षर प्रबंधन के लिए हमारी चरण-दर-चरण मार्गदर्शिका का पालन करें।
weight: 16
url: /hi/net/delete-operations/delete-qr-code-signature/
---

# दस्तावेज़ से QR कोड हस्ताक्षर हटाएँ

## परिचय
इस ट्यूटोरियल में, हम .NET के लिए GroupDocs.Signature का उपयोग करके किसी दस्तावेज़ से QR कोड हस्ताक्षर हटाने की प्रक्रिया में आपका मार्गदर्शन करेंगे। QR कोड हस्ताक्षरों को प्रभावी ढंग से हटाने के लिए इन चरण-दर-चरण निर्देशों का पालन करें।
## आवश्यक शर्तें
शुरू करने से पहले, सुनिश्चित करें कि आपके पास निम्नलिखित शर्तें हैं:
-  .NET के लिए GroupDocs.Signature: सुनिश्चित करें कि आपके .NET प्रोजेक्ट में GroupDocs.Signature लाइब्रेरी स्थापित है। आप इसे यहां से डाउनलोड कर सकते हैं[यहाँ](https://releases.groupdocs.com/signature/net/).
- QR कोड हस्ताक्षर वाला दस्तावेज़: QR कोड हस्ताक्षर वाला एक दस्तावेज़ तैयार करें जिसे आप हटाना चाहते हैं।
- C# का बुनियादी ज्ञान: C# प्रोग्रामिंग भाषा की बुनियादी बातों से खुद को परिचित करें।

## नामस्थान आयात करना
कोड में गोता लगाने से पहले, अपनी C# फ़ाइल में आवश्यक नामस्थान आयात करें:
```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## चरण 1: फ़ाइल पथ परिभाषित करें
```csharp
// दस्तावेज़ निर्देशिका का पथ.
string filePath = "sample_multiple_signatures.docx";
string fileName = Path.GetFileName(filePath);
// संशोधित दस्तावेज़ के लिए आउटपुट फ़ाइल पथ को परिभाषित करें।
string outputFilePath = Path.Combine("Your Document Directory", "DeleteQRCode", fileName);
// स्रोत फ़ाइल की प्रतिलिपि बनाएँ क्योंकि डिलीट विधि उसी दस्तावेज़ के साथ काम करती है।
File.Copy(filePath, outputFilePath, true);
```
## चरण 2: हस्ताक्षर वस्तु को आरंभ करें
```csharp
using (Signature signature = new Signature(outputFilePath))
{
    // क्यूआर कोड हस्ताक्षर खोजने के लिए विकल्प बनाएं।
    QrCodeSearchOptions options = new QrCodeSearchOptions();
    // दस्तावेज़ में QR कोड हस्ताक्षर खोजें।
    List<QrCodeSignature> signatures = signature.Search<QrCodeSignature>(options);
```
## चरण 3: क्यूआर कोड हस्ताक्षर की मौजूदगी की जांच करें
```csharp
    if (signatures.Count > 0)
    {
        // दस्तावेज़ में पाया गया पहला क्यूआर कोड हस्ताक्षर प्राप्त करें।
        QrCodeSignature qrCodeSignature = signatures[0];
```
## चरण 4: क्यूआर कोड हस्ताक्षर हटाएं
```csharp
        // दस्तावेज़ से QR कोड हस्ताक्षर हटाएँ।
        bool result = signature.Delete(qrCodeSignature);
        if (result)
        {
            Console.WriteLine($"Signature with QR-Code '{qrCodeSignature.Text}' and encode type '{qrCodeSignature.EncodeType.TypeName}' was deleted from document ['{fileName}'].");
        }
        else
        {
            Helper.WriteError($"Signature was not deleted from the document! Signature with Barcode '{qrCodeSignature.Text}' and encode type '{qrCodeSignature.EncodeType.TypeName}' was not found!");
        }
    }
}
```
बधाई हो! आपने .NET के लिए GroupDocs.Signature का उपयोग करके दस्तावेज़ से QR कोड हस्ताक्षर सफलतापूर्वक हटा दिया है।

## निष्कर्ष
इस ट्यूटोरियल में, हमने सीखा कि .NET के लिए GroupDocs.Signature का उपयोग करके किसी दस्तावेज़ से QR कोड हस्ताक्षर को कैसे हटाया जाए। दिए गए चरणों का पालन करके, आप अपने .NET अनुप्रयोगों के भीतर हस्ताक्षरों को कुशलतापूर्वक प्रबंधित और हेरफेर कर सकते हैं।
## अक्सर पूछे जाने वाले प्रश्न
### क्या मैं किसी दस्तावेज़ से एकाधिक QR कोड हस्ताक्षर हटा सकता हूँ?
हां, आप सभी क्यूआर कोड हस्ताक्षरों के माध्यम से पुनरावृत्त करने के लिए कोड को संशोधित कर सकते हैं और तदनुसार उन्हें हटा सकते हैं।
### क्या GroupDocs.Signature QR कोड के अलावा अन्य प्रकार के हस्ताक्षरों का समर्थन करता है?
हां, GroupDocs.Signature विभिन्न हस्ताक्षर प्रकारों जैसे टेक्स्ट, छवि, बारकोड और बहुत कुछ का समर्थन करता है।
### क्या GroupDocs.Signature सभी दस्तावेज़ प्रारूपों के साथ संगत है?
GroupDocs.Signature पीडीएफ, माइक्रोसॉफ्ट वर्ड, एक्सेल, पॉवरपॉइंट और अन्य सहित दस्तावेज़ प्रारूपों की एक विस्तृत श्रृंखला का समर्थन करता है।
### क्या मैं हस्ताक्षरों के लिए खोज विकल्पों को अनुकूलित कर सकता हूँ?
हाँ, आप दस्तावेज़ के भीतर विशिष्ट हस्ताक्षरों का पता लगाने के लिए अपनी आवश्यकताओं के अनुसार खोज विकल्पों को अनुकूलित कर सकते हैं।
### क्या GroupDocs.Signature के लिए कोई परीक्षण संस्करण उपलब्ध है?
 हां, आप GroupDocs.Signature के निःशुल्क परीक्षण संस्करण तक पहुंच सकते हैं[यहाँ](https://releases.groupdocs.com/).