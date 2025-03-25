---
title: Verify QR Code in Documents
linktitle: Verify QR Code
second_title: GroupDocs.Signature .NET API
description: Learn how to verify QR codes in documents using GroupDocs.Signature for .NET. Complete guide with code examples and best practices for document authentication.
weight: 12
url: /net/verify-operations/verify-qr-code/
---

## Introduction

Document security is a critical aspect of modern business operations. QR codes have become an increasingly popular method for embedding information within documents that can be verified for authenticity. GroupDocs.Signature for .NET provides a powerful and flexible solution for verifying QR codes embedded within documents across various formats.

This comprehensive tutorial will guide you through the process of implementing QR code verification in your .NET applications, ensuring your documents maintain their integrity and authenticity.

## Prerequisites

Before implementing QR code verification functionality, ensure you have the following prerequisites:

1. GroupDocs.Signature for .NET: Download and install the library from the [download page](https://releases.groupdocs.com/signature/net/).
2. Development Environment: Visual Studio or any compatible .NET development environment.
3. Test Document: A document containing QR code signatures for verification purposes.
4. Basic Knowledge: Familiarity with C# programming and .NET framework concepts.

## Import Namespaces

Start by importing the required namespaces to access the GroupDocs.Signature functionality:

```csharp
using System;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

## Step-by-Step QR Code Verification Process

Follow these detailed steps to verify QR codes within your documents:

### Step 1: Specify the Document Path

```csharp
// Provide the path to the document containing QR code signatures
string filePath = "sample_multiple_signatures.docx";
```

Ensure you replace the example path with the actual path to your document.

### Step 2: Initialize the Signature Object

```csharp
// Create a Signature instance by passing the document path
using (Signature signature = new Signature(filePath))
{
    // Verification code will be implemented here
}
```

The Signature class is the main entry point for all operations in the GroupDocs.Signature API.

### Step 3: Configure QR Code Verification Options

```csharp
// Define QR code verification options
QrCodeVerifyOptions options = new QrCodeVerifyOptions()
{
    AllPages = true, // Check all pages of the document
    Text = "John",   // Text to verify within the QR code
    MatchType = TextMatchType.Contains // Specify the text matching criteria
};
```

The verification options allow you to define specific criteria for the verification process:
- `AllPages`: Set to true to check all document pages (default behavior)
- `Text`: The text content to match within the QR code
- `MatchType`: The method for text matching (Contains, Exact, StartsWith, etc.)

### Step 4: Execute Verification Process

```csharp
// Perform verification
VerificationResult result = signature.Verify(options);
```

This executes the verification process based on the options you've specified.

### Step 5: Process Verification Results

```csharp
// Check verification result and process accordingly
if (result.IsValid)
{
    Console.WriteLine($"Document {filePath} contains valid QR code signature!");
    
    // Display information about successful signatures
    foreach (QrCodeSignature signature in result.Succeeded)
    {
        Console.WriteLine($"Found valid QR Code signature with text: {signature.Text}");
        Console.WriteLine($"QR Code type: {signature.EncodeType.TypeName}");
        Console.WriteLine($"Location: Page {signature.PageNumber}, {signature.Left}x{signature.Top}");
    }
}
else
{
    Console.WriteLine($"Document {filePath} failed verification process.");
    Console.WriteLine($"Number of failed signatures: {result.Failed.Count}");
}
```

Properly handling the verification result allows your application to take appropriate actions based on the verification outcome.

## Complete Example

Here's a complete, working example that demonstrates QR code verification:

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
            
            // Initialize Signature instance
            using (Signature signature = new Signature(filePath))
            {
                // Setup verification options
                QrCodeVerifyOptions options = new QrCodeVerifyOptions()
                {
                    AllPages = true,
                    Text = "John",
                    MatchType = TextMatchType.Contains
                };
                
                // Verify document signatures
                VerificationResult result = signature.Verify(options);
                
                // Process verification results
                if (result.IsValid)
                {
                    Console.WriteLine($"Document {filePath} contains valid QR code signature!");
                    
                    foreach (QrCodeSignature qrSignature in result.Succeeded)
                    {
                        Console.WriteLine($"Found valid QR Code with text: {qrSignature.Text}");
                    }
                }
                else
                {
                    Console.WriteLine($"Document {filePath} failed verification process.");
                }
            }
        }
    }
}
```

## Advanced Verification Options

GroupDocs.Signature provides additional options for more complex verification scenarios:

### Verifying Specific QR Code Types

```csharp
QrCodeVerifyOptions options = new QrCodeVerifyOptions()
{
    EncodeType = QrCodeTypes.QR,  // Verify only standard QR codes
    Text = "Confidential",
    MatchType = TextMatchType.Exact
};
```

### Verifying on Specific Pages

```csharp
QrCodeVerifyOptions options = new QrCodeVerifyOptions()
{
    AllPages = false,
    PageNumber = 2,  // Verify only on page 2
    Text = "Approved"
};
```

### Using Regular Expressions for Verification

```csharp
QrCodeVerifyOptions options = new QrCodeVerifyOptions()
{
    Text = "INV-\\d{6}",  // Match invoice numbers (e.g., INV-123456)
    MatchType = TextMatchType.Regex
};
```

## Best Practices for QR Code Verification

1. Always validate inputs: Ensure document paths and verification criteria are valid before processing.
2. Implement error handling: Use try-catch blocks to handle potential exceptions during verification.
3. Consider performance: For large documents, consider verifying specific pages rather than the entire document.
4. Log verification results: Maintain logs of verification processes for audit purposes.
5. Test with various document formats: Ensure your verification works across all required document formats.

## Conclusion

Verifying QR codes in documents is an essential aspect of ensuring document authenticity and integrity. GroupDocs.Signature for .NET provides a comprehensive and user-friendly API for implementing QR code verification in your .NET applications.

By following this tutorial, you've learned how to:
- Configure and initialize the verification process
- Specify various verification criteria
- Process and interpret verification results
- Implement advanced verification options

This knowledge empowers you to enhance the security and reliability of your document management systems.

## FAQ's

### Can GroupDocs.Signature verify multiple QR codes in a single document?
Yes, GroupDocs.Signature can verify multiple QR codes within a single document. The verification results will include all matching QR codes.

### Which document formats are supported for QR code verification?
GroupDocs.Signature supports a wide range of document formats including PDF, Word (DOC, DOCX), Excel (XLS, XLSX), PowerPoint (PPT, PPTX), images, and more.

### Can I verify QR codes with specific encryption or formatting?
Yes, GroupDocs.Signature provides options to verify QR codes with specific encoding types and content formatting patterns.

### Is it possible to verify QR codes created by third-party applications?
Yes, GroupDocs.Signature can verify standard QR codes generated by most applications, as long as they follow standard QR code formats.

### How do I handle QR codes that contain binary data instead of text?
GroupDocs.Signature provides options for verifying QR codes with binary data through the `BinaryData` property of the verification options.

### Related Resources
* [GroupDocs.Signature API Reference](https://reference.groupdocs.com/signature/net/)
* [GroupDocs.Signature Downloads](https://releases.groupdocs.com/signature/net/)
* [Code Examples on GitHub](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
* [Documentation](https://docs.groupdocs.com/signature/net/)
* [Product Page](https://products.groupdocs.com/signature/net/)
* [Blog Articles](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
* [Support Forum](https://forum.groupdocs.com/c/signature/13)
* [Temporary License](https://purchase.groupdocs.com/temporary-license/)