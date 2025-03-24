---
title: Sök efter flera signaturer
linktitle: Sök efter flera signaturer
second_title: GroupDocs.Signature .NET API
description: Lär dig hur du söker efter flera signaturer i .NET-dokument med GroupDocs.Signature för effektiv dokumentsäkerhet och integritet.
weight: 14
url: /sv/net/signature-searching/search-for-multiple-signatures/
---

# Sök efter flera signaturer

## Introduktion
GroupDocs.Signature för .NET är ett kraftfullt bibliotek som gör det möjligt för utvecklare att lägga till, söka och ta bort olika typer av signaturer i populära dokumentformat med .NET-applikationer. I den här handledningen kommer vi att fokusera på att söka efter flera signaturer i ett dokument med GroupDocs.Signature för .NET.
## Förutsättningar
Innan vi börjar, se till att du har följande förutsättningar:
- Visual Studio installerat på ditt system.
- Grundläggande förståelse för programmeringsspråket C#.
- GroupDocs.Signature för .NET-biblioteket installerat i ditt projekt. Du kan ladda ner den från[här](https://releases.groupdocs.com/signature/net/).

## Importera namnområden
Först måste du importera de nödvändiga namnområdena för att komma åt klasserna och metoderna som tillhandahålls av GroupDocs.Signature för .NET.
```csharp
using System;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## Steg 1: Ladda dokumentet
Ladda dokumentet där du vill söka efter flera signaturer. Se till att du anger rätt sökväg.
```csharp
string filePath = "sample_multiple_signatures.docx";
using (Signature signature = new Signature(filePath))
{
    // Din kod kommer hit
}
```
## Steg 2: Definiera sökalternativ
Definiera sökalternativ för olika typer av signaturer som text, digital, streckkod, QR-kod och metadata. Du kan ange sökkriterier som text som ska matchas, matchningstyp och söka på alla sidor.
```csharp
// Definiera sökalternativ
TextSearchOptions textOptions = new TextSearchOptions()
{
    AllPages = true
};
DigitalSearchOptions digitalOptions = new DigitalSearchOptions()
{
    AllPages = true
};
BarcodeSearchOptions barcodeOptions = new BarcodeSearchOptions()
{
    AllPages = true,
    Text = "123456",
    MatchType = TextMatchType.Exact
};
QrCodeSearchOptions qrCodeOptions = new QrCodeSearchOptions()
{
    AllPages = true,
    Text = "John",
    MatchType = TextMatchType.Contains
};
MetadataSearchOptions metadataOptions = new MetadataSearchOptions();
```
## Steg 3: Lägg till sökalternativ i listan
Lägg till de definierade sökalternativen till en lista.
```csharp
// Lägg till alternativ i listan
List<SearchOptions> listOptions = new List<SearchOptions>();
listOptions.Add(textOptions);
listOptions.Add(barcodeOptions);
listOptions.Add(qrCodeOptions);
listOptions.Add(metadataOptions);
listOptions.Add(digitalOptions);
```
## Steg 4: Sök efter signaturer
Sök efter signaturer i dokumentet med de definierade sökalternativen.
```csharp
// Sök efter signaturer i dokument
SearchResult result = signature.Search(listOptions);
if (result.Signatures.Count > 0)
{
    Console.WriteLine($"\nSource document ['{filePath}'] contains following signatures.");
    foreach (var resSignature in result.Signatures)
    {
        Console.WriteLine($"Signature found at page {resSignature.PageNumber} with type {resSignature.SignatureType} and Id#: {resSignature.SignatureId}");
    }
}
else
{
    Helper.WriteError("No one signature was found.");
}
```

## Slutsats
den här handledningen lärde vi oss hur man söker efter flera signaturer i ett dokument med GroupDocs.Signature för .NET. Genom att följa de medföljande stegen kan du effektivt hitta olika typer av signaturer i dina dokument, vilket förbättrar dokumentsäkerheten och integriteten.
## FAQ's
### Kan jag söka efter signaturer i olika dokumentformat?
Ja, GroupDocs.Signature för .NET stöder ett brett utbud av dokumentformat inklusive Word, PDF, Excel och mer.
### Är det möjligt att anpassa sökkriterier för signaturer?
Absolut, du kan skräddarsy sökkriterier efter dina krav, som att ange exakta textmatchningar eller söka på alla sidor.
### Erbjuder GroupDocs.Signature för .NET stöd för digitala signaturer?
Ja, du kan söka efter digitala signaturer såväl som andra typer som text, streckkod och QR-kodsignaturer.
### Kan jag enkelt integrera signatursökningsfunktioner i mina .NET-applikationer?
Ja, GroupDocs.Signature för .NET tillhandahåller ett enkelt API som förenklar integrationsprocessen.
### Var kan jag hitta ytterligare stöd eller hjälp?
 Du kan besöka forumet GroupDocs.Signature[här](https://forum.groupdocs.com/c/signature/13) för eventuella frågor eller hjälp.