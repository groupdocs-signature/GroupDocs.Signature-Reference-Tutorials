---
title: Delete Signature by Type
linktitle: Delete Signature by Type
second_title: GroupDocs.Signature .NET API
description: 
type: docs
weight: 12
url: /net/delete-operations/delete-signature-by-type/
---

## Complete Source Code
```csharp
using System;
using System.IO;

namespace GroupDocs.Signature.Examples.CSharp.BasicUsage
{
    using GroupDocs.Signature;
    using GroupDocs.Signature.Domain;

    public class DeleteBySignatureType
    {
        /// <summary>
        /// Delete signatures of the certain type
        /// </summary>
        public static void Run()
        {
            Console.WriteLine("--------------------------------------------------------------------------------------------------------------------");
            Console.WriteLine("[Example Basic Usage] # DeleteBySignatureType : Delete signatures of the certain type \n");

            // The path to the documents directory.
            string filePath = "sample_multiple_signatures.docx";
            string fileName = Path.GetFileName(filePath);
            // copy source file since Delete method works with same Document
            string outputFilePath = Path.Combine("Your Document Directory", "DeleteBySignatureType", fileName);
            
            File.Copy(filePath, outputFilePath, true);
            // processing QR-Code signatures
            using (Signature signature = new Signature(outputFilePath))
            {                
                // deleting QR-Code signatures from the document
                DeleteResult result = signature.Delete(SignatureType.QrCode);
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
                    Helper.WriteError("No one QR-Code signature was deleted.");
                }
            }
        }
    }
}
```
