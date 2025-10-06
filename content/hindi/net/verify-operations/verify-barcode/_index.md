---
"description": "GroupDocs.Signature के साथ .NET अनुप्रयोगों में मज़बूत बारकोड सत्यापन लागू करें। दस्तावेज़ की प्रामाणिकता सुनिश्चित करने के लिए संपूर्ण कोड उदाहरण और सर्वोत्तम अभ्यास।"
"linktitle": "बारकोड सत्यापित करें"
"second_title": "GroupDocs.Signature .NET एपीआई"
"title": "दस्तावेज़ों में बारकोड हस्ताक्षर सत्यापित करें"
"url": "/hi/net/verify-operations/verify-barcode/"
"weight": 10
type: docs
---
## परिचय

बारकोड आधुनिक दस्तावेज़ प्रबंधन प्रणालियों का एक अभिन्न अंग बन गए हैं, जो एन्कोडेड जानकारी तक त्वरित पहुँच प्रदान करते हैं और साथ ही एक सुरक्षा सुविधा के रूप में भी कार्य करते हैं। GroupDocs.Signature for .NET दस्तावेज़ों में बारकोड हस्ताक्षरों की पुष्टि करने और उनकी प्रामाणिकता और अखंडता सुनिश्चित करने के लिए एक शक्तिशाली API प्रदान करता है।

यह विस्तृत ट्यूटोरियल GroupDocs.Signature का उपयोग करके .NET अनुप्रयोगों में बारकोड सत्यापन लागू करने की प्रक्रिया का अन्वेषण करता है। चाहे आप व्यावसायिक दस्तावेज़ों, प्रमाणपत्रों, अनुबंधों, या किसी भी प्रकार के दस्तावेज़ के साथ काम कर रहे हों जो प्रमाणीकरण के लिए बारकोड का उपयोग करते हैं, यह मार्गदर्शिका आपको मज़बूत सत्यापन कार्यक्षमता लागू करने में मदद करेगी।

## आवश्यक शर्तें

बारकोड सत्यापन कार्यक्षमता को लागू करने से पहले, सुनिश्चित करें कि आपके पास निम्नलिखित पूर्वापेक्षाएँ मौजूद हैं:

1. .NET के लिए GroupDocs.Signature: लाइब्रेरी को डाउनलोड करें और इंस्टॉल करें [डाउनलोड पृष्ठ](https://releases.groupdocs.com/signature/net/).
2. .NET विकास वातावरण: विजुअल स्टूडियो या कोई भी संगत .NET विकास वातावरण।
3. बुनियादी ज्ञान: C# प्रोग्रामिंग और .NET फ्रेमवर्क अवधारणाओं से परिचित होना।
4. परीक्षण दस्तावेज़: सत्यापन प्रयोजनों के लिए बारकोड हस्ताक्षर युक्त दस्तावेज़।

## आवश्यक नामस्थान आयात करें

GroupDocs.Signature कार्यक्षमता तक पहुँचने के लिए आवश्यक नामस्थानों को आयात करके प्रारंभ करें:

```csharp
using System;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

आइए बारकोड सत्यापन प्रक्रिया को स्पष्ट, प्रबंधनीय चरणों में विभाजित करें:

## चरण 1: दस्तावेज़ पथ निर्दिष्ट करें

```csharp
// बारकोड हस्ताक्षर वाले दस्तावेज़ का पथ
string filePath = "sample_multiple_signatures.docx";
```

सुनिश्चित करें कि आप उदाहरण पथ को बारकोड हस्ताक्षर वाले अपने दस्तावेज़ के वास्तविक पथ से प्रतिस्थापित करें।

## चरण 2: हस्ताक्षर ऑब्जेक्ट को आरंभ करें

```csharp
// दस्तावेज़ पथ पास करके हस्ताक्षर वर्ग का एक उदाहरण बनाएँ
using (Signature signature = new Signature(filePath))
{
    // सत्यापन कोड यहां लागू किया जाएगा
}
```

हस्ताक्षर वर्ग GroupDocs.Signature API में सभी कार्यों के लिए मुख्य प्रवेश बिंदु है।

## चरण 3: बारकोड सत्यापन विकल्प कॉन्फ़िगर करें

```csharp
// बारकोड सत्यापन विकल्प परिभाषित करें
BarcodeVerifyOptions options = new BarcodeVerifyOptions()
{
    AllPages = true,           // दस्तावेज़ के सभी पृष्ठों की जाँच करें
    Text = "12345",            // बारकोड के भीतर मिलान करने के लिए पाठ
    MatchType = TextMatchType.Contains // पाठ मिलान मानदंड निर्दिष्ट करें
};
```

सत्यापन विकल्प आपको सत्यापन प्रक्रिया के लिए विशिष्ट मानदंड निर्धारित करने की अनुमति देते हैं:
- `AllPages`: सभी दस्तावेज़ पृष्ठों की जाँच करने के लिए true पर सेट करें
- `Text`: बारकोड के भीतर मिलान करने के लिए पाठ सामग्री
- `MatchType`: पाठ मिलान की विधि (इसमें शामिल है, सटीक, आरंभ होता है, इसके साथ समाप्त होता है)

## चरण 4: सत्यापन प्रक्रिया निष्पादित करें

```csharp
// सत्यापन करें
VerificationResult result = signature.Verify(options);
```

यह आपके द्वारा निर्दिष्ट विकल्पों के आधार पर सत्यापन प्रक्रिया निष्पादित करता है।

## चरण 5: सत्यापन परिणामों की प्रक्रिया

```csharp
// सत्यापन परिणाम की जाँच करें और तदनुसार प्रक्रिया करें
if (result.IsValid)
{
    Console.WriteLine($"Document {filePath} contains valid barcode signatures!");
    
    // सफल हस्ताक्षरों के बारे में जानकारी प्रदर्शित करें
    foreach (BarcodeSignature barcodeSignature in result.Succeeded)
    {
        Console.WriteLine($"\nFound valid barcode signature:");
        Console.WriteLine($"Text: {barcodeSignature.Text}");
        Console.WriteLine($"Type: {barcodeSignature.EncodeType.TypeName}");
        Console.WriteLine($"Location: Page {barcodeSignature.PageNumber}, {barcodeSignature.Left}x{barcodeSignature.Top}");
    }
}
else
{
    Console.WriteLine($"Document {filePath} failed verification process.");
    Console.WriteLine($"Number of failed signatures: {result.Failed.Count}");
}
```

यह कोड जांचता है कि सत्यापन सफल रहा या नहीं और सत्यापित किए गए बारकोड हस्ताक्षरों के बारे में विस्तृत जानकारी प्रदान करता है।

## पूर्ण उदाहरण

यहां बारकोड सत्यापन को प्रदर्शित करने वाला एक पूर्ण कार्यशील उदाहरण दिया गया है:

```csharp
using System;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;

namespace GroupDocs.Signature.Examples
{
    class Program
    {
        static void Main(string[] args)
        {
            // दस्तावेज़ पथ
            string filePath = "sample_multiple_signatures.docx";
            
            try
            {
                // हस्ताक्षर उदाहरण आरंभ करें
                using (Signature signature = new Signature(filePath))
                {
                    // सत्यापन विकल्प सेटअप करें
                    BarcodeVerifyOptions options = new BarcodeVerifyOptions()
                    {
                        AllPages = true,
                        Text = "12345",
                        MatchType = TextMatchType.Contains
                    };
                    
                    // दस्तावेज़ हस्ताक्षर सत्यापित करें
                    VerificationResult result = signature.Verify(options);
                    
                    // प्रक्रिया सत्यापन परिणाम
                    if (result.IsValid)
                    {
                        Console.WriteLine($"Document {filePath} contains valid barcode signatures!");
                        
                        foreach (BarcodeSignature item in result.Succeeded)
                        {
                            Console.WriteLine($"\nValid signature found with text: {item.Text}");
                            Console.WriteLine($"Barcode type: {item.EncodeType.TypeName}");
                            Console.WriteLine($"Page: {item.PageNumber}");
                        }
                    }
                    else
                    {
                        Console.WriteLine($"\nDocument {filePath} failed verification process.");
                    }
                }
            }
            catch (Exception ex)
            {
                Console.WriteLine($"Error: {ex.Message}");
            }
        }
    }
}
```

## उन्नत सत्यापन परिदृश्य

GroupDocs.Signature अधिक जटिल सत्यापन परिदृश्यों के लिए अतिरिक्त विकल्प प्रदान करता है:

### विशिष्ट बारकोड प्रकारों का सत्यापन

यदि आप जानते हैं कि आप किस विशिष्ट बारकोड प्रकार की तलाश कर रहे हैं, तो आप सत्यापन को उस प्रकार तक सीमित कर सकते हैं:

```csharp
BarcodeVerifyOptions options = new BarcodeVerifyOptions()
{
    EncodeType = BarcodeTypes.Code128,  // केवल Code128 बारकोड सत्यापित करें
    Text = "PROD-12345",
    MatchType = TextMatchType.Exact
};
```

### विशिष्ट पृष्ठों पर बारकोड सत्यापित करना

बहु-पृष्ठ दस्तावेज़ों के लिए, आप सत्यापन को विशिष्ट पृष्ठों तक सीमित कर सकते हैं:

```csharp
BarcodeVerifyOptions options = new BarcodeVerifyOptions()
{
    AllPages = false,
    PageNumber = 2,  // केवल पृष्ठ 2 पर सत्यापित करें
    Text = "INV-2023"
};
```

### सत्यापन के लिए नियमित अभिव्यक्तियों का उपयोग करना

अधिक लचीले पैटर्न मिलान के लिए, आप नियमित अभिव्यक्तियों का उपयोग कर सकते हैं:

```csharp
BarcodeVerifyOptions options = new BarcodeVerifyOptions()
{
    Text = "INV-\\d{4}-\\d{2}",  // INV-2023-01 जैसे इनवॉइस नंबरों का मिलान करें
    MatchType = TextMatchType.Regex
};
```

### एक साथ कई बारकोड प्रकारों का सत्यापन

आप विभिन्न बारकोड प्रकारों की जांच के लिए कई सत्यापन विकल्प बना सकते हैं:

```csharp
// सत्यापन विकल्पों की सूची बनाएँ
List<VerifyOptions> listOptions = new List<VerifyOptions>();

// QR कोड सत्यापन जोड़ें
listOptions.Add(new BarcodeVerifyOptions()
{
    EncodeType = BarcodeTypes.QR,
    Text = "Security"
});

// Code128 सत्यापन जोड़ें
listOptions.Add(new BarcodeVerifyOptions()
{
    EncodeType = BarcodeTypes.Code128,
    Text = "12345"
});

// कई विकल्पों के साथ सत्यापित करें
VerificationResult result = signature.Verify(listOptions);
```

## बारकोड सत्यापन के लिए सर्वोत्तम अभ्यास

1. त्रुटि प्रबंधन: अप्रत्याशित परिदृश्यों को सुचारू रूप से प्रबंधित करने के लिए हमेशा उचित त्रुटि प्रबंधन को लागू करें।
2. प्रदर्शन अनुकूलन: बड़े दस्तावेज़ों के लिए, संपूर्ण दस्तावेज़ के बजाय विशिष्ट पृष्ठों को सत्यापित करने पर विचार करें।
3. लॉगिंग: ऑडिटिंग उद्देश्यों के लिए सत्यापन प्रयासों और परिणामों को ट्रैक करने के लिए लॉगिंग लागू करें।
4. सुरक्षा संबंधी विचार: सत्यापन मानदंडों को सुरक्षित रूप से संग्रहीत करें, विशेषकर यदि वे आपकी सुरक्षा संरचना का हिस्सा हों।
5. परीक्षण: अनुकूलता सुनिश्चित करने के लिए विभिन्न दस्तावेज़ प्रारूपों और बारकोड प्रकारों के साथ परीक्षण सत्यापन।

## सामान्य समस्याओं का निवारण

### बारकोड नहीं मिला
- सुनिश्चित करें कि दस्तावेज़ में बारकोड स्पष्ट रूप से दिखाई दे रहा है
- जांचें कि क्या बारकोड प्रकार GroupDocs.Signature द्वारा समर्थित है
- सत्यापित करें कि बारकोड विकृत या क्षतिग्रस्त नहीं है

### सत्यापन विफलताएँ
- पुष्टि करें कि सत्यापन मानदंड (पाठ, बारकोड प्रकार) सही हैं
- जांचें कि क्या MatchType आपके उपयोग के लिए उपयुक्त है
- सत्यापित करें कि बारकोड लागू होने के बाद से दस्तावेज़ में कोई बदलाव नहीं किया गया है

### निष्पादन मुद्दे
- उन विशिष्ट पृष्ठों को लक्षित करके सत्यापन को अनुकूलित करें जहाँ बारकोड अपेक्षित हैं
- यदि पहले से ज्ञात हो तो सत्यापन को विशिष्ट बारकोड प्रकारों तक सीमित रखें

## निष्कर्ष

आधुनिक दस्तावेज़ प्रबंधन प्रणालियों में दस्तावेज़ की प्रामाणिकता और अखंडता सुनिश्चित करने के लिए बारकोड सत्यापन एक आवश्यक उपकरण है। GroupDocs.Signature for .NET आपके .NET अनुप्रयोगों में मज़बूत बारकोड सत्यापन कार्यक्षमता को लागू करने के लिए एक व्यापक और उपयोग में आसान API प्रदान करता है।

इस चरण-दर-चरण मार्गदर्शिका का पालन करके, आपने सीखा है कि कैसे:
- सत्यापन प्रक्रिया को कॉन्फ़िगर और आरंभ करें
- विभिन्न सत्यापन मानदंड निर्दिष्ट करें
- सत्यापन परिणामों को संसाधित करना और उनकी व्याख्या करना
- उन्नत सत्यापन परिदृश्यों को लागू करें

ये क्षमताएं आपको सुरक्षित और विश्वसनीय दस्तावेज़ प्रसंस्करण प्रणालियां बनाने की अनुमति देती हैं जो विभिन्न दस्तावेज़ प्रारूपों में बारकोड की प्रामाणिकता को सत्यापित कर सकती हैं।

## पूछे जाने वाले प्रश्न

### बारकोड सत्यापन के लिए कौन से दस्तावेज़ प्रारूप समर्थित हैं?
GroupDocs.Signature पीडीएफ, वर्ड दस्तावेज़ (DOC, DOCX), एक्सेल स्प्रेडशीट (XLS, XLSX), पावरपॉइंट प्रस्तुतियाँ (PPT, PPTX), चित्र, और अधिक सहित दस्तावेज़ स्वरूपों की एक विस्तृत श्रृंखला का समर्थन करता है।

### क्या GroupDocs.Signature एक ही दस्तावेज़ में एकाधिक बारकोड सत्यापित कर सकता है?
हां, GroupDocs.Signature एक ही दस्तावेज़ में कई बारकोड सत्यापित कर सकता है। सत्यापन परिणामों में सभी मिलान वाले बारकोड शामिल होंगे।

### सत्यापन के लिए कौन से बारकोड प्रकार समर्थित हैं?
GroupDocs.Signature कई प्रकार के बारकोड का समर्थन करता है, जिनमें Code39, Code128, EAN13, EAN8, QR Code, DataMatrix, PDF417, और कई अन्य शामिल हैं।

### क्या मैं पासवर्ड-संरक्षित दस्तावेज़ों में बारकोड सत्यापित कर सकता हूँ?
हां, GroupDocs.Signature सत्यापन के लिए संरक्षित दस्तावेज़ों को खोलते समय दस्तावेज़ पासवर्ड निर्दिष्ट करने के विकल्प प्रदान करता है।

### क्या ऐसे बारकोड को सत्यापित करना संभव है जिसमें टेक्स्ट के बजाय बाइनरी डेटा हो?
हां, GroupDocs.Signature बाइनरी डेटा के माध्यम से बारकोड को सत्यापित करने के विकल्प प्रदान करता है `BinaryData` सत्यापन विकल्पों की संपत्ति.

### संबंधित संसाधन
* [GroupDocs.Signature API संदर्भ](https://reference.groupdocs.com/signature/net/)
* [GroupDocs.Signature डाउनलोड](https://releases.groupdocs.com/signature/net/)
* [GitHub पर कोड उदाहरण](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
* [प्रलेखन](https://docs.groupdocs.com/signature/net/)
* [उत्पाद पृष्ठ](https://products.groupdocs.com/signature/net/)
* [ब्लॉग लेख](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
* [सहयता मंच](https://forum.groupdocs.com/c/signature/13)
* [अस्थायी लाइसेंस](https://purchase.groupdocs.com/temporary-license/)