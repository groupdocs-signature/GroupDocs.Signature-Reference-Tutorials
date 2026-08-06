---
date: '2026-07-15'
description: Lär dig hur du lägger till barcode PDF Java med GroupDocs.Signature –
  steg‑för‑steg guide för att sign, verify, search, update och delete barcode signatures
  i Java-dokument.
keywords:
- add barcode pdf java
- groupdocs barcode signature
- java document signing
lastmod: '2026-07-15'
linktitle: Barcode Signature Java‑guide
og_description: Lär dig hur du lägger till barcode PDF Java med GroupDocs.Signature
  – steg‑för‑steg guide för att sign, verify, search, update och delete barcode signatures
  i Java-dokument.
og_image_alt: Guide showing how to add barcode PDF Java using GroupDocs.Signature
og_title: Lägg till barcode PDF Java – Signera & verifiera med GroupDocs
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
title: Lägg till barcode PDF Java – Signera & verifiera med GroupDocs
type: docs
url: /sv/java/digital-signatures/java-document-signature-groupdocs-signature-barcode/
weight: 1
---

# Lägg till streckkod PDF Java – Signera & Verifiera med GroupDocs

Om du behöver ett snabbt, visuellt sätt att märka dokument för interna arbetsflöden är det att lägga till en streckkod i en PDF i Java en perfekt lösning. Med **GroupDocs.Signature** kan du bädda in, verifiera, söka, uppdatera och ta bort streckkodssignaturer utan den extra bördan av fullständiga PKI‑baserade digitala signaturer. Denna handledning guidar dig genom varje steg, från miljöinställning till produktionsklara bästa praxis.

## Snabba svar
- **Vilket bibliotek lägger till streckkod i PDF‑filer i Java?** GroupDocs.Signature för Java.  
- **Kan jag signera PDF, Word och bilder?** Ja – API‑et stöder över 30 format.  
- **Behöver jag licens för utveckling?** En tillfällig 30‑dagars licens är gratis; en fullständig licens krävs för produktion.  
- **Hur många kodrader behövs för att signera en PDF?** Endast två rader: skapa ett `Signature`‑objekt och anropa `sign`.  
- **Är streckkodverifiering skiftlägeskänslig?** Ja – texten måste matcha exakt, inklusive skiftläge och blanksteg.

## Vad är add barcode pdf java?
`add barcode pdf java` avser processen att med Java‑kod bädda in en streckkod (såsom Code128, QR eller Data Matrix) i en PDF‑fil. Denna teknik ger en maskinläsbar tagg som kan skannas eller verifieras programmässigt, vilket möjliggör snabb dokumentspårning i interna system.

## Varför använda streckkodssignaturer istället för fullständiga digitala signaturer?
Streckkodssignaturer är **30‑50 % snabbare** att generera och verifiera än PKI‑baserade digitala signaturer, och de fungerar pålitligt efter en utskrifts‑skanningscykel. De kräver dessutom ingen certifikathantering, vilket gör dem idealiska för högvolym, interna arbetsflöden där kryptografiskt bevis inte är obligatoriskt.

## Förutsättningar

- **Java Development Kit (JDK) 8+** – Java 11 eller 17 rekommenderas för bättre prestanda.  
- **IDE** – IntelliJ IDEA eller Eclipse (exemplen använder IntelliJ‑syntax).  
- **Byggverktyg** – Maven eller Gradle för beroendehantering.  

### Lägga till GroupDocs.Signature i ditt projekt

Det enklaste sättet att komma igång är att lägga till biblioteket via ditt byggverktyg. Så här gör du:

**Maven‑användare** – Lägg till detta i din `pom.xml`:

```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

**Gradle‑användare** – Lägg till detta i din `build.gradle`:

```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

**Direkt JAR‑nedladdning** – Om du föredrar manuell installation, hämta JAR‑filen från [GroupDocs.Signature releases](https://releases.groupdocs.com/signature/java/) och lägg till den i din classpath.

### Skaffa licens

GroupDocs.Signature är inte gratis för produktionsbruk, men du har flexibla alternativ:

- **Gratis provperiod** – Ladda ner från [GroupDocs download page](https://releases.groupdocs.com/signature/java/) för att testa funktionerna (utvärderingsvattenmärken läggs till).  
- **Tillfällig licens** – Få 30 dagars full åtkomst via [GroupDocs' temporary license page](https://purchase.groupdocs.com/temporary-license/) – perfekt för proof‑of‑concept.  
- **Full licens** – För produktionsdistribution, se [GroupDocs purchase options](https://purchase.groupdocs.com/buy).  

**Pro‑tips:** Börja med den tillfälliga licensen för utveckling; den tar bort vattenmärken när du byter till en permanent nyckel.

### Snabb miljökontroll

När du har lagt till beroendet, kör ett enkelt röktest:

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

Om programmet körs utan fel är din miljö klar. Om du stöter på problem, kontrollera JDK‑versionen och exakt vilken biblioteksversion du lagt till.

## När ska man använda streckkodssignaturer

Streckkodssignaturer glänser i specifika scenarier:

- **Interna dokumentarbetsflöden** – Spåra fakturor, inköpsorder eller memon genom godkännandekedjor.  
- **Högvolym‑bearbetning** – Signera tusentals dokument snabbt; streckkodsgenerering är upp till **2× snabbare** än fullständig digital signering.  
- **Utskrifts‑skanningsbroar** – Streckkoder överlever utskrifts‑skanningscykeln, vilket gör dem idealiska för hybridprocesser med papper och digitalt.  
- **Integration med äldre system** – Existerande streckkodsläsare kan läsa taggarna utan extra mjukvara.  
- **Revisionsspår** – Bädda in transaktions‑ID eller tidsstämplar som revisorer kan verifiera omedelbart.

Undvik streckkodssignaturer för juridiska kontrakt, högsäkerhetsdokument eller externa partnerutbyten där PKI‑baserade digitala signaturer krävs.

## Ställa in GroupDocs.Signature för Java

### Kärnklassdefinition

Klassen `Signature` är ingångspunkten för alla signerings-, verifierings-, sök‑, uppdaterings‑ och borttagningsoperationer i GroupDocs.Signature.

```java
import com.groupdocs.signature.Signature;
```

### Grundläggande initiering

Skapa ett `Signature`‑objekt som pekar på målfilen:

```java
Signature signature = new Signature("path/to/your/document.pdf");
```

**Viktiga anteckningar**

- Sökvägar kan vara absoluta eller relativa; använd `System.getProperty("user.home")` för plattformsoberoende kompatibilitet.  
- GroupDocs stöder **30+ in‑ och utdataformat**, inklusive PDF, DOCX, XLSX, PPTX och PNG.  
- Frigör alltid resurser med `signature.dispose()` eller ett try‑with‑resources‑block:

```java
try (Signature signature = new Signature("path/to/your/document.pdf")) {
    // Your signing operations here
} catch (Exception e) {
    System.err.println("Error working with document: " + e.getMessage());
}
```

Nu är du redo att lägga till streckkoder.

## Hur lägger jag till en streckkod i en PDF i Java?

Läs in käll‑PDF‑filen med `new Signature("input.pdf")`, konfigurera ett `BarcodeSignature`‑objekt (t.ex. Code128 med texten “John Smith”) och anropa `sign` för att producera den signerade filen – allt i tre koncisa kodrader. Detta tillvägagångssätt låter dig bädda in en maskinläsbar tagg samtidigt som dokumentlayouten förblir intakt, och det fungerar för alla stödda format, inte bara PDF.

### Steg‑för‑steg‑implementation

#### 1. Definiera filsökvägar

Ange platserna för käll‑ och målfilen:

```java
String filePath = "YOUR_DOCUMENT_DIRECTORY/sample.docx";
String outputFilePath = "YOUR_OUTPUT_DIRECTORY/signed_sample.docx";
```

#### 2. Skapa signaturhanteraren

Initiera hanteraren med källdokumentet:

```java
Signature signature = new Signature(filePath);
```

#### 3. Konfigurera streckkodsalternativ

Ett `BarcodeSignature`‑objekt definierar de visuella och datamässiga egenskaperna för streckkoden som ska bäddas in. Ställ in streckkodstyp, kodad text, position, storlek, färg och valfri läsbar teckensnitt:

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

> **Pro‑tips:** Om den kodade strängen överstiger 20 tecken, öka streckkodens bredd för att undvika skanningsfel.

#### 4. Tillämpa signaturen

Utför signeringsoperationen och generera målfilen:

```java
signature.sign(outputFilePath, signOptions);
```

#### 5. Exempel från verkligheten

I ett fakturagodkännandesystem kan du bädda in godkännandets medarbetar‑ID och en tidsstämpel:

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

Den resulterande PDF‑filen innehåller nu en skanningsbar streckkod som kodar all nödvändig godkännandemetadata.

## Hur verifierar jag en streckkodssignatur i ett Java‑dokument?

Metoden `Signature.verify` kontrollerar ett dokument för matchande streckkodssignaturer baserat på angivna alternativ och returnerar en boolean som indikerar om den förväntade streckkoden finns. Verifiering är användbar för automatiserade arbetsflöden där du måste bekräfta att ett dokument har behandlats av rätt part innan vidare åtgärder.

### Verifieringssteg

#### 1. Läs in det signerade dokumentet

```java
Signature signature = new Signature("YOUR_OUTPUT_DIRECTORY/signed_sample.docx");
```

#### 2. Ställ in verifieringskriterier

Definiera exakt text, streckkodformat och sidnummer du förväntar dig:

```java
BarcodeVerifyOptions verifyOptions = new BarcodeVerifyOptions();
verifyOptions.setAllPages(false); // Only check the first page
verifyOptions.setPageNumber(1);
verifyOptions.setEncodeType(BarcodeTypes.Code128);
verifyOptions.setText("John Smith");
```

#### 3. Kör verifieringen

Utför kontrollen och hantera resultatet:

```java
boolean isValid = signature.verify(verifyOptions) != null;

if (isValid) {
    System.out.println("Document signature verified successfully!");
} else {
    System.out.println("Warning: Signature verification failed!");
}
```

**Vanligt mönster:** För att bara bekräfta att *någon* streckkod av en given typ finns, utelämna `setText`‑filtret:

```java
BarcodeVerifyOptions flexibleOptions = new BarcodeVerifyOptions();
flexibleOptions.setAllPages(true);
flexibleOptions.setEncodeType(BarcodeTypes.Code128);
// No setText() call = accept any text with this barcode type

boolean hasAnySignature = signature.verify(flexibleOptions) != null;
```

Eller verifiera endast streckkodformatet utan att bry dig om innehållet:

```java
BarcodeVerifyOptions formatOnly = new BarcodeVerifyOptions();
formatOnly.setEncodeType(BarcodeTypes.QR);
// Confirms a QR code exists, regardless of content
```

> **Varning:** Verifiering är skift‑ och blankstegskänslig; trimma och normalisera data innan signering.

## Hur söker jag efter streckkodssignaturer i ett dokument?

Metoden `Signature.search` skannar ett dokument efter streckkodssignaturer som matchar de angivna `BarcodeSearchOptions` och returnerar en samling som innehåller varje streckkods position, sidnummer och kodat värde. Denna funktion möjliggör massutdrag av metadata utan att öppna varje fil manuellt.

### Sökflöde

#### 1. Initiera sökningen

```java
Signature signature = new Signature("YOUR_OUTPUT_DIRECTORY/signed_sample.docx");
```

#### 2. Konfigurera sökparametrar

Ange sidintervall, streckkodstyp eller textfilter:

```java
BarcodeSearchOptions searchOptions = new BarcodeSearchOptions();
searchOptions.setAllPages(true); // Search the entire document
```

Avgränsa sökningen för att förbättra prestanda:

```java
BarcodeSearchOptions narrowSearch = new BarcodeSearchOptions();
narrowSearch.setAllPages(false);
narrowSearch.setPageNumber(1); // Only search page 1
narrowSearch.setEncodeType(BarcodeTypes.Code128); // Only find Code128 barcodes
```

#### 3. Utför sökningen

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

#### 4. Exempel på datautdrag

Hämta godkännandedata från varje streckkod i en fakturabatch:

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

> **Prestandatips:** För dokument med mer än 100 sidor, begränsa alltid sökningen till de sidor som faktiskt innehåller streckkoder; detta kan minska körtiden med upp till **70 %**.

## Hur uppdaterar jag en befintlig streckkodssignatur?

Metoden `Signature.update` ändrar visuella attribut för en befintlig streckkodssignatur – såsom position, storlek eller färg – samtidigt som den kodade datan bevaras. Detta är praktiskt när layoutändringar krävs efter att dokumentet redan har signerats.

### Uppdateringsprocedur

#### 1. Hitta signaturer att uppdatera

```java
Signature signature = new Signature("YOUR_OUTPUT_DIRECTORY/signed_sample.docx");

BarcodeSearchOptions searchOptions = new BarcodeSearchOptions();
searchOptions.setAllPages(true);

List<BarcodeSignature> signatures = signature.search(BarcodeSignature.class, searchOptions);
```

#### 2. Modifiera önskade egenskaper

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

Du kan ändra flera attribut på en gång:

```java
bcSignature.setLeft(50);
bcSignature.setTop(50);
bcSignature.setWidth(150);
bcSignature.setHeight(45);
// Note: You can't change the encoded text or barcode type with update
// For that, you'd need to delete and re-sign
```

#### 3. Spara ändringarna

```java
ByteArrayOutputStream outputStream = new ByteArrayOutputStream();
signature.update(outputStream, signaturesToUpdate);

// If you want to save to a file instead:
// signature.update("path/to/updated_document.docx", signaturesToUpdate);
```

#### 4. Verkligt scenario

Omplacera alla signaturer för att undvika överlappning med en ny företagslogotyp:

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

> **Begränsning:** Att ändra den kodade texten kräver borttagning och en ny signaturinsättning.

## Hur tar jag bort streckkodssignaturer från ett dokument?

Metoden `Signature.delete` tar permanent bort valda streckkodssignaturer från ett dokument, både den visuella delen och den kodade datan. Använd denna operation när du rensar testsignaturer eller när en streckkod inte längre är relevant.

### Borttagningssteg

#### 1. Lokalisera signaturerna

```java
Signature signature = new Signature("YOUR_OUTPUT_DIRECTORY/signed_sample.docx");

BarcodeSearchOptions searchOptions = new BarcodeSearchOptions();
searchOptions.setAllPages(true);

List<BarcodeSignature> signatures = signature.search(BarcodeSignature.class, searchOptions);
```

#### 2. Ta bort valda signaturer

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

#### 3. Villkorligt borttagningsexempel

Ta bara bort streckkoder äldre än en viss tidsstämpel (förutsatt att tidsstämpeln är en del av den kodade texten):

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

> **Varning:** Borttagning kan inte ångras; arbeta alltid på en kopia av produktionsfiler under testning.

#### 4. Batch‑borttagningsmönster

Rensa testsignaturer före en release:

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

## Streckkodstyper: En praktisk guide

Att välja rätt streckkod påverkar skanningspålitlighet, datakapacitet och skrivarkompatibilitet.

### Code128 (Mest vanliga)

- **När den ska användas:** Alfanumerisk data, hög densitet, utskrivna dokument.  
- **Fördelar:** Kompakt, fungerar med standardläsare, skrivs tydligt i små storlekar.  
- **Nackdelar:** Begränsad till ASCII, mindre fel‑resistent än 2‑D‑koder.  

Exempel:

```java
BarcodeSignOptions code128 = new BarcodeSignOptions("INV-2025-042", BarcodeTypes.Code128);
```

### QR‑kod (Bäst för mobil)

- **När den ska användas:** Mobilskanning, stora datamängder (URL‑er, JSON, osv.), dokument som kan skadas.  
- **Fördelar:** Upp till 4 000 tecken, inbyggd felkorrigering, smartphone‑vänlig.  
- **Nackdelar:** Större visuellt fotavtryck, kräver högre upplösning för små storlekar.  

Exempel:

```java
String jsonData = "{\"invoice\":\"INV-042\",\"amount\":1500.00,\"approver\":\"john@company.com\"}";
BarcodeSignOptions qrCode = new BarcodeSignOptions(jsonData, BarcodeTypes.QR);
```

### Code39 (Gammal pålitlig)

- **När den ska användas:** Legacy‑läsarmiljöer, behov av mänskligt läsbar text.  
- **Fördelar:** Bred legacy‑support, enkel format, ingen kontrollsumma krävs.  
- **Nackdelar:** Låg datadensitet, begränsat teckensnitt, tar mer plats.  

### Data Matrix (Kompakt kraftpaket)

- **När den ska användas:** Extremt begränsat utrymme, märkning av små föremål, hög‑densitetsdata.  
- **Fördelar:** Mycket kompakt, stark felkorrigering, fungerar på böjda ytor.  
- **Nackdelar:** Kräver högkvalitativ utskrift, mindre vanlig läsarsupport.  

#### Snabb jämförelse

| Streckkodstyp | Datakapacitet | Bäst för | Typisk storlek |
|---------------|---------------|----------|----------------|
| Code128       | ~100 tecken   | Allmän märkning | Liten |
| QR‑kod        | ~4 000 tecken | Mobilskanning, rik data | Medium |
| Code39        | ~43 tecken    | Legacy‑hårdvara | Stor |
| Data Matrix   | ~3 000 tecken | Små utrymmen, industriella taggar | Mycket liten |

**Rekommendation:** Börja med **Code128** för enkla ID:n. Byt till **QR** när du behöver bädda in URL‑er eller större payloads. Använd **Code39** endast för legacy‑integrationer.

## Vanliga problem & lösningar

### Problem: “Streckkod hittas inte vid verifiering”

**Symptom:** Verifiering returnerar `false` trots att streckkoden syns.

**Vanliga orsaker**

1. Skift‑mismatch (t.ex. “John Smith” vs. “john smith”).  
2. Extra blanksteg i den kodade texten.  
3. Fel streckkodstyp angiven i verifieringsalternativen.  
4. Sökning på fel sidnummer.

**Lösning:** Normalisera texten före signering och verifiering, och säkerställ att `setEncodeType` matchar den ursprungliga typen.

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

### Problem: “Streckkod är suddig eller oläslig”

**Symptom:** Utskrivna streckkoder kan inte skannas.

**Orsaker**

- Streckkodens dimensioner är för små för den kodade datan.  
- Låga upplösningsinställningar på skrivaren.  
- Otillräcklig kontrast mellan streckkodsfärg och bakgrund.

**Lösning:** Öka streckkodens bredd/höjd, använd högkontrastfärger (svart på vitt) och sätt skrivardpi till minst 300 dpi.

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

### Problem: “OutOfMemoryError med stora dokument”

**Symptom:** Applikationen kraschar när den bearbetar PDF‑filer med hundratals sidor.

**Orsak:** Biblioteket laddar hela dokumentet i minnet.

**Lösning:** Aktivera streaming‑läge och bearbeta sidor inkrementellt.

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

### Problem: “Signaturposition inkonsekvent mellan dokumenttyper”

**Symptom:** Streckkoder visas på olika platser när du signerar PDF‑ respektive Word‑dokument.

**Orsak:** PDF använder ett ursprung längst ner till vänster, medan Word använder ett ursprung längst upp till vänster.

**Lösning:** Detektera dokumenttypen och applicera lämplig koordinattransformering.

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

### Problem: “Uppdaterade signaturer förlorar formatering”

**Symptom:** Efter anrop av `update` ändras streckkodens färg eller teckensnitt oväntat.

**Orsak:** Inte alla visuella egenskaper bevaras under en uppdateringsoperation.

**Lösning:** Återapplicera eventuella visuella inställningar efter uppdateringsanropet.

```java
// When updating, explicitly set all visual properties
bcSignature.setLeft(newLeft);
bcSignature.setTop(newTop);
bcSignature.setWidth(originalWidth); // Don't forget these!
bcSignature.setHeight(originalHeight);
// Note: Color and font can't be updated - you'd need to delete and re-sign
```

## Bästa praxis för produktion

### Prestandaoptimering

1. **Återanvänd Signature‑instanser** – Skapa ett enda `Signature`‑objekt per dokument och återanvänd det för flera operationer.

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

2. **Sök endast på specifika sidor** – Begränsa sidintervallet till där streckkoder förväntas.

```java
// Slow for 100+ page documents
BarcodeSearchOptions slowSearch = new BarcodeSearchOptions();
slowSearch.setAllPages(true);

// Fast - only check where signatures actually are
BarcodeSearchOptions fastSearch = new BarcodeSearchOptions();
fastSearch.setAllPages(false);
fastSearch.setPageNumber(1); // Only check cover page
```

3. **Välj den enklaste streckkodstypen** – Enklare streckkoder genereras snabbare; använd QR eller Data Matrix endast när extra kapacitet verkligen behövs.

```java
// Overkill for simple IDs
BarcodeSignOptions slow = new BarcodeSignOptions("12345", BarcodeTypes.QR);

// Faster and more appropriate
BarcodeSignOptions fast = new BarcodeSignOptions("12345", BarcodeTypes.Code128);
```

### Säkerhetsaspekter

1. **Kod aldrig känslig personlig data** – Streckkoder är lättlästa; undvik PII som personnummer eller lösenord.

```java
// Bad - exposes sensitive data
String barcodeData = "SSN:123-45-6789|Password:hunter2";

// Good - use reference IDs
String barcodeData = "USER-REF-7721X"; // Look up sensitive data server-side
```

2. **Validera på servern** – Lita aldrig enbart på klient‑sida verifiering; verifiera alltid på en betrodd backend.

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

3. **Lägg till tidsstämplar** – Inkludera en tidsstämpel i streckkodens payload för att förhindra replay‑attacker.

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

### Felhanteringsmönster

- **Använd alltid try‑with‑resources** för att säkerställa att `Signature`‑objekt frigörs.

```java
try (Signature signature = new Signature(documentPath)) {
    // Your operations here
    signature.sign(outputPath, signOptions);
} catch (Exception e) {
    logger.error("Failed to sign document: " + documentPath, e);
    throw new DocumentSigningException("Could not process document", e);
}
```

- **Validera filåtkomst** innan du försöker signera.

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

- **Synkronisera åtkomst** om flera trådar kan arbeta på samma fil.

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

### Testa din implementation

**Enhetstestmall**

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

**Integrationschecklista**

- ✅ Testa alla stödda format (PDF, DOCX, XLSX, PPTX, PNG).  
- ✅ Verifiera att streckkoder överlever en utskrifts‑skanningscykel.  
- ✅ Stress‑testa med maximala datalängder.  
- ✅ Bekräfta positionering på A4, Letter och anpassade sidstorlekar.  
- ✅ Kör samtidiga signeringar på flera dokument.  
- ✅ Övervaka minnesanvändning för dokument > 500 sidor.  
- ✅ Säkerställ att streckkodsläsare läser utdata pålitligt.

### Loggning och övervakning

Lägg till meningsfulla loggar runt varje operation:

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

Spåra nyckelmetrik som bearbetningstid, minnesförbrukning och felprocent:

```java
// Track success/failure rates
metricsService.incrementCounter("signature.sign.success");
metricsService.incrementCounter("signature.verify.failure");

// Track performance
metricsService.recordTimer("signature.sign.duration", duration);

// Track document sizes
metricsService.recordHistogram("signature.document.pages", pageCount);
```

## Pro‑tips från verklig användning

**Batch‑bearbetningsstrategi**

När du hanterar hundratals filer, bearbeta dem i batcher och rapportera framsteg:

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

**Externalisera konfiguration**

Spara streckkodinställningar (typ, storlek, färg) i en properties‑fil för enkel justering utan omkompilering:

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

**Standardisera streckkodspayload**

Använd ett avgränsat format som `EMPID|TIMESTAMP|DOCID` för enkel och konsekvent parsning:

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

**Detektera dokumenttyp automatiskt**

Justera streckkodsdimensioner baserat på om målet är PDF, Word eller en bild:

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

## Ytterligare resurser

- [GroupDocs.Signature documentation](https://docs.groupdocs.com/signature/java/) – Fullständig API‑guide och exempel.  
- [GroupDocs support forum](https://forum.groupdocs.com/c/signature/13) – Community‑hjälp och felsökning.  
- [API reference](https://apireference.groupdocs.com/signature/java) – Detaljerade metodsignaturer och parameterbeskrivningar.

## Vanliga frågor

**Q: Kan jag använda GroupDocs.Signature med Java 17?**  
A: Ja – biblioteket är fullt kompatibelt med JDK 8, 11 och 17.

**Q: Överlever streckkoden en utskrifts‑skanningscykel?**  
A: När du använder Code128 eller QR med tillräcklig storlek och kontrast förblir streckkoden skanningsbar efter utskrift och skanning.

**Q: Hur många streckkoder kan ett enda dokument innehålla?**  
A: Det finns ingen hård gräns; för optimal prestanda håll dock antalet under **200** per dokument.

**Q: Krävs licens för utvecklingsbyggen?**  
A: En tillfällig licens tar bort utvärderingsvattenmärken; en full licens är obligatorisk för någon produktionsdistribution.

**Q: Kan jag signera lösenordsskyddade PDF‑filer?**  
A: Ja – ange lösenordet när du skapar `Signature`‑objektet; API‑et låser upp filen internt.

---

**Senast uppdaterad:** 2026-07-15  
**Testat med:** GroupDocs.Signature 23.9 för Java  
**Författare:** GroupDocs  

{< /blocks/products/pf/tutorial-page-section >}
{< /blocks/products/pf/main-container >}
{< /blocks/products/pf/main-wrap-class >}
{< blocks/products/products-backtop-button >}

## Relaterade handledningar

- [How to Verify Barcode Signatures in Java with GroupDocs.Signature](/signature/java/search-verification/groupdocs-signature-java-document-verification/)
- [How to Search Digital Signatures in Java Documents with GroupDocs](/signature/java/search-verification/groupdocs-signature-java-digital-search-tutorial/)
- [Java Barcode Signature Tutorial - Add, Verify & Manage Barcodes in PDFs](/signature/java/barcode-signatures/)