---
title: How to Remove Document Signatures by Type in .NET
linktitle: Delete Signature by Type
second_title: GroupDocs.Signature .NET API
description: Learn how to easily delete specific signature types from documents using GroupDocs.Signature for .NET. Master signature management in just minutes!
weight: 12
url: /net/delete-operations/delete-signature-by-type/
---

# How to Remove Document Signatures by Type in .NET

## Why Signature Management Matters in Document Processing

In today's document-driven business world, managing digital signatures efficiently can make or break your workflow. Whether you're handling contracts with multiple approvals, processing legal documents, or maintaining compliance records, having control over the signatures in your documents is essential. That's where GroupDocs.Signature for .NET comes to the rescue, offering a straightforward way to manage signatures—including selectively removing them by type.

Think about it: how often have you needed to update a document by removing outdated QR codes or digital signatures while keeping others intact? We'll show you exactly how to accomplish this with minimal code, helping you streamline your document management process.

## What You'll Need Before Starting

Before we dive into the code, let's make sure you have everything ready:

- A basic understanding of C# programming (don't worry, our examples are beginner-friendly)
- GroupDocs.Signature for .NET installed in your project (download it [here](https://releases.groupdocs.com/signature/net/))
- Visual Studio or your preferred .NET development environment
- A sample document with signatures you'd like to remove (we'll use a document with multiple signature types for demonstration)

## Setting Up Your Project Environment

First, let's import the necessary namespaces to access all the functionality we need from GroupDocs.Signature:

```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
```

These imports give us access to the core signature manipulation tools and document handling capabilities we'll need throughout the process.

## Step 1: Where Are Your Documents Located?

Let's start by defining where your document is located and where you want to save the modified version:

```csharp
string filePath = "sample_multiple_signatures.docx";
string fileName = Path.GetFileName(filePath);
string outputFilePath = Path.Combine("Your Document Directory", "DeleteBySignatureType", fileName);
```

Remember to replace "Your Document Directory" with the actual folder path where you store your documents. This setup ensures your original file stays intact while we work on a copy.

## Step 2: Creating a Working Copy of Your Document

When deleting signatures, it's always wise to preserve your original document. Here's how we'll create a backup before making any changes:

```csharp
File.Copy(filePath, outputFilePath, true);
```

This simple line creates a duplicate of your document that we can modify safely. The "true" parameter ensures we overwrite any existing file with the same name, giving us a fresh start each time we run the code.

## Step 3: Removing the Signatures You Don't Need

Now for the main event—let's initialize the GroupDocs.Signature object and tell it which signature types to remove:

```csharp
using (Signature signature = new Signature(outputFilePath))
{
    DeleteResult result = signature.Delete(SignatureType.QrCode);
```

In this example, we're targeting QR code signatures for removal. Need to delete a different type instead? Simply replace `SignatureType.QrCode` with the appropriate type, such as:
- `SignatureType.Text` for text-based signatures
- `SignatureType.Image` for image signatures
- `SignatureType.Digital` for digital certificate signatures
- `SignatureType.Barcode` for standard barcodes

## Step 4: Verifying What Changed in Your Document

After removing signatures, it's helpful to know exactly what was deleted. Let's add some code to provide that feedback:

```csharp
if (result.Succeeded.Count > 0)
{
    Console.WriteLine("Successfully removed the following QR-Code signatures:");
    int number = 1;
    foreach (QrCodeSignature temp in result.Succeeded)
    {
        Console.WriteLine($"Signature #{number++}: Type: {temp.SignatureType} Id:{temp.SignatureId}, Text: {temp.Text}");
    }
}
else
{
    Console.WriteLine("No QR-Code signatures were found to delete in this document.");
}
```

This gives you clear confirmation of which signatures were removed, including their details—extremely helpful when processing batches of documents or when you need to track changes for compliance purposes.

## Take Control of Your Document Signatures

Managing signatures in your documents doesn't have to be complicated. With GroupDocs.Signature for .NET, you have a powerful tool at your fingertips to selectively remove signatures based on their type. This capability is invaluable when you need to update documents, remove outdated approvals, or prepare templates for new signature cycles.

The best part? You can integrate this functionality directly into your existing document management systems, creating a seamless workflow for your team or clients.

Ready to take your document processing to the next level? Give this code a try in your next project and experience the efficiency of programmatic signature management.

## Common Questions About Signature Deletion

### Can I remove multiple types of signatures at once?
Yes! You can either chain multiple delete operations or use a collection of signature types to remove several types in one pass. For example:
```csharp
DeleteResult result = signature.Delete(new[] { SignatureType.QrCode, SignatureType.Barcode });
```

### What document formats does GroupDocs.Signature for .NET support?
The library supports a comprehensive range of formats including PDF, Word documents (DOC, DOCX), Excel spreadsheets (XLS, XLSX), PowerPoint presentations (PPT, PPTX), images, and many more. Your document management needs are covered regardless of file type.

### Can I filter which signatures to delete based on content or other properties?
Absolutely! GroupDocs.Signature provides advanced options for targeted deletion based on signature content, position, appearance, and other attributes. You can craft specific criteria to precisely control which signatures get removed.

### Is there a way to try GroupDocs.Signature before purchasing?
Yes, you can download a free trial version from [the GroupDocs website](https://releases.groupdocs.com/) to explore all features before making a decision.

### Where can I get help if I run into issues with signature deletion?
The GroupDocs community is active and supportive. Visit the [GroupDocs.Signature forum](https://forum.groupdocs.com/c/signature/13) for assistance from both the development team and other users.