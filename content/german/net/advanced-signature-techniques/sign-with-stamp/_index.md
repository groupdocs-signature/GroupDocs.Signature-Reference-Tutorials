---
title: Signieren mit Stempel mit GroupDocs.Signature
linktitle: Unterschreiben mit Stempel
second_title: GroupDocs.Signature .NET-API
description: Erfahren Sie, wie Sie mit GroupDocs.Signature für .NET ganz einfach Stempelsignaturen zu Ihren .NET-Dokumenten hinzufügen. Verbessern Sie die Dokumentensicherheit.
type: docs
weight: 16
url: /de/net/advanced-signature-techniques/sign-with-stamp/
---
## Einführung
In diesem Tutorial führen wir Sie durch den Prozess des Signierens eines Dokuments mit einem Stempel mithilfe von GroupDocs.Signature für .NET. Wenn Sie diese Schritt-für-Schritt-Anleitung befolgen, können Sie ganz einfach eine Stempelsignatur zu Ihren Dokumenten hinzufügen.
## Voraussetzungen
Bevor wir beginnen, stellen Sie sicher, dass Sie die folgenden Voraussetzungen erfüllen:
1.  GroupDocs.Signature für .NET SDK: Laden Sie das SDK von herunter und installieren Sie es[Webseite](https://releases.groupdocs.com/signature/net/).
2. Entwicklungsumgebung: Stellen Sie sicher, dass Sie eine geeignete Entwicklungsumgebung für die .NET-Entwicklung eingerichtet haben.
3. Zu signierendes Dokument: Bereiten Sie das Dokument (z. B. PDF) vor, das Sie mit einem Stempel signieren möchten.

## Namespaces importieren
Beginnen Sie mit dem Importieren der erforderlichen Namespaces in Ihr Projekt:
```csharp
using System;
using System.IO;
using System.Drawing;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## Schritt 1: Laden Sie das Dokument
```csharp
string filePath = "sample.pdf";
using (Signature signature = new Signature(filePath))
{
    // Ihr Code kommt hierher
}
```
## Schritt 2: Legen Sie die Stempelzeichenoptionen fest
```csharp
StampSignOptions options = new StampSignOptions()
{
    Left = 50,
    Top = 150,                    
    Width = 200,
    Height = 200
};
```
## Schritt 3: Konfigurieren Sie das Erscheinungsbild des Stempels
```csharp
StampLine outerLine = new StampLine();
outerLine.Text = " * European Union ";
outerLine.TextRepeatType = StampTextRepeatType.FullTextRepeat;
outerLine.Font.Size = 12;
outerLine.Height = 22;
outerLine.TextBottomIntent = 6;
outerLine.TextColor = Color.WhiteSmoke;
outerLine.BackgroundColor = Color.DarkSlateBlue;
options.OuterLines.Add(outerLine);
StampLine innerLine = new StampLine();
innerLine.Text = "John Smith";
innerLine.TextColor = Color.MediumVioletRed;
innerLine.Font.Size = 20;
innerLine.Font.Bold = true;
innerLine.Height = 40;
options.InnerLines.Add(innerLine);
```
## Schritt 4: Unterschreiben Sie das Dokument
```csharp
string outputFilePath = Path.Combine("Your Document Directory", "SignWithStamp", fileName);
SignResult result = signature.Sign(outputFilePath, options);
Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).\nFile saved at {outputFilePath}.");
```

## Abschluss
Das Hinzufügen von Stempelsignaturen zu Ihren Dokumenten mit GroupDocs.Signature für .NET ist ein unkomplizierter Vorgang, wie in diesem Tutorial gezeigt. Mit den bereitgestellten Schritten können Sie die Sicherheit und Authentizität Ihrer Dokumente ganz einfach verbessern.
## Häufig gestellte Fragen
### Kann ich das Erscheinungsbild der Stempelsignatur anpassen?
Ja, Sie können verschiedene Aspekte wie Text, Schriftart, Farbe und Positionierung der Stempelsignatur Ihren Anforderungen entsprechend anpassen.
### Unterstützt GroupDocs.Signature das Signieren mehrerer Dokumentformate?
Ja, GroupDocs.Signature unterstützt eine Vielzahl von Dokumentformaten, darunter PDF, Microsoft Word, Excel, PowerPoint und mehr.
### Gibt es eine Testversion für GroupDocs.Signature?
 Ja, Sie können über das auf die kostenlose Testversion zugreifen[Webseite](https://releases.groupdocs.com/).
### Kann ich einem einzelnen Dokument mehrere Signaturen hinzufügen?
Absolut, mit GroupDocs.Signature können Sie einem einzelnen Dokument mehrere Signaturen hinzufügen, darunter Stempel, Text, Bilder und digitale Signaturen.
### Wo finde ich Unterstützung, wenn bei der Implementierung Probleme auftreten?
 Unterstützung und Hilfe finden Sie im GroupDocs.Signature-Community-Forum[Hier](https://forum.groupdocs.com/c/signature/13).