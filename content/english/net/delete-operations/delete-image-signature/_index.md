---
title: Delete Image Signature
linktitle: Delete Image Signature
second_title: GroupDocs.Signature .NET API
description: Learn how to delete image signatures from documents using GroupDocs.Signature for .NET. Follow our step-by-step guide for efficient signature management.
weight: 14
url: /net/delete-operations/delete-image-signature/
---

# Delete Image Signature

## Introduction
In this tutorial, we'll explore how to delete image signatures from documents using GroupDocs.Signature for .NET. GroupDocs.Signature is a powerful library that allows developers to work with digital signatures, stamps, and form fields within various document formats.
## Prerequisites
Before we begin, ensure you have the following:
### 1. GroupDocs.Signature for .NET
Download and install GroupDocs.Signature for .NET from the [website](https://releases.groupdocs.com/signature/net/). Follow the installation instructions provided in the documentation.
### 2. .NET Framework
Make sure you have the .NET Framework installed on your machine.
## Import Namespaces
Include the necessary namespaces in your project:
```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
Let's break down the process of deleting image signatures into multiple steps:
## Step 1: Define File Paths
First, specify the paths for the input document and the output document after deleting the signature:
```csharp
string filePath = "sample_multiple_signatures.docx";
string fileName = Path.GetFileName(filePath);
string outputFilePath = Path.Combine("Your Document Directory", "DeleteImage", fileName);
```
## Step 2: Copy the Source File
Since the `Delete` method works with the same document, it's essential to copy the source file to another location:
```csharp
File.Copy(filePath, outputFilePath, true);
```
## Step 3: Initialize Signature Object
Create an instance of the `Signature` class and specify the path to the output document:
```csharp
using (Signature signature = new Signature(outputFilePath))
{
    // Code goes here
}
```
## Step 4: Search for Image Signatures
Define search options and search for image signatures within the document:
```csharp
ImageSearchOptions options = new ImageSearchOptions();
List<ImageSignature> signatures = signature.Search<ImageSignature>(options);
```
## Step 5: Delete Image Signature
If image signatures are found, delete the first one:
```csharp
if (signatures.Count > 0)
{
    ImageSignature imageSignature = signatures[0];
    bool result = signature.Delete(imageSignature);
    if (result)
    {
        Console.WriteLine($"Image signature at location {imageSignature.Left}x{imageSignature.Top} and Size {imageSignature.Size} was deleted from document ['{fileName}'].");
    }
    else
    {
        Helper.WriteError($"Signature was not deleted from the document! Signature at location {imageSignature.Left}x{imageSignature.Top} and Size {imageSignature.Size} was not found!");
    }
}
```
## Conclusion
In this tutorial, we learned how to delete image signatures from documents using GroupDocs.Signature for .NET. By following the step-by-step guide, developers can efficiently manage digital signatures within their applications.
## FAQ's
### Can I delete multiple image signatures from a document?
Yes, you can modify the code to delete multiple image signatures by iterating over the `signatures` list.
### Does GroupDocs.Signature support other document formats besides DOCX?
Yes, GroupDocs.Signature supports a wide range of document formats, including PDF, PPT, XLS, and more.
### Is there a trial version available for GroupDocs.Signature for .NET?
Yes, you can download a free trial version from the [website](https://releases.groupdocs.com/).
### How can I get support for GroupDocs.Signature?
You can visit the [GroupDocs.Signature forum](https://forum.groupdocs.com/c/signature/13) for assistance and support.
### Can I purchase a temporary license for GroupDocs.Signature?
Yes, you can purchase a temporary license from the [purchase page](https://purchase.groupdocs.com/temporary-license/).
