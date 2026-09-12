---
categories:
- Java Development
- Document Management
date: '2026-08-25'
description: Naučte se, jak přidat barcode do PDF dokumentů v Java pomocí GroupDocs.Signature.
  Tento krok‑za‑krokem průvodce ukazuje, jak přidat GS1DotCode barcode, extrahovat
  obrázky a vyhnout se běžným úskalím.
keywords:
- how to add barcode
- groupdocs signature java
- pdf document barcode
lastmod: '2026-08-25'
linktitle: Přidat Barcode do PDF Java
og_description: Naučte se, jak přidat barcode do PDF v Java s GroupDocs.Signature.
  Krok‑za‑krokem tutoriál, příklady kódu a tipy na řešení problémů pro GS1DotCode
  barcode.
og_image_alt: Guide showing Java code to embed GS1DotCode barcode into a PDF using
  GroupDocs.Signature
og_title: Jak přidat barcode do PDF v Java – Kompletní průvodce
schemas:
- author: GroupDocs
  dateModified: '2026-08-25'
  description: Learn how to add barcode to PDF documents in Java using GroupDocs.Signature.
    This step‑by‑step guide shows how to add GS1DotCode barcodes, extract images,
    and avoid common pitfalls.
  headline: How to Add Barcode to PDF in Java
  type: TechArticle
- description: Learn how to add barcode to PDF documents in Java using GroupDocs.Signature.
    This step‑by‑step guide shows how to add GS1DotCode barcodes, extract images,
    and avoid common pitfalls.
  name: How to Add Barcode to PDF in Java
  steps:
  - name: Validate GS1 payloads before encoding.
    text: Validate GS1 payloads before encoding.
  - name: Choose barcode dimensions that balance scan reliability with layout constraints.
    text: Choose barcode dimensions that balance scan reliability with layout constraints.
  - name: Combine barcode signatures with cryptographic signatures for full security
      coverage.
    text: Combine barcode signatures with cryptographic signatures for full security
      coverage.
  type: HowTo
- questions:
  - answer: GS1DotCode is a compact 2‑D dot matrix that stores up to **3,116 characters**
      in a smaller footprint than QR codes, making it ideal for tiny labels and high‑speed
      printing.
    question: What is GS1DotCode and why is it different from QR codes?
  - answer: The free trial is limited to evaluation and adds a watermark to output
      files. Production use requires a purchased or temporary 30‑day license.
    question: Can I use a free trial for production deployments?
  - answer: Set `setPageNumber(pageIndex)` on the `BarcodeSignOptions` object, then
      adjust `setLeft()` and `setTop()` to place it precisely.
    question: How do I position the barcode on a specific page?
  - answer: 'Yes. Provide the password when constructing the `Signature` object: `new
      Signature("file.pdf", "password")`.'
    question: Does GroupDocs.Signature support password‑protected PDFs?
  - answer: Aim for at least **108 pt × 108 pt** (1.5 in × 1.5 in). Larger sizes improve
      readability, especially on low‑resolution printers.
    question: What is the minimum barcode size for reliable scanning?
  type: FAQPage
tags:
- java
- pdf-signing
- barcodes
- groupdocs
- document-security
title: Jak přidat Barcode do PDF v Java
type: docs
url: /cs/java/digital-signatures/master-java-document-signing-groupdocs-signature/
weight: 1
---

# Jak přidat čárový kód do PDF v Javě

## Úvod

Už jste se někdy potýkali s ověřováním pravosti dokumentů ve své Java aplikaci? Nejste sami. Ať už budujete inventární systém, spravujete smlouvy nebo pracujete s dokumenty dodavatelského řetězce, je pravděpodobné, že potřebujete spolehlivý způsob, jak automaticky podepisovat a ověřovat PDF soubory.

Tradiční digitální podpisy jsou skvělé, ale někdy potřebujete něco specializovanějšího – například čárové kódy, které fungují bez problémů se skenovacími systémy a automatizovanými pracovními postupy. Právě zde se hodí čárové kódy GS1DotCode.

**Co se naučíte:**
- Jak podepsat PDF dokumenty pomocí čárových kódů GS1DotCode v Javě
- Jak extrahovat a uložit obrázky podpisu čárového kódu
- Kdy (a proč) použít podpisy čárových kódů místo tradičních metod
- Běžné úskalí a jak se jim vyhnout

Na konci tohoto průvodce budete mít připravené řešení, které můžete integrovat do jakéhokoli Java projektu.

## Rychlé odpovědi
- **Která knihovna přidává čárové kódy do PDF v Javě?** GroupDocs.Signature for Java.
- **Jaký formát čárového kódu je podporován?** GS1DotCode, kompaktní 2‑D matice bodů.
- **Potřebuji placenou licenci?** Bezplatná zkušební verze funguje pro testování; pro produkci je vyžadována komerční licence.
- **Mohu extrahovat čárový kód jako obrázek?** Ano, pomocí API `BarcodeSignature`.
- **Jaká verze Javy je vyžadována?** JDK 8 nebo vyšší.

## Co je přidání čárového kódu?
*Jak přidat čárový kód* označuje proces programového vložení grafiky strojově čitelného čárového kódu do PDF souboru tak, aby se čárový kód stal součástí obsahového proudu dokumentu. To zahrnuje generování obrázku čárového kódu, jeho umístění na stránku a uložení upraveného PDF, přičemž se zajistí, že čárový kód zůstane vyhledávatelný a tisknutelný.

## Proč zvolit čárové kódy GS1DotCode?
GS1DotCode je navržen pro situace, kde je málo místa. Na rozdíl od lineárních čárových kódů, které se táhnou horizontálně, DotCode vytváří 2‑D matici bodů, která do malého prostoru zabaluje spoustu informací. To z něj dělá ideální volbu pro:

- **Malé produktové štítky** kde každý milimetr se počítá  
- **Vysokorychlostní tisk** na výrobních linkách (formát je pro to navržen)  
- **Sledování dodavatelského řetězce** kde potřebujete kódovat složité datové struktury  

Formát může v kompaktním prostoru zpracovat až **3 116 znaků** a čte spolehlivě i při vysokých rychlostech nebo s částečným poškozením. Pokud pracujete v maloobchodu nebo logistice, vaši partneři pravděpodobně již používají standardy GS1 – takže mluvíte stejným jazykem.

> **Tip:** Použijte GS1DotCode, když potřebujete vložit více než 20 znaků na štítek menší než 1 palec × 1 palec.

## Předpoklady

Než začnete kódovat, ověřte, že vaše prostředí splňuje následující požadavky.

### Požadované knihovny a závislosti
- **GroupDocs.Signature for Java** 23.12 nebo novější (podporuje **30+** formátů dokumentů)
- Maven nebo Gradle pro správu závislostí

### Nastavení prostředí
- **JDK 8** nebo novější nainstalovaný a nakonfigurovaný ve vašem `PATH`
- IDE jako IntelliJ IDEA, Eclipse nebo NetBeans
- Ukázkový PDF soubor pro experimentování (libovolný nechráněný PDF bude stačit)

### Předpoklady znalostí
- Základní syntaxe Javy (proměnné, metody, objekty)
- Znalost deklarace závislostí v Maven nebo Gradle
- Porozumění souborovému I/O v Javě (např. `FileInputStream`)

Pokud některá z těchto položek chybí, pozastavte se a nainstalujte je nyní; pozdější kroky předpokládají, že jsou přítomny.

## Nastavení GroupDocs.Signature pro Java

### Maven
If you’re using Maven, add the following dependency to your `pom.xml`:

```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

Maven automatically downloads the library and all required transitive dependencies.

### Gradle
For Gradle users, insert this line into your `build.gradle` file:

```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

Gradle resolves the package in the same hands‑off manner.

### Přímé stažení
If you prefer manual management, download the JAR files from the official release page: [GroupDocs.Signature for Java releases](https://releases.groupdocs.com/signature/java/). Place the JARs on your project’s classpath.

**Tip:** Maven nebo Gradle zjednodušuje budoucí aktualizace – stačí zvýšit číslo verze.

### Získání licence
GroupDocs offers three licensing options:

- **Bezplatná zkušební verze** – bez kreditní karty, na výstup jsou aplikovány vodoznaky
- **Dočasná licence** – 30‑denní plnofunkční hodnocení
- **Komerční licence** – odstraňuje omezení zkušební verze a poskytuje práva pro produkci

After obtaining a license file, place it in your project’s resources folder and load it before any `Signature` object is created.

`License.setLicense` načte licenční soubor GroupDocs, umožňující plnofunkční provoz bez omezení zkušební verze.

Run the following snippet to verify the library loads correctly:

```java
import com.groupdocs.signature.Signature;

public class InitializeGroupDocs {
    public static void main(String[] args) {
        // Create an instance of Signature
        Signature signature = new Signature("path/to/your/document.pdf");
        
        System.out.println("Initialization successful!");
    }
}
```

If you see “Initialization successful!” the setup is complete. Otherwise, double‑check the classpath and license path.

## Průvodce implementací

We’ll cover two core features: (1) signing a PDF with a GS1DotCode barcode and (2) extracting that barcode as an image file.

### Funkce 1: podepsat dokument čárovým kódem GS1DotCode

#### Jak podepsat PDF čárovým kódem GS1DotCode v Javě?

Load the target PDF with `new Signature("source.pdf")`, configure a `BarcodeSignOptions` object containing GS1‑formatted data, and call `sign()` to produce a new PDF that embeds the barcode. This operation writes the barcode directly into the PDF content stream, preserving it through printing and rescanning.

The process involves three concise steps: create a `Signature` instance, set up `BarcodeSignOptions`, and invoke `sign()`. The code below demonstrates each step.

##### 1. inicializace objektu signature
The `Signature` class is the entry point for all document‑processing operations in GroupDocs.Signature.

```java
import com.groupdocs.signature.Signature;

String sourceFilePath = "YOUR_DOCUMENT_DIRECTORY/document.pdf";
final Signature signature = new Signature(sourceFilePath);
```

> **Proč je to důležité:** Objekt `Signature` abstrahuje práci se soubory, efektivně streamuje velké PDF bez načítání celého souboru do paměti.

##### 2. konfigurace možností čárového kódu
`BarcodeSignOptions` vám umožňuje specifikovat typ čárového kódu, kódovaná data, pozici a rozměry.

```java
import com.groupdocs.signature.domain.signatures.BarcodeSignature;
import com.groupdocs.signature.options.sign.BarcodeSignOptions;
import com.groupdocs.signature.domain.barcodes.BarcodeTypes;

BarcodeSignOptions gs1DotCodeOptions = new BarcodeSignOptions("(01)04912345123459(15)970331(30)128(10)ABC123", BarcodeTypes.GS1DotCode);
gs1DotCodeOptions.setLeft(100); // Set barcode position
gs1DotCodeOptions.setTop(100);
gs1DotCodeOptions.setHeight(150);
gs1DotCodeOptions.setWidth(200);
```

> **Key points:**  
> - Kódovaný řetězec následuje identifikátory aplikací GS1 (AI) jako `(01)` pro GTIN, `(15)` pro datum expirace, atd.  
> - `setLeft()` a `setTop()` používají body (72 pt = 1 in).  
> - Minimální doporučená velikost pro spolehlivé skenování je **108 pt × 108 pt** (1,5 in × 1,5 in).

##### 3. podepsání dokumentu
Add the configured options to a list (you can combine multiple signature types) and call `sign()`.

```java
import java.util.ArrayList;
import java.util.List;

List<com.groupdocs.signature.options.sign.SignOptions> listOptions = new ArrayList<>();
listOptions.add(gs1DotCodeOptions);
signature.sign("YOUR_OUTPUT_DIRECTORY/signed_document_with_gs1dotcode.pdf", listOptions);
```

> **Performance note:** Opakované používání jedné instance `Signature` pro dávkové operace snižuje režii vytváření objektů a zvyšuje propustnost.

### Funkce 2: uložit obsah podpisu čárového kódu do souboru

#### Jak extrahovat obrázek čárového kódu ze podepsaného PDF v Javě?

`BarcodeSignature` představuje objekt podpisu čárového kódu extrahovaný ze podepsaného dokumentu, poskytující přístup k jeho datům a obsahu obrázku.

Create a `BarcodeSignature` instance (or retrieve one via `search()`), read its Base64‑encoded image data via `getContent()`, decode it, and write the bytes to a PNG file. This yields a standalone image you can display in a UI or send to a label printer.

##### 1. simulace vytvoření podpisu čárového kódu
In real scenarios you would obtain the `BarcodeSignature` from a search result; here we instantiate it manually for illustration.

```java
import com.groupdocs.signature.domain.signatures.BarcodeSignature;
import java.io.FileOutputStream;

String base64String = "SampleBase64EncodedData";
BarcodeSignature barcodeSignature = new BarcodeSignature(base64String);
```

##### 2. uložení obsahu do souboru
Decode the Base64 string and write the resulting bytes to disk using a try‑with‑resources block.

```java
int imageNumber = 1;
String formatExtension = ".png";  // Assume PNG format

try (FileOutputStream outputStream = new FileOutputStream("YOUR_OUTPUT_DIRECTORY/barcode_image" + imageNumber + formatExtension)) {
    byte[] byteArray = barcodeSignature.getContent();
    if (byteArray != null) {
        outputStream.write(byteArray);
    }
}
```

> **Gotcha:** `getContent()` může vrátit `null`, pokud byl podpis vytvořen bez vložení obrázku. Vždy před zápisem zkontrolujte, zda není `null`.

## Časté problémy a řešení

### Problém: čárový kód se nenačte
**Příznaky:**
- Čárový kód vypadá v prohlížeči PDF v pořádku, ale skenery vracejí chyby.

**Řešení:**
- Zvyšte velikost čárového kódu alespoň na **108 pt × 108 pt**.  
- Zajistěte, aby rozlišení tiskárny bylo **≥ 300 dpi**.  
- Ověřte, že řetězec GS1 dat dodržuje správnou syntaxi AI; chybějící závorka rozbije skener.

### Problém: OutOfMemoryError u velkých PDF
**Příznaky:**
- Zpracování dokumentů větších než **50 MB** spouští selhání paměti haldy.

**Řešení:**
- Spusťte JVM s větší haldou, např. `-Xmx2g`.  
- Zpracovávejte dokumenty v menších dávkách.  
- Explicitně uvolněte objekty `Signature`: `signature.dispose()` po každém souboru.

### Problém: čárový kód je rozmazaný
**Příznaky:**
- Vykreslený čárový kód v PDF výstupu vypadá pixelovaně.

**Řešení:**
- Použijte větší rozměry; knihovna vykresluje vektorovou grafiku, pokud je to možné, ale zmenšování po generování zavádí artefakty.  
- Vyhněte se konverzím raster‑vektor; nechte GroupDocs provádět vykreslování přímo z vektorové definice.

### Problém: výjimky licence
**Příznaky:**
- Chyby jako „License not found“ nebo „Trial limitations exceeded“.

**Řešení:**
- Umístěte licenční soubor do kořene classpath (`src/main/resources`).  
- Zavolejte `License.setLicense("GroupDocs.Signature.lic")` **před** jakoukoliv instancí `Signature`.  
- U dočasných licencí ověřte datum expirace (30 dnů od vydání).

## Kdy použít tento přístup

### Vhodné případy použití
- **Sledování dodavatelského řetězce** – vložit ID produktů, čísla šarží a data expirace přímo na přepravní dokumenty.  
- **Automatizovaný tisk štítků** – generovat čárové kódy za běhu pro každou PDF fakturu.  
- **Regulované odvětví** – standardy GS1 jsou povinné v mnoha maloobchodních a zdravotnických prostředích.

### Kdy zvážit alternativy
- Pokud potřebujete pouze kryptografickou integritu, standardní PKI digitální podpis je vhodnější.  
- Pro jednoduché vizuální anotace může stačit textový podpis nebo obrázková razítko.  
- Když je velikost dokumentu kritickým omezením, vyhněte se přidávání vysoce rozlišených obrázků čárových kódů; místo toho použijte QR kódy, které mohou být menší při srovnatelné datové hustotě.

## Bezpečnostní osvědčené postupy

### Validace dat
Očistěte všechna uživatelem poskytnutá data před jejich zakódováním do čárového kódu. Špatně formátované řetězce GS1 mohou způsobit chyby skenování v následných systémech nebo v nejhorším případě vyvolat přetečení bufferu ve starém firmware skeneru.

### Řízení přístupu
Implementujte řízení přístupu založené na rolích (RBAC), aby pouze oprávnění uživatelé mohli volat API pro podepisování. Uložte licenční soubor bezpečně a omezte oprávnění souborového systému.

### Auditní logování
Logujte každou operaci podepisování s podrobnostmi jako ID uživatele, časové razítko, cesta ke zdrojovému souboru a přesný GS1 payload. Příklad logovacího úryvku:

```java
// Simple logging example (use a proper logging framework in production)
System.out.println("Document signed by: " + userId + " at " + new Date());
System.out.println("Barcode data: " + barcodeData);
```

### Detekce manipulace
Kombinujte podpis čárového kódu s kryptografickým digitálním podpisem. Čárový kód poskytuje strojově čitelná data, zatímco digitální podpis zaručuje integritu a nezpochybnitelnost.

## Praktické aplikace

### 1. řízení dodavatelského řetězce
Každý balicí list dostane čárový kód GS1DotCode kódující GTIN zásilky, šarži a destinaci. Skenery na každém kontrolním bodě automaticky aktualizují ERP systém, čímž snižují chyby ručního zadávání o **98 %**.

### 2. řízení zásob
Když zboží dorazí, přijímací PDF je podepsáno čárovým kódem, který obsahuje číslo objednávky (PO) a množství položek. Skladový personál skenuje čárový kód a databáze zásob se aktualizuje v reálném čase.

### 3. maloobchodní pokladna
Faktury vytisknuté s čárovým kódem umožňují pokladníkům zpracovávat vrácení skenováním faktury místo ručního zadávání ID transakce, čímž se průměrná doba pokladny zkrátí o **30 sekund** na vrácení.

### 4. zdravotnická dokumentace
Předpisy podepsané čárovým kódem GS1DotCode obsahují ID pacienta, kód léku a pokyny k dávkování. Lékárny skenují čárový kód, čímž eliminují chyby při přepisování, které způsobují nepříznivé události související s léky.

## Výkonnostní úvahy

### Správa paměti
GroupDocs.Signature streams PDF data, but you should still close resources promptly:

```java
try (Signature signature = new Signature(sourceFilePath)) {
    // Do your signing operations here
} // Signature automatically disposed here
```

Using try‑with‑resources guarantees the `Signature` object releases file handles even if an exception occurs.

### Tipy pro dávkové zpracování
- Znovu použijte stejnou instanci `BarcodeSignOptions`, když je náklad identický napříč mnoha dokumenty.  
- Paralelizujte podepisování pomocí `ExecutorService` pro CPU‑intenzivní úlohy; typický 8‑jádrový server může podepsat **≈ 150 PDF za minutu**, pokud je každý soubor menší než 5 MB.  
- Omezte externí volání ověření licence, aby nedošlo k omezení rychlosti.

### Optimalizace formátu souboru
- Upřednostněte PDF/A‑1b pro archivaci; komprimuje proudy a snižuje velikost souboru až o **40 %**.  
- Udržujte rozměry čárového kódu nevětší než je nutné; čárový kód 1,5 in × 1,5 in přidá přibližně **15 KB** k PDF o velikosti 2 MB.

## Závěr

You now have a complete, production‑ready workflow for adding GS1DotCode barcode signatures to PDF files in Java, extracting those barcodes as images, and integrating the process into larger document‑management pipelines. Remember to:

1. Ověřte GS1 náklady před kódováním.  
2. Zvolte rozměry čárového kódu, které vyvažují spolehlivost skenování s omezeními rozvržení.  
3. Kombinujte podpisy čárových kódů s kryptografickými podpisy pro kompletní zabezpečení.

Další kroky: prozkoumejte další typy podpisů nabízené GroupDocs.Signature – QR kódy, textová razítka a digitální certifikáty – všechny sdílejí konzistentní API.

---

## Často kladené otázky

**Q: Co je GS1DotCode a proč se liší od QR kódů?**  
A: GS1DotCode je kompaktní 2‑D matice bodů, která ukládá až **3 116 znaků** v menším prostoru než QR kódy, což ji činí ideální pro malé štítky a vysokorychlostní tisk.

**Q: Mohu použít bezplatnou zkušební verzi pro produkční nasazení?**  
A: Bezplatná zkušební verze je omezena na hodnocení a přidává vodoznak do výstupních souborů. Pro produkční použití je vyžadována zakoupená nebo dočasná 30‑denní licence.

**Q: Jak umístit čárový kód na konkrétní stránku?**  
A: Nastavte `setPageNumber(pageIndex)` na objektu `BarcodeSignOptions`, poté upravte `setLeft()` a `setTop()` pro přesné umístění.

**Q: Podporuje GroupDocs.Signature PDF soubory chráněné heslem?**  
A: Ano. Zadejte heslo při vytváření objektu `Signature`: `new Signature("file.pdf", "password")`.

**Q: Jak mohu ověřit, že byl podpis čárového kódu přidán správně?**  
`Signature.search()` prohledá dokument na podpisy a vrátí kolekci odpovídajících objektů podpisu. Použijte `Signature.search()` s `BarcodeSearchOptions`. Vrácené objekty `BarcodeSignature` obsahují zakódovaná data a obsah obrázku pro ověření.

**Q: Jaká je minimální velikost čárového kódu pro spolehlivé skenování?**  
A: Cílem je alespoň **108 pt × 108 pt** (1,5 in × 1,5 in). Větší velikosti zlepšují čitelnost, zejména na tiskárnách s nízkým rozlišením.

**Q: Mohu podepisovat více PDF souborů současně?**  
A: Ano. Vytvořte pool vláken a pro každé vlákno vytvořte samostatný objekt `Signature`; knihovna je bezpečná pro vlákna, pokud každé vlákno pracuje na svém vlastním dokumentu.

**Q: Existuje limit, kolik čárových kódů mohu vložit do jednoho PDF?**  
A: Neexistuje pevný limit, ale každý čárový kód přidá přibližně **15 KB** dat. Pro PDF větší než **100 MB** zvažte dávkové zpracování pro správu využití paměti.

**Q: Funguje knihovna na ne‑Windows platformách?**  
A: GroupDocs.Signature for Java je platformově nezávislá a běží na jakémkoli OS s kompatibilní JRE, včetně Linuxu a macOS.

**Poslední aktualizace:** 2026-08-25  
**Testováno s:** GroupDocs.Signature 23.12 for Java  
**Autor:** GroupDocs

## Související tutoriály

- [Jak ověřit podpisy čárových kódů v Javě pomocí GroupDocs.Signature](/signature/java/barcode-signatures/verify-barcode-signatures-groupdocs-signature-java/)
- [Vytvořit podpis čárového kódu v Javě – aktualizovat PDF čárové kódy](/signature/java/barcode-signatures/java-groupdocs-signature-barcode-initialize-update/)
- [Přidat QR kód do PDF v Javě – kompletní průvodce s GroupDocs.Signature](/signature/java/qr-code-signatures/qr-code-signatures-java-groupdocs/)