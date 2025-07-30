---
"date": "2025-05-07"
"description": "Erfahren Sie, wie Sie PDF-Dokumente mit HIBC-QR-Codes mithilfe von GroupDocs.Signature für .NET signieren. Diese Anleitung behandelt LIC- und PAS-Codes, einschließlich QR-Code, Aztec-Code und DataMatrix."
"title": "So signieren Sie Dokumente mit HIBC-QR-Codes mithilfe von GroupDocs.Signature für .NET – Ein umfassender Leitfaden"
"url": "/de/net/qr-code-signatures/sign-documents-hibc-qr-groupdocs-dotnet/"
"weight": 1
---

# So signieren Sie Dokumente mit HIBC-QR-Codes mithilfe von GroupDocs.Signature für .NET

## Einführung

In der heutigen schnelllebigen Geschäftswelt ist die Gewährleistung der Authentizität und Integrität von Dokumenten von größter Bedeutung. Ob Sie mit Arzneimitteln, Gesundheitsprodukten oder Logistik arbeiten – eine sichere Methode zum Signieren und Verfolgen von Dokumenten spart Zeit und verhindert Fehler. Geben Sie ein **GroupDocs.Signature für .NET**, eine leistungsstarke Bibliothek zur Optimierung von Dokumentenverwaltungsprozessen durch die nahtlose Integration von HIBC-QR-Codes in Ihre Dokumente.

In diesem Tutorial erfahren Sie, wie Sie GroupDocs.Signature für .NET nutzen können, um PDF-Dokumente mit verschiedenen HIBC-QR-Codes – LIC (Lizenz) und PAS (Produktauthentifizierungssystem) – zu signieren, darunter QR-Code, Aztec-Code und DataMatrix. Am Ende verfügen Sie über ein solides Verständnis für die Implementierung dieser Lösungen in Ihren .NET-Anwendungen.

**Was Sie lernen werden:**
- So richten Sie GroupDocs.Signature für .NET ein
- Implementierung von HIBC LIC QR-Codes, Aztec-Codes und DataMatrix
- Hinzufügen von HIBC PAS QR-Codes, Aztec-Codes und DataMatrix
- Praktische Anwendungsfälle und Integrationsmöglichkeiten

Lassen Sie uns die Voraussetzungen genauer betrachten, bevor wir mit der Implementierung dieser Funktionen beginnen.

## Voraussetzungen

Bevor wir mit der Codierung beginnen, stellen Sie sicher, dass Sie Folgendes eingerichtet haben:

- **.NET-Umgebung**: Stellen Sie sicher, dass .NET auf Ihrem System installiert ist (vorzugsweise .NET Core oder .NET 5/6+).
- **GroupDocs.Signature für .NET**: Diese Bibliothek wird unser primäres Tool sein. Sie können sie über NuGet installieren.
- **Grundlegende Programmierkenntnisse**: Kenntnisse in C# und der Dateiverwaltung in .NET werden empfohlen.

### Erforderliche Bibliotheken

Um GroupDocs.Signature für .NET zu verwenden, müssen Sie das Paket mit einer der folgenden Methoden hinzufügen:

**.NET-CLI**
```bash
dotnet add package GroupDocs.Signature
```

**Paketmanager**
```powershell
Install-Package GroupDocs.Signature
```

**NuGet-Paket-Manager-Benutzeroberfläche**
Suchen Sie nach „GroupDocs.Signature“ und installieren Sie die neueste Version.

### Lizenzerwerb

Zu Testzwecken steht Ihnen eine kostenlose Testlizenz zur Verfügung. Für eine längere Nutzung können Sie ein Abonnement erwerben oder eine temporäre Lizenz anfordern:

- **Kostenlose Testversion**: Zugang [Hier](https://releases.groupdocs.com/signature/net/)
- **Temporäre Lizenz**: Anfrage an [dieser Link](https://purchase.groupdocs.com/temporary-license/)

### Umgebungseinrichtung

Richten Sie Ihre Umgebung ein, indem Sie sicherstellen, dass Ihr Projekt auf die entsprechende .NET-Version abzielt und Zugriff auf GroupDocs.Signature hat. Initialisieren Sie es in Ihrer Anwendung wie gezeigt:

```csharp
using GroupDocs.Signature;
```

## Einrichten von GroupDocs.Signature für .NET

Um GroupDocs.Signature für .NET zu verwenden, müssen Sie die Bibliothek installieren und eine grundlegende Einrichtung in Ihrem Projekt konfigurieren.

### Installation

Folgen Sie einer der oben genannten Methoden, um GroupDocs.Signature zu Ihrem Projekt hinzuzufügen. Stellen Sie nach der Installation sicher, dass Ihr Projekt für die Verwendung konfiguriert ist, indem Sie in Ihren Codedateien darauf verweisen.

### Lizenzinitialisierung

Nachdem Sie eine Lizenz erworben haben, initialisieren Sie diese wie folgt:

```csharp
SignatureConfig signConfig = new SignatureConfig();
signConfig.LicensePath = "path/to/your/license.lic";
Signature signature = new Signature("Sample.pdf", signConfig);
```

Mit dieser Einrichtung können Sie uneingeschränkt auf alle Funktionen von GroupDocs.Signature zugreifen.

## Implementierungshandbuch

Lassen Sie uns nun in die Implementierung der einzelnen Funktionen mithilfe von HIBC-QR-Codes mit GroupDocs.Signature für .NET eintauchen.

### Dokument mit HIBC LIC QR-Code signieren

#### Überblick

Das Signieren eines Dokuments mit einem HIBC LIC QR-Code gewährleistet Compliance und Rückverfolgbarkeit in Lizenzierungsszenarien. Dieser Abschnitt führt Sie durch die Erstellung und Einbettung eines QR-Codes in Ihre PDF-Dokumente.

#### Implementierungsschritte

##### Schritt 1: Konfigurieren Sie die Quell- und Ausgabepfade

Definieren Sie, wo sich Ihr Quelldokument befindet und wo die signierte Ausgabe gespeichert werden soll:

```csharp
string sourceFilePath = Path.Combine("YOUR_DOCUMENT_DIRECTORY", "Sample.pdf");
string outputPath = Path.Combine("YOUR_OUTPUT_DIRECTORY", "SignWithHIBCLICQR");
string destinFilePath = Path.Combine(outputPath, "SignedDocumentWithHIBCLICQR.pdf");
```

##### Schritt 2: QR-Code-Sign-Optionen erstellen

Konfigurieren Sie Ihren QR-Code mit spezifischem Text und Einstellungen:

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

    // Unterschreiben Sie das Dokument mit diesen Optionen.
    signature.Sign(destinFilePath, hibcLic_QR_Options);
}
```

**Erläuterung**: 
- `QrCodeSignOptions` richtet das Erscheinungsbild und den Inhalt des QR-Codes ein. Hier geben wir den HIBC LIC QR-Code-Typ an und positionieren ihn auf dem Dokument.
- `ReturnContent` Wenn dieser Wert auf „true“ gesetzt ist, können Sie ein gerendertes Bild des signierten Dokuments abrufen.

#### Tipps zur Fehlerbehebung

- Stellen Sie sicher, dass der Dokumentpfad richtig angegeben ist.
- Stellen Sie sicher, dass GroupDocs.Signature für die volle Funktionalität ordnungsgemäß lizenziert ist.

### Dokument mit HIBC LIC Aztec Code signieren

#### Überblick

Der Aztec-Code bietet eine weitere Form der Kodierung, die sich für die Speicherung von Informationen mit hoher Dichte eignet. Dieser Abschnitt konzentriert sich auf das Einbetten eines Aztec-Codes in Ihre Dokumente mithilfe von GroupDocs.Signature.

#### Implementierungsschritte

##### Schritt 1: Pfade konfigurieren

Definieren Sie Ihre Dateipfade ähnlich wie bei der vorherigen Funktion:

```csharp
string sourceFilePath = Path.Combine("YOUR_DOCUMENT_DIRECTORY", "Sample.pdf");
string outputPath = Path.Combine("YOUR_OUTPUT_DIRECTORY", "SignWithHIBCLICAztec");
string destinFilePath = Path.Combine(outputPath, "SignedDocumentWithHIBCLICAztec.pdf");
```

##### Schritt 2: Konfigurieren Sie die Aztec-Code-Optionen

Richten Sie Ihren Aztec-Code mit GroupDocs.Signature ein:

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

**Erläuterung**: 
- Der `QrCodeSignOptions` wird hier erneut verwendet, jedoch mit dem Aztec-Codetyp.
- Positionierung (`Top`, `Left`) und die Einstellungen zum Abrufen von Inhalten ähneln denen von QR-Codes.

#### Tipps zur Fehlerbehebung

- Bestätigen Sie, dass die Dateipfade korrekt sind.
- Stellen Sie sicher, dass die Version von GroupDocs.Signature Aztec-Codetypen unterstützt.

### Dokument mit HIBC LIC DataMatrix signieren

#### Überblick

Der DataMatrix-Code bietet eine weitere robuste Methode zum Speichern von Daten. Dieser Abschnitt zeigt, wie Sie eine DataMatrix in Ihre PDF-Dokumente integrieren.

#### Implementierungsschritte

##### Schritt 1: Dateipfade festlegen

Stellen Sie wie zuvor fest, wo sich Ihre Dateien befinden:

```csharp
string sourceFilePath = Path.Combine("YOUR_DOCUMENT_DIRECTORY", "Sample.pdf");
string outputPath = Path.Combine("YOUR_OUTPUT_DIRECTORY", "SignWithHIBCLICDataMatrix");
string destinFilePath = Path.Combine(outputPath, "SignedDocumentWithHIBCLICDataMatrix.pdf");
```

##### Schritt 2: DataMatrix-Signaturoptionen erstellen

Konfigurieren und wenden Sie den DataMatrix-Code an:

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

**Erläuterung**: 
- `QrCodeSignOptions` wird verwendet, um das Erscheinungsbild und den Inhalt des DataMatrix-Codes einzurichten.
- Positionierung (`Top`, `Left`) und Abrufeinstellungen folgen demselben Muster wie vorherige Codes.

#### Tipps zur Fehlerbehebung

- Stellen Sie sicher, dass alle Dateipfade korrekt angegeben sind.
- Stellen Sie sicher, dass GroupDocs.Signature in Ihrer Version DataMatrix-Codetypen unterstützt.

### Dokument mit HIBC PAS QR-Code signieren

#### Überblick

Das Signieren von Dokumenten mit einem HIBC PAS QR-Code verbessert die Produktverfolgung und -rückverfolgbarkeit. Dieser Abschnitt führt Sie durch das Einbetten eines PAS QR-Codes in PDFs mit GroupDocs.Signature.

#### Implementierungsschritte

##### Schritt 1: Konfigurieren Sie die Quell- und Ausgabepfade

Definieren Sie, wo sich Ihr Quelldokument befindet und wo die signierte Ausgabe gespeichert werden soll:

```csharp
string sourceFilePath = Path.Combine("YOUR_DOCUMENT_DIRECTORY", "Sample.pdf");
string outputPath = Path.Combine("YOUR_OUTPUT_DIRECTORY", "SignWithHIBCPASQR");
string destinFilePath = Path.Combine(outputPath, "SignedDocumentWithHIBCPASQR.pdf");
```

##### Schritt 2: QR-Code-Sign-Optionen erstellen

Konfigurieren Sie Ihren PAS-QR-Code mit spezifischem Text und Einstellungen:

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

    // Unterschreiben Sie das Dokument mit diesen Optionen.
    signature.Sign(destinFilePath, hibcPas_QR_Options);
}
```

**Erläuterung**: 
- `QrCodeSignOptions` ist für den HIBC PAS QR-Code-Typ konfiguriert und auf dem Dokument positioniert.
- `ReturnContent` Auf „true“ gesetzt, ruft ein gerendertes Bild des signierten Dokuments ab.

#### Tipps zur Fehlerbehebung

- Stellen Sie sicher, dass alle Pfade korrekt angegeben sind.
- Stellen Sie sicher, dass GroupDocs.Signature in Ihrer Version PAS-QR-Codetypen unterstützt.

### Abschluss

Mit dieser Anleitung können Sie HIBC LIC- und PAS-QR-Codes mithilfe von GroupDocs.Signature für .NET effizient in PDF-Dokumente integrieren. Dieser Prozess verbessert die Dokumentensicherheit, Rückverfolgbarkeit und Compliance in verschiedenen Branchen. Weitere Anpassungsmöglichkeiten und erweiterte Funktionen finden Sie im [GroupDocs-Dokumentation](https://docs.groupdocs.com/signature/net/).