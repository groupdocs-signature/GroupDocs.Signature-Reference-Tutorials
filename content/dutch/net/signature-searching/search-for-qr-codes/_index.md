---
"description": "Leer hoe u efficiënt naar QR-codes in documenten kunt zoeken met GroupDocs.Signature voor .NET met deze uitgebreide stapsgewijze handleiding en codevoorbeelden."
"linktitle": "Zoeken naar QR-codes"
"second_title": "GroupDocs.Signature .NET API"
"title": "Zoeken naar QR-codehandtekeningen in documenten"
"url": "/nl/net/signature-searching/search-for-qr-codes/"
"weight": 15
type: docs
---
## Invoering

In het huidige digitale documentecosysteem zijn QR-codehandtekeningen een onmisbaar hulpmiddel geworden voor het integreren van informatie, authenticatie en het verbeteren van de documentbeveiliging. GroupDocs.Signature voor .NET biedt ontwikkelaars een krachtige API om QR-codes te zoeken en te extraheren uit verschillende documentformaten, wat geavanceerde documentanalyse en -verificatiemogelijkheden in .NET-applicaties mogelijk maakt.

Deze uitgebreide tutorial begeleidt u door het proces van het implementeren van QR-codezoekfunctionaliteit met behulp van GroupDocs.Signature voor .NET. De tutorial biedt duidelijke uitleg, stapsgewijze instructies en praktische codevoorbeelden die u in uw eigen toepassingen kunt integreren.

## Vereisten

Voordat u met het zoeken naar QR-codehandtekeningen aan de slag gaat, moet u ervoor zorgen dat u aan de volgende vereisten voldoet:

1. GroupDocs.Signature voor .NET SDK: Download en installeer de SDK vanaf de [downloadpagina](https://releases.groupdocs.com/signature/net/).

2. Ontwikkelomgeving: Stel een .NET-ontwikkelomgeving in, zoals Visual Studio, met .NET Framework of .NET Core geïnstalleerd.

3. Basiskennis: Kennis van C#-programmering en .NET-ontwikkelingsconcepten.

4. Voorbeelddocumenten: bereid testdocumenten voor met QR-codes voor verificatie en testen.

## Naamruimten importeren

Begin met het importeren van de benodigde naamruimten om toegang te krijgen tot de GroupDocs.Signature-functionaliteit:

```csharp
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
using System;
using System.Collections.Generic;
```

Laten we het proces van het zoeken naar QR-codes opsplitsen in duidelijke, gemakkelijk te volgen stappen:

## Stap 1: Definieer het documentpad

Geef eerst het pad op naar het document met de QR-codes waarnaar u wilt zoeken:

```csharp
string filePath = "sample_multiple_signatures.docx";
```

## Stap 2: Initialiseer het handtekeningobject

Maak een exemplaar van de `Signature` klasse door het documentpad door te geven:

```csharp
using (Signature signature = new Signature(filePath))
{
    // QR-code zoekcode wordt hier toegevoegd
}
```

## Stap 3: Zoek naar QR-codehandtekeningen

Gebruik de `Search` Methode met het juiste handtekeningstype om QR-codes in het document te vinden:

```csharp
// Zoek naar QR-codehandtekeningen in het document
List<QrCodeSignature> signatures = signature.Search<QrCodeSignature>(SignatureType.QrCode);
```

## Stap 4: Resultaten verwerken en weergeven

Loop door de gevonden QR-codehandtekeningen en krijg toegang tot hun eigenschappen:

```csharp
// Informatie weergeven over gevonden QR-codes
Console.WriteLine($"\nSource document contains {signatures.Count} QR code signature(s):");

foreach (var qrCodeSignature in signatures)
{
    Console.WriteLine($"QR Code found at page {qrCodeSignature.PageNumber} with type {qrCodeSignature.EncodeType.TypeName}");
    Console.WriteLine($"Content: {qrCodeSignature.Text}");
    Console.WriteLine($"Location: X={qrCodeSignature.Left}, Y={qrCodeSignature.Top}, Width={qrCodeSignature.Width}, Height={qrCodeSignature.Height}");
    Console.WriteLine();
}
```

## Volledig voorbeeld

Hier is een uitgebreid werkend voorbeeld dat het volledige proces van het zoeken naar QR-codes in een document demonstreert:

```csharp
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
using System;
using System.Collections.Generic;

namespace QrCodeSignatureSearch
{
    class Program
    {
        static void Main(string[] args)
        {
            // Documentpad - bijwerken met uw bestandspad
            string filePath = "sample_multiple_signatures.docx";
            
            // Initialiseer Signature-instantie
            using (Signature signature = new Signature(filePath))
            {
                try
                {
                    // Zoek naar QR-codehandtekeningen in het document
                    List<QrCodeSignature> signatures = signature.Search<QrCodeSignature>(SignatureType.QrCode);
                    
                    // Zoekresultaten weergeven
                    Console.WriteLine($"\nSource document ['{filePath}'] contains {signatures.Count} QR code signature(s):");
                    
                    foreach (var qrCodeSignature in signatures)
                    {
                        Console.WriteLine($"QR Code found at page {qrCodeSignature.PageNumber} with type {qrCodeSignature.EncodeType.TypeName}");
                        Console.WriteLine($"Content: {qrCodeSignature.Text}");
                        Console.WriteLine($"Location: X={qrCodeSignature.Left}, Y={qrCodeSignature.Top}, Width={qrCodeSignature.Width}, Height={qrCodeSignature.Height}");
                        Console.WriteLine();
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

## Geavanceerde QR-codezoektechnieken

### Zoeken met specifieke criteria

Voor gerichtere zoekopdrachten kunt u gebruik maken van `QrCodeSearchOptions` om uw zoekcriteria aan te passen:

```csharp
// Maak QR-codezoekopties met specifieke criteria
QrCodeSearchOptions options = new QrCodeSearchOptions
{
    // Zoek alleen op specifieke pagina's
    AllPages = false,
    PageNumber = 1,
    PagesSetup = new PagesSetup { Pages = new List<int> { 1, 3, 5 } },
    
    // Filteren op QR-code-inhoud
    Text = "Invoice",
    MatchType = TextMatchType.Contains,
    
    // Filter op specifieke QR-codetypen
    EncodeType = QrCodeTypes.QR,
    
    // Definieer een specifiek gebied om binnen te zoeken
    Rectangle = new Rectangle(100, 100, 400, 400)
};

// Zoeken met specifieke opties
List<QrCodeSignature> filteredSignatures = signature.Search<QrCodeSignature>(options);
```

### Verwerken van QR-codegegevens

U kunt aangepaste verwerking voor QR-codegegevens implementeren op basis van uw toepassingsvereisten:

```csharp
foreach (var qrCode in signatures)
{
    // QR-codegegevens extraheren en verwerken op basis van inhoud
    string qrContent = qrCode.Text;
    
    if (qrContent.StartsWith("URL:"))
    {
        // URL-gegevens verwerken
        string url = qrContent.Substring(4);
        Console.WriteLine($"Found URL in QR code: {url}");
    }
    else if (qrContent.StartsWith("CONTACT:"))
    {
        // Contactgegevens verwerken
        string contact = qrContent.Substring(8);
        Console.WriteLine($"Found contact information in QR code: {contact}");
    }
    else if (qrContent.StartsWith("INVOICE:"))
    {
        // Factuurgegevens verwerken
        string invoiceData = qrContent.Substring(8);
        Console.WriteLine($"Found invoice information in QR code: {invoiceData}");
        
        // Factuurgegevens parseren en valideren
        if (ValidateInvoiceData(invoiceData))
        {
            Console.WriteLine("Invoice data is valid!");
        }
        else
        {
            Console.WriteLine("Warning: Invalid invoice data detected!");
        }
    }
}

// Voorbeeldvalidatiemethode
static bool ValidateInvoiceData(string data)
{
    // Implementeer uw validatielogica
    return !string.IsNullOrEmpty(data) && data.Contains("ID") && data.Contains("Amount");
}
```

### Implementatie van beveiligingsverificatie

QR-codes worden vaak gebruikt voor authenticatiedoeleinden. Zo implementeert u basisbeveiligingsverificatie:

```csharp
// Controleren of het document een geldige QR-authenticatiecode bevat
bool hasValidAuthQrCode = false;

foreach (var qrCode in signatures)
{
    if (qrCode.Text.StartsWith("AUTH:"))
    {
        string authCode = qrCode.Text.Substring(5);
        
        // Verifieer de authenticatiecode (bijvoorbeeld aan de hand van een database of een vooraf gedefinieerde lijst)
        if (VerifyAuthCode(authCode))
        {
            hasValidAuthQrCode = true;
            Console.WriteLine("Document contains valid authentication QR code!");
            break;
        }
    }
}

if (!hasValidAuthQrCode)
{
    Console.WriteLine("Warning: Document does not contain a valid authentication QR code!");
}

// Voorbeeld verificatiemethode
static bool VerifyAuthCode(string code)
{
    // Implementeer uw verificatielogica
    // Dit kan een database-opzoekactie, API-aanroep of vergelijking met vooraf gedefinieerde waarden zijn
    return code == "A7B82C3D" || code == "X9Y8Z7W6";
}
```

### QR-codeafbeeldingen extraheren

U kunt QR-codeafbeeldingen uit documenten halen voor verdere verwerking of weergave:

```csharp
// QR-codeafbeeldingen op schijf opslaan
foreach (var qrCode in signatures)
{
    if (qrCode.Content != null)
    {
        // Maak een unieke bestandsnaam op basis van paginanummer en positie
        string outputPath = $"QrCode_P{qrCode.PageNumber}_X{qrCode.Left}_Y{qrCode.Top}.png";
        
        // Sla de afbeeldingsgegevens op
        File.WriteAllBytes(outputPath, qrCode.Content);
        Console.WriteLine($"Saved QR code image to {outputPath}");
    }
}
```

## Conclusie

In deze uitgebreide handleiding hebben we besproken hoe u met GroupDocs.Signature voor .NET naar QR-codehandtekeningen in documenten kunt zoeken. Van eenvoudig zoeken tot geavanceerde technieken: u beschikt nu over de kennis om robuuste QR-codeverwerking in uw .NET-applicaties te implementeren. De GroupDocs.Signature API biedt een krachtig, flexibel framework voor het werken met verschillende soorten handtekeningen, waaronder QR-codes, in verschillende documentformaten.

Door deze mogelijkheden te benutten, kunt u documentverificatieprocessen verbeteren, authenticatiesystemen implementeren en waardevolle informatie uit QR-codes extraheren, allemaal binnen uw .NET-toepassingen.

## Veelgestelde vragen

### Welke QR-codeformaten worden ondersteund door GroupDocs.Signature?

GroupDocs.Signature ondersteunt verschillende QR-codeformaten, waaronder standaard QR-codes, micro-QR-codes en andere gangbare QR-codestandaarden. Het specifieke formaat is toegankelijk via de `EncodeType` eigendom van de `QrCodeSignature` voorwerp.

### Kan ik naar QR-codes zoeken in documenten die met een wachtwoord zijn beveiligd?

Ja, GroupDocs.Signature ondersteunt het zoeken naar QR-codes in met een wachtwoord beveiligde documenten door het wachtwoord op te geven bij het initialiseren van de `Signature` voorwerp:

```csharp
LoadOptions loadOptions = new LoadOptions { Password = "your_password" };
using (Signature signature = new Signature(filePath, loadOptions))
{
    // Zoeken naar QR-codes
}
```

### Hoe kan ik QR-codes filteren op basis van hun inhoud?

U kunt QR-codes filteren op basis van hun inhoud met behulp van de `Text` En `MatchType` eigenschappen van `QrCodeSearchOptions`:

```csharp
QrCodeSearchOptions options = new QrCodeSearchOptions
{
    Text = "Invoice",
    MatchType = TextMatchType.Contains // Andere opties: Exact, Begint met, Eindigt met
};
```

### Kan GroupDocs.Signature beschadigde of gedeeltelijk zichtbare QR-codes detecteren?

GroupDocs.Signature kan gedeeltelijk zichtbare QR-codes detecteren, maar ernstig beschadigde QR-codes worden mogelijk niet herkend. De nauwkeurigheid van de detectie is afhankelijk van de kwaliteit en zichtbaarheid van de QR-code in het document.

### Welke documentformaten worden ondersteund voor het zoeken met QR-codes?

GroupDocs.Signature ondersteunt het zoeken naar QR-codes in verschillende documentformaten, waaronder PDF, Microsoft Office-documenten (Word, Excel, PowerPoint), afbeeldingen (JPEG, PNG, TIFF) en vele andere.

## Zie ook

* [API-referentie](https://reference.groupdocs.com/signature/net/)
* [Codevoorbeelden op GitHub](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
* [Productdocumentatie](https://docs.groupdocs.com/signature/net/)
* [Productpagina](https://products.groupdocs.com/signature/net/)
* [Download de nieuwste versie](https://releases.groupdocs.com/signature/net/)
* [Blogartikelen](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
* [Gratis ondersteuningsforum](https://forum.groupdocs.com/c/signature/13)
* [Tijdelijke licentie](https://purchase.groupdocs.com/temporary-license/)