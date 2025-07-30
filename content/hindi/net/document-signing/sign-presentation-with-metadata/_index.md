---
"description": ".NET के लिए GroupDocs.Signature का उपयोग करके PowerPoint प्रस्तुतियों में मेटाडेटा हस्ताक्षर एम्बेड करना सीखें। प्रस्तुति की प्रामाणिकता और ट्रेसबिलिटी को बेहतर बनाने के लिए लेखक विवरण, टाइमस्टैम्प और कस्टम गुण जोड़ें।"
"linktitle": "मेटाडेटा के साथ प्रस्तुति पर हस्ताक्षर करें"
"second_title": "GroupDocs.Signature .NET एपीआई"
"title": "C# .NET में मेटाडेटा हस्ताक्षरों के साथ पावरपॉइंट प्रस्तुतियों को बेहतर बनाएँ"
"url": "/hi/net/document-signing/sign-presentation-with-metadata/"
"weight": 12
---

## परिचय

आज के डिजिटल कार्यस्थल में, प्रस्तुतियाँ संचार और सूचना साझा करने के लिए महत्वपूर्ण उपकरण हैं। इन प्रस्तुति फ़ाइलों की प्रामाणिकता और अखंडता सुनिश्चित करना, विशेष रूप से कॉर्पोरेट और शैक्षिक वातावरण में, तेज़ी से महत्वपूर्ण होता जा रहा है। प्रस्तुति की सुरक्षा और ट्रेसबिलिटी को बेहतर बनाने का एक प्रभावी तरीका मेटाडेटा सिग्नेचर एम्बेड करना है।

यह विस्तृत ट्यूटोरियल आपको .NET के लिए GroupDocs.Signature का उपयोग करके मेटाडेटा के साथ PowerPoint प्रस्तुतियों (PPTX, PPT) पर हस्ताक्षर करने की प्रक्रिया में मार्गदर्शन करेगा। मेटाडेटा हस्ताक्षर जोड़कर, आप लेखक विवरण, निर्माण समय-चिह्न, दस्तावेज़ पहचानकर्ता, और अन्य कस्टम गुण जैसी मूल्यवान जानकारी सीधे प्रस्तुति फ़ाइल संरचना में एम्बेड कर सकते हैं।

## आवश्यक शर्तें

इस ट्यूटोरियल के साथ आगे बढ़ने से पहले, सुनिश्चित करें कि आपके पास निम्नलिखित हैं:

1. [.NET के लिए GroupDocs.Signature](https://releases.groupdocs.com/signature/net/) - लाइब्रेरी डाउनलोड करें और इंस्टॉल करें
2. विकास परिवेश - विज़ुअल स्टूडियो या कोई अन्य .NET-संगत IDE
3. पावरपॉइंट प्रस्तुति - एक नमूना प्रस्तुति फ़ाइल (PPTX या PPT प्रारूप)
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

अपने स्रोत प्रस्तुतिकरण के लिए पथ निर्धारित करें और हस्ताक्षरित आउटपुट को कहाँ सहेजा जाना चाहिए:

```csharp
// अपनी प्रस्तुति फ़ाइल का पथ निर्दिष्ट करें
string filePath = "sample.pptx";

// हस्ताक्षरित प्रस्तुति के लिए आउटपुट निर्देशिका और फ़ाइल नाम परिभाषित करें
string outputDirectory = "Your Document Directory";
string outputFilePath = Path.Combine(outputDirectory, "SignPresentationWithMetadata", "SignedWithMetadata.pptx");

// सुनिश्चित करें कि आउटपुट निर्देशिका मौजूद है
Directory.CreateDirectory(Path.GetDirectoryName(outputFilePath));
```

## चरण 2: हस्ताक्षर ऑब्जेक्ट को आरंभ करें

अपनी स्रोत प्रस्तुति फ़ाइल के साथ हस्ताक्षर वर्ग का एक उदाहरण बनाएँ:

```csharp
using (Signature signature = new Signature(filePath))
{
    // बाकी कोड यहां जाएगा
}
```

## चरण 3: मेटाडेटा हस्ताक्षर बनाएँ और कॉन्फ़िगर करें

इसके बाद, मेटाडेटा विकल्प परिभाषित करें और प्रस्तुति मेटाडेटा हस्ताक्षरों की एक सरणी बनाएं:

```csharp
// मेटाडेटा विकल्प ऑब्जेक्ट बनाएँ
MetadataSignOptions options = new MetadataSignOptions();

// विभिन्न डेटा प्रकारों के साथ प्रस्तुति मेटाडेटा हस्ताक्षरों की एक सरणी बनाएँ
PresentationMetadataSignature[] signatures = new PresentationMetadataSignature[]
{
    new PresentationMetadataSignature("Author", "Mr.Sherlock Holmes"), // स्ट्रिंग वैल्यू
    new PresentationMetadataSignature("CreatedOn", DateTime.Now),      // दिनांक-समय मान
    new PresentationMetadataSignature("DocumentId", 123456),           // पूर्णांक मान
    new PresentationMetadataSignature("SignatureId", 123.456D),        // दोहरा मूल्य
    new PresentationMetadataSignature("Amount", 123.456M),             // दशमलव मान
    new PresentationMetadataSignature("Total", 123.456F)               // फ्लोट मान
};

// विकल्पों में हस्ताक्षर संग्रह जोड़ें
options.Signatures.AddRange(signatures);
```

## चरण 4: मेटाडेटा के साथ प्रस्तुति पर हस्ताक्षर करें

प्रस्तुति पर मेटाडेटा हस्ताक्षर लागू करें और परिणाम सहेजें:

```csharp
// दस्तावेज़ पर हस्ताक्षर करें और आउटपुट फ़ाइल पथ पर सहेजें
SignResult result = signature.Sign(outputFilePath, options);

// सफलता संदेश प्रदर्शित करें
Console.WriteLine($"\nSource presentation signed successfully with {result.Succeeded.Count} metadata signature(s).");
Console.WriteLine($"Signed presentation saved at: {outputFilePath}");
```

## पूर्ण उदाहरण

यहां संपूर्ण कोड उदाहरण दिया गया है जो सभी चरणों को एक साथ लाता है:

```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;

namespace SignPresentationWithMetadataExample
{
    class Program
    {
        static void Main(string[] args)
        {
            // फ़ाइल पथ निर्दिष्ट करें
            string filePath = "sample.pptx";
            string outputFilePath = Path.Combine("Your Document Directory", "SignPresentationWithMetadata", "SignedWithMetadata.pptx");
            
            // सुनिश्चित करें कि आउटपुट निर्देशिका मौजूद है
            Directory.CreateDirectory(Path.GetDirectoryName(outputFilePath));

            // मेटाडेटा के साथ प्रस्तुति पर हस्ताक्षर करें
            using (Signature signature = new Signature(filePath))
            {
                // मेटाडेटा विकल्प ऑब्जेक्ट बनाएँ
                MetadataSignOptions options = new MetadataSignOptions();
                
                // विभिन्न डेटा प्रकारों के साथ प्रस्तुति मेटाडेटा हस्ताक्षरों की एक सरणी बनाएँ
                PresentationMetadataSignature[] signatures = new PresentationMetadataSignature[]
                {
                    new PresentationMetadataSignature("Author", "Mr.Sherlock Holmes"), // स्ट्रिंग वैल्यू
                    new PresentationMetadataSignature("CreatedOn", DateTime.Now),      // दिनांक-समय मान
                    new PresentationMetadataSignature("DocumentId", 123456),           // पूर्णांक मान
                    new PresentationMetadataSignature("SignatureId", 123.456D),        // दोहरा मूल्य
                    new PresentationMetadataSignature("Amount", 123.456M),             // दशमलव मान
                    new PresentationMetadataSignature("Total", 123.456F)               // फ्लोट मान
                };
                
                // विकल्पों में हस्ताक्षर संग्रह जोड़ें
                options.Signatures.AddRange(signatures);
                
                // दस्तावेज़ पर हस्ताक्षर करें और फ़ाइल में सहेजें
                SignResult result = signature.Sign(outputFilePath, options);
                
                // परिणाम प्रदर्शित करें
                Console.WriteLine($"\nSource presentation signed successfully with {result.Succeeded.Count} signature(s).");
                Console.WriteLine($"File saved at {outputFilePath}.");
            }
        }
    }
}
```

## उन्नत प्रस्तुति मेटाडेटा तकनीकें

### कस्टम और अंतर्निहित प्रस्तुति गुणों के साथ कार्य करना

पावरपॉइंट प्रस्तुतियों में अंतर्निहित और कस्टम दोनों प्रकार के गुण होते हैं जिन्हें फ़ाइल गुण संवाद के माध्यम से एक्सेस किया जा सकता है। GroupDocs.Signature आपको दोनों के साथ काम करने की अनुमति देता है:

```csharp
// अंतर्निहित गुण जोड़ें
signatures = new PresentationMetadataSignature[]
{
    new PresentationMetadataSignature("Company", "Sherlock Holmes Consulting"),
    new PresentationMetadataSignature("Category", "Presentation"),
    new PresentationMetadataSignature("Keywords", "metadata,signing,groupdocs"),
    new PresentationMetadataSignature("Comments", "This document was signed with GroupDocs.Signature"),
    new PresentationMetadataSignature("Manager", "John Watson")
};
options.Signatures.AddRange(signatures);

// कस्टम गुण जोड़ें
options.Signatures.Add(new PresentationMetadataSignature("CustomProperty1", "Custom Value 1"));
options.Signatures.Add(new PresentationMetadataSignature("CustomProperty2", "Custom Value 2"));
```

### हस्ताक्षरित प्रस्तुतियों में मेटाडेटा खोजना

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

### मौजूदा मेटाडेटा को अपडेट करना

आप समान गुण नामों का उपयोग करके प्रस्तुतियों में मौजूदा मेटाडेटा को अपडेट कर सकते हैं:

```csharp
// मौजूदा मेटाडेटा अपडेट करें
options.Signatures.Add(new PresentationMetadataSignature("Author", "Updated Author Name"));
```

## निष्कर्ष

इस विस्तृत ट्यूटोरियल में, आपने .NET के लिए GroupDocs.Signature का उपयोग करके मेटाडेटा के साथ PowerPoint प्रस्तुतियों पर हस्ताक्षर करना सीखा है। प्रस्तुति फ़ाइलों में मेटाडेटा एम्बेड करने से दस्तावेज़ की ट्रेसेबिलिटी बढ़ती है, मूल्यवान संदर्भ मिलता है, और प्रामाणिकता स्थापित करने में मदद मिलती है।

प्रस्तुतियों में मेटाडेटा हस्ताक्षर व्यावसायिक और शैक्षणिक परिवेशों में विशेष रूप से उपयोगी होते हैं जहाँ दस्तावेज़ की उत्पत्ति, लेखकत्व और संस्करण ट्रैकिंग महत्वपूर्ण होती है। एम्बेडेड मेटाडेटा में लेखक, निर्माण समय, दस्तावेज़ पहचानकर्ता और आपके संगठन की आवश्यकताओं के लिए प्रासंगिक कस्टम गुणों के बारे में जानकारी शामिल हो सकती है।

GroupDocs.Signature के साथ मेटाडेटा हस्ताक्षरों को लागू करके, आप यह सुनिश्चित कर सकते हैं कि आपकी पावरपॉइंट प्रस्तुतियाँ अपनी अखंडता बनाए रखें और अपने पूरे जीवनचक्र में सत्यापन योग्य जानकारी प्रदान करें।

## अक्सर पूछे जाने वाले प्रश्न

### क्या मैं उन प्रस्तुतियों में मेटाडेटा जोड़ सकता हूँ जिनमें पहले से ही कुछ गुण परिभाषित हैं?

हाँ, आप प्रस्तुतियों में नया मेटाडेटा जोड़ सकते हैं या मौजूदा मेटाडेटा को अपडेट कर सकते हैं। GroupDocs.Signature नए गुण जोड़कर या समान नामों वाले मौजूदा गुणों को अपडेट करके एकीकरण को संभालेगा।

### मेटाडेटा हस्ताक्षर के लिए कौन से प्रस्तुति प्रारूप समर्थित हैं?

GroupDocs.Signature for .NET, PPT, PPTX, PPTM, PPS, PPSX और अन्य PowerPoint फ़ॉर्मैट में PowerPoint प्रस्तुतियों के लिए मेटाडेटा साइनिंग का समर्थन करता है। पूरी सूची के लिए, देखें [आधिकारिक दस्तावेज](https://docs.groupdocs.com/signature/net/).

### क्या प्रस्तुतियों में मेटाडेटा हस्ताक्षर दर्शकों को दिखाई देते हैं?

मेटाडेटा हस्ताक्षर प्रस्तुति स्लाइड में दिखाई नहीं देते। हालाँकि, इन्हें पावरपॉइंट या अन्य संगत अनुप्रयोगों में दस्तावेज़ गुण पैनल के माध्यम से देखा जा सकता है।

### क्या मैं प्रस्तुतियों में संवेदनशील मेटाडेटा को एन्क्रिप्ट कर सकता हूँ?

यद्यपि व्यक्तिगत मेटाडेटा गुणों को एन्क्रिप्ट नहीं किया जा सकता, GroupDocs.Signature संपूर्ण दस्तावेज़ को सुरक्षित करने के विकल्प प्रदान करता है। आप प्रस्तुति और उसके मेटाडेटा तक पहुँच को सीमित करने के लिए पासवर्ड सुरक्षा लागू कर सकते हैं।

### क्या मेटाडेटा जोड़ने से प्रस्तुतिकरण प्रदर्शन प्रभावित होता है?

मेटाडेटा जोड़ने से फ़ाइल आकार पर न्यूनतम प्रभाव पड़ता है और प्रस्तुतिकरण प्रदर्शन पर कोई प्रभाव नहीं पड़ता। यह उपयोगकर्ता अनुभव को प्रभावित किए बिना दस्तावेज़ गुणों को बेहतर बनाने का एक आसान तरीका है।

### मुझे और अधिक संसाधन और सहायता कहां मिल सकती है?

- [एपीआई संदर्भ](https://reference.groupdocs.com/signature/net/)
- [डाउनलोड](https://releases.groupdocs.com/signature/net/)
- [उदाहरण](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
- [प्रलेखन](https://docs.groupdocs.com/signature/net/)
- [उत्पाद पृष्ठ](https://products.groupdocs.com/signature/net/)
- [ब्लॉग](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
- [सहयता मंच](https://forum.groupdocs.com/c/signature/13)
- [अस्थायी लाइसेंस](https://purchase.groupdocs.com/temporary-license/)