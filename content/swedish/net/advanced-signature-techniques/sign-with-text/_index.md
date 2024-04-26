---
title: Signering med text med GroupDocs.Signature för .NET
linktitle: Signering med text
second_title: GroupDocs.Signature .NET API
description: Lär dig hur du signerar dokument med text med GroupDocs.Signature för .NET. Steg-för-steg-guide för att lägga till textsignaturer programmatiskt.
type: docs
weight: 17
url: /sv/net/advanced-signature-techniques/sign-with-text/
---
## Introduktion
I den digitala tidsåldern har det blivit standard att signera dokument elektroniskt, vilket sparar tid och resurser. GroupDocs.Signature för .NET erbjuder en heltäckande lösning för att lägga till textsignaturer till olika dokumentformat programmatiskt. I den här självstudien går vi igenom processen att signera ett dokument med text med GroupDocs.Signature för .NET.
## Förutsättningar
Innan vi dyker in i handledningen, se till att du har följande förutsättningar:
1.  GroupDocs.Signature for .NET: Se till att du har GroupDocs.Signature for .NET-biblioteket installerat. Du kan ladda ner den från[här](https://releases.groupdocs.com/signature/net/).
2. Utvecklingsmiljö: Ha en arbetsmiljö inrättad för .NET-utveckling.
3. Dokument: Förbered dokumentet (t.ex. PDF, Word) som du vill signera med text.

## Importera namnområden
Först måste du importera de nödvändiga namnområdena till ditt .NET-projekt för att använda GroupDocs.Signature-funktioner.
```csharp
using System;
using System.IO;
using System.Drawing;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

Låt oss dela upp processen att signera ett dokument med text i flera steg:
## Steg 1: Ladda dokument
Ladda dokumentet du vill signera med text.
```csharp
string filePath = "sample.pdf"; // Sökväg till dokumentet
string fileName = Path.GetFileName(filePath);
```
## Steg 2: Ställ in sökväg för utdatafil
Definiera utdatafilens sökväg där det signerade dokumentet ska sparas.
```csharp
string outputFilePath = Path.Combine("Your Document Directory", "SignWithText", fileName);
```
## Steg 3: Skapa signaturalternativ
Ställ in alternativen för textsignatur, inklusive textinnehåll, position, storlek, färg och teckensnitt.
```csharp
TextSignOptions options = new TextSignOptions("John Smith")
{
    Left = 50, // Ställ in signaturposition
    Top = 200,
    Width = 100, // Ställ in signaturrektangel
    Height = 30,
    ForeColor = Color.Red, // Ställ in textfärg
    Font = new SignatureFont { Size = 14, FamilyName = "Comic Sans MS" } // Ställ in teckensnitt
};
```
## Steg 4: Signera dokument
Använd GroupDocs.Signature för att signera dokumentet med de angivna alternativen och spara det signerade dokumentet till utdatafilens sökväg.
```csharp
using (Signature signature = new Signature(filePath))
{
    SignResult result = signature.Sign(outputFilePath, options); // Signera dokument
    Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).\nFile saved at {outputFilePath}.");
}
```

## Slutsats
den här handledningen har vi lärt oss hur man signerar ett dokument med text med GroupDocs.Signature för .NET. Genom att följa dessa steg kan du effektivt lägga till textsignaturer till dina dokument programmässigt, vilket förbättrar säkerheten och äktheten.
## FAQ's
### Kan jag anpassa utseendet på textsignaturen?
Ja, du kan anpassa olika parametrar som färg, teckensnitt, storlek och position för textsignaturen enligt dina preferenser.
### Är GroupDocs.Signature kompatibel med flera dokumentformat?
Ja, GroupDocs.Signature stöder olika dokumentformat inklusive PDF, Word, Excel, PowerPoint och mer.
### Kan jag lägga till flera textsignaturer i ett enda dokument?
Absolut, du kan lägga till flera textsignaturer till ett dokument, var och en med sin egen uppsättning anpassningsalternativ.
### Säkerställer GroupDocs.Signature dokumentintegritet efter signering?
Ja, GroupDocs.Signature använder robusta kryptografiska algoritmer för att säkerställa dokumentintegritet och förhindra manipulering efter signering.
### Finns det en testversion tillgänglig för testning innan du köper?
 Ja, du kan ladda ner en gratis testversion från[här](https://releases.groupdocs.com/) att utforska funktionerna innan du gör ett köp.