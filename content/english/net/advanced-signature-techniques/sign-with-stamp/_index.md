---
title: Signing with Stamp using GroupDocs.Signature
linktitle: Signing with Stamp
second_title: GroupDocs.Signature .NET API
description: Learn how to add stamp signatures to your .NET documents easily with GroupDocs.Signature for .NET. Enhance document security.
weight: 16
url: /net/advanced-signature-techniques/sign-with-stamp/
---

# Signing with Stamp using GroupDocs.Signature

## Introduction
In this tutorial, we'll walk you through the process of signing a document with a stamp using GroupDocs.Signature for .NET. By following these step-by-step instructions, you'll be able to add a stamp signature to your documents with ease.
## Prerequisites
Before we begin, ensure you have the following prerequisites:
1. GroupDocs.Signature for .NET SDK: Download and install the SDK from the [website](https://releases.groupdocs.com/signature/net/).
2. Development Environment: Make sure you have a suitable development environment set up for .NET development.
3. Document to Sign: Prepare the document (e.g., PDF) that you want to sign with a stamp.

## Importing Namespaces
Start by importing the necessary namespaces into your project:
```csharp
using System;
using System.IO;
using System.Drawing;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## Step 1: Load the Document
```csharp
string filePath = "sample.pdf";
using (Signature signature = new Signature(filePath))
{
    // Your code goes here
}
```
## Step 2: Set Stamp Sign Options
```csharp
StampSignOptions options = new StampSignOptions()
{
    Left = 50,
    Top = 150,                    
    Width = 200,
    Height = 200
};
```
## Step 3: Configure Stamp Appearance
```csharp
StampLine outerLine = new StampLine();
outerLine.Text = " * European Union ";
outerLine.TextRepeatType = StampTextRepeatType.FullTextRepeat;
outerLine.Font.Size = 12;
outerLine.Height = 22;
outerLine.TextBottomIntent = 6;
outerLine.TextColor = Color.WhiteSmoke;
outerLine.BackgroundColor = Color.DarkSlateBlue;
options.OuterLines.Add(outerLine);
StampLine innerLine = new StampLine();
innerLine.Text = "John Smith";
innerLine.TextColor = Color.MediumVioletRed;
innerLine.Font.Size = 20;
innerLine.Font.Bold = true;
innerLine.Height = 40;
options.InnerLines.Add(innerLine);
```
## Step 4: Sign the Document
```csharp
string outputFilePath = Path.Combine("Your Document Directory", "SignWithStamp", fileName);
SignResult result = signature.Sign(outputFilePath, options);
Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).\nFile saved at {outputFilePath}.");
```

## Conclusion
Adding stamp signatures to your documents using GroupDocs.Signature for .NET is a straightforward process, as demonstrated in this tutorial. With the provided steps, you can easily enhance the security and authenticity of your documents.
## FAQ's
### Can I customize the appearance of the stamp signature?
Yes, you can customize various aspects such as text, font, color, and positioning of the stamp signature according to your requirements.
### Does GroupDocs.Signature support signing multiple document formats?
Yes, GroupDocs.Signature supports a wide range of document formats including PDF, Microsoft Word, Excel, PowerPoint, and more.
### Is there a trial version available for GroupDocs.Signature?
Yes, you can access the free trial version from the [website](https://releases.groupdocs.com/).
### Can I add multiple signatures to a single document?
Absolutely, GroupDocs.Signature allows you to add multiple signatures, including stamps, text, images, and digital signatures, to a single document.
### Where can I find support if I encounter any issues during implementation?
You can find support and assistance from the GroupDocs.Signature community forum [here](https://forum.groupdocs.com/c/signature/13).
