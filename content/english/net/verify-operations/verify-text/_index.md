---
title: Verify Text
linktitle: Verify Text
second_title: GroupDocs.Signature .NET API
description: Learn how to verify text in documents using GroupDocs.Signature for .NET. Follow our step-by-step tutorial for seamless integration.
weight: 13
url: /net/verify-operations/verify-text/
---

# Verify Text

## Introduction
In this tutorial, we'll guide you through the process of verifying text in documents using GroupDocs.Signature for .NET. This powerful library allows you to seamlessly integrate text verification functionality into your .NET applications, ensuring the integrity and authenticity of your documents.
## Prerequisites
Before we get started, make sure you have the following prerequisites:
1. GroupDocs.Signature for .NET: Ensure you have installed and configured GroupDocs.Signature for .NET. You can download the library from [here](https://releases.groupdocs.com/signature/net/).
2. Document File: Prepare the document file (e.g., sample_multiple_signatures.docx) that you want to verify.

## Import Namespaces
Firstly, you need to import the necessary namespaces into your project:
```csharp
using System;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## Step 1: Set Document File Path
Define the file path of the document you want to verify. Replace `"sample_multiple_signatures.docx"` with the path to your document file.
```csharp
string filePath = "sample_multiple_signatures.docx";
```
## Step 2: Initialize Signature Object
Create an instance of the `Signature` class and pass the file path to its constructor.
```csharp
using (Signature signature = new Signature(filePath))
{
    // Verification code will be written here
}
```
## Step 3: Specify Text Verification Options
Define the text verification options including the text to be verified, match type, and other parameters.
```csharp
TextVerifyOptions options = new TextVerifyOptions()
{
    AllPages = true, // Verify text on all pages
    SignatureImplementation = TextSignatureImplementation.Native,
    Text = "signature", // Text to be verified
    MatchType = TextMatchType.Contains // Specify match type
};
```
## Step 4: Verify Document Signatures
Invoke the `Verify` method on the `Signature` object and pass the verification options.
```csharp
VerificationResult result = signature.Verify(options);
```
## Step 5: Handle Verification Result
Check the validity of the verification result and process accordingly.
```csharp
if(result.IsValid)
{
    Console.WriteLine($"\nDocument {filePath} was verified successfully!");
    foreach (TextSignature item in result.Succeeded)
    {
        Console.WriteLine($"\nValid signature is found with text: {item.Text}");
    }
}
else
{
    Helper.WriteError($"\nDocument {filePath} failed verification process.");
}
```

## Conclusion
In conclusion, GroupDocs.Signature for .NET provides a seamless way to verify text in documents, ensuring document integrity and authenticity. By following the steps outlined in this tutorial, you can easily integrate text verification functionality into your .NET applications.
## FAQ's
### Is GroupDocs.Signature for .NET compatible with all document formats?
Yes, GroupDocs.Signature for .NET supports a wide range of document formats including DOCX, PDF, XLSX, and more.
### Can I customize the text verification criteria?
Absolutely, you can customize various parameters such as match type, page range, and more to suit your verification requirements.
### Does GroupDocs.Signature for .NET provide support for digital signatures?
Yes, GroupDocs.Signature for .NET supports both text and digital signatures, providing comprehensive document verification capabilities.
### Is there a free trial available for GroupDocs.Signature for .NET?
Yes, you can avail of a free trial from [here](https://releases.groupdocs.com/).
### Where can I get help or support for GroupDocs.Signature for .NET?
You can visit the [GroupDocs.Signature forum](https://forum.groupdocs.com/c/signature/13) for assistance and support from the community.
