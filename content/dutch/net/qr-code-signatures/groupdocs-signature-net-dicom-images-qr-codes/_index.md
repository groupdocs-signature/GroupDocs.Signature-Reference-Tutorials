---
"date": "2025-05-07"
"description": "Leer hoe u DICOM-afbeeldingen kunt ondertekenen met QR-codes met GroupDocs.Signature voor .NET. Deze handleiding behandelt de installatie, implementatie en verificatie van QR-codehandtekeningen in medische beeldvorming."
"title": "DICOM-afbeeldingen ondertekenen met QR-codes met GroupDocs.Signature voor .NET&#58; een uitgebreide handleiding"
"url": "/nl/net/qr-code-signatures/groupdocs-signature-net-dicom-images-qr-codes/"
"weight": 1
---

# DICOM-afbeeldingen ondertekenen met QR-codes met GroupDocs.Signature voor .NET: een uitgebreide handleiding

Bent u op zoek naar een veilige methode om uw DICOM-bestanden te verifiëren? Deze gedetailleerde handleiding laat u zien hoe u GroupDocs.Signature voor .NET kunt gebruiken om QR-codehandtekeningen in DICOM-afbeeldingen te integreren. Deze tutorial is ideaal voor zorgprofessionals, ontwikkelaars en iedereen die met digitale medische documenten werkt en behandelt de installatie tot en met de implementatie.

## Wat je leert:
- Uw ontwikkelomgeving instellen met GroupDocs.Signature voor .NET.
- Stapsgewijze instructies voor het ondertekenen van DICOM-afbeeldingen met behulp van QR-codes.
- Methoden om QR-codehandtekeningen in DICOM-bestanden te verifiëren en te zoeken.
- Technieken om voorbeelden van ondertekende documenten te genereren voor beoordelingsdoeleinden.
- Aanbevolen procedures voor het optimaliseren van prestaties en het effectief beheren van resources.

Laten we beginnen met de vereisten!

## Vereisten

Om GroupDocs.Signature voor .NET te gebruiken, moet u ervoor zorgen dat uw omgeving klaar is. Dit heeft u nodig:

### Vereiste bibliotheken en versies
- **GroupDocs.Signature voor .NET**Zorg voor compatibiliteit met uw .NET Framework.

### Vereisten voor omgevingsinstellingen
- Een ontwikkelomgeving op Windows of Linux.
- Visual Studio of een andere .NET-compatibele IDE geïnstalleerd.

### Kennisvereisten
- Basiskennis van C#-programmering.
- Kennis van bestands-I/O in .NET-toepassingen.

## GroupDocs.Signature instellen voor .NET

Installeer de GroupDocs.Signature-bibliotheek volgens uw voorkeursmethode:

**Met behulp van .NET CLI:**
```bash
dotnet add package GroupDocs.Signature
```

**Pakketbeheerder:**
```powershell
Install-Package GroupDocs.Signature
```

**Gebruikersinterface van NuGet Package Manager:**
- Zoek naar "GroupDocs.Signature" en installeer de nieuwste versie.

### Licentieverwerving

Begin met een gratis proefperiode om de mogelijkheden te verkennen. Voor langdurig gebruik kunt u een tijdelijke of volledige licentie aanschaffen bij [Groepsdocumenten](https://purchase.groupdocs.com/buy).

Nadat de bibliotheek is geïnstalleerd, initialiseert u deze:

```csharp
using GroupDocs.Signature;
// Initialiseer het Signature-object met uw DICOM-bestandspad.
Signature signature = new Signature("YOUR_DOCUMENT_DIRECTORY\\sample.dicom");
```

## Implementatiegids

### Onderteken DICOM-afbeelding met QR-code

#### Overzicht
Voeg QR-codehandtekeningen toe om de authenticiteit en traceerbaarheid van medische documenten te garanderen.

**Stap 1: Initialiseer het handtekeningobject**

```csharp
string filePath = "YOUR_DOCUMENT_DIRECTORY\\sample.dicom";
using (Signature signature = new Signature(filePath))
{
    // Ga door met de ondertekeningsoperaties...
}
```

**Stap 2: QR-code-ondertekeningsopties maken**

Configureer eigenschappen zoals tekst, grootte en uitlijning.

```csharp
QrCodeSignOptions options = new QrCodeSignOptions("Patient #36363393. R: No-Issues")
{
    AllPages = true,
    Width = 100,
    Height = 100,
    VerticalAlignment = VerticalAlignment.Bottom,
    HorizontalAlignment = HorizontalAlignment.Right,
    Margin = new Padding() { Right = 5, Left = 5 }
};
```

**Stap 3: XMP-metagegevens toevoegen**

Verrijk het document met extra metagegevens.

```csharp
DicomSaveOptions dicomSaveOptions = new DicomSaveOptions()
{
    XmpEntries = new List<DicomXmpEntry>() { new DicomXmpEntry(DicomXmpType.PatientName, "Patient #4") }
};
```

**Stap 4: Onderteken het document**

Ondertekening uitvoeren en opslaan.

```csharp
SignResult signResult = signature.Sign("YOUR_OUTPUT_DIRECTORY\\SignedDicom", options, dicomSaveOptions);
```

### Documentinfo ophalen

Haal metagegevens op uit ondertekende DICOM-bestanden om de integriteit van de gegevens te garanderen.

**Overzicht:**
Krijg toegang tot documentinformatie en XMP-metadatahandtekeningen voor verificatie.

**Stap 1: Documentinformatie ophalen**

```csharp
using (Signature signature = new Signature("YOUR_DOCUMENT_DIRECTORY\\sample_signed.dicom"))
{
    IDocumentInfo signedDocumentInfo = signature.GetDocumentInfo();
}
```

**Stap 2: XMP-gegevens herhalen en afdrukken**

Metagegevensdetails weergeven.

```csharp
foreach (var item in signedDocumentInfo.MetadataSignatures)
{
    Console.WriteLine(item.ToString());
}
```

### DICOM-handtekeningen verifiëren

Valideer de authenticiteit van QR-codehandtekeningen in DICOM-afbeeldingen.

**Overzicht:**
Zorg ervoor dat de handtekeningen juist en authentiek zijn.

**Stap 1: QR-codeverificatieopties maken**

Stel opties in die overeenkomen met specifieke tekst in de QR-codes.

```csharp
QrCodeVerifyOptions options = new QrCodeVerifyOptions()
{
    AllPages = true,
    Text = "Patient #36363393",
    MatchType = TextMatchType.Contains
};
```

**Stap 2: Handtekeningen verifiëren**

Controleren of de handtekeningen aan de criteria voldoen.

```csharp
VerificationResult result = signature.Verify(options);

if (result.IsValid)
{
    Console.WriteLine($"DICOM {filePath} has {result.Succeeded.Count} successfully verified signatures!");
}
```

### Zoeken naar handtekeningen in DICOM

Zoek QR-codehandtekeningen in ondertekende DICOM-afbeeldingen.

**Overzicht:**
Vind efficiënt alle QR-codehandtekeningen om de authenticiteit van documenten te beheren.

**Stap 1: Zoek naar QR-codehandtekeningen**

```csharp
List<QrCodeSignature> signatures = signature.Search<QrCodeSignature>(SignatureType.QrCode);
```

**Stap 2: Herhaal en druk handtekeningdetails af**

Bekijk de details van elke gevonden handtekening.

```csharp
foreach (var QrCodeSignature in signatures)
{
    Console.WriteLine($"QRCode signature found at page {QrCodeSignature.PageNumber} with type {QrCodeSignature.EncodeType.TypeName} and text {QrCodeSignature.Text}");
}
```

### Voorbeeld van ondertekende DICOM genereren

Maak visuele voorbeelden ter verificatie.

**Overzicht:**
Genereer voorbeeldafbeeldingen om inhoud te verifiëren zonder speciale software.

**Stap 1: Streammethoden definiëren**

Stel methoden in voor bestandsstroombeheer tijdens het genereren van voorbeelden.

```csharp
Stream CreatePageStream(PreviewPageData pageData)
{
    string imageFilePath = Path.Combine("YOUR_OUTPUT_DIRECTORY", "SignDicomImageAdvanced", $"preview-{pageData.PageNumber}.jpg");
    var folder = Path.GetDirectoryName(imageFilePath);
    if (!Directory.Exists(folder))
    {
        Directory.CreateDirectory(folder);
    }
    return new FileStream(imageFilePath, FileMode.Create);
}

void ReleasePageStream(PreviewPageData pageData, Stream pageStream)
{
    pageStream.Dispose();
}
```

**Stap 2: Previews genereren**

Voer het preview-generatieproces uit.

```csharp
using (Signature signature = new Signature("YOUR_DOCUMENT_DIRECTORY\\sample_signed.dicom"))
{
    PreviewOptions previewOption = new PreviewOptions(CreatePageStream, ReleasePageStream)
    {
        PreviewFormat = PreviewOptions.PreviewFormats.PNG,
    };

    signature.GeneratePreview(previewOption);
}
```

## Praktische toepassingen

1. **Medisch dossierbeheer**: Verifieer patiëntendossiers met behulp van QR-codehandtekeningen voor naleving.
2. **Audittrails in zorgsystemen**: Volg documentwijzigingen en verifieer de authenticiteit met QR-codes.
3. **Veilig delen van gegevens**: Zorg voor veilig delen van medische beelden door digitale handtekeningen in te bouwen.
4. **Nalevingsverificatie**: Controleer regelmatig de integriteit van DICOM-bestanden om te voldoen aan de wettelijke vereisten.
5. **Integratie met EPD-systemen**: Integreer naadloos ondertekende DICOM-bestanden in elektronische patiëntendossiers (EPD)-systemen voor gestroomlijnde processen.