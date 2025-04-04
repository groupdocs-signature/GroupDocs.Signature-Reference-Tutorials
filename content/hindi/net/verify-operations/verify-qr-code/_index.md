---
title: QR कोड सत्यापित करें
linktitle: QR कोड सत्यापित करें
second_title: GroupDocs.Signature .NET API
description: .NET के लिए GroupDocs.Signature का उपयोग करके दस्तावेज़ों में QR कोड सत्यापित करना सीखें। चरण-दर-चरण मार्गदर्शिका के साथ व्यापक ट्यूटोरियल।
weight: 12
url: /hi/net/verify-operations/verify-qr-code/
---

# QR कोड सत्यापित करें

## परिचय
दस्तावेज़ प्रबंधन और प्रमाणीकरण के क्षेत्र में, हस्ताक्षरों की अखंडता और वैधता सुनिश्चित करना सर्वोपरि है। .NET के लिए GroupDocs.Signature दस्तावेज़ों में एम्बेडेड QR कोड को सत्यापित करने के लिए एक व्यापक समाधान प्रदान करता है। इस ट्यूटोरियल में, हम .NET के लिए GroupDocs.Signature का उपयोग करके QR कोड को सत्यापित करने की चरण-दर-चरण प्रक्रिया के बारे में विस्तार से जानेंगे।
## आवश्यक शर्तें
सत्यापन प्रक्रिया में उतरने से पहले, सुनिश्चित करें कि आपके पास निम्नलिखित शर्तें हैं:
1.  .NET के लिए GroupDocs.Signature की स्थापना: .NET के लिए GroupDocs.Signature को डाउनलोड और इंस्टॉल करें।[लिंक को डाउनलोड करें](https://releases.groupdocs.com/signature/net/).
2. क्यूआर कोड वाले दस्तावेज़ तक पहुंच: सत्यापन के लिए एक नमूना दस्तावेज़ तैयार करें जिसमें क्यूआर कोड शामिल हों। 

## नामस्थान आयात करें
सबसे पहले, आपको .NET के लिए GroupDocs.Signature द्वारा प्रदान की गई कार्यक्षमताओं का उपयोग करने के लिए आवश्यक नेमस्पेस आयात करने की आवश्यकता है। इन चरणों का पालन करें:

```csharp
using System;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```


अब, आइए .NET के लिए GroupDocs.Signature का उपयोग करके किसी दस्तावेज़ में एम्बेडेड QR कोड को सत्यापित करने की प्रक्रिया को तोड़ें:
## चरण 1: दस्तावेज़ पथ निर्दिष्ट करें
```csharp
string filePath = "sample_multiple_signatures.docx";
```
 प्रतिस्थापित करना सुनिश्चित करें`"sample_multiple_signatures.docx"` आपके दस्तावेज़ के पथ के साथ।
## चरण 2: हस्ताक्षर वस्तु को आरंभ करें
```csharp
using (Signature signature = new Signature(filePath))
{
    //सत्यापन कोड यहां जाता है
}
```
 आरंभ करें a`Signature` दस्तावेज़ को पथ प्रदान करके ऑब्जेक्ट करें।
## चरण 3: सत्यापन विकल्प निर्दिष्ट करें
```csharp
QrCodeVerifyOptions options = new QrCodeVerifyOptions()
{
    AllPages = true, // यह मान डिफ़ॉल्ट रूप से सेट है
    Text = "John",
    MatchType = TextMatchType.Contains
};
```
 जैसे सत्यापन विकल्पों को परिभाषित करें`AllPages` सभी पृष्ठों को सत्यापित करने के लिए,`Text` क्यूआर कोड के भीतर मिलान किए जाने वाले टेक्स्ट को निर्दिष्ट करने के लिए, और`MatchType` मिलान मानदंडों को परिभाषित करने के लिए।
## चरण 4: दस्तावेज़ हस्ताक्षर सत्यापित करें
```csharp
VerificationResult result = signature.Verify(options);
```
 का आह्वान करें`Verify` की विधि`Signature` आपत्ति, सत्यापन विकल्प पास करना।
## चरण 5: सत्यापन परिणाम संभालें
```csharp
if (result.IsValid)
{
    // वैध हस्ताक्षर मिले
}
else
{
    // अमान्य हस्ताक्षर पाया गया
}
```
सत्यापन परिणाम के आधार पर, तदनुसार सफलता या विफलता परिदृश्यों को संभालें।

## निष्कर्ष
इस ट्यूटोरियल में, हमने .NET के लिए GroupDocs.Signature का उपयोग करके दस्तावेज़ों के भीतर QR कोड को सत्यापित करने की प्रक्रिया का पता लगाया है। इन चरणों का पालन करके, आप दस्तावेज़ की अखंडता और प्रामाणिकता सुनिश्चित करते हुए, अपने .NET अनुप्रयोगों में QR कोड सत्यापन कार्यक्षमता को सहजता से एकीकृत कर सकते हैं।
## अक्सर पूछे जाने वाले प्रश्न
### क्या .NET के लिए GroupDocs.Signature विभिन्न दस्तावेज़ प्रारूपों में QR कोड सत्यापित कर सकता है?
हां, .NET के लिए GroupDocs.Signature QR कोड सत्यापन के लिए DOCX, PDF और अन्य सहित दस्तावेज़ प्रारूपों की एक विस्तृत श्रृंखला का समर्थन करता है।
### क्या .NET के लिए GroupDocs.Signature के लिए कोई निःशुल्क परीक्षण उपलब्ध है?
 हाँ, आप नि:शुल्क परीक्षण का लाभ उठा सकते हैं[पृष्ठ जारी करता है](https://releases.groupdocs.com/).
### .NET उपयोगकर्ताओं के लिए GroupDocs.Signature के लिए कौन से समर्थन विकल्प उपलब्ध हैं?
 उपयोगकर्ता इसके माध्यम से सहायता प्राप्त कर सकते हैं[मंच](https://forum.groupdocs.com/c/signature/13) GroupDocs.Signature के लिए.
### क्या मैं .NET के लिए GroupDocs.Signature का अस्थायी लाइसेंस खरीद सकता हूँ?
 हाँ, अस्थायी लाइसेंस खरीद के लिए उपलब्ध हैं[ग्रुपडॉक्स खरीद पृष्ठ](https://purchase.groupdocs.com/temporary-license/).
### क्या .NET के लिए GroupDocs.Signature के लिए व्यापक दस्तावेज़ उपलब्ध हैं?
 बिल्कुल, आप दिए गए विस्तृत दस्तावेज़ का संदर्भ ले सकते हैं[यहाँ](https://tutorials.groupdocs.com/signature/net/) .NET के लिए GroupDocs.Signature की कार्यक्षमताओं के उपयोग पर व्यापक मार्गदर्शन के लिए।