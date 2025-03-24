---
title: Ondertekenen met tekst met GroupDocs.Signature voor .NET
linktitle: Ondertekenen met tekst
second_title: GroupDocs.Signature .NET API
description: Leer hoe u documenten met tekst kunt ondertekenen met GroupDocs.Signature voor .NET. Stapsgewijze handleiding voor het programmatisch toevoegen van teksthandtekeningen.
weight: 17
url: /nl/net/advanced-signature-techniques/sign-with-text/
---
## Invoering
In het digitale tijdperk is het elektronisch ondertekenen van documenten een standaardpraktijk geworden, waardoor tijd en middelen worden bespaard. GroupDocs.Signature voor .NET biedt een uitgebreide oplossing voor het programmatisch toevoegen van teksthandtekeningen aan verschillende documentformaten. In deze zelfstudie begeleiden we u bij het ondertekenen van een document met tekst met GroupDocs.Signature voor .NET.
## Vereisten
Voordat we ingaan op de tutorial, zorg ervoor dat je aan de volgende vereisten voldoet:
1.  GroupDocs.Signature voor .NET: Zorg ervoor dat de GroupDocs.Signature voor .NET-bibliotheek is geïnstalleerd. Je kunt het downloaden van[hier](https://releases.groupdocs.com/signature/net/).
2. Ontwikkelomgeving: Zorg dat u een werkomgeving hebt ingericht voor .NET-ontwikkeling.
3. Document: Bereid het document voor (bijvoorbeeld PDF, Word) dat u met tekst wilt ondertekenen.

## Naamruimten importeren
Eerst moet u de benodigde naamruimten in uw .NET-project importeren om de functionaliteiten van GroupDocs.Signature te kunnen gebruiken.
```csharp
using System;
using System.IO;
using System.Drawing;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

Laten we het proces van het ondertekenen van een document met tekst in meerdere stappen opsplitsen:
## Stap 1: Document laden
Laad het document dat u met tekst wilt ondertekenen.
```csharp
string filePath = "sample.pdf"; // Pad naar het document
string fileName = Path.GetFileName(filePath);
```
## Stap 2: Stel het uitvoerbestandspad in
Definieer het uitvoerbestandspad waar het ondertekende document zal worden opgeslagen.
```csharp
string outputFilePath = Path.Combine("Your Document Directory", "SignWithText", fileName);
```
## Stap 3: Handtekeningopties maken
Stel de opties in voor teksthandtekening, inclusief tekstinhoud, positie, grootte, kleur en lettertype.
```csharp
TextSignOptions options = new TextSignOptions("John Smith")
{
    Left = 50, // Handtekeningpositie instellen
    Top = 200,
    Width = 100, // Stel handtekeningrechthoek in
    Height = 30,
    ForeColor = Color.Red, // Tekstkleur instellen
    Font = new SignatureFont { Size = 14, FamilyName = "Comic Sans MS" } // Lettertype instellen
};
```
## Stap 4: Document ondertekenen
Gebruik GroupDocs.Signature om het document te ondertekenen met de opgegeven opties en sla het ondertekende document op in het uitvoerbestandspad.
```csharp
using (Signature signature = new Signature(filePath))
{
    SignResult result = signature.Sign(outputFilePath, options); // Onderteken document
    Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).\nFile saved at {outputFilePath}.");
}
```

## Conclusie
In deze zelfstudie hebben we geleerd hoe u een document met tekst kunt ondertekenen met GroupDocs.Signature voor .NET. Door deze stappen te volgen, kunt u programmatisch efficiënt teksthandtekeningen aan uw documenten toevoegen, waardoor de beveiliging en authenticiteit worden verbeterd.
## Veelgestelde vragen
### Kan ik het uiterlijk van de teksthandtekening aanpassen?
Ja, u kunt verschillende parameters, zoals kleur, lettertype, grootte en positie van de teksthandtekening, aanpassen aan uw voorkeuren.
### Is GroupDocs.Signature compatibel met meerdere documentformaten?
Ja, GroupDocs.Signature ondersteunt verschillende documentformaten, waaronder PDF, Word, Excel, PowerPoint en meer.
### Kan ik meerdere teksthandtekeningen aan één document toevoegen?
Absoluut, u kunt meerdere teksthandtekeningen aan een document toevoegen, elk met zijn eigen set aanpassingsopties.
### Garandeert GroupDocs.Signature de documentintegriteit na ondertekening?
Ja, GroupDocs.Signature maakt gebruik van robuuste cryptografische algoritmen om de documentintegriteit te garanderen en manipulatie na ondertekening te voorkomen.
### Is er een proefversie beschikbaar om te testen voordat u deze aanschaft?
 Ja, u kunt een gratis proefversie downloaden van[hier](https://releases.groupdocs.com/) om de functies te verkennen voordat u een aankoop doet.