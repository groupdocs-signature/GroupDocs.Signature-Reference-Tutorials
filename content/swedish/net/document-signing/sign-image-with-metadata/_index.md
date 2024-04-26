---
title: Signera bild med metadata
linktitle: Signera bild med metadata
second_title: GroupDocs.Signature .NET API
description: Lär dig hur du signerar bilder med metadata i .NET med GroupDocs.Signature. Enkel, effektiv och anpassningsbar metadatasigneringslösning.
type: docs
weight: 10
url: /sv/net/document-signing/sign-image-with-metadata/
---
## Introduktion
GroupDocs.Signature för .NET gör det möjligt för utvecklare att signera bilder med metadata effektivt. Denna handledning guidar dig genom processen steg för steg.
## Förutsättningar
Innan du börjar, se till att du har följande:
1. GroupDocs.Signature för .NET: Installera GroupDocs.Signature-paketet i ditt .NET-projekt. Du kan ladda ner den från[här](https://releases.groupdocs.com/signature/net/).   
2. Bildfil: Förbered bildfilen som du vill signera med metadata.

## Importera namnområden
Se till att importera de nödvändiga namnrymden i din C#-kod:
```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## Steg 1: Ladda bildfil
Ange först sökvägen till din bildfil och utdatakatalogen för den signerade bilden med metadata:
```csharp
string filePath = "sample.png";            
string outputFilePath = Path.Combine("Your Document Directory", "SignImageWithMetadata", "SignedWithMetadata.png");
```
## Steg 2: Skapa metadatasignaturer
Skapa sedan olika metadatasignaturer och lägg till dem i signatursamlingen för alternativ:
```csharp
using (Signature signature = new Signature(filePath))
{
    ushort imgsMetadataId = 41996;
    MetadataSignOptions options = new MetadataSignOptions();
    options
        .Add(new ImageMetadataSignature(imgsMetadataId++, "Mr.Scherlock Holmes")) // Strängvärde
        .Add(new ImageMetadataSignature(imgsMetadataId++, DateTime.Now))          // Datum Tid värde
        .Add(new ImageMetadataSignature(imgsMetadataId++, 123456))                // Heltalsvärde
        .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456D))              // Dubbelt värde
        .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456M))              // Decimalvärde
        .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456F));             // Flytande värde
    
    // underteckna dokument till fil
    SignResult result = signature.Sign(outputFilePath, options);
    Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).\nFile saved at {outputFilePath}.");
}
```

## Slutsats
I den här handledningen lärde du dig hur du signerar en bild med metadata med GroupDocs.Signature för .NET. Genom att följa dessa steg kan du enkelt införliva metadatasignaturer i dina .NET-applikationer.

## FAQ's
### Kan jag signera flera bilder med metadata med GroupDocs.Signature för .NET?
Ja, du kan signera flera bilder med metadata genom att iterera igenom varje bildfil och använda metadatasignaturerna.
### Finns det en testversion tillgänglig för GroupDocs.Signature för .NET?
 Ja, du kan ladda ner testversionen från[här](https://releases.groupdocs.com/).
### Stöder GroupDocs.Signature for .NET andra filformat än bilder?
Ja, GroupDocs.Signature stöder olika filformat, inklusive PDF, Word, Excel och mer.
### Kan jag anpassa utseendet på metadatasignaturen?
Ja, du kan anpassa utseendet på metadatasignaturen, som teckenstorlek, färg och position.
### Var kan jag få support för GroupDocs.Signature för .NET?
 Du kan få support från GroupDocs.Signature-forumet[här](https://forum.groupdocs.com/c/signature/13).