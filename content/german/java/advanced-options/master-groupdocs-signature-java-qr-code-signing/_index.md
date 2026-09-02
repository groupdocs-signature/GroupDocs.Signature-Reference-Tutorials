---
categories:
- Java Development
date: '2026-05-21'
description: Erfahren Sie, wie Sie qr code java signatures in PDFs mit GroupDocs.Signature
  für Java erzeugen. Enthält Maven-Setup, positioning-Tipps und production best practices.
keywords:
- generate qr code java
- java generate qr code
- groupdocs signature java
lastmod: '2026-05-21'
linktitle: QR Code Signing Java Leitfaden
schemas:
- author: GroupDocs
  dateModified: '2026-05-21'
  description: Learn how to generate qr code java signatures in PDFs using GroupDocs.Signature
    for Java. Includes Maven setup, positioning tips, and production best practices.
  headline: 'generate qr code java: Complete QR Code Signing Guide'
  type: TechArticle
- description: Learn how to generate qr code java signatures in PDFs using GroupDocs.Signature
    for Java. Includes Maven setup, positioning tips, and production best practices.
  name: 'generate qr code java: Complete QR Code Signing Guide'
  steps:
  - name: Use absolute paths or ensure the working directory is correct.
    text: Use absolute paths or ensure the working directory is correct.
  - name: Confirm read permissions for the source and write permissions for the output
      folder.
    text: Confirm read permissions for the source and write permissions for the output
      folder.
  - name: Escape any special characters in the path.
    text: Escape any special characters in the path.
  - name: '**Batch Processing** – process documents in parallel, but cap concurrency
      based on RAM.'
    text: '**Batch Processing** – process documents in parallel, but cap concurrency
      based on RAM.'
  - name: '**Caching** – reuse identical `QrCodeSignOptions` objects across documents.'
    text: '**Caching** – reuse identical `QrCodeSignOptions` objects across documents.'
  - name: '**Async Operations** – move signing to background workers for responsive
      APIs.'
    text: '**Async Operations** – move signing to background workers for responsive
      APIs.'
  - name: '**Memory Monitoring** – set alerts for spikes and tune batch size accordingly.'
    text: '**Memory Monitoring** – set alerts for spikes and tune batch size accordingly.'
  - name: Verify the output file is actually created.
    text: Verify the output file is actually created.
  - name: Confirm you’re opening the correct output file.
    text: Confirm you’re opening the correct output file.
  - name: Check `SignResult` for a success count.
    text: Check `SignResult` for a success count.
  type: HowTo
- questions:
  - answer: GroupDocs.Signature for Java
    question: What library adds QR code signatures in Java?
  - answer: Maven (see *maven dependency groupdocs*)
    question: Which build tool supports the Maven dependency?
  - answer: Yes, using alignment and page‑number options
    question: Can I position QR codes on specific pages?
  - answer: Yes, a commercial GroupDocs license is required
    question: Do I need a license for production?
  - answer: Absolutely, when sized ≥ 100 × 100 px and placed with proper margins
    question: Is the QR code scannable after signing?
  type: FAQPage
tags:
- QR codes
- PDF signing
- digital signatures
- document security
title: 'qr code java generieren: Vollständiger Leitfaden zur QR-Code-Signatur'
type: docs
url: /de/java/advanced-options/master-groupdocs-signature-java-qr-code-signing/
weight: 1
---

# QR-Code in Java generieren: Vollständiger Leitfaden zum Signieren von QR-Codes

In diesem Tutorial lernen Sie, wie Sie **generate qr code java** Signaturen in PDF-Dokumenten mit GroupDocs.Signature für Java erzeugen. Wir zeigen, wie QR-Codes hinzugefügt, präzise positioniert und typische Fallstricke vermieden werden, die die meisten Entwickler überraschen. Egal, ob Sie eine Vertrags‑Management‑Plattform oder eine sichere Rechnungs‑Pipeline bauen, bietet dieser Leitfaden eine produktionsreife Lösung.

## Schnelle Antworten
- **Welche Bibliothek fügt QR-Code‑Signaturen in Java hinzu?** GroupDocs.Signature for Java  
- **Welches Build‑Tool unterstützt die Maven‑Abhängigkeit?** Maven (siehe *maven dependency groupdocs*)  
- **Kann ich QR-Codes auf bestimmten Seiten positionieren?** Ja, mittels Ausrichtungs‑ und Seitenzahl‑Optionen  
- **Benötige ich eine Lizenz für die Produktion?** Ja, eine kommerzielle GroupDocs‑Lizenz ist erforderlich  
- **Ist der QR-Code nach dem Signieren scanbar?** Absolut, wenn er ≥ 100 × 100 px groß ist und mit korrekten Rändern platziert wird  

## Was Sie lernen werden
Am Ende dieses Leitfadens wissen Sie, wie Sie:
- QR-Code‑Signaturen in Ihrem Java‑Projekt einrichten (Maven, Gradle oder direkter Download)  
- QR-Codes an genauen Positionen zu Dokumenten hinzufügen (Ecken, Zentren, benutzerdefinierte Ausrichtungen)  
- Häufige Implementierungsprobleme behandeln, bevor sie zu Produktionsproblemen werden  
- Die Leistung für hochdurchsatzfähige Dokumenten‑Workflows optimieren  
- Diese Techniken in realen Geschäftsszenarien anwenden  

## Voraussetzungen
Bevor wir in den Code eintauchen, stellen Sie sicher, dass Sie Folgendes haben:
- **GroupDocs.Signature for Java** – Version 23.12 oder höher (die Installation wird weiter unten behandelt)  
- **Java Development Kit** – JDK 8 oder höher (die meisten Produktionsumgebungen verwenden JDK 11+)  
- **Build‑Tool** – Maven oder Gradle für das Abhängigkeitsmanagement  
- **Grundlegende Java‑Kenntnisse** – vertraut mit try‑catch‑Blöcken und dem Umgang mit Dateipfaden  

Keine Sorge, wenn Sie neu bei GroupDocs sind – wir gehen alles Schritt für Schritt durch.

## Einrichtung Ihrer Umgebung
GroupDocs.Signature in Ihr Projekt zu integrieren ist unkompliziert. Wählen Sie die Methode, die zu Ihrem Build‑System passt.

### Verwendung von Maven
Fügen Sie diese **maven dependency groupdocs** zu Ihrer `pom.xml`‑Datei hinzu:

``` 
```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```
```

Nachdem Sie dies hinzugefügt haben, führen Sie `mvn clean install` aus, um die Bibliothek herunterzuladen.

### Verwendung von Gradle
Für Gradle‑Projekte fügen Sie diese Zeile zu Ihrer `build.gradle`‑Datei hinzu:

``` 
```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```
```

Synchronisieren Sie dann Ihr Projekt mit `gradle build`.

### Direkter Download
Bevorzugen Sie eine manuelle Installation? Laden Sie das JAR direkt von [GroupDocs.Signature for Java releases](https://releases.groupdocs.com/signature/java/) herunter und fügen Sie es dem Klassenpfad Ihres Projekts hinzu.

### Lizenzsetup (Wichtig!)
Hier ist etwas, das viele überrascht: GroupDocs erfordert für die Produktion eine Lizenz. Optionen:
- **Kostenlose Testversion** – volle Funktionen, zeitlich begrenzt  
- **Temporäre Lizenz** – benötigen Sie mehr Zeit? Holen Sie sich eine [temporary license](https://purchase.groupdocs.com/temporary-license/) für erweitertes Testen  
- **Kommerzielle Lizenz** – für Produktionsbereitstellungen, [purchase a license](https://purchase.groupdocs.com/buy)  

Die Testversion fügt ein Wasserzeichen hinzu, planen Sie also entsprechend für Demos.

## Grundlegende Initialisierung
`Signature` ist die zentrale Einstiegsklasse in GroupDocs.Signature für Java, die Dokumente zum Signieren lädt und manipuliert. Sobald Sie die Bibliothek installiert haben, ist die Initialisierung so einfach wie das Verweisen auf Ihr Dokument:

``` 
```java
String filePath = "YOUR_DOCUMENT_DIRECTORY/sample.pdf";
Signature signature = new Signature(filePath);
```
```

Damit wird ein `Signature`‑Objekt erstellt, das einsatzbereit ist.

## Verständnis von QR-Code‑Signaturen
Eine QR-Code‑Signatur bettet verifizierbare Daten – wie Zeitstempel, Signatur‑Identität oder Verifizierungs‑URLs – in ein scanbares QR‑Bild im Dokument ein. Beim Scannen leitet der QR‑Code den Benutzer zu einem Verifizierungs‑Portal weiter oder zeigt eingebettete Metadaten an, wodurch eine schnelle mobile Verifizierung ohne spezielle Software ermöglicht wird.

**Wann sollten Sie QR-Code‑Signaturen verwenden?**
- Schnelle mobile Verifizierung (mit dem Telefon scannen)  
- Physische Kopien, die gedruckt werden können  
- Einbetten von Links zu Verifizierungs‑Portalen  
- Unterstützung von Offline‑Verifizierungs‑Workflows  

## Implementierungs‑Leitfaden: Hinzufügen von QR-Code‑Signaturen
Hier wird der Code praktisch. Wir signieren ein PDF mit QR‑Codes, die an verschiedenen Positionen auf der Seite platziert sind.

### Warum die Positionierung wichtig ist
Eine korrekte Positionierung stellt sicher, dass der QR‑Code leicht scanbar ist, gesetzlichen Standards entspricht und wichtige Dokumenteninhalte nicht verdeckt. Für Verträge ist unten‑rechts üblich; für Rechnungen funktioniert oben‑rechts am besten; für Zertifikate bietet die Zentrierung am unteren Rand ein sauberes Aussehen.

### Schritt‑für‑Schritt‑Implementierung
#### 1. Konfigurieren Sie Ihre Dateipfade
Definieren Sie, wo Ihr Quelldokument liegt und wo die signierte Version gespeichert werden soll:

``` 
```java
String filePath = "YOUR_DOCUMENT_DIRECTORY/sample.pdf";
String fileName = Paths.get(filePath).getFileName().toString();
String outputFilePath = new File("YOUR_OUTPUT_DIRECTORY", "SignWithAlignment/" + fileName).getPath();
```
```

**Pro‑Tipp:** Verwenden Sie `Paths.get()` anstelle von String‑Verkettung für Dateipfade – es verarbeitet automatisch betriebssystemspezifische Trennzeichen.

#### 2. Initialisieren Sie das Signature‑Objekt
Kapseln Sie Ihre Initialisierung in einen try‑catch‑Block, um mögliche Datei‑Zugriffsprobleme zu behandeln:

``` 
```java
try {
    Signature signature = new Signature(filePath);
    // Signing logic goes here...
} catch (Exception e) {
    throw new RuntimeException("Error initializing signature: " + e.getMessage(), e);
}
```
```

`RuntimeException` fügt beim Debuggen Kontext hinzu, was in der Produktion Zeit spart.

#### 3. Definieren Sie QR‑Code‑Größe und Positionen
`QrCodeSignOptions` konfiguriert das QR‑Bild, das im Dokument platziert wird. Es ermöglicht das Festlegen von Größe, Rändern und Ausrichtung.

``` 
```java
int qrWidth = 100;
int qrHeight = 100;
List<SignOptions> listOptions = new ArrayList<>();

for (int horizontalAlignment : HorizontalAlignment.getValues()) {
    for (int verticalAlignment : VerticalAlignment.getValues()) {
        if (verticalAlignment != VerticalAlignment.None && horizontalAlignment != HorizontalAlignment.None) {
            QrCodeSignOptions options = new QrCodeSignOptions("Left-Top");
            options.setWidth(qrWidth);
            options.setHeight(qrHeight);
            options.setHorizontalAlignment(horizontalAlignment);
            options.setVerticalAlignment(verticalAlignment);
            options.setMargin(new Padding(5));
            listOptions.add(options);
        }
    }
}
```
```

Die Schleife erstellt QR‑Code‑Optionen für jede horizontale (Links, Mitte, Rechts) und vertikale (Oben, Mitte, Unten) Ausrichtung und fügt einen 5‑Pixel‑Rand hinzu, sodass der Code nie die Seitenkante berührt.

Für die meisten Produktionsszenarien wählen Sie eine einzelne Position, z. B. unten‑rechts für Verträge:

``` 
```java
QrCodeSignOptions options = new QrCodeSignOptions("Signature");
options.setWidth(100);
options.setHeight(100);
options.setHorizontalAlignment(HorizontalAlignment.Right);
options.setVerticalAlignment(VerticalAlignment.Bottom);
options.setMargin(new Padding(10));
```
```

#### 4. Signieren Sie das Dokument
Jetzt wenden wir alle konfigurierten Signaturen in einem Vorgang an:

``` 
```java
SignResult signResult = signature.sign(outputFilePath, listOptions);
```
```

Die Methode `sign()` verarbeitet jeden QR‑Code in der Liste und speichert das Ergebnis in Ihrem Ausgabepfad. Sie gibt ein `SignResult`‑Objekt zurück, das angibt, wie viele Signaturen erfolgreich hinzugefügt wurden – ideal für das Logging.

**Hinweis zur Leistung:** Das Signieren ist synchron. Für Hochvolumen‑Workloads (Hunderte Dokumente pro Stunde) führen Sie dies in einer Hintergrund‑Job‑Warteschlange statt in einer benutzerorientierten Anfrage aus.

## Häufige Fallstricke und Lösungen
### Problem 1: „Datei nicht gefunden“-Fehler
**Symptom:** Eine Datei‑nicht‑gefunden‑Ausnahme, obwohl die Datei existiert.  
**Lösung:** Überprüfen Sie drei Dinge:
1. Verwenden Sie absolute Pfade oder stellen Sie sicher, dass das Arbeitsverzeichnis korrekt ist.  
2. Bestätigen Sie Lese‑Berechtigungen für die Quelle und Schreib‑Berechtigungen für den Ausgabordner.  
3. Escapen Sie Sonderzeichen im Pfad.  

``` 
```java
// Better approach: Use absolute paths
String absolutePath = new File(filePath).getAbsolutePath();
Signature signature = new Signature(absolutePath);
```
```

### Problem 2: QR‑Codes überlappen Dokumenteninhalt
**Symptom:** QR‑Codes verdecken wichtigen Text oder werden an Seitenrändern abgeschnitten.  
**Lösung:** Erhöhen Sie die Randwerte und wählen Sie Ausrichtungen, die den Code in leeren Bereichen halten:

``` 
```java
options.setMargin(new Padding(20)); // Increase from 5 to 20 pixels
```
```

### Problem 3: Speicherprobleme bei großen Dokumenten
**Symptom:** `OutOfMemoryError` beim Verarbeiten von PDFs über 10 MB.  
**Lösung:** Entsorgen Sie `Signature`‑Objekte umgehend und verarbeiten Sie große Dateien in Batches:

``` 
```java
try (Signature signature = new Signature(filePath)) {
    // Your signing code
} // Automatically closes and releases resources
```
```

Die try‑with‑resources‑Anweisung garantiert Aufräumen, selbst wenn eine Ausnahme auftritt.

### Problem 4: QR‑Code‑Inhalt wird nicht aktualisiert
**Symptom:** Alle QR‑Codes zeigen denselben Text, obwohl versucht wird, sie anzupassen.  
**Lösung:** Erstellen Sie für jede Position eine **neue** `QrCodeSignOptions`‑Instanz, anstatt dasselbe Objekt wiederzuverwenden:

``` 
```java
// Wrong - reuses same object
QrCodeSignOptions options = new QrCodeSignOptions("Text");
options.setHorizontalAlignment(HorizontalAlignment.Left);
listOptions.add(options);
options.setHorizontalAlignment(HorizontalAlignment.Right); // Modifies existing!
listOptions.add(options);

// Correct - creates new object each time
listOptions.add(new QrCodeSignOptions("Left"));
listOptions.add(new QrCodeSignOptions("Right"));
```
```

## Praktische Anwendungen
### 1. Vertrags‑Management‑Systeme
Ablauf: Vertrags‑PDF erzeugen → QR‑Code mit Vertrags‑ID, Zeitstempel, Signatur‑Hash hinzufügen → sicher speichern → Benutzer scannt QR → Portal zeigt Vertragsdetails an. So können Rechtsteams die Authentizität von gedruckten Kopien sofort prüfen.

### 2. Automatisierung der Rechnungs‑Verarbeitung
Fügen Sie jedem verarbeiteten Rechnung einen QR‑Code oben‑rechts hinzu, der Rechnungsnummer, Lieferanten‑ID und Verarbeitungs‑Zeitstempel kodiert. Konsistente Platzierung ermöglicht automatisierten Scannern, den Code schnell zu finden, und verbessert die Prüfgeschwindigkeit.

### 3. Dokumenten‑Zertifizierung
Zentrieren Sie einen QR‑Code am unteren Rand von Zertifikaten mit einer Verifizierungs‑URL und Zertifikats‑ID. Empfänger können scannen, um die Berechtigung zu bestätigen, und eine gedruckte URL wird ebenfalls für nicht‑mobile Nutzer bereitgestellt.

### 4. Internes Dokumenten‑Tracking
Während mehrstufiger Genehmigungen betten Sie nach jeder Unterschrift einen QR‑Code ein, der Genehmiger‑ID, Zeitstempel und Version enthält. Durch Scannen wird die vollständige Genehmigungshistorie angezeigt, was Compliance‑Audits erfüllt.

## Best Practices für die Produktion
### Ressourcen‑Management
Schließen Sie immer `Signature`‑Objekte, um Speicherlecks zu vermeiden:

``` 
```java
try (Signature signature = new Signature(filePath)) {
    // Your code
} // Auto‑closes
```
```

Erwägen Sie einen Verarbeitungs‑Pool für Web‑Apps, um gleichzeitige Vorgänge zu begrenzen.

### Fehler‑Handhabungs‑Strategie
Geben Sie umsetzbare Fehlermeldungen aus, anstatt stillschweigend zu fangen:

``` 
```java
try {
    SignResult result = signature.sign(outputFilePath, listOptions);
    if (result.getSucceeded().size() < listOptions.size()) {
        logger.warn("Only {} of {} signatures applied",
                    result.getSucceeded().size(),
                    listOptions.size());
    }
} catch (Exception e) {
    logger.error("Signature failed for document: {}", filePath, e);
    // Implement retry logic or alert mechanism
}
```
```

### Leistungs‑Optimierung
Für Hochdurchsatz‑Umgebungen:
1. **Batch‑Verarbeitung** – Dokumente parallel verarbeiten, aber die Parallelität basierend auf RAM begrenzen.  
2. **Caching** – identische `QrCodeSignOptions`‑Objekte über Dokumente hinweg wiederverwenden.  
3. **Asynchrone Vorgänge** – Signieren in Hintergrund‑Worker verlagern für reaktionsschnelle APIs.  
4. **Speicher‑Überwachung** – Alarme für Spitzen setzen und die Batch‑Größe entsprechend anpassen.

### Sicherheits‑Überlegungen
- Signierte Dokumente getrennt von den Originalen speichern.  
- Jede Signatur‑Operation für Auditrückverfolgung protokollieren.  
- Strenge Zugriffskontrollen für Signatur‑Endpunkte durchsetzen.  
- Sensible QR‑Payloads bei Bedarf verschlüsseln.

## Wann QR‑Code‑Signaturen verwenden (und wann nicht)
**Verwenden Sie QR‑Code‑Signaturen, wenn:**
- Mobile‑freundliche Verifizierung erforderlich ist.  
- Dokumente gedruckt und erneut gescannt werden können.  
- Sie Verifizierungs‑URLs oder IDs einbetten müssen.  
- Offline‑Verifizierungs‑Workflows Teil des Prozesses sind.  

**Vermeiden Sie QR‑Code‑Signaturen, wenn:**
- Eine rechtlich bindende PKI‑Signatur zwingend erforderlich ist (stattdessen kryptografische Signaturen verwenden).  
- QR‑Codes beim Drucken beschädigt oder verdeckt werden könnten.  
- Ihr Verifizierungssystem vollständig offline ist.  
- Die Dokumentgröße ein kritischer Faktor ist (QR‑Codes fügen ca. 5‑20 KB pro Stück hinzu).  

**Best Practice:** Kombinieren Sie eine kryptografische Signatur mit einem QR‑Code, um sowohl rechtliche Gültigkeit als auch schnelle mobile Verifizierung zu erhalten.

## Fehlersuch‑Leitfaden
### Signatur erscheint nicht
1. Überprüfen Sie, ob die Ausgabedatei tatsächlich erstellt wurde.  
2. Stellen Sie sicher, dass Sie die richtige Ausgabedatei öffnen.  
3. Prüfen Sie `SignResult` auf die Anzahl erfolgreicher Vorgänge.  
4. Stellen Sie sicher, dass Ausrichtungs‑ und Randwerte den QR‑Code nicht von der Seite schieben.  

### QR‑Code lässt sich nicht scannen
- QR‑Größe ≥ 100 × 100 px beibehalten.  
- Hoher Kontrast verwenden (dunkler Code auf hellem Hintergrund).  
- Kodierte Daten auf < 100 Zeichen beschränken für zuverlässiges Scannen.  
- Für physische Kopien bei ≥ 300 dpi drucken.  

### Leistungs‑Abnahme
- Anzahl der QR‑Codes pro Dokument reduzieren.  
- `Signature`‑Instanzen nach Möglichkeit wiederverwenden.  
- Speicherverbrauch profilieren; Verarbeitung in kleineren Batches erwägen.  

## Häufig gestellte Fragen
**Q:** *Kann ich Dokumente außer PDFs signieren?*  
**A:** Ja. GroupDocs.Signature unterstützt Word (DOC/DOCX), Excel (XLS/XLSX), PowerPoint (PPT/PPTX) und Bildformate (JPG, PNG, TIFF). Die API bleibt für alle unterstützten Typen konsistent.

**Q:** *Wie passe ich das Aussehen des QR‑Codes an?*  
**A:** Verwenden Sie `QrCodeSignOptions`‑Eigenschaften wie `setForeColor()`, `setBackgroundColor()` und `setBorder()`. Halten Sie Anpassungen einfach, um die Scanbarkeit zu erhalten.

**Q:** *Kann ich QR‑Codes zu bestimmten Seiten in einem mehrseitigen Dokument hinzufügen?*  
**A:** Absolut. Setzen Sie die Seitenzahl mit `options.setPageNumber(pageNumber);`. Beispiel:

``` 
```java
options.setPageNumber(1); // Add to first page only
```
```

**Q:** *Welche Daten kann ich im QR‑Code kodieren?*  
**A:** Beliebiger Text, URL, JSON oder XML – vorzugsweise unter 200 Zeichen für zuverlässiges Scannen. Für größere Payloads kodieren Sie eine kurze URL, die auf die vollständigen Daten auf einem Server verweist.

**Q:** *Wie verifiziere ich QR‑Code‑Signaturen programmgesteuert?*  
**A:** GroupDocs.Signature bietet eine `verify`‑Methode. Beispiel:

``` 
```java
VerificationResult result = signature.verify(verifyOptions);
if (result.isValid()) {
    // Signature is authentic
}
```
```

Die Klasse `Signature` ist der zentrale Einstiegspunkt zum Anwenden von Signaturen auf Dokumente.

**Q:** *Kann ich dies in einer multithreaded Umgebung verwenden?*  
**A:** Ja, aber erstellen Sie pro Thread ein separates `Signature`‑Objekt – Instanzen sind nicht thread‑sicher. Verwenden Sie eine Verarbeitungs‑Warteschlange für Szenarien mit hoher Parallelität.

**Q:** *Wie stark beeinflusst das Hinzufügen von QR‑Codes die Dateigröße?*  
**A:** Minimal – typischerweise 5‑20 KB pro QR‑Code, abhängig von Größe und Inhalt. Für die meisten PDFs ist das vernachlässigbar, aber bei der Signatur von tausenden Seiten in Batch‑Jobs sollte es berücksichtigt werden.

---

**Zuletzt aktualisiert:** 2026-05-21  
**Getestet mit:** GroupDocs.Signature 23.12 für Java  
**Autor:** GroupDocs  

## Ressourcen
- [GroupDocs.Signature für Java Releases](https://releases.groupdocs.com/signature/java/)  
- [temporäre Lizenz](https://purchase.groupdocs.com/temporary-license/)  
- [Lizenz kaufen](https://purchase.groupdocs.com/buy)  
- [GroupDocs Dokumentation](https://docs.groupdocs.com/signature/java/)  
- [GroupDocs.Signature Java Docs](https://docs.groupdocs.com/signature/java/)  
- [Vollständige API-Referenz](https://reference.groupdocs.com/signature/java/)  
- [Neueste Java-Version](https://releases.groupdocs.com/signature/java/)  
- [GroupDocs.Signature kaufen](https://purchase.groupdocs.com/buy)  
- [Kostenlose Testversion starten](https://releases.groupdocs.com/signature/java/)  
- [Temporäre Lizenz erhalten](https://purchase.groupdocs.com/temporary-license/)  
- [GroupDocs Forum](https://forum.groupdocs.com/c/signature/)  

## Verwandte Tutorials
- [Java QR-Code Signatur Bibliothek – Vollständiges GroupDocs Tutorial](/signature/java/qr-code-signatures/)  
- [QR-Code-Daten in Java extrahieren – Vollständiger Leitfaden mit GroupDocs](/signature/java/qr-code-signatures/detect-qr-code-mecard-signatures-groupdocs-java/)  
- [QR-Code aus PDF Java entfernen – Vollständiger Leitfaden mit GroupDocs](/signature/java/signature-management/delete-qr-code-signatures-groupdocs-java/)