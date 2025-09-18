---
title: "How to Cancel Document Verification in .NET - GroupDocs.Signature"
linktitle: "Cancel Document Verification .NET"
description: "Learn how to cancel document verification in .NET using GroupDocs.Signature progress events. Stop long-running processes with practical examples and troubleshooting tips."
keywords: "cancel document verification .NET, GroupDocs Signature progress events, document verification cancellation C#, .NET signature library timeout, how to cancel long running document verification"
weight: 1
url: "/net/event-handling/cancel-document-verification-groupdocs-signature-net/"
date: "2025-01-02"
lastmod: "2025-01-02"
categories: ["GroupDocs.Signature"]
tags: ["document-verification", "progress-events", "cancellation", "dotnet", "csharp"]
---

# How to Cancel Document Verification in .NET - GroupDocs.Signature

## Introduction

Ever had a document verification process that just won't finish? You're not alone. Long-running document verification can freeze your application, frustrate users, and waste valuable system resources. That's where GroupDocs.Signature for .NET's progress event handling comes to the rescue.

In this comprehensive guide, you'll discover how to implement smart cancellation mechanisms that automatically stop document verification when it takes too long. We'll walk through practical examples, common pitfalls, and real-world scenarios where this feature becomes essential.

By the end of this tutorial, you'll have a robust system that keeps your applications responsive while handling document verification efficiently.

## When to Use This Feature

Understanding when document verification cancellation is most valuable can help you decide if this approach fits your needs:

**Perfect for These Scenarios:**
- **Large Document Processing**: When dealing with PDFs or documents over 10MB that might take several seconds to verify
- **Batch Operations**: Processing multiple documents where one slow file shouldn't hold up the entire queue  
- **User-Facing Applications**: Web apps or desktop software where users expect quick responses
- **Resource-Constrained Environments**: Servers with limited CPU or memory that need careful resource management
- **Automated Workflows**: Background processes that need to complete within specific time windows

**Less Useful When:**
- Processing small, simple documents (usually under 1MB)
- Working in environments where processing time isn't a concern
- Handling single documents in offline scenarios

## Prerequisites and Setup

### What You'll Need

Before diving into the implementation, make sure you have:
- **.NET Framework 4.6.1 or .NET Core 2.0+** (newer versions work great too)
- **Visual Studio or VS Code** for development
- **Basic C# knowledge** (we'll explain the tricky parts)
- **GroupDocs.Signature for .NET library** (we'll install this next)

### Installing GroupDocs.Signature for .NET

Getting started is straightforward. Choose your preferred installation method:

**Option 1: .NET CLI (Recommended)**
```bash
dotnet add package GroupDocs.Signature
```

**Option 2: Package Manager Console**
```powershell
Install-Package GroupDocs.Signature
```

**Option 3: NuGet Package Manager**
1. Right-click your project → "Manage NuGet Packages"
2. Search for "GroupDocs.Signature"
3. Click "Install" on the official GroupDocs package

### License Setup (Important!)

You'll need a license to unlock full functionality:
- **Free Trial**: Perfect for testing - gives you full features for evaluation
- **Temporary License**: Extends evaluation period if you need more time
- **Production License**: Required for commercial applications

## Core Implementation: Progress Event Handling

Now let's get into the practical implementation. We'll build this step-by-step so you understand every piece.

### Step 1: Setting Up the Event Handler

The heart of our cancellation system is the progress event handler. This method gets called during verification and decides whether to continue or stop:

```csharp
private static void OnVerifyProgress(Signature sender, ProcessProgressEventArgs args)
{
    // Check if the processing time exceeds 350 ticks.
    if (args.Ticks > 350) 
    {
        args.Cancel = true; // Cancel the process.
        Console.WriteLine("Sign progress was canceled. Time spent {0} mlsec", args.Ticks);
    }
}
```

**What's happening here?**
- The method receives progress updates through `ProcessProgressEventArgs`
- We check if processing time exceeds 350 milliseconds (you can adjust this)
- If it takes too long, we set `args.Cancel = true` to stop the process
- A console message lets us know what happened (useful for debugging)

### Step 2: Connecting Everything Together

Here's how you wire up the event handler with your document verification:

```csharp
using (Signature signature = new Signature(filePath))
{
    // Attach an event handler for progress events.
    signature.VerifyProgress += OnVerifyProgress;

    // Configure what we want to verify
    TextVerifyOptions options = new TextVerifyOptions("Text signature")
    {
        // Additional configurations can be specified here.
    };

    // Execute the verification process.
    VerificationResult result = signature.Verify(options);

    if (result.IsValid)
    {
        Console.WriteLine("Document verification was not canceled!");
    }
    else
    {
        Console.WriteLine("Document verification was canceled successfully!");
    }
}
```

**Key Points:**
- Always use `using` statements to properly dispose of resources
- Attach the event handler before calling `Verify()`
- The `VerificationResult` tells you if the process completed or was canceled

## Advanced Tips and Best Practices

### Choosing the Right Timeout Value

The 350-tick timeout in our example might not fit every situation. Here's how to choose wisely:

**For Different Document Types:**
- **Simple text documents**: 100-200 ticks (0.1-0.2 seconds)
- **Complex PDFs with images**: 500-1000 ticks (0.5-1.0 seconds)  
- **Large corporate documents**: 2000-5000 ticks (2-5 seconds)
- **Batch processing**: Consider per-document limits based on average size

**Dynamic Timeout Calculation:**
```csharp
private static void OnVerifyProgressDynamic(Signature sender, ProcessProgressEventArgs args)
{
    // Calculate timeout based on document size or complexity
    int dynamicTimeout = CalculateTimeoutForDocument(args);
    
    if (args.Ticks > dynamicTimeout) 
    {
        args.Cancel = true;
        Console.WriteLine($"Process canceled after {args.Ticks}ms (limit: {dynamicTimeout}ms)");
    }
}
```

### Memory Management Best Practices

When processing multiple documents, memory management becomes crucial:

```csharp
// Good: Dispose properly in batch scenarios
foreach (string filePath in documentPaths)
{
    using (Signature signature = new Signature(filePath))
    {
        signature.VerifyProgress += OnVerifyProgress;
        var result = signature.Verify(options);
        // Signature is automatically disposed here
    }
    
    // Optional: Force garbage collection for large batches
    if (processedCount % 100 == 0)
    {
        GC.Collect();
    }
}
```

### Error Handling Integration

Combine cancellation with proper error handling:

```csharp
try
{
    using (Signature signature = new Signature(filePath))
    {
        signature.VerifyProgress += OnVerifyProgress;
        VerificationResult result = signature.Verify(options);
        
        if (result.IsValid)
        {
            // Handle successful verification
            ProcessValidDocument(filePath, result);
        }
        else
        {
            // Could be canceled or genuinely invalid
            HandleCanceledOrInvalid(filePath, result);
        }
    }
}
catch (GroupDocsSignatureException ex)
{
    // Handle GroupDocs-specific errors
    LogError($"Verification failed for {filePath}: {ex.Message}");
}
catch (Exception ex)
{
    // Handle unexpected errors
    LogError($"Unexpected error processing {filePath}: {ex.Message}");
}
```

## Common Issues and Solutions

### Issue 1: Event Handler Not Firing

**Problem:** Your progress event handler never gets called, so cancellation doesn't work.

**Solution:** 
- Ensure you attach the event handler BEFORE calling `Verify()`
- Check that your document actually requires processing time (very small documents might complete instantly)
- Verify the file path is correct and the file exists

```csharp
// Wrong order - handler attached too late
var result = signature.Verify(options);
signature.VerifyProgress += OnVerifyProgress; // Too late!

// Correct order
signature.VerifyProgress += OnVerifyProgress;
var result = signature.Verify(options); // Now it works
```

### Issue 2: Cancellation Happening Too Quickly

**Problem:** Documents get canceled immediately, even small ones that should process quickly.

**Solution:**
- Increase your timeout threshold
- Add minimum processing time before cancellation is allowed
- Consider document size in your cancellation logic

```csharp
private static void OnVerifyProgressImproved(Signature sender, ProcessProgressEventArgs args)
{
    // Don't cancel in the first 50ms to avoid premature cancellation
    if (args.Ticks < 50) return;
    
    // Now apply your actual timeout logic
    if (args.Ticks > 350) 
    {
        args.Cancel = true;
        Console.WriteLine($"Process canceled after {args.Ticks}ms");
    }
}
```

### Issue 3: Memory Leaks in Batch Processing

**Problem:** Processing many documents causes memory usage to climb steadily.

**Solution:**
- Always use `using` statements for Signature objects
- Detach event handlers when done (optional but good practice)
- Consider periodic garbage collection in large batches

```csharp
// Clean approach for batch processing
foreach (string filePath in documentPaths)
{
    using (Signature signature = new Signature(filePath))
    {
        // Create a new handler instance to avoid potential issues
        ProcessProgressEventHandler handler = (sender, args) => {
            if (args.Ticks > 350) 
            {
                args.Cancel = true;
            }
        };
        
        signature.VerifyProgress += handler;
        
        try 
        {
            var result = signature.Verify(options);
            ProcessResult(result);
        }
        finally 
        {
            // Optional: explicitly detach handler
            signature.VerifyProgress -= handler;
        }
    } // Signature disposed here automatically
}
```

## Real-World Application Examples

### Example 1: Web API with Timeout Protection

Here's how you might implement this in an ASP.NET Core Web API:

```csharp
[ApiController]
[Route("api/[controller]")]
public class DocumentController : ControllerBase
{
    [HttpPost("verify")]
    public async Task<IActionResult> VerifyDocument(IFormFile file)
    {
        if (file == null || file.Length == 0)
            return BadRequest("No file provided");

        try
        {
            using var stream = file.OpenReadStream();
            using var signature = new Signature(stream);
            
            // Set up cancellation with reasonable timeout for web requests
            signature.VerifyProgress += (sender, args) => {
                if (args.Ticks > 2000) // 2 seconds max for web requests
                {
                    args.Cancel = true;
                }
            };

            var options = new TextVerifyOptions("Required signature text");
            var result = signature.Verify(options);

            return Ok(new { 
                IsValid = result.IsValid,
                Message = result.IsValid ? "Document verified successfully" : "Verification failed or timed out"
            });
        }
        catch (Exception ex)
        {
            return StatusCode(500, $"Error processing document: {ex.Message}");
        }
    }
}
```

### Example 2: Background Service with Configurable Timeouts

For background processing services, you might want configurable timeouts:

```csharp
public class DocumentProcessingService
{
    private readonly IConfiguration _config;
    
    public DocumentProcessingService(IConfiguration config)
    {
        _config = config;
    }
    
    public async Task<bool> ProcessDocumentBatch(IEnumerable<string> filePaths)
    {
        int timeoutMs = _config.GetValue<int>("DocumentProcessing:TimeoutMs", 1000);
        int successCount = 0;
        
        foreach (string filePath in filePaths)
        {
            if (await ProcessSingleDocument(filePath, timeoutMs))
            {
                successCount++;
            }
        }
        
        return successCount > 0;
    }
    
    private async Task<bool> ProcessSingleDocument(string filePath, int timeoutMs)
    {
        return await Task.Run(() => 
        {
            using var signature = new Signature(filePath);
            
            signature.VerifyProgress += (sender, args) => {
                if (args.Ticks > timeoutMs)
                {
                    args.Cancel = true;
                    // Log the cancellation for monitoring
                    Console.WriteLine($"Document {Path.GetFileName(filePath)} processing canceled after {args.Ticks}ms");
                }
            };
            
            var options = new TextVerifyOptions("Company signature");
            var result = signature.Verify(options);
            
            return result.IsValid;
        });
    }
}
```

## Performance Optimization Tips

### Optimize for Your Use Case

Different scenarios benefit from different approaches:

**High-Volume, Low-Latency (Web APIs):**
- Use shorter timeouts (500-1000ms)
- Consider async processing for larger documents
- Implement request queuing to prevent overload

**Batch Processing:**
- Use longer timeouts but still set limits
- Process documents in parallel when possible
- Monitor memory usage and implement cleanup cycles

**Desktop Applications:**
- Provide user feedback during processing
- Allow users to cancel manually
- Use progress bars to show actual progress

### Monitoring and Metrics

Track your cancellation patterns to optimize timeout values:

```csharp
public class DocumentProcessingMetrics
{
    private static readonly Dictionary<string, List<long>> ProcessingTimes = new();
    
    public static void RecordProcessingTime(string documentType, long processingTimeMs, bool wasCanceled)
    {
        if (!ProcessingTimes.ContainsKey(documentType))
            ProcessingTimes[documentType] = new List<long>();
            
        ProcessingTimes[documentType].Add(processingTimeMs);
        
        // Log cancellation events
        if (wasCanceled)
        {
            Console.WriteLine($"CANCELED: {documentType} after {processingTimeMs}ms");
        }
    }
    
    public static double GetAverageProcessingTime(string documentType)
    {
        if (!ProcessingTimes.ContainsKey(documentType) || !ProcessingTimes[documentType].Any())
            return 0;
            
        return ProcessingTimes[documentType].Average();
    }
}
```

## Troubleshooting Guide

### Quick Diagnostic Questions

When things aren't working as expected, ask yourself:

1. **Is the event handler attached before verification starts?**
2. **Are you using the correct timeout value for your document types?**
3. **Is the file path correct and accessible?**
4. **Are you properly disposing of Signature objects?**
5. **Is your cancellation logic too aggressive or too lenient?**

### Debug Mode Implementation

Add detailed logging to understand what's happening:

```csharp
private static void OnVerifyProgressDebug(Signature sender, ProcessProgressEventArgs args)
{
    Console.WriteLine($"Progress update: {args.Ticks}ms elapsed");
    
    if (args.Ticks > 350) 
    {
        Console.WriteLine($"CANCELING: Process exceeded {args.Ticks}ms (limit: 350ms)");
        args.Cancel = true;
    }
    else 
    {
        Console.WriteLine($"Continuing: {args.Ticks}ms elapsed (limit: 350ms)");
    }
}
```

## Conclusion

You now have a complete toolkit for implementing smart document verification cancellation in your .NET applications. This approach helps you maintain responsive applications while efficiently managing system resources.

**Key takeaways:**
- Progress event handling prevents long-running operations from blocking your application
- Proper timeout values depend on your specific use case and document types  
- Always combine cancellation with proper error handling and resource disposal
- Monitor your applications to optimize timeout values based on real-world usage

**Next steps to explore:**
- Implement user-initiated cancellation in desktop applications
- Add progress bars and user feedback mechanisms
- Explore other GroupDocs.Signature features like digital signing and signature search
- Consider integrating with background job processing libraries for enterprise scenarios

The techniques you've learned here apply beyond just document verification - you can use similar patterns anywhere you need to control long-running operations in .NET applications.

## Frequently Asked Questions

**Q: What happens to partially processed data when verification is canceled?**
A: When you cancel verification through the progress event, GroupDocs.Signature stops processing immediately and returns a result indicating the operation was not completed. No partial results are saved or returned.

**Q: Can I cancel verification based on criteria other than time?**
A: Absolutely! The `ProcessProgressEventArgs` provides information you can use for different cancellation criteria. You could cancel based on memory usage, user input, or any other condition your application monitors.

**Q: Is there a performance impact from using progress events?**
A: The performance impact is minimal. Progress events fire periodically during processing, but the overhead is negligible compared to the actual document verification work.

**Q: How do I handle cancellation in async/await scenarios?**
A: The event handler approach works the same way in async contexts. The verification process itself is synchronous, but you can wrap it in `Task.Run()` if you need true async behavior.

**Q: Can I adjust timeout values dynamically based on document size?**
A: Yes! You can examine document properties or file size before verification and set different timeout thresholds accordingly. This gives you more flexible control over the cancellation logic.

**Q: What's the difference between canceling through events vs using CancellationToken?**
A: GroupDocs.Signature uses its own progress event system rather than the standard .NET CancellationToken pattern. The progress events are specifically designed for document processing scenarios and provide processing time information.