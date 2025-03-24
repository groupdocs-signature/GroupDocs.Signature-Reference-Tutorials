---
title: Delete Signature by ID
linktitle: Delete Signature by ID
second_title: GroupDocs.Signature .NET API
description: Learn how to delete a signature by ID in .NET documents using GroupDocs.Signature library. Easy step-by-step guide.
weight: 11
url: /net/delete-operations/delete-signature-by-id/
---
## Introduction
In this tutorial, we'll explore how to delete a signature by its ID using GroupDocs.Signature for .NET. GroupDocs.Signature for .NET is a powerful library that allows developers to add, remove, or verify digital signatures in various document formats using .NET applications.
## Prerequisites
Before we begin, make sure you have the following prerequisites:
1. GroupDocs.Signature for .NET Library: Download and install the library from [here](https://releases.groupdocs.com/signature/net/).
2. .NET Framework: Ensure you have .NET Framework installed on your system.
3. Document with Signature: Prepare a document (e.g., DOCX, PDF) with a signature that you want to delete.

## Import Namespaces
```csharp
using System;
using System.IO;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## Step 1: Define File Paths
First, specify the file path for the document containing the signature, and the output file path where the modified document will be saved.
```csharp
string filePath = "sample_multiple_signatures.docx";
string fileName = Path.GetFileName(filePath);
string outputFilePath = Path.Combine("Your Document Directory", "DeleteById", fileName);
```
## Step 2: Copy the Document
Since the `Delete` method modifies the document in place, it's best to create a copy of the original document.
```csharp
File.Copy(filePath, outputFilePath, true);
```
## Step 3: Delete Signature by ID
Initialize the `Signature` object with the document file path and use the `Delete` method to remove the signature by its ID.
```csharp
using (Signature signature = new Signature(outputFilePath))
{
    string id = @"eff64a14-dad9-47b0-88e5-2ee4e3604e71";
    bool result = signature.Delete(id);
    if (result)
    {
        Console.WriteLine($"Signature with Id# '{id}' was deleted from document ['{fileName}'].");
    }
    else
    {
        Helper.WriteError($"Signature was not deleted from the document! Signature with id# '{id}' was not found!");
    }
}
```

## Conclusion
In this tutorial, we've learned how to delete a signature by its ID using GroupDocs.Signature for .NET. This library provides a convenient way to manage digital signatures in various document formats programmatically.
## FAQ's
### Can I delete multiple signatures at once?
Yes, you can delete multiple signatures by iterating through their IDs and calling the `Delete` method for each ID.
### Is GroupDocs.Signature for .NET compatible with all document formats?
GroupDocs.Signature for .NET supports a wide range of document formats, including PDF, DOCX, XLSX, and more.
### Can I customize the appearance of the signature?
Yes, you can customize the appearance of the signature, including its position, size, font, and color.
### Is there a trial version available?
Yes, you can download a free trial version from [here](https://releases.groupdocs.com/).
### Where can I find help or support for GroupDocs.Signature for .NET?
You can visit the support forum [here](https://forum.groupdocs.com/c/signature/13) for assistance.
