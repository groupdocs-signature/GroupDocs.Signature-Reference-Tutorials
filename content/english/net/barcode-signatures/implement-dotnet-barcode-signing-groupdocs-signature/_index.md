---
title: "Complete .NET Barcode Signing Tutorial with GroupDocs.Signature"
linktitle: ".NET Barcode Signing Tutorial"
description: "Master barcode signing in .NET with GroupDocs.Signature. Step-by-step tutorial covering GS1CompositeBar, HIBCCode39LIC, and HIBCCode128LIC implementation for secure document authentication."
keywords: "dotnet barcode signing tutorial, GroupDocs Signature .NET implementation, GS1 barcode PDF signing, HIBC barcode document authentication, secure PDF barcode signing GroupDocs"
weight: 1
url: "/net/barcode-signatures/implement-dotnet-barcode-signing-groupdocs-signature/"
date: "2025-01-02"
lastmod: "2025-01-02"
categories: [".NET Development"]
tags: ["barcode-signing", "document-security", "groupdocs", "pdf-automation"]
type: docs
---
# Complete .NET Barcode Signing Tutorial with GroupDocs.Signature

Ever wondered how major companies secure their digital documents with those tiny, data-packed barcodes? You're about to discover the exact process. This **dotnet barcode signing tutorial** will walk you through implementing professional-grade barcode authentication using GroupDocs.Signature for .NET.

Whether you're building a supply chain management system, healthcare document platform, or just need to add that extra layer of security to your PDFs, this guide has you covered. By the end, you'll know exactly how to implement GS1CompositeBar, HIBCCode39LIC, and HIBCCode128LIC barcode signatures – and more importantly, when to use each one.

## Why Choose Barcode Signing for Your .NET Applications?

Before diving into the code, let's address the elephant in the room: why barcodes? In an age of QR codes and digital signatures, barcode signing might seem old-school. Here's why it's actually brilliant:

**Industry Compliance**: Many sectors (healthcare, pharmaceuticals, logistics) require specific barcode standards. HIBC barcodes, for example, are mandatory for medical device tracking in many countries.

**Offline Verification**: Unlike digital certificates that need online validation, barcodes can be read and verified with simple scanners – perfect for warehouses or remote locations.

**Data Density**: Modern barcode types can pack surprising amounts of information into a small space. GS1CompositeBar can store product details, batch numbers, expiration dates, and more.

**Universal Compatibility**: Every smartphone can scan barcodes, making your documents instantly verifiable by anyone.

## Prerequisites and Environment Setup

You'll need a few things before we start coding:

### Essential Requirements
- **.NET Framework 4.6.1+** or **.NET Core 2.0+** (works with .NET 5, 6, 7, and 8 too)
- **Visual Studio 2019** or later (VS Code works fine too)
- **Basic C# knowledge** – if you can write a simple class, you're good to go
- **A PDF document** to test with (any PDF will do)

### Installing GroupDocs.Signature: Three Ways That Actually Work

I've seen developers struggle with NuGet installations, so here are three foolproof methods:

#### Method 1: .NET CLI (Recommended)
```bash
dotnet add package GroupDocs.Signature
```

#### Method 2: Package Manager Console
```powershell
Install-Package GroupDocs.Signature
```

#### Method 3: Visual Studio Package Manager UI
1. Right-click your project → "Manage NuGet Packages"
2. Browse tab → Search "GroupDocs.Signature"
3. Install the one by GroupDocs (should be the first result)

**Pro Tip**: Always check the package has downloaded properly by looking for `GroupDocs.Signature.dll` in your bin folder after building.

### License Setup (Don't Skip This!)

Here's what most tutorials don't tell you: GroupDocs.Signature needs proper licensing for production use. Here's your roadmap:

**Development Phase**:
- **Free Trial**: Perfect for learning and testing – [Download here](https://releases.groupdocs.com/signature/net/)
- **Temporary License**: Needed for extended development – [Get it here](https://purchase.groupdocs.com/temporary-license/)

**Production Phase**:
- **Full License**: Required for deployment – [Purchase here](https://purchase.groupdocs.com/buy)

### Basic Project Setup

Let's get the foundation right:

```csharp
using GroupDocs.Signature;
using GroupDocs.Signature.Options;
using System.IO;

namespace BarcodeSigningDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            string filePath = "YOUR_DOCUMENT_DIRECTORY/Sample.pdf";
            
            // This is your starting point for any barcode signing operation
            using (var signature = new Signature(filePath))
            {
                // All the magic happens here
            }
        }
    }
}
```

## Understanding Barcode Types: Which One Should You Use?

This is where most developers get confused. Let me break down the three main types we'll implement and when to use each:

### GS1CompositeBar: The Supply Chain Powerhouse

**Best for**: Product tracking, inventory management, retail applications
**Data capacity**: Extremely high – can store GTINs, batch numbers, expiration dates, and more
**Industry use**: Retail, manufacturing, logistics

Think of GS1CompositeBar as the Swiss Army knife of barcodes. It's what you see on products in stores, but way more powerful.

### HIBCCode39LIC: Healthcare's Reliable Workhorse

**Best for**: Medical devices, pharmaceutical tracking, patient records
**Data capacity**: Moderate – good balance of size and information
**Industry use**: Healthcare, pharmaceuticals, medical device manufacturing

This is your go-to for anything health-related. It's specifically designed for healthcare industry compliance.

### HIBCCode128LIC: Maximum Data Density

**Best for**: Complex healthcare data, detailed patient information, regulatory compliance
**Data capacity**: High – more information than Code39 in the same space
**Industry use**: Advanced healthcare systems, pharmaceutical research

When HIBCCode39LIC isn't enough, this is your upgrade path.

## Implementation Guide: Let's Build Something Real

Now for the fun part – actually implementing these barcode signatures. I'll walk you through each type with real-world examples and explain the "why" behind each parameter.

### GS1CompositeBar Implementation: Supply Chain Document Signing

Here's how to implement GS1CompositeBar signing for supply chain documents. This example shows how you'd sign a shipping manifest or product certificate:

#### Setting Up GS1CompositeBar Options

```csharp
using GroupDocs.Signature.Options;

string filePath = Path.Combine("YOUR_DOCUMENT_DIRECTORY", "Sample.pdf");

// The data string follows GS1 standards - this example includes:
// (01) = GTIN, (21) = Serial number
var bc_GS1CompositeBar = new BarcodeSignOptions("(01)03212345678906|(21)A1B2C3D4E5F6G7H8", BarcodeTypes.GS1CompositeBar)
{
    Top = 100, // 100 pixels from top of page
    Left = 50, // Optional: 50 pixels from left edge
    Width = 200, // Optional: barcode width
    Height = 50, // Optional: barcode height
    ReturnContent = true, // This saves the barcode image for later use
    ReturnContentType = FileType.PNG // Save as PNG for quality
};
```

**What's happening here?** The data string `"(01)03212345678906|(21)A1B2C3D4E5F6G7H8"` follows GS1 Application Identifier standards. The `(01)` identifies a GTIN (Global Trade Item Number), while `(21)` is a serial number. The pipe `|` separates different data elements.

#### Signing the Document

```csharp
using (Signature signature = new Signature(filePath))
{
    string outputFilePath = Path.Combine("YOUR_OUTPUT_DIRECTORY", "SignWithBarcodeTypes", "Sample_GS1_Signed.pdf");
    
    try
    {
        SignResult signResult = signature.Sign(outputFilePath, bc_GS1CompositeBar);
        
        Console.WriteLine($"Document signed successfully!");
        Console.WriteLine($"Output file: {outputFilePath}");
        Console.WriteLine($"Signatures created: {signResult.Succeeded.Count}");
    }
    catch (Exception ex)
    {
        Console.WriteLine($"Signing failed: {ex.Message}");
    }
}
```

### HIBCCode39LIC Implementation: Healthcare Document Authentication

Healthcare documents require special handling. Here's how to implement HIBC barcode signing for medical records or device certificates:

#### Setting Up HIBCCode39LIC Options

```csharp
// HIBC data format: +A99912345/$$52001510X3
// + = Start character, A999 = Labeler ID, 12345 = Product ID
// /$$520015 = Date (YYDDD format), 10X3 = Check characters
var bc_HIBCLICCode39 = new BarcodeSignOptions("+A99912345/$$52001510X3", BarcodeTypes.HIBCCode39LIC)
{
    Top = 300, // Position below the GS1 barcode
    Left = 50,
    Width = 250, // HIBC codes often need more width for readability
    Height = 60,
    ReturnContent = true,
    ReturnContentType = FileType.PNG,
    
    // Additional formatting options
    ForeColor = System.Drawing.Color.Black,
    BackgroundColor = System.Drawing.Color.White
};
```

**Healthcare Compliance Note**: The data format here follows HIBC standards exactly. The `+A999` prefix identifies the manufacturer, and the date format `$$520015` represents day 152 of 2020. This isn't arbitrary – it's required for FDA compliance in many cases.

#### Signing with Error Handling

```csharp
using (Signature signature = new Signature(filePath))
{
    string outputFilePath = Path.Combine("YOUR_OUTPUT_DIRECTORY", "SignWithBarcodeTypes", "Sample_HIBC39_Signed.pdf");
    
    try
    {
        SignResult signResult = signature.Sign(outputFilePath, bc_HIBCLICCode39);
        
        // Verify the signature was created successfully
        if (signResult.Succeeded.Count > 0)
        {
            Console.WriteLine("HIBC Code39 signature added successfully!");
            
            // Optional: Log signature details for audit trail
            foreach (var signature_result in signResult.Succeeded)
            {
                Console.WriteLine($"Signature ID: {signature_result.SignatureId}");
                Console.WriteLine($"Position: Top={signature_result.Top}, Left={signature_result.Left}");
            }
        }
    }
    catch (GroupDocsSignatureException ex)
    {
        Console.WriteLine($"GroupDocs specific error: {ex.Message}");
    }
    catch (Exception ex)
    {
        Console.WriteLine($"General error: {ex.Message}");
    }
}
```

### HIBCCode128LIC Implementation: High-Density Healthcare Data

When you need to pack more information into your healthcare barcodes, HIBCCode128LIC is your answer:

#### Setting Up HIBCCode128LIC Options

```csharp
// Same data format as Code39, but Code128 can handle it more efficiently
var bc_HIBCLICCode128 = new BarcodeSignOptions("+A99912345/$$52001510X3", BarcodeTypes.HIBCCode128LIC)
{
    Top = 500, // Position below previous barcodes
    Left = 50,
    Width = 200, // Code128 is more compact than Code39
    Height = 50,
    ReturnContent = true,
    ReturnContentType = FileType.PNG,
    
    // Code128 specific optimizations
    Border = new Border()
    {
        Color = System.Drawing.Color.Black,
        DashStyle = System.Drawing.Drawing2D.DashStyle.Solid,
        Weight = 1,
        Visible = true
    }
};
```

#### Advanced Signing with Batch Processing

```csharp
using (Signature signature = new Signature(filePath))
{
    string outputFilePath = Path.Combine("YOUR_OUTPUT_DIRECTORY", "SignWithBarcodeTypes", "Sample_HIBC128_Signed.pdf");
    
    // You can sign with multiple barcode types in one operation
    var signOptions = new List<SignOptions> { bc_HIBCLICCode128 };
    
    SignResult signResult = signature.Sign(outputFilePath, signOptions);
    
    Console.WriteLine($"Batch signing completed!");
    Console.WriteLine($"Total signatures: {signResult.Succeeded.Count}");
    Console.WriteLine($"Failed signatures: {signResult.Failed.Count}");
    
    // Handle any failures
    if (signResult.Failed.Count > 0)
    {
        foreach (var failure in signResult.Failed)
        {
            Console.WriteLine($"Failed signature: {failure.Error}");
        }
    }
}
```

## Real-World Implementation Scenarios

Let me show you how these barcode types work in actual business scenarios:

### Scenario 1: E-commerce Order Fulfillment System

```csharp
public class OrderFulfillmentService
{
    public void SignShippingLabel(string orderNumber, string productGTIN, DateTime shippingDate)
    {
        // Create GS1 data for shipping label
        string gs1Data = $"(01){productGTIN}|(02){orderNumber}|(13){shippingDate:yyyyMMdd}";
        
        var barcodeOptions = new BarcodeSignOptions(gs1Data, BarcodeTypes.GS1CompositeBar)
        {
            Top = 50,
            Left = 300, // Position on shipping label
            Width = 150,
            Height = 75
        };
        
        // Sign the shipping label PDF
        using (var signature = new Signature("ShippingLabelTemplate.pdf"))
        {
            signature.Sign($"ShippingLabel_{orderNumber}.pdf", barcodeOptions);
        }
    }
}
```

### Scenario 2: Medical Device Certificate Generation

```csharp
public class MedicalDeviceCertificateGenerator
{
    public void GenerateDeviceCertificate(string deviceId, string lotNumber, DateTime manufacturingDate)
    {
        // HIBC format for medical device tracking
        string hibcData = $"+{deviceId}/{lotNumber}$${manufacturingDate:yyddd}";
        
        var hibcOptions = new BarcodeSignOptions(hibcData, BarcodeTypes.HIBCCode128LIC)
        {
            Top = 200,
            Left = 100,
            Width = 200,
            Height = 60,
            ReturnContent = true // Save for quality control verification
        };
        
        using (var signature = new Signature("DeviceCertificateTemplate.pdf"))
        {
            var result = signature.Sign($"Certificate_{deviceId}.pdf", hibcOptions);
            
            // Log for regulatory compliance
            LogCertificateGeneration(deviceId, result);
        }
    }
    
    private void LogCertificateGeneration(string deviceId, SignResult result)
    {
        // Implementation for audit trail
    }
}
```

## Common Pitfalls and Solutions

After helping hundreds of developers implement barcode signing, here are the issues I see most often:

### Issue 1: "Invalid Barcode Data Format" Errors

**Problem**: Your barcode data doesn't match the expected format for the barcode type.

**Solution**: Always validate your data format before creating the barcode options:

```csharp
public static bool ValidateGS1Data(string data)
{
    // GS1 data should start with application identifier in parentheses
    var pattern = @"^\(\d{2,4}\).*";
    return System.Text.RegularExpressions.Regex.IsMatch(data, pattern);
}

public static bool ValidateHIBCData(string data)
{
    // HIBC data should start with +
    return data.StartsWith("+") && data.Length >= 4;
}
```

### Issue 2: Barcodes Appearing Cut Off or Distorted

**Problem**: Your barcode dimensions don't match the data complexity or document layout.

**Solution**: Calculate appropriate dimensions based on your data:

```csharp
private static BarcodeSignOptions CreateOptimalBarcodeOptions(string data, BarcodeType type)
{
    var options = new BarcodeSignOptions(data, type);
    
    // Adjust dimensions based on data length and type
    switch (type.Name)
    {
        case "GS1CompositeBar":
            options.Width = Math.Max(150, data.Length * 5);
            options.Height = 75;
            break;
        case "HIBCCode39LIC":
            options.Width = Math.Max(200, data.Length * 8); // Code39 needs more space
            options.Height = 60;
            break;
        case "HIBCCode128LIC":
            options.Width = Math.Max(150, data.Length * 4); // Code128 is more compact
            options.Height = 50;
            break;
    }
    
    return options;
}
```

### Issue 3: Performance Issues with Large Document Batches

**Problem**: Signing multiple documents is taking too long.

**Solution**: Implement batch processing with proper resource management:

```csharp
public async Task SignDocumentsBatch(IEnumerable<string> documentPaths, BarcodeSignOptions barcodeOptions)
{
    var semaphore = new SemaphoreSlim(Environment.ProcessorCount); // Limit concurrent operations
    
    var tasks = documentPaths.Select(async path =>
    {
        await semaphore.WaitAsync();
        try
        {
            using (var signature = new Signature(path))
            {
                var outputPath = Path.ChangeExtension(path, ".signed.pdf");
                await Task.Run(() => signature.Sign(outputPath, barcodeOptions));
            }
        }
        finally
        {
            semaphore.Release();
        }
    });
    
    await Task.WhenAll(tasks);
}
```

## Performance Optimization Tips

Here's how to make your barcode signing blazingly fast:

### Memory Management Best Practices

```csharp
// DON'T do this - creates memory leaks
public void BadExample()
{
    for (int i = 0; i < 1000; i++)
    {
        var signature = new Signature("document.pdf"); // Never disposed!
        signature.Sign("output.pdf", options);
    }
}

// DO this - proper resource disposal
public void GoodExample()
{
    var options = new BarcodeSignOptions(data, BarcodeTypes.GS1CompositeBar);
    
    for (int i = 0; i < 1000; i++)
    {
        using (var signature = new Signature($"document{i}.pdf"))
        {
            signature.Sign($"output{i}.pdf", options);
        } // Automatically disposed here
    }
}
```

### Caching Strategies for Better Performance

```csharp
private static readonly ConcurrentDictionary<string, BarcodeSignOptions> _optionsCache = 
    new ConcurrentDictionary<string, BarcodeSignOptions>();

public BarcodeSignOptions GetCachedBarcodeOptions(string data, BarcodeType type)
{
    string cacheKey = $"{data}_{type.Name}";
    
    return _optionsCache.GetOrAdd(cacheKey, key => new BarcodeSignOptions(data, type)
    {
        Width = CalculateOptimalWidth(data, type),
        Height = CalculateOptimalHeight(type),
        ReturnContent = false // Don't generate images unless needed
    });
}
```

## Advanced Troubleshooting Guide

### Debug Mode: Understanding What's Going Wrong

When things go sideways (and they will), enable detailed logging:

```csharp
public void SignWithDetailedLogging(string filePath, BarcodeSignOptions options)
{
    using (var signature = new Signature(filePath))
    {
        try
        {
            // Enable detailed error information
            signature.Options.SaveOptions.OverwriteExistingFiles = true;
            signature.Options.SaveOptions.AddMissingExtenstion = true;
            
            var result = signature.Sign("output.pdf", options);
            
            // Log success details
            Console.WriteLine($"Success! Created {result.Succeeded.Count} signatures");
            
            foreach (var sig in result.Succeeded)
            {
                Console.WriteLine($"Signature: {sig.SignatureId} at position ({sig.Top}, {sig.Left})");
            }
        }
        catch (Exception ex)
        {
            Console.WriteLine($"Error Type: {ex.GetType().Name}");
            Console.WriteLine($"Error Message: {ex.Message}");
            Console.WriteLine($"Stack Trace: {ex.StackTrace}");
            
            // Check for specific GroupDocs exceptions
            if (ex is GroupDocsSignatureException gdEx)
            {
                Console.WriteLine($"GroupDocs Error Code: {gdEx.ErrorCode}");
            }
        }
    }
}
```

### Common Exception Types and Solutions

| Exception Type | Common Cause | Solution |
|----------------|--------------|----------|
| `ArgumentException` | Invalid barcode data format | Validate data format before signing |
| `FileNotFoundException` | Input file path incorrect | Check file exists and path is correct |
| `UnauthorizedAccessException` | File permissions issue | Check file isn't locked, verify permissions |
| `GroupDocsSignatureException` | License or API issue | Verify license status, check API usage |
| `OutOfMemoryException` | Processing large files | Implement batch processing, dispose resources |

## Testing Your Implementation

Here's a comprehensive test suite to ensure your barcode signing works perfectly:

```csharp
[TestClass]
public class BarcodeSigningTests
{
    private string testDocumentPath;
    private string outputDirectory;
    
    [TestInitialize]
    public void Setup()
    {
        testDocumentPath = "TestAssets/sample.pdf";
        outputDirectory = "TestOutputs";
        Directory.CreateDirectory(outputDirectory);
    }
    
    [TestMethod]
    public void TestGS1CompositeBarSigning()
    {
        var options = new BarcodeSignOptions("(01)12345678901234|(21)SERIAL123", BarcodeTypes.GS1CompositeBar);
        
        using (var signature = new Signature(testDocumentPath))
        {
            var outputPath = Path.Combine(outputDirectory, "gs1_test.pdf");
            var result = signature.Sign(outputPath, options);
            
            Assert.IsTrue(result.Succeeded.Count > 0);
            Assert.IsTrue(File.Exists(outputPath));
        }
    }
    
    [TestMethod]
    public void TestInvalidBarcodeDataThrowsException()
    {
        var options = new BarcodeSignOptions("INVALID_DATA", BarcodeTypes.HIBCCode39LIC);
        
        using (var signature = new Signature(testDocumentPath))
        {
            Assert.ThrowsException<ArgumentException>(() =>
            {
                signature.Sign("output.pdf", options);
            });
        }
    }
    
    [TestMethod]
    public void TestMultipleBarcodeTypesInOneDocument()
    {
        var gs1Options = new BarcodeSignOptions("(01)12345678901234", BarcodeTypes.GS1CompositeBar) { Top = 100 };
        var hibcOptions = new BarcodeSignOptions("+A12345", BarcodeTypes.HIBCCode39LIC) { Top = 200 };
        
        using (var signature = new Signature(testDocumentPath))
        {
            var outputPath = Path.Combine(outputDirectory, "multiple_barcodes.pdf");
            var result = signature.Sign(outputPath, new List<SignOptions> { gs1Options, hibcOptions });
            
            Assert.AreEqual(2, result.Succeeded.Count);
        }
    }
}
```

## Conclusion: You're Now Ready for Production

Congratulations! You've mastered the art of .NET barcode signing with GroupDocs.Signature. Let's recap what you've learned:

✅ **Three powerful barcode types** and when to use each one  
✅ **Production-ready code examples** with proper error handling  
✅ **Performance optimization** techniques for large-scale applications  
✅ **Troubleshooting strategies** for when things go wrong  
✅ **Real-world scenarios** from e-commerce to healthcare  

### What's Next?

1. **Start Small**: Pick one barcode type and implement it in a test project
2. **Expand Gradually**: Add error handling, then performance optimizations
3. **Go Live**: Deploy with confidence using the patterns you've learned

The world of secure document management is at your fingertips. Whether you're tracking products across global supply chains or ensuring healthcare compliance, you now have the tools to build professional-grade barcode signing systems.

**Ready to implement this in your own project?** Start with the GS1CompositeBar example – it's the most versatile and will teach you the core concepts quickly.

## Frequently Asked Questions

**Q: Can I use GroupDocs.Signature with other document formats besides PDF?**  
A: Absolutely! GroupDocs.Signature supports Word documents (.docx), Excel spreadsheets (.xlsx), PowerPoint presentations (.pptx), and many image formats. The barcode signing process is nearly identical across formats.

**Q: How do I handle barcode signing in a multi-tenant application?**  
A: Create separate output directories for each tenant and include tenant ID in your file naming convention. Always validate that users can only access their own documents. Consider implementing resource quotas to prevent abuse.

**Q: What's the maximum amount of data I can encode in these barcode types?**  
A: GS1CompositeBar can handle up to 2,335 alphanumeric characters, HIBCCode39LIC supports about 43 characters efficiently, and HIBCCode128LIC can handle up to 99 characters efficiently. However, practical scanning reliability decreases with data density.

**Q: Can I customize the appearance of the barcodes (colors, borders, fonts)?**  
A: Yes! You can customize foreground color, background color, borders, and positioning. However, be careful with colors – ensure sufficient contrast for reliable scanning. Black on white is always the safest choice.

**Q: How do I verify that a barcode was signed correctly without a physical scanner?**  
A: Enable `ReturnContent = true` in your barcode options. This saves a PNG image of the generated barcode that you can inspect visually or process programmatically for quality control.

**Q: Is there a way to batch sign multiple documents with different barcode data?**  
A: Definitely! Create a dictionary mapping document paths to barcode data, then iterate through it. Use the async batch processing pattern I showed in the performance section for best results.

**Q: What happens if I try to sign a document that already has barcodes?**  
A: GroupDocs.Signature will add your new barcodes alongside existing ones. If you need to replace existing barcodes, you'll need to remove them first using the signature search and delete functionality.

**Q: Can I sign password-protected PDFs?**  
A: Yes, but you'll need to provide the password when initializing the Signature class: `new Signature(filePath, new LoadOptions { Password = "your_password" })`.

**Q: How do I handle licensing in a production environment?**  
A: Store your license file securely (not in source control) and load it at application startup using `License.SetLicense()`. For cloud deployments, consider using environment variables or secure key management services.

**Q: What's the best way to position barcodes so they don't interfere with document content?**  
A: Analyze your document template first. Common safe zones are: bottom-right corner, header/footer areas, or dedicated signature blocks. Use the document's page dimensions to calculate relative positions rather than fixed pixel values.

## Resources and Next Steps

**Documentation**: [GroupDocs.Signature for .NET Documentation](https://docs.groupdocs.com/signature/net/)  
**API Reference**: [Complete API Documentation](https://reference.groupdocs.com/signature/net/)  
**Download**: [Get GroupDocs.Signature for .NET](https://releases.groupdocs.com/signature/net/)  
**Licensing**: [Purchase a License](https://purchase.groupdocs.com/buy)  
**Support**: [Community Forum](https://forum.groupdocs.com/c/signature/)  
**Free Trial**: [Try Before You Buy](https://releases.groupdocs.com/signature/net/)  
**Temporary License**: [Extended Development License](https://purchase.groupdocs.com/temporary-license/)