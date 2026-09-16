---
categories:
- Document Signing
- Healthcare Integration
date: '2026-09-15'
description: Naučte se, jak podepsat PDF pomocí čárového kódu s GroupDocs.Signature
  pro Java. Podrobný návod krok za krokem pro přidání Data Matrix a QR kódů do zdravotnických
  dokumentů.
keywords:
- sign pdf with barcode
- add qr code pdf
- hibc barcode java
- pdf signing java
- healthcare barcode signing
lastmod: '2026-09-15'
linktitle: Průvodce podepisováním PDF HIBC v Javě
og_description: Podepište PDF pomocí čárového kódu s GroupDocs.Signature pro Java.
  Naučte se vložit Data Matrix a QR kódy do zdravotnických dokumentů během několika
  kroků.
og_image_alt: 'Developer tutorial: sign PDF with HIBC barcode using GroupDocs.Signature
  for Java'
og_title: Podepište PDF pomocí čárového kódu HIBC v Javě – průvodce GroupDocs
schemas:
- author: GroupDocs
  dateModified: '2026-09-15'
  description: Learn how to sign PDF with barcode using GroupDocs.Signature for Java.
    Step‑by‑step guide for adding Data Matrix and QR codes in healthcare documents.
  headline: Sign PDF with barcode using HIBC in Java
  type: TechArticle
- description: Learn how to sign PDF with barcode using GroupDocs.Signature for Java.
    Step‑by‑step guide for adding Data Matrix and QR codes in healthcare documents.
  name: Sign PDF with barcode using HIBC in Java
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
- sign pdf
- barcode
- java
- healthcare
- groupdocs
title: Jak podepsat PDF pomocí čárového kódu HIBC v Javě
type: docs
url: /cs/java/barcode-signatures/sign-pdfs-hibc-lic-codes-groupdocs-java/
weight: 1
---

# Podepsat PDF s čárovým kódem pomocí HIBC v Javě

Pokud vytváříte software pro farmaceutickou nebo zdravotnickou logistiku, pravděpodobně jste narazili na problémy s papírovým sledováním, ztracenými podpisy a nočními můrami auditů. **Podepsání PDF s čárovým kódem**—zejména HIBC Data Matrix nebo QR kódem—vytváří důkaz o manipulaci, strojově čitelnou stopu, která přežije tisk, skenování a regulatorní kontrolu. V tomto tutoriálu uvidíte přesně, jak přidat jak Data Matrix, tak QR čárové kódy do PDF pomocí GroupDocs.Signature pro Javu.

## Rychlé odpovědi
- **Jaká knihovna zpracovává HIBC čárové kódy v Javě?** GroupDocs.Signature for Java.  
- **Který formát čárového kódu je nejkompaktnější?** Data Matrix – ideální pro malé štítky.  
- **Mohu přidat jak QR, tak Data Matrix do stejného PDF?** Ano, stačí vytvořit samostatné `QrCodeSignOptions`.  
- **Potřebuji během běhu internetové připojení?** Ne, knihovna funguje zcela offline po instalaci.  
- **Jaká verze Javy je doporučená?** Java 11+ pro produkční výkon.

## Co je podepisování PDF čárovým kódem HIBC?
`Signature` je jádrová třída GroupDocs.Signature, která představuje PDF dokument a umožňuje vkládání digitálních podpisů. Třída `Signature` v GroupDocs.Signature pro Javu poskytuje metody pro vložení HIBC čárových kódů jako digitálních podpisů. Podepsáním PDF HIBC čárovým kódem vytvoříte ověřitelný, důkaz o manipulaci, který může být skenován v libovolném bodě dodavatelského řetězce.

## Proč používat Data Matrix a QR kódy společně?
Data Matrix nabízí nejmenší rozměr a přitom pojme až 2 335 alfanumerických znaků, což je ideální pro hustě označené oblasti štítků. QR kódy naopak podporují až 4 296 znaků a jsou univerzálně čitelné chytrými telefony. Kombinací obou získáte nejlepší rovnováhu mezi úsporností místa a kapacitou dat, což zajišťuje, že každý zainteresovaný – od skenerů ve skladu po mobilní aplikace – může přečíst potřebné informace.

## Předpoklady
- **JDK 11 nebo vyšší** (Java 8 funguje, ale Java 11+ je doporučena pro optimální výkon).  
- **IDE** jako IntelliJ IDEA, Eclipse nebo VS Code s rozšířeními pro Javu.  
- **Maven nebo Gradle** pro správu závislostí (příklady níže).  
- **Ukázkový PDF** (např. `sample.pdf`) pro testování implementace.  
- **Platná licence GroupDocs.Signature** (bezplatná zkušební verze pro vývoj, placená licence pro produkci).

## Nastavení GroupDocs.Signature pro Javu

### Konfigurace Maven
Přidejte závislost do vašeho `pom.xml`:

```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

### Konfigurace Gradle
Pro projekty Gradle přidejte toto do vašeho `build.gradle`:

```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

### Možnost přímého stažení
Můžete také stáhnout soubor JAR přímo z [GroupDocs.Signature for Java releases](https://releases.groupdocs.com/signature/java/) a přidat jej ručně do classpath vašeho projektu. Tento přístup dobře funguje v prostředích s omezeným připojením k síti.

### Získání licence
Požádejte o bezplatnou zkušební verzi nebo dočasnou licenci od GroupDocs, abyste odstranili vodoznaky a odemkli všechny funkce. Produkční nasazení vyžaduje zakoupenou licenci.

### Základní inicializace
`Signature` je vstupní bod pro všechny operace podepisování. Načte PDF, aplikuje čárový kód a zapíše podepsaný soubor.

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
Vytvořte instanci `Signature` s vaším zdrojovým PDF, nastavte `QrCodeSignOptions` na formát **Data Matrix**, poskytněte správně naformátovaný HIBC řetězec a zavolejte `sign()`. Knihovna zapíše podepsané PDF do cíle, zachová rozvržení a vloží čárový kód jako důkaz o manipulaci.

`QrCodeSignOptions` určuje typ čárového kódu, obsah, velikost a umístění pro podpis.

1. **Importujte požadované třídy** – ty vám umožní přístup k podpisovému enginu a možnostem Data Matrix.  

```java
import com.groupdocs.signature.Signature;
import com.groupdocs.signature.options.sign.QrCodeSignOptions;
import com.groupdocs.signature.domain.qrcodes.QrCodeTypes;
```

2. **Vytvořte objekt `Signature`** s absolutními cestami ke zdrojovým a cílovým souborům.  

```java
String sourceFilePath = "YOUR_DOCUMENT_DIRECTORY";
String destinFilePath = "YOUR_OUTPUT_DIRECTORY/SignWithHIBCLICQR.pdf";

final Signature signature = new Signature(sourceFilePath);
```

3. **Nastavte možnosti Data Matrix** – nastavte HIBC řetězec, vyberte `QrCodeTypes.HIBCLICDataMatrix` a definujte souřadnice umístění. `QrCodeTypes` vyjmenovává podporované formáty čárových kódů pro HIBC podpisy.  

```java
QrCodeSignOptions hibcLic_QR = new QrCodeSignOptions("A123PROD30917/75#422011907#GP293", QrCodeTypes.HIBCLICQR);
hibcLic_QR.setLeft(1); // Set the position from left
hibcLic_QR.setTop(1);   // Set the position from top
hibcLic_QR.setReturnContent(true); // Return content after signing
hibcLic_QR.setReturnContentType(FileType.PNG); // Specify return content type as PNG
```

4. **Aplikujte podpis** na PDF.  

```java
signature.sign(destinFilePath, hibcLic_QR);
```

5. **Uvolněte prostředky** pro uvolnění souborových handle a zabránění únikům paměti.  

```java
finally {
    if (signature != null) signature.dispose();
}
```

### Kompletní funkční příklad
Zde je celý tok v jednom bloku (zástupci představují přesný kód, který vložíte z předchozích úryvků):

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
Pro **vytvoření PDF s Data Matrix** vytvořte instanci `Signature` s vaším zdrojovým PDF, nastavte `QrCodeSignOptions` na `QrCodeTypes.HIBCLICDataMatrix` a poskytněte správně naformátovaný HIBC řetězec, poté zavolejte `signature.sign(outputPath, options)`. Knihovna zapíše podepsané PDF do cíle, zachová rozvržení a vloží čárový kód jako důkaz o manipulaci.

## Jak přidat QR kód do PDF pomocí GroupDocs.Signature?
Načtěte PDF, nakonfigurujte `QrCodeSignOptions` pro QR formát a zavolejte `sign()`. Knihovna škáluje QR obrázek pro čitelnost a umístí jej podle nastavených souřadnic, aby nedocházelo k překrytí s existujícím obsahem. To zajišťuje, že čárový kód zůstane po tisku skenovatelný a splňuje standardy HIBC.

`QrCodeSignOptions` definuje obsah, velikost a pozici QR čárového kódu.

1. **Importujte třídy specifické pro QR**  

```java
QrCodeSignOptions hibcLic_AZ = new QrCodeSignOptions("A123PROD30917/75#422011907#GP293", QrCodeTypes.HIBCLICAztec);
hibcLic_AZ.setLeft(1); // Set the position from left
hibcLic_AZ.setTop(200); // Set the position from top
hibcLic_AZ.setReturnContent(true); // Return content after signing
hibcLic_AZ.setReturnContentType(FileType.PNG); // Specify return content type as PNG
```

2. **Vytvořte a nakonfigurujte QR možnosti** – všimněte si použití `QrCodeTypes.HIBCLICQR`.  

```java
signature.sign(destinFilePath, hibcLic_AZ);
```

3. **Podepište dokument**  

```java
QrCodeSignOptions hibcLic_DM = new QrCodeSignOptions("A123PROD30917/75#422011907#GP293", QrCodeTypes.HIBCLICDataMatrix);
hibcLic_DM.setLeft(1); // Set the position from left
hibcLic_DM.setTop(400); // Set the position from top
hibcLic_DM.setReturnContent(true); // Return content after signing
hibcLic_DM.setReturnContentType(FileType.PNG); // Specify return content type as PNG
```

> **Přímá odpověď:** Použijte `QrCodeTypes.HIBCLICQR` v `QrCodeSignOptions`, nastavte HIBC obsahový řetězec, umístěte kód pomocí `setLeft()` a `setTop()`, poté zavolejte `signature.sign(outputPath, options)`. QR čárový kód je vložen okamžitě, připraven pro zachycení chytrým telefonem nebo skenerem.

## Běžné chyby, kterým se vyhnout

### 1. Zapomenutí uvolnění prostředků
**Špatně:**  
```java
Signature signature = new Signature("sample.pdf");
signature.sign(destinFilePath, options);
// Oops, no dispose() call
```  

**Oprava:** Zabalte použití `Signature` do bloku try‑with‑resources nebo explicitně zavolejte `close()` ve finally bloku.

### 2. Použití nesprávných HIBC formátových řetězců
**Špatně:** Používání obecných řetězců jako “12345”.  
**Oprava:** Dodržujte standard HIBCC (např. `A123PROD30917/75#422011907#GP293`). Ověřte pomocí [HIBCC online validator](https://www.hibcc.org/).

### 3. Hard‑kódování cest k souborům
**Špatně:**  
```java
String sourceFilePath = "C:/Users/John/Documents/test.pdf";
```  

**Oprava:** Uložte cesty do konfiguračního souboru nebo proměnné prostředí a načtěte je během běhu.

### 4. Ignorování konfliktů pozic čárových kódů
Umístěte čárové kódy mimo existující text nebo podpisy. Používejte PDF souřadnice (počátek je doleva dole) a testujte s tištěným vzorkem.

### 5. Netestování s reálnými skenery
Vytiskněte podepsané PDF a skenujte jej pomocí přesného hardwaru používaného ve vašem workflow. Ověřte čitelnost při různých kvalitách tisku.

## Praktické aplikace ve zdravotnictví

| Scénář | Doporučený čárový kód | Proč to vyhovuje |
|----------|--------------------|--------------|
| **Distribuce farmaceutik** | QR kód | Vysoká kapacita dat, široce skenováno smartphony. |
| **Správa zásob** | Data Matrix | Malý rozměr, ideální pro husté štítky na policích. |
| **Regulační soulad (FDA 21 CFR Part 11)** | QR + Data Matrix | Dvojitý formát poskytuje redundanci a auditovatelnost. |
| **Sledování zdravotnických zařízení** | Aztec Code | Kompaktní velikost funguje na balení s omezeným prostorem. |

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

- Vytvořte novou instanci `Signature` pro každý soubor, aby byl nízký odběr paměti.  
- Použijte pevný thread pool (`Executors.newFixedThreadPool(Runtime.getRuntime().availableProcessors() - 1)`) pro paralelní zpracování, ale monitorujte velikost haldy, protože každá `Signature` drží celé PDF v paměti.

### Udržujte knihovny aktualizované
Vydání GroupDocs zlepšují rychlost zpracování až o **20 %** a přidávají nové funkce pro soulad s HIBC. Plánujte čtvrtletní kontrolu závislostí.

### Kešování šablon
Načtěte PDF šablonu jednou, klonujte ji pro každou variantu čárového kódu a podepisujte klony. Tím se sníží I/O a urychlí workflow s vysokým objemem.

## Často kladené otázky

**Q: Může GroupDocs.Signature podepisovat soubory jiných typů než PDF?**  
A: Ano, také podporuje DOCX, XLSX, PPTX, PNG, JPEG a TIFF pomocí stejného API pro podepisování čárových kódů.

**Q: Jak řešit chyby „Invalid barcode content“?**  
A: Ověřte, že váš HIBC řetězec přesně odpovídá syntaxi HIBCC, použijte online validátor a ujistěte se, že používáte správnou konstantu `QrCodeTypes` pro zvolený formát.

**Q: Jaká je maximální kapacita dat pro každý HIBC formát?**  
A: QR ≈ 4 296 alfanumerických znaků, Aztec ≈ 3 832 číselných / 3 067 alfanumerických, Data Matrix ≈ 3 116 číselných / 2 335 alfanumerických. Udržujte kódy pod 200 znaky pro optimální spolehlivost skenování.

**Q: Je možné vložit více typů čárových kódů do jednoho PDF?**  
A: Rozhodně. Vytvořte samostatné objekty `QrCodeSignOptions` s různými pozicemi a pro každý zavolejte `signature.sign()`. Jen se ujistěte, že se nepřekrývají.

**Q: Potřebuji během běhu internetové připojení pro podepisování?**  
A: Ne. Po umístění JAR do classpath a aktivaci licence jsou všechny operace prováděny lokálně.

## Další zdroje
- [GroupDocs.Signature for Java Documentation](https://docs.groupdocs.com/signature/java/)  
- [API Reference Guide](https://reference.groupdocs.com/signature/java/)  
- [Latest Release Downloads](https://releases.groupdocs.com/signature/java/)  
- [Purchase License](https://purchase.groupdocs.com/buy)  
- [Get Free Trial](https://releases.groupdocs.com/signature/java/)  
- [Request Temporary License](https://purchase.groupdocs.com/temporary-license/)  
- [GroupDocs Forum](https://forum.groupdocs.com/c/signature/)  

---

**Poslední aktualizace:** 2026-09-15  
**Testováno s:** GroupDocs.Signature 23.12 pro Javu  
**Autor:** GroupDocs  

## Související tutoriály

- [Create Barcode Signature PDF in Java – GroupDocs Guide](/signature/java/barcode-signatures/create-sign-pdfs-groupdocs-barcode-java/)
- [Create Barcode Signature in Java – Update PDF Barcodes](/signature/java/barcode-signatures/java-groupdocs-signature-barcode-initialize-update/)
- [How to read QR code PDF using Java and GroupDocs.Signature](/signature/java/barcode-signatures/java-pdf-barcode-search-groupdocs-signature-api/)

```java
signature.sign(destinFilePath, hibcLic_DM);
```

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}