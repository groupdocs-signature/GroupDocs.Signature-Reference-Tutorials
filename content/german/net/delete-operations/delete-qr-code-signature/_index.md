---
title: Löschen Sie die QR-Code-Signatur aus dem Dokument
linktitle: Löschen Sie die QR-Code-Signatur aus dem Dokument
second_title: GroupDocs.Signature .NET-API
description: Erfahren Sie, wie Sie mit GroupDocs.Signature für .NET QR-Code-Signaturen aus Dokumenten löschen. Befolgen Sie unsere Schritt-für-Schritt-Anleitung für eine effiziente Signaturverwaltung.
weight: 16
url: /de/net/delete-operations/delete-qr-code-signature/
---

# Löschen Sie die QR-Code-Signatur aus dem Dokument

## Einführung
In diesem Tutorial führen wir Sie durch den Prozess des Entfernens einer QR-Code-Signatur aus einem Dokument mithilfe von GroupDocs.Signature für .NET. Befolgen Sie diese Schritt-für-Schritt-Anleitung, um QR-Code-Signaturen effektiv zu löschen.
## Voraussetzungen
Bevor Sie beginnen, stellen Sie sicher, dass Sie die folgenden Voraussetzungen erfüllen:
-  GroupDocs.Signature für .NET: Stellen Sie sicher, dass die GroupDocs.Signature-Bibliothek in Ihrem .NET-Projekt installiert ist. Sie können es herunterladen unter[Hier](https://releases.groupdocs.com/signature/net/).
- Dokument mit QR-Code-Signatur: Bereiten Sie ein Dokument mit QR-Code-Signaturen vor, die Sie löschen möchten.
- Grundkenntnisse in C#: Machen Sie sich mit den Grundlagen der Programmiersprache C# vertraut.

## Namespaces importieren
Bevor Sie in den Code eintauchen, importieren Sie die erforderlichen Namespaces in Ihre C#-Datei:
```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## Schritt 1: Dateipfade definieren
```csharp
// Der Pfad zum Dokumentenverzeichnis.
string filePath = "sample_multiple_signatures.docx";
string fileName = Path.GetFileName(filePath);
// Definieren Sie den Ausgabedateipfad für das geänderte Dokument.
string outputFilePath = Path.Combine("Your Document Directory", "DeleteQRCode", fileName);
// Kopieren Sie die Quelldatei, da die Löschmethode mit demselben Dokument funktioniert.
File.Copy(filePath, outputFilePath, true);
```
## Schritt 2: Signaturobjekt initialisieren
```csharp
using (Signature signature = new Signature(outputFilePath))
{
    // Erstellen Sie Optionen für die Suche nach QR-Code-Signaturen.
    QrCodeSearchOptions options = new QrCodeSearchOptions();
    // Suchen Sie im Dokument nach QR-Code-Signaturen.
    List<QrCodeSignature> signatures = signature.Search<QrCodeSignature>(options);
```
## Schritt 3: Überprüfen Sie, ob eine QR-Code-Signatur vorhanden ist
```csharp
    if (signatures.Count > 0)
    {
        // Holen Sie sich die erste im Dokument gefundene QR-Code-Signatur.
        QrCodeSignature qrCodeSignature = signatures[0];
```
## Schritt 4: QR-Code-Signatur löschen
```csharp
        // Löschen Sie die QR-Code-Signatur aus dem Dokument.
        bool result = signature.Delete(qrCodeSignature);
        if (result)
        {
            Console.WriteLine($"Signature with QR-Code '{qrCodeSignature.Text}' and encode type '{qrCodeSignature.EncodeType.TypeName}' was deleted from document ['{fileName}'].");
        }
        else
        {
            Helper.WriteError($"Signature was not deleted from the document! Signature with Barcode '{qrCodeSignature.Text}' and encode type '{qrCodeSignature.EncodeType.TypeName}' was not found!");
        }
    }
}
```
Glückwunsch! Sie haben die QR-Code-Signatur mit GroupDocs.Signature für .NET erfolgreich aus dem Dokument entfernt.

## Abschluss
In diesem Tutorial haben wir gelernt, wie man mit GroupDocs.Signature für .NET eine QR-Code-Signatur aus einem Dokument löscht. Indem Sie die bereitgestellten Schritte befolgen, können Sie Signaturen in Ihren .NET-Anwendungen effizient verwalten und bearbeiten.
## Häufig gestellte Fragen
### Kann ich mehrere QR-Code-Signaturen aus einem Dokument löschen?
Ja, Sie können den Code ändern, um alle QR-Code-Signaturen zu durchlaufen und diese entsprechend zu löschen.
### Unterstützt GroupDocs.Signature neben QR-Codes auch andere Arten von Signaturen?
Ja, GroupDocs.Signature unterstützt verschiedene Signaturtypen wie Text, Bild, Barcode und mehr.
### Ist GroupDocs.Signature mit allen Dokumentformaten kompatibel?
GroupDocs.Signature unterstützt eine Vielzahl von Dokumentformaten, darunter PDF, Microsoft Word, Excel, PowerPoint und mehr.
### Kann ich die Suchoptionen für Signaturen anpassen?
Ja, Sie können die Suchoptionen an Ihre Anforderungen anpassen, um bestimmte Signaturen im Dokument zu finden.
### Gibt es eine Testversion für GroupDocs.Signature?
 Ja, Sie können auf eine kostenlose Testversion von GroupDocs.Signature zugreifen[Hier](https://releases.groupdocs.com/).