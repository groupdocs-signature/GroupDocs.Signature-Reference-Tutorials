---
title: Verify Digital Signature
linktitle: Verify Digital Signature
second_title: GroupDocs.Signature .NET API
description: Verify digital signatures in .NET with ease using GroupDocs.Signature. Ensure document authenticity and integrity effortlessly.
weight: 11
url: /net/verify-operations/verify-digital/
---

# Verify Digital Signature

## Introduction
In the realm of digital documents, ensuring authenticity and integrity is paramount. Digital signatures serve as the digital equivalent of handwritten signatures, providing a secure way to verify the origin and integrity of electronic documents. GroupDocs.Signature for .NET offers a powerful toolkit for working with digital signatures in .NET applications, facilitating the verification of digital signatures with ease.
## Prerequisites
Before diving into the verification process using GroupDocs.Signature for .NET, ensure that you have the following prerequisites in place:
### 1. Install GroupDocs.Signature for .NET
To begin, download and install GroupDocs.Signature for .NET. You can find the download link [here](https://releases.groupdocs.com/signature/net/).
### 2. Obtain Digital Signature File
You'll need a digital signature file (e.g., YourSignature.pfx) for verification purposes. Make sure you have access to this file and its associated password.

## Import Namespaces
In your .NET project, import the necessary namespaces to utilize GroupDocs.Signature functionality.

```csharp
using System;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## 1. Specify Document Path
```csharp
string filePath = "sample_multiple_signatures.docx";
```
Specify the path to the document that you want to verify.
## 2. Initialize Signature Object
```csharp
using (Signature signature = new Signature(filePath))
```
Create a new Signature object by passing the document path as a parameter.
## 3. Set Verification Options
```csharp
DigitalVerifyOptions options = new DigitalVerifyOptions("YourSignature.pfx")
{
    Contact = "Mr.Smith",
    Password = "1234567890"
};
```
Create DigitalVerifyOptions object, specifying the path to the digital signature file (e.g., YourSignature.pfx), along with any additional options such as contact information and password.
## 4. Verify Signatures
```csharp
VerificationResult result = signature.Verify(options);
```
Invoke the Verify method on the Signature object, passing the verification options.
## 5. Handle Verification Result
```csharp
if (result.IsValid)
{
    // Valid signatures found
    foreach (DigitalSignature item in result.Succeeded)
    {
        Console.WriteLine($"\nValid signature is found.");
    }
}
else
{
    // Verification failed
    Helper.WriteError($"\nDocument {filePath} failed verification process.");
}
```
Check if the verification result is valid. If valid, iterate through the list of succeeded signatures. Otherwise, handle the verification failure.

## Conclusion
In conclusion, GroupDocs.Signature for .NET simplifies the process of verifying digital signatures in .NET applications. By following the step-by-step guide outlined above and leveraging the powerful features of GroupDocs.Signature, you can ensure the authenticity and integrity of your digital documents with confidence.
## FAQ's
### Can GroupDocs.Signature verify multiple signatures within a single document?
Yes, GroupDocs.Signature supports the verification of multiple signatures within a single document, providing comprehensive validation capabilities.
### Is GroupDocs.Signature compatible with different types of digital signature files?
GroupDocs.Signature supports various digital signature file formats, including PFX, P12, and others, ensuring flexibility in verification processes.
### Can I customize verification options such as contact information during the verification process?
Yes, GroupDocs.Signature allows customization of verification options, enabling users to specify contact information, passwords, and other parameters as needed.
### Does GroupDocs.Signature offer support for troubleshooting and assistance?
Yes, GroupDocs.Signature provides dedicated support through its forum, where users can seek assistance, share insights, and troubleshoot issues effectively.
### Is there a trial version available for GroupDocs.Signature?
Yes, interested users can access a free trial version of GroupDocs.Signature to explore its features and functionality before making a purchase decision.
