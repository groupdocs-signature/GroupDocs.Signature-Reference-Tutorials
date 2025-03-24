---
title: Ondertekenen met Stamp met GroupDocs.Signature
linktitle: Ondertekenen met stempel
second_title: GroupDocs.Signature .NET API
description: Leer hoe u eenvoudig stempelhandtekeningen aan uw .NET-documenten kunt toevoegen met GroupDocs.Signature voor .NET. Verbeter de documentbeveiliging.
weight: 16
url: /nl/net/advanced-signature-techniques/sign-with-stamp/
---

# Ondertekenen met Stamp met GroupDocs.Signature

## Invoering
In deze zelfstudie leiden we u door het proces van het ondertekenen van een document met een stempel met GroupDocs.Signature voor .NET. Door deze stapsgewijze instructies te volgen, kunt u eenvoudig een stempelhandtekening aan uw documenten toevoegen.
## Vereisten
Voordat we beginnen, zorg ervoor dat u aan de volgende vereisten voldoet:
1.  GroupDocs.Signature voor .NET SDK: Download en installeer de SDK van de[website](https://releases.groupdocs.com/signature/net/).
2. Ontwikkelomgeving: Zorg ervoor dat u over een geschikte ontwikkelomgeving beschikt voor .NET-ontwikkeling.
3. Te ondertekenen document: Bereid het document (bijvoorbeeld PDF) voor dat u met een stempel wilt ondertekenen.

## Naamruimten importeren
Begin met het importeren van de benodigde naamruimten in uw project:
```csharp
using System;
using System.IO;
using System.Drawing;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## Stap 1: Laad het document
```csharp
string filePath = "sample.pdf";
using (Signature signature = new Signature(filePath))
{
    // Je code komt hier
}
```
## Stap 2: Stel stempeltekenopties in
```csharp
StampSignOptions options = new StampSignOptions()
{
    Left = 50,
    Top = 150,                    
    Width = 200,
    Height = 200
};
```
## Stap 3: Configureer de weergave van de stempel
```csharp
StampLine outerLine = new StampLine();
outerLine.Text = " * European Union ";
outerLine.TextRepeatType = StampTextRepeatType.FullTextRepeat;
outerLine.Font.Size = 12;
outerLine.Height = 22;
outerLine.TextBottomIntent = 6;
outerLine.TextColor = Color.WhiteSmoke;
outerLine.BackgroundColor = Color.DarkSlateBlue;
options.OuterLines.Add(outerLine);
StampLine innerLine = new StampLine();
innerLine.Text = "John Smith";
innerLine.TextColor = Color.MediumVioletRed;
innerLine.Font.Size = 20;
innerLine.Font.Bold = true;
innerLine.Height = 40;
options.InnerLines.Add(innerLine);
```
## Stap 4: Onderteken het document
```csharp
string outputFilePath = Path.Combine("Your Document Directory", "SignWithStamp", fileName);
SignResult result = signature.Sign(outputFilePath, options);
Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).\nFile saved at {outputFilePath}.");
```

## Conclusie
Het toevoegen van stempelhandtekeningen aan uw documenten met GroupDocs.Signature voor .NET is een eenvoudig proces, zoals gedemonstreerd in deze zelfstudie. Met de meegeleverde stappen kunt u eenvoudig de veiligheid en authenticiteit van uw documenten verbeteren.
## Veelgestelde vragen
### Kan ik het uiterlijk van de stempelhandtekening aanpassen?
Ja, u kunt verschillende aspecten, zoals tekst, lettertype, kleur en positionering van de stempelhandtekening, aanpassen aan uw wensen.
### Ondersteunt GroupDocs.Signature het ondertekenen van meerdere documentformaten?
Ja, GroupDocs.Signature ondersteunt een breed scala aan documentformaten, waaronder PDF, Microsoft Word, Excel, PowerPoint en meer.
### Is er een proefversie beschikbaar voor GroupDocs.Signature?
 Ja, u kunt toegang krijgen tot de gratis proefversie via de[website](https://releases.groupdocs.com/).
### Kan ik meerdere handtekeningen toevoegen aan één document?
Absoluut, met GroupDocs.Signature kunt u meerdere handtekeningen, inclusief stempels, tekst, afbeeldingen en digitale handtekeningen, aan één document toevoegen.
### Waar kan ik ondersteuning vinden als ik tijdens de implementatie problemen tegenkom?
 U kunt ondersteuning en assistentie vinden op het GroupDocs.Signature-communityforum[hier](https://forum.groupdocs.com/c/signature/13).