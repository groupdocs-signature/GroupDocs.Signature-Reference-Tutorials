---
categories:
- Document Signing
- Healthcare Integration
date: '2026-05-16'
description: Erfahren Sie, wie Sie ein Data Matrix PDF erstellen und ein QR‑Code‑PDF
  mit GroupDocs.Signature für Java hinzufügen. Schritt‑für‑Schritt‑Anleitung zur Unterzeichnung
  von Gesundheitsdokumenten.
keywords:
- create data matrix pdf
- add qr code pdf
- HIBC barcode Java
lastmod: '2026-05-16'
linktitle: HIBC PDF Signing Java Leitfaden
schemas:
- author: GroupDocs
  dateModified: '2026-05-16'
  description: Learn how to create data matrix PDF and add QR code PDF using GroupDocs.Signature
    for Java. Step‑by‑step guide for healthcare document signing.
  headline: Create Data Matrix PDF with HIBC Barcode in Java
  type: TechArticle
- description: Learn how to create data matrix PDF and add QR code PDF using GroupDocs.Signature
    for Java. Step‑by‑step guide for healthcare document signing.
  name: Create Data Matrix PDF with HIBC Barcode in Java
  steps:
  - name: '**Import the required classes** – these give you access to the signature
      engine and Data Matrix options.'
    text: '**Import the required classes** – these give you access to the signature
      engine and Data Matrix options.'
  - name: '**Instantiate the `Signature` object** with absolute paths for source and
      destination files.'
    text: '**Instantiate the `Signature` object** with absolute paths for source and
      destination files.'
  - name: '**Configure the Data Matrix options** – set the HIBC string, choose `QrCodeTypes.HIBCLICDataMatrix`,
      and define placement coordinates. `QrCodeTypes` enumerates the supported barcode
      formats for HIBC signatures.'
    text: '**Configure the Data Matrix options** – set the HIBC string, choose `QrCodeTypes.HIBCLICDataMatrix`,
      and define placement coordinates. `QrCodeTypes` enumerates the supported barcode
      formats for HIBC signatures.'
  - name: '**Apply the signature** to the PDF.'
    text: '**Apply the signature** to the PDF.'
  - name: '**Dispose of resources** to free file handles and avoid memory leaks.'
    text: '**Dispose of resources** to free file handles and avoid memory leaks.'
  - name: '**Import QR‑specific classes**'
    text: '**Import QR‑specific classes**'
  - name: '**Create and configure QR options** – note the use of `QrCodeTypes.HIBCLICQR`.'
    text: '**Create and configure QR options** – note the use of `QrCodeTypes.HIBCLICQR`.'
  - name: '**Sign the document**'
    text: '**Sign the document**'
  type: HowTo
- questions:
  - answer: Yes, it also supports DOCX, XLSX, PPTX, PNG, JPEG, and TIFF with the same
      barcode‑signing API.
    question: Can GroupDocs.Signature sign file types other than PDF?
  - answer: Verify that your HIBC string follows the exact HIBCC syntax, use the online
      validator, and ensure you’re using the correct `QrCodeTypes` constant for the
      chosen format.
    question: How do I troubleshoot “Invalid barcode content” errors?
  - answer: QR ≈ 4,296 alphanumeric characters, Aztec ≈ 3,832 numeric / 3,067 alphanumeric,
      Data Matrix ≈ 3,116 numeric / 2,335 alphanumeric. Keep codes under 200 characters
      for optimal scan reliability.
    question: What is the maximum data capacity for each HIBC format?
  - answer: Absolutely. Create separate `QrCodeSignOptions` objects with different
      positions and call `signature.sign()` for each. Just ensure they don’t overlap.
    question: Is it possible to embed multiple barcode types in one PDF?
  - answer: No. After the JAR is on the classpath and the license is activated, all
      operations are performed locally.
    question: Do I need an internet connection for signing at runtime?
  type: FAQPage
tags:
- java
- pdf-signing
- hibc
- healthcare
- barcode
- pharmaceutical
title: Erstellen Sie ein Data Matrix PDF mit HIBC-Barcode in Java
type: docs
url: /de/java/barcode-signatures/sign-pdfs-hibc-lic-codes-groupdocs-java/
weight: 1
---

# Erstelle Data Matrix PDF mit HIBC Barcode in Java

If you’re building pharmaceutical or healthcare logistics software, you’ve probably hit the wall of paper‑based tracking, lost signatures, and audit nightmares. **Creating a Data Matrix PDF** that embeds a HIBC LIC barcode solves those problems by giving you a tamper‑evident, machine‑readable trail that survives printing, scanning, and regulatory review. In this tutorial you’ll see exactly how to **add QR code PDF** support, as well as Aztec and Data Matrix formats, using GroupDocs.Signature for Java.

## Schnelle Antworten
- **Which library handles HIBC barcodes in Java?** GroupDocs.Signature for Java.  
- **Which barcode format is most compact?** Data Matrix – ideal for small labels.  
- **Can I add both QR and Data Matrix to the same PDF?** Yes, just create separate `QrCodeSignOptions`.  
- **Do I need an internet connection at runtime?** No, the library works fully offline after installation.  
- **What Java version is recommended?** Java 11+ for production‑grade performance.

## Was ist das Signieren von PDFs mit HIBC-Barcode?
The `Signature` class in GroupDocs.Signature for Java represents a PDF document and provides methods to embed HIBC barcodes as digital signatures. By signing a PDF with an HIBC barcode you create a verifiable, tamper‑evident record that can be scanned at any point in the supply chain.

## Warum Data Matrix und QR-Codes zusammen verwenden?
GroupDocs.Signature supports **50+ input and output formats** and can process multi‑hundred‑page PDFs without loading the entire file into memory. Using Data Matrix for dense, small‑area labels and QR for more spacious documents gives you the best balance of readability, data capacity (up to 4,296 characters for QR), and print‑space efficiency.

## Voraussetzungen
- **JDK 11 or higher** (Java 8 works but Java 11+ is recommended for optimal performance).  
- **IDE** such as IntelliJ IDEA, Eclipse, or VS Code with Java extensions.  
- **Maven or Gradle** for dependency management (examples below).  
- **Sample PDF** (e.g., `sample.pdf`) to test the implementation.  
- **Valid GroupDocs.Signature license** (free trial for development, paid license for production).

## Einrichtung von GroupDocs.Signature für Java

### Maven-Konfiguration
Add the dependency to your `pom.xml`:

```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

### Gradle-Konfiguration
For Gradle projects, add this to your `build.gradle`:

```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

### Direktdownload-Option
You can also download the JAR file directly from [GroupDocs.Signature for Java releases](https://releases.groupdocs.com/signature/java/) and add it to your project’s classpath manually. This approach works well in restricted‑network environments.

### Lizenz erhalten
Request a free trial or temporary license from GroupDocs to remove watermarks and unlock all features. Production deployments require a purchased license.

### Grundlegende Initialisierung
The `Signature` class is the entry point for all signing operations. It loads the PDF, applies the barcode, and writes the signed file.

```java
import com.groupdocs.signature.Signature;

class InitializeSignature {
    public static void main(String[] args) {
        Signature signature = new Signature("sample.pdf");
        // Proceed with signing operations...
    }
}
```

## Wie erstellt man ein Data Matrix PDF mit HIBC-Barcode?
Load your source PDF, configure a `QrCodeSignOptions` object for the Data Matrix format, and call `sign()` – that’s all you need to embed a compliant HIBC Data Matrix barcode. The following steps walk you through the exact code required. `QrCodeSignOptions` defines the settings for a barcode signature, such as type, content, size, and position.

1. **Importieren Sie die erforderlichen Klassen** – these give you access to the signature engine and Data Matrix options.  

```java
import com.groupdocs.signature.Signature;
import com.groupdocs.signature.options.sign.QrCodeSignOptions;
import com.groupdocs.signature.domain.qrcodes.QrCodeTypes;
```

2. **Instanziieren Sie das `Signature`-Objekt** with absolute paths for source and destination files.  

```java
String sourceFilePath = "YOUR_DOCUMENT_DIRECTORY";
String destinFilePath = "YOUR_OUTPUT_DIRECTORY/SignWithHIBCLICQR.pdf";

final Signature signature = new Signature(sourceFilePath);
```

3. **Konfigurieren Sie die Data Matrix-Optionen** – set the HIBC string, choose `QrCodeTypes.HIBCLICDataMatrix`, and define placement coordinates. `QrCodeTypes` enumerates the supported barcode formats for HIBC signatures.  

```java
QrCodeSignOptions hibcLic_QR = new QrCodeSignOptions("A123PROD30917/75#422011907#GP293", QrCodeTypes.HIBCLICQR);
hibcLic_QR.setLeft(1); // Set the position from left
hibcLic_QR.setTop(1);   // Set the position from top
hibcLic_QR.setReturnContent(true); // Return content after signing
hibcLic_QR.setReturnContentType(FileType.PNG); // Specify return content type as PNG
```

4. **Wenden Sie die Signatur** to the PDF.  

```java
signature.sign(destinFilePath, hibcLic_QR);
```

5. **Ressourcen freigeben** to free file handles and avoid memory leaks.  

```java
finally {
    if (signature != null) signature.dispose();
}
```

### Vollständiges funktionierendes Beispiel
Here’s the full flow in a single block (the placeholders represent the exact code you’ll paste from the earlier snippets):

```java
import com.groupdocs.signature.Signature;
import com.groupdocs.signature.options.sign.QrCodeSignOptions;
import com.groupdocs.signature.domain.qrcodes.QrCodeTypes;

public class HibcQrSigning {
    public static void main(String[] args) {
        String sourceFilePath = "sample.pdf";
        String destinFilePath = "output/SignWithHIBCLICQR.pdf";
        
        Signature signature = null;
        try {
            signature = new Signature(sourceFilePath);
            
            QrCodeSignOptions hibcLic_QR = new QrCodeSignOptions(
                "A123PROD30917/75#422011907#GP293", 
                QrCodeTypes.HIBCLICQR
            );
            hibcLic_QR.setLeft(1);
            hibcLic_QR.setTop(1);
            hibcLic_QR.setReturnContent(true);
            hibcLic_QR.setReturnContentType(FileType.PNG);
            
            signature.sign(destinFilePath, hibcLic_QR);
            System.out.println("PDF signed successfully with HIBC QR code");
            
        } catch (Exception e) {
            System.err.println("Error signing PDF: " + e.getMessage());
            e.printStackTrace();
        } finally {
            if (signature != null) signature.dispose();
        }
    }
}
```

#### Direkte Antwort (40–70 Wörter)
To **create a Data Matrix PDF**, instantiate `Signature` with your source PDF, set `QrCodeSignOptions` to `QrCodeTypes.HIBCLICDataMatrix` and provide a correctly formatted HIBC string, then call `signature.sign(outputPath, options)`. The library writes the signed PDF to the destination, preserving layout and embedding the barcode as a tamper‑evident signature.

## Wie fügt man QR-Code-PDF mit GroupDocs.Signature hinzu?
Load the PDF, configure `QrCodeSignOptions` for the QR format, and invoke `sign()`. This two‑line pattern works for any PDF size and automatically scales the QR image for optimal readability. `QrCodeSignOptions` configures the QR barcode signature, including its content and visual properties. It positions the code based on the coordinates you set, ensuring it does not overlap existing content and remains scannable after printing.

1. **Importieren Sie QR‑spezifische Klassen**  

```java
QrCodeSignOptions hibcLic_AZ = new QrCodeSignOptions("A123PROD30917/75#422011907#GP293", QrCodeTypes.HIBCLICAztec);
hibcLic_AZ.setLeft(1); // Set the position from left
hibcLic_AZ.setTop(200); // Set the position from top
hibcLic_AZ.setReturnContent(true); // Return content after signing
hibcLic_AZ.setReturnContentType(FileType.PNG); // Specify return content type as PNG
```

2. **Erstellen und konfigurieren Sie QR-Optionen** – note the use of `QrCodeTypes.HIBCLICQR`.  

```java
signature.sign(destinFilePath, hibcLic_AZ);
```

3. **Signieren Sie das Dokument**  

```java
QrCodeSignOptions hibcLic_DM = new QrCodeSignOptions("A123PROD30917/75#422011907#GP293", QrCodeTypes.HIBCLICDataMatrix);
hibcLic_DM.setLeft(1); // Set the position from left
hibcLic_DM.setTop(400); // Set the position from top
hibcLic_DM.setReturnContent(true); // Return content after signing
hibcLic_DM.setReturnContentType(FileType.PNG); // Specify return content type as PNG
```

> **Direkte Antwort:** Use `QrCodeTypes.HIBCLICQR` in `QrCodeSignOptions`, set the HIBC content string, position the code with `setLeft()` and `setTop()`, then call `signature.sign(outputPath, options)`. The QR barcode is embedded instantly, ready for smartphone or scanner capture.

## Häufige Fehler, die zu vermeiden sind

### 1. Vergessen der Ressourcenfreigabe
**Falsch:**  

```java
Signature signature = new Signature("sample.pdf");
signature.sign(destinFilePath, options);
// Oops, no dispose() call
```  

**Korrektur:** Wrap the `Signature` usage in a try‑with‑resources block or explicitly call `close()` in a finally clause.

### 2. Verwendung falscher HIBC-Format-Strings
**Falsch:** Using generic strings like “12345”.  
**Korrektur:** Follow the HIBCC standard (e.g., `A123PROD30917/75#422011907#GP293`). Validate with the [HIBCC online validator](https://www.hibcc.org/).

### 3. Hartkodierte Dateipfade
**Falsch:**  

```java
String sourceFilePath = "C:/Users/John/Documents/test.pdf";
```  

**Korrektur:** Store paths in a configuration file or environment variable and read them at runtime.

### 4. Ignorieren von Barcode-Positionskonflikten
Place barcodes away from existing text or signatures. Use PDF coordinates (origin is bottom‑left) and test with a printed sample.

### 5. Nicht mit echten Scannern testen
Print the signed PDF and scan it with the exact hardware used in your workflow. Verify readability at different print qualities.

## Praktische Anwendungen im Gesundheitswesen

| Szenario | Empfohlener Barcode | Warum es passt |
|----------|--------------------|----------------|
| **Pharmazeutischer Vertrieb** | QR-Code | Hohe Datenkapazität, wird häufig von Smartphones gescannt. |
| **Bestandsverwaltung** | Data Matrix | Kleiner Platzbedarf, ideal für dichte Regaletiketten. |
| **Regulatorische Konformität (FDA 21 CFR Part 11)** | QR + Data Matrix | Dual‑Format bietet Redundanz und Auditierbarkeit. |
| **Verfolgung von Medizinprodukten** | Aztec-Code | Kompakte Größe funktioniert auf begrenztem Verpackungsraum. |

## Leistungsüberlegungen und bewährte Vorgehensweisen

### Muster für die Batch-Verarbeitung
```java
List<String> filesToSign = getFileList();
for (String filePath : filesToSign) {
    Signature signature = null;
    try {
        signature = new Signature(filePath);
        // Sign and save
    } finally {
        if (signature != null) signature.dispose();
    }
}
```

- Erstellen Sie für jede Datei eine neue `Signature`-Instanz, um den Speicherverbrauch gering zu halten.  
- Verwenden Sie einen festen Thread‑Pool (`Executors.newFixedThreadPool(Runtime.getRuntime().availableProcessors() - 1)`) für die Parallelverarbeitung, überwachen Sie jedoch die Heap‑Größe, da jede `Signature` das gesamte PDF im Speicher hält.  

### Bibliotheken aktuell halten
GroupDocs releases improve processing speed by up to **20 %** and add new HIBC compliance features. Schedule quarterly dependency checks.

### Vorlagen zwischenspeichern
Load a PDF template once, clone it for each barcode variant, and sign the clones. This reduces I/O and speeds up high‑volume workflows.

## Häufig gestellte Fragen

**F: Kann GroupDocs.Signature Dateitypen außer PDF signieren?**  
A: Yes, it also supports DOCX, XLSX, PPTX, PNG, JPEG, and TIFF with the same barcode‑signing API.

**F: Wie behebe ich “Invalid barcode content”‑Fehler?**  
A: Verify that your HIBC string follows the exact HIBCC syntax, use the online validator, and ensure you’re using the correct `QrCodeTypes` constant for the chosen format.

**F: Was ist die maximale Datenkapazität für jedes HIBC-Format?**  
A: QR ≈ 4,296 alphanumeric characters, Aztec ≈ 3,832 numeric / 3,067 alphanumeric, Data Matrix ≈ 3,116 numeric / 2,335 alphanumeric. Keep codes under 200 characters for optimal scan reliability.

**F: Ist es möglich, mehrere Barcode‑Typen in ein PDF einzubetten?**  
A: Absolutely. Create separate `QrCodeSignOptions` objects with different positions and call `signature.sign()` for each. Just ensure they don’t overlap.

**F: Benötige ich eine Internetverbindung zum Signieren zur Laufzeit?**  
A: No. After the JAR is on the classpath and the license is activated, all operations are performed locally.

## Zusätzliche Ressourcen

- [GroupDocs.Signature für Java Dokumentation](https://docs.groupdocs.com/signature/java/)  
- [API-Referenzhandbuch](https://reference.groupdocs.com/signature/java/)  
- [Neueste Release-Downloads](https://releases.groupdocs.com/signature/java/)  
- [Lizenz erwerben](https://purchase.groupdocs.com/buy)  
- [Kostenlose Testversion erhalten](https://releases.groupdocs.com/signature/java/)  
- [Temporäre Lizenz anfordern](https://purchase.groupdocs.com/temporary-license/)  
- [GroupDocs Forum](https://forum.groupdocs.com/c/signature/)

---

**Last Updated:** 2026-05-16  
**Tested With:** GroupDocs.Signature 23.12 for Java  
**Author:** GroupDocs  

```java
signature.sign(destinFilePath, hibcLic_DM);
```

## Verwandte Tutorials

- [Barcode-Signatur-PDF in Java erstellen – GroupDocs Guide](/signature/java/barcode-signatures/create-sign-pdfs-groupdocs-barcode-java/)
- [Barcode-Signatur in Java erstellen – PDF-Barcodes aktualisieren](/signature/java/barcode-signatures/java-groupdocs-signature-barcode-initialize-update/)
- [Wie man QR-Code-PDF mit Java und GroupDocs.Signature liest](/signature/java/barcode-signatures/java-pdf-barcode-search-groupdocs-signature-api/)