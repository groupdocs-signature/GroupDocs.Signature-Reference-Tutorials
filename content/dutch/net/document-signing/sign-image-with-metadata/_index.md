---
title: Onderteken afbeelding met metadata
linktitle: Onderteken afbeelding met metadata
second_title: GroupDocs.Signature .NET API
description: Leer hoe u afbeeldingen kunt ondertekenen met metagegevens in .NET met behulp van GroupDocs.Signature. Eenvoudige, efficiënte en aanpasbare oplossing voor het ondertekenen van metagegevens.
weight: 10
url: /nl/net/document-signing/sign-image-with-metadata/
---

# Onderteken afbeelding met metadata

## Invoering
Met GroupDocs.Signature voor .NET kunnen ontwikkelaars afbeeldingen efficiënt met metadata ondertekenen. Deze tutorial begeleidt u stap voor stap door het proces.
## Vereisten
Zorg ervoor dat u over het volgende beschikt voordat u begint:
1. GroupDocs.Signature voor .NET: Installeer het GroupDocs.Signature-pakket in uw .NET-project. Je kunt het downloaden van[hier](https://releases.groupdocs.com/signature/net/).   
2. Afbeeldingsbestand: bereid het afbeeldingsbestand voor dat u wilt ondertekenen met metagegevens.

## Naamruimten importeren
Zorg ervoor dat u de benodigde naamruimten in uw C#-code importeert:
```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## Stap 1: Afbeeldingsbestand laden
Geef eerst het pad naar uw afbeeldingsbestand en de uitvoermap voor de ondertekende afbeelding met metagegevens op:
```csharp
string filePath = "sample.png";            
string outputFilePath = Path.Combine("Your Document Directory", "SignImageWithMetadata", "SignedWithMetadata.png");
```
## Stap 2: Metagegevenshandtekeningen maken
Maak vervolgens verschillende metadata-handtekeningen en voeg deze toe aan de handtekeningverzameling met opties:
```csharp
using (Signature signature = new Signature(filePath))
{
    ushort imgsMetadataId = 41996;
    MetadataSignOptions options = new MetadataSignOptions();
    options
        .Add(new ImageMetadataSignature(imgsMetadataId++, "Mr.Scherlock Holmes")) // Tekenreekswaarde
        .Add(new ImageMetadataSignature(imgsMetadataId++, DateTime.Now))          // Datum Tijd waarde
        .Add(new ImageMetadataSignature(imgsMetadataId++, 123456))                // Integere waarde
        .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456D))              // Dubbele waarde
        .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456M))              // Decimale waarde
        .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456F));             // Zwevende waarde
    
    // document naar bestand ondertekenen
    SignResult result = signature.Sign(outputFilePath, options);
    Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).\nFile saved at {outputFilePath}.");
}
```

## Conclusie
In deze zelfstudie hebt u geleerd hoe u een afbeelding met metagegevens kunt ondertekenen met GroupDocs.Signature voor .NET. Door deze stappen te volgen, kunt u eenvoudig metadata-handtekeningen in uw .NET-applicaties opnemen.

## Veelgestelde vragen
### Kan ik meerdere afbeeldingen met metadata ondertekenen met GroupDocs.Signature voor .NET?
Ja, u kunt meerdere afbeeldingen ondertekenen met metagegevens door elk afbeeldingsbestand te doorlopen en de metagegevenshandtekeningen toe te passen.
### Is er een proefversie beschikbaar voor GroupDocs.Signature voor .NET?
 Ja, u kunt de proefversie downloaden van[hier](https://releases.groupdocs.com/).
### Ondersteunt GroupDocs.Signature voor .NET naast afbeeldingen ook andere bestandsindelingen?
Ja, GroupDocs.Signature ondersteunt verschillende bestandsindelingen, waaronder PDF, Word, Excel en meer.
### Kan ik het uiterlijk van de metadatahandtekening aanpassen?
Ja, u kunt het uiterlijk van de metagegevenshandtekening aanpassen, zoals lettergrootte, kleur en positie.
### Waar kan ik ondersteuning krijgen voor GroupDocs.Signature voor .NET?
 U kunt ondersteuning krijgen via het GroupDocs.Signature-forum[hier](https://forum.groupdocs.com/c/signature/13).