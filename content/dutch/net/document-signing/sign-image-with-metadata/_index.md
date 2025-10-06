---
"description": "Leer hoe u metadata in afbeeldingen kunt ondertekenen en insluiten met GroupDocs.Signature voor .NET. Voeg auteursinformatie, tijdstempels en aangepaste gegevens toe om de authenticiteit en traceerbaarheid van afbeeldingen te verbeteren."
"linktitle": "Tekenafbeelding met metagegevens"
"second_title": "GroupDocs.Signature .NET API"
"title": "Onderteken afbeeldingen met metagegevens in C# .NET"
"url": "/nl/net/document-signing/sign-image-with-metadata/"
"weight": 10
type: docs
---
## Invoering

Het digitaal ondertekenen van afbeeldingen met metadata wordt steeds belangrijker om authenticiteit, eigenaarschap en traceerbaarheid vast te stellen. GroupDocs.Signature voor .NET biedt een krachtige en gebruiksvriendelijke oplossing voor het toevoegen van metadatahandtekeningen aan verschillende afbeeldingsformaten. Deze tutorial begeleidt u door het volledige proces van het ondertekenen van afbeeldingen met metadata in C#.

Met metadatahandtekeningen kunt u waardevolle informatie rechtstreeks in afbeeldingsbestanden insluiten, zoals auteursinformatie, tijdstempels van aanmaak, unieke identificatiegegevens en meer. Deze informatie wordt onderdeel van het afbeeldingsbestand zelf en biedt een betrouwbare methode om de authenticiteit van de afbeelding te volgen en te verifiëren.

## Vereisten

Voordat u met deze tutorial begint, moet u ervoor zorgen dat u over het volgende beschikt:

1. [GroupDocs.Signature voor .NET](https://releases.groupdocs.com/signature/net/) - Download en installeer de bibliotheek
2. Ontwikkelomgeving - Visual Studio of een compatibele IDE met .NET-ondersteuning
3. Afbeeldingsbestand - Een voorbeeld van een afbeeldingsbestand in een ondersteund formaat (PNG, JPG, TIFF, enz.)
4. Basiskennis van C#-programmering - Kennis van C#-programmeerconcepten

## Naamruimten importeren

Begin met het importeren van de benodigde naamruimten om toegang te krijgen tot de GroupDocs.Signature-functionaliteit:

```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

## Stap 1: Bestandspaden instellen

Definieer de paden voor uw bronafbeelding en waar de ondertekende uitvoer moet worden opgeslagen:

```csharp
// Geef het pad naar uw bronafbeeldingsbestand op
string filePath = "sample.png";

// Definieer de uitvoermap en bestandsnaam voor de ondertekende afbeelding
string outputDirectory = "Your Document Directory";
string outputFilePath = Path.Combine(outputDirectory, "SignImageWithMetadata", "SignedWithMetadata.png");

// Zorg ervoor dat de uitvoermap bestaat
Directory.CreateDirectory(Path.GetDirectoryName(outputFilePath));
```

## Stap 2: Initialiseer het handtekeningobject

Maak een instantie van de Signature-klasse met uw bronafbeeldingsbestand:

```csharp
using (Signature signature = new Signature(filePath))
{
    // De rest van de code komt hier
}
```

## Stap 3: Metadatahandtekeningen maken en configureren

Definieer vervolgens de metadata die u in de afbeelding wilt insluiten. GroupDocs.Signature ondersteunt verschillende gegevenstypen voor metadata:

```csharp
// Initialiseer metadata-ID (specifiek voor afbeeldingsformaat)
ushort imgsMetadataId = 41996;

// Metadata-optiesobject maken
MetadataSignOptions options = new MetadataSignOptions();

// Voeg verschillende soorten metadatahandtekeningen toe
options
    .Add(new ImageMetadataSignature(imgsMetadataId++, "Mr.Sherlock Holmes"))  // Stringwaarde
    .Add(new ImageMetadataSignature(imgsMetadataId++, DateTime.Now))          // Datum Tijdwaarde
    .Add(new ImageMetadataSignature(imgsMetadataId++, 123456))                // Gehele waarde
    .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456D))              // Dubbele waarde
    .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456M))              // Decimale waarde
    .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456F));             // Vlotterwaarde
```

## Stap 4: Onderteken de afbeelding met metagegevens

Pas de metadatahandtekeningen toe op de afbeelding en sla het resultaat op:

```csharp
// Onderteken het document en sla het op in het pad van het uitvoerbestand
SignResult result = signature.Sign(outputFilePath, options);

// Succesbericht weergeven
Console.WriteLine($"\nSource image signed successfully with {result.Succeeded.Count} metadata signature(s).");
Console.WriteLine($"Signed image saved at: {outputFilePath}");
```

## Volledig voorbeeld

Hier is het volledige codevoorbeeld dat alle stappen samenbrengt:

```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;

namespace SignImageWithMetadataExample
{
    class Program
    {
        static void Main(string[] args)
        {
            // Geef bestandspaden op
            string filePath = "sample.png";            
            string outputFilePath = Path.Combine("Your Document Directory", "SignImageWithMetadata", "SignedWithMetadata.png");
            
            // Zorg ervoor dat de uitvoermap bestaat
            Directory.CreateDirectory(Path.GetDirectoryName(outputFilePath));

            // Onderteken de afbeelding met metagegevens
            using (Signature signature = new Signature(filePath))
            {
                // Initialiseer metadata-ID (specifiek voor afbeeldingsformaat)
                ushort imgsMetadataId = 41996;
                
                // Metagegevensopties maken
                MetadataSignOptions options = new MetadataSignOptions();
                
                // Verschillende soorten metadatahandtekeningen toevoegen
                options
                    .Add(new ImageMetadataSignature(imgsMetadataId++, "Mr.Sherlock Holmes")) // Stringwaarde
                    .Add(new ImageMetadataSignature(imgsMetadataId++, DateTime.Now))          // Datum Tijdwaarde
                    .Add(new ImageMetadataSignature(imgsMetadataId++, 123456))                // Gehele waarde
                    .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456D))              // Dubbele waarde
                    .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456M))              // Decimale waarde
                    .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456F));             // Vlotterwaarde
                
                // Document ondertekenen en opslaan in bestand
                SignResult result = signature.Sign(outputFilePath, options);
                
                // Resultaten weergeven
                Console.WriteLine($"\nSource image signed successfully with {result.Succeeded.Count} signature(s).");
                Console.WriteLine($"File saved at {outputFilePath}.");
            }
        }
    }
}
```

## Geavanceerde technieken voor metadata-ondertekening

### Werken met aangepaste metagegevens

U kunt ook aangepaste metagegevensvelden maken met specifieke ID's:

```csharp
// Aangepaste metagegevens maken met een specifieke ID
options.Add(new ImageMetadataSignature(42000, "CustomValue"));
```

### Metadata-handtekeningen verifiëren

Nadat u hebt ondertekend, wilt u mogelijk de metadatahandtekeningen verifiëren:

```csharp
// Verificatieopties aanmaken
MetadataSearchOptions searchOptions = new MetadataSearchOptions();

// Zoeken naar metadatahandtekeningen
SearchResult result = signature.Search(searchOptions);

// Gevonden handtekeningen weergeven
Console.WriteLine($"Found {result.Signatures.Count} metadata signatures:");
foreach(var metadataSignature in result.Signatures)
{
    Console.WriteLine($"- {metadataSignature.Name}: {metadataSignature.Value}");
}
```

## Conclusie

In deze tutorial heb je geleerd hoe je afbeeldingen kunt ondertekenen met metadata met behulp van GroupDocs.Signature voor .NET. Het insluiten van metadata in afbeeldingen biedt een uitstekende manier om de authenticiteit van afbeeldingen te verbeteren, essentiële informatie toe te voegen en workflows voor documentbeheer te verbeteren. Het proces is eenvoudig maar krachtig en biedt mogelijkheden voor aanpassing aan je specifieke vereisten.

De metadata die in het afbeeldingsbestand zijn opgenomen, kunnen voor verschillende doeleinden worden gebruikt, zoals auteursrechtbescherming, het traceren van de herkomst van de afbeelding, het toevoegen van beschrijvende informatie en het vaststellen van een digitale bewaarketen. Door metadatahandtekeningen te implementeren, kunt u ervoor zorgen dat uw afbeeldingen hun integriteit en authenticiteit gedurende hun hele levenscyclus behouden.

## Veelgestelde vragen

### Kan ik metadata toevoegen aan bestaande ondertekende afbeeldingen?

Ja, u kunt extra metadata toevoegen aan afbeeldingen die al een metadatahandtekening bevatten. De bestaande metadata blijft behouden en nieuwe metadata wordt dienovereenkomstig toegevoegd.

### Welke afbeeldingsformaten worden ondersteund voor metadataondertekening?

GroupDocs.Signature voor .NET ondersteunt metadataondertekening voor diverse afbeeldingsformaten, waaronder PNG, JPEG, TIFF, BMP, GIF en meer. Raadpleeg de [officiële documentatie](https://docs.groupdocs.com/signature/net/).

### Is het mogelijk om de metadata van afbeeldingen te versleutelen?

Ja, GroupDocs.Signature biedt opties om metadata te versleutelen voor extra beveiliging. U kunt de versleutelingsopties van de bibliotheek gebruiken om gevoelige metadata te beschermen.

### Kan ik de authenticiteit van ondertekende afbeeldingen programmatisch valideren?

Absoluut. U kunt de verificatiemethoden in GroupDocs.Signature gebruiken om metadatahandtekeningen te valideren en de authenticiteit van ondertekende afbeeldingen te bevestigen.

### Is er een beperking op de bestandsgrootte bij het ondertekenen van afbeeldingen met metagegevens?

De bibliotheek zelf stelt geen specifieke limiet aan de bestandsgrootte, maar zeer grote bestanden vereisen mogelijk meer verwerkingstijd en geheugen. Het is raadzaam om rekening te houden met de systeembronnen bij het werken met extreem grote afbeeldingen.

### Hoe kan ik een tijdelijke licentie krijgen voor testdoeleinden?

U kunt een [tijdelijke licentie](https://purchase.groupdocs.com/temporary-license/) om GroupDocs.Signature te testen voordat u tot aankoop overgaat.

### Waar kan ik meer informatie en ondersteuning vinden?

- [API-referentie](https://reference.groupdocs.com/signature/net/)
- [Downloaden](https://releases.groupdocs.com/signature/net/)
- [Voorbeelden](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
- [Documentatie](https://docs.groupdocs.com/signature/net/)
- [Productpagina](https://products.groupdocs.com/signature/net/)
- [Blog](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
- [Ondersteuningsforum](https://forum.groupdocs.com/c/signature/13)