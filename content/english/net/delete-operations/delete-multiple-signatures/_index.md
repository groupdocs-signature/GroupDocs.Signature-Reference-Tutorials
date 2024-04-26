---
title: Delete Multiple Signatures from Document
linktitle: Delete Multiple Signatures from Document
second_title: GroupDocs.Signature .NET API
description: Effortlessly delete multiple signatures from documents using GroupDocs.Signature for .NET. Streamline your document management workflow.
type: docs
weight: 15
url: /net/delete-operations/delete-multiple-signatures/
---
## Introduction
In the digital world, document management often involves handling various signatures. Deleting multiple signatures from a document programmatically can streamline workflows and enhance efficiency. With GroupDocs.Signature for .NET, this task becomes seamless and straightforward. This tutorial will guide you through the process of deleting multiple signatures from a document step by step.
## Prerequisites
Before diving into the tutorial, ensure you have the following prerequisites:
- Basic understanding of C# programming language.
- Installed GroupDocs.Signature for .NET library.
- Sample document with multiple signatures for testing.

## Import Namespaces
Begin by importing the necessary namespaces to access the functionality of GroupDocs.Signature for .NET:
```csharp
using System;
using System.IO;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## Step 1: Define Document Path and File Name
Set the file path of the document containing multiple signatures. Ensure you have the appropriate file path and file name:
```csharp
string filePath = "sample_multiple_signatures.docx";
string fileName = Path.GetFileName(filePath);
```
## Step 2: Copy the Document for Processing
To avoid modifying the original document, create a copy for processing:
```csharp
string outputFilePath = Path.Combine("Your Document Directory", "DeleteMultiple", fileName);
File.Copy(filePath, outputFilePath, true);
```
## Step 3: Initialize Signature Object
Instantiate a Signature object using the output file path:
```csharp
using (Signature signature = new Signature(outputFilePath))
{
    // Signature processing code goes here
}
```
## Step 4: Define Search Options
Define various search options to identify signatures within the document. Options include text search, image search, barcode search, and QR code search:
```csharp
TextSearchOptions textSearchOptions = new TextSearchOptions();
ImageSearchOptions imageSearchOptions = new ImageSearchOptions();
BarcodeSearchOptions barcodeOptions = new BarcodeSearchOptions();
QrCodeSearchOptions qrCodeOptions = new QrCodeSearchOptions();
// Add options to list
List<SearchOptions> listOptions = new List<SearchOptions>();
listOptions.Add(textSearchOptions);
listOptions.Add(imageSearchOptions);
listOptions.Add(barcodeOptions);
listOptions.Add(qrCodeOptions);
```
## Step 5: Search for Signatures
Execute a search operation to find all signatures within the document based on the defined search options:
```csharp
SearchResult result = signature.Search(listOptions);
```
## Step 6: Delete Signatures
If signatures are found, proceed to delete them:
```csharp
if (result.Signatures.Count > 0)
{
    // Attempt to delete all signatures
    DeleteResult deleteResult = signature.Delete(result.Signatures);
    // Check if deletion was successful
    if(deleteResult.Succeeded.Count == result.Signatures.Count)
    {
        Console.WriteLine("\nAll signatures were successfully deleted!");                        
    }
    else
    {
        Console.WriteLine($"Successfully deleted signatures : {deleteResult.Succeeded.Count}");
        Helper.WriteError($"Not deleted signatures : {deleteResult.Failed.Count}");
    }
    // Display information about deleted signatures
    Console.WriteLine("\nList of deleted signatures:");
    int number = 1;
    foreach(BaseSignature temp in deleteResult.Succeeded)
    {
        Console.WriteLine($"Signature #{number++}: Type: {temp.SignatureType} Id:{temp.SignatureId}, Location: {temp.Left}x{temp.Top}. Size: {temp.Width}x{temp.Height}");
    }
}
else
{
    Helper.WriteError("No one signature was found.");
}
```

## Conclusion
Deleting multiple signatures from a document programmatically is a crucial task in document management. With GroupDocs.Signature for .NET, this process becomes efficient and reliable. By following the steps outlined in this tutorial, you can easily integrate signature deletion functionality into your .NET applications.
## FAQ's
### Can GroupDocs.Signature for .NET handle various document formats?
Yes, GroupDocs.Signature for .NET supports a wide range of document formats, including DOCX, PDF, PPTX, XLSX, and more.
### Is it possible to customize search options for signature detection?
Absolutely, you can tailor search options such as text search, image search, barcode search, and QR code search to meet your specific requirements.
### Does GroupDocs.Signature for .NET provide error handling mechanisms?
Yes, the library offers robust error handling capabilities to ensure smooth execution of document processing tasks.
### Can I integrate GroupDocs.Signature for .NET with other third-party libraries?
Certainly, GroupDocs.Signature for .NET is designed to seamlessly integrate with other .NET libraries, providing flexibility and extensibility.
### Where can I find additional support and resources for GroupDocs.Signature for .NET?
You can visit the GroupDocs [forum](https://forum.groupdocs.com/c/signature/13) dedicated to signature-related discussions and seek assistance from the community and experts.
