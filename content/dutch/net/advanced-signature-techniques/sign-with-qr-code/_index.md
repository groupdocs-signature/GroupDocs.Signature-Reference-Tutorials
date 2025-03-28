---
title: Documenten ondertekenen met QR-code met GroupDocs.Signature
linktitle: Ondertekenen met QR-code
second_title: GroupDocs.Signature .NET API
description: Leer hoe u QR-codehandtekeningen aan uw documenten kunt toevoegen met GroupDocs.Signature voor .NET. Verbeter moeiteloos de beveiliging en authenticatie.
weight: 15
url: /nl/net/advanced-signature-techniques/sign-with-qr-code/
---

# Documenten ondertekenen met QR-code met GroupDocs.Signature

## Invoering
In deze zelfstudie doorlopen we het proces van het ondertekenen van documenten met een QR-code met behulp van GroupDocs.Signature voor .NET. GroupDocs.Signature voor .NET is een krachtige API waarmee ontwikkelaars programmatisch verschillende soorten handtekeningen aan digitale documenten kunnen toevoegen. Het ondertekenen van documenten met QR-codes kan een extra beveiligings- en authenticatielaag voor uw documenten bieden.
## Vereisten
Voordat we beginnen, zorg ervoor dat de volgende vereisten zijn geïnstalleerd:
1.  GroupDocs.Signature voor .NET: u kunt de bibliotheek downloaden van de[website](https://releases.groupdocs.com/signature/net/).
2. Ontwikkelomgeving: Zorg ervoor dat er een .NET-ontwikkelomgeving op uw computer is geïnstalleerd.
3. Voorbeelddocument: bereid een voorbeelddocument voor (bijvoorbeeld PDF) dat u wilt ondertekenen met een QR-code.

## Noodzakelijke naamruimten importeren
Laten we, voordat we in de code duiken, de benodigde naamruimten importeren:
```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

## Stap 1: Definieer bestandspaden
```csharp
string filePath = "sample.pdf";
string fileName = Path.GetFileName(filePath);
string outputFilePath = Path.Combine("Your Document Directory", "SignWithQRCode", fileName);
```
 Zorg ervoor dat u deze vervangt`"Your Document Directory"` met het pad naar de map waar u het ondertekende document wilt opslaan.
## Stap 2: Initialiseer het handtekeningobject
```csharp
using (Signature signature = new Signature(filePath))
{
    //Code voor ondertekening vindt u hier
}
```
 Initialiseer een`Signature` object met het pad naar het document dat u wilt ondertekenen.
## Stap 3: Maak QRCodeSignOptions
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
 Maak een`QrCodeSignOptions` object met de gewenste instellingen voor de QR-codehandtekening. U kunt parameters aanpassen, zoals de te coderen tekst, de positie en de afmetingen van de QR-code.
## Stap 4: Onderteken het document
```csharp
SignResult result = signature.Sign(outputFilePath, options);
```
 Gebruik de`Sign` werkwijze van de`Signature` bezwaar maken om het document met de opgegeven opties te ondertekenen. Deze methode retourneert a`SignResult` object dat informatie bevat over het ondertekenproces.
## Stap 5: Resultaat weergeven
```csharp
Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).\nFile saved at {outputFilePath}.");
```
Geef een bericht weer dat het succes van het ondertekeningsproces aangeeft en de locatie waar het ondertekende document is opgeslagen.

## Conclusie
In deze zelfstudie hebben we geleerd hoe u documenten kunt ondertekenen met een QR-code met behulp van GroupDocs.Signature voor .NET. Door deze eenvoudige stappen te volgen, kunt u QR-codehandtekeningen aan uw digitale documenten toevoegen, waardoor de beveiliging en authenticatie worden verbeterd.

## Veelgestelde vragen
### Kan ik het uiterlijk van de QR-code aanpassen?
Ja, u kunt verschillende parameters, zoals grootte, positie en coderingstype van de QR-code, aanpassen aan uw vereisten.
### Welke documentformaten worden ondersteund voor ondertekening met QR-codes?
GroupDocs.Signature voor .NET ondersteunt een breed scala aan documentformaten, waaronder PDF, Word, Excel, PowerPoint en meer.
### Is het mogelijk om meerdere documenten in een batchproces te ondertekenen?
Absoluut, u kunt GroupDocs.Signature voor .NET gebruiken om meerdere documenten tegelijkertijd te ondertekenen, waardoor uw workflow wordt gestroomlijnd.
### Kan ik de authenticiteit verifiëren van een document dat is ondertekend met een QR-code?
Ja, GroupDocs.Signature voor .NET biedt verificatiemechanismen om de integriteit en authenticiteit van ondertekende documenten te garanderen.
### Is er een proefversie beschikbaar om de functionaliteit te testen voordat u deze aanschaft?
 Ja, u kunt een gratis proefversie downloaden van de[website](https://releases.groupdocs.com/) om de functies en mogelijkheden van GroupDocs.Signature voor .NET te evalueren.