---
title: Signing with Multiple Options
linktitle: Signing with Multiple Options
second_title: GroupDocs.Signature .NET API
description: Learn how to sign documents with multiple options using GroupDocs.Signature for .NET. Enhance document security with text, barcode, QR code, digital and image.
type: docs
weight: 14
url: /net/advanced-signature-techniques/sign-with-multiple-options/
---
## Introduction
In this tutorial, we'll explore how to sign a document using multiple signature options using the GroupDocs.Signature library for .NET. Signing documents with various options like text, barcode, QR code, digital, image, and metadata signatures can provide versatility and enhance document security.
## Prerequisites
Before getting started, ensure you have the following prerequisites:
1. GroupDocs.Signature for .NET Library: Download and install the GroupDocs.Signature for .NET library from [here](https://releases.groupdocs.com/signature/net/).
2. Development Environment: Set up a development environment with .NET Framework installed.
3. Document to Sign: Prepare the document (e.g., sample.docx) that you want to sign.
4. Certificates and Images: Prepare any required certificates and images for digital and image signatures.

## Import Namespaces
First, import the necessary namespaces to use the GroupDocs.Signature library in your .NET application:
```csharp
using System;
using System.IO;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## Step 1: Load the Document
```csharp
string filePath = "sample.docx";
string outputFilePath = Path.Combine("Your Document Directory", "SignWithMultiple", "SignWithMultiple.docx");
using (Signature signature = new Signature(filePath))
{
    // Your code continues...
}
```
## Step 2: Define Signature Options
Define several signature options of different types and settings, such as text, barcode, QR code, digital, image, and metadata signatures:
```csharp
TextSignOptions textOptions = new TextSignOptions("Text signature")
{
    VerticalAlignment = VerticalAlignment.Top,
    HorizontalAlignment = HorizontalAlignment.Left
};
BarcodeSignOptions barcodeOptions = new BarcodeSignOptions("123456")
{
    EncodeType = BarcodeTypes.Code128,
    Left = 0,
    Top = 150,
    Height = 50,
    Width = 200
};
// Define other signature options (e.g., QR code, digital, image, metadata)...
```
## Step 3: Create a List of Signature Options
Define a list of signature options containing all the previously defined options:
```csharp
List<SignOptions> listOptions = new List<SignOptions>();
listOptions.Add(textOptions);
listOptions.Add(barcodeOptions);
// Add other signature options to the list...
```
## Step 4: Sign the Document
Sign the document with the list of signature options and save the signed document:
```csharp
SignResult result = signature.Sign(outputFilePath, listOptions);
Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).\nFile saved at {outputFilePath}.");
```

## Conclusion
Signing documents with multiple options using GroupDocs.Signature for .NET provides a robust solution for enhancing document security and versatility. By following the steps outlined in this tutorial, you can seamlessly integrate various signature types into your .NET applications.
## FAQ's
### Can I use custom images for digital signatures?
Yes, you can specify custom images for digital signatures using the GroupDocs.Signature library.
### Is GroupDocs.Signature compatible with different document formats?
Yes, GroupDocs.Signature supports various document formats, including DOCX, PDF, PPTX, and more.
### Can I customize the appearance of text signatures?
Absolutely, you can customize the appearance of text signatures, including font size, color, and style.
### Does GroupDocs.Signature provide encryption for digital signatures?
Yes, GroupDocs.Signature offers encryption options for digital signatures to ensure document security.
### Is there a trial version available for GroupDocs.Signature for .NET?
Yes, you can download a free trial version of GroupDocs.Signature for .NET from [here](https://releases.groupdocs.com/).
