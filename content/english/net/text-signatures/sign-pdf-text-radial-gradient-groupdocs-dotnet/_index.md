---
title: "Add Text Signature to PDF in C# with Custom Gradients"
linktitle: "Text Signature to PDF C#"
description: "Learn how to add professional text signatures to PDFs in C# using GroupDocs.Signature for .NET. Includes gradient customization, code examples, and best practices."
keywords: "add text signature to PDF C#, PDF signature .NET library, customize PDF signatures C#, electronic signature PDF .NET, GroupDocs.Signature tutorial"
weight: 1
url: "/net/text-signatures/sign-pdf-text-radial-gradient-groupdocs-dotnet/"
date: "2025-01-02"
lastmod: "2025-01-02"
categories: ["PDF Processing"]
tags: ["csharp", "pdf-signature", "dotnet", "groupdocs", "document-automation"]
---

# Add Text Signature to PDF in C# with Custom Gradients

## Introduction

Let's be honest—manually signing PDFs or dealing with clunky third-party signing tools gets old fast, especially when you're processing dozens (or hundreds) of documents. If you're building a .NET application that needs to add professional-looking signatures to PDFs programmatically, you've probably wondered: how do I make those signatures actually look good while keeping the process automated?

Here's the thing: basic text stamps work, but they don't exactly scream "professional." What if you could add text signatures with smooth gradient backgrounds that look like they came from premium design software? That's exactly what we'll cover in this guide.

You'll learn how to use GroupDocs.Signature for .NET to add customizable text signatures to PDF documents—complete with eye-catching radial gradients. Whether you're building an invoice system, contract management platform, or any document workflow, this approach gives you the flexibility to match your brand while maintaining that polished, professional appearance.

**What you'll master by the end:**
- Setting up GroupDocs.Signature for .NET in your project (it's easier than you think)
- Adding text signatures to PDFs programmatically
- Creating stunning radial gradient backgrounds for signatures
- Customizing every aspect of your signature's appearance
- Avoiding common pitfalls that trip up developers

Let's dive in and get those PDFs signed with style!

## Why Choose GroupDocs.Signature for PDF Signing?

Before we jump into code, you might be wondering: why GroupDocs.Signature specifically? Fair question—there are other PDF libraries out there.

Here's what sets it apart for signature work:

**Purpose-built for signatures**: Unlike general PDF libraries where you're piecing together low-level drawing commands, GroupDocs.Signature is designed specifically for document signing. This means fewer lines of code and less room for errors.

**Multiple signature types**: Text signatures are just the beginning. The library supports image signatures, digital certificates, QR codes, barcodes, and metadata stamps—all with a consistent API.

**Professional appearance out of the box**: Those gradient brushes we're about to use? They're built-in features, not something you have to calculate pixel-by-pixel. The library handles the rendering complexity while you focus on your application logic.

**Cross-format support**: While we're focusing on PDFs here, the same code patterns work for Word documents, Excel spreadsheets, and more. Learn it once, use it everywhere.

That said, if you're just adding simple watermarks or need basic PDF manipulation, you might not need this library's full power. But for professional document signing with customization options? It's hard to beat.

## Prerequisites

Let's make sure you've got everything lined up before we start coding. Nothing's worse than getting halfway through a tutorial and realizing you're missing a critical piece.

### Required Libraries and Dependencies

You'll need **GroupDocs.Signature for .NET** installed in your project. The library requires .NET Framework 4.6.1 or later (or .NET Core 2.0+, or .NET 5/6/7/8 if you're on the newer frameworks).

Don't worry about hunting down additional dependencies—the NuGet package handles everything automatically. That's one of the nice things about working with well-maintained libraries.

### Environment Setup Requirements

Any IDE that supports .NET development will work, but most developers use **Visual Studio 2019 or later** (Community Edition is perfectly fine). If you're more of a VS Code person, that works too with the C# extension installed.

Make sure your project targets .NET Framework 4.6.1 at minimum. If you're starting fresh, I'd recommend .NET 6 or later for the best performance and modern language features.

### Knowledge Prerequisites

This guide assumes you're comfortable with:
- Basic C# syntax (variables, methods, using statements)
- File path operations in .NET
- The concept of electronic signatures (nothing too deep though)

If you're newer to .NET, don't stress—I'll explain each code block as we go. The actual implementation is more straightforward than it might seem at first glance.

## Setting Up GroupDocs.Signature for .NET

Alright, let's get the library installed. You've got three ways to do this, so pick whichever matches your workflow:

### Installation Options

**.NET CLI** (if you're a terminal person):
```bash
dotnet add package GroupDocs.Signature
```

**Package Manager Console** (classic Visual Studio approach):
```powershell
Install-Package GroupDocs.Signature
```

**NuGet Package Manager UI** (point-and-click):
1. Right-click your project → Manage NuGet Packages
2. Search for "GroupDocs.Signature"
3. Click Install on the latest stable version

Pro tip: Always grab the latest stable version unless you have a specific reason not to. GroupDocs regularly pushes performance improvements and bug fixes.

### License Acquisition Steps

Here's the licensing situation (and it's pretty straightforward):

**Free Trial**: When you first install the library, you can use it without a license, but there'll be watermarks on your output and some limitations. Perfect for testing whether this is the right solution for your needs.

**Temporary License**: Need to do a proper evaluation without watermarks? Grab a free 30-day temporary license from the [GroupDocs website](https://purchase.groupdocs.com/temporary-license/). No credit card required, just a quick form.

**Full License**: For production use, you'll need to [purchase a license](https://purchase.groupdocs.com/buy). They offer different tiers based on your needs (developer, site, or enterprise licenses).

The licensing model is developer-friendly: buy once, use in multiple projects. No per-document fees or usage limits.

### Basic Initialization and Setup

Once installed, here's how you initialize the library in your code:

```csharp
using GroupDocs.Signature;

// Initialize the Signature object with your document path
Signature signature = new Signature("YOUR_DOCUMENT_DIRECTORY\\Sample.pdf");
```

Quick note on that path: Use `Path.Combine()` or `@"literal strings"` to avoid headaches with backslash escaping. Trust me on this—path-related bugs are frustrating because they work fine on your machine but fail mysteriously in production.

If you've got a license file, you'll apply it before creating the Signature object (usually in your startup configuration):

```csharp
// Apply license (do this once at application startup)
License license = new License();
license.SetLicense("path-to-your-license-file.lic");
```

That's it for setup! Now let's get to the fun part: actually signing some PDFs.

## How to Add Text Signatures with Radial Gradients to PDFs

This is where things get interesting. We're going to walk through the complete process of adding a text signature with a smooth radial gradient background—the kind that makes your documents look professionally designed rather than programmatically stamped.

### Understanding the Feature: Text Signatures with Radial Gradient Brushes

First, let's clarify what we're building here. A **text signature** is exactly what it sounds like: text rendered directly onto your PDF as a signature. Could be a name, a title, a stamp phrase—whatever you need.

The **radial gradient** is what makes it pop. Instead of a flat background color, you get a smooth color transition radiating from the center outward (think of a spotlight effect). This creates depth and draws the eye without being overly flashy.

Why does this matter? Because in business documents, presentation matters. A well-designed signature conveys professionalism and attention to detail. Plus, gradients naturally work with most color schemes without clashing.

### Step 1: Set Up Your Document Paths

Before we touch any signature code, let's organize our file paths. Hardcoding paths is a recipe for confusion later, so we'll define them clearly at the start:

```csharp
string filePath = "YOUR_DOCUMENT_DIRECTORY\\Sample.pdf";
string outputFilePath = Path.Combine("YOUR_OUTPUT_DIRECTORY", "SignWithBrushes", "SignedLinearRadialBrush.pdf");
```

**What's happening here:**
- `filePath` points to your input PDF (the unsigned document)
- `outputFilePath` uses `Path.Combine()` to safely build the output path, creating subdirectories if needed

Replace `YOUR_DOCUMENT_DIRECTORY` and `YOUR_OUTPUT_DIRECTORY` with your actual paths. In production, you'd typically pull these from configuration files rather than hardcoding them.

Pro tip: The library doesn't modify the original document—it always creates a new file. This is intentional and actually a good thing for audit trails and safety.

### Step 2: Initialize the Signature Object

Now we create the Signature instance that'll handle all the heavy lifting:

```csharp
using (Signature signature = new Signature(filePath))
{
    // All signing operations happen inside this block
}
```

**Why the `using` statement?** It ensures proper disposal of resources when we're done. The Signature object opens file handles and allocates memory, so letting it clean up automatically prevents memory leaks. This is especially important if you're processing multiple documents in a loop.

If you forget the `using` statement and run this in a long-running application, you might hit file lock issues or memory problems. Been there, debugged that—just use `using`.

### Step 3: Configure Your Text Signature Options

This is where the magic happens. We're going to create a `TextSignOptions` object and configure every aspect of how our signature looks:

```csharp
TextSignOptions options = new TextSignOptions("John Smith")
{
    Background = new Background()
    {
        Color = Color.LimeGreen,
        Transparency = 0.5,
        Brush = new RadialGradientBrush(Color.LimeGreen, Color.DarkGreen)
    },
    Width = 100,
    Height = 80,
    VerticalAlignment = Domain.VerticalAlignment.Center,
    HorizontalAlignment = Domain.HorizontalAlignment.Center,
    Margin = new Padding() { Top = 20, Right = 20 },
    SignatureImplementation = TextSignatureImplementation.Image
};
```

Let's break down each configuration option (because there's a lot going on here):

**The Text**: `"John Smith"` is the actual text that'll appear in your signature. This could be dynamic—pulled from a database, user input, or configuration.

**Background Configuration**:
- `Color = Color.LimeGreen`: The base background color. Even with a gradient, this affects the overall tone.
- `Transparency = 0.5`: Makes the background 50% transparent (0 = fully transparent, 1 = fully opaque). Adjust this based on whether you want the signature to blend subtly or stand out boldly.
- `Brush = new RadialGradientBrush(Color.LimeGreen, Color.DarkGreen)`: Here's the gradient itself. The first color (LimeGreen) starts at the center, gradually transitioning to the second color (DarkGreen) at the edges.

**Dimensions**:
- `Width = 100` and `Height = 80`: Size in pixels. Scale these based on your document size and desired prominence. For standard PDFs, 100-150px width usually looks good.

**Positioning**:
- `VerticalAlignment` and `HorizontalAlignment`: Controls where the signature appears. `Center/Center` places it dead center. You can also use `Top`, `Bottom`, `Left`, or `Right` for different placements.
- `Margin`: Fine-tune positioning with pixel offsets. This signature will be 20 pixels from the top and 20 from the right.

**Implementation Type**:
- `SignatureImplementation = TextSignatureImplementation.Image`: Renders the signature as an image layer on the PDF. This gives you the most control over appearance and ensures consistent rendering across all PDF viewers.

### When to Use Radial Gradients (and When to Skip Them)

Quick decision guide: Radial gradients work best for:
- Approval stamps ("APPROVED", "REVIEWED")
- Centered signatures on certificates
- Eye-catching watermarks
- Situations where you want visual emphasis

Skip them for:
- Signatures that need to blend into the background
- Dense documents where they might be distracting
- Cases where simplicity is paramount
- Accessibility-focused documents (stick to high-contrast solid colors)

If you want a more subtle effect, try a linear gradient instead by using `LinearGradientBrush` with the same color scheme. Or just use a solid color with `Color.FromArgb(alpha, r, g, b)` for simple transparency.

### Step 4: Sign and Save the Document

Final step—actually apply the signature and write out the new PDF:

```csharp
SignResult signResult = signature.Sign(outputFilePath, options);
```

That's it. One method call does everything: renders the signature, applies it to the document, and saves the result to your specified path.

The `SignResult` object contains useful metadata like:
- How many signatures were applied (useful if you're doing batch operations)
- Whether the signing succeeded
- Any warnings or issues encountered

In production code, you'd typically check `signResult.Succeeded` before continuing:

```csharp
if (signResult.Succeeded)
{
    Console.WriteLine($"Document signed successfully. Output: {outputFilePath}");
}
else
{
    // Handle errors
    Console.WriteLine("Signing failed. Check file paths and permissions.");
}
```

### Complete Working Example

Here's everything put together in one runnable method:

```csharp
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
using System.Drawing;
using System.IO;

public void SignPdfWithRadialGradient()
{
    string filePath = @"C:\Documents\Sample.pdf";
    string outputFilePath = Path.Combine(@"C:\Output", "SignWithBrushes", "SignedLinearRadialBrush.pdf");
    
    using (Signature signature = new Signature(filePath))
    {
        TextSignOptions options = new TextSignOptions("John Smith")
        {
            Background = new Background()
            {
                Color = Color.LimeGreen,
                Transparency = 0.5,
                Brush = new RadialGradientBrush(Color.LimeGreen, Color.DarkGreen)
            },
            Width = 100,
            Height = 80,
            VerticalAlignment = Domain.VerticalAlignment.Center,
            HorizontalAlignment = Domain.HorizontalAlignment.Center,
            Margin = new Padding() { Top = 20, Right = 20 },
            SignatureImplementation = TextSignatureImplementation.Image
        };
        
        SignResult signResult = signature.Sign(outputFilePath, options);
        Console.WriteLine($"Signed successfully: {signResult.Succeeded}");
    }
}
```

Copy this, update the paths, and you're good to go. Seriously, that's all the code needed for professional PDF signatures.

## Common Mistakes to Avoid

Let me save you some debugging time by pointing out the mistakes I see developers make with this library (and yes, I've made most of these myself):

### 1. File Path Issues

**The mistake**: Using relative paths without checking the working directory, or forgetting to escape backslashes.

**The fix**: Always use `Path.Combine()` for safety, or use verbatim strings (`@"C:\Path\To\File"`). Test your paths with `File.Exists()` before trying to sign.

```csharp
// Good: Clear and safe
string path = Path.Combine(baseDirectory, "subfolder", "document.pdf");

// Bad: Works on your machine, fails in production
string path = "..\\..\\documents\\file.pdf";
```

### 2. Forgetting the `using` Statement

**The mistake**: Creating a Signature object without proper disposal.

**The fix**: Always wrap in `using` or manually call `.Dispose()`. In long-running applications, this will bite you with file locks and memory leaks.

### 3. Transparency Confusion

**The mistake**: Setting `Transparency = 1` expecting a subtle signature, then wondering why it's invisible.

**The fix**: Remember, transparency is inverted from what you might expect. 0 = fully transparent (invisible), 1 = fully opaque (solid). For subtle signatures, use 0.3-0.5.

### 4. Signature Size Issues

**The mistake**: Using dimensions that are too small (invisible) or too large (overwhelming).

**The fix**: Start with Width=100, Height=80 as a baseline. Adjust based on your document size. For A4 PDFs, 80-150px width usually looks professional.

### 5. Color Contrast Problems

**The mistake**: Choosing gradient colors that clash with the document or lack contrast.

**The fix**: Test your color combinations on actual documents, not just white backgrounds. If readability is critical, skip gradients entirely and use high-contrast solid colors.

### 6. Not Checking SignResult

**The mistake**: Assuming the signing always succeeds and not handling failures.

**The fix**: Always check `signResult.Succeeded` before assuming success. Log errors for debugging:

```csharp
if (!signResult.Succeeded)
{
    Console.WriteLine($"Signing failed for {filePath}");
    // Log details, send alerts, whatever your error handling requires
}
```

## Practical Applications and Real-World Use Cases

Now that you know *how* to add signatures, let's talk about *when* you'd actually use this in production:

### 1. Automated Invoice Approval Systems

Imagine you've got an invoicing system where managers approve invoices electronically. Instead of printing, signing, and scanning, your application could:
- Generate the invoice as a PDF
- Add the manager's text signature with a company-branded gradient (matching your logo colors)
- Timestamp it automatically
- Store in your document management system

The radial gradient makes it clear at a glance that the invoice has been approved—it's not just plain text that could be easily overlooked.

### 2. Contract Management Platforms

For SaaS platforms handling contracts, you might need to add signature blocks for multiple parties. With this approach, you could:
- Programmatically add signature fields
- Customize the appearance based on role (different gradient colors for Client vs. Vendor signatures)
- Generate audit-ready documents that clearly show who signed and when

### 3. Certificate Generation

Educational platforms or training systems often need to generate certificates. Using text signatures with gradients lets you:
- Add professional-looking "CERTIFIED" or "COMPLETED" stamps
- Match your brand colors automatically
- Scale to thousands of certificates without manual intervention

### 4. Document Watermarking

While not strictly a "signature," the same technique works perfectly for watermarks. Add "DRAFT," "CONFIDENTIAL," or "SAMPLE" across documents with semi-transparent gradients that won't obscure the underlying content.

### Integration Possibilities

This library integrates smoothly with:
- **ASP.NET applications**: Add signing endpoints to your Web API
- **Document management systems**: Hook into upload/approval workflows
- **Workflow engines**: Trigger signing as part of automated business processes
- **Cloud storage**: Sign documents before uploading to AWS S3, Azure Blob Storage, etc.

The key is that it's just .NET code—if you can call a method, you can integrate it.

## Performance Considerations and Best Practices

Let's talk about making this fast and reliable in production environments.

### Memory Management

The library is generally efficient, but when processing large batches of documents, keep these in mind:

**Do this:**
- Process documents one at a time if memory is constrained
- Use `using` statements consistently
- Dispose of Signature objects immediately after use

**Avoid this:**
- Loading hundreds of Signature objects into memory simultaneously
- Keeping references to completed signatures
- Reusing Signature objects for multiple documents (create a new one each time)

### File I/O Optimization

PDF signing is I/O-bound (lots of reading and writing), so:

**Best practices:**
- Use fast local storage for temporary files (SSD preferred)
- Batch operations when possible rather than one-at-a-time processing
- Consider async/await patterns for web applications to avoid blocking threads

**Quick tip**: If you're processing many documents, create the output directory structure beforehand rather than letting the library create it on each operation. Small optimization, but it adds up.

### Scaling for Production

When moving from development to production:

1. **Test with large files**: That 50KB sample PDF? Try it with a 50MB multi-page contract. Performance characteristics change dramatically.

2. **Implement proper error handling**: Network hiccups, permission issues, and corrupt PDFs all happen in production. Wrap your signing operations in try-catch blocks with meaningful error messages.

3. **Add logging**: Log each signing operation with timing information. This helps you identify bottlenecks and track down issues when users report problems.

4. **Consider caching**: If you're applying the same signature to multiple documents, configure your options once and reuse the object (but still create a new Signature instance for each document).

### Library Version Updates

GroupDocs releases updates regularly. When updating:
- Check the changelog for breaking changes
- Test your signature appearance (rendering can occasionally change between versions)
- Take advantage of performance improvements and new features

## Troubleshooting Guide

Here are solutions to the most common issues you'll encounter:

### "File is being used by another process"

**Cause**: You forgot to dispose of the Signature object, or another application has the file open.

**Solution**:
```csharp
// Make sure you're using this pattern:
using (Signature sig = new Signature(path))
{
    // Do work
} // Automatically disposed here
```

Also check that your PDF isn't open in Adobe Reader or another viewer while testing.

### "Invalid license" or watermarks appearing

**Cause**: License file not found, expired, or not applied correctly.

**Solution**: Double-check your license path and ensure you're calling `SetLicense()` before creating any Signature objects. For temporary licenses, verify the expiration date.

### Signature appears in wrong location

**Cause**: Alignment and margin settings conflict or aren't what you expected.

**Solution**: Start simple:
```csharp
// Dead center, no margins
VerticalAlignment = Domain.VerticalAlignment.Center,
HorizontalAlignment = Domain.HorizontalAlignment.Center,
Margin = new Padding() { Top = 0, Right = 0 }
```

Then adjust margins incrementally until you get the placement you want. Remember: margins are relative to the alignment point.

### Gradient doesn't appear or looks wrong

**Cause**: Usually a transparency issue or color selection problem.

**Solution**:
1. Verify transparency is set correctly (0.5 for semi-transparent)
2. Try with high-contrast colors first (like White to Black) to ensure the gradient is working
3. Check that `SignatureImplementation = TextSignatureImplementation.Image` is set

### Output PDF is corrupted or won't open

**Cause**: Source PDF might be corrupted, or permissions issue writing to output directory.

**Solution**:
1. Test with a known-good PDF first
2. Verify you have write permissions to the output directory
3. Check that the output path doesn't exceed Windows path length limits (260 characters)

### Performance is slower than expected

**Cause**: Large PDF files, slow disk I/O, or processing too many documents sequentially.

**Solution**:
1. Profile your code to identify bottlenecks (is it file I/O or signature rendering?)
2. For batch operations, consider parallel processing with `Parallel.ForEach()`
3. Ensure you're using local storage, not network drives
4. Update to the latest library version (performance improvements are common)

## Frequently Asked Questions

### 1. Can I add multiple signatures to the same PDF?

Absolutely! Just call `signature.Sign()` multiple times with different options, or pass a list of signature options in a single call. Common pattern for documents needing multiple approval signatures:

```csharp
var options1 = new TextSignOptions("Approved by: Manager");
var options2 = new TextSignOptions("Reviewed by: QA");

// Apply both signatures
signature.Sign(outputPath, options1);
signature.Sign(outputPath, options2); // Adds to existing signatures
```

### 2. What's the difference between radial and linear gradients?

**Radial gradients** spread outward from a center point in a circular pattern—like a spotlight or ripple effect. Great for centered stamps and emphasis.

**Linear gradients** transition in a straight line from one side to another. Better for backgrounds that should complement rather than dominate, or for creating ribbon-like effects.

Choose based on the visual weight you want: radial for attention, linear for subtlety.

### 3. Can I use custom fonts for the text signature?

Yes! The `TextSignOptions` object has a `Font` property where you can specify:
```csharp
options.Font = new SignatureFont
{
    FontFamily = "Arial",
    Size = 24,
    Bold = true
};
```

Just make sure the font is installed on the machine running your code (or embed it if you're using a custom font).

### 4. Does this work with password-protected PDFs?

Yes, but you need to provide the password when initializing:
```csharp
LoadOptions loadOptions = new LoadOptions { Password = "your-pdf-password" };
using (Signature signature = new Signature(filePath, loadOptions))
{
    // Sign as usual
}
```

### 5. How do I sign specific pages in a multi-page PDF?

Use the `PagesSetup` property in your signature options:
```csharp
options.PagesSetup = new PagesSetup
{
    FirstPage = true,  // Sign first page
    LastPage = false,
    OddPages = false,
    EvenPages = false
};

// Or specify exact page numbers:
options.PagesSetup = new PagesSetup { PageNumbers = new List<int> { 1, 3, 5 } };
```

### 6. Can I rotate the signature?

Yes, use the `RotationAngle` property:
```csharp
options.RotationAngle = 45; // 45 degrees clockwise
```

Useful for diagonal watermarks or matching document orientation.

### 7. What if I need to verify signatures later?

GroupDocs.Signature also has verification capabilities. You can search for and verify signatures using the `Verify()` and `Search()` methods. Check the API documentation for details on signature verification workflows.

### 8. Does this create legally binding digital signatures?

The text signatures we've covered are visual signatures. For legally binding digital signatures with certificates, use the library's `DigitalSignOptions` instead, which supports X.509 certificates and creates cryptographically signed PDFs.

## Next Steps and Further Learning

Congratulations! You now know how to add professional-looking text signatures to PDFs in C#. But this is just scratching the surface of what GroupDocs.Signature can do.

### Explore More Signature Types

Once you're comfortable with text signatures, check out:
- **Image signatures**: Add scanned signature images or company logos
- **Digital signatures**: Implement certificate-based signing for legal compliance
- **QR codes and barcodes**: Embed machine-readable data in your documents
- **Metadata signatures**: Add invisible metadata for tracking and validation

### Integration Ideas

Think about how you might integrate this into your existing systems:
- Add a signing API endpoint to your web application
- Create a bulk signing utility for batch processing
- Build a workflow approval system with multi-step signatures
- Implement automatic watermarking for draft documents

### Expand Your Skills

To level up your document processing capabilities:
- Explore the GroupDocs.Viewer library for rendering documents
- Check out GroupDocs.Conversion for format transformations
- Learn about GroupDocs.Merger for combining and splitting documents

### Community and Support

Stuck on something? The GroupDocs community is active and helpful:
- Check the [support forum](https://forum.groupdocs.com/c/signature/) for common issues and solutions
- Browse the [documentation](https://docs.groupdocs.com/signature/net/) for detailed API references
- Review code samples on their website for more advanced scenarios

## Resources and Links

Everything you need to continue your GroupDocs.Signature journey:

- [Documentation](https://docs.groupdocs.com/signature/net/): Comprehensive API reference and guides
- [API Reference](https://reference.groupdocs.com/signature/net/): Detailed class and method documentation
- [Download Library](https://releases.groupdocs.com/signature/net/): Get the latest version
- [Purchase License](https://purchase.groupdocs.com/buy): Production licensing options
- [Free Trial](https://releases.groupdocs.com/signature/net/): Test before you commit
- [Temporary License](https://purchase.groupdocs.com/temporary-license/): 30-day evaluation license
- [Support Forum](https://forum.groupdocs.com/c/signature/): Community help and official support
