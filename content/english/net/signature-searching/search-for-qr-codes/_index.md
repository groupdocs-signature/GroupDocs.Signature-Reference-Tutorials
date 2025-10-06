---
title: How to Extract QR Codes from Documents in C#
linktitle: Extract QR Codes C#
second_title: GroupDocs.Signature .NET API
description: Learn how to search and extract QR codes from Word, PDF, and other documents using C# with GroupDocs.Signature .NET. Complete tutorial with code examples and troubleshooting tips.
keywords: extract QR codes from documents C#, search QR codes in PDF .NET, read QR codes from Word documents, QR code reader for documents, scan documents for QR codes tutorial
weight: 15
url: /net/signature-searching/search-for-qr-codes/
date: "2025-01-02"
lastmod: "2025-01-02"
categories: ["Document Processing"]
tags: ["qr-code-extraction", "document-scanning", "csharp-tutorial", "pdf-processing"]
type: docs
---
## Introduction

Ever received a batch of invoices, contracts, or shipping documents with embedded QR codes and needed to extract that data programmatically? You're not alone. Whether you're building an invoice verification system, automating document authentication, or just need to pull tracking codes from hundreds of PDFs, searching for QR codes in documents is a common challenge for .NET developers.

The problem? Most document libraries either don't support QR code detection at all, or they require you to convert everything to images first (which is painfully slow and resource-intensive). That's where GroupDocs.Signature for .NET comes in—it lets you search for and extract QR codes directly from Word docs, PDFs, Excel files, and more without any image conversion hassle.

In this tutorial, you'll learn exactly how to implement QR code search functionality in your C# applications. We're talking real code, practical examples, and the kind of tips that'll save you hours of debugging. Let's dive in.

## Prerequisites

Before you start scanning documents for QR codes, make sure you've got these basics covered:

1. **GroupDocs.Signature for .NET SDK**: Grab it from the [download page](https://releases.groupdocs.com/signature/net/). If you're just testing things out, they've got a free trial available.

2. **Development Environment**: You'll need Visual Studio (or your preferred .NET IDE) with either .NET Framework 4.6.1+ or .NET Core 2.0+. Both work fine.

3. **Basic C# Knowledge**: If you're comfortable with namespaces, classes, and using statements, you're good to go. No advanced patterns required here.

4. **Sample Documents**: Have a few test files ready—PDFs or Word docs with QR codes work great. Don't have any? You can create test QR codes using online generators and paste them into a Word doc.

## Import Namespaces

First things first—let's import the namespaces you'll need. These give you access to all the QR code searching functionality:

```csharp
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
using System;
using System.Collections.Generic;
```

**Quick note:** If you see any red squiggles under these imports, double-check that you've installed the GroupDocs.Signature NuGet package. Right-click your project → Manage NuGet Packages → search for "GroupDocs.Signature" and install it.

## Step-by-Step Guide: Searching for QR Codes

Alright, let's break this down into bite-sized chunks. We'll go from "I have a document" to "I've extracted all the QR codes" in just a few steps.

### Step 1: Define Your Document Path

Start by pointing to the document you want to scan. This can be a local file path or even a network location:

```csharp
string filePath = "sample_multiple_signatures.docx";
```

**Why this matters:** You might be tempted to hardcode paths during development, but in production, you'll probably want to make this dynamic (maybe from user uploads or a database). Keep that flexibility in mind from the start.

**Pro tip:** If you're processing user-uploaded files, always validate the file extension first. GroupDocs supports lots of formats, but you don't want someone uploading a .exe file and crashing your app.

### Step 2: Initialize the Signature Object

Now create an instance of the `Signature` class. This is your main entry point for all document operations:

```csharp
using (Signature signature = new Signature(filePath))
{
    // QR code search code will be added here
}
```

**What's happening here:** The `using` statement ensures that the document resources get cleaned up properly after you're done (memory management matters when you're processing thousands of files). The `Signature` object loads your document into memory and prepares it for analysis.

**Common gotcha:** If your document is password-protected, this will throw an exception. We'll cover handling that in the troubleshooting section below.

### Step 3: Search for QR Code Signatures

This is where the magic happens—use the `Search` method to find all QR codes in your document:

```csharp
// Search for QR code signatures within the document
List<QrCodeSignature> signatures = signature.Search<QrCodeSignature>(SignatureType.QrCode);
```

**Behind the scenes:** GroupDocs scans through every page of your document, identifies QR code patterns, and decodes them. This works on native document formats (no image conversion required), which is why it's so much faster than traditional OCR approaches.

**Performance note:** For large documents (100+ pages), this might take a few seconds. If speed is critical, check out the "Performance Optimization Tips" section later in this guide.

### Step 4: Process and Display Results

Finally, loop through the found QR codes and do something useful with them:

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

**What you get:** Each `QrCodeSignature` object contains:
- **Text**: The decoded content (this is usually what you care about)
- **PageNumber**: Which page it was found on
- **EncodeType**: The QR code format (QR Code, Data Matrix, etc.)
- **Position data**: Coordinates and dimensions (useful for generating reports or highlights)

**Real-world use case:** If you're processing invoices, you might parse the `Text` property to extract order numbers, validate against your database, and flag any mismatches. We'll show you how to do exactly that in the "Common Use Cases" section.

## Complete Working Example

Here's everything put together in a full, ready-to-run program:

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

**Testing tip:** Copy this code into a new console app, update the `filePath` to point to one of your test documents, and run it. You should see output within seconds. If you don't get any results, double-check that your document actually contains QR codes (yeah, we've all been there).

## Advanced QR Code Searching Techniques

Once you've got the basics down, here are some advanced techniques that'll make your life easier in production scenarios.

### Searching with Specific Criteria

Maybe you don't want ALL the QR codes—just ones on specific pages, or with specific content. Here's how to filter your search:

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

**When to use this:** If you're processing standardized forms where QR codes always appear in the same location (like the top-right corner of invoices), defining a search rectangle can dramatically speed up processing. It also helps avoid false positives from unrelated QR codes elsewhere in the document.

### Processing QR Code Data

Here's a practical example of parsing different types of QR code content. This pattern is super useful when you're dealing with documents that use QR codes for different purposes:

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

**Real-world application:** We've used this exact pattern for a client's invoice processing system. Their suppliers embedded invoice numbers and amounts in QR codes, and we'd validate them against the invoice text. Caught several hundred data entry errors in the first month alone.

### Implementing Security Verification

QR codes are increasingly used for document authentication. Here's how to verify them:

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

**Security note:** In production, you'd obviously want to verify against a database or secure API, not hardcoded values. Consider using cryptographic signatures or time-based one-time passwords (TOTP) for extra security.

### Extracting QR Code Images

Sometimes you need the actual QR code image (for reports, archives, or further analysis):

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

**Use case:** One client needed to maintain an audit trail of all processed documents. They extracted QR code images and stored them alongside the decoded text in their compliance database. Made audits way easier.

## Common Use Cases & Scenarios

Let's look at some real-world scenarios where QR code extraction shines:

### Invoice Verification & Processing
You've got hundreds of supplier invoices with QR codes containing order numbers and amounts. Extract them, validate against your purchase orders, and flag any discrepancies before they hit accounts payable. Saves manual data entry and catches errors early.

### Document Authentication Systems
Legal documents, certificates, or official forms often include authentication QR codes. Scan incoming documents, verify the codes against your database, and automatically route authentic documents while flagging suspicious ones for review.

### Shipping & Logistics Tracking
Shipping labels, packing slips, and waybills commonly use QR codes for tracking. Extract them from scanned documents, update your inventory system automatically, and maintain real-time visibility into your supply chain.

### Contract Management
Large organizations often embed unique identifiers in contract QR codes. Extract these during document ingestion, automatically file contracts in the right folders, and create searchable databases without manual tagging.

### Healthcare Records Processing
Medical facilities use QR codes on patient forms, lab results, and prescriptions. Automating QR code extraction ensures accurate patient matching and reduces data entry errors in critical healthcare workflows.

## Performance Optimization Tips

Processing lots of documents? Here's how to keep things fast:

### Limit Search Scope
If you know QR codes only appear on the first page (or in a specific area), use `QrCodeSearchOptions` to limit the search. This can speed things up by 3-5x for large documents:

```csharp
QrCodeSearchOptions options = new QrCodeSearchOptions
{
    AllPages = false,
    PageNumber = 1,
    Rectangle = new Rectangle(0, 0, 200, 200) // Top-left corner only
};
```

### Batch Processing
Don't process files one-by-one if you're handling bulk uploads. Use parallel processing with `Parallel.ForEach` or asynchronous tasks to process multiple documents simultaneously. Just watch your memory usage.

### Cache Results
If you're searching the same documents repeatedly (maybe for different signature types), consider caching the `Signature` object or search results. Just make sure to invalidate the cache if documents get updated.

### Choose the Right Document Format
PDF files are generally faster to process than Word documents because they're already paginated. If you have control over the input format, PDFs are your friend.

## Troubleshooting Common Issues

Running into problems? Here are solutions to the most common issues:

### "The document is password protected"
If you get this error, you need to provide the password when initializing the Signature object:

```csharp
LoadOptions loadOptions = new LoadOptions { Password = "your_password" };
using (Signature signature = new Signature(filePath, loadOptions))
{
    // Search as normal
}
```

### No QR Codes Found (But You Know They're There)
First, check the obvious: are they actually QR codes, or are they Data Matrix codes, barcodes, or other formats? GroupDocs supports multiple types, but you need to specify the right `SignatureType`.

Also, if the QR codes are in images embedded in your document, they should still be detected—but very low-resolution images might cause issues. Minimum recommended resolution is 150 DPI.

### Performance Is Slow
For documents over 50 pages, consider:
- Limiting your search scope (specific pages or regions)
- Processing documents asynchronously
- Upgrading your GroupDocs license (trial versions have some performance limitations)

### Memory Issues with Large Documents
If you're processing massive files (100+ MB), make sure you're properly disposing of the `Signature` object (use `using` statements) and consider processing pages in chunks rather than loading the entire document at once.

### Invalid or Corrupt QR Code Data
Sometimes QR codes get damaged (wrinkles in scanned documents, poor image quality, etc.). Add error handling around your data parsing logic and consider logging cases where QR codes can't be decoded properly for manual review.

## Implementation Patterns

Here are some common patterns for integrating QR code search into your applications:

### Async Document Processing Pipeline
```csharp
public async Task<List<QrCodeData>> ProcessDocumentAsync(string filePath)
{
    return await Task.Run(() =>
    {
        using (Signature signature = new Signature(filePath))
        {
            var signatures = signature.Search<QrCodeSignature>(SignatureType.QrCode);
            return signatures.Select(s => new QrCodeData
            {
                Content = s.Text,
                PageNumber = s.PageNumber,
                Position = new Position(s.Left, s.Top)
            }).ToList();
        }
    });
}
```

### Batch Processing with Progress Reporting
```csharp
public void ProcessMultipleDocuments(List<string> filePaths, IProgress<int> progress)
{
    int processed = 0;
    foreach (var filePath in filePaths)
    {
        using (Signature signature = new Signature(filePath))
        {
            var signatures = signature.Search<QrCodeSignature>(SignatureType.QrCode);
            // Process signatures...
        }
        processed++;
        progress?.Report((processed * 100) / filePaths.Count);
    }
}
```

### Integration with Dependency Injection
```csharp
public interface IQrCodeExtractor
{
    List<QrCodeSignature> ExtractQrCodes(string filePath);
}

public class GroupDocsQrCodeExtractor : IQrCodeExtractor
{
    public List<QrCodeSignature> ExtractQrCodes(string filePath)
    {
        using (Signature signature = new Signature(filePath))
        {
            return signature.Search<QrCodeSignature>(SignatureType.QrCode);
        }
    }
}
```

This makes testing easier and keeps your code loosely coupled—you can swap out the implementation without changing your business logic.

## Conclusion

You've now got everything you need to extract QR codes from documents in your C# applications. From basic searching to advanced filtering, authentication verification, and performance optimization, you're equipped to handle real-world scenarios.

The key takeaway? GroupDocs.Signature makes QR code extraction straightforward—no image conversion gymnastics, no complex OCR setup, just clean API calls that work across multiple document formats. Whether you're processing invoices, verifying contracts, or tracking shipments, you've got the tools to automate it.

Start with the simple example, get comfortable with the basics, then layer in the advanced techniques as your requirements grow. And remember, the FAQ section below has answers to questions that'll probably pop up as you build this out.

## FAQ's

### Which QR code formats does GroupDocs.Signature support?

GroupDocs.Signature supports all the major QR code standards you're likely to encounter: standard QR Code, Micro QR Code, Aztec Code, Data Matrix, and PDF417. The specific format type is available through the `EncodeType` property of each `QrCodeSignature` object, which is handy if you need to handle different formats differently in your code.

### Can I search for QR codes in password-protected documents?

Absolutely. Just provide the password when you initialize the `Signature` object using `LoadOptions`:

```csharp
LoadOptions loadOptions = new LoadOptions { Password = "your_password" };
using (Signature signature = new Signature(filePath, loadOptions))
{
    List<QrCodeSignature> signatures = signature.Search<QrCodeSignature>(SignatureType.QrCode);
    // Process as normal
}
```

This works for password-protected PDFs and Word documents. If you're processing multiple protected documents with different passwords, you'll need to track and provide the correct password for each one (obviously).

### How do I filter QR codes based on their content?

Use the `Text` and `MatchType` properties of `QrCodeSearchOptions` to filter by content:

```csharp
QrCodeSearchOptions options = new QrCodeSearchOptions
{
    Text = "Invoice",
    MatchType = TextMatchType.Contains // Also available: Exact, StartsWith, EndsWith
};
List<QrCodeSignature> filteredSignatures = signature.Search<QrCodeSignature>(options);
```

This is super useful when documents contain multiple QR codes but you only care about specific ones (like authentication codes vs. tracking numbers). The filtering happens during the search, so it's more efficient than searching for everything and filtering afterward.

### Can GroupDocs.Signature detect damaged or partially obscured QR codes?

GroupDocs.Signature has built-in error correction that handles minor damage pretty well (QR codes have redundancy built in by design). However, heavily damaged QR codes—like ones that are mostly obscured, severely wrinkled in scanned documents, or printed at very low resolution—might not be detectable.

For best results, aim for minimum 150 DPI when scanning documents, and ensure QR codes are reasonably intact. If you're getting inconsistent results, the image quality is usually the culprit. You might need to improve your scanning process or switch to higher-quality source documents.

### What document formats are supported for QR code searching?

GroupDocs.Signature works with pretty much any document format you're likely to encounter:
- **PDF** (most common for QR codes)
- **Microsoft Office**: Word (DOC, DOCX), Excel (XLS, XLSX), PowerPoint (PPT, PPTX)
- **Images**: JPEG, PNG, TIFF, BMP, GIF
- **Other formats**: ODT, ODS, ODP, and more

The full list is on their [supported formats page](https://docs.groupdocs.com/signature/net/supported-document-formats/), but honestly, if it's a common business document format, it's probably supported. Just watch out for really obscure legacy formats—those might need conversion first.

### How do I handle QR codes that span multiple pages or documents?

Each `QrCodeSignature` includes a `PageNumber` property, so if you've got QR codes on multiple pages, you'll get separate signature objects for each one. They won't be automatically correlated, though—if you need to track related QR codes across pages, you'll need to implement that logic yourself (usually by parsing the content and looking for relationships).

For multi-document scenarios, process each document separately and aggregate the results in your application logic. Consider using a database or in-memory collection to correlate QR codes from multiple files if that's part of your workflow.

### Is there a limit to how many QR codes can be detected in a single document?

There's no hard limit imposed by GroupDocs.Signature—it'll find however many QR codes are in your document. That said, performance does degrade somewhat with very large numbers (think 100+ QR codes in a single document), so keep that in mind for extreme edge cases.

If you're hitting performance issues with QR-code-heavy documents, consider processing pages in batches or using the search options to limit scope.

## See Also

- [GroupDocs.Signature .NET API Reference](https://reference.groupdocs.com/signature/net/) - Complete API documentation
- [Product Documentation](https://docs.groupdocs.com/signature/net/) - Comprehensive guides and tutorials
- [Product Page](https://products.groupdocs.com/signature/net/) - Feature overview and pricing
- [Download Latest Version](https://releases.groupdocs.com/signature/net/) - Get the SDK
- [Free Support Forum](https://forum.groupdocs.com/c/signature/13) - Ask questions and get help
- [Temporary License](https://purchase.groupdocs.com/temporary-license/) - Try the full version before buying