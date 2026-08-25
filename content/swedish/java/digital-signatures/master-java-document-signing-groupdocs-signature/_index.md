---
categories:
- Java Development
- Document Management
date: '2026-08-25'
description: Lär dig hur du lägger till streckkod i PDF‑dokument i Java med GroupDocs.Signature.
  Denna steg‑för‑steg‑guide visar hur du lägger till GS1DotCode‑streckkoder, extraherar
  bilder och undviker vanliga fallgropar.
keywords:
- how to add barcode
- groupdocs signature java
- pdf document barcode
lastmod: '2026-08-25'
linktitle: Lägg till streckkod i PDF Java
og_description: Lär dig hur du lägger till streckkod i PDF i Java med GroupDocs.Signature.
  Steg‑för‑steg‑handledning, kodexempel och felsökningstips för GS1DotCode‑streckkoder.
og_image_alt: Guide showing Java code to embed GS1DotCode barcode into a PDF using
  GroupDocs.Signature
og_title: Hur man lägger till streckkod i PDF i Java – Komplett guide
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
title: Hur man lägger till streckkod i PDF i Java
type: docs
url: /sv/java/digital-signatures/master-java-document-signing-groupdocs-signature/
weight: 1
---

# Hur du lägger till streckkod i PDF i Java

## Introduktion

Har du någonsin kämpat med dokumentautenticitet i din Java‑applikation? Du är inte ensam. Oavsett om du bygger ett lagersystem, hanterar kontrakt eller arbetar med leveranskedjedokument, finns det en god chans att du behöver ett pålitligt sätt att automatiskt signera och verifiera PDF‑filer.

Traditionella digitala signaturer är bra, men ibland behöver du något mer specialiserat—som streckkodssignaturer som fungerar sömlöst med skanningssystem och automatiserade arbetsflöden. Det är där GS1DotCode‑streckkoder kommer till nytta.

**Vad du kommer att lära dig:**
- Hur du signerar PDF‑dokument med GS1DotCode‑streckkoder i Java
- Hur du extraherar och sparar streckkodssignaturbilder
- När (och varför) du ska använda streckkodssignaturer istället för traditionella metoder
- Vanliga fallgropar och hur du undviker dem

I slutet av den här guiden har du en färdig lösning som du kan integrera i vilket Java‑projekt som helst.

## Snabba svar
- **Vilket bibliotek lägger till streckkoder i PDF‑filer i Java?** GroupDocs.Signature för Java.  
- **Vilket streckkodformat täcks?** GS1DotCode, en kompakt 2‑D‑dotmatris.  
- **Behöver jag en betald licens?** En gratis provversion fungerar för testning; produktion kräver en kommersiell licens.  
- **Kan jag extrahera streckkoden som en bild?** Ja, med `BarcodeSignature`‑API:n.  
- **Vilken Java‑version krävs?** JDK 8 eller högre.

## Vad innebär att lägga till streckkod?

*How to add barcode* avser processen att programatiskt bädda in en maskinläsbar streckkodsgrafik i en PDF‑fil så att streckkoden blir en del av dokumentets innehållsström. Detta innebär att generera streckkodsbilden, placera den på en sida och spara den modifierade PDF‑filen, vilket säkerställer att streckkoden förblir sökbar och utskrivbar.

## Varför välja GS1DotCode‑streckkoder?

GS1DotCode är utformat för situationer där utrymmet är begränsat. Till skillnad från linjära streckkoder som sträcker sig horisontellt, skapar DotCode en 2‑D‑matris av prickar som packar en massa information i ett litet område. Detta gör den perfekt för:
- **Små produktetiketter** där varje millimeter räknas  
- **Hög hastighetsskrivning** på produktionslinjer (formatet är konstruerat för det)  
- **Spårning av leveranskedjan** där du behöver koda komplexa datastrukturer  

Formatet kan hantera upp till **3 116 tecken** i ett kompakt utrymme och läses pålitligt även vid hög hastighet eller med delvis skada. Om du arbetar inom detaljhandel eller logistik använder dina partners sannolikt redan GS1‑standarder—så du talar samma språk.

> **Proffstips:** Använd GS1DotCode när du behöver bädda in mer än 20 tecken på en etikett mindre än 1 tum × 1 tum.

## Förutsättningar

Innan du börjar koda, verifiera att din miljö uppfyller följande krav.

### Nödvändiga bibliotek och beroenden
- **GroupDocs.Signature för Java** 23.12 eller senare (stödjer **30+** dokumentformat)
- Maven eller Gradle för beroendehantering

### Miljöinställning
- **JDK 8** eller nyare installerad och konfigurerad i din `PATH`
- En IDE såsom IntelliJ IDEA, Eclipse eller NetBeans
- En exempel‑PDF‑fil att experimentera med (vilken som helst icke‑skyddad PDF fungerar)

### Kunskapsförutsättningar
- Grundläggande Java‑syntax (variabler, metoder, objekt)
- Bekantskap med Maven‑ eller Gradle‑beroendedeklaration
- Förståelse för fil‑I/O i Java (t.ex. `FileInputStream`)

Om någon av dessa komponenter saknas, pausa och installera dem nu; de senare stegen förutsätter att de finns.

## Konfigurering av GroupDocs.Signature för Java

### Maven
Om du använder Maven, lägg till följande beroende i din `pom.xml`:

```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

Maven kommer automatiskt att ladda ner biblioteket och alla nödvändiga transitiva beroenden.

### Gradle
För Gradle‑användare, infoga denna rad i din `build.gradle`‑fil:

```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

Gradle löser paketet på samma enkla sätt.

### Direkt nedladdning
Om du föredrar manuell hantering, ladda ner JAR‑filerna från den officiella releasesidan: [GroupDocs.Signature for Java releases](https://releases.groupdocs.com/signature/java/). Placera JAR‑filerna på ditt projekts classpath.

**Proffstips:** Maven eller Gradle förenklar framtida uppgraderingar—höj bara versionsnumret.

### Licensanskaffning
GroupDocs erbjuder tre licensalternativ:
- **Gratis provversion** – inget kreditkort, vattenstämplar appliceras på utdata
- **Tillfällig licens** – 30‑dagars fullständig utvärdering
- **Kommersiell licens** – tar bort provbegränsningar och ger produktionsrättigheter

Efter att ha fått en licensfil, placera den i ditt projekts resurser‑mapp och ladda den innan något `Signature`‑objekt skapas.  
`License.setLicense` laddar GroupDocs‑licensfilen, vilket möjliggör full funktion utan provbegränsningar.

Kör följande kodsnutt för att verifiera att biblioteket laddas korrekt:

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

Om du ser “Initialization successful!” är konfigurationen klar. Annars, dubbelkolla classpath och licenssökväg.

## Implementeringsguide

Vi kommer att gå igenom två kärnfunktioner: (1) signera en PDF med en GS1DotCode‑streckkod och (2) extrahera den streckkoden som en bildfil.

### Funktion 1: signera dokument med GS1DotCode‑streckkod

#### Hur signerar du en PDF med en GS1DotCode‑streckkod i Java?

Läs in mål‑PDF‑filen med `new Signature("source.pdf")`, konfigurera ett `BarcodeSignOptions`‑objekt som innehåller GS1‑formaterad data, och anropa `sign()` för att producera en ny PDF som bäddar in streckkoden. Denna operation skriver streckkoden direkt in i PDF‑innehållsströmmen, vilket bevarar den vid utskrift och åter‑skanning.

Processen innefattar tre korta steg: skapa en `Signature`‑instans, konfigurera `BarcodeSignOptions` och anropa `sign()`. Koden nedan demonstrerar varje steg.

##### 1. initiera signatur‑objektet
`Signature`‑klassen är ingångspunkten för alla dokumentbehandlingsoperationer i GroupDocs.Signature.

```java
import com.groupdocs.signature.Signature;

String sourceFilePath = "YOUR_DOCUMENT_DIRECTORY/document.pdf";
final Signature signature = new Signature(sourceFilePath);
```

> **Varför detta är viktigt:** `Signature`‑objektet abstraherar filhantering, strömmar stora PDF‑filer effektivt utan att ladda hela filen i minnet.

##### 2. konfigurera streckkodsalternativ
`BarcodeSignOptions` låter dig ange streckkodstyp, kodad data, position och dimensioner.

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

> **Viktiga punkter:**  
> - Den kodade strängen följer GS1 Application Identifiers (AIs) såsom `(01)` för GTIN, `(15)` för utgångsdatum, etc.  
> - `setLeft()` och `setTop()` använder punkter (72 pt = 1 tum).  
> - Minsta rekommenderade storlek för pålitlig skanning är **108 pt × 108 pt** (1,5 tum × 1,5 tum).

##### 3. signera dokumentet
Lägg till de konfigurerade alternativen i en lista (du kan kombinera flera signaturtyper) och anropa `sign()`.

```java
import java.util.ArrayList;
import java.util.List;

List<com.groupdocs.signature.options.sign.SignOptions> listOptions = new ArrayList<>();
listOptions.add(gs1DotCodeOptions);
signature.sign("YOUR_OUTPUT_DIRECTORY/signed_document_with_gs1dotcode.pdf", listOptions);
```

> **Prestandaanteckning:** Att återanvända en enda `Signature`‑instans för batch‑operationer minskar objekt‑skapande overhead och förbättrar genomströmning.

### Funktion 2: spara streckkodssignaturens innehåll till fil

#### Hur extraherar du en streckkodsbild från en signerad PDF i Java?

`BarcodeSignature` representerar ett streckkodssignaturobjekt extraherat från ett signerat dokument, och ger åtkomst till dess data och bildinnehåll. Skapa en `BarcodeSignature`‑instans (eller hämta en via `search()`), läs dess Base64‑kodade bilddata via `getContent()`, avkoda den och skriv bytes till en PNG‑fil. Detta ger en fristående bild som du kan visa i ett UI eller skicka till en etikettprinter.

##### 1. simulera skapande av streckkodssignatur
I verkliga scenarier skulle du hämta `BarcodeSignature` från ett sökresultat; här instansierar vi den manuellt för illustration.

```java
import com.groupdocs.signature.domain.signatures.BarcodeSignature;
import java.io.FileOutputStream;

String base64String = "SampleBase64EncodedData";
BarcodeSignature barcodeSignature = new BarcodeSignature(base64String);
```

##### 2. spara innehållet till en fil
Avkoda Base64‑strängen och skriv de resulterande bytes till disk med ett try‑with‑resources‑block.

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

> **Gotcha:** `getContent()` kan returnera `null` om signaturen skapades utan att bädda in en bild. Kontrollera alltid `null` innan du skriver.

## Vanliga problem och lösningar

### Problem: streckkoden skannar inte
**Symptom:** Streckkoden ser bra ut i PDF‑visaren men skannrar ger fel.  
**Lösningar:**
- Öka streckkodens storlek till minst **108 pt × 108 pt**.  
- Säkerställ att skrivarupplösningen är **≥ 300 dpi**.  
- Verifiera att GS1‑datasträngen följer korrekt AI‑syntax; en saknad parentes bryter skannern.

### Problem: OutOfMemoryError på stora PDF‑filer
**Symptom:** Bearbetning av dokument större än **50 MB** utlöser heap‑space‑fel.  
**Lösningar:**
- Starta JVM med en större heap, t.ex. `-Xmx2g`.  
- Bearbeta dokument i mindre batcher.  
- Explicit avlasta `Signature`‑objekt: `signature.dispose()` efter varje fil.

### Problem: streckkoden ser suddig ut
**Symptom:** Den renderade streckkoden ser pixelerad ut i den genererade PDF‑filen.  
**Lösningar:**
- Använd större dimensioner; biblioteket renderar vektorgrafik när det är möjligt, men nedskalning efter generering introducerar artefakter.  
- Undvik raster‑till‑vektor‑konverteringar; låt GroupDocs hantera rendering direkt från vektordefinitionen.

### Problem: licensundantag
**Symptom:** Fel som “License not found” eller “Trial limitations exceeded”.  
**Lösningar:**
- Placera licensfilen i classpath‑roten (`src/main/resources`).  
- Anropa `License.setLicense("GroupDocs.Signature.lic")` **innan** någon `Signature`‑instansiering.  
- För tillfälliga licenser, bekräfta utgångsdatumet (30 dagar från utfärdandet).

## När man ska använda detta tillvägagångssätt

### Bra användningsfall
- **Spårning av leveranskedjan** – bädda in produkt‑ID:n, batch‑nummer och utgångsdatum direkt på fraktdokument.  
- **Automatiserad etikettutskrift** – generera streckkoder i realtid för varje PDF‑faktura.  
- **Reglerade industrier** – GS1‑standarder är obligatoriska i många detaljhandels‑ och vårdmiljöer.

### När man bör överväga alternativ
- Om du bara behöver kryptografisk integritet är en standard PKI‑digital signatur mer lämplig.  
- För enkla visuella anteckningar kan en textsignatur eller bildstämpel vara tillräcklig.  
- När dokumentstorlek är en kritisk begränsning, undvik att lägga till högupplösta streckkodsbilder; använd istället QR‑koder som kan vara mindre för jämförbar datadensitet.

## Säkerhetsbästa praxis

### Datavalidering
Sanitera all användargenererad data innan den kodas till en streckkod. Felaktiga GS1‑strängar kan orsaka skanningsfel nedströms eller, i värsta fall, utlösa bufferöverskridningar i äldre skanner‑firmware.

### Åtkomstkontroll
Implementera rollbaserad åtkomstkontroll (RBAC) så att endast auktoriserade användare kan anropa signerings‑API:n. Förvara licensfilen säkert och begränsa filsystembehörigheter.

### Revisionsloggning
Logga varje signeringsoperation med detaljer som användar‑ID, tidsstämpel, källfilens sökväg och exakt GS1‑payload. Exempel på loggkod:

```java
// Simple logging example (use a proper logging framework in production)
System.out.println("Document signed by: " + userId + " at " + new Date());
System.out.println("Barcode data: " + barcodeData);
```

### Manipuleringsdetektering
Kombinera en streckkodssignatur med en kryptografisk digital signatur. Streckkoden ger maskinläsbar data, medan den digitala signaturen garanterar integritet och icke‑förnekelse.

## Praktiska tillämpningar

### 1. leveranskedjehantering
Varje packsedel får en GS1DotCode‑streckkod som kodar leveransens GTIN, batch och destination. Skannrar vid varje kontrollpunkt uppdaterar automatiskt ERP‑systemet, vilket minskar manuella inmatningsfel med **98 %**.

### 2. lagerkontroll
När varor anländer signeras mottagnings‑PDF‑filen med en streckkod som innehåller inköpsordernummer och artikelmängder. Lagerpersonalen skannar streckkoden, och lagerdatabasen uppdateras i realtid.

### 3. detaljhandels‑kassa
Fakturor som skrivs ut med en streckkod låter kassörer hantera returer genom att skanna fakturan istället för att manuellt ange transaktions‑ID, vilket minskar genomsnittlig kassatid med **30 sekunder** per retur.

### 4. hälso‑dokumentation
Recept som signeras med en GS1DotCode‑streckkod bäddar in patient‑ID, läkemedelskod och doseringsinstruktioner. Apotek skannar streckkoden, vilket eliminerar transkriptionsfel som orsakar negativa läkemedelseffekter.

## Prestandaöverväganden

### Minneshantering
GroupDocs.Signature strömmar PDF‑data, men du bör ändå stänga resurser omedelbart:

```java
try (Signature signature = new Signature(sourceFilePath)) {
    // Do your signing operations here
} // Signature automatically disposed here
```

Att använda try‑with‑resources garanterar att `Signature`‑objektet frigör filhandtag även om ett undantag inträffar.

### Tips för batch‑behandling
- Återanvänd samma `BarcodeSignOptions`‑instans när payloaden är identisk över många dokument.  
- Parallellisera signering med `ExecutorService` för CPU‑intensiva arbetsbelastningar; en typisk 8‑kärnig server kan signera **≈ 150 PDF‑filer per minut** när varje fil är under 5 MB.  
- Begränsa externa licensvalideringsanrop för att undvika hastighetsbegränsnings‑throttling.

### Filformatoptimering
- Föredra PDF/A‑1b för arkivering; den komprimerar strömmar och minskar filstorleken med upp till **40 %**.  
- Håll streckkodens dimensioner så små som möjligt; en 1,5 tum × 1,5 tum streckkod lägger till ungefär **15 KB** till en 2 MB PDF.

## Slutsats

Du har nu ett komplett, produktionsklart arbetsflöde för att lägga till GS1DotCode‑streckkodssignaturer till PDF‑filer i Java, extrahera dessa streckkoder som bilder och integrera processen i större dokumenthanterings‑pipeline. Kom ihåg att:
1. Validera GS1‑payloaden innan kodning.  
2. Välj streckkodsdimensioner som balanserar skanningspålitlighet med layoutbegränsningar.  
3. Kombinera streckkodssignaturer med kryptografiska signaturer för full säkerhets täckning.

Nästa steg: utforska andra signaturtyper som erbjuds av GroupDocs.Signature—QR‑koder, textstämplar och digitala certifikat—alla med ett enhetligt API.

---

## Vanliga frågor

**Q: Vad är GS1DotCode och varför är det annorlunda än QR‑koder?**  
A: GS1DotCode är en kompakt 2‑D‑dotmatris som lagrar upp till **3 116 tecken** i ett mindre fotavtryck än QR‑koder, vilket gör den idealisk för små etiketter och hög hastighetsskrivning.

**Q: Kan jag använda en gratis provversion för produktionsdistributioner?**  
A: Gratisprovversionen är begränsad till utvärdering och lägger till en vattenstämpel på utdatafiler. Produktion kräver en köpt eller tillfällig 30‑dagars licens.

**Q: Hur placerar jag streckkoden på en specifik sida?**  
A: Använd `setPageNumber(pageIndex)` på `BarcodeSignOptions`‑objektet, och justera sedan `setLeft()` och `setTop()` för att placera den exakt.

**Q: Stöder GroupDocs.Signature lösenordsskyddade PDF‑filer?**  
A: Ja. Ange lösenordet när du konstruerar `Signature`‑objektet: `new Signature("file.pdf", "password")`.

**Q: Hur kan jag verifiera att en streckkodssignatur har lagts till korrekt?**  
`Signature.search()` söker ett dokument efter signaturer och returnerar en samling matchande signaturobjekt. Använd `Signature.search()` med `BarcodeSearchOptions`. De returnerade `BarcodeSignature`‑objekten innehåller den kodade datan och bildinnehållet för verifiering.

**Q: Vad är den minsta streckkodsstorleken för pålitlig skanning?**  
A: Sikta på minst **108 pt × 108 pt** (1,5 tum × 1,5 tum). Större storlekar förbättrar läsbarheten, särskilt på lågupplösta skrivare.

**Q: Kan jag signera flera PDF‑filer samtidigt?**  
A: Ja. Skapa en trådpool och instansiera ett separat `Signature`‑objekt per tråd; biblioteket är trådsäkert när varje tråd arbetar med sitt eget dokument.

**Q: Finns det någon gräns för hur många streckkoder jag kan bädda in i en enda PDF?**  
A: Ingen hård gräns, men varje streckkod lägger till ungefär **15 KB** data. För PDF‑filer större än **100 MB**, överväg batch‑behandling för att hantera minnesanvändning.

**Q: Fungerar biblioteket på icke‑Windows‑plattformar?**  
A: GroupDocs.Signature för Java är plattformsoberoende och körs på alla operativsystem med en kompatibel JRE, inklusive Linux och macOS.

**Senast uppdaterad:** 2026-08-25  
**Testat med:** GroupDocs.Signature 23.12 för Java  
**Författare:** GroupDocs

## Relaterade handledningar

- [Hur man verifierar streckkodssignaturer i Java med GroupDocs.Signature](/signature/java/barcode-signatures/verify-barcode-signatures-groupdocs-signature-java/)
- [Skapa streckkodssignatur Java – Uppdatera PDF‑streckkoder](/signature/java/barcode-signatures/java-groupdocs-signature-barcode-initialize-update/)
- [Lägg till QR‑kod i PDF Java – Komplett guide med GroupDocs.Signature](/signature/java/qr-code-signatures/qr-code-signatures-java-groupdocs/)