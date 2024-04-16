---
title: View Document Processing History
linktitle: View Document Processing History
second_title: GroupDocs.Signature .NET API
description: 
type: docs
weight: 12
url: /net/document-preview-operations/view-document-processing-history/
---

## Complete Source Code
```csharp
using System;
using System.IO;

namespace GroupDocs.Signature.Examples.CSharp.BasicUsage
{
    using GroupDocs.Signature;
    using GroupDocs.Signature.Domain;
    public class GetDocumentProcessHistory
    {
        /// <summary>
        /// Get document form fields and signatures information 
        /// </summary>
        public static void Run()
        {
            Console.WriteLine("\n--------------------------------------------------------------------------------------------------------------------");
            Console.WriteLine("[Example Advanced Usage] # GetDocumentProcessHistory : Get document process history\n");

            // The path to the documents directory.
            string filePath = "sample_history.docx";

            using (Signature signature = new Signature(filePath))
            {
                IDocumentInfo documentInfo = signature.GetDocumentInfo();
                // display document process history information
                Console.WriteLine($"Document Process logs information: count = {documentInfo.ProcessLogs.Count}");
                foreach (ProcessLog processLog in documentInfo.ProcessLogs)
                {
                    Console.WriteLine($" - operation [{processLog.Type}] on {processLog.Date.ToShortDateString()}. Succeeded/Failed {processLog.Succeeded}/{processLog.Failed}. Message: {processLog.Message}");
                }
            }
        }
    }
}
```
