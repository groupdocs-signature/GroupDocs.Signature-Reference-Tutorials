---
"description": ".NET के लिए GroupDocs.Signature का उपयोग करके मेटाडेटा हस्ताक्षर एम्बेड करके Excel स्प्रेडशीट को सुरक्षित और बेहतर बनाएँ। दस्तावेज़ की ट्रेसेबिलिटी और प्रामाणिकता बेहतर बनाने के लिए लेखक जानकारी, टाइमस्टैम्प और कस्टम डेटा जोड़ें।"
"linktitle": "मेटाडेटा के साथ स्प्रेडशीट पर हस्ताक्षर करें"
"second_title": "GroupDocs.Signature .NET एपीआई"
"title": "C# .NET में एक्सेल स्प्रेडशीट में मेटाडेटा हस्ताक्षर जोड़ें"
"url": "/hi/net/document-signing/sign-spreadsheet-with-metadata/"
"weight": 13
---

## परिचय

एक्सेल स्प्रेडशीट में अक्सर महत्वपूर्ण व्यावसायिक डेटा, वित्तीय जानकारी और महत्वपूर्ण गणनाएँ होती हैं। उनकी प्रामाणिकता सुनिश्चित करना, उनके स्रोत का पता लगाना और उनकी अखंडता की रक्षा करना कई व्यावसायिक वातावरणों में महत्वपूर्ण है। स्प्रेडशीट की सुरक्षा और ट्रेसेबिलिटी बढ़ाने का एक प्रभावी तरीका मेटाडेटा सिग्नेचर एम्बेड करना है।

यह विस्तृत ट्यूटोरियल आपको .NET के लिए GroupDocs.Signature का उपयोग करके मेटाडेटा के साथ एक्सेल स्प्रेडशीट पर हस्ताक्षर करने की प्रक्रिया में मार्गदर्शन करेगा। मेटाडेटा हस्ताक्षर जोड़कर, आप लेखक विवरण, निर्माण समय-चिह्न, दस्तावेज़ पहचानकर्ता और अन्य कस्टम गुण जैसी मूल्यवान जानकारी सीधे स्प्रेडशीट फ़ाइल संरचना में एम्बेड कर सकते हैं।

## आवश्यक शर्तें

इस ट्यूटोरियल के साथ आगे बढ़ने से पहले, सुनिश्चित करें कि आपके पास निम्नलिखित हैं:

1. [.NET के लिए GroupDocs.Signature](https://releases.groupdocs.com/signature/net/) - लाइब्रेरी डाउनलोड करें और इंस्टॉल करें
2. विकास परिवेश - विज़ुअल स्टूडियो या कोई अन्य .NET-संगत IDE
3. एक्सेल स्प्रेडशीट - एक नमूना स्प्रेडशीट फ़ाइल (XLSX, XLS, आदि)
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

अपने स्रोत स्प्रेडशीट के लिए पथ निर्धारित करें और हस्ताक्षरित आउटपुट को कहाँ सहेजा जाना चाहिए:

```csharp
// अपनी Excel फ़ाइल का पथ निर्दिष्ट करें
string filePath = "sample.xlsx";

// हस्ताक्षरित स्प्रेडशीट के लिए आउटपुट निर्देशिका और फ़ाइल नाम परिभाषित करें
string outputDirectory = "Your Document Directory";
string outputFilePath = Path.Combine(outputDirectory, "SignSpreadsheetWithMetadata", "SignedWithMetadata.xlsx");

// सुनिश्चित करें कि आउटपुट निर्देशिका मौजूद है
Directory.CreateDirectory(Path.GetDirectoryName(outputFilePath));
```

## चरण 2: हस्ताक्षर ऑब्जेक्ट को आरंभ करें

अपनी स्रोत स्प्रेडशीट फ़ाइल के साथ हस्ताक्षर वर्ग का एक उदाहरण बनाएँ:

```csharp
using (Signature signature = new Signature(filePath))
{
    // बाकी कोड यहां जाएगा
}
```

## चरण 3: मेटाडेटा हस्ताक्षर बनाएँ और कॉन्फ़िगर करें

इसके बाद, मेटाडेटा विकल्प परिभाषित करें और स्प्रेडशीट मेटाडेटा हस्ताक्षरों की एक सरणी बनाएं:

```csharp
// मेटाडेटा विकल्प ऑब्जेक्ट बनाएँ
MetadataSignOptions options = new MetadataSignOptions();

// विभिन्न डेटा प्रकारों के साथ स्प्रेडशीट मेटाडेटा हस्ताक्षरों की एक सरणी बनाएँ
SpreadsheetMetadataSignature[] signatures = new SpreadsheetMetadataSignature[]
{
    new SpreadsheetMetadataSignature("Author", "Mr.Sherlock Holmes"), // स्ट्रिंग वैल्यू
    new SpreadsheetMetadataSignature("CreatedOn", DateTime.Now),      // दिनांक-समय मान
    new SpreadsheetMetadataSignature("DocumentId", 123456),           // पूर्णांक मान
    new SpreadsheetMetadataSignature("SignatureId", 123.456D),        // दोहरा मूल्य
    new SpreadsheetMetadataSignature("Amount", 123.456M),             // दशमलव मान
    new SpreadsheetMetadataSignature("Total", 123.456F)               // फ्लोट मान
};

// विकल्पों में हस्ताक्षर संग्रह जोड़ें
options.Signatures.AddRange(signatures);
```

## चरण 4: मेटाडेटा के साथ स्प्रेडशीट पर हस्ताक्षर करें

स्प्रेडशीट पर मेटाडेटा हस्ताक्षर लागू करें और परिणाम सहेजें:

```csharp
// दस्तावेज़ पर हस्ताक्षर करें और आउटपुट फ़ाइल पथ पर सहेजें
SignResult result = signature.Sign(outputFilePath, options);

// सफलता संदेश प्रदर्शित करें
Console.WriteLine($"\nSource spreadsheet signed successfully with {result.Succeeded.Count} metadata signature(s).");
Console.WriteLine($"Signed spreadsheet saved at: {outputFilePath}");
```

## पूर्ण उदाहरण

यहां संपूर्ण कोड उदाहरण दिया गया है जो सभी चरणों को एक साथ लाता है:

```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;

namespace SignSpreadsheetWithMetadataExample
{
    class Program
    {
        static void Main(string[] args)
        {
            // फ़ाइल पथ निर्दिष्ट करें
            string filePath = "sample.xlsx";
            string outputFilePath = Path.Combine("Your Document Directory", "SignSpreadsheetWithMetadata", "SignedWithMetadata.xlsx");
            
            // सुनिश्चित करें कि आउटपुट निर्देशिका मौजूद है
            Directory.CreateDirectory(Path.GetDirectoryName(outputFilePath));

            // मेटाडेटा के साथ स्प्रेडशीट पर हस्ताक्षर करें
            using (Signature signature = new Signature(filePath))
            {
                // मेटाडेटा विकल्प ऑब्जेक्ट बनाएँ
                MetadataSignOptions options = new MetadataSignOptions();
                
                // विभिन्न डेटा प्रकारों के साथ स्प्रेडशीट मेटाडेटा हस्ताक्षरों की एक सरणी बनाएँ
                SpreadsheetMetadataSignature[] signatures = new SpreadsheetMetadataSignature[]
                {
                    new SpreadsheetMetadataSignature("Author", "Mr.Sherlock Holmes"), // स्ट्रिंग वैल्यू
                    new SpreadsheetMetadataSignature("CreatedOn", DateTime.Now),      // दिनांक-समय मान
                    new SpreadsheetMetadataSignature("DocumentId", 123456),           // पूर्णांक मान
                    new SpreadsheetMetadataSignature("SignatureId", 123.456D),        // दोहरा मूल्य
                    new SpreadsheetMetadataSignature("Amount", 123.456M),             // दशमलव मान
                    new SpreadsheetMetadataSignature("Total", 123.456F)               // फ्लोट मान
                };
                
                // विकल्पों में हस्ताक्षर संग्रह जोड़ें
                options.Signatures.AddRange(signatures);
                
                // दस्तावेज़ पर हस्ताक्षर करें और फ़ाइल में सहेजें
                SignResult result = signature.Sign(outputFilePath, options);
                
                // परिणाम प्रदर्शित करें
                Console.WriteLine($"\nSource spreadsheet signed successfully with {result.Succeeded.Count} signature(s).");
                Console.WriteLine($"File saved at {outputFilePath}.");
            }
        }
    }
}
```

## उन्नत स्प्रेडशीट मेटाडेटा तकनीकें

### कस्टम और अंतर्निहित स्प्रेडशीट गुणों के साथ कार्य करना

एक्सेल स्प्रेडशीट में बिल्ट-इन और कस्टम दोनों तरह के गुण होते हैं जिन्हें फ़ाइल गुण संवाद के माध्यम से एक्सेस किया जा सकता है। GroupDocs.Signature आपको दोनों के साथ काम करने की अनुमति देता है:

```csharp
// अंतर्निहित गुण जोड़ें
signatures = new SpreadsheetMetadataSignature[]
{
    new SpreadsheetMetadataSignature("Company", "Sherlock Holmes Consulting"),
    new SpreadsheetMetadataSignature("Category", "Financial"),
    new SpreadsheetMetadataSignature("Keywords", "budget,forecast,analysis"),
    new SpreadsheetMetadataSignature("Comments", "This spreadsheet contains confidential information"),
    new SpreadsheetMetadataSignature("Manager", "John Watson")
};
options.Signatures.AddRange(signatures);

// कस्टम गुण जोड़ें
options.Signatures.Add(new SpreadsheetMetadataSignature("Department", "Finance"));
options.Signatures.Add(new SpreadsheetMetadataSignature("SecurityLevel", "Confidential"));
```

### हस्ताक्षरित स्प्रेडशीट में मेटाडेटा खोजना

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

आप समान प्रॉपर्टी नामों का उपयोग करके स्प्रेडशीट में मौजूदा मेटाडेटा को अपडेट कर सकते हैं:

```csharp
// मौजूदा मेटाडेटा अपडेट करें
options.Signatures.Add(new SpreadsheetMetadataSignature("Author", "Updated Author Name"));
```

## निष्कर्ष

इस विस्तृत ट्यूटोरियल में, आपने .NET के लिए GroupDocs.Signature का उपयोग करके मेटाडेटा के साथ Excel स्प्रेडशीट पर हस्ताक्षर करना सीखा है। स्प्रेडशीट फ़ाइलों में मेटाडेटा एम्बेड करने से दस्तावेज़ की ट्रेसेबिलिटी बेहतर होती है, मूल्यवान संदर्भ मिलता है और प्रामाणिकता स्थापित करने में मदद मिलती है।

स्प्रेडशीट में मेटाडेटा हस्ताक्षर विशेष रूप से उन व्यावसायिक परिवेशों में उपयोगी होते हैं जहाँ दस्तावेज़ की उत्पत्ति, लेखकत्व और संस्करण ट्रैकिंग महत्वपूर्ण होती है। एम्बेडेड मेटाडेटा में लेखक, निर्माण समय, दस्तावेज़ पहचानकर्ता और आपके संगठन की आवश्यकताओं के लिए प्रासंगिक कस्टम गुणों के बारे में जानकारी शामिल हो सकती है।

GroupDocs.Signature के साथ मेटाडेटा हस्ताक्षरों को लागू करके, आप यह सुनिश्चित कर सकते हैं कि आपकी एक्सेल स्प्रेडशीट अपनी अखंडता बनाए रखें और अपने पूरे जीवनचक्र में सत्यापन योग्य जानकारी प्रदान करें।

## अक्सर पूछे जाने वाले प्रश्न

### क्या मैं उन स्प्रेडशीट में मेटाडेटा जोड़ सकता हूँ जिनमें पहले से ही कुछ गुण परिभाषित हैं?

हाँ, आप स्प्रेडशीट में नया मेटाडेटा जोड़ सकते हैं या मौजूदा मेटाडेटा को अपडेट कर सकते हैं। GroupDocs.Signature नए गुण जोड़कर या समान नामों वाले मौजूदा गुणों को अपडेट करके एकीकरण को संभालेगा।

### मेटाडेटा हस्ताक्षर के लिए कौन से स्प्रेडशीट प्रारूप समर्थित हैं?

GroupDocs.Signature for .NET विभिन्न स्प्रेडशीट फ़ॉर्मैट के लिए मेटाडेटा साइनिंग का समर्थन करता है, जिसमें XLSX, XLS, XLSM, ODS आदि शामिल हैं। पूरी सूची के लिए, देखें [आधिकारिक दस्तावेज](https://docs.groupdocs.com/signature/net/).

### क्या स्प्रेडशीट में मेटाडेटा हस्ताक्षर उपयोगकर्ताओं को दिखाई देते हैं?

मेटाडेटा हस्ताक्षर स्प्रेडशीट की सामग्री में दिखाई नहीं देते। हालाँकि, इन्हें एक्सेल या अन्य संगत अनुप्रयोगों में दस्तावेज़ गुण पैनल के माध्यम से देखा जा सकता है।

### क्या मैं प्रोग्रामेटिक रूप से यह सत्यापित कर सकता हूँ कि मेटाडेटा जोड़ने के बाद स्प्रेडशीट के साथ छेड़छाड़ की गई है?

हां, GroupDocs.Signature सत्यापन क्षमताएं प्रदान करता है जो यह पता लगाने में मदद कर सकता है कि हस्ताक्षर करने के बाद दस्तावेज़ को संशोधित किया गया है या नहीं, जिसमें मेटाडेटा में परिवर्तन शामिल हैं।

### क्या मेटाडेटा जोड़ने से स्प्रेडशीट की कार्यक्षमता प्रभावित होती है?

मेटाडेटा जोड़ने से फ़ाइल आकार पर न्यूनतम प्रभाव पड़ता है और स्प्रेडशीट की कार्यक्षमता पर कोई प्रभाव नहीं पड़ता। यह गणनाओं, सूत्रों या अन्य एक्सेल सुविधाओं को प्रभावित किए बिना दस्तावेज़ गुणों को बेहतर बनाने का एक आसान तरीका है।

### मुझे और अधिक संसाधन और सहायता कहां मिल सकती है?

- [एपीआई संदर्भ](https://reference.groupdocs.com/signature/net/)
- [डाउनलोड](https://releases.groupdocs.com/signature/net/)
- [उदाहरण](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
- [प्रलेखन](https://docs.groupdocs.com/signature/net/)
- [उत्पाद पृष्ठ](https://products.groupdocs.com/signature/net/)
- [ब्लॉग](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
- [सहयता मंच](https://forum.groupdocs.com/c/signature/13)
- [अस्थायी लाइसेंस](https://purchase.groupdocs.com/temporary-license/)