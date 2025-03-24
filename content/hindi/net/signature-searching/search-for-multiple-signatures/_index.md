---
title: एकाधिक हस्ताक्षर खोजें
linktitle: एकाधिक हस्ताक्षर खोजें
second_title: GroupDocs.Signature .NET API
description: कुशल दस्तावेज़ सुरक्षा और अखंडता के लिए GroupDocs.Signature का उपयोग करके .NET दस्तावेज़ों में एकाधिक हस्ताक्षरों की खोज करना सीखें।
weight: 14
url: /hi/net/signature-searching/search-for-multiple-signatures/
---
## परिचय
.NET के लिए GroupDocs.Signature एक शक्तिशाली लाइब्रेरी है जो डेवलपर्स को .NET अनुप्रयोगों का उपयोग करके लोकप्रिय दस्तावेज़ प्रारूपों में विभिन्न प्रकार के हस्ताक्षर जोड़ने, खोजने और हटाने में सक्षम बनाता है। इस ट्यूटोरियल में, हम .NET के लिए GroupDocs.Signature का उपयोग करके एक दस्तावेज़ के भीतर एकाधिक हस्ताक्षरों की खोज पर ध्यान केंद्रित करेंगे।
## आवश्यक शर्तें
शुरू करने से पहले, सुनिश्चित करें कि आपके पास निम्नलिखित शर्तें हैं:
- आपके सिस्टम पर विज़ुअल स्टूडियो स्थापित है।
- C# प्रोग्रामिंग भाषा की बुनियादी समझ।
- आपके प्रोजेक्ट में .NET लाइब्रेरी के लिए GroupDocs.Signature स्थापित है। आप इसे यहां से डाउनलोड कर सकते हैं[यहाँ](https://releases.groupdocs.com/signature/net/).

## नामस्थान आयात करें
सबसे पहले, आपको .NET के लिए GroupDocs.Signature द्वारा प्रदान की गई कक्षाओं और विधियों तक पहुँचने के लिए आवश्यक नामस्थान आयात करने की आवश्यकता है।
```csharp
using System;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## चरण 1: दस्तावेज़ लोड करें
वह दस्तावेज़ लोड करें जहाँ आप एकाधिक हस्ताक्षर खोजना चाहते हैं। सुनिश्चित करें कि आपने सही फ़ाइल पथ प्रदान किया है।
```csharp
string filePath = "sample_multiple_signatures.docx";
using (Signature signature = new Signature(filePath))
{
    // आपका कोड यहां जाता है
}
```
## चरण 2: खोज विकल्प परिभाषित करें
टेक्स्ट, डिजिटल, बारकोड, क्यूआर कोड और मेटाडेटा जैसे विभिन्न प्रकार के हस्ताक्षरों के लिए खोज विकल्पों को परिभाषित करें। आप मिलान के लिए पाठ, मिलान प्रकार और सभी पृष्ठों पर खोज जैसे खोज मानदंड निर्दिष्ट कर सकते हैं।
```csharp
// खोज विकल्प परिभाषित करें
TextSearchOptions textOptions = new TextSearchOptions()
{
    AllPages = true
};
DigitalSearchOptions digitalOptions = new DigitalSearchOptions()
{
    AllPages = true
};
BarcodeSearchOptions barcodeOptions = new BarcodeSearchOptions()
{
    AllPages = true,
    Text = "123456",
    MatchType = TextMatchType.Exact
};
QrCodeSearchOptions qrCodeOptions = new QrCodeSearchOptions()
{
    AllPages = true,
    Text = "John",
    MatchType = TextMatchType.Contains
};
MetadataSearchOptions metadataOptions = new MetadataSearchOptions();
```
## चरण 3: सूची में खोज विकल्प जोड़ें
किसी सूची में परिभाषित खोज विकल्प जोड़ें।
```csharp
// सूची में विकल्प जोड़ें
List<SearchOptions> listOptions = new List<SearchOptions>();
listOptions.Add(textOptions);
listOptions.Add(barcodeOptions);
listOptions.Add(qrCodeOptions);
listOptions.Add(metadataOptions);
listOptions.Add(digitalOptions);
```
## चरण 4: हस्ताक्षर खोजें
परिभाषित खोज विकल्पों का उपयोग करके दस्तावेज़ में हस्ताक्षर खोजें।
```csharp
// दस्तावेज़ में हस्ताक्षर खोजें
SearchResult result = signature.Search(listOptions);
if (result.Signatures.Count > 0)
{
    Console.WriteLine($"\nSource document ['{filePath}'] contains following signatures.");
    foreach (var resSignature in result.Signatures)
    {
        Console.WriteLine($"Signature found at page {resSignature.PageNumber} with type {resSignature.SignatureType} and Id#: {resSignature.SignatureId}");
    }
}
else
{
    Helper.WriteError("No one signature was found.");
}
```

## निष्कर्ष
इस ट्यूटोरियल में, हमने सीखा कि .NET के लिए GroupDocs.Signature का उपयोग करके किसी दस्तावेज़ के भीतर एकाधिक हस्ताक्षरों की खोज कैसे करें। दिए गए चरणों का पालन करके, आप दस्तावेज़ सुरक्षा और अखंडता को बढ़ाते हुए, अपने दस्तावेज़ों में विभिन्न प्रकार के हस्ताक्षरों का कुशलतापूर्वक पता लगा सकते हैं।
## अक्सर पूछे जाने वाले प्रश्न
### क्या मैं विभिन्न दस्तावेज़ प्रारूपों में हस्ताक्षर खोज सकता हूँ?
हां, .NET के लिए GroupDocs.Signature वर्ड, पीडीएफ, एक्सेल और अन्य सहित दस्तावेज़ प्रारूपों की एक विस्तृत श्रृंखला का समर्थन करता है।
### क्या हस्ताक्षरों के लिए खोज मानदंड को अनुकूलित करना संभव है?
बिल्कुल, आप अपनी आवश्यकताओं के अनुसार खोज मानदंड तैयार कर सकते हैं, जैसे सटीक टेक्स्ट मिलान निर्दिष्ट करना या सभी पृष्ठों पर खोज करना।
### क्या .NET के लिए GroupDocs.Signature डिजिटल हस्ताक्षरों के लिए समर्थन प्रदान करता है?
हां, आप डिजिटल हस्ताक्षर के साथ-साथ टेक्स्ट, बारकोड और क्यूआर कोड हस्ताक्षर जैसे अन्य प्रकार भी खोज सकते हैं।
### क्या मैं हस्ताक्षर खोज कार्यक्षमता को अपने .NET अनुप्रयोगों में आसानी से एकीकृत कर सकता हूँ?
हां, .NET के लिए GroupDocs.Signature एक सीधा एपीआई प्रदान करता है जो एकीकरण प्रक्रिया को सरल बनाता है।
### मुझे अतिरिक्त सहायता या सहायता कहां मिल सकती है?
 आप GroupDocs.Signature फोरम पर जा सकते हैं[यहाँ](https://forum.groupdocs.com/c/signature/13) किसी भी प्रश्न या सहायता के लिए।