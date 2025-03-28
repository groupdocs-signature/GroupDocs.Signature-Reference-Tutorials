---
title: Ta bort flera signaturer från dokument
linktitle: Ta bort flera signaturer från dokument
second_title: GroupDocs.Signature .NET API
description: Ta enkelt bort flera signaturer från dokument med GroupDocs.Signature för .NET. Effektivisera ditt arbetsflöde för dokumenthantering.
weight: 15
url: /sv/net/delete-operations/delete-multiple-signatures/
---

# Ta bort flera signaturer från dokument

## Introduktion
I den digitala världen innebär dokumenthantering ofta att hantera olika signaturer. Att ta bort flera signaturer från ett dokument programmatiskt kan effektivisera arbetsflöden och förbättra effektiviteten. Med GroupDocs.Signature för .NET blir denna uppgift sömlös och enkel. Denna handledning guidar dig genom processen att ta bort flera signaturer från ett dokument steg för steg.
## Förutsättningar
Innan du dyker in i handledningen, se till att du har följande förutsättningar:
- Grundläggande förståelse för programmeringsspråket C#.
- Installerade GroupDocs.Signature för .NET-biblioteket.
- Exempeldokument med flera signaturer för testning.

## Importera namnområden
Börja med att importera de nödvändiga namnområdena för att komma åt funktionaliteten i GroupDocs.Signature for .NET:
```csharp
using System;
using System.IO;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## Steg 1: Definiera dokumentsökväg och filnamn
Ställ in sökvägen för dokumentet som innehåller flera signaturer. Se till att du har rätt sökväg och filnamn:
```csharp
string filePath = "sample_multiple_signatures.docx";
string fileName = Path.GetFileName(filePath);
```
## Steg 2: Kopiera dokumentet för bearbetning
För att undvika att ändra originaldokumentet, skapa en kopia för bearbetning:
```csharp
string outputFilePath = Path.Combine("Your Document Directory", "DeleteMultiple", fileName);
File.Copy(filePath, outputFilePath, true);
```
## Steg 3: Initiera signaturobjekt
Instantiera ett signaturobjekt med hjälp av utdatafilens sökväg:
```csharp
using (Signature signature = new Signature(outputFilePath))
{
    // Signaturbearbetningskoden går här
}
```
## Steg 4: Definiera sökalternativ
Definiera olika sökalternativ för att identifiera signaturer i dokumentet. Alternativen inkluderar textsökning, bildsökning, streckkodssökning och QR-kodsökning:
```csharp
TextSearchOptions textSearchOptions = new TextSearchOptions();
ImageSearchOptions imageSearchOptions = new ImageSearchOptions();
BarcodeSearchOptions barcodeOptions = new BarcodeSearchOptions();
QrCodeSearchOptions qrCodeOptions = new QrCodeSearchOptions();
// Lägg till alternativ i listan
List<SearchOptions> listOptions = new List<SearchOptions>();
listOptions.Add(textSearchOptions);
listOptions.Add(imageSearchOptions);
listOptions.Add(barcodeOptions);
listOptions.Add(qrCodeOptions);
```
## Steg 5: Sök efter signaturer
Utför en sökoperation för att hitta alla signaturer i dokumentet baserat på de definierade sökalternativen:
```csharp
SearchResult result = signature.Search(listOptions);
```
## Steg 6: Ta bort signaturer
Om signaturer hittas, fortsätt att ta bort dem:
```csharp
if (result.Signatures.Count > 0)
{
    // Försök att radera alla signaturer
    DeleteResult deleteResult = signature.Delete(result.Signatures);
    //Kontrollera om raderingen lyckades
    if(deleteResult.Succeeded.Count == result.Signatures.Count)
    {
        Console.WriteLine("\nAll signatures were successfully deleted!");                        
    }
    else
    {
        Console.WriteLine($"Successfully deleted signatures : {deleteResult.Succeeded.Count}");
        Helper.WriteError($"Not deleted signatures : {deleteResult.Failed.Count}");
    }
    // Visa information om raderade signaturer
    Console.WriteLine("\nList of deleted signatures:");
    int number = 1;
    foreach(BaseSignature temp in deleteResult.Succeeded)
    {
        Console.WriteLine($"Signature #{number++}: Type: {temp.SignatureType} Id:{temp.SignatureId}, Location: {temp.Left}x{temp.Top}. Size: {temp.Width}x{temp.Height}");
    }
}
else
{
    Helper.WriteError("No one signature was found.");
}
```

## Slutsats
Att ta bort flera signaturer från ett dokument programmatiskt är en avgörande uppgift i dokumenthantering. Med GroupDocs.Signature för .NET blir denna process effektiv och pålitlig. Genom att följa stegen som beskrivs i den här handledningen kan du enkelt integrera funktioner för borttagning av signaturer i dina .NET-applikationer.
## FAQ's
### Kan GroupDocs.Signature för .NET hantera olika dokumentformat?
Ja, GroupDocs.Signature för .NET stöder ett brett utbud av dokumentformat, inklusive DOCX, PDF, PPTX, XLSX och mer.
### Är det möjligt att anpassa sökalternativ för signaturdetektering?
Absolut, du kan skräddarsy sökalternativ som textsökning, bildsökning, streckkodssökning och QR-kodsökning för att möta dina specifika krav.
### Ger GroupDocs.Signature för .NET felhanteringsmekanismer?
Ja, biblioteket erbjuder robusta felhanteringsfunktioner för att säkerställa smidigt utförande av dokumentbearbetningsuppgifter.
### Kan jag integrera GroupDocs.Signature för .NET med andra tredjepartsbibliotek?
Visst är GroupDocs.Signature för .NET utformad för att sömlöst integreras med andra .NET-bibliotek, vilket ger flexibilitet och utökningsbarhet.
### Var kan jag hitta ytterligare support och resurser för GroupDocs.Signature för .NET?
 Du kan besöka GroupDocs[forum](https://forum.groupdocs.com/c/signature/13) ägnas åt signaturrelaterade diskussioner och söka hjälp från samhället och experter.