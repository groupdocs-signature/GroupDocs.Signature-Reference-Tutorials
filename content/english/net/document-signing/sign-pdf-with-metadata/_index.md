---
title: Add Metadata Signatures to PDF Documents in C# .NET
linktitle: Sign PDF with Metadata
second_title: GroupDocs.Signature .NET API
description: Integrate metadata signatures into PDF documents using GroupDocs.Signature for .NET. Learn to embed author info, timestamps, and custom data to enhance PDF authenticity and traceability.
weight: 11
url: /net/document-signing/sign-pdf-with-metadata/
---

## Introduction

PDF (Portable Document Format) documents are widely used across industries due to their consistency and platform independence. Ensuring the authenticity and traceability of these documents is crucial in many professional environments. One effective way to achieve this is by embedding metadata into the PDF files themselves.

In this comprehensive tutorial, we'll explore how to sign PDF documents with metadata using GroupDocs.Signature for .NET. Metadata signatures allow you to embed additional information within the document, such as author details, creation timestamps, document identifiers, and custom values, without visibly altering the document's appearance.

## Prerequisites

Before we begin, make sure you have the following in place:

1. [GroupDocs.Signature for .NET](https://releases.groupdocs.com/signature/net/) - Download and install the library
2. Development Environment - Visual Studio or any other .NET-compatible IDE
3. PDF Document - A sample PDF file for signing
4. Basic C# Knowledge - Familiarity with C# programming language

## Import Namespaces

Start by importing the necessary namespaces to access the GroupDocs.Signature functionality:

```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

## Step 1: Set Up File Paths

First, define the path to your PDF document and specify where you want to save the signed output:

```csharp
// Specify the path to your PDF document
string filePath = "sample.pdf";

// Define output directory and file path
string outputDirectory = "Your Document Directory";
string outputFilePath = Path.Combine(outputDirectory, "SignPdfWithMetadata", "SignedWithMetadata.pdf");

// Ensure the output directory exists
Directory.CreateDirectory(Path.GetDirectoryName(outputFilePath));
```

## Step 2: Initialize the Signature Object

Create an instance of the Signature class with your source PDF document:

```csharp
using (Signature signature = new Signature(filePath))
{
    // The code for signing will go here
}
```

## Step 3: Define Metadata Options

Create and configure the metadata options, adding various types of metadata signatures:

```csharp
// Create metadata options object
MetadataSignOptions options = new MetadataSignOptions();

// Add various types of metadata using the fluent interface
options
    .Add(new PdfMetadataSignature("Author", "Mr.Sherlock Holmes")) // String value
    .Add(new PdfMetadataSignature("CreatedOn", DateTime.Now))       // DateTime value
    .Add(new PdfMetadataSignature("DocumentId", 123456))            // Integer value
    .Add(new PdfMetadataSignature("SignatureId", 123.456D))         // Double value
    .Add(new PdfMetadataSignature("Amount", 123.456M))              // Decimal value
    .Add(new PdfMetadataSignature("Total", 123.456F));              // Float value
```

## Step 4: Sign the PDF with Metadata

Apply the metadata signatures to the PDF document and save the result:

```csharp
// Sign the document and save to the output path
SignResult result = signature.Sign(outputFilePath, options);

// Display success message
Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} metadata signature(s).");
Console.WriteLine($"Signed document saved at: {outputFilePath}");
```

## Complete Example

Here's the complete code example that brings all steps together:

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
            // Specify file paths
            string filePath = "sample.pdf";
            string outputFilePath = Path.Combine("Your Document Directory", "SignPdfWithMetadata", "SignedWithMetadata.pdf");
            
            // Ensure the output directory exists
            Directory.CreateDirectory(Path.GetDirectoryName(outputFilePath));

            // Sign the PDF with metadata
            using (Signature signature = new Signature(filePath))
            {
                // Create metadata options object
                MetadataSignOptions options = new MetadataSignOptions();
                
                // Add different types of metadata signatures
                options
                    .Add(new PdfMetadataSignature("Author", "Mr.Sherlock Holmes")) // String value
                    .Add(new PdfMetadataSignature("CreatedOn", DateTime.Now))       // DateTime value
                    .Add(new PdfMetadataSignature("DocumentId", 123456))            // Integer value
                    .Add(new PdfMetadataSignature("SignatureId", 123.456D))         // Double value
                    .Add(new PdfMetadataSignature("Amount", 123.456M))              // Decimal value
                    .Add(new PdfMetadataSignature("Total", 123.456F));              // Float value
                
                // Sign document and save to file
                SignResult result = signature.Sign(outputFilePath, options);
                
                // Display results
                Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).");
                Console.WriteLine($"File saved at {outputFilePath}.");
            }
        }
    }
}
```

## Advanced PDF Metadata Operations

### Adding Custom Metadata with Namespace Support

PDF documents support custom metadata with XML namespace support:

```csharp
// Add custom metadata with namespace
options.Add(new PdfMetadataSignature("CustomProperty", "Custom Value")
{
    NamespaceUri = "http://your-namespace.com/schema"
});
```

### Searching for Metadata in Signed PDFs

After signing, you may want to verify or extract the metadata:

```csharp
// Create search options for metadata
MetadataSearchOptions searchOptions = new MetadataSearchOptions();

// Search for metadata signatures
SearchResult searchResult = signature.Search(searchOptions);

// Display found signatures
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

### Working with Standard PDF Metadata

PDF documents have standard metadata fields that can be accessed and modified:

```csharp
// Set standard PDF metadata fields
options
    .Add(new PdfMetadataSignature("Title", "Important Contract"))
    .Add(new PdfMetadataSignature("Subject", "Legal Agreement"))
    .Add(new PdfMetadataSignature("Keywords", "contract, agreement, legal, binding"))
    .Add(new PdfMetadataSignature("Creator", "Legal Department"))
    .Add(new PdfMetadataSignature("Producer", "GroupDocs.Signature"));
```

## Conclusion

In this tutorial, you've learned how to sign PDF documents with metadata using GroupDocs.Signature for .NET. Embedding metadata into PDF files provides an excellent way to enhance document authenticity, add critical information, and improve document management workflows.

Metadata signatures in PDFs are particularly valuable in business environments where document traceability and authenticity verification are essential. The embedded metadata can include information about the document's origin, author, creation time, version, and custom properties relevant to your organization's workflow.

By implementing metadata signatures with GroupDocs.Signature, you can ensure your PDF documents maintain their integrity and provide verifiable information throughout their lifecycle.

## FAQ's

### Can I modify existing metadata in a PDF document?

Yes, you can modify existing metadata in PDF documents. When you apply new metadata signatures with the same names as existing ones, the values will be updated accordingly.

### Are metadata signatures in PDF documents visible to the end-user?

Metadata signatures are not visible in the document content itself. However, they can be viewed through the document properties panel in PDF readers like Adobe Acrobat or using specialized tools for viewing metadata.

### Can I encrypt or protect the metadata in PDFs?

GroupDocs.Signature provides options for securing documents, including encryption. You can apply document-level encryption to protect the entire PDF, including its metadata.

### Is there a limit to how much metadata I can add to a PDF?

While there's no strict limit imposed by the PDF specification, adding excessive amounts of metadata may increase the file size. It's recommended to include only relevant and necessary information in the metadata.

### Can I programmatically validate if a PDF has been tampered with after adding metadata?

Yes, GroupDocs.Signature provides verification capabilities that can help detect if a document has been modified after signing, including changes to metadata.

### Where can I find more resources and support?

- [API Reference](https://reference.groupdocs.com/signature/net/)
- [Downloads](https://releases.groupdocs.com/signature/net/)
- [Examples](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
- [Documentation](https://docs.groupdocs.com/signature/net/)
- [Product Page](https://products.groupdocs.com/signature/net/)
- [Blog](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
- [Support Forum](https://forum.groupdocs.com/c/signature/13)
- [Temporary License](https://purchase.groupdocs.com/temporary-license/)