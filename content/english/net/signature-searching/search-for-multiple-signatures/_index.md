---
title: Search for Multiple Signatures
linktitle: Search for Multiple Signatures
second_title: GroupDocs.Signature .NET API
description: Learn how to search for multiple signatures in .NET documents using GroupDocs.Signature for efficient document security and integrity.
weight: 14
url: /net/signature-searching/search-for-multiple-signatures/
---
## Introduction
GroupDocs.Signature for .NET is a powerful library that enables developers to add, search, and remove various types of signatures in popular document formats using .NET applications. In this tutorial, we'll focus on searching for multiple signatures within a document using GroupDocs.Signature for .NET.
## Prerequisites
Before we begin, make sure you have the following prerequisites:
- Visual Studio installed on your system.
- Basic understanding of C# programming language.
- GroupDocs.Signature for .NET library installed in your project. You can download it from [here](https://releases.groupdocs.com/signature/net/).

## Import Namespaces
First, you need to import the necessary namespaces to access the classes and methods provided by GroupDocs.Signature for .NET.
```csharp
using System;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## Step 1: Load the Document
Load the document where you want to search for multiple signatures. Ensure that you provide the correct file path.
```csharp
string filePath = "sample_multiple_signatures.docx";
using (Signature signature = new Signature(filePath))
{
    // Your code goes here
}
```
## Step 2: Define Search Options
Define search options for various types of signatures such as text, digital, barcode, QR code, and metadata. You can specify search criteria like text to match, match type, and search across all pages.
```csharp
// Define search options
TextSearchOptions textOptions = new TextSearchOptions()
{
    AllPages = true
};
DigitalSearchOptions digitalOptions = new DigitalSearchOptions()
{
    AllPages = true
};
BarcodeSearchOptions barcodeOptions = new BarcodeSearchOptions()
{
    AllPages = true,
    Text = "123456",
    MatchType = TextMatchType.Exact
};
QrCodeSearchOptions qrCodeOptions = new QrCodeSearchOptions()
{
    AllPages = true,
    Text = "John",
    MatchType = TextMatchType.Contains
};
MetadataSearchOptions metadataOptions = new MetadataSearchOptions();
```
## Step 3: Add Search Options to List
Add the defined search options to a list.
```csharp
// Add options to list
List<SearchOptions> listOptions = new List<SearchOptions>();
listOptions.Add(textOptions);
listOptions.Add(barcodeOptions);
listOptions.Add(qrCodeOptions);
listOptions.Add(metadataOptions);
listOptions.Add(digitalOptions);
```
## Step 4: Search for Signatures
Search for signatures in the document using the defined search options.
```csharp
// Search for signatures in document
SearchResult result = signature.Search(listOptions);
if (result.Signatures.Count > 0)
{
    Console.WriteLine($"\nSource document ['{filePath}'] contains following signatures.");
    foreach (var resSignature in result.Signatures)
    {
        Console.WriteLine($"Signature found at page {resSignature.PageNumber} with type {resSignature.SignatureType} and Id#: {resSignature.SignatureId}");
    }
}
else
{
    Helper.WriteError("No one signature was found.");
}
```

## Conclusion
In this tutorial, we learned how to search for multiple signatures within a document using GroupDocs.Signature for .NET. By following the provided steps, you can efficiently locate various types of signatures in your documents, enhancing document security and integrity.
## FAQ's
### Can I search for signatures in different document formats?
Yes, GroupDocs.Signature for .NET supports a wide range of document formats including Word, PDF, Excel, and more.
### Is it possible to customize search criteria for signatures?
Absolutely, you can tailor search criteria according to your requirements, such as specifying exact text matches or searching across all pages.
### Does GroupDocs.Signature for .NET offer support for digital signatures?
Yes, you can search for digital signatures as well as other types like text, barcode, and QR code signatures.
### Can I integrate signature searching functionality into my .NET applications easily?
Yes, GroupDocs.Signature for .NET provides a straightforward API that simplifies the integration process.
### Where can I find additional support or assistance?
You can visit the GroupDocs.Signature forum [here](https://forum.groupdocs.com/c/signature/13) for any queries or assistance.
