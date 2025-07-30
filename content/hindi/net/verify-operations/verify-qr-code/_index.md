---
"description": ".NET के लिए GroupDocs.Signature का उपयोग करके दस्तावेज़ों में QR कोड सत्यापित करना सीखें। दस्तावेज़ प्रमाणीकरण के लिए कोड उदाहरणों और सर्वोत्तम प्रथाओं के साथ एक संपूर्ण मार्गदर्शिका।"
"linktitle": "QR कोड सत्यापित करें"
"second_title": "GroupDocs.Signature .NET एपीआई"
"title": "दस्तावेज़ों में QR कोड सत्यापित करें"
"url": "/hi/net/verify-operations/verify-qr-code/"
"weight": 12
---

## परिचय

दस्तावेज़ सुरक्षा आधुनिक व्यावसायिक कार्यों का एक महत्वपूर्ण पहलू है। क्यूआर कोड, दस्तावेज़ों में जानकारी एम्बेड करने का एक तेज़ी से लोकप्रिय तरीका बन गया है जिसकी प्रामाणिकता की पुष्टि की जा सकती है। GroupDocs.Signature for .NET विभिन्न फ़ॉर्मैट में दस्तावेज़ों में एम्बेड किए गए क्यूआर कोड की पुष्टि के लिए एक शक्तिशाली और लचीला समाधान प्रदान करता है।

यह व्यापक ट्यूटोरियल आपको अपने .NET अनुप्रयोगों में QR कोड सत्यापन को लागू करने की प्रक्रिया के माध्यम से मार्गदर्शन करेगा, यह सुनिश्चित करते हुए कि आपके दस्तावेज़ अपनी अखंडता और प्रामाणिकता बनाए रखें।

## आवश्यक शर्तें

QR कोड सत्यापन कार्यक्षमता को लागू करने से पहले, सुनिश्चित करें कि आपके पास निम्नलिखित पूर्वापेक्षाएँ हैं:

1. .NET के लिए GroupDocs.Signature: लाइब्रेरी को डाउनलोड करें और इंस्टॉल करें [डाउनलोड पृष्ठ](https://releases.groupdocs.com/signature/net/).
2. विकास वातावरण: विजुअल स्टूडियो या कोई भी संगत .NET विकास वातावरण।
3. परीक्षण दस्तावेज़: सत्यापन प्रयोजनों के लिए QR कोड हस्ताक्षर युक्त दस्तावेज़।
4. बुनियादी ज्ञान: C# प्रोग्रामिंग और .NET फ्रेमवर्क अवधारणाओं से परिचित होना।

## नामस्थान आयात करें

GroupDocs.Signature कार्यक्षमता तक पहुँचने के लिए आवश्यक नामस्थानों को आयात करके प्रारंभ करें:

```csharp
using System;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

## चरण-दर-चरण QR कोड सत्यापन प्रक्रिया

अपने दस्तावेज़ों में QR कोड सत्यापित करने के लिए इन विस्तृत चरणों का पालन करें:

### चरण 1: दस्तावेज़ पथ निर्दिष्ट करें

```csharp
// QR कोड हस्ताक्षर वाले दस्तावेज़ का पथ प्रदान करें
string filePath = "sample_multiple_signatures.docx";
```

सुनिश्चित करें कि आप उदाहरण पथ को अपने दस्तावेज़ के वास्तविक पथ से प्रतिस्थापित करें।

### चरण 2: हस्ताक्षर ऑब्जेक्ट को आरंभ करें

```csharp
// दस्तावेज़ पथ पास करके एक हस्ताक्षर उदाहरण बनाएँ
using (Signature signature = new Signature(filePath))
{
    // सत्यापन कोड यहां लागू किया जाएगा
}
```

हस्ताक्षर वर्ग GroupDocs.Signature API में सभी कार्यों के लिए मुख्य प्रवेश बिंदु है।

### चरण 3: QR कोड सत्यापन विकल्प कॉन्फ़िगर करें

```csharp
// QR कोड सत्यापन विकल्प परिभाषित करें
QrCodeVerifyOptions options = new QrCodeVerifyOptions()
{
    AllPages = true, // दस्तावेज़ के सभी पृष्ठों की जाँच करें
    Text = "John",   // QR कोड के भीतर सत्यापन हेतु पाठ
    MatchType = TextMatchType.Contains // पाठ मिलान मानदंड निर्दिष्ट करें
};
```

सत्यापन विकल्प आपको सत्यापन प्रक्रिया के लिए विशिष्ट मानदंड निर्धारित करने की अनुमति देते हैं:
- `AllPages`: सभी दस्तावेज़ पृष्ठों की जाँच करने के लिए सत्य पर सेट करें (डिफ़ॉल्ट व्यवहार)
- `Text`: QR कोड के भीतर मिलान करने के लिए पाठ सामग्री
- `MatchType`: पाठ मिलान की विधि (Contains, Exact, StartsWith, आदि)

### चरण 4: सत्यापन प्रक्रिया निष्पादित करें

```csharp
// सत्यापन करें
VerificationResult result = signature.Verify(options);
```

यह आपके द्वारा निर्दिष्ट विकल्पों के आधार पर सत्यापन प्रक्रिया निष्पादित करता है।

### चरण 5: सत्यापन परिणामों की प्रक्रिया

```csharp
// सत्यापन परिणाम की जाँच करें और तदनुसार प्रक्रिया करें
if (result.IsValid)
{
    Console.WriteLine($"Document {filePath} contains valid QR code signature!");
    
    // सफल हस्ताक्षरों के बारे में जानकारी प्रदर्शित करें
    foreach (QrCodeSignature signature in result.Succeeded)
    {
        Console.WriteLine($"Found valid QR Code signature with text: {signature.Text}");
        Console.WriteLine($"QR Code type: {signature.EncodeType.TypeName}");
        Console.WriteLine($"Location: Page {signature.PageNumber}, {signature.Left}x{signature.Top}");
    }
}
else
{
    Console.WriteLine($"Document {filePath} failed verification process.");
    Console.WriteLine($"Number of failed signatures: {result.Failed.Count}");
}
```

सत्यापन परिणाम को उचित ढंग से संभालने से आपके एप्लिकेशन को सत्यापन परिणाम के आधार पर उचित कार्रवाई करने की अनुमति मिलती है।

## पूर्ण उदाहरण

यहां एक पूर्ण, कार्यशील उदाहरण दिया गया है जो QR कोड सत्यापन को प्रदर्शित करता है:

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
            
            // हस्ताक्षर उदाहरण आरंभ करें
            using (Signature signature = new Signature(filePath))
            {
                // सत्यापन विकल्प सेटअप करें
                QrCodeVerifyOptions options = new QrCodeVerifyOptions()
                {
                    AllPages = true,
                    Text = "John",
                    MatchType = TextMatchType.Contains
                };
                
                // दस्तावेज़ हस्ताक्षर सत्यापित करें
                VerificationResult result = signature.Verify(options);
                
                // प्रक्रिया सत्यापन परिणाम
                if (result.IsValid)
                {
                    Console.WriteLine($"Document {filePath} contains valid QR code signature!");
                    
                    foreach (QrCodeSignature qrSignature in result.Succeeded)
                    {
                        Console.WriteLine($"Found valid QR Code with text: {qrSignature.Text}");
                    }
                }
                else
                {
                    Console.WriteLine($"Document {filePath} failed verification process.");
                }
            }
        }
    }
}
```

## उन्नत सत्यापन विकल्प

GroupDocs.Signature अधिक जटिल सत्यापन परिदृश्यों के लिए अतिरिक्त विकल्प प्रदान करता है:

### विशिष्ट QR कोड प्रकारों का सत्यापन

```csharp
QrCodeVerifyOptions options = new QrCodeVerifyOptions()
{
    EncodeType = QrCodeTypes.QR,  // केवल मानक QR कोड सत्यापित करें
    Text = "Confidential",
    MatchType = TextMatchType.Exact
};
```

### विशिष्ट पृष्ठों पर सत्यापन

```csharp
QrCodeVerifyOptions options = new QrCodeVerifyOptions()
{
    AllPages = false,
    PageNumber = 2,  // केवल पृष्ठ 2 पर सत्यापित करें
    Text = "Approved"
};
```

### सत्यापन के लिए नियमित अभिव्यक्तियों का उपयोग करना

```csharp
QrCodeVerifyOptions options = new QrCodeVerifyOptions()
{
    Text = "INV-\\d{6}",  // इनवॉइस नंबरों का मिलान करें (उदाहरण के लिए, INV-123456)
    MatchType = TextMatchType.Regex
};
```

## QR कोड सत्यापन के लिए सर्वोत्तम अभ्यास

1. इनपुट को हमेशा मान्य करें: प्रसंस्करण से पहले सुनिश्चित करें कि दस्तावेज़ पथ और सत्यापन मानदंड मान्य हैं।
2. त्रुटि प्रबंधन लागू करें: सत्यापन के दौरान संभावित अपवादों को संभालने के लिए try-catch ब्लॉक का उपयोग करें।
3. प्रदर्शन पर विचार करें: बड़े दस्तावेज़ों के लिए, संपूर्ण दस्तावेज़ के बजाय विशिष्ट पृष्ठों को सत्यापित करने पर विचार करें।
4. लॉग सत्यापन परिणाम: ऑडिट उद्देश्यों के लिए सत्यापन प्रक्रियाओं के लॉग बनाए रखें।
5. विभिन्न दस्तावेज़ प्रारूपों के साथ परीक्षण करें: सुनिश्चित करें कि आपका सत्यापन सभी आवश्यक दस्तावेज़ प्रारूपों में काम करता है।

## निष्कर्ष

दस्तावेज़ों में QR कोड का सत्यापन, दस्तावेज़ की प्रामाणिकता और अखंडता सुनिश्चित करने का एक अनिवार्य पहलू है। GroupDocs.Signature for .NET आपके .NET अनुप्रयोगों में QR कोड सत्यापन लागू करने के लिए एक व्यापक और उपयोगकर्ता-अनुकूल API प्रदान करता है।

इस ट्यूटोरियल का अनुसरण करके, आपने सीखा है कि कैसे:
- सत्यापन प्रक्रिया को कॉन्फ़िगर और आरंभ करें
- विभिन्न सत्यापन मानदंड निर्दिष्ट करें
- सत्यापन परिणामों को संसाधित करना और उनकी व्याख्या करना
- उन्नत सत्यापन विकल्प लागू करें

यह ज्ञान आपको अपने दस्तावेज़ प्रबंधन प्रणालियों की सुरक्षा और विश्वसनीयता बढ़ाने में सक्षम बनाता है।

## अक्सर पूछे जाने वाले प्रश्न

### क्या GroupDocs.Signature एक ही दस्तावेज़ में एकाधिक QR कोड सत्यापित कर सकता है?
हां, GroupDocs.Signature एक ही दस्तावेज़ में कई QR कोड सत्यापित कर सकता है। सत्यापन परिणामों में सभी मिलान वाले QR कोड शामिल होंगे।

### QR कोड सत्यापन के लिए कौन से दस्तावेज़ प्रारूप समर्थित हैं?
GroupDocs.Signature पीडीएफ, वर्ड (DOC, DOCX), एक्सेल (XLS, XLSX), पावरपॉइंट (PPT, PPTX), चित्र, आदि सहित दस्तावेज़ प्रारूपों की एक विस्तृत श्रृंखला का समर्थन करता है।

### क्या मैं विशिष्ट एन्क्रिप्शन या फ़ॉर्मेटिंग के साथ QR कोड सत्यापित कर सकता हूँ?
हां, GroupDocs.Signature विशिष्ट एन्कोडिंग प्रकारों और सामग्री स्वरूपण पैटर्न के साथ QR कोड को सत्यापित करने के विकल्प प्रदान करता है।

### क्या तृतीय-पक्ष अनुप्रयोगों द्वारा बनाए गए QR कोड को सत्यापित करना संभव है?
हां, GroupDocs.Signature अधिकांश अनुप्रयोगों द्वारा उत्पन्न मानक QR कोड को सत्यापित कर सकता है, जब तक वे मानक QR कोड प्रारूपों का पालन करते हैं।

### मैं ऐसे QR कोड को कैसे संभालूँ जिसमें टेक्स्ट के बजाय बाइनरी डेटा हो?
GroupDocs.Signature बाइनरी डेटा के माध्यम से QR कोड को सत्यापित करने के विकल्प प्रदान करता है `BinaryData` सत्यापन विकल्पों की संपत्ति.

### संबंधित संसाधन
* [GroupDocs.Signature API संदर्भ](https://reference.groupdocs.com/signature/net/)
* [GroupDocs.Signature डाउनलोड](https://releases.groupdocs.com/signature/net/)
* [GitHub पर कोड उदाहरण](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
* [प्रलेखन](https://docs.groupdocs.com/signature/net/)
* [उत्पाद पृष्ठ](https://products.groupdocs.com/signature/net/)
* [ब्लॉग लेख](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
* [सहयता मंच](https://forum.groupdocs.com/c/signature/13)
* [अस्थायी लाइसेंस](https://purchase.groupdocs.com/temporary-license/)