---
title: Bild mit Metadaten signieren
linktitle: Bild mit Metadaten signieren
second_title: GroupDocs.Signature .NET-API
description: Erfahren Sie, wie Sie mithilfe von GroupDocs.Signature Bilder mit Metadaten in .NET signieren. Einfache, effiziente und anpassbare Metadaten-Signaturlösung.
weight: 10
url: /de/net/document-signing/sign-image-with-metadata/
---
## Einführung
GroupDocs.Signature für .NET ermöglicht Entwicklern das effiziente Signieren von Bildern mit Metadaten. Dieses Tutorial führt Sie Schritt für Schritt durch den Prozess.
## Voraussetzungen
Bevor Sie beginnen, stellen Sie sicher, dass Sie über Folgendes verfügen:
1. GroupDocs.Signature für .NET: Installieren Sie das GroupDocs.Signature-Paket in Ihrem .NET-Projekt. Sie können es herunterladen unter[Hier](https://releases.groupdocs.com/signature/net/).   
2. Bilddatei: Bereiten Sie die Bilddatei vor, die Sie mit Metadaten signieren möchten.

## Namespaces importieren
Stellen Sie sicher, dass Sie die erforderlichen Namespaces in Ihren C#-Code importieren:
```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## Schritt 1: Bilddatei laden
Geben Sie zunächst den Pfad zu Ihrer Bilddatei und das Ausgabeverzeichnis für das signierte Bild mit Metadaten an:
```csharp
string filePath = "sample.png";            
string outputFilePath = Path.Combine("Your Document Directory", "SignImageWithMetadata", "SignedWithMetadata.png");
```
## Schritt 2: Metadatensignaturen erstellen
Erstellen Sie als Nächstes verschiedene Metadatensignaturen und fügen Sie sie der Optionssignatursammlung hinzu:
```csharp
using (Signature signature = new Signature(filePath))
{
    ushort imgsMetadataId = 41996;
    MetadataSignOptions options = new MetadataSignOptions();
    options
        .Add(new ImageMetadataSignature(imgsMetadataId++, "Mr.Scherlock Holmes")) // String-Wert
        .Add(new ImageMetadataSignature(imgsMetadataId++, DateTime.Now))          // Datum-Uhrzeit-Wert
        .Add(new ImageMetadataSignature(imgsMetadataId++, 123456))                // Integer Wert
        .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456D))              // Doppelter Wert
        .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456M))              // Dezimalwert
        .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456F));             // Float-Wert
    
    // Dokument unterzeichnen und ablegen
    SignResult result = signature.Sign(outputFilePath, options);
    Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).\nFile saved at {outputFilePath}.");
}
```

## Abschluss
In diesem Tutorial haben Sie gelernt, wie Sie mit GroupDocs.Signature für .NET ein Bild mit Metadaten signieren. Wenn Sie diese Schritte befolgen, können Sie problemlos Metadatensignaturen in Ihre .NET-Anwendungen integrieren.

## Häufig gestellte Fragen
### Kann ich mit GroupDocs.Signature für .NET mehrere Bilder mit Metadaten signieren?
Ja, Sie können mehrere Bilder mit Metadaten signieren, indem Sie jede Bilddatei durchlaufen und die Metadatensignaturen anwenden.
### Gibt es eine Testversion für GroupDocs.Signature für .NET?
 Ja, Sie können die Testversion hier herunterladen[Hier](https://releases.groupdocs.com/).
### Unterstützt GroupDocs.Signature für .NET neben Bildern auch andere Dateiformate?
Ja, GroupDocs.Signature unterstützt verschiedene Dateiformate, darunter PDF, Word, Excel und mehr.
### Kann ich das Erscheinungsbild der Metadatensignatur anpassen?
Ja, Sie können das Erscheinungsbild der Metadatensignatur anpassen, z. B. Schriftgröße, Farbe und Position.
### Wo erhalte ich Support für GroupDocs.Signature für .NET?
 Unterstützung erhalten Sie im GroupDocs.Signature-Forum[Hier](https://forum.groupdocs.com/c/signature/13).