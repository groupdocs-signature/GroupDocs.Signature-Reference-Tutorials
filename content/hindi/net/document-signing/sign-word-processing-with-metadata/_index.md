---
"description": ".NET के लिए GroupDocs.Signature का उपयोग करके Word दस्तावेज़ों में मेटाडेटा हस्ताक्षर जोड़ें। दस्तावेज़ की सुरक्षा और पता लगाने की क्षमता बढ़ाने के लिए लेखक विवरण, टाइमस्टैम्प और कस्टम गुण एम्बेड करें।"
"linktitle": "मेटाडेटा के साथ साइन वर्ड प्रोसेसिंग"
"second_title": "GroupDocs.Signature .NET एपीआई"
"title": "C# .NET में मेटाडेटा हस्ताक्षरों के साथ Word दस्तावेज़ों को बेहतर बनाएँ"
"url": "/hi/net/document-signing/sign-word-processing-with-metadata/"
"weight": 14
---

## परिचय

वर्ड प्रोसेसिंग दस्तावेज़ व्यवसाय, शिक्षा और व्यक्तिगत संचार में उपयोग किए जाने वाले सबसे आम फ़ाइल प्रकारों में से एक हैं। इन दस्तावेज़ों की प्रामाणिकता सुनिश्चित करना, उनके मूल स्रोत का पता लगाना और उनकी अखंडता बनाए रखना कई व्यावसायिक वातावरणों में महत्वपूर्ण है। दस्तावेज़ सुरक्षा और पता लगाने की क्षमता बढ़ाने का एक प्रभावी तरीका मेटाडेटा हस्ताक्षरों को एम्बेड करना है।

यह विस्तृत ट्यूटोरियल आपको .NET के लिए GroupDocs.Signature का उपयोग करके मेटाडेटा के साथ वर्ड प्रोसेसिंग दस्तावेज़ों पर हस्ताक्षर करने की प्रक्रिया में मार्गदर्शन करेगा। मेटाडेटा हस्ताक्षर जोड़कर, आप लेखक विवरण, निर्माण समय-चिह्न, दस्तावेज़ पहचानकर्ता और अन्य कस्टम गुण जैसी मूल्यवान जानकारी सीधे दस्तावेज़ फ़ाइल संरचना में एम्बेड कर सकते हैं।

## आवश्यक शर्तें

इस ट्यूटोरियल के साथ आगे बढ़ने से पहले, सुनिश्चित करें कि आपके पास निम्नलिखित हैं:

1. [.NET के लिए GroupDocs.Signature](https://releases.groupdocs.com/signature/net/) - लाइब्रेरी डाउनलोड करें और इंस्टॉल करें
2. विकास परिवेश - विज़ुअल स्टूडियो या कोई अन्य .NET-संगत IDE
3. वर्ड दस्तावेज़ - एक नमूना दस्तावेज़ फ़ाइल (DOCX, DOC, आदि)
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

अपने स्रोत Word दस्तावेज़ के लिए पथ निर्धारित करें और हस्ताक्षरित आउटपुट को कहाँ सहेजा जाना चाहिए:

```csharp
// अपने Word दस्तावेज़ का पथ निर्दिष्ट करें
string filePath = "sample.docx";

// हस्ताक्षरित दस्तावेज़ के लिए आउटपुट निर्देशिका और फ़ाइल नाम परिभाषित करें
string outputDirectory = "Your Document Directory";
string outputFilePath = Path.Combine(outputDirectory, "SignWordProcessingWithMetadata", "SignedWithMetadata.docx");

// सुनिश्चित करें कि आउटपुट निर्देशिका मौजूद है
Directory.CreateDirectory(Path.GetDirectoryName(outputFilePath));
```

## चरण 2: हस्ताक्षर ऑब्जेक्ट को आरंभ करें

अपने स्रोत Word दस्तावेज़ के साथ हस्ताक्षर वर्ग का एक उदाहरण बनाएँ:

```csharp
using (Signature signature = new Signature(filePath))
{
    // बाकी कोड यहां जाएगा
}
```

## चरण 3: मेटाडेटा हस्ताक्षर बनाएँ और कॉन्फ़िगर करें

इसके बाद, मेटाडेटा विकल्प परिभाषित करें और विभिन्न प्रकार के मेटाडेटा हस्ताक्षर जोड़ें:

```csharp
// मेटाडेटा विकल्प ऑब्जेक्ट बनाएँ
MetadataSignOptions options = new MetadataSignOptions();

// फ़्लुएंट इंटरफ़ेस का उपयोग करके विभिन्न प्रकार के मेटाडेटा जोड़ें
options
    .Add(new WordProcessingMetadataSignature("Author", "Mr.Sherlock Holmes")) // स्ट्रिंग वैल्यू
    .Add(new WordProcessingMetadataSignature("CreatedOn", DateTime.Now))      // दिनांक-समय मान
    .Add(new WordProcessingMetadataSignature("DocumentId", 123456))           // पूर्णांक मान
    .Add(new WordProcessingMetadataSignature("SignatureId", 123.456D))        // दोहरा मूल्य
    .Add(new WordProcessingMetadataSignature("Amount", 123.456M))             // दशमलव मान
    .Add(new WordProcessingMetadataSignature("Total", 123.456F));             // फ्लोट मान
```

## चरण 4: मेटाडेटा के साथ दस्तावेज़ पर हस्ताक्षर करें

वर्ड दस्तावेज़ पर मेटाडेटा हस्ताक्षर लागू करें और परिणाम सहेजें:

```csharp
// दस्तावेज़ पर हस्ताक्षर करें और आउटपुट फ़ाइल पथ पर सहेजें
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

namespace SignWordProcessingWithMetadataExample
{
    class Program
    {
        static void Main(string[] args)
        {
            // फ़ाइल पथ निर्दिष्ट करें
            string filePath = "sample.docx";
            string outputFilePath = Path.Combine("Your Document Directory", "SignWordProcessingWithMetadata", "SignedWithMetadata.docx");
            
            // सुनिश्चित करें कि आउटपुट निर्देशिका मौजूद है
            Directory.CreateDirectory(Path.GetDirectoryName(outputFilePath));

            // मेटाडेटा के साथ Word दस्तावेज़ पर हस्ताक्षर करें
            using (Signature signature = new Signature(filePath))
            {
                // मेटाडेटा विकल्प ऑब्जेक्ट बनाएँ
                MetadataSignOptions options = new MetadataSignOptions();
                
                // विभिन्न प्रकार के मेटाडेटा हस्ताक्षर जोड़ें
                options
                    .Add(new WordProcessingMetadataSignature("Author", "Mr.Sherlock Holmes")) // स्ट्रिंग वैल्यू
                    .Add(new WordProcessingMetadataSignature("CreatedOn", DateTime.Now))      // दिनांक-समय मान
                    .Add(new WordProcessingMetadataSignature("DocumentId", 123456))           // पूर्णांक मान
                    .Add(new WordProcessingMetadataSignature("SignatureId", 123.456D))        // दोहरा मूल्य
                    .Add(new WordProcessingMetadataSignature("Amount", 123.456M))             // दशमलव मान
                    .Add(new WordProcessingMetadataSignature("Total", 123.456F));             // फ्लोट मान
                
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

## उन्नत वर्ड दस्तावेज़ मेटाडेटा तकनीकें

### कस्टम और अंतर्निहित दस्तावेज़ गुणों के साथ कार्य करना

Word दस्तावेज़ों में अंतर्निहित और कस्टम दोनों प्रकार के गुण होते हैं जिन्हें दस्तावेज़ गुण पैनल के माध्यम से एक्सेस किया जा सकता है। GroupDocs.Signature आपको दोनों के साथ काम करने की अनुमति देता है:

```csharp
// अंतर्निहित गुण जोड़ें
options
    .Add(new WordProcessingMetadataSignature("Company", "Sherlock Holmes Consulting"))
    .Add(new WordProcessingMetadataSignature("Category", "Legal Document"))
    .Add(new WordProcessingMetadataSignature("Keywords", "contract,agreement,legal"))
    .Add(new WordProcessingMetadataSignature("Comments", "This document is confidential"))
    .Add(new WordProcessingMetadataSignature("Manager", "John Watson"));

// कस्टम गुण जोड़ें
options.Add(new WordProcessingMetadataSignature("Department", "Legal"));
options.Add(new WordProcessingMetadataSignature("SecurityLevel", "Confidential"));
```

### हस्ताक्षरित वर्ड दस्तावेज़ों में मेटाडेटा खोजना

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

### दस्तावेज़ चर के साथ कार्य करना

वर्ड दस्तावेज़ दस्तावेज़ चरों का भी समर्थन करते हैं, जो मेटाडेटा का दूसरा रूप हैं:

```csharp
// दस्तावेज़ चर जोड़ें
options.Add(new WordProcessingMetadataSignature("DocVariable1", "Custom Value 1", true));
options.Add(new WordProcessingMetadataSignature("DocVariable2", DateTime.Now, true));
```

## निष्कर्ष

इस विस्तृत ट्यूटोरियल में, आपने .NET के लिए GroupDocs.Signature का उपयोग करके मेटाडेटा के साथ Word प्रोसेसिंग दस्तावेज़ों पर हस्ताक्षर करना सीखा है। Word दस्तावेज़ों में मेटाडेटा एम्बेड करने से दस्तावेज़ की ट्रेसेबिलिटी बेहतर होती है, मूल्यवान संदर्भ मिलता है, और प्रामाणिकता स्थापित करने में मदद मिलती है।

वर्ड दस्तावेज़ों में मेटाडेटा हस्ताक्षर व्यावसायिक और कानूनी परिवेशों में विशेष रूप से उपयोगी होते हैं जहाँ दस्तावेज़ की उत्पत्ति, लेखकत्व और संस्करण ट्रैकिंग महत्वपूर्ण होती है। एम्बेडेड मेटाडेटा में लेखक, निर्माण समय, दस्तावेज़ पहचानकर्ता और आपके संगठन की आवश्यकताओं के लिए प्रासंगिक कस्टम गुणों के बारे में जानकारी शामिल हो सकती है।

GroupDocs.Signature के साथ मेटाडेटा हस्ताक्षरों को क्रियान्वित करके, आप यह सुनिश्चित कर सकते हैं कि आपके Word दस्तावेज़ अपनी अखंडता बनाए रखें और अपने पूरे जीवनचक्र में सत्यापन योग्य जानकारी प्रदान करें।

## अक्सर पूछे जाने वाले प्रश्न

### क्या मैं उन Word दस्तावेज़ों में मेटाडेटा जोड़ सकता हूँ जिनमें पहले से ही कुछ गुण परिभाषित हैं?

हाँ, आप Word दस्तावेज़ों में नया मेटाडेटा जोड़ सकते हैं या मौजूदा मेटाडेटा को अपडेट कर सकते हैं। GroupDocs.Signature नए गुण जोड़कर या मौजूदा गुणों को समान नामों से अपडेट करके एकीकरण को संभालेगा।

### मेटाडेटा हस्ताक्षर के लिए कौन से वर्ड प्रोसेसिंग प्रारूप समर्थित हैं?

GroupDocs.Signature for .NET विभिन्न वर्ड प्रोसेसिंग फ़ॉर्मैट के लिए मेटाडेटा साइनिंग का समर्थन करता है, जिसमें DOCX, DOC, RTF, ODT आदि शामिल हैं। पूरी सूची के लिए, देखें [प्रलेखन](https://docs.groupdocs.com/signature/net/).

### क्या वर्ड दस्तावेज़ों में मेटाडेटा हस्ताक्षर पाठकों को दिखाई देते हैं?

मेटाडेटा हस्ताक्षर दस्तावेज़ की सामग्री में दिखाई नहीं देते। हालाँकि, इन्हें Microsoft Word या अन्य संगत अनुप्रयोगों में दस्तावेज़ गुण पैनल के माध्यम से देखा जा सकता है।

### क्या मैं प्रोग्रामेटिक रूप से यह सत्यापित कर सकता हूँ कि मेटाडेटा जोड़ने के बाद वर्ड दस्तावेज़ में छेड़छाड़ की गई है?

हां, GroupDocs.Signature सत्यापन क्षमताएं प्रदान करता है जो यह पता लगाने में मदद कर सकता है कि हस्ताक्षर करने के बाद दस्तावेज़ को संशोधित किया गया है या नहीं, जिसमें मेटाडेटा में परिवर्तन शामिल हैं।

### क्या वर्ड दस्तावेज़ से मेटाडेटा हटाना संभव है?

हाँ, GroupDocs.Signature ज़रूरत पड़ने पर दस्तावेज़ों से मेटाडेटा हस्ताक्षर हटाने के विकल्प प्रदान करता है। दस्तावेज़ों को बाहरी रूप से साझा करने से पहले संवेदनशील जानकारी साफ़ करने के लिए यह उपयोगी हो सकता है।

### मुझे और अधिक संसाधन और सहायता कहां मिल सकती है?

- [एपीआई संदर्भ](https://reference.groupdocs.com/signature/net/)
- [डाउनलोड](https://releases.groupdocs.com/signature/net/)
- [उदाहरण](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
- [प्रलेखन](https://docs.groupdocs.com/signature/net/)
- [उत्पाद पृष्ठ](https://products.groupdocs.com/signature/net/)
- [ब्लॉग](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
- [सहयता मंच](https://forum.groupdocs.com/c/signature/13)
- [अस्थायी लाइसेंस](https://purchase.groupdocs.com/temporary-license/)