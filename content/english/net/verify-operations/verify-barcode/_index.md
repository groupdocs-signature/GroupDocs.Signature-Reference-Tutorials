---
title: Verify Barcode Signatures in Documents
linktitle: Verify Barcode
second_title: GroupDocs.Signature .NET API
description: Implement robust barcode verification in .NET applications with GroupDocs.Signature. Complete code examples and best practices for ensuring document authenticity.
weight: 10
url: /net/verify-operations/verify-barcode/
---

## Introduction

Barcodes have become an integral part of modern document management systems, enabling quick access to encoded information while also serving as a security feature. GroupDocs.Signature for .NET provides a powerful API for verifying barcode signatures within documents, ensuring their authenticity and integrity.

This comprehensive tutorial explores the process of implementing barcode verification in .NET applications using GroupDocs.Signature. Whether you're working with business documents, certificates, contracts, or any document type that utilizes barcodes for authentication, this guide will help you implement robust verification functionality.

## Prerequisites

Before implementing barcode verification functionality, ensure you have the following prerequisites in place:

1. GroupDocs.Signature for .NET: Download and install the library from the [download page](https://releases.groupdocs.com/signature/net/).
2. .NET Development Environment: Visual Studio or any compatible .NET development environment.
3. Basic Knowledge: Familiarity with C# programming and .NET framework concepts.
4. Test Document: A document containing barcode signatures for verification purposes.

## Import Required Namespaces

Start by importing the necessary namespaces to access the GroupDocs.Signature functionality:

```csharp
using System;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

Let's break down the barcode verification process into clear, manageable steps:

## Step 1: Specify the Document Path

```csharp
// Path to the document containing barcode signatures
string filePath = "sample_multiple_signatures.docx";
```

Ensure you replace the example path with the actual path to your document containing barcode signatures.

## Step 2: Initialize the Signature Object

```csharp
// Create an instance of Signature class by passing document path
using (Signature signature = new Signature(filePath))
{
    // Verification code will be implemented here
}
```

The Signature class is the main entry point for all operations in the GroupDocs.Signature API.

## Step 3: Configure Barcode Verification Options

```csharp
// Define barcode verification options
BarcodeVerifyOptions options = new BarcodeVerifyOptions()
{
    AllPages = true,           // Check all pages of the document
    Text = "12345",            // Text to match within the barcode
    MatchType = TextMatchType.Contains // Specify text matching criteria
};
```

The verification options allow you to define specific criteria for the verification process:
- `AllPages`: Set to true to check all document pages
- `Text`: The text content to match within the barcode
- `MatchType`: The method for text matching (Contains, Exact, StartsWith, EndsWith)

## Step 4: Execute Verification Process

```csharp
// Perform verification
VerificationResult result = signature.Verify(options);
```

This executes the verification process based on the options you've specified.

## Step 5: Process Verification Results

```csharp
// Check verification result and process accordingly
if (result.IsValid)
{
    Console.WriteLine($"Document {filePath} contains valid barcode signatures!");
    
    // Display information about successful signatures
    foreach (BarcodeSignature barcodeSignature in result.Succeeded)
    {
        Console.WriteLine($"\nFound valid barcode signature:");
        Console.WriteLine($"Text: {barcodeSignature.Text}");
        Console.WriteLine($"Type: {barcodeSignature.EncodeType.TypeName}");
        Console.WriteLine($"Location: Page {barcodeSignature.PageNumber}, {barcodeSignature.Left}x{barcodeSignature.Top}");
    }
}
else
{
    Console.WriteLine($"Document {filePath} failed verification process.");
    Console.WriteLine($"Number of failed signatures: {result.Failed.Count}");
}
```

This code checks if the verification was successful and provides detailed information about the barcode signatures that were verified.

## Complete Example

Here's a complete working example that demonstrates barcode verification:

```csharp
using System;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;

namespace GroupDocs.Signature.Examples
{
    class Program
    {
        static void Main(string[] args)
        {
            // Document path
            string filePath = "sample_multiple_signatures.docx";
            
            try
            {
                // Initialize Signature instance
                using (Signature signature = new Signature(filePath))
                {
                    // Setup verification options
                    BarcodeVerifyOptions options = new BarcodeVerifyOptions()
                    {
                        AllPages = true,
                        Text = "12345",
                        MatchType = TextMatchType.Contains
                    };
                    
                    // Verify document signatures
                    VerificationResult result = signature.Verify(options);
                    
                    // Process verification results
                    if (result.IsValid)
                    {
                        Console.WriteLine($"Document {filePath} contains valid barcode signatures!");
                        
                        foreach (BarcodeSignature item in result.Succeeded)
                        {
                            Console.WriteLine($"\nValid signature found with text: {item.Text}");
                            Console.WriteLine($"Barcode type: {item.EncodeType.TypeName}");
                            Console.WriteLine($"Page: {item.PageNumber}");
                        }
                    }
                    else
                    {
                        Console.WriteLine($"\nDocument {filePath} failed verification process.");
                    }
                }
            }
            catch (Exception ex)
            {
                Console.WriteLine($"Error: {ex.Message}");
            }
        }
    }
}
```

## Advanced Verification Scenarios

GroupDocs.Signature provides additional options for more complex verification scenarios:

### Verifying Specific Barcode Types

If you know the specific barcode type you're looking for, you can restrict verification to that type:

```csharp
BarcodeVerifyOptions options = new BarcodeVerifyOptions()
{
    EncodeType = BarcodeTypes.Code128,  // Verify only Code128 barcodes
    Text = "PROD-12345",
    MatchType = TextMatchType.Exact
};
```

### Verifying Barcodes on Specific Pages

For multi-page documents, you can limit verification to specific pages:

```csharp
BarcodeVerifyOptions options = new BarcodeVerifyOptions()
{
    AllPages = false,
    PageNumber = 2,  // Verify only on page 2
    Text = "INV-2023"
};
```

### Using Regular Expressions for Verification

For more flexible pattern matching, you can use regular expressions:

```csharp
BarcodeVerifyOptions options = new BarcodeVerifyOptions()
{
    Text = "INV-\\d{4}-\\d{2}",  // Match invoice numbers like INV-2023-01
    MatchType = TextMatchType.Regex
};
```

### Verifying Multiple Barcode Types Simultaneously

You can create multiple verification options to check for different barcode types:

```csharp
// Create a list of verification options
List<VerifyOptions> listOptions = new List<VerifyOptions>();

// Add QR Code verification
listOptions.Add(new BarcodeVerifyOptions()
{
    EncodeType = BarcodeTypes.QR,
    Text = "Security"
});

// Add Code128 verification
listOptions.Add(new BarcodeVerifyOptions()
{
    EncodeType = BarcodeTypes.Code128,
    Text = "12345"
});

// Verify with multiple options
VerificationResult result = signature.Verify(listOptions);
```

## Best Practices for Barcode Verification

1. Error Handling: Always implement proper error handling to manage unexpected scenarios gracefully.
2. Performance Optimization: For large documents, consider verifying specific pages rather than the entire document.
3. Logging: Implement logging to track verification attempts and results for auditing purposes.
4. Security Considerations: Store verification criteria securely, especially if they're part of your security infrastructure.
5. Testing: Test verification with various document formats and barcode types to ensure compatibility.

## Troubleshooting Common Issues

### Barcode Not Detected
- Ensure the barcode is clearly visible in the document
- Check if the barcode type is supported by GroupDocs.Signature
- Verify that the barcode is not distorted or damaged

### Verification Failures
- Confirm that the verification criteria (text, barcode type) are correct
- Check if the MatchType is appropriate for your use case
- Verify that the document hasn't been modified since the barcode was applied

### Performance Issues
- Optimize verification by targeting specific pages where barcodes are expected
- Limit the verification to specific barcode types if known in advance

## Conclusion

Barcode verification is an essential tool for ensuring document authenticity and integrity in modern document management systems. GroupDocs.Signature for .NET provides a comprehensive and easy-to-use API for implementing robust barcode verification functionality in your .NET applications.

By following this step-by-step guide, you've learned how to:
- Configure and initialize the verification process
- Specify various verification criteria
- Process and interpret verification results
- Implement advanced verification scenarios

These capabilities allow you to build secure and reliable document processing systems that can verify the authenticity of barcodes across various document formats.

## FAQs

### Which document formats are supported for barcode verification?
GroupDocs.Signature supports a wide range of document formats including PDF, Word documents (DOC, DOCX), Excel spreadsheets (XLS, XLSX), PowerPoint presentations (PPT, PPTX), images, and more.

### Can GroupDocs.Signature verify multiple barcodes in a single document?
Yes, GroupDocs.Signature can verify multiple barcodes within a single document. The verification results will include all matching barcodes.

### Which barcode types are supported for verification?
GroupDocs.Signature supports numerous barcode types including Code39, Code128, EAN13, EAN8, QR Code, DataMatrix, PDF417, and many others.

### Can I verify barcodes in password-protected documents?
Yes, GroupDocs.Signature provides options to specify document passwords when opening protected documents for verification.

### Is it possible to verify barcodes that contain binary data instead of text?
Yes, GroupDocs.Signature provides options for verifying barcodes with binary data through the `BinaryData` property of the verification options.

### Related Resources
* [GroupDocs.Signature API Reference](https://reference.groupdocs.com/signature/net/)
* [GroupDocs.Signature Downloads](https://releases.groupdocs.com/signature/net/)
* [Code Examples on GitHub](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
* [Documentation](https://docs.groupdocs.com/signature/net/)
* [Product Page](https://products.groupdocs.com/signature/net/)
* [Blog Articles](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
* [Support Forum](https://forum.groupdocs.com/c/signature/13)
* [Temporary License](https://purchase.groupdocs.com/temporary-license/)