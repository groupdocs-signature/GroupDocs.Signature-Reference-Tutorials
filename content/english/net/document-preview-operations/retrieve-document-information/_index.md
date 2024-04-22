---
title: Retrieve Document Information
linktitle: Retrieve Document Information
second_title: GroupDocs.Signature .NET API
description: Enhance document management in .NET with GroupDocs.Signature. Retrieve document info step-by-step. Supports various formats.
type: docs
weight: 11
url: /net/document-preview-operations/retrieve-document-information/
---
## Introduction
In the realm of digital documentation, ensuring authenticity and integrity is paramount. GroupDocs.Signature for .NET provides a robust solution for managing document signatures within the .NET environment. In this tutorial, we delve into the process of retrieving document information using GroupDocs.Signature for .NET, breaking down each step for a comprehensive understanding.
## Prerequisites
Before diving into the tutorial, ensure you have the following prerequisites in place:
1. Installation: Install GroupDocs.Signature for .NET by downloading it from [here](https://releases.groupdocs.com/signature/net/).
2. .NET Environment: Have a working knowledge of the .NET framework.
3. Document: Prepare a sample document (e.g., "sample_multiple_signatures.docx") for testing purposes.

## Importing Namespaces
Before proceeding with the document signature retrieval process, import the necessary namespaces:
```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
```

## Step 1: Set Document File Path:
Define the file path for the document you intend to retrieve information from.
```csharp
string filePath = "sample_multiple_signatures.docx";
```
## Step 2: Instantiate Signature Object:
Create an instance of the `Signature` class by passing the document file path.
```csharp
using (Signature signature = new Signature(filePath))
{

}
```
## Step 3: Retrieve Document Information:
Utilize the `GetDocumentInfo()` method to fetch comprehensive information about the document.
```csharp
IDocumentInfo documentInfo = signature.GetDocumentInfo();
```
## Step 4: Display Document Properties:
Output various properties of the document such as format, extension, size, page count, etc.
```csharp
Console.WriteLine($"Document properties {Path.GetFileName(filePath)}:");
Console.WriteLine($" - format : {documentInfo.FileType.FileFormat}");
Console.WriteLine($" - extension : {documentInfo.FileType.Extension}");
Console.WriteLine($" - size : {documentInfo.Size}");
Console.WriteLine($" - page count : {documentInfo.PageCount}");
Console.WriteLine($" - Form Fields count : {documentInfo.FormFields.Count}");
Console.WriteLine($" - Text signatures count : {documentInfo.TextSignatures.Count}");
Console.WriteLine($" - Image signatures count : {documentInfo.ImageSignatures.Count}");
Console.WriteLine($" - Digital signatures count : {documentInfo.DigitalSignatures.Count}");
Console.WriteLine($" - Barcode signatures count : {documentInfo.BarcodeSignatures.Count}");
Console.WriteLine($" - QrCode signatures count : {documentInfo.QrCodeSignatures.Count}");
Console.WriteLine($" - FormField signatures count : {documentInfo.FormFieldSignatures.Count}");
foreach (PageInfo pageInfo in documentInfo.Pages)
{
   Console.WriteLine($" - page-{pageInfo.PageNumber} Width {pageInfo.Width}, Height {pageInfo.Height}");
}
```


## Conclusion
GroupDocs.Signature for .NET offers a powerful suite of tools for managing document signatures seamlessly within the .NET framework. By following the steps outlined in this guide, you can efficiently retrieve comprehensive information about your documents, facilitating enhanced document management capabilities.

## FAQ's
### Can GroupDocs.Signature for .NET handle multiple document formats?
Yes, GroupDocs.Signature supports a wide range of document formats, including but not limited to DOCX, PDF, PNG, and JPEG.
### Is there a trial version available for GroupDocs.Signature for .NET?
Yes, you can access the trial version from [here](https://releases.groupdocs.com/).
### Does GroupDocs.Signature for .NET provide support for digital signatures?
Absolutely, GroupDocs.Signature offers robust support for digital signatures, ensuring document authenticity and integrity.
### Where can I find additional documentation and support for GroupDocs.Signature for .NET?
You can refer to the comprehensive documentation [here](https://reference.groupdocs.com/signature/net/), and for support, visit the GroupDocs forum [here](https://forum.groupdocs.com/c/signature/13).
### Can temporary licenses be obtained for GroupDocs.Signature for .NET?
Yes, temporary licenses are available for purchase [here](https://purchase.groupdocs.com/temporary-license/).
