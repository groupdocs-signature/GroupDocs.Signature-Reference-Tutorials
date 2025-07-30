---
"date": "2025-05-07"
"description": ".NET के लिए GroupDocs.Signature का उपयोग करके QR कोड के साथ DICOM छवियों पर हस्ताक्षर करना सीखें। यह मार्गदर्शिका मेडिकल इमेजिंग में QR कोड हस्ताक्षरों की स्थापना, कार्यान्वयन और सत्यापन को कवर करती है।"
"title": "GroupDocs का उपयोग करके QR कोड के साथ DICOM छवियों पर हस्ताक्षर कैसे करें..NET के लिए हस्ताक्षर एक व्यापक गाइड"
"url": "/hi/net/qr-code-signatures/groupdocs-signature-net-dicom-images-qr-codes/"
"weight": 1
---

# GroupDocs का उपयोग करके QR कोड के साथ DICOM छवियों पर हस्ताक्षर कैसे करें. .NET के लिए हस्ताक्षर: एक व्यापक गाइड

क्या आप अपनी DICOM फ़ाइलों को प्रमाणित करने के लिए एक सुरक्षित तरीका खोज रहे हैं? यह विस्तृत मार्गदर्शिका आपको DICOM छवियों में QR कोड हस्ताक्षरों को एकीकृत करने के लिए GroupDocs.Signature for .NET का उपयोग करने का तरीका बताएगी। स्वास्थ्य सेवा पेशेवरों, डेवलपर्स और डिजिटल मेडिकल दस्तावेज़ों के साथ काम करने वाले सभी लोगों के लिए आदर्श, यह ट्यूटोरियल सेटअप से लेकर कार्यान्वयन तक की जानकारी देता है।

## आप क्या सीखेंगे:
- .NET के लिए GroupDocs.Signature के साथ अपने विकास वातावरण की स्थापना।
- क्यूआर कोड का उपयोग करके DICOM छवियों पर हस्ताक्षर करने के चरण-दर-चरण निर्देश।
- DICOM फ़ाइलों में QR कोड हस्ताक्षरों को सत्यापित करने और खोजने के तरीके।
- समीक्षा प्रयोजनों के लिए हस्ताक्षरित दस्तावेजों का पूर्वावलोकन तैयार करने की तकनीकें।
- प्रदर्शन को अनुकूलित करने और संसाधनों को प्रभावी ढंग से प्रबंधित करने के लिए सर्वोत्तम अभ्यास।

आइये, पूर्वापेक्षाओं से शुरुआत करें!

## आवश्यक शर्तें

.NET के लिए GroupDocs.Signature का इस्तेमाल करने के लिए, सुनिश्चित करें कि आपका वातावरण तैयार है। आपको इन चीज़ों की ज़रूरत होगी:

### आवश्यक लाइब्रेरी और संस्करण
- **.NET के लिए GroupDocs.Signature**अपने .NET फ्रेमवर्क के साथ संगतता सुनिश्चित करें।

### पर्यावरण सेटअप आवश्यकताएँ
- विंडोज़ या लिनक्स पर एक विकास वातावरण.
- Visual Studio या कोई अन्य .NET-संगत IDE स्थापित.

### ज्ञान पूर्वापेक्षाएँ
- C# प्रोग्रामिंग की बुनियादी समझ.
- .NET अनुप्रयोगों में फ़ाइल I/O से परिचित होना।

## .NET के लिए GroupDocs.Signature सेट अप करना

अपनी पसंदीदा विधि का उपयोग करके GroupDocs.Signature लाइब्रेरी स्थापित करें:

**.NET CLI का उपयोग करना:**
```bash
dotnet add package GroupDocs.Signature
```

**पैकेज प्रबंधक:**
```powershell
Install-Package GroupDocs.Signature
```

**NuGet पैकेज प्रबंधक UI:**
- "GroupDocs.Signature" खोजें और नवीनतम संस्करण स्थापित करें।

### लाइसेंस अधिग्रहण

क्षमताओं का अनुभव करने के लिए मुफ़्त परीक्षण से शुरुआत करें। विस्तारित उपयोग के लिए, अस्थायी या पूर्ण लाइसेंस प्राप्त करने पर विचार करें। [ग्रुपडॉक्स](https://purchase.groupdocs.com/buy).

एक बार स्थापित हो जाने पर, लाइब्रेरी को आरंभ करें:

```csharp
using GroupDocs.Signature;
// अपने DICOM फ़ाइल पथ के साथ हस्ताक्षर ऑब्जेक्ट को आरंभ करें।
Signature signature = new Signature("YOUR_DOCUMENT_DIRECTORY\\sample.dicom");
```

## कार्यान्वयन मार्गदर्शिका

### QR कोड के साथ DICOM छवि पर हस्ताक्षर करें

#### अवलोकन
चिकित्सा दस्तावेजों की प्रामाणिकता और पता लगाने की क्षमता सुनिश्चित करने के लिए क्यूआर कोड हस्ताक्षर जोड़ें।

**चरण 1: हस्ताक्षर ऑब्जेक्ट को आरंभ करें**

```csharp
string filePath = "YOUR_DOCUMENT_DIRECTORY\\sample.dicom";
using (Signature signature = new Signature(filePath))
{
    // हस्ताक्षर कार्य के साथ आगे बढ़ें...
}
```

**चरण 2: QR कोड साइन विकल्प बनाएँ**

पाठ, आकार और संरेखण जैसे गुण कॉन्फ़िगर करें.

```csharp
QrCodeSignOptions options = new QrCodeSignOptions("Patient #36363393. R: No-Issues")
{
    AllPages = true,
    Width = 100,
    Height = 100,
    VerticalAlignment = VerticalAlignment.Bottom,
    HorizontalAlignment = HorizontalAlignment.Right,
    Margin = new Padding() { Right = 5, Left = 5 }
};
```

**चरण 3: XMP मेटाडेटा जोड़ें**

दस्तावेज़ को अतिरिक्त मेटाडेटा के साथ संवर्धित करें.

```csharp
DicomSaveOptions dicomSaveOptions = new DicomSaveOptions()
{
    XmpEntries = new List<DicomXmpEntry>() { new DicomXmpEntry(DicomXmpType.PatientName, "Patient #4") }
};
```

**चरण 4: दस्तावेज़ पर हस्ताक्षर करें**

हस्ताक्षर निष्पादित करें और सहेजें.

```csharp
SignResult signResult = signature.Sign("YOUR_OUTPUT_DIRECTORY\\SignedDicom", options, dicomSaveOptions);
```

### दस्तावेज़ जानकारी प्राप्त करें

डेटा अखंडता सुनिश्चित करने के लिए हस्ताक्षरित DICOM फ़ाइलों से मेटाडेटा पुनर्प्राप्त करें।

**अवलोकन:**
सत्यापन के लिए दस्तावेज़ जानकारी और XMP मेटाडेटा हस्ताक्षर तक पहुँच प्राप्त करें।

**चरण 1: दस्तावेज़ जानकारी पुनर्प्राप्त करें**

```csharp
using (Signature signature = new Signature("YOUR_DOCUMENT_DIRECTORY\\sample_signed.dicom"))
{
    IDocumentInfo signedDocumentInfo = signature.GetDocumentInfo();
}
```

**चरण 2: XMP डेटा को पुनरावृत्त और प्रिंट करें**

मेटाडेटा विवरण प्रदर्शित करें.

```csharp
foreach (var item in signedDocumentInfo.MetadataSignatures)
{
    Console.WriteLine(item.ToString());
}
```

### DICOM हस्ताक्षर सत्यापित करें

DICOM छवियों के भीतर QR कोड हस्ताक्षरों की प्रामाणिकता को सत्यापित करें।

**अवलोकन:**
सुनिश्चित करें कि हस्ताक्षर सही और प्रामाणिक हों।

**चरण 1: QR कोड सत्यापन विकल्प बनाएँ**

QR कोड में विशिष्ट पाठ से मेल खाने वाले विकल्प सेट करें.

```csharp
QrCodeVerifyOptions options = new QrCodeVerifyOptions()
{
    AllPages = true,
    Text = "Patient #36363393",
    MatchType = TextMatchType.Contains
};
```

**चरण 2: हस्ताक्षर सत्यापित करें**

जाँच करें कि हस्ताक्षर मानदंडों को पूरा करते हैं या नहीं।

```csharp
VerificationResult result = signature.Verify(options);

if (result.IsValid)
{
    Console.WriteLine($"DICOM {filePath} has {result.Succeeded.Count} successfully verified signatures!");
}
```

### DICOM में हस्ताक्षर खोजें

हस्ताक्षरित DICOM छवियों के भीतर QR कोड हस्ताक्षरों का पता लगाएं।

**अवलोकन:**
दस्तावेज़ की प्रामाणिकता प्रबंधित करने के लिए सभी QR कोड हस्ताक्षरों को कुशलतापूर्वक खोजें।

**चरण 1: QR कोड हस्ताक्षर खोजें**

```csharp
List<QrCodeSignature> signatures = signature.Search<QrCodeSignature>(SignatureType.QrCode);
```

**चरण 2: हस्ताक्षर विवरण दोहराएँ और प्रिंट करें**

प्रत्येक पाए गए हस्ताक्षर के विवरण की समीक्षा करें।

```csharp
foreach (var QrCodeSignature in signatures)
{
    Console.WriteLine($"QRCode signature found at page {QrCodeSignature.PageNumber} with type {QrCodeSignature.EncodeType.TypeName} and text {QrCodeSignature.Text}");
}
```

### हस्ताक्षरित DICOM का पूर्वावलोकन उत्पन्न करें

सत्यापन के लिए दृश्य पूर्वावलोकन बनाएं.

**अवलोकन:**
विशेष सॉफ्टवेयर के बिना सामग्री को सत्यापित करने के लिए छवि पूर्वावलोकन उत्पन्न करें।

**चरण 1: स्ट्रीम विधियाँ परिभाषित करें**

पूर्वावलोकन निर्माण के दौरान फ़ाइल स्ट्रीम प्रबंधन के लिए विधियाँ सेट करें.

```csharp
Stream CreatePageStream(PreviewPageData pageData)
{
    string imageFilePath = Path.Combine("YOUR_OUTPUT_DIRECTORY", "SignDicomImageAdvanced", $"preview-{pageData.PageNumber}.jpg");
    var folder = Path.GetDirectoryName(imageFilePath);
    if (!Directory.Exists(folder))
    {
        Directory.CreateDirectory(folder);
    }
    return new FileStream(imageFilePath, FileMode.Create);
}

void ReleasePageStream(PreviewPageData pageData, Stream pageStream)
{
    pageStream.Dispose();
}
```

**चरण 2: पूर्वावलोकन उत्पन्न करें**

पूर्वावलोकन निर्माण प्रक्रिया निष्पादित करें.

```csharp
using (Signature signature = new Signature("YOUR_DOCUMENT_DIRECTORY\\sample_signed.dicom"))
{
    PreviewOptions previewOption = new PreviewOptions(CreatePageStream, ReleasePageStream)
    {
        PreviewFormat = PreviewOptions.PreviewFormats.PNG,
    };

    signature.GeneratePreview(previewOption);
}
```

## व्यावहारिक अनुप्रयोगों

1. **मेडिकल रिकॉर्ड प्रबंधन**: अनुपालन के लिए क्यूआर कोड हस्ताक्षर का उपयोग करके रोगी रिकॉर्ड को प्रमाणित करें।
2. **स्वास्थ्य सेवा प्रणालियों में ऑडिट ट्रेल्स**: दस्तावेज़ परिवर्तनों को ट्रैक करें और क्यूआर कोड के साथ प्रामाणिकता सत्यापित करें।
3. **सुरक्षित डेटा साझाकरण**डिजिटल हस्ताक्षर एम्बेड करके चिकित्सा छवियों का सुरक्षित साझाकरण सुनिश्चित करें।
4. **अनुपालन सत्यापन**कानूनी आवश्यकताओं को पूरा करने के लिए नियमित रूप से DICOM फ़ाइल अखंडता को सत्यापित करें।
5. **ईएचआर सिस्टम के साथ एकीकरण**सुव्यवस्थित संचालन के लिए हस्ताक्षरित DICOM फाइलों को इलेक्ट्रॉनिक स्वास्थ्य रिकॉर्ड (EHR) प्रणालियों में निर्बाध रूप से एकीकृत करना।