---
"description": "Erfahren Sie, wie Sie mit GroupDocs.Signature für .NET Metadaten in Bilder signieren und einbetten. Fügen Sie Autoreninformationen, Zeitstempel und benutzerdefinierte Daten hinzu, um die Authentizität und Rückverfolgbarkeit von Bildern zu verbessern."
"linktitle": "Bild mit Metadaten signieren"
"second_title": "GroupDocs.Signature .NET API"
"title": "Signieren Sie Bilder mit Metadaten in C# .NET"
"url": "/de/net/document-signing/sign-image-with-metadata/"
"weight": 10
---

## Einführung

Die digitale Bildsignierung mit Metadaten wird für die Authentizität, Eigentumsverhältnisse und Rückverfolgbarkeit immer wichtiger. GroupDocs.Signature für .NET bietet eine leistungsstarke und dennoch benutzerfreundliche Lösung zum Hinzufügen von Metadatensignaturen zu verschiedenen Bildformaten. Dieses Tutorial führt Sie durch den gesamten Prozess der Bildsignierung mit Metadaten in C#.

Mithilfe von Metadatensignaturen können Sie wertvolle Informationen wie Autoreninformationen, Erstellungszeitstempel, eindeutige Kennungen und mehr direkt in Bilddateien einbetten. Diese Informationen werden Teil der Bilddatei selbst und bieten eine zuverlässige Methode zur Verfolgung und Überprüfung der Bildauthentizität.

## Voraussetzungen

Bevor Sie mit diesem Lernprogramm fortfahren, stellen Sie sicher, dass Sie über Folgendes verfügen:

1. [GroupDocs.Signature für .NET](https://releases.groupdocs.com/signature/net/) - Laden Sie die Bibliothek herunter und installieren Sie sie
2. Entwicklungsumgebung – Visual Studio oder jede kompatible IDE mit .NET-Unterstützung
3. Bilddatei – Eine Beispielbilddatei in einem unterstützten Format (PNG, JPG, TIFF usw.)
4. Grundlegende C#-Programmierkenntnisse – Vertrautheit mit C#-Programmierkonzepten

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

Definieren Sie die Pfade für Ihr Quellbild und wo die signierte Ausgabe gespeichert werden soll:

```csharp
// Geben Sie den Pfad zu Ihrer Quellbilddatei an
string filePath = "sample.png";

// Definieren Sie das Ausgabeverzeichnis und den Dateinamen für das signierte Bild
string outputDirectory = "Your Document Directory";
string outputFilePath = Path.Combine(outputDirectory, "SignImageWithMetadata", "SignedWithMetadata.png");

// Stellen Sie sicher, dass das Ausgabeverzeichnis vorhanden ist
Directory.CreateDirectory(Path.GetDirectoryName(outputFilePath));
```

## Schritt 2: Initialisieren des Signaturobjekts

Erstellen Sie eine Instanz der Signature-Klasse mit Ihrer Quellbilddatei:

```csharp
using (Signature signature = new Signature(filePath))
{
    // Der Rest des Codes kommt hierhin
}
```

## Schritt 3: Erstellen und Konfigurieren von Metadatensignaturen

Definieren Sie anschließend die Metadaten, die Sie in das Bild einbetten möchten. GroupDocs.Signature unterstützt verschiedene Datentypen für Metadaten:

```csharp
// Metadaten-ID initialisieren (spezifisch für das Bildformat)
ushort imgsMetadataId = 41996;

// Metadatenoptionsobjekt erstellen
MetadataSignOptions options = new MetadataSignOptions();

// Fügen Sie verschiedene Arten von Metadatensignaturen hinzu
options
    .Add(new ImageMetadataSignature(imgsMetadataId++, "Mr.Sherlock Holmes"))  // Zeichenfolgenwert
    .Add(new ImageMetadataSignature(imgsMetadataId++, DateTime.Now))          // Datums./Uhrzeitwert
    .Add(new ImageMetadataSignature(imgsMetadataId++, 123456))                // Ganzzahliger Wert
    .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456D))              // Doppelter Wert
    .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456M))              // Dezimalwert
    .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456F));             // Gleitkommawert
```

## Schritt 4: Signieren Sie das Bild mit Metadaten

Wenden Sie die Metadatensignaturen auf das Bild an und speichern Sie das Ergebnis:

```csharp
// Signieren Sie das Dokument und speichern Sie es im Ausgabedateipfad
SignResult result = signature.Sign(outputFilePath, options);

// Erfolgsmeldung anzeigen
Console.WriteLine($"\nSource image signed successfully with {result.Succeeded.Count} metadata signature(s).");
Console.WriteLine($"Signed image saved at: {outputFilePath}");
```

## Vollständiges Beispiel

Hier ist das vollständige Codebeispiel, das alle Schritte zusammenfasst:

```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;

namespace SignImageWithMetadataExample
{
    class Program
    {
        static void Main(string[] args)
        {
            // Dateipfade angeben
            string filePath = "sample.png";            
            string outputFilePath = Path.Combine("Your Document Directory", "SignImageWithMetadata", "SignedWithMetadata.png");
            
            // Stellen Sie sicher, dass das Ausgabeverzeichnis vorhanden ist
            Directory.CreateDirectory(Path.GetDirectoryName(outputFilePath));

            // Signieren Sie das Bild mit Metadaten
            using (Signature signature = new Signature(filePath))
            {
                // Metadaten-ID initialisieren (spezifisch für das Bildformat)
                ushort imgsMetadataId = 41996;
                
                // Optionen zum Erstellen von Metadaten
                MetadataSignOptions options = new MetadataSignOptions();
                
                // Fügen Sie verschiedene Arten von Metadatensignaturen hinzu
                options
                    .Add(new ImageMetadataSignature(imgsMetadataId++, "Mr.Sherlock Holmes")) // Zeichenfolgenwert
                    .Add(new ImageMetadataSignature(imgsMetadataId++, DateTime.Now))          // Datums./Uhrzeitwert
                    .Add(new ImageMetadataSignature(imgsMetadataId++, 123456))                // Ganzzahliger Wert
                    .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456D))              // Doppelter Wert
                    .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456M))              // Dezimalwert
                    .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456F));             // Gleitkommawert
                
                // Dokument signieren und in Datei speichern
                SignResult result = signature.Sign(outputFilePath, options);
                
                // Ergebnisse anzeigen
                Console.WriteLine($"\nSource image signed successfully with {result.Succeeded.Count} signature(s).");
                Console.WriteLine($"File saved at {outputFilePath}.");
            }
        }
    }
}
```

## Erweiterte Techniken zur Metadatensignatur

### Arbeiten mit benutzerdefinierten Metadaten

Sie können auch benutzerdefinierte Metadatenfelder mit bestimmten IDs erstellen:

```csharp
// Erstellen Sie benutzerdefinierte Metadaten mit einer bestimmten ID
options.Add(new ImageMetadataSignature(42000, "CustomValue"));
```

### Überprüfen von Metadatensignaturen

Nach der Signierung möchten Sie möglicherweise die Metadatensignaturen überprüfen:

```csharp
// Erstellen Sie Überprüfungsoptionen
MetadataSearchOptions searchOptions = new MetadataSearchOptions();

// Suche nach Metadatensignaturen
SearchResult result = signature.Search(searchOptions);

// Gefundene Signaturen anzeigen
Console.WriteLine($"Found {result.Signatures.Count} metadata signatures:");
foreach(var metadataSignature in result.Signatures)
{
    Console.WriteLine($"- {metadataSignature.Name}: {metadataSignature.Value}");
}
```

## Abschluss

In diesem Tutorial haben Sie gelernt, wie Sie Bilder mit GroupDocs.Signature für .NET mit Metadaten signieren. Das Einbetten von Metadaten in Bilder bietet eine hervorragende Möglichkeit, die Bildauthentizität zu erhöhen, wichtige Informationen hinzuzufügen und die Workflows im Dokumentenmanagement zu verbessern. Der Prozess ist unkompliziert und dennoch leistungsstark und ermöglicht eine individuelle Anpassung an Ihre Anforderungen.

Die in der Bilddatei eingebetteten Metadaten können für verschiedene Zwecke verwendet werden, z. B. zum Schutz des Urheberrechts, zur Rückverfolgung der Bildherkunft, zum Hinzufügen beschreibender Informationen und zur Erstellung einer digitalen Verwahrungskette. Durch die Implementierung von Metadatensignaturen stellen Sie sicher, dass Ihre Bilder während ihres gesamten Lebenszyklus ihre Integrität und Authentizität bewahren.

## Häufig gestellte Fragen

### Kann ich vorhandenen signierten Bildern Metadaten hinzufügen?

Ja, Sie können Bildern, die bereits Metadatensignaturen enthalten, zusätzliche Metadaten hinzufügen. Die vorhandenen Metadaten bleiben erhalten und neue Metadaten werden entsprechend hinzugefügt.

### Welche Bildformate werden für die Metadatensignatur unterstützt?

GroupDocs.Signature für .NET unterstützt die Metadatensignatur für verschiedene Bildformate, darunter PNG, JPEG, TIFF, BMP, GIF und mehr. Eine vollständige Liste finden Sie im [offizielle Dokumentation](https://docs.groupdocs.com/signature/net/).

### Ist es möglich, die Metadaten in Bildern zu verschlüsseln?

Ja, GroupDocs.Signature bietet Optionen zum Verschlüsseln von Metadaten für erhöhte Sicherheit. Sie können die von der Bibliothek bereitgestellten Verschlüsselungsoptionen verwenden, um vertrauliche Metadateninformationen zu schützen.

### Kann ich die Authentizität signierter Bilder programmgesteuert überprüfen?

Absolut. Sie können die Verifizierungsmethoden in GroupDocs.Signature verwenden, um Metadatensignaturen zu validieren und die Authentizität signierter Bilder zu bestätigen.

### Gibt es eine Dateigrößenbeschränkung beim Signieren von Bildern mit Metadaten?

Die Bibliothek selbst gibt keine spezifische Dateigrößenbeschränkung vor, sehr große Dateien benötigen jedoch möglicherweise mehr Verarbeitungszeit und Speicher. Es wird empfohlen, bei der Arbeit mit extrem großen Bildern die Systemressourcen zu berücksichtigen.

### Wie kann ich eine temporäre Lizenz zu Testzwecken erhalten?

Sie erhalten eine [vorläufige Lizenz](https://purchase.groupdocs.com/temporary-license/) zum Testen von GroupDocs.Signature vor dem Kauf.

### Wo finde ich weitere Ressourcen und Unterstützung?

- [API-Referenz](https://reference.groupdocs.com/signature/net/)
- [Downloads](https://releases.groupdocs.com/signature/net/)
- [Beispiele](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
- [Dokumentation](https://docs.groupdocs.com/signature/net/)
- [Produktseite](https://products.groupdocs.com/signature/net/)
- [Der Blog](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
- [Support-Forum](https://forum.groupdocs.com/c/signature/13)