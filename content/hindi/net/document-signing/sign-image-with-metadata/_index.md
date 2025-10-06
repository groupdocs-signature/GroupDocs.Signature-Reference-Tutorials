---
"description": ".NET के लिए GroupDocs.Signature का उपयोग करके छवियों में मेटाडेटा को हस्ताक्षरित और एम्बेड करना सीखें। छवि की प्रामाणिकता और पता लगाने की क्षमता बढ़ाने के लिए लेखक की जानकारी, टाइमस्टैम्प और कस्टम डेटा जोड़ें।"
"linktitle": "मेटाडेटा के साथ साइन छवि"
"second_title": "GroupDocs.Signature .NET एपीआई"
"title": "C# .NET में मेटाडेटा के साथ छवियों पर हस्ताक्षर करें"
"url": "/hi/net/document-signing/sign-image-with-metadata/"
"weight": 10
type: docs
---
## परिचय

प्रामाणिकता, स्वामित्व और पता लगाने की क्षमता स्थापित करने के लिए मेटाडेटा के साथ डिजिटल इमेज साइनिंग का महत्व लगातार बढ़ता जा रहा है। .NET के लिए GroupDocs.Signature विभिन्न इमेज फ़ॉर्मैट में मेटाडेटा सिग्नेचर जोड़ने के लिए एक शक्तिशाली, फिर भी उपयोग में आसान समाधान प्रदान करता है। यह ट्यूटोरियल आपको C# का उपयोग करके मेटाडेटा के साथ इमेज साइन करने की पूरी प्रक्रिया से परिचित कराता है।

मेटाडेटा सिग्नेचर आपको इमेज फ़ाइलों में सीधे मूल्यवान जानकारी एम्बेड करने की सुविधा देते हैं, जैसे कि लेखक की जानकारी, निर्माण समय, विशिष्ट पहचानकर्ता, आदि। यह जानकारी इमेज फ़ाइल का ही हिस्सा बन जाती है, जिससे इमेज की प्रामाणिकता को ट्रैक और सत्यापित करने का एक विश्वसनीय तरीका मिलता है।

## आवश्यक शर्तें

इस ट्यूटोरियल के साथ आगे बढ़ने से पहले, सुनिश्चित करें कि आपके पास निम्नलिखित हैं:

1. [.NET के लिए GroupDocs.Signature](https://releases.groupdocs.com/signature/net/) - लाइब्रेरी डाउनलोड करें और इंस्टॉल करें
2. विकास परिवेश - विजुअल स्टूडियो या .NET समर्थन वाला कोई भी संगत IDE
3. छवि फ़ाइल - समर्थित प्रारूप (PNG, JPG, TIFF, आदि) में एक नमूना छवि फ़ाइल.
4. बुनियादी C# प्रोग्रामिंग ज्ञान - C# प्रोग्रामिंग अवधारणाओं से परिचित होना

## नामस्थान आयात करें

GroupDocs.Signature कार्यक्षमता तक पहुँचने के लिए आवश्यक नामस्थानों को आयात करके प्रारंभ करें:

```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

## चरण 1: फ़ाइल पथ सेट करें

अपने स्रोत चित्र के लिए पथ निर्धारित करें और हस्ताक्षरित आउटपुट को कहाँ सहेजा जाना चाहिए:

```csharp
// अपनी स्रोत छवि फ़ाइल का पथ निर्दिष्ट करें
string filePath = "sample.png";

// हस्ताक्षरित छवि के लिए आउटपुट निर्देशिका और फ़ाइल नाम परिभाषित करें
string outputDirectory = "Your Document Directory";
string outputFilePath = Path.Combine(outputDirectory, "SignImageWithMetadata", "SignedWithMetadata.png");

// सुनिश्चित करें कि आउटपुट निर्देशिका मौजूद है
Directory.CreateDirectory(Path.GetDirectoryName(outputFilePath));
```

## चरण 2: हस्ताक्षर ऑब्जेक्ट को आरंभ करें

अपनी स्रोत छवि फ़ाइल के साथ हस्ताक्षर वर्ग का एक उदाहरण बनाएँ:

```csharp
using (Signature signature = new Signature(filePath))
{
    // बाकी कोड यहां जाएगा
}
```

## चरण 3: मेटाडेटा हस्ताक्षर बनाएँ और कॉन्फ़िगर करें

इसके बाद, उस मेटाडेटा को परिभाषित करें जिसे आप छवि में एम्बेड करना चाहते हैं। GroupDocs.Signature मेटाडेटा के लिए विभिन्न डेटा प्रकारों का समर्थन करता है:

```csharp
// मेटाडेटा आईडी आरंभ करें (छवि प्रारूप के लिए विशिष्ट)
ushort imgsMetadataId = 41996;

// मेटाडेटा विकल्प ऑब्जेक्ट बनाएँ
MetadataSignOptions options = new MetadataSignOptions();

// विभिन्न प्रकार के मेटाडेटा हस्ताक्षर जोड़ें
options
    .Add(new ImageMetadataSignature(imgsMetadataId++, "Mr.Sherlock Holmes"))  // स्ट्रिंग वैल्यू
    .Add(new ImageMetadataSignature(imgsMetadataId++, DateTime.Now))          // दिनांक समय मान
    .Add(new ImageMetadataSignature(imgsMetadataId++, 123456))                // पूर्णांक मान
    .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456D))              // दोहरा मूल्य
    .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456M))              // दशमलव मान
    .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456F));             // फ्लोट मान
```

## चरण 4: मेटाडेटा के साथ छवि पर हस्ताक्षर करें

छवि पर मेटाडेटा हस्ताक्षर लागू करें और परिणाम सहेजें:

```csharp
// दस्तावेज़ पर हस्ताक्षर करें और आउटपुट फ़ाइल पथ पर सहेजें
SignResult result = signature.Sign(outputFilePath, options);

// सफलता संदेश प्रदर्शित करें
Console.WriteLine($"\nSource image signed successfully with {result.Succeeded.Count} metadata signature(s).");
Console.WriteLine($"Signed image saved at: {outputFilePath}");
```

## पूर्ण उदाहरण

यहां संपूर्ण कोड उदाहरण दिया गया है जो सभी चरणों को एक साथ लाता है:

```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;

namespace SignImageWithMetadataExample
{
    class Program
    {
        static void Main(string[] args)
        {
            // फ़ाइल पथ निर्दिष्ट करें
            string filePath = "sample.png";            
            string outputFilePath = Path.Combine("Your Document Directory", "SignImageWithMetadata", "SignedWithMetadata.png");
            
            // सुनिश्चित करें कि आउटपुट निर्देशिका मौजूद है
            Directory.CreateDirectory(Path.GetDirectoryName(outputFilePath));

            // छवि पर मेटाडेटा से हस्ताक्षर करें
            using (Signature signature = new Signature(filePath))
            {
                // मेटाडेटा आईडी आरंभ करें (छवि प्रारूप के लिए विशिष्ट)
                ushort imgsMetadataId = 41996;
                
                // मेटाडेटा विकल्प बनाएँ
                MetadataSignOptions options = new MetadataSignOptions();
                
                // विभिन्न प्रकार के मेटाडेटा हस्ताक्षर जोड़ें
                options
                    .Add(new ImageMetadataSignature(imgsMetadataId++, "Mr.Sherlock Holmes")) // स्ट्रिंग वैल्यू
                    .Add(new ImageMetadataSignature(imgsMetadataId++, DateTime.Now))          // दिनांक समय मान
                    .Add(new ImageMetadataSignature(imgsMetadataId++, 123456))                // पूर्णांक मान
                    .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456D))              // दोहरा मूल्य
                    .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456M))              // दशमलव मान
                    .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456F));             // फ्लोट मान
                
                // दस्तावेज़ पर हस्ताक्षर करें और फ़ाइल में सहेजें
                SignResult result = signature.Sign(outputFilePath, options);
                
                // परिणाम प्रदर्शित करें
                Console.WriteLine($"\nSource image signed successfully with {result.Succeeded.Count} signature(s).");
                Console.WriteLine($"File saved at {outputFilePath}.");
            }
        }
    }
}
```

## उन्नत मेटाडेटा हस्ताक्षर तकनीकें

### कस्टम मेटाडेटा के साथ कार्य करना

आप विशिष्ट आईडी के साथ कस्टम मेटाडेटा फ़ील्ड भी बना सकते हैं:

```csharp
// विशिष्ट आईडी के साथ कस्टम मेटाडेटा बनाएँ
options.Add(new ImageMetadataSignature(42000, "CustomValue"));
```

### मेटाडेटा हस्ताक्षरों का सत्यापन

हस्ताक्षर करने के बाद, आप मेटाडेटा हस्ताक्षरों को सत्यापित करना चाह सकते हैं:

```csharp
// सत्यापन विकल्प बनाएँ
MetadataSearchOptions searchOptions = new MetadataSearchOptions();

// मेटाडेटा हस्ताक्षरों की खोज करें
SearchResult result = signature.Search(searchOptions);

// पाए गए हस्ताक्षर प्रदर्शित करें
Console.WriteLine($"Found {result.Signatures.Count} metadata signatures:");
foreach(var metadataSignature in result.Signatures)
{
    Console.WriteLine($"- {metadataSignature.Name}: {metadataSignature.Value}");
}
```

## निष्कर्ष

इस ट्यूटोरियल में, आपने .NET के लिए GroupDocs.Signature का उपयोग करके मेटाडेटा के साथ छवियों पर हस्ताक्षर करना सीखा। छवियों में मेटाडेटा एम्बेड करने से छवि की प्रामाणिकता बढ़ाने, महत्वपूर्ण जानकारी जोड़ने और दस्तावेज़ प्रबंधन वर्कफ़्लो को बेहतर बनाने का एक बेहतरीन तरीका मिलता है। यह प्रक्रिया सरल और शक्तिशाली है, जिससे आप अपनी विशिष्ट आवश्यकताओं के अनुसार अनुकूलन कर सकते हैं।

छवि फ़ाइल में एम्बेड किए गए मेटाडेटा का उपयोग कॉपीराइट सुरक्षा, छवि की उत्पत्ति का पता लगाने, वर्णनात्मक जानकारी जोड़ने और डिजिटल कस्टडी श्रृंखला स्थापित करने जैसे विभिन्न उद्देश्यों के लिए किया जा सकता है। मेटाडेटा हस्ताक्षरों को लागू करके, आप यह सुनिश्चित कर सकते हैं कि आपकी छवियाँ अपने पूरे जीवनचक्र में अपनी अखंडता और प्रामाणिकता बनाए रखें।

## अक्सर पूछे जाने वाले प्रश्न

### क्या मैं मौजूदा हस्ताक्षरित छवियों में मेटाडेटा जोड़ सकता हूँ?

हाँ, आप उन इमेज में अतिरिक्त मेटाडेटा जोड़ सकते हैं जिनमें पहले से ही मेटाडेटा सिग्नेचर मौजूद हैं। मौजूदा मेटाडेटा सुरक्षित रहेगा और उसके अनुसार नया मेटाडेटा जोड़ा जाएगा।

### मेटाडेटा हस्ताक्षर के लिए कौन से छवि प्रारूप समर्थित हैं?

GroupDocs.Signature for .NET विभिन्न इमेज फ़ॉर्मैट के लिए मेटाडेटा साइनिंग का समर्थन करता है, जिसमें PNG, JPEG, TIFF, BMP, GIF, आदि शामिल हैं। पूरी सूची के लिए, देखें [आधिकारिक दस्तावेज](https://docs.groupdocs.com/signature/net/).

### क्या छवियों में मेटाडेटा को एन्क्रिप्ट करना संभव है?

हां, GroupDocs.Signature बेहतर सुरक्षा के लिए मेटाडेटा एन्क्रिप्ट करने के विकल्प प्रदान करता है। आप संवेदनशील मेटाडेटा जानकारी की सुरक्षा के लिए लाइब्रेरी द्वारा प्रदान किए गए एन्क्रिप्शन विकल्पों का उपयोग कर सकते हैं।

### क्या मैं हस्ताक्षरित छवियों की प्रामाणिकता को प्रोग्रामेटिक रूप से सत्यापित कर सकता हूँ?

बिल्कुल। आप मेटाडेटा हस्ताक्षरों को मान्य करने और हस्ताक्षरित छवियों की प्रामाणिकता की पुष्टि करने के लिए GroupDocs.Signature में सत्यापन विधियों का उपयोग कर सकते हैं।

### क्या मेटाडेटा के साथ छवियों पर हस्ताक्षर करते समय फ़ाइल आकार की कोई सीमा होती है?

लाइब्रेरी द्वारा फ़ाइल आकार की कोई विशिष्ट सीमा नहीं लगाई गई है, लेकिन बहुत बड़ी फ़ाइलों के लिए ज़्यादा प्रोसेसिंग समय और मेमोरी की आवश्यकता हो सकती है। अत्यधिक बड़ी छवियों के साथ काम करते समय सिस्टम संसाधनों पर विचार करने की सलाह दी जाती है।

### मैं परीक्षण प्रयोजनों के लिए अस्थायी लाइसेंस कैसे प्राप्त कर सकता हूँ?

आप प्राप्त कर सकते हैं [अस्थायी लाइसेंस](https://purchase.groupdocs.com/temporary-license/) खरीद करने से पहले GroupDocs.Signature का परीक्षण करने के लिए।

### मुझे और अधिक संसाधन और सहायता कहां मिल सकती है?

- [एपीआई संदर्भ](https://reference.groupdocs.com/signature/net/)
- [डाउनलोड](https://releases.groupdocs.com/signature/net/)
- [उदाहरण](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
- [प्रलेखन](https://docs.groupdocs.com/signature/net/)
- [उत्पाद पृष्ठ](https://products.groupdocs.com/signature/net/)
- [ब्लॉग](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
- [सहयता मंच](https://forum.groupdocs.com/c/signature/13)