---
"description": "Schützen und verbessern Sie Excel-Tabellen durch die Einbettung von Metadatensignaturen mit GroupDocs.Signature für .NET. Fügen Sie Autoreninformationen, Zeitstempel und benutzerdefinierte Daten hinzu, um die Rückverfolgbarkeit und Authentizität von Dokumenten zu verbessern."
"linktitle": "Tabellenkalkulation mit Metadaten signieren"
"second_title": "GroupDocs.Signature .NET API"
"title": "Hinzufügen von Metadatensignaturen zu Excel-Tabellen in C# .NET"
"url": "/de/net/document-signing/sign-spreadsheet-with-metadata/"
"weight": 13
---

## Einführung

Excel-Tabellen enthalten häufig wichtige Geschäftsdaten, Finanzinformationen und Berechnungen. Die Sicherstellung ihrer Authentizität, die Rückverfolgung ihrer Herkunft und der Schutz ihrer Integrität sind in vielen professionellen Umgebungen von entscheidender Bedeutung. Ein effektiver Ansatz zur Verbesserung der Sicherheit und Rückverfolgbarkeit von Tabellen ist die Einbettung von Metadatensignaturen.

Dieses umfassende Tutorial führt Sie durch den Prozess der Signatur von Excel-Tabellen mit Metadaten mithilfe von GroupDocs.Signature für .NET. Durch das Hinzufügen von Metadatensignaturen können Sie wertvolle Informationen wie Autorendetails, Erstellungszeitstempel, Dokumentkennungen und andere benutzerdefinierte Eigenschaften direkt in die Tabellenstruktur einbetten.

## Voraussetzungen

Bevor Sie mit diesem Lernprogramm fortfahren, stellen Sie sicher, dass Sie über Folgendes verfügen:

1. [GroupDocs.Signature für .NET](https://releases.groupdocs.com/signature/net/) - Laden Sie die Bibliothek herunter und installieren Sie sie
2. Entwicklungsumgebung – Visual Studio oder eine andere .NET-kompatible IDE
3. Excel-Tabelle – Eine Beispiel-Tabellenkalkulationsdatei (XLSX, XLS usw.)
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

Definieren Sie die Pfade für Ihre Quelltabelle und den Speicherort der signierten Ausgabe:

```csharp
// Geben Sie den Pfad zu Ihrer Excel-Datei an
string filePath = "sample.xlsx";

// Definieren Sie das Ausgabeverzeichnis und den Dateinamen für die signierte Tabelle
string outputDirectory = "Your Document Directory";
string outputFilePath = Path.Combine(outputDirectory, "SignSpreadsheetWithMetadata", "SignedWithMetadata.xlsx");

// Stellen Sie sicher, dass das Ausgabeverzeichnis vorhanden ist
Directory.CreateDirectory(Path.GetDirectoryName(outputFilePath));
```

## Schritt 2: Initialisieren des Signaturobjekts

Erstellen Sie eine Instanz der Signature-Klasse mit Ihrer Quelltabellendatei:

```csharp
using (Signature signature = new Signature(filePath))
{
    // Der Rest des Codes kommt hierhin
}
```

## Schritt 3: Erstellen und Konfigurieren von Metadatensignaturen

Definieren Sie als Nächstes die Metadatenoptionen und erstellen Sie ein Array von Metadatensignaturen für Tabellenkalkulationen:

```csharp
// Metadatenoptionsobjekt erstellen
MetadataSignOptions options = new MetadataSignOptions();

// Erstellen Sie ein Array von Tabellenkalkulationsmetadatensignaturen mit unterschiedlichen Datentypen
SpreadsheetMetadataSignature[] signatures = new SpreadsheetMetadataSignature[]
{
    new SpreadsheetMetadataSignature("Author", "Mr.Sherlock Holmes"), // Zeichenfolgenwert
    new SpreadsheetMetadataSignature("CreatedOn", DateTime.Now),      // DateTime-Wert
    new SpreadsheetMetadataSignature("DocumentId", 123456),           // Ganzzahliger Wert
    new SpreadsheetMetadataSignature("SignatureId", 123.456D),        // Doppelter Wert
    new SpreadsheetMetadataSignature("Amount", 123.456M),             // Dezimalwert
    new SpreadsheetMetadataSignature("Total", 123.456F)               // Gleitkommawert
};

// Signatursammlung zu Optionen hinzufügen
options.Signatures.AddRange(signatures);
```

## Schritt 4: Signieren Sie die Tabelle mit Metadaten

Wenden Sie die Metadatensignaturen auf die Tabelle an und speichern Sie das Ergebnis:

```csharp
// Signieren Sie das Dokument und speichern Sie es im Ausgabedateipfad
SignResult result = signature.Sign(outputFilePath, options);

// Erfolgsmeldung anzeigen
Console.WriteLine($"\nSource spreadsheet signed successfully with {result.Succeeded.Count} metadata signature(s).");
Console.WriteLine($"Signed spreadsheet saved at: {outputFilePath}");
```

## Vollständiges Beispiel

Hier ist das vollständige Codebeispiel, das alle Schritte zusammenfasst:

```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;

namespace SignSpreadsheetWithMetadataExample
{
    class Program
    {
        static void Main(string[] args)
        {
            // Dateipfade angeben
            string filePath = "sample.xlsx";
            string outputFilePath = Path.Combine("Your Document Directory", "SignSpreadsheetWithMetadata", "SignedWithMetadata.xlsx");
            
            // Stellen Sie sicher, dass das Ausgabeverzeichnis vorhanden ist
            Directory.CreateDirectory(Path.GetDirectoryName(outputFilePath));

            // Signieren Sie die Tabelle mit Metadaten
            using (Signature signature = new Signature(filePath))
            {
                // Metadatenoptionsobjekt erstellen
                MetadataSignOptions options = new MetadataSignOptions();
                
                // Erstellen Sie ein Array von Tabellenkalkulationsmetadatensignaturen mit unterschiedlichen Datentypen
                SpreadsheetMetadataSignature[] signatures = new SpreadsheetMetadataSignature[]
                {
                    new SpreadsheetMetadataSignature("Author", "Mr.Sherlock Holmes"), // Zeichenfolgenwert
                    new SpreadsheetMetadataSignature("CreatedOn", DateTime.Now),      // DateTime-Wert
                    new SpreadsheetMetadataSignature("DocumentId", 123456),           // Ganzzahliger Wert
                    new SpreadsheetMetadataSignature("SignatureId", 123.456D),        // Doppelter Wert
                    new SpreadsheetMetadataSignature("Amount", 123.456M),             // Dezimalwert
                    new SpreadsheetMetadataSignature("Total", 123.456F)               // Gleitkommawert
                };
                
                // Signatursammlung zu Optionen hinzufügen
                options.Signatures.AddRange(signatures);
                
                // Dokument signieren und in Datei speichern
                SignResult result = signature.Sign(outputFilePath, options);
                
                // Ergebnisse anzeigen
                Console.WriteLine($"\nSource spreadsheet signed successfully with {result.Succeeded.Count} signature(s).");
                Console.WriteLine($"File saved at {outputFilePath}.");
            }
        }
    }
}
```

## Erweiterte Tabellenkalkulations-Metadatentechniken

### Arbeiten mit benutzerdefinierten und integrierten Tabellenkalkulationseigenschaften

Excel-Tabellen verfügen über integrierte und benutzerdefinierte Eigenschaften, auf die über den Dateieigenschaftendialog zugegriffen werden kann. GroupDocs.Signature ermöglicht Ihnen die Arbeit mit beiden:

```csharp
// Integrierte Eigenschaften hinzufügen
signatures = new SpreadsheetMetadataSignature[]
{
    new SpreadsheetMetadataSignature("Company", "Sherlock Holmes Consulting"),
    new SpreadsheetMetadataSignature("Category", "Financial"),
    new SpreadsheetMetadataSignature("Keywords", "budget,forecast,analysis"),
    new SpreadsheetMetadataSignature("Comments", "This spreadsheet contains confidential information"),
    new SpreadsheetMetadataSignature("Manager", "John Watson")
};
options.Signatures.AddRange(signatures);

// Hinzufügen benutzerdefinierter Eigenschaften
options.Signatures.Add(new SpreadsheetMetadataSignature("Department", "Finance"));
options.Signatures.Add(new SpreadsheetMetadataSignature("SecurityLevel", "Confidential"));
```

### Suchen nach Metadaten in signierten Tabellen

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

### Aktualisieren vorhandener Metadaten

Sie können vorhandene Metadaten in Tabellenkalkulationen aktualisieren, indem Sie dieselben Eigenschaftsnamen verwenden:

```csharp
// Aktualisieren vorhandener Metadaten
options.Signatures.Add(new SpreadsheetMetadataSignature("Author", "Updated Author Name"));
```

## Abschluss

In diesem umfassenden Tutorial haben Sie gelernt, wie Sie Excel-Tabellen mit Metadaten mithilfe von GroupDocs.Signature für .NET signieren. Das Einbetten von Metadaten in Tabellenkalkulationsdateien verbessert die Nachverfolgbarkeit von Dokumenten, liefert wertvollen Kontext und trägt zur Authentizität bei.

Metadatensignaturen in Tabellenkalkulationen sind besonders in Geschäftsumgebungen nützlich, in denen Dokumentherkunft, Autorschaft und Versionsverfolgung wichtig sind. Die eingebetteten Metadaten können Informationen über den Autor, den Erstellungszeitpunkt, Dokumentkennungen und benutzerdefinierte Eigenschaften enthalten, die für die Anforderungen Ihres Unternehmens relevant sind.

Durch die Implementierung von Metadatensignaturen mit GroupDocs.Signature können Sie sicherstellen, dass Ihre Excel-Tabellen ihre Integrität bewahren und während ihres gesamten Lebenszyklus überprüfbare Informationen bereitstellen.

## Häufig gestellte Fragen

### Kann ich Tabellenkalkulationen, für die bereits einige Eigenschaften definiert sind, Metadaten hinzufügen?

Ja, Sie können neue Metadaten hinzufügen oder vorhandene Metadaten in Tabellen aktualisieren. GroupDocs.Signature übernimmt die Integration, indem es entweder neue Eigenschaften hinzufügt oder vorhandene mit denselben Namen aktualisiert.

### Welche Tabellenkalkulationsformate werden für die Metadatensignatur unterstützt?

GroupDocs.Signature für .NET unterstützt die Metadatensignatur für verschiedene Tabellenkalkulationsformate, darunter XLSX, XLS, XLSM, ODS und mehr. Eine vollständige Liste finden Sie im [offizielle Dokumentation](https://docs.groupdocs.com/signature/net/).

### Sind Metadatensignaturen in Tabellenkalkulationen für die Benutzer sichtbar?

Metadatensignaturen sind im Tabelleninhalt selbst nicht sichtbar. Sie können jedoch über das Dokumenteigenschaftenfenster in Excel oder anderen kompatiblen Anwendungen angezeigt werden.

### Kann ich programmgesteuert überprüfen, ob eine Tabelle nach dem Hinzufügen von Metadaten manipuliert wurde?

Ja, GroupDocs.Signature bietet Überprüfungsfunktionen, mit denen festgestellt werden kann, ob ein Dokument nach der Signierung geändert wurde, einschließlich Änderungen an Metadaten.

### Beeinträchtigt das Hinzufügen von Metadaten die Tabellenkalkulationsfunktionalität?

Das Hinzufügen von Metadaten hat nur minimale Auswirkungen auf die Dateigröße und keine Auswirkungen auf die Tabellenkalkulationsfunktionalität. Es ist eine einfache Möglichkeit, Dokumenteigenschaften zu verbessern, ohne Berechnungen, Formeln oder andere Excel-Funktionen zu beeinträchtigen.

### Wo finde ich weitere Ressourcen und Unterstützung?

- [API-Referenz](https://reference.groupdocs.com/signature/net/)
- [Downloads](https://releases.groupdocs.com/signature/net/)
- [Beispiele](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
- [Dokumentation](https://docs.groupdocs.com/signature/net/)
- [Produktseite](https://products.groupdocs.com/signature/net/)
- [Der Blog](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
- [Support-Forum](https://forum.groupdocs.com/c/signature/13)
- [Temporäre Lizenz](https://purchase.groupdocs.com/temporary-license/)