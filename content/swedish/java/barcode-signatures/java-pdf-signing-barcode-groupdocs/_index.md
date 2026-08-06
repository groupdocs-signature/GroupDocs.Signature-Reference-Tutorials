---
categories:
- Java PDF Processing
date: '2026-07-20'
description: Lär dig hur du skapar barcode-signatur i PDF-dokument med Java och GroupDocs.Signature.
  Steg-för-steg handledning med kodexempel och bästa praxis.
keywords:
- create barcode signature
- how to add barcode
- generate code128 barcode
- add barcode pdf
- tamper evident barcode
lastmod: '2026-07-20'
linktitle: Skapa barcode-signatur i Java
og_description: Skapa barcode-signatur i PDF med Java med GroupDocs.Signature. Lär
  dig steg-för-steg hur du lägger till Code128 barcode, placerar dem och säkrar dokument.
og_image_alt: 'Developer guide: Create barcode signature in PDF using Java and GroupDocs'
og_title: Skapa barcode-signatur i PDF med Java – Fullständig guide
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
title: Hur man skapar barcode-signatur i PDF med Java
type: docs
url: /sv/java/barcode-signatures/java-pdf-signing-barcode-groupdocs/
weight: 1
---

# Hur man skapar streckkodsignatur i PDF med Java

I den här handledningen kommer du att lära dig hur du **skapar streckkodsignatur** i PDF‑filer med Java och GroupDocs.Signature. Streckkodsignaturer inbäddar maskinläsbara identifierare som både är manipulering‑evidenta och enkla att skanna—perfekta för kontrakt, certifikat, fakturor och alla dokument som kräver pålitlig verifiering.

## Snabba svar
- **Vad är en streckkodsignatur?** En streckkod inbäddad i en PDF som lagrar strukturerad data och kan läsas av skannrar eller programvara.  
- **Vilken streckkodstyp rekommenderas?** Code128, eftersom den hanterar alfanumerisk data kompakt.  
- **Behöver jag en licens?** En gratis provversion fungerar för testning; en full licens krävs för produktion.  
- **Kan jag placera streckkoden på vilken sidstorlek som helst?** Ja—använd procentbaserad positionering för automatisk skalning.  
- **Är streckkoden vektorbaserad?** Ja, den lägger bara till några kilobyte till PDF‑filen och förblir skarp vid vilken upplösning som helst.  

## Vad är en streckkodsignatur?
En streckkodsignatur är en vektorbaserad streckkod som inbäddas direkt i en PDF‑sida, och fungerar både som ett visuellt element och som en kryptografisk signatur som kan valideras senare. Den lagrar strukturerad data, såsom ID:n eller tidsstämplar, och säkerställer dokumentets integritet samtidigt som den ger en maskinläsbar referens.

## Varför streckkodsignaturer är viktiga för dina PDF‑filer
Streckkodsignaturer ger PDF‑filer ett kompakt, maskinläsbart identifieringsnummer som kan skannas omedelbart, vilket eliminerar manuell datainmatning och minskar fel. Eftersom de inbäddas som vektorgrafik förblir de skarpa vid vilken upplösning som helst och lägger bara till några kilobyte till filen. Denna kombination av läsbarhet, manipulering‑evidens och minimal storlek gör dem idealiska för kontrakt, fakturor, certifikat och alla dokument som kräver pålitlig verifiering.

Här är en utmaning du förmodligen har stött på: du behöver lägga till unika identifierare i PDF‑filer som både är maskinläsbara och manipulering‑evidenta. Kanske arbetar du med ett dokumenthanteringssystem, bearbetar certifikat eller hanterar kontrakt som behöver verifieras senare.

Det är här streckkodsignaturer är praktiska. Till skillnad från enkla textstämplar låter streckkoder dig inbädda strukturerad data som skannrar (och din programvara) kan läsa omedelbart. Dessutom, när du kombinerar dem med PDF‑signering via GroupDocs.Signature för Java, får du ett kraftfullt sätt att spåra och verifiera dokument utan att behöva komplexa databassökningar.

I den här guiden kommer du att lära dig exakt hur du implementerar streckkodsignaturer i dina Java‑PDF‑filer — från grundläggande installation till produktionsklar kod med flexibel positionering. Oavsett om du bygger ett fakturasystem, en certifikatgenerator eller en plattform för kontraktshantering, kommer du att ha allt du behöver när du är klar.

**Vad du kommer att behärska:**
- Installera GroupDocs.Signature för Java på några minuter  
- Skapa Code128‑streckkodsignaturer (och varför de ofta är ditt bästa val)  
- Positionera streckkoder med procentbaserade layouter som fungerar för alla PDF‑storlekar  
- Undvika vanliga fallgropar som får utvecklare att snubbla  
- Testa din implementation på rätt sätt  

## Hur man skapar streckkodsignatur i Java
Att skapa en streckkodsignatur i Java innebär att ladda mål‑PDF‑filen, konfigurera streckkodsalternativen såsom data, typ, storlek och position, och sedan applicera signaturen för att generera ett nytt dokument. GroupDocs.Signature hanterar rendering och kryptografisk bindning, så du behöver bara ange de önskade parametrarna och hantera filsökvägar.

## Förutsättningar och miljöchecklista
Innan du börjar, kontrollera att du har följande saker redo:

- **Java Development Kit (JDK) 8 eller nyare** – krävs för alla GroupDocs Java‑bibliotek.  
- **Maven eller Gradle** – för att hantera GroupDocs.Signature‑beroendet.  
- **En IDE** såsom IntelliJ IDEA, Eclipse eller VS Code med Java‑tillägg.  
- **GroupDocs.Signature för Java** (version 23.12 eller nyare rekommenderas).  
- **Grundläggande Java‑kunskaper** – du bör vara bekväm med att skapa klasser, hantera undantag och arbeta med fil‑I/O.  

## Installera GroupDocs.Signature i ditt projekt
Att få biblioteket in i ditt projekt är enkelt. Välj ditt byggverktyg:

**För Maven‑användare**, lägg till detta beroende i din `pom.xml`:

```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

**Använder du Gradle?** Lägg till den här raden i din `build.gradle`:

```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

**Föredrar du manuell installation?** Ladda ner JAR‑filen direkt från [GroupDocs.Signature för Java‑utgåvor](https://releases.groupdocs.com/signature/java/) och lägg till den i din classpath.

### Skaffa din licens i ordning
Innan du går i full produktion vill du hantera licensiering:

- **Gratis provversion:** Perfekt för testning — hämta den från GroupDocs‑webbplatsen för att utforska kärnfunktionerna.  
- **Tillfällig licens:** Behöver du mer tid för utvärdering? Ansök om en 30‑dagars tillfällig licens.  
- **Full licens:** Klar för produktion? Köp en licens för obegränsad användning.  

Här är en snabb kontroll för att säkerställa att allt fungerar:

```java
Signature signature = new Signature("sample.pdf");
System.out.println("Signature object created successfully.");
```

Om det körs utan fel är du klar!

## Hur man skapar streckkodsignatur i Java
Nu till den roliga delen — låt oss signera en PDF med en streckkod. Vi delar upp det i små steg så att du förstår exakt vad som händer i varje steg.

### Steg 1: Initiera Signature‑objektet
**Definition ankare:** `Signature`‑klassen är GroupDocs.Signatures ingångspunkt för att ladda, modifiera och spara PDF‑dokument.

Först måste du tala om för GroupDocs vilken PDF du arbetar med:

```java
Signature signature = new Signature("input.pdf");
```

**Vad som händer här:** `Signature`‑objektet laddar din PDF i minnet och förbereder den för modifieringar. Se till att din filsökväg är korrekt — en vanlig fallgrop är att använda bakåtsnedstreck på Windows utan att escape:a dem (använd `\\` eller bara framåtsnedstreck, som fungerar på alla plattformar).

### Steg 2: Konfigurera dina streckkodsalternativ (Hur man lägger till streckkod)
**Definition ankare:** `BarcodeSignOptions` kapslar in alla inställningar som krävs för att rendera en streckkod i en PDF.

Låt oss nu skapa streckkodsignaturen med din data:

```java
BarcodeSignOptions options = new BarcodeSignOptions("12345678");
options.setEncodeType(BarcodeEncodeType.Code128);
```

- `"12345678"` är din streckkodsdata — det kan vara ett order‑ID, certifikatnummer eller någon identifierare du behöver.  
- `Code128` är kodningstypen (mer om hur du väljer rätt typ nedan).  

**Pro‑tips:** Code128 kan hantera både siffror och bokstäver, vilket gör den mångsidig för de flesta användningsområden. Om du bara behöver siffror kan `Code39` vara enklare, men Code128 ger dig mer flexibilitet.

### Steg 3: Positionera din streckkod (Hur man signerar PDF med streckkod)
**Definition ankare:** `SignatureOptions` tillhandahåller layout‑egenskaper såsom sidnummer, storlek och justering.

Här glänser GroupDocs verkligen — procentbaserad positionering betyder att din streckkod ser bra ut på alla PDF‑storlekar:

```java
options.setLeft(10);   // 10% from the left edge
options.setTop(90);    // 90% from the bottom edge (near the footer)
options.setWidth(30);  // 30% of page width
options.setHeight(10); // 10% of page height
options.setPageNumber(1);
```

**Varför procent är viktigt:** Föreställ dig att du signerar både A4‑dokument och legal‑storleksformulär. Med procentuell positionering skalas din streckkod automatiskt för att se konsekvent ut på båda. Att använda fasta pixelvärden skulle göra streckkoden för liten på stora dokument eller för stor på små.

**Exempel från verkligheten:** På en A4‑sida (595 × 842 punkter) blir en streckkod med 30 % bredd cirka 180 punkter bred. På en legal‑sida (612 × 1008 punkter) blir den cirka 184 punkter bred — automatiskt proportionell.

### Steg 4: Signera och spara ditt dokument (Hur man lägger till streckkod i PDF)
Dags att faktiskt applicera signaturen och spara ditt arbete:

```java
signature.sign(outputPath, options);
```

**Viktig notering:** Utdata‑katalogen måste finnas innan du kör koden. GroupDocs skapar inte underkataloger åt dig, så skapa dem först eller hantera det i din kod:

```java
new File("output").mkdirs();
```

**Vad händer om något går fel?** Omge detta med ett try‑catch‑block:

```java
try {
    signature.sign("signed.pdf", options);
} catch (Exception e) {
    e.printStackTrace();
}
```

## Välja rätt streckkodstyp för dina behov (generera code128 streckkod)
GroupDocs stöder flera streckkodformat, och valet av rätt är viktigt. Här är en praktisk jämförelse:

**Code128 (Our Default Choice):**
- **Bäst för:** Blandad alfanumerisk data (ID:n som "INV2024-001")  
- **Kapacitet:** Upp till 128 ASCII‑tecken  
- **Varför den vinner:** Kompakt, brett stöd, hanterar både bokstäver och siffror  
- **Använd när:** Du behöver flexibilitet och inte vet vilken typ av data du kommer att koda  

**Code39:**
- **Bäst för:** Enkla alfanumeriska koder  
- **Kapacitet:** 43 tecken (A‑Z, 0‑9 och vissa symboler)  
- **Varför överväga:** Äldre skannrar stödjer den ofta bättre  
- **Använd när:** Du arbetar med äldre system eller när enkelhet är viktigare än datatäthet  

**QR Code:**
- **Bäst för:** Stora mängder data (URL:er, JSON‑payloads)  
- **Kapacitet:** Upp till 3 KB data  
- **Varför den är kraftfull:** Kan lagra komplexa datastrukturer, inbyggd felkorrigering  
- **Använd när:** Du behöver inbädda strukturerad data eller URL:er  

**EAN/UPC:**
- **Bäst för:** Produktidentifiering  
- **Kapacitet:** Fast längd numeriska koder (8‑13 siffror)  
- **Använd när:** Du arbetar med detaljhandel eller lagerhanteringssystem  

**Snabb beslutsguide:**  
- Behöver du bokstäver och siffror? → Code128  
- Endast siffror, håll det enkelt? → Code39  
- Mycket data eller URL:er? → QR‑kod  
- Detaljhandel/produktkoder? → EAN/UPC  

## Vanliga fallgropar och hur du undviker dem (manipulerings‑evident streckkod)
Här är de problem som utvecklare oftast stöter på (så att du slipper dem):

### Problem 1: Streckkodens position ser felaktig ut
**Symtom:** Din streckkod visas på oväntade platser eller blir avklippt.

**Vanliga orsaker:**  
- Använda pixelvärden på olika sidstorlekar  
- Glömma att PDF‑koordinater startar från nedre vänstra hörnet, inte övre vänstra  
- Marginaler som skjuter innehållet utanför det synliga området  

**Lösning:** Använd alltid procentbaserad positionering för konsistens:

```java
options.setLeft(5);
options.setTop(95);
options.setWidth(40);
options.setHeight(12);
```

### Problem 2: Streckkodstexten är oläslig
**Symtom:** Den kodade texten visas men skannrar kan inte läsa den.

**Orsaker:**  
- Streckkoden är för liten för mängden data  
- Fel kodningstyp för din data  
- Låg kontrast mellan streck och bakgrund  

**Lösning:** Anpassa streckkodens storlek efter datalängden. För Code128 med 10‑15 tecken, sikta på minst 8‑10 % av sidbredden.

### Problem 3: Undantag för filsökväg
**Symtom:** `FileNotFoundException` eller liknande fel.

**Orsaker:**  
- Hårdkodade Windows‑sökvägar med enkla bakåtsnedstreck  
- Utdata‑katalogen finns inte  
- Filbehörighetsproblem  

**Lösning:** Använd framåtsnedstreck (de fungerar överallt) och skapa kataloger först:

```java
Path output = Paths.get("output/signed.pdf");
Files.createDirectories(output.getParent());
```

### Problem 4: Minnesproblem med stora PDF‑filer
**Symtom:** Minnesbristfel när stora dokument bearbetas.

**Lösning:** Stäng `Signature`‑objektet när du är klar för att frigöra resurser:

```java
signature.close();
```

## Testa din streckkodimplementation
Innan du distribuerar, se till att dina streckkoder faktiskt fungerar. Här är en praktisk testchecklista:

### 1. Visuell inspektionstest
- Öppna din signerade PDF och kontrollera:
- Är streckkoden synlig och korrekt positionerad?
- Ser den skarp ut (inte suddig eller pixelerad)?
- Finns det tillräckligt med vitt utrymme runt den?

### 2. Skannertest
Använd en streckkodsskannerapp på din telefon (t.ex. “Barcode Scanner” eller “QR & Barcode Reader”) för att verifiera:
- Skannern kan läsa din streckkod
- Den avkodade datan matchar det du kodade
- Den fungerar från olika vinklar och avstånd

### 3. Plattformöverskridande test
Öppna din PDF på olika enheter:
- Windows (Adobe Reader, Chrome)
- Mac (Preview, Chrome)
- Mobila enheter (iOS, Android)

Se till att streckkoden renderas korrekt överallt.

### 4. Automatiserad testkod
Här är ett enkelt test du kan köra:

```java
Signature testSignature = new Signature("signed.pdf");
List<BarcodeSignature> signatures = testSignature.search(BarcodeSignature.class);
if (signatures.size() > 0) {
    System.out.println("Barcode found: " + signatures.get(0).getText());
}
```

## Verkliga användningsfall för streckkodsignaturer
Låt oss titta på var denna teknik verkligen lyser i produktionssystem:

### 1. Generering och verifiering av certifikat
**Scenario:** Du bygger en utbildningsplattform som utfärdar avslutningscertifikat.  
**Implementation:** Generera ett unikt certifikat‑ID (t.ex. “CERT‑2024‑00123”) och inbädda det som en Code128‑streckkod i det nedre högra hörnet. Genom att skanna streckkoden kan ditt API hämta certifikatdetaljerna omedelbart, vilket eliminerar manuell datainmatning.

### 2. Fakturaspårningssystem
**Scenario:** Ditt företag behandlar tusentals fakturor varje månad.  
**Implementation:** Lägg till fakturanummer och förfallodatum som en QR‑kod placerad där skanningsutrustning enkelt kan läsa den. Automatiska sorteringssystem kan dirigera fakturor utan mänsklig inblandning, vilket minskar bearbetningstiden från timmar till minuter.

### 3. Juridisk kontraktshantering
**Scenario:** En advokatbyrå behöver spåra kontraktsversioner och ändringar.  
**Implementation:** Varje kontraktsversion får en unik streckkodidentifierare som inkluderar kontrakts‑ID, versionsnummer och signeringsdatum. Skanning under revisioner hämtar automatiskt hela versionshistoriken.

### 4. Säkerhet för medicinska journaler
**Scenario:** Ett sjukhus vill förhindra obehörig åtkomst till journaler.  
**Implementation:** Inbädda patient‑ID och tidsstämpel för journalens skapande i en streckkod. Endast autentiserade enheter kan avkoda och komma åt hela journalen, och varje skanning skapar en revisionslogg för efterlevnad.

## Prestandaoptimeringstips (java dokument säkerhet)
När du signerar många PDF‑filer är prestanda viktigt. Här är några tips för att hålla allt igång smidigt:

### Batch‑bearbetningsstrategi
Istället för att signera ett dokument i taget, batcha dem:

```java
for (String filePath : pdfList) {
    Signature batchSignature = new Signature(filePath);
    batchSignature.sign(outputPath, options);
    batchSignature.close();
}
```

**Varför detta hjälper:** Återanvändning av options‑objektet och korrekt stängning av resurser förhindrar minnesläckor.

### Minneshantering för stora PDF‑filer
För PDF‑filer större än 50 MB:
- Bearbeta dem sekventiellt istället för att ladda flera samtidigt.  
- Använd try‑with‑resources för att säkerställa städning.  
- Övervaka heap‑storlek och justera JVM‑parametrar vid behov: `-Xmx2g`.

### Cacha ofta använda streckkoder
Om du signerar många dokument med samma streckkod, cacha `BarcodeSignOptions`‑instansen:

```java
BarcodeSignOptions cachedOptions = new BarcodeSignOptions("STATIC_ID");
cachedOptions.setEncodeType(BarcodeEncodeType.Code128);
```

## När du ska använda streckkodsignaturer (och när du inte bör)
**Perfekta scenarier:**
- Du behöver maskinläsbara dokumentidentifierare.  
- Dokument kommer att skannas eller bearbetas automatiskt.  
- Du vill ha manipulering‑evident spårning utan digitala certifikat.  
- Integration med befintlig streckkodsinfrastruktur krävs.  

**Inte idealiskt när:**
- Du behöver juridiskt bindande digitala signaturer (använd digitala certifikat istället).  
- Dokument endast kommer att visas av människor (en enkel textvattenstämpel kan räcka).  
- Du arbetar med extremt små dokument där en streckkod skulle dominera sidan.  
- Säkerhetskrav kräver kryptering—streckkoder är synliga och kan skannas av vem som helst.  

**Kan du kombinera metoder?** Absolut! Många system använder både streckkodsignaturer för spårning och digitala signaturer för juridisk giltighet.

## Vanliga frågor
**Q: Kan jag använda olika streckkodstyper i samma PDF?**  
A: Ja! Anropa `signature.sign()` flera gånger med olika `BarcodeSignOptions` för varje streckkodstyp. Se bara till att de inte överlappar.

**Q: Hur hanterar jag streckkoder som innehåller specialtecken?**  
A: Code128 hanterar de flesta ASCII‑tecken bra. För Unicode eller komplex data, byt till QR‑koder—de stödjer UTF‑8‑kodning.

**Q: Vad är den maximala mängden data jag kan lagra i en Code128‑streckkod?**  
A: Tekniskt upp till 128 tecken, men läsbarheten minskar markant över 30‑40 tecken. För större payloads, använd QR‑koder.

**Q: Kommer tillägg av streckkoder att avsevärt öka min PDF‑filstorlek?**  
A: Inte märkbart—streckkoder är vektorgrafik, vanligtvis lägger de bara till 5‑20 KB per streckkod beroende på storlek och komplexitet.

**Q: Kan jag rotera streckkoder eller placera dem vertikalt?**  
A: Ja! Använd `options.setRotationAngle(90)` för att rotera din streckkod, vilket är praktiskt för placering i marginalen.

**Q: Hur får jag streckkoder att visas på varje sida i en flersidig PDF?**  
A: Iterera genom sidorna och applicera signaturen på varje. Kontrollera `PagesSetup`‑klassen i GroupDocs‑dokumentationen för att styra vilka sidor som signeras.

**Q: Vad händer om min streckkodsskanner inte kan läsa den genererade streckkoden?**  
A: Först, verifiera att skannern stödjer den valda streckkodstypen. Öka sedan streckkodens storlek—de flesta skanningsproblem beror på för små streck. Sikta på minst 1 tum (2,54 cm) bredd för pålitlig läsning.

## Ytterligare resurser
**Documentation:**  
- [GroupDocs.Signature for Java Docs](https://docs.groupdocs.com/signature/java/)  
- [API Reference Guide](https://reference.groupdocs.com/signature/java/)  

**Downloads and Licensing:**  
- [Download Latest Version](https://releases.groupdocs.com/signature/java/)  
- [Free Trial Access](https://releases.groupdocs.com/signature/java/)  
- [Get Temporary License](https://purchase.groupdocs.com/temporary-license/)  
- [Purchase Full License](https://purchase.groupdocs.com/buy)  

**Community and Support:**  
- [Support Forum](https://forum.groupdocs.com/c/signature/) - Active community with GroupDocs engineers  

**Last Updated:** 2026-07-20  
**Tested With:** GroupDocs.Signature 23.12 (Java)  
**Author:** GroupDocs

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

## Relaterade handledningar

- [Java Barcode Signature Tutorial - Lägg till, verifiera och hantera streckkoder i PDF](/signature/java/barcode-signatures/)
- [Skapa streckkodsignatur i Java – Uppdatera PDF‑streckkoder](/signature/java/barcode-signatures/java-groupdocs-signature-barcode-initialize-update/)
- [Hur man läser QR‑kod PDF med Java och GroupDocs.Signature](/signature/java/barcode-signatures/java-pdf-barcode-search-groupdocs-signature-api/)