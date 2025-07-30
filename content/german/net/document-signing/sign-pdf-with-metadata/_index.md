---
"description": "Integrieren Sie Metadatensignaturen in PDF-Dokumente mit GroupDocs.Signature für .NET. Erfahren Sie, wie Sie Autoreninformationen, Zeitstempel und benutzerdefinierte Daten einbetten, um die Authentizität und Rückverfolgbarkeit von PDF-Dokumenten zu verbessern."
"linktitle": "PDF mit Metadaten signieren"
"second_title": "GroupDocs.Signature .NET API"
"title": "Hinzufügen von Metadatensignaturen zu PDF-Dokumenten in C# .NET"
"url": "/de/net/document-signing/sign-pdf-with-metadata/"
"weight": 11
---

## Einführung

PDF-Dokumente (Portable Document Format) sind aufgrund ihrer Konsistenz und Plattformunabhängigkeit branchenübergreifend weit verbreitet. Die Gewährleistung der Authentizität und Rückverfolgbarkeit dieser Dokumente ist in vielen professionellen Umgebungen von entscheidender Bedeutung. Eine effektive Möglichkeit, dies zu erreichen, ist die Einbettung von Metadaten in die PDF-Dateien selbst.

In diesem umfassenden Tutorial erfahren Sie, wie Sie PDF-Dokumente mithilfe von GroupDocs.Signature für .NET mit Metadaten signieren. Mit Metadatensignaturen können Sie zusätzliche Informationen wie Autorendetails, Erstellungszeitstempel, Dokumentkennungen und benutzerdefinierte Werte in das Dokument einbetten, ohne das Erscheinungsbild des Dokuments sichtbar zu verändern.

## Voraussetzungen

Bevor wir beginnen, stellen Sie sicher, dass Sie Folgendes eingerichtet haben:

1. [GroupDocs.Signature für .NET](https://releases.groupdocs.com/signature/net/) - Laden Sie die Bibliothek herunter und installieren Sie sie
2. Entwicklungsumgebung – Visual Studio oder eine andere .NET-kompatible IDE
3. PDF-Dokument – Eine Beispiel-PDF-Datei zum Unterschreiben
4. Grundlegende C#-Kenntnisse – Vertrautheit mit der Programmiersprache C#

## Namespaces importieren

Beginnen Sie mit dem Importieren der erforderlichen Namespaces, um auf die GroupDocs.Signature-Funktionalität zuzugreifen:

```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

## Schritt 1: Dateipfade einrichten

Definieren Sie zunächst den Pfad zu Ihrem PDF-Dokument und geben Sie an, wo Sie die signierte Ausgabe speichern möchten:

```csharp
// Geben Sie den Pfad zu Ihrem PDF-Dokument an
string filePath = "sample.pdf";

// Definieren Sie das Ausgabeverzeichnis und den Dateipfad
string outputDirectory = "Your Document Directory";
string outputFilePath = Path.Combine(outputDirectory, "SignPdfWithMetadata", "SignedWithMetadata.pdf");

// Stellen Sie sicher, dass das Ausgabeverzeichnis vorhanden ist
Directory.CreateDirectory(Path.GetDirectoryName(outputFilePath));
```

## Schritt 2: Initialisieren des Signaturobjekts

Erstellen Sie eine Instanz der Signature-Klasse mit Ihrem PDF-Quelldokument:

```csharp
using (Signature signature = new Signature(filePath))
{
    // Der Code zum Signieren wird hier eingefügt
}
```

## Schritt 3: Metadatenoptionen definieren

Erstellen und konfigurieren Sie die Metadatenoptionen und fügen Sie verschiedene Arten von Metadatensignaturen hinzu:

```csharp
// Metadatenoptionsobjekt erstellen
MetadataSignOptions options = new MetadataSignOptions();

// Fügen Sie mithilfe der Fluent-Schnittstelle verschiedene Arten von Metadaten hinzu
options
    .Add(new PdfMetadataSignature("Author", "Mr.Sherlock Holmes")) // Zeichenfolgenwert
    .Add(new PdfMetadataSignature("CreatedOn", DateTime.Now))       // DateTime-Wert
    .Add(new PdfMetadataSignature("DocumentId", 123456))            // Ganzzahliger Wert
    .Add(new PdfMetadataSignature("SignatureId", 123.456D))         // Doppelter Wert
    .Add(new PdfMetadataSignature("Amount", 123.456M))              // Dezimalwert
    .Add(new PdfMetadataSignature("Total", 123.456F));              // Gleitkommawert
```

## Schritt 4: Signieren Sie das PDF mit Metadaten

Wenden Sie die Metadatensignaturen auf das PDF-Dokument an und speichern Sie das Ergebnis:

```csharp
// Signieren Sie das Dokument und speichern Sie es im Ausgabepfad
SignResult result = signature.Sign(outputFilePath, options);

// Erfolgsmeldung anzeigen
Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} metadata signature(s).");
Console.WriteLine($"Signed document saved at: {outputFilePath}");
```

## Vollständiges Beispiel

Hier ist das vollständige Codebeispiel, das alle Schritte zusammenfasst:

```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;

namespace SignPdfWithMetadataExample
{
    class Program
    {
        static void Main(string[] args)
        {
            // Dateipfade angeben
            string filePath = "sample.pdf";
            string outputFilePath = Path.Combine("Your Document Directory", "SignPdfWithMetadata", "SignedWithMetadata.pdf");
            
            // Stellen Sie sicher, dass das Ausgabeverzeichnis vorhanden ist
            Directory.CreateDirectory(Path.GetDirectoryName(outputFilePath));

            // Signieren Sie das PDF mit Metadaten
            using (Signature signature = new Signature(filePath))
            {
                // Metadatenoptionsobjekt erstellen
                MetadataSignOptions options = new MetadataSignOptions();
                
                // Fügen Sie verschiedene Arten von Metadatensignaturen hinzu
                options
                    .Add(new PdfMetadataSignature("Author", "Mr.Sherlock Holmes")) // Zeichenfolgenwert
                    .Add(new PdfMetadataSignature("CreatedOn", DateTime.Now))       // DateTime-Wert
                    .Add(new PdfMetadataSignature("DocumentId", 123456))            // Ganzzahliger Wert
                    .Add(new PdfMetadataSignature("SignatureId", 123.456D))         // Doppelter Wert
                    .Add(new PdfMetadataSignature("Amount", 123.456M))              // Dezimalwert
                    .Add(new PdfMetadataSignature("Total", 123.456F));              // Gleitkommawert
                
                // Dokument signieren und in Datei speichern
                SignResult result = signature.Sign(outputFilePath, options);
                
                // Ergebnisse anzeigen
                Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).");
                Console.WriteLine($"File saved at {outputFilePath}.");
            }
        }
    }
}
```

## Erweiterte PDF-Metadatenoperationen

### Hinzufügen benutzerdefinierter Metadaten mit Namespace-Unterstützung

PDF-Dokumente unterstützen benutzerdefinierte Metadaten mit XML-Namespace-Unterstützung:

```csharp
// Benutzerdefinierte Metadaten mit Namespace hinzufügen
options.Add(new PdfMetadataSignature("CustomProperty", "Custom Value")
{
    NamespaceUri = "http://Ihr-Namensraum.com/Schema"
});
```

### Suchen nach Metadaten in signierten PDFs

Nach der Signierung möchten Sie möglicherweise die Metadaten überprüfen oder extrahieren:

```csharp
// Suchoptionen für Metadaten erstellen
MetadataSearchOptions searchOptions = new MetadataSearchOptions();

// Suche nach Metadatensignaturen
SearchResult searchResult = signature.Search(searchOptions);

// Gefundene Signaturen anzeigen
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

### Arbeiten mit Standard-PDF-Metadaten

PDF-Dokumente verfügen über standardmäßige Metadatenfelder, auf die zugegriffen und die geändert werden können:

```csharp
// Festlegen von Standard-PDF-Metadatenfeldern
options
    .Add(new PdfMetadataSignature("Title", "Important Contract"))
    .Add(new PdfMetadataSignature("Subject", "Legal Agreement"))
    .Add(new PdfMetadataSignature("Keywords", "contract, agreement, legal, binding"))
    .Add(new PdfMetadataSignature("Creator", "Legal Department"))
    .Add(new PdfMetadataSignature("Producer", "GroupDocs.Signature"));
```

## Abschluss

In diesem Tutorial haben Sie gelernt, wie Sie PDF-Dokumente mit GroupDocs.Signature für .NET mit Metadaten signieren. Das Einbetten von Metadaten in PDF-Dateien bietet eine hervorragende Möglichkeit, die Authentizität von Dokumenten zu erhöhen, wichtige Informationen hinzuzufügen und die Workflows im Dokumentenmanagement zu verbessern.

Metadatensignaturen in PDF-Dateien sind besonders in Geschäftsumgebungen wertvoll, in denen die Rückverfolgbarkeit und Echtheitsprüfung von Dokumenten unerlässlich ist. Die eingebetteten Metadaten können Informationen über den Ursprung, den Autor, den Erstellungszeitpunkt, die Version und benutzerdefinierte Eigenschaften des Dokuments enthalten, die für den Workflow Ihres Unternehmens relevant sind.

Durch die Implementierung von Metadatensignaturen mit GroupDocs.Signature können Sie sicherstellen, dass Ihre PDF-Dokumente ihre Integrität bewahren und während ihres gesamten Lebenszyklus überprüfbare Informationen bereitstellen.

## Häufig gestellte Fragen

### Kann ich vorhandene Metadaten in einem PDF-Dokument ändern?

Ja, Sie können vorhandene Metadaten in PDF-Dokumenten ändern. Wenn Sie neue Metadatensignaturen mit denselben Namen wie die vorhandenen anwenden, werden die Werte entsprechend aktualisiert.

### Sind Metadatensignaturen in PDF-Dokumenten für den Endbenutzer sichtbar?

Metadatensignaturen sind im Dokumentinhalt selbst nicht sichtbar. Sie können jedoch über das Dokumenteigenschaftenfenster in PDF-Readern wie Adobe Acrobat oder mithilfe spezieller Tools zur Anzeige von Metadaten angezeigt werden.

### Kann ich die Metadaten in PDFs verschlüsseln oder schützen?

GroupDocs.Signature bietet Optionen zum Sichern von Dokumenten, einschließlich Verschlüsselung. Sie können die Verschlüsselung auf Dokumentebene anwenden, um das gesamte PDF einschließlich der Metadaten zu schützen.

### Gibt es eine Begrenzung für die Menge an Metadaten, die ich zu einer PDF-Datei hinzufügen kann?

Obwohl die PDF-Spezifikation keine strikte Beschränkung vorsieht, kann das Hinzufügen übermäßiger Metadaten die Dateigröße erhöhen. Es wird empfohlen, nur relevante und notwendige Informationen in die Metadaten aufzunehmen.

### Kann ich programmgesteuert überprüfen, ob eine PDF-Datei nach dem Hinzufügen von Metadaten manipuliert wurde?

Ja, GroupDocs.Signature bietet Überprüfungsfunktionen, mit denen festgestellt werden kann, ob ein Dokument nach der Signierung geändert wurde, einschließlich Änderungen an Metadaten.

### Wo finde ich weitere Ressourcen und Unterstützung?

- [API-Referenz](https://reference.groupdocs.com/signature/net/)
- [Downloads](https://releases.groupdocs.com/signature/net/)
- [Beispiele](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
- [Dokumentation](https://docs.groupdocs.com/signature/net/)
- [Produktseite](https://products.groupdocs.com/signature/net/)
- [Der Blog](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
- [Support-Forum](https://forum.groupdocs.com/c/signature/13)
- [Temporäre Lizenz](https://purchase.groupdocs.com/temporary-license/)