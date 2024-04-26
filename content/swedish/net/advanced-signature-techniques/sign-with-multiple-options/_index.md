---
title: Signering med flera alternativ
linktitle: Signering med flera alternativ
second_title: GroupDocs.Signature .NET API
description: Lär dig hur du signerar dokument med flera alternativ med GroupDocs.Signature för .NET. Förbättra dokumentsäkerheten med text, streckkod, QR-kod, digital och bild.
type: docs
weight: 14
url: /sv/net/advanced-signature-techniques/sign-with-multiple-options/
---
## Introduktion
den här självstudien kommer vi att utforska hur man signerar ett dokument med flera signaturalternativ med hjälp av GroupDocs.Signature-biblioteket för .NET. Att signera dokument med olika alternativ som text, streckkod, QR-kod, digital, bild och metadatasignaturer kan ge mångsidighet och förbättra dokumentsäkerheten.
## Förutsättningar
Innan du börjar, se till att du har följande förutsättningar:
1.  GroupDocs.Signature for .NET Library: Ladda ner och installera GroupDocs.Signature for .NET-biblioteket från[här](https://releases.groupdocs.com/signature/net/).
2. Utvecklingsmiljö: Skapa en utvecklingsmiljö med .NET Framework installerat.
3. Dokument att signera: Förbered dokumentet (t.ex. sample.docx) som du vill signera.
4. Certifikat och bilder: Förbered alla nödvändiga certifikat och bilder för digitala signaturer och bildsignaturer.

## Importera namnområden
Importera först de nödvändiga namnområdena för att använda GroupDocs.Signature-biblioteket i din .NET-applikation:
```csharp
using System;
using System.IO;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## Steg 1: Ladda dokumentet
```csharp
string filePath = "sample.docx";
string outputFilePath = Path.Combine("Your Document Directory", "SignWithMultiple", "SignWithMultiple.docx");
using (Signature signature = new Signature(filePath))
{
    // Din kod fortsätter...
}
```
## Steg 2: Definiera signaturalternativ
Definiera flera signaturalternativ av olika typer och inställningar, såsom text, streckkod, QR-kod, digital, bild och metadatasignaturer:
```csharp
TextSignOptions textOptions = new TextSignOptions("Text signature")
{
    VerticalAlignment = VerticalAlignment.Top,
    HorizontalAlignment = HorizontalAlignment.Left
};
BarcodeSignOptions barcodeOptions = new BarcodeSignOptions("123456")
{
    EncodeType = BarcodeTypes.Code128,
    Left = 0,
    Top = 150,
    Height = 50,
    Width = 200
};
// Definiera andra signaturalternativ (t.ex. QR-kod, digital, bild, metadata)...
```
## Steg 3: Skapa en lista med signaturalternativ
Definiera en lista med signaturalternativ som innehåller alla tidigare definierade alternativ:
```csharp
List<SignOptions> listOptions = new List<SignOptions>();
listOptions.Add(textOptions);
listOptions.Add(barcodeOptions);
// Lägg till andra signaturalternativ till listan...
```
## Steg 4: Signera dokumentet
Signera dokumentet med listan över signaturalternativ och spara det signerade dokumentet:
```csharp
SignResult result = signature.Sign(outputFilePath, listOptions);
Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).\nFile saved at {outputFilePath}.");
```

## Slutsats
Att signera dokument med flera alternativ med GroupDocs.Signature för .NET ger en robust lösning för att förbättra dokumentsäkerheten och mångsidigheten. Genom att följa stegen som beskrivs i den här handledningen kan du sömlöst integrera olika signaturtyper i dina .NET-applikationer.
## FAQ's
### Kan jag använda anpassade bilder för digitala signaturer?
Ja, du kan ange anpassade bilder för digitala signaturer med hjälp av biblioteket GroupDocs.Signature.
### Är GroupDocs.Signature kompatibel med olika dokumentformat?
Ja, GroupDocs.Signature stöder olika dokumentformat, inklusive DOCX, PDF, PPTX och mer.
### Kan jag anpassa utseendet på textsignaturer?
Absolut, du kan anpassa utseendet på textsignaturer, inklusive teckenstorlek, färg och stil.
### Tillhandahåller GroupDocs.Signature kryptering för digitala signaturer?
Ja, GroupDocs.Signature erbjuder krypteringsalternativ för digitala signaturer för att säkerställa dokumentsäkerhet.
### Finns det en testversion tillgänglig för GroupDocs.Signature för .NET?
 Ja, du kan ladda ner en gratis testversion av GroupDocs.Signature för .NET från[här](https://releases.groupdocs.com/).