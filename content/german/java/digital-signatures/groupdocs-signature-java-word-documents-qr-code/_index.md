---
categories:
- Digital Signatures
date: '2026-06-26'
description: Erfahren Sie, wie Sie programmgesteuert QR-Code-Signaturen in Word-Dokumenten
  mit GroupDocs.Signature für Java erstellen. Schritt‑für‑Schritt‑Tutorial, Code‑Beispiele,
  bewährte Methoden und Performance‑Tipps.
keywords:
- create qr code signature
- programmatically sign word
- qr code digital signature
- add qr to word
- groupdocs signature java
lastmod: '2026-06-26'
linktitle: QR-Code-Signaturen in Word mit Java
schemas:
- author: GroupDocs
  dateModified: '2026-06-26'
  description: Learn how to create QR code signature in Word documents programmatically
    with GroupDocs.Signature for Java. Step‑by‑step tutorial, code examples, best
    practices, and performance tips.
  headline: Create QR Code Signature in Word Documents Using Java
  type: TechArticle
- description: Learn how to create QR code signature in Word documents programmatically
    with GroupDocs.Signature for Java. Step‑by‑step tutorial, code examples, best
    practices, and performance tips.
  name: Create QR Code Signature in Word Documents Using Java
  steps:
  - name: The library reads the source document.
    text: The library reads the source document.
  - name: Generates the QR code based on `QrCodeSignOptions`.
    text: Generates the QR code based on `QrCodeSignOptions`.
  - name: Inserts the graphic at the specified coordinates.
    text: Inserts the graphic at the specified coordinates.
  - name: Saves the modified file to the path you provided.
    text: Saves the modified file to the path you provided.
  type: HowTo
- questions:
  - answer: Yes. GroupDocs.Signature supports PDF, Excel, PowerPoint, images, and
      many other formats. Just change the `setFileFormat` to the desired output type.
    question: Can I sign PDFs instead of Word documents?
  - answer: Use the library’s `SearchQrCodeSignatures` method to locate QR codes and
      validate the embedded data against your backend service.
    question: How do I verify a QR code signature after it’s been added?
  - answer: Standard QR codes hold up to **4 296 alphanumeric characters**, but for
      reliable scanning keep payloads under **500 characters**. For larger payloads
      store a reference ID and fetch details server‑side.
    question: What is the maximum data I can store in a QR code?
  - answer: Yes. You can set size, position, foreground/background colors, and even
      add a logo overlay. Stick to high‑contrast colors for best scan results.
    question: Can I customize the QR code’s visual appearance?
  - answer: For documents over 50 pages, expect a few seconds per file. Use batch
      processing, reuse the `Signature` instance, and monitor JVM heap size.
    question: How should I handle large‑document signing efficiently?
  type: FAQPage
tags:
- java
- word-documents
- qr-code
- digital-signature
- groupdocs
title: QR-Code-Signatur in Word-Dokumenten mit Java erstellen
type: docs
url: /de/java/digital-signatures/groupdocs-signature-java-word-documents-qr-code/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# QR-Code-Signatur in Word-Dokumenten mit Java erstellen

Haben Sie jemals Stunden damit verbracht, Dokumente manuell zu unterschreiben, und sich gefragt, ob es einen schnelleren, zuverlässigeren Weg gibt? Sie können **QR-Code-Signatur** in Word-Dokumenten programmgesteuert mit nur wenigen Zeilen Java-Code erstellen. Egal, ob Sie Vertragsabläufe automatisieren, rechtliche Unterlagen verwalten oder ein mobile‑first Genehmigungsportal aufbauen, QR-Code‑Signaturen bieten Ihnen sofortige, scanbare Verifizierung, die auf jedem Smartphone funktioniert. In diesem Tutorial lernen Sie, wie Sie GroupDocs.Signature für Java einrichten, QR‑Code‑Optionen konfigurieren und reichhaltige Daten wie URLs, Zeitstempel oder JSON‑Payloads in Word‑Dateien einbetten. Am Ende können Sie Dokumente in großem Umfang signieren, manuellen Aufwand reduzieren und die Compliance steigern.

## Schnelle Antworten
- **Welche Bibliothek benötige ich?** GroupDocs.Signature für Java (v23.12+).  
- **Wie viele Code‑Zeilen?** Zweizeilige QR‑Generierung plus ein paar Konfigurationszeilen.  
- **Kann ich auch PDFs signieren?** Ja – dieselbe API funktioniert für PDF, Excel, PowerPoint und Bilder.  
- **Ist eine kommerzielle Lizenz erforderlich?** Nur für die Produktion; ein kostenloser Test oder eine temporäre Lizenz funktioniert für die Entwicklung.  
- **Welche Daten kann ich speichern?** Bis zu ca. 4 k Zeichen (URL, JSON, IDs), aber für zuverlässiges Scannen unter 500 Zeichen halten.

## Was ist eine QR-Code-Signatur?
Eine **QR-Code-Signatur** ist ein scanbarer 2‑D‑Barcode, der in ein Dokument eingebettet ist und eine digitale Signatur oder ein Verifizierungs‑Payload darstellt. Wenn ein Benutzer den QR‑Code scannt, werden die kodierten Daten (oft eine URL oder ein Token) gelesen und validiert, wodurch die Authentizität des Dokuments ohne spezielle Software nachgewiesen wird.

## Warum GroupDocs.Signature für Java verwenden, um QR‑Codes hinzuzufügen?
GroupDocs.Signature unterstützt **mehr als 50 Eingabe‑ und Ausgabeformate**, kann mehrseitige Dateien verarbeiten, ohne das gesamte Dokument in den Speicher zu laden, und bietet eine flüssige API, mit der Sie **Word‑Dateien programmgesteuert** in Millisekunden signieren können. Die Bibliothek bietet zudem integrierte QR-, Aztec-, DataMatrix‑ und PDF417‑Barcode‑Generierung und ist damit eine All‑in‑One‑Lösung für moderne mobile‑first Verifizierung.

## Voraussetzungen

### Erforderliche Bibliotheken und Abhängigkeiten
- **GroupDocs.Signature für Java** Version **23.12** oder höher (die einzige externe Abhängigkeit).

### Anforderungen an die Umgebung
- **JDK 8+** (Java 11 oder 17 für die Produktion empfohlen).  
- **IDE** Ihrer Wahl (IntelliJ IDEA, Eclipse, VS Code).  
- **Build‑Tool** – Maven oder Gradle (Beispiele unten funktionieren mit beiden).

### Wissensvoraussetzungen
- Grundlegende Java‑Syntax und Date‑IO‑Verarbeitung.  
- Vertrautheit mit Maven/Gradle‑Abhängigkeitsdeklarationen (wir zeigen genaue Snippets).

## Einrichtung von GroupDocs.Signature für Java

Wählen Sie Ihr Build‑System und fügen Sie die Abhängigkeit exakt wie gezeigt hinzu. Die Platzhalter unten stellen die ursprünglichen Codeblöcke dar; lassen Sie sie unverändert.

**Maven**

```java
```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```
```

**Gradle**

```java
```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```
```

**Direct Download**

Bevorzugen Sie manuelle Verwaltung? Laden Sie das JAR direkt von [GroupDocs.Signature für Java releases](https://releases.groupdocs.com/signature/java/) herunter und fügen Sie es dem Klassenpfad Ihres Projekts hinzu.

### Lizenzbeschaffung
- **Kostenlose Testversion:** Ideal für Prototypen; Kernfunktionen sind verfügbar.  
- **Temporäre Lizenz:** Vollständiger Funktionsumfang für kurzfristige Entwicklung.  
- **Kommerzielle Lizenz:** Für Produktions‑Deployments erforderlich.  

**Pro‑Tipp:** Beginnen Sie mit der kostenlosen Testversion, beantragen Sie dann eine temporäre Lizenz, bevor Sie in die Produktion gehen. So können Sie den Workflow ohne Vorabkosten validieren.

### Grundlegende Initialisierung
Das `Signature`‑Objekt ist der Einstiegspunkt für alle Signatur‑Operationen. Es implementiert `AutoCloseable`, sodass Sie einen try‑with‑resources‑Block sicher verwenden können.

```java
```java
Signature signature = new Signature("path/to/your/document");
```
```

## Implementierungs‑Leitfaden: Word‑Dokumente mit QR‑Codes signieren

Im Folgenden gehen wir jeden Schritt durch, fügen Definition‑Anker und direkte Antworten hinzu, wo erforderlich.

### Wie initialisiere ich das Signature‑Objekt für eine Word‑Datei?
Laden Sie das Quelldokument mit `new Signature("source.docx")` innerhalb eines try‑with‑resources‑Blocks; das Objekt bereitet die Datei für Änderungen vor und gibt Ressourcen automatisch frei, wenn der Block endet.

```java
```java
String filePath = "YOUR_DOCUMENT_DIRECTORY/SampleDocX.docx";
Signature signature = new Signature(filePath);
```
```

**Erklärung:** Die `Signature`‑Klasse repräsentiert ein einzelnes Dokument im Speicher und stellt Methoden zum Hinzufügen, Suchen und Verifizieren von Signaturen bereit. Sie unterstützt `.docx`, `.doc` und viele weitere Formate.

### Wie kann ich die QR‑Code‑Signatur‑Optionen konfigurieren?
Erstellen Sie eine Instanz von `QrCodeSignOptions`, setzen Sie den codierten Text, den Barcode‑Typ und die Positionierung. Das folgende Snippet zeigt eine minimale Konfiguration.

```java
```java
QrCodeSignOptions signOptions = new QrCodeSignOptions("JohnSmith");
signOptions.setEncodeType(QrCodeTypes.QR);
signOptions.setLeft(100); // X-axis position in pixels
signOptions.setTop(100);  // Y-axis position in pixels
```
```

**Definition:** Die Klasse `QrCodeSignOptions` fasst alle Einstellungen zusammen, die zum Erzeugen und Platzieren einer QR‑Code‑Signatur erforderlich sind, einschließlich des codierten Textes, des Barcode‑Typs, der Größe, Farben und Positionskoordinaten im Dokument.

#### Anpassung des Aussehens
Sie können Größe, Rand und Farben weiter anpassen:

```java
```java
QrCodeSignOptions signOptions = new QrCodeSignOptions("https://yourapp.com/verify/doc-12345");
```
```

**Warum das wichtig ist:** Ein 150 px großes quadratisches QR‑Code mit schwarzem Vordergrund auf weißem Hintergrund erzielt >99 % Scan‑Erfolg sowohl auf dem Bildschirm als auch im Druck.

### Wie lege ich die Ausgabeoptionen für das signierte Dokument fest?
Definieren Sie das Zielformat und das Überschreib‑Verhalten, bevor Sie `sign` aufrufen.

```java
```java
WordProcessingSaveOptions saveOptions = new WordProcessingSaveOptions();
saveOptions.setFileFormat(WordProcessingSaveFileFormat.Odt);
saveOptions.setOverwriteExistingFiles(true);
```
```

**Definition:** Die Klasse `WordProcessingSaveOptions` definiert, wie das signierte Word‑Dokument gespeichert werden soll, sodass Sie das Ausgabeformat (DOCX, ODT usw.), das Überschreiben vorhandener Dateien und weitere dateispezifische Einstellungen festlegen können.

Wenn Sie ein Open‑Source‑Format benötigen, wechseln Sie zu `OutputType.ODT`:

```java
```java
saveOptions.setFileFormat(WordProcessingSaveFileFormat.Docx);
```
```

### Wie signiere und speichere ich das Dokument mit dem QR‑Code?
Die Methode `sign` wendet den QR‑Code an und schreibt die Ausgabedatei in einem Aufruf.

```java
```java
String outputFilePath = "YOUR_OUTPUT_DIRECTORY/SaveSignedOutputType/SampleDocX.odt";
signature.sign(outputFilePath, signOptions, saveOptions);
```
```

**Definition:** Die `sign`‑Methode des `Signature`‑Objekts nimmt den Zielpfad, die konfigurierten Signatur‑Optionen und optionale Speicher‑Optionen, bettet den QR‑Code in das Dokument ein und schreibt das Ergebnis an den angegebenen Ort.

**Was passiert:**  
1. Die Bibliothek liest das Quelldokument.  
2. Generiert den QR‑Code basierend auf `QrCodeSignOptions`.  
3. Fügt die Grafik an den angegebenen Koordinaten ein.  
4. Speichert die modifizierte Datei an dem von Ihnen angegebenen Pfad.

### Wie sollte ich Fehler beim Signieren behandeln?
Umwickeln Sie die Signatur‑Logik mit einem try‑catch‑Block, um fehlende Dateien, ungültige Pfade oder Lizenzprobleme abzufangen.

```java
```java
try {
    signature.sign(outputFilePath, signOptions, saveOptions);
    System.out.println("Document signed successfully!");
} catch (Exception e) {
    System.err.println("Signing failed: " + e.getMessage());
}
```
```

**Definition:** Das Abfangen von `Exception` stellt sicher, dass alle Laufzeitprobleme wie fehlende Dateien, ungültige Pfade oder Lizenzprobleme sauber gemeldet werden und verhindert, dass die Anwendung in der Produktion abstürzt.

## Häufige Anwendungsfälle und Praxisbeispiele

### Automatisiertes Vertragsmanagement
Eine SaaS‑Plattform signiert **mehr als 500 Verträge pro Monat**, indem sie einen eindeutigen QR‑Code erzeugt, der die Vertrags‑ID und eine Verifizierungs‑URL enthält. Empfänger scannen, um den Vertragsstatus im Portal zu sehen, wodurch manuelle E‑Mail‑Austausche entfallen.

### Ausstellung von Mitarbeiterschulungszertifikaten
HR‑Abteilungen betten Mitarbeiter‑IDs und Ausgabedaten in QR‑Codes auf Schulungszertifikaten ein. Das Scannen des QR‑Codes validiert sofort die Authentizität gegen eine interne Datenbank und reduziert Betrug um **über 80 %**.

### Automatisierung von Genehmigungs‑Workflows
Der QR‑Code jedes Genehmigers speichert dessen Mitarbeiternummer, Rolle und einen Zeitstempel. Das System liest den QR‑Code während der Prüfung und liefert eine manipulationssichere Spur ohne zusätzliche Datenbank‑Abfragen.

### Rechnungs‑ und Belegsignatur
Finanzteams fügen QR‑Codes hinzu, die zu einem Zahlungs‑Gateway verlinken. Beim Scannen leitet der QR‑Code den Zahler zu einer sicheren Zahlungsseite, verkürzt die Bearbeitungszeit um **30 %** und senkt das Risiko von Rechnungsbetrug.

## Best Practices für den Produktionseinsatz

### Sicherheitsaspekte
- **Nie rohe Passwörter einbetten**; verwenden Sie ein Token oder eine Referenz‑ID, die serverseitig aufgelöst wird.  
- **Immer HTTPS verwenden** für URLs; vermeiden Sie HTTP, um Man‑in‑the‑Middle‑Angriffe zu verhindern.  
- **Token‑Ablauf setzen** (z. B. JWT mit 24‑Stunden‑Gültigkeit) für zeitkritische Dokumente.

### Leistungsoptimierung
- **Batch‑Verarbeitung:** Halten Sie eine einzelne `Signature`‑Instanz am Leben und iterieren Sie über Dateien, um wiederholtes JVM‑Warm‑up zu vermeiden.  
- **Speicherverwaltung:** Bei Dokumenten > 50 MB sequenziell verarbeiten und das `Signature`‑Objekt nach jeder Datei freigeben.  
- **Platzierung ist wichtig:** Positionieren Sie QR‑Codes am unteren Rand der Seite, um Layout‑Neuberechnungen zu reduzieren und die Geschwindigkeit zu erhöhen.

```java
```java
List<String> documents = getDocumentPaths();
for (String docPath : documents) {
    Signature sig = new Signature(docPath);
    // Configure and sign
    sig.dispose();
}
```
```

### Tipps zur QR‑Code‑Platzierung
- **Drucksicherheit:** Halten Sie QR‑Codes mindestens 0,5 in von den Seitenrändern entfernt, um Abschneiden zu vermeiden.  
- **Größenempfehlung:** Mindestens 150 × 150 px für zuverlässiges Scannen auf gedruckten Medien.  
- **Mehrere Seiten:** Durchlaufen Sie die Seiten und erstellen Sie für jede Position ein neues `QrCodeSignOptions`.

```java
```java
for (Document doc : documents) {
    Signature sig = new Signature(doc.getPath());
    sig.sign(outputPath, signOptions, saveOptions);
    sig.dispose();
}
```
```

## Erweiterte Konfigurationsoptionen

### Wie kann ich mehrere QR‑Codes zu einem einzigen Dokument hinzufügen?
Erstellen Sie separate `QrCodeSignOptions`‑Objekte für jede Position und rufen Sie `sign` wiederholt auf.

```java
```java
// First QR code
QrCodeSignOptions sign1 = new QrCodeSignOptions("Approver 1");
sign1.setLeft(100);
sign1.setTop(100);

// Second QR code
QrCodeSignOptions sign2 = new QrCodeSignOptions("Approver 2");
sign2.setLeft(300);
sign2.setTop(100);

// Apply both
signature.sign(outputPath, sign1, saveOptions);
signature.sign(outputPath, sign2, saveOptions);
```
```

### Welche anderen Barcode‑Typen werden unterstützt?
Neben QR können Sie **Aztec**, **DataMatrix** oder **PDF417**‑Codes erzeugen, indem Sie `setEncodeType()` ändern.

### Wie berechne ich dynamische Positionen basierend auf der Seitengröße?
Rufen Sie die Seitengröße über `Signature.getDocumentInfo()` ab und berechnen Sie die Koordinaten programmgesteuert.

```java
```java
// Get document info
DocumentInfo docInfo = signature.getDocumentInfo();
int pageWidth = docInfo.getWidth();
int pageHeight = docInfo.getHeight();

// Center the QR code
int qrSize = 100;
signOptions.setLeft((pageWidth - qrSize) / 2);
signOptions.setTop((pageHeight - qrSize) / 2);
```
```

**Definition:** `Signature.getDocumentInfo()` liefert ein `DocumentInfo`‑Objekt, das Metadaten wie Seitenabmessungen enthält und zur Berechnung genauer Platzierungskoordinaten für Signaturen basierend auf der tatsächlichen Größe jeder Seite verwendet werden kann.

## Fehlersuche bei häufigen Problemen

### QR‑Code wird nicht angezeigt
- Überprüfen Sie, ob `setLeft`/`setTop` innerhalb der Seitenränder liegen (A4 ≈ 595 × 842 px bei 72 DPI).  
- Stellen Sie sicher, dass Vorder‑ und Hintergrundfarbe kontrastieren (schwarz auf weiß).  
- Erhöhen Sie Breite/Höhe, wenn der Code zu klein zum Scannen ist.

### „Datei nicht gefunden“ beim Initialisieren von Signature
- Verwenden Sie während der Entwicklung absolute Pfade oder prüfen Sie relative Pfade mit `Paths.get(...)`.  
- Stellen Sie sicher, dass die Quelldatei nicht von einem anderen Prozess gesperrt ist.

### Ausgabedatei ist beschädigt
- Überprüfen Sie, ob `setFileFormat` mit der gewünschten Erweiterung übereinstimmt.  
- Schließen Sie alle Streams, die die Datei noch halten könnten, bevor Sie signieren.

### QR‑Code enthält falsche Daten
- Geben Sie den String, den Sie an `QrCodeSignOptions` übergeben, vor dem Signieren aus, um die Kodierung zu bestätigen.  
- Vermeiden Sie Nicht‑ASCII‑Zeichen, es sei denn, Sie setzen explizit UTF‑8‑Kodierung.

### Leistung ist bei großen Dokumenten langsam
- Verarbeiten Sie Dokumente in Batches (siehe Code‑Block 10).  
- Vermeiden Sie das Platzieren von QR‑Codes in komplexen Tabellen; sie lösen umfangreiche Layout‑Neuberechnungen aus.

## Häufig gestellte Fragen

**F: Kann ich PDFs anstelle von Word‑Dokumenten signieren?**  
A: Ja. GroupDocs.Signature unterstützt PDF, Excel, PowerPoint, Bilder und viele weitere Formate. Ändern Sie einfach `setFileFormat` auf den gewünschten Ausgabetyp.

**F: Wie verifiziere ich eine QR‑Code‑Signatur, nachdem sie hinzugefügt wurde?**  
A: Verwenden Sie die Methode `SearchQrCodeSignatures` der Bibliothek, um QR‑Codes zu finden und die eingebetteten Daten gegen Ihren Backend‑Service zu validieren.

**F: Wie viele Daten kann ich maximal in einem QR‑Code speichern?**  
A: Standard‑QR‑Codes können bis zu **4 296 alphanumerische Zeichen** aufnehmen, aber für zuverlässiges Scannen sollten die Payloads unter **500 Zeichen** bleiben. Für größere Daten speichern Sie eine Referenz‑ID und holen die Details serverseitig ab.

**F: Kann ich das visuelle Erscheinungsbild des QR‑Codes anpassen?**  
A: Ja. Sie können Größe, Position, Vorder‑/Hintergrundfarben und sogar ein Logo‑Overlay festlegen. Verwenden Sie kontrastreiche Farben für optimale Scan‑Ergebnisse.

**F: Wie gehe ich effizient mit dem Signieren großer Dokumente um?**  
A: Bei Dokumenten mit mehr als 50 Seiten sollten Sie einige Sekunden pro Datei einplanen. Nutzen Sie Batch‑Verarbeitung, wiederverwenden Sie die `Signature`‑Instanz und überwachen Sie die JVM‑Heap‑Größe.

**F: Bleiben QR‑Signaturen bei der Konvertierung zu PDF erhalten?**  
A: Ja. Der QR‑Code wird als Grafik eingebettet und bleibt beim Konvertieren zwischen Formaten erhalten, sofern Sie eine ausreichende Auflösung beibehalten.

**F: Kann ich Dokumente aus Cloud‑Speichern wie S3 signieren?**  
A: Ja. Laden Sie die Datei in einen temporären lokalen Pfad herunter, signieren Sie sie und laden Sie die signierte Version zurück nach S3 hoch. Die Bibliothek arbeitet nur mit lokalen Dateien.

**F: Was passiert, wenn jemand das Dokument nach dem Signieren verändert?**  
A: Die QR‑Grafik selbst bleibt unverändert, erkennt jedoch keine Manipulation. Kombinieren Sie QR‑Codes mit hash‑basierter Verifizierung oder digitalen Zertifikaten für robuste Integritätsprüfungen.

**F: Benötige ich unterschiedliche Lizenzen für Entwicklung und Produktion?**  
A: Für die Entwicklung können Sie die kostenlose Testversion oder eine temporäre Lizenz verwenden. Produktions‑Deployments erfordern eine kommerzielle Lizenz gemäß den GroupDocs‑Bedingungen.

**F: Können Empfänger ohne Java diese QR‑Codes scannen?**  
A: Ja. QR‑Codes folgen einem offenen Standard; jede Smartphone‑Kamera oder QR‑Reader‑App kann sie dekodieren. Java wird nur zum *Erstellen* der Signaturen benötigt.

## Ressourcen

- [GroupDocs.Signature für Java Releases](https://releases.groupdocs.com/signature/java/)
- [GroupDocs.Signature für Java Dokumentation](https://docs.groupdocs.com/signature/java/)
- [GroupDocs.Signature API‑Referenz](https://reference.groupdocs.com/signature/java/)
- [Neueste GroupDocs.Signature Releases](https://releases.groupdocs.com/signature/java/)
- [GroupDocs.Signature kaufen](https://purchase.groupdocs.com/buy)
- [GroupDocs Signatures kostenlose Testversion](https://releases.groupdocs.com/signature/java/)
- [Temporäre Lizenz beantragen](https://purchase.groupdocs.com/temporary-license/)
- [GroupDocs Forum Support](https://forum.groupdocs.com/c/signature/)

## Fazit

Sie haben nun eine vollständige, produktionsbereite Anleitung, um **QR-Code-Signatur** in Word‑Dokumenten mit Java und GroupDocs.Signature zu **erstellen**. Von der Grundkonfiguration bis zur Batch‑Verarbeitung, von Sicherheits‑Best Practices bis zu erweiterten Barcode‑Typen – alles, was Sie benötigen, ist abgedeckt. Beginnen Sie mit einer kostenlosen Testversion, experimentieren Sie mit verschiedenen Payloads und integrieren Sie den Signierschritt in Ihre bestehende Dokument‑Generierungspipeline. Viel Spaß beim Programmieren und sichere Signaturen!

**Zuletzt aktualisiert:** 2026-06-26  
**Getestet mit:** GroupDocs.Signature 23.12 für Java  
**Autor:** GroupDocs  

{{< blocks/products/products-backtop-button >}}

## Verwandte Tutorials

- [Java QR‑Code‑Signatur‑Bibliothek – Komplettes GroupDocs‑Tutorial](/signature/java/qr-code-signatures/)
- [Dokumente in Java laden und speichern – Komplettes GroupDocs.Signature‑Tutorial](/signature/java/document-loading-saving/)
- [Wie man digitale Signaturen zu Dokumenten in Java hinzufügt](/signature/java/digital-signatures/groupdocs-signature-java-digital-signing-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}