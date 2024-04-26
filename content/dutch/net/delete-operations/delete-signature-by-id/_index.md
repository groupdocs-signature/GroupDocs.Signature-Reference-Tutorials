---
title: Handtekening op ID verwijderen
linktitle: Handtekening op ID verwijderen
second_title: GroupDocs.Signature .NET API
description: Leer hoe u een handtekening op ID in .NET-documenten verwijdert met behulp van de GroupDocs.Signature-bibliotheek. Gemakkelijke stap-voor-stap handleiding.
type: docs
weight: 11
url: /nl/net/delete-operations/delete-signature-by-id/
---
## Invoering
In deze zelfstudie onderzoeken we hoe u een handtekening op basis van de ID kunt verwijderen met behulp van GroupDocs.Signature voor .NET. GroupDocs.Signature voor .NET is een krachtige bibliotheek waarmee ontwikkelaars digitale handtekeningen in verschillende documentformaten kunnen toevoegen, verwijderen of verifiëren met behulp van .NET-toepassingen.
## Vereisten
Voordat we beginnen, zorg ervoor dat u aan de volgende vereisten voldoet:
1.  GroupDocs.Signature voor .NET Library: Download en installeer de bibliotheek van[hier](https://releases.groupdocs.com/signature/net/).
2. .NET Framework: Zorg ervoor dat .NET Framework op uw systeem is geïnstalleerd.
3. Document met handtekening: bereid een document voor (bijvoorbeeld DOCX, PDF) met een handtekening die u wilt verwijderen.

## Naamruimten importeren
```csharp
using System;
using System.IO;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## Stap 1: Definieer bestandspaden
Geef eerst het bestandspad op voor het document dat de handtekening bevat, en het uitvoerbestandspad waar het gewijzigde document zal worden opgeslagen.
```csharp
string filePath = "sample_multiple_signatures.docx";
string fileName = Path.GetFileName(filePath);
string outputFilePath = Path.Combine("Your Document Directory", "DeleteById", fileName);
```
## Stap 2: Kopieer het document
 Sinds de`Delete` methode het document op zijn plaats wijzigt, kunt u het beste een kopie van het originele document maken.
```csharp
File.Copy(filePath, outputFilePath, true);
```
## Stap 3: Handtekening op ID verwijderen
 Initialiseer de`Signature` object met het documentbestandspad en gebruik de`Delete` methode om de handtekening op basis van zijn ID te verwijderen.
```csharp
using (Signature signature = new Signature(outputFilePath))
{
    string id = @"eff64a14-dad9-47b0-88e5-2ee4e3604e71";
    bool result = signature.Delete(id);
    if (result)
    {
        Console.WriteLine($"Signature with Id# '{id}' was deleted from document ['{fileName}'].");
    }
    else
    {
        Helper.WriteError($"Signature was not deleted from the document! Signature with id# '{id}' was not found!");
    }
}
```

## Conclusie
In deze zelfstudie hebben we geleerd hoe u een handtekening op basis van de ID kunt verwijderen met behulp van GroupDocs.Signature voor .NET. Deze bibliotheek biedt een handige manier om digitale handtekeningen in verschillende documentformaten programmatisch te beheren.
## Veelgestelde vragen
### Kan ik meerdere handtekeningen tegelijk verwijderen?
 Ja, u kunt meerdere handtekeningen verwijderen door hun ID's te doorlopen en de`Delete` methode voor elke ID.
### Is GroupDocs.Signature voor .NET compatibel met alle documentformaten?
GroupDocs.Signature voor .NET ondersteunt een breed scala aan documentformaten, waaronder PDF, DOCX, XLSX en meer.
### Kan ik het uiterlijk van de handtekening aanpassen?
Ja, u kunt het uiterlijk van de handtekening aanpassen, inclusief de positie, grootte, lettertype en kleur.
### Is er een proefversie beschikbaar?
 Ja, u kunt een gratis proefversie downloaden van[hier](https://releases.groupdocs.com/).
### Waar kan ik hulp of ondersteuning vinden voor GroupDocs.Signature voor .NET?
 U kunt het ondersteuningsforum bezoeken[hier](https://forum.groupdocs.com/c/signature/13) Voor assistentie.