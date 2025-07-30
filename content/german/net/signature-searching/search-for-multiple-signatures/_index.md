---
"description": "Erfahren Sie, wie Sie mit GroupDocs.Signature für .NET nach mehreren Signaturtypen in Dokumenten suchen. Umfassender Leitfaden mit Codebeispielen für verbesserte Dokumentensicherheit."
"linktitle": "Suche nach mehreren Signaturen"
"second_title": "GroupDocs.Signature .NET API"
"title": "Suche nach mehreren Signaturtypen in Dokumenten"
"url": "/de/net/signature-searching/search-for-multiple-signatures/"
"weight": 14
---

## Einführung

In modernen Dokumentenmanagementsystemen wird die Möglichkeit, mehrere Signaturtypen innerhalb eines Dokuments zu suchen und zu validieren, immer wichtiger. Unternehmen nutzen häufig verschiedene Signaturtypen – wie digitale Signaturen, Textsignaturen, Barcodes, QR-Codes und mehr –, um die Dokumentensicherheit zu erhöhen und Verifizierungsprozesse zu optimieren. GroupDocs.Signature für .NET bietet ein leistungsstarkes Framework, mit dem Entwickler eine umfassende Signatursuchfunktion für verschiedene Dokumentformate implementieren können.

Dieses Tutorial führt Sie durch den Prozess der Suche nach mehreren Signaturtypen in Dokumenten mithilfe von GroupDocs.Signature für .NET und bietet detaillierte Erklärungen und praktische Codebeispiele.

## Voraussetzungen

Bevor Sie mit der Implementierung der Suchfunktion für mehrere Signaturen beginnen, stellen Sie sicher, dass Sie die folgenden Voraussetzungen erfüllen:

1. Entwicklungsumgebung: Visual Studio oder eine beliebige bevorzugte .NET-Entwicklungsumgebung, die auf Ihrem System installiert ist.
  
2. GroupDocs.Signature für .NET: Laden Sie die Bibliothek GroupDocs.Signature für .NET herunter und installieren Sie sie von [Hier](https://releases.groupdocs.com/signature/net/).

3. Grundlegende C#-Kenntnisse: Vertrautheit mit der Programmiersprache C# und den Konzepten des .NET-Frameworks.

4. Beispieldokumente: Bereiten Sie zu Testzwecken Testdokumente mit verschiedenen Arten von Signaturen vor.

## Namespaces importieren

Beginnen Sie mit dem Importieren der erforderlichen Namespaces, um auf die GroupDocs.Signature-Funktionalität zuzugreifen:

```csharp
using System;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

Lassen Sie uns nun den Prozess der Suche nach mehreren Signaturtypen in klare, überschaubare Schritte unterteilen:

## Schritt 1: Laden Sie das Dokument

Laden Sie zunächst das Dokument mit den Signaturen, nach denen Sie suchen möchten:

```csharp
string filePath = "sample_multiple_signatures.docx";
using (Signature signature = new Signature(filePath))
{
    // Hier wird ein Suchcode für mehrere Signaturen hinzugefügt
}
```

## Schritt 2: Suchoptionen für verschiedene Signaturtypen definieren

Erstellen Sie Suchoptionen für jeden Signaturtyp, nach dem Sie suchen möchten:

```csharp
// Suchoptionen für Textsignaturen festlegen
TextSearchOptions textOptions = new TextSearchOptions
{
    AllPages = true,  // Suche auf allen Seiten
    Text = "Signature",  // Optional: zu suchender Text
    MatchType = TextMatchType.Contains  // Übereinstimmungskriterien
};

// Suchoptionen für digitale Signaturen festlegen
DigitalSearchOptions digitalOptions = new DigitalSearchOptions
{
    AllPages = true
};

// Suchoptionen für Barcode-Signaturen festlegen
BarcodeSearchOptions barcodeOptions = new BarcodeSearchOptions
{
    AllPages = true,
    Text = "123456",  // Optional: passender Barcode-Text
    MatchType = TextMatchType.Exact  // Übereinstimmungskriterien
};

// Suchoptionen für QR-Code-Signaturen definieren
QrCodeSearchOptions qrCodeOptions = new QrCodeSearchOptions
{
    AllPages = true,
    Text = "John",  // Optional: Passender QR-Code-Text
    MatchType = TextMatchType.Contains  // Übereinstimmungskriterien
};

// Suchoptionen für Metadatensignaturen definieren
MetadataSearchOptions metadataOptions = new MetadataSearchOptions();
```

## Schritt 3: Optionen zu einer Sammlung hinzufügen

Fügen Sie alle Suchoptionen zu einer Sammlung hinzu:

```csharp
// Erstellen Sie eine Liste mit allen Suchoptionen
List<SearchOptions> searchOptions = new List<SearchOptions>
{
    textOptions,
    digitalOptions,
    barcodeOptions,
    qrCodeOptions,
    metadataOptions
};
```

## Schritt 4: Suche durchführen und Ergebnisse verarbeiten

Führen Sie die Suche mit den kombinierten Suchoptionen durch und verarbeiten Sie die Ergebnisse:

```csharp
// Suche nach allen Signaturtypen mit den definierten Optionen
SearchResult result = signature.Search(searchOptions);

// Prüfen, ob Signaturen gefunden wurden
if (result.Signatures.Count > 0)
{
    Console.WriteLine($"\nSource document ['{filePath}'] contains {result.Signatures.Count} signature(s):");
    
    // Durchlaufen Sie die gefundenen Signaturen
    foreach (var foundSignature in result.Signatures)
    {
        Console.WriteLine($"Signature found: Type: {foundSignature.SignatureType}, Page: {foundSignature.PageNumber}, ID: {foundSignature.SignatureId}");
        
        // Prozessspezifische Signaturtypen
        if (foundSignature is TextSignature textSignature)
        {
            Console.WriteLine($"Text: '{textSignature.Text}'");
        }
        else if (foundSignature is BarcodeSignature barcodeSignature)
        {
            Console.WriteLine($"Barcode Type: {barcodeSignature.EncodeType.TypeName}, Text: '{barcodeSignature.Text}'");
        }
        else if (foundSignature is QrCodeSignature qrCodeSignature)
        {
            Console.WriteLine($"QR Code Type: {qrCodeSignature.EncodeType.TypeName}, Text: '{qrCodeSignature.Text}'");
        }
        else if (foundSignature is DigitalSignature digitalSignature)
        {
            Console.WriteLine($"Certificate: {digitalSignature.Certificate?.SubjectName}, Valid: {digitalSignature.IsValid}");
        }
        else if (foundSignature is MetadataSignature metadataSignature)
        {
            Console.WriteLine($"Metadata: Name: {metadataSignature.Name}, Value: {metadataSignature.Value}");
        }
    }
}
else
{
    Console.WriteLine("No signatures were found in the document.");
}
```

## Vollständiges Beispiel

Hier ist ein vollständiges, funktionierendes Beispiel, das die Suche nach mehreren Signaturtypen in einem Dokument demonstriert:

```csharp
using System;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;

namespace MultiSignatureSearch
{
    class Program
    {
        static void Main(string[] args)
        {
            // Dokumentpfad
            string filePath = "sample_multiple_signatures.docx";
            
            // Signaturinstanz initialisieren
            using (Signature signature = new Signature(filePath))
            {
                try
                {
                    // Suchoptionen für Textsignaturen festlegen
                    TextSearchOptions textOptions = new TextSearchOptions
                    {
                        AllPages = true,
                        MatchType = TextMatchType.Contains
                    };

                    // Suchoptionen für digitale Signaturen festlegen
                    DigitalSearchOptions digitalOptions = new DigitalSearchOptions
                    {
                        AllPages = true
                    };

                    // Suchoptionen für Barcode-Signaturen festlegen
                    BarcodeSearchOptions barcodeOptions = new BarcodeSearchOptions
                    {
                        AllPages = true
                    };

                    // Suchoptionen für QR-Code-Signaturen definieren
                    QrCodeSearchOptions qrCodeOptions = new QrCodeSearchOptions
                    {
                        AllPages = true
                    };

                    // Suchoptionen für Metadatensignaturen definieren
                    MetadataSearchOptions metadataOptions = new MetadataSearchOptions();

                    // Erstellen Sie eine Liste mit allen Suchoptionen
                    List<SearchOptions> searchOptions = new List<SearchOptions>
                    {
                        textOptions,
                        digitalOptions,
                        barcodeOptions,
                        qrCodeOptions,
                        metadataOptions
                    };

                    // Suche nach allen Signaturtypen
                    SearchResult result = signature.Search(searchOptions);

                    // Prüfen, ob Signaturen gefunden wurden
                    if (result.Signatures.Count > 0)
                    {
                        Console.WriteLine($"\nSource document ['{filePath}'] contains {result.Signatures.Count} signature(s):");
                        
                        // Ergebnisse nach Signaturtyp verarbeiten
                        foreach (var foundSignature in result.Signatures)
                        {
                            Console.WriteLine($"Signature found: Type: {foundSignature.SignatureType}, Page: {foundSignature.PageNumber}");
                            
                            // Prozessspezifische Signaturtypen
                            switch (foundSignature.SignatureType)
                            {
                                case SignatureType.Text:
                                    var textSignature = foundSignature as TextSignature;
                                    Console.WriteLine($"Text: '{textSignature.Text}'");
                                    break;
                                    
                                case SignatureType.Barcode:
                                    var barcodeSignature = foundSignature as BarcodeSignature;
                                    Console.WriteLine($"Barcode Type: {barcodeSignature.EncodeType.TypeName}, Text: '{barcodeSignature.Text}'");
                                    break;
                                    
                                case SignatureType.QrCode:
                                    var qrCodeSignature = foundSignature as QrCodeSignature;
                                    Console.WriteLine($"QR Code Type: {qrCodeSignature.EncodeType.TypeName}, Text: '{qrCodeSignature.Text}'");
                                    break;
                                    
                                case SignatureType.Digital:
                                    var digitalSignature = foundSignature as DigitalSignature;
                                    Console.WriteLine($"Certificate: {digitalSignature.Certificate?.SubjectName}, Valid: {digitalSignature.IsValid}");
                                    break;
                                    
                                case SignatureType.Metadata:
                                    var metadataSignature = foundSignature as MetadataSignature;
                                    Console.WriteLine($"Metadata: Name: {metadataSignature.Name}, Value: {metadataSignature.Value}");
                                    break;
                            }
                            
                            Console.WriteLine(); // Zeilenumbruch zwischen Signaturen hinzufügen
                        }
                    }
                    else
                    {
                        Console.WriteLine("No signatures were found in the document.");
                    }
                }
                catch (Exception ex)
                {
                    Console.WriteLine($"Error occurred: {ex.Message}");
                }
            }
            
            Console.WriteLine("Press any key to exit...");
            Console.ReadKey();
        }
    }
}
```

## Erweiterte Multi-Signatur-Suchtechniken

### Filtern von Suchergebnissen

Sie können erweiterte Filter implementieren, um die Suchergebnisse einzugrenzen:

```csharp
// Ergebnisse nach Seitenzahl filtern
var signaturesOnFirstPage = result.Signatures.FindAll(s => s.PageNumber == 1);

// Ergebnisse nach Signaturtyp filtern
var digitalSignatures = result.Signatures.FindAll(s => s.SignatureType == SignatureType.Digital);
var qrCodeSignatures = result.Signatures.FindAll(s => s.SignatureType == SignatureType.QrCode);

// Filtern Sie Textsignaturen mit bestimmten Inhalten
var approvalSignatures = result.Signatures
    .FindAll(s => s is TextSignature && ((TextSignature)s).Text.Contains("Approved"));
```

### Validieren mehrerer Signaturen

Implementieren Sie eine Validierungslogik für verschiedene Signaturtypen:

```csharp
bool ValidateAllSignatures(SearchResult result)
{
    bool isDocumentValid = true;
    
    // Prüfen, ob ein Dokument eine gültige digitale Signatur hat
    bool hasValidDigitalSignature = result.Signatures
        .Any(s => s is DigitalSignature && ((DigitalSignature)s).IsValid);
    
    if (!hasValidDigitalSignature)
    {
        Console.WriteLine("Warning: Document does not contain a valid digital signature");
        isDocumentValid = false;
    }
    
    // Prüfen Sie, ob das Dokument den erforderlichen QR-Code enthält
    bool hasRequiredQRCode = result.Signatures
        .Any(s => s is QrCodeSignature && ((QrCodeSignature)s).Text.Contains("Auth-Code"));
    
    if (!hasRequiredQRCode)
    {
        Console.WriteLine("Warning: Document does not contain the required authentication QR code");
        isDocumentValid = false;
    }
    
    return isDocumentValid;
}
```

### Suchen mit benutzerdefinierter Verarbeitung

Sie können eine benutzerdefinierte Verarbeitungslogik für Suchvorgänge definieren:

```csharp
// Erstellen Sie Suchoptionen mit benutzerdefinierter Verarbeitung
TextSearchOptions textOptions = new TextSearchOptions
{
    AllPages = true,
    
    // Definieren Sie die benutzerdefinierte Verarbeitung mithilfe eines Delegaten
    ProcessCompleted = (signature) =>
    {
        // Benutzerdefinierte Validierungslogik – akzeptieren Sie nur Signaturen auf bestimmten Seiten
        TextSignature textSignature = signature as TextSignature;
        return textSignature != null && (textSignature.PageNumber == 1 || textSignature.PageNumber == 2);
    }
};
```

## Abschluss

In diesem umfassenden Leitfaden haben wir untersucht, wie Sie mit GroupDocs.Signature für .NET nach verschiedenen Signaturtypen in Dokumenten suchen. Von der Einrichtung von Suchoptionen für verschiedene Signaturtypen bis hin zur Verarbeitung und Validierung der Ergebnisse verfügen Sie nun über das Wissen, um eine robuste Signatursuchfunktion in Ihren .NET-Anwendungen zu implementieren.

Die Möglichkeit, gleichzeitig nach mehreren Signaturtypen zu suchen, verbessert die Dokumentenüberprüfung, stärkt die Sicherheitsmaßnahmen und optimiert die Workflows zur Dokumentenvalidierung. GroupDocs.Signature bietet ein leistungsstarkes, flexibles Framework für die Arbeit mit verschiedenen Signaturtypen in unterschiedlichen Dokumentformaten und ist somit eine hervorragende Wahl für Anwendungen zur Dokumentenverarbeitung.

## Häufig gestellte Fragen

### Kann ich in passwortgeschützten Dokumenten nach Signaturen suchen?

Ja, GroupDocs.Signature unterstützt die Suche nach Signaturen in passwortgeschützten Dokumenten. Sie können das Passwort bei der Initialisierung des `Signature` Objekt:

```csharp
LoadOptions loadOptions = new LoadOptions { Password = "your_password" };
using (Signature signature = new Signature(filePath, loadOptions))
{
    // Suche nach Signaturen
}
```

### Welche Dokumentformate werden für die Signatursuche unterstützt?

GroupDocs.Signature unterstützt eine Vielzahl von Dokumentformaten, darunter PDF, Microsoft Office-Dokumente (Word, Excel, PowerPoint), OpenOffice-Formate, Bilder und mehr.

### Kann ich die Suche auf bestimmte Seiten in einem Dokument beschränken?

Ja, jeder Suchoptionstyp verfügt über Eigenschaften, mit denen Sie angeben können, welche Seiten durchsucht werden sollen:

```csharp
TextSearchOptions options = new TextSearchOptions
{
    AllPages = false,  // Nicht alle Seiten durchsuchen
    PageNumber = 1,    // Suche nur auf Seite 1
    
    // Oder geben Sie mehrere Seiten an
    PagesSetup = new PagesSetup { Pages = new List<int> { 1, 3, 5 } }
};
```

### Wie kann ich die Leistung bei der Suche in großen Dokumenten optimieren?

Bei großen Dokumenten können Sie die Leistung folgendermaßen optimieren:

1. Einschränken der Suche auf bestimmte Seiten oder Seitenbereiche
2. Verwenden Sie spezifischere Suchkriterien, um die Anzahl potenzieller Übereinstimmungen zu reduzieren
3. Implementieren der Paginierung in Ihrer Ergebnisanzeige
4. Suchen Sie jeweils nach einem Signaturtyp, wenn Sie keine gleichzeitigen Ergebnisse benötigen

### Kann ich GroupDocs.Signature erweitern, um benutzerdefinierte Signaturtypen zu unterstützen?

Während GroupDocs.Signature integrierte Unterstützung für gängige Signaturtypen bietet, können Sie seine Funktionalität wie folgt erweitern:

1. Erstellen von benutzerdefinierten Suchoptionsklassen, abgeleitet von `SearchOptions`
2. Implementieren einer benutzerdefinierten Verarbeitungslogik mithilfe der `ProcessCompleted` delegieren
3. Entwicklung von Wrapper-Klassen, die mehrere Signatursuchen mit erweiterter Geschäftslogik kombinieren

## Siehe auch

* [API-Referenz](https://reference.groupdocs.com/signature/net/)
* [Codebeispiele auf GitHub](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
* [Produktdokumentation](https://docs.groupdocs.com/signature/net/)
* [Produktseite](https://products.groupdocs.com/signature/net/)
* [Lade die neueste Version herunter](https://releases.groupdocs.com/signature/net/)
* [Blogartikel](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
* [Kostenloses Support-Forum](https://forum.groupdocs.com/c/signature/13)
* [Temporäre Lizenz](https://purchase.groupdocs.com/temporary-license/)