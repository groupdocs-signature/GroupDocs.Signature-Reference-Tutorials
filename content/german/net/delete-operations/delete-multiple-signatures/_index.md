---
title: Mehrere Signaturen aus dem Dokument löschen
linktitle: Mehrere Signaturen aus dem Dokument löschen
second_title: GroupDocs.Signature .NET-API
description: Löschen Sie mühelos mehrere Signaturen aus Dokumenten mit GroupDocs.Signature für .NET. Optimieren Sie Ihren Dokumentenmanagement-Workflow.
weight: 15
url: /de/net/delete-operations/delete-multiple-signatures/
---
## Einführung
In der digitalen Welt geht es bei der Dokumentenverwaltung häufig um die Handhabung verschiedener Signaturen. Das programmgesteuerte Löschen mehrerer Signaturen aus einem Dokument kann Arbeitsabläufe rationalisieren und die Effizienz steigern. Mit GroupDocs.Signature für .NET wird diese Aufgabe nahtlos und unkompliziert. Dieses Tutorial führt Sie Schritt für Schritt durch den Prozess des Löschens mehrerer Signaturen aus einem Dokument.
## Voraussetzungen
Bevor Sie mit dem Tutorial beginnen, stellen Sie sicher, dass Sie die folgenden Voraussetzungen erfüllen:
- Grundlegendes Verständnis der Programmiersprache C#.
- Installierte GroupDocs.Signature für die .NET-Bibliothek.
- Beispieldokument mit mehreren Signaturen zum Testen.

## Namespaces importieren
Beginnen Sie mit dem Importieren der erforderlichen Namespaces, um auf die Funktionalität von GroupDocs.Signature für .NET zuzugreifen:
```csharp
using System;
using System.IO;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## Schritt 1: Definieren Sie Dokumentpfad und Dateinamen
Legen Sie den Dateipfad des Dokuments fest, das mehrere Signaturen enthält. Stellen Sie sicher, dass Sie den richtigen Dateipfad und Dateinamen haben:
```csharp
string filePath = "sample_multiple_signatures.docx";
string fileName = Path.GetFileName(filePath);
```
## Schritt 2: Kopieren Sie das Dokument zur Bearbeitung
Um eine Änderung des Originaldokuments zu vermeiden, erstellen Sie eine Kopie zur Bearbeitung:
```csharp
string outputFilePath = Path.Combine("Your Document Directory", "DeleteMultiple", fileName);
File.Copy(filePath, outputFilePath, true);
```
## Schritt 3: Signaturobjekt initialisieren
Instanziieren Sie ein Signature-Objekt mithilfe des Ausgabedateipfads:
```csharp
using (Signature signature = new Signature(outputFilePath))
{
    // Hier steht der Signaturverarbeitungscode
}
```
## Schritt 4: Suchoptionen definieren
Definieren Sie verschiedene Suchoptionen, um Signaturen innerhalb des Dokuments zu identifizieren. Zu den Optionen gehören Textsuche, Bildsuche, Barcode-Suche und QR-Code-Suche:
```csharp
TextSearchOptions textSearchOptions = new TextSearchOptions();
ImageSearchOptions imageSearchOptions = new ImageSearchOptions();
BarcodeSearchOptions barcodeOptions = new BarcodeSearchOptions();
QrCodeSearchOptions qrCodeOptions = new QrCodeSearchOptions();
// Optionen zur Liste hinzufügen
List<SearchOptions> listOptions = new List<SearchOptions>();
listOptions.Add(textSearchOptions);
listOptions.Add(imageSearchOptions);
listOptions.Add(barcodeOptions);
listOptions.Add(qrCodeOptions);
```
## Schritt 5: Suchen Sie nach Signaturen
Führen Sie einen Suchvorgang aus, um alle Signaturen im Dokument basierend auf den definierten Suchoptionen zu finden:
```csharp
SearchResult result = signature.Search(listOptions);
```
## Schritt 6: Signaturen löschen
Wenn Signaturen gefunden werden, löschen Sie diese:
```csharp
if (result.Signatures.Count > 0)
{
    // Versuchen Sie, alle Signaturen zu löschen
    DeleteResult deleteResult = signature.Delete(result.Signatures);
    //Überprüfen Sie, ob das Löschen erfolgreich war
    if(deleteResult.Succeeded.Count == result.Signatures.Count)
    {
        Console.WriteLine("\nAll signatures were successfully deleted!");                        
    }
    else
    {
        Console.WriteLine($"Successfully deleted signatures : {deleteResult.Succeeded.Count}");
        Helper.WriteError($"Not deleted signatures : {deleteResult.Failed.Count}");
    }
    // Informationen zu gelöschten Signaturen anzeigen
    Console.WriteLine("\nList of deleted signatures:");
    int number = 1;
    foreach(BaseSignature temp in deleteResult.Succeeded)
    {
        Console.WriteLine($"Signature #{number++}: Type: {temp.SignatureType} Id:{temp.SignatureId}, Location: {temp.Left}x{temp.Top}. Size: {temp.Width}x{temp.Height}");
    }
}
else
{
    Helper.WriteError("No one signature was found.");
}
```

## Abschluss
Das programmgesteuerte Löschen mehrerer Signaturen aus einem Dokument ist eine wichtige Aufgabe im Dokumentenmanagement. Mit GroupDocs.Signature für .NET wird dieser Prozess effizient und zuverlässig. Indem Sie die in diesem Tutorial beschriebenen Schritte befolgen, können Sie die Funktion zum Löschen von Signaturen problemlos in Ihre .NET-Anwendungen integrieren.
## Häufig gestellte Fragen
### Kann GroupDocs.Signature für .NET verschiedene Dokumentformate verarbeiten?
Ja, GroupDocs.Signature für .NET unterstützt eine breite Palette von Dokumentformaten, darunter DOCX, PDF, PPTX, XLSX und mehr.
### Ist es möglich, die Suchoptionen zur Signaturerkennung anzupassen?
Selbstverständlich können Sie Suchoptionen wie Textsuche, Bildsuche, Barcodesuche und QR-Codesuche an Ihre spezifischen Anforderungen anpassen.
### Bietet GroupDocs.Signature für .NET Mechanismen zur Fehlerbehandlung?
Ja, die Bibliothek bietet robuste Fehlerbehandlungsfunktionen, um eine reibungslose Ausführung von Dokumentenverarbeitungsaufgaben sicherzustellen.
### Kann ich GroupDocs.Signature für .NET mit anderen Bibliotheken von Drittanbietern integrieren?
Natürlich ist GroupDocs.Signature für .NET so konzipiert, dass es sich nahtlos in andere .NET-Bibliotheken integrieren lässt und so Flexibilität und Erweiterbarkeit bietet.
### Wo finde ich zusätzliche Unterstützung und Ressourcen für GroupDocs.Signature für .NET?
 Sie können die GroupDocs besuchen[Forum](https://forum.groupdocs.com/c/signature/13) widmet sich den unterschriftsbezogenen Diskussionen und bittet die Community und Experten um Unterstützung.