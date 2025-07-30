---
"description": "Meistern Sie die Suche nach digitalen Signaturen in Dokumenten mit GroupDocs.Signature für .NET. Verbessern Sie die Dokumentensicherheit und -überprüfung mit unserer detaillierten Schritt-für-Schritt-Anleitung."
"linktitle": "Suche nach digitalen Signaturen"
"second_title": "GroupDocs.Signature .NET API"
"title": "Suche nach digitalen Signaturen in Dokumenten"
"url": "/de/net/signature-searching/search-for-digital-signatures/"
"weight": 11
---

## Einführung

In der heutigen digitalen Landschaft ist die Gewährleistung der Authentizität und Integrität von Dokumenten für Unternehmen und Organisationen von entscheidender Bedeutung. Digitale Signaturen bieten einen robusten Mechanismus zur Überprüfung der Dokumentauthentizität und zur Erkennung nicht autorisierter Änderungen. GroupDocs.Signature für .NET bietet eine umfassende Lösung für die Arbeit mit digitalen Signaturen in verschiedenen Dokumentformaten und ermöglicht Entwicklern die nahtlose Integration von Signaturfunktionen in ihre .NET-Anwendungen.

Dieses Tutorial führt Sie durch den Prozess der Suche nach digitalen Signaturen in Dokumenten mithilfe von GroupDocs.Signature für .NET und bietet detaillierte Erklärungen und praktische Codebeispiele.

## Voraussetzungen

Bevor Sie sich in die Implementierungsdetails vertiefen, stellen Sie sicher, dass Sie die folgenden Voraussetzungen erfüllen:

1. GroupDocs.Signature für .NET: Laden Sie die Bibliothek herunter und installieren Sie sie von [Hier](https://releases.groupdocs.com/signature/net/).
   
2. Entwicklungsumgebung: Richten Sie eine .NET-Entwicklungsumgebung mit Visual Studio oder Ihrer bevorzugten IDE ein.
   
3. Beispieldokumente: Bereiten Sie zu Testzwecken Beispieldokumente mit digitalen Signaturen vor.

4. Grundkenntnisse: Vertrautheit mit der Programmiersprache C# und den Grundlagen des .NET-Frameworks.

## Namespaces importieren

Beginnen Sie mit dem Importieren der erforderlichen Namespaces, um auf die von GroupDocs.Signature für .NET bereitgestellte Funktionalität zuzugreifen:

```csharp
using System;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

Lassen Sie uns nun den Prozess der Suche nach digitalen Signaturen in klare, überschaubare Schritte unterteilen:

## Schritt 1: Signaturobjekt initialisieren

Beginnen Sie mit der Erstellung einer Instanz des `Signature` Klasse, die den Pfad zu Ihrem Dokument übergibt:

```csharp
string filePath = "sample_multiple_signatures.docx";
using (Signature signature = new Signature(filePath))
{
    // Code zum Suchen digitaler Signaturen wird hier hinzugefügt
}
```

## Schritt 2: Suche nach digitalen Signaturen

Verwenden Sie als Nächstes die `Search` Methode mit der `SignatureType.Digital` Parameter zum Suchen nach digitalen Signaturen im Dokument:

```csharp
// Suche nach digitalen Signaturen im Dokument
List<DigitalSignature> signatures = signature.Search<DigitalSignature>(SignatureType.Digital);
```

## Schritt 3: Ergebnisse verarbeiten und anzeigen

Abschließend verarbeiten Sie die Suchergebnisse und zeigen relevante Informationen zu den gefundenen digitalen Signaturen an:

```csharp
Console.WriteLine($"\nSource document ['{filePath}'] contains the following digital signatures:");
foreach (var digitalSignature in signatures)
{
    Console.WriteLine($"Digital signature found from {digitalSignature.SignTime} with validation status: {digitalSignature.IsValid}");
    Console.WriteLine($"Certificate: Subject: {digitalSignature.Certificate?.SubjectName}");
    Console.WriteLine($"Certificate: Issuer: {digitalSignature.Certificate?.IssuerName}");
    Console.WriteLine($"Certificate: Serial Number: {digitalSignature.Certificate?.SerialNumber}");
    Console.WriteLine();
}
```

## Vollständiges Beispiel

Hier ist ein vollständiges, funktionierendes Beispiel, das zeigt, wie Sie in einem Dokument nach digitalen Signaturen suchen:

```csharp
using System;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;

namespace SearchDigitalSignatures
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
                // Suche nach digitalen Signaturen im Dokument
                List<DigitalSignature> signatures = signature.Search<DigitalSignature>(SignatureType.Digital);
                
                // Suchergebnisse anzeigen
                Console.WriteLine($"\nSource document ['{filePath}'] contains the following digital signatures:");
                
                if (signatures.Count > 0)
                {
                    foreach (var digitalSignature in signatures)
                    {
                        Console.WriteLine($"Digital signature found from {digitalSignature.SignTime} with validation status: {digitalSignature.IsValid}");
                        Console.WriteLine($"Certificate: Subject: {digitalSignature.Certificate?.SubjectName}");
                        Console.WriteLine($"Certificate: Issuer: {digitalSignature.Certificate?.IssuerName}");
                        Console.WriteLine($"Certificate: Serial Number: {digitalSignature.Certificate?.SerialNumber}");
                        Console.WriteLine();
                    }
                }
                else
                {
                    Console.WriteLine("No digital signatures found in the document.");
                }
            }
        }
    }
}
```

## Erweiterte Suchoptionen

Für gezieltere Suchen können Sie `DigitalSearchOptions` So passen Sie die Suchkriterien an:

```csharp
// Digitale Suchoptionen schaffen
DigitalSearchOptions options = new DigitalSearchOptions()
{
    // Suche nur auf bestimmten Seiten (zB Seite 1 und 2)
    PageNumber = 1,
    PagesSetup = new PagesSetup() { Pages = new List<int> { 1, 2 } },
    
    // Filtern nach Kommentaren in digitalen Signaturen
    Comments = "Approved",
    
    // Datums- und Zeitbereich für die Suche festlegen
    SignDateTimeFrom = new DateTime(2022, 1, 1),
    SignDateTimeTo = DateTime.Now
};

// Suche mit spezifischen Optionen
List<DigitalSignature> signatures = signature.Search<DigitalSignature>(options);
```

## Arbeiten mit Zertifikatsinformationen

Digitale Signaturen enthalten wertvolle Zertifikatsinformationen, auf die Sie zugreifen und die Sie validieren können:

```csharp
foreach (var digitalSignature in signatures)
{
    if (digitalSignature.Certificate != null)
    {
        // Zugriff auf Zertifikateigenschaften
        Console.WriteLine($"Certificate Valid From: {digitalSignature.Certificate.NotBefore}");
        Console.WriteLine($"Certificate Valid To: {digitalSignature.Certificate.NotAfter}");
        
        // Prüfen, ob das Zertifikat in einem gültigen Datumsbereich liegt
        bool isDateValid = DateTime.Now >= digitalSignature.Certificate.NotBefore && 
                          DateTime.Now <= digitalSignature.Certificate.NotAfter;
        
        Console.WriteLine($"Certificate Date Validity: {isDateValid}");
        
        // Zugriff auf die Ausstellerdetails des Zertifikats
        Console.WriteLine($"Certificate Issuer: {digitalSignature.Certificate.IssuerName}");
    }
}
```

## Abschluss

GroupDocs.Signature für .NET bietet eine leistungsstarke und flexible Lösung zum Suchen und Validieren digitaler Signaturen in Dokumenten. In diesem Tutorial haben wir die Implementierung der Suchfunktion für digitale Signaturen in .NET-Anwendungen Schritt für Schritt erläutert und Ihnen das Wissen vermittelt, wie Sie die Dokumentensicherheit und Integritätsprüfung verbessern können.

Durch die Nutzung von GroupDocs.Signature können Sie robuste Dokumentenverwaltungssysteme erstellen, die die Authentizität und Integrität Ihrer digitalen Dokumente gewährleisten und so das Vertrauen und die Compliance in Ihren Geschäftsprozessen fördern.

## Häufig gestellte Fragen

### Kann GroupDocs.Signature die Gültigkeit digitaler Signaturen überprüfen?

Ja, GroupDocs.Signature validiert digitale Signaturen automatisch während des Suchvorgangs und stellt den Validierungsstatus über die `IsValid` Eigentum der `DigitalSignature` Klasse.

### Welche Dokumentformate unterstützen die Suche nach digitalen Signaturen?

GroupDocs.Signature unterstützt die Suche nach digitalen Signaturen in verschiedenen Formaten, darunter PDF, Microsoft Office-Dokumente (Word, Excel, PowerPoint), OpenOffice-Formate und mehr.

### Kann ich in passwortgeschützten Dokumenten nach digitalen Signaturen suchen?

Ja, Sie können nach digitalen Signaturen in passwortgeschützten Dokumenten suchen, indem Sie das Passwort bei der Initialisierung des `Signature` Objekt:

```csharp
LoadOptions loadOptions = new LoadOptions() { Password = "your_password" };
using (Signature signature = new Signature(filePath, loadOptions))
{
    // Suche nach digitalen Signaturen
}
```

### Wie kann ich überprüfen, ob eine digitale Signatur von einer bestimmten Person erstellt wurde?

Sie können den Betreffnamen und andere Eigenschaften des Zertifikats prüfen, um die Identität des Unterzeichners zu bestätigen:

```csharp
foreach (var signature in signatures)
{
    if (signature.Certificate?.SubjectName?.Contains("John Doe") == true)
    {
        Console.WriteLine("Found signature by John Doe");
    }
}
```

### Kann ich den öffentlichen Schlüssel aus einem digitalen Signaturzertifikat extrahieren?

Ja, Sie können über die Zertifikatseigenschaften auf die Informationen zum öffentlichen Schlüssel zugreifen:

```csharp
if (signature.Certificate != null)
{
    // Zugriff auf öffentliche Schlüsselinformationen
    Console.WriteLine($"Public Key: {signature.Certificate.GetPublicKeyString()}");
}
```

## Siehe auch

* [API-Referenz](https://reference.groupdocs.com/signature/net/)
* [Codebeispiele](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
* [Produktdokumentation](https://docs.groupdocs.com/signature/net/)
* [Produktseite](https://products.groupdocs.com/signature/net/)
* [Lade die neueste Version herunter](https://releases.groupdocs.com/signature/net/)
* [Blogartikel](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
* [Support-Forum](https://forum.groupdocs.com/c/signature/13)
* [Temporäre Lizenz](https://purchase.groupdocs.com/temporary-license/)