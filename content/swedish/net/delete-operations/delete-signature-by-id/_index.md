---
title: Ta bort signatur med ID
linktitle: Ta bort signatur med ID
second_title: GroupDocs.Signature .NET API
description: Lär dig hur du tar bort en signatur med ID i .NET-dokument med hjälp av GroupDocs.Signature-biblioteket. Enkel steg-för-steg guide.
type: docs
weight: 11
url: /sv/net/delete-operations/delete-signature-by-id/
---
## Introduktion
I den här handledningen kommer vi att utforska hur man tar bort en signatur med dess ID med GroupDocs.Signature för .NET. GroupDocs.Signature för .NET är ett kraftfullt bibliotek som låter utvecklare lägga till, ta bort eller verifiera digitala signaturer i olika dokumentformat med hjälp av .NET-applikationer.
## Förutsättningar
Innan vi börjar, se till att du har följande förutsättningar:
1.  GroupDocs.Signature for .NET Library: Ladda ner och installera biblioteket från[här](https://releases.groupdocs.com/signature/net/).
2. .NET Framework: Se till att du har .NET Framework installerat på ditt system.
3. Dokument med signatur: Förbered ett dokument (t.ex. DOCX, PDF) med en signatur som du vill ta bort.

## Importera namnområden
```csharp
using System;
using System.IO;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## Steg 1: Definiera filsökvägar
Ange först filsökvägen för dokumentet som innehåller signaturen och utdatafilsökvägen där det ändrade dokumentet kommer att sparas.
```csharp
string filePath = "sample_multiple_signatures.docx";
string fileName = Path.GetFileName(filePath);
string outputFilePath = Path.Combine("Your Document Directory", "DeleteById", fileName);
```
## Steg 2: Kopiera dokumentet
 Sedan`Delete` modifierar dokumentet på plats, är det bäst att skapa en kopia av originaldokumentet.
```csharp
File.Copy(filePath, outputFilePath, true);
```
## Steg 3: Ta bort signatur med ID
 Initiera`Signature` objekt med dokumentets sökväg och använd`Delete` metod för att ta bort signaturen med dess ID.
```csharp
using (Signature signature = new Signature(outputFilePath))
{
    string id = @"eff64a14-dad9-47b0-88e5-2ee4e3604e71";
    bool result = signature.Delete(id);
    if (result)
    {
        Console.WriteLine($"Signature with Id# '{id}' was deleted from document ['{fileName}'].");
    }
    else
    {
        Helper.WriteError($"Signature was not deleted from the document! Signature with id# '{id}' was not found!");
    }
}
```

## Slutsats
I den här handledningen har vi lärt oss hur man tar bort en signatur med dess ID med GroupDocs.Signature för .NET. Detta bibliotek ger ett bekvämt sätt att hantera digitala signaturer i olika dokumentformat programmatiskt.
## FAQ's
### Kan jag ta bort flera signaturer samtidigt?
 Ja, du kan ta bort flera signaturer genom att iterera genom deras ID och ringa till`Delete` metod för varje ID.
### Är GroupDocs.Signature för .NET kompatibelt med alla dokumentformat?
GroupDocs.Signature för .NET stöder ett brett utbud av dokumentformat, inklusive PDF, DOCX, XLSX och mer.
### Kan jag anpassa utseendet på signaturen?
Ja, du kan anpassa signaturens utseende, inklusive dess position, storlek, teckensnitt och färg.
### Finns det en testversion tillgänglig?
 Ja, du kan ladda ner en gratis testversion från[här](https://releases.groupdocs.com/).
### Var kan jag hitta hjälp eller support för GroupDocs.Signature för .NET?
 Du kan besöka supportforumet[här](https://forum.groupdocs.com/c/signature/13) för assistens.