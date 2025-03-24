---
title: Signing with Text using GroupDocs.Signature for .NET
linktitle: Signing with Text
second_title: GroupDocs.Signature .NET API
description: Learn how to sign documents with text using GroupDocs.Signature for .NET. Step-by-step guide for adding text signatures programmatically.
weight: 17
url: /net/advanced-signature-techniques/sign-with-text/
---
## Introduction
In the digital age, signing documents electronically has become a standard practice, saving time and resources. GroupDocs.Signature for .NET offers a comprehensive solution for adding text signatures to various document formats programmatically. In this tutorial, we'll walk you through the process of signing a document with text using GroupDocs.Signature for .NET.
## Prerequisites
Before we dive into the tutorial, make sure you have the following prerequisites:
1. GroupDocs.Signature for .NET: Ensure you have the GroupDocs.Signature for .NET library installed. You can download it from [here](https://releases.groupdocs.com/signature/net/).
2. Development Environment: Have a working environment set up for .NET development.
3. Document: Prepare the document (e.g., PDF, Word) that you want to sign with text.

## Import Namespaces
First, you need to import the necessary namespaces into your .NET project to use GroupDocs.Signature functionalities.
```csharp
using System;
using System.IO;
using System.Drawing;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

Let's break down the process of signing a document with text into multiple steps:
## Step 1: Load Document
Load the document you want to sign with text.
```csharp
string filePath = "sample.pdf"; // Path to the document
string fileName = Path.GetFileName(filePath);
```
## Step 2: Set Output File Path
Define the output file path where the signed document will be saved.
```csharp
string outputFilePath = Path.Combine("Your Document Directory", "SignWithText", fileName);
```
## Step 3: Create Signature Options
Set up the options for text signature, including text content, position, size, color, and font.
```csharp
TextSignOptions options = new TextSignOptions("John Smith")
{
    Left = 50, // Set signature position
    Top = 200,
    Width = 100, // Set signature rectangle
    Height = 30,
    ForeColor = Color.Red, // Set text color
    Font = new SignatureFont { Size = 14, FamilyName = "Comic Sans MS" } // Set font
};
```
## Step 4: Sign Document
Use GroupDocs.Signature to sign the document with the specified options and save the signed document to the output file path.
```csharp
using (Signature signature = new Signature(filePath))
{
    SignResult result = signature.Sign(outputFilePath, options); // Sign document
    Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).\nFile saved at {outputFilePath}.");
}
```

## Conclusion
In this tutorial, we've learned how to sign a document with text using GroupDocs.Signature for .NET. By following these steps, you can efficiently add text signatures to your documents programmatically, enhancing security and authenticity.
## FAQ's
### Can I customize the appearance of the text signature?
Yes, you can customize various parameters such as color, font, size, and position of the text signature according to your ptutorialss.
### Is GroupDocs.Signature compatible with multiple document formats?
Yes, GroupDocs.Signature supports various document formats including PDF, Word, Excel, PowerPoint, and more.
### Can I add multiple text signatures to a single document?
Absolutely, you can add multiple text signatures to a document, each with its own set of customization options.
### Does GroupDocs.Signature ensure document integrity after signing?
Yes, GroupDocs.Signature employs robust cryptographic algorithms to ensure document integrity and prevent tampering after signing.
### Is there a trial version available for testing before purchasing?
Yes, you can download a free trial version from [here](https://releases.groupdocs.com/) to explore the features before making a purchase.
