---
title: Signieren mit mehreren Optionen
linktitle: Signieren mit mehreren Optionen
second_title: GroupDocs.Signature .NET-API
description: Erfahren Sie, wie Sie mit GroupDocs.Signature für .NET Dokumente mit mehreren Optionen signieren. Erhöhen Sie die Dokumentensicherheit mit Text, Barcode, QR-Code, Digital und Bild.
weight: 14
url: /de/net/advanced-signature-techniques/sign-with-multiple-options/
---

# Signieren mit mehreren Optionen

## Einführung
In diesem Tutorial erfahren Sie, wie Sie mithilfe der GroupDocs.Signature-Bibliothek für .NET ein Dokument mit mehreren Signaturoptionen signieren. Das Signieren von Dokumenten mit verschiedenen Optionen wie Text-, Barcode-, QR-Code-, Digital-, Bild- und Metadatensignaturen bietet Vielseitigkeit und erhöht die Dokumentensicherheit.
## Voraussetzungen
Bevor Sie beginnen, stellen Sie sicher, dass Sie die folgenden Voraussetzungen erfüllen:
1.  GroupDocs.Signature for .NET-Bibliothek: Laden Sie die GroupDocs.Signature for .NET-Bibliothek herunter und installieren Sie sie von[Hier](https://releases.groupdocs.com/signature/net/).
2. Entwicklungsumgebung: Richten Sie eine Entwicklungsumgebung mit installiertem .NET Framework ein.
3. Zu signierendes Dokument: Bereiten Sie das Dokument (z. B. sample.docx) vor, das Sie signieren möchten.
4. Zertifikate und Bilder: Bereiten Sie alle erforderlichen Zertifikate und Bilder für digitale Signaturen und Bildsignaturen vor.

## Namespaces importieren
Importieren Sie zunächst die erforderlichen Namespaces, um die GroupDocs.Signature-Bibliothek in Ihrer .NET-Anwendung zu verwenden:
```csharp
using System;
using System.IO;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## Schritt 1: Laden Sie das Dokument
```csharp
string filePath = "sample.docx";
string outputFilePath = Path.Combine("Your Document Directory", "SignWithMultiple", "SignWithMultiple.docx");
using (Signature signature = new Signature(filePath))
{
    // Ihr Code geht weiter...
}
```
## Schritt 2: Signaturoptionen definieren
Definieren Sie mehrere Signaturoptionen unterschiedlicher Art und Einstellungen, z. B. Text-, Barcode-, QR-Code-, Digital-, Bild- und Metadatensignaturen:
```csharp
TextSignOptions textOptions = new TextSignOptions("Text signature")
{
    VerticalAlignment = VerticalAlignment.Top,
    HorizontalAlignment = HorizontalAlignment.Left
};
BarcodeSignOptions barcodeOptions = new BarcodeSignOptions("123456")
{
    EncodeType = BarcodeTypes.Code128,
    Left = 0,
    Top = 150,
    Height = 50,
    Width = 200
};
// Definieren Sie andere Signaturoptionen (z. B. QR-Code, digital, Bild, Metadaten) ...
```
## Schritt 3: Erstellen Sie eine Liste mit Signaturoptionen
Definieren Sie eine Liste von Signaturoptionen, die alle zuvor definierten Optionen enthält:
```csharp
List<SignOptions> listOptions = new List<SignOptions>();
listOptions.Add(textOptions);
listOptions.Add(barcodeOptions);
// Fügen Sie der Liste weitere Signaturoptionen hinzu...
```
## Schritt 4: Unterschreiben Sie das Dokument
Signieren Sie das Dokument mit der Liste der Signaturoptionen und speichern Sie das signierte Dokument:
```csharp
SignResult result = signature.Sign(outputFilePath, listOptions);
Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).\nFile saved at {outputFilePath}.");
```

## Abschluss
Das Signieren von Dokumenten mit mehreren Optionen mithilfe von GroupDocs.Signature für .NET bietet eine robuste Lösung zur Verbesserung der Dokumentensicherheit und Vielseitigkeit. Indem Sie die in diesem Tutorial beschriebenen Schritte befolgen, können Sie verschiedene Signaturtypen nahtlos in Ihre .NET-Anwendungen integrieren.
## Häufig gestellte Fragen
### Kann ich benutzerdefinierte Bilder für digitale Signaturen verwenden?
Ja, Sie können mithilfe der GroupDocs.Signature-Bibliothek benutzerdefinierte Bilder für digitale Signaturen angeben.
### Ist GroupDocs.Signature mit verschiedenen Dokumentformaten kompatibel?
Ja, GroupDocs.Signature unterstützt verschiedene Dokumentformate, darunter DOCX, PDF, PPTX und mehr.
### Kann ich das Erscheinungsbild von Textsignaturen anpassen?
Sie können das Erscheinungsbild von Textsignaturen, einschließlich Schriftgröße, Farbe und Stil, auf jeden Fall anpassen.
### Bietet GroupDocs.Signature Verschlüsselung für digitale Signaturen?
Ja, GroupDocs.Signature bietet Verschlüsselungsoptionen für digitale Signaturen, um die Dokumentensicherheit zu gewährleisten.
### Gibt es eine Testversion für GroupDocs.Signature für .NET?
 Ja, Sie können eine kostenlose Testversion von GroupDocs.Signature für .NET unter herunterladen[Hier](https://releases.groupdocs.com/).