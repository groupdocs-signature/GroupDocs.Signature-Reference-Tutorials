---
categories:
- Java Development
date: '2026-06-11'
description: Naučte se, jak podepsat PDF pomocí Java pomocí GroupDocs.Signature, přidat
  Digital Signature a Timestamp. Průvodce krok za krokem s ukázkami kódu a osvědčenými
  postupy.
keywords:
- how to sign pdf
- add digital signature pdf
- timestamp pdf signature
- java pdf signature library
- groupdocs signature java
lastmod: '2026-06-11'
linktitle: Add Digital Signature do PDF Java
schemas:
- author: GroupDocs
  dateModified: '2026-06-11'
  description: Learn how to sign PDF with Java using GroupDocs.Signature, add digital
    signature and timestamp. Step-by-step guide with code examples and best practices.
  headline: 'How to Sign PDF with Java: Add Digital Signature and Timestamp'
  type: TechArticle
- description: Learn how to sign PDF with Java using GroupDocs.Signature, add digital
    signature and timestamp. Step-by-step guide with code examples and best practices.
  name: 'How to Sign PDF with Java: Add Digital Signature and Timestamp'
  steps:
  - name: Import Required Classes
    text: The following imports give you access to signature configuration, positioning,
      and timestamp functionality.
  - name: Define Your File Paths
    text: Set up paths for your input PDF, certificate, and where you want the signed
      PDF saved. Keep the certificate file secure; it contains your private key.
  - name: Initialize the Signature Object
    text: Create a `Signature` instance pointing to the PDF you want to sign. This
      loads the PDF into memory and prepares it for signing.
  - name: Configure Signature Properties and Timestamp
    text: The `DigitalSignature` class represents the cryptographic seal that will
      be embedded in the PDF. You can also attach a timestamp from a trusted authority.
      * **ContactInfo** – e.g., `john.doe@company.com` * **Location** – e.g., `New
      York Office` * **Reason** – e.g., `Contract Approval` We use FreeTSA
  - name: Configure Digital Sign Options
    text: The `SignOptions` class ties together the certificate, signature properties,
      and visual placement. Alignment enums control where the signature appears.
  - name: Sign and Save the Document
    text: Execute the signing process and write the signed PDF to disk. The returned
      `SignResult` object tells you whether the operation succeeded and lists any
      warnings.
  type: HowTo
- questions:
  - answer: A digital signature uses cryptographic algorithms to verify identity and
      detect tampering, while an electronic signature can be as simple as a typed
      name.
    question: What's the difference between a digital signature and an electronic
      signature?
  - answer: Only for the timestamp service; the cryptographic signing itself runs
      locally.
    question: Do I need internet connectivity to sign PDFs?
  - answer: Any modification breaks the signature, and PDF viewers will display a
      warning indicating the document has been altered.
    question: Can signed PDFs be edited later?
  - answer: Most PDF readers verify automatically; programmatically, use GroupDocs.Signature's
      verification API to check status, signer details, and timestamp validity.
    question: How do I verify a signed PDF?
  - answer: The embedded timestamp proves the signature was created while the certificate
      was still valid, preserving legal standing.
    question: What happens if my certificate expires after I've signed documents?
  type: FAQPage
tags:
- pdf-signing
- digital-signatures
- java-security
- groupdocs
title: 'Jak podepsat PDF pomocí Java: Add Digital Signature a Timestamp'
type: docs
url: /cs/java/digital-signatures/digital-signature-timestamp-pdf-java-groupdocs/
weight: 1
---

# Jak podepsat PDF pomocí Javy a časové razítko

Chtěli jste někdy poslat důležitý dokument a obávat se, že by ho někdo mohl později pozměnit? Nejste sami. Ať už budujete podnikovou správu dokumentů, vytváříte platformu pro podepisování smluv, nebo jen potřebujete programově zabezpečit své PDF soubory, **jak podepsat PDF** s důvěryhodným časovým razítkem je řešení. Přidání digitálního podpisu nejen dokazuje, kdo soubor podepsal, ale také vytváří neměnný záznam o *přesně* kdy k podpisu došlo.

## Rychlé odpovědi
- **Jaká knihovna zjednodušuje podepisování PDF v Javě?** GroupDocs.Signature for Java.  
- **Potřebuji internetové připojení?** Pouze pro autoritu časového razítka; samotné podepisování probíhá offline.  
- **Mohu pro testování použít samopodepsaný certifikát?** Ano, vygenerujte jej pomocí `keytool`.  
- **Existuje limit velikosti?** Knihovna může podepisovat PDF až do 500 MB, aniž by načítala celý soubor do paměti.  
- **Kolik formátů GroupDocs podporuje?** Více než 50 vstupních a výstupních formátů, včetně DOCX, XLSX, PPTX, HTML a obrázků.

## Proč jsou digitální podpisy důležité (a proč potřebujete časová razítka)

Načtěte své PDF, aplikujte kryptografické razítko a vložte důvěryhodné časové razítko — tento dvoustupňový proces zaručuje autentizaci, integritu a neodmítnutí. Časové razítko dokazuje, že podpis existoval v konkrétním okamžiku, i když certifikát pro podpis později vyprší nebo bude odvolán.

## Jak podepsat PDF pomocí Javy?

Načtěte své PDF pomocí `new Signature("input.pdf")`, nakonfigurujte objekt `DigitalSignature`, připojte časové razítko od důvěryhodné autority a zavolejte `sign()` — celá operace se dokončí během několika řádků kódu. GroupDocs.Signature automaticky zpracovává parsování certifikátu, výpočet hash a získání časového razítka, takže se můžete soustředit na obchodní logiku místo kryptografie.

## Nastavení GroupDocs.Signature pro Javu

### Metody integrace

Vyberte si nástroj pro sestavení, který používáte:

**Pro uživatele Maven:**  
Přidejte tuto závislost do svého `pom.xml`:
```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

**Pro uživatele Gradle:**  
Přidejte toto do svého `build.gradle`:
```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

**Přímé stažení (pokud dáváte přednost):**  
Navštivte [GroupDocs.Signature for Java releases](https://releases.groupdocs.com/signature/java/) a stáhněte soubor JAR. Přidejte jej ručně do classpath vašeho projektu. Podívejte se na [GroupDocs.Signature Documentation](https://docs.groupdocs.com/signature/java/) pro podrobnou referenci API. Pro nejnovější sestavení viz [Latest Version & Releases](https://releases.groupdocs.com/signature/java/).

Tip: Používejte Maven nebo Gradle, pokud je to možné — usnadní to správu závislostí a aktualizace v budoucnu.

### Zajištění licence

GroupDocs nabízí několik možností, v závislosti na tom, kde ve svém projektu jste:

1. **Free Trial** – Ideální pro vyzkoušení. [Download Trial Version](https://releases.groupdocs.com/signature/java/) a vyzkoušejte všechny funkce.  
2. **Temporary License** – Potřebujete plný přístup pro vývoj bez vodotisku z trial verze? Získejte 30‑denní dočasnou licenci.  
3. **Commercial License** – Pro produkční použití, [Buy License](https://purchase.groupdocs.com/buy). Ceny se liší podle typu nasazení.

Potřebujete pomoc? Navštivte [GroupDocs Forum](https://forum.groupdocs.com/c/signature/).

### Základní inicializace

Třída `Signature` je nejvyšší objekt GroupDocs.Signature, který představuje jeden PDF soubor v paměti. Po vytvoření instance všechny operace čtení a zápisu probíhají přes tento objekt.
```java
import com.groupdocs.signature.Signature;

String filePath = "YOUR_DOCUMENT_DIRECTORY/sample.pdf";
final Signature signature = new Signature(filePath);
```

Jednoduché, že? Stačí ji nasměrovat na váš PDF soubor a můžete začít. Objekt `Signature` je vaše hlavní rozhraní pro všechny operace podepisování.

## Jak přidat digitální podpis do PDF v Javě: krok za krokem

Načtěte své PDF, nakonfigurujte podrobnosti podpisu, připojte časové razítko a uložte podepsaný dokument — vše v přehledném lineárním postupu.

### Krok 1: Import požadovaných tříd

Následující importy vám poskytují přístup k nastavení podpisu, umístění a funkci časového razítka.
```java
import com.groupdocs.signature.Signature;
import com.groupdocs.signature.domain.enums.HorizontalAlignment;
import com.groupdocs.signature.domain.enums.VerticalAlignment;
import com.groupdocs.signature.domain.signatures.PdfDigitalSignature;
import com.groupdocs.signature.domain.structs.TimeStamp;
import com.groupdocs.signature.options.sign.DigitalSignOptions;
```

### Krok 2: Definujte cesty k souborům

Nastavte cesty k vašemu vstupnímu PDF, certifikátu a místu, kam chcete uložit podepsané PDF. Uchovávejte soubor s certifikátem v bezpečí; obsahuje váš soukromý klíč.
```java
String filePath = "YOUR_DOCUMENT_DIRECTORY/sample.pdf";
String certificatePath = "YOUR_DOCUMENT_DIRECTORY/certificate.pfx";
String outputFilePath = "YOUR_OUTPUT_DIRECTORY/digitallySignedTimeStamp.pdf";
```

### Krok 3: Inicializujte objekt Signature

Vytvořte instanci `Signature`, která ukazuje na PDF, které chcete podepsat. Tím se PDF načte do paměti a připraví k podepsání.
```java
final Signature signature = new Signature(filePath);
```

### Krok 4: Nakonfigurujte vlastnosti podpisu a časové razítko

Třída `DigitalSignature` představuje kryptografické razítko, které bude vloženo do PDF. Můžete také připojit časové razítko od důvěryhodné autority.
```java
PdfDigitalSignature pdfDigitalSignature = new PdfDigitalSignature();
pdfDigitalSignature.setContactInfo("Contact Information");
pdfDigitalSignature.setLocation("Location Info");
pdfDigitalSignature.setReason("Signing Reason");

// Configure the TimeStamp with URL, User Id, and Password
TimeStamp timeStamp = new TimeStamp("https://freetsa.org/tsr", "User Id", "Password");
pdfDigitalSignature.setTimeStamp(timeStamp);
```

* **ContactInfo** – např. `john.doe@company.com`  
* **Location** – např. `New York Office`  
* **Reason** – např. `Contract Approval`  

Pro demonstraci používáme FreeTSA (bezplatnou autoritu časových razítek). V produkci zvolte komerční TSA pro zaručenou dostupnost a právní platnost.

### Krok 5: Nakonfigurujte možnosti digitálního podpisu

Třída `SignOptions` spojuje certifikát, vlastnosti podpisu a vizuální umístění. Výčty zarovnání určují, kde se podpis zobrazí.
```java
DigitalSignOptions options = new DigitalSignOptions(certificatePath);
options.setPassword("YourCertificatePassword"); // Certificate password
options.setSignature(pdfDigitalSignature); // Attach the PdfDigitalSignature object

// Specify signature alignment (where it appears on the page)
options.setVerticalAlignment(VerticalAlignment.Bottom);
options.setHorizontalAlignment(HorizontalAlignment.Right);
```

### Krok 6: Podepište a uložte dokument

Spusťte proces podepisování a zapište podepsané PDF na disk. Vrácený objekt `SignResult` vám sdělí, zda operace uspěla, a vypíše případná varování.
```java
try {
    SignResult signResult = signature.sign(outputFilePath, options);
    System.out.println("Document signed successfully!");
    System.out.println("Output: " + outputFilePath);
} catch (Exception e) {
    throw new RuntimeException("Error during signing process: " + e.getMessage());
}
```

## Běžné úskalí, kterým se vyhnout

### 1. Problémy s certifikátem

**Problém:** chyby „Invalid certificate“.  
**Řešení:** Ověřte heslo pomocí `keytool -list -v -keystore your.pfx`.
```bash
keytool -list -v -keystore certificate.pfx -storetype PKCS12
```

### 2. Časové limity služby časových razítek

**Problém:** časové limity sítě při kontaktování TSA.  
**Řešení:** Otestujte konektivitu (`curl -I https://freetsa.org/tsr`), přidejte logiku opakování nebo nastavte záložní TSA.
```java
new File(outputFilePath).getParentFile().mkdirs();
```

### 3. Problémy s oprávněním souborů

**Problém:** „Access denied“ při ukládání.  
**Řešení:** Ujistěte se, že výstupní adresář existuje a aplikace má oprávnění k zápisu.
```bash
keytool -genkeypair -alias mykey -keyalg RSA -keysize 2048 -storetype PKCS12 -keystore certificate.pfx -validity 365
```

### 4. Problémy s pamětí u velkých PDF

**Problém:** `OutOfMemoryError` u velkých souborů.  
**Řešení:** Zvyšte haldu JVM (`-Xmx4g`) nebo zpracovávejte soubory po dávkách.

### 5. Nesprávné umístění podpisu

**Problém:** podpis překrývá existující obsah.  
**Řešení:** Nejprve otestujte nastavení zarovnání; pro pixel‑dokonalé umístění použijte možnosti založené na souřadnicích.

## Tipy pro správu certifikátů

### Získání certifikátu pro vývoj

Vygenerujte samopodepsaný certifikát pomocí Java `keytool` pro testovací účely.
```java
   String certPassword = System.getenv("CERT_PASSWORD");
   ```

### Nejlepší postupy pro certifikáty

1. **Nikdy nezakódujte hesla** – používejte proměnné prostředí.  
2. **Rotujte certifikáty** před jejich vypršením.  
3. **Ukládejte soukromé klíče** v zabezpečeném hardwaru (HSM) pro aplikace s vysokou úrovní zabezpečení.  
4. **Zálohujte certifikáty** na chráněném místě.  
5. **Validujte certifikáty** před podepsáním, abyste zachytili vypršené nebo odvolané.

## Bezpečnostní nejlepší postupy

### 1. Chraňte soukromé klíče

Ukládejte certifikáty mimo adresář projektu, používejte konfigurace specifické pro prostředí a zvažte HSM pro podnikovou nasazení.

### 2. Validujte vstupní PDF

Zkontrolujte poškození, existující podpisy, limity velikosti a shodu obsahu před podepsáním.

### 3. Implementujte auditní logování

Logujte každou operaci podepisování s časovým razítkem, uživatelem, názvem dokumentu a stavem.
```java
try {
    SignResult result = signature.sign(outputFilePath, options);
    logger.info("Document signed: " + filePath + " by " + signerEmail);
} catch (Exception e) {
    logger.error("Signing failed: " + filePath + " - " + e.getMessage());
    // Handle appropriately
}
```

### 4. Používejte důvěryhodné autority časových razítek

Nikdy se nespoléhejte na lokální systémový čas; vždy požádejte o časové razítko od TSA kompatibilního s RFC 3161.

### 5. Implementujte zpracování chyb

Zachytávejte výjimky, aniž byste odhalili citlivé detaily.
```java
try {
    signature.sign(outputFilePath, options);
} catch (Exception e) {
    // Log detailed error internally
    logger.error("Signing error: " + e.getMessage(), e);
    // Return generic error to client
    throw new ApplicationException("Unable to sign document. Please try again.");
}
```

## Reálné případy použití a aplikace

### 1. Systémy správy smluv

Zaměstnanci elektronicky podepisují NDA a smlouvy; časová razítka dokazují přesně, kdy byl každý kontrakt přijat.

### 2. Zpracování finančních dokumentů

Dávkově podepisujte faktury a objednávky, čímž poskytujete neměnný auditní záznam pro regulátory.

### 3. Ověřování vzdělávacích osvědčení

Univerzity vydávají nefalšovatelné výpisy, které lze okamžitě ověřit pomocí odkazu s QR kódem.

### 4. Správa softwarových licencí

Generujte licenční certifikáty s digitálním podpisem a časovým razítkem, aby se zabránilo padělání.

### 5. Regulační soulad (FDA 21 CFR Part 11, atd.)

Společnosti vyrábějící zdravotnická zařízení podepisují SOP a validační zprávy; časová razítka splňují požadavky na neodmítnutí.

## Úvahy o výkonu a optimalizaci

### Správa paměti

Zpracovávejte velké PDF v dávkách, rychle uzavírejte objekty `Signature` a zvyšujte velikost haldy podle potřeby.

### Optimalizace sítě pro časová razítka

Sdružujte HTTP spojení, implementujte exponenciální backoff retry a cachujte časová razítka pro rychlé následné podepisování.

### Nejlepší postupy pro dávkové zpracování
```java
// Pseudo‑code: process a list of PDFs in parallel, limiting to 5 concurrent TSA calls
```
*Vyhněte se spouštění příliš mnoha vláken; 5‑10 souběžných podepisování vyvažuje propustnost a zatížení TSA.*

### Optimalizace diskových I/O

Používejte SSD pro dočasné soubory, minimalizujte čtecí/zápisové cykly a po každém běhu podepisování odstraňujte dočasné artefakty.

## Průvodce řešením problémů

### Chyba: „Invalid Certificate Password“

**Řešení:** Ověřte heslo pomocí `keytool -list -keystore your.pfx`.
```java
ExecutorService executor = Executors.newFixedThreadPool(5);
List<Future<SignResult>> futures = new ArrayList<>();

for (String pdfPath : pdfPaths) {
    futures.add(executor.submit(() -> {
        try (Signature sig = new Signature(pdfPath)) {
            return sig.sign(outputPath, options);
        }
    }));
}

// Wait for all to complete
for (Future<SignResult> future : futures) {
    SignResult result = future.get();
    // Process result
}

executor.shutdown();
```

### Chyba: „Timestamp Authority Not Responding“

**Řešení:** Otestujte URL TSA, zkontrolujte pravidla firewallu a přidejte logiku záložního TSA.
```bash
keytool -list -v -keystore certificate.pfx -storetype PKCS12
```

### Chyba: „PDF is Already Signed“

**Řešení:** Nejprve detekujte existující podpisy; buď přidejte kontra‑podpis, nebo podepište novou kopii.

### Chyba: „Access Denied“ při ukládání

**Řešení:** Ujistěte se, že výstupní adresář existuje, aplikace má práva k zápisu a žádný jiný proces soubor neblokuje.
```java
TimeStamp timeStamp;
try {
    timeStamp = new TimeStamp("https://freetsa.org/tsr", "", "");
} catch (Exception e) {
    // Fallback to alternative TSA
    timeStamp = new TimeStamp("https://alternate-tsa.com/tsr", "", "");
}
```

### Chyba: OutOfMemoryError

**Řešení:** Zvyšte haldu JVM, zpracovávejte PDF v menších dávkách nebo přejděte na streamingové API pro velmi velké soubory.

## Závěr a další kroky

Naučili jste se **jak podepsat PDF** soubory pomocí Javy, přidat důvěryhodné časové razítko a řešit běžné úskalí. Dále prozkoumejte:
1. Přidání více polí pro podpis pro více‑stranné dohody.  
2. Programatické ověřování podpisů pomocí GroupDocs.Signature.  
3. Přizpůsobení vzhledu podpisu (obrázky, text, umístění).  
4. Vytvoření robustní služby pro dávkové podepisování s frontou a monitorováním.

## Často kladené otázky

**Q: Jaký je rozdíl mezi digitálním podpisem a elektronickým podpisem?**  
A: Digitální podpis používá kryptografické algoritmy k ověření identity a detekci manipulace, zatímco elektronický podpis může být tak jednoduchý jako napsané jméno.

**Q: Potřebuji internetové připojení k podepisování PDF?**  
A: Pouze pro službu časových razítek; samotné kryptografické podepisování probíhá lokálně.

**Q: Lze podepsané PDF později upravovat?**  
A: Jakákoli úprava rozbije podpis a PDF prohlížeče zobrazí varování, že dokument byl změněn.

**Q: Jak ověřím podepsané PDF?**  
A: Většina PDF čteček ověřuje automaticky; programaticky použijte ověřovací API GroupDocs.Signature k ověření stavu, údajů o podepisujícím a platnosti časového razítka.

**Q: Co se stane, pokud mi po podepsání dokumentů vyprší certifikát?**  
A: Vložené časové razítko dokazuje, že podpis byl vytvořen, když byl certifikát ještě platný, čímž zachovává právní platnost.

**Q: Můžu to použít s cloudovým úložištěm (S3, Azure Blob, atd.)?**  
A: Ano — stáhněte PDF do dočasného umístění, podepište jej a poté nahrajte podepsanou verzi zpět do cloudu.

**Q: Existují limity velikosti souborů?**  
A: Knihovna zvládá PDF až do 500 MB, aniž by načítala celý soubor do paměti; větší soubory mohou vyžadovat streaming.

**Q: Kolik stojí GroupDocs.Signature pro komerční použití?**  
A: Ceny se liší podle typu nasazení; kontaktujte prodejní tým GroupDocs pro aktuální sazby. Pro vyzkoušení jsou k dispozici bezplatné trial verze a dočasné licence.

**Q: Funguje to na Linux serverech?**  
A: Rozhodně. GroupDocs.Signature pro Javu je platformově nezávislý a běží na jakémkoli OS s JRE.

---

**Poslední aktualizace:** 2026-06-11  
**Testováno s:** GroupDocs.Signature 23.9 for Java  
**Autor:** GroupDocs

```java
File outputFile = new File(outputFilePath);
outputFile.getParentFile().mkdirs(); // Create directories if needed

if (!outputFile.canWrite() && outputFile.exists()) {
    throw new IOException("Cannot write to " + outputFilePath);
}
```

## Související tutoriály

- [Jak ověřit digitální certifikáty v Javě – kompletní průvodce s ukázkami kódu](/signature/java/digital-signatures/java-certificate-verification-groupdocs-signature/)
- [Jak programově podepsat PDF v Javě s GroupDocs.Signature](/signature/java/digital-signatures/sign-pdfs-groupdocs-signature-java/)
- [Přidat obrázkový podpis do PDF v Javě s GroupDocs](/signature/java/image-signatures/sign-pdf-image-signature-groupdocs-java/)