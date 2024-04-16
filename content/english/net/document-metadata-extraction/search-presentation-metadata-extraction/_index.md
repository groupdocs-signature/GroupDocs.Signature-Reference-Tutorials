---
title: Search Presentation Metadata Extraction
linktitle: Search Presentation Metadata Extraction
second_title: GroupDocs.Signature .NET API
description: 
type: docs
weight: 12
url: /net/document-metadata-extraction/search-presentation-metadata-extraction/
---

## Complete Source Code
```csharp
using System;
using System.Collections.Generic;

namespace GroupDocs.Signature.Examples.CSharp.BasicUsage
{
    using GroupDocs.Signature;
    using GroupDocs.Signature.Domain;

    public class SearchPresentationForMetadata
    {
        /// <summary>
        /// Search document for metadata signature
        /// </summary>
        public static void Run()
        {
            Console.WriteLine("\n--------------------------------------------------------------------------------------------------------------------");
            Console.WriteLine("[Example Basic Usage] # SearchPresentationForMetadata : Search Presentation document for metadata signature(s)\n");

            // The path to the documents directory.
            string filePath = "sample.pptx"_SIGNED_METADATA;
            using (Signature signature = new Signature(filePath))
            {
                // search for signatures in document
                List<PresentationMetadataSignature> signatures = signature.Search<PresentationMetadataSignature>(SignatureType.Metadata);
                Console.WriteLine($"\nSource document ['{filePath}'] contains following signatures.");
                foreach (PresentationMetadataSignature mdSignature in signatures)
                {
                    Console.WriteLine($"\t[{mdSignature.Name}] = {mdSignature.Value} ({mdSignature.Type})");
                }
            }
        }
    }
}
```
