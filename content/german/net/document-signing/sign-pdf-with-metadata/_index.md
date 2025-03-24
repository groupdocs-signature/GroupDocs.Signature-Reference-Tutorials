---
title: PDF mit Metadaten signieren
linktitle: PDF mit Metadaten signieren
second_title: GroupDocs.Signature .NET-API
description: Erfahren Sie, wie Sie PDF-Dokumente mit Metadaten mit GroupDocs.Signature für .NET signieren. Verbessern Sie ganz einfach die Rückverfolgbarkeit und Authentizität von Dokumenten.
weight: 11
url: /de/net/document-signing/sign-pdf-with-metadata/
---
## Einführung
In diesem Tutorial erfahren Sie, wie Sie mithilfe von GroupDocs.Signature für .NET ein PDF-Dokument mit Metadaten signieren. Durch das Hinzufügen von Metadaten zu einer PDF-Datei können zusätzliche Informationen über das Dokument bereitgestellt werden, z. B. Autorschaft, Erstellungsdatum, Dokument-ID und mehr.
## Voraussetzungen
Bevor wir beginnen, stellen Sie sicher, dass Sie über Folgendes verfügen:
1.  GroupDocs.Signature für .NET: Sie können es herunterladen unter[Hier](https://releases.groupdocs.com/signature/net/).
2. Ein PDF-Dokument: Halten Sie eine Beispiel-PDF-Datei zum Signieren bereit.
3. Grundkenntnisse der C#-Programmierung: Zum Verständnis der Codebeispiele sind Kenntnisse der C#-Syntax erforderlich.
## Namespaces importieren
Stellen Sie zunächst sicher, dass Sie die erforderlichen Namespaces importieren, um auf die erforderlichen Klassen und Methoden zuzugreifen:
```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## Schritt 1: Laden Sie das PDF-Dokument
Laden Sie das PDF-Dokument, das Sie signieren möchten:
```csharp
string filePath = "sample.pdf";
```
## Schritt 2: Geben Sie den Pfad der Ausgabedatei an
Definieren Sie den Ausgabedateipfad, in dem das signierte PDF mit Metadaten gespeichert wird:
```csharp
string outputFilePath = Path.Combine("Your Document Directory", "SignPdfWithMetadata", "SignedWithMetadata.pdf");
```
## Schritt 3: Signaturinstanz erstellen
Initialisieren Sie eine Signature-Instanz, indem Sie den Pfad zum PDF-Dokument angeben:
```csharp
using (Signature signature = new Signature(filePath))
{
    // Der signaturbezogene Code wird hier angezeigt
}
```
## Schritt 4: Metadatenoptionen definieren
Erstellen Sie MetadataSignOptions und fügen Sie Metadatenfelder mit ihren jeweiligen Werten hinzu:
```csharp
MetadataSignOptions options = new MetadataSignOptions();
options
    .Add(new PdfMetadataSignature("Author", "Mr.Sherlock Holmes")) // String-Wert
    .Add(new PdfMetadataSignature("CreatedOn", DateTime.Now))       // DateTime-Werte
    .Add(new PdfMetadataSignature("DocumentId", 123456))            // Integer Wert
    .Add(new PdfMetadataSignature("SignatureId", 123.456D))         // Doppelter Wert
    .Add(new PdfMetadataSignature("Amount", 123.456M))              // Dezimalwert
    .Add(new PdfMetadataSignature("Total", 123.456F));              // Float-Wert
```
## Schritt 5: Unterschreiben Sie das Dokument
Signieren Sie das PDF-Dokument mit den angegebenen Metadatenoptionen und speichern Sie das signierte Dokument:
```csharp
SignResult result = signature.Sign(outputFilePath, options);
Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).\nFile saved at {outputFilePath}.");
```

## Abschluss
In diesem Tutorial haben wir behandelt, wie Sie mithilfe von GroupDocs.Signature für .NET ein PDF-Dokument mit Metadaten signieren. Wenn Sie der Schritt-für-Schritt-Anleitung folgen, können Sie ganz einfach Metadateninformationen wie Urheberschaft, Erstellungsdatum und mehr zu Ihren PDF-Dateien hinzufügen und so deren Nützlichkeit und Nachverfolgbarkeit verbessern.
## Häufig gestellte Fragen
### Kann ich meinen PDF-Dokumenten benutzerdefinierte Metadatenfelder hinzufügen?
Ja, Sie können benutzerdefinierte Metadatenfelder hinzufügen, indem Sie den Feldnamen und den entsprechenden Wert mit GroupDocs.Signature für .NET angeben.
### Ist GroupDocs.Signature für .NET mit allen Versionen von .NET Framework kompatibel?
GroupDocs.Signature für .NET ist mit verschiedenen Versionen von .NET Framework kompatibel und gewährleistet so Flexibilität und einfache Integration.
### Unterstützt GroupDocs.Signature das Signieren anderer Dokumentformate außer PDF?
Ja, GroupDocs.Signature unterstützt eine Vielzahl von Dokumentformaten, darunter Word, Excel, PowerPoint und mehr.
### Kann ich mit GroupDocs.Signature für .NET mehrere Dokumente in großen Mengen signieren?
Ja, Sie können mehrere Dokumente in großen Mengen signieren, indem Sie eine Liste von Dateien durchlaufen und den Signaturprozess programmgesteuert anwenden.
### Ist technischer Support für GroupDocs.Signature-Benutzer verfügbar?
 Ja, GroupDocs bietet über seine Foren dedizierten technischen Support. Sie können auf das Support-Forum zugreifen[Hier](https://forum.groupdocs.com/c/signature/13).