---
title: Signieren von Dokumenten mit QR-Code mit GroupDocs.Signature
linktitle: Signieren mit QR-Code
second_title: GroupDocs.Signature .NET-API
description: Erfahren Sie, wie Sie mit GroupDocs.Signature für .NET QR-Code-Signaturen zu Ihren Dokumenten hinzufügen. Verbessern Sie mühelos Sicherheit und Authentifizierung.
weight: 15
url: /de/net/advanced-signature-techniques/sign-with-qr-code/
---

# Signieren von Dokumenten mit QR-Code mit GroupDocs.Signature

## Einführung
In diesem Tutorial führen wir den Prozess des Signierens von Dokumenten mit einem QR-Code mithilfe von GroupDocs.Signature für .NET durch. GroupDocs.Signature für .NET ist eine leistungsstarke API, mit der Entwickler programmgesteuert verschiedene Arten von Signaturen zu digitalen Dokumenten hinzufügen können. Das Signieren von Dokumenten mit QR-Codes kann Ihren Dokumenten eine zusätzliche Sicherheits- und Authentifizierungsebene verleihen.
## Voraussetzungen
Bevor wir beginnen, stellen Sie sicher, dass die folgenden Voraussetzungen installiert sind:
1.  GroupDocs.Signature für .NET: Sie können die Bibliothek von herunterladen[Webseite](https://releases.groupdocs.com/signature/net/).
2. Entwicklungsumgebung: Stellen Sie sicher, dass auf Ihrem Computer eine .NET-Entwicklungsumgebung eingerichtet ist.
3. Beispieldokument: Bereiten Sie ein Beispieldokument (z. B. PDF) vor, das Sie mit einem QR-Code signieren möchten.

## Notwendige Namespaces importieren
Bevor wir uns mit dem Code befassen, importieren wir die erforderlichen Namespaces:
```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

## Schritt 1: Dateipfade definieren
```csharp
string filePath = "sample.pdf";
string fileName = Path.GetFileName(filePath);
string outputFilePath = Path.Combine("Your Document Directory", "SignWithQRCode", fileName);
```
 Stellen Sie sicher, dass Sie es ersetzen`"Your Document Directory"` mit dem Pfad zu dem Verzeichnis, in dem Sie das signierte Dokument speichern möchten.
## Schritt 2: Signaturobjekt initialisieren
```csharp
using (Signature signature = new Signature(filePath))
{
    //Code zum Signieren finden Sie hier
}
```
 Initialisieren Sie a`Signature` Objekt mit dem Pfad zu dem Dokument, das Sie signieren möchten.
## Schritt 3: Erstellen Sie QRCodeSignOptions
```csharp
QrCodeSignOptions options = new QrCodeSignOptions("JohnSmith")
{
    EncodeType = QrCodeTypes.QR,
    Left = 50,
    Top = 150,
    Width = 200,
    Height = 200
};
```
 Ein ... kreieren`QrCodeSignOptions` Objekt mit den gewünschten Einstellungen für die QR-Code-Signatur. Sie können Parameter wie den zu kodierenden Text, die Position und die Abmessungen des QR-Codes anpassen.
## Schritt 4: Unterschreiben Sie das Dokument
```csharp
SignResult result = signature.Sign(outputFilePath, options);
```
 Benutzen Sie die`Sign` Methode der`Signature` Objekt, um das Dokument mit den angegebenen Optionen zu signieren. Diese Methode gibt a zurück`SignResult` Objekt, das Informationen über den Signiervorgang enthält.
## Schritt 5: Ergebnis anzeigen
```csharp
Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).\nFile saved at {outputFilePath}.");
```
Zeigt eine Meldung an, die den Erfolg des Signiervorgangs und den Speicherort des signierten Dokuments angibt.

## Abschluss
In diesem Tutorial haben wir gelernt, wie man mit GroupDocs.Signature für .NET Dokumente mit einem QR-Code signiert. Wenn Sie diese einfachen Schritte befolgen, können Sie Ihren digitalen Dokumenten QR-Code-Signaturen hinzufügen und so die Sicherheit und Authentifizierung verbessern.

## Häufig gestellte Fragen
### Kann ich das Erscheinungsbild des QR-Codes anpassen?
Ja, Sie können verschiedene Parameter wie Größe, Position und Kodierungsart des QR-Codes entsprechend Ihren Anforderungen anpassen.
### Welche Dokumentformate werden zum Signieren mit QR-Codes unterstützt?
GroupDocs.Signature für .NET unterstützt eine Vielzahl von Dokumentformaten, darunter PDF, Word, Excel, PowerPoint und mehr.
### Ist es möglich, mehrere Dokumente in einem Stapelprozess zu signieren?
Auf jeden Fall können Sie GroupDocs.Signature für .NET verwenden, um mehrere Dokumente gleichzeitig zu signieren und so Ihren Arbeitsablauf zu optimieren.
### Kann ich die Echtheit eines mit einem QR-Code signierten Dokuments überprüfen?
Ja, GroupDocs.Signature für .NET bietet Überprüfungsmechanismen, um die Integrität und Authentizität signierter Dokumente sicherzustellen.
### Gibt es eine Testversion, um die Funktionalität vor dem Kauf zu testen?
 Ja, Sie können eine kostenlose Testversion herunterladen[Webseite](https://releases.groupdocs.com/) um die Funktionen und Fähigkeiten von GroupDocs.Signature für .NET zu bewerten.