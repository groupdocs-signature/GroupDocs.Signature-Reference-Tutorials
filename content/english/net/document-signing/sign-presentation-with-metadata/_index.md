---
title: Sign Presentation with Metadata
linktitle: Sign Presentation with Metadata
second_title: GroupDocs.Signature .NET API
description: Learn how to sign presentation files with metadata using GroupDocs.Signature for .NET. Enhance document integrity and add valuable information.
weight: 12
url: /net/document-signing/sign-presentation-with-metadata/
---
## Introduction
In this tutorial, we will learn how to sign a presentation file (PPTX) with metadata using the GroupDocs.Signature for .NET library. Signing presentations with metadata adds valuable information to the document, such as the author's name, creation date, document ID, signature ID, and various numerical values.
## Prerequisites
Before we begin, make sure you have the following:
1. GroupDocs.Signature for .NET Library: Download and install the library from [here](https://releases.groupdocs.com/signature/net/).
2. Development Environment: Ensure you have a .NET development environment set up.
3. Presentation File: Have a sample presentation file (PPTX format) ready for signing.
4. Basic Understanding of C#: Familiarity with C# programming language will be beneficial.

## Import Namespaces
Before diving into the code, let's import the necessary namespaces:
```csharp
using System;
using System.IO;
    using GroupDocs.Signature;
    using GroupDocs.Signature.Domain;
    using GroupDocs.Signature.Options;
```
## Step 1: Load Presentation File
```csharp
string filePath = "sample.pptx";
```
Replace `"sample.pptx"` with the path to your presentation file.
## Step 2: Specify Output File Path
```csharp
string outputFilePath = Path.Combine("Your Document Directory", "SignPresentationWithMetadata", "SignedWithMetadata.pptx");
```
Specify the directory where you want to save the signed presentation file along with the filename.
## Step 3: Initialize Signature Object
```csharp
using (Signature signature = new Signature(filePath))
```
Initialize a Signature object by providing the path to the presentation file.
## Step 4: Define Metadata Sign Options
```csharp
MetadataSignOptions options = new MetadataSignOptions();
```
Create an instance of MetadataSignOptions to define metadata signing options.
## Step 5: Create Metadata Signatures
```csharp
PresentationMetadataSignature[] signatures = new PresentationMetadataSignature[]
{
    new PresentationMetadataSignature("Author", "Mr.Scherlock Holmes"),
    new PresentationMetadataSignature("CreatedOn", DateTime.Now),
    new PresentationMetadataSignature("DocumentId", 123456),
    new PresentationMetadataSignature("SignatureId", 123.456D),
    new PresentationMetadataSignature("Amount", 123.456M),
    new PresentationMetadataSignature("Total", 123.456F)
};
```
Create an array of PresentationMetadataSignature objects, each representing a metadata signature. You can add various types of metadata, including string, DateTime, integer, double, decimal, and float.
## Step 6: Add Signatures to Options
```csharp
options.Signatures.AddRange(signatures);
```
Add the created metadata signatures to the MetadataSignOptions object.
## Step 7: Sign Document
```csharp
SignResult result = signature.Sign(outputFilePath, options);
```
Sign the presentation file with metadata using the specified options and save the signed file to the output path.
## Step 8: Display Result
```csharp
Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).\nFile saved at {outputFilePath}.");
```
Display a success message along with the number of signatures applied and the path where the signed file is saved.

## Conclusion
In this tutorial, we've learned how to sign a presentation file with metadata using the GroupDocs.Signature for .NET library. Adding metadata signatures enhances the document's integrity and provides valuable information about its content.

## FAQ's
### Can I sign other document formats besides PPTX with metadata using GroupDocs.Signature for .NET?
Yes, GroupDocs.Signature supports various document formats, including Word, Excel, PDF, and more, for signing with metadata.
### Is GroupDocs.Signature for .NET compatible with .NET Core?
Yes, the library is compatible with both .NET Framework and .NET Core.
### Can I customize the appearance of metadata signatures?
Yes, you can customize the appearance, position, and other properties of metadata signatures according to your requirements.
### Does GroupDocs.Signature for .NET provide encryption for signed documents?
Yes, GroupDocs.Signature offers encryption options to secure signed documents from unauthorized access.
### Is there a trial version available for testing before purchasing?
Yes, you can avail of a free trial of GroupDocs.Signature for .NET from [here](https://releases.groupdocs.com/).
