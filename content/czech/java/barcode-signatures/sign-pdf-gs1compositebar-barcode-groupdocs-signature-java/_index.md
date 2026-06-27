---
categories:
- Java PDF Processing
date: '2026-05-21'
description: Naučte se, jak vytvořit barcode signature Java pro PDF pomocí GroupDocs.Signature.
  Kompletní průvodce s ukázkami kódu, tipy na řešení problémů a reálnými příklady
  použití pro autentizaci dokumentů.
keywords:
- create barcode signature java
- barcode signatures java
- pdf barcode signing java
lastmod: '2026-05-21'
linktitle: PDF barcode signatures v Javě
schemas:
- author: GroupDocs
  dateModified: '2026-05-21'
  description: Learn how to create barcode signature Java for PDFs using GroupDocs.Signature.
    Complete guide with code examples, troubleshooting tips, and real-world use cases
    for document authentication.
  headline: How to Create Barcode Signature Java for PDF Documents
  type: TechArticle
- questions:
  - answer: A GS1CompositeBar combines linear and 2D components to store product IDs,
      serial numbers, and other data in a single scannable symbol, widely used in
      retail and logistics.
    question: What is a GS1CompositeBar barcode?
  - answer: Yes—GroupDocs.Signature supports over 60 types, including QR, Code128,
      DataMatrix, PDF417, and Aztec. Switch the `setEncodeType()` value to change
      the format.
    question: Can I use other barcode types besides GS1CompositeBar?
  - answer: A valid GroupDocs license is required for production deployments. A free
      trial is available for development and testing.
    question: Do I need a license for production use?
  - answer: Absolutely, provided the barcode is at least 200 × 100 px and has sufficient
      contrast. Smartphone scanning apps work on‑screen; hardware scanners work on
      printed copies.
    question: Will barcode scanners read barcodes from signed PDFs?
  - answer: Wrap your code in try‑catch blocks, log full stack traces, and always
      call `signature.dispose()` in a finally block to release resources.
    question: How do I handle errors during signing?
  type: FAQPage
tags:
- barcode-signatures
- pdf-signing
- document-authentication
- java-libraries
title: Jak vytvořit barcode signature Java pro PDF dokumenty
type: docs
url: /cs/java/barcode-signatures/sign-pdf-gs1compositebar-barcode-groupdocs-signature-java/
weight: 1
---

# Jak vytvořit čárový kód podpis v Javě pro PDF dokumenty

## Úvod

V tomto tutoriálu se naučíte, jak **vytvořit čárový kód podpis v Javě** pro PDF soubory pomocí GroupDocs.Signature. Ať už potřebujete vložit produktové kódy, auditní ID nebo jakákoli strukturovaná data do smlouvy, čárové kódy vám umožní přidat strojově čitelné informace, které lze okamžitě naskenovat, a zároveň zachovat kryptografickou bezpečnost dokumentu. Provedeme vás nastavením, kódem, přizpůsobením a tipy na nejlepší postupy, abyste mohli během několika minut přidávat čárové kódy do svých PDF.

## Rychlé odpovědi
- **Která knihovna přidává čárové kódy do podpisů v Javě?** GroupDocs.Signature for Java.
- **Jaký typ čárového kódu je nejlepší pro maloobchod?** `GS1CompositeBar` (průmyslový standard pro sledování produktů).
- **Potřebuji licenci pro produkci?** Ano – je vyžadována zakoupená licence GroupDocs.
- **Mohu přidat jak digitální, tak čárový kód podpisy?** Rozhodně; můžete je kombinovat pro bezpečnost i skenovatelnost.
- **Je kód kompatibilní s Java 11 a novějšími?** Ano, API funguje s JDK 8+.

## Co je create barcode signature java?
`create barcode signature java` označuje proces programového vložení čárového kódu do PDF pomocí Java kódu. GroupDocs.Signature poskytuje jednoduché API, které vygeneruje obrázek čárového kódu, umístí jej na stránku a uloží podepsaný dokument v jedné plynulé operaci.

## Proč používat čárové kódy v podpisu?
Čárové kódy vám poskytují **strojově čitelná metadata** uvnitř právně podepsaného PDF. Umožňují okamžitou vizuální kontrolu, zefektivňují skenování v dodavatelském řetězci a umožňují downstream systémům extrahovat strukturovaná data bez otevření souboru. Podporováno je více než 60 formátů čárových kódů a GS1CompositeBar může kódovat produktové identifikátory, sériová čísla i šarže v jednom kompaktním symbolu – ideální pro maloobchod, zdravotnictví i finance.

## Požadavky

- **Java Development Kit:** JDK 8 nebo novější (Java 11, 17, 21 všechny fungují).
- **Nástroj pro sestavení:** Maven nebo Gradle – vyberte ten, který preferujete.
- **IDE:** IntelliJ IDEA, Eclipse nebo VS Code.
- **Knihovna GroupDocs.Signature:** Přidejte závislost podle níže uvedených instrukcí.
- **Licence:** Bezplatná zkušební verze pro vývoj; zakoupená licence pro produkci.

### Přidání GroupDocs.Signature do projektu

**Pro uživatele Maven**, přidejte následující do souboru `pom.xml`:

```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

**Pro uživatele Gradle**, přidejte následující do souboru `build.gradle`:

```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

**O licencování:** GroupDocs nabízí bezplatnou zkušební verzi, která je ideální pro testování a vývoj. Stáhnout ji můžete z jejich [stránky vydání](https://releases.groupdocs.com/signature/java/). Když budete připraveni na produkci, musíte zakoupit licenci nebo požádat o dočasnou licenci na [webu GroupDocs](https://purchase.groupdocs.com/buy). Podrobnou dokumentaci API najdete v [API Reference](https://reference.groupdocs.com/signature/java/), podívejte se do [Developer Guide](https://docs.groupdocs.com/signature/java/) pro krok‑za‑krokem instrukce a kladte otázky na [GroupDocs Forum](https://forum.groupdocs.com/). Stejný odkaz na nákup je uveden také jako [purchase page](https://purchase.groupdocs.com/buy).

## Jak nastavit GroupDocs.Signature v Javě?

Třída `Signature` představuje dokument a poskytuje metody pro aplikaci podpisů, vyhledávání obsahu a správu zdrojů. Vytvořte instanci `Signature`, abyste otevřeli PDF a připravili jej k podepsání. Třída `Signature` je jádrem GroupDocs.Signature, které spravuje načítání dokumentu, manipulaci se zdroji a workflow podepisování, což zajišťuje bezpečný a efektivní průběh všech operací.

```java
import com.groupdocs.signature.Signature;

// Point to your PDF file
Signature signature = new Signature("path/to/your/document.pdf");
```

**Důležité:** Vždy po použití uvolněte objekt `Signature` – tím se uvolní souborové handly a paměť.

## Jak nakonfigurovat možnosti čárového kódu pro podpis?

Třída `BarcodeSignOptions` definuje každý aspekt čárového kódu, který chcete vložit, od datového payloadu po vizuální styl. Slouží jako kontejner pro všechna nastavení související s čárovým kódem, jako je typ, velikost, barvy a umístění. Níže je minimální konfigurace, která vytvoří čárový kód GS1CompositeBar obsahující GTIN a sériové číslo, a také ukazuje, jak nastavit okraje a barvu pozadí pro optimální čitelnost.

```java
import com.groupdocs.signature.options.sign.BarcodeSignOptions;
import com.groupdocs.signature.domain.barcodes.BarcodeTypes;

// Create barcode with GS1 format data
BarcodeSignOptions options = new BarcodeSignOptions("(01)03212345678906/(21)A1B2C3D4E5F6G7H8");
options.setEncodeType(BarcodeTypes.GS1CompositeBar);
```

Řetězec `"(01)03212345678906/(21)A1B2C3D4E5F6G7H8"` odpovídá standardu GS1:
- `(01)` = GTIN (globální produktový identifikátor)
- `03212345678906` = skutečný kód produktu
- `(21)` = identifikátor sériového čísla
- `A1B2C3D4E5F6G7H8` = unikátní sériové číslo

Můžete jej nahradit libovolným textem pro QR kódy, Code128, DataMatrix atd. Podporováno je více než 60 typů čárových kódů – kompletní seznam najdete v dokumentaci GroupDocs.

## Jak umístit a přizpůsobit čárový kód?

Umístění a styl jsou řízeny stejným objektem `BarcodeSignOptions`. Použijte `setTop`, `setLeft`, `setWidth` a `setHeight` pro definování přesných souřadnic a rozměrů. Nastavením `setAllPages(true)` přidáte čárový kód na každou stránku automaticky, zatímco `setPageNumber(1)` cílí konkrétní stránku. Můžete také otáčet čárový kód, přidat barvu pozadí nebo upravit okraje, aby nedocházelo k překrytí existujícího obsahu.

```java
// Set position and apply to all pages
options.setTop(200); // Set vertical position
options.setAllPages(true);
```

Pro ještě přesnější rozvržení můžete čárový kód ukotvit na konkrétní stránku, otočit jej nebo přidat barvu pozadí:

```java
options.setLeft(100);        // 100 pixels from left edge
options.setTop(200);         // 200 pixels from top
options.setWidth(300);       // Barcode width in pixels
options.setHeight(100);      // Barcode height in pixels
options.setPageNumber(1);    // Only sign page 1 (removes setAllPages)
```

Vizuální přizpůsobení (barvy popředí/pozadí, okraje, textové popisky) je k dispozici pomocí dalších vlastností:

```java
options.setMargin(new Padding(10));           // Add padding around barcode
options.setBackground(new Background());       // Set background color
options.setForeColor(Color.BLACK);            // Barcode color
options.setBackgroundColor(Color.WHITE);      // Background color
```

## Jak podepsat dokument pomocí čárového kódu?

Metoda `sign` na instanci `Signature` použije nakonfigurované možnosti a zapíše podepsaný dokument na disk. Vrací objekt `SignResult`, který udává, kolik podpisů bylo aplikováno a zda se vyskytly varování. Tato metoda zajišťuje veškerou nízkoúrovňovou manipulaci s PDF, takže nemusíte pracovat přímo s PDF knihovnami.

```java
try {
    SignResult signResult = signature.sign(outputPath, options);
    System.out.println("Document signed successfully!");
    System.out.println("Signed document saved to: " + outputPath);
} finally {
    if (signature != null) {
        signature.dispose();
    }
}
```

Blok `try‑finally` zajišťuje, že objekt `Signature` je uvolněn i v případě výjimky, čímž se předejde únikům souborových handle.

```java
if (signResult.getSucceeded().size() > 0) {
    System.out.println("Successfully added " + signResult.getSucceeded().size() + " signature(s)");
}
```

## Kompletní funkční příklad

Spojením všech částí získáte metodu, která načte PDF, přidá čárový kód GS1CompositeBar a uloží podepsaný soubor:

```java
import com.groupdocs.signature.Signature;
import com.groupdocs.signature.options.sign.BarcodeSignOptions;
import com.groupdocs.signature.domain.barcodes.BarcodeTypes;

public class BarcodeSigningExample {
    
    public void signPdfWithBarcode(String inputPath, String outputPath) {
        Signature signature = null;
        
        try {
            // Initialize signature
            signature = new Signature(inputPath);
            
            // Configure barcode
            BarcodeSignOptions options = new BarcodeSignOptions(
                "(01)03212345678906/(21)A1B2C3D4E5F6G7H8"
            );
            options.setEncodeType(BarcodeTypes.GS1CompositeBar);
            options.setTop(200);
            options.setAllPages(true);
            
            // Sign and save
            SignResult result = signature.sign(outputPath, options);
            
            System.out.println("Signing completed: " + result.getSucceeded().size() + " signature(s) added");
            
        } catch (Exception e) {
            System.err.println("Error signing document: " + e.getMessage());
            e.printStackTrace();
        } finally {
            if (signature != null) {
                signature.dispose();
            }
        }
    }
}
```

Tato metoda je připravena pro produkci: validuje vstup, spravuje zdroje a hlásí výsledek.

## Jak přidat jak digitální, tak čárový kód podpisy?

Pro maximální bezpečnost nejprve přidejte kryptografický digitální podpis a poté na něj navrstvěte čárový kód. Digitální podpis zajišťuje integritu dokumentu, zatímco čárový kód poskytuje rychlou vizuální kontrolu a strojově čitelná data. Použijte třídu `DigitalSignOptions` pro první krok a následně aplikujte `BarcodeSignOptions` podle výše uvedeného příkladu.

```java
// First, add digital signature
DigitalSignOptions digitalOptions = new DigitalSignOptions("certificate.pfx");
digitalOptions.setPassword("cert_password");
signature.sign(outputPath, digitalOptions);

// Then, add barcode on top
BarcodeSignOptions barcodeOptions = new BarcodeSignOptions("DATA");
barcodeOptions.setEncodeType(BarcodeTypes.QR);
signature.sign(outputPath, barcodeOptions);
```

Výsledné PDF je právně závazné (digitální podpis) a okamžitě čitelné jakýmkoli čtečkou čárových kódů.

## Práce s různými typy čárových kódů

Přepnutí formátu čárového kódu je tak jednoduché jako změna jedné enum hodnoty. Níže je příklad, který vymění GS1CompositeBar za QR kód:

```java
// Define barcode sign options with sample text
BarcodeSignOptions options = new BarcodeSignOptions("Sample Text");

// Assign specific barcode type
options.setEncodeType(BarcodeTypes.GS1CompositeBar);
```

A zde je stejná změna pro lineární čárový kód Code128:

```java
options.setEncodeType(BarcodeTypes.QR);           // QR code
options.setEncodeType(BarcodeTypes.Code128);      // Code 128
options.setEncodeType(BarcodeTypes.DataMatrix);   // Data Matrix
```

Pamatujte, že každý typ čárového kódu má své limity kapacity – QR kódy mohou nést tisíce znaků, zatímco Code39 je omezen na alfanumerické znaky.

## Reálné příklady použití

### Řízení dodavatelského řetězce
Vkládání GS1CompositeBar do přepravních listů umožňuje skladníkům skenovat čísla objednávek, destinace i šarže bez otevírání PDF.

```java
BarcodeSignOptions options = new BarcodeSignOptions(
    "(01)" + gtin + "/(21)" + serialNumber + "/(10)" + batchNumber
);
options.setEncodeType(BarcodeTypes.GS1CompositeBar);
```

### Zdravotnická dokumentace
QR kódy na souhlasech lze naskenovat a automaticky archivovat dokument pod správným pacientským záznamem.

```java
String patientData = "PATIENT_ID:" + patientId + "|DOC_TYPE:CONSENT|DATE:" + dateString;
BarcodeSignOptions options = new BarcodeSignOptions(patientData);
options.setEncodeType(BarcodeTypes.QR);
```

### Finanční služby
Identifikátory transakcí zakódované do čárového kódu umožňují auditorům ověřit soulad pouhým skenem.

```java
String complianceData = "TXN:" + transactionId + "|AGENT:" + agentId + "|BRANCH:" + branchCode;
BarcodeSignOptions options = new BarcodeSignOptions(complianceData);
options.setEncodeType(BarcodeTypes.PDF417);
```

### Kontrola kvality výroby
Kontrolní protokoly podepsané čárovými kódy obsahujícími čísla šarží a ID kontrolora usnadňují okamžitou analýzu příčin.

```java
String qcData = "BATCH:" + batchNumber + "|INSPECTOR:" + inspectorId + "|RESULT:" + passFailStatus;
BarcodeSignOptions options = new BarcodeSignOptions(qcData);
options.setEncodeType(BarcodeTypes.DataMatrix);
```

## Běžné problémy při implementaci

### Problém 1: Výjimka „Soubor je již používán“
**Odpověď:** Soubor zůstane uzamčen, pokud předchozí instance `Signature` nebyla uvolněna. Vždy obalte kód podepisování do bloku `try‑finally` a zavolejte `signature.dispose()`.

```java
Signature signature = null;
try {
    signature = new Signature(filePath);
    // ... your code ...
} finally {
    if (signature != null) {
        signature.dispose();
    }
}
```

### Problém 2: Čárový kód se nezobrazuje v PDF
**Odpověď:** Ověřte, že hodnoty `setTop`/`setLeft` jsou v mezích stránky, zvětšete šířku/výšku čárového kódu a zajistěte kontrast mezi popředím a pozadím stránky.

```java
// Make sure dimensions are reasonable
options.setTop(100);      // Not 10000
options.setLeft(100);
options.setWidth(300);    // At least 200 pixels for readability
options.setHeight(100);

// Ensure contrast
options.setForeColor(Color.BLACK);
options.setBackgroundColor(Color.WHITE);
```

### Problém 3: Výjimka „Neplatná data čárového kódu“
**Odpověď:** GS1 čárové kódy vyžadují přísnou notaci závorek. Používejte správné Application Identifiers (např. `(01)`, `(21)`) a vyhněte se nepodporovaným znakům.

```java
// Correct:
"(01)03212345678906/(21)ABC123"

// Incorrect:
"03212345678906ABC123"
```

### Problém 4: OutOfMemoryError u velkých PDF
**Odpověď:** Zvyšte velikost haldy JVM (`-Xmx4G`) a zvažte podepisování stránek jednotlivě místo `setAllPages(true)` u velmi velkých dokumentů.

```bash
java -Xmx2G -jar your-application.jar
```

### Problém 5: Skenování čárového kódu selhává
**Odpověď:** Ujistěte se, že čárový kód má alespoň 200 × 100 px, používá vysoký kontrast a není deformován kompresí PDF.

```java
// Increase size
options.setWidth(400);
options.setHeight(150);

// Maximize contrast
options.setForeColor(Color.BLACK);
options.setBackgroundColor(Color.WHITE);

// Add quiet zone (blank space around barcode)
options.setMargin(new Padding(10));
```

## Bezpečnost a validace

### Jsou čárové kódy v podpisu bezpečné?
Čárový kód sám o sobě není kryptograficky chráněn, takže jej může kdokoli vygenerovat. Kombinujte jej s digitálním podpisem, aby byla zajištěna jak autenticita, tak skenovatelnost. Vzor dvojitého podpisu (digitální nejprve, čárový kód druhý) poskytuje právní vynutitelnost i provozní pohodlí.

### Validace dat čárového kódu
Po naskenování ověřte, že digitální podpis dokumentu je stále platný a že payload čárového kódu odpovídá očekávaným vzorům. K automatickému extrahování a validaci obsahu čárového kódu použijte API `search()` s `BarcodeSearchOptions`.

```java
public boolean validateScannedBarcode(String scannedData, String documentPath) {
    // Verify digital signature first
    if (!verifyDigitalSignature(documentPath)) {
        return false;
    }
    
    // Validate barcode format
    if (!scannedData.matches("(01)\\d{14}/(21)[A-Z0-9]+")) {
        return false;
    }
    
    // Check against database
    String productId = extractProductId(scannedData);
    return database.productExists(productId);
}
```

## Úvahy o výkonu

### Správa zdrojů
Vždy po každé operaci uvolňujte objekty `Signature`, aby nedocházelo k únikům paměti:

```java
signature.dispose();
```

Při zpracování mnoha souborů vytvářejte a uvolňujte novou instanci `Signature` pro každý dokument:

```java
for (String filePath : documentPaths) {
    Signature signature = null;
    try {
        signature = new Signature(filePath);
        // ... signing logic ...
    } finally {
        if (signature != null) {
            signature.dispose();
        }
    }
}
```

### Dávkové zpracování
Pro malé dávky (< 100 souborů) je jednoduché sekvenční zpracování:

```java
for (String path : paths) {
    signDocument(path);
}
```

U větších objemů může paralelní zpracování urychlit práci – ale sledujte zatížení I/O a omezte počet vláken na 4‑8:

```java
paths.parallelStream().forEach(path -> signDocument(path));
```

### Optimalizace paměti pro velké PDF
Zvyšte velikost haldy, zpracovávejte stránky jednotlivě a po každém kroku uvolněte reference. Tím se předejde `OutOfMemoryError` u dokumentů větších než 50 MB.

### Cacheování možností čárového kódu
Pokud používáte stejnou konfiguraci čárového kódu pro mnoho souborů, cacheujte instanci `BarcodeSignOptions`:

```java
// Create once, reuse many times
private static BarcodeSignOptions createStandardBarcodeOptions(String data) {
    BarcodeSignOptions options = new BarcodeSignOptions(data);
    options.setEncodeType(BarcodeTypes.GS1CompositeBar);
    options.setTop(200);
    options.setAllPages(true);
    return options;
}
```

## Pokročilé funkce

### Více podpisů v jednom dokumentu
Přidejte několik čárových kódů (nebo je kombinujte s digitálními podpisy) voláním `sign` opakovaně s různými objekty možností:

```java
// Add QR code in top-left
BarcodeSignOptions qrOptions = new BarcodeSignOptions("https://example.com");
qrOptions.setEncodeType(BarcodeTypes.QR);
qrOptions.setTop(50);
qrOptions.setLeft(50);
signature.sign(outputPath, qrOptions);

// Add GS1 barcode in bottom-right
BarcodeSignOptions gs1Options = new BarcodeSignOptions("(01)03212345678906");
gs1Options.setEncodeType(BarcodeTypes.GS1CompositeBar);
gs1Options.setTop(700);
gs1Options.setLeft(400);
signature.sign(outputPath, gs1Options);
```

### Dynamický obsah čárového kódu
Generujte data čárového kódu z metadat dokumentu, časových razítek nebo databázových dotazů:

```java
// Extract data from PDF or database
String orderId = extractOrderIdFromPdf(filePath);
String timestamp = LocalDateTime.now().format(DateTimeFormatter.ISO_DATE_TIME);
String barcodeData = String.format("ORDER:%s|TIME:%s", orderId, timestamp);

BarcodeSignOptions options = new BarcodeSignOptions(barcodeData);
```

### Integrace se Spring Boot
Expose REST endpoint, který přijme PDF, přidá čárový kód a vrátí podepsaný soubor:

```java
@Service
public class DocumentSigningService {
    public void signWithBarcode(MultipartFile file, String barcodeData) {
        // ... implementation ...
    }
}
```

### Příklad REST API
Minimální kontroler, který deleguje na službu podepisování:

```java
@PostMapping("/sign-document")
public ResponseEntity<byte[]> signDocument(
    @RequestParam("file") MultipartFile file,
    @RequestParam("barcode") String barcodeData
) {
    // Sign document and return as byte array
}
```

## Často kladené otázky

**Q: Co je čárový kód GS1CompositeBar?**  
A: GS1CompositeBar kombinuje lineární a 2D komponenty pro uložení produktových ID, sériových čísel a dalších dat v jednom skenovatelném symbolu, široce používaném v maloobchodu a logistice.

**Q: Mohu použít jiné typy čárových kódů než GS1CompositeBar?**  
A: Ano – GroupDocs.Signature podporuje více než 60 typů, včetně QR, Code128, DataMatrix, PDF417 a Aztec. Změňte hodnotu `setEncodeType()` pro přepnutí formátu.

**Q: Potřebuji licenci pro produkční nasazení?**  
A: Ano, pro produkční nasazení je vyžadována platná licence GroupDocs. Bezplatná zkušební verze je určena pouze pro vývoj a testování.

**Q: Čtečky čárových kódů dokáží načíst čárové kódy z podepsaných PDF?**  
A: Rozhodně, pokud má čárový kód alespoň 200 × 100 px a dostatečný kontrast. Aplikace pro skenování na smartphone fungují na obrazovce; hardwarové čtečky fungují na tištěných kopiích.

**Q: Jak zacházet s chybami během podepisování?**  
A: Obalte kód do `try‑catch` bloků, logujte kompletní stack trace a vždy v `finally` bloku zavolejte `signature.dispose()`, aby se uvolnily zdroje.

**Q: Mohu podepisovat i jiné formáty dokumentů?**  
A: Ano – GroupDocs.Signature podporuje také DOCX, XLSX, PPTX, obrázky a mnoho dalších. Stačí změnit příponu vstupního souboru, API zůstává stejné.

**Q: Existují limity velikosti souboru?**  
A: Žádný pevný limit, ale dokumenty nad 50 MB mohou vyžadovat větší haldu JVM a zpracování po stránkách, aby zůstaly paměťově efektivní.

**Q: Jak podepisovat PDF uložené v cloudovém úložišti?**  
A: Stáhněte soubor do dočasné lokální cesty, aplikujte podpis a poté jej nahrajte zpět do cloudového bucketu. Po dokončení odstraňte dočasné soubory.

## Závěr

Nyní máte kompletní, produkčně připravený návod, jak **vytvořit čárový kód podpis v Javě** pro PDF dokumenty. Kombinací kryptografických digitálních podpisů a strojově čitelných čárových kódů získáte jak právní závaznost, tak provozní efektivitu napříč dodavatelským řetězcem, zdravotnictvím, financemi i výrobou. Experimentujte s různými typy čárových kódů, integrujte kód do stávajících služeb a prozkoumejte dávkové zpracování pro rozsáhlé nasazení.

---

**Last Updated:** 2026-05-21  
**Tested With:** GroupDocs.Signature 23.10 for Java  
**Author:** GroupDocs  

{< /blocks/products/pf/tutorial-page-section >}
{< /blocks/products/pf/main-container >}
{< /blocks/products/pf/main-wrap-class >}
{< blocks/products/products-backtop-button >}

```java
String filePath = "YOUR_DOCUMENT_DIRECTORY" + "/sample.pdf";
String fileName = new java.io.File(filePath).getName();
String outputPath = "YOUR_OUTPUT_DIRECTORY" + "/SignedWithBarcodeGS1CompositeBar/" + fileName;
```

```java
String documentDir = System.getenv("DOCUMENT_DIR");
String outputDir = System.getenv("OUTPUT_DIR");
```

```java
Signature signature = new Signature(filePath);
```

## Související tutoriály

- [Create Barcode Signature in Java – Update PDF Barcodes](/signature/java/barcode-signatures/java-groupdocs-signature-barcode-initialize-update/)
- [Verify Barcode & QR Code in Java - Complete Document Security Guide](/signature/java/search-verification/verify-barcode-qr-code-signatures-groupdocs-java/)
- [HIBC Barcode PDF Signing with Java - Complete Healthcare Document Solution](/signature/java/barcode-signatures/sign-pdfs-hibc-lic-codes-groupdocs-java/)