---
title: Sign Image with Metadata
linktitle: Sign Image with Metadata
second_title: GroupDocs.Signature .NET API
description: Learn how to sign images with metadata in .NET using GroupDocs.Signature. Easy, efficient, and customizable metadata signing solution.
weight: 10
url: /net/document-signing/sign-image-with-metadata/
---

# Sign Image with Metadata

## Introduction
GroupDocs.Signature for .NET enables developers to sign images with metadata efficiently. This tutorial guides you through the process step by step.
## Prerequisites
Before you begin, make sure you have the following:
1. GroupDocs.Signature for .NET: Install the GroupDocs.Signature package in your .NET project. You can download it from [here](https://releases.groupdocs.com/signature/net/).   
2. Image File: Prepare the image file that you want to sign with metadata.

## Import Namespaces
Make sure to import the necessary namespaces in your C# code:
```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## Step 1: Load Image File
First, specify the path to your image file and the output directory for the signed image with metadata:
```csharp
string filePath = "sample.png";            
string outputFilePath = Path.Combine("Your Document Directory", "SignImageWithMetadata", "SignedWithMetadata.png");
```
## Step 2: Create Metadata Signatures
Next, create different metadata signatures and add them to the options signature collection:
```csharp
using (Signature signature = new Signature(filePath))
{
    ushort imgsMetadataId = 41996;
    MetadataSignOptions options = new MetadataSignOptions();
    options
        .Add(new ImageMetadataSignature(imgsMetadataId++, "Mr.Scherlock Holmes")) // String value
        .Add(new ImageMetadataSignature(imgsMetadataId++, DateTime.Now))          // Date Time value
        .Add(new ImageMetadataSignature(imgsMetadataId++, 123456))                // Integer value
        .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456D))              // Double value
        .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456M))              // Decimal value
        .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456F));             // Float value
    
    // sign document to file
    SignResult result = signature.Sign(outputFilePath, options);
    Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).\nFile saved at {outputFilePath}.");
}
```

## Conclusion
In this tutorial, you learned how to sign an image with metadata using GroupDocs.Signature for .NET. By following these steps, you can easily incorporate metadata signatures into your .NET applications.

## FAQ's
### Can I sign multiple images with metadata using GroupDocs.Signature for .NET?
Yes, you can sign multiple images with metadata by iterating through each image file and applying the metadata signatures.
### Is there a trial version available for GroupDocs.Signature for .NET?
Yes, you can download the trial version from [here](https://releases.groupdocs.com/).
### Does GroupDocs.Signature for .NET support other file formats besides images?
Yes, GroupDocs.Signature supports various file formats, including PDF, Word, Excel, and more.
### Can I customize the appearance of the metadata signature?
Yes, you can customize the appearance of the metadata signature, such as font size, color, and position.
### Where can I get support for GroupDocs.Signature for .NET?
You can get support from the GroupDocs.Signature forum [here](https://forum.groupdocs.com/c/signature/13).
