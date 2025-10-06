---
"description": "इस व्यापक चरण-दर-चरण मार्गदर्शिका और कोड उदाहरणों के साथ GroupDocs.Signature for .NET का उपयोग करके दस्तावेज़ों में QR कोड को कुशलतापूर्वक खोजने का तरीका जानें।"
"linktitle": "क्यूआर कोड खोजें"
"second_title": "GroupDocs.Signature .NET एपीआई"
"title": "दस्तावेज़ों में QR कोड हस्ताक्षर खोजें"
"url": "/hi/net/signature-searching/search-for-qr-codes/"
"weight": 15
type: docs
---
## परिचय

आज के डिजिटल दस्तावेज़ पारिस्थितिकी तंत्र में, क्यूआर कोड हस्ताक्षर जानकारी एम्बेड करने, प्रमाणीकरण और दस्तावेज़ सुरक्षा बढ़ाने के लिए एक अमूल्य उपकरण बन गए हैं। GroupDocs.Signature for .NET, डेवलपर्स को विभिन्न दस्तावेज़ स्वरूपों से क्यूआर कोड खोजने और निकालने के लिए एक शक्तिशाली एपीआई प्रदान करता है, जिससे .NET अनुप्रयोगों में उन्नत दस्तावेज़ विश्लेषण और सत्यापन क्षमताएँ सक्षम होती हैं।

यह व्यापक ट्यूटोरियल आपको .NET के लिए GroupDocs.Signature का उपयोग करके QR कोड खोज कार्यक्षमता को लागू करने की प्रक्रिया के माध्यम से मार्गदर्शन करेगा, स्पष्ट स्पष्टीकरण, चरण-दर-चरण निर्देश और व्यावहारिक कोड उदाहरण प्रदान करेगा जिन्हें आप अपने स्वयं के अनुप्रयोगों में एकीकृत कर सकते हैं।

## आवश्यक शर्तें

QR कोड हस्ताक्षर खोज में उतरने से पहले, सुनिश्चित करें कि आपके पास निम्नलिखित पूर्वापेक्षाएँ हैं:

1. .NET SDK के लिए GroupDocs.Signature: SDK को डाउनलोड करें और इंस्टॉल करें [डाउनलोड पृष्ठ](https://releases.groupdocs.com/signature/net/).

2. विकास परिवेश: .NET फ्रेमवर्क या .NET कोर स्थापित करके Visual Studio जैसे .NET विकास परिवेश को सेट करें।

3. बुनियादी ज्ञान: C# प्रोग्रामिंग और .NET विकास अवधारणाओं से परिचित होना।

4. नमूना दस्तावेज़: सत्यापन और परीक्षण के लिए क्यूआर कोड युक्त परीक्षण दस्तावेज़ तैयार करें।

## नामस्थान आयात करें

GroupDocs.Signature कार्यक्षमता तक पहुँचने के लिए आवश्यक नामस्थानों को आयात करके प्रारंभ करें:

```csharp
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
using System;
using System.Collections.Generic;
```

अब, आइए QR कोड खोजने की प्रक्रिया को स्पष्ट, आसान चरणों में विभाजित करें:

## चरण 1: दस्तावेज़ पथ परिभाषित करें

सबसे पहले, उस QR कोड वाले दस्तावेज़ का पथ निर्दिष्ट करें जिसे आप खोजना चाहते हैं:

```csharp
string filePath = "sample_multiple_signatures.docx";
```

## चरण 2: हस्ताक्षर ऑब्जेक्ट को आरंभ करें

इसका एक उदाहरण बनाएँ `Signature` दस्तावेज़ पथ पास करके क्लास:

```csharp
using (Signature signature = new Signature(filePath))
{
    // क्यूआर कोड खोज कोड यहां जोड़ा जाएगा
}
```

## चरण 3: QR कोड हस्ताक्षर खोजें

उपयोग `Search` दस्तावेज़ में क्यूआर कोड खोजने के लिए उपयुक्त हस्ताक्षर प्रकार के साथ विधि:

```csharp
// दस्तावेज़ में QR कोड हस्ताक्षर खोजें
List<QrCodeSignature> signatures = signature.Search<QrCodeSignature>(SignatureType.QrCode);
```

## चरण 4: प्रक्रिया करें और परिणाम प्रदर्शित करें

प्राप्त क्यूआर कोड हस्ताक्षरों को पुनरावृत्त करें और उनके गुणों तक पहुंचें:

```csharp
// पाए गए QR कोड के बारे में जानकारी प्रदर्शित करें
Console.WriteLine($"\nSource document contains {signatures.Count} QR code signature(s):");

foreach (var qrCodeSignature in signatures)
{
    Console.WriteLine($"QR Code found at page {qrCodeSignature.PageNumber} with type {qrCodeSignature.EncodeType.TypeName}");
    Console.WriteLine($"Content: {qrCodeSignature.Text}");
    Console.WriteLine($"Location: X={qrCodeSignature.Left}, Y={qrCodeSignature.Top}, Width={qrCodeSignature.Width}, Height={qrCodeSignature.Height}");
    Console.WriteLine();
}
```

## पूर्ण उदाहरण

यहां एक व्यापक कार्यशील उदाहरण दिया गया है जो किसी दस्तावेज़ में QR कोड खोजने की पूरी प्रक्रिया को प्रदर्शित करता है:

```csharp
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
using System;
using System.Collections.Generic;

namespace QrCodeSignatureSearch
{
    class Program
    {
        static void Main(string[] args)
        {
            // दस्तावेज़ पथ - अपने फ़ाइल पथ के साथ अद्यतन करें
            string filePath = "sample_multiple_signatures.docx";
            
            // हस्ताक्षर उदाहरण आरंभ करें
            using (Signature signature = new Signature(filePath))
            {
                try
                {
                    // दस्तावेज़ में QR कोड हस्ताक्षर खोजें
                    List<QrCodeSignature> signatures = signature.Search<QrCodeSignature>(SignatureType.QrCode);
                    
                    // खोज परिणाम प्रदर्शित करें
                    Console.WriteLine($"\nSource document ['{filePath}'] contains {signatures.Count} QR code signature(s):");
                    
                    foreach (var qrCodeSignature in signatures)
                    {
                        Console.WriteLine($"QR Code found at page {qrCodeSignature.PageNumber} with type {qrCodeSignature.EncodeType.TypeName}");
                        Console.WriteLine($"Content: {qrCodeSignature.Text}");
                        Console.WriteLine($"Location: X={qrCodeSignature.Left}, Y={qrCodeSignature.Top}, Width={qrCodeSignature.Width}, Height={qrCodeSignature.Height}");
                        Console.WriteLine();
                    }
                }
                catch (Exception ex)
                {
                    Console.WriteLine($"Error occurred: {ex.Message}");
                }
            }
            
            Console.WriteLine("Press any key to exit...");
            Console.ReadKey();
        }
    }
}
```

## उन्नत QR कोड खोज तकनीकें

### विशिष्ट मानदंडों के साथ खोज

अधिक लक्षित खोजों के लिए, आप उपयोग कर सकते हैं `QrCodeSearchOptions` अपने खोज मानदंड को अनुकूलित करने के लिए:

```csharp
// विशिष्ट मानदंडों के साथ QR कोड खोज विकल्प बनाएँ
QrCodeSearchOptions options = new QrCodeSearchOptions
{
    // केवल विशिष्ट पृष्ठों पर खोजें
    AllPages = false,
    PageNumber = 1,
    PagesSetup = new PagesSetup { Pages = new List<int> { 1, 3, 5 } },
    
    // QR कोड सामग्री के आधार पर फ़िल्टर करें
    Text = "Invoice",
    MatchType = TextMatchType.Contains,
    
    // विशिष्ट QR कोड प्रकारों के अनुसार फ़िल्टर करें
    EncodeType = QrCodeTypes.QR,
    
    // खोज करने के लिए एक विशिष्ट क्षेत्र निर्धारित करें
    Rectangle = new Rectangle(100, 100, 400, 400)
};

// विशिष्ट विकल्पों के साथ खोजें
List<QrCodeSignature> filteredSignatures = signature.Search<QrCodeSignature>(options);
```

### QR कोड डेटा का प्रसंस्करण

आप अपनी एप्लिकेशन आवश्यकताओं के आधार पर QR कोड डेटा के लिए कस्टम प्रोसेसिंग लागू कर सकते हैं:

```csharp
foreach (var qrCode in signatures)
{
    // सामग्री के आधार पर QR कोड डेटा निकालें और संसाधित करें
    string qrContent = qrCode.Text;
    
    if (qrContent.StartsWith("URL:"))
    {
        // URL डेटा संसाधित करें
        string url = qrContent.Substring(4);
        Console.WriteLine($"Found URL in QR code: {url}");
    }
    else if (qrContent.StartsWith("CONTACT:"))
    {
        // प्रक्रिया संपर्क जानकारी
        string contact = qrContent.Substring(8);
        Console.WriteLine($"Found contact information in QR code: {contact}");
    }
    else if (qrContent.StartsWith("INVOICE:"))
    {
        // प्रक्रिया चालान जानकारी
        string invoiceData = qrContent.Substring(8);
        Console.WriteLine($"Found invoice information in QR code: {invoiceData}");
        
        // इनवॉइस डेटा को पार्स और मान्य करें
        if (ValidateInvoiceData(invoiceData))
        {
            Console.WriteLine("Invoice data is valid!");
        }
        else
        {
            Console.WriteLine("Warning: Invalid invoice data detected!");
        }
    }
}

// उदाहरण सत्यापन विधि
static bool ValidateInvoiceData(string data)
{
    // अपने सत्यापन तर्क को लागू करें
    return !string.IsNullOrEmpty(data) && data.Contains("ID") && data.Contains("Amount");
}
```

### सुरक्षा सत्यापन लागू करना

क्यूआर कोड का इस्तेमाल अक्सर प्रमाणीकरण के लिए किया जाता है। बुनियादी सुरक्षा सत्यापन कैसे लागू करें, यहाँ बताया गया है:

```csharp
// जाँच करें कि दस्तावेज़ में मान्य प्रमाणीकरण QR कोड है या नहीं
bool hasValidAuthQrCode = false;

foreach (var qrCode in signatures)
{
    if (qrCode.Text.StartsWith("AUTH:"))
    {
        string authCode = qrCode.Text.Substring(5);
        
        // प्रमाणीकरण कोड सत्यापित करें (उदाहरण के लिए, किसी डेटाबेस या पूर्वनिर्धारित सूची के विरुद्ध)
        if (VerifyAuthCode(authCode))
        {
            hasValidAuthQrCode = true;
            Console.WriteLine("Document contains valid authentication QR code!");
            break;
        }
    }
}

if (!hasValidAuthQrCode)
{
    Console.WriteLine("Warning: Document does not contain a valid authentication QR code!");
}

// उदाहरण सत्यापन विधि
static bool VerifyAuthCode(string code)
{
    // अपना सत्यापन तर्क लागू करें
    // यह डेटाबेस लुकअप, API कॉल, या पूर्वनिर्धारित मानों के विरुद्ध तुलना हो सकती है
    return code == "A7B82C3D" || code == "X9Y8Z7W6";
}
```

### QR कोड छवियाँ निकालना

आप आगे की प्रक्रिया या प्रदर्शन के लिए दस्तावेज़ों से QR कोड चित्र निकाल सकते हैं:

```csharp
// QR कोड छवियों को डिस्क पर सहेजें
foreach (var qrCode in signatures)
{
    if (qrCode.Content != null)
    {
        // पृष्ठ संख्या और स्थिति के आधार पर एक अद्वितीय फ़ाइल नाम बनाएँ
        string outputPath = $"QrCode_P{qrCode.PageNumber}_X{qrCode.Left}_Y{qrCode.Top}.png";
        
        // छवि डेटा सहेजें
        File.WriteAllBytes(outputPath, qrCode.Content);
        Console.WriteLine($"Saved QR code image to {outputPath}");
    }
}
```

## निष्कर्ष

इस विस्तृत मार्गदर्शिका में, हमने .NET के लिए GroupDocs.Signature का उपयोग करके दस्तावेज़ों में QR कोड हस्ताक्षरों की खोज करने का तरीका बताया है। बुनियादी खोज से लेकर उन्नत तकनीकों तक, अब आपके पास अपने .NET अनुप्रयोगों में मज़बूत QR कोड प्रबंधन लागू करने का ज्ञान है। GroupDocs.Signature API विभिन्न दस्तावेज़ स्वरूपों में QR कोड सहित विभिन्न प्रकार के हस्ताक्षरों के साथ काम करने के लिए एक शक्तिशाली, लचीला ढाँचा प्रदान करता है।

इन क्षमताओं का उपयोग करके, आप दस्तावेज़ सत्यापन प्रक्रियाओं को बढ़ा सकते हैं, प्रमाणीकरण प्रणालियों को लागू कर सकते हैं, और अपने .NET अनुप्रयोगों के भीतर QR कोड में अंतर्निहित मूल्यवान जानकारी निकाल सकते हैं।

## अक्सर पूछे जाने वाले प्रश्न

### GroupDocs.Signature द्वारा कौन से QR कोड प्रारूप समर्थित हैं?

GroupDocs.Signature मानक QR कोड, माइक्रो QR कोड और अन्य सामान्य QR कोड मानकों सहित विभिन्न QR कोड स्वरूपों का समर्थन करता है। विशिष्ट स्वरूप तक पहुँचने के लिए निम्न लिंक का उपयोग करें: `EncodeType` की संपत्ति `QrCodeSignature` वस्तु।

### क्या मैं पासवर्ड-संरक्षित दस्तावेज़ों में QR कोड खोज सकता हूँ?

हां, GroupDocs.Signature आरंभ करते समय पासवर्ड प्रदान करके पासवर्ड-संरक्षित दस्तावेज़ों में QR कोड खोजने का समर्थन करता है `Signature` वस्तु:

```csharp
LoadOptions loadOptions = new LoadOptions { Password = "your_password" };
using (Signature signature = new Signature(filePath, loadOptions))
{
    // क्यूआर कोड खोजें
}
```

### मैं QR कोड को उनकी सामग्री के आधार पर कैसे फ़िल्टर कर सकता हूँ?

आप QR कोड को उनकी सामग्री के आधार पर फ़िल्टर कर सकते हैं `Text` और `MatchType` के गुण `QrCodeSearchOptions`:

```csharp
QrCodeSearchOptions options = new QrCodeSearchOptions
{
    Text = "Invoice",
    MatchType = TextMatchType.Contains // अन्य विकल्प: सटीक, प्रारंभ, अंत
};
```

### क्या GroupDocs.Signature क्षतिग्रस्त या आंशिक रूप से दिखाई देने वाले QR कोड का पता लगा सकता है?

GroupDocs.Signature में आंशिक रूप से दिखाई देने वाले QR कोड का पता लगाने की कुछ क्षमता है, लेकिन गंभीर रूप से क्षतिग्रस्त QR कोड पहचाने नहीं जा सकते। पहचान की सटीकता दस्तावेज़ में QR कोड की गुणवत्ता और दृश्यता पर निर्भर करती है।

### क्यूआर कोड खोज के लिए कौन से दस्तावेज़ प्रारूप समर्थित हैं?

GroupDocs.Signature पीडीएफ, माइक्रोसॉफ्ट ऑफिस दस्तावेज़ (वर्ड, एक्सेल, पावरपॉइंट), छवियों (जेपीईजी, पीएनजी, टीआईएफएफ) और कई अन्य सहित विभिन्न दस्तावेज़ प्रारूपों में क्यूआर कोड खोज का समर्थन करता है।

## यह भी देखें

* [एपीआई संदर्भ](https://reference.groupdocs.com/signature/net/)
* [GitHub पर कोड उदाहरण](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
* [उत्पाद दस्तावेज़ीकरण](https://docs.groupdocs.com/signature/net/)
* [उत्पाद पृष्ठ](https://products.groupdocs.com/signature/net/)
* [नवीनतम संस्करण डाउनलोड करें](https://releases.groupdocs.com/signature/net/)
* [ब्लॉग लेख](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
* [निःशुल्क सहायता मंच](https://forum.groupdocs.com/c/signature/13)
* [अस्थायी लाइसेंस](https://purchase.groupdocs.com/temporary-license/)