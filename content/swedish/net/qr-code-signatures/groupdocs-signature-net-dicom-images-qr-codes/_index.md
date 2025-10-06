---
"date": "2025-05-07"
"description": "Lär dig hur du signerar DICOM-bilder med QR-koder med GroupDocs.Signature för .NET. Den här guiden behandlar installation, implementering och verifiering av QR-kodsignaturer inom medicinsk avbildning."
"title": "Hur man signerar DICOM-bilder med QR-koder med GroupDocs.Signature för .NET – en omfattande guide"
"url": "/sv/net/qr-code-signatures/groupdocs-signature-net-dicom-images-qr-codes/"
"weight": 1
type: docs
---
# Så här signerar du DICOM-bilder med QR-koder med GroupDocs.Signature för .NET: En omfattande guide

Letar du efter en säker metod för att autentisera dina DICOM-filer? Den här detaljerade guiden visar hur du använder GroupDocs.Signature för .NET för att integrera QR-kodsignaturer i DICOM-bilder. Den här handledningen är idealisk för sjukvårdspersonal, utvecklare och alla som arbetar med digitala medicinska dokument och täcker allt från installation till implementering.

## Vad du kommer att lära dig:
- Konfigurera din utvecklingsmiljö med GroupDocs.Signature för .NET.
- Steg-för-steg-instruktioner för att signera DICOM-bilder med QR-koder.
- Metoder för att verifiera och söka efter QR-kodsignaturer i DICOM-filer.
- Tekniker för att generera förhandsvisningar av signerade dokument för granskningsändamål.
- Bästa praxis för att optimera prestanda och hantera resurser effektivt.

Låt oss börja med förutsättningarna!

## Förkunskapskrav

För att använda GroupDocs.Signature för .NET, se till att din miljö är redo. Här är vad du behöver:

### Nödvändiga bibliotek och versioner
- **GroupDocs.Signature för .NET**Säkerställ kompatibilitet med ditt .NET-ramverk.

### Krav för miljöinstallation
- En utvecklingsmiljö på Windows eller Linux.
- Visual Studio eller annan .NET-kompatibel IDE installerad.

### Kunskapsförkunskaper
- Grundläggande förståelse för C#-programmering.
- Bekantskap med fil-I/O i .NET-applikationer.

## Konfigurera GroupDocs.Signature för .NET

Installera GroupDocs.Signature-biblioteket med din föredragna metod:

**Använda .NET CLI:**
```bash
dotnet add package GroupDocs.Signature
```

**Pakethanterare:**
```powershell
Install-Package GroupDocs.Signature
```

**NuGet-pakethanterarens användargränssnitt:**
- Sök efter "GroupDocs.Signature" och installera den senaste versionen.

### Licensförvärv

Börja med en gratis provperiod för att utforska funktionerna. För längre tids användning kan du överväga att skaffa en tillfällig eller fullständig licens från [Gruppdokument](https://purchase.groupdocs.com/buy).

När biblioteket är installerat, initiera det:

```csharp
using GroupDocs.Signature;
// Initiera signaturobjektet med din DICOM-filsökväg.
Signature signature = new Signature("YOUR_DOCUMENT_DIRECTORY\\sample.dicom");
```

## Implementeringsguide

### Signera DICOM-bild med QR-kod

#### Översikt
Lägg till QR-kodsignaturer för att säkerställa äkthet och spårbarhet av medicinska dokument.

**Steg 1: Initiera signaturobjektet**

```csharp
string filePath = "YOUR_DOCUMENT_DIRECTORY\\sample.dicom";
using (Signature signature = new Signature(filePath))
{
    // Fortsätt med signeringsåtgärderna...
}
```

**Steg 2: Skapa alternativ för QR-kodsignering**

Konfigurera egenskaper som text, storlek och justering.

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

**Steg 3: Lägg till XMP-metadata**

Förbättra dokumentet med ytterligare metadata.

```csharp
DicomSaveOptions dicomSaveOptions = new DicomSaveOptions()
{
    XmpEntries = new List<DicomXmpEntry>() { new DicomXmpEntry(DicomXmpType.PatientName, "Patient #4") }
};
```

**Steg 4: Signera dokumentet**

Utför signering och spara.

```csharp
SignResult signResult = signature.Sign("YOUR_OUTPUT_DIRECTORY\\SignedDicom", options, dicomSaveOptions);
```

### Hämta dokumentinformation

Hämta metadata från signerade DICOM-filer för att säkerställa dataintegritet.

**Översikt:**
Få åtkomst till dokumentinformation och XMP-metadatasignaturer för verifiering.

**Steg 1: Hämta dokumentinformation**

```csharp
using (Signature signature = new Signature("YOUR_DOCUMENT_DIRECTORY\\sample_signed.dicom"))
{
    IDocumentInfo signedDocumentInfo = signature.GetDocumentInfo();
}
```

**Steg 2: Iterera och skriv ut XMP-data**

Visa metadatadetaljer.

```csharp
foreach (var item in signedDocumentInfo.MetadataSignatures)
{
    Console.WriteLine(item.ToString());
}
```

### Verifiera DICOM-signaturer

Validera äktheten hos QR-kodsignaturer i DICOM-bilder.

**Översikt:**
Se till att underskrifterna är korrekta och autentiska.

**Steg 1: Skapa verifieringsalternativ för QR-koden**

Ange alternativ som matchar specifik text i QR-koderna.

```csharp
QrCodeVerifyOptions options = new QrCodeVerifyOptions()
{
    AllPages = true,
    Text = "Patient #36363393",
    MatchType = TextMatchType.Contains
};
```

**Steg 2: Verifiera signaturer**

Kontrollera om signaturerna uppfyller kriterierna.

```csharp
VerificationResult result = signature.Verify(options);

if (result.IsValid)
{
    Console.WriteLine($"DICOM {filePath} has {result.Succeeded.Count} successfully verified signatures!");
}
```

### Sök efter signaturer i DICOM

Leta reda på QR-kodsignaturer i signerade DICOM-bilder.

**Översikt:**
Hitta effektivt alla QR-kodsignaturer för att hantera dokumentäkthet.

**Steg 1: Sök efter QR-kodsignaturer**

```csharp
List<QrCodeSignature> signatures = signature.Search<QrCodeSignature>(SignatureType.QrCode);
```

**Steg 2: Iterera och skriv ut signaturdetaljer**

Granska informationen om varje funnen signatur.

```csharp
foreach (var QrCodeSignature in signatures)
{
    Console.WriteLine($"QRCode signature found at page {QrCodeSignature.PageNumber} with type {QrCodeSignature.EncodeType.TypeName} and text {QrCodeSignature.Text}");
}
```

### Generera förhandsgranskning av signerad DICOM

Skapa visuella förhandsvisningar för verifiering.

**Översikt:**
Generera förhandsgranskningar av bilder för att verifiera innehåll utan specialiserad programvara.

**Steg 1: Definiera strömmetoder**

Konfigurera metoder för hantering av filströmmar under generering av förhandsvisning.

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

**Steg 2: Generera förhandsvisningar**

Kör förhandsvisningsprocessen.

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

## Praktiska tillämpningar

1. **Hantering av medicinska journaler**Autentisera patientjournaler med hjälp av QR-kodsignaturer för efterlevnad.
2. **Revisionsspår i hälso- och sjukvårdssystem**Spåra dokumentändringar och verifiera äkthet med QR-koder.
3. **Säker datadelning**Säkerställ säker delning av medicinska bilder genom att bädda in digitala signaturer.
4. **Verifiering av efterlevnad**Kontrollera regelbundet DICOM-filernas integritet för att uppfylla lagkrav.
5. **Integration med elektroniska patientjournalsystem**Integrera sömlöst signerade DICOM-filer i elektroniska patientjournalsystem (EHR) för effektiviserad drift.