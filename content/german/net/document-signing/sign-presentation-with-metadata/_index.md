---
title: Präsentation mit Metadaten signieren
linktitle: Präsentation mit Metadaten signieren
second_title: GroupDocs.Signature .NET-API
description: Erfahren Sie, wie Sie Präsentationsdateien mit Metadaten mit GroupDocs.Signature für .NET signieren. Verbessern Sie die Dokumentenintegrität und fügen Sie wertvolle Informationen hinzu.
weight: 12
url: /de/net/document-signing/sign-presentation-with-metadata/
---
## Einführung
In diesem Tutorial erfahren Sie, wie Sie mithilfe der GroupDocs.Signature for .NET-Bibliothek eine Präsentationsdatei (PPTX) mit Metadaten signieren. Durch das Signieren von Präsentationen mit Metadaten werden dem Dokument wertvolle Informationen hinzugefügt, z. B. der Name des Autors, das Erstellungsdatum, die Dokument-ID, die Signatur-ID und verschiedene numerische Werte.
## Voraussetzungen
Bevor wir beginnen, stellen Sie sicher, dass Sie über Folgendes verfügen:
1.  GroupDocs.Signature für .NET-Bibliothek: Laden Sie die Bibliothek herunter und installieren Sie sie von[Hier](https://releases.groupdocs.com/signature/net/).
2. Entwicklungsumgebung: Stellen Sie sicher, dass Sie eine .NET-Entwicklungsumgebung eingerichtet haben.
3. Präsentationsdatei: Halten Sie eine Beispielpräsentationsdatei (PPTX-Format) zum Signieren bereit.
4. Grundkenntnisse von C#: Vertrautheit mit der Programmiersprache C# ist von Vorteil.

## Namespaces importieren
Bevor wir uns mit dem Code befassen, importieren wir die erforderlichen Namespaces:
```csharp
using System;
using System.IO;
    using GroupDocs.Signature;
    using GroupDocs.Signature.Domain;
    using GroupDocs.Signature.Options;
```
## Schritt 1: Präsentationsdatei laden
```csharp
string filePath = "sample.pptx";
```
 Ersetzen`"sample.pptx"` mit dem Pfad zu Ihrer Präsentationsdatei.
## Schritt 2: Geben Sie den Pfad der Ausgabedatei an
```csharp
string outputFilePath = Path.Combine("Your Document Directory", "SignPresentationWithMetadata", "SignedWithMetadata.pptx");
```
Geben Sie das Verzeichnis, in dem Sie die signierte Präsentationsdatei speichern möchten, zusammen mit dem Dateinamen an.
## Schritt 3: Signaturobjekt initialisieren
```csharp
using (Signature signature = new Signature(filePath))
```
Initialisieren Sie ein Signature-Objekt, indem Sie den Pfad zur Präsentationsdatei angeben.
## Schritt 4: Definieren Sie Metadaten-Signierungsoptionen
```csharp
MetadataSignOptions options = new MetadataSignOptions();
```
Erstellen Sie eine Instanz von MetadataSignOptions, um Metadatensignaturoptionen zu definieren.
## Schritt 5: Metadatensignaturen erstellen
```csharp
PresentationMetadataSignature[] signatures = new PresentationMetadataSignature[]
{
    new PresentationMetadataSignature("Author", "Mr.Scherlock Holmes"),
    new PresentationMetadataSignature("CreatedOn", DateTime.Now),
    new PresentationMetadataSignature("DocumentId", 123456),
    new PresentationMetadataSignature("SignatureId", 123.456D),
    new PresentationMetadataSignature("Amount", 123.456M),
    new PresentationMetadataSignature("Total", 123.456F)
};
```
Erstellen Sie ein Array von PresentationMetadataSignature-Objekten, die jeweils eine Metadatensignatur darstellen. Sie können verschiedene Metadatentypen hinzufügen, darunter Zeichenfolge, DateTime, Ganzzahl, Double, Dezimalzahl und Gleitkommazahl.
## Schritt 6: Signaturen zu Optionen hinzufügen
```csharp
options.Signatures.AddRange(signatures);
```
Fügen Sie die erstellten Metadatensignaturen dem MetadataSignOptions-Objekt hinzu.
## Schritt 7: Dokument unterzeichnen
```csharp
SignResult result = signature.Sign(outputFilePath, options);
```
Signieren Sie die Präsentationsdatei mit Metadaten unter Verwendung der angegebenen Optionen und speichern Sie die signierte Datei im Ausgabepfad.
## Schritt 8: Ergebnis anzeigen
```csharp
Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).\nFile saved at {outputFilePath}.");
```
Zeigen Sie eine Erfolgsmeldung zusammen mit der Anzahl der angewendeten Signaturen und dem Pfad an, in dem die signierte Datei gespeichert ist.

## Abschluss
In diesem Tutorial haben wir gelernt, wie man eine Präsentationsdatei mit Metadaten unter Verwendung der Bibliothek GroupDocs.Signature für .NET signiert. Das Hinzufügen von Metadatensignaturen verbessert die Integrität des Dokuments und liefert wertvolle Informationen über seinen Inhalt.

## Häufig gestellte Fragen
### Kann ich mit GroupDocs.Signature für .NET auch andere Dokumentformate außer PPTX mit Metadaten signieren?
Ja, GroupDocs.Signature unterstützt verschiedene Dokumentformate, darunter Word, Excel, PDF und mehr, zum Signieren mit Metadaten.
### Ist GroupDocs.Signature für .NET mit .NET Core kompatibel?
Ja, die Bibliothek ist sowohl mit .NET Framework als auch mit .NET Core kompatibel.
### Kann ich das Erscheinungsbild von Metadatensignaturen anpassen?
Ja, Sie können das Aussehen, die Position und andere Eigenschaften von Metadatensignaturen Ihren Anforderungen entsprechend anpassen.
### Bietet GroupDocs.Signature für .NET Verschlüsselung für signierte Dokumente?
Ja, GroupDocs.Signature bietet Verschlüsselungsoptionen, um signierte Dokumente vor unbefugtem Zugriff zu schützen.
### Gibt es eine Testversion zum Testen vor dem Kauf?
 Ja, Sie können eine kostenlose Testversion von GroupDocs.Signature für .NET nutzen von[Hier](https://releases.groupdocs.com/).