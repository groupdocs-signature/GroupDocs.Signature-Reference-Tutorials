---
"description": ".NET के लिए GroupDocs.Signature का उपयोग करके PDF दस्तावेज़ों में मेटाडेटा हस्ताक्षर एकीकृत करें। PDF की प्रामाणिकता और पता लगाने की क्षमता बढ़ाने के लिए लेखक जानकारी, टाइमस्टैम्प और कस्टम डेटा एम्बेड करना सीखें।"
"linktitle": "मेटाडेटा के साथ PDF पर हस्ताक्षर करें"
"second_title": "GroupDocs.Signature .NET एपीआई"
"title": "C# .NET में PDF दस्तावेज़ों में मेटाडेटा हस्ताक्षर जोड़ें"
"url": "/hi/net/document-signing/sign-pdf-with-metadata/"
"weight": 11
type: docs
---
## परिचय

पीडीएफ (पोर्टेबल डॉक्यूमेंट फॉर्मेट) दस्तावेज़ अपनी स्थिरता और प्लेटफ़ॉर्म स्वतंत्रता के कारण विभिन्न उद्योगों में व्यापक रूप से उपयोग किए जाते हैं। इन दस्तावेज़ों की प्रामाणिकता और पता लगाने की क्षमता सुनिश्चित करना कई व्यावसायिक वातावरणों में महत्वपूर्ण है। इसे प्राप्त करने का एक प्रभावी तरीका पीडीएफ फाइलों में ही मेटाडेटा एम्बेड करना है।

इस विस्तृत ट्यूटोरियल में, हम .NET के लिए GroupDocs.Signature का उपयोग करके मेटाडेटा के साथ PDF दस्तावेज़ों पर हस्ताक्षर करने का तरीका जानेंगे। मेटाडेटा हस्ताक्षर आपको दस्तावेज़ के स्वरूप में कोई स्पष्ट बदलाव किए बिना, दस्तावेज़ में अतिरिक्त जानकारी, जैसे लेखक का विवरण, निर्माण समय, दस्तावेज़ पहचानकर्ता और कस्टम मान, एम्बेड करने की अनुमति देते हैं।

## आवश्यक शर्तें

शुरू करने से पहले, सुनिश्चित करें कि आपके पास निम्नलिखित चीजें मौजूद हैं:

1. [.NET के लिए GroupDocs.Signature](https://releases.groupdocs.com/signature/net/) - लाइब्रेरी डाउनलोड करें और इंस्टॉल करें
2. विकास परिवेश - विज़ुअल स्टूडियो या कोई अन्य .NET-संगत IDE
3. पीडीएफ दस्तावेज़ - हस्ताक्षर करने के लिए एक नमूना पीडीएफ फ़ाइल
4. बुनियादी C# ज्ञान - C# प्रोग्रामिंग भाषा से परिचित होना

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

सबसे पहले, अपने PDF दस्तावेज़ का पथ निर्धारित करें और निर्दिष्ट करें कि आप हस्ताक्षरित आउटपुट को कहाँ सहेजना चाहते हैं:

```csharp
// अपने PDF दस्तावेज़ का पथ निर्दिष्ट करें
string filePath = "sample.pdf";

// आउटपुट निर्देशिका और फ़ाइल पथ परिभाषित करें
string outputDirectory = "Your Document Directory";
string outputFilePath = Path.Combine(outputDirectory, "SignPdfWithMetadata", "SignedWithMetadata.pdf");

// सुनिश्चित करें कि आउटपुट निर्देशिका मौजूद है
Directory.CreateDirectory(Path.GetDirectoryName(outputFilePath));
```

## चरण 2: हस्ताक्षर ऑब्जेक्ट को आरंभ करें

अपने स्रोत PDF दस्तावेज़ के साथ हस्ताक्षर वर्ग का एक उदाहरण बनाएँ:

```csharp
using (Signature signature = new Signature(filePath))
{
    // हस्ताक्षर करने का कोड यहां दिया जाएगा
}
```

## चरण 3: मेटाडेटा विकल्प परिभाषित करें

विभिन्न प्रकार के मेटाडेटा हस्ताक्षर जोड़ते हुए मेटाडेटा विकल्प बनाएं और कॉन्फ़िगर करें:

```csharp
// मेटाडेटा विकल्प ऑब्जेक्ट बनाएँ
MetadataSignOptions options = new MetadataSignOptions();

// फ़्लुएंट इंटरफ़ेस का उपयोग करके विभिन्न प्रकार के मेटाडेटा जोड़ें
options
    .Add(new PdfMetadataSignature("Author", "Mr.Sherlock Holmes")) // स्ट्रिंग वैल्यू
    .Add(new PdfMetadataSignature("CreatedOn", DateTime.Now))       // दिनांक-समय मान
    .Add(new PdfMetadataSignature("DocumentId", 123456))            // पूर्णांक मान
    .Add(new PdfMetadataSignature("SignatureId", 123.456D))         // दोहरा मूल्य
    .Add(new PdfMetadataSignature("Amount", 123.456M))              // दशमलव मान
    .Add(new PdfMetadataSignature("Total", 123.456F));              // फ्लोट मान
```

## चरण 4: मेटाडेटा के साथ PDF पर हस्ताक्षर करें

पीडीएफ दस्तावेज़ पर मेटाडेटा हस्ताक्षर लागू करें और परिणाम सहेजें:

```csharp
// दस्तावेज़ पर हस्ताक्षर करें और आउटपुट पथ पर सहेजें
SignResult result = signature.Sign(outputFilePath, options);

// सफलता संदेश प्रदर्शित करें
Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} metadata signature(s).");
Console.WriteLine($"Signed document saved at: {outputFilePath}");
```

## पूर्ण उदाहरण

यहां संपूर्ण कोड उदाहरण दिया गया है जो सभी चरणों को एक साथ लाता है:

```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;

namespace SignPdfWithMetadataExample
{
    class Program
    {
        static void Main(string[] args)
        {
            // फ़ाइल पथ निर्दिष्ट करें
            string filePath = "sample.pdf";
            string outputFilePath = Path.Combine("Your Document Directory", "SignPdfWithMetadata", "SignedWithMetadata.pdf");
            
            // सुनिश्चित करें कि आउटपुट निर्देशिका मौजूद है
            Directory.CreateDirectory(Path.GetDirectoryName(outputFilePath));

            // मेटाडेटा के साथ PDF पर हस्ताक्षर करें
            using (Signature signature = new Signature(filePath))
            {
                // मेटाडेटा विकल्प ऑब्जेक्ट बनाएँ
                MetadataSignOptions options = new MetadataSignOptions();
                
                // विभिन्न प्रकार के मेटाडेटा हस्ताक्षर जोड़ें
                options
                    .Add(new PdfMetadataSignature("Author", "Mr.Sherlock Holmes")) // स्ट्रिंग वैल्यू
                    .Add(new PdfMetadataSignature("CreatedOn", DateTime.Now))       // दिनांक-समय मान
                    .Add(new PdfMetadataSignature("DocumentId", 123456))            // पूर्णांक मान
                    .Add(new PdfMetadataSignature("SignatureId", 123.456D))         // दोहरा मूल्य
                    .Add(new PdfMetadataSignature("Amount", 123.456M))              // दशमलव मान
                    .Add(new PdfMetadataSignature("Total", 123.456F));              // फ्लोट मान
                
                // दस्तावेज़ पर हस्ताक्षर करें और फ़ाइल में सहेजें
                SignResult result = signature.Sign(outputFilePath, options);
                
                // परिणाम प्रदर्शित करें
                Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).");
                Console.WriteLine($"File saved at {outputFilePath}.");
            }
        }
    }
}
```

## उन्नत PDF मेटाडेटा संचालन

### नामस्थान समर्थन के साथ कस्टम मेटाडेटा जोड़ना

पीडीएफ दस्तावेज़ XML नामस्थान समर्थन के साथ कस्टम मेटाडेटा का समर्थन करते हैं:

```csharp
// नामस्थान के साथ कस्टम मेटाडेटा जोड़ें
options.Add(new PdfMetadataSignature("CustomProperty", "Custom Value")
{
    NamespaceUri = "http://your-namespace.com/schema"
});
```

### हस्ताक्षरित PDF में मेटाडेटा खोजना

हस्ताक्षर करने के बाद, आप मेटाडेटा को सत्यापित या निकालना चाह सकते हैं:

```csharp
// मेटाडेटा के लिए खोज विकल्प बनाएँ
MetadataSearchOptions searchOptions = new MetadataSearchOptions();

// मेटाडेटा हस्ताक्षरों की खोज करें
SearchResult searchResult = signature.Search(searchOptions);

// पाए गए हस्ताक्षर प्रदर्शित करें
Console.WriteLine($"Found {searchResult.Signatures.Count} metadata signatures:");
foreach (var foundSignature in searchResult.Signatures)
{
    MetadataSignature metadataSignature = foundSignature as MetadataSignature;
    if (metadataSignature != null)
    {
        Console.WriteLine($"- {metadataSignature.Name}: {metadataSignature.Value} ({metadataSignature.Value.GetType().Name})");
    }
}
```

### मानक PDF मेटाडेटा के साथ कार्य करना

पीडीएफ दस्तावेजों में मानक मेटाडेटा फ़ील्ड होते हैं जिन्हें एक्सेस और संशोधित किया जा सकता है:

```csharp
// मानक PDF मेटाडेटा फ़ील्ड सेट करें
options
    .Add(new PdfMetadataSignature("Title", "Important Contract"))
    .Add(new PdfMetadataSignature("Subject", "Legal Agreement"))
    .Add(new PdfMetadataSignature("Keywords", "contract, agreement, legal, binding"))
    .Add(new PdfMetadataSignature("Creator", "Legal Department"))
    .Add(new PdfMetadataSignature("Producer", "GroupDocs.Signature"));
```

## निष्कर्ष

इस ट्यूटोरियल में, आपने .NET के लिए GroupDocs.Signature का उपयोग करके मेटाडेटा के साथ PDF दस्तावेज़ों पर हस्ताक्षर करना सीखा। PDF फ़ाइलों में मेटाडेटा एम्बेड करना दस्तावेज़ की प्रामाणिकता बढ़ाने, महत्वपूर्ण जानकारी जोड़ने और दस्तावेज़ प्रबंधन वर्कफ़्लो को बेहतर बनाने का एक बेहतरीन तरीका है।

PDF में मेटाडेटा हस्ताक्षर व्यावसायिक परिवेशों में विशेष रूप से उपयोगी होते हैं जहाँ दस्तावेज़ की ट्रेसेबिलिटी और प्रामाणिकता सत्यापन आवश्यक होता है। एम्बेडेड मेटाडेटा में दस्तावेज़ के मूल, लेखक, निर्माण समय, संस्करण और आपके संगठन के वर्कफ़्लो से संबंधित कस्टम गुणों के बारे में जानकारी शामिल हो सकती है।

GroupDocs.Signature के साथ मेटाडेटा हस्ताक्षरों को लागू करके, आप यह सुनिश्चित कर सकते हैं कि आपके PDF दस्तावेज़ अपनी अखंडता बनाए रखें और अपने पूरे जीवनचक्र में सत्यापन योग्य जानकारी प्रदान करें।

## अक्सर पूछे जाने वाले प्रश्न

### क्या मैं PDF दस्तावेज़ में मौजूदा मेटाडेटा को संशोधित कर सकता हूँ?

हाँ, आप PDF दस्तावेज़ों में मौजूदा मेटाडेटा को संशोधित कर सकते हैं। जब आप मौजूदा मेटाडेटा के समान नामों वाले नए मेटाडेटा हस्ताक्षर लागू करते हैं, तो मान तदनुसार अपडेट हो जाएँगे।

### क्या पीडीएफ दस्तावेजों में मेटाडेटा हस्ताक्षर अंतिम उपयोगकर्ता को दिखाई देते हैं?

मेटाडेटा हस्ताक्षर दस्तावेज़ की सामग्री में दिखाई नहीं देते। हालाँकि, इन्हें Adobe Acrobat जैसे PDF रीडर में दस्तावेज़ गुण पैनल के माध्यम से या मेटाडेटा देखने के लिए विशेष टूल का उपयोग करके देखा जा सकता है।

### क्या मैं PDF में मेटाडेटा को एन्क्रिप्ट या सुरक्षित कर सकता हूँ?

GroupDocs.Signature दस्तावेज़ों को सुरक्षित करने के विकल्प प्रदान करता है, जिसमें एन्क्रिप्शन भी शामिल है। आप संपूर्ण PDF को, उसके मेटाडेटा सहित, सुरक्षित रखने के लिए दस्तावेज़-स्तरीय एन्क्रिप्शन लागू कर सकते हैं।

### क्या पीडीएफ में मैं कितना मेटाडेटा जोड़ सकता हूं, इसकी कोई सीमा है?

हालाँकि PDF विनिर्देशन द्वारा कोई सख्त सीमा निर्धारित नहीं की गई है, लेकिन अत्यधिक मात्रा में मेटाडेटा जोड़ने से फ़ाइल का आकार बढ़ सकता है। मेटाडेटा में केवल प्रासंगिक और आवश्यक जानकारी ही शामिल करने की अनुशंसा की जाती है।

### क्या मैं प्रोग्रामेटिक रूप से यह सत्यापित कर सकता हूँ कि मेटाडेटा जोड़ने के बाद PDF में छेड़छाड़ की गई है?

हां, GroupDocs.Signature सत्यापन क्षमताएं प्रदान करता है जो यह पता लगाने में मदद कर सकता है कि हस्ताक्षर करने के बाद दस्तावेज़ को संशोधित किया गया है या नहीं, जिसमें मेटाडेटा में परिवर्तन शामिल हैं।

### मुझे और अधिक संसाधन और सहायता कहां मिल सकती है?

- [एपीआई संदर्भ](https://reference.groupdocs.com/signature/net/)
- [डाउनलोड](https://releases.groupdocs.com/signature/net/)
- [उदाहरण](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
- [प्रलेखन](https://docs.groupdocs.com/signature/net/)
- [उत्पाद पृष्ठ](https://products.groupdocs.com/signature/net/)
- [ब्लॉग](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
- [सहयता मंच](https://forum.groupdocs.com/c/signature/13)
- [अस्थायी लाइसेंस](https://purchase.groupdocs.com/temporary-license/)