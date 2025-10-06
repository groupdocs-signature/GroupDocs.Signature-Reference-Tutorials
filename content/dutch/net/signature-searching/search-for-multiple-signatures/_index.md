---
"description": "Leer hoe u met GroupDocs.Signature voor .NET naar meerdere handtekeningtypen in documenten kunt zoeken. Uitgebreide handleiding met codevoorbeelden voor verbeterde documentbeveiliging."
"linktitle": "Zoeken naar meerdere handtekeningen"
"second_title": "GroupDocs.Signature .NET API"
"title": "Zoeken naar meerdere handtekeningtypen in documenten"
"url": "/nl/net/signature-searching/search-for-multiple-signatures/"
"weight": 14
type: docs
---
## Invoering

In moderne documentmanagementsystemen wordt de mogelijkheid om meerdere handtekeningtypen binnen één document te zoeken en te valideren steeds belangrijker. Organisaties gebruiken vaak verschillende handtekeningtypen – zoals digitale handtekeningen, teksthandtekeningen, barcodes, QR-codes en meer – om de documentbeveiliging te verbeteren en verificatieprocessen te stroomlijnen. GroupDocs.Signature voor .NET biedt een krachtig framework waarmee ontwikkelaars uitgebreide zoekfunctionaliteit voor handtekeningen kunnen implementeren in verschillende documentformaten.

In deze tutorial wordt u door het proces van het zoeken naar meerdere handtekeningtypen in documenten met behulp van GroupDocs.Signature voor .NET geleid. De tutorial biedt gedetailleerde uitleg en praktische codevoorbeelden.

## Vereisten

Voordat u begint met het implementeren van de functionaliteit voor zoeken met meerdere handtekeningen, moet u ervoor zorgen dat u aan de volgende vereisten voldoet:

1. Ontwikkelomgeving: Visual Studio of een andere gewenste .NET-ontwikkelomgeving die op uw systeem is geïnstalleerd.
  
2. GroupDocs.Signature voor .NET: Download en installeer de GroupDocs.Signature voor .NET-bibliotheek van [hier](https://releases.groupdocs.com/signature/net/).

3. Basiskennis van C#: Kennis van de programmeertaal C# en concepten van het .NET Framework.

4. Voorbeelddocumenten: bereid testdocumenten voor met verschillende typen handtekeningen voor testdoeleinden.

## Naamruimten importeren

Begin met het importeren van de benodigde naamruimten om toegang te krijgen tot de GroupDocs.Signature-functionaliteit:

```csharp
using System;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

Laten we het proces van het zoeken naar meerdere handtekeningtypen opsplitsen in duidelijke, beheersbare stappen:

## Stap 1: Het document laden

Laad eerst het document met de handtekeningen die u wilt doorzoeken:

```csharp
string filePath = "sample_multiple_signatures.docx";
using (Signature signature = new Signature(filePath))
{
    // Hier wordt een zoekcode voor meerdere handtekeningen toegevoegd
}
```

## Stap 2: Zoekopties definiëren voor verschillende handtekeningtypen

Maak zoekopties voor elk type handtekening waarnaar u wilt zoeken:

```csharp
// Zoekopties voor teksthandtekeningen definiëren
TextSearchOptions textOptions = new TextSearchOptions
{
    AllPages = true,  // Zoeken op alle pagina's
    Text = "Signature",  // Optioneel: tekst om te vinden
    MatchType = TextMatchType.Contains  // Overeenkomende criteria
};

// Zoekopties voor digitale handtekeningen definiëren
DigitalSearchOptions digitalOptions = new DigitalSearchOptions
{
    AllPages = true
};

// Zoekopties voor barcodehandtekeningen definiëren
BarcodeSearchOptions barcodeOptions = new BarcodeSearchOptions
{
    AllPages = true,
    Text = "123456",  // Optioneel: barcodetekst om te matchen
    MatchType = TextMatchType.Exact  // Overeenkomende criteria
};

// Zoekopties voor QR-codehandtekeningen definiëren
QrCodeSearchOptions qrCodeOptions = new QrCodeSearchOptions
{
    AllPages = true,
    Text = "John",  // Optioneel: QR-codetekst om te matchen
    MatchType = TextMatchType.Contains  // Overeenkomende criteria
};

// Zoekopties voor metadatahandtekeningen definiëren
MetadataSearchOptions metadataOptions = new MetadataSearchOptions();
```

## Stap 3: Opties toevoegen aan een collectie

Voeg alle zoekopties toe aan een verzameling:

```csharp
// Maak een lijst om alle zoekopties in op te slaan
List<SearchOptions> searchOptions = new List<SearchOptions>
{
    textOptions,
    digitalOptions,
    barcodeOptions,
    qrCodeOptions,
    metadataOptions
};
```

## Stap 4: Zoekopdracht uitvoeren en resultaten verwerken

Voer de zoekopdracht uit met behulp van de gecombineerde zoekopties en verwerk de resultaten:

```csharp
// Zoek naar alle handtekeningtypen met behulp van de gedefinieerde opties
SearchResult result = signature.Search(searchOptions);

// Controleer of er handtekeningen zijn gevonden
if (result.Signatures.Count > 0)
{
    Console.WriteLine($"\nSource document ['{filePath}'] contains {result.Signatures.Count} signature(s):");
    
    // Herhaal de gevonden handtekeningen
    foreach (var foundSignature in result.Signatures)
    {
        Console.WriteLine($"Signature found: Type: {foundSignature.SignatureType}, Page: {foundSignature.PageNumber}, ID: {foundSignature.SignatureId}");
        
        // Processpecifieke handtekeningtypen
        if (foundSignature is TextSignature textSignature)
        {
            Console.WriteLine($"Text: '{textSignature.Text}'");
        }
        else if (foundSignature is BarcodeSignature barcodeSignature)
        {
            Console.WriteLine($"Barcode Type: {barcodeSignature.EncodeType.TypeName}, Text: '{barcodeSignature.Text}'");
        }
        else if (foundSignature is QrCodeSignature qrCodeSignature)
        {
            Console.WriteLine($"QR Code Type: {qrCodeSignature.EncodeType.TypeName}, Text: '{qrCodeSignature.Text}'");
        }
        else if (foundSignature is DigitalSignature digitalSignature)
        {
            Console.WriteLine($"Certificate: {digitalSignature.Certificate?.SubjectName}, Valid: {digitalSignature.IsValid}");
        }
        else if (foundSignature is MetadataSignature metadataSignature)
        {
            Console.WriteLine($"Metadata: Name: {metadataSignature.Name}, Value: {metadataSignature.Value}");
        }
    }
}
else
{
    Console.WriteLine("No signatures were found in the document.");
}
```

## Volledig voorbeeld

Hier is een volledig, werkend voorbeeld dat laat zien hoe u naar meerdere handtekeningtypen in een document kunt zoeken:

```csharp
using System;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;

namespace MultiSignatureSearch
{
    class Program
    {
        static void Main(string[] args)
        {
            // Documentpad
            string filePath = "sample_multiple_signatures.docx";
            
            // Initialiseer Signature-instantie
            using (Signature signature = new Signature(filePath))
            {
                try
                {
                    // Zoekopties voor teksthandtekeningen definiëren
                    TextSearchOptions textOptions = new TextSearchOptions
                    {
                        AllPages = true,
                        MatchType = TextMatchType.Contains
                    };

                    // Zoekopties voor digitale handtekeningen definiëren
                    DigitalSearchOptions digitalOptions = new DigitalSearchOptions
                    {
                        AllPages = true
                    };

                    // Zoekopties voor barcodehandtekeningen definiëren
                    BarcodeSearchOptions barcodeOptions = new BarcodeSearchOptions
                    {
                        AllPages = true
                    };

                    // Zoekopties voor QR-codehandtekeningen definiëren
                    QrCodeSearchOptions qrCodeOptions = new QrCodeSearchOptions
                    {
                        AllPages = true
                    };

                    // Zoekopties voor metadatahandtekeningen definiëren
                    MetadataSearchOptions metadataOptions = new MetadataSearchOptions();

                    // Maak een lijst om alle zoekopties in op te slaan
                    List<SearchOptions> searchOptions = new List<SearchOptions>
                    {
                        textOptions,
                        digitalOptions,
                        barcodeOptions,
                        qrCodeOptions,
                        metadataOptions
                    };

                    // Zoeken naar alle handtekeningtypen
                    SearchResult result = signature.Search(searchOptions);

                    // Controleer of er handtekeningen zijn gevonden
                    if (result.Signatures.Count > 0)
                    {
                        Console.WriteLine($"\nSource document ['{filePath}'] contains {result.Signatures.Count} signature(s):");
                        
                        // Resultaten verwerken op handtekeningtype
                        foreach (var foundSignature in result.Signatures)
                        {
                            Console.WriteLine($"Signature found: Type: {foundSignature.SignatureType}, Page: {foundSignature.PageNumber}");
                            
                            // Processpecifieke handtekeningtypen
                            switch (foundSignature.SignatureType)
                            {
                                case SignatureType.Text:
                                    var textSignature = foundSignature as TextSignature;
                                    Console.WriteLine($"Text: '{textSignature.Text}'");
                                    break;
                                    
                                case SignatureType.Barcode:
                                    var barcodeSignature = foundSignature as BarcodeSignature;
                                    Console.WriteLine($"Barcode Type: {barcodeSignature.EncodeType.TypeName}, Text: '{barcodeSignature.Text}'");
                                    break;
                                    
                                case SignatureType.QrCode:
                                    var qrCodeSignature = foundSignature as QrCodeSignature;
                                    Console.WriteLine($"QR Code Type: {qrCodeSignature.EncodeType.TypeName}, Text: '{qrCodeSignature.Text}'");
                                    break;
                                    
                                case SignatureType.Digital:
                                    var digitalSignature = foundSignature as DigitalSignature;
                                    Console.WriteLine($"Certificate: {digitalSignature.Certificate?.SubjectName}, Valid: {digitalSignature.IsValid}");
                                    break;
                                    
                                case SignatureType.Metadata:
                                    var metadataSignature = foundSignature as MetadataSignature;
                                    Console.WriteLine($"Metadata: Name: {metadataSignature.Name}, Value: {metadataSignature.Value}");
                                    break;
                            }
                            
                            Console.WriteLine(); // Regeleinde tussen handtekeningen toevoegen
                        }
                    }
                    else
                    {
                        Console.WriteLine("No signatures were found in the document.");
                    }
                }
                catch (Exception ex)
                {
                    Console.WriteLine($"Error occurred: {ex.Message}");
                }
            }
            
            Console.WriteLine("Press any key to exit...");
            Console.ReadKey();
        }
    }
}
```

## Geavanceerde multi-signature zoektechnieken

### Zoekresultaten filteren

U kunt geavanceerde filtering implementeren om de zoekresultaten te verfijnen:

```csharp
// Filter resultaten op paginanummer
var signaturesOnFirstPage = result.Signatures.FindAll(s => s.PageNumber == 1);

// Filter resultaten op handtekeningtype
var digitalSignatures = result.Signatures.FindAll(s => s.SignatureType == SignatureType.Digital);
var qrCodeSignatures = result.Signatures.FindAll(s => s.SignatureType == SignatureType.QrCode);

// Filter teksthandtekeningen met specifieke inhoud
var approvalSignatures = result.Signatures
    .FindAll(s => s is TextSignature && ((TextSignature)s).Text.Contains("Approved"));
```

### Validatie van meerdere handtekeningen

Validatielogica implementeren voor verschillende handtekeningtypen:

```csharp
bool ValidateAllSignatures(SearchResult result)
{
    bool isDocumentValid = true;
    
    // Controleren of het document een geldige digitale handtekening heeft
    bool hasValidDigitalSignature = result.Signatures
        .Any(s => s is DigitalSignature && ((DigitalSignature)s).IsValid);
    
    if (!hasValidDigitalSignature)
    {
        Console.WriteLine("Warning: Document does not contain a valid digital signature");
        isDocumentValid = false;
    }
    
    // Controleren of het document een QR-code vereist
    bool hasRequiredQRCode = result.Signatures
        .Any(s => s is QrCodeSignature && ((QrCodeSignature)s).Text.Contains("Auth-Code"));
    
    if (!hasRequiredQRCode)
    {
        Console.WriteLine("Warning: Document does not contain the required authentication QR code");
        isDocumentValid = false;
    }
    
    return isDocumentValid;
}
```

### Zoeken met aangepaste verwerking

kunt aangepaste verwerkingslogica voor zoekopdrachten definiëren:

```csharp
// Zoekopties creëren met aangepaste verwerking
TextSearchOptions textOptions = new TextSearchOptions
{
    AllPages = true,
    
    // Aangepaste verwerking definiëren met behulp van een gedelegeerde
    ProcessCompleted = (signature) =>
    {
        // Aangepaste validatielogica: accepteer alleen handtekeningen op opgegeven pagina's
        TextSignature textSignature = signature as TextSignature;
        return textSignature != null && (textSignature.PageNumber == 1 || textSignature.PageNumber == 2);
    }
};
```

## Conclusie

In deze uitgebreide handleiding hebben we uitgelegd hoe u met GroupDocs.Signature voor .NET naar meerdere handtekeningtypen in documenten kunt zoeken. Van het instellen van zoekopties voor verschillende handtekeningtypen tot het verwerken en valideren van de resultaten: u beschikt nu over de kennis om robuuste handtekeningzoekfunctionaliteit te implementeren in uw .NET-applicaties.

De mogelijkheid om tegelijkertijd naar meerdere handtekeningtypen te zoeken, verbetert documentverificatieprocessen, versterkt beveiligingsmaatregelen en stroomlijnt documentvalidatieworkflows. GroupDocs.Signature biedt een krachtig, flexibel raamwerk voor het werken met verschillende handtekeningtypen in verschillende documentformaten, waardoor het een uitstekende keuze is voor documentverwerkingstoepassingen.

## Veelgestelde vragen

### Kan ik zoeken naar handtekeningen in documenten die met een wachtwoord zijn beveiligd?

Ja, GroupDocs.Signature ondersteunt het zoeken naar handtekeningen in wachtwoordbeveiligde documenten. U kunt het wachtwoord opgeven bij het initialiseren van de `Signature` voorwerp:

```csharp
LoadOptions loadOptions = new LoadOptions { Password = "your_password" };
using (Signature signature = new Signature(filePath, loadOptions))
{
    // Zoeken naar handtekeningen
}
```

### Welke documentformaten worden ondersteund voor het zoeken naar handtekeningen?

GroupDocs.Signature ondersteunt een breed scala aan documentformaten, waaronder PDF, Microsoft Office-documenten (Word, Excel, PowerPoint), OpenOffice-formaten, afbeeldingen en meer.

### Kan ik de zoekopdracht beperken tot specifieke pagina's in een document?

Ja, elk type zoekoptie heeft eigenschappen waarmee u kunt aangeven welke pagina's u wilt doorzoeken:

```csharp
TextSearchOptions options = new TextSearchOptions
{
    AllPages = false,  // Zoek niet op alle pagina's
    PageNumber = 1,    // Zoek alleen op pagina 1
    
    // Of geef meerdere pagina's op
    PagesSetup = new PagesSetup { Pages = new List<int> { 1, 3, 5 } }
};
```

### Hoe kan ik de prestaties optimaliseren bij het zoeken in grote documenten?

Voor grote documenten kunt u de prestaties als volgt optimaliseren:

1. Beperk de zoekopdracht tot specifieke pagina's of paginabereiken
2. Door specifiekere zoekcriteria te gebruiken om het aantal potentiële matches te verminderen
3. Paginering implementeren in uw resultatenweergave
4. Zoeken naar één handtekeningtype tegelijk als u geen gelijktijdige resultaten nodig hebt

### Kan ik GroupDocs.Signature uitbreiden zodat het aangepaste handtekeningtypen ondersteunt?

Hoewel GroupDocs.Signature ingebouwde ondersteuning biedt voor veelgebruikte handtekeningtypen, kunt u de functionaliteit ervan uitbreiden door:

1. Het creëren van aangepaste zoekoptiesklassen afgeleid van `SearchOptions`
2. Implementatie van aangepaste verwerkingslogica met behulp van de `ProcessCompleted` delegeren
3. Het ontwikkelen van wrapperklassen die meerdere handtekeningzoekopdrachten combineren met geavanceerde bedrijfslogica

## Zie ook

* [API-referentie](https://reference.groupdocs.com/signature/net/)
* [Codevoorbeelden op GitHub](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
* [Productdocumentatie](https://docs.groupdocs.com/signature/net/)
* [Productpagina](https://products.groupdocs.com/signature/net/)
* [Download de nieuwste versie](https://releases.groupdocs.com/signature/net/)
* [Blogartikelen](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
* [Gratis ondersteuningsforum](https://forum.groupdocs.com/c/signature/13)
* [Tijdelijke licentie](https://purchase.groupdocs.com/temporary-license/)