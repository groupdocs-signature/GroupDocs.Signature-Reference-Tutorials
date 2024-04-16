---
title: Sign Spreadsheet with Metadata
linktitle: Sign Spreadsheet with Metadata
second_title: GroupDocs.Signature .NET API
description: 
type: docs
weight: 13
url: /net/document-signing/sign-spreadsheet-with-metadata/
---

## Complete Source Code
```csharp
using System;
using System.IO;

namespace GroupDocs.Signature.Examples.CSharp.BasicUsage
{
    using GroupDocs.Signature;
    using GroupDocs.Signature.Domain;
    using GroupDocs.Signature.Options;

    public class SignSpreadsheetWithMetadata
    {
        /// <summary>
        /// Sign spreadsheets document with metadata signature
        /// </summary>
        public static void Run()
        {
            Console.WriteLine("\n--------------------------------------------------------------------------------------------------------------------");
            Console.WriteLine("[Example Basic Usage] # SignSpreadsheetWithMetadata : Sign spreadsheets document with metadata signature\n");

            // The path to the documents directory.
            string filePath = "sample.xlsx";
            string outputFilePath = Path.Combine("Your Document Directory", "SignSpreadsheetWithMetadata", "SignedWithMetadata.xlsx");

            using (Signature signature = new Signature(filePath))
            {
                // create Metadata option with predefined Metadata text
                MetadataSignOptions options = new MetadataSignOptions();

                // Create few Spreadsheet Metadata signatures
                SpreadsheetMetadataSignature[] signatures = new SpreadsheetMetadataSignature[]
                {
                    new SpreadsheetMetadataSignature("Author", "Mr.Scherlock Holmes"), // String value
                    new SpreadsheetMetadataSignature("CreatedOn", DateTime.Now), // DateTime values
                    new SpreadsheetMetadataSignature("DocumentId", 123456), // Integer value
                    new SpreadsheetMetadataSignature("SignatureId", 123.456D), // Double value
                    new SpreadsheetMetadataSignature("Amount", 123.456M), // Decimal value
                    new SpreadsheetMetadataSignature("Total", 123.456F) // Float value
                };
                options.Signatures.AddRange(signatures);

                // sign document to file
                SignResult result = signature.Sign(outputFilePath, options);

                Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).\nFile saved at {outputFilePath}.");
            }
        }
    }
}
```
