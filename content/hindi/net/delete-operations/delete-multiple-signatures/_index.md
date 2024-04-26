---
title: दस्तावेज़ से एकाधिक हस्ताक्षर हटाएँ
linktitle: दस्तावेज़ से एकाधिक हस्ताक्षर हटाएँ
second_title: GroupDocs.Signature .NET API
description: .NET के लिए GroupDocs.Signature का उपयोग करके दस्तावेज़ों से आसानी से एकाधिक हस्ताक्षर हटाएं। अपने दस्तावेज़ प्रबंधन वर्कफ़्लो को सुव्यवस्थित करें।
type: docs
weight: 15
url: /hi/net/delete-operations/delete-multiple-signatures/
---
## परिचय
डिजिटल दुनिया में, दस्तावेज़ प्रबंधन में अक्सर विभिन्न हस्ताक्षरों को संभालना शामिल होता है। किसी दस्तावेज़ से एकाधिक हस्ताक्षरों को प्रोग्रामेटिक रूप से हटाने से वर्कफ़्लो सुव्यवस्थित हो सकता है और दक्षता बढ़ सकती है। .NET के लिए GroupDocs.Signature के साथ, यह कार्य सहज और सीधा हो जाता है। यह ट्यूटोरियल आपको किसी दस्तावेज़ से चरण दर चरण एकाधिक हस्ताक्षर हटाने की प्रक्रिया में मार्गदर्शन करेगा।
## आवश्यक शर्तें
ट्यूटोरियल में जाने से पहले, सुनिश्चित करें कि आपके पास निम्नलिखित शर्तें हैं:
- C# प्रोग्रामिंग भाषा की बुनियादी समझ।
- .NET लाइब्रेरी के लिए GroupDocs.Signature स्थापित किया गया।
- परीक्षण के लिए अनेक हस्ताक्षरों वाला नमूना दस्तावेज़।

## नामस्थान आयात करें
.NET के लिए GroupDocs.Signature की कार्यक्षमता तक पहुँचने के लिए आवश्यक नामस्थान आयात करके शुरुआत करें:
```csharp
using System;
using System.IO;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## चरण 1: दस्तावेज़ पथ और फ़ाइल नाम परिभाषित करें
एकाधिक हस्ताक्षर वाले दस्तावेज़ का फ़ाइल पथ सेट करें। सुनिश्चित करें कि आपके पास उचित फ़ाइल पथ और फ़ाइल नाम है:
```csharp
string filePath = "sample_multiple_signatures.docx";
string fileName = Path.GetFileName(filePath);
```
## चरण 2: प्रसंस्करण के लिए दस्तावेज़ की प्रतिलिपि बनाएँ
मूल दस्तावेज़ को संशोधित करने से बचने के लिए, प्रसंस्करण के लिए एक प्रति बनाएँ:
```csharp
string outputFilePath = Path.Combine("Your Document Directory", "DeleteMultiple", fileName);
File.Copy(filePath, outputFilePath, true);
```
## चरण 3: हस्ताक्षर वस्तु को आरंभ करें
आउटपुट फ़ाइल पथ का उपयोग करके एक हस्ताक्षर ऑब्जेक्ट को इंस्टेंट करें:
```csharp
using (Signature signature = new Signature(outputFilePath))
{
    // हस्ताक्षर प्रसंस्करण कोड यहां जाता है
}
```
## चरण 4: खोज विकल्प परिभाषित करें
दस्तावेज़ के भीतर हस्ताक्षरों की पहचान करने के लिए विभिन्न खोज विकल्पों को परिभाषित करें। विकल्पों में पाठ खोज, छवि खोज, बारकोड खोज और क्यूआर कोड खोज शामिल हैं:
```csharp
TextSearchOptions textSearchOptions = new TextSearchOptions();
ImageSearchOptions imageSearchOptions = new ImageSearchOptions();
BarcodeSearchOptions barcodeOptions = new BarcodeSearchOptions();
QrCodeSearchOptions qrCodeOptions = new QrCodeSearchOptions();
// सूची में विकल्प जोड़ें
List<SearchOptions> listOptions = new List<SearchOptions>();
listOptions.Add(textSearchOptions);
listOptions.Add(imageSearchOptions);
listOptions.Add(barcodeOptions);
listOptions.Add(qrCodeOptions);
```
## चरण 5: हस्ताक्षर खोजें
परिभाषित खोज विकल्पों के आधार पर दस्तावेज़ के भीतर सभी हस्ताक्षर खोजने के लिए एक खोज अभियान निष्पादित करें:
```csharp
SearchResult result = signature.Search(listOptions);
```
## चरण 6: हस्ताक्षर हटाएँ
यदि हस्ताक्षर पाए जाते हैं, तो उन्हें हटाने के लिए आगे बढ़ें:
```csharp
if (result.Signatures.Count > 0)
{
    // सभी हस्ताक्षर हटाने का प्रयास करें
    DeleteResult deleteResult = signature.Delete(result.Signatures);
    //जाँचें कि क्या विलोपन सफल रहा
    if(deleteResult.Succeeded.Count == result.Signatures.Count)
    {
        Console.WriteLine("\nAll signatures were successfully deleted!");                        
    }
    else
    {
        Console.WriteLine($"Successfully deleted signatures : {deleteResult.Succeeded.Count}");
        Helper.WriteError($"Not deleted signatures : {deleteResult.Failed.Count}");
    }
    // हटाए गए हस्ताक्षरों के बारे में जानकारी प्रदर्शित करें
    Console.WriteLine("\nList of deleted signatures:");
    int number = 1;
    foreach(BaseSignature temp in deleteResult.Succeeded)
    {
        Console.WriteLine($"Signature #{number++}: Type: {temp.SignatureType} Id:{temp.SignatureId}, Location: {temp.Left}x{temp.Top}. Size: {temp.Width}x{temp.Height}");
    }
}
else
{
    Helper.WriteError("No one signature was found.");
}
```

## निष्कर्ष
किसी दस्तावेज़ से एकाधिक हस्ताक्षरों को प्रोग्रामेटिक रूप से हटाना दस्तावेज़ प्रबंधन में एक महत्वपूर्ण कार्य है। .NET के लिए GroupDocs.Signature के साथ, यह प्रक्रिया कुशल और विश्वसनीय हो जाती है। इस ट्यूटोरियल में बताए गए चरणों का पालन करके, आप आसानी से हस्ताक्षर हटाने की कार्यक्षमता को अपने .NET अनुप्रयोगों में एकीकृत कर सकते हैं।
## अक्सर पूछे जाने वाले प्रश्न
### क्या .NET के लिए GroupDocs.Signature विभिन्न दस्तावेज़ प्रारूपों को संभाल सकता है?
हां, .NET के लिए GroupDocs.Signature DOCX, PDF, PPTX, XLSX और अन्य सहित दस्तावेज़ प्रारूपों की एक विस्तृत श्रृंखला का समर्थन करता है।
### क्या हस्ताक्षर पहचान के लिए खोज विकल्पों को अनुकूलित करना संभव है?
बिल्कुल, आप अपनी विशिष्ट आवश्यकताओं को पूरा करने के लिए टेक्स्ट खोज, छवि खोज, बारकोड खोज और क्यूआर कोड खोज जैसे खोज विकल्पों को अनुकूलित कर सकते हैं।
### क्या .NET के लिए GroupDocs.Signature त्रुटि प्रबंधन तंत्र प्रदान करता है?
हां, दस्तावेज़ प्रसंस्करण कार्यों के सुचारू निष्पादन को सुनिश्चित करने के लिए लाइब्रेरी मजबूत त्रुटि प्रबंधन क्षमताएं प्रदान करती है।
### क्या मैं .NET के लिए GroupDocs.Signature को अन्य तृतीय-पक्ष लाइब्रेरीज़ के साथ एकीकृत कर सकता हूँ?
निश्चित रूप से, .NET के लिए GroupDocs.Signature को लचीलापन और विस्तारशीलता प्रदान करते हुए अन्य .NET पुस्तकालयों के साथ सहजता से एकीकृत करने के लिए डिज़ाइन किया गया है।
### मुझे .NET के लिए GroupDocs.Signature के लिए अतिरिक्त समर्थन और संसाधन कहां मिल सकते हैं?
 आप GroupDocs पर जा सकते हैं[मंच](https://forum.groupdocs.com/c/signature/13) हस्ताक्षर-संबंधी चर्चाओं के लिए समर्पित और समुदाय और विशेषज्ञों से सहायता चाहते हैं।