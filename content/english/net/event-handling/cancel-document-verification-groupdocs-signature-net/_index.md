---
title: "How to Cancel Document Verification Using GroupDocs.Signature for .NET&#58; Event Handling Guide"
description: "Learn how to efficiently manage document verification processes with progress event handling and cancellation in GroupDocs.Signature for .NET. Improve application performance today."
date: "2025-05-07"
weight: 1
url: "/net/event-handling/cancel-document-verification-groupdocs-signature-net/"
keywords:
- cancel document verification GroupDocs
- progress event handling .NET
- GroupDocs Signature cancellation

---


# How to Cancel Document Verification Using GroupDocs.Signature for .NET: Event Handling Guide

## Introduction

Are you looking for efficient ways to manage long-running document verification tasks? With GroupDocs.Signature for .NET, you can handle progress events to monitor and control these processes effectively. This guide will show you how to implement a system that cancels operations based on specific conditions like processing time exceeding a threshold.

In this article, we'll explore:
- Setting up and installing GroupDocs.Signature for .NET
- Implementing progress event handling in your application
- Canceling a process based on specific conditions
- Real-world applications of these features

## Prerequisites

### Required Libraries and Dependencies

To follow along with this guide, ensure you have:
- **GroupDocs.Signature for .NET**: The core library for document signatures.
- **.NET Framework or .NET Core**: Version 4.6.1 or later is recommended.

### Environment Setup Requirements

Ensure your development environment is set up with Visual Studio or a compatible IDE that supports .NET projects.

### Knowledge Prerequisites

Familiarity with C# and basic knowledge of event handling in .NET will be beneficial, but not mandatory, as we'll cover the essentials here.

## Setting Up GroupDocs.Signature for .NET

To get started, install the GroupDocs.Signature library using one of these methods:

**.NET CLI**
```bash
dotnet add package GroupDocs.Signature
```

**Package Manager**
```powershell
Install-Package GroupDocs.Signature
```

**NuGet Package Manager UI**
Search for "GroupDocs.Signature" and install the latest version.

### License Acquisition

You can obtain a free trial license to test the full capabilities of GroupDocs.Signature. For production use, you might consider purchasing a license:
- **Free Trial**: Ideal for testing and initial development.
- **Temporary License**: Useful if you need more time beyond the trial period for evaluation.
- **Purchase**: Obtain a full license for long-term commercial projects.

### Basic Initialization

Once installed, initialize GroupDocs.Signature in your project to start working with document signatures:
```csharp
using GroupDocs.Signature;
```
This setup allows you to create instances of `Signature` and begin exploring its features.

## Implementation Guide

We'll break down the implementation into manageable sections focusing on different functionalities.

### Feature 1: Progress Event Handling

The ability to handle progress events lets you monitor ongoing processes. Here's how you can implement this feature:

#### Overview
This feature allows your application to react to changes in process progress, providing a mechanism to cancel operations if needed.

#### Step-by-Step Implementation

**3.1 Setting Up the Event Handler**
First, define an event handler method that checks whether the processing time exceeds 100 milliseconds (0.1 second).
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

**3.2 Attaching the Event Handler**
Next, attach this event handler to your `Signature` instance within your verification method.
```csharp
using (Signature signature = new Signature(filePath))
{
    // Attach an event handler for progress events.
    signature.VerifyProgress += OnVerifyProgress;

    ...
}
```

**3.3 Executing the Verification Process**
Finally, execute the document verification process while handling potential cancellation:
```csharp
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
```

### Feature 2: Document Verification with Cancellation
This section focuses on verifying documents while incorporating progress event handling for cancellation.

#### Overview
By setting up verification options and attaching a progress handler, you can cancel the process if it takes too long, ensuring your application remains responsive.

**4.1 Define Verification Options**
Set up the `TextVerifyOptions` to specify what aspects of the document need verification:
```csharp
TextVerifyOptions options = new TextVerifyOptions("Text signature")
{
    // Additional configurations can be specified here.
};
```

## Practical Applications

Understanding how progress event handling and cancellation can benefit your applications is crucial. Here are a few use cases:
1. **Batch Processing**: Manage processing time effectively in scenarios where multiple documents need verification.
2. **User Feedback Systems**: Provide real-time feedback to users when operations take longer than expected, improving user experience.
3. **Resource Management**: Automatically cancel long-running tasks that could otherwise strain system resources.
4. **Integration with Workflow Automation**: Use these features within larger automated workflows to ensure smooth operation without delays.
5. **Testing and Development Environments**: Quickly test how your application handles different processing scenarios.

## Performance Considerations
Optimizing performance when using GroupDocs.Signature is crucial for maintaining efficient operations:
- **Resource Usage**: Be mindful of memory usage, especially when handling large documents.
  
- **Best Practices**:
  - Dispose of `Signature` objects promptly to free resources.
  - Use cancellation events judiciously to prevent unnecessary processing.

## Conclusion
In this tutorial, you've learned how to implement progress event handling and process cancellation in document verification using GroupDocs.Signature for .NET. These techniques can significantly enhance the efficiency and responsiveness of your applications.

As a next step, consider exploring other features offered by GroupDocs.Signature, such as digital signing and signature search capabilities, to further improve your document management solutions.

## FAQ Section

**Q1: What is the purpose of handling progress events in GroupDocs.Signature?**
Progress events help monitor and control long-running verification tasks, allowing you to cancel them if they exceed a certain time threshold.

**Q2: How do I attach an event handler for process progress?**
Attach it using the `VerifyProgress` event on your `Signature` instance.

**Q3: What are common scenarios where cancellation of document processing is useful?**
Useful in batch processing, user feedback systems, and resource management to maintain system efficiency.

**Q4: Can I adjust the time threshold for canceling a process?**
Yes, modify the condition within your event handler method (e.g., `args.Ticks > 350`) to suit your requirements.

**Q5: What should I do if my application needs to handle multiple document types?**
GroupDocs.Signature supports various document formats. Ensure you configure appropriate verification options for each type.

## Resources
- **Documentation**: [GroupDocs.Signature Documentation](https://docs.groupdocs.com/signature/net/)
- **API Reference**: [API Reference](https://reference.groupdocs.com/signature/net/)
- **Download**: [Latest Release](https://releases.groupdocs.com/signature/net/)
- **Purchase License**: [GroupDocs.Signature Licensing](https://purchase.groupdocs.com/signature)
