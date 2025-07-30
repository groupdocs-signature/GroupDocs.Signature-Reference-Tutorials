---
"description": "Leer hoe u QR-codehandtekeningen in verschillende documentformaten dynamisch kunt bijwerken met GroupDocs.Signature voor .NET. Uitgebreide ontwikkelaarshandleiding voor moderne oplossingen voor documentbeheer."
"linktitle": "QR-code bijwerken"
"second_title": "GroupDocs.Signature .NET API"
"title": "QR-codehandtekeningen in documenten bijwerken"
"url": "/nl/net/update-operations/update-qr-code/"
"weight": 12
---

## Invoering
In de huidige, digitaal georiënteerde bedrijfsomgeving zijn QR-codes een essentieel onderdeel geworden van documentbeheer- en authenticatiesystemen. Ze bieden een handige manier om informatie te coderen en te openen, van eenvoudige URL's tot complexe gestructureerde gegevens. GroupDocs.Signature voor .NET biedt een uitgebreide toolkit waarmee ontwikkelaars geavanceerde mogelijkheden voor elektronische handtekeningen in hun applicaties kunnen integreren, inclusief de mogelijkheid om bestaande QR-codehandtekeningen in documenten bij te werken.

Deze tutorial richt zich specifiek op het bijwerken van QR-codehandtekeningen in documenten met GroupDocs.Signature voor .NET. Of u nu de positie, grootte of gecodeerde gegevens van bestaande QR-codes wilt wijzigen, deze handleiding leidt u stap voor stap door het proces met duidelijke codevoorbeelden en uitleg.

## Vereisten
Voordat u met GroupDocs.Signature voor .NET aan de slag gaat met het bijwerken van QR-codehandtekeningen, moet u ervoor zorgen dat aan de volgende vereisten is voldaan:

1. Ontwikkelomgeving: Een werkende .NET-ontwikkelomgeving, zoals Visual Studio 2017 of later.
2. GroupDocs.Signature-bibliotheek: download en installeer de GroupDocs.Signature voor .NET-bibliotheek van de [downloadpagina](https://releases.groupdocs.com/signature/net/).
3. Licentie (optioneel): Voor productiegebruik heb je een geldige licentie nodig. Voor testdoeleinden kun je een [tijdelijke licentie](https://purchase.groupdocs.com/temporary-license/).
4. Voorbeelddocument: Een document met QR-codehandtekeningen die u wilt bijwerken.
5. Basiskennis van C#: Kennis van C#-programmeerconcepten.

## Naamruimten importeren
Begin met het importeren van de benodigde naamruimten om toegang te krijgen tot de GroupDocs.Signature-functionaliteit:

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

Laten we het proces voor het bijwerken van QR-codehandtekeningen opsplitsen in duidelijke, beheersbare stappen:

## Stap 1: Documentpaden instellen
Definieer eerst de paden voor uw brondocument en waar het bijgewerkte document wordt opgeslagen:

```csharp
// Pad naar het brondocument met QR-codehandtekeningen
string filePath = "sample_multiple_signatures.docx";

// Haal de bestandsnaam op voor de uitvoer
string fileName = Path.GetFileName(filePath);

// Definieer de uitvoermap en het bestandspad
string outputDirectory = Path.Combine("Your Document Directory", "UpdateQRCode");
string outputFilePath = Path.Combine(outputDirectory, fileName);

// Zorg ervoor dat de uitvoermap bestaat
Directory.CreateDirectory(outputDirectory);
```

## Stap 2: Kopieer het brondocument
Omdat de updatebewerking het document rechtstreeks wijzigt, maakt u een kopie van het originele document om het te behouden:

```csharp
// Maak een kopie van het originele document
File.Copy(filePath, outputFilePath, true);
```

## Stap 3: Initialiseer de handtekeninginstantie
Maak een exemplaar van de `Signature` klasse om met het document te werken:

```csharp
// Initialiseer het Signature-exemplaar met het pad naar het uitvoerbestand
using (Signature signature = new Signature(outputFilePath))
{
    // Hier worden handtekeningbewerkingen uitgevoerd
}
```

## Stap 4: Configureer QR-codezoekopties
Stel de zoekopties in om bestaande QR-codehandtekeningen in het document te vinden:

```csharp
// Zoekopties voor QR-codehandtekeningen configureren
QrCodeSearchOptions options = new QrCodeSearchOptions();

// U kunt de zoekopties indien nodig aanpassen
// options.AllPages = true; // Zoeken op alle pagina's
// options.PageNumber = 1; // Zoeken op een specifieke pagina
// options.EncodeType = QrCodeTypes.QR; // Zoeken naar een specifiek QR-codetype
```

## Stap 5: Zoek naar QR-codehandtekeningen
Gebruik de geconfigureerde zoekopties om QR-codehandtekeningen in het document te vinden:

```csharp
// Zoeken naar QR-codehandtekeningen
List<QrCodeSignature> signatures = signature.Search<QrCodeSignature>(options);
```

## Stap 6: QR-code-handtekeningeigenschappen bijwerken
Als er QR-codehandtekeningen worden gevonden, werk dan hun eigenschappen indien nodig bij:

```csharp
// Controleer of er handtekeningen zijn gevonden
if (signatures.Count > 0)
{
    // Ontvang de eerste QR-codehandtekening
    QrCodeSignature qrCodeSignature = signatures[0];
    
    // Positie bijwerken
    qrCodeSignature.Left = 200;
    qrCodeSignature.Top = 250;
    
    // Grootte bijwerken
    qrCodeSignature.Width = 200;
    qrCodeSignature.Height = 200;
    
    // U kunt de QR-codegegevens indien nodig ook bijwerken
    // qrCodeSignature.Text = "Bijgewerkte QR-codegegevens";
    
    // Pas de updates toe
    bool result = signature.Update(qrCodeSignature);
    
    // Controleer het resultaat
    if (result)
    {
        Console.WriteLine($"QR Code signature was successfully updated in the document '{fileName}'.");
        Console.WriteLine($"New position: {qrCodeSignature.Left}x{qrCodeSignature.Top}");
        Console.WriteLine($"New size: {qrCodeSignature.Width}x{qrCodeSignature.Height}");
    }
    else
    {
        Console.WriteLine($"Failed to update QR Code signature in the document!");
    }
}
else
{
    Console.WriteLine("No QR Code signatures found in the document.");
}
```

## Volledig voorbeeld
Hier is een volledig, functioneel voorbeeld dat laat zien hoe u een QR-codehandtekening in een document kunt bijwerken:

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;

namespace UpdateQRCodeSignatureExample
{
    class Program
    {
        static void Main(string[] args)
        {
            // Documentpad
            string filePath = "sample_multiple_signatures.docx";
            
            // Definieer uitvoerpad
            string fileName = Path.GetFileName(filePath);
            string outputDirectory = Path.Combine(Environment.CurrentDirectory, "UpdateQRCode");
            string outputFilePath = Path.Combine(outputDirectory, fileName);
            
            // Zorg ervoor dat de uitvoermap bestaat
            Directory.CreateDirectory(outputDirectory);
            
            // Maak een kopie van het originele document
            File.Copy(filePath, outputFilePath, true);
            
            // Initialiseer Signature-instantie
            using (Signature signature = new Signature(outputFilePath))
            {
                // Zoekopties configureren
                QrCodeSearchOptions options = new QrCodeSearchOptions();
                
                // Zoeken naar QR-codehandtekeningen
                List<QrCodeSignature> signatures = signature.Search<QrCodeSignature>(options);
                
                // Controleer of er handtekeningen zijn gevonden
                if (signatures.Count > 0)
                {
                    // Ontvang de eerste handtekening
                    QrCodeSignature qrCodeSignature = signatures[0];
                    
                    // Positie en grootte bijwerken
                    qrCodeSignature.Left = 200;
                    qrCodeSignature.Top = 250;
                    qrCodeSignature.Width = 200;
                    qrCodeSignature.Height = 200;
                    
                    // Pas de updates toe
                    bool result = signature.Update(qrCodeSignature);
                    
                    // Controleer resultaat
                    if (result)
                    {
                        Console.WriteLine($"QR Code signature was successfully updated in document '{fileName}'.");
                        Console.WriteLine($"New position: {qrCodeSignature.Left}x{qrCodeSignature.Top}");
                        Console.WriteLine($"New size: {qrCodeSignature.Width}x{qrCodeSignature.Height}");
                        Console.WriteLine($"Output file path: {outputFilePath}");
                    }
                    else
                    {
                        Console.WriteLine("Failed to update QR Code signature!");
                    }
                }
                else
                {
                    Console.WriteLine("No QR Code signatures found in the document.");
                }
            }
            
            Console.WriteLine("\nPress any key to exit...");
            Console.ReadKey();
        }
    }
}
```

## Geavanceerde aanpassing van QR-codehandtekeningen
GroupDocs.Signature biedt extra opties voor het aanpassen van QR-codehandtekeningen die verder gaan dan de basispositie en -grootte:

### De gecodeerde gegevens bijwerken
U kunt de werkelijke gegevens die in de QR-code zijn gecodeerd, bijwerken:

```csharp
// De gecodeerde gegevens bijwerken
qrCodeSignature.Text = "https://www.bijgewerkte-website.com";
```

### Uiterlijke eigenschappen aanpassen
Pas de visuele aspecten van de QR-code aan:

```csharp
// Voorgrondkleur instellen (QR-codekleur)
qrCodeSignature.ForeColor = System.Drawing.Color.Blue;

// Achtergrondkleur instellen
qrCodeSignature.BackgroundColor = System.Drawing.Color.LightYellow;

// Transparantie aanpassen
qrCodeSignature.Opacity = 0.8;
```

### Randen toevoegen
Verbeter de QR-code met aangepaste randen:

```csharp
qrCodeSignature.Border.Color = System.Drawing.Color.Red;
qrCodeSignature.Border.DashStyle = System.Drawing.Drawing2D.DashStyle.Dash;
qrCodeSignature.Border.Weight = 2;
qrCodeSignature.Border.Visible = true;
```

### De QR-code roteren
Draai de QR-codehandtekening naar een specifieke hoek:

```csharp
qrCodeSignature.Angle = 30; // 30 graden draaien
```

## Werken met verschillende documentformaten
GroupDocs.Signature ondersteunt het bijwerken van QR-codehandtekeningen in verschillende documentformaten:

- PDF-documenten
- Microsoft Word-documenten (DOC, DOCX)
- Microsoft Excel-spreadsheets (XLS, XLSX)
- Microsoft PowerPoint-presentaties (PPT, PPTX)
- OpenDocument-formaten
- Afbeeldingsformaten

Dezelfde code kan met minimale aanpassingen in alle formaten worden gebruikt.

## Conclusie
GroupDocs.Signature voor .NET biedt een krachtige en flexibele oplossing voor het bijwerken van QR-codehandtekeningen in documenten. Door de stappen in deze tutorial te volgen, kunnen ontwikkelaars de functionaliteit voor het bijwerken van QR-codehandtekeningen efficiënt implementeren in hun .NET-applicaties, waardoor documentbeheer en authenticatiemogelijkheden worden verbeterd.

Dankzij de uitgebreide functieset en intuïtieve API kunnen ontwikkelaars met GroupDocs.Signature geavanceerde oplossingen voor het ondertekenen van documenten bouwen die voldoen aan de vereisten van moderne zakelijke toepassingen en tegelijkertijd de integriteit en toegankelijkheid van documenten garanderen.

## Veelgestelde vragen
### Kan ik meerdere QR-codehandtekeningen in één document bijwerken?
Ja, met GroupDocs.Signature kunt u meerdere QR-codehandtekeningen in hetzelfde document bijwerken. Nadat u naar handtekeningen hebt gezocht, kunt u door de resulterende lijst bladeren en elke QR-codehandtekening afzonderlijk bijwerken.

### Ondersteunt GroupDocs.Signature verschillende QR-codetypen?
Ja, GroupDocs.Signature ondersteunt verschillende QR-codetypen, waaronder standaard QR, micro QR en andere. U kunt het QR-codetype opgeven met behulp van de `EncodeType` eigendom.

### Is er een proefversie beschikbaar voor GroupDocs.Signature voor .NET?
Ja, u kunt een gratis proefversie downloaden van de [GroupDocs-website](https://releases.groupdocs.com/signature/net/) om de functies van de bibliotheek te evalueren voordat u tot aankoop overgaat.

### Kan ik het foutcorrectieniveau van de QR-code programmatisch wijzigen?
Ja, u kunt het foutcorrectieniveau wijzigen wanneer u nieuwe QR-codes toevoegt, maar het bijwerken van deze eigenschap voor bestaande QR-codes wordt mogelijk niet in alle documentindelingen ondersteund.

### Waar kan ik aanvullende ondersteuning vinden voor GroupDocs.Signature voor .NET?
kunt uitgebreide ondersteuning krijgen via de volgende bronnen:
- [API-documentatie](https://docs.groupdocs.com/signature/net/)
- [API-referentie](https://reference.groupdocs.com/signature/net/)
- [GitHub-voorbeelden](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
- [Ondersteuningsforum](https://forum.groupdocs.com/c/signature/13)
- [Blog](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)