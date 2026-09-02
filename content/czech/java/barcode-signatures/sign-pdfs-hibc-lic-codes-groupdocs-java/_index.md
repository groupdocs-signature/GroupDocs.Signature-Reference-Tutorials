---
categories:
- Document Signing
- Healthcare Integration
date: '2026-05-16'
description: Naučte se, jak vytvořit data matrix PDF a přidat QR code PDF pomocí GroupDocs.Signature
  pro Java. Podrobný návod krok za krokem pro podepisování zdravotnických dokumentů.
keywords:
- create data matrix pdf
- add qr code pdf
- HIBC barcode Java
lastmod: '2026-05-16'
linktitle: Průvodce podepisováním HIBC PDF v Javě
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
title: Vytvořte Data Matrix PDF s HIBC Barcode v Javě
type: docs
url: /cs/java/barcode-signatures/sign-pdfs-hibc-lic-codes-groupdocs-java/
weight: 1
---

# Vytvoření PDF s Data Matrix a čárovým kódem HIBC v Javě

Pokud vyvíjíte software pro farmaceutickou nebo zdravotnickou logistiku, pravděpodobně jste narazili na problémy s papírovým sledováním, ztracenými podpisy a nočními můrami auditů. **Vytvoření PDF s Data Matrix** obsahujícího čárový kód HIBC LIC řeší tyto problémy tím, že vám poskytne zjevně manipulovatelnou, strojově čitelnou stopu, která přežije tisk, skenování i regulatorní kontrolu. V tomto tutoriálu uvidíte přesně, jak **přidat podporu QR kódu do PDF**, stejně jako formáty Aztec a Data Matrix, pomocí GroupDocs.Signature pro Javu.

## Rychlé odpovědi
- **Která knihovna zpracovává HIBC čárové kódy v Javě?** GroupDocs.Signature for Java.  
- **Který formát čárového kódu je nejkompaktnější?** Data Matrix – ideální pro malé štítky.  
- **Mohu přidat jak QR, tak Data Matrix do stejného PDF?** Ano, stačí vytvořit samostatné `QrCodeSignOptions`.  
- **Potřebuji během běhu internetové připojení?** Ne, knihovna funguje zcela offline po instalaci.  
- **Jaká verze Javy je doporučena?** Java 11+ pro produkční výkon.

## Co je podepisování PDF pomocí HIBC čárového kódu?
Třída `Signature` v GroupDocs.Signature pro Javu představuje PDF dokument a poskytuje metody pro vložení HIBC čárových kódů jako digitálních podpisů. Podepsáním PDF HIBC čárovým kódem vytvoříte ověřitelný, zjevně manipulovatelný záznam, který může být skenován v libovolném bodě dodavatelského řetězce.

## Proč používat Data Matrix a QR kódy společně?
GroupDocs.Signature podporuje **více než 50 vstupních a výstupních formátů** a dokáže zpracovat PDF s několika stovkami stránek, aniž by načítal celý soubor do paměti. Použití Data Matrix pro husté, malé štítky a QR pro prostornější dokumenty vám poskytuje nejlepší rovnováhu čitelnosti, kapacity dat (až 4 296 znaků pro QR) a efektivity tisku.

## Předpoklady
- **JDK 11 nebo vyšší** (Java 8 funguje, ale Java 11+ je doporučena pro optimální výkon).  
- **IDE** jako IntelliJ IDEA, Eclipse nebo VS Code s rozšířeními pro Javu.  
- **Maven nebo Gradle** pro správu závislostí (příklady níže).  
- **Ukázkový PDF** (např. `sample.pdf`) pro testování implementace.  
- **Platná licence GroupDocs.Signature** (bezplatná zkušební verze pro vývoj, placená licence pro produkci).

## Nastavení GroupDocs.Signature pro Javu

### Konfigurace Maven
Add the dependency to your `pom.xml`:

```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

### Konfigurace Gradle
For Gradle projects, add this to your `build.gradle`:

```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

### Možnost přímého stažení
Můžete také stáhnout soubor JAR přímo z [GroupDocs.Signature for Java releases](https://releases.groupdocs.com/signature/java/) a přidat jej ručně do classpath vašeho projektu. Tento přístup dobře funguje v prostředích s omezeným přístupem k síti.

### Získání licence
Požádejte o bezplatnou zkušební verzi nebo dočasnou licenci od GroupDocs, abyste odstranili vodoznaky a odemkli všechny funkce. Produkční nasazení vyžaduje zakoupenou licenci.

### Základní inicializace
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

## Jak vytvořit PDF s Data Matrix a HIBC čárovým kódem?
Načtěte svůj zdrojový PDF, nakonfigurujte objekt `QrCodeSignOptions` pro formát Data Matrix a zavolejte `sign()` – to je vše, co potřebujete k vložení kompatibilního HIBC Data Matrix čárového kódu. Následující kroky vás provedou přesným potřebným kódem. `QrCodeSignOptions` definuje nastavení podpisu čárového kódu, jako typ, obsah, velikost a pozici.

1. **Import the required classes** – these give you access to the signature engine and Data Matrix options.  

```java
import com.groupdocs.signature.Signature;
import com.groupdocs.signature.options.sign.QrCodeSignOptions;
import com.groupdocs.signature.domain.qrcodes.QrCodeTypes;
```

2. **Instantiate the `Signature` object** with absolute paths for source and destination files.  

```java
String sourceFilePath = "YOUR_DOCUMENT_DIRECTORY";
String destinFilePath = "YOUR_OUTPUT_DIRECTORY/SignWithHIBCLICQR.pdf";

final Signature signature = new Signature(sourceFilePath);
```

3. **Configure the Data Matrix options** – set the HIBC string, choose `QrCodeTypes.HIBCLICDataMatrix`, and define placement coordinates. `QrCodeTypes` enumerates the supported barcode formats for HIBC signatures.  

```java
QrCodeSignOptions hibcLic_QR = new QrCodeSignOptions("A123PROD30917/75#422011907#GP293", QrCodeTypes.HIBCLICQR);
hibcLic_QR.setLeft(1); // Set the position from left
hibcLic_QR.setTop(1);   // Set the position from top
hibcLic_QR.setReturnContent(true); // Return content after signing
hibcLic_QR.setReturnContentType(FileType.PNG); // Specify return content type as PNG
```

4. **Apply the signature** to the PDF.  

```java
signature.sign(destinFilePath, hibcLic_QR);
```

5. **Dispose of resources** to free file handles and avoid memory leaks.  

```java
finally {
    if (signature != null) signature.dispose();
}
```

### Kompletní funkční příklad
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

#### Přímá odpověď (40–70 slov)
To **create a Data Matrix PDF**, instantiate `Signature` with your source PDF, set `QrCodeSignOptions` to `QrCodeTypes.HIBCLICDataMatrix` and provide a correctly formatted HIBC string, then call `signature.sign(outputPath, options)`. The library writes the signed PDF to the destination, preserving layout and embedding the barcode as a tamper‑evident signature.

## Jak přidat QR kód do PDF pomocí GroupDocs.Signature?
Load the PDF, configure `QrCodeSignOptions` for the QR format, and invoke `sign()`. This two‑line pattern works for any PDF size and automatically scales the QR image for optimal readability. `QrCodeSignOptions` configures the QR barcode signature, including its content and visual properties. It positions the code based on the coordinates you set, ensuring it does not overlap existing content and remains scannable after printing.

1. **Import QR‑specific classes**  

```java
QrCodeSignOptions hibcLic_AZ = new QrCodeSignOptions("A123PROD30917/75#422011907#GP293", QrCodeTypes.HIBCLICAztec);
hibcLic_AZ.setLeft(1); // Set the position from left
hibcLic_AZ.setTop(200); // Set the position from top
hibcLic_AZ.setReturnContent(true); // Return content after signing
hibcLic_AZ.setReturnContentType(FileType.PNG); // Specify return content type as PNG
```

2. **Create and configure QR options** – note the use of `QrCodeTypes.HIBCLICQR`.  

```java
signature.sign(destinFilePath, hibcLic_AZ);
```

3. **Sign the document**  

```java
QrCodeSignOptions hibcLic_DM = new QrCodeSignOptions("A123PROD30917/75#422011907#GP293", QrCodeTypes.HIBCLICDataMatrix);
hibcLic_DM.setLeft(1); // Set the position from left
hibcLic_DM.setTop(400); // Set the position from top
hibcLic_DM.setReturnContent(true); // Return content after signing
hibcLic_DM.setReturnContentType(FileType.PNG); // Specify return content type as PNG
```

> **Direct answer:** Use `QrCodeTypes.HIBCLICQR` in `QrCodeSignOptions`, set the HIBC content string, position the code with `setLeft()` and `setTop()`, then call `signature.sign(outputPath, options)`. The QR barcode is embedded instantly, ready for smartphone or scanner capture.

## Časté chyby, kterým se vyhnout

### 1. Zapomenutí uvolnění prostředků
**Wrong:**  
```java
Signature signature = new Signature("sample.pdf");
signature.sign(destinFilePath, options);
// Oops, no dispose() call
```  

**Fix:** Wrap the `Signature` usage in a try‑with‑resources block or explicitly call `close()` in a finally clause.

### 2. Použití nesprávných HIBC formátových řetězců
**Wrong:** Using generic strings like “12345”.  
**Fix:** Follow the HIBCC standard (e.g., `A123PROD30917/75#422011907#GP293`). Validate with the [HIBCC online validator](https://www.hibcc.org/).

### 3. Hard‑coding souborových cest
**Wrong:**  
```java
String sourceFilePath = "C:/Users/John/Documents/test.pdf";
```  

**Fix:** Store paths in a configuration file or environment variable and read them at runtime.

### 4. Ignorování konfliktů pozic čárových kódů
Place barcodes away from existing text or signatures. Use PDF coordinates (origin is bottom‑left) and test with a printed sample.

### 5. Nepoužívání reálných skenerů při testování
Print the signed PDF and scan it with the exact hardware used in your workflow. Verify readability at different print qualities.

## Praktické aplikace ve zdravotnictví

| Scénář | Doporučený čárový kód | Proč to vyhovuje |
|----------|--------------------|--------------|
| **Distribuce farmaceutik** | QR kód | Vysoká kapacita dat, široce skenováno smartphony. |
| **Správa zásob** | Data Matrix | Malá stopa, ideální pro husté štítky na policích. |
| **Regulační shoda (FDA 21 CFR Part 11)** | QR + Data Matrix | Dvojformát poskytuje redundanci a auditovatelnost. |
| **Sledování zdravotnických zařízení** | Aztec Code | Kompaktní velikost funguje na obalech s omezeným prostorem. |

## Úvahy o výkonu a osvědčené postupy

### Vzor dávkového zpracování
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

- Vytvořte novou instanci `Signature` pro každý soubor, aby se udržovala nízká spotřeba paměti.  
- Použijte pevný thread pool (`Executors.newFixedThreadPool(Runtime.getRuntime().availableProcessors() - 1)`) pro paralelní zpracování, ale sledujte velikost haldy, protože každá `Signature` drží celý PDF v paměti.  

### Udržujte knihovny aktualizované
GroupDocs releases improve processing speed by up to **20 %** and add new HIBC compliance features. Schedule quarterly dependency checks.

### Kešování šablon
Load a PDF template once, clone it for each barcode variant, and sign the clones. This reduces I/O and speeds up high‑volume workflows.

## Často kladené otázky

**Q: Can GroupDocs.Signature sign file types other than PDF?**  
A: Yes, it also supports DOCX, XLSX, PPTX, PNG, JPEG, and TIFF with the same barcode‑signing API.

**Q: How do I troubleshoot “Invalid barcode content” errors?**  
A: Verify that your HIBC string follows the exact HIBCC syntax, use the online validator, and ensure you’re using the correct `QrCodeTypes` constant for the chosen format.

**Q: What is the maximum data capacity for each HIBC format?**  
A: QR ≈ 4,296 alphanumeric characters, Aztec ≈ 3,832 numeric / 3,067 alphanumeric, Data Matrix ≈ 3,116 numeric / 2,335 alphanumeric. Keep codes under 200 characters for optimal scan reliability.

**Q: Is it possible to embed multiple barcode types in one PDF?**  
A: Absolutely. Create separate `QrCodeSignOptions` objects with different positions and call `signature.sign()` for each. Just ensure they don’t overlap.

**Q: Do I need an internet connection for signing at runtime?**  
A: No. After the JAR is on the classpath and the license is activated, all operations are performed locally.

## Další zdroje

- [GroupDocs.Signature for Java Documentation](https://docs.groupdocs.com/signature/java/)  
- [API Reference Guide](https://reference.groupdocs.com/signature/java/)  
- [Latest Release Downloads](https://releases.groupdocs.com/signature/java/)  
- [Purchase License](https://purchase.groupdocs.com/buy)  
- [Get Free Trial](https://releases.groupdocs.com/signature/java/)  
- [Request Temporary License](https://purchase.groupdocs.com/temporary-license/)  
- [GroupDocs Forum](https://forum.groupdocs.com/c/signature/)

---

**Last Updated:** 2026-05-16  
**Tested With:** GroupDocs.Signature 23.12 for Java  
**Author:** GroupDocs  

```java
signature.sign(destinFilePath, hibcLic_DM);
```

## Související tutoriály

- [Create Barcode Signature PDF in Java – GroupDocs Guide](/signature/java/barcode-signatures/create-sign-pdfs-groupdocs-barcode-java/)  
- [Create Barcode Signature in Java – Update PDF Barcodes](/signature/java/barcode-signatures/java-groupdocs-signature-barcode-initialize-update/)  
- [How to read QR code PDF using Java and GroupDocs.Signature](/signature/java/barcode-signatures/java-pdf-barcode-search-groupdocs-signature-api/)