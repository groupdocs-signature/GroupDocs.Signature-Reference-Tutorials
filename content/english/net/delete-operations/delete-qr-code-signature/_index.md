---
title: Delete QR Code Signature from Document
linktitle: Delete QR Code Signature from Document
second_title: GroupDocs.Signature .NET API
description: Learn how to delete QR code signatures from documents using GroupDocs.Signature for .NET. Follow our step-by-step guide for efficient signature management.
weight: 16
url: /net/delete-operations/delete-qr-code-signature/
---
## Introduction
In this tutorial, we'll guide you through the process of removing a QR code signature from a document using GroupDocs.Signature for .NET. Follow these step-by-step instructions to effectively delete QR code signatures.
## Prerequisites
Before you begin, ensure you have the following prerequisites:
- GroupDocs.Signature for .NET: Make sure you have the GroupDocs.Signature library installed in your .NET project. You can download it from [here](https://releases.groupdocs.com/signature/net/).
- Document with QR Code Signature: Prepare a document containing QR code signatures that you want to delete.
- Basic Knowledge of C#: Familiarize yourself with C# programming language basics.

## Importing Namespaces
Before diving into the code, import the necessary namespaces to your C# file:
```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## Step 1: Define File Paths
```csharp
// The path to the documents directory.
string filePath = "sample_multiple_signatures.docx";
string fileName = Path.GetFileName(filePath);
// Define the output file path for the modified document.
string outputFilePath = Path.Combine("Your Document Directory", "DeleteQRCode", fileName);
// Copy the source file since the Delete method works with the same Document.
File.Copy(filePath, outputFilePath, true);
```
## Step 2: Initialize Signature Object
```csharp
using (Signature signature = new Signature(outputFilePath))
{
    // Create options for searching QR code signatures.
    QrCodeSearchOptions options = new QrCodeSearchOptions();
    // Search for QR code signatures in the document.
    List<QrCodeSignature> signatures = signature.Search<QrCodeSignature>(options);
```
## Step 3: Check for Existence of QR Code Signature
```csharp
    if (signatures.Count > 0)
    {
        // Get the first QR code signature found in the document.
        QrCodeSignature qrCodeSignature = signatures[0];
```
## Step 4: Delete QR Code Signature
```csharp
        // Delete the QR code signature from the document.
        bool result = signature.Delete(qrCodeSignature);
        if (result)
        {
            Console.WriteLine($"Signature with QR-Code '{qrCodeSignature.Text}' and encode type '{qrCodeSignature.EncodeType.TypeName}' was deleted from document ['{fileName}'].");
        }
        else
        {
            Helper.WriteError($"Signature was not deleted from the document! Signature with Barcode '{qrCodeSignature.Text}' and encode type '{qrCodeSignature.EncodeType.TypeName}' was not found!");
        }
    }
}
```
Congratulations! You've successfully removed the QR code signature from the document using GroupDocs.Signature for .NET.

## Conclusion
In this tutorial, we learned how to delete a QR code signature from a document using GroupDocs.Signature for .NET. By following the provided steps, you can efficiently manage and manipulate signatures within your .NET applications.
## FAQ's
### Can I delete multiple QR code signatures from a document?
Yes, you can modify the code to iterate through all QR code signatures and delete them accordingly.
### Does GroupDocs.Signature support other types of signatures besides QR codes?
Yes, GroupDocs.Signature supports various signature types such as text, image, barcode, and more.
### Is GroupDocs.Signature compatible with all document formats?
GroupDocs.Signature supports a wide range of document formats including PDF, Microsoft Word, Excel, PowerPoint, and more.
### Can I customize the search options for signatures?
Yes, you can tailor the search options according to your requirements to locate specific signatures within the document.
### Is there a trial version available for GroupDocs.Signature?
Yes, you can access a free trial version of GroupDocs.Signature from [here](https://releases.groupdocs.com/).
