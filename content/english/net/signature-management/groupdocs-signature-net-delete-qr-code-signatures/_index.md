---
title: "How to Remove Digital Signatures in .NET - Delete QR-Code Signatures by ID"
linktitle: "Delete QR-Code Signatures by ID"
description: "Learn how to programmatically remove QR code signatures from documents using GroupDocs.Signature for .NET. Step-by-step guide with troubleshooting tips."
keywords: "remove digital signatures .NET, delete QR code signatures, signature management .NET library, GroupDocs.Signature, programmatically remove signatures C#, delete specific signature by ID"
date: "2025-01-02"
lastmod: "2025-01-02"
weight: 1
url: "/net/signature-management/groupdocs-signature-net-delete-qr-code-signatures/"
categories: ["Signature Management"]
tags: ["qr-code", "digital-signatures", "dotnet", "document-management", "groupdocs"]
type: docs
---
# How to Remove Digital Signatures in .NET - Delete QR-Code Signatures by ID

## Introduction

Ever had to remove an outdated QR code signature from a contract after a client revision? Or needed to clean up test signatures before sending documents to production? You're not alone—managing digital signatures is one of those tasks that seems simple until you actually need to do it programmatically.

Here's the thing: manually removing signatures from documents is tedious (and error-prone). If you're dealing with hundreds of contracts, invoices, or compliance documents, you need an automated solution. That's where **GroupDocs.Signature for .NET** comes in—it lets you delete specific QR code signatures by their unique ID, giving you surgical precision over your document management.

**What You'll Learn in This Guide:**
- How to remove QR code signatures programmatically using C#
- The complete setup process for GroupDocs.Signature for .NET
- Practical techniques for managing signature lifecycles
- Troubleshooting common errors (file locks, invalid IDs, etc.)
- Best practices for signature management in production environments

By the end, you'll be able to confidently delete signatures from your documents without breaking a sweat. Let's start with what you'll need.

## Prerequisites

Before you can start removing signatures, make sure you've got these basics covered:

**Required Tools & Libraries:**
- **GroupDocs.Signature for .NET** (latest version recommended)
- **.NET Framework 4.6.1+** or **.NET Core 2.0+** / **.NET 5/6/7/8**
- **Visual Studio 2019+** or any C# IDE

**Knowledge Prerequisites:**
- Basic C# programming (you should be comfortable with classes and methods)
- Understanding of file I/O operations in .NET
- Familiarity with using NuGet packages

**Helpful (But Not Required):**
- Experience with digital signature concepts
- Knowledge of document formats (PDF, DOCX, XLSX)

If you're working with sensitive documents, you'll also want to ensure you have proper access permissions set up for the files you're modifying.

## Setting Up GroupDocs.Signature for .NET

Getting started with GroupDocs.Signature is straightforward—here's how to add it to your project.

### Installation Methods

**Option 1: Using .NET CLI**
```bash
dotnet add package GroupDocs.Signature
```

**Option 2: Using Package Manager Console**
```powershell
Install-Package GroupDocs.Signature
```

**Option 3: Via NuGet Package Manager UI**
1. Right-click your project in Visual Studio
2. Select "Manage NuGet Packages"
3. Search for "GroupDocs.Signature"
4. Click "Install" on the latest stable version

### License Acquisition

You've got a few options here depending on your needs:

- **Free Trial:** Download a [free trial](https://releases.groupdocs.com/signature/net/) to test features (perfect for POCs)
- **Temporary License:** Get a [temporary license](https://purchase.groupdocs.com/temporary-license/) for extended evaluation (no trial limitations)
- **Full License:** [Purchase a license](https://purchase.groupdocs.com/buy) for production use with full support

### Basic Initialization

Once you've installed the package, here's how to initialize it in your code:

```csharp
using GroupDocs.Signature;

// Initialize Signature object with your document path
Signature signature = new Signature("YOUR_DOCUMENT_PATH");
```

**Pro Tip:** Always wrap your `Signature` object in a `using` statement to ensure proper disposal of resources (we'll see this in action below).

## Why Delete QR Code Signatures? (Real-World Scenarios)

Before we dive into the code, let's talk about when and why you'd actually need this functionality. Understanding the use cases will help you architect your solution better.

### Common Business Scenarios

**1. Contract Revisions & Amendments**
When a contract gets revised, you often need to remove the old approval signatures before routing it for new signatures. Keeping outdated QR codes in place can create legal confusion about which version is active.

**2. Invoice Processing Workflows**
In accounts payable systems, invoices might go through multiple approval stages. If an invoice gets rejected and needs resubmission, you'll want to clear previous approval signatures to avoid processing confusion.

**3. Compliance & Audit Requirements**
Regulatory compliance often requires removing signatures from documents when they're no longer valid (expired certifications, revoked approvals, etc.). Manual removal doesn't scale for high-volume document processing.

**4. Testing & Development Environments**
During development, you'll add test signatures to documents. Before moving to production, you need to clean these up—programmatically deleting signatures by ID makes this process repeatable and automated.

**5. Document Template Management**
If you maintain document templates with placeholder QR codes, you'll need to remove them before creating actual documents. This ensures clean starting points for your document generation workflows.

### Why Signature IDs Matter

Each signature in GroupDocs.Signature has a unique identifier (SignatureId). This is crucial because:
- It lets you target specific signatures without affecting others
- You can track signature history and audit trails
- It enables precise control in multi-signature documents

Think of it like deleting a specific email from your inbox instead of clearing everything—you want surgical precision, not a sledgehammer.

## Understanding Signature IDs (Before You Delete)

Here's something that trips up a lot of developers: **you need to know the SignatureId before you can delete it**. You can't just say "delete all QR codes" (well, you can, but that's a different method).

### How to Find Signature IDs

Before deletion, you'll typically want to search for signatures in your document:

```csharp
using (Signature signature = new Signature("your-document.pdf"))
{
    // Search for QR code signatures
    QrCodeSearchOptions searchOptions = new QrCodeSearchOptions();
    List<QrCodeSignature> signatures = signature.Search<QrCodeSignature>(searchOptions);
    
    // Display found signatures with their IDs
    foreach (QrCodeSignature qrSignature in signatures)
    {
        Console.WriteLine($"QR Code: {qrSignature.Text}");
        Console.WriteLine($"ID: {qrSignature.SignatureId}");
        Console.WriteLine($"Position: {qrSignature.Left}, {qrSignature.Top}");
        Console.WriteLine("---");
    }
}
```

**When to Use This Approach:**
- You're building a UI where users select signatures to delete
- You need to validate signatures before removal
- You're implementing conditional deletion logic (e.g., only delete expired signatures)

### Storing Signature IDs

If you're managing documents long-term, consider storing SignatureIds in your database alongside document metadata. This makes future operations much faster and enables audit trails.

## Implementation Guide

Alright, let's get to the actual code. This is the step-by-step process for removing QR code signatures by their ID.

### Deleting a QR-Code Signature by ID

This approach gives you precise control—you specify exactly which signatures to remove based on their unique identifiers.

#### Step 1: Prepare Your File Paths

First, set up where your files live. This includes creating output directories if they don't exist (important for production environments where paths might not be pre-created):

```csharp
string filePath = "YOUR_DOCUMENT_DIRECTORY"; // Set your source file path here
string fileName = System.IO.Path.GetFileName(filePath);
string outputFilePath = System.IO.Path.Combine("YOUR_OUTPUT_DIRECTORY", "DeleteQRCodeById", fileName);

// Create the directory if it doesn't exist
if (!System.IO.Directory.Exists(System.IO.Path.GetDirectoryName(outputFilePath)))
{
    System.IO.Directory.CreateDirectory(System.IO.Path.GetDirectoryName(outputFilePath));
}

// Copy source file to output path
System.IO.File.Copy(filePath, outputFilePath, true);
```

**Why Copy the File?**
You're working with a copy instead of the original file. This is a best practice because:
- It preserves your original document as a backup
- It prevents accidental data loss if something goes wrong
- It's easier to implement versioning and audit trails

**Pro Tip:** In production, you might want to add a timestamp to the output filename to track different versions: `$"DeleteQRCodeById/{fileName}_{DateTime.Now:yyyyMMddHHmmss}"`

#### Step 2: Initialize Signature Object

Now create your `Signature` object pointing to the document you want to modify:

```csharp
using (Signature signature = new Signature(outputFilePath))
{
    // Continue with deletion process...
}
```

**Why Use `using`?**
The `using` statement ensures that the document file gets properly closed and disposed of, even if an exception occurs. This prevents file lock issues that can plague document processing applications.

#### Step 3: Specify QR-Code Signatures to Delete

Here's where you specify which signatures to remove. You'll need the SignatureIds you want to delete:

```csharp
string[] signatureIdList = new string[] { "eff64a14-dad9-47b0-88e5-2ee4e3604e71" };
var signatures = signatureIdList.Select(id => new QrCodeSignature(id)).ToList();
```

**Real-World Variation:**
In practice, you might get these IDs from:
- A database query
- User input (from a document management UI)
- A previous search operation
- An external system (workflow engine, CRM, etc.)

Here's an example with dynamic ID retrieval:

```csharp
// Example: Get IDs from a database
string[] signatureIdList = GetSignatureIdsFromDatabase(documentId);

// Or from a previous search operation
var foundSignatures = signature.Search<QrCodeSignature>(new QrCodeSearchOptions());
string[] signatureIdList = foundSignatures
    .Where(s => s.Text.Contains("APPROVED") && s.SignTime < DateTime.Now.AddDays(-30))
    .Select(s => s.SignatureId)
    .ToArray();
```

#### Step 4: Delete the Signatures

Execute the deletion and handle the results properly:

```csharp
var deleteResult = signature.Delete(signatures);

if (deleteResult.Succeeded.Count == signatures.Count)
{
    Console.WriteLine("All signatures were successfully deleted!");
}
else
{
    Console.WriteLine($"Successfully deleted signatures : {deleteResult.Succeeded.Count}");
    Console.WriteLine($"Not deleted signatures : {deleteResult.Failed.Count}");
}
```

**Understanding the Result Object:**
The `deleteResult` object gives you granular information:
- `Succeeded`: List of signatures that were successfully deleted
- `Failed`: List of signatures that couldn't be deleted
- You can inspect these lists to log errors or retry failed deletions

**Production Enhancement:**
For production code, you'll want more robust error handling:

```csharp
var deleteResult = signature.Delete(signatures);

if (deleteResult.Succeeded.Count > 0)
{
    Console.WriteLine($"✓ Successfully deleted {deleteResult.Succeeded.Count} signature(s)");
    
    // Log successful deletions for audit trail
    foreach (var sig in deleteResult.Succeeded)
    {
        LogDeletion(documentId, sig.SignatureId, "Success");
    }
}

if (deleteResult.Failed.Count > 0)
{
    Console.WriteLine($"✗ Failed to delete {deleteResult.Failed.Count} signature(s)");
    
    // Log failures with details
    foreach (var sig in deleteResult.Failed)
    {
        Console.WriteLine($"  Failed ID: {sig.SignatureId}");
        LogDeletion(documentId, sig.SignatureId, "Failed");
    }
}
```

## Common Errors and How to Fix Them

Let's address the issues you're most likely to encounter (and their solutions).

### Error 1: "File is Being Used by Another Process"

**Symptom:** Exception thrown when trying to open the document file.

**Causes:**
- The file is open in another application (Adobe Reader, Word, etc.)
- A previous operation didn't properly close the file
- Antivirus software is scanning the file

**Solutions:**
```csharp
// Solution 1: Implement retry logic with delay
int maxRetries = 3;
int retryCount = 0;
bool success = false;

while (retryCount < maxRetries && !success)
{
    try
    {
        using (Signature signature = new Signature(outputFilePath))
        {
            // Your deletion code here
            success = true;
        }
    }
    catch (IOException ex)
    {
        retryCount++;
        if (retryCount >= maxRetries)
            throw;
        
        System.Threading.Thread.Sleep(1000); // Wait 1 second before retry
    }
}

// Solution 2: Check if file is locked before attempting
public static bool IsFileLocked(string filePath)
{
    try
    {
        using (FileStream stream = File.Open(filePath, FileMode.Open, FileAccess.Read, FileShare.None))
        {
            stream.Close();
        }
    }
    catch (IOException)
    {
        return true;
    }
    return false;
}
```

### Error 2: "Signature Not Found" or Zero Deletions

**Symptom:** The deletion operation reports 0 successful deletions.

**Causes:**
- The SignatureId doesn't exist in the document
- Typo in the SignatureId string
- The signature was already deleted in a previous operation

**Solution:**
```csharp
// Always verify signature exists before attempting deletion
public bool VerifySignatureExists(string signatureId, string filePath)
{
    using (Signature signature = new Signature(filePath))
    {
        var searchResults = signature.Search<QrCodeSignature>(new QrCodeSearchOptions());
        return searchResults.Any(s => s.SignatureId == signatureId);
    }
}

// Use it in your workflow
if (VerifySignatureExists(targetId, outputFilePath))
{
    // Proceed with deletion
}
else
{
    Console.WriteLine($"Warning: Signature {targetId} not found in document");
}
```

### Error 3: Permission Denied

**Symptom:** Access denied when trying to modify the file.

**Causes:**
- Insufficient file system permissions
- File is read-only
- Network path permissions (if file is on a shared drive)

**Solution:**
```csharp
// Check and remove read-only attribute
FileInfo fileInfo = new FileInfo(outputFilePath);
if (fileInfo.IsReadOnly)
{
    fileInfo.IsReadOnly = false;
}

// For network paths, ensure proper credentials are used
// Consider using impersonation if accessing shared drives
```

### Error 4: Invalid Document Format

**Symptom:** Exception about unsupported file format.

**Causes:**
- Document is corrupted
- File extension doesn't match actual format
- Document format is not supported by GroupDocs.Signature

**Solution:**
```csharp
// Validate document before processing
public bool IsValidDocument(string filePath)
{
    try
    {
        using (Signature signature = new Signature(filePath))
        {
            var documentInfo = signature.GetDocumentInfo();
            return documentInfo != null;
        }
    }
    catch (Exception ex)
    {
        Console.WriteLine($"Invalid document: {ex.Message}");
        return false;
    }
}
```

## Best Practices for Signature Management

Now that you know how to delete signatures, let's talk about doing it the right way in production environments.

### 1. Always Create Backups Before Deletion

```csharp
public string CreateBackup(string originalPath)
{
    string backupDir = Path.Combine(Path.GetDirectoryName(originalPath), "Backups");
    Directory.CreateDirectory(backupDir);
    
    string backupPath = Path.Combine(
        backupDir, 
        $"{Path.GetFileNameWithoutExtension(originalPath)}_backup_{DateTime.Now:yyyyMMddHHmmss}{Path.GetExtension(originalPath)}"
    );
    
    File.Copy(originalPath, backupPath);
    return backupPath;
}
```

### 2. Implement Audit Logging

Track all signature operations for compliance and debugging:

```csharp
public void LogSignatureOperation(string documentId, string signatureId, string operation, bool success)
{
    var logEntry = new
    {
        Timestamp = DateTime.UtcNow,
        DocumentId = documentId,
        SignatureId = signatureId,
        Operation = operation,
        Success = success,
        User = Environment.UserName
    };
    
    // Write to your logging system (database, file, etc.)
    Logger.LogInformation($"Signature operation: {JsonConvert.SerializeObject(logEntry)}");
}
```

### 3. Validate Before Deletion

Don't blindly delete signatures—validate them first:

```csharp
public bool ShouldDeleteSignature(QrCodeSignature signature)
{
    // Example business rules
    return signature.SignTime < DateTime.Now.AddYears(-1) || // Older than 1 year
           signature.Text.Contains("TEST") ||                 // Test signatures
           !signature.IsValid;                                // Invalid signatures
}
```

### 4. Handle Concurrent Access

If multiple users might access the same document:

```csharp
// Use file locking to prevent concurrent modifications
public void DeleteSignatureWithLock(string filePath, string signatureId)
{
    string lockFile = filePath + ".lock";
    
    try
    {
        // Create lock file
        using (File.Create(lockFile)) { }
        
        // Perform deletion
        using (Signature signature = new Signature(filePath))
        {
            var qrSignature = new QrCodeSignature(signatureId);
            signature.Delete(new List<QrCodeSignature> { qrSignature });
        }
    }
    finally
    {
        // Release lock
        if (File.Exists(lockFile))
            File.Delete(lockFile);
    }
}
```

### 5. Batch Processing for Performance

If you're deleting multiple signatures, batch them:

```csharp
public void DeleteMultipleSignatures(string filePath, List<string> signatureIds)
{
    using (Signature signature = new Signature(filePath))
    {
        // Create all signature objects at once
        var signatureslist = signatureIds.Select(id => new QrCodeSignature(id)).ToList();
        
        // Single delete operation for all signatures
        var result = signature.Delete(signatures);
        
        Console.WriteLine($"Batch deleted {result.Succeeded.Count}/{signatureIds.Count} signatures");
    }
}
```

## Alternative Approaches (When to Use Each)

While deleting by ID is precise, there are other approaches depending on your use case.

### Approach 1: Delete by ID (What We've Covered)
**Best for:** Precise control, user-selected deletions, targeted cleanup

**Pros:**
- Surgical precision
- Can delete specific signatures without affecting others
- Ideal for UI-driven operations

**Cons:**
- Requires knowing SignatureIds upfront
- More code for bulk operations

### Approach 2: Delete All Signatures of a Type
**Best for:** Clearing all QR codes, document template reset

```csharp
using (Signature signature = new Signature(filePath))
{
    // Search for all QR codes
    var qrSignatures = signature.Search<QrCodeSignature>(new QrCodeSearchOptions());
    
    // Delete all found signatures
    var result = signature.Delete(qrSignatures);
}
```

**When to use this:**
- Resetting document templates
- Clearing test signatures in bulk
- Document archival processes

### Approach 3: Conditional Deletion
**Best for:** Business rule-based cleanup

```csharp
using (Signature signature = new Signature(filePath))
{
    var qrSignatures = signature.Search<QrCodeSignature>(new QrCodeSearchOptions());
    
    // Delete only signatures matching criteria
    var toDelete = qrSignatures
        .Where(s => s.SignTime < DateTime.Now.AddDays(-90)) // Older than 90 days
        .ToList();
    
    var result = signature.Delete(toDelete);
}
```

**When to use this:**
- Automated cleanup jobs
- Compliance-driven deletion
- Expiration-based workflows

## Practical Applications & Integration

Let's look at how this fits into real-world systems.

### Integration Example: Document Management System

```csharp
public class DocumentSignatureService
{
    private readonly Signature _signature;
    private readonly IDocumentRepository _repository;
    private readonly IAuditLogger _logger;
    
    public async Task<bool> RemoveSignatureAsync(int documentId, string signatureId)
    {
        // 1. Retrieve document metadata
        var document = await _repository.GetDocumentAsync(documentId);
        
        // 2. Create backup
        var backupPath = CreateBackup(document.FilePath);
        
        try
        {
            // 3. Perform deletion
            using (var signature = new Signature(document.FilePath))
            {
                var qrSignature = new QrCodeSignature(signatureId);
                var result = signature.Delete(new List<QrCodeSignature> { qrSignature });
                
                // 4. Update database
                if (result.Succeeded.Count > 0)
                {
                    await _repository.UpdateSignatureStatusAsync(documentId, signatureId, "Deleted");
                    
                    // 5. Log operation
                    await _logger.LogAsync($"Signature {signatureId} deleted from document {documentId}");
                    
                    return true;
                }
            }
        }
        catch (Exception ex)
        {
            // Restore from backup on error
            File.Copy(backupPath, document.FilePath, true);
            await _logger.LogErrorAsync($"Failed to delete signature: {ex.Message}");
        }
        
        return false;
    }
}
```

### Workflow Automation Example

```csharp
public class SignatureCleanupJob
{
    public void ExecuteCleanup()
    {
        // Get all documents requiring signature cleanup
        var documentsToClean = GetDocumentsForCleanup();
        
        foreach (var doc in documentsToClean)
        {
            try
            {
                using (Signature signature = new Signature(doc.FilePath))
                {
                    // Find expired signatures
                    var allSignatures = signature.Search<QrCodeSignature>(new QrCodeSearchOptions());
                    var expiredSignatures = allSignatures
                        .Where(s => IsSignatureExpired(s))
                        .ToList();
                    
                    if (expiredSignatures.Any())
                    {
                        var result = signature.Delete(expiredSignatures);
                        NotifyDocumentOwner(doc.Id, result.Succeeded.Count);
                    }
                }
            }
            catch (Exception ex)
            {
                LogError(doc.Id, ex);
            }
        }
    }
}
```

## Performance Considerations

When working with large documents or high-volume operations, keep these in mind:

### 1. Memory Management
```csharp
// BAD: Loading all documents at once
var allDocs = GetThousandsOfDocuments();
foreach (var doc in allDocs)
{
    ProcessSignatures(doc);
}

// GOOD: Process in batches
int batchSize = 50;
int skip = 0;
while (true)
{
    var batch = GetDocumentBatch(skip, batchSize);
    if (!batch.Any()) break;
    
    foreach (var doc in batch)
    {
        ProcessSignatures(doc);
    }
    
    skip += batchSize;
}
```

### 2. File I/O Optimization
- Use `FileShare.Read` when possible to allow concurrent reads
- Process multiple documents in parallel (but be mindful of system resources)
- Consider moving processed files to reduce directory scan times

### 3. Async Operations
For web applications, wrap signature operations in async methods:

```csharp
public async Task<DeleteResult> DeleteSignatureAsync(string filePath, string signatureId)
{
    return await Task.Run(() =>
    {
        using (Signature signature = new Signature(filePath))
        {
            var qrSignature = new QrCodeSignature(signatureId);
            return signature.Delete(new List<QrCodeSignature> { qrSignature });
        }
    });
}
```

## Conclusion

You now have everything you need to programmatically remove QR code signatures from documents using GroupDocs.Signature for .NET. We've covered the basics of deletion by ID, troubleshooting common issues, and implementing production-ready solutions with proper error handling and logging.

**Key Takeaways:**
- Deletion by SignatureId gives you precise control over which signatures to remove
- Always create backups before modifying documents
- Implement proper error handling and logging for production use
- Consider your use case when choosing between deletion approaches
- Batch operations when working with multiple signatures

**Next Steps:**
- Explore [adding signatures](https://docs.groupdocs.com/signature/net/) to documents
- Learn about [signature verification](https://docs.groupdocs.com/signature/net/) workflows
- Implement [search functionality](https://docs.groupdocs.com/signature/net/) for complex filtering
- Check out [digital signature types](https://docs.groupdocs.com/signature/net/) beyond QR codes

Ready to level up your document management system? Start experimenting with the code samples above and adapt them to your specific needs.

## FAQ Section

### 1. Can I delete multiple types of signatures (QR codes, barcodes, text) at once?
Yes! GroupDocs.Signature lets you delete different signature types in a single operation. Just search for multiple signature types and pass them all to the `Delete()` method:

```csharp
var qrSignatures = signature.Search<QrCodeSignature>(new QrCodeSearchOptions());
var barcodeSignatures = signature.Search<BarcodeSignature>(new BarcodeSearchOptions());
var allSignatures = new List<BaseSignature>();
allSignatures.AddRange(qrSignatures);
allSignatures.AddRange(barcodeSignatures);
var result = signature.Delete(allSignatures);
```

### 2. What happens if I try to delete a signature that doesn't exist?
The operation won't throw an error, but the `deleteResult.Failed` count will increment. The signature you attempted to delete will appear in the `Failed` collection. Always check the result object to verify successful deletions.

### 3. Does deleting a signature modify the original document or create a new one?
It depends on your implementation. In our examples, we copy the file first, then modify the copy. But you can work directly on the original if you want—just be sure to have proper backups and error handling in place.

### 4. Can I undo a signature deletion?
Not directly through GroupDocs.Signature. Once deleted, the signature is removed from the document. This is why creating backups before deletion is critical. If you need undo functionality, implement a versioning system or backup strategy in your application.

### 5. How do I delete signatures from password-protected documents?
You need to provide the password when initializing the `Signature` object:

```csharp
LoadOptions loadOptions = new LoadOptions()
{
    Password = "your_document_password"
};
using (Signature signature = new Signature(filePath, loadOptions))
{
    // Deletion code here
}
```

### 6. Is there a limit to how many signatures I can delete in one operation?
There's no hard limit imposed by GroupDocs.Signature, but performance depends on your document size and system resources. For hundreds of signatures, consider batching the operations to avoid memory issues.

### 7. Can I delete signatures from documents stored in cloud storage (S3, Azure Blob, etc.)?
Yes, but you'll need to download the file first, perform the operation locally, then upload it back. GroupDocs.Signature works with local file streams. Alternatively, use stream-based initialization if your cloud SDK supports it.

### 8. Will deleting a QR code signature affect the document layout or formatting?
No. GroupDocs.Signature removes the signature object cleanly without affecting the document's layout, formatting, or other content. The space where the signature was remains empty.

### 9. How can I delete all signatures from a specific date range?
Search for signatures, filter by date, then delete:

```csharp
var allSignatures = signature.Search<QrCodeSignature>(new QrCodeSearchOptions());
var targetSignatures = allSignatures
    .Where(s => s.SignTime >= startDate && s.SignTime <= endDate)
    .ToList();
var result = signature.Delete(targetSignatures);
```

### 10. What's the best way to test signature deletion without affecting production documents?
Create a dedicated test environment with copies of your production documents. Add test signatures with known IDs, then practice your deletion workflows