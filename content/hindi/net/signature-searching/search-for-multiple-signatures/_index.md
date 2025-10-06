---
"description": ".NET के लिए GroupDocs.Signature का उपयोग करके दस्तावेज़ों में एकाधिक हस्ताक्षर प्रकारों की खोज करना सीखें। बेहतर दस्तावेज़ सुरक्षा के लिए कोड उदाहरणों सहित व्यापक मार्गदर्शिका।"
"linktitle": "एकाधिक हस्ताक्षरों की खोज करें"
"second_title": "GroupDocs.Signature .NET एपीआई"
"title": "दस्तावेज़ों में एकाधिक हस्ताक्षर प्रकारों की खोज करें"
"url": "/hi/net/signature-searching/search-for-multiple-signatures/"
"weight": 14
type: docs
---
## परिचय

आधुनिक दस्तावेज़ प्रबंधन प्रणालियों में, एक ही दस्तावेज़ में कई प्रकार के हस्ताक्षरों को खोजने और सत्यापित करने की क्षमता का महत्व लगातार बढ़ता जा रहा है। दस्तावेज़ सुरक्षा बढ़ाने और सत्यापन प्रक्रियाओं को सरल बनाने के लिए संगठन अक्सर विभिन्न प्रकार के हस्ताक्षरों—जैसे डिजिटल हस्ताक्षर, टेक्स्ट हस्ताक्षर, बारकोड, क्यूआर कोड, आदि—का उपयोग करते हैं। .NET के लिए GroupDocs.Signature एक शक्तिशाली ढाँचा प्रदान करता है जो डेवलपर्स को विभिन्न दस्तावेज़ स्वरूपों में व्यापक हस्ताक्षर खोज कार्यक्षमता लागू करने में सक्षम बनाता है।

यह ट्यूटोरियल आपको GroupDocs.Signature for .NET का उपयोग करके दस्तावेज़ों के भीतर कई हस्ताक्षर प्रकारों की खोज करने की प्रक्रिया के माध्यम से मार्गदर्शन करेगा, विस्तृत स्पष्टीकरण और व्यावहारिक कोड उदाहरण प्रदान करेगा।

## आवश्यक शर्तें

एकाधिक हस्ताक्षर खोज कार्यक्षमता को लागू करने से पहले, सुनिश्चित करें कि आपके पास निम्नलिखित पूर्वापेक्षाएँ हैं:

1. विकास वातावरण: आपके सिस्टम पर स्थापित विजुअल स्टूडियो या कोई भी पसंदीदा .NET विकास वातावरण।
  
2. .NET के लिए GroupDocs.Signature: .NET लाइब्रेरी के लिए GroupDocs.Signature डाउनलोड और इंस्टॉल करें [यहाँ](https://releases.groupdocs.com/signature/net/).

3. बुनियादी C# ज्ञान: C# प्रोग्रामिंग भाषा और .NET फ्रेमवर्क अवधारणाओं से परिचित होना।

4. नमूना दस्तावेज: परीक्षण प्रयोजनों के लिए विभिन्न प्रकार के हस्ताक्षरों वाले परीक्षण दस्तावेज तैयार करें।

## नामस्थान आयात करें

GroupDocs.Signature कार्यक्षमता तक पहुँचने के लिए आवश्यक नामस्थानों को आयात करके आरंभ करें:

```csharp
using System;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

अब, आइए एकाधिक हस्ताक्षर प्रकारों की खोज की प्रक्रिया को स्पष्ट, प्रबंधनीय चरणों में विभाजित करें:

## चरण 1: दस्तावेज़ लोड करें

सबसे पहले, उस हस्ताक्षर वाले दस्तावेज़ को लोड करें जिसे आप खोजना चाहते हैं:

```csharp
string filePath = "sample_multiple_signatures.docx";
using (Signature signature = new Signature(filePath))
{
    // बहु-हस्ताक्षर खोज कोड यहां जोड़ा जाएगा
}
```

## चरण 2: विभिन्न हस्ताक्षर प्रकारों के लिए खोज विकल्प परिभाषित करें

प्रत्येक हस्ताक्षर प्रकार के लिए खोज विकल्प बनाएं जिसे आप खोजना चाहते हैं:

```csharp
// पाठ हस्ताक्षरों के लिए खोज विकल्प परिभाषित करें
TextSearchOptions textOptions = new TextSearchOptions
{
    AllPages = true,  // सभी पृष्ठों पर खोजें
    Text = "Signature",  // वैकल्पिक: खोजने के लिए पाठ
    MatchType = TextMatchType.Contains  // मिलान मानदंड
};

// डिजिटल हस्ताक्षरों के लिए खोज विकल्प परिभाषित करें
DigitalSearchOptions digitalOptions = new DigitalSearchOptions
{
    AllPages = true
};

// बारकोड हस्ताक्षरों के लिए खोज विकल्प परिभाषित करें
BarcodeSearchOptions barcodeOptions = new BarcodeSearchOptions
{
    AllPages = true,
    Text = "123456",  // वैकल्पिक: मिलान करने के लिए बारकोड पाठ
    MatchType = TextMatchType.Exact  // मिलान मानदंड
};

// QR कोड हस्ताक्षरों के लिए खोज विकल्प परिभाषित करें
QrCodeSearchOptions qrCodeOptions = new QrCodeSearchOptions
{
    AllPages = true,
    Text = "John",  // वैकल्पिक: मिलान करने के लिए QR कोड टेक्स्ट
    MatchType = TextMatchType.Contains  // मिलान मानदंड
};

// मेटाडेटा हस्ताक्षरों के लिए खोज विकल्प परिभाषित करें
MetadataSearchOptions metadataOptions = new MetadataSearchOptions();
```

## चरण 3: संग्रह में विकल्प जोड़ें

सभी खोज विकल्पों को एक संग्रह में जोड़ें:

```csharp
// सभी खोज विकल्पों को रखने के लिए एक सूची बनाएँ
List<SearchOptions> searchOptions = new List<SearchOptions>
{
    textOptions,
    digitalOptions,
    barcodeOptions,
    qrCodeOptions,
    metadataOptions
};
```

## चरण 4: खोज करें और परिणामों को संसाधित करें

संयुक्त खोज विकल्पों का उपयोग करके खोज निष्पादित करें और परिणामों को संसाधित करें:

```csharp
// निर्धारित विकल्पों का उपयोग करके सभी हस्ताक्षर प्रकारों की खोज करें
SearchResult result = signature.Search(searchOptions);

// जाँच करें कि हस्ताक्षर मिले या नहीं
if (result.Signatures.Count > 0)
{
    Console.WriteLine($"\nSource document ['{filePath}'] contains {result.Signatures.Count} signature(s):");
    
    // पाए गए हस्ताक्षरों के माध्यम से पुनरावृति करें
    foreach (var foundSignature in result.Signatures)
    {
        Console.WriteLine($"Signature found: Type: {foundSignature.SignatureType}, Page: {foundSignature.PageNumber}, ID: {foundSignature.SignatureId}");
        
        // प्रक्रिया विशिष्ट हस्ताक्षर प्रकार
        if (foundSignature is TextSignature textSignature)
        {
            Console.WriteLine($"Text: '{textSignature.Text}'");
        }
        else if (foundSignature is BarcodeSignature barcodeSignature)
        {
            Console.WriteLine($"Barcode Type: {barcodeSignature.EncodeType.TypeName}, Text: '{barcodeSignature.Text}'");
        }
        else if (foundSignature is QrCodeSignature qrCodeSignature)
        {
            Console.WriteLine($"QR Code Type: {qrCodeSignature.EncodeType.TypeName}, Text: '{qrCodeSignature.Text}'");
        }
        else if (foundSignature is DigitalSignature digitalSignature)
        {
            Console.WriteLine($"Certificate: {digitalSignature.Certificate?.SubjectName}, Valid: {digitalSignature.IsValid}");
        }
        else if (foundSignature is MetadataSignature metadataSignature)
        {
            Console.WriteLine($"Metadata: Name: {metadataSignature.Name}, Value: {metadataSignature.Value}");
        }
    }
}
else
{
    Console.WriteLine("No signatures were found in the document.");
}
```

## पूर्ण उदाहरण

यहां एक पूर्ण, कार्यशील उदाहरण दिया गया है जो किसी दस्तावेज़ में एकाधिक हस्ताक्षर प्रकारों की खोज को प्रदर्शित करता है:

```csharp
using System;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;

namespace MultiSignatureSearch
{
    class Program
    {
        static void Main(string[] args)
        {
            // दस्तावेज़ पथ
            string filePath = "sample_multiple_signatures.docx";
            
            // हस्ताक्षर उदाहरण आरंभ करें
            using (Signature signature = new Signature(filePath))
            {
                try
                {
                    // पाठ हस्ताक्षरों के लिए खोज विकल्प परिभाषित करें
                    TextSearchOptions textOptions = new TextSearchOptions
                    {
                        AllPages = true,
                        MatchType = TextMatchType.Contains
                    };

                    // डिजिटल हस्ताक्षरों के लिए खोज विकल्प परिभाषित करें
                    DigitalSearchOptions digitalOptions = new DigitalSearchOptions
                    {
                        AllPages = true
                    };

                    // बारकोड हस्ताक्षरों के लिए खोज विकल्प परिभाषित करें
                    BarcodeSearchOptions barcodeOptions = new BarcodeSearchOptions
                    {
                        AllPages = true
                    };

                    // QR कोड हस्ताक्षरों के लिए खोज विकल्प परिभाषित करें
                    QrCodeSearchOptions qrCodeOptions = new QrCodeSearchOptions
                    {
                        AllPages = true
                    };

                    // मेटाडेटा हस्ताक्षरों के लिए खोज विकल्प परिभाषित करें
                    MetadataSearchOptions metadataOptions = new MetadataSearchOptions();

                    // सभी खोज विकल्पों को रखने के लिए एक सूची बनाएँ
                    List<SearchOptions> searchOptions = new List<SearchOptions>
                    {
                        textOptions,
                        digitalOptions,
                        barcodeOptions,
                        qrCodeOptions,
                        metadataOptions
                    };

                    // सभी प्रकार के हस्ताक्षर खोजें
                    SearchResult result = signature.Search(searchOptions);

                    // जाँच करें कि हस्ताक्षर मिले या नहीं
                    if (result.Signatures.Count > 0)
                    {
                        Console.WriteLine($"\nSource document ['{filePath}'] contains {result.Signatures.Count} signature(s):");
                        
                        // हस्ताक्षर प्रकार के अनुसार प्रक्रिया परिणाम
                        foreach (var foundSignature in result.Signatures)
                        {
                            Console.WriteLine($"Signature found: Type: {foundSignature.SignatureType}, Page: {foundSignature.PageNumber}");
                            
                            // प्रक्रिया विशिष्ट हस्ताक्षर प्रकार
                            switch (foundSignature.SignatureType)
                            {
                                case SignatureType.Text:
                                    var textSignature = foundSignature as TextSignature;
                                    Console.WriteLine($"Text: '{textSignature.Text}'");
                                    break;
                                    
                                case SignatureType.Barcode:
                                    var barcodeSignature = foundSignature as BarcodeSignature;
                                    Console.WriteLine($"Barcode Type: {barcodeSignature.EncodeType.TypeName}, Text: '{barcodeSignature.Text}'");
                                    break;
                                    
                                case SignatureType.QrCode:
                                    var qrCodeSignature = foundSignature as QrCodeSignature;
                                    Console.WriteLine($"QR Code Type: {qrCodeSignature.EncodeType.TypeName}, Text: '{qrCodeSignature.Text}'");
                                    break;
                                    
                                case SignatureType.Digital:
                                    var digitalSignature = foundSignature as DigitalSignature;
                                    Console.WriteLine($"Certificate: {digitalSignature.Certificate?.SubjectName}, Valid: {digitalSignature.IsValid}");
                                    break;
                                    
                                case SignatureType.Metadata:
                                    var metadataSignature = foundSignature as MetadataSignature;
                                    Console.WriteLine($"Metadata: Name: {metadataSignature.Name}, Value: {metadataSignature.Value}");
                                    break;
                            }
                            
                            Console.WriteLine(); // हस्ताक्षरों के बीच लाइन ब्रेक जोड़ें
                        }
                    }
                    else
                    {
                        Console.WriteLine("No signatures were found in the document.");
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

## उन्नत बहु-हस्ताक्षर खोज तकनीकें

### खोज परिणामों को फ़िल्टर करना

आप खोज परिणामों को सीमित करने के लिए उन्नत फ़िल्टरिंग लागू कर सकते हैं:

```csharp
// पृष्ठ संख्या के अनुसार परिणाम फ़िल्टर करें
var signaturesOnFirstPage = result.Signatures.FindAll(s => s.PageNumber == 1);

// हस्ताक्षर प्रकार के अनुसार परिणाम फ़िल्टर करें
var digitalSignatures = result.Signatures.FindAll(s => s.SignatureType == SignatureType.Digital);
var qrCodeSignatures = result.Signatures.FindAll(s => s.SignatureType == SignatureType.QrCode);

// विशिष्ट सामग्री वाले टेक्स्ट हस्ताक्षरों को फ़िल्टर करें
var approvalSignatures = result.Signatures
    .FindAll(s => s is TextSignature && ((TextSignature)s).Text.Contains("Approved"));
```

### एकाधिक हस्ताक्षरों का सत्यापन

विभिन्न हस्ताक्षर प्रकारों के लिए सत्यापन तर्क लागू करें:

```csharp
bool ValidateAllSignatures(SearchResult result)
{
    bool isDocumentValid = true;
    
    // जाँच करें कि दस्तावेज़ में वैध डिजिटल हस्ताक्षर है या नहीं
    bool hasValidDigitalSignature = result.Signatures
        .Any(s => s is DigitalSignature && ((DigitalSignature)s).IsValid);
    
    if (!hasValidDigitalSignature)
    {
        Console.WriteLine("Warning: Document does not contain a valid digital signature");
        isDocumentValid = false;
    }
    
    // जांचें कि दस्तावेज़ में आवश्यक QR कोड है या नहीं
    bool hasRequiredQRCode = result.Signatures
        .Any(s => s is QrCodeSignature && ((QrCodeSignature)s).Text.Contains("Auth-Code"));
    
    if (!hasRequiredQRCode)
    {
        Console.WriteLine("Warning: Document does not contain the required authentication QR code");
        isDocumentValid = false;
    }
    
    return isDocumentValid;
}
```

### कस्टम प्रोसेसिंग के साथ खोज

आप खोज कार्यों के लिए कस्टम प्रसंस्करण तर्क परिभाषित कर सकते हैं:

```csharp
// कस्टम प्रोसेसिंग के साथ खोज विकल्प बनाएँ
TextSearchOptions textOptions = new TextSearchOptions
{
    AllPages = true,
    
    // प्रतिनिधि का उपयोग करके कस्टम प्रसंस्करण परिभाषित करें
    ProcessCompleted = (signature) =>
    {
        // कस्टम सत्यापन तर्क - केवल निर्दिष्ट पृष्ठों पर हस्ताक्षर स्वीकार करें
        TextSignature textSignature = signature as TextSignature;
        return textSignature != null && (textSignature.PageNumber == 1 || textSignature.PageNumber == 2);
    }
};
```

## निष्कर्ष

इस विस्तृत मार्गदर्शिका में, हमने .NET के लिए GroupDocs.Signature का उपयोग करके दस्तावेज़ों में एकाधिक हस्ताक्षर प्रकारों की खोज करने का तरीका बताया है। विभिन्न हस्ताक्षर प्रकारों के लिए खोज विकल्प सेट अप करने से लेकर परिणामों को संसाधित और सत्यापित करने तक, अब आपके पास अपने .NET अनुप्रयोगों में मज़बूत हस्ताक्षर खोज कार्यक्षमता लागू करने का ज्ञान है।

एक साथ कई हस्ताक्षर प्रकारों की खोज करने की क्षमता दस्तावेज़ सत्यापन प्रक्रियाओं को बेहतर बनाती है, सुरक्षा उपायों को मज़बूत करती है, और दस्तावेज़ सत्यापन कार्यप्रवाह को सुव्यवस्थित बनाती है। GroupDocs.Signature विभिन्न दस्तावेज़ स्वरूपों में विभिन्न हस्ताक्षर प्रकारों के साथ काम करने के लिए एक शक्तिशाली, लचीला ढाँचा प्रदान करता है, जो इसे दस्तावेज़ प्रसंस्करण अनुप्रयोगों के लिए एक उत्कृष्ट विकल्प बनाता है।

## अक्सर पूछे जाने वाले प्रश्न

### क्या मैं पासवर्ड-संरक्षित दस्तावेज़ों में हस्ताक्षर खोज सकता हूँ?

हाँ, GroupDocs.Signature पासवर्ड से सुरक्षित दस्तावेज़ों में हस्ताक्षर खोजने का समर्थन करता है। आप इसे प्रारंभ करते समय पासवर्ड प्रदान कर सकते हैं। `Signature` वस्तु:

```csharp
LoadOptions loadOptions = new LoadOptions { Password = "your_password" };
using (Signature signature = new Signature(filePath, loadOptions))
{
    // हस्ताक्षर खोजें
}
```

### हस्ताक्षर खोज के लिए कौन से दस्तावेज़ प्रारूप समर्थित हैं?

GroupDocs.Signature दस्तावेज़ स्वरूपों की एक विस्तृत श्रृंखला का समर्थन करता है, जिसमें PDF, Microsoft Office दस्तावेज़ (Word, Excel, PowerPoint), OpenOffice स्वरूप, चित्र आदि शामिल हैं।

### क्या मैं खोज को दस्तावेज़ के विशिष्ट पृष्ठों तक सीमित कर सकता हूँ?

हां, प्रत्येक खोज विकल्प प्रकार में ऐसे गुण होते हैं जो आपको यह निर्दिष्ट करने की अनुमति देते हैं कि किन पृष्ठों पर खोज करनी है:

```csharp
TextSearchOptions options = new TextSearchOptions
{
    AllPages = false,  // सभी पृष्ठों को न खोजें
    PageNumber = 1,    // केवल पृष्ठ 1 पर खोजें
    
    // या एकाधिक पृष्ठ निर्दिष्ट करें
    PagesSetup = new PagesSetup { Pages = new List<int> { 1, 3, 5 } }
};
```

### बड़े दस्तावेज़ों में खोज करते समय मैं प्रदर्शन को कैसे अनुकूलित कर सकता हूँ?

बड़े दस्तावेज़ों के लिए, आप निम्न प्रकार से प्रदर्शन को अनुकूलित कर सकते हैं:

1. खोज को विशिष्ट पृष्ठों या पृष्ठ श्रेणियों तक सीमित करना
2. संभावित मिलानों की संख्या कम करने के लिए अधिक विशिष्ट खोज मानदंडों का उपयोग करना
3. अपने परिणाम प्रदर्शन में पृष्ठांकन लागू करना
4. यदि आप एक साथ परिणाम नहीं चाहते हैं तो एक समय में एक हस्ताक्षर प्रकार की खोज करें

### क्या मैं कस्टम हस्ताक्षर प्रकारों का समर्थन करने के लिए GroupDocs.Signature का विस्तार कर सकता हूँ?

यद्यपि GroupDocs.Signature सामान्य हस्ताक्षर प्रकारों के लिए अंतर्निहित समर्थन प्रदान करता है, आप इसकी कार्यक्षमता को निम्न प्रकार से बढ़ा सकते हैं:

1. से व्युत्पन्न कस्टम खोज विकल्प वर्ग बनाना `SearchOptions`
2. का उपयोग करके कस्टम प्रसंस्करण तर्क को कार्यान्वित करना `ProcessCompleted` प्रतिनिधि
3. ऐसे रैपर क्लासेस का विकास करना जो उन्नत व्यावसायिक तर्क के साथ एकाधिक हस्ताक्षर खोजों को संयोजित करते हैं

## यह भी देखें

* [एपीआई संदर्भ](https://reference.groupdocs.com/signature/net/)
* [GitHub पर कोड उदाहरण](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
* [उत्पाद दस्तावेज़ीकरण](https://docs.groupdocs.com/signature/net/)
* [उत्पाद पृष्ठ](https://products.groupdocs.com/signature/net/)
* [नवीनतम संस्करण डाउनलोड करें](https://releases.groupdocs.com/signature/net/)
* [ब्लॉग लेख](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
* [निःशुल्क सहायता मंच](https://forum.groupdocs.com/c/signature/13)
* [अस्थायी लाइसेंस](https://purchase.groupdocs.com/temporary-license/)