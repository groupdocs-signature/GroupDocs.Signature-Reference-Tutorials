---
date: '2026-07-15'
description: Zjistěte, jak přidat čárový kód PDF Java pomocí GroupDocs.Signature –
  podrobný průvodce krok za krokem pro podepisování, ověřování, vyhledávání, aktualizaci
  a mazání podpisů čárových kódů v Java dokumentech.
keywords:
- add barcode pdf java
- groupdocs barcode signature
- java document signing
lastmod: '2026-07-15'
linktitle: Průvodce podpisem čárového kódu v Javě
og_description: Zjistěte, jak přidat čárový kód PDF Java pomocí GroupDocs.Signature
  – podrobný průvodce krok za krokem pro podepisování, ověřování, vyhledávání, aktualizaci
  a mazání podpisů čárových kódů v Java dokumentech.
og_image_alt: Guide showing how to add barcode PDF Java using GroupDocs.Signature
og_title: Přidání čárového kódu PDF Java – podepisování a ověřování pomocí GroupDocs
schemas:
- author: GroupDocs
  dateModified: '2026-07-15'
  description: Learn how to add barcode PDF Java using GroupDocs.Signature – step‑by‑step
    guide to sign, verify, search, update and delete barcode signatures in Java documents.
  headline: Add Barcode PDF Java – Sign & Verify with GroupDocs
  type: TechArticle
- description: Learn how to add barcode PDF Java using GroupDocs.Signature – step‑by‑step
    guide to sign, verify, search, update and delete barcode signatures in Java documents.
  name: Add Barcode PDF Java – Sign & Verify with GroupDocs
  steps:
  - name: Case mismatch (e.g., “John Smith” vs. “john smith”).
    text: Case mismatch (e.g., “John Smith” vs. “john smith”).
  - name: Extra whitespace in the encoded text.
    text: Extra whitespace in the encoded text.
  - name: Wrong barcode type specified in the verification options.
    text: Wrong barcode type specified in the verification options.
  - name: Searching the wrong page number.
    text: Searching the wrong page number.
  - name: '**Reuse Signature Instances** – Create a single `Signature` object per
      document and reuse it for multiple operations.'
    text: '**Reuse Signature Instances** – Create a single `Signature` object per
      document and reuse it for multiple operations.'
  - name: '**Search Specific Pages Only** – Limit the page range to where barcodes
      are expected.'
    text: '**Search Specific Pages Only** – Limit the page range to where barcodes
      are expected.'
  - name: '**Choose the Simplest Barcode Type** – Simpler barcodes generate faster;
      only use QR or Data Matrix when you truly need the extra capacity.'
    text: '**Choose the Simplest Barcode Type** – Simpler barcodes generate faster;
      only use QR or Data Matrix when you truly need the extra capacity.'
  - name: '**Never Encode Sensitive Personal Data** – Barcodes are easily readable;
      avoid PII such as SSNs or passwords.'
    text: '**Never Encode Sensitive Personal Data** – Barcodes are easily readable;
      avoid PII such as SSNs or passwords.'
  - name: '**Validate Server‑Side** – Never trust client‑side verification alone;
      always re‑verify on a trusted backend.'
    text: '**Validate Server‑Side** – Never trust client‑side verification alone;
      always re‑verify on a trusted backend.'
  - name: '**Add Timestamps** – Include a timestamp in the barcode payload to prevent
      replay attacks.'
    text: '**Add Timestamps** – Include a timestamp in the barcode payload to prevent
      replay attacks.'
  type: HowTo
- questions:
  - answer: Yes – the library is fully compatible with JDK 8, 11, and 17.
    question: Can I use GroupDocs.Signature with Java 17?
  - answer: When you use Code128 or QR with sufficient size and contrast, the barcode
      remains scannable after printing and scanning.
    question: Does the barcode survive a print‑scan cycle?
  - answer: There is no hard limit; however, for optimal performance keep the total
      count below **200** per document.
    question: How many barcodes can a single document contain?
  - answer: A temporary license removes evaluation watermarks; a full license is mandatory
      for any production deployment.
    question: Is a license required for development builds?
  - answer: Yes – provide the password when creating the `Signature` object; the API
      will unlock the file internally.
    question: Can I sign password‑protected PDFs?
  type: FAQPage
tags:
- barcode signature
- groupdocs
- java
- pdf
- document signing
title: Přidání čárového kódu PDF Java – podepisování a ověřování pomocí GroupDocs
type: docs
url: /cs/java/digital-signatures/java-document-signature-groupdocs-signature-barcode/
weight: 1
---

# Přidání čárového kódu PDF v Javě – Podepisování a ověřování pomocí GroupDocs

Pokud potřebujete rychlý, vizuální způsob, jak označit dokumenty pro interní workflow, přidání čárového kódu do PDF v Javě je ideální řešení. S **GroupDocs.Signature** můžete vkládat, ověřovat, vyhledávat, aktualizovat a mazat čárové podpisy bez zátěže plných PKI‑založených digitálních podpisů. Tento tutoriál vás provede každým krokem, od nastavení prostředí až po osvědčené postupy připravené pro produkci.

## Rychlé odpovědi
- **Jaká knihovna přidává čárový kód do PDF v Javě?** GroupDocs.Signature for Java.  
- **Mohu podepisovat PDF, Word a obrázky?** Ano – API podporuje více než 30 formátů.  
- **Potřebuji licenci pro vývoj?** Dočasná 30‑denní licence je zdarma; plná licence je vyžadována pro produkci.  
- **Kolik řádků kódu je potřeba k podepsání PDF?** Pouze dva řádky: vytvořit objekt `Signature` a zavolat `sign`.  
- **Je ověřování čárového kódu citlivé na velikost písmen?** Ano – text se musí přesně shodovat, včetně velikosti písmen a mezer.

## Co je přidání čárového kódu PDF v Javě?
`add barcode pdf java` odkazuje na proces použití Java kódu k vložení čárového kódu (např. Code128, QR nebo Data Matrix) do PDF souboru. Tato technika poskytuje strojově čitelnou značku, kterou lze skenovat nebo programově ověřovat, což umožňuje rychlé sledování dokumentů v interních systémech.

## Proč používat čárové podpisy místo plných digitálních podpisů?
Čárové podpisy jsou **30‑50 % rychlejší** při generování i ověřování než PKI‑založené digitální podpisy a spolehlivě fungují i po cyklu tisk‑sken. Nevyžadují správu certifikátů, což je ideální pro vysokovýkonné interní workflow, kde kryptografický důkaz není povinný.

## Prerequisites

- **Java Development Kit (JDK) 8+** – Java 11 nebo 17 je doporučená pro lepší výkon.  
- **IDE** – IntelliJ IDEA nebo Eclipse (příklady používají syntaxi IntelliJ).  
- **Nástroj pro sestavení** – Maven nebo Gradle pro správu závislostí.  

### Přidání GroupDocs.Signature do vašeho projektu

Nejjednodušší způsob, jak začít, je přidat knihovnu pomocí vašeho nástroje pro sestavení. Zde je postup:

**Uživatelé Maven** – Přidejte toto do vašeho `pom.xml`:

```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

**Uživatelé Gradle** – Přidejte toto do vašeho `build.gradle`:

```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

**Direct JAR Download** – Pokud dáváte přednost ručnímu nastavení, stáhněte JAR ze [GroupDocs.Signature releases](https://releases.groupdocs.com/signature/java/) a přidejte jej do classpath.

### Získání licence

GroupDocs.Signature není zdarma pro produkční použití, ale máte flexibilní možnosti:

- **Bezplatná zkušební verze** – Stáhněte ze [stánky ke stažení GroupDocs](https://releases.groupdocs.com/signature/java/) pro vyzkoušení funkcí (přidávají se vodotisky hodnocení).  
- **Dočasná licence** – Získejte 30 dnů plného přístupu přes [stránku dočasné licence GroupDocs](https://purchase.groupdocs.com/temporary-license/) – ideální pro koncepty.  
- **Plná licence** – Pro produkční nasazení si prohlédněte [možnosti nákupu GroupDocs](https://purchase.groupdocs.com/buy).  

**Pro tip:** Začněte s dočasnou licencí pro vývoj; odstraní vodotisky, jakmile přejdete na trvalý klíč.

### Rychlá kontrola prostředí

Jakmile přidáte závislost, spusťte jednoduchý test:

```java
import com.groupdocs.signature.Signature;

public class SignatureTest {
    public static void main(String[] args) {
        try {
            Signature signature = new Signature("test.pdf");
            System.out.println("GroupDocs.Signature initialized successfully!");
            signature.dispose();
        } catch (Exception e) {
            System.err.println("Setup issue: " + e.getMessage());
        }
    }
}
```

Pokud program běží bez chyb, je vaše prostředí připravené. V případě problémů ověřte verzi JDK a přesnou verzi knihovny, kterou jste přidali.

## Kdy použít čárové podpisy

Čárové podpisy vynikají v konkrétních scénářích:

- **Interní workflow dokumentů** – Sledovat faktury, objednávky nebo poznámky skrze schvalovací řetězce.  
- **Zpracování velkého objemu** – Podepisovat tisíce dokumentů rychle; generování čárových kódů je až **2× rychlejší** než plné digitální podepisování.  
- **Mosty tisk‑sken** – Čárové kódy přežijí cyklus tisk‑sken, což je ideální pro hybridní papír‑digitální procesy.  
- **Integrace se starými systémy** – Existující čtečky čárových kódů mohou značky číst bez dalšího softwaru.  
- **Auditní stopy** – Vložit ID transakcí nebo časové razítka, která auditoři mohou okamžitě ověřit.

Vyhněte se čárovým podpisům u právních smluv, vysoce zabezpečených dokumentů nebo výměn s externími partnery, kde jsou vyžadovány PKI‑založené digitální podpisy.

## Nastavení GroupDocs.Signature pro Java

### Definice hlavní třídy

Třída `Signature` je vstupním bodem pro všechny operace podepisování, ověřování, vyhledávání, aktualizace a mazání v GroupDocs.Signature.

```java
import com.groupdocs.signature.Signature;
```

### Základní inicializace

Vytvořte objekt `Signature`, který ukazuje na cílový soubor:

```java
Signature signature = new Signature("path/to/your/document.pdf");
```

**Důležité poznámky**

- Cesty mohou být absolutní nebo relativní; použijte `System.getProperty("user.home")` pro kompatibilitu napříč platformami.  
- GroupDocs podporuje **více než 30 vstupních a výstupních formátů**, včetně PDF, DOCX, XLSX, PPTX a PNG.  
- Vždy uvolněte zdroje pomocí `signature.dispose()` nebo bloku try‑with‑resources:

```java
try (Signature signature = new Signature("path/to/your/document.pdf")) {
    // Your signing operations here
} catch (Exception e) {
    System.err.println("Error working with document: " + e.getMessage());
}
```

Nyní jste připraveni přidávat čárové kódy.

## Jak přidat čárový kód do PDF v Javě?

Načtěte zdrojové PDF pomocí `new Signature("input.pdf")`, nakonfigurujte objekt `BarcodeSignature` (např. Code128 s textem “John Smith”) a zavolejte `sign`, abyste vytvořili podepsaný soubor – vše ve třech stručných řádcích kódu. Tento přístup vám umožní vložit strojově čitelnou značku a zachovat původní rozložení dokumentu, a funguje pro jakýkoli podporovaný formát, nejen pro PDF.

### Implementace krok za krokem

#### 1. Definice cest k souborům

Nastavte umístění zdrojových a výstupních souborů:

```java
String filePath = "YOUR_DOCUMENT_DIRECTORY/sample.docx";
String outputFilePath = "YOUR_OUTPUT_DIRECTORY/signed_sample.docx";
```

#### 2. Vytvoření obslužného objektu Signature

Inicializujte obslužný objekt se zdrojovým dokumentem:

```java
Signature signature = new Signature(filePath);
```

#### 3. Konfigurace možností čárového kódu

Objekt `BarcodeSignature` definuje vizuální a datové vlastnosti čárového kódu, který má být vložen. Nastavte typ čárového kódu, kódovaný text, pozici, velikost, barvu a volitelný čitelný font:

```java
BarcodeSignOptions signOptions = new BarcodeSignOptions("John Smith", BarcodeTypes.Code128);
signOptions.setVerticalAlignment(VerticalAlignment.Top);
signOptions.setHorizontalAlignment(HorizontalAlignment.Center);
signOptions.setWidth(100);
signOptions.setHeight(40);
signOptions.setMargin(new java.awt.Rectangle(20, 20, 0, 0));
signOptions.setForeColor(Color.RED);

SignatureFont signatureFont = new SignatureFont();
signatureFont.setSize(12);
signatureFont.setFamilyName("Comic Sans MS");
signOptions.setFont(signatureFont);
```

> **Pro tip:** Pokud kódovaný řetězec překročí 20 znaků, zvětšete šířku čárového kódu, aby nedošlo k chybám při skenování.

#### 4. Použití podpisu

Spusťte operaci podepisování a vygenerujte výstupní soubor:

```java
signature.sign(outputFilePath, signOptions);
```

#### 5. Praktický příklad

V systému schvalování faktur můžete vložit ID zaměstnance schvalujícího a časové razítko:

```java
String invoiceId = "INV-2025-0042";
String approver = "john.smith@company.com";
String timestamp = LocalDateTime.now().toString();

// Combine into barcode data
String barcodeData = invoiceId + "|" + approver + "|" + timestamp;

BarcodeSignOptions signOptions = new BarcodeSignOptions(barcodeData, BarcodeTypes.QR);
signOptions.setVerticalAlignment(VerticalAlignment.Bottom);
signOptions.setHorizontalAlignment(HorizontalAlignment.Right);

signature.sign(outputFilePath, signOptions);
```

Výsledné PDF nyní obsahuje skenovatelný čárový kód, který kóduje veškerá potřebná metadata schválení.

## Jak mohu ověřit čárový podpis v dokumentu Java?

Metoda `Signature.verify` kontroluje dokument na shodu s čárovými podpisy podle zadaných možností a vrací boolean, který indikuje, zda očekávaný čárový kód existuje. Ověření je užitečné pro automatizované workflow, kde je nutné potvrdit, že dokument byl zpracován správnou stranou před dalšími akcemi.

### Kroky ověření

#### 1. Načtení podepsaného dokumentu

```java
Signature signature = new Signature("YOUR_OUTPUT_DIRECTORY/signed_sample.docx");
```

#### 2. Nastavení kritérií ověření

Definujte přesný text, formát čárového kódu a číslo stránky, které očekáváte:

```java
BarcodeVerifyOptions verifyOptions = new BarcodeVerifyOptions();
verifyOptions.setAllPages(false); // Only check the first page
verifyOptions.setPageNumber(1);
verifyOptions.setEncodeType(BarcodeTypes.Code128);
verifyOptions.setText("John Smith");
```

#### 3. Spuštění ověření

Proveďte kontrolu a zpracujte výsledek:

```java
boolean isValid = signature.verify(verifyOptions) != null;

if (isValid) {
    System.out.println("Document signature verified successfully!");
} else {
    System.out.println("Warning: Signature verification failed!");
}
```

**Běžný vzor:** Pro jednoduché potvrzení, že *jakýkoli* čárový kód daného typu existuje, vynechte filtr `setText`:

```java
BarcodeVerifyOptions flexibleOptions = new BarcodeVerifyOptions();
flexibleOptions.setAllPages(true);
flexibleOptions.setEncodeType(BarcodeTypes.Code128);
// No setText() call = accept any text with this barcode type

boolean hasAnySignature = signature.verify(flexibleOptions) != null;
```

Nebo ověřte pouze formát čárového kódu bez ohledu na obsah:

```java
BarcodeVerifyOptions formatOnly = new BarcodeVerifyOptions();
formatOnly.setEncodeType(BarcodeTypes.QR);
// Confirms a QR code exists, regardless of content
```

> **Warning:** Ověření je citlivé na velikost písmen a mezery; před podepsáním a ověřením vždy ořízněte a normalizujte data.

## Jak vyhledat čárové podpisy v dokumentu?

Metoda `Signature.search` prohledá dokument na čárové podpisy, které odpovídají zadaným `BarcodeSearchOptions`, a vrátí kolekci obsahující umístění, číslo stránky a kódovanou hodnotu každého čárového kódu. Tato schopnost umožňuje hromadný výpis metadat bez nutnosti otevírat každý soubor ručně.

### Průběh vyhledávání

#### 1. Inicializace vyhledávání

```java
Signature signature = new Signature("YOUR_OUTPUT_DIRECTORY/signed_sample.docx");
```

#### 2. Konfigurace parametrů vyhledávání

Zadejte rozsah stránek, typ čárového kódu nebo textové filtry:

```java
BarcodeSearchOptions searchOptions = new BarcodeSearchOptions();
searchOptions.setAllPages(true); // Search the entire document
```

Volitelně omezte vyhledávání pro zlepšení výkonu:

```java
BarcodeSearchOptions narrowSearch = new BarcodeSearchOptions();
narrowSearch.setAllPages(false);
narrowSearch.setPageNumber(1); // Only search page 1
narrowSearch.setEncodeType(BarcodeTypes.Code128); // Only find Code128 barcodes
```

#### 3. Provedení vyhledávání

```java
java.util.List<BarcodeSignature> signatures = signature.search(BarcodeSignature.class, searchOptions);

System.out.println("Found " + signatures.size() + " barcode signature(s)");

for (BarcodeSignature bcSignature : signatures) {
    System.out.println("Barcode Type: " + bcSignature.getEncodeType().getTypeName());
    System.out.println("Text: " + bcSignature.getText());
    System.out.println("Position: (" + bcSignature.getLeft() + ", " + bcSignature.getTop() + ")");
    System.out.println("Size: " + bcSignature.getWidth() + "x" + bcSignature.getHeight());
    System.out.println("---");
}
```

#### 4. Příklad extrakce dat

Vytažení dat schválení z každého čárového kódu v dávce faktur:

```java
List<BarcodeSignature> foundSignatures = signature.search(BarcodeSignature.class, searchOptions);

for (BarcodeSignature sig : foundSignatures) {
    String barcodeData = sig.getText();
    
    // Parse your custom format (remember our invoice example?)
    String[] parts = barcodeData.split("\\|");
    if (parts.length == 3) {
        String invoiceId = parts[0];
        String approver = parts[1];
        String timestamp = parts[2];
        
        System.out.println("Invoice " + invoiceId + " approved by " + approver + " at " + timestamp);
    }
}
```

> **Performance tip:** U dokumentů přes 100 stran vždy omezte vyhledávání na stránky, které skutečně obsahují čárové kódy; tím lze zkrátit dobu běhu až o **70 %**.

## Jak mohu aktualizovat existující čárový podpis?

Metoda `Signature.update` upravuje vizuální atributy existujícího čárového podpisu – například pozici, velikost nebo barvu – a zachovává původní kódovaná data. To je užitečné, když jsou po podepsání potřeba změny rozvržení.

### Postup aktualizace

#### 1. Najít podpisy k aktualizaci

```java
Signature signature = new Signature("YOUR_OUTPUT_DIRECTORY/signed_sample.docx");

BarcodeSearchOptions searchOptions = new BarcodeSearchOptions();
searchOptions.setAllPages(true);

List<BarcodeSignature> signatures = signature.search(BarcodeSignature.class, searchOptions);
```

#### 2. Upravit požadované vlastnosti

```java
List<BarcodeSignature> signaturesToUpdate = new ArrayList<>();

if (!signatures.isEmpty()) {
    BarcodeSignature bcSignature = signatures.get(0); // Update the first found signature
    
    // Move it 100px right and 100px down
    bcSignature.setLeft(bcSignature.getLeft() + 100);
    bcSignature.setTop(bcSignature.getTop() + 100);
    
    // Make it bigger
    bcSignature.setWidth(200);
    bcSignature.setHeight(50);
    
    signaturesToUpdate.add(bcSignature);
}
```

Můžete změnit několik atributů najednou:

```java
bcSignature.setLeft(50);
bcSignature.setTop(50);
bcSignature.setWidth(150);
bcSignature.setHeight(45);
// Note: You can't change the encoded text or barcode type with update
// For that, you'd need to delete and re-sign
```

#### 3. Uložit změny

```java
ByteArrayOutputStream outputStream = new ByteArrayOutputStream();
signature.update(outputStream, signaturesToUpdate);

// If you want to save to a file instead:
// signature.update("path/to/updated_document.docx", signaturesToUpdate);
```

#### 4. Praktický scénář

Přesunout všechny podpisy, aby se nepřekrývaly s nově přidaným logem společnosti:

```java
List<BarcodeSignature> allSignatures = signature.search(BarcodeSignature.class, searchOptions);
List<BarcodeSignature> toUpdate = new ArrayList<>();

for (BarcodeSignature sig : allSignatures) {
    // Move all signatures down by 50px to clear space for new logo
    if (sig.getTop() < 100) {
        sig.setTop(sig.getTop() + 50);
        toUpdate.add(sig);
    }
}

if (!toUpdate.isEmpty()) {
    signature.update(outputStream, toUpdate);
    System.out.println("Repositioned " + toUpdate.size() + " signature(s)");
}
```

> **Limitation:** Změna kódovaného textu vyžaduje smazání a opětovné vložení podpisu.

## Jak smazat čárové podpisy z dokumentu?

Metoda `Signature.delete` trvale odstraňuje vybrané čárové podpisy z dokumentu, vymazává jak vizuální prvek, tak jeho kódovaná data. Použijte tuto operaci při čištění testovacích podpisů nebo když čárový kód již není relevantní.

### Kroky mazání

#### 1. Najít podpisy

```java
Signature signature = new Signature("YOUR_OUTPUT_DIRECTORY/signed_sample.docx");

BarcodeSearchOptions searchOptions = new BarcodeSearchOptions();
searchOptions.setAllPages(true);

List<BarcodeSignature> signatures = signature.search(BarcodeSignature.class, searchOptions);
```

#### 2. Smazat vybrané podpisy

```java
List<BarcodeSignature> signaturesToDelete = new ArrayList<>();

// Delete all Code128 signatures (for example)
for (BarcodeSignature sig : signatures) {
    if (sig.getEncodeType().equals(BarcodeTypes.Code128)) {
        signaturesToDelete.add(sig);
    }
}

if (!signaturesToDelete.isEmpty()) {
    boolean result = signature.delete(signaturesToDelete);
    
    if (result) {
        System.out.println("Successfully deleted " + signaturesToDelete.size() + " signature(s)");
    } else {
        System.err.println("Failed to delete signatures");
    }
}
```

#### 3. Příklad podmíněného mazání

Odstraňte pouze čárové kódy starší než konkrétní časové razítko (předpokládá se, že časové razítko je součástí kódovaného textu):

```java
LocalDateTime cutoffDate = LocalDateTime.now().minusDays(30);
List<BarcodeSignature> outdatedSignatures = new ArrayList<>();

for (BarcodeSignature sig : signatures) {
    try {
        String text = sig.getText();
        // Assuming format like "data|timestamp"
        String[] parts = text.split("\\|");
        if (parts.length > 1) {
            LocalDateTime sigDate = LocalDateTime.parse(parts[1]);
            if (sigDate.isBefore(cutoffDate)) {
                outdatedSignatures.add(sig);
            }
        }
    } catch (Exception e) {
        // Skip signatures that don't match our format
        continue;
    }
}

if (!outdatedSignatures.isEmpty()) {
    signature.delete(outdatedSignatures);
    System.out.println("Removed " + outdatedSignatures.size() + " outdated signature(s)");
}
```

> **Caution:** Mazání nelze vrátit; během testování vždy pracujte s kopií produkčních souborů.

#### 4. Vzor hromadného mazání

Vyčistěte testovací podpisy před vydáním:

```java
// Remove all signatures containing "TEST" in their text
List<BarcodeSignature> testSignatures = signatures.stream()
    .filter(sig -> sig.getText().toUpperCase().contains("TEST"))
    .collect(Collectors.toList());

if (!testSignatures.isEmpty()) {
    signature.delete(testSignatures);
    System.out.println("Cleaned up " + testSignatures.size() + " test signature(s)");
}
```

## Typy čárových kódů: Praktický průvodce

Výběr správného čárového kódu ovlivňuje spolehlivost skenování, kapacitu dat a kompatibilitu s tiskárnou.

### Code128 (Nejčastější volba)

- **Kdy použít:** Alfanumerická data, vysoká hustota, tištěné dokumenty.  
- **Výhody:** Kompaktní, funguje se standardními skenery, tiskne se jasně i v malých velikostech.  
- **Nevýhody:** Omezeno na ASCII, méně odolné vůči chybám než 2‑D kódy.  

```java
BarcodeSignOptions code128 = new BarcodeSignOptions("INV-2025-042", BarcodeTypes.Code128);
```

### QR kód (Nejlepší pro mobilní zařízení)

- **Kdy použít:** Mobilní skenování, velké objemy dat (URL, JSON atd.), dokumenty, které mohou být poškozeny.  
- **Výhody:** Až 4 000 znaků, vestavěná korekce chyb, přátelské pro chytré telefony.  
- **Nevýhody:** Větší vizuální stopa, vyžaduje vyšší rozlišení pro malé velikosti.  

```java
String jsonData = "{\"invoice\":\"INV-042\",\"amount\":1500.00,\"approver\":\"john@company.com\"}";
BarcodeSignOptions qrCode = new BarcodeSignOptions(jsonData, BarcodeTypes.QR);
```

### Code39 (Starý spolehlivý)

- **Kdy použít:** Prostředí se staršími skenery, potřeba čitelného textu.  
- **Výhody:** Široká podpora starších systémů, jednoduchý formát, nevyžaduje kontrolní součet.  
- **Nevýhody:** Nízká datová hustota, omezená znaková sada, zabírá více místa.

### Data Matrix (Kompaktní výkonný kód)

- **Kdy použít:** Extrémně omezený prostor, označování malých předmětů, data s vysokou hustotou.  
- **Výhody:** Velmi kompaktní, silná korekce chyb, funguje na zakřivených površích.  
- **Nevýhody:** Vyžaduje vysoce kvalitní tisk, méně běžná podpora scannerů.

#### Rychlé srovnání

| Barcode Type | Data Capacity | Best For | Typical Size |
|--------------|---------------|----------|--------------|
| Code128 | ~100 znaků | Obecné označování | Malá |
| QR Code | ~4 000 znaků | Mobilní skenování, bohatá data | Střední |
| Code39 | ~43 znaků | Starý hardware | Velká |
| Data Matrix | ~3 000 znaků | Malé prostory, průmyslové značky | Velmi malá |

**Recommendation:** Začněte s **Code128** pro jednoduchá ID. Přepněte na **QR**, když potřebujete vložit URL nebo větší payload. **Code39** používejte jen pro staré integrace.

## Časté problémy a řešení

### Problém: „Čárový kód nebyl během ověření nalezen“

**Symptoms:** Ověření vrací `false`, i když je čárový kód viditelný.

**Typical causes**
1. Nesoulad velikosti písmen (např. “John Smith” vs. “john smith”).  
2. Přebytečné mezery v kódovaném textu.  
3. Nesprávný typ čárového kódu uvedený v možnostech ověření.  
4. Vyhledávání na špatném čísle stránky.

**Solution:** Normalizujte text před podepsáním i ověřením a zajistěte, aby `setEncodeType` odpovídal původnímu typu.

```java
// Always normalize your data
String signatureText = originalText.trim().toLowerCase();

// When signing:
BarcodeSignOptions signOptions = new BarcodeSignOptions(signatureText, BarcodeTypes.Code128);

// When verifying:
BarcodeVerifyOptions verifyOptions = new BarcodeVerifyOptions();
verifyOptions.setText(signatureText); // Use the same normalized text
verifyOptions.setEncodeType(BarcodeTypes.Code128);
```

### Problém: „Čárový kód je rozmazaný nebo nečitelné“

**Symptoms:** Vytisknuté čárové kódy nelze skenovat.

**Causes**
- Rozměry čárového kódu jsou příliš malé pro kódovaná data.  
- Nastavení tiskárny s nízkým rozlišením.  
- Nedostatečný kontrast mezi barvou čárového kódu a pozadím.

**Solution:** Zvětšete šířku/výšku čárového kódu, použijte vysoký kontrast (černá na bílém) a nastavte DPI tiskárny alespoň na 300 dpi.

```java
// Increase size for longer strings
int dataLength = barcodeText.length();
int minWidth = Math.max(100, dataLength * 10); // 10px per character minimum

BarcodeSignOptions signOptions = new BarcodeSignOptions(barcodeText, BarcodeTypes.Code128);
signOptions.setWidth(minWidth);
signOptions.setHeight(60); // Taller = easier to scan

// Use high-contrast colors
signOptions.setForeColor(Color.BLACK); // Black on white is most reliable
signOptions.setBackColor(Color.WHITE);
```

### Problém: „OutOfMemoryError u velkých dokumentů“

**Symptoms:** Aplikace spadne při zpracování PDF se stovkami stran.

**Cause:** Knihovna načítá celý dokument do paměti.

**Solution:** Aktivujte streamingový režim a zpracovávejte stránky po částech.

```java
// Process pages in batches instead of all at once
BarcodeSearchOptions searchOptions = new BarcodeSearchOptions();
searchOptions.setAllPages(false);

List<BarcodeSignature> allSignatures = new ArrayList<>();

for (int page = 1; page <= totalPages; page++) {
    searchOptions.setPageNumber(page);
    List<BarcodeSignature> pageSignatures = signature.search(BarcodeSignature.class, searchOptions);
    allSignatures.addAll(pageSignatures);
    
    // Process and clear as you go
    if (page % 10 == 0) {
        System.gc(); // Suggest garbage collection every 10 pages
    }
}
```

### Problém: „Pozice podpisu je nekonzistentní napříč typy dokumentů“

**Symptoms:** Čárové kódy se objevují na různých místech při podepisování PDF vs. Word dokumentů.

**Cause:** PDF používá počátek v levém dolním rohu, zatímco Word používá levý horní roh.

**Solution:** Detekujte typ dokumentu a aplikujte odpovídající transformaci souřadnic.

```java
// Use relative positioning instead of absolute
signOptions.setVerticalAlignment(VerticalAlignment.Bottom);
signOptions.setHorizontalAlignment(HorizontalAlignment.Right);

// Then use margins for fine-tuning
Padding margin = new Padding();
margin.setRight(50); // 50px from right edge
margin.setBottom(50); // 50px from bottom
signOptions.setMargin(margin);

// This works consistently across PDF, DOCX, XLSX, etc.
```

### Problém: „Aktualizované podpisy ztrácejí formátování“

**Symptoms:** Po volání `update` se barva nebo font čárového kódu neočekávaně změní.

**Cause:** Ne všechny vizuální vlastnosti jsou při aktualizaci zachovány.

**Solution:** Po volání `update` znovu aplikujte požadované vizuální nastavení.

```java
// When updating, explicitly set all visual properties
bcSignature.setLeft(newLeft);
bcSignature.setTop(newTop);
bcSignature.setWidth(originalWidth); // Don't forget these!
bcSignature.setHeight(originalHeight);
// Note: Color and font can't be updated - you'd need to delete and re-sign
```

## Nejlepší postupy pro produkci

### Optimalizace výkonu

1. **Znovupoužití instancí Signature** – Vytvořte jeden objekt `Signature` na dokument a znovu jej použijte pro více operací.

```java
// Bad - Creates new instance each time
public void processDocument(String path) {
    Signature sig1 = new Signature(path);
    sig1.search(/* ... */);
    
    Signature sig2 = new Signature(path); // Unnecessary reload
    sig2.verify(/* ... */);
}

// Good - Reuse the same instance
public void processDocument(String path) {
    try (Signature signature = new Signature(path)) {
        signature.search(/* ... */);
        signature.verify(/* ... */);
        signature.update(/* ... */);
    }
}
```

2. **Vyhledávejte pouze konkrétní stránky** – Omezte rozsah stránek na ty, kde se očekávají čárové kódy.

```java
// Slow for 100+ page documents
BarcodeSearchOptions slowSearch = new BarcodeSearchOptions();
slowSearch.setAllPages(true);

// Fast - only check where signatures actually are
BarcodeSearchOptions fastSearch = new BarcodeSearchOptions();
fastSearch.setAllPages(false);
fastSearch.setPageNumber(1); // Only check cover page
```

3. **Zvolte nejjednodušší typ čárového kódu** – Jednodušší kódy se generují rychleji; QR nebo Data Matrix používejte jen když skutečně potřebujete větší kapacitu.

```java
// Overkill for simple IDs
BarcodeSignOptions slow = new BarcodeSignOptions("12345", BarcodeTypes.QR);

// Faster and more appropriate
BarcodeSignOptions fast = new BarcodeSignOptions("12345", BarcodeTypes.Code128);
```

### Bezpečnostní úvahy

1. **Nikdy neenkódujte citlivá osobní data** – Čárové kódy jsou snadno čitelné; vyhněte se PII jako SSN nebo hesla.

```java
// Bad - exposes sensitive data
String barcodeData = "SSN:123-45-6789|Password:hunter2";

// Good - use reference IDs
String barcodeData = "USER-REF-7721X"; // Look up sensitive data server-side
```

2. **Validujte na serveru** – Nikdy nevěřte pouze klientskému ověření; vždy znovu ověřte na důvěryhodném backendu.

```java
// Client scans barcode and extracts "APPROVED-BY-ADMIN"
// Always verify server-side:
public boolean verifyApproval(String documentId, String scannedData) {
    // Load document from secure storage
    Signature signature = new Signature(getSecureDocument(documentId));
    
    BarcodeVerifyOptions verifyOptions = new BarcodeVerifyOptions();
    verifyOptions.setText(scannedData);
    
    boolean isValid = signature.verify(verifyOptions) != null;
    
    // Also check against your database
    boolean isInDatabase = checkApprovalDatabase(documentId, scannedData);
    
    return isValid && isInDatabase;
}
```

3. **Přidejte časová razítka** – Zahrňte časové razítko do payloadu čárového kódu, aby se zabránilo útokům typu replay.

```java
import java.time.LocalDateTime;
import java.time.temporal.ChronoUnit;

String timestamp = LocalDateTime.now().truncatedTo(ChronoUnit.SECONDS).toString();
String barcodeData = "APPROVAL|" + userId + "|" + timestamp;

// When verifying, check the timestamp isn't too old
public boolean isSignatureRecent(String barcodeData, int maxAgeHours) {
    String[] parts = barcodeData.split("\\|");
    if (parts.length < 3) return false;
    
    LocalDateTime signatureTime = LocalDateTime.parse(parts[2]);
    LocalDateTime now = LocalDateTime.now();
    
    long hoursSince = ChronoUnit.HOURS.between(signatureTime, now);
    return hoursSince <= maxAgeHours;
}
```

### Vzory pro zpracování chyb

- **Vždy používejte Try‑With‑Resources** pro zajištění uvolnění objektů `Signature`.

```java
try (Signature signature = new Signature(documentPath)) {
    // Your operations here
    signature.sign(outputPath, signOptions);
} catch (Exception e) {
    logger.error("Failed to sign document: " + documentPath, e);
    throw new DocumentSigningException("Could not process document", e);
}
```

- **Ověřte přístup k souboru** před pokusem o podepsání.

```java
public void signDocument(String inputPath, String outputPath) {
    File inputFile = new File(inputPath);
    
    if (!inputFile.exists()) {
        throw new IllegalArgumentException("Input file not found: " + inputPath);
    }
    
    if (!inputFile.canRead()) {
        throw new SecurityException("Cannot read input file: " + inputPath);
    }
    
    File outputDir = new File(outputPath).getParentFile();
    if (outputDir != null && !outputDir.exists()) {
        outputDir.mkdirs();
    }
    
    try (Signature signature = new Signature(inputPath)) {
        signature.sign(outputPath, signOptions);
    }
}
```

- **Synchronizujte přístup** pokud více vláken může pracovat se stejným souborem.

```java
import java.util.concurrent.locks.ReentrantLock;
import java.util.concurrent.ConcurrentHashMap;

public class SignatureManager {
    private final ConcurrentHashMap<String, ReentrantLock> documentLocks = new ConcurrentHashMap<>();
    
    public void signDocument(String documentPath, BarcodeSignOptions options) {
        ReentrantLock lock = documentLocks.computeIfAbsent(documentPath, k -> new ReentrantLock());
        
        lock.lock();
        try (Signature signature = new Signature(documentPath)) {
            signature.sign(documentPath + ".signed", options);
        } finally {
            lock.unlock();
        }
    }
}
```

### Testování vaší implementace

**Unit Test Template**

```java
import org.junit.jupiter.api.Test;
import org.junit.jupiter.api.io.TempDir;
import static org.junit.jupiter.api.Assertions.*;

public class BarcodeSignatureTest {
    
    @TempDir
    Path tempDir;
    
    @Test
    public void testSignAndVerify() throws Exception {
        // Setup
        String testDoc = "test-document.pdf";
        String outputDoc = tempDir.resolve("signed-test.pdf").toString();
        String testData = "TEST-USER-12345";
        
        // Sign
        try (Signature signature = new Signature(testDoc)) {
            BarcodeSignOptions signOptions = new BarcodeSignOptions(testData, BarcodeTypes.Code128);
            signature.sign(outputDoc, signOptions);
        }
        
        // Verify
        try (Signature signature = new Signature(outputDoc)) {
            BarcodeVerifyOptions verifyOptions = new BarcodeVerifyOptions();
            verifyOptions.setText(testData);
            verifyOptions.setEncodeType(BarcodeTypes.Code128);
            
            boolean isValid = signature.verify(verifyOptions) != null;
            assertTrue(isValid, "Signature should be valid");
        }
    }
    
    @Test
    public void testSearchFindsSignature() throws Exception {
        String signedDoc = "signed-document.pdf";
        
        try (Signature signature = new Signature(signedDoc)) {
            BarcodeSearchOptions searchOptions = new BarcodeSearchOptions();
            searchOptions.setAllPages(true);
            
            List<BarcodeSignature> signatures = signature.search(BarcodeSignature.class, searchOptions);
            
            assertFalse(signatures.isEmpty(), "Should find at least one signature");
            assertEquals("TEST-USER-12345", signatures.get(0).getText());
        }
    }
}
```

**Integration Checklist**

- ✅ Testujte všechny podporované formáty (PDF, DOCX, XLSX, PPTX, PNG).  
- ✅ Ověřte, že čárové kódy přežijí cyklus tisk‑sken.  
- ✅ Proveďte zátěžový test s maximální délkou datových řetězců.  
- ✅ Potvrďte správnou pozici na formátech A4, Letter a vlastních velikostech stránek.  
- ✅ Spusťte souběžné podepisování na více dokumentech.  
- ✅ Sledujte využití paměti u dokumentů > 500 stran.  
- ✅ Zajistěte, aby čtečky čárových kódů spolehlivě četly výstup.

### Logování a monitorování

Přidejte smysluplné logy kolem každé operace:

```java
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

public class DocumentSigningService {
    private static final Logger logger = LoggerFactory.getLogger(DocumentSigningService.class);
    
    public void signDocument(String docPath, String barcodeData) {
        logger.info("Starting signature process for document: {}", docPath);
        logger.debug("Barcode data length: {} characters", barcodeData.length());
        
        try (Signature signature = new Signature(docPath)) {
            BarcodeSignOptions options = new BarcodeSignOptions(barcodeData, BarcodeTypes.Code128);
            
            long startTime = System.currentTimeMillis();
            signature.sign(docPath + ".signed", options);
            long duration = System.currentTimeMillis() - startTime;
            
            logger.info("Successfully signed document in {}ms", duration);
        } catch (Exception e) {
            logger.error("Failed to sign document: {}", docPath, e);
            throw new RuntimeException("Signature operation failed", e);
        }
    }
}
```

Sledujte klíčové metriky jako čas zpracování, spotřebu paměti a míru chyb:

```java
// Track success/failure rates
metricsService.incrementCounter("signature.sign.success");
metricsService.incrementCounter("signature.verify.failure");

// Track performance
metricsService.recordTimer("signature.sign.duration", duration);

// Track document sizes
metricsService.recordHistogram("signature.document.pages", pageCount);
```

## Profesionální tipy z reálného použití

**Strategie dávkového zpracování**

Při práci se stovkami souborů je zpracovávejte po dávkách a průběžně hlaste postup:

```java
public void signBatch(List<String> documents, String barcodePrefix) {
    int total = documents.size();
    int completed = 0;
    int failed = 0;
    
    for (String docPath : documents) {
        try {
            String barcodeData = barcodePrefix + "-" + UUID.randomUUID().toString();
            signDocument(docPath, barcodeData);
            completed++;
            
            if (completed % 10 == 0) {
                logger.info("Progress: {}/{} documents signed", completed, total);
            }
        } catch (Exception e) {
            failed++;
            logger.warn("Failed to sign: {}", docPath, e);
        }
    }
    
    logger.info("Batch complete: {} succeeded, {} failed", completed, failed);
}
```

**Externalizace konfigurace**

Uložte nastavení čárových kódů (typ, velikost, barvu) do souboru properties, aby bylo možné je snadno ladit bez rekompilace:

```java
public class BarcodeConfig {
    private int defaultWidth = 100;
    private int defaultHeight = 40;
    private String defaultBarcodeType = "Code128";
    private String defaultColor = "BLACK";
    
    // Load from properties file or environment variables
    public BarcodeConfig() {
        this.defaultWidth = Integer.parseInt(
            System.getProperty("barcode.width", "100")
        );
        // ... load other properties
    }
    
    public BarcodeSignOptions createDefaultOptions(String text) {
        BarcodeSignOptions options = new BarcodeSignOptions(text, getBarcodeType());
        options.setWidth(defaultWidth);
        options.setHeight(defaultHeight);
        options.setForeColor(getColor());
        return options;
    }
}
```

**Standardizace payloadu čárového kódu**

Používejte oddělený formát jako `EMPID|TIMESTAMP|DOCID`, aby bylo parsování jednoduché a konzistentní:

```java
public class BarcodeDataBuilder {
    private String userId;
    private String action;
    private LocalDateTime timestamp;
    private String documentId;
    
    public BarcodeDataBuilder setUserId(String userId) {
        this.userId = userId;
        return this;
    }
    
    public BarcodeDataBuilder setAction(String action) {
        this.action = action;
        return this;
    }
    
    public BarcodeDataBuilder setDocumentId(String documentId) {
        this.documentId = documentId;
        return this;
    }
    
    public String build() {
        this.timestamp = LocalDateTime.now();
        
        // Format: VERSION|USER|ACTION|DOC_ID|TIMESTAMP|CHECKSUM
        String data = String.join("|",
            "v1",
            userId,
            action,
            documentId,
            timestamp.toString()
        );
        
        // Add simple checksum
        int checksum = data.hashCode();
        return data + "|" + checksum;
    }
    
    public static ParsedBarcodeData parse(String barcodeData) {
        String[] parts = barcodeData.split("\\|");
        if (parts.length != 6 || !parts[0].equals("v1")) {
            throw new IllegalArgumentException("Invalid barcode format");
        }
        
        return new ParsedBarcodeData(parts[1], parts[2], parts[3], 
                                     LocalDateTime.parse(parts[4]));
    }
}

// Usage:
String barcodeData = new BarcodeDataBuilder()
    .setUserId("john.smith")
    .setAction("APPROVED")
    .setDocumentId("INV-2025-042")
    .build();
```

**Automatická detekce typu dokumentu**

Upravte rozměry čárového kódu podle toho, zda je cílem PDF, Word nebo obrázek:

```java
public BarcodeSignOptions getOptimalOptions(String documentPath, String text) {
    String extension = documentPath.substring(documentPath.lastIndexOf(".") + 1).toLowerCase();
    
    BarcodeSignOptions options = new BarcodeSignOptions(text, BarcodeTypes.Code128);
    
    switch (extension) {
        case "pdf":
            // PDFs can handle larger, detailed barcodes
            options.setWidth(150);
            options.setHeight(50);
            break;
        case "docx":
        case "doc":
            // Word docs need compact signatures that don't disrupt flow
            options.setWidth(100);
            options.setHeight(35);
            options.setVerticalAlignment(VerticalAlignment.Bottom);
            break;
        case "xlsx":
        case "xls":
            // Excel needs signatures that don't obscure data
            options.setWidth(80);
            options.setHeight(30);
            options.setHorizontalAlignment(HorizontalAlignment.Right);
            break;
        default:
            // Safe defaults
            options.setWidth(100);
            options.setHeight(40);
    }
    
    return options;
}
```

## Další zdroje

- [GroupDocs.Signature dokumentace](https://docs.groupdocs.com/signature/java/) – Kompletní průvodce API a příklady použití.  
- [GroupDocs fórum podpory](https://forum.groupdocs.com/c/signature/13) – Komunitní pomoc a řešení problémů.  
- [API reference](https://apireference.groupdocs.com/signature/java) – Podrobné popisy metod a parametrů.

## Často kladené otázky

**Q: Mohu použít GroupDocs.Signature s Java 17?**  
**A:** Ano – knihovna je plně kompatibilní s JDK 8, 11 a 17.

**Q: Přetrvá čárový kód cyklus tisk‑sken?**  
**A:** Když použijete Code128 nebo QR s dostatečnou velikostí a kontrastem, čárový kód zůstane po tisku a skenování čitelný.

**Q: Kolik čárových kódů může jeden dokument obsahovat?**  
**A:** Neexistuje pevný limit; pro optimální výkon však udržujte celkový počet pod **200** na dokument.

**Q: Je licence vyžadována pro vývojové sestavení?**  
**A:** Dočasná licence odstraňuje vodotisky hodnocení; plná licence je povinná pro jakékoli produkční nasazení.

**Q: Mohu podepisovat PDF chráněné heslem?**  
**A:** Ano – při vytváření objektu `Signature` poskytněte heslo; API soubor interně odemkne.

**Last Updated:** 2026-07-15  
**Tested With:** GroupDocs.Signature 23.9 for Java  
**Author:** GroupDocs  

{< /blocks/products/pf/tutorial-page-section >}
{< /blocks/products/pf/main-container >}
{< /blocks/products/pf/main-wrap-class >}
{< blocks/products/products-backtop-button >}

## Související tutoriály

- [Jak ověřit čárové podpisy v Javě pomocí GroupDocs.Signature](/signature/java/search-verification/groupdocs-signature-java-document-verification/)
- [Jak vyhledat digitální podpisy v dokumentech Java pomocí GroupDocs](/signature/java/search-verification/groupdocs-signature-java-digital-search-tutorial/)
- [Java tutoriál čárových podpisů – Přidání, ověření a správa čárových kódů v PDF](/signature/java/barcode-signatures/)