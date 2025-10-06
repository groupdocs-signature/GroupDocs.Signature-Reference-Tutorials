---
"description": "Bescherm en verbeter Excel-spreadsheets door metadatahandtekeningen in te sluiten met GroupDocs.Signature voor .NET. Voeg auteursinformatie, tijdstempels en aangepaste gegevens toe om de traceerbaarheid en authenticiteit van documenten te verbeteren."
"linktitle": "Onderteken spreadsheet met metagegevens"
"second_title": "GroupDocs.Signature .NET API"
"title": "Metadata-handtekeningen toevoegen aan Excel-spreadsheets in C# .NET"
"url": "/nl/net/document-signing/sign-spreadsheet-with-metadata/"
"weight": 13
type: docs
---
## Invoering

Excel-spreadsheets bevatten vaak cruciale bedrijfsgegevens, financiële informatie en belangrijke berekeningen. Het waarborgen van de authenticiteit, het traceren van de herkomst en het beschermen van de integriteit ervan is cruciaal in veel professionele omgevingen. Een effectieve manier om de beveiliging en traceerbaarheid van spreadsheets te verbeteren, is door metadatahandtekeningen in te bouwen.

Deze uitgebreide tutorial begeleidt u door het proces van het ondertekenen van Excel-spreadsheets met metadata met behulp van GroupDocs.Signature voor .NET. Door metadatahandtekeningen toe te voegen, kunt u waardevolle informatie zoals auteursgegevens, tijdstempels van aanmaak, document-ID's en andere aangepaste eigenschappen rechtstreeks in de spreadsheetstructuur insluiten.

## Vereisten

Voordat u met deze tutorial begint, moet u ervoor zorgen dat u over het volgende beschikt:

1. [GroupDocs.Signature voor .NET](https://releases.groupdocs.com/signature/net/) - Download en installeer de bibliotheek
2. Ontwikkelomgeving - Visual Studio of een andere .NET-compatibele IDE
3. Excel-spreadsheet - Een voorbeeld van een spreadsheetbestand (XLSX, XLS, enz.)
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

Definieer de paden voor uw bronspreadsheet en waar de ondertekende uitvoer moet worden opgeslagen:

```csharp
// Geef het pad naar uw Excel-bestand op
string filePath = "sample.xlsx";

// Definieer de uitvoermap en bestandsnaam voor het ondertekende spreadsheet
string outputDirectory = "Your Document Directory";
string outputFilePath = Path.Combine(outputDirectory, "SignSpreadsheetWithMetadata", "SignedWithMetadata.xlsx");

// Zorg ervoor dat de uitvoermap bestaat
Directory.CreateDirectory(Path.GetDirectoryName(outputFilePath));
```

## Stap 2: Initialiseer het handtekeningobject

Maak een instantie van de Signature-klasse met uw bronspreadsheetbestand:

```csharp
using (Signature signature = new Signature(filePath))
{
    // De rest van de code komt hier
}
```

## Stap 3: Metadatahandtekeningen maken en configureren

Definieer vervolgens de metagegevensopties en maak een reeks spreadsheetmetagegevenshandtekeningen:

```csharp
// Metadata-optiesobject maken
MetadataSignOptions options = new MetadataSignOptions();

// Maak een reeks spreadsheet-metadatahandtekeningen met verschillende gegevenstypen
SpreadsheetMetadataSignature[] signatures = new SpreadsheetMetadataSignature[]
{
    new SpreadsheetMetadataSignature("Author", "Mr.Sherlock Holmes"), // Stringwaarde
    new SpreadsheetMetadataSignature("CreatedOn", DateTime.Now),      // Datum/tijd-waarde
    new SpreadsheetMetadataSignature("DocumentId", 123456),           // Gehele waarde
    new SpreadsheetMetadataSignature("SignatureId", 123.456D),        // Dubbele waarde
    new SpreadsheetMetadataSignature("Amount", 123.456M),             // Decimale waarde
    new SpreadsheetMetadataSignature("Total", 123.456F)               // Vlotterwaarde
};

// Voeg handtekeningencollectie toe aan opties
options.Signatures.AddRange(signatures);
```

## Stap 4: Onderteken het spreadsheet met metagegevens

Pas de metadatahandtekeningen toe op het spreadsheet en sla het resultaat op:

```csharp
// Onderteken het document en sla het op in het pad van het uitvoerbestand
SignResult result = signature.Sign(outputFilePath, options);

// Succesbericht weergeven
Console.WriteLine($"\nSource spreadsheet signed successfully with {result.Succeeded.Count} metadata signature(s).");
Console.WriteLine($"Signed spreadsheet saved at: {outputFilePath}");
```

## Volledig voorbeeld

Hier is het volledige codevoorbeeld dat alle stappen samenbrengt:

```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;

namespace SignSpreadsheetWithMetadataExample
{
    class Program
    {
        static void Main(string[] args)
        {
            // Geef bestandspaden op
            string filePath = "sample.xlsx";
            string outputFilePath = Path.Combine("Your Document Directory", "SignSpreadsheetWithMetadata", "SignedWithMetadata.xlsx");
            
            // Zorg ervoor dat de uitvoermap bestaat
            Directory.CreateDirectory(Path.GetDirectoryName(outputFilePath));

            // Onderteken het spreadsheet met metagegevens
            using (Signature signature = new Signature(filePath))
            {
                // Metadata-optiesobject maken
                MetadataSignOptions options = new MetadataSignOptions();
                
                // Maak een reeks spreadsheet-metadatahandtekeningen met verschillende gegevenstypen
                SpreadsheetMetadataSignature[] signatures = new SpreadsheetMetadataSignature[]
                {
                    new SpreadsheetMetadataSignature("Author", "Mr.Sherlock Holmes"), // Stringwaarde
                    new SpreadsheetMetadataSignature("CreatedOn", DateTime.Now),      // Datum/tijd-waarde
                    new SpreadsheetMetadataSignature("DocumentId", 123456),           // Gehele waarde
                    new SpreadsheetMetadataSignature("SignatureId", 123.456D),        // Dubbele waarde
                    new SpreadsheetMetadataSignature("Amount", 123.456M),             // Decimale waarde
                    new SpreadsheetMetadataSignature("Total", 123.456F)               // Vlotterwaarde
                };
                
                // Voeg handtekeningencollectie toe aan opties
                options.Signatures.AddRange(signatures);
                
                // Document ondertekenen en opslaan in bestand
                SignResult result = signature.Sign(outputFilePath, options);
                
                // Resultaten weergeven
                Console.WriteLine($"\nSource spreadsheet signed successfully with {result.Succeeded.Count} signature(s).");
                Console.WriteLine($"File saved at {outputFilePath}.");
            }
        }
    }
}
```

## Geavanceerde spreadsheet-metadatatechnieken

### Werken met aangepaste en ingebouwde spreadsheeteigenschappen

Excel-spreadsheets hebben zowel ingebouwde als aangepaste eigenschappen die toegankelijk zijn via het dialoogvenster Bestandseigenschappen. Met GroupDocs.Signature kunt u met beide werken:

```csharp
// Ingebouwde eigenschappen toevoegen
signatures = new SpreadsheetMetadataSignature[]
{
    new SpreadsheetMetadataSignature("Company", "Sherlock Holmes Consulting"),
    new SpreadsheetMetadataSignature("Category", "Financial"),
    new SpreadsheetMetadataSignature("Keywords", "budget,forecast,analysis"),
    new SpreadsheetMetadataSignature("Comments", "This spreadsheet contains confidential information"),
    new SpreadsheetMetadataSignature("Manager", "John Watson")
};
options.Signatures.AddRange(signatures);

// Aangepaste eigenschappen toevoegen
options.Signatures.Add(new SpreadsheetMetadataSignature("Department", "Finance"));
options.Signatures.Add(new SpreadsheetMetadataSignature("SecurityLevel", "Confidential"));
```

### Zoeken naar metagegevens in ondertekende spreadsheets

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

### Bestaande metagegevens bijwerken

U kunt bestaande metagegevens in spreadsheets bijwerken door dezelfde eigenschapsnamen te gebruiken:

```csharp
// Bestaande metagegevens bijwerken
options.Signatures.Add(new SpreadsheetMetadataSignature("Author", "Updated Author Name"));
```

## Conclusie

In deze uitgebreide tutorial hebt u geleerd hoe u Excel-spreadsheets kunt ondertekenen met metadata met behulp van GroupDocs.Signature voor .NET. Het insluiten van metadata in spreadsheetbestanden verbetert de traceerbaarheid van documenten, biedt waardevolle context en helpt bij het vaststellen van de authenticiteit.

Metadatahandtekeningen in spreadsheets zijn met name nuttig in zakelijke omgevingen waar de herkomst, het auteurschap en de versieregistratie van documenten belangrijk zijn. De ingesloten metadata kunnen informatie bevatten over de auteur, de aanmaaktijd, document-ID's en aangepaste eigenschappen die relevant zijn voor de behoeften van uw organisatie.

Door metagegevenshandtekeningen te implementeren met GroupDocs.Signature, kunt u ervoor zorgen dat uw Excel-spreadsheets hun integriteit behouden en verifieerbare informatie bieden gedurende hun levenscyclus.

## Veelgestelde vragen

### Kan ik metagegevens toevoegen aan spreadsheets waarin al eigenschappen zijn gedefinieerd?

Ja, u kunt nieuwe metadata toevoegen of bestaande metadata in spreadsheets bijwerken. GroupDocs.Signature verzorgt de integratie door nieuwe eigenschappen toe te voegen of bestaande eigenschappen met dezelfde naam bij te werken.

### Welke spreadsheetformaten worden ondersteund voor metadataondertekening?

GroupDocs.Signature voor .NET ondersteunt metadataondertekening voor verschillende spreadsheetformaten, waaronder XLSX, XLS, XLSM, ODS en meer. Raadpleeg de [officiële documentatie](https://docs.groupdocs.com/signature/net/).

### Zijn metadatahandtekeningen in spreadsheets zichtbaar voor de gebruikers?

Metadatahandtekeningen zijn niet zichtbaar in de spreadsheet zelf. Ze zijn echter wel te bekijken via het paneel met documenteigenschappen in Excel of andere compatibele applicaties.

### Kan ik programmatisch valideren of er met een spreadsheet is geknoeid nadat ik metagegevens heb toegevoegd?

Ja, GroupDocs.Signature biedt verificatiemogelijkheden waarmee kan worden vastgesteld of een document na ondertekening is gewijzigd, inclusief wijzigingen in metagegevens.

### Heeft het toevoegen van metagegevens invloed op de functionaliteit van een spreadsheet?

Het toevoegen van metadata heeft minimale impact op de bestandsgrootte en geen invloed op de functionaliteit van spreadsheets. Het is een eenvoudige manier om documenteigenschappen te verbeteren zonder dat dit gevolgen heeft voor berekeningen, formules of andere Excel-functies.

### Waar kan ik meer informatie en ondersteuning vinden?

- [API-referentie](https://reference.groupdocs.com/signature/net/)
- [Downloaden](https://releases.groupdocs.com/signature/net/)
- [Voorbeelden](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
- [Documentatie](https://docs.groupdocs.com/signature/net/)
- [Productpagina](https://products.groupdocs.com/signature/net/)
- [Blog](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
- [Ondersteuningsforum](https://forum.groupdocs.com/c/signature/13)
- [Tijdelijke licentie](https://purchase.groupdocs.com/temporary-license/)