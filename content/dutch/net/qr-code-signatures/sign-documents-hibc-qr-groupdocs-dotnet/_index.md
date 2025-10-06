---
"date": "2025-05-07"
"description": "Leer hoe u PDF-documenten ondertekent met HIBC QR-codes met GroupDocs.Signature voor .NET. Deze handleiding behandelt LIC- en PAS-codes, waaronder QR-codes, Aztec-codes en DataMatrix-codes."
"title": "Documenten ondertekenen met HIBC QR-codes met GroupDocs.Signature voor .NET&#58; een uitgebreide handleiding"
"url": "/nl/net/qr-code-signatures/sign-documents-hibc-qr-groupdocs-dotnet/"
"weight": 1
type: docs
---
# Documenten ondertekenen met HIBC QR-codes met GroupDocs.Signature voor .NET

## Invoering

In de huidige snelle zakelijke omgeving is het van het grootste belang om de authenticiteit en integriteit van documenten te waarborgen. Of u nu geneesmiddelen, gezondheidsproducten of logistiek verwerkt, een veilige manier om documenten te ondertekenen en te volgen kan tijd besparen en fouten voorkomen. **GroupDocs.Signature voor .NET**, een krachtige bibliotheek die is ontworpen om documentbeheerprocessen te stroomlijnen door naadloze integratie van HIBC QR-codes in uw documenten mogelijk te maken.

In deze tutorial onderzoeken we hoe u GroupDocs.Signature voor .NET kunt gebruiken om PDF-documenten te ondertekenen met verschillende soorten HIBC QR-codes – LIC (License) en PAS (Product Authentication System) – waaronder QR-code, Aztec Code en DataMatrix. Na afloop hebt u een gedegen begrip van de implementatie van deze oplossingen in uw .NET-applicaties.

**Wat je leert:**
- GroupDocs.Signature voor .NET instellen
- Implementatie van HIBC LIC QR-codes, Aztec-codes en DataMatrix
- HIBC PAS QR-codes, Aztec-codes en DataMatrix toevoegen
- Praktische use cases en integratiemogelijkheden

Laten we eens kijken naar de vereisten voordat we beginnen met het implementeren van deze functies.

## Vereisten

Voordat we beginnen met coderen, zorg ervoor dat u het volgende heeft geregeld:

- **.NET-omgeving**: Zorg ervoor dat u .NET op uw systeem hebt geïnstalleerd (bij voorkeur .NET Core of .NET 5/6+).
- **GroupDocs.Signature voor .NET**: Deze bibliotheek wordt onze primaire tool. Je kunt hem installeren via NuGet.
- **Basiskennis programmeren**: Kennis van C# en het werken met bestanden in .NET wordt aanbevolen.

### Vereiste bibliotheken

Om GroupDocs.Signature voor .NET te gebruiken, moet u het pakket toevoegen met een van de volgende methoden:

**.NET CLI**
```bash
dotnet add package GroupDocs.Signature
```

**Pakketbeheerder**
```powershell
Install-Package GroupDocs.Signature
```

**NuGet Package Manager-gebruikersinterface**
Zoek naar "GroupDocs.Signature" en installeer de nieuwste versie.

### Licentieverwerving

Voor testdoeleinden kunt u een gratis proeflicentie verkrijgen. Voor langdurig gebruik kunt u een abonnement nemen of een tijdelijke licentie aanvragen:

- **Gratis proefperiode**: Toegang [hier](https://releases.groupdocs.com/signature/net/)
- **Tijdelijke licentie**: Aanvraag bij [deze link](https://purchase.groupdocs.com/temporary-license/)

### Omgevingsinstelling

Stel uw omgeving in door ervoor te zorgen dat uw project de juiste .NET-versie gebruikt en toegang heeft tot GroupDocs.Signature. Initialiseer het in uw applicatie zoals weergegeven:

```csharp
using GroupDocs.Signature;
```

## GroupDocs.Signature instellen voor .NET

Om GroupDocs.Signature voor .NET te kunnen gebruiken, moet u de bibliotheek installeren en een basisconfiguratie in uw project configureren.

### Installatie

Volg een van de hierboven genoemde methoden om GroupDocs.Signature aan uw project toe te voegen. Controleer na de installatie of uw project geconfigureerd is om GroupDocs.Signature te gebruiken door ernaar te verwijzen in uw codebestanden.

### Licentie-initialisatie

Nadat u een licentie hebt verkregen, initialiseert u deze als volgt:

```csharp
SignatureConfig signConfig = new SignatureConfig();
signConfig.LicensePath = "path/to/your/license.lic";
Signature signature = new Signature("Sample.pdf", signConfig);
```

Met deze instelling hebt u onbeperkt toegang tot alle functies van GroupDocs.Signature.

## Implementatiegids

Laten we nu eens kijken hoe u elke functie implementeert met behulp van HIBC QR-codes met GroupDocs.Signature voor .NET.

### Onderteken document met HIBC LIC QR-code

#### Overzicht

Het ondertekenen van een document met een HIBC LIC QR-code garandeert naleving en traceerbaarheid in licentiescenario's. Deze sectie begeleidt u bij het maken en insluiten van een QR-code in uw PDF-documenten.

#### Implementatiestappen

##### Stap 1: Configureer de bron- en uitvoerpaden

Geef aan waar uw brondocument zich bevindt en waar de ondertekende uitvoer moet worden opgeslagen:

```csharp
string sourceFilePath = Path.Combine("YOUR_DOCUMENT_DIRECTORY", "Sample.pdf");
string outputPath = Path.Combine("YOUR_OUTPUT_DIRECTORY", "SignWithHIBCLICQR");
string destinFilePath = Path.Combine(outputPath, "SignedDocumentWithHIBCLICQR.pdf");
```

##### Stap 2: QR-code-ondertekeningsopties maken

Configureer uw QR-code met specifieke tekst en instellingen:

```csharp
using (Signature signature = new Signature(sourceFilePath))
{
    var hibcLic_QR_Options = new QrCodeSignOptions("A123PROD30917/75#422011907#GP293", QrCodeTypes.HIBCLICQR)
    {
        Left = 1,
        Top = 1,
        ReturnContent = true,
        ReturnContentType = FileType.PNG
    };

    // Onderteken het document met deze opties.
    signature.Sign(destinFilePath, hibcLic_QR_Options);
}
```

**Uitleg**: 
- `QrCodeSignOptions` Hiermee stelt u het uiterlijk en de inhoud van de QR-code in. Hier specificeren we het HIBC LIC QR-codetype en positioneren we deze op het document.
- `ReturnContent` Als u deze optie op true instelt, kunt u een gerenderde afbeelding van het ondertekende document ophalen.

#### Tips voor probleemoplossing

- Zorg ervoor dat het documentpad correct is opgegeven.
- Controleer of GroupDocs.Signature over de juiste licentie beschikt voor volledige functionaliteit.

### Onderteken document met HIBC LIC Aztec-code

#### Overzicht

De Azteekse code biedt een andere vorm van codering, geschikt voor informatieopslag met hoge dichtheid. Deze sectie richt zich op het insluiten van een Azteekse code in uw documenten met behulp van GroupDocs.Signature.

#### Implementatiestappen

##### Stap 1: Paden configureren

Vergelijkbaar met de vorige functie, definieert u uw bestandspaden:

```csharp
string sourceFilePath = Path.Combine("YOUR_DOCUMENT_DIRECTORY", "Sample.pdf");
string outputPath = Path.Combine("YOUR_OUTPUT_DIRECTORY", "SignWithHIBCLICAztec");
string destinFilePath = Path.Combine(outputPath, "SignedDocumentWithHIBCLICAztec.pdf");
```

##### Stap 2: Aztec-codeopties configureren

Stel uw Aztec-code in met GroupDocs.Signature:

```csharp
using (Signature signature = new Signature(sourceFilePath))
{
    var hibcLic_AZ_Options = new QrCodeSignOptions("A123PROD30917/75#422011907#GP293", QrCodeTypes.HIBCLICAztec)
    {
        Left = 1,
        Top = 200,
        ReturnContent = true,
        ReturnContentType = FileType.PNG
    };

    signature.Sign(destinFilePath, hibcLic_AZ_Options);
}
```

**Uitleg**: 
- De `QrCodeSignOptions` wordt hier opnieuw gebruikt, maar dan met het Azteekse codetype.
- Positionering (`Top`, `Left`) en de instellingen voor het ophalen van inhoud zijn vergelijkbaar met die van QR-codes.

#### Tips voor probleemoplossing

- Controleer of de bestandspaden correct zijn.
- Zorg ervoor dat de versie van GroupDocs.Signature Aztec-codetypen ondersteunt.

### Document ondertekenen met HIBC LIC DataMatrix

#### Overzicht

De DataMatrix-code biedt een andere robuuste methode voor het opslaan van gegevens. Deze sectie laat zien hoe u een DataMatrix in uw PDF-documenten kunt integreren.

#### Implementatiestappen

##### Stap 1: Bestandspaden instellen

Bepaal zoals eerder aangegeven waar uw bestanden zich bevinden:

```csharp
string sourceFilePath = Path.Combine("YOUR_DOCUMENT_DIRECTORY", "Sample.pdf");
string outputPath = Path.Combine("YOUR_OUTPUT_DIRECTORY", "SignWithHIBCLICDataMatrix");
string destinFilePath = Path.Combine(outputPath, "SignedDocumentWithHIBCLICDataMatrix.pdf");
```

##### Stap 2: DataMatrix-tekenopties maken

Configureer en pas de DataMatrix-code toe:

```csharp
using (Signature signature = new Signature(sourceFilePath))
{
    var hibcLic_DM_Options = new QrCodeSignOptions("A123PROD30917/75#422011907#GP293", QrCodeTypes.HIBCLICDataMatrix)
    {
        Left = 1,
        Top = 400,
        ReturnContent = true,
        ReturnContentType = FileType.PNG
    };

    signature.Sign(destinFilePath, hibcLic_DM_Options);
}
```

**Uitleg**: 
- `QrCodeSignOptions` wordt gebruikt om het uiterlijk en de inhoud van de DataMatrix-code in te stellen.
- Positionering (`Top`, `Left`) en de ophaalinstellingen volgen hetzelfde patroon als voorgaande codes.

#### Tips voor probleemoplossing

- Zorg ervoor dat alle bestandspaden correct zijn opgegeven.
- Controleer of GroupDocs.Signature DataMatrix-codetypen ondersteunt in uw versie.

### Onderteken document met HIBC PAS QR-code

#### Overzicht

Het ondertekenen van documenten met een HIBC PAS QR-code verbetert de tracking en traceerbaarheid van producten. Deze sectie begeleidt u bij het insluiten van een PAS QR-code in PDF's met behulp van GroupDocs.Signature.

#### Implementatiestappen

##### Stap 1: Configureer de bron- en uitvoerpaden

Geef aan waar uw brondocument zich bevindt en waar de ondertekende uitvoer moet worden opgeslagen:

```csharp
string sourceFilePath = Path.Combine("YOUR_DOCUMENT_DIRECTORY", "Sample.pdf");
string outputPath = Path.Combine("YOUR_OUTPUT_DIRECTORY", "SignWithHIBCPASQR");
string destinFilePath = Path.Combine(outputPath, "SignedDocumentWithHIBCPASQR.pdf");
```

##### Stap 2: QR-code-ondertekeningsopties maken

Configureer uw PAS QR-code met specifieke tekst en instellingen:

```csharp
using (Signature signature = new Signature(sourceFilePath))
{
    var hibcPas_QR_Options = new QrCodeSignOptions("PAS123456789012", QrCodeTypes.HIBCPASQR)
    {
        Left = 1,
        Top = 500,
        ReturnContent = true,
        ReturnContentType = FileType.PNG
    };

    // Onderteken het document met deze opties.
    signature.Sign(destinFilePath, hibcPas_QR_Options);
}
```

**Uitleg**: 
- `QrCodeSignOptions` is geconfigureerd voor het HIBC PAS QR-codetype en op het document geplaatst.
- `ReturnContent` Als deze optie op true is ingesteld, wordt een gerenderde afbeelding van het ondertekende document opgehaald.

#### Tips voor probleemoplossing

- Zorg ervoor dat alle paden correct zijn opgegeven.
- Controleer of GroupDocs.Signature de PAS QR-codetypen in uw versie ondersteunt.

### Conclusie

Door deze handleiding te volgen, kunt u HIBC LIC- en PAS QR-codes efficiënt integreren in PDF-documenten met GroupDocs.Signature voor .NET. Dit proces verbetert de documentbeveiliging, traceerbaarheid en naleving in diverse sectoren. Raadpleeg de [GroupDocs-documentatie](https://docs.groupdocs.com/signature/net/).