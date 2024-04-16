---
title: Search for Images
linktitle: Search for Images
second_title: GroupDocs.Signature .NET API
description: 
type: docs
weight: 13
url: /net/signature-searching/search-for-images/
---

## Complete Source Code
```csharp
using System;
using System.IO;
using System.Collections.Generic;

namespace GroupDocs.Signature.Examples.CSharp.BasicUsage
{
    using GroupDocs.Signature;
    using GroupDocs.Signature.Domain;
    using GroupDocs.Signature.Options;
    
    public class SearchForImage
    {
        /// <summary>
        /// Search document for Image signature
        /// </summary>
        public static void Run()
        {
            Console.WriteLine("\n--------------------------------------------------------------------------------------------------------------------");
            Console.WriteLine("[Example Basic Usage] # SearchForImage : Search document for Image signature \n");

            // The path to the documents directory.
            string filePath = "sample_multiple_signatures.docx";
            string fileName = Path.GetFileName(filePath);
            using (Signature signature = new Signature(filePath))
            {
                // search document
                List<ImageSignature> signatures = signature.Search<ImageSignature>(SignatureType.Image);
                Console.WriteLine($"\nSource document ['{fileName}'] contains following image signature(s).");
                // output signatures
                foreach (ImageSignature imageSignature in signatures)
                {
                    Console.WriteLine($"Found Image signature at page {imageSignature.PageNumber} and size {imageSignature.Size}.");
                }
            }
        }
    }
}
```
