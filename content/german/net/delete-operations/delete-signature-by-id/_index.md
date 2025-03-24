---
title: Signatur nach ID löschen
linktitle: Signatur nach ID löschen
second_title: GroupDocs.Signature .NET-API
description: Erfahren Sie, wie Sie mithilfe der GroupDocs.Signature-Bibliothek eine Signatur nach ID in .NET-Dokumenten löschen. Einfache Schritt-für-Schritt-Anleitung.
weight: 11
url: /de/net/delete-operations/delete-signature-by-id/
---

# Signatur nach ID löschen

## Einführung
In diesem Tutorial erfahren Sie, wie Sie mit GroupDocs.Signature für .NET eine Signatur anhand ihrer ID löschen. GroupDocs.Signature für .NET ist eine leistungsstarke Bibliothek, die es Entwicklern ermöglicht, mithilfe von .NET-Anwendungen digitale Signaturen in verschiedenen Dokumentformaten hinzuzufügen, zu entfernen oder zu überprüfen.
## Voraussetzungen
Bevor wir beginnen, stellen Sie sicher, dass Sie die folgenden Voraussetzungen erfüllen:
1.  GroupDocs.Signature für .NET-Bibliothek: Laden Sie die Bibliothek herunter und installieren Sie sie von[Hier](https://releases.groupdocs.com/signature/net/).
2. .NET Framework: Stellen Sie sicher, dass .NET Framework auf Ihrem System installiert ist.
3. Dokument mit Signatur: Bereiten Sie ein Dokument (z. B. DOCX, PDF) mit einer Signatur vor, die Sie löschen möchten.

## Namespaces importieren
```csharp
using System;
using System.IO;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## Schritt 1: Dateipfade definieren
Geben Sie zunächst den Dateipfad für das Dokument an, das die Signatur enthält, und den Ausgabedateipfad, in dem das geänderte Dokument gespeichert wird.
```csharp
string filePath = "sample_multiple_signatures.docx";
string fileName = Path.GetFileName(filePath);
string outputFilePath = Path.Combine("Your Document Directory", "DeleteById", fileName);
```
## Schritt 2: Kopieren Sie das Dokument
 Seit der`Delete` Methode das Dokument an Ort und Stelle ändert, ist es am besten, eine Kopie des Originaldokuments zu erstellen.
```csharp
File.Copy(filePath, outputFilePath, true);
```
## Schritt 3: Signatur nach ID löschen
 Initialisieren Sie die`Signature` Objekt mit dem Dokumentdateipfad und verwenden Sie das`Delete` Methode zum Entfernen der Signatur anhand ihrer ID.
```csharp
using (Signature signature = new Signature(outputFilePath))
{
    string id = @"eff64a14-dad9-47b0-88e5-2ee4e3604e71";
    bool result = signature.Delete(id);
    if (result)
    {
        Console.WriteLine($"Signature with Id# '{id}' was deleted from document ['{fileName}'].");
    }
    else
    {
        Helper.WriteError($"Signature was not deleted from the document! Signature with id# '{id}' was not found!");
    }
}
```

## Abschluss
In diesem Tutorial haben wir gelernt, wie man mit GroupDocs.Signature für .NET eine Signatur anhand ihrer ID löscht. Diese Bibliothek bietet eine praktische Möglichkeit, digitale Signaturen in verschiedenen Dokumentformaten programmgesteuert zu verwalten.
## Häufig gestellte Fragen
### Kann ich mehrere Signaturen gleichzeitig löschen?
 Ja, Sie können mehrere Signaturen löschen, indem Sie deren IDs durchlaufen und aufrufen`Delete` Methode für jede ID.
### Ist GroupDocs.Signature für .NET mit allen Dokumentformaten kompatibel?
GroupDocs.Signature für .NET unterstützt eine Vielzahl von Dokumentformaten, darunter PDF, DOCX, XLSX und mehr.
### Kann ich das Erscheinungsbild der Signatur anpassen?
Ja, Sie können das Erscheinungsbild der Signatur anpassen, einschließlich Position, Größe, Schriftart und Farbe.
### Gibt es eine Testversion?
 Ja, Sie können eine kostenlose Testversion herunterladen von[Hier](https://releases.groupdocs.com/).
### Wo finde ich Hilfe oder Support für GroupDocs.Signature für .NET?
 Sie können das Support-Forum besuchen[Hier](https://forum.groupdocs.com/c/signature/13) zur Hilfe.