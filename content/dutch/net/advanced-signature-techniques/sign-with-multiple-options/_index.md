---
title: Ondertekenen met meerdere opties
linktitle: Ondertekenen met meerdere opties
second_title: GroupDocs.Signature .NET API
description: Leer hoe u documenten met meerdere opties kunt ondertekenen met GroupDocs.Signature voor .NET. Verbeter de documentbeveiliging met tekst, barcode, QR-code, digitaal en beeld.
weight: 14
url: /nl/net/advanced-signature-techniques/sign-with-multiple-options/
---

# Ondertekenen met meerdere opties

## Invoering
In deze zelfstudie onderzoeken we hoe u een document kunt ondertekenen met meerdere handtekeningopties met behulp van de GroupDocs.Signature-bibliotheek voor .NET. Het ondertekenen van documenten met verschillende opties, zoals handtekeningen met tekst, streepjescode, QR-code, digitale handtekeningen, afbeeldingen en metagegevens, kan veelzijdigheid bieden en de documentbeveiliging verbeteren.
## Vereisten
Voordat u aan de slag gaat, moet u ervoor zorgen dat u aan de volgende vereisten voldoet:
1.  GroupDocs.Signature voor .NET Library: Download en installeer de GroupDocs.Signature voor .NET-bibliotheek van[hier](https://releases.groupdocs.com/signature/net/).
2. Ontwikkelomgeving: Zet een ontwikkelomgeving op waarop .NET Framework is geïnstalleerd.
3. Te ondertekenen document: bereid het document voor (bijvoorbeeld voorbeeld.docx) dat u wilt ondertekenen.
4. Certificaten en afbeeldingen: bereid alle vereiste certificaten en afbeeldingen voor voor digitale en beeldhandtekeningen.

## Naamruimten importeren
Importeer eerst de benodigde naamruimten om de GroupDocs.Signature-bibliotheek in uw .NET-toepassing te gebruiken:
```csharp
using System;
using System.IO;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## Stap 1: Laad het document
```csharp
string filePath = "sample.docx";
string outputFilePath = Path.Combine("Your Document Directory", "SignWithMultiple", "SignWithMultiple.docx");
using (Signature signature = new Signature(filePath))
{
    // Je code gaat verder...
}
```
## Stap 2: Definieer handtekeningopties
Definieer verschillende handtekeningopties van verschillende typen en instellingen, zoals tekst-, streepjescode-, QR-code-, digitale, afbeelding- en metagegevenshandtekeningen:
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
// Definieer andere handtekeningopties (bijvoorbeeld QR-code, digitaal, afbeelding, metadata)...
```
## Stap 3: Maak een lijst met handtekeningopties
Definieer een lijst met handtekeningopties die alle eerder gedefinieerde opties bevatten:
```csharp
List<SignOptions> listOptions = new List<SignOptions>();
listOptions.Add(textOptions);
listOptions.Add(barcodeOptions);
// Voeg andere handtekeningopties toe aan de lijst...
```
## Stap 4: Onderteken het document
Onderteken het document met de lijst met ondertekeningsopties en sla het ondertekende document op:
```csharp
SignResult result = signature.Sign(outputFilePath, listOptions);
Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).\nFile saved at {outputFilePath}.");
```

## Conclusie
Het ondertekenen van documenten met meerdere opties met GroupDocs.Signature voor .NET biedt een robuuste oplossing voor het verbeteren van de documentbeveiliging en veelzijdigheid. Door de stappen in deze zelfstudie te volgen, kunt u verschillende handtekeningtypen naadloos integreren in uw .NET-toepassingen.
## Veelgestelde vragen
### Kan ik aangepaste afbeeldingen gebruiken voor digitale handtekeningen?
Ja, u kunt aangepaste afbeeldingen opgeven voor digitale handtekeningen met behulp van de GroupDocs.Signature-bibliotheek.
### Is GroupDocs.Signature compatibel met verschillende documentformaten?
Ja, GroupDocs.Signature ondersteunt verschillende documentformaten, waaronder DOCX, PDF, PPTX en meer.
### Kan ik het uiterlijk van teksthandtekeningen aanpassen?
Absoluut, u kunt het uiterlijk van teksthandtekeningen aanpassen, inclusief lettergrootte, kleur en stijl.
### Biedt GroupDocs.Signature codering voor digitale handtekeningen?
Ja, GroupDocs.Signature biedt coderingsopties voor digitale handtekeningen om de veiligheid van documenten te garanderen.
### Is er een proefversie beschikbaar voor GroupDocs.Signature voor .NET?
 Ja, u kunt een gratis proefversie van GroupDocs.Signature voor .NET downloaden van[hier](https://releases.groupdocs.com/).