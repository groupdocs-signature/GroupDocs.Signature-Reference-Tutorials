---
title: Signing Documents with QR Code using GroupDocs.Signature
linktitle: Signing with QR Code
second_title: GroupDocs.Signature .NET API
description: Learn how to add QR code signatures to your documents with GroupDocs.Signature for .NET. Enhance security and authentication effortlessly.
weight: 15
url: /net/advanced-signature-techniques/sign-with-qr-code/
---

# Signing Documents with QR Code using GroupDocs.Signature

## Introduction
In this tutorial, we'll walk through the process of signing documents with a QR code using GroupDocs.Signature for .NET. GroupDocs.Signature for .NET is a powerful API that allows developers to add various types of signatures to digital documents programmatically. Signing documents with QR codes can provide an additional layer of security and authentication to your documents.
## Prerequisites
Before we begin, make sure you have the following prerequisites installed:
1. GroupDocs.Signature for .NET: You can download the library from the [website](https://releases.groupdocs.com/signature/net/).
2. Development Environment: Ensure you have a .NET development environment set up on your machine.
3. Sample Document: Prepare a sample document (e.g., PDF) that you want to sign with a QR code.

## Importing Necessary Namespaces
Before diving into the code, let's import the necessary namespaces:
```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

## Step 1: Define File Paths
```csharp
string filePath = "sample.pdf";
string fileName = Path.GetFileName(filePath);
string outputFilePath = Path.Combine("Your Document Directory", "SignWithQRCode", fileName);
```
Ensure to replace `"Your Document Directory"` with the path to the directory where you want to save the signed document.
## Step 2: Initialize Signature Object
```csharp
using (Signature signature = new Signature(filePath))
{
    // Code for signing goes here
}
```
Initialize a `Signature` object with the path to the document you want to sign.
## Step 3: Create QRCodeSignOptions
```csharp
QrCodeSignOptions options = new QrCodeSignOptions("JohnSmith")
{
    EncodeType = QrCodeTypes.QR,
    Left = 50,
    Top = 150,
    Width = 200,
    Height = 200
};
```
Create a `QrCodeSignOptions` object with the desired settings for the QR code signature. You can customize parameters such as the text to encode, position, and dimensions of the QR code.
## Step 4: Sign the Document
```csharp
SignResult result = signature.Sign(outputFilePath, options);
```
Use the `Sign` method of the `Signature` object to sign the document with the specified options. This method returns a `SignResult` object containing information about the signing process.
## Step 5: Display Result
```csharp
Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).\nFile saved at {outputFilePath}.");
```
Display a message indicating the success of the signing process and the location where the signed document is saved.

## Conclusion
In this tutorial, we've learned how to sign documents with a QR code using GroupDocs.Signature for .NET. By following these simple steps, you can add QR code signatures to your digital documents, enhancing security and authentication.

## FAQ's
### Can I customize the appearance of the QR code?
Yes, you can customize various parameters such as size, position, and encoding type of the QR code according to your requirements.
### Which document formats are supported for signing with QR codes?
GroupDocs.Signature for .NET supports a wide range of document formats, including PDF, Word, Excel, PowerPoint, and more.
### Is it possible to sign multiple documents in a batch process?
Absolutely, you can use GroupDocs.Signature for .NET to sign multiple documents simultaneously, streamlining your workflow.
### Can I verify the authenticity of a document signed with a QR code?
Yes, GroupDocs.Signature for .NET provides verification mechanisms to ensure the integrity and authenticity of signed documents.
### Is there a trial version available to test the functionality before purchasing?
Yes, you can download a free trial version from the [website](https://releases.groupdocs.com/) to evaluate the features and capabilities of GroupDocs.Signature for .NET.
