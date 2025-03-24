---
title: Ta bort QR-kodsignatur från dokument
linktitle: Ta bort QR-kodsignatur från dokument
second_title: GroupDocs.Signature .NET API
description: Lär dig hur du tar bort QR-kodsignaturer från dokument med GroupDocs.Signature för .NET. Följ vår steg-för-steg-guide för effektiv signaturhantering.
weight: 16
url: /sv/net/delete-operations/delete-qr-code-signature/
---
## Introduktion
den här självstudien guidar vi dig genom processen att ta bort en QR-kodsignatur från ett dokument med GroupDocs.Signature för .NET. Följ dessa steg-för-steg-instruktioner för att effektivt ta bort QR-kodsignaturer.
## Förutsättningar
Innan du börjar, se till att du har följande förutsättningar:
-  GroupDocs.Signature för .NET: Se till att du har GroupDocs.Signature-biblioteket installerat i ditt .NET-projekt. Du kan ladda ner den från[här](https://releases.groupdocs.com/signature/net/).
- Dokument med QR-kodsignatur: Förbered ett dokument som innehåller QR-kodsignaturer som du vill radera.
- Grundläggande kunskaper i C#: Bekanta dig med grunderna i programmeringsspråket i C#.

## Importera namnområden
Innan du dyker in i koden, importera de nödvändiga namnrymden till din C#-fil:
```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## Steg 1: Definiera filsökvägar
```csharp
// Sökvägen till dokumentkatalogen.
string filePath = "sample_multiple_signatures.docx";
string fileName = Path.GetFileName(filePath);
// Definiera utdatafilens sökväg för det ändrade dokumentet.
string outputFilePath = Path.Combine("Your Document Directory", "DeleteQRCode", fileName);
// Kopiera källfilen eftersom raderingsmetoden fungerar med samma dokument.
File.Copy(filePath, outputFilePath, true);
```
## Steg 2: Initiera signaturobjekt
```csharp
using (Signature signature = new Signature(outputFilePath))
{
    // Skapa alternativ för att söka efter QR-kodsignaturer.
    QrCodeSearchOptions options = new QrCodeSearchOptions();
    // Sök efter QR-kodsignaturer i dokumentet.
    List<QrCodeSignature> signatures = signature.Search<QrCodeSignature>(options);
```
## Steg 3: Kontrollera om det finns QR-kodsignatur
```csharp
    if (signatures.Count > 0)
    {
        // Få den första QR-kodsignaturen som finns i dokumentet.
        QrCodeSignature qrCodeSignature = signatures[0];
```
## Steg 4: Ta bort QR-kodsignatur
```csharp
        // Ta bort QR-kodsignaturen från dokumentet.
        bool result = signature.Delete(qrCodeSignature);
        if (result)
        {
            Console.WriteLine($"Signature with QR-Code '{qrCodeSignature.Text}' and encode type '{qrCodeSignature.EncodeType.TypeName}' was deleted from document ['{fileName}'].");
        }
        else
        {
            Helper.WriteError($"Signature was not deleted from the document! Signature with Barcode '{qrCodeSignature.Text}' and encode type '{qrCodeSignature.EncodeType.TypeName}' was not found!");
        }
    }
}
```
Grattis! Du har tagit bort QR-kodsignaturen från dokumentet med GroupDocs.Signature för .NET.

## Slutsats
I den här handledningen lärde vi oss hur man tar bort en QR-kodsignatur från ett dokument med GroupDocs.Signature för .NET. Genom att följa de medföljande stegen kan du effektivt hantera och manipulera signaturer i dina .NET-applikationer.
## FAQ's
### Kan jag ta bort flera QR-kodsignaturer från ett dokument?
Ja, du kan ändra koden så att den går igenom alla QR-kodsignaturer och radera dem därefter.
### Stöder GroupDocs.Signature andra typer av signaturer förutom QR-koder?
Ja, GroupDocs.Signature stöder olika signaturtyper som text, bild, streckkod och mer.
### Är GroupDocs.Signature kompatibel med alla dokumentformat?
GroupDocs.Signature stöder ett brett utbud av dokumentformat inklusive PDF, Microsoft Word, Excel, PowerPoint och mer.
### Kan jag anpassa sökalternativen för signaturer?
Ja, du kan skräddarsy sökalternativen efter dina krav för att hitta specifika signaturer i dokumentet.
### Finns det en testversion tillgänglig för GroupDocs.Signature?
 Ja, du kan få tillgång till en gratis testversion av GroupDocs.Signature från[här](https://releases.groupdocs.com/).