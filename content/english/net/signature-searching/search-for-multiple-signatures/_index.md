---
title: Search for Multiple Signature Types in Documents
linktitle: Search for Multiple Signatures
second_title: GroupDocs.Signature .NET API
description: Learn how to search for multiple signature types in documents using GroupDocs.Signature for .NET. Comprehensive guide with code examples for enhanced document security.
weight: 14
url: /net/signature-searching/search-for-multiple-signatures/
---

## Introduction

In modern document management systems, the ability to search for and validate multiple signature types within a single document is increasingly important. Organizations often employ various signature types—such as digital signatures, text signatures, barcodes, QR codes, and more—to enhance document security and streamline verification processes. GroupDocs.Signature for .NET provides a powerful framework that enables developers to implement comprehensive signature search functionality across various document formats.

This tutorial will guide you through the process of searching for multiple signature types within documents using GroupDocs.Signature for .NET, offering detailed explanations and practical code examples.

## Prerequisites

Before diving into implementing multiple signature search functionality, ensure you have the following prerequisites:

1. Development Environment: Visual Studio or any preferred .NET development environment installed on your system.
  
2. GroupDocs.Signature for .NET: Download and install the GroupDocs.Signature for .NET library from [here](https://releases.groupdocs.com/signature/net/).

3. Basic C# Knowledge: Familiarity with C# programming language and .NET framework concepts.

4. Sample Documents: Prepare test documents containing various types of signatures for testing purposes.

## Import Namespaces

Begin by importing the necessary namespaces to access GroupDocs.Signature functionality:

```csharp
using System;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

Now, let's break down the process of searching for multiple signature types into clear, manageable steps:

## Step 1: Load the Document

First, load the document containing signatures that you want to search:

```csharp
string filePath = "sample_multiple_signatures.docx";
using (Signature signature = new Signature(filePath))
{
    // Multi-signature search code will be added here
}
```

## Step 2: Define Search Options for Different Signature Types

Create search options for each signature type you want to search for:

```csharp
// Define search options for text signatures
TextSearchOptions textOptions = new TextSearchOptions
{
    AllPages = true,  // Search on all pages
    Text = "Signature",  // Optional: text to find
    MatchType = TextMatchType.Contains  // Matching criteria
};

// Define search options for digital signatures
DigitalSearchOptions digitalOptions = new DigitalSearchOptions
{
    AllPages = true
};

// Define search options for barcode signatures
BarcodeSearchOptions barcodeOptions = new BarcodeSearchOptions
{
    AllPages = true,
    Text = "123456",  // Optional: barcode text to match
    MatchType = TextMatchType.Exact  // Matching criteria
};

// Define search options for QR code signatures
QrCodeSearchOptions qrCodeOptions = new QrCodeSearchOptions
{
    AllPages = true,
    Text = "John",  // Optional: QR code text to match
    MatchType = TextMatchType.Contains  // Matching criteria
};

// Define search options for metadata signatures
MetadataSearchOptions metadataOptions = new MetadataSearchOptions();
```

## Step 3: Add Options to a Collection

Add all the search options to a collection:

```csharp
// Create a list to hold all search options
List<SearchOptions> searchOptions = new List<SearchOptions>
{
    textOptions,
    digitalOptions,
    barcodeOptions,
    qrCodeOptions,
    metadataOptions
};
```

## Step 4: Perform the Search and Process Results

Execute the search using the combined search options and process the results:

```csharp
// Search for all signature types using the defined options
SearchResult result = signature.Search(searchOptions);

// Check if signatures were found
if (result.Signatures.Count > 0)
{
    Console.WriteLine($"\nSource document ['{filePath}'] contains {result.Signatures.Count} signature(s):");
    
    // Iterate through the found signatures
    foreach (var foundSignature in result.Signatures)
    {
        Console.WriteLine($"Signature found: Type: {foundSignature.SignatureType}, Page: {foundSignature.PageNumber}, ID: {foundSignature.SignatureId}");
        
        // Process specific signature types
        if (foundSignature is TextSignature textSignature)
        {
            Console.WriteLine($"Text: '{textSignature.Text}'");
        }
        else if (foundSignature is BarcodeSignature barcodeSignature)
        {
            Console.WriteLine($"Barcode Type: {barcodeSignature.EncodeType.TypeName}, Text: '{barcodeSignature.Text}'");
        }
        else if (foundSignature is QrCodeSignature qrCodeSignature)
        {
            Console.WriteLine($"QR Code Type: {qrCodeSignature.EncodeType.TypeName}, Text: '{qrCodeSignature.Text}'");
        }
        else if (foundSignature is DigitalSignature digitalSignature)
        {
            Console.WriteLine($"Certificate: {digitalSignature.Certificate?.SubjectName}, Valid: {digitalSignature.IsValid}");
        }
        else if (foundSignature is MetadataSignature metadataSignature)
        {
            Console.WriteLine($"Metadata: Name: {metadataSignature.Name}, Value: {metadataSignature.Value}");
        }
    }
}
else
{
    Console.WriteLine("No signatures were found in the document.");
}
```

## Complete Example

Here's a complete, working example that demonstrates searching for multiple signature types in a document:

```csharp
using System;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;

namespace MultiSignatureSearch
{
    class Program
    {
        static void Main(string[] args)
        {
            // Document path
            string filePath = "sample_multiple_signatures.docx";
            
            // Initialize Signature instance
            using (Signature signature = new Signature(filePath))
            {
                try
                {
                    // Define search options for text signatures
                    TextSearchOptions textOptions = new TextSearchOptions
                    {
                        AllPages = true,
                        MatchType = TextMatchType.Contains
                    };

                    // Define search options for digital signatures
                    DigitalSearchOptions digitalOptions = new DigitalSearchOptions
                    {
                        AllPages = true
                    };

                    // Define search options for barcode signatures
                    BarcodeSearchOptions barcodeOptions = new BarcodeSearchOptions
                    {
                        AllPages = true
                    };

                    // Define search options for QR code signatures
                    QrCodeSearchOptions qrCodeOptions = new QrCodeSearchOptions
                    {
                        AllPages = true
                    };

                    // Define search options for metadata signatures
                    MetadataSearchOptions metadataOptions = new MetadataSearchOptions();

                    // Create a list to hold all search options
                    List<SearchOptions> searchOptions = new List<SearchOptions>
                    {
                        textOptions,
                        digitalOptions,
                        barcodeOptions,
                        qrCodeOptions,
                        metadataOptions
                    };

                    // Search for all signature types
                    SearchResult result = signature.Search(searchOptions);

                    // Check if signatures were found
                    if (result.Signatures.Count > 0)
                    {
                        Console.WriteLine($"\nSource document ['{filePath}'] contains {result.Signatures.Count} signature(s):");
                        
                        // Process results by signature type
                        foreach (var foundSignature in result.Signatures)
                        {
                            Console.WriteLine($"Signature found: Type: {foundSignature.SignatureType}, Page: {foundSignature.PageNumber}");
                            
                            // Process specific signature types
                            switch (foundSignature.SignatureType)
                            {
                                case SignatureType.Text:
                                    var textSignature = foundSignature as TextSignature;
                                    Console.WriteLine($"Text: '{textSignature.Text}'");
                                    break;
                                    
                                case SignatureType.Barcode:
                                    var barcodeSignature = foundSignature as BarcodeSignature;
                                    Console.WriteLine($"Barcode Type: {barcodeSignature.EncodeType.TypeName}, Text: '{barcodeSignature.Text}'");
                                    break;
                                    
                                case SignatureType.QrCode:
                                    var qrCodeSignature = foundSignature as QrCodeSignature;
                                    Console.WriteLine($"QR Code Type: {qrCodeSignature.EncodeType.TypeName}, Text: '{qrCodeSignature.Text}'");
                                    break;
                                    
                                case SignatureType.Digital:
                                    var digitalSignature = foundSignature as DigitalSignature;
                                    Console.WriteLine($"Certificate: {digitalSignature.Certificate?.SubjectName}, Valid: {digitalSignature.IsValid}");
                                    break;
                                    
                                case SignatureType.Metadata:
                                    var metadataSignature = foundSignature as MetadataSignature;
                                    Console.WriteLine($"Metadata: Name: {metadataSignature.Name}, Value: {metadataSignature.Value}");
                                    break;
                            }
                            
                            Console.WriteLine(); // Add line break between signatures
                        }
                    }
                    else
                    {
                        Console.WriteLine("No signatures were found in the document.");
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

## Advanced Multi-Signature Search Techniques

### Filtering Search Results

You can implement advanced filtering to narrow down search results:

```csharp
// Filter results by page number
var signaturesOnFirstPage = result.Signatures.FindAll(s => s.PageNumber == 1);

// Filter results by signature type
var digitalSignatures = result.Signatures.FindAll(s => s.SignatureType == SignatureType.Digital);
var qrCodeSignatures = result.Signatures.FindAll(s => s.SignatureType == SignatureType.QrCode);

// Filter text signatures containing specific content
var approvalSignatures = result.Signatures
    .FindAll(s => s is TextSignature && ((TextSignature)s).Text.Contains("Approved"));
```

### Validating Multiple Signatures

Implement validation logic for different signature types:

```csharp
bool ValidateAllSignatures(SearchResult result)
{
    bool isDocumentValid = true;
    
    // Check if document has a valid digital signature
    bool hasValidDigitalSignature = result.Signatures
        .Any(s => s is DigitalSignature && ((DigitalSignature)s).IsValid);
    
    if (!hasValidDigitalSignature)
    {
        Console.WriteLine("Warning: Document does not contain a valid digital signature");
        isDocumentValid = false;
    }
    
    // Check if document has required QR code
    bool hasRequiredQRCode = result.Signatures
        .Any(s => s is QrCodeSignature && ((QrCodeSignature)s).Text.Contains("Auth-Code"));
    
    if (!hasRequiredQRCode)
    {
        Console.WriteLine("Warning: Document does not contain the required authentication QR code");
        isDocumentValid = false;
    }
    
    return isDocumentValid;
}
```

### Searching with Custom Processing

You can define custom processing logic for search operations:

```csharp
// Create search options with custom processing
TextSearchOptions textOptions = new TextSearchOptions
{
    AllPages = true,
    
    // Define custom processing using a delegate
    ProcessCompleted = (signature) =>
    {
        // Custom validation logic - accept only signatures on specified pages
        TextSignature textSignature = signature as TextSignature;
        return textSignature != null && (textSignature.PageNumber == 1 || textSignature.PageNumber == 2);
    }
};
```

## Conclusion

In this comprehensive guide, we've explored how to search for multiple signature types within documents using GroupDocs.Signature for .NET. From setting up search options for different signature types to processing and validating the results, you now have the knowledge to implement robust signature search functionality in your .NET applications.

The ability to search for multiple signature types simultaneously enhances document verification processes, strengthens security measures, and streamlines document validation workflows. GroupDocs.Signature provides a powerful, flexible framework for working with various signature types across different document formats, making it an excellent choice for document processing applications.

## FAQ's

### Can I search for signatures in password-protected documents?

Yes, GroupDocs.Signature supports searching for signatures in password-protected documents. You can provide the password when initializing the `Signature` object:

```csharp
LoadOptions loadOptions = new LoadOptions { Password = "your_password" };
using (Signature signature = new Signature(filePath, loadOptions))
{
    // Search for signatures
}
```

### Which document formats are supported for signature searching?

GroupDocs.Signature supports a wide range of document formats, including PDF, Microsoft Office documents (Word, Excel, PowerPoint), OpenOffice formats, images, and more.

### Can I limit the search to specific pages in a document?

Yes, each search option type has properties that allow you to specify which pages to search:

```csharp
TextSearchOptions options = new TextSearchOptions
{
    AllPages = false,  // Don't search all pages
    PageNumber = 1,    // Search only on page 1
    
    // Or specify multiple pages
    PagesSetup = new PagesSetup { Pages = new List<int> { 1, 3, 5 } }
};
```

### How can I optimize performance when searching in large documents?

For large documents, you can optimize performance by:

1. Limiting the search to specific pages or page ranges
2. Using more specific search criteria to reduce the number of potential matches
3. Implementing pagination in your results display
4. Searching for one signature type at a time if you don't need simultaneous results

### Can I extend GroupDocs.Signature to support custom signature types?

While GroupDocs.Signature provides built-in support for common signature types, you can extend its functionality by:

1. Creating custom search options classes derived from `SearchOptions`
2. Implementing custom processing logic using the `ProcessCompleted` delegate
3. Developing wrapper classes that combine multiple signature searches with advanced business logic

## See Also

* [API Reference](https://reference.groupdocs.com/signature/net/)
* [Code Examples on GitHub](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
* [Product Documentation](https://docs.groupdocs.com/signature/net/)
* [Product Page](https://products.groupdocs.com/signature/net/)
* [Download Latest Version](https://releases.groupdocs.com/signature/net/)
* [Blog Articles](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
* [Free Support Forum](https://forum.groupdocs.com/c/signature/13)
* [Temporary License](https://purchase.groupdocs.com/temporary-license/)