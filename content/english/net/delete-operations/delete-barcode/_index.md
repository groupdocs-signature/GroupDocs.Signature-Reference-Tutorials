---
title: Delete Barcode from Document
linktitle: Delete Barcode from Document
second_title: GroupDocs.Signature .NET API
description: Learn how to delete barcode from a document using GroupDocs.Signature for .NET. Step-by-step guide with code examples.
weight: 10
url: /net/delete-operations/delete-barcode/
---

# Delete Barcode from Document

## Introduction
GroupDocs.Signature for .NET is a powerful library that enables developers to seamlessly work with digital signatures, stamps, and barcodes within .NET applications. In this tutorial, we will guide you through the process of deleting a barcode from a document using GroupDocs.Signature for .NET.
## Prerequisites
Before we get started, ensure that you have the following prerequisites:
- Basic knowledge of C# programming language.
- Visual Studio installed on your system.
- GroupDocs.Signature for .NET library installed. You can download it from [here](https://releases.groupdocs.com/signature/net/).
- A sample document with a barcode that you want to delete.

## Import Namespaces
First, make sure to import the necessary namespaces into your C# code:
```csharp
using System;
using System.IO;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

Let's break down the process of deleting a barcode from a document into simple steps:
## Step 1: Define File Paths
```csharp
string filePath = "sample_multiple_signatures.docx";
string fileName = Path.GetFileName(filePath);
string outputFilePath = Path.Combine("Your Document Directory", "DeleteBarcode", fileName);
```
Ensure to replace `"sample_multiple_signatures.docx"` with the path to your document containing the barcode.
## Step 2: Copy the Source File
```csharp
File.Copy(filePath, outputFilePath, true);
```
This step ensures that we are working with a copy of the original document to preserve the original file.
## Step 3: Initialize GroupDocs.Signature
```csharp
using (Signature signature = new Signature(outputFilePath))
{
    // Your code goes here
}
```
Initialize the Signature object by passing the path to the document copy created in the previous step.
## Step 4: Search for Barcode Signatures
```csharp
BarcodeSearchOptions options = new BarcodeSearchOptions();
List<BarcodeSignature> signatures = signature.Search<BarcodeSignature>(options);
```
Create an instance of BarcodeSearchOptions and use it to search for barcode signatures within the document.
## Step 5: Delete Barcode Signature
```csharp
if (signatures.Count > 0)
{
    BarcodeSignature barcodeSignature = signatures[0];
    bool result = signature.Delete(barcodeSignature);
    if (result)
    {
        Console.WriteLine($"Signature with Barcode '{barcodeSignature.Text}' and encode type '{barcodeSignature.EncodeType.TypeName}' was deleted from document ['{fileName}'].");
    }
    else
    {
        Helper.WriteError($"Signature was not deleted from the document! Signature with Barcode '{barcodeSignature.Text}' and encode type '{barcodeSignature.EncodeType.TypeName}' was not found!");
    }
}
```
Check if barcode signatures are found in the document. If found, delete the first barcode signature found.

## Conclusion
In this tutorial, we have learned how to delete a barcode from a document using GroupDocs.Signature for .NET. By following the step-by-step guide, you can seamlessly integrate barcode deletion functionality into your .NET applications.
## FAQ's
### Can I delete multiple barcode signatures from a document?
Yes, you can modify the code to delete multiple barcode signatures by iterating over the list of signatures.
### Does GroupDocs.Signature for .NET support other types of signatures?
Yes, GroupDocs.Signature for .NET supports various types of signatures, including digital signatures, stamps, and text signatures.
### Can I customize the search options for barcode signatures?
Yes, you can customize the search options according to your requirements, such as specifying barcode types or search areas within the document.
### Is GroupDocs.Signature for .NET compatible with different document formats?
Yes, GroupDocs.Signature for .NET supports a wide range of document formats, including Word, Excel, PDF, and more.
### Where can I find additional support or resources for GroupDocs.Signature for .NET?
You can visit the GroupDocs.Signature forum [here](https://forum.groupdocs.com/c/signature/13) for any queries or assistance regarding the library.
