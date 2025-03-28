---
title: एकाधिक विकल्पों के साथ हस्ताक्षर करना
linktitle: एकाधिक विकल्पों के साथ हस्ताक्षर करना
second_title: GroupDocs.Signature .NET API
description: .NET के लिए GroupDocs.Signature का उपयोग करके कई विकल्पों के साथ दस्तावेज़ों पर हस्ताक्षर करना सीखें। टेक्स्ट, बारकोड, क्यूआर कोड, डिजिटल और छवि के साथ दस्तावेज़ सुरक्षा बढ़ाएँ।
weight: 14
url: /hi/net/advanced-signature-techniques/sign-with-multiple-options/
---

# एकाधिक विकल्पों के साथ हस्ताक्षर करना

## परिचय
इस ट्यूटोरियल में, हम जानेंगे कि .NET के लिए GroupDocs.Signature लाइब्रेरी का उपयोग करके एकाधिक हस्ताक्षर विकल्पों का उपयोग करके किसी दस्तावेज़ पर हस्ताक्षर कैसे करें। टेक्स्ट, बारकोड, क्यूआर कोड, डिजिटल, छवि और मेटाडेटा हस्ताक्षर जैसे विभिन्न विकल्पों के साथ दस्तावेज़ों पर हस्ताक्षर करना बहुमुखी प्रतिभा प्रदान कर सकता है और दस्तावेज़ सुरक्षा बढ़ा सकता है।
## आवश्यक शर्तें
आरंभ करने से पहले, सुनिश्चित करें कि आपके पास निम्नलिखित शर्तें हैं:
1.  .NET लाइब्रेरी के लिए GroupDocs.Signature: .NET लाइब्रेरी के लिए GroupDocs.Signature को यहां से डाउनलोड और इंस्टॉल करें।[यहाँ](https://releases.groupdocs.com/signature/net/).
2. विकास परिवेश: .NET फ्रेमवर्क स्थापित करके एक विकास परिवेश स्थापित करें।
3. हस्ताक्षर करने के लिए दस्तावेज़: वह दस्तावेज़ तैयार करें (उदाहरण के लिए, नमूना.docx) जिस पर आप हस्ताक्षर करना चाहते हैं।
4. प्रमाणपत्र और छवियाँ: डिजिटल और छवि हस्ताक्षर के लिए कोई भी आवश्यक प्रमाणपत्र और छवियाँ तैयार करें।

## नामस्थान आयात करें
सबसे पहले, अपने .NET एप्लिकेशन में GroupDocs.Signature लाइब्रेरी का उपयोग करने के लिए आवश्यक नामस्थान आयात करें:
```csharp
using System;
using System.IO;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## चरण 1: दस्तावेज़ लोड करें
```csharp
string filePath = "sample.docx";
string outputFilePath = Path.Combine("Your Document Directory", "SignWithMultiple", "SignWithMultiple.docx");
using (Signature signature = new Signature(filePath))
{
    // आपका कोड जारी है...
}
```
## चरण 2: हस्ताक्षर विकल्प परिभाषित करें
विभिन्न प्रकार और सेटिंग्स के कई हस्ताक्षर विकल्पों को परिभाषित करें, जैसे टेक्स्ट, बारकोड, क्यूआर कोड, डिजिटल, छवि और मेटाडेटा हस्ताक्षर:
```csharp
TextSignOptions textOptions = new TextSignOptions("Text signature")
{
    VerticalAlignment = VerticalAlignment.Top,
    HorizontalAlignment = HorizontalAlignment.Left
};
BarcodeSignOptions barcodeOptions = new BarcodeSignOptions("123456")
{
    EncodeType = BarcodeTypes.Code128,
    Left = 0,
    Top = 150,
    Height = 50,
    Width = 200
};
// अन्य हस्ताक्षर विकल्पों को परिभाषित करें (उदाहरण के लिए, क्यूआर कोड, डिजिटल, छवि, मेटाडेटा)...
```
## चरण 3: हस्ताक्षर विकल्पों की एक सूची बनाएं
पहले से परिभाषित सभी विकल्पों वाले हस्ताक्षर विकल्पों की एक सूची परिभाषित करें:
```csharp
List<SignOptions> listOptions = new List<SignOptions>();
listOptions.Add(textOptions);
listOptions.Add(barcodeOptions);
// सूची में अन्य हस्ताक्षर विकल्प जोड़ें...
```
## चरण 4: दस्तावेज़ पर हस्ताक्षर करें
हस्ताक्षर विकल्पों की सूची के साथ दस्तावेज़ पर हस्ताक्षर करें और हस्ताक्षरित दस्तावेज़ को सहेजें:
```csharp
SignResult result = signature.Sign(outputFilePath, listOptions);
Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).\nFile saved at {outputFilePath}.");
```

## निष्कर्ष
.NET के लिए GroupDocs.Signature का उपयोग करके कई विकल्पों के साथ दस्तावेज़ों पर हस्ताक्षर करना दस्तावेज़ सुरक्षा और बहुमुखी प्रतिभा को बढ़ाने के लिए एक मजबूत समाधान प्रदान करता है। इस ट्यूटोरियल में बताए गए चरणों का पालन करके, आप विभिन्न हस्ताक्षर प्रकारों को अपने .NET अनुप्रयोगों में सहजता से एकीकृत कर सकते हैं।
## अक्सर पूछे जाने वाले प्रश्न
### क्या मैं डिजिटल हस्ताक्षरों के लिए कस्टम छवियों का उपयोग कर सकता हूँ?
हां, आप GroupDocs.Signature लाइब्रेरी का उपयोग करके डिजिटल हस्ताक्षरों के लिए कस्टम छवियां निर्दिष्ट कर सकते हैं।
### क्या GroupDocs.Signature विभिन्न दस्तावेज़ प्रारूपों के साथ संगत है?
हां, GroupDocs.Signature DOCX, PDF, PPTX और अन्य सहित विभिन्न दस्तावेज़ प्रारूपों का समर्थन करता है।
### क्या मैं टेक्स्ट हस्ताक्षरों के स्वरूप को अनुकूलित कर सकता हूँ?
बिल्कुल, आप फ़ॉन्ट आकार, रंग और शैली सहित टेक्स्ट हस्ताक्षरों की उपस्थिति को अनुकूलित कर सकते हैं।
### क्या GroupDocs.Signature डिजिटल हस्ताक्षरों के लिए एन्क्रिप्शन प्रदान करता है?
हाँ, GroupDocs.Signature दस्तावेज़ सुरक्षा सुनिश्चित करने के लिए डिजिटल हस्ताक्षर के लिए एन्क्रिप्शन विकल्प प्रदान करता है।
### क्या .NET के लिए GroupDocs.Signature का कोई परीक्षण संस्करण उपलब्ध है?
 हाँ, आप .NET के लिए GroupDocs.Signature का निःशुल्क परीक्षण संस्करण डाउनलोड कर सकते हैं[यहाँ](https://releases.groupdocs.com/).