---
title: Verify Text Signatures in Documents
linktitle: Verify Text
second_title: GroupDocs.Signature .NET API
description: Master text signature verification in .NET applications with GroupDocs.Signature. Step-by-step implementation guide with complete code examples and best practices.
weight: 13
url: /net/verify-operations/verify-text/
---

## Introduction

Text signatures, while often simpler than digital or electronic signatures, play a crucial role in document management and verification. Whether it's watermarks, footer text, or specific content patterns, validating the presence and integrity of text signatures is an important aspect of document verification processes.

GroupDocs.Signature for .NET provides a powerful API for verifying text signatures within documents across a wide range of formats. This comprehensive tutorial will guide you through implementing text verification functionality in your .NET applications, ensuring your documents maintain their integrity and authenticity.

## Prerequisites

Before implementing text verification functionality, ensure you have the following prerequisites in place:

1. GroupDocs.Signature for .NET: Download and install the library from the [download page](https://releases.groupdocs.com/signature/net/).
2. .NET Development Environment: Visual Studio or any compatible .NET development environment.
3. Basic Knowledge: Familiarity with C# programming and .NET framework concepts.
4. Test Document: A document containing text signatures for verification purposes.

## Import Required Namespaces

Start by importing the necessary namespaces to access the GroupDocs.Signature functionality:

```csharp
using System;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

Let's break down the text verification process into clear, manageable steps:

## Step 1: Specify the Document Path

```csharp
// Path to the document containing text signatures
string filePath = "sample_multiple_signatures.docx";
```

Ensure you replace the example path with the actual path to your document containing text signatures.

## Step 2: Initialize the Signature Object

```csharp
// Create an instance of Signature class by passing document path
using (Signature signature = new Signature(filePath))
{
    // Verification code will be implemented here
}
```

The Signature class is the main entry point for all operations in the GroupDocs.Signature API.

## Step 3: Configure Text Verification Options

```csharp
// Define text verification options
TextVerifyOptions options = new TextVerifyOptions()
{
    AllPages = true,                               // Check all pages of the document
    SignatureImplementation = TextSignatureImplementation.Native,
    Text = "signature",                            // Text to be verified
    MatchType = TextMatchType.Contains             // Specify matching criteria
};
```

The verification options allow you to define specific criteria for the verification process:
- `AllPages`: Set to true to check all document pages
- `SignatureImplementation`: Specify how the text is implemented (Native or Sticker)
- `Text`: The text content to match within the document
- `MatchType`: The method for text matching (Contains, Exact, StartsWith, etc.)

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
    Console.WriteLine($"Document {filePath} contains valid text signatures!");
    
    // Display information about successful signatures
    foreach (TextSignature textSignature in result.Succeeded)
    {
        Console.WriteLine($"\nFound valid text signature:");
        Console.WriteLine($"Text: {textSignature.Text}");
        Console.WriteLine($"Location: Page {textSignature.PageNumber}, {textSignature.Left}x{textSignature.Top}");
    }
}
else
{
    Console.WriteLine($"Document {filePath} failed verification process.");
    Console.WriteLine($"Number of failed signatures: {result.Failed.Count}");
}
```

This code checks if the verification was successful and provides detailed information about the text signatures that were verified.

## Complete Example

Here's a complete working example that demonstrates text signature verification:

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
                    TextVerifyOptions options = new TextVerifyOptions()
                    {
                        AllPages = true,
                        SignatureImplementation = TextSignatureImplementation.Native,
                        Text = "signature",
                        MatchType = TextMatchType.Contains
                    };
                    
                    // Verify document signatures
                    VerificationResult result = signature.Verify(options);
                    
                    // Process verification results
                    if(result.IsValid)
                    {
                        Console.WriteLine($"\nDocument {filePath} was verified successfully!");
                        foreach (TextSignature item in result.Succeeded)
                        {
                            Console.WriteLine($"\nValid signature is found with text: {item.Text}");
                            Console.WriteLine($"Location: Page {item.PageNumber}, position {item.Left}x{item.Top}");
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

### Using Regular Expressions for Verification

For more flexible pattern matching, you can use regular expressions:

```csharp
TextVerifyOptions options = new TextVerifyOptions()
{
    Text = "Invoice\\s+#\\d{5,6}",  // Match patterns like "Invoice #12345"
    MatchType = TextMatchType.Regex
};
```

### Verifying Text in Specific Document Areas

You can restrict verification to specific areas of the document:

```csharp
TextVerifyOptions options = new TextVerifyOptions()
{
    AllPages = false,
    PageNumber = 1,  // Verify only on first page
    
    // Define area to search in (coordinates in points)
    PagesSetup = new PagesSetup() 
    { 
        FirstPage = true,
        LastPage = false,
        OddPages = false,
        EvenPages = false 
    },
    
    // Rectangle area in millimeters
    Rectangle = new Rectangle(10, 10, 100, 30),
    
    Text = "Confidential"
};
```

### Verifying Multiple Text Patterns Simultaneously

You can create multiple verification options to check for different text patterns:

```csharp
// Create a list of verification options
List<VerifyOptions> listOptions = new List<VerifyOptions>();

// Add first text verification
listOptions.Add(new TextVerifyOptions()
{
    Text = "Confidential",
    MatchType = TextMatchType.Exact
});

// Add second text verification
listOptions.Add(new TextVerifyOptions()
{
    Text = "Do not copy",
    MatchType = TextMatchType.Contains
});

// Verify with multiple options
VerificationResult result = signature.Verify(listOptions);
```

### Verifying Text with Specific Appearance

You can also verify text with specific formatting characteristics:

```csharp
TextVerifyOptions options = new TextVerifyOptions()
{
    Text = "APPROVED",
    MatchType = TextMatchType.Exact,
    
    // Verify specific appearance properties
    ForegroundColorRGB = System.Drawing.Color.Green,
    Font = new SignatureFont() { FontFamily = "Arial", FontSize = 12, Bold = true }
};
```

## Best Practices for Text Verification

1. Choose Appropriate Match Types: Select the right match type (Contains, Exact, Regex) based on your verification requirements.
2. Optimize for Performance: For large documents, consider verifying specific pages rather than the entire document.
3. Error Handling: Implement proper error handling to manage unexpected scenarios gracefully.
4. Consider Case Sensitivity: Be mindful of case sensitivity in text matching, especially for critical verifications.
5. Test Thoroughly: Test verification with various document formats and text patterns to ensure compatibility.

## Troubleshooting Common Issues

### Text Not Detected
- Check if the text formatting or encoding is affecting detection
- Ensure the text is actually present in the document as regular text (not an image)
- Try different matching criteria (Contains instead of Exact)

### Performance Issues
- Optimize verification by targeting specific pages or areas
- Use more specific text patterns to reduce false positives

### Verification Failures
- Check if spaces, special characters, or formatting are affecting the match
- Verify text is not part of a scanned image (which requires OCR)
- Ensure document hasn't been modified since the text was added

## Conclusion

Text verification is a versatile and practical approach to document authentication that can be used alone or in combination with other verification methods. GroupDocs.Signature for .NET provides a comprehensive and easy-to-use API for implementing robust text verification functionality in your .NET applications.

By following this step-by-step guide, you've learned how to:
- Configure and initialize the text verification process
- Specify various verification criteria
- Process and interpret verification results
- Implement advanced verification scenarios

These capabilities allow you to build secure and reliable document processing systems that can verify the authenticity of text across various document formats.

## FAQs

### Can GroupDocs.Signature verify text in scanned documents?
GroupDocs.Signature is primarily designed for digital text verification. For scanned documents, you would need to use OCR (Optical Character Recognition) technology first to convert the scanned images to text.

### Which document formats are supported for text verification?
GroupDocs.Signature supports a wide range of document formats including PDF, Word documents (DOC, DOCX), Excel spreadsheets (XLS, XLSX), PowerPoint presentations (PPT, PPTX), images, and more.

### Can I verify formatted text (bold, italics, specific fonts)?
Yes, GroupDocs.Signature provides options to verify text with specific formatting characteristics including font family, size, style (bold, italic), and color.

### Is it possible to verify text in password-protected documents?
Yes, GroupDocs.Signature provides options to specify document passwords when opening protected documents for verification.

### Can I verify watermarks and background text?
Yes, GroupDocs.Signature can verify various types of text signatures including watermarks and background text, depending on how they were implemented in the document.

### Related Resources
* [GroupDocs.Signature API Reference](https://reference.groupdocs.com/signature/net/)
* [GroupDocs.Signature Downloads](https://releases.groupdocs.com/signature/net/)
* [Code Examples on GitHub](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
* [Documentation](https://docs.groupdocs.com/signature/net/)
* [Product Page](https://products.groupdocs.com/signature/net/)
* [Blog Articles](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
* [Support Forum](https://forum.groupdocs.com/c/signature/13)
* [Temporary License](https://purchase.groupdocs.com/temporary-license/)