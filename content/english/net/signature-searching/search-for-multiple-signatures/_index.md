---
title: "Search Multiple Signature Types in Documents"
linktitle: "Search for Multiple Signatures"
description: "Learn how to search multiple signature types (digital, barcode, QR code, text) in one document using .NET. Complete guide with code examples and troubleshooting tips."
keywords: "search multiple signature types document, validate digital signatures, document signature verification .NET, search barcode QR code signatures, multi signature validation C#"
weight: 14
url: /net/signature-searching/search-for-multiple-signatures/
date: "2025-01-02"
lastmod: "2025-01-02"
categories: ["Document Security"]
tags: ["signature-search", "document-validation", "digital-signatures", "barcode-signatures", "qr-codes"]
---

## Introduction

Ever opened a contract or compliance document and wondered, "Does this have all the required signatures?" Maybe you need to verify a digital signature, check for an approval stamp, and validate a QR code—all in the same document. Doing this manually is tedious, error-prone, and honestly, a waste of your time.

Here's the thing: modern documents don't just use one type of signature anymore. You might have a digital certificate for authenticity, a barcode for tracking, a QR code for mobile verification, and text signatures for approvals. Searching for each one separately? That's inefficient.

GroupDocs.Signature for .NET lets you search for multiple signature types in a single pass—whether it's digital signatures, text stamps, barcodes, QR codes, or metadata. In this guide, you'll learn exactly how to implement multi-signature search functionality that actually works in production environments.

## Why Search Multiple Signature Types?

Before we dive into code, let's talk about why you'd need this functionality (because it's not just a "nice-to-have" feature).

**Real-world scenarios where this matters:**

- **Contract Verification:** You need to confirm that a legal document has both the signer's digital certificate AND the witness's text signature before processing
- **Compliance Auditing:** Regulatory documents require multiple approval signatures—missing even one could mean non-compliance
- **Invoice Processing:** Modern invoices might have barcodes for tracking, QR codes for payment, and digital signatures for authenticity
- **Document Workflow Automation:** Your system needs to verify that documents have passed through all required approval stages before moving forward

The alternative? Writing separate code for each signature type, running multiple scans, and trying to correlate results. That's messy, slow, and hard to maintain.

## Prerequisites

Before we get started, make sure you've got these basics covered:

**What you'll need:**

1. **Development Environment:** Visual Studio 2019 or later (or any .NET IDE you're comfortable with)
  
2. **GroupDocs.Signature for .NET:** Download the library from [here](https://releases.groupdocs.com/signature/net/). If you're using NuGet, just run:
   ```
   Install-Package GroupDocs.Signature
   ```

3. **Basic C# Knowledge:** You should be comfortable with classes, namespaces, and LINQ (we'll use it for filtering results)

4. **Test Documents:** Grab a few sample documents with different signature types. Don't have any? The library works with PDF, DOCX, XLSX, and many other formats—just create a simple test file and add signatures using the library's signing features first

**Pro tip:** Start with a PDF that has at least two different signature types. PDFs are the most common use case for this functionality.

## Import Namespaces

First things first—let's import the namespaces you'll need. These give you access to all the signature search functionality:

```csharp
using System;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

**What each namespace does:**
- `GroupDocs.Signature`: Core library functionality
- `GroupDocs.Signature.Domain`: Signature objects and enums (like `SignatureType`)
- `GroupDocs.Signature.Options`: Search configuration classes

Now let's build the search functionality step by step.

## Step 1: Load the Document

Every signature search starts by loading your document into memory. Here's how:

```csharp
string filePath = "sample_multiple_signatures.docx";
using (Signature signature = new Signature(filePath))
{
    // Multi-signature search code will be added here
}
```

**What's happening here:**
- The `Signature` class is your main entry point for all operations
- We're using `using` statement for automatic cleanup (important for file handles)
- `filePath` can be an absolute or relative path—whatever works for your setup

**Common mistake:** Forgetting the `using` statement and leaving file handles open. This can cause "file in use" errors when you try to process the same document again.

## Step 2: Define Search Options for Different Signature Types

This is where the magic happens. Instead of running separate searches, you define options for each signature type you care about:

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

**Key things to understand:**

- **AllPages:** Set to `true` to search the entire document, or `false` to specify specific pages (we'll cover that in the advanced section)
- **Text property:** This is optional. If you leave it empty, the search will find ALL signatures of that type. If you specify text, it'll only match signatures containing that text
- **MatchType:** Choose between `Exact`, `Contains`, `StartsWith`, or `EndsWith` depending on your needs

**When to use which match type:**
- `Exact`: When you know the precise signature text (e.g., "Approved by Manager")
- `Contains`: When the signature text might vary slightly (e.g., any signature containing "Approved")
- `StartsWith`: For standardized prefixes (e.g., all signatures starting with "AUTH-")
- `EndsWith`: Less common, but useful for specific suffixes

## Step 3: Add Options to a Collection

Now bundle all your search options together:

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

**Why use a list?** The `Search` method accepts multiple search options at once. This is what enables the simultaneous multi-signature search—instead of calling `Search` five times (once per signature type), you call it once with all options.

**Pro tip:** You don't have to include all signature types. If you only care about digital and barcode signatures for a particular workflow, just add those two to the list.

## Step 4: Perform the Search and Process Results

Here's where you execute the search and handle what you find:

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

**Breaking down the result processing:**

- `SearchResult.Signatures`: This collection contains ALL found signatures, regardless of type
- Type checking (`if (foundSignature is TextSignature)`): Each signature type has specific properties—you need to cast to access them
- `SignatureId`: A unique identifier for each signature (useful for logging or tracking)
- `PageNumber`: Tells you exactly where the signature was found

**Real-world tip:** In production code, you'd probably log these results to a database or return them in a structured format rather than using `Console.WriteLine`. The pattern remains the same, though.

## Complete Example

Here's everything put together in a working program you can actually run:

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

**About this example:** Notice we're using a `switch` statement instead of `if-else` chains for type checking. Both work, but `switch` is cleaner when you have many signature types to handle.

## When to Use Each Signature Type

Not sure which signature types you should be searching for? Here's a practical guide:

**Digital Signatures** - Use when:
- Legal authenticity matters
- You need non-repudiation (proof that someone signed)
- Compliance requires certificate-based signatures
- Example: Contracts, regulatory filings, official documents

**Text Signatures** - Use when:
- You need human-readable approval stamps
- Simple workflows where visual confirmation is enough
- Creating audit trails with names and dates
- Example: "Reviewed by John Smith - 2025-01-15"

**Barcode Signatures** - Use when:
- You need to encode tracking numbers or IDs
- Integration with inventory or logistics systems
- Machine-readable identifiers are required
- Example: Invoice tracking, shipping documents

**QR Code Signatures** - Use when:
- Mobile verification is important
- You need to embed URLs or complex data
- Quick scanning capabilities matter
- Example: Event tickets, mobile payment confirmations

**Metadata Signatures** - Use when:
- You need hidden signature data
- File properties need to carry authentication info
- Workflow tracking happens behind the scenes
- Example: Document processing systems, automated workflows

## Advanced Multi-Signature Search Techniques

### Filtering Search Results

Once you've got your results, you'll often need to filter them based on specific criteria:

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

**Why filter results?** In complex documents, you might find dozens of signatures. Filtering helps you focus on what matters for your specific workflow—like ensuring page 1 has a digital signature, or finding all approval stamps.

### Validating Multiple Signatures

Here's a practical validation function you can adapt for your needs:

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

**Real-world use case:** Let's say your compliance process requires both a valid digital signature AND a specific QR code before a document can be processed. This validation function checks both requirements and returns `false` if either is missing.

### Searching with Custom Processing

For advanced scenarios, you can add custom validation logic during the search itself:

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

**What this does:** The `ProcessCompleted` delegate acts as a filter DURING the search. Only signatures that pass your custom logic will be included in the results. This is more efficient than searching everything and filtering afterward.

## Common Issues & How to Fix Them

### Issue 1: "File is Being Used by Another Process"

**Symptom:** You get an IOException when trying to load the document.

**Causes:**
- Forgot to use `using` statement with the `Signature` object
- Previous search operation didn't properly dispose
- File is actually open in another application

**Fix:**
```csharp
// Always use 'using' for automatic cleanup
using (Signature signature = new Signature(filePath))
{
    // Do your work here
} // File handle automatically released here
```

### Issue 2: Search Returns No Results (But You Know Signatures Exist)

**Possible causes:**

1. **Wrong file path:** Double-check your path is correct
2. **Search options too restrictive:** If you specified text in your search options, it might not match what's actually in the document
3. **Wrong signature type:** Maybe you're searching for digital signatures in a document that only has text signatures

**Debugging tip:**
```csharp
// Start with a broad search - no text filters
TextSearchOptions textOptions = new TextSearchOptions
{
    AllPages = true
    // Don't specify Text property yet
};
```

Run this first to see what's actually in the document, then narrow down your search criteria.

### Issue 3: Slow Performance on Large Documents

**Symptom:** Search takes a long time on documents with hundreds of pages.

**Solutions:**
```csharp
// Search specific pages instead of all pages
TextSearchOptions textOptions = new TextSearchOptions
{
    AllPages = false,
    PagesSetup = new PagesSetup 
    { 
        FirstPage = true,  // Search first page
        LastPage = true    // And last page only
    }
};
```

Or if you know which pages matter:
```csharp
PagesSetup = new PagesSetup 
{ 
    Pages = new List<int> { 1, 5, 10 }  // Specific pages only
}
```

### Issue 4: "Invalid Digital Signature" Even Though It Looks Valid

**Common reasons:**
- Certificate has expired
- Document was modified after signing
- Certificate chain can't be validated
- System date/time is incorrect

**Check validity properly:**
```csharp
var digitalSignature = foundSignature as DigitalSignature;
if (digitalSignature != null)
{
    Console.WriteLine($"Valid: {digitalSignature.IsValid}");
    Console.WriteLine($"Valid from: {digitalSignature.Certificate?.NotBefore}");
    Console.WriteLine($"Valid until: {digitalSignature.Certificate?.NotAfter}");
    
    // Check if certificate is currently valid
    DateTime now = DateTime.Now;
    bool certIsValid = digitalSignature.Certificate != null &&
                       now >= digitalSignature.Certificate.NotBefore &&
                       now <= digitalSignature.Certificate.NotAfter;
}
```

## Performance Tips for Large Documents

When you're dealing with big files (100+ pages), these optimizations make a real difference:

### 1. Search Only What You Need

Don't search for signature types you don't care about. If you only need digital signatures, only include digital search options:

```csharp
// Instead of all signature types...
List<SearchOptions> searchOptions = new List<SearchOptions>
{
    new DigitalSearchOptions { AllPages = true }  // Only what you need
};
```

### 2. Use Page Ranges Strategically

Most document workflows have patterns. Signatures often appear in predictable locations:

```csharp
// Common pattern: signatures on first and last pages
TextSearchOptions textOptions = new TextSearchOptions
{
    PagesSetup = new PagesSetup
    {
        FirstPage = true,
        LastPage = true
    }
};
```

### 3. Process Results Efficiently

If you have many signatures, avoid loading everything into memory at once:

```csharp
// Process as you iterate instead of collecting all results first
foreach (var signature in result.Signatures)
{
    // Process immediately
    LogSignatureToDatabase(signature);
    // Don't store in another collection unless necessary
}
```

### 4. Cache Results When Appropriate

If you're processing the same document multiple times, cache the search results:

```csharp
// Simple caching pattern
private static Dictionary<string, SearchResult> _signatureCache = new Dictionary<string, SearchResult>();

SearchResult GetOrSearchSignatures(string filePath)
{
    if (_signatureCache.ContainsKey(filePath))
    {
        return _signatureCache[filePath];
    }
    
    using (Signature signature = new Signature(filePath))
    {
        SearchResult result = signature.Search(searchOptions);
        _signatureCache[filePath] = result;
        return result;
    }
}
```

**Warning:** This is a simple example. In production, you'd want to add cache invalidation logic (clear cache if file is modified), memory limits, and expiration policies.

## Best Practices

### 1. Always Validate Input Files

Before searching, make sure the file exists and is accessible:

```csharp
if (!File.Exists(filePath))
{
    Console.WriteLine($"Error: File not found at {filePath}");
    return;
}

// Check file size if needed
FileInfo fileInfo = new FileInfo(filePath);
if (fileInfo.Length > 100 * 1024 * 1024) // 100 MB
{
    Console.WriteLine("Warning: Large file detected. Search may take time.");
}
```

### 2. Use Structured Logging

Instead of `Console.WriteLine`, use a proper logging framework in production:

```csharp
// Example with common logging pattern
_logger.LogInformation("Starting signature search for {FilePath}", filePath);
_logger.LogInformation("Found {Count} signatures", result.Signatures.Count);

foreach (var sig in result.Signatures)
{
    _logger.LogDebug("Signature details: Type={Type}, Page={Page}, Id={Id}", 
                     sig.SignatureType, sig.PageNumber, sig.SignatureId);
}
```

### 3. Handle Exceptions Gracefully

Different things can go wrong—corrupt files, permission issues, unsupported formats:

```csharp
try
{
    using (Signature signature = new Signature(filePath))
    {
        SearchResult result = signature.Search(searchOptions);
        // Process results
    }
}
catch (FileNotFoundException)
{
    Console.WriteLine("Error: Document file not found.");
}
catch (UnauthorizedAccessException)
{
    Console.WriteLine("Error: Access denied. Check file permissions.");
}
catch (GroupDocsSignatureException ex)
{
    Console.WriteLine($"Error: GroupDocs-specific error: {ex.Message}");
}
catch (Exception ex)
{
    Console.WriteLine($"Unexpected error: {ex.Message}");
    // Log full exception details for debugging
}
```

### 4. Return Structured Results

For API or service applications, return results in a structured format:

```csharp
public class SignatureSearchResponse
{
    public bool Success { get; set; }
    public string Message { get; set; }
    public int TotalSignaturesFound { get; set; }
    public Dictionary<string, int> SignatureCountByType { get; set; }
    public List<SignatureDetail> Signatures { get; set; }
}

public class SignatureDetail
{
    public string Type { get; set; }
    public int Page { get; set; }
    public string Content { get; set; }
    public bool IsValid { get; set; }
}
```

## Conclusion

Searching for multiple signature types simultaneously isn't just a convenient feature—it's essential for modern document processing workflows. Whether you're building compliance systems, automating approval processes, or validating contracts, the ability to search for digital signatures, barcodes, QR codes, text signatures, and metadata in one pass saves time and reduces complexity.

Here's what you've learned:
- How to set up search options for different signature types
- The importance of using the right match types and search criteria
- Practical filtering and validation techniques for real-world scenarios
- Common pitfalls and how to avoid them
- Performance optimization strategies for large documents

GroupDocs.Signature for .NET makes this complex task straightforward with its unified API. Instead of juggling multiple libraries or writing custom parsers for each signature type, you get a single, reliable solution that works across all major document formats.

**Next steps:** Start with a simple proof-of-concept using one of the code examples in this guide. Test it with your own documents, then gradually add the signature types and validation logic your specific workflow requires. The beauty of this approach is that it scales from simple searches to complex, multi-criteria validation workflows without major architectural changes.

## FAQ's

### Can I search for signatures in password-protected documents?

Yes, absolutely. GroupDocs.Signature supports password-protected documents—you just need to provide the password when initializing the `Signature` object:

```csharp
LoadOptions loadOptions = new LoadOptions { Password = "your_password" };
using (Signature signature = new Signature(filePath, loadOptions))
{
    // Search for signatures normally
}
```

**Important:** Make sure to handle incorrect passwords gracefully in production code. You'll get a `GroupDocsSignatureException` if the password is wrong.

### Which document formats are supported for signature searching?

GroupDocs.Signature has broad format support. The main ones you'll likely work with include:

- **PDF documents** (most common for signatures)
- **Microsoft Word** (DOC, DOCX)
- **Microsoft Excel** (XLS, XLSX)
- **Microsoft PowerPoint** (PPT, PPTX)
- **OpenOffice formats** (ODT, ODS)
- **Image formats** (PNG, JPG, TIFF, BMP)

You can also search signatures in archived formats and many other specialized document types. Check the official documentation for the complete list, as it's regularly updated.

### Can I limit the search to specific pages in a document?

Yes, and you should when possible for better performance. Each search option type has properties for page control:

```csharp
TextSearchOptions options = new TextSearchOptions
{
    AllPages = false,  // Don't search all pages
    PageNumber = 1,    // Search only on page 1
    
    // Or for more control
    PagesSetup = new PagesSetup 
    { 
        FirstPage = true,   // Include first page
        LastPage = true,    // Include last page
        Pages = new List<int> { 3, 5, 7 }  // Include specific pages
    }
};
```

**Practical tip:** In many document workflows, signatures appear on the first page (approvals), last page (sign-offs), or both. Limiting your search to these pages can significantly improve performance on large documents.

### How can I optimize performance when searching in large documents?

Performance optimization depends on your specific use case, but here are the most effective strategies:

1. **Limit page ranges** - Don't search all pages if you don't need to
2. **Be specific with search criteria** - Use exact text matching when you know what you're looking for
3. **Search for fewer signature types** - Only include the types you actually need
4. **Use pagination** - If displaying results, implement paging rather than loading everything at once
5. **Consider caching** - Cache results if you're processing the same document multiple times

For documents over 500 pages, consider implementing the page range strategy:

```csharp
// Search in batches if needed
for (int i = 1; i <= totalPages; i += 50)
{
    var options = new TextSearchOptions
    {
        PagesSetup = new PagesSetup 
        { 
            Pages = Enumerable.Range(i, Math.Min(50, totalPages - i + 1)).ToList()
        }
    };
    // Process batch
}
```

**Real talk:** Most documents are under 50 pages, so don't over-optimize until you actually have performance issues. Measure first, optimize second.

### Can I extend GroupDocs.Signature to support custom signature types?

While GroupDocs.Signature provides comprehensive built-in support for common signature types, you can extend its functionality in several ways:

**1. Custom Processing Logic:**
```csharp
TextSearchOptions options = new TextSearchOptions
{
    AllPages = true,
    ProcessCompleted = (signature) =>
    {
        // Your custom validation logic here
        TextSignature textSig = signature as TextSignature;
        if (textSig != null)
        {
            // Custom business rules
            return textSig.Text.StartsWith("CUSTOM-");
        }
        return false;
    }
};
```

**2. Wrapper Classes for Business Logic:**
```csharp
public class CustomSignatureValidator
{
    private readonly Signature _signature;
    
    public CustomSignatureValidator(string filePath)
    {
        _signature = new Signature(filePath);
    }
    
    public CustomValidationResult ValidateWithBusinessRules(List<SearchOptions> options)
    {
        var result = _signature.Search(options);
        
        // Apply your custom business rules
        var customResult = new CustomValidationResult
        {
            IsValid = ApplyCustomValidation(result),
            ValidationDetails = GenerateCustomReport(result)
        };
        
        return customResult;
    }
    
    private bool ApplyCustomValidation(SearchResult result)
    {
        // Your organization-specific validation logic
        return result.Signatures.Count >= 2 && 
               result.Signatures.Any(s => s.SignatureType == SignatureType.Digital);
    }
}
```

**3. Metadata for Custom Signature Information:**

You can use metadata signatures to store and search for custom data:

```csharp
MetadataSearchOptions metadataOptions = new MetadataSearchOptions();
var result = signature.Search(metadataOptions);

foreach (var sig in result.Signatures.OfType<MetadataSignature>())
{
    if (sig.Name == "CustomApprovalLevel")
    {
        // Process your custom metadata
        string approvalLevel = sig.Value.ToString();
    }
}
```

**The bottom line:** While you can't directly create new signature *types* (that would require modifying the library), you can build sophisticated custom validation and processing logic on top of the existing types.

### What's the difference between synchronous and asynchronous search operations?

GroupDocs.Signature primarily uses synchronous operations. The `Search` method blocks until results are ready:

```csharp
// This is synchronous - waits for completion
SearchResult result = signature.Search(searchOptions);
```

For asynchronous scenarios (like web applications), wrap the operation in a Task:

```csharp
public async Task<SearchResult> SearchSignaturesAsync(string filePath, List<SearchOptions> options)
{
    return await Task.Run(() =>
    {
        using (Signature signature = new Signature(filePath))
        {
            return signature.Search(options);
        }
    });
}
```

**When to use async:**
- Web applications where you don't want to block request threads
- Processing multiple documents in parallel
- UI applications where you need to keep the interface responsive

**When synchronous is fine:**
- Console applications
- Batch processing jobs
- Simple scripts where blocking isn't an issue

### How do I handle documents with hundreds of signatures?

Large numbers of signatures require a strategy for efficient processing and display:

**1. Implement Pagination:**
```csharp
public class PaginatedSignatures
{
    public List<BaseSignature> GetPage(SearchResult result, int pageNumber, int pageSize)
    {
        return result.Signatures
            .Skip((pageNumber - 1) * pageSize)
            .Take(pageSize)
            .ToList();
    }
    
    public int GetTotalPages(SearchResult result, int pageSize)
    {
        return (int)Math.Ceiling(result.Signatures.Count / (double)pageSize);
    }
}
```

**2. Group by Type:**
```csharp
var groupedSignatures = result.Signatures
    .GroupBy(s => s.SignatureType)
    .ToDictionary(g => g.Key, g => g.ToList());

Console.WriteLine($"Digital: {groupedSignatures[SignatureType.Digital].Count}");
Console.WriteLine($"Text: {groupedSignatures[SignatureType.Text].Count}");
```

**3. Filter Strategically:**
```csharp
// Only show signatures that matter for your workflow
var relevantSignatures = result.Signatures
    .Where(s => s.PageNumber <= 3 || s.PageNumber == result.Signatures.Max(x => x.PageNumber))
    .ToList();
```

**4. Use Summary Views:**

Instead of displaying every signature detail, show summaries:

```csharp
public class SignatureSummary
{
    public int TotalCount { get; set; }
    public Dictionary<SignatureType, int> CountByType { get; set; }
    public int PagesWithSignatures { get; set; }
    public bool HasRequiredSignatures { get; set; }
}

public SignatureSummary CreateSummary(SearchResult result)
{
    return new SignatureSummary
    {
        TotalCount = result.Signatures.Count,
        CountByType = result.Signatures
            .GroupBy(s => s.SignatureType)
            .ToDictionary(g => g.Key, g => g.Count()),
        PagesWithSignatures = result.Signatures
            .Select(s => s.PageNumber)
            .Distinct()
            .Count(),
        HasRequiredSignatures = ValidateRequiredSignatures(result)
    };
}
```

### Can I search for signatures based on creation date or other temporal criteria?

Yes, though the approach depends on the signature type:

**For Digital Signatures:**
```csharp
var result = signature.Search(new List<SearchOptions> 
{ 
    new DigitalSearchOptions { AllPages = true } 
});

// Filter by date after search
var recentDigitalSignatures = result.Signatures
    .OfType<DigitalSignature>()
    .Where(s => s.SignDate >= DateTime.Now.AddMonths(-3))
    .ToList();
```

**For Metadata Signatures:**

If your workflow stores dates in metadata:

```csharp
var metadataResult = signature.Search(new List<SearchOptions> 
{ 
    new MetadataSearchOptions() 
});

foreach (var sig in metadataResult.Signatures.OfType<MetadataSignature>())
{
    if (sig.Name == "SignatureDate" && DateTime.TryParse(sig.Value?.ToString(), out DateTime signDate))
    {
        if (signDate >= DateTime.Now.AddDays(-30))
        {
            // Process recent signature
        }
    }
}
```

**Important note:** Not all signature types have date information embedded. Text and barcode signatures typically don't carry timestamp data unless it's part of their text content.

### What happens if I search for a signature type that doesn't exist in the document?

Nothing breaks—the library handles this gracefully. The `SearchResult` simply won't contain any signatures of that type:

```csharp
// Even if document has no digital signatures, this won't throw an exception
var result = signature.Search(new List<SearchOptions>
{
    new DigitalSearchOptions { AllPages = true }
});

if (result.Signatures.Count == 0)
{
    Console.WriteLine("No digital signatures found");
    // Continue normally
}
```

**Best practice:** Always check `result.Signatures.Count` before processing results. Don't assume signatures will be found.

### How do I verify that a digital signature hasn't been tampered with?

The `DigitalSignature` object includes validation information:

```csharp
var digitalSigs = result.Signatures.OfType<DigitalSignature>();

foreach (var digitalSig in digitalSigs)
{
    Console.WriteLine($"Valid: {digitalSig.IsValid}");
    
    // Check specific validation details
    if (!digitalSig.IsValid)
    {
        Console.WriteLine("Digital signature validation failed!");
        Console.WriteLine($"Certificate: {digitalSig.Certificate?.SubjectName}");
        Console.WriteLine($"Sign time: {digitalSig.SignDate}");
        
        // Document was likely modified after signing
        // or certificate chain cannot be verified
    }
    else
    {
        Console.WriteLine("Digital signature is valid - document integrity confirmed");
    }
}
```

**What `IsValid` checks:**
- Certificate validity (not expired, trusted)
- Document integrity (not modified since signing)
- Certificate chain validation
- Signature algorithm strength

**Security tip:** Always validate digital signatures when document authenticity matters. A signature being present doesn't mean it's valid.

### Can I use this library with cloud storage (AWS S3, Azure Blob, etc.)?

Absolutely. The library works with file paths and streams, so you can easily integrate with cloud storage:

**Example with a generic cloud download pattern:**
```csharp
public async Task<SearchResult> SearchCloudDocument(string cloudFileId, List<SearchOptions> searchOptions)
{
    // Download from cloud to temp file
    string tempFile = Path.GetTempFileName();
    
    try
    {
        // Your cloud download logic here
        await DownloadFromCloud(cloudFileId, tempFile);
        
        // Search signatures
        using (Signature signature = new Signature(tempFile))
        {
            return signature.Search(searchOptions);
        }
    }
    finally
    {
        // Clean up temp file
        if (File.Exists(tempFile))
        {
            File.Delete(tempFile);
        }
    }
}
```

**Alternative using streams (no temp file needed):**
```csharp
public SearchResult SearchFromStream(Stream documentStream, List<SearchOptions> searchOptions)
{
    using (Signature signature = new Signature(documentStream))
    {
        return signature.Search(searchOptions);
    }
}

// Usage with cloud storage
using (var stream = await DownloadStreamFromCloud(fileId))
{
    var result = SearchFromStream(stream, searchOptions);
}
```

**Performance tip:** For repeated operations on the same cloud document, consider caching it locally rather than downloading it every time.

## See Also

- [API Reference](https://reference.groupdocs.com/signature/net/)
- [Product Documentation](https://docs.groupdocs.com/signature/net/)
- [Product Page](https://products.groupdocs.com/signature/net/)
- [Download Latest Version](https://releases.groupdocs.com/signature/net/)
- [Free Support Forum](https://forum.groupdocs.com/c/signature/13)
- [Temporary License](https://purchase.groupdocs.com/temporary-license/)