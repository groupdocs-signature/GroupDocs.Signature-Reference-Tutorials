---
title: How to Remove QR Code Signatures from Documents in .NET
linktitle: Delete QR Code Signature from Document
second_title: GroupDocs.Signature .NET API
description: Learn how to easily delete QR code signatures from your documents using GroupDocs.Signature for .NET with our step-by-step developer guide.
weight: 16
url: /net/delete-operations/delete-qr-code-signature/
---

# How to Delete QR Code Signatures from Your Documents

## Introduction

Have you ever needed to remove a QR code signature from a document programmatically? Whether you're cleaning up outdated information or preparing documents for redistribution, being able to manage document signatures effectively is a crucial skill for .NET developers.

In this friendly guide, we'll walk you through exactly how to delete QR code signatures from documents using GroupDocs.Signature for .NET. This powerful library makes signature management straightforward, allowing you to focus on building great applications rather than wrestling with document manipulation challenges.

## What You'll Need Before Starting

Before we dive into the code, let's make sure you have everything ready:

- GroupDocs.Signature for .NET: You'll need the library installed in your project. You can download it directly from [the GroupDocs releases page](https://releases.groupdocs.com/signature/net/).
- A document with QR codes: For practice, prepare a document that contains at least one QR code signature you want to remove.
- Basic C# knowledge: You should be comfortable with C# fundamentals to follow along with our examples.

Once you have these prerequisites in place, you're ready to start removing those QR codes!

## Setting Up Your Project with the Right Namespaces

First things first – let's import the necessary namespaces to make our code work smoothly:

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

These imports give us access to all the functionality we need from the GroupDocs.Signature library, as well as some essential .NET classes for file handling.

## Step 1: Where Are Your Files? Setting Up Document Paths

Let's start by defining where our documents are located and where we want to save the modified version:

```csharp
// The path to the documents directory.
string filePath = "sample_multiple_signatures.docx";
string fileName = Path.GetFileName(filePath);

// Define the output file path for the modified document.
string outputFilePath = Path.Combine("Your Document Directory", "DeleteQRCode", fileName);

// Copy the source file since the Delete method works with the same Document.
File.Copy(filePath, outputFilePath, true);
```

Notice that we're creating a copy of our original document. This is important because the signature deletion process will modify the file directly, and we always want to preserve our original documents.

## Step 2: Creating a Signature Object to Work With

Now we'll create a Signature object that connects to our document:

```csharp
using (Signature signature = new Signature(outputFilePath))
{
    // Create options for searching QR code signatures.
    QrCodeSearchOptions options = new QrCodeSearchOptions();
    
    // Search for QR code signatures in the document.
    List<QrCodeSignature> signatures = signature.Search<QrCodeSignature>(options);
```

This code initializes the Signature object with our document and then searches for any QR code signatures present in it. The search returns a list of all QR code signatures found.

## Step 3: Are There Any QR Codes to Delete?

Before attempting to delete anything, we should check if there are actually QR codes present:

```csharp
    if (signatures.Count > 0)
    {
        // Get the first QR code signature found in the document.
        QrCodeSignature qrCodeSignature = signatures[0];
```

This simple check ensures we only proceed if there's at least one QR code signature in the document. In this example, we're targeting the first QR code found, but you could easily modify this to handle multiple signatures if needed.

## Step 4: Removing the QR Code From Your Document

Now for the main event – actually deleting the QR code:

```csharp
        // Delete the QR code signature from the document.
        bool result = signature.Delete(qrCodeSignature);
        
        if (result)
        {
            Console.WriteLine($"Signature with QR-Code '{qrCodeSignature.Text}' and encode type '{qrCodeSignature.EncodeType.TypeName}' was deleted from document ['{fileName}'].");
        }
        else
        {
            Console.WriteLine($"Signature was not deleted from the document! Signature with QR-Code '{qrCodeSignature.Text}' and encode type '{qrCodeSignature.EncodeType.TypeName}' was not found!");
        }
    }
}
```

The code deletes the signature and provides feedback about whether the operation was successful. This feedback is crucial for debugging and confirming that your code is working as expected.

## What Have We Accomplished?

Congratulations! You've just learned how to remove QR code signatures from documents using GroupDocs.Signature for .NET. This skill opens up numerous possibilities for document management in your applications.

With just a few lines of code, you can now programmatically clean up documents by removing outdated or unnecessary QR code signatures, ensuring your documents always contain only the relevant information.

## Common Questions You Might Have

### Can I delete multiple QR codes at once?

Absolutely! Instead of just deleting the first signature found, you could iterate through the entire list of signatures and delete each one like this:

```csharp
foreach(var qrSignature in signatures)
{
    signature.Delete(qrSignature);
}
```

### What other types of signatures can I manage with GroupDocs.Signature?

GroupDocs.Signature is incredibly versatile, supporting various signature types including:
- Text signatures
- Image signatures
- Barcode signatures
- Digital signatures
- And many more!

### Will this work with all my document formats?

You'll be pleased to know that GroupDocs.Signature works with a wide range of document formats, including:
- PDF documents
- Microsoft Word documents
- Excel spreadsheets
- PowerPoint presentations
- And many others

### Can I search for specific QR codes rather than deleting all of them?

Yes! The `QrCodeSearchOptions` class offers various properties to filter your search. You could, for example, search for QR codes containing specific text or encoded with particular formats.

### Is there a way to try GroupDocs.Signature before purchasing?

Yes, you can download a free trial version from [the GroupDocs website](https://releases.groupdocs.com/) to test it with your specific use cases before making a commitment.
