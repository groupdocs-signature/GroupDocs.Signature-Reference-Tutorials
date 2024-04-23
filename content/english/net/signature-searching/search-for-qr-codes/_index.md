---
title: Search for QR Codes
linktitle: Search for QR Codes
second_title: GroupDocs.Signature .NET API
description: Learn how to search for QR codes within documents using GroupDocs.Signature for .NET. Enhance document security effortlessly.
type: docs
weight: 15
url: /net/signature-searching/search-for-qr-codes/
---
## Introduction

In the digital age, ensuring the authenticity and integrity of documents is paramount. GroupDocs.Signature for .NET empowers developers to integrate advanced signature features seamlessly into their .NET applications. This comprehensive guide will walk you through the process of leveraging GroupDocs.Signature for .NET to search for QR codes within documents. By the end, you'll have a solid understanding of how to harness this powerful tool to enhance document security and efficiency.

## Prerequisites

Before diving into the tutorial, ensure you have the following prerequisites:

1. GroupDocs.Signature for .NET SDK: Download and install the SDK from the [download page](https://releases.groupdocs.com/signature/net/).
2. Development Environment: Set up a .NET development environment, such as Visual Studio, with .NET Framework or .NET Core installed.

## Import Namespaces

To begin, import the necessary namespaces into your project:

```csharp
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
using System;
using System.Collections.Generic;
```

Let's break down the example into multiple steps:

## Step 1: Define File Path

```csharp
string filePath = "sample_multiple_signatures.docx";
```

In this step, we specify the file path of the document containing the QR codes you want to search for. Ensure the file path is correct and accessible within your application.

## Step 2: Initialize Signature Object

```csharp
using (Signature signature = new Signature(filePath))
{
    // Your code here
}
```

Here, we initialize a `Signature` object, passing the file path of the document as a parameter. The `using` statement ensures proper disposal of resources after use.

## Step 3: Search for Signatures

```csharp
List<QrCodeSignature> signatures = signature.Search<QrCodeSignature>(SignatureType.QrCode);
```

This step involves searching for QR code signatures within the document using the `Search` method of the `Signature` object. We specify the signature type as `QrCodeSignature` and retrieve the results in a list.

## Step 4: Iterate Through Results

```csharp
foreach (var qrCodeSignature in signatures)
{
    Console.WriteLine($"QRCode signature found at page {qrCodeSignature.PageNumber} with type {qrCodeSignature.EncodeType.TypeName} and text {qrCodeSignature.Text}");
}
```

In this final step, we iterate through the list of QR code signatures found in the document. For each signature found, we print relevant information such as page number, encode type, and text associated with the QR code.

## Conclusion

GroupDocs.Signature for .NET offers a robust solution for integrating signature functionality into your .NET applications. By following this guide, you've learned how to search for QR codes within documents with ease, enhancing document security and productivity.

## FAQ's

### Q: Can GroupDocs.Signature for .NET handle other signature types besides QR codes?
A: Yes, GroupDocs.Signature for .NET supports various signature types, including digital signatures, barcode signatures, and more.

### Q: Is there a trial version available for GroupDocs.Signature for .NET?
A: Yes, you can access a free trial of GroupDocs.Signature for .NET from the [releases page](https://releases.groupdocs.com/).

### Q: How can I obtain support for GroupDocs.Signature for .NET?
A: You can seek assistance and engage with the community on the [GroupDocs.Signature forum](https://forum.groupdocs.com/c/signature/13).

### Q: Are temporary licenses available for GroupDocs.Signature for .NET?
A: Yes, you can acquire temporary licenses from the [purchase page](https://purchase.groupdocs.com/temporary-license/) for testing and evaluation purposes.

### Q: Where can I purchase a license for GroupDocs.Signature for .NET?
A: You can purchase licenses for GroupDocs.Signature for .NET from the [purchase page](https://purchase.groupdocs.com/buy).
