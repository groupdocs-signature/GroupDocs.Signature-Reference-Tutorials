---
title: Search Image Metadata Extraction
linktitle: Search Image Metadata Extraction
second_title: GroupDocs.Signature .NET API
description: 
type: docs
weight: 10
url: /net/document-metadata-extraction/search-image-metadata-extraction/
---

## Complete Source Code
```csharp
using System;
using System.Collections.Generic;

namespace GroupDocs.Signature.Examples.CSharp.BasicUsage
{
    using GroupDocs.Signature;
    using GroupDocs.Signature.Domain;

    public class SearchImageForMetadata
    {
        /// <summary>
        /// Search document for metadata signature
        /// </summary>
        public static void Run()
        {
            Console.WriteLine("\n--------------------------------------------------------------------------------------------------------------------");
            Console.WriteLine("[Example Basic Usage] # SearchImageForMetadata : Search Image document for metadata signature(s)\n");

            // The path to the documents directory.
            string filePath = "sample.png"_SIGNED_METADATA;
            using (Signature signature = new Signature(filePath))
            {
                // search for signatures in document
                List<ImageMetadataSignature> signatures = signature.Search<ImageMetadataSignature>(SignatureType.Metadata);
                Console.WriteLine($"\nSource document ['{filePath}'] contains following signatures.");
                foreach (ImageMetadataSignature mdSignature in signatures)
                {
                    // display only added from example with 41996 + numbers
                    if (mdSignature.Id > 41995)
                    {
                        Console.WriteLine($"\t[{mdSignature.Id}] = {mdSignature.Value} ({mdSignature.Type})");
                    }
                }
            }
        }
    }
}
```
