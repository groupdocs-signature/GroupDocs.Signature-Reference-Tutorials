---
"description": "Erfahren Sie mit dieser umfassenden Schritt-für-Schritt-Anleitung und Codebeispielen, wie Sie mit GroupDocs.Signature für .NET effizient nach QR-Codes in Dokumenten suchen."
"linktitle": "Suche nach QR-Codes"
"second_title": "GroupDocs.Signature .NET API"
"title": "Suche nach QR-Code-Signaturen in Dokumenten"
"url": "/de/net/signature-searching/search-for-qr-codes/"
"weight": 15
---

## Einführung

Im heutigen digitalen Dokumenten-Ökosystem sind QR-Code-Signaturen zu einem unverzichtbaren Werkzeug für die Einbettung von Informationen, die Authentifizierung und die Verbesserung der Dokumentensicherheit geworden. GroupDocs.Signature für .NET bietet Entwicklern eine leistungsstarke API zum Suchen und Extrahieren von QR-Codes aus verschiedenen Dokumentformaten und ermöglicht so erweiterte Dokumentanalyse- und Verifizierungsfunktionen in .NET-Anwendungen.

Dieses umfassende Tutorial führt Sie durch den Prozess der Implementierung der QR-Code-Suchfunktion mit GroupDocs.Signature für .NET und bietet klare Erklärungen, Schritt-für-Schritt-Anleitungen und praktische Codebeispiele, die Sie in Ihre eigenen Anwendungen integrieren können.

## Voraussetzungen

Bevor Sie mit der Suche nach QR-Code-Signaturen beginnen, stellen Sie sicher, dass Sie die folgenden Voraussetzungen erfüllen:

1. GroupDocs.Signature für .NET SDK: Laden Sie das SDK herunter und installieren Sie es von der [Download-Seite](https://releases.groupdocs.com/signature/net/).

2. Entwicklungsumgebung: Richten Sie eine .NET-Entwicklungsumgebung wie Visual Studio mit installiertem .NET Framework oder .NET Core ein.

3. Grundkenntnisse: Vertrautheit mit C#-Programmierung und .NET-Entwicklungskonzepten.

4. Beispieldokumente: Bereiten Sie Testdokumente mit QR-Codes zur Überprüfung und zum Testen vor.

## Namespaces importieren

Beginnen Sie mit dem Importieren der erforderlichen Namespaces, um auf die GroupDocs.Signature-Funktionalität zuzugreifen:

```csharp
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
using System;
using System.Collections.Generic;
```

Lassen Sie uns nun den Prozess der Suche nach QR-Codes in klare, leicht verständliche Schritte unterteilen:

## Schritt 1: Dokumentpfad definieren

Geben Sie zunächst den Pfad zum Dokument mit den QR-Codes an, nach denen Sie suchen möchten:

```csharp
string filePath = "sample_multiple_signatures.docx";
```

## Schritt 2: Initialisieren des Signaturobjekts

Erstellen Sie eine Instanz des `Signature` Klasse durch Übergabe des Dokumentpfads:

```csharp
using (Signature signature = new Signature(filePath))
{
    // Der QR-Code-Suchcode wird hier hinzugefügt
}
```

## Schritt 3: Suche nach QR-Code-Signaturen

Verwenden Sie die `Search` Methode mit dem entsprechenden Signaturtyp, um QR-Codes im Dokument zu finden:

```csharp
// Suche nach QR-Code-Signaturen im Dokument
List<QrCodeSignature> signatures = signature.Search<QrCodeSignature>(SignatureType.QrCode);
```

## Schritt 4: Ergebnisse verarbeiten und anzeigen

Durchlaufen Sie die gefundenen QR-Code-Signaturen und greifen Sie auf ihre Eigenschaften zu:

```csharp
// Informationen zu gefundenen QR-Codes anzeigen
Console.WriteLine($"\nSource document contains {signatures.Count} QR code signature(s):");

foreach (var qrCodeSignature in signatures)
{
    Console.WriteLine($"QR Code found at page {qrCodeSignature.PageNumber} with type {qrCodeSignature.EncodeType.TypeName}");
    Console.WriteLine($"Content: {qrCodeSignature.Text}");
    Console.WriteLine($"Location: X={qrCodeSignature.Left}, Y={qrCodeSignature.Top}, Width={qrCodeSignature.Width}, Height={qrCodeSignature.Height}");
    Console.WriteLine();
}
```

## Vollständiges Beispiel

Hier ist ein umfassendes funktionierendes Beispiel, das den vollständigen Prozess der Suche nach QR-Codes in einem Dokument demonstriert:

```csharp
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
using System;
using System.Collections.Generic;

namespace QrCodeSignatureSearch
{
    class Program
    {
        static void Main(string[] args)
        {
            // Dokumentpfad – aktualisieren Sie mit Ihrem Dateipfad
            string filePath = "sample_multiple_signatures.docx";
            
            // Signaturinstanz initialisieren
            using (Signature signature = new Signature(filePath))
            {
                try
                {
                    // Suche nach QR-Code-Signaturen im Dokument
                    List<QrCodeSignature> signatures = signature.Search<QrCodeSignature>(SignatureType.QrCode);
                    
                    // Suchergebnisse anzeigen
                    Console.WriteLine($"\nSource document ['{filePath}'] contains {signatures.Count} QR code signature(s):");
                    
                    foreach (var qrCodeSignature in signatures)
                    {
                        Console.WriteLine($"QR Code found at page {qrCodeSignature.PageNumber} with type {qrCodeSignature.EncodeType.TypeName}");
                        Console.WriteLine($"Content: {qrCodeSignature.Text}");
                        Console.WriteLine($"Location: X={qrCodeSignature.Left}, Y={qrCodeSignature.Top}, Width={qrCodeSignature.Width}, Height={qrCodeSignature.Height}");
                        Console.WriteLine();
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

## Erweiterte QR-Code-Suchtechniken

### Suche mit bestimmten Kriterien

Für gezieltere Suchen können Sie `QrCodeSearchOptions` So passen Sie Ihre Suchkriterien an:

```csharp
// Erstellen Sie QR-Code-Suchoptionen mit bestimmten Kriterien
QrCodeSearchOptions options = new QrCodeSearchOptions
{
    // Nur auf bestimmten Seiten suchen
    AllPages = false,
    PageNumber = 1,
    PagesSetup = new PagesSetup { Pages = new List<int> { 1, 3, 5 } },
    
    // Filtern nach QR-Code-Inhalt
    Text = "Invoice",
    MatchType = TextMatchType.Contains,
    
    // Filtern nach bestimmten QR-Codetypen
    EncodeType = QrCodeTypes.QR,
    
    // Definieren Sie einen bestimmten Bereich, in dem gesucht werden soll
    Rectangle = new Rectangle(100, 100, 400, 400)
};

// Suche mit spezifischen Optionen
List<QrCodeSignature> filteredSignatures = signature.Search<QrCodeSignature>(options);
```

### Verarbeitung von QR-Code-Daten

Sie können eine benutzerdefinierte Verarbeitung für QR-Code-Daten basierend auf Ihren Anwendungsanforderungen implementieren:

```csharp
foreach (var qrCode in signatures)
{
    // Extrahieren und verarbeiten Sie QR-Code-Daten basierend auf dem Inhalt
    string qrContent = qrCode.Text;
    
    if (qrContent.StartsWith("URL:"))
    {
        // URL-Daten verarbeiten
        string url = qrContent.Substring(4);
        Console.WriteLine($"Found URL in QR code: {url}");
    }
    else if (qrContent.StartsWith("CONTACT:"))
    {
        // Kontaktinformationen verarbeiten
        string contact = qrContent.Substring(8);
        Console.WriteLine($"Found contact information in QR code: {contact}");
    }
    else if (qrContent.StartsWith("INVOICE:"))
    {
        // Rechnungsinformationen verarbeiten
        string invoiceData = qrContent.Substring(8);
        Console.WriteLine($"Found invoice information in QR code: {invoiceData}");
        
        // Rechnungsdaten analysieren und validieren
        if (ValidateInvoiceData(invoiceData))
        {
            Console.WriteLine("Invoice data is valid!");
        }
        else
        {
            Console.WriteLine("Warning: Invalid invoice data detected!");
        }
    }
}

// Beispiel einer Validierungsmethode
static bool ValidateInvoiceData(string data)
{
    // Implementieren Sie Ihre Validierungslogik
    return !string.IsNullOrEmpty(data) && data.Contains("ID") && data.Contains("Amount");
}
```

### Implementieren der Sicherheitsüberprüfung

QR-Codes werden häufig zur Authentifizierung verwendet. So implementieren Sie eine grundlegende Sicherheitsüberprüfung:

```csharp
// Prüfen Sie, ob das Dokument einen gültigen Authentifizierungs-QR-Code enthält
bool hasValidAuthQrCode = false;

foreach (var qrCode in signatures)
{
    if (qrCode.Text.StartsWith("AUTH:"))
    {
        string authCode = qrCode.Text.Substring(5);
        
        // Authentifizierungscode überprüfen (z. B. anhand einer Datenbank oder einer vordefinierten Liste)
        if (VerifyAuthCode(authCode))
        {
            hasValidAuthQrCode = true;
            Console.WriteLine("Document contains valid authentication QR code!");
            break;
        }
    }
}

if (!hasValidAuthQrCode)
{
    Console.WriteLine("Warning: Document does not contain a valid authentication QR code!");
}

// Beispiel einer Überprüfungsmethode
static bool VerifyAuthCode(string code)
{
    // Implementieren Sie Ihre Verifizierungslogik
    // Dies kann eine Datenbanksuche, ein API-Aufruf oder ein Vergleich mit vordefinierten Werten sein.
    return code == "A7B82C3D" || code == "X9Y8Z7W6";
}
```

### Extrahieren von QR-Code-Bildern

Sie können QR-Code-Bilder aus Dokumenten zur weiteren Verarbeitung oder Anzeige extrahieren:

```csharp
// QR-Code-Bilder auf der Festplatte speichern
foreach (var qrCode in signatures)
{
    if (qrCode.Content != null)
    {
        // Erstellen Sie einen eindeutigen Dateinamen basierend auf Seitenzahl und Position
        string outputPath = $"QrCode_P{qrCode.PageNumber}_X{qrCode.Left}_Y{qrCode.Top}.png";
        
        // Speichern der Bilddaten
        File.WriteAllBytes(outputPath, qrCode.Content);
        Console.WriteLine($"Saved QR code image to {outputPath}");
    }
}
```

## Abschluss

In diesem umfassenden Leitfaden haben wir die Suche nach QR-Code-Signaturen in Dokumenten mit GroupDocs.Signature für .NET erläutert. Von der einfachen Suche bis hin zu fortgeschrittenen Techniken verfügen Sie nun über das Wissen, um eine robuste QR-Code-Verarbeitung in Ihren .NET-Anwendungen zu implementieren. Die GroupDocs.Signature-API bietet ein leistungsstarkes, flexibles Framework für die Arbeit mit verschiedenen Signaturtypen, einschließlich QR-Codes, in unterschiedlichen Dokumentformaten.

Durch die Nutzung dieser Funktionen können Sie Dokumentüberprüfungsprozesse verbessern, Authentifizierungssysteme implementieren und wertvolle, in QR-Codes eingebettete Informationen extrahieren – und das alles innerhalb Ihrer .NET-Anwendungen.

## Häufig gestellte Fragen

### Welche QR-Code-Formate werden von GroupDocs.Signature unterstützt?

GroupDocs.Signature unterstützt verschiedene QR-Code-Formate, darunter Standard-QR-Code, Micro-QR-Code und andere gängige QR-Code-Standards. Das spezifische Format kann über die `EncodeType` Eigentum der `QrCodeSignature` Objekt.

### Kann ich in passwortgeschützten Dokumenten nach QR-Codes suchen?

Ja, GroupDocs.Signature unterstützt die Suche nach QR-Codes in passwortgeschützten Dokumenten, indem das Passwort bei der Initialisierung des `Signature` Objekt:

```csharp
LoadOptions loadOptions = new LoadOptions { Password = "your_password" };
using (Signature signature = new Signature(filePath, loadOptions))
{
    // Suche nach QR-Codes
}
```

### Wie kann ich QR-Codes nach ihrem Inhalt filtern?

Sie können QR-Codes anhand ihres Inhalts filtern, indem Sie die `Text` Und `MatchType` Eigenschaften von `QrCodeSearchOptions`:

```csharp
QrCodeSearchOptions options = new QrCodeSearchOptions
{
    Text = "Invoice",
    MatchType = TextMatchType.Contains // Andere Optionen: Genau, BeginntMit, EndetMit
};
```

### Kann GroupDocs.Signature beschädigte oder teilweise sichtbare QR-Codes erkennen?

GroupDocs.Signature kann teilweise sichtbare QR-Codes erkennen, stark beschädigte QR-Codes werden jedoch möglicherweise nicht erkannt. Die Erkennungsgenauigkeit hängt von der Qualität und Sichtbarkeit des QR-Codes im Dokument ab.

### Welche Dokumentformate werden für die QR-Code-Suche unterstützt?

GroupDocs.Signature unterstützt die QR-Code-Suche in verschiedenen Dokumentformaten, darunter PDF, Microsoft Office-Dokumente (Word, Excel, PowerPoint), Bilder (JPEG, PNG, TIFF) und viele andere.

## Siehe auch

* [API-Referenz](https://reference.groupdocs.com/signature/net/)
* [Codebeispiele auf GitHub](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
* [Produktdokumentation](https://docs.groupdocs.com/signature/net/)
* [Produktseite](https://products.groupdocs.com/signature/net/)
* [Lade die neueste Version herunter](https://releases.groupdocs.com/signature/net/)
* [Blogartikel](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
* [Kostenloses Support-Forum](https://forum.groupdocs.com/c/signature/13)
* [Temporäre Lizenz](https://purchase.groupdocs.com/temporary-license/)