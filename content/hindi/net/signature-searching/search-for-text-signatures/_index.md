---
"description": "हमारे व्यापक चरण-दर-चरण मार्गदर्शिका और कोड उदाहरणों के साथ GroupDocs.Signature for .NET का उपयोग करके दस्तावेज़ों में टेक्स्ट हस्ताक्षरों को कुशलतापूर्वक खोजना सीखें।"
"linktitle": "पाठ हस्ताक्षर खोजें"
"second_title": "GroupDocs.Signature .NET एपीआई"
"title": "दस्तावेज़ों में पाठ हस्ताक्षर खोजें"
"url": "/hi/net/signature-searching/search-for-text-signatures/"
"weight": 16
---

## परिचय

टेक्स्ट हस्ताक्षर, दस्तावेज़ के लेखकत्व, अनुमोदन या सत्यापन को दर्शाने का एक सामान्य तरीका है। डिजिटल दस्तावेज़ प्रबंधन में, प्रोग्रामेटिक रूप से टेक्स्ट हस्ताक्षरों को खोजने और निकालने की क्षमता, दस्तावेज़ सत्यापन, वर्कफ़्लो स्वचालन और अनुपालन सत्यापन के लिए अत्यंत महत्वपूर्ण है। GroupDocs.Signature for .NET आपके .NET अनुप्रयोगों में टेक्स्ट हस्ताक्षर खोज कार्यक्षमता को लागू करने के लिए एक व्यापक समाधान प्रदान करता है, जो विभिन्न दस्तावेज़ स्वरूपों और उन्नत खोज क्षमताओं का समर्थन करता है।

यह ट्यूटोरियल आपको GroupDocs.Signature for .NET का उपयोग करके दस्तावेज़ों में टेक्स्ट हस्ताक्षरों की खोज करने की प्रक्रिया के माध्यम से मार्गदर्शन करेगा, विस्तृत स्पष्टीकरण, चरण-दर-चरण निर्देश और व्यावहारिक कोड उदाहरण प्रदान करेगा।

## आवश्यक शर्तें

पाठ हस्ताक्षर खोज में उतरने से पहले, सुनिश्चित करें कि आपके पास निम्नलिखित पूर्वापेक्षाएँ हैं:

1. .NET लाइब्रेरी के लिए GroupDocs.Signature: लाइब्रेरी को डाउनलोड करें और इंस्टॉल करें [रिलीज़ पृष्ठ](https://releases.groupdocs.com/signature/net/).

2. विकास परिवेश: उपयुक्त विकास परिवेश स्थापित करें जैसे कि विजुअल स्टूडियो या .NET समर्थन वाला कोई संगत IDE.

3. नमूना दस्तावेज़: सत्यापन और परीक्षण के लिए पाठ हस्ताक्षर युक्त परीक्षण दस्तावेज़ तैयार करें।

4. बुनियादी C# ज्ञान: C# प्रोग्रामिंग भाषा और .NET फ्रेमवर्क अवधारणाओं से परिचित होना।

## नामस्थान आयात करें

GroupDocs.Signature कार्यक्षमता तक पहुँचने के लिए आवश्यक नामस्थानों को आयात करके आरंभ करें:

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

अब, आइए पाठ हस्ताक्षरों की खोज की प्रक्रिया को स्पष्ट, प्रबंधनीय चरणों में विभाजित करें:

## चरण 1: दस्तावेज़ लोड करें

सबसे पहले, दस्तावेज़ पथ को परिभाषित करें और आरंभ करें `Signature` वस्तु:

```csharp
string filePath = "sample_multiple_signatures.docx";
string fileName = Path.GetFileName(filePath);

using (Signature signature = new Signature(filePath))
{
    // पाठ हस्ताक्षर खोज कोड यहां जोड़ा जाएगा
}
```

## चरण 2: खोज विकल्प कॉन्फ़िगर करें

बनाएँ और कॉन्फ़िगर करें `TextSearchOptions` यह निर्दिष्ट करने के लिए कि पाठ हस्ताक्षरों को कैसे खोजा जाना चाहिए:

```csharp
// पाठ खोज विकल्प कॉन्फ़िगर करें
TextSearchOptions options = new TextSearchOptions
{
    // सभी पृष्ठों पर खोजें
    AllPages = true,
    
    // वैकल्पिक: मिलान करने के लिए पाठ निर्दिष्ट करें
    // पाठ = "स्वीकृत",
    
    // वैकल्पिक: मिलान प्रकार निर्दिष्ट करें
    // मिलान प्रकार = टेक्स्टमैचटाइप.कंटेन्स
};
```

## चरण 3: टेक्स्ट हस्ताक्षर खोज करें

कॉन्फ़िगर किए गए विकल्पों का उपयोग करके खोज ऑपरेशन निष्पादित करें:

```csharp
// पाठ हस्ताक्षर खोजें
List<TextSignature> signatures = signature.Search<TextSignature>(options);
```

## चरण 4: प्रक्रिया करें और परिणाम प्रदर्शित करें

प्राप्त पाठ हस्ताक्षरों को पुनरावृत्त करें और उनका विवरण प्रदर्शित करें:

```csharp
// खोज परिणाम प्रदर्शित करें
Console.WriteLine($"\nSource document '{fileName}' contains {signatures.Count} text signature(s):");

foreach (TextSignature textSignature in signatures)
{
    Console.WriteLine($"Text signature found at page {textSignature.PageNumber} with text '{textSignature.Text}'");
    Console.WriteLine($"Location: X={textSignature.Left}, Y={textSignature.Top}, Width={textSignature.Width}, Height={textSignature.Height}");
    Console.WriteLine($"Signature type: {textSignature.SignatureImplementation}");
    Console.WriteLine();
}
```

## पूर्ण उदाहरण

यहां एक पूर्ण कार्यशील उदाहरण दिया गया है जो दर्शाता है कि किसी दस्तावेज़ में पाठ हस्ताक्षरों की खोज कैसे की जाती है:

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;

namespace TextSignatureSearch
{
    class Program
    {
        static void Main(string[] args)
        {
            // दस्तावेज़ पथ - अपने फ़ाइल पथ के साथ अद्यतन करें
            string filePath = "sample_multiple_signatures.docx";
            string fileName = Path.GetFileName(filePath);
            
            // हस्ताक्षर उदाहरण आरंभ करें
            using (Signature signature = new Signature(filePath))
            {
                try
                {
                    // पाठ खोज विकल्प कॉन्फ़िगर करें
                    TextSearchOptions options = new TextSearchOptions
                    {
                        // सभी पृष्ठों पर खोजें
                        AllPages = true
                    };
                    
                    // पाठ हस्ताक्षर खोजें
                    List<TextSignature> signatures = signature.Search<TextSignature>(options);
                    
                    // खोज परिणाम प्रदर्शित करें
                    Console.WriteLine($"\nSource document '{fileName}' contains {signatures.Count} text signature(s):");
                    
                    foreach (TextSignature textSignature in signatures)
                    {
                        Console.WriteLine($"Text signature found at page {textSignature.PageNumber} with text '{textSignature.Text}'");
                        Console.WriteLine($"Location: X={textSignature.Left}, Y={textSignature.Top}, Width={textSignature.Width}, Height={textSignature.Height}");
                        Console.WriteLine($"Signature type: {textSignature.SignatureImplementation}");
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

## उन्नत पाठ हस्ताक्षर खोज तकनीकें

### विशिष्ट पाठ मानदंड के साथ खोज करना

अधिक लक्षित खोजों के लिए, आप अनुकूलित कर सकते हैं `TextSearchOptions` विशिष्ट पाठ सामग्री के आधार पर फ़िल्टर करने के लिए:

```csharp
// विशिष्ट पाठ मानदंड के साथ खोज विकल्प बनाएँ
TextSearchOptions options = new TextSearchOptions
{
    // सभी पृष्ठों पर खोजें
    AllPages = true,
    
    // विशिष्ट पाठ खोजें
    Text = "Approved",
    
    // मिलान प्रकार निर्दिष्ट करें (इसमें शामिल है, सटीक, आरंभ होता है, समाप्त होता है)
    MatchType = TextMatchType.Contains,
    
    // केस-सेंसिटिव खोज
    MatchCase = true
};
```

### विशिष्ट दस्तावेज़ क्षेत्रों में खोज करना

आप खोज को दस्तावेज़ के विशिष्ट क्षेत्रों तक सीमित कर सकते हैं:

```csharp
// किसी विशिष्ट दस्तावेज़ क्षेत्र के लिए खोज विकल्प बनाएँ
TextSearchOptions options = new TextSearchOptions
{
    // केवल विशिष्ट पृष्ठों पर खोजें
    AllPages = false,
    PageNumber = 1,
    
    // या एकाधिक पृष्ठ निर्दिष्ट करें
    PagesSetup = new PagesSetup { Pages = new List<int> { 1, 3, 5 } },
    
    // खोज करने के लिए एक विशिष्ट क्षेत्र निर्धारित करें
    Rectangle = new Rectangle(100, 100, 400, 200)
};
```

### उन्नत पाठ फ़िल्टरिंग

अधिक जटिल खोज आवश्यकताओं के लिए कस्टम फ़िल्टरिंग तर्क लागू करें:

```csharp
// कस्टम प्रोसेसिंग के साथ खोज विकल्प बनाएँ
TextSearchOptions options = new TextSearchOptions
{
    AllPages = true,
    
    // प्रतिनिधि का उपयोग करके कस्टम प्रसंस्करण परिभाषित करें
    ProcessCompleted = (TextSignature signature) =>
    {
        // कस्टम सत्यापन तर्क
        bool isValid = signature.Text.Length > 5 && 
                      (signature.Text.Contains("Approved") || signature.Text.Contains("Verified"));
        
        return isValid;
    }
};
```

### विभिन्न पाठ शैलियों की खोज

पाठ हस्ताक्षरों को फ़िल्टर करने के लिए फ़ॉन्ट और शैली गुणों का उपयोग करें:

```csharp
// विशिष्ट पाठ स्वरूप को लक्षित करते हुए खोज विकल्प बनाएँ
TextSearchOptions options = new TextSearchOptions
{
    // फ़ॉन्ट नाम से फ़िल्टर करें
    FontName = "Arial",
    
    // फ़ॉन्ट आकार सीमा के अनुसार फ़िल्टर करें
    MinFontSize = 10,
    MaxFontSize = 14,
    
    // फ़ॉन्ट रंग द्वारा फ़िल्टर करें
    ForeColor = System.Drawing.Color.Blue
};
```

### हस्ताक्षर मेटाडेटा निकालना

पाठ हस्ताक्षरों से संबद्ध मेटाडेटा निकालें और संसाधित करें:

```csharp
foreach (TextSignature signature in signatures)
{
    // हस्ताक्षर मेटाडेटा तक पहुँचें
    if (signature.Metadata != null && signature.Metadata.Count > 0)
    {
        Console.WriteLine("Signature Metadata:");
        
        foreach (var item in signature.Metadata)
        {
            Console.WriteLine($"  {item.Key}: {item.Value}");
        }
    }
    
    // हस्ताक्षर निर्माण और संशोधन तिथियों की जाँच करें
    if (signature.CreatedOn.HasValue)
    {
        Console.WriteLine($"Created on: {signature.CreatedOn.Value}");
    }
    
    if (signature.ModifiedOn.HasValue)
    {
        Console.WriteLine($"Modified on: {signature.ModifiedOn.Value}");
    }
}
```

## निष्कर्ष

इस विस्तृत मार्गदर्शिका में, हमने .NET के लिए GroupDocs.Signature का उपयोग करके दस्तावेज़ों में टेक्स्ट हस्ताक्षरों की खोज करने का तरीका बताया है। बुनियादी खोज कार्यों से लेकर उन्नत तकनीकों तक, अब आपके पास अपने .NET अनुप्रयोगों में मज़बूत टेक्स्ट हस्ताक्षर कार्यक्षमता लागू करने का ज्ञान है।

GroupDocs.Signature पाठ हस्ताक्षरों के साथ काम करने के लिए एक शक्तिशाली और लचीला ढांचा प्रदान करता है, जिससे आप परिष्कृत दस्तावेज़ सत्यापन प्रणाली, स्वचालित वर्कफ़्लो समाधान और अनुपालन सत्यापन उपकरण बना सकते हैं।

## अक्सर पूछे जाने वाले प्रश्न

### क्या मैं पासवर्ड-संरक्षित दस्तावेज़ों में पाठ हस्ताक्षर खोज सकता हूँ?

हाँ, GroupDocs.Signature पासवर्ड-सुरक्षित दस्तावेज़ों में टेक्स्ट हस्ताक्षरों की खोज का समर्थन करता है। आप आरंभ करते समय पासवर्ड प्रदान कर सकते हैं `Signature` वस्तु:

```csharp
LoadOptions loadOptions = new LoadOptions { Password = "your_password" };
using (Signature signature = new Signature(filePath, loadOptions))
{
    // पाठ हस्ताक्षर खोजें
}
```

### पाठ हस्ताक्षर खोज के लिए कौन से दस्तावेज़ प्रारूप समर्थित हैं?

GroupDocs.Signature पीडीएफ, माइक्रोसॉफ्ट ऑफिस दस्तावेज़ (वर्ड, एक्सेल, पावरपॉइंट), ओपनऑफिस प्रारूप, चित्र, आदि सहित दस्तावेज़ प्रारूपों की एक विस्तृत श्रृंखला का समर्थन करता है।

### क्या मैं बोल्ड या इटैलिक जैसे विशिष्ट स्वरूपण वाले टेक्स्ट हस्ताक्षर खोज सकता हूँ?

हां, आप इसका उपयोग करके विशिष्ट स्वरूपण वाले पाठ हस्ताक्षर खोज सकते हैं `FontBold` और `FontItalic` में गुण `TextSearchOptions`:

```csharp
TextSearchOptions options = new TextSearchOptions
{
    FontBold = true,
    FontItalic = true
};
```

### मैं बड़े दस्तावेज़ों के लिए खोज प्रदर्शन कैसे सुधार सकता हूँ?

बड़े दस्तावेज़ों के लिए, आप निम्न तरीकों से खोज प्रदर्शन को अनुकूलित कर सकते हैं:

1. संपूर्ण दस्तावेज़ की खोज के बजाय विशिष्ट पृष्ठों तक खोज को सीमित करना
2. मिलानों की संख्या कम करने के लिए अधिक विशिष्ट खोज मानदंडों का उपयोग करना
3. का उपयोग करके खोज क्षेत्र निर्दिष्ट करना `Rectangle` यदि आप जानते हैं कि हस्ताक्षर आमतौर पर कहाँ स्थित होते हैं तो संपत्ति
4. खोज परिणामों को बैचों में संसाधित करने के लिए अपने एप्लिकेशन में पृष्ठांकन लागू करना

### क्या मैं यह पता लगा सकता हूं कि कोई पाठ हस्ताक्षर इलेक्ट्रॉनिक रूप से जोड़ा गया था या वह मूल दस्तावेज़ सामग्री का हिस्सा है?

GroupDocs.Signature दस्तावेज़ों में विभिन्न प्रकार के टेक्स्ट तत्वों के बीच अंतर कर सकता है। `SignatureImplementation` की संपत्ति `TextSignature` यह दर्शाता है कि पाठ एक औपचारिक हस्ताक्षर है या नियमित दस्तावेज़ सामग्री। हालाँकि, निश्चित निर्धारण इस बात पर निर्भर हो सकता है कि पाठ को मूल रूप से दस्तावेज़ में कैसे जोड़ा गया था।

## यह भी देखें

* [एपीआई संदर्भ](https://reference.groupdocs.com/signature/net/)
* [GitHub पर कोड उदाहरण](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
* [उत्पाद दस्तावेज़ीकरण](https://docs.groupdocs.com/signature/net/)
* [उत्पाद पृष्ठ](https://products.groupdocs.com/signature/net/)
* [नवीनतम संस्करण डाउनलोड करें](https://releases.groupdocs.com/signature/net/)
* [ब्लॉग लेख](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
* [निःशुल्क सहायता मंच](https://forum.groupdocs.com/c/signature/13)
* [अस्थायी लाइसेंस](https://purchase.groupdocs.com/temporary-license/)