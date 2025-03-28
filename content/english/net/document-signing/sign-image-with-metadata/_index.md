---
title: Sign Images with Metadata in C# .NET
linktitle: Sign Image with Metadata
second_title: GroupDocs.Signature .NET API
description: Learn how to sign and embed metadata in images using GroupDocs.Signature for .NET. Add author info, timestamps, and custom data to enhance image authenticity and traceability.
weight: 10
url: /net/document-signing/sign-image-with-metadata/
---

## Introduction

Digital image signing with metadata is becoming increasingly important for establishing authenticity, ownership, and traceability. GroupDocs.Signature for .NET provides a powerful, yet easy-to-use solution for adding metadata signatures to various image formats. This tutorial guides you through the complete process of signing images with metadata using C#.

Metadata signatures allow you to embed valuable information directly into image files, such as author information, creation timestamps, unique identifiers, and more. This information becomes part of the image file itself, providing a reliable method to track and verify image authenticity.

## Prerequisites

Before proceeding with this tutorial, ensure you have the following:

1. [GroupDocs.Signature for .NET](https://releases.groupdocs.com/signature/net/) - Download and install the library
2. Development Environment - Visual Studio or any compatible IDE with .NET support
3. Image File - A sample image file in a supported format (PNG, JPG, TIFF, etc.)
4. Basic C# Programming Knowledge - Familiarity with C# programming concepts

## Import Namespaces

Start by importing the necessary namespaces to access GroupDocs.Signature functionality:

```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

## Step 1: Set Up File Paths

Define the paths for your source image and where the signed output should be saved:

```csharp
// Specify the path to your source image file
string filePath = "sample.png";

// Define the output directory and filename for the signed image
string outputDirectory = "Your Document Directory";
string outputFilePath = Path.Combine(outputDirectory, "SignImageWithMetadata", "SignedWithMetadata.png");

// Ensure the output directory exists
Directory.CreateDirectory(Path.GetDirectoryName(outputFilePath));
```

## Step 2: Initialize the Signature Object

Create an instance of the Signature class with your source image file:

```csharp
using (Signature signature = new Signature(filePath))
{
    // The rest of the code will go here
}
```

## Step 3: Create and Configure Metadata Signatures

Next, define the metadata that you want to embed in the image. GroupDocs.Signature supports various data types for metadata:

```csharp
// Initialize metadata ID (specific to image format)
ushort imgsMetadataId = 41996;

// Create metadata options object
MetadataSignOptions options = new MetadataSignOptions();

// Add various types of metadata signatures
options
    .Add(new ImageMetadataSignature(imgsMetadataId++, "Mr.Sherlock Holmes"))  // String value
    .Add(new ImageMetadataSignature(imgsMetadataId++, DateTime.Now))          // Date Time value
    .Add(new ImageMetadataSignature(imgsMetadataId++, 123456))                // Integer value
    .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456D))              // Double value
    .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456M))              // Decimal value
    .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456F));             // Float value
```

## Step 4: Sign the Image with Metadata

Apply the metadata signatures to the image and save the result:

```csharp
// Sign the document and save to the output file path
SignResult result = signature.Sign(outputFilePath, options);

// Display success message
Console.WriteLine($"\nSource image signed successfully with {result.Succeeded.Count} metadata signature(s).");
Console.WriteLine($"Signed image saved at: {outputFilePath}");
```

## Complete Example

Here's the complete code example that brings all steps together:

```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;

namespace SignImageWithMetadataExample
{
    class Program
    {
        static void Main(string[] args)
        {
            // Specify file paths
            string filePath = "sample.png";            
            string outputFilePath = Path.Combine("Your Document Directory", "SignImageWithMetadata", "SignedWithMetadata.png");
            
            // Ensure the output directory exists
            Directory.CreateDirectory(Path.GetDirectoryName(outputFilePath));

            // Sign the image with metadata
            using (Signature signature = new Signature(filePath))
            {
                // Initialize metadata ID (specific to image format)
                ushort imgsMetadataId = 41996;
                
                // Create metadata options
                MetadataSignOptions options = new MetadataSignOptions();
                
                // Add different types of metadata signatures
                options
                    .Add(new ImageMetadataSignature(imgsMetadataId++, "Mr.Sherlock Holmes")) // String value
                    .Add(new ImageMetadataSignature(imgsMetadataId++, DateTime.Now))          // Date Time value
                    .Add(new ImageMetadataSignature(imgsMetadataId++, 123456))                // Integer value
                    .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456D))              // Double value
                    .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456M))              // Decimal value
                    .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456F));             // Float value
                
                // Sign document and save to file
                SignResult result = signature.Sign(outputFilePath, options);
                
                // Display results
                Console.WriteLine($"\nSource image signed successfully with {result.Succeeded.Count} signature(s).");
                Console.WriteLine($"File saved at {outputFilePath}.");
            }
        }
    }
}
```

## Advanced Metadata Signing Techniques

### Working with Custom Metadata

You can also create custom metadata fields with specific IDs:

```csharp
// Create custom metadata with specific ID
options.Add(new ImageMetadataSignature(42000, "CustomValue"));
```

### Verifying Metadata Signatures

After signing, you may want to verify the metadata signatures:

```csharp
// Create verification options
MetadataSearchOptions searchOptions = new MetadataSearchOptions();

// Search for metadata signatures
SearchResult result = signature.Search(searchOptions);

// Display found signatures
Console.WriteLine($"Found {result.Signatures.Count} metadata signatures:");
foreach(var metadataSignature in result.Signatures)
{
    Console.WriteLine($"- {metadataSignature.Name}: {metadataSignature.Value}");
}
```

## Conclusion

In this tutorial, you've learned how to sign images with metadata using GroupDocs.Signature for .NET. Embedding metadata into images provides an excellent way to enhance image authenticity, add critical information, and improve document management workflows. The process is straightforward yet powerful, allowing for customization based on your specific requirements.

The metadata embedded in the image file can be used for various purposes such as copyright protection, tracking image origin, adding descriptive information, and establishing digital chain of custody. By implementing metadata signatures, you can ensure your images maintain their integrity and authenticity throughout their lifecycle.

## FAQ's

### Can I add metadata to existing signed images?

Yes, you can add additional metadata to images that already contain metadata signatures. The existing metadata will be preserved, and new metadata will be added accordingly.

### Which image formats are supported for metadata signing?

GroupDocs.Signature for .NET supports metadata signing for various image formats, including PNG, JPEG, TIFF, BMP, GIF, and more. For a complete list, refer to the [official documentation](https://docs.groupdocs.com/signature/net/).

### Is it possible to encrypt the metadata in images?

Yes, GroupDocs.Signature provides options to encrypt metadata for enhanced security. You can use the encryption options provided by the library to protect sensitive metadata information.

### Can I programmatically validate the authenticity of signed images?

Absolutely. You can use the verification methods in GroupDocs.Signature to validate metadata signatures and confirm the authenticity of signed images.

### Is there a file size limitation when signing images with metadata?

There's no specific file size limitation imposed by the library itself, but very large files might require more processing time and memory. It's recommended to consider system resources when working with extremely large images.

### How can I get a temporary license for testing purposes?

You can obtain a [temporary license](https://purchase.groupdocs.com/temporary-license/) for testing GroupDocs.Signature before making a purchase.

### Where can I find more resources and support?

- [API Reference](https://reference.groupdocs.com/signature/net/)
- [Downloads](https://releases.groupdocs.com/signature/net/)
- [Examples](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
- [Documentation](https://docs.groupdocs.com/signature/net/)
- [Product Page](https://products.groupdocs.com/signature/net/)
- [Blog](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
- [Support Forum](https://forum.groupdocs.com/c/signature/13)