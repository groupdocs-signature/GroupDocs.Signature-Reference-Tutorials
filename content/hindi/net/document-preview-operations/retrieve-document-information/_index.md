---
title: दस्तावेज़ जानकारी पुनः प्राप्त करें
linktitle: दस्तावेज़ जानकारी पुनः प्राप्त करें
second_title: GroupDocs.Signature .NET API
description: GroupDocs.Signature के साथ .NET में दस्तावेज़ प्रबंधन बढ़ाएँ। चरण-दर-चरण दस्तावेज़ जानकारी पुनर्प्राप्त करें। विभिन्न प्रारूपों का समर्थन करता है.
weight: 11
url: /hi/net/document-preview-operations/retrieve-document-information/
---

# दस्तावेज़ जानकारी पुनः प्राप्त करें

## परिचय
डिजिटल दस्तावेज़ीकरण के क्षेत्र में, प्रामाणिकता और अखंडता सुनिश्चित करना सर्वोपरि है। .NET के लिए GroupDocs.Signature, .NET वातावरण के भीतर दस्तावेज़ हस्ताक्षरों के प्रबंधन के लिए एक मजबूत समाधान प्रदान करता है। इस ट्यूटोरियल में, हम .NET के लिए GroupDocs.Signature का उपयोग करके दस्तावेज़ जानकारी पुनर्प्राप्त करने की प्रक्रिया में गहराई से उतरते हैं, व्यापक समझ के लिए प्रत्येक चरण को तोड़ते हैं।
## आवश्यक शर्तें
ट्यूटोरियल में जाने से पहले, सुनिश्चित करें कि आपके पास निम्नलिखित आवश्यक शर्तें हैं:
1.  इंस्टालेशन: .NET के लिए GroupDocs.Signature को यहां से डाउनलोड करके इंस्टाल करें[यहाँ](https://releases.groupdocs.com/signature/net/).
2. .NET वातावरण: .NET ढांचे का कार्यसाधक ज्ञान हो।
3. दस्तावेज़: परीक्षण उद्देश्यों के लिए एक नमूना दस्तावेज़ तैयार करें (उदाहरण के लिए, "sample_multiple_signatures.docx")।

## नामस्थान आयात करना
दस्तावेज़ हस्ताक्षर पुनर्प्राप्ति प्रक्रिया के साथ आगे बढ़ने से पहले, आवश्यक नामस्थान आयात करें:
```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
```

## चरण 1: दस्तावेज़ फ़ाइल पथ सेट करें:
जिस दस्तावेज़ से आप जानकारी प्राप्त करना चाहते हैं उसके लिए फ़ाइल पथ परिभाषित करें।
```csharp
string filePath = "sample_multiple_signatures.docx";
```
## चरण 2: त्वरित हस्ताक्षर वस्तु:
 का एक उदाहरण बनाएं`Signature` दस्तावेज़ फ़ाइल पथ पास करके कक्षा।
```csharp
using (Signature signature = new Signature(filePath))
{

}
```
## चरण 3: दस्तावेज़ जानकारी पुनः प्राप्त करें:
 का उपयोग करें`GetDocumentInfo()` दस्तावेज़ के बारे में व्यापक जानकारी प्राप्त करने की विधि।
```csharp
IDocumentInfo documentInfo = signature.GetDocumentInfo();
```
## चरण 4: दस्तावेज़ गुण प्रदर्शित करें:
दस्तावेज़ के विभिन्न गुणों जैसे प्रारूप, विस्तार, आकार, पृष्ठ संख्या आदि को आउटपुट करें।
```csharp
Console.WriteLine($"Document properties {Path.GetFileName(filePath)}:");
Console.WriteLine($" - format : {documentInfo.FileType.FileFormat}");
Console.WriteLine($" - extension : {documentInfo.FileType.Extension}");
Console.WriteLine($" - size : {documentInfo.Size}");
Console.WriteLine($" - page count : {documentInfo.PageCount}");
Console.WriteLine($" - Form Fields count : {documentInfo.FormFields.Count}");
Console.WriteLine($" - Text signatures count : {documentInfo.TextSignatures.Count}");
Console.WriteLine($" - Image signatures count : {documentInfo.ImageSignatures.Count}");
Console.WriteLine($" - Digital signatures count : {documentInfo.DigitalSignatures.Count}");
Console.WriteLine($" - Barcode signatures count : {documentInfo.BarcodeSignatures.Count}");
Console.WriteLine($" - QrCode signatures count : {documentInfo.QrCodeSignatures.Count}");
Console.WriteLine($" - FormField signatures count : {documentInfo.FormFieldSignatures.Count}");
foreach (PageInfo pageInfo in documentInfo.Pages)
{
   Console.WriteLine($" - page-{pageInfo.PageNumber} Width {pageInfo.Width}, Height {pageInfo.Height}");
}
```


## निष्कर्ष
.NET के लिए GroupDocs.Signature, .NET ढांचे के भीतर दस्तावेज़ हस्ताक्षरों को निर्बाध रूप से प्रबंधित करने के लिए उपकरणों का एक शक्तिशाली सूट प्रदान करता है। इस गाइड में उल्लिखित चरणों का पालन करके, आप अपने दस्तावेज़ों के बारे में व्यापक जानकारी कुशलतापूर्वक प्राप्त कर सकते हैं, जिससे उन्नत दस्तावेज़ प्रबंधन क्षमताओं को सुविधाजनक बनाया जा सकता है।

## अक्सर पूछे जाने वाले प्रश्न
### क्या .NET के लिए GroupDocs.Signature एकाधिक दस्तावेज़ प्रारूपों को संभाल सकता है?
हां, GroupDocs.Signature दस्तावेज़ प्रारूपों की एक विस्तृत श्रृंखला का समर्थन करता है, जिसमें DOCX, PDF, PNG और JPEG शामिल हैं, लेकिन इन्हीं तक सीमित नहीं हैं।
### क्या .NET के लिए GroupDocs.Signature का कोई परीक्षण संस्करण उपलब्ध है?
 हां, आप यहां से परीक्षण संस्करण तक पहुंच सकते हैं[यहाँ](https://releases.groupdocs.com/).
### क्या .NET के लिए GroupDocs.Signature डिजिटल हस्ताक्षर के लिए समर्थन प्रदान करता है?
बिल्कुल, GroupDocs.Signature डिजिटल हस्ताक्षरों के लिए मजबूत समर्थन प्रदान करता है, दस्तावेज़ की प्रामाणिकता और अखंडता सुनिश्चित करता है।
### मुझे .NET के लिए GroupDocs.Signature के लिए अतिरिक्त दस्तावेज़ और समर्थन कहां मिल सकता है?
 आप विस्तृत दस्तावेज़ का संदर्भ ले सकते हैं[यहाँ](https://tutorials.groupdocs.com/signature/net/) , और सहायता के लिए, GroupDocs फ़ोरम पर जाएँ[यहाँ](https://forum.groupdocs.com/c/signature/13).
### क्या .NET के लिए GroupDocs.Signature के लिए अस्थायी लाइसेंस प्राप्त किया जा सकता है?
 हां, अस्थायी लाइसेंस खरीद के लिए उपलब्ध हैं[यहाँ](https://purchase.groupdocs.com/temporary-license/).