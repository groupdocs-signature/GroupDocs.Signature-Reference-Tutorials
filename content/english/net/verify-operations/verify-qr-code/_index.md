---
title: Verify QR Code
linktitle: Verify QR Code
second_title: GroupDocs.Signature .NET API
description: Learn how to verify QR codes within documents using GroupDocs.Signature for .NET. Comprehensive tutorial with step-by-step guide.
type: docs
weight: 12
url: /net/verify-operations/verify-qr-code/
---
## Introduction
In the realm of document management and authentication, ensuring the integrity and validity of signatures is paramount. GroupDocs.Signature for .NET provides a comprehensive solution for verifying QR codes embedded within documents. In this tutorial, we'll delve into the step-by-step process of verifying QR codes using GroupDocs.Signature for .NET.
## Prerequisites
Before diving into the verification process, ensure that you have the following prerequisites in place:
1. Installation of GroupDocs.Signature for .NET: Download and install GroupDocs.Signature for .NET from the [download link](https://releases.groupdocs.com/signature/net/).
2. Access to a Document Containing QR Codes: Prepare a sample document that contains QR codes for verification. 

## Import Namespaces
Firstly, you need to import the necessary namespaces to utilize the functionalities provided by GroupDocs.Signature for .NET. Follow these steps:

```csharp
using System;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```


Now, let's break down the process of verifying QR codes embedded within a document using GroupDocs.Signature for .NET:
## Step 1: Specify Document Path
```csharp
string filePath = "sample_multiple_signatures.docx";
```
Ensure to replace `"sample_multiple_signatures.docx"` with the path to your document.
## Step 2: Initialize Signature Object
```csharp
using (Signature signature = new Signature(filePath))
{
    // Verification code goes here
}
```
Initialize a `Signature` object by providing the path to the document.
## Step 3: Specify Verification Options
```csharp
QrCodeVerifyOptions options = new QrCodeVerifyOptions()
{
    AllPages = true, // this value is set by default
    Text = "John",
    MatchType = TextMatchType.Contains
};
```
Define verification options such as `AllPages` to verify all pages, `Text` to specify the text to be matched within the QR code, and `MatchType` to define the matching criteria.
## Step 4: Verify Document Signatures
```csharp
VerificationResult result = signature.Verify(options);
```
Invoke the `Verify` method of the `Signature` object, passing the verification options.
## Step 5: Handle Verification Results
```csharp
if (result.IsValid)
{
    // Valid signature found
}
else
{
    // Invalid signature found
}
```
Based on the verification result, handle the success or failure scenarios accordingly.

## Conclusion
In this tutorial, we've explored the process of verifying QR codes within documents using GroupDocs.Signature for .NET. By following these steps, you can seamlessly integrate QR code verification functionality into your .NET applications, ensuring document integrity and authenticity.
## FAQ's
### Can GroupDocs.Signature for .NET verify QR codes across different document formats?
Yes, GroupDocs.Signature for .NET supports a wide range of document formats including DOCX, PDF, and more for QR code verification.
### Is there a free trial available for GroupDocs.Signature for .NET?
Yes, you can avail of a free trial from the [releases page](https://releases.groupdocs.com/).
### What support options are available for GroupDocs.Signature for .NET users?
Users can access support via the [forum](https://forum.groupdocs.com/c/signature/13) for GroupDocs.Signature.
### Can I purchase a temporary license for GroupDocs.Signature for .NET?
Yes, temporary licenses are available for purchase from the [GroupDocs purchase page](https://purchase.groupdocs.com/temporary-license/).
### Is there extensive documentation available for GroupDocs.Signature for .NET?
Absolutely, you can refer to the detailed documentation provided [here](https://reference.groupdocs.com/signature/net/) for comprehensive guidance on utilizing the functionalities of GroupDocs.Signature for .NET.
