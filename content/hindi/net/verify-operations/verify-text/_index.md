---
"description": "GroupDocs.Signature के साथ .NET अनुप्रयोगों में टेक्स्ट हस्ताक्षर सत्यापन में महारत हासिल करें। संपूर्ण कोड उदाहरणों और सर्वोत्तम प्रथाओं के साथ चरण-दर-चरण कार्यान्वयन मार्गदर्शिका।"
"linktitle": "पाठ सत्यापित करें"
"second_title": "GroupDocs.Signature .NET एपीआई"
"title": "दस्तावेज़ों में पाठ हस्ताक्षर सत्यापित करें"
"url": "/hi/net/verify-operations/verify-text/"
"weight": 13
---

## परिचय

टेक्स्ट हस्ताक्षर, डिजिटल या इलेक्ट्रॉनिक हस्ताक्षरों की तुलना में अक्सर सरल होते हुए भी, दस्तावेज़ प्रबंधन और सत्यापन में महत्वपूर्ण भूमिका निभाते हैं। चाहे वॉटरमार्क हों, फ़ुटर टेक्स्ट हों, या विशिष्ट सामग्री पैटर्न हों, टेक्स्ट हस्ताक्षरों की उपस्थिति और अखंडता की पुष्टि करना दस्तावेज़ सत्यापन प्रक्रियाओं का एक महत्वपूर्ण पहलू है।

GroupDocs.Signature for .NET, विभिन्न स्वरूपों में दस्तावेज़ों में टेक्स्ट हस्ताक्षरों के सत्यापन हेतु एक शक्तिशाली API प्रदान करता है। यह व्यापक ट्यूटोरियल आपके .NET अनुप्रयोगों में टेक्स्ट सत्यापन कार्यक्षमता को लागू करने में आपकी सहायता करेगा, जिससे यह सुनिश्चित होगा कि आपके दस्तावेज़ों की अखंडता और प्रामाणिकता बनी रहे।

## आवश्यक शर्तें

पाठ सत्यापन कार्यक्षमता को लागू करने से पहले, सुनिश्चित करें कि आपके पास निम्नलिखित पूर्वापेक्षाएँ मौजूद हैं:

1. .NET के लिए GroupDocs.Signature: लाइब्रेरी को डाउनलोड करें और इंस्टॉल करें [डाउनलोड पृष्ठ](https://releases.groupdocs.com/signature/net/).
2. .NET विकास वातावरण: विजुअल स्टूडियो या कोई भी संगत .NET विकास वातावरण।
3. बुनियादी ज्ञान: C# प्रोग्रामिंग और .NET फ्रेमवर्क अवधारणाओं से परिचित होना।
4. परीक्षण दस्तावेज़: सत्यापन प्रयोजनों के लिए पाठ हस्ताक्षर युक्त दस्तावेज़।

## आवश्यक नामस्थान आयात करें

GroupDocs.Signature कार्यक्षमता तक पहुँचने के लिए आवश्यक नामस्थानों को आयात करके प्रारंभ करें:

```csharp
using System;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

आइए पाठ सत्यापन प्रक्रिया को स्पष्ट, प्रबंधनीय चरणों में विभाजित करें:

## चरण 1: दस्तावेज़ पथ निर्दिष्ट करें

```csharp
// पाठ हस्ताक्षरों वाले दस्तावेज़ का पथ
string filePath = "sample_multiple_signatures.docx";
```

सुनिश्चित करें कि आप उदाहरण पथ को अपने दस्तावेज़ के वास्तविक पथ से प्रतिस्थापित करें जिसमें पाठ हस्ताक्षर शामिल हैं।

## चरण 2: हस्ताक्षर ऑब्जेक्ट को आरंभ करें

```csharp
// दस्तावेज़ पथ पास करके हस्ताक्षर वर्ग का एक उदाहरण बनाएँ
using (Signature signature = new Signature(filePath))
{
    // सत्यापन कोड यहां लागू किया जाएगा
}
```

हस्ताक्षर वर्ग GroupDocs.Signature API में सभी कार्यों के लिए मुख्य प्रवेश बिंदु है।

## चरण 3: पाठ सत्यापन विकल्प कॉन्फ़िगर करें

```csharp
// पाठ सत्यापन विकल्प परिभाषित करें
TextVerifyOptions options = new TextVerifyOptions()
{
    AllPages = true,                               // दस्तावेज़ के सभी पृष्ठों की जाँच करें
    SignatureImplementation = TextSignatureImplementation.Native,
    Text = "signature",                            // सत्यापित किया जाने वाला पाठ
    MatchType = TextMatchType.Contains             // मिलान मानदंड निर्दिष्ट करें
};
```

सत्यापन विकल्प आपको सत्यापन प्रक्रिया के लिए विशिष्ट मानदंड निर्धारित करने की अनुमति देते हैं:
- `AllPages`: सभी दस्तावेज़ पृष्ठों की जाँच करने के लिए true पर सेट करें
- `SignatureImplementation`: निर्दिष्ट करें कि पाठ कैसे क्रियान्वित किया जाता है (नेटिव या स्टिकर)
- `Text`: दस्तावेज़ के भीतर मिलान करने के लिए पाठ सामग्री
- `MatchType`: पाठ मिलान की विधि (Contains, Exact, StartsWith, आदि)

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
    Console.WriteLine($"Document {filePath} contains valid text signatures!");
    
    // सफल हस्ताक्षरों के बारे में जानकारी प्रदर्शित करें
    foreach (TextSignature textSignature in result.Succeeded)
    {
        Console.WriteLine($"\nFound valid text signature:");
        Console.WriteLine($"Text: {textSignature.Text}");
        Console.WriteLine($"Location: Page {textSignature.PageNumber}, {textSignature.Left}x{textSignature.Top}");
    }
}
else
{
    Console.WriteLine($"Document {filePath} failed verification process.");
    Console.WriteLine($"Number of failed signatures: {result.Failed.Count}");
}
```

यह कोड जांचता है कि सत्यापन सफल रहा या नहीं और सत्यापित किए गए पाठ हस्ताक्षरों के बारे में विस्तृत जानकारी प्रदान करता है।

## पूर्ण उदाहरण

यहां एक पूर्ण कार्यशील उदाहरण दिया गया है जो पाठ हस्ताक्षर सत्यापन को प्रदर्शित करता है:

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
                    TextVerifyOptions options = new TextVerifyOptions()
                    {
                        AllPages = true,
                        SignatureImplementation = TextSignatureImplementation.Native,
                        Text = "signature",
                        MatchType = TextMatchType.Contains
                    };
                    
                    // दस्तावेज़ हस्ताक्षर सत्यापित करें
                    VerificationResult result = signature.Verify(options);
                    
                    // प्रक्रिया सत्यापन परिणाम
                    if(result.IsValid)
                    {
                        Console.WriteLine($"\nDocument {filePath} was verified successfully!");
                        foreach (TextSignature item in result.Succeeded)
                        {
                            Console.WriteLine($"\nValid signature is found with text: {item.Text}");
                            Console.WriteLine($"Location: Page {item.PageNumber}, position {item.Left}x{item.Top}");
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

### सत्यापन के लिए नियमित अभिव्यक्तियों का उपयोग करना

अधिक लचीले पैटर्न मिलान के लिए, आप नियमित अभिव्यक्तियों का उपयोग कर सकते हैं:

```csharp
TextVerifyOptions options = new TextVerifyOptions()
{
    Text = "Invoice\\s+#\\d{5,6}",  // "इनवॉइस #12345" जैसे पैटर्न का मिलान करें
    MatchType = TextMatchType.Regex
};
```

### विशिष्ट दस्तावेज़ क्षेत्रों में पाठ का सत्यापन

आप सत्यापन को दस्तावेज़ के विशिष्ट क्षेत्रों तक सीमित कर सकते हैं:

```csharp
TextVerifyOptions options = new TextVerifyOptions()
{
    AllPages = false,
    PageNumber = 1,  // केवल प्रथम पृष्ठ पर सत्यापित करें
    
    // खोज करने के लिए क्षेत्र निर्धारित करें (बिंदुओं में निर्देशांक)
    PagesSetup = new PagesSetup() 
    { 
        FirstPage = true,
        LastPage = false,
        OddPages = false,
        EvenPages = false 
    },
    
    // आयत का क्षेत्रफल मिलीमीटर में
    Rectangle = new Rectangle(10, 10, 100, 30),
    
    Text = "Confidential"
};
```

### एक साथ कई पाठ पैटर्न सत्यापित करना

आप विभिन्न टेक्स्ट पैटर्न की जांच करने के लिए कई सत्यापन विकल्प बना सकते हैं:

```csharp
// सत्यापन विकल्पों की सूची बनाएँ
List<VerifyOptions> listOptions = new List<VerifyOptions>();

// पहला पाठ सत्यापन जोड़ें
listOptions.Add(new TextVerifyOptions()
{
    Text = "Confidential",
    MatchType = TextMatchType.Exact
});

// दूसरा टेक्स्ट सत्यापन जोड़ें
listOptions.Add(new TextVerifyOptions()
{
    Text = "Do not copy",
    MatchType = TextMatchType.Contains
});

// कई विकल्पों के साथ सत्यापित करें
VerificationResult result = signature.Verify(listOptions);
```

### विशिष्ट स्वरूप वाले पाठ का सत्यापन

आप विशिष्ट स्वरूपण विशेषताओं वाले पाठ का सत्यापन भी कर सकते हैं:

```csharp
TextVerifyOptions options = new TextVerifyOptions()
{
    Text = "APPROVED",
    MatchType = TextMatchType.Exact,
    
    // विशिष्ट उपस्थिति गुणों को सत्यापित करें
    ForegroundColorRGB = System.Drawing.Color.Green,
    Font = new SignatureFont() { FontFamily = "Arial", FontSize = 12, Bold = true }
};
```

## पाठ सत्यापन के लिए सर्वोत्तम अभ्यास

1. उपयुक्त मिलान प्रकार चुनें: अपनी सत्यापन आवश्यकताओं के आधार पर सही मिलान प्रकार (Contains, Exact, Regex) चुनें.
2. प्रदर्शन के लिए अनुकूलन करें: बड़े दस्तावेज़ों के लिए, संपूर्ण दस्तावेज़ के बजाय विशिष्ट पृष्ठों को सत्यापित करने पर विचार करें।
3. त्रुटि प्रबंधन: अप्रत्याशित परिदृश्यों को सुचारू रूप से प्रबंधित करने के लिए उचित त्रुटि प्रबंधन को कार्यान्वित करें।
4. केस संवेदनशीलता पर विचार करें: पाठ मिलान में केस संवेदनशीलता का ध्यान रखें, विशेष रूप से महत्वपूर्ण सत्यापन के लिए।
5. पूरी तरह से परीक्षण करें: संगतता सुनिश्चित करने के लिए विभिन्न दस्तावेज़ प्रारूपों और पाठ पैटर्न के साथ सत्यापन का परीक्षण करें।

## सामान्य समस्याओं का निवारण

### पाठ नहीं मिला
- जाँच करें कि क्या पाठ स्वरूपण या एन्कोडिंग पहचान को प्रभावित कर रहा है
- सुनिश्चित करें कि दस्तावेज़ में पाठ वास्तव में नियमित पाठ के रूप में मौजूद है (छवि के रूप में नहीं)
- विभिन्न मिलान मानदंड आज़माएँ (सटीक के बजाय सम्मिलित)

### निष्पादन मुद्दे
- विशिष्ट पृष्ठों या क्षेत्रों को लक्षित करके सत्यापन को अनुकूलित करें
- गलत सकारात्मक परिणामों को कम करने के लिए अधिक विशिष्ट पाठ पैटर्न का उपयोग करें

### सत्यापन विफलताएँ
- जांचें कि क्या रिक्त स्थान, विशेष वर्ण या स्वरूपण मिलान को प्रभावित कर रहे हैं
- सत्यापित करें कि पाठ स्कैन की गई छवि का हिस्सा नहीं है (जिसके लिए OCR की आवश्यकता होती है)
- सुनिश्चित करें कि पाठ जोड़े जाने के बाद से दस्तावेज़ में कोई संशोधन नहीं किया गया है

## निष्कर्ष

पाठ सत्यापन दस्तावेज़ प्रमाणीकरण के लिए एक बहुमुखी और व्यावहारिक तरीका है जिसका उपयोग अकेले या अन्य सत्यापन विधियों के संयोजन में किया जा सकता है। .NET के लिए GroupDocs.Signature आपके .NET अनुप्रयोगों में मज़बूत पाठ सत्यापन कार्यक्षमता को लागू करने के लिए एक व्यापक और उपयोग में आसान API प्रदान करता है।

इस चरण-दर-चरण मार्गदर्शिका का पालन करके, आपने सीखा है कि कैसे:
- पाठ सत्यापन प्रक्रिया को कॉन्फ़िगर और आरंभ करें
- विभिन्न सत्यापन मानदंड निर्दिष्ट करें
- सत्यापन परिणामों को संसाधित करना और उनकी व्याख्या करना
- उन्नत सत्यापन परिदृश्यों को लागू करें

ये क्षमताएं आपको सुरक्षित और विश्वसनीय दस्तावेज़ प्रसंस्करण प्रणालियां बनाने की अनुमति देती हैं जो विभिन्न दस्तावेज़ प्रारूपों में पाठ की प्रामाणिकता को सत्यापित कर सकती हैं।

## पूछे जाने वाले प्रश्न

### क्या GroupDocs.Signature स्कैन किए गए दस्तावेज़ों में पाठ सत्यापित कर सकता है?
GroupDocs.Signature मुख्य रूप से डिजिटल टेक्स्ट सत्यापन के लिए डिज़ाइन किया गया है। स्कैन किए गए दस्तावेज़ों के लिए, आपको स्कैन की गई छवियों को टेक्स्ट में बदलने के लिए पहले OCR (ऑप्टिकल कैरेक्टर रिकॉग्निशन) तकनीक का उपयोग करना होगा।

### पाठ सत्यापन के लिए कौन से दस्तावेज़ प्रारूप समर्थित हैं?
GroupDocs.Signature पीडीएफ, वर्ड दस्तावेज़ (DOC, DOCX), एक्सेल स्प्रेडशीट (XLS, XLSX), पावरपॉइंट प्रस्तुतियाँ (PPT, PPTX), चित्र, और अधिक सहित दस्तावेज़ स्वरूपों की एक विस्तृत श्रृंखला का समर्थन करता है।

### क्या मैं स्वरूपित पाठ (बोल्ड, इटैलिक, विशिष्ट फ़ॉन्ट) सत्यापित कर सकता हूँ?
हां, GroupDocs.Signature फ़ॉन्ट परिवार, आकार, शैली (बोल्ड, इटैलिक) और रंग सहित विशिष्ट स्वरूपण विशेषताओं के साथ पाठ को सत्यापित करने के विकल्प प्रदान करता है।

### क्या पासवर्ड-संरक्षित दस्तावेज़ों में पाठ का सत्यापन संभव है?
हां, GroupDocs.Signature सत्यापन के लिए संरक्षित दस्तावेज़ों को खोलते समय दस्तावेज़ पासवर्ड निर्दिष्ट करने के विकल्प प्रदान करता है।

### क्या मैं वॉटरमार्क और पृष्ठभूमि पाठ सत्यापित कर सकता हूँ?
हां, GroupDocs.Signature वॉटरमार्क और पृष्ठभूमि पाठ सहित विभिन्न प्रकार के पाठ हस्ताक्षरों को सत्यापित कर सकता है, यह इस बात पर निर्भर करता है कि उन्हें दस्तावेज़ में कैसे लागू किया गया था।

### संबंधित संसाधन
* [GroupDocs.Signature API संदर्भ](https://reference.groupdocs.com/signature/net/)
* [GroupDocs.Signature डाउनलोड](https://releases.groupdocs.com/signature/net/)
* [GitHub पर कोड उदाहरण](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
* [प्रलेखन](https://docs.groupdocs.com/signature/net/)
* [उत्पाद पृष्ठ](https://products.groupdocs.com/signature/net/)
* [ब्लॉग लेख](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
* [सहयता मंच](https://forum.groupdocs.com/c/signature/13)
* [अस्थायी लाइसेंस](https://purchase.groupdocs.com/temporary-license/)