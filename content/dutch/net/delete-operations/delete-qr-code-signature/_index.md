---
title: Verwijder de QR-codehandtekening uit het document
linktitle: Verwijder de QR-codehandtekening uit het document
second_title: GroupDocs.Signature .NET API
description: Leer hoe u QR-codehandtekeningen uit documenten verwijdert met GroupDocs.Signature voor .NET. Volg onze stapsgewijze handleiding voor efficiënt handtekeningbeheer.
weight: 16
url: /nl/net/delete-operations/delete-qr-code-signature/
---
## Invoering
In deze zelfstudie begeleiden we u bij het verwijderen van een QR-codehandtekening uit een document met behulp van GroupDocs.Signature voor .NET. Volg deze stapsgewijze instructies om QR-codehandtekeningen effectief te verwijderen.
## Vereisten
Voordat u begint, moet u ervoor zorgen dat u aan de volgende vereisten voldoet:
-  GroupDocs.Signature voor .NET: Zorg ervoor dat de GroupDocs.Signature-bibliotheek in uw .NET-project is geïnstalleerd. Je kunt het downloaden van[hier](https://releases.groupdocs.com/signature/net/).
- Document met QR-codehandtekening: bereid een document voor met QR-codehandtekeningen die u wilt verwijderen.
- Basiskennis van C#: maak uzelf vertrouwd met de basisprincipes van de programmeertaal C#.

## Naamruimten importeren
Voordat u in de code duikt, importeert u de benodigde naamruimten in uw C#-bestand:
```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## Stap 1: Definieer bestandspaden
```csharp
// Het pad naar de documentenmap.
string filePath = "sample_multiple_signatures.docx";
string fileName = Path.GetFileName(filePath);
// Definieer het uitvoerbestandspad voor het gewijzigde document.
string outputFilePath = Path.Combine("Your Document Directory", "DeleteQRCode", fileName);
// Kopieer het bronbestand, aangezien de methode Verwijderen met hetzelfde document werkt.
File.Copy(filePath, outputFilePath, true);
```
## Stap 2: Initialiseer het handtekeningobject
```csharp
using (Signature signature = new Signature(outputFilePath))
{
    // Creëer opties voor het zoeken naar QR-codehandtekeningen.
    QrCodeSearchOptions options = new QrCodeSearchOptions();
    // Zoek naar QR-codehandtekeningen in het document.
    List<QrCodeSignature> signatures = signature.Search<QrCodeSignature>(options);
```
## Stap 3: Controleer of er een QR-codehandtekening bestaat
```csharp
    if (signatures.Count > 0)
    {
        // Haal de eerste QR-codehandtekening op die in het document wordt gevonden.
        QrCodeSignature qrCodeSignature = signatures[0];
```
## Stap 4: QR-codehandtekening verwijderen
```csharp
        // Verwijder de QR-codehandtekening uit het document.
        bool result = signature.Delete(qrCodeSignature);
        if (result)
        {
            Console.WriteLine($"Signature with QR-Code '{qrCodeSignature.Text}' and encode type '{qrCodeSignature.EncodeType.TypeName}' was deleted from document ['{fileName}'].");
        }
        else
        {
            Helper.WriteError($"Signature was not deleted from the document! Signature with Barcode '{qrCodeSignature.Text}' and encode type '{qrCodeSignature.EncodeType.TypeName}' was not found!");
        }
    }
}
```
Gefeliciteerd! U hebt de QR-codehandtekening uit het document verwijderd met behulp van GroupDocs.Signature voor .NET.

## Conclusie
In deze zelfstudie hebben we geleerd hoe u een QR-codehandtekening uit een document kunt verwijderen met behulp van GroupDocs.Signature voor .NET. Door de aangegeven stappen te volgen, kunt u handtekeningen binnen uw .NET-applicaties efficiënt beheren en manipuleren.
## Veelgestelde vragen
### Kan ik meerdere QR-codehandtekeningen uit een document verwijderen?
Ja, u kunt de code aanpassen om alle handtekeningen van de QR-code te doorlopen en deze dienovereenkomstig te verwijderen.
### Ondersteunt GroupDocs.Signature naast QR-codes ook andere typen handtekeningen?
Ja, GroupDocs.Signature ondersteunt verschillende soorten handtekeningen, zoals tekst, afbeeldingen, streepjescodes en meer.
### Is GroupDocs.Signature compatibel met alle documentformaten?
GroupDocs.Signature ondersteunt een breed scala aan documentformaten, waaronder PDF, Microsoft Word, Excel, PowerPoint en meer.
### Kan ik de zoekopties voor handtekeningen aanpassen?
Ja, u kunt de zoekopties aanpassen aan uw vereisten om specifieke handtekeningen in het document te vinden.
### Is er een proefversie beschikbaar voor GroupDocs.Signature?
 Ja, u heeft toegang tot een gratis proefversie van GroupDocs.Signature vanaf[hier](https://releases.groupdocs.com/).