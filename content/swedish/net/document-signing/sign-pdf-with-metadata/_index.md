---
title: Signera PDF med metadata
linktitle: Signera PDF med metadata
second_title: GroupDocs.Signature .NET API
description: Lär dig hur du signerar PDF-dokument med metadata med GroupDocs.Signature för .NET. Förbättra dokumentspårbarhet och äkthet enkelt.
type: docs
weight: 11
url: /sv/net/document-signing/sign-pdf-with-metadata/
---
## Introduktion
den här handledningen lär vi oss hur du signerar ett PDF-dokument med metadata med GroupDocs.Signature för .NET. Att lägga till metadata till en PDF-fil kan ge ytterligare information om dokumentet, såsom författarskap, skapelsedatum, dokument-ID och mer.
## Förutsättningar
Innan vi börjar, se till att du har följande:
1.  GroupDocs.Signature för .NET: Du kan ladda ner den från[här](https://releases.groupdocs.com/signature/net/).
2. Ett PDF-dokument: Ha ett exempel på en PDF-fil redo för signering.
3. Grundläggande kunskaper i C#-programmering: Förtrogenhet med C#-syntax krävs för att förstå kodexemplen.
## Importera namnområden
Se först till att du importerar de nödvändiga namnområdena för att komma åt de obligatoriska klasserna och metoderna:
```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## Steg 1: Ladda PDF-dokumentet
Ladda PDF-dokumentet du vill signera:
```csharp
string filePath = "sample.pdf";
```
## Steg 2: Ange sökväg för utdatafil
Definiera utdatafilens sökväg där den signerade PDF-filen med metadata ska sparas:
```csharp
string outputFilePath = Path.Combine("Your Document Directory", "SignPdfWithMetadata", "SignedWithMetadata.pdf");
```
## Steg 3: Skapa signaturinstans
Initiera en signaturinstans genom att ange sökvägen till PDF-dokumentet:
```csharp
using (Signature signature = new Signature(filePath))
{
    // Signaturrelaterad kod kommer hit
}
```
## Steg 4: Definiera metadataalternativ
Skapa MetadataSignOptions och lägg till metadatafält med deras respektive värden:
```csharp
MetadataSignOptions options = new MetadataSignOptions();
options
    .Add(new PdfMetadataSignature("Author", "Mr.Sherlock Holmes")) // Strängvärde
    .Add(new PdfMetadataSignature("CreatedOn", DateTime.Now))       // DateTime värden
    .Add(new PdfMetadataSignature("DocumentId", 123456))            // Heltalsvärde
    .Add(new PdfMetadataSignature("SignatureId", 123.456D))         // Dubbelt värde
    .Add(new PdfMetadataSignature("Amount", 123.456M))              // Decimalvärde
    .Add(new PdfMetadataSignature("Total", 123.456F));              // Flytande värde
```
## Steg 5: Signera dokumentet
Signera PDF-dokumentet med de angivna metadataalternativen och spara det signerade dokumentet:
```csharp
SignResult result = signature.Sign(outputFilePath, options);
Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).\nFile saved at {outputFilePath}.");
```

## Slutsats
I den här handledningen har vi tagit upp hur man signerar ett PDF-dokument med metadata med GroupDocs.Signature för .NET. Genom att följa den steg-för-steg-guiden kan du enkelt lägga till metadatainformation som författarskap, skapelsedatum och mer till dina PDF-filer, vilket förbättrar deras användbarhet och spårbarhet.
## FAQ's
### Kan jag lägga till anpassade metadatafält i mina PDF-dokument?
Ja, du kan lägga till anpassade metadatafält genom att ange fältnamnet och dess motsvarande värde med GroupDocs.Signature för .NET.
### Är GroupDocs.Signature for .NET kompatibel med alla versioner av .NET Framework?
GroupDocs.Signature för .NET är kompatibel med olika versioner av .NET Framework, vilket säkerställer flexibilitet och enkel integration.
### Stöder GroupDocs.Signature signering av andra dokumentformat förutom PDF?
Ja, GroupDocs.Signature stöder ett brett utbud av dokumentformat, inklusive Word, Excel, PowerPoint och mer.
### Kan jag signera flera dokument samtidigt med GroupDocs.Signature för .NET?
Ja, du kan signera flera dokument samtidigt genom att iterera genom en lista med filer och tillämpa signaturprocessen programmatiskt.
### Finns teknisk support tillgänglig för GroupDocs.Signature-användare?
 Ja, GroupDocs tillhandahåller dedikerad teknisk support genom sina forum. Du kan komma åt supportforumet[här](https://forum.groupdocs.com/c/signature/13).