---
"description": ".NET के लिए GroupDocs.Signature के साथ विभिन्न दस्तावेज़ स्वरूपों में QR कोड हस्ताक्षरों को गतिशील रूप से अपडेट करने का तरीका जानें। आधुनिक दस्तावेज़ प्रबंधन समाधानों के लिए व्यापक डेवलपर मार्गदर्शिका।"
"linktitle": "QR कोड अपडेट करें"
"second_title": "GroupDocs.Signature .NET एपीआई"
"title": "दस्तावेज़ों में QR कोड हस्ताक्षर अपडेट करें"
"url": "/hi/net/update-operations/update-qr-code/"
"weight": 12
---

## परिचय
आज के डिजिटल-प्रथम व्यावसायिक परिवेश में, क्यूआर कोड दस्तावेज़ प्रबंधन और प्रमाणीकरण प्रणालियों में एक अनिवार्य तत्व बन गए हैं। ये सरल URL से लेकर जटिल संरचित डेटा तक, जानकारी को एनकोड और एक्सेस करने का एक सुविधाजनक तरीका प्रदान करते हैं। .NET के लिए GroupDocs.Signature एक व्यापक टूलकिट प्रदान करता है जो डेवलपर्स को अपने अनुप्रयोगों में उन्नत इलेक्ट्रॉनिक हस्ताक्षर क्षमताओं को एकीकृत करने में सक्षम बनाता है, जिसमें दस्तावेज़ों में मौजूदा क्यूआर कोड हस्ताक्षरों को अपडेट करने की क्षमता भी शामिल है।

यह ट्यूटोरियल विशेष रूप से .NET के लिए GroupDocs.Signature का उपयोग करके दस्तावेज़ों में QR कोड हस्ताक्षरों को अपडेट करने पर केंद्रित है। चाहे आपको मौजूदा QR कोड की स्थिति, आकार या एन्कोडेड डेटा को संशोधित करना हो, यह मार्गदर्शिका आपको स्पष्ट कोड उदाहरणों और स्पष्टीकरणों के साथ चरण-दर-चरण प्रक्रिया से परिचित कराएगी।

## आवश्यक शर्तें
GroupDocs.Signature for .NET के साथ QR कोड हस्ताक्षर अपडेट में गोता लगाने से पहले, सुनिश्चित करें कि आपके पास निम्नलिखित पूर्वापेक्षाएँ मौजूद हैं:

1. विकास परिवेश: एक कार्यशील .NET विकास परिवेश, जैसे Visual Studio 2017 या बाद का संस्करण.
2. GroupDocs.Signature लाइब्रेरी: .NET लाइब्रेरी के लिए GroupDocs.Signature को डाउनलोड और इंस्टॉल करें [डाउनलोड पृष्ठ](https://releases.groupdocs.com/signature/net/).
3. लाइसेंस (वैकल्पिक): उत्पादन उपयोग के लिए, आपको एक वैध लाइसेंस की आवश्यकता होगी। परीक्षण उद्देश्यों के लिए, आप एक का उपयोग कर सकते हैं [अस्थायी लाइसेंस](https://purchase.groupdocs.com/temporary-license/).
4. नमूना दस्तावेज़: वह दस्तावेज़ जिसमें QR कोड हस्ताक्षर हैं जिन्हें आप अद्यतन करना चाहते हैं।
5. बुनियादी C# ज्ञान: C# प्रोग्रामिंग अवधारणाओं से परिचित होना।

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

आइए QR कोड हस्ताक्षरों को अद्यतन करने की प्रक्रिया को स्पष्ट, प्रबंधनीय चरणों में विभाजित करें:

## चरण 1: दस्तावेज़ पथ सेट करें
सबसे पहले, अपने स्रोत दस्तावेज़ के लिए पथ निर्धारित करें और यह भी निर्धारित करें कि अद्यतन दस्तावेज़ कहाँ सहेजा जाएगा:

```csharp
// QR कोड हस्ताक्षरों के साथ स्रोत दस्तावेज़ का पथ
string filePath = "sample_multiple_signatures.docx";

// आउटपुट के लिए फ़ाइल नाम प्राप्त करें
string fileName = Path.GetFileName(filePath);

// आउटपुट निर्देशिका और फ़ाइल पथ परिभाषित करें
string outputDirectory = Path.Combine("Your Document Directory", "UpdateQRCode");
string outputFilePath = Path.Combine(outputDirectory, fileName);

// सुनिश्चित करें कि आउटपुट निर्देशिका मौजूद है
Directory.CreateDirectory(outputDirectory);
```

## चरण 2: स्रोत दस्तावेज़ की प्रतिलिपि बनाएँ
चूंकि अद्यतन कार्रवाई दस्तावेज़ को सीधे संशोधित करती है, इसलिए इसे संरक्षित करने के लिए मूल दस्तावेज़ की एक प्रतिलिपि बनाएँ:

```csharp
// मूल दस्तावेज़ की एक प्रति बनाएँ
File.Copy(filePath, outputFilePath, true);
```

## चरण 3: हस्ताक्षर इंस्टेंस को आरंभ करें
इसका एक उदाहरण बनाएँ `Signature` दस्तावेज़ के साथ काम करने के लिए क्लास:

```csharp
// आउटपुट फ़ाइल पथ के साथ हस्ताक्षर इंस्टेंस को आरंभ करें
using (Signature signature = new Signature(outputFilePath))
{
    // हस्ताक्षर कार्य यहां किए जाएंगे
}
```

## चरण 4: QR कोड खोज विकल्प कॉन्फ़िगर करें
दस्तावेज़ में मौजूदा QR कोड हस्ताक्षरों को खोजने के लिए खोज विकल्प सेट करें:

```csharp
// QR कोड हस्ताक्षरों के लिए खोज विकल्प कॉन्फ़िगर करें
QrCodeSearchOptions options = new QrCodeSearchOptions();

// यदि आवश्यक हो तो आप खोज विकल्पों को अनुकूलित कर सकते हैं
// options.AllPages = true; // सभी पृष्ठों पर खोजें
// options.PageNumber = 1; // किसी विशिष्ट पृष्ठ पर खोजें
// options.EncodeType = QrCodeTypes.QR; // विशिष्ट QR कोड प्रकार खोजें
```

## चरण 5: QR कोड हस्ताक्षर खोजें
दस्तावेज़ में QR कोड हस्ताक्षर खोजने के लिए कॉन्फ़िगर किए गए खोज विकल्पों का उपयोग करें:

```csharp
// QR कोड हस्ताक्षर खोजें
List<QrCodeSignature> signatures = signature.Search<QrCodeSignature>(options);
```

## चरण 6: QR कोड हस्ताक्षर गुण अपडेट करें
यदि QR कोड हस्ताक्षर पाए जाते हैं, तो आवश्यकतानुसार उनके गुणों को अपडेट करें:

```csharp
// जाँच करें कि हस्ताक्षर मिले या नहीं
if (signatures.Count > 0)
{
    // पहला QR कोड हस्ताक्षर प्राप्त करें
    QrCodeSignature qrCodeSignature = signatures[0];
    
    // स्थिति अपडेट करें
    qrCodeSignature.Left = 200;
    qrCodeSignature.Top = 250;
    
    // आकार अपडेट करें
    qrCodeSignature.Width = 200;
    qrCodeSignature.Height = 200;
    
    // यदि आवश्यक हो तो आप QR कोड डेटा को अपडेट भी कर सकते हैं
    // qrCodeSignature.Text = "अपडेट किया गया QR कोड डेटा";
    
    // अद्यतन लागू करें
    bool result = signature.Update(qrCodeSignature);
    
    // परिणाम की जाँच करें
    if (result)
    {
        Console.WriteLine($"QR Code signature was successfully updated in the document '{fileName}'.");
        Console.WriteLine($"New position: {qrCodeSignature.Left}x{qrCodeSignature.Top}");
        Console.WriteLine($"New size: {qrCodeSignature.Width}x{qrCodeSignature.Height}");
    }
    else
    {
        Console.WriteLine($"Failed to update QR Code signature in the document!");
    }
}
else
{
    Console.WriteLine("No QR Code signatures found in the document.");
}
```

## पूर्ण उदाहरण
यहां एक पूर्ण, कार्यात्मक उदाहरण दिया गया है जो दर्शाता है कि किसी दस्तावेज़ में QR कोड हस्ताक्षर को कैसे अपडेट किया जाए:

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;

namespace UpdateQRCodeSignatureExample
{
    class Program
    {
        static void Main(string[] args)
        {
            // दस्तावेज़ पथ
            string filePath = "sample_multiple_signatures.docx";
            
            // आउटपुट पथ परिभाषित करें
            string fileName = Path.GetFileName(filePath);
            string outputDirectory = Path.Combine(Environment.CurrentDirectory, "UpdateQRCode");
            string outputFilePath = Path.Combine(outputDirectory, fileName);
            
            // सुनिश्चित करें कि आउटपुट निर्देशिका मौजूद है
            Directory.CreateDirectory(outputDirectory);
            
            // मूल दस्तावेज़ की एक प्रति बनाएँ
            File.Copy(filePath, outputFilePath, true);
            
            // हस्ताक्षर उदाहरण आरंभ करें
            using (Signature signature = new Signature(outputFilePath))
            {
                // खोज विकल्प कॉन्फ़िगर करें
                QrCodeSearchOptions options = new QrCodeSearchOptions();
                
                // QR कोड हस्ताक्षर खोजें
                List<QrCodeSignature> signatures = signature.Search<QrCodeSignature>(options);
                
                // जाँच करें कि हस्ताक्षर मिले या नहीं
                if (signatures.Count > 0)
                {
                    // पहला हस्ताक्षर प्राप्त करें
                    QrCodeSignature qrCodeSignature = signatures[0];
                    
                    // स्थिति और आकार अपडेट करें
                    qrCodeSignature.Left = 200;
                    qrCodeSignature.Top = 250;
                    qrCodeSignature.Width = 200;
                    qrCodeSignature.Height = 200;
                    
                    // अद्यतन लागू करें
                    bool result = signature.Update(qrCodeSignature);
                    
                    // परिणाम जांचें
                    if (result)
                    {
                        Console.WriteLine($"QR Code signature was successfully updated in document '{fileName}'.");
                        Console.WriteLine($"New position: {qrCodeSignature.Left}x{qrCodeSignature.Top}");
                        Console.WriteLine($"New size: {qrCodeSignature.Width}x{qrCodeSignature.Height}");
                        Console.WriteLine($"Output file path: {outputFilePath}");
                    }
                    else
                    {
                        Console.WriteLine("Failed to update QR Code signature!");
                    }
                }
                else
                {
                    Console.WriteLine("No QR Code signatures found in the document.");
                }
            }
            
            Console.WriteLine("\nPress any key to exit...");
            Console.ReadKey();
        }
    }
}
```

## उन्नत QR कोड हस्ताक्षर अनुकूलन
GroupDocs.Signature मूल स्थिति और आकार से परे QR कोड हस्ताक्षरों को अनुकूलित करने के लिए अतिरिक्त विकल्प प्रदान करता है:

### एन्कोडेड डेटा को अपडेट करना
आप QR कोड में एनकोड किए गए वास्तविक डेटा को अपडेट कर सकते हैं:

```csharp
// एन्कोडेड डेटा को अपडेट करें
qrCodeSignature.Text = "https://www.updated-website.com";
```

### उपस्थिति गुणों को समायोजित करना
QR कोड के दृश्य पहलुओं को अनुकूलित करें:

```csharp
// अग्रभूमि रंग सेट करें (QR कोड रंग)
qrCodeSignature.ForeColor = System.Drawing.Color.Blue;

// पृष्ठभूमि रंग सेट करें
qrCodeSignature.BackgroundColor = System.Drawing.Color.LightYellow;

// पारदर्शिता समायोजित करें
qrCodeSignature.Opacity = 0.8;
```

### सीमाएँ जोड़ना
कस्टम बॉर्डर के साथ QR कोड को बेहतर बनाएं:

```csharp
qrCodeSignature.Border.Color = System.Drawing.Color.Red;
qrCodeSignature.Border.DashStyle = System.Drawing.Drawing2D.DashStyle.Dash;
qrCodeSignature.Border.Weight = 2;
qrCodeSignature.Border.Visible = true;
```

### QR कोड को घुमाना
QR कोड हस्ताक्षर को एक विशिष्ट कोण पर घुमाएँ:

```csharp
qrCodeSignature.Angle = 30; // 30 डिग्री घुमाएँ
```

## विभिन्न दस्तावेज़ स्वरूपों के साथ कार्य करना
GroupDocs.Signature विभिन्न दस्तावेज़ स्वरूपों में QR कोड हस्ताक्षर अद्यतन करने का समर्थन करता है:

- पीडीएफ दस्तावेज़
- माइक्रोसॉफ्ट वर्ड दस्तावेज़ (DOC, DOCX)
- माइक्रोसॉफ्ट एक्सेल स्प्रेडशीट (XLS, XLSX)
- माइक्रोसॉफ्ट पावरपॉइंट प्रस्तुतियाँ (पीपीटी, पीपीटीएक्स)
- ओपनडॉक्यूमेंट प्रारूप
- छवि प्रारूप

न्यूनतम समायोजन के साथ एक ही कोड का उपयोग इन सभी प्रारूपों में किया जा सकता है।

## निष्कर्ष
GroupDocs.Signature for .NET दस्तावेज़ों में QR कोड हस्ताक्षरों को अपडेट करने के लिए एक शक्तिशाली और लचीला समाधान प्रदान करता है। इस ट्यूटोरियल में बताए गए चरणों का पालन करके, डेवलपर्स अपने .NET अनुप्रयोगों में QR कोड हस्ताक्षर अपडेट कार्यक्षमता को कुशलतापूर्वक लागू कर सकते हैं, जिससे दस्तावेज़ प्रबंधन और प्रमाणीकरण क्षमताएँ बेहतर हो जाती हैं।

अपने व्यापक फीचर सेट और सहज API के साथ, GroupDocs.Signature डेवलपर्स को परिष्कृत दस्तावेज़ हस्ताक्षर समाधान बनाने में सक्षम बनाता है जो दस्तावेज़ अखंडता और पहुंच सुनिश्चित करते हुए आधुनिक व्यावसायिक अनुप्रयोगों की आवश्यकताओं को पूरा करते हैं।

## अक्सर पूछे जाने वाले प्रश्न
### क्या मैं एक ही दस्तावेज़ में एकाधिक QR कोड हस्ताक्षर अपडेट कर सकता हूँ?
हाँ, GroupDocs.Signature आपको एक ही दस्तावेज़ में कई QR कोड हस्ताक्षर अपडेट करने की अनुमति देता है। हस्ताक्षरों की खोज करने के बाद, आप परिणामी सूची को फिर से देख सकते हैं और प्रत्येक QR कोड हस्ताक्षर को अलग-अलग अपडेट कर सकते हैं।

### क्या GroupDocs.Signature विभिन्न QR कोड प्रकारों का समर्थन करता है?
हां, GroupDocs.Signature मानक QR, माइक्रो QR और अन्य सहित विभिन्न QR कोड प्रकारों का समर्थन करता है। आप QR कोड प्रकार को निर्दिष्ट करने के लिए निम्न का उपयोग कर सकते हैं: `EncodeType` संपत्ति।

### क्या .NET के लिए GroupDocs.Signature का कोई परीक्षण संस्करण उपलब्ध है?
हां, आप यहां से निःशुल्क परीक्षण संस्करण डाउनलोड कर सकते हैं। [ग्रुपडॉक्स वेबसाइट](https://releases.groupdocs.com/signature/net/) खरीदारी करने से पहले पुस्तकालय की विशेषताओं का मूल्यांकन करें।

### क्या मैं प्रोग्रामेटिक रूप से QR कोड त्रुटि सुधार स्तर को बदल सकता हूँ?
हां, आप नए QR कोड जोड़ते समय त्रुटि सुधार स्तर को बदल सकते हैं, लेकिन मौजूदा QR कोड के लिए इस गुण को अपडेट करना सभी दस्तावेज़ प्रारूपों में समर्थित नहीं हो सकता है।

### मुझे .NET के लिए GroupDocs.Signature हेतु अतिरिक्त समर्थन कहां मिल सकता है?
आप निम्नलिखित संसाधनों के माध्यम से व्यापक सहायता पा सकते हैं:
- [एपीआई दस्तावेज़ीकरण](https://docs.groupdocs.com/signature/net/)
- [एपीआई संदर्भ](https://reference.groupdocs.com/signature/net/)
- [GitHub उदाहरण](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
- [सहयता मंच](https://forum.groupdocs.com/c/signature/13)
- [ब्लॉग](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)