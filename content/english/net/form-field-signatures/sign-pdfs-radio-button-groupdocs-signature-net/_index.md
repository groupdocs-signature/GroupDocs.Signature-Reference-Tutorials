---
title: "PDF Radio Button Signature .NET - Complete Implementation"
linktitle: "PDF Radio Button Signatures .NET"
description: "Master PDF radio button signatures in .NET with GroupDocs.Signature. Step-by-step tutorial with code examples, troubleshooting, and performance tips."
keywords: "PDF radio button signature .NET, GroupDocs.Signature radio buttons, interactive PDF form fields .NET, digital signature form controls, PDF signing C#"
weight: 1
url: "/net/form-field-signatures/sign-pdfs-radio-button-groupdocs-signature-net/"
date: "2025-01-02"
lastmod: "2025-01-02"
categories: ["Digital Signatures"]
tags: ["pdf-signing", "radio-buttons", "form-fields", "groupdocs", "dotnet"]
---

# PDF Radio Button Signature .NET - Complete Implementation

## Introduction

Ever struggled with creating interactive PDF signatures that actually engage users? You're not alone. Traditional digital signatures can feel clunky and impersonal, but **PDF radio button signatures in .NET** change the game entirely.

Here's the thing: radio button form fields don't just collect signatures—they create an interactive experience that guides users through decision-making processes while maintaining legal compliance. Whether you're building survey systems, contract approval workflows, or feedback collection tools, this approach transforms static PDFs into dynamic, user-friendly documents.

In this guide, you'll discover how to implement robust PDF radio button signatures using GroupDocs.Signature for .NET. We'll cover everything from basic setup to advanced optimization techniques that'll make your signatures both functional and performant.

**What you'll master today:**
- Complete GroupDocs.Signature setup and configuration
- Step-by-step radio button signature implementation
- Common pitfalls (and how to avoid them)
- Performance optimization strategies
- Real-world application scenarios
- Troubleshooting techniques that actually work

Let's dive into building something your users will actually want to interact with.

## Why Radio Button Signatures Matter

Before jumping into code, let's understand why PDF radio button signatures are becoming essential for modern .NET applications:

**User Experience Benefits:**
- Eliminates guesswork—users select from predefined options
- Reduces form abandonment rates significantly
- Works seamlessly across devices and PDF viewers
- Provides immediate visual feedback

**Technical Advantages:**
- Structured data collection (no parsing messy text inputs)
- Built-in validation through option constraints
- Consistent formatting across all signed documents
- Easier integration with backend systems

**Business Impact:**
- Faster document processing workflows
- Reduced manual review requirements
- Better compliance tracking and reporting
- Enhanced professional appearance

## Prerequisites and Environment Setup

### What You'll Need

Before we start building, make sure you have these components ready:

**Development Environment:**
- Visual Studio 2019+ (or VS Code with C# extension)
- .NET Core 3.1+ or .NET Framework 4.6.1+
- Basic familiarity with C# and PDF handling

**Required Libraries:**
- GroupDocs.Signature for .NET (we'll install this next)
- System.IO for file operations
- Standard .NET libraries

### Installing GroupDocs.Signature for .NET

The installation process is straightforward, but there are a few ways to do it depending on your preferred workflow:

**Method 1: .NET CLI (Recommended)**
```bash
dotnet add package GroupDocs.Signature
```

**Method 2: Package Manager Console**
```powershell
Install-Package GroupDocs.Signature
```

**Method 3: Visual Studio Package Manager UI**
1. Right-click your project → "Manage NuGet Packages"
2. Search for "GroupDocs.Signature"
3. Install the latest stable version

**Pro Tip:** Always check the [releases page](https://releases.groupdocs.com/signature/net/) for the most current version and changelog.

### License Configuration

GroupDocs.Signature offers flexible licensing options:

**For Development/Testing:**
```csharp
// Free evaluation (includes watermarks)
var signature = new Signature("sample.pdf");
```

**For Production:**
```csharp
// Apply license to remove limitations
License license = new License();
license.SetLicense("path/to/GroupDocs.Signature.lic");
var signature = new Signature("sample.pdf");
```

**Temporary License Option:**
If you need full features for testing, grab a [temporary license](https://purchase.groupdocs.com/temporary-license/) that's valid for 30 days.

## Core Implementation: Building Radio Button Signatures

Now for the main event—let's build a robust PDF radio button signature system step by step.

### Step 1: Setting Up the Foundation

First, let's create the basic structure that'll handle our PDF signing operations:

```csharp
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
using System;
using System.Collections.Generic;
using System.IO;

public class PdfRadioButtonSigner
{
    private readonly string _inputPath;
    private readonly string _outputPath;
    
    public PdfRadioButtonSigner(string inputPath, string outputPath)
    {
        _inputPath = inputPath ?? throw new ArgumentNullException(nameof(inputPath));
        _outputPath = outputPath ?? throw new ArgumentNullException(nameof(outputPath));
    }
}
```

### Step 2: Creating Radio Button Form Fields

Here's where the magic happens. We'll create a method that sets up radio button options and configures their behavior:

```csharp
public SignResult CreateRadioButtonSignature(string fieldName, 
    List<string> options, 
    string defaultSelection = null,
    int top = 200, 
    int left = 50, 
    int width = 200, 
    int height = 90)
{
    using (Signature signature = new Signature(_inputPath))
    {
        // Define the radio button options
        List<string> radioOptions = options ?? throw new ArgumentNullException(nameof(options));
        
        // Create the radio button form field signature
        RadioButtonFormFieldSignature radioSignature = 
            new RadioButtonFormFieldSignature(fieldName, radioOptions, defaultSelection ?? options[0]);
        
        // Configure the form field options
        FormFieldSignOptions signOptions = new FormFieldSignOptions(radioSignature)
        {
            Top = top,
            Left = left,
            Height = height,
            Width = width,
            // Optional: Set page number (default is 1)
            AllPages = false,
            PageNumber = 1
        };
        
        // Execute the signing process
        SignResult result = signature.Sign(_outputPath, signOptions);
        
        return result;
    }
}
```

### Step 3: Practical Implementation Example

Let's see this in action with a real-world scenario—creating a contract approval form:

```csharp
public void CreateContractApprovalForm()
{
    try
    {
        var signer = new PdfRadioButtonSigner(
            "contract-template.pdf", 
            "signed-contract.pdf"
        );
        
        // Create approval status radio buttons
        var approvalOptions = new List<string> 
        { 
            "Approved", 
            "Rejected", 
            "Needs Revision" 
        };
        
        SignResult result = signer.CreateRadioButtonSignature(
            fieldName: "approvalStatus",
            options: approvalOptions,
            defaultSelection: "Needs Revision",
            top: 300,
            left: 100,
            width: 250,
            height: 100
        );
        
        Console.WriteLine($"✅ Contract signed successfully!");
        Console.WriteLine($"📁 Signed document saved to: signed-contract.pdf");
        Console.WriteLine($"📊 {result.Succeeded.Count} signature(s) added");
        
        // Optionally, display signature details
        foreach (var signature in result.Succeeded)
        {
            Console.WriteLine($"📝 Signature ID: {signature.SignatureId}");
        }
    }
    catch (Exception ex)
    {
        Console.WriteLine($"❌ Error creating signature: {ex.Message}");
        // Log the full exception for debugging
        Console.WriteLine($"🔍 Full error: {ex}");
    }
}
```

## Advanced Configuration Options

### Multi-Field Forms

Real applications often need multiple radio button groups. Here's how to handle that efficiently:

```csharp
public SignResult CreateMultiFieldForm()
{
    using (Signature signature = new Signature(_inputPath))
    {
        var signOptions = new List<FormFieldSignOptions>();
        
        // Priority level selection
        var prioritySignature = new RadioButtonFormFieldSignature(
            "priority", 
            new List<string> { "Low", "Medium", "High", "Critical" }, 
            "Medium"
        );
        signOptions.Add(new FormFieldSignOptions(prioritySignature)
        {
            Top = 200, Left = 50, Width = 180, Height = 80
        });
        
        // Department selection
        var departmentSignature = new RadioButtonFormFieldSignature(
            "department", 
            new List<string> { "Sales", "Marketing", "Engineering", "HR" }, 
            "Engineering"
        );
        signOptions.Add(new FormFieldSignOptions(departmentSignature)
        {
            Top = 300, Left = 50, Width = 180, Height = 80
        });
        
        // Sign with multiple form fields
        SignResult result = signature.Sign(_outputPath, signOptions);
        return result;
    }
}
```

### Custom Positioning and Styling

Fine-tune the appearance and placement of your radio buttons:

```csharp
public FormFieldSignOptions CreateStyledRadioButton(
    string fieldName, 
    List<string> options, 
    string defaultValue,
    bool rightToLeft = false,
    int fontSize = 12)
{
    var radioSignature = new RadioButtonFormFieldSignature(fieldName, options, defaultValue);
    
    return new FormFieldSignOptions(radioSignature)
    {
        Top = 250,
        Left = 75,
        Width = 300,
        Height = 120,
        HorizontalAlignment = HorizontalAlignment.Left,
        VerticalAlignment = VerticalAlignment.Top,
        // Note: Advanced styling options may vary by PDF viewer
        AllPages = false,
        PageNumber = 1
    };
}
```

## Common Pitfalls and Solutions

After working with hundreds of PDF signing implementations, here are the most frequent issues and their solutions:

### Issue 1: FileNotFoundException During Signing

**Problem:** Your code throws a `FileNotFoundException` even though the file exists.

**Solution:**
```csharp
public bool ValidateFilePath(string filePath)
{
    if (!File.Exists(filePath))
    {
        Console.WriteLine($"❌ File not found: {filePath}");
        Console.WriteLine($"🔍 Working directory: {Directory.GetCurrentDirectory()}");
        return false;
    }
    
    // Check if file is locked
    try
    {
        using (var stream = File.OpenRead(filePath))
        {
            return true;
        }
    }
    catch (IOException)
    {
        Console.WriteLine($"🔒 File is locked or in use: {filePath}");
        return false;
    }
}
```

### Issue 2: Radio Buttons Not Appearing in PDF

**Problem:** The signing process completes successfully, but radio buttons aren't visible.

**Root Causes & Solutions:**
1. **Positioning outside page boundaries**
   ```csharp
   // Always validate coordinates
   public bool ValidatePosition(int top, int left, int width, int height)
   {
       // Standard PDF page is ~595x842 points (A4)
       return top >= 0 && left >= 0 && 
              (top + height) <= 842 && 
              (left + width) <= 595;
   }
   ```

2. **PDF viewer compatibility issues**
   ```csharp
   // Test with multiple viewers: Adobe Reader, Chrome, Edge
   Console.WriteLine("💡 Test your signed PDFs in multiple viewers:");
   Console.WriteLine("   - Adobe Acrobat Reader");
   Console.WriteLine("   - Google Chrome PDF viewer");
   Console.WriteLine("   - Microsoft Edge PDF viewer");
   ```

### Issue 3: Memory Leaks in Production

**Problem:** Memory usage grows continuously when processing multiple PDFs.

**Solution:**
```csharp
public async Task<SignResult> ProcessMultiplePdfsAsync(List<string> pdfPaths)
{
    SignResult lastResult = null;
    
    foreach (string path in pdfPaths)
    {
        using (var signature = new Signature(path))
        {
            // Process each PDF
            var options = CreateRadioButtonOptions();
            lastResult = signature.Sign($"{path}_signed.pdf", options);
        }
        
        // Force garbage collection for large batches
        if (pdfPaths.Count > 50)
        {
            GC.Collect();
            GC.WaitForPendingFinalizers();
        }
    }
    
    return lastResult;
}
```

## Performance Optimization Strategies

### Batch Processing Optimization

When handling multiple documents, efficiency matters:

```csharp
public class OptimizedPdfSigner
{
    private readonly SemaphoreSlim _semaphore;
    
    public OptimizedPdfSigner(int maxConcurrency = 3)
    {
        _semaphore = new SemaphoreSlim(maxConcurrency, maxConcurrency);
    }
    
    public async Task<List<SignResult>> ProcessBatchAsync(List<PdfSigningTask> tasks)
    {
        var results = new List<SignResult>();
        var concurrentTasks = tasks.Select(async task =>
        {
            await _semaphore.WaitAsync();
            try
            {
                return await ProcessSingleDocumentAsync(task);
            }
            finally
            {
                _semaphore.Release();
            }
        });
        
        var completedResults = await Task.WhenAll(concurrentTasks);
        return completedResults.ToList();
    }
}
```

### Memory Management Best Practices

```csharp
public void OptimizedSigning()
{
    // Use specific disposal patterns
    using var signature = new Signature(_inputPath);
    
    // Minimize object creation in loops
    var reusableOptions = new FormFieldSignOptions();
    
    // Clear references when done
    signature?.Dispose();
    GC.Collect();
}
```

## Real-World Implementation Scenarios

### Scenario 1: Employee Feedback System

Perfect for HR departments collecting structured feedback:

```csharp
public class EmployeeFeedbackSigner
{
    public SignResult CreateFeedbackForm(string employeeName, string reviewPeriod)
    {
        using (var signature = new Signature("feedback-template.pdf"))
        {
            var satisfactionOptions = new List<string> 
            { 
                "Very Satisfied", 
                "Satisfied", 
                "Neutral", 
                "Dissatisfied", 
                "Very Dissatisfied" 
            };
            
            var radioSignature = new RadioButtonFormFieldSignature(
                "jobSatisfaction", 
                satisfactionOptions, 
                "Neutral"
            );
            
            var options = new FormFieldSignOptions(radioSignature)
            {
                Top = 350,
                Left = 100,
                Width = 300,
                Height = 150
            };
            
            return signature.Sign($"feedback_{employeeName}_{reviewPeriod}.pdf", options);
        }
    }
}
```

### Scenario 2: Survey Response Collection

Ideal for market research and customer feedback:

```csharp
public class SurveyResponseSigner
{
    public SignResult CreateProductRatingForm(string productName)
    {
        using (var signature = new Signature("survey-template.pdf"))
        {
            var ratingOptions = new List<string> 
            { 
                "⭐ 1 Star", 
                "⭐⭐ 2 Stars", 
                "⭐⭐⭐ 3 Stars", 
                "⭐⭐⭐⭐ 4 Stars", 
                "⭐⭐⭐⭐⭐ 5 Stars" 
            };
            
            var ratingSignature = new RadioButtonFormFieldSignature(
                $"rating_{productName.Replace(" ", "_")}", 
                ratingOptions, 
                "⭐⭐⭐ 3 Stars"
            );
            
            var options = new FormFieldSignOptions(ratingSignature)
            {
                Top = 400,
                Left = 80,
                Width = 350,
                Height = 180
            };
            
            return signature.Sign($"survey_{productName}_rating.pdf", options);
        }
    }
}
```

### Scenario 3: Contract Approval Workflows

Essential for legal and procurement departments:

```csharp
public class ContractApprovalSigner
{
    public SignResult CreateApprovalWorkflow(string contractId, string approverRole)
    {
        using (var signature = new Signature($"contract_{contractId}.pdf"))
        {
            var approvalOptions = GetApprovalOptionsForRole(approverRole);
            
            var approvalSignature = new RadioButtonFormFieldSignature(
                $"approval_{approverRole}_{contractId}", 
                approvalOptions, 
                "Pending Review"
            );
            
            var options = new FormFieldSignOptions(approvalSignature)
            {
                Top = 500,
                Left = 120,
                Width = 280,
                Height = 140
            };
            
            return signature.Sign($"contract_{contractId}_approval.pdf", options);
        }
    }
    
    private List<string> GetApprovalOptionsForRole(string role)
    {
        return role.ToLower() switch
        {
            "legal" => new List<string> { "Approved", "Legal Review Required", "Rejected" },
            "finance" => new List<string> { "Budget Approved", "Budget Denied", "Needs Adjustment" },
            "manager" => new List<string> { "Approved", "Rejected", "Escalate to Director" },
            _ => new List<string> { "Approved", "Rejected", "Needs Review" }
        };
    }
}
```

## Testing and Validation

### Unit Testing Your Implementation

```csharp
[TestClass]
public class RadioButtonSignatureTests
{
    [TestMethod]
    public void CreateRadioButtonSignature_ValidInputs_ReturnsSuccess()
    {
        // Arrange
        var signer = new PdfRadioButtonSigner("test-input.pdf", "test-output.pdf");
        var options = new List<string> { "Option1", "Option2", "Option3" };
        
        // Act
        var result = signer.CreateRadioButtonSignature("testField", options);
        
        // Assert
        Assert.IsTrue(result.Succeeded.Count > 0);
        Assert.IsTrue(File.Exists("test-output.pdf"));
    }
    
    [TestMethod]
    public void CreateRadioButtonSignature_EmptyOptions_ThrowsException()
    {
        // Arrange
        var signer = new PdfRadioButtonSigner("test-input.pdf", "test-output.pdf");
        var emptyOptions = new List<string>();
        
        // Act & Assert
        Assert.ThrowsException<ArgumentNullException>(() => 
            signer.CreateRadioButtonSignature("testField", emptyOptions));
    }
}
```

### Integration Testing

```csharp
public class IntegrationTestSuite
{
    public async Task TestFullWorkflow()
    {
        // Test the complete signing workflow
        var tasks = new List<Task<bool>>
        {
            TestSingleSignature(),
            TestMultipleSignatures(),
            TestBatchProcessing(),
            TestErrorHandling()
        };
        
        var results = await Task.WhenAll(tasks);
        
        Console.WriteLine($"Integration tests completed: {results.Count(r => r)} passed");
    }
}
```

## Troubleshooting Guide

### Diagnostic Tools

When things go wrong, use these debugging techniques:

```csharp
public class DiagnosticHelper
{
    public void DiagnosePdfIssues(string pdfPath)
    {
        Console.WriteLine("🔍 Running PDF diagnostics...");
        
        // Check file accessibility
        Console.WriteLine($"📁 File exists: {File.Exists(pdfPath)}");
        Console.WriteLine($"📏 File size: {new FileInfo(pdfPath).Length / 1024}KB");
        
        // Test basic signature operations
        try
        {
            using var signature = new Signature(pdfPath);
            Console.WriteLine("✅ PDF can be opened for signing");
            
            // Check for existing signatures
            var existingSignatures = signature.Search<FormFieldSignature>(SignatureType.FormField);
            Console.WriteLine($"📝 Existing form fields: {existingSignatures.Count}");
        }
        catch (Exception ex)
        {
            Console.WriteLine($"❌ PDF access error: {ex.Message}");
        }
    }
}
```

### Common Error Messages and Solutions

**"Unable to find the signature options"**
- Verify that FormFieldSignOptions is properly initialized
- Check that the RadioButtonFormFieldSignature has valid options

**"Signature position is outside document boundaries"**
- Use ValidatePosition() method shown earlier
- Remember: PDF coordinates start from bottom-left corner

**"Document is password protected"**
- Remove password protection before signing
- Or use LoadOptions with password parameter

## Advanced Features and Extensions

### Custom Validation Logic

```csharp
public class ValidatedRadioButtonSigner : PdfRadioButtonSigner
{
    private readonly List<Func<string, List<string>, bool>> _validators;
    
    public ValidatedRadioButtonSigner(string inputPath, string outputPath) 
        : base(inputPath, outputPath)
    {
        _validators = new List<Func<string, List<string>, bool>>
        {
            ValidateFieldName,
            ValidateOptionCount,
            ValidateOptionLength
        };
    }
    
    private bool ValidateFieldName(string fieldName, List<string> options)
    {
        return !string.IsNullOrWhiteSpace(fieldName) && fieldName.Length <= 50;
    }
    
    private bool ValidateOptionCount(string fieldName, List<string> options)
    {
        return options.Count >= 2 && options.Count <= 10;
    }
    
    private bool ValidateOptionLength(string fieldName, List<string> options)
    {
        return options.All(option => option.Length <= 100);
    }
}
```

### Event Handling and Callbacks

```csharp
public class EventAwareRadioButtonSigner : PdfRadioButtonSigner
{
    public event EventHandler<SignatureCompletedEventArgs> SignatureCompleted;
    public event EventHandler<SignatureErrorEventArgs> SignatureError;
    
    public SignResult CreateSignatureWithEvents(string fieldName, List<string> options)
    {
        try
        {
            var result = CreateRadioButtonSignature(fieldName, options);
            
            SignatureCompleted?.Invoke(this, new SignatureCompletedEventArgs 
            { 
                FieldName = fieldName, 
                Result = result 
            });
            
            return result;
        }
        catch (Exception ex)
        {
            SignatureError?.Invoke(this, new SignatureErrorEventArgs 
            { 
                FieldName = fieldName, 
                Exception = ex 
            });
            throw;
        }
    }
}
```

## Conclusion and Next Steps

You've now mastered the art of implementing PDF radio button signatures in .NET using GroupDocs.Signature. Let's recap what you've accomplished:

**✅ What You've Learned:**
- Complete GroupDocs.Signature setup and configuration
- Robust radio button signature implementation
- Advanced troubleshooting and optimization techniques
- Real-world application scenarios and best practices
- Performance optimization strategies for production use

**🚀 Immediate Action Items:**
1. **Test the basic implementation** with your own PDF documents
2. **Experiment with different positioning** and styling options
3. **Implement error handling** for your specific use cases
4. **Set up unit tests** to ensure reliability

**📈 Advanced Next Steps:**
- Explore other form field types (checkboxes, text fields)
- Integrate with your existing authentication systems
- Build a complete document workflow management system
- Implement digital certificate-based signatures for enhanced security

**🛠️ Production Considerations:**
- Monitor memory usage in high-volume scenarios
- Implement proper logging and error tracking
- Set up automated testing pipelines
- Consider caching strategies for frequently used templates

The power of interactive PDF signatures is now in your hands. Whether you're building internal approval workflows, customer feedback systems, or complex document processing pipelines, you have the tools and knowledge to create professional, user-friendly solutions.

Ready to take it to the next level? Start with a simple proof-of-concept using your most common PDF scenario, then gradually expand with the advanced features we've covered.

## Frequently Asked Questions

**Q: Can I customize the appearance of radio buttons beyond positioning?**

A: GroupDocs.Signature focuses on functionality over visual customization. You can control position, size, and basic layout, but advanced styling (colors, fonts, etc.) depends on the PDF viewer. For maximum compatibility, stick with standard appearances.

**Q: How many radio button options can I include in a single field?**

A: While there's no hard technical limit, practical considerations suggest keeping it under 10 options for usability. Too many options can make the form cluttered and difficult to use, especially on mobile devices.

**Q: Are radio button signatures legally binding?**

A: Yes, when properly implemented with audit trails and authentication, radio button signatures can be legally binding in most jurisdictions. However, consult with legal experts for your specific use case and location, as requirements vary by industry and region.

**Q: Can users change their radio button selection after signing?**

A: This depends on your PDF configuration. By default, form fields remain editable after signing unless you specifically lock the document. Use additional security features if you need to prevent modifications.

**Q: How do I extract the selected values from signed PDFs?**

A: Use GroupDocs.Signature's search functionality:
```csharp
using (var signature = new Signature("signed-document.pdf"))
{
    var formFields = signature.Search<FormFieldSignature>(SignatureType.FormField);
    foreach (var field in formFields)
    {
        if (field is RadioButtonFormFieldSignature radioField)
        {
            Console.WriteLine($"Field: {radioField.Name}, Selected: {radioField.Selected}");
        }
    }
}
```

**Q: Can I use this approach with other document formats besides PDF?**

A: GroupDocs.Signature supports multiple formats, but radio button form fields work best with PDF documents. For other formats (Word, Excel), consider alternative signature approaches like text-based or image-based signatures.

**Q: What happens if the PDF already contains form fields?**

A: GroupDocs.Signature can work alongside existing form fields. Each field needs a unique name to avoid conflicts. If you're adding to existing forms, scan for current field names first to ensure uniqueness.

**Q: How do I handle multi-language radio button options?**

A: Simply include the translated text in your options list:
```csharp
var multiLanguageOptions = new List<string> 
{ 
    "Yes / Sí / Oui", 
    "No / No / Non", 
    "Maybe / Quizás / Peut-être" 
};
```

**Q: Is there a limit to how many signatures I can add to a single PDF?**

A: There's no strict limit, but performance and usability decrease with too many form fields. For complex forms, consider splitting across multiple pages or using a dedicated form-building solution.

**Q: Can I integrate this with cloud storage services like Azure or AWS?**

A: Absolutely! GroupDocs.Signature works with streams, so you can easily integrate with cloud storage:
```csharp
// Example with Azure Blob Storage
var blobStream = await blobClient.OpenReadAsync();
using var signature = new Signature(blobStream);
// ... perform signing operations
```

## Resources and Further Learning

**📚 Essential Documentation:**
- [GroupDocs.Signature .NET Documentation](https://docs.groupdocs.com/signature/net/) - Comprehensive API reference
- [API Reference Guide](https://reference.groupdocs.com/signature/net/) - Detailed method documentation

**🔗 Links:**
- [Download GroupDocs.Signature](https://releases.groupdocs.com/signature/net/) - Get the latest version
- [Free Trial Access](https://releases.groupdocs.com/signature/net/) - Test without limitations
- [Temporary License](https://purchase.groupdocs.com/temporary-license/) - 30-day full access
- [Purchase Options](https://purchase.groupdocs.com/buy) - Commercial licensing
- [Support Forum](https://forum.groupdocs.com/c/signature/) - Community help and discussions
