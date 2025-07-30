---
"description": "Integreer metadatahandtekeningen in PDF-documenten met GroupDocs.Signature voor .NET. Leer hoe u auteursinformatie, tijdstempels en aangepaste gegevens kunt insluiten om de authenticiteit en traceerbaarheid van PDF's te verbeteren."
"linktitle": "PDF ondertekenen met metagegevens"
"second_title": "GroupDocs.Signature .NET API"
"title": "Metadata-handtekeningen toevoegen aan PDF-documenten in C# .NET"
"url": "/nl/net/document-signing/sign-pdf-with-metadata/"
"weight": 11
---

## Invoering

PDF-documenten (Portable Document Format) worden veel gebruikt in verschillende sectoren vanwege hun consistentie en platformonafhankelijkheid. Het waarborgen van de authenticiteit en traceerbaarheid van deze documenten is cruciaal in veel professionele omgevingen. Een effectieve manier om dit te bereiken, is door metadata in de PDF-bestanden zelf in te sluiten.

In deze uitgebreide tutorial laten we zien hoe je PDF-documenten kunt ondertekenen met metadata met behulp van GroupDocs.Signature voor .NET. Met metadatahandtekeningen kun je extra informatie in het document insluiten, zoals auteursgegevens, tijdstempels van aanmaak, document-ID's en aangepaste waarden, zonder de weergave van het document zichtbaar te veranderen.

## Vereisten

Voordat we beginnen, zorg ervoor dat u het volgende geregeld heeft:

1. [GroupDocs.Signature voor .NET](https://releases.groupdocs.com/signature/net/) - Download en installeer de bibliotheek
2. Ontwikkelomgeving - Visual Studio of een andere .NET-compatibele IDE
3. PDF-document - Een voorbeeld-PDF-bestand voor ondertekening
4. Basiskennis van C# - Kennis van de programmeertaal C#

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

Definieer eerst het pad naar uw PDF-document en geef aan waar u de ondertekende uitvoer wilt opslaan:

```csharp
// Geef het pad naar uw PDF-document op
string filePath = "sample.pdf";

// Definieer de uitvoermap en het bestandspad
string outputDirectory = "Your Document Directory";
string outputFilePath = Path.Combine(outputDirectory, "SignPdfWithMetadata", "SignedWithMetadata.pdf");

// Zorg ervoor dat de uitvoermap bestaat
Directory.CreateDirectory(Path.GetDirectoryName(outputFilePath));
```

## Stap 2: Initialiseer het handtekeningobject

Maak een instantie van de Signature-klasse met uw bron-PDF-document:

```csharp
using (Signature signature = new Signature(filePath))
{
    // De code voor ondertekening komt hier
}
```

## Stap 3: Metagegevensopties definiëren

Maak en configureer de metagegevensopties en voeg verschillende typen metagegevenshandtekeningen toe:

```csharp
// Metadata-optiesobject maken
MetadataSignOptions options = new MetadataSignOptions();

// Voeg verschillende soorten metagegevens toe met behulp van de vloeiende interface
options
    .Add(new PdfMetadataSignature("Author", "Mr.Sherlock Holmes")) // Stringwaarde
    .Add(new PdfMetadataSignature("CreatedOn", DateTime.Now))       // Datum/tijd-waarde
    .Add(new PdfMetadataSignature("DocumentId", 123456))            // Gehele waarde
    .Add(new PdfMetadataSignature("SignatureId", 123.456D))         // Dubbele waarde
    .Add(new PdfMetadataSignature("Amount", 123.456M))              // Decimale waarde
    .Add(new PdfMetadataSignature("Total", 123.456F));              // Vlotterwaarde
```

## Stap 4: Onderteken de PDF met metagegevens

Pas de metadatahandtekeningen toe op het PDF-document en sla het resultaat op:

```csharp
// Onderteken het document en sla het op in het uitvoerpad
SignResult result = signature.Sign(outputFilePath, options);

// Succesbericht weergeven
Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} metadata signature(s).");
Console.WriteLine($"Signed document saved at: {outputFilePath}");
```

## Volledig voorbeeld

Hier is het volledige codevoorbeeld dat alle stappen samenbrengt:

```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;

namespace SignPdfWithMetadataExample
{
    class Program
    {
        static void Main(string[] args)
        {
            // Geef bestandspaden op
            string filePath = "sample.pdf";
            string outputFilePath = Path.Combine("Your Document Directory", "SignPdfWithMetadata", "SignedWithMetadata.pdf");
            
            // Zorg ervoor dat de uitvoermap bestaat
            Directory.CreateDirectory(Path.GetDirectoryName(outputFilePath));

            // Onderteken de PDF met metagegevens
            using (Signature signature = new Signature(filePath))
            {
                // Metadata-optiesobject maken
                MetadataSignOptions options = new MetadataSignOptions();
                
                // Verschillende soorten metadatahandtekeningen toevoegen
                options
                    .Add(new PdfMetadataSignature("Author", "Mr.Sherlock Holmes")) // Stringwaarde
                    .Add(new PdfMetadataSignature("CreatedOn", DateTime.Now))       // Datum/tijd-waarde
                    .Add(new PdfMetadataSignature("DocumentId", 123456))            // Gehele waarde
                    .Add(new PdfMetadataSignature("SignatureId", 123.456D))         // Dubbele waarde
                    .Add(new PdfMetadataSignature("Amount", 123.456M))              // Decimale waarde
                    .Add(new PdfMetadataSignature("Total", 123.456F));              // Vlotterwaarde
                
                // Document ondertekenen en opslaan in bestand
                SignResult result = signature.Sign(outputFilePath, options);
                
                // Resultaten weergeven
                Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).");
                Console.WriteLine($"File saved at {outputFilePath}.");
            }
        }
    }
}
```

## Geavanceerde PDF-metadatabewerkingen

### Aangepaste metagegevens toevoegen met naamruimteondersteuning

PDF-documenten ondersteunen aangepaste metagegevens met XML-naamruimteondersteuning:

```csharp
// Aangepaste metagegevens toevoegen met naamruimte
options.Add(new PdfMetadataSignature("CustomProperty", "Custom Value")
{
    NamespaceUri = "http://uw-naamruimte.com/schema"
});
```

### Zoeken naar metagegevens in ondertekende PDF's

Nadat u hebt ondertekend, wilt u mogelijk de metagegevens verifiëren of extraheren:

```csharp
// Zoekopties voor metadata maken
MetadataSearchOptions searchOptions = new MetadataSearchOptions();

// Zoeken naar metadatahandtekeningen
SearchResult searchResult = signature.Search(searchOptions);

// Gevonden handtekeningen weergeven
Console.WriteLine($"Found {searchResult.Signatures.Count} metadata signatures:");
foreach (var foundSignature in searchResult.Signatures)
{
    MetadataSignature metadataSignature = foundSignature as MetadataSignature;
    if (metadataSignature != null)
    {
        Console.WriteLine($"- {metadataSignature.Name}: {metadataSignature.Value} ({metadataSignature.Value.GetType().Name})");
    }
}
```

### Werken met standaard PDF-metagegevens

PDF-documenten hebben standaardmetagegevensvelden die u kunt openen en wijzigen:

```csharp
// Standaard PDF-metagegevensvelden instellen
options
    .Add(new PdfMetadataSignature("Title", "Important Contract"))
    .Add(new PdfMetadataSignature("Subject", "Legal Agreement"))
    .Add(new PdfMetadataSignature("Keywords", "contract, agreement, legal, binding"))
    .Add(new PdfMetadataSignature("Creator", "Legal Department"))
    .Add(new PdfMetadataSignature("Producer", "GroupDocs.Signature"));
```

## Conclusie

In deze tutorial heb je geleerd hoe je PDF-documenten kunt ondertekenen met metadata met behulp van GroupDocs.Signature voor .NET. Het insluiten van metadata in PDF-bestanden biedt een uitstekende manier om de authenticiteit van documenten te verbeteren, belangrijke informatie toe te voegen en workflows voor documentbeheer te verbeteren.

Metadatahandtekeningen in PDF's zijn met name waardevol in zakelijke omgevingen waar documenttraceerbaarheid en authenticiteitsverificatie essentieel zijn. De ingesloten metadata kunnen informatie bevatten over de oorsprong, auteur, aanmaaktijd, versie en aangepaste eigenschappen van het document die relevant zijn voor de workflow van uw organisatie.

Door metadatahandtekeningen te implementeren met GroupDocs.Signature, kunt u ervoor zorgen dat uw PDF-documenten hun integriteit behouden en verifieerbare informatie bieden gedurende hun levenscyclus.

## Veelgestelde vragen

### Kan ik bestaande metagegevens in een PDF-document wijzigen?

Ja, u kunt bestaande metadata in PDF-documenten wijzigen. Wanneer u nieuwe metadatahandtekeningen met dezelfde namen als bestaande toepast, worden de waarden dienovereenkomstig bijgewerkt.

### Zijn metadatahandtekeningen in PDF-documenten zichtbaar voor de eindgebruiker?

Metadatahandtekeningen zijn niet zichtbaar in de documentinhoud zelf. Ze kunnen echter wel worden bekeken via het paneel met documenteigenschappen in PDF-readers zoals Adobe Acrobat of met behulp van speciale tools voor het bekijken van metadata.

### Kan ik de metagegevens in PDF's versleutelen of beveiligen?

GroupDocs.Signature biedt opties voor het beveiligen van documenten, waaronder encryptie. U kunt encryptie op documentniveau toepassen om de volledige PDF te beveiligen, inclusief de metadata.

### Is er een limiet aan de hoeveelheid metadata die ik aan een PDF kan toevoegen?

Hoewel de PDF-specificatie geen strikte limiet stelt, kan het toevoegen van te veel metadata de bestandsgrootte vergroten. Het is raadzaam om alleen relevante en noodzakelijke informatie in de metadata op te nemen.

### Kan ik programmatisch valideren of er met een PDF is geknoeid nadat ik metagegevens heb toegevoegd?

Ja, GroupDocs.Signature biedt verificatiemogelijkheden waarmee kan worden vastgesteld of een document na ondertekening is gewijzigd, inclusief wijzigingen in metagegevens.

### Waar kan ik meer informatie en ondersteuning vinden?

- [API-referentie](https://reference.groupdocs.com/signature/net/)
- [Downloaden](https://releases.groupdocs.com/signature/net/)
- [Voorbeelden](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
- [Documentatie](https://docs.groupdocs.com/signature/net/)
- [Productpagina](https://products.groupdocs.com/signature/net/)
- [Blog](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
- [Ondersteuningsforum](https://forum.groupdocs.com/c/signature/13)
- [Tijdelijke licentie](https://purchase.groupdocs.com/temporary-license/)