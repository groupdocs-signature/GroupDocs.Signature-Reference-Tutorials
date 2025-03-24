---
title: Signera dokument med QR-kod med GroupDocs.Signature
linktitle: Signering med QR-kod
second_title: GroupDocs.Signature .NET API
description: Lär dig hur du lägger till QR-kodsignaturer i dina dokument med GroupDocs.Signature för .NET. Förbättra säkerhet och autentisering utan ansträngning.
weight: 15
url: /sv/net/advanced-signature-techniques/sign-with-qr-code/
---
## Introduktion
den här handledningen går vi igenom processen att signera dokument med en QR-kod med GroupDocs.Signature för .NET. GroupDocs.Signature för .NET är ett kraftfullt API som tillåter utvecklare att lägga till olika typer av signaturer till digitala dokument programmatiskt. Att signera dokument med QR-koder kan ge ett extra lager av säkerhet och autentisering till dina dokument.
## Förutsättningar
Innan vi börjar, se till att du har följande förutsättningar installerade:
1.  GroupDocs.Signature för .NET: Du kan ladda ner biblioteket från[hemsida](https://releases.groupdocs.com/signature/net/).
2. Utvecklingsmiljö: Se till att du har en .NET-utvecklingsmiljö inställd på din dator.
3. Exempeldokument: Förbered ett exempeldokument (t.ex. PDF) som du vill signera med en QR-kod.

## Importera nödvändiga namnområden
Innan vi dyker in i koden, låt oss importera de nödvändiga namnrymden:
```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

## Steg 1: Definiera filsökvägar
```csharp
string filePath = "sample.pdf";
string fileName = Path.GetFileName(filePath);
string outputFilePath = Path.Combine("Your Document Directory", "SignWithQRCode", fileName);
```
 Se till att byta ut`"Your Document Directory"` med sökvägen till katalogen där du vill spara det signerade dokumentet.
## Steg 2: Initiera signaturobjekt
```csharp
using (Signature signature = new Signature(filePath))
{
    //Koden för signering går här
}
```
 Initiera a`Signature` objekt med sökvägen till dokumentet du vill signera.
## Steg 3: Skapa QRCodeSignOptions
```csharp
QrCodeSignOptions options = new QrCodeSignOptions("JohnSmith")
{
    EncodeType = QrCodeTypes.QR,
    Left = 50,
    Top = 150,
    Width = 200,
    Height = 200
};
```
 Skapa en`QrCodeSignOptions` objekt med önskade inställningar för QR-kodsignaturen. Du kan anpassa parametrar som texten som ska kodas, positionera och dimensioner för QR-koden.
## Steg 4: Signera dokumentet
```csharp
SignResult result = signature.Sign(outputFilePath, options);
```
 Använd`Sign` metod för`Signature` objekt för att signera dokumentet med de angivna alternativen. Denna metod returnerar en`SignResult` objekt som innehåller information om signeringsprocessen.
## Steg 5: Visa resultat
```csharp
Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).\nFile saved at {outputFilePath}.");
```
Visa ett meddelande som anger att signeringsprocessen har lyckats och platsen där det signerade dokumentet sparas.

## Slutsats
I den här handledningen har vi lärt oss hur man signerar dokument med en QR-kod med GroupDocs.Signature för .NET. Genom att följa dessa enkla steg kan du lägga till QR-kodsignaturer till dina digitala dokument, vilket förbättrar säkerheten och autentiseringen.

## FAQ's
### Kan jag anpassa utseendet på QR-koden?
Ja, du kan anpassa olika parametrar som storlek, position och kodningstyp för QR-koden enligt dina krav.
### Vilka dokumentformat stöds för signering med QR-koder?
GroupDocs.Signature för .NET stöder ett brett utbud av dokumentformat, inklusive PDF, Word, Excel, PowerPoint och mer.
### Är det möjligt att signera flera dokument i en batchprocess?
Absolut, du kan använda GroupDocs.Signature för .NET för att signera flera dokument samtidigt, vilket effektiviserar ditt arbetsflöde.
### Kan jag verifiera äktheten av ett dokument signerat med en QR-kod?
Ja, GroupDocs.Signature för .NET tillhandahåller verifieringsmekanismer för att säkerställa integriteten och äktheten hos signerade dokument.
### Finns det en testversion tillgänglig för att testa funktionen innan du köper?
 Ja, du kan ladda ner en gratis testversion från[hemsida](https://releases.groupdocs.com/) för att utvärdera funktionerna och kapaciteten hos GroupDocs.Signature för .NET.