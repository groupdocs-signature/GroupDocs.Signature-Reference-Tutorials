---
title: Search for Text Signatures in Documents
linktitle: Search for Text Signatures
second_title: GroupDocs.Signature .NET API
description: Learn how to efficiently search for text signatures in documents using GroupDocs.Signature for .NET with our comprehensive step-by-step guide and code examples.
weight: 16
url: /net/signature-searching/search-for-text-signatures/
---

## Introduction

Text signatures are a common method of indicating document authorship, approval, or verification. In digital document management, the ability to programmatically search for and extract text signatures is crucial for document validation, workflow automation, and compliance verification. GroupDocs.Signature for .NET offers a comprehensive solution for implementing text signature search functionality in your .NET applications, supporting various document formats and advanced search capabilities.

This tutorial will guide you through the process of searching for text signatures in documents using GroupDocs.Signature for .NET, providing detailed explanations, step-by-step instructions, and practical code examples.

## Prerequisites

Before diving into text signature searching, ensure you have the following prerequisites:

1. GroupDocs.Signature for .NET Library: Download and install the library from the [releases page](https://releases.groupdocs.com/signature/net/).

2. Development Environment: Set up a suitable development environment such as Visual Studio or any compatible IDE with .NET support.

3. Sample Documents: Prepare test documents containing text signatures for verification and testing.

4. Basic C# Knowledge: Familiarity with C# programming language and .NET framework concepts.

## Import Namespaces

Begin by importing the necessary namespaces to access GroupDocs.Signature functionality:

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

Now, let's break down the process of searching for text signatures into clear, manageable steps:

## Step 1: Load the Document

First, define the document path and initialize a `Signature` object:

```csharp
string filePath = "sample_multiple_signatures.docx";
string fileName = Path.GetFileName(filePath);

using (Signature signature = new Signature(filePath))
{
    // Text signature search code will be added here
}
```

## Step 2: Configure Search Options

Create and configure `TextSearchOptions` to specify how text signatures should be searched:

```csharp
// Configure text search options
TextSearchOptions options = new TextSearchOptions
{
    // Search on all pages
    AllPages = true,
    
    // Optional: specify text to match
    // Text = "Approved",
    
    // Optional: specify match type
    // MatchType = TextMatchType.Contains
};
```

## Step 3: Perform Text Signature Search

Execute the search operation using the configured options:

```csharp
// Search for text signatures
List<TextSignature> signatures = signature.Search<TextSignature>(options);
```

## Step 4: Process and Display Results

Iterate through the found text signatures and display their details:

```csharp
// Display search results
Console.WriteLine($"\nSource document '{fileName}' contains {signatures.Count} text signature(s):");

foreach (TextSignature textSignature in signatures)
{
    Console.WriteLine($"Text signature found at page {textSignature.PageNumber} with text '{textSignature.Text}'");
    Console.WriteLine($"Location: X={textSignature.Left}, Y={textSignature.Top}, Width={textSignature.Width}, Height={textSignature.Height}");
    Console.WriteLine($"Signature type: {textSignature.SignatureImplementation}");
    Console.WriteLine();
}
```

## Complete Example

Here's a complete working example that demonstrates how to search for text signatures in a document:

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
            // Document path - update with your file path
            string filePath = "sample_multiple_signatures.docx";
            string fileName = Path.GetFileName(filePath);
            
            // Initialize Signature instance
            using (Signature signature = new Signature(filePath))
            {
                try
                {
                    // Configure text search options
                    TextSearchOptions options = new TextSearchOptions
                    {
                        // Search on all pages
                        AllPages = true
                    };
                    
                    // Search for text signatures
                    List<TextSignature> signatures = signature.Search<TextSignature>(options);
                    
                    // Display search results
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

## Advanced Text Signature Search Techniques

### Searching with Specific Text Criteria

For more targeted searches, you can customize the `TextSearchOptions` to filter by specific text content:

```csharp
// Create search options with specific text criteria
TextSearchOptions options = new TextSearchOptions
{
    // Search on all pages
    AllPages = true,
    
    // Search for specific text
    Text = "Approved",
    
    // Specify match type (Contains, Exact, StartsWith, EndsWith)
    MatchType = TextMatchType.Contains,
    
    // Case-sensitive search
    MatchCase = true
};
```

### Searching in Specific Document Areas

You can limit the search to specific areas of the document:

```csharp
// Create search options for a specific document area
TextSearchOptions options = new TextSearchOptions
{
    // Search only on specific pages
    AllPages = false,
    PageNumber = 1,
    
    // Or specify multiple pages
    PagesSetup = new PagesSetup { Pages = new List<int> { 1, 3, 5 } },
    
    // Define a specific area to search within
    Rectangle = new Rectangle(100, 100, 400, 200)
};
```

### Advanced Text Filtering

Implement custom filtering logic for more complex search requirements:

```csharp
// Create search options with custom processing
TextSearchOptions options = new TextSearchOptions
{
    AllPages = true,
    
    // Define custom processing using a delegate
    ProcessCompleted = (TextSignature signature) =>
    {
        // Custom validation logic
        bool isValid = signature.Text.Length > 5 && 
                      (signature.Text.Contains("Approved") || signature.Text.Contains("Verified"));
        
        return isValid;
    }
};
```

### Searching for Different Text Styles

Use font and style properties to filter text signatures:

```csharp
// Create search options targeting specific text appearance
TextSearchOptions options = new TextSearchOptions
{
    // Filter by font name
    FontName = "Arial",
    
    // Filter by font size range
    MinFontSize = 10,
    MaxFontSize = 14,
    
    // Filter by font color
    ForeColor = System.Drawing.Color.Blue
};
```

### Extracting Signature Metadata

Extract and process metadata associated with text signatures:

```csharp
foreach (TextSignature signature in signatures)
{
    // Access signature metadata
    if (signature.Metadata != null && signature.Metadata.Count > 0)
    {
        Console.WriteLine("Signature Metadata:");
        
        foreach (var item in signature.Metadata)
        {
            Console.WriteLine($"  {item.Key}: {item.Value}");
        }
    }
    
    // Check for signature creation and modification dates
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

## Conclusion

In this comprehensive guide, we have explored how to search for text signatures in documents using GroupDocs.Signature for .NET. From basic search operations to advanced techniques, you now have the knowledge to implement robust text signature functionality in your .NET applications.

GroupDocs.Signature provides a powerful and flexible framework for working with text signatures, enabling you to build sophisticated document verification systems, automated workflow solutions, and compliance validation tools.

## FAQ's

### Can I search for text signatures in password-protected documents?

Yes, GroupDocs.Signature supports searching for text signatures in password-protected documents. You can provide the password when initializing the `Signature` object:

```csharp
LoadOptions loadOptions = new LoadOptions { Password = "your_password" };
using (Signature signature = new Signature(filePath, loadOptions))
{
    // Search for text signatures
}
```

### Which document formats are supported for text signature searching?

GroupDocs.Signature supports a wide range of document formats including PDF, Microsoft Office documents (Word, Excel, PowerPoint), OpenOffice formats, images, and more.

### Can I search for text signatures with specific formatting like bold or italic?

Yes, you can search for text signatures with specific formatting by using the `FontBold` and `FontItalic` properties in `TextSearchOptions`:

```csharp
TextSearchOptions options = new TextSearchOptions
{
    FontBold = true,
    FontItalic = true
};
```

### How can I improve search performance for large documents?

For large documents, you can optimize search performance by:

1. Limiting the search to specific pages instead of searching the entire document
2. Using more specific search criteria to reduce the number of matches
3. Specifying a search area using the `Rectangle` property if you know where signatures are typically located
4. Implementing pagination in your application to process search results in batches

### Can I detect whether a text signature was electronically added or is part of the original document content?

GroupDocs.Signature can distinguish between different types of text elements in documents. The `SignatureImplementation` property of `TextSignature` indicates whether the text is a formal signature or regular document content. However, definitive determination may depend on how the text was originally added to the document.

## See Also

* [API Reference](https://reference.groupdocs.com/signature/net/)
* [Code Examples on GitHub](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
* [Product Documentation](https://docs.groupdocs.com/signature/net/)
* [Product Page](https://products.groupdocs.com/signature/net/)
* [Download Latest Version](https://releases.groupdocs.com/signature/net/)
* [Blog Articles](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
* [Free Support Forum](https://forum.groupdocs.com/c/signature/13)
* [Temporary License](https://purchase.groupdocs.com/temporary-license/)