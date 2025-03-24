---
title: Search for Digital Signatures
linktitle: Search for Digital Signatures
second_title: GroupDocs.Signature .NET API
description: Learn how to search for digital signatures in documents using GroupDocs.Signature for .NET. Enhance document security and integrity with this comprehensive.
weight: 11
url: /net/signature-searching/search-for-digital-signatures/
---
## Introduction
In the digital age, ensuring the authenticity and integrity of documents is paramount. Digital signatures play a pivotal role in this process, providing a secure way to sign and verify electronic documents. GroupDocs.Signature for .NET offers a comprehensive solution for working with digital signatures in .NET applications. In this tutorial, we'll delve into the fundamentals of using GroupDocs.Signature for .NET to search for digital signatures within documents.
## Prerequisites
Before we begin, make sure you have the following prerequisites:
1. GroupDocs.Signature for .NET: Ensure that you have installed GroupDocs.Signature for .NET. You can download the library from [here](https://releases.groupdocs.com/signature/net/).
   
2. Development Environment: Set up your development environment with the necessary tools for .NET development.
   
3. Sample Document: Prepare a sample document (e.g., "sample_multiple_signatures.docx") containing digital signatures for testing purposes.

## Import Namespaces
First, import the necessary namespaces to access the functionality provided by GroupDocs.Signature for .NET.

```csharp
using System;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

Now, let's dive into the process of searching for digital signatures within a document using GroupDocs.Signature for .NET.
## Step 1: Initialize Signature Object
```csharp
string filePath = "sample_multiple_signatures.docx";
using (Signature signature = new Signature(filePath))
{
```
## Step 2: Search for Signatures
```csharp
	// search for signatures in document
	List<DigitalSignature> signatures = signature.Search<DigitalSignature>(SignatureType.Digital);
```
## Step 3: Display Results
```csharp
	Console.WriteLine($"\nSource document ['{filePath}'] contains the following signatures.");
	foreach (var digitalSignature in signatures)
	{
		Console.WriteLine($"Digital signature found from {digitalSignature.SignTime} with validation flag {digitalSignature.IsValid}. Certificate SN {digitalSignature.Certificate?.SerialNumber}");
	}
}
```

## Conclusion
GroupDocs.Signature for .NET provides a robust framework for working with digital signatures in .NET applications. By following this tutorial, you've learned how to search for digital signatures within documents, enhancing document security and integrity.
## FAQ's
### Can I use GroupDocs.Signature for .NET with other document formats besides DOCX?
Yes, GroupDocs.Signature for .NET supports various document formats, including PDF, XLSX, PPTX, and more.
### Is there a free trial available for GroupDocs.Signature for .NET?
Yes, you can access a free trial of GroupDocs.Signature for .NET from [here](https://releases.groupdocs.com/).
### Where can I find documentation for GroupDocs.Signature for .NET?
You can find detailed documentation for GroupDocs.Signature for .NET [here](https://tutorials.groupdocs.com/signature/net/).
### How can I get temporary licenses for GroupDocs.Signature for .NET?
Temporary licenses for GroupDocs.Signature for .NET can be obtained [here](https://purchase.groupdocs.com/temporary-license/).
### Where can I seek support for GroupDocs.Signature for .NET?
For support related to GroupDocs.Signature for .NET, visit the [GroupDocs forum](https://forum.groupdocs.com/c/signature/13).
