---
title: Sign PDF with Metadata
linktitle: Sign PDF with Metadata
second_title: GroupDocs.Signature .NET API
description: Learn how to sign PDF documents with metadata using GroupDocs.Signature for .NET. Enhance document traceability and authenticity easily.
weight: 11
url: /net/document-signing/sign-pdf-with-metadata/
---
## Introduction
In this tutorial, we'll learn how to sign a PDF document with metadata using GroupDocs.Signature for .NET. Adding metadata to a PDF can provide additional information about the document, such as authorship, creation date, document ID, and more.
## Prerequisites
Before we begin, make sure you have the following:
1. GroupDocs.Signature for .NET: You can download it from [here](https://releases.groupdocs.com/signature/net/).
2. A PDF Document: Have a sample PDF file ready for signing.
3. Basic Knowledge of C# Programming: Familiarity with C# syntax is required to understand the code examples.
## Import Namespaces
First, ensure you import the necessary namespaces to access the required classes and methods:
```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## Step 1: Load the PDF Document
Load the PDF document you want to sign:
```csharp
string filePath = "sample.pdf";
```
## Step 2: Specify Output File Path
Define the output file path where the signed PDF with metadata will be saved:
```csharp
string outputFilePath = Path.Combine("Your Document Directory", "SignPdfWithMetadata", "SignedWithMetadata.pdf");
```
## Step 3: Create Signature Instance
Initialize a Signature instance by providing the path to the PDF document:
```csharp
using (Signature signature = new Signature(filePath))
{
    // Signature related code will go here
}
```
## Step 4: Define Metadata Options
Create MetadataSignOptions and add metadata fields with their respective values:
```csharp
MetadataSignOptions options = new MetadataSignOptions();
options
    .Add(new PdfMetadataSignature("Author", "Mr.Sherlock Holmes")) // String value
    .Add(new PdfMetadataSignature("CreatedOn", DateTime.Now))       // DateTime values
    .Add(new PdfMetadataSignature("DocumentId", 123456))            // Integer value
    .Add(new PdfMetadataSignature("SignatureId", 123.456D))         // Double value
    .Add(new PdfMetadataSignature("Amount", 123.456M))              // Decimal value
    .Add(new PdfMetadataSignature("Total", 123.456F));              // Float value
```
## Step 5: Sign the Document
Sign the PDF document with the specified metadata options and save the signed document:
```csharp
SignResult result = signature.Sign(outputFilePath, options);
Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).\nFile saved at {outputFilePath}.");
```

## Conclusion
In this tutorial, we've covered how to sign a PDF document with metadata using GroupDocs.Signature for .NET. By following the step-by-step guide, you can easily add metadata information such as authorship, creation date, and more to your PDF files, enhancing their utility and traceability.
## FAQ's
### Can I add custom metadata fields to my PDF documents?
Yes, you can add custom metadata fields by specifying the field name and its corresponding value using GroupDocs.Signature for .NET.
### Is GroupDocs.Signature for .NET compatible with all versions of .NET Framework?
GroupDocs.Signature for .NET is compatible with various versions of .NET Framework, ensuring flexibility and ease of integration.
### Does GroupDocs.Signature support signing other document formats apart from PDF?
Yes, GroupDocs.Signature supports a wide range of document formats, including Word, Excel, PowerPoint, and more.
### Can I sign multiple documents in bulk using GroupDocs.Signature for .NET?
Yes, you can sign multiple documents in bulk by iterating through a list of files and applying the signature process programmatically.
### Is technical support available for GroupDocs.Signature users?
Yes, GroupDocs provides dedicated technical support through its forums. You can access the support forum [here](https://forum.groupdocs.com/c/signature/13).
