---
title: Delete Signature by Type
linktitle: Delete Signature by Type
second_title: GroupDocs.Signature .NET API
description: Learn how to delete signatures by type in .NET documents effortlessly using GroupDocs.Signature, enhancing document management efficiency.
weight: 12
url: /net/delete-operations/delete-signature-by-type/
---
## Introduction
In today's digital age, the need for efficient document management is paramount. Whether you're a business professional handling contracts or an individual processing legal documents, ensuring the authenticity and integrity of your files is crucial. GroupDocs.Signature for .NET offers a powerful solution to manage signatures within your documents seamlessly. In this tutorial, we'll delve into the process of deleting signatures by type using GroupDocs.Signature for .NET, providing you with a step-by-step guide to streamline your document management tasks.
## Prerequisites
Before we begin, ensure you have the following prerequisites in place:
- Basic knowledge of C# programming language.
- GroupDocs.Signature for .NET installed in your development environment. You can download it from [here](https://releases.groupdocs.com/signature/net/).
- An Integrated Development Environment (IDE) such as Visual Studio installed on your system.
- Sample document(s) containing signatures for demonstration purposes.
## Import Namespaces
To start with, make sure to import the necessary namespaces into your project. This allows you to access the functionalities provided by GroupDocs.Signature for .NET effortlessly.
```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
```
## Step 1: Define File Paths
Begin by defining the paths for your input document and the output directory where the modified document will be saved.
```csharp
string filePath = "sample_multiple_signatures.docx";
string fileName = Path.GetFileName(filePath);
string outputFilePath = Path.Combine("Your Document Directory", "DeleteBySignatureType", fileName);
```
Ensure to replace `"Your Document Directory"` with the actual directory path where your documents are stored.
## Step 2: Copy the Source File
Since the `Delete` method works with the same document, it's recommended to make a copy of the source file to preserve the original.
```csharp
File.Copy(filePath, outputFilePath, true);
```
This step ensures that any modifications made to the document do not affect the original file.
## Step 3: Delete Signatures
Now, initialize a `Signature` object with the output file path and proceed to delete signatures by type.
```csharp
using (Signature signature = new Signature(outputFilePath))
{
    DeleteResult result = signature.Delete(SignatureType.QrCode);
```
Here, we're deleting QR-Code signatures from the document. You can replace `SignatureType.QrCode` with the desired signature type according to your requirements.
## Step 4: Process Deletion Result
After deletion, check the result to determine the success of the operation and display relevant information.
```csharp
if (result.Succeeded.Count > 0)
{
    Console.WriteLine("Following QR-Code signatures were deleted:");
    int number = 1;
    foreach (QrCodeSignature temp in result.Succeeded)
    {
        Console.WriteLine($"Signature #{number++}: Type: {temp.SignatureType} Id:{temp.SignatureId}, Text: {temp.Text}");
    }
}
else
{
    Helper.WriteError("No QR-Code signature was deleted.");
}
```
This step ensures transparency by providing feedback on the deleted signatures.

## Conclusion
In conclusion, managing signatures within your documents is simplified with GroupDocs.Signature for .NET. By following the steps outlined in this tutorial, you can effortlessly delete signatures by type, enhancing the efficiency of your document management workflows.
## FAQ's
### Can I delete multiple types of signatures in a single operation?
Yes, you can delete multiple types of signatures by iterating through each type and performing the deletion process accordingly.
### Is GroupDocs.Signature for .NET compatible with various document formats?
Absolutely! GroupDocs.Signature for .NET supports a wide range of document formats including PDF, Word, Excel, PowerPoint, and more.
### Can I customize the deletion process based on specific criteria?
Certainly! GroupDocs.Signature for .NET provides extensive options for customizing signature deletion based on various parameters such as signature type, text content, location, and more.
### Is there a trial version available for testing before purchasing?
Yes, you can explore the features of GroupDocs.Signature for .NET by downloading the free trial version from [here](https://releases.groupdocs.com/).
### Where can I seek assistance or support regarding GroupDocs.Signature for .NET?
For any queries or assistance, you can visit the GroupDocs.Signature forum [here](https://forum.groupdocs.com/c/signature/13).
