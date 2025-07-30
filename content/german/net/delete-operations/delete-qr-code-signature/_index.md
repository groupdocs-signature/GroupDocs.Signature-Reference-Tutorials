---
"description": "Erfahren Sie in unserem Schritt-für-Schritt-Entwicklerhandbuch, wie Sie mit GroupDocs.Signature für .NET ganz einfach QR-Code-Signaturen aus Ihren Dokumenten löschen."
"linktitle": "QR-Code-Signatur aus Dokument löschen"
"second_title": "GroupDocs.Signature .NET API"
"title": "So entfernen Sie QR-Code-Signaturen aus Dokumenten in .NET"
"url": "/de/net/delete-operations/delete-qr-code-signature/"
"weight": 16
---

# So löschen Sie QR-Code-Signaturen aus Ihren Dokumenten

## Einführung

Mussten Sie schon einmal eine QR-Code-Signatur programmgesteuert aus einem Dokument entfernen? Ob Sie veraltete Informationen bereinigen oder Dokumente für die Weiterverteilung vorbereiten – die effektive Verwaltung von Dokumentsignaturen ist eine wichtige Fähigkeit für .NET-Entwickler.

In dieser benutzerfreundlichen Anleitung erfahren Sie, wie Sie QR-Code-Signaturen mit GroupDocs.Signature für .NET aus Dokumenten löschen. Diese leistungsstarke Bibliothek vereinfacht die Signaturverwaltung, sodass Sie sich auf die Entwicklung herausragender Anwendungen konzentrieren können, anstatt sich mit der Dokumentenbearbeitung herumzuschlagen.

## Was Sie vor dem Start benötigen

Bevor wir uns in den Code stürzen, stellen wir sicher, dass Sie alles bereit haben:

- GroupDocs.Signature für .NET: Sie benötigen die Bibliothek in Ihrem Projekt. Sie können sie direkt herunterladen von [die GroupDocs-Releases-Seite](https://releases.groupdocs.com/signature/net/).
- Ein Dokument mit QR-Codes: Bereiten Sie zur Übung ein Dokument vor, das mindestens eine QR-Code-Signatur enthält, die Sie entfernen möchten.
- Grundlegende C#-Kenntnisse: Sie sollten mit den Grundlagen von C# vertraut sein, um unseren Beispielen folgen zu können.

Sobald diese Voraussetzungen erfüllt sind, können Sie mit dem Entfernen dieser QR-Codes beginnen!

## Einrichten Ihres Projekts mit den richtigen Namespaces

Das Wichtigste zuerst – importieren wir die erforderlichen Namespaces, damit unser Code reibungslos funktioniert:

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

Diese Importe geben uns Zugriff auf alle Funktionen, die wir aus der GroupDocs.Signature-Bibliothek benötigen, sowie auf einige wichtige .NET-Klassen für die Dateiverwaltung.

## Schritt 1: Wo sind Ihre Dateien? Einrichten von Dokumentpfaden

Beginnen wir damit, zu definieren, wo sich unsere Dokumente befinden und wo wir die geänderte Version speichern möchten:

```csharp
// Der Pfad zum Dokumentenverzeichnis.
string filePath = "sample_multiple_signatures.docx";
string fileName = Path.GetFileName(filePath);

// Definieren Sie den Ausgabedateipfad für das geänderte Dokument.
string outputFilePath = Path.Combine("Your Document Directory", "DeleteQRCode", fileName);

// Kopieren Sie die Quelldatei, da die Löschmethode mit demselben Dokument funktioniert.
File.Copy(filePath, outputFilePath, true);
```

Beachten Sie, dass wir eine Kopie unseres Originaldokuments erstellen. Dies ist wichtig, da die Datei durch das Löschen der Signatur direkt geändert wird und wir unsere Originaldokumente stets erhalten möchten.

## Schritt 2: Erstellen eines Signaturobjekts zum Arbeiten

Jetzt erstellen wir ein Signaturobjekt, das eine Verbindung zu unserem Dokument herstellt:

```csharp
using (Signature signature = new Signature(outputFilePath))
{
    // Erstellen Sie Optionen zum Suchen von QR-Code-Signaturen.
    QrCodeSearchOptions options = new QrCodeSearchOptions();
    
    // Suchen Sie im Dokument nach QR-Code-Signaturen.
    List<QrCodeSignature> signatures = signature.Search<QrCodeSignature>(options);
```

Dieser Code initialisiert das Signaturobjekt mit unserem Dokument und sucht dann nach darin vorhandenen QR-Code-Signaturen. Die Suche gibt eine Liste aller gefundenen QR-Code-Signaturen zurück.

## Schritt 3: Gibt es QR-Codes zum Löschen?

Bevor wir versuchen, etwas zu löschen, sollten wir prüfen, ob tatsächlich QR-Codes vorhanden sind:

```csharp
    if (signatures.Count > 0)
    {
        // Holen Sie sich die erste im Dokument gefundene QR-Code-Signatur.
        QrCodeSignature qrCodeSignature = signatures[0];
```

Diese einfache Prüfung stellt sicher, dass wir nur fortfahren, wenn das Dokument mindestens eine QR-Code-Signatur enthält. In diesem Beispiel zielen wir auf den ersten gefundenen QR-Code ab. Sie können dies jedoch problemlos ändern, um bei Bedarf mehrere Signaturen zu verarbeiten.

## Schritt 4: Entfernen des QR-Codes aus Ihrem Dokument

Nun zum Hauptereignis – dem eigentlichen Löschen des QR-Codes:

```csharp
        // Löschen Sie die QR-Code-Signatur aus dem Dokument.
        bool result = signature.Delete(qrCodeSignature);
        
        if (result)
        {
            Console.WriteLine($"Signature with QR-Code '{qrCodeSignature.Text}' and encode type '{qrCodeSignature.EncodeType.TypeName}' was deleted from document ['{fileName}'].");
        }
        else
        {
            Console.WriteLine($"Signature was not deleted from the document! Signature with QR-Code '{qrCodeSignature.Text}' and encode type '{qrCodeSignature.EncodeType.TypeName}' was not found!");
        }
    }
}
```

Der Code löscht die Signatur und gibt Feedback darüber, ob der Vorgang erfolgreich war. Dieses Feedback ist entscheidend für das Debuggen und die Bestätigung, dass Ihr Code wie erwartet funktioniert.

## Was haben wir erreicht?

Herzlichen Glückwunsch! Sie haben gelernt, wie Sie QR-Code-Signaturen mit GroupDocs.Signature für .NET aus Dokumenten entfernen. Diese Fähigkeit eröffnet Ihnen zahlreiche Möglichkeiten für das Dokumentenmanagement in Ihren Anwendungen.

Mit nur wenigen Codezeilen können Sie Dokumente jetzt programmgesteuert bereinigen, indem Sie veraltete oder unnötige QR-Code-Signaturen entfernen und so sicherstellen, dass Ihre Dokumente immer nur die relevanten Informationen enthalten.

## Häufige Fragen, die Sie möglicherweise haben

### Kann ich mehrere QR-Codes gleichzeitig löschen?

Absolut! Anstatt nur die erste gefundene Signatur zu löschen, können Sie die gesamte Liste der Signaturen durchlaufen und jede einzelne wie folgt löschen:

```csharp
foreach(var qrSignature in signatures)
{
    signature.Delete(qrSignature);
}
```

### Welche anderen Arten von Signaturen kann ich mit GroupDocs.Signature verwalten?

GroupDocs.Signature ist unglaublich vielseitig und unterstützt verschiedene Signaturtypen, darunter:
- Textsignaturen
- Bildsignaturen
- Barcode-Signaturen
- Digitale Signaturen
- Und viele mehr!

### Funktioniert dies mit allen meinen Dokumentformaten?

Sie werden erfreut sein zu hören, dass GroupDocs.Signature mit einer Vielzahl von Dokumentformaten funktioniert, darunter:
- PDF-Dokumente
- Microsoft Word-Dokumente
- Excel-Tabellen
- PowerPoint-Präsentationen
- Und viele andere

### Kann ich nach bestimmten QR-Codes suchen, anstatt sie alle zu löschen?

Ja! Die `QrCodeSearchOptions` Die Klasse bietet verschiedene Eigenschaften zum Filtern Ihrer Suche. Sie können beispielsweise nach QR-Codes suchen, die bestimmten Text enthalten oder in bestimmten Formaten codiert sind.

### Gibt es eine Möglichkeit, GroupDocs.Signature vor dem Kauf auszuprobieren?

Ja, Sie können eine kostenlose Testversion herunterladen von [die GroupDocs-Website](https://releases.groupdocs.com/) um es mit Ihren spezifischen Anwendungsfällen zu testen, bevor Sie eine Verpflichtung eingehen.