---
title: Signieren mit Text mit GroupDocs.Signature für .NET
linktitle: Mit Text signieren
second_title: GroupDocs.Signature .NET-API
description: Erfahren Sie, wie Sie mit GroupDocs.Signature für .NET Dokumente mit Text signieren. Schritt-für-Schritt-Anleitung zum programmgesteuerten Hinzufügen von Textsignaturen.
type: docs
weight: 17
url: /de/net/advanced-signature-techniques/sign-with-text/
---
## Einführung
Im digitalen Zeitalter ist die elektronische Unterzeichnung von Dokumenten zur Standardpraxis geworden, was Zeit und Ressourcen spart. GroupDocs.Signature für .NET bietet eine umfassende Lösung zum programmgesteuerten Hinzufügen von Textsignaturen zu verschiedenen Dokumentformaten. In diesem Tutorial führen wir Sie durch den Prozess des Signierens eines Dokuments mit Text mithilfe von GroupDocs.Signature für .NET.
## Voraussetzungen
Bevor wir uns mit dem Tutorial befassen, stellen Sie sicher, dass Sie die folgenden Voraussetzungen erfüllen:
1.  GroupDocs.Signature für .NET: Stellen Sie sicher, dass die GroupDocs.Signature für .NET-Bibliothek installiert ist. Sie können es herunterladen unter[Hier](https://releases.groupdocs.com/signature/net/).
2. Entwicklungsumgebung: Richten Sie eine Arbeitsumgebung für die .NET-Entwicklung ein.
3. Dokument: Bereiten Sie das Dokument (z. B. PDF, Word) vor, das Sie mit Text signieren möchten.

## Namespaces importieren
Zunächst müssen Sie die erforderlichen Namespaces in Ihr .NET-Projekt importieren, um die GroupDocs.Signature-Funktionen nutzen zu können.
```csharp
using System;
using System.IO;
using System.Drawing;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

Lassen Sie uns den Prozess des Signierens eines Dokuments mit Text in mehrere Schritte unterteilen:
## Schritt 1: Dokument laden
Laden Sie das Dokument, das Sie signieren möchten, mit Text.
```csharp
string filePath = "sample.pdf"; // Pfad zum Dokument
string fileName = Path.GetFileName(filePath);
```
## Schritt 2: Legen Sie den Ausgabedateipfad fest
Definieren Sie den Ausgabedateipfad, in dem das signierte Dokument gespeichert wird.
```csharp
string outputFilePath = Path.Combine("Your Document Directory", "SignWithText", fileName);
```
## Schritt 3: Signaturoptionen erstellen
Richten Sie die Optionen für die Textsignatur ein, einschließlich Textinhalt, Position, Größe, Farbe und Schriftart.
```csharp
TextSignOptions options = new TextSignOptions("John Smith")
{
    Left = 50, // Signaturposition festlegen
    Top = 200,
    Width = 100, // Signaturrechteck festlegen
    Height = 30,
    ForeColor = Color.Red, // Textfarbe festlegen
    Font = new SignatureFont { Size = 14, FamilyName = "Comic Sans MS" } // Schriftart festlegen
};
```
## Schritt 4: Dokument unterschreiben
Verwenden Sie GroupDocs.Signature, um das Dokument mit den angegebenen Optionen zu signieren und das signierte Dokument im Ausgabedateipfad zu speichern.
```csharp
using (Signature signature = new Signature(filePath))
{
    SignResult result = signature.Sign(outputFilePath, options); // Dokument unterschreiben
    Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).\nFile saved at {outputFilePath}.");
}
```

## Abschluss
In diesem Tutorial haben wir gelernt, wie man mit GroupDocs.Signature für .NET ein Dokument mit Text signiert. Wenn Sie diese Schritte befolgen, können Sie Ihren Dokumenten effizient und programmgesteuert Textsignaturen hinzufügen und so die Sicherheit und Authentizität verbessern.
## Häufig gestellte Fragen
### Kann ich das Erscheinungsbild der Textsignatur anpassen?
Ja, Sie können verschiedene Parameter wie Farbe, Schriftart, Größe und Position der Textsignatur nach Ihren Wünschen anpassen.
### Ist GroupDocs.Signature mit mehreren Dokumentformaten kompatibel?
Ja, GroupDocs.Signature unterstützt verschiedene Dokumentformate, darunter PDF, Word, Excel, PowerPoint und mehr.
### Kann ich einem einzelnen Dokument mehrere Textsignaturen hinzufügen?
Sie können einem Dokument auf jeden Fall mehrere Textsignaturen hinzufügen, jede mit ihren eigenen Anpassungsoptionen.
### Stellt GroupDocs.Signature die Dokumentenintegrität nach dem Signieren sicher?
Ja, GroupDocs.Signature verwendet robuste kryptografische Algorithmen, um die Dokumentenintegrität sicherzustellen und Manipulationen nach dem Signieren zu verhindern.
### Gibt es eine Testversion zum Testen vor dem Kauf?
 Ja, Sie können eine kostenlose Testversion herunterladen von[Hier](https://releases.groupdocs.com/) um die Funktionen vor dem Kauf zu erkunden.