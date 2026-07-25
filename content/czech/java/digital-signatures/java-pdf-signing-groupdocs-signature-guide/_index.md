---
categories:
- Java Development
date: '2026-07-25'
description: Zjistěte, jak přidat čárový kód jako podpis do PDF pomocí GroupDocs.Signature
  pro Java. Postupné nastavení Maven, možnosti čárových kódů, zpracování chyb a tipy
  pro produkci.
keywords:
- add barcode signature
- groupdocs signature java
- scannable pdf signature
- pdf signing java
- troubleshoot pdf signing
lastmod: '2026-07-25'
linktitle: Návod GroupDocs.Signature Java
og_description: Přidejte čárový kód jako podpis do PDF pomocí GroupDocs.Signature
  Java. Kompletní nastavení Maven, možnosti čárových kódů, řešení problémů a osvědčené
  postupy pro produkci pro vývojáře Java.
og_image_alt: 'Guide: add barcode signature to PDF using GroupDocs.Signature Java'
og_title: Přidejte čárový kód jako podpis do PDF pomocí GroupDocs.Signature Java
schemas:
- author: GroupDocs
  dateModified: '2026-07-25'
  description: Learn how to add barcode signature to PDFs using GroupDocs.Signature
    for Java. Step‑by‑step Maven setup, barcode options, error handling, and production
    tips.
  headline: Add barcode signature to PDFs with GroupDocs.Signature Java
  type: TechArticle
- description: Learn how to add barcode signature to PDFs using GroupDocs.Signature
    for Java. Step‑by‑step Maven setup, barcode options, error handling, and production
    tips.
  name: Add barcode signature to PDFs with GroupDocs.Signature Java
  steps:
  - name: Initialize the Signature Object
    text: 'The `Signature` class is GroupDocs.Signature''s entry point for all signing
      operations. It represents a single PDF document in memory and provides lazy
      loading to keep memory usage low. java import com.groupdocs.signature.Signature;
      public class InitializeSignature { public static void main(String[] '
  - name: Configure Barcode Sign Options
    text: '`BarcodeSignOptions` lets you define every attribute of the barcode—type,
      data, position, colors, borders, and even whether the raw barcode image should
      be returned. java import com.groupdocs.signature.Signature; import com.groupdocs.signature.exception.GroupDocsSignatureException;
      import java.nio.f'
  - name: Sign the Document
    text: 'The `sign` method applies the configured barcode to the PDF and writes
      the result to the target path. java signOptions.setEncodeType(BarcodeTypes.QR);
      // QR codes for more data signOptions.setForeColor(Color.BLACK); signOptions.setBackgroundColor(Color.WHITE);
      // Remove border and fancy styling for '
  type: HowTo
- questions:
  - answer: GroupDocs.Signature for Java is self‑contained; after adding the Maven/Gradle
      artifact you get full barcode generation and PDF rendering without any third‑party
      libraries.
    question: How do I add a barcode signature to a PDF in Java without external dependencies?
  - answer: Absolutely. Switch the `BarcodeTypes` enum to `QRCode` and adjust size
      parameters as needed.
    question: Can I configure barcode sign options in Java to generate QR codes?
  - answer: Pin the exact version in `pom.xml` (e.g., `23.10.0`) to avoid accidental
      upgrades, and enable the Maven `shade` plugin to produce a single executable
      JAR.
    question: What is the recommended Maven setup for production use?
  - answer: Yes. Provide the password when constructing the `Signature` object, then
      proceed with signing as usual.
    question: Does the library support password‑protected PDFs?
  - answer: GroupDocs.Signature can address all pages in a PDF at once or target specific
      pages via `setPageNumber()`. Performance scales linearly; a 200‑page PDF signs
      in ~2 seconds on a typical cloud VM.
    question: How many pages can I sign in one operation?
  type: FAQPage
tags:
- pdf-signing
- digital-signatures
- groupdocs
- barcode-signatures
title: Přidejte čárový kód jako podpis do PDF pomocí GroupDocs.Signature Java
type: docs
url: /cs/java/digital-signatures/java-pdf-signing-groupdocs-signature-guide/
weight: 1
---

# Přidání čárového kódu jako podpisu do PDF pomocí GroupDocs.Signature Java

V moderních aplikacích zaměřených na dokumenty je **přidání čárového kódu jako podpisu** rychlý a spolehlivý způsob, jak učinit PDF čitelné jak pro člověka, tak pro stroj. Tento tutoriál vás provede každým krokem – od konfigurace Maven, přes stylování čárového kódu, až po řešení okrajových případů u velkých souborů – takže můžete s jistotou integrovat čárové kódy jako podpisy do svých Java projektů.

## Rychlé odpovědi
- **Jaký je první řádek kódu pro zahájení podepisování?** `Signature signature = new Signature("sample.pdf");`
- **Který Maven artefakt potřebuji?** `com.groupdocs:groupdocs-signature:23.10` (nahraďte nejnovější verzí)
- **Mohu podepisovat PDF chráněné heslem?** Ano — předáte heslo při vytváření objektu `Signature`.
- **Kolik formátů čárových kódů je podporováno?** Více než 30, včetně Code128, QR, DataMatrix a Aztec.
- **Jaká je doporučená velikost haldy pro PDF o velikosti 100 MB?** Nejméně `-Xmx2g` (2 GB), aby se předešlo `OutOfMemoryError`.

## Co je čárový kód jako podpis?
**Čárový kód jako podpis** je strojově čitelný čárový kód vložený do PDF, který slouží jako indikátor neoprávněné manipulace a může nést vlastní data, jako jsou ID, časová razítka nebo URL. Kombinuje vizuální ověření s automatickým skenováním, což jej činí ideálním pro inventarizaci, soulad a automatizaci pracovních toků s vysokým objemem.

## Proč přidat čárový kód jako podpis pomocí GroupDocs.Signature Java?
GroupDocs.Signature podporuje **více než 50** vstupních a výstupních formátů, zpracovává PDF s mnoha stovkami stran bez načítání celého souboru do paměti a poskytuje plynulé Java API, které vám umožní jemně doladit každý vizuální aspekt čárového kódu. V benchmarkových testech trvá podepsání 150‑stránkového PDF s čárovým kódem Code128 **méně než 1,2 sekundy** na standardní cloudové instanci s 2 vCPU.

## Předpoklady
Před zahájením ověřte, že máte následující:

- **Java Development Kit (JDK)** 8 nebo novější (JDK 11 nebo 17 doporučeno pro dlouhodobou podporu)
- **IDE** (IntelliJ IDEA, Eclipse nebo VS Code s rozšířeními pro Java)
- **Nástroj pro sestavení** (Maven 3.6+ nebo Gradle 7.0+)
- **Knihovna GroupDocs.Signature Java** (ukážeme nastavení pro Maven a Gradle níže)
- Základní znalost OOP konceptů v Javě a struktury projektů Maven/Gradle

### Požadované knihovny a závislosti
GroupDocs.Signature se hladce integruje s Maven nebo Gradle. Vyberte si nástroj, který již používáte:

**Nastavení Maven**  
```markdown
```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```
```

**Nastavení Gradle**  
```markdown
```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```
```

Pokud dáváte přednost ručnímu zpracování JAR souborů, stáhněte si nejnovější vydání z [GroupDocs.Signature pro Java vydání](https://releases.groupdocs.com/signature/java/) a přidejte jej do své classpath.

### Kroky pro získání licence
GroupDocs nabízí tři licenční modely:

- **Free Trial** – Plný přístup ke všem funkcím po 30 dnů (vodoznak aplikovaný na podepsané PDF)
- **Temporary License** – Rozšířená zkušební verze bez omezení funkcí (ideální pro vývojové pipeline)
- **Full License** – Připravená pro produkci, zahrnuje prioritu podpory a žádné vodoznaky

Získejte vhodnou licenci na [GroupDocs Licensing](https://purchase.groupdocs.com/buy). I během zkušební verze můžete kód spouštět lokálně; jen nezapomeňte před nasazením nahradit zkušební klíč trvalým.

## Jak přidat čárový kód jako podpis do PDF pomocí GroupDocs.Signature Java?
Třída `Signature` je hlavním vstupním bodem pro práci s dokumenty v GroupDocs.Signature.
Třída `BarcodeSignOptions` určuje data čárového kódu, typ a vizuální vzhled.

Načtěte svůj zdrojový PDF pomocí `new Signature("source.pdf")`, nakonfigurujte objekt `BarcodeSignOptions` s požadovanými daty a vizuálním stylem a poté zavolejte `signature.sign("output.pdf", options)`. Tento tříkrokový vzor zpracovává souborové I/O, generování čárového kódu a zápis PDF v jediném, vlákny‑bezpečném volání a funguje pro PDF od několika kilobytů až po několik stovek megabytů.

### Krok 1: Inicializace objektu Signature
Třída `Signature` je vstupním bodem GroupDocs.Signature pro všechny operace podepisování. Reprezentuje jeden PDF dokument v paměti a poskytuje líné načítání, aby se udržovala nízká spotřeba paměti.

```markdown
```java
import com.groupdocs.signature.Signature;

public class InitializeSignature {
    public static void main(String[] args) {
        Signature signature = new Signature("YOUR_DOCUMENT_DIRECTORY/sample.pdf");
        System.out.println("GroupDocs.Signature initialized successfully.");
    }
}
```
```

**Vysvětlení:**  
- `filePath` ukazuje na zdrojový PDF, který chcete podepsat.  
- `outputFilePath` je místo, kam bude podepsaný PDF uložen, přičemž zachová původní soubor.  
- Blok `try‑catch` zajišťuje elegantní zpracování I/O chyb, chybějících souborů nebo problémů s oprávněním.

### Krok 2: Konfigurace možností čárového kódu
`BarcodeSignOptions` vám umožňuje definovat každý atribut čárového kódu — typ, data, pozici, barvy, okraje a dokonce i to, zda má být vrácen surový obrázek čárového kódu.

```markdown
```java
import com.groupdocs.signature.Signature;
import com.groupdocs.signature.exception.GroupDocsSignatureException;
import java.nio.file.Paths;
import java.io.File;

public class Feature1 {
    public static void run() throws Exception {
        String filePath = "YOUR_DOCUMENT_DIRECTORY/sample.pdf";
        String outputFilePath = new File("YOUR_OUTPUT_DIRECTORY", "SignedOutputSample.pdf").getPath();

        try {
            Signature signature = new Signature(filePath);
            System.out.println("Signature initialized and paths set.");
        } catch (Exception e) {
            throw new GroupDocsSignatureException(e.getMessage());
        }
    }
}
```
```

**Rozpis klíčových nastavení:**

- **Data & Typ** – `"12345678"` je náklad; `BarcodeTypes.Code128` funguje pro alfanumerické řetězce a je široce podporován skenery.  
- **Umístění** – `setLeft(100)` a `setTop(100)` posunou čárový kód o 100 px od levého horního rohu; `VerticalAlignment.Top` + `HorizontalAlignment.Right` upravují zarovnání vzhledem k těmto posunům.  
- **Okraje & Odsazení** – Objekt `Padding` přidává 20 px rezervu, aby se zabránilo oříznutí na okrajích stránky.  
- **Styling** – Okraj, font a pozadí jsou plně přizpůsobitelné; pro produkci můžete odstranit gradient pro zrychlení vykreslování.  
- **Vrácení obsahu** – Povolení `setReturnContent(true)` vám poskytne čárový kód jako `byte[]`, což je užitečné pro uložení obrázku v databázi nebo jeho zobrazení v UI.

#### Minimální konfigurace připravená pro produkci
Pro čistý právní dokument obvykle chcete jednoduchý černobílý čárový kód bez dalších okrajů:

```markdown
```java
import com.groupdocs.signature.domain.enums.*;
import com.groupdocs.signature.domain.Padding;
import com.groupdocs.signature.domain.Border;
import com.groupdocs.signature.domain.DashStyle;
import com.groupdocs.signature.domain.extensions.LinearGradientBrush;
import com.groupdocs.signature.domain.font.SignatureFont;
import java.awt.Color;
import com.groupdocs.signature.options.sign.BarcodeSignOptions;

public class Feature2 {
    public static void configureBarcodeOptions() throws Exception {
        BarcodeSignOptions signOptions = new BarcodeSignOptions("12345678");
        signOptions.setEncodeType(BarcodeTypes.Code128);
        signOptions.setLeft(100);
        signOptions.setTop(100);
        signOptions.setVerticalAlignment(VerticalAlignment.Top);
        signOptions.setHorizontalAlignment(HorizontalAlignment.Right);

        Padding padding = new Padding();
        padding.setLeft(20);
        padding.setTop(20);
        signOptions.setMargin(padding);

        Border border = new Border();
        border.setColor(Color.GREEN);
        border.setDashStyle(DashStyle.DashLongDashDot);
        border.setWeight(2);
        border.setTransparency(0.5);
        border.setVisible(true);
        signOptions.setBorder(border);

        signOptions.setForeColor(Color.RED);
        SignatureFont font = new SignatureFont();
        font.setSize(12);
        font.setFamilyName("Comic Sans MS");
        signOptions.setFont(font);

        signOptions.setCodeTextAlignment(CodeTextAlignment.Above);

        Background background = new Background();
        background.setColor(Color.GREEN);
        background.setTransparency(0.5);
        background.setBrush(new LinearGradientBrush(Color.GREEN, Color.DARK_GRAY, 0));
        signOptions.setBackground(background);

        signOptions.setReturnContent(true);
        signOptions.setReturnContentType(FileType.PNG);
    }
}
```
```

### Krok 3: Podepsání dokumentu
Metoda `sign` aplikuje nakonfigurovaný čárový kód na PDF a zapíše výsledek do cílové cesty.

```markdown
```java
signOptions.setEncodeType(BarcodeTypes.QR); // QR codes for more data
signOptions.setForeColor(Color.BLACK);
signOptions.setBackgroundColor(Color.WHITE);
// Remove border and fancy styling for professional appearance
```
```

**Pod povrchem:**  
- `signature.sign(outputFilePath, signOptions)` zapisuje čárový kód do PDF, přičemž zdroj zůstane nedotčen.  
- `SignResult` uvádí, kolik podpisů bylo přidáno, které stránky byly upraveny a jaká varování byla vygenerována.  
- Pro dávkové úlohy obalte toto volání do `ExecutorService`, aby se paralelizovalo napříč jádry CPU.

## Časté problémy a řešení

### Problém 1: FileNotFoundException při inicializaci
**Příznak:** Aplikace vyhodí `FileNotFoundException` při vytváření objektu `Signature`.

**Příčiny:**  
- Nesprávná cesta k souboru (relativní vs. absolutní)  
- Chybějící oprávnění ke čtení  
- Soubor je uzamčen jiným procesem (např. otevřen v Acrobat)

**Oprava:**  
```markdown
```java
import com.groupdocs.signature.Signature;
import com.groupdocs.signature.exception.GroupDocsSignatureException;
import com.groupdocs.signature.options.sign.BarcodeSignOptions;
import com.groupdocs.signature.domain.BaseSignature;

public class Feature3 {
    public static void signDocument(String filePath, BarcodeSignOptions signOptions) throws Exception {
        Signature signature = new Signature(filePath);
        String outputFilePath = filePath.replace(".pdf", "_Signed.pdf");

        try {
            com.groupdocs.signature.domain.signatures.SignResult signResult = signature.sign(outputFilePath, signOptions);
            System.out.println("Document signed successfully.");
        } catch (Exception e) {
            throw new GroupDocsSignatureException(e.getMessage());
        }
    }
}
```
```
Ujistěte se, že cesta používá lomítka (`C:/Docs/sample.pdf`) nebo escapované zpětné lomítka (`C:\\Docs\\sample.pdf`). Ověřte oprávnění OS a zavřete jakýkoli program, který by mohl soubor uzamknout.

### Problém 2: Čárový kód se neobjevuje ve výstupu
**Příznak:** Podepisování skončí bez chyb, ale čárový kód je neviditelný.

**Typické důvody:**  
- Umístění umístí čárový kód mimo tisknutelnou oblast.  
- Průhlednost nastavena na `1.0` (zcela průhledná).  
- Velikost fontu nastavena na `0`.

**Řešení:**  
- Udržujte hodnoty `setLeft`/`setTop` v rozměrech stránky (0‑600 px pro standardní A4).  
- Použijte hodnotu průhlednosti mezi `0.0` (neprůhledná) a `0.9`.  
- Nastavte čitelnou velikost fontu, např. `12pt`.

### Problém 3: Chyby Out of Memory u velkých dokumentů
**Příznak:** `OutOfMemoryError` při zpracování PDF větších než ~50 MB.

**Řešení:**  
- Zvyšte haldu JVM: `-Xmx2g` nebo vyšší v závislosti na velikosti dokumentu.  
- Zpracovávejte PDF stránku po stránce pomocí streaming API `Signature`.  
- Výslovně uzavřete instanci `Signature` po každé operaci, aby se uvolnily nativní zdroje.

```markdown
```java
import java.nio.file.Files;
import java.nio.file.Path;

Path filePath = Path.of("YOUR_DOCUMENT_DIRECTORY/sample.pdf");
if (!Files.exists(filePath)) {
    throw new IllegalArgumentException("PDF file not found: " + filePath);
}
if (!Files.isReadable(filePath)) {
    throw new SecurityException("Cannot read PDF file: " + filePath);
}
// Now safe to initialize
Signature signature = new Signature(filePath.toString());
```
```

### Problém 4: Chyba neplatných dat čárového kódu
**Příznak:** API vyhodí výjimku s výčtem nepodporovaných znaků.

**Příčina:** Různé standardy čárových kódů akceptují různé znakové sady. Code128 umožňuje alfanumerické řetězce; QR může zpracovat Unicode; některé 1D kódy akceptují pouze číslice.

**Řešení:** Vyberte typ čárového kódu, který odpovídá vašemu datovému souboru, nebo očistěte řetězec před přiřazením do `BarcodeSignOptions`.

```markdown
```java
String barcodeData = "ABC123"; // Your data
BarcodeTypes type = BarcodeTypes.Code128; // Alphanumeric support

// For numeric-only barcodes, validate first:
if (type == BarcodeTypes.EAN13 && !barcodeData.matches("\\d+")) {
    throw new IllegalArgumentException("EAN13 requires numeric data only");
}
```
```

## Nejlepší postupy pro produkci

### 1. Ověření PDF před podepsáním
Vždy ověřte, že soubor je dobře vytvořený PDF, aby se předešlo chybám při parsování za běhu.

```markdown
```java
try (Signature signature = new Signature(filePath)) {
    // If this succeeds, file is valid
    signature.getDocumentInfo();
} catch (Exception e) {
    // Handle invalid PDF
}
```
```

### 2. Použití asynchronního zpracování pro vysokozátěžové úlohy
Přesuňte podepisování do poolu vláken na pozadí; to zabraňuje zamrznutí UI a zvyšuje propustnost.

```markdown
```java
ExecutorService executor = Executors.newFixedThreadPool(4);
List<String> pdfFiles = Arrays.asList("doc1.pdf", "doc2.pdf", "doc3.pdf");

pdfFiles.forEach(file -> {
    executor.submit(() -> {
        try {
            signDocument(file, signOptions);
        } catch (Exception e) {
            // Log error
        }
    });
});
executor.shutdown();
```
```

### 3. Implementace strukturovaného logování
Logujte každý požadavek na podepsání s cestou vstupu, cestou výstupu, daty čárového kódu a případnými výjimkami. To výrazně urychlí analýzu po události.

```markdown
```java
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

private static final Logger logger = LoggerFactory.getLogger(YourClass.class);

try {
    SignResult result = signature.sign(outputFilePath, signOptions);
    logger.info("Document signed successfully: {}", outputFilePath);
    logger.debug("Signatures added: {}", result.getSucceeded().size());
} catch (Exception e) {
    logger.error("Failed to sign document: {}", filePath, e);
}
```
```

### 4. Optimalizace nastavení čárového kódu pro rychlost
- Zakázat `setReturnContent(true)`, pokud nepotřebujete obrázek samostatně.  
- Upřednostňovat plné pozadí před gradienty.  
- Vynechat okraje pro jednoduché sledovací případy.

### 5. Elegantní handling vypršení dočasné licence
Třída `License` načítá a ověřuje licenční soubor GroupDocs pro API.
Zkontrolujte stav licence před každou operací podepisování a v případě potřeby přejděte do režimu jen pro čtení nebo upozorněte správce.

```markdown
```java
try {
    License license = new License();
    license.setLicense(licensePath);
} catch (Exception e) {
    logger.warn("License validation failed. Using trial mode.");
    // Continue with trial limitations
}
```
```

## Kdy použít čárové kódy jako podpisy

### Ideální scénáře
- **Inventář & logistika:** Připojte skenovatelný čárový kód k přepravním listům, balicím seznamům nebo štítkům majetku.  
- **Regulační soulad:** Odvětví jako farmacie vyžadují strojově čitelné auditní stopy.  
- **Automatizované dokumentové pipeline:** Kombinujte čárové kódy s OCR pro umožnění end‑to‑end zpracování bez ručního zadávání dat.  
- **Dávkové úlohy s vysokým objemem:** Čárové kódy jsou rychlejší na ověření než kryptografické digitální podpisy při skenování velkých papírových archivů.

### Kdy upřednostnit jiné typy podpisů
- **Právní smlouvy:** Použijte PKI‑založené digitální podpisy (např. X.509) pro neodmítnutelnost.  
- **PDF určené zákazníkům:** QR kódy jsou na mobilních zařízeních lépe rozpoznatelné.  
- **Ultra‑bezpečné dokumenty:** Spojte čárový kód s šifrovaným digitálním podpisem pro vrstvenou bezpečnost.

> **Tip:** Můžete vložit více typů podpisů do jednoho PDF — přidejte čárový kód pro sledování a digitální certifikát pro právní vynutitelnost.

## Často kladené otázky

**Q: Jak přidat čárový kód jako podpis do PDF v Javě bez externích závislostí?**  
A: GroupDocs.Signature pro Java je samostatná; po přidání Maven/Gradle artefaktu získáte kompletní generování čárových kódů a renderování PDF bez jakýchkoli knihoven třetích stran.

**Q: Mohu v Javě konfigurovat možnosti čárového kódu pro generování QR kódů?**  
A: Rozhodně. Přepněte enum `BarcodeTypes` na `QRCode` a podle potřeby upravte parametry velikosti.

```markdown
```java
signOptions.setEncodeType(BarcodeTypes.QR);
```
```

**Q: Jaké je doporučené nastavení Maven pro produkční použití?**  
A: Připevněte přesnou verzi v `pom.xml` (např. `23.10.0`), aby se předešlo nechtěným aktualizacím, a povolte Maven plugin `shade` pro vytvoření jediného spustitelného JAR.

```markdown
```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version> <!-- Don't use LATEST -->
</dependency>
```
```

**Q: Podporuje knihovna PDF chráněné heslem?**  
A: Ano. Poskytněte heslo při vytváření objektu `Signature` a poté pokračujte v podepisování jako obvykle.

```markdown
```java
LoadOptions loadOptions = new LoadOptions();
loadOptions.setPassword("your_pdf_password");
Signature signature = new Signature(filePath, loadOptions);
```
```

**Q: Kolik stránek mohu podepsat v jedné operaci?**  
A: GroupDocs.Signature může adresovat všechny stránky PDF najednou nebo cílit konkrétní stránky pomocí `setPageNumber()`. Výkon roste lineárně; 200‑stránkový PDF se podepíše za ~2 sekundy na typické cloudové VM.

**Q: Jaké formáty čárových kódů jsou k dispozici kromě Code128?**  
A: Více než 30 formátů, včetně QR, DataMatrix, Aztec, UPC‑A, EAN‑13, PDF417 a dalších. Pro úplný seznam nahlédněte do enumu `BarcodeTypes`.

**Q: Existuje limit na délku dat čárového kódu?**  
A: Limity délky závisí na typu čárového kódu; pro Code128 je praktický limit 80 znaků, zatímco QR kódy mohou uložit až 4 KB dat.

**Q: Mohu po podepsání získat vygenerovaný obrázek čárového kódu?**  
A: Nastavte `setReturnContent(true)` a `setReturnContentType(FileType.PNG)`; `SignResult` bude obsahovat `byte[]`, který můžete zapsat na disk nebo do databáze.

**Poslední aktualizace:** 2026-07-25  
**Testováno s:** GroupDocs.Signature 23.10 pro Java  
**Autor:** GroupDocs

## Související tutoriály

- [Jak přidat digitální podpis v Javě - kompletní tutoriál GroupDocs](/signature/java/getting-started/groupdocs-signature-java-digital-setup-guide/)
- [Přidat QR kód do PDF v Javě - kompletní tutoriál GroupDocs](/signature/java/qr-code-signatures/qr-code-signature-generation-java-groupdocs/)
- [Přidat textový podpis do PDF v Javě - kompletní tutoriál GroupDocs](/signature/java/text-signatures/implement-text-signatures-groupdocs-java/)