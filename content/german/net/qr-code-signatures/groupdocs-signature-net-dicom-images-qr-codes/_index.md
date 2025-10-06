---
"date": "2025-05-07"
"description": "Erfahren Sie, wie Sie DICOM-Bilder mit QR-Codes mithilfe von GroupDocs.Signature für .NET signieren. Dieser Leitfaden behandelt die Einrichtung, Implementierung und Überprüfung von QR-Code-Signaturen in der medizinischen Bildgebung."
"title": "So signieren Sie DICOM-Bilder mit QR-Codes mithilfe von GroupDocs.Signature für .NET – Ein umfassender Leitfaden"
"url": "/de/net/qr-code-signatures/groupdocs-signature-net-dicom-images-qr-codes/"
"weight": 1
type: docs
---
# So signieren Sie DICOM-Bilder mit QR-Codes mithilfe von GroupDocs.Signature für .NET: Ein umfassender Leitfaden

Suchen Sie nach einer sicheren Methode zur Authentifizierung Ihrer DICOM-Dateien? Diese ausführliche Anleitung zeigt Ihnen, wie Sie mit GroupDocs.Signature für .NET QR-Code-Signaturen in DICOM-Bilder integrieren. Dieses Tutorial ist ideal für medizinisches Fachpersonal, Entwickler und alle, die mit digitalen medizinischen Dokumenten arbeiten. Es deckt die gesamte Einrichtung und Implementierung ab.

## Was Sie lernen werden:
- Einrichten Ihrer Entwicklungsumgebung mit GroupDocs.Signature für .NET.
- Schritt-für-Schritt-Anleitung zum Signieren von DICOM-Bildern mithilfe von QR-Codes.
- Methoden zum Überprüfen und Suchen von QR-Code-Signaturen in DICOM-Dateien.
- Techniken zum Generieren einer Vorschau signierter Dokumente zu Überprüfungszwecken.
- Best Practices zur Leistungsoptimierung und effektiven Ressourcenverwaltung.

Beginnen wir mit den Voraussetzungen!

## Voraussetzungen

Um GroupDocs.Signature für .NET zu verwenden, stellen Sie sicher, dass Ihre Umgebung bereit ist. Folgendes benötigen Sie:

### Erforderliche Bibliotheken und Versionen
- **GroupDocs.Signature für .NET**Stellen Sie die Kompatibilität mit Ihrem .NET-Framework sicher.

### Anforderungen für die Umgebungseinrichtung
- Eine Entwicklungsumgebung unter Windows oder Linux.
- Visual Studio oder eine andere .NET-kompatible IDE installiert.

### Erforderliche Kenntnisse
- Grundlegende Kenntnisse der C#-Programmierung.
- Vertrautheit mit Datei-E/A in .NET-Anwendungen.

## Einrichten von GroupDocs.Signature für .NET

Installieren Sie die Bibliothek GroupDocs.Signature mit Ihrer bevorzugten Methode:

**Verwenden der .NET-CLI:**
```bash
dotnet add package GroupDocs.Signature
```

**Paketmanager:**
```powershell
Install-Package GroupDocs.Signature
```

**NuGet-Paket-Manager-Benutzeroberfläche:**
- Suchen Sie nach „GroupDocs.Signature“ und installieren Sie die neueste Version.

### Lizenzerwerb

Starten Sie mit einer kostenlosen Testversion, um die Funktionen zu erkunden. Für eine erweiterte Nutzung können Sie eine temporäre oder Volllizenz erwerben. [Gruppendokumente](https://purchase.groupdocs.com/buy).

Initialisieren Sie die Bibliothek nach der Installation:

```csharp
using GroupDocs.Signature;
// Initialisieren Sie das Signaturobjekt mit Ihrem DICOM-Dateipfad.
Signature signature = new Signature("YOUR_DOCUMENT_DIRECTORY\\sample.dicom");
```

## Implementierungshandbuch

### DICOM-Bild mit QR-Code signieren

#### Überblick
Fügen Sie QR-Code-Signaturen hinzu, um die Authentizität und Rückverfolgbarkeit medizinischer Dokumente sicherzustellen.

**Schritt 1: Signaturobjekt initialisieren**

```csharp
string filePath = "YOUR_DOCUMENT_DIRECTORY\\sample.dicom";
using (Signature signature = new Signature(filePath))
{
    // Fahren Sie mit den Signiervorgängen fort ...
}
```

**Schritt 2: QR-Code-Sign-Optionen erstellen**

Konfigurieren Sie Eigenschaften wie Text, Größe und Ausrichtung.

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

**Schritt 3: XMP-Metadaten hinzufügen**

Erweitern Sie das Dokument mit zusätzlichen Metadaten.

```csharp
DicomSaveOptions dicomSaveOptions = new DicomSaveOptions()
{
    XmpEntries = new List<DicomXmpEntry>() { new DicomXmpEntry(DicomXmpType.PatientName, "Patient #4") }
};
```

**Schritt 4: Unterschreiben Sie das Dokument**

Signieren Sie und speichern Sie.

```csharp
SignResult signResult = signature.Sign("YOUR_OUTPUT_DIRECTORY\\SignedDicom", options, dicomSaveOptions);
```

### Dokumentinformationen abrufen

Rufen Sie Metadaten aus signierten DICOM-Dateien ab, um die Datenintegrität sicherzustellen.

**Überblick:**
Greifen Sie zur Überprüfung auf Dokumentinformationen und XMP-Metadatensignaturen zu.

**Schritt 1: Dokumentinformationen abrufen**

```csharp
using (Signature signature = new Signature("YOUR_DOCUMENT_DIRECTORY\\sample_signed.dicom"))
{
    IDocumentInfo signedDocumentInfo = signature.GetDocumentInfo();
}
```

**Schritt 2: Iterieren und Drucken von XMP-Daten**

Metadatendetails anzeigen.

```csharp
foreach (var item in signedDocumentInfo.MetadataSignatures)
{
    Console.WriteLine(item.ToString());
}
```

### DICOM-Signaturen überprüfen

Überprüfen Sie die Authentizität von QR-Code-Signaturen in DICOM-Bildern.

**Überblick:**
Stellen Sie sicher, dass die Unterschriften korrekt und authentisch sind.

**Schritt 1: Optionen zur QR-Code-Verifizierung erstellen**

Legen Sie Optionen fest, die zu bestimmtem Text in den QR-Codes passen.

```csharp
QrCodeVerifyOptions options = new QrCodeVerifyOptions()
{
    AllPages = true,
    Text = "Patient #36363393",
    MatchType = TextMatchType.Contains
};
```

**Schritt 2: Signaturen überprüfen**

Prüfen Sie, ob die Signaturen die Kriterien erfüllen.

```csharp
VerificationResult result = signature.Verify(options);

if (result.IsValid)
{
    Console.WriteLine($"DICOM {filePath} has {result.Succeeded.Count} successfully verified signatures!");
}
```

### Suche nach Signaturen in DICOM

Suchen Sie QR-Code-Signaturen in signierten DICOM-Bildern.

**Überblick:**
Finden Sie effizient alle QR-Code-Signaturen, um die Authentizität von Dokumenten zu verwalten.

**Schritt 1: Suche nach QR-Code-Signaturen**

```csharp
List<QrCodeSignature> signatures = signature.Search<QrCodeSignature>(SignatureType.QrCode);
```

**Schritt 2: Signaturdetails iterieren und drucken**

Überprüfen Sie die Details jeder gefundenen Signatur.

```csharp
foreach (var QrCodeSignature in signatures)
{
    Console.WriteLine($"QRCode signature found at page {QrCodeSignature.PageNumber} with type {QrCodeSignature.EncodeType.TypeName} and text {QrCodeSignature.Text}");
}
```

### Vorschau des signierten DICOM generieren

Erstellen Sie visuelle Vorschauen zur Überprüfung.

**Überblick:**
Erstellen Sie Bildvorschauen, um Inhalte ohne spezielle Software zu überprüfen.

**Schritt 1: Stream-Methoden definieren**

Richten Sie Methoden für die Dateistreamverwaltung während der Vorschaugenerierung ein.

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

**Schritt 2: Vorschauen generieren**

Führen Sie den Vorschaugenerierungsprozess aus.

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

## Praktische Anwendungen

1. **Verwaltung medizinischer Unterlagen**: Authentifizieren Sie Patientenakten zur Einhaltung der Vorschriften mithilfe von QR-Code-Signaturen.
2. **Prüfpfade in Gesundheitssystemen**: Verfolgen Sie Dokumentänderungen und überprüfen Sie die Echtheit mit QR-Codes.
3. **Sicherer Datenaustausch**: Sorgen Sie durch die Einbettung digitaler Signaturen für die sichere Weitergabe medizinischer Bilder.
4. **Konformitätsprüfung**: Überprüfen Sie regelmäßig die Integrität der DICOM-Dateien, um die gesetzlichen Anforderungen zu erfüllen.
5. **Integration mit EHR-Systemen**: Integrieren Sie signierte DICOM-Dateien nahtlos in elektronische Gesundheitsaktensysteme (EHR) für optimierte Abläufe.