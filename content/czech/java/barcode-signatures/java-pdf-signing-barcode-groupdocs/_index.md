---
categories:
- Java PDF Processing
date: '2026-07-20'
description: Naučte se, jak vytvořit barcode signature v PDF dokumentech pomocí Javy
  a GroupDocs.Signature. Praktický návod krok za krokem s ukázkami kódu a osvědčenými
  postupy.
keywords:
- create barcode signature
- how to add barcode
- generate code128 barcode
- add barcode pdf
- tamper evident barcode
lastmod: '2026-07-20'
linktitle: Vytvořit barcode signature v Javě
og_description: Vytvořte barcode signature v PDF pomocí Javy s GroupDocs.Signature.
  Naučte se krok za krokem, jak přidat Code128 čárové kódy, umístit je a zabezpečit
  dokumenty.
og_image_alt: 'Developer guide: Create barcode signature in PDF using Java and GroupDocs'
og_title: Vytvořit barcode signature v PDF pomocí Javy – Kompletní průvodce
schemas:
- author: GroupDocs
  dateModified: '2026-07-20'
  description: Learn how to create barcode signature in PDF documents using Java and
    GroupDocs.Signature. Step-by-step tutorial with code examples and best practices.
  headline: How to Create Barcode Signature in PDF using Java
  type: TechArticle
- description: Learn how to create barcode signature in PDF documents using Java and
    GroupDocs.Signature. Step-by-step tutorial with code examples and best practices.
  name: How to Create Barcode Signature in PDF using Java
  steps:
  - name: Initialize the Signature object
    text: '**Definition anchor:** The `Signature` class is GroupDocs.Signature''s
      entry point for loading, modifying, and saving PDF documents. First, you need
      to tell GroupDocs which PDF you''re working with: **What''s happening here:**
      The `Signature` object loads your PDF into memory and prepares it for modifi'
  - name: Configure your barcode options (How to add barcode)
    text: '**Definition anchor:** `BarcodeSignOptions` encapsulates all settings required
      to render a barcode inside a PDF. Now let''s create the barcode signature with
      your data: - `"12345678"` is your barcode data — this could be an order ID,
      certificate number, or any identifier you need. - `Code128` is the '
  - name: Position your barcode (How to sign PDF with barcode)
    text: '**Definition anchor:** `SignatureOptions` provides layout properties such
      as page number, size, and alignment. Here''s where GroupDocs really shines —
      percentage‑based positioning means your barcode looks good on any PDF size:
      **Why percentages matter:** Imagine you''re signing both A4 documents and l'
  - name: Sign and save your document (How to add barcode pdf)
    text: 'Time to actually apply the signature and save your work: **Important note:**
      The output directory must exist before you run this code. GroupDocs won''t create
      nested directories for you, so create them first or handle that in your code:
      **What if something goes wrong?** Wrap this in a try‑catch block'
  type: HowTo
- questions:
  - answer: Yes! Call `signature.sign()` multiple times with different `BarcodeSignOptions`
      for each barcode type. Just ensure they don’t overlap.
    question: Can I use different barcode types in the same PDF?
  - answer: Code128 handles most ASCII characters fine. For Unicode or complex data,
      switch to QR codes—they support UTF‑8 encoding.
    question: How do I handle barcodes that contain special characters?
  - answer: Technically up to 128 characters, but readability drops significantly
      above 30‑40 characters. For larger payloads, use QR codes.
    question: What's the maximum data I can store in a Code128 barcode?
  - answer: Not noticeably—barcodes are vector graphics, typically adding only 5‑20
      KB per barcode depending on size and complexity.
    question: Will adding barcodes significantly increase my PDF file size?
  - answer: Yes! Use `options.setRotationAngle(90)` to rotate your barcode, which
      is handy for margin placement.
    question: Can I rotate barcodes or place them vertically?
  type: FAQPage
tags:
- pdf-signing
- barcode-signature
- document-security
- groupdocs
- java
- pdf
title: Jak vytvořit barcode signature v PDF pomocí Javy
type: docs
url: /cs/java/barcode-signatures/java-pdf-signing-barcode-groupdocs/
weight: 1
---

# Jak vytvořit podpis čárového kódu v PDF pomocí Javy

V tomto tutoriálu se naučíte, jak **vytvořit podpis čárového kódu** v PDF souborech pomocí Javy a GroupDocs.Signature. Podpisy čárových kódů vkládají strojově čitelné identifikátory, které jsou zároveň odolné vůči manipulaci a snadno skenovatelné — ideální pro smlouvy, certifikáty, faktury a jakýkoli dokument, který vyžaduje spolehlivé ověření.

## Rychlé odpovědi
- **Co je podpis čárového kódu?** Čárový kód vložený do PDF, který ukládá strukturovaná data a může být čten skenery nebo softwarem.  
- **Který typ čárového kódu se doporučuje?** Code128, protože kompaktně zpracovává alfanumerická data.  
- **Potřebuji licenci?** Pro testování stačí bezplatná zkušební verze; pro produkci je vyžadována plná licence.  
- **Mohu umístit čárový kód na jakoukoli velikost stránky?** Ano — použijte procentuální umístění pro automatické škálování.  
- **Je čárový kód vektorový?** Ano, přidá do PDF jen několik kilobytů a zůstane ostrý při jakémkoli rozlišení.  

## Co je podpis čárového kódu?
Podpis čárového kódu je vektorový čárový kód vložený přímo do stránky PDF, který funguje jak jako vizuální prvek, tak jako kryptografický podpis, který lze později ověřit. Ukládá strukturovaná data, například ID nebo časové razítko, a zajišťuje integritu dokumentu při poskytování strojově čitelného odkazu.

## Proč jsou podpisy čárových kódů důležité pro vaše PDF
Podpisy čárových kódů dodávají PDF kompaktní, strojově čitelný identifikátor, který lze okamžitě naskenovat, čímž se eliminuje ruční zadávání dat a snižuje se chybovost. Protože jsou vloženy jako vektorová grafika, zůstávají ostré při jakémkoli rozlišení a přidají do souboru jen několik kilobytů. Tato kombinace čitelnosti, odolnosti vůči manipulaci a minimální velikosti je ideální pro smlouvy, faktury, certifikáty a jakýkoli dokument vyžadující spolehlivé ověření.

Zde je výzva, se kterou jste pravděpodobně čelili: potřebujete přidat jedinečné identifikátory do PDF, které jsou jak strojově čitelné, tak odolné vůči manipulaci. Možná pracujete na systému správy dokumentů, zpracováváte certifikáty nebo řešíte smlouvy, které je třeba v budoucnu ověřovat.

Právě zde přicházejí na řadu podpisy čárových kódů. Na rozdíl od jednoduchých textových razítek umožňují čárové kódy vložit strukturovaná data, která skenery (a váš software) mohou okamžitě přečíst. Navíc, když je zkombinujete s podepisováním PDF pomocí GroupDocs.Signature pro Javu, získáte výkonný způsob sledování a ověřování dokumentů bez nutnosti složitých databázových dotazů.

V tomto průvodci se naučíte přesně, jak implementovat podpisy čárových kódů ve vašich PDF — od základního nastavení po produkčně připravený kód s flexibilním umístěním. Ať už budujete fakturační systém, generátor certifikátů nebo platformu pro správu smluv, na konci budete mít vše, co potřebujete.

**Co se naučíte:**
- Nastavení GroupDocs.Signature pro Javu během několika minut  
- Vytváření podpisů čárových kódů Code128 (a proč jsou často nejlepší volbou)  
- Umisťování čárových kódů pomocí procentuálního rozvržení, které funguje na jakékoli velikosti PDF  
- Vyhýbání se běžným úskalím, která programátory zaskočí  
- Správné testování vaší implementace  

## Jak vytvořit podpis čárového kódu v Javě
Vytvoření podpisu čárového kódu v Javě zahrnuje načtení cílového PDF, konfiguraci možností čárového kódu (data, typ, velikost, pozice) a následné aplikování podpisu pro vygenerování nového dokumentu. GroupDocs.Signature se postará o vykreslení a kryptografické propojení, takže stačí dodat požadované parametry a spravovat cesty k souborům.

## Předpoklady a kontrolní seznam prostředí

Než se pustíte do práce, ověřte, že máte připravené následující položky:

- **Java Development Kit (JDK) 8 nebo novější** – požadováno pro všechny knihovny GroupDocs Java.  
- **Maven nebo Gradle** – pro správu závislosti GroupDocs.Signature.  
- **IDE** jako IntelliJ IDEA, Eclipse nebo VS Code s rozšířeními pro Javu.  
- **GroupDocs.Signature pro Javu** (doporučena verze 23.12 nebo novější).  
- **Základní znalost Javy** – měli byste být schopni vytvářet třídy, zpracovávat výjimky a pracovat se souborovým I/O.

## Nastavení GroupDocs.Signature ve vašem projektu

Získání knihovny do projektu je jednoduché. Vyberte si nástroj pro sestavení:

**Pro uživatele Maven**, přidejte tuto závislost do souboru `pom.xml`:

```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

**Používáte Gradle?** Přidejte tento řádek do souboru `build.gradle`:

```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

**Preferujete ruční nastavení?** Stáhněte JAR přímo z [GroupDocs.Signature for Java releases](https://releases.groupdocs.com/signature/java/) a přidejte jej do classpath.

### Zajištění licence

Než přejdete do plné produkce, budete chtít vyřešit licencování:

- **Bezplatná zkušební verze:** Ideální pro testování — získáte ji na webu GroupDocs a můžete prozkoumat základní funkce.  
- **Dočasná licence:** Potřebujete více času na vyhodnocení? Požádejte o 30‑denní dočasnou licenci.  
- **Plná licence:** Připravení na produkci? Zakupte licenci pro neomezené používání.  

Zde je rychlá kontrola, zda vše funguje:

```java
Signature signature = new Signature("sample.pdf");
System.out.println("Signature object created successfully.");
```

Pokud se spustí bez chyb, jste připraveni!

## Jak vytvořit podpis čárového kódu v Javě

Nyní k zábavné části — podepíšeme PDF čárovým kódem. Rozdělíme to na malé kroky, abyste přesně věděli, co se děje v každé fázi.

### Krok 1: Inicializace objektu Signature

**Definiční kotva:** Třída `Signature` je vstupním bodem GroupDocs.Signature pro načítání, úpravu a ukládání PDF dokumentů.

Nejprve musíte GroupDocs říct, s jakým PDF pracujete:

```java
Signature signature = new Signature("input.pdf");
```

**Co se zde děje:** Objekt `Signature` načte vaše PDF do paměti a připraví jej k úpravám. Ujistěte se, že cesta k souboru je správná — častým úskalím je používání zpětných lomítek na Windows bez jejich escapování (použijte `\\` nebo raději dopředná lomítka, která fungují napříč platformami).

### Krok 2: Konfigurace možností čárového kódu (Jak přidat čárový kód)

**Definiční kotva:** `BarcodeSignOptions` obsahuje všechna nastavení potřebná k vykreslení čárového kódu v PDF.

Nyní vytvoříme podpis čárového kódu s vašimi daty:

```java
BarcodeSignOptions options = new BarcodeSignOptions("12345678");
options.setEncodeType(BarcodeEncodeType.Code128);
```

- `"12345678"` jsou data vašeho čárového kódu — může se jednat o ID objednávky, číslo certifikátu nebo jakýkoli identifikátor, který potřebujete.  
- `Code128` je typ kódování (více o výběru správného typu níže).  

**Tip:** Code128 zvládne jak čísla, tak písmena, což ho činí univerzálním pro většinu případů. Pokud potřebujete jen čísla, může být jednodušší `Code39`, ale Code128 nabízí větší flexibilitu.

### Krok 3: Umístění čárového kódu (Jak podepsat PDF čárovým kódem)

**Definiční kotva:** `SignatureOptions` poskytuje vlastnosti rozvržení, jako je číslo stránky, velikost a zarovnání.

Zde GroupDocs opravdu zazáří — procentuální umístění znamená, že váš čárový kód bude vypadat dobře na jakékoli velikosti PDF:

```java
options.setLeft(10);   // 10% from the left edge
options.setTop(90);    // 90% from the bottom edge (near the footer)
options.setWidth(30);  // 30% of page width
options.setHeight(10); // 10% of page height
options.setPageNumber(1);
```

**Proč jsou procenta důležitá:** Představte si, že podepisujete jak dokumenty formátu A4, tak právnické formuláře. S procentuálním umístěním se čárový kód automaticky přizpůsobí a bude vypadat konzistentně na obou. Použití pevně daných pixelových hodnot by způsobilo, že čárový kód bude na velkých dokumentech příliš malý a na malých příliš velký.

**Praktický příklad:** Na stránce A4 (595 × 842 bodů) bude čárový kód o šířce 30 % široký přibližně 180 bodů. Na právnické stránce (612 × 1008 bodů) bude široký ~184 bodů — automaticky proporcionální.

### Krok 4: Podepsání a uložení dokumentu (Jak přidat čárový kód do PDF)

Nyní skutečně aplikujeme podpis a uložíme výsledek:

```java
signature.sign(outputPath, options);
```

**Důležitá poznámka:** Výstupní adresář musí existovat před spuštěním kódu. GroupDocs nevytvoří vnořené adresáře automaticky, takže je vytvořte předem nebo to ošetřete ve svém kódu:

```java
new File("output").mkdirs();
```

**Co když se něco pokazí?** Zabalte kód do bloku try‑catch:

```java
try {
    signature.sign("signed.pdf", options);
} catch (Exception e) {
    e.printStackTrace();
}
```

## Výběr správného typu čárového kódu pro vaše potřeby (generování kódu 128)

GroupDocs podporuje více formátů čárových kódů a výběr toho správného má význam. Zde je praktické srovnání:

**Code128 (naše výchozí volba):**
- **Nejlepší pro:** Smíšená alfanumerická data (např. „INV2024-001“)  
- **Kapacita:** až 128 znaků ASCII  
- **Proč vyhrává:** Kompaktní, široce podporovaný, zvládá písmena i čísla  
- **Použijte, když:** Potřebujete flexibilitu a nevíte, jaký typ dat budete kódovat  

**Code39:**
- **Nejlepší pro:** Jednoduché alfanumerické kódy  
- **Kapacita:** 43 znaků (A‑Z, 0‑9 a některé symboly)  
- **Proč zvážit:** Starší skenery jej často podporují lépe  
- **Použijte, když:** Pracujete se staršími systémy nebo je jednoduchost důležitější než hustota dat  

**QR Code:**
- **Nejlepší pro:** Velké objemy dat (URL, JSON)  
- **Kapacita:** až 3 KB dat  
- **Proč je silný:** Umožňuje ukládat komplexní struktury, má vestavěnou korekci chyb  
- **Použijte, když:** Potřebujete vložit strukturovaná data nebo odkazy  

**EAN/UPC:**
- **Nejlepší pro:** Identifikaci produktů  
- **Kapacita:** pevná délka číselných kódů (8‑13 číslic)  
- **Použijte, když:** Pracujete s maloobchodními nebo inventárními systémy  

**Rychlý rozhodovací průvodce:**  
- Potřebujete písmena i čísla? → Code128  
- Jen čísla, jednoduchost? → Code39  
- Hodně dat nebo URL? → QR Code  
- Kódy pro retail/produkty? → EAN/UPC  

## Běžné úskalí a jak se jim vyhnout (tamper evident barcode)

Zde jsou problémy, se kterými se vývojáři nejčastěji setkávají (aby se vám to nestalo):

### Problém 1: Umístění čárového kódu vypadá špatně

**Příznak:** Čárový kód se objeví na neočekávaných místech nebo bude oříznutý.

**Běžné příčiny:**  
- Používání pixelových hodnot na různých velikostech stránek  
- Zapomenutí, že souřadnice PDF začínají v levém dolním rohu, ne v levém horním  
- Okraje posunující obsah mimo viditelnou oblast  

**Řešení:** Vždy používejte procentuální umístění pro konzistenci:

```java
options.setLeft(5);
options.setTop(95);
options.setWidth(40);
options.setHeight(12);
```

### Problém 2: Text čárového kódu je nečitelný

**Příznak:** Kód se zobrazí, ale skenery jej nedokážou přečíst.

**Příčiny:**  
- Čárový kód je příliš malý vzhledem k množství dat  
- Nesprávný typ kódování pro vaše data  
- Nízký kontrast mezi čarami a pozadím  

**Řešení:** Přizpůsobte velikost čárového kódu délce dat. Pro Code128 s 10‑15 znaky cílem alespoň 8‑10 % šířky stránky.

### Problém 3: Výjimky související s cestou k souboru

**Příznak:** `FileNotFoundException` nebo podobné chyby.

**Příčiny:**  
- Hardcodované Windows cesty s jedním zpětným lomítkem  
- Výstupní adresář neexistuje  
- Problémy s oprávněními  

**Řešení:** Používejte dopředná lomítka (fungují všude) a nejprve vytvořte adresáře:

```java
Path output = Paths.get("output/signed.pdf");
Files.createDirectories(output.getParent());
```

### Problém 4: Problémy s pamětí u velkých PDF

**Příznak:** Chyby „Out of memory“ při zpracování velkých dokumentů.

**Řešení:** Po dokončení uzavřete objekt `Signature`, aby se uvolnily prostředky:

```java
signature.close();
```

## Testování implementace čárového kódu

Před nasazením se ujistěte, že vaše čárové kódy skutečně fungují. Praktický kontrolní seznam:

### 1. Test vizuální kontroly
Otevřete podepsané PDF a zkontrolujte:
- Je čárový kód viditelný a správně umístěný?  
- Vypadá ostrý (ne rozmazaný ani pixelovaný)?  
- Je kolem něj dostatek bílého prostoru?

### 2. Test skenování
Použijte aplikaci pro skenování čárových kódů na telefonu (např. “Barcode Scanner” nebo “QR & Barcode Reader”) a ověřte:
- Dokáže skener přečíst váš čárový kód?  
- Odpovídá dekódovaná data tomu, co jste zakódovali?  
- Funguje to z různých úhlů a vzdáleností?

### 3. Test napříč platformami
Otevřete PDF na různých zařízeních:
- Windows (Adobe Reader, Chrome)  
- macOS (Preview, Chrome)  
- Mobilní zařízení (iOS, Android)  

Ujistěte se, že čárový kód se všude vykresluje správně.

### 4. Automatizovaný testovací kód
Zde je jednoduchý test, který můžete spustit:

```java
Signature testSignature = new Signature("signed.pdf");
List<BarcodeSignature> signatures = testSignature.search(BarcodeSignature.class);
if (signatures.size() > 0) {
    System.out.println("Barcode found: " + signatures.get(0).getText());
}
```

## Reálné případy použití podpisů čárových kódů

Podívejme se, kde tato technika skutečně vyniká v produkčních systémech:

### 1. Generování a ověřování certifikátů
**Scénář:** Vytváříte platformu pro školení, která vydává certifikáty o absolvování.  
**Implementace:** Vygenerujte jedinečné ID certifikátu (např. “CERT‑2024‑00123”) a vložte jej jako Code128 čárový kód v pravém dolním rohu. Skenováním kódu vaše API okamžitě načte podrobnosti certifikátu, čímž se eliminuje ruční zadávání dat.

### 2. Systémy sledování faktur
**Scénář:** Vaše firma zpracovává tisíce faktur měsíčně.  
**Implementace:** Přidejte číslo faktury a datum splatnosti jako QR kód umístěný tam, kde ho snadno přečte skenovací zařízení. Automatizované třídící systémy mohou faktury směrovat bez lidského zásahu, což zkrátí dobu zpracování z hodin na minuty.

### 3. Správa právních smluv
**Scénář:** Právnická firma potřebuje sledovat verze a dodatky smluv.  
**Implementace:** Každá verze smlouvy získá unikátní čárový kód, který obsahuje ID smlouvy, číslo verze a datum podpisu. Při auditech skenování okamžitě načte kompletní historii verzí.

### 4. Bezpečnost zdravotních záznamů
**Scénář:** Nemocnice chce zabránit neoprávněnému přístupu k záznamům.  
**Implementace:** Vložte do čárového kódu ID pacienta a časové razítko vytvoření záznamu. Pouze autentizovaná zařízení mohou data dekódovat a přistupovat k plnému záznamu, přičemž každé skenování vytvoří auditní log pro soulad s předpisy.

## Tipy pro optimalizaci výkonu (java document security)

Při podepisování velkého množství PDF je výkon klíčový. Zde jsou tipy, jak udržet věci plynulé:

### Strategie dávkového zpracování
Místo podepisování jednoho dokumentu po druhém zpracovávejte dávky:

```java
for (String filePath : pdfList) {
    Signature batchSignature = new Signature(filePath);
    batchSignature.sign(outputPath, options);
    batchSignature.close();
}
```

**Proč to pomáhá:** Opětovné použití objektu s možnostmi a správné uzavírání prostředků zabraňuje únikům paměti.

### Správa paměti pro velké PDF
Pro PDF větší než 50 MB:
- Zpracovávejte je sekvenčně místo načítání více najednou.  
- Používejte try‑with‑resources pro zajištění úklidu.  
- Sledujte velikost haldy a podle potřeby upravte parametry JVM: `-Xmx2g`.

### Cache často používaných čárových kódů
Pokud podepisujete mnoho dokumentů stejným čárovým kódem, cachujte instanci `BarcodeSignOptions`:

```java
BarcodeSignOptions cachedOptions = new BarcodeSignOptions("STATIC_ID");
cachedOptions.setEncodeType(BarcodeEncodeType.Code128);
```

## Kdy použít podpisy čárových kódů (a kdy ne)

**Ideální scénáře:**
- Potřebujete strojově čitelný identifikátor dokumentu.  
- Dokumenty budou skenovány nebo automaticky zpracovávány.  
- Chcete sledovat manipulaci bez digitálních certifikátů.  
- Vyžaduje se integrace s existující čárovou infrastrukturou.  

**Není vhodné, když:**
- Potřebujete právně závazné digitální podpisy (použijte digitální certifikáty).  
- Dokumenty budou číst jen lidé (stačí jednoduchá textová vodoznak).  
- Pracujete s extrémně malými dokumenty, kde by čárový kód převzal většinu stránky.  
- Bezpečnostní požadavky vyžadují šifrování — čárové kódy jsou viditelné a skenovatelné kdokoli.  

**Můžete kombinovat přístupy?** Rozhodně! Mnoho systémů používá čárové kódy pro sledování a digitální podpisy pro právní platnost.

## Často kladené otázky

**Q: Mohu použít různé typy čárových kódů ve stejném PDF?**  
A: Ano! Zavolejte `signature.sign()` vícekrát s různými `BarcodeSignOptions` pro každý typ čárového kódu. Jen se ujistěte, že se nepřekrývají.

**Q: Jak zacházet s čárovými kódy obsahujícími speciální znaky?**  
A: Code128 podporuje většinu ASCII znaků. Pro Unicode nebo složitější data přejděte na QR kódy — podporují kódování UTF‑8.

**Q: Jaká je maximální velikost dat, kterou mohu uložit do Code128?**  
A: Technicky až 128 znaků, ale čitelnost výrazně klesá nad 30‑40 znaků. Pro větší objemy použijte QR kódy.

**Q: Zvětší přidání čárových kódů podstatně velikost PDF?**  
A: Ne, čárové kódy jsou vektorová grafika, typicky přidají jen 5‑20 KB na kód v závislosti na velikosti a složitosti.

**Q: Můžu otáčet čárové kódy nebo je umístit vertikálně?**  
A: Ano! Použijte `options.setRotationAngle(90)` pro otočení, což je užitečné při umístění na okraj.

**Q: Jak zajistit, aby se čárové kódy objevily na každé stránce vícestránkového PDF?**  
A: Projděte stránky a aplikujte podpis na každou. Podívejte se na třídu `PagesSetup` v dokumentaci GroupDocs, kde můžete určit, které stránky se mají podepsat.

**Q: Co když můj skener nedokáže přečíst vygenerovaný čárový kód?**  
A: Nejprve ověřte, že skener podporuje zvolený typ čárového kódu. Pak zvětšete velikost čárového kódu — většina problémů pramení z příliš malých čar. Cílem je alespoň 1 inch (2,54 cm) šířky pro spolehlivé čtení.

## Další zdroje

**Dokumentace:**  
- [GroupDocs.Signature for Java Docs](https://docs.groupdocs.com/signature/java/)  
- [API Reference Guide](https://reference.groupdocs.com/signature/java/)  

**Stažení a licence:**  
- [Download Latest Version](https://releases.groupdocs.com/signature/java/)  
- [Free Trial Access](https://releases.groupdocs.com/signature/java/)  
- [Get Temporary License](https://purchase.groupdocs.com/temporary-license/)  
- [Purchase Full License](https://purchase.groupdocs.com/buy)  

**Komunita a podpora:**  
- [Support Forum](https://forum.groupdocs.com/c/signature/) - Aktivní komunita s inženýry GroupDocs  

---

**Poslední aktualizace:** 2026-07-20  
**Testováno s:** GroupDocs.Signature 23.12 (Java)  
**Autor:** GroupDocs

```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

```java
import com.groupdocs.signature.Signature;

public class QuickTest {
    public static void main(String[] args) {
        try {
            Signature signature = new Signature("test-document.pdf");
            System.out.println("GroupDocs.Signature is ready to go!");
        } catch (Exception e) {
            System.err.println("Setup issue: " + e.getMessage());
        }
    }
}
```

```java
String filePath = "YOUR_DOCUMENT_DIRECTORY/sample.pdf";
Signature signature = new Signature(filePath);
```

```java
import com.groupdocs.signature.options.sign.BarcodeSignOptions;
import com.groupdocs.signature.domain.barcodes.BarcodeTypes;

BarcodeSignOptions options = new BarcodeSignOptions("12345678");
options.setEncodeType(BarcodeTypes.Code128);
```

```java
import com.groupdocs.signature.domain.enums.MeasureType;
import com.groupdocs.signature.domain.Padding;

// Use percentages instead of fixed pixels
options.setLocationMeasureType(MeasureType.Percents);
options.setLeft(5);  // 5% from the left edge
options.setTop(5);   // 5% from the top

// Size it proportionally too
options.setSizeMeasureType(MeasureType.Percents);
options.setWidth(10);  // 10% of page width
options.setHeight(5);  // 5% of page height

// Add some breathing room with margins
Padding margins = new Padding();
margins.setLeft(1);
margins.setTop(1);
margins.setRight(1);
options.setMargin(margins);
```

```java
String outputFilePath = "YOUR_OUTPUT_DIRECTORY/SignWithPercents/sample_signed.pdf";
signature.sign(outputFilePath, options);
```

```java
Path outputPath = Paths.get(outputFilePath);
Files.createDirectories(outputPath.getParent());
signature.sign(outputFilePath, options);
```

```java
try {
    signature.sign(outputFilePath, options);
    System.out.println("PDF signed successfully at: " + outputFilePath);
} catch (Exception e) {
    System.err.println("Signing failed: " + e.getMessage());
    e.printStackTrace();
}
```

```java
options.setLocationMeasureType(MeasureType.Percents);
options.setLeft(5);  // 5% from left works on any page width
```

```java
options.setWidth(10);  // Give it room to breathe
options.setHeight(5);  // Maintain proper aspect ratio
```

```java
String filePath = "documents/sample.pdf";  // Works on Windows, Mac, Linux
Files.createDirectories(Paths.get("output/signed"));
```

```java
try (Signature signature = new Signature(filePath)) {
    signature.sign(outputFilePath, options);
} // Automatically closes and releases memory
```

```java
import org.junit.Test;
import static org.junit.Assert.*;

public class BarcodeSignatureTest {
    
    @Test
    public void testBarcodeSigning() {
        String testPdf = "test-data/sample.pdf";
        String output = "test-output/signed.pdf";
        
        try (Signature signature = new Signature(testPdf)) {
            BarcodeSignOptions options = new BarcodeSignOptions("TEST123");
            options.setEncodeType(BarcodeTypes.Code128);
            
            signature.sign(output, options);
            
            // Verify output file exists
            assertTrue(new File(output).exists());
            
            // Verify file size increased (signature was added)
            long originalSize = new File(testPdf).length();
            long signedSize = new File(output).length();
            assertTrue(signedSize > originalSize);
            
        } catch (Exception e) {
            fail("Signing should not throw exception: " + e.getMessage());
        }
    }
}
```

```java
List<String> pdfFiles = Arrays.asList("doc1.pdf", "doc2.pdf", "doc3.pdf");

for (String pdfFile : pdfFiles) {
    try (Signature signature = new Signature(pdfFile)) {
        BarcodeSignOptions options = createBarcodeOptions(); // Reuse options
        signature.sign(getOutputPath(pdfFile), options);
    }
}
```

```java
// Create options once, reuse many times
BarcodeSignOptions templateOptions = createStandardBarcodeOptions();

// For each document, clone and customize
BarcodeSignOptions documentOptions = templateOptions.clone();
documentOptions.setText(uniqueDocumentId);
```

## Související tutoriály

- [Java Barcode Signature Tutorial - Add, Verify & Manage Barcodes in PDFs](/signature/java/barcode-signatures/)
- [Create Barcode Signature in Java – Update PDF Barcodes](/signature/java/barcode-signatures/java-groupdocs-signature-barcode-initialize-update/)
- [How to read QR code PDF using Java and GroupDocs.Signature](/signature/java/barcode-signatures/java-pdf-barcode-search-groupdocs-signature-api/)