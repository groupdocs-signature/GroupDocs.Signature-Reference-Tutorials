---
title: Controleer QR-code
linktitle: Controleer QR-code
second_title: GroupDocs.Signature .NET API
description: Leer hoe u QR-codes in documenten kunt verifiëren met GroupDocs.Signature voor .NET. Uitgebreide tutorial met stapsgewijze handleiding.
type: docs
weight: 12
url: /nl/net/verify-operations/verify-qr-code/
---
## Invoering
Op het gebied van documentbeheer en authenticatie is het waarborgen van de integriteit en geldigheid van handtekeningen van het allergrootste belang. GroupDocs.Signature voor .NET biedt een uitgebreide oplossing voor het verifiëren van QR-codes die in documenten zijn ingebed. In deze zelfstudie gaan we dieper in op het stapsgewijze proces van het verifiëren van QR-codes met GroupDocs.Signature voor .NET.
## Vereisten
Voordat u zich in het verificatieproces begeeft, moet u ervoor zorgen dat u aan de volgende vereisten voldoet:
1.  Installatie van GroupDocs.Signature voor .NET: Download en installeer GroupDocs.Signature voor .NET vanaf de[download link](https://releases.groupdocs.com/signature/net/).
2. Toegang tot een document dat QR-codes bevat: bereid een voorbeelddocument voor dat QR-codes bevat ter verificatie. 

## Naamruimten importeren
Ten eerste moet u de benodigde naamruimten importeren om de functionaliteiten van GroupDocs.Signature voor .NET te kunnen gebruiken. Volg deze stappen:

```csharp
using System;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```


Laten we nu het proces van het verifiëren van QR-codes die in een document zijn ingebed met behulp van GroupDocs.Signature voor .NET opsplitsen:
## Stap 1: Geef het documentpad op
```csharp
string filePath = "sample_multiple_signatures.docx";
```
 Zorg ervoor dat u deze vervangt`"sample_multiple_signatures.docx"` met het pad naar uw document.
## Stap 2: Initialiseer het handtekeningobject
```csharp
using (Signature signature = new Signature(filePath))
{
    //Verificatiecode komt hier
}
```
 Initialiseer een`Signature` object door het pad naar het document op te geven.
## Stap 3: Geef verificatieopties op
```csharp
QrCodeVerifyOptions options = new QrCodeVerifyOptions()
{
    AllPages = true, // deze waarde is standaard ingesteld
    Text = "John",
    MatchType = TextMatchType.Contains
};
```
 Definieer verificatieopties zoals`AllPages` om alle pagina's te verifiëren,`Text` om de tekst op te geven die moet worden gekoppeld binnen de QR-code, en`MatchType` om de matchingcriteria te definiëren.
## Stap 4: Documenthandtekeningen verifiëren
```csharp
VerificationResult result = signature.Verify(options);
```
 Roep de`Verify` werkwijze van de`Signature` object, waarbij de verificatie-opties worden doorgegeven.
## Stap 5: Verwerk de verificatieresultaten
```csharp
if (result.IsValid)
{
    // Geldige handtekening gevonden
}
else
{
    // Ongeldige handtekening gevonden
}
```
Op basis van het verificatieresultaat handelt u de succes- of faalscenario's dienovereenkomstig af.

## Conclusie
In deze zelfstudie hebben we het proces van het verifiëren van QR-codes in documenten onderzocht met behulp van GroupDocs.Signature voor .NET. Door deze stappen te volgen, kunt u de QR-codeverificatiefunctionaliteit naadloos integreren in uw .NET-applicaties, waardoor de documentintegriteit en authenticiteit wordt gegarandeerd.
## Veelgestelde vragen
### Kan GroupDocs.Signature voor .NET QR-codes in verschillende documentformaten verifiëren?
Ja, GroupDocs.Signature voor .NET ondersteunt een breed scala aan documentformaten, waaronder DOCX, PDF en meer voor QR-codeverificatie.
### Is er een gratis proefversie beschikbaar voor GroupDocs.Signature voor .NET?
 Ja, u kunt gebruikmaken van een gratis proefperiode van de[releases pagina](https://releases.groupdocs.com/).
### Welke ondersteuningsopties zijn beschikbaar voor GroupDocs.Signature voor .NET-gebruikers?
 Gebruikers hebben toegang tot ondersteuning via de[forum](https://forum.groupdocs.com/c/signature/13) voor GroupDocs.Handtekening.
### Kan ik een tijdelijke licentie kopen voor GroupDocs.Signature voor .NET?
 Ja, tijdelijke licenties zijn te koop bij de[GroupDocs-aankooppagina](https://purchase.groupdocs.com/temporary-license/).
### Is er uitgebreide documentatie beschikbaar voor GroupDocs.Signature voor .NET?
 Absoluut, u kunt de meegeleverde gedetailleerde documentatie raadplegen[hier](https://reference.groupdocs.com/signature/net/) voor uitgebreide begeleiding bij het gebruik van de functionaliteiten van GroupDocs.Signature voor .NET.