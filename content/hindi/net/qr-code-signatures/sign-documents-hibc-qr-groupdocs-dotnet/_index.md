---
"date": "2025-05-07"
"description": ".NET के लिए GroupDocs.Signature का उपयोग करके HIBC QR कोड से PDF दस्तावेज़ों पर हस्ताक्षर करना सीखें। यह मार्गदर्शिका LIC और PAS कोड, जिनमें QR कोड, Aztec कोड और DataMatrix शामिल हैं, के बारे में बताती है।"
"title": "GroupDocs का उपयोग करके HIBC QR कोड के साथ दस्तावेज़ों पर हस्ताक्षर कैसे करें. .NET के लिए हस्ताक्षर एक व्यापक गाइड"
"url": "/hi/net/qr-code-signatures/sign-documents-hibc-qr-groupdocs-dotnet/"
"weight": 1
---

# .NET के लिए GroupDocs.Signature का उपयोग करके HIBC QR कोड वाले दस्तावेज़ों पर हस्ताक्षर कैसे करें

## परिचय

आज के तेज़-तर्रार कारोबारी माहौल में, दस्तावेज़ों की प्रामाणिकता और अखंडता सुनिश्चित करना बेहद ज़रूरी है। चाहे आप दवाइयों, स्वास्थ्य सेवा उत्पादों या लॉजिस्टिक्स से जुड़े हों, दस्तावेज़ों पर हस्ताक्षर करने और उन्हें ट्रैक करने का एक सुरक्षित तरीका होने से समय की बचत हो सकती है और गलतियाँ भी कम हो सकती हैं। **.NET के लिए GroupDocs.Signature**, एक शक्तिशाली लाइब्रेरी जो आपके दस्तावेज़ों में HIBC QR कोड के सहज एकीकरण को सक्षम करके दस्तावेज़ प्रबंधन प्रक्रियाओं को सुव्यवस्थित करने के लिए डिज़ाइन की गई है।

इस ट्यूटोरियल में, हम जानेंगे कि आप .NET के लिए GroupDocs.Signature का उपयोग विभिन्न प्रकार के HIBC QR कोड—LIC (लाइसेंस) और PAS (उत्पाद प्रमाणीकरण प्रणाली)—जिनमें QR कोड, Aztec कोड और DataMatrix शामिल हैं—के साथ PDF दस्तावेज़ों पर हस्ताक्षर करने के लिए कैसे कर सकते हैं। अंत तक, आपको अपने .NET अनुप्रयोगों में इन समाधानों को लागू करने की अच्छी समझ हो जाएगी।

**आप क्या सीखेंगे:**
- .NET के लिए GroupDocs.Signature कैसे सेट करें
- HIBC LIC QR कोड, एज़्टेक कोड और डेटामैट्रिक्स का कार्यान्वयन
- HIBC PAS QR कोड, एज़्टेक कोड और डेटामैट्रिक्स जोड़ना
- व्यावहारिक उपयोग के मामले और एकीकरण की संभावनाएं

इन सुविधाओं को लागू करने से पहले आइए हम पूर्वापेक्षाओं पर गौर करें।

## आवश्यक शर्तें

कोडिंग शुरू करने से पहले, सुनिश्चित करें कि आपके पास निम्नलिखित चीजें मौजूद हैं:

- **.NET वातावरण**: सुनिश्चित करें कि आपके सिस्टम पर .NET स्थापित है (अधिमानतः .NET कोर या .NET 5/6+)।
- **.NET के लिए GroupDocs.Signature**यह लाइब्रेरी हमारा प्राथमिक टूल होगा। आप इसे NuGet के ज़रिए इंस्टॉल कर सकते हैं।
- **बुनियादी प्रोग्रामिंग ज्ञान**: C# से परिचित होना तथा .NET में फ़ाइलों को संभालना अनुशंसित है।

### आवश्यक पुस्तकालय

.NET के लिए GroupDocs.Signature का उपयोग करने के लिए, आपको इनमें से किसी एक विधि का उपयोग करके पैकेज जोड़ना होगा:

**.NET सीएलआई**
```bash
dotnet add package GroupDocs.Signature
```

**पैकेज प्रबंधक**
```powershell
Install-Package GroupDocs.Signature
```

**NuGet पैकेज प्रबंधक UI**
"GroupDocs.Signature" खोजें और नवीनतम संस्करण स्थापित करें।

### लाइसेंस अधिग्रहण

परीक्षण के लिए, आप एक निःशुल्क परीक्षण लाइसेंस प्राप्त कर सकते हैं। विस्तारित उपयोग के लिए, सदस्यता खरीदने या अस्थायी लाइसेंस का अनुरोध करने पर विचार करें:

- **मुफ्त परीक्षण**: पहुँच [यहाँ](https://releases.groupdocs.com/signature/net/)
- **अस्थायी लाइसेंस**: अनुरोध करें [इस लिंक](https://purchase.groupdocs.com/temporary-license/)

### पर्यावरण सेटअप

यह सुनिश्चित करके अपना परिवेश सेट करें कि आपका प्रोजेक्ट उपयुक्त .NET संस्करण को लक्षित करता है और उसकी GroupDocs.Signature तक पहुँच है। इसे अपने अनुप्रयोग में दिखाए अनुसार प्रारंभ करें:

```csharp
using GroupDocs.Signature;
```

## .NET के लिए GroupDocs.Signature सेट अप करना

.NET के लिए GroupDocs.Signature का उपयोग शुरू करने के लिए, आपको लाइब्रेरी स्थापित करने और अपने प्रोजेक्ट के भीतर एक बुनियादी सेटअप कॉन्फ़िगर करने की आवश्यकता है।

### इंस्टालेशन

अपने प्रोजेक्ट में GroupDocs.Signature जोड़ने के लिए ऊपर बताए गए तरीकों में से किसी एक का पालन करें। इंस्टॉल हो जाने के बाद, सुनिश्चित करें कि आपका प्रोजेक्ट इसे इस्तेमाल करने के लिए कॉन्फ़िगर किया गया है और इसे अपनी कोड फ़ाइलों में संदर्भित करें।

### लाइसेंस आरंभीकरण

लाइसेंस प्राप्त करने के बाद, इसे निम्न प्रकार से आरंभ करें:

```csharp
SignatureConfig signConfig = new SignatureConfig();
signConfig.LicensePath = "path/to/your/license.lic";
Signature signature = new Signature("Sample.pdf", signConfig);
```

यह सेटअप आपको बिना किसी सीमा के GroupDocs.Signature की सभी सुविधाओं तक पहुंचने की अनुमति देगा।

## कार्यान्वयन मार्गदर्शिका

अब, आइए .NET के लिए GroupDocs.Signature के साथ HIBC QR कोड का उपयोग करके प्रत्येक सुविधा को लागू करने में गोता लगाएँ।

### HIBC LIC QR-कोड के साथ दस्तावेज़ पर हस्ताक्षर करें

#### अवलोकन

HIBC LIC QR कोड से दस्तावेज़ पर हस्ताक्षर करने से लाइसेंसिंग परिदृश्यों में अनुपालन और पता लगाने की क्षमता सुनिश्चित होती है। यह अनुभाग आपको अपने PDF दस्तावेज़ों में QR कोड बनाने और एम्बेड करने के बारे में मार्गदर्शन करेगा।

#### कार्यान्वयन चरण

##### चरण 1: स्रोत और आउटपुट पथ कॉन्फ़िगर करें

परिभाषित करें कि आपका स्रोत दस्तावेज़ कहाँ स्थित है और हस्ताक्षरित आउटपुट कहाँ सहेजा जाना चाहिए:

```csharp
string sourceFilePath = Path.Combine("YOUR_DOCUMENT_DIRECTORY", "Sample.pdf");
string outputPath = Path.Combine("YOUR_OUTPUT_DIRECTORY", "SignWithHIBCLICQR");
string destinFilePath = Path.Combine(outputPath, "SignedDocumentWithHIBCLICQR.pdf");
```

##### चरण 2: QR कोड साइन विकल्प बनाएँ

अपने QR कोड को विशिष्ट टेक्स्ट और सेटिंग्स के साथ कॉन्फ़िगर करें:

```csharp
using (Signature signature = new Signature(sourceFilePath))
{
    var hibcLic_QR_Options = new QrCodeSignOptions("A123PROD30917/75#422011907#GP293", QrCodeTypes.HIBCLICQR)
    {
        Left = 1,
        Top = 1,
        ReturnContent = true,
        ReturnContentType = FileType.PNG
    };

    // इन विकल्पों के साथ दस्तावेज़ पर हस्ताक्षर करें।
    signature.Sign(destinFilePath, hibcLic_QR_Options);
}
```

**स्पष्टीकरण**: 
- `QrCodeSignOptions` QR कोड का स्वरूप और विषय-वस्तु निर्धारित करता है। यहाँ, हम HIBC LIC QR कोड का प्रकार निर्दिष्ट करते हैं और उसे दस्तावेज़ पर रखते हैं।
- `ReturnContent` सत्य पर सेट करने से आप हस्ताक्षरित दस्तावेज़ की रेंडर की गई छवि प्राप्त कर सकते हैं।

#### समस्या निवारण युक्तियों

- सुनिश्चित करें कि दस्तावेज़ पथ सही ढंग से निर्दिष्ट किया गया है.
- सत्यापित करें कि GroupDocs.Signature पूर्ण कार्यक्षमता के लिए उचित रूप से लाइसेंसीकृत है।

### HIBC LIC Aztec कोड के साथ दस्तावेज़ पर हस्ताक्षर करें

#### अवलोकन

एज़्टेक कोड उच्च-घनत्व वाली सूचना संग्रहण के लिए उपयुक्त, एन्कोडिंग का एक अन्य रूप प्रदान करता है। यह अनुभाग GroupDocs.Signature का उपयोग करके आपके दस्तावेज़ों में एज़्टेक कोड एम्बेड करने पर केंद्रित है।

#### कार्यान्वयन चरण

##### चरण 1: पथ कॉन्फ़िगर करें

पिछली सुविधा के समान, अपने फ़ाइल पथ परिभाषित करें:

```csharp
string sourceFilePath = Path.Combine("YOUR_DOCUMENT_DIRECTORY", "Sample.pdf");
string outputPath = Path.Combine("YOUR_OUTPUT_DIRECTORY", "SignWithHIBCLICAztec");
string destinFilePath = Path.Combine(outputPath, "SignedDocumentWithHIBCLICAztec.pdf");
```

##### चरण 2: एज़्टेक कोड विकल्प कॉन्फ़िगर करें

GroupDocs.Signature का उपयोग करके अपना एज़्टेक कोड सेट करें:

```csharp
using (Signature signature = new Signature(sourceFilePath))
{
    var hibcLic_AZ_Options = new QrCodeSignOptions("A123PROD30917/75#422011907#GP293", QrCodeTypes.HIBCLICAztec)
    {
        Left = 1,
        Top = 200,
        ReturnContent = true,
        ReturnContentType = FileType.PNG
    };

    signature.Sign(destinFilePath, hibcLic_AZ_Options);
}
```

**स्पष्टीकरण**: 
- The `QrCodeSignOptions` यहाँ पुनः इसका प्रयोग किया गया है, लेकिन एज़्टेक कोड प्रकार के साथ।
- स्थिति निर्धारण (`Top`, `Left`) और सामग्री पुनर्प्राप्ति सेटिंग्स क्यूआर कोड के समान हैं।

#### समस्या निवारण युक्तियों

- पुष्टि करें कि फ़ाइल पथ सटीक हैं.
- सुनिश्चित करें कि GroupDocs.Signature का संस्करण एज़्टेक कोड प्रकारों का समर्थन करता है।

### HIBC LIC डेटामैट्रिक्स के साथ दस्तावेज़ पर हस्ताक्षर करें

#### अवलोकन

डेटामैट्रिक्स कोड डेटा संग्रहीत करने का एक और मज़बूत तरीका प्रदान करता है। यह खंड दर्शाता है कि डेटामैट्रिक्स को अपने PDF दस्तावेज़ों में कैसे एकीकृत किया जाए।

#### कार्यान्वयन चरण

##### चरण 1: फ़ाइल पथ सेट करें

पहले की तरह, यह निर्धारित करें कि आपकी फ़ाइलें कहाँ स्थित हैं:

```csharp
string sourceFilePath = Path.Combine("YOUR_DOCUMENT_DIRECTORY", "Sample.pdf");
string outputPath = Path.Combine("YOUR_OUTPUT_DIRECTORY", "SignWithHIBCLICDataMatrix");
string destinFilePath = Path.Combine(outputPath, "SignedDocumentWithHIBCLICDataMatrix.pdf");
```

##### चरण 2: डेटामैट्रिक्स साइन विकल्प बनाएँ

डेटामैट्रिक्स कोड कॉन्फ़िगर करें और लागू करें:

```csharp
using (Signature signature = new Signature(sourceFilePath))
{
    var hibcLic_DM_Options = new QrCodeSignOptions("A123PROD30917/75#422011907#GP293", QrCodeTypes.HIBCLICDataMatrix)
    {
        Left = 1,
        Top = 400,
        ReturnContent = true,
        ReturnContentType = FileType.PNG
    };

    signature.Sign(destinFilePath, hibcLic_DM_Options);
}
```

**स्पष्टीकरण**: 
- `QrCodeSignOptions` डेटामैट्रिक्स कोड की उपस्थिति और सामग्री को सेट करने के लिए उपयोग किया जाता है।
- स्थिति निर्धारण (`Top`, `Left`) और पुनर्प्राप्ति सेटिंग्स पिछले कोड के समान पैटर्न का पालन करती हैं।

#### समस्या निवारण युक्तियों

- सुनिश्चित करें कि सभी फ़ाइल पथ सही ढंग से निर्दिष्ट हैं.
- सत्यापित करें कि GroupDocs.Signature आपके संस्करण में डेटामैट्रिक्स कोड प्रकारों का समर्थन करता है।

### HIBC PAS QR-कोड के साथ दस्तावेज़ पर हस्ताक्षर करें

#### अवलोकन

HIBC PAS QR कोड से दस्तावेज़ों पर हस्ताक्षर करने से उत्पाद ट्रैकिंग और ट्रेसेबिलिटी बेहतर होती है। यह अनुभाग आपको GroupDocs.Signature का उपयोग करके PDF में PAS QR कोड एम्बेड करने के तरीके के बारे में बताता है।

#### कार्यान्वयन चरण

##### चरण 1: स्रोत और आउटपुट पथ कॉन्फ़िगर करें

परिभाषित करें कि आपका स्रोत दस्तावेज़ कहाँ स्थित है और हस्ताक्षरित आउटपुट कहाँ सहेजा जाना चाहिए:

```csharp
string sourceFilePath = Path.Combine("YOUR_DOCUMENT_DIRECTORY", "Sample.pdf");
string outputPath = Path.Combine("YOUR_OUTPUT_DIRECTORY", "SignWithHIBCPASQR");
string destinFilePath = Path.Combine(outputPath, "SignedDocumentWithHIBCPASQR.pdf");
```

##### चरण 2: QR कोड साइन विकल्प बनाएँ

अपने PAS QR कोड को विशिष्ट टेक्स्ट और सेटिंग्स के साथ कॉन्फ़िगर करें:

```csharp
using (Signature signature = new Signature(sourceFilePath))
{
    var hibcPas_QR_Options = new QrCodeSignOptions("PAS123456789012", QrCodeTypes.HIBCPASQR)
    {
        Left = 1,
        Top = 500,
        ReturnContent = true,
        ReturnContentType = FileType.PNG
    };

    // इन विकल्पों के साथ दस्तावेज़ पर हस्ताक्षर करें।
    signature.Sign(destinFilePath, hibcPas_QR_Options);
}
```

**स्पष्टीकरण**: 
- `QrCodeSignOptions` HIBC PAS QR कोड प्रकार के लिए कॉन्फ़िगर किया गया है और दस्तावेज़ पर स्थित है।
- `ReturnContent` सत्य पर सेट करने पर हस्ताक्षरित दस्तावेज़ की रेंडर की गई छवि प्राप्त होती है।

#### समस्या निवारण युक्तियों

- सुनिश्चित करें कि सभी पथ सही ढंग से निर्दिष्ट हैं।
- सत्यापित करें कि GroupDocs.Signature आपके संस्करण में PAS QR कोड प्रकारों का समर्थन करता है।

### निष्कर्ष

इस गाइड का पालन करके, आप .NET के लिए GroupDocs.Signature का उपयोग करके HIBC LIC और PAS QR कोड को PDF दस्तावेज़ों में कुशलतापूर्वक एकीकृत कर सकते हैं। यह प्रक्रिया विभिन्न उद्योगों में दस्तावेज़ सुरक्षा, पता लगाने की क्षमता और अनुपालन को बढ़ाती है। अधिक अनुकूलन और उन्नत सुविधाओं के लिए, देखें। [ग्रुपडॉक्स दस्तावेज़ीकरण](https://docs.groupdocs.com/signature/net/).