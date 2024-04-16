---
title: Search PDF Metadata Extraction
linktitle: Search PDF Metadata Extraction
second_title: GroupDocs.Signature .NET API
description: 
type: docs
weight: 11
url: /net/document-metadata-extraction/search-pdf-metadata-extraction/
---

## Complete Source Code
```csharp
using System;
using System.Collections.Generic;

namespace GroupDocs.Signature.Examples.CSharp.BasicUsage
{
    using GroupDocs.Signature;
    using GroupDocs.Signature.Domain;    

    public class SearchPdfForMetadata
    {
        /// <summary>
        /// Search document for metadata signature
        /// </summary>
        public static void Run()
        {
            Console.WriteLine("\n--------------------------------------------------------------------------------------------------------------------");
            Console.WriteLine("[Example Basic Usage] # SearchPdfForMetadata : Search Pdf document for metadata signature(s)\n");

            // The path to the documents directory.
            string filePath = "sample.pdf"_SIGNED_METADATA;
            using (Signature signature = new Signature(filePath))
            {
                // search for signatures in document
                List<PdfMetadataSignature> signatures = signature.Search<PdfMetadataSignature>(SignatureType.Metadata);
                Console.WriteLine($"\nSource document ['{filePath}'] contains following signatures.");
                foreach (PdfMetadataSignature mdSignature in signatures)
                {
                    Console.WriteLine($"\t[{mdSignature.TagPrefix} : {mdSignature.Name}] = {mdSignature.Value} ({mdSignature.Type})");
                }
            }
        }
    }
}
```
