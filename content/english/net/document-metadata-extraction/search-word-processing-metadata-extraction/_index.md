---
title: Search Word Processing Metadata Extraction
linktitle: Search Word Processing Metadata Extraction
second_title: GroupDocs.Signature .NET API
description: 
type: docs
weight: 14
url: /net/document-metadata-extraction/search-word-processing-metadata-extraction/
---

## Complete Source Code
```csharp
using System;
using System.Collections.Generic;

namespace GroupDocs.Signature.Examples.CSharp.BasicUsage
{
    using GroupDocs.Signature;
    using GroupDocs.Signature.Domain;

    public class SearchWordProcessingForMetadata
    {
        /// <summary>
        /// Search document for metadata signature
        /// </summary>
        public static void Run()
        {
            Console.WriteLine("\n--------------------------------------------------------------------------------------------------------------------");
            Console.WriteLine("[Example Basic Usage] # SearchWordProcessingForMetadata : Search Word Processing document for metadata signature(s)\n");

            // The path to the documents directory.
            string filePath = Constants.SAMPLE_WORDSPROCESSING_SIGNED_METADATA;
            using (Signature signature = new Signature(filePath))
            {
                // search for signatures in document
                List<WordProcessingMetadataSignature> signatures = signature.Search<WordProcessingMetadataSignature>(SignatureType.Metadata);
                Console.WriteLine($"\nSource document ['{filePath}'] contains following signatures.");
                foreach (WordProcessingMetadataSignature mdSignature in signatures)
                {
                    Console.WriteLine($"\t[{mdSignature.Name}] = {mdSignature.Value} ({mdSignature.Type})");
                }
            }
        }
    }
}
```
