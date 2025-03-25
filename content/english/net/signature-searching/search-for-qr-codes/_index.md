---
title: Search for QR Code Signatures in Documents
linktitle: Search for QR Codes
second_title: GroupDocs.Signature .NET API
description: Learn how to efficiently search for QR codes in documents using GroupDocs.Signature for .NET with this comprehensive step-by-step guide and code examples.
weight: 15
url: /net/signature-searching/search-for-qr-codes/
---

## Introduction

In today's digital document ecosystem, QR code signatures have become an invaluable tool for embedding information, authentication, and enhancing document security. GroupDocs.Signature for .NET provides developers with a powerful API to search for and extract QR codes from various document formats, enabling advanced document analysis and verification capabilities in .NET applications.

This comprehensive tutorial will guide you through the process of implementing QR code search functionality using GroupDocs.Signature for .NET, providing clear explanations, step-by-step instructions, and practical code examples that you can integrate into your own applications.

## Prerequisites

Before diving into QR code signature searching, ensure you have the following prerequisites:

1. GroupDocs.Signature for .NET SDK: Download and install the SDK from the [download page](https://releases.groupdocs.com/signature/net/).

2. Development Environment: Set up a .NET development environment, such as Visual Studio, with .NET Framework or .NET Core installed.

3. Basic Knowledge: Familiarity with C# programming and .NET development concepts.

4. Sample Documents: Prepare test documents containing QR codes for verification and testing.

## Import Namespaces

Start by importing the necessary namespaces to access GroupDocs.Signature functionality:

```csharp
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
using System;
using System.Collections.Generic;
```

Now, let's break down the process of searching for QR codes into clear, easy-to-follow steps:

## Step 1: Define the Document Path

First, specify the path to the document containing QR codes that you want to search:

```csharp
string filePath = "sample_multiple_signatures.docx";
```

## Step 2: Initialize the Signature Object

Create an instance of the `Signature` class by passing the document path:

```csharp
using (Signature signature = new Signature(filePath))
{
    // QR code search code will be added here
}
```

## Step 3: Search for QR Code Signatures

Use the `Search` method with the appropriate signature type to find QR codes in the document:

```csharp
// Search for QR code signatures within the document
List<QrCodeSignature> signatures = signature.Search<QrCodeSignature>(SignatureType.QrCode);
```

## Step 4: Process and Display Results

Iterate through the found QR code signatures and access their properties:

```csharp
// Display information about found QR codes
Console.WriteLine($"\nSource document contains {signatures.Count} QR code signature(s):");

foreach (var qrCodeSignature in signatures)
{
    Console.WriteLine($"QR Code found at page {qrCodeSignature.PageNumber} with type {qrCodeSignature.EncodeType.TypeName}");
    Console.WriteLine($"Content: {qrCodeSignature.Text}");
    Console.WriteLine($"Location: X={qrCodeSignature.Left}, Y={qrCodeSignature.Top}, Width={qrCodeSignature.Width}, Height={qrCodeSignature.Height}");
    Console.WriteLine();
}
```

## Complete Example

Here's a comprehensive working example that demonstrates the complete process of searching for QR codes in a document:

```csharp
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
using System;
using System.Collections.Generic;

namespace QrCodeSignatureSearch
{
    class Program
    {
        static void Main(string[] args)
        {
            // Document path - update with your file path
            string filePath = "sample_multiple_signatures.docx";
            
            // Initialize Signature instance
            using (Signature signature = new Signature(filePath))
            {
                try
                {
                    // Search for QR code signatures in the document
                    List<QrCodeSignature> signatures = signature.Search<QrCodeSignature>(SignatureType.QrCode);
                    
                    // Display search results
                    Console.WriteLine($"\nSource document ['{filePath}'] contains {signatures.Count} QR code signature(s):");
                    
                    foreach (var qrCodeSignature in signatures)
                    {
                        Console.WriteLine($"QR Code found at page {qrCodeSignature.PageNumber} with type {qrCodeSignature.EncodeType.TypeName}");
                        Console.WriteLine($"Content: {qrCodeSignature.Text}");
                        Console.WriteLine($"Location: X={qrCodeSignature.Left}, Y={qrCodeSignature.Top}, Width={qrCodeSignature.Width}, Height={qrCodeSignature.Height}");
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

## Advanced QR Code Searching Techniques

### Searching with Specific Criteria

For more targeted searches, you can use `QrCodeSearchOptions` to customize your search criteria:

```csharp
// Create QR code search options with specific criteria
QrCodeSearchOptions options = new QrCodeSearchOptions
{
    // Search only on specific pages
    AllPages = false,
    PageNumber = 1,
    PagesSetup = new PagesSetup { Pages = new List<int> { 1, 3, 5 } },
    
    // Filter by QR code content
    Text = "Invoice",
    MatchType = TextMatchType.Contains,
    
    // Filter by specific QR code types
    EncodeType = QrCodeTypes.QR,
    
    // Define a specific area to search within
    Rectangle = new Rectangle(100, 100, 400, 400)
};

// Search with specific options
List<QrCodeSignature> filteredSignatures = signature.Search<QrCodeSignature>(options);
```

### Processing QR Code Data

You can implement custom processing for QR code data based on your application requirements:

```csharp
foreach (var qrCode in signatures)
{
    // Extract and process QR code data based on content
    string qrContent = qrCode.Text;
    
    if (qrContent.StartsWith("URL:"))
    {
        // Process URL data
        string url = qrContent.Substring(4);
        Console.WriteLine($"Found URL in QR code: {url}");
    }
    else if (qrContent.StartsWith("CONTACT:"))
    {
        // Process contact information
        string contact = qrContent.Substring(8);
        Console.WriteLine($"Found contact information in QR code: {contact}");
    }
    else if (qrContent.StartsWith("INVOICE:"))
    {
        // Process invoice information
        string invoiceData = qrContent.Substring(8);
        Console.WriteLine($"Found invoice information in QR code: {invoiceData}");
        
        // Parse and validate invoice data
        if (ValidateInvoiceData(invoiceData))
        {
            Console.WriteLine("Invoice data is valid!");
        }
        else
        {
            Console.WriteLine("Warning: Invalid invoice data detected!");
        }
    }
}

// Example validation method
static bool ValidateInvoiceData(string data)
{
    // Implement your validation logic
    return !string.IsNullOrEmpty(data) && data.Contains("ID") && data.Contains("Amount");
}
```

### Implementing Security Verification

QR codes are often used for authentication purposes. Here's how to implement basic security verification:

```csharp
// Check if document contains a valid authentication QR code
bool hasValidAuthQrCode = false;

foreach (var qrCode in signatures)
{
    if (qrCode.Text.StartsWith("AUTH:"))
    {
        string authCode = qrCode.Text.Substring(5);
        
        // Verify authentication code (e.g., against a database or predefined list)
        if (VerifyAuthCode(authCode))
        {
            hasValidAuthQrCode = true;
            Console.WriteLine("Document contains valid authentication QR code!");
            break;
        }
    }
}

if (!hasValidAuthQrCode)
{
    Console.WriteLine("Warning: Document does not contain a valid authentication QR code!");
}

// Example verification method
static bool VerifyAuthCode(string code)
{
    // Implement your verification logic
    // This could be a database lookup, API call, or comparison against predefined values
    return code == "A7B82C3D" || code == "X9Y8Z7W6";
}
```

### Extracting QR Code Images

You can extract QR code images from documents for further processing or display:

```csharp
// Save QR code images to disk
foreach (var qrCode in signatures)
{
    if (qrCode.Content != null)
    {
        // Create a unique filename based on page number and position
        string outputPath = $"QrCode_P{qrCode.PageNumber}_X{qrCode.Left}_Y{qrCode.Top}.png";
        
        // Save the image data
        File.WriteAllBytes(outputPath, qrCode.Content);
        Console.WriteLine($"Saved QR code image to {outputPath}");
    }
}
```

## Conclusion

In this comprehensive guide, we've explored how to search for QR code signatures in documents using GroupDocs.Signature for .NET. From basic searching to advanced techniques, you now have the knowledge to implement robust QR code handling in your .NET applications. The GroupDocs.Signature API provides a powerful, flexible framework for working with various signature types, including QR codes, across different document formats.

By harnessing these capabilities, you can enhance document verification processes, implement authentication systems, and extract valuable information embedded in QR codes, all within your .NET applications.

## FAQ's

### Which QR code formats are supported by GroupDocs.Signature?

GroupDocs.Signature supports various QR code formats including standard QR Code, Micro QR Code, and other common QR code standards. The specific format can be accessed through the `EncodeType` property of the `QrCodeSignature` object.

### Can I search for QR codes in password-protected documents?

Yes, GroupDocs.Signature supports searching for QR codes in password-protected documents by providing the password when initializing the `Signature` object:

```csharp
LoadOptions loadOptions = new LoadOptions { Password = "your_password" };
using (Signature signature = new Signature(filePath, loadOptions))
{
    // Search for QR codes
}
```

### How can I filter QR codes based on their content?

You can filter QR codes based on their content using the `Text` and `MatchType` properties of `QrCodeSearchOptions`:

```csharp
QrCodeSearchOptions options = new QrCodeSearchOptions
{
    Text = "Invoice",
    MatchType = TextMatchType.Contains // Other options: Exact, StartsWith, EndsWith
};
```

### Can GroupDocs.Signature detect damaged or partially visible QR codes?

GroupDocs.Signature has some ability to detect partially visible QR codes, but heavily damaged QR codes may not be recognized. The detection accuracy depends on the quality and visibility of the QR code in the document.

### What document formats are supported for QR code searching?

GroupDocs.Signature supports QR code searching in various document formats including PDF, Microsoft Office documents (Word, Excel, PowerPoint), images (JPEG, PNG, TIFF), and many others.

## See Also

* [API Reference](https://reference.groupdocs.com/signature/net/)
* [Code Examples on GitHub](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
* [Product Documentation](https://docs.groupdocs.com/signature/net/)
* [Product Page](https://products.groupdocs.com/signature/net/)
* [Download Latest Version](https://releases.groupdocs.com/signature/net/)
* [Blog Articles](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
* [Free Support Forum](https://forum.groupdocs.com/c/signature/13)
* [Temporary License](https://purchase.groupdocs.com/temporary-license/)