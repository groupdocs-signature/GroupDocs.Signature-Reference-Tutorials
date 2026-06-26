---
categories:
- Digital Signatures
date: '2026-06-26'
description: Lär dig hur du skapar QR-kodsignatur i Word-dokument programatiskt med
  GroupDocs.Signature för Java. Steg-för-steg-handledning, kodexempel, bästa praxis
  och prestandatips.
keywords:
- create qr code signature
- programmatically sign word
- qr code digital signature
- add qr to word
- groupdocs signature java
lastmod: '2026-06-26'
linktitle: QR-kodsignaturer i Word med Java
schemas:
- author: GroupDocs
  dateModified: '2026-06-26'
  description: Learn how to create QR code signature in Word documents programmatically
    with GroupDocs.Signature for Java. Step‑by‑step tutorial, code examples, best
    practices, and performance tips.
  headline: Create QR Code Signature in Word Documents Using Java
  type: TechArticle
- description: Learn how to create QR code signature in Word documents programmatically
    with GroupDocs.Signature for Java. Step‑by‑step tutorial, code examples, best
    practices, and performance tips.
  name: Create QR Code Signature in Word Documents Using Java
  steps:
  - name: The library reads the source document.
    text: The library reads the source document.
  - name: Generates the QR code based on `QrCodeSignOptions`.
    text: Generates the QR code based on `QrCodeSignOptions`.
  - name: Inserts the graphic at the specified coordinates.
    text: Inserts the graphic at the specified coordinates.
  - name: Saves the modified file to the path you provided.
    text: Saves the modified file to the path you provided.
  type: HowTo
- questions:
  - answer: Yes. GroupDocs.Signature supports PDF, Excel, PowerPoint, images, and
      many other formats. Just change the `setFileFormat` to the desired output type.
    question: Can I sign PDFs instead of Word documents?
  - answer: Use the library’s `SearchQrCodeSignatures` method to locate QR codes and
      validate the embedded data against your backend service.
    question: How do I verify a QR code signature after it’s been added?
  - answer: Standard QR codes hold up to **4 296 alphanumeric characters**, but for
      reliable scanning keep payloads under **500 characters**. For larger payloads
      store a reference ID and fetch details server‑side.
    question: What is the maximum data I can store in a QR code?
  - answer: Yes. You can set size, position, foreground/background colors, and even
      add a logo overlay. Stick to high‑contrast colors for best scan results.
    question: Can I customize the QR code’s visual appearance?
  - answer: For documents over 50 pages, expect a few seconds per file. Use batch
      processing, reuse the `Signature` instance, and monitor JVM heap size.
    question: How should I handle large‑document signing efficiently?
  type: FAQPage
tags:
- java
- word-documents
- qr-code
- digital-signature
- groupdocs
title: Skapa QR-kodsignatur i Word-dokument med Java
type: docs
url: /sv/java/digital-signatures/groupdocs-signature-java-word-documents-qr-code/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Skapa QR‑kodsignatur i Word‑dokument med Java

Någon gång har du spenderat timmar på att manuellt signera dokument, bara för att undra om det finns ett snabbare, mer pålitligt sätt? Du kan **create QR code signature** i Word‑dokument programatiskt med bara några rader Java‑kod. Oavsett om du automatiserar kontraktsarbetsflöden, hanterar juridiska papper eller bygger en mobil‑först godkännandeportal, ger QR‑kodsignaturer dig omedelbar, skanningsbar verifiering som fungerar på vilken smartphone som helst. I den här handledningen kommer du att lära dig hur du installerar GroupDocs.Signature för Java, konfigurerar QR‑kodalternativ och bäddar in rik data såsom URL‑er, tidsstämplar eller JSON‑payloads i Word‑filer. I slutet kommer du att kunna signera dokument i skala, minska manuellt arbete och öka efterlevnaden.

## Snabba svar
- **Vilket bibliotek behöver jag?** GroupDocs.Signature for Java (v23.12+).  
- **Hur många kodrader?** Two‑line QR generation plus a few configuration lines.  
- **Kan jag signera PDF‑filer också?** Yes – the same API works for PDF, Excel, PowerPoint, and images.  
- **Krävs en kommersiell licens?** Only for production; a free trial or temporary license works for development.  
- **Vilken data kan jag lagra?** Up to ~4 k characters (URL, JSON, IDs), but keep it under 500 chars for reliable scanning.

## Vad är create QR code signature?
En **create QR code signature** är en skannbar 2‑D‑streckkod inbäddad i ett dokument som representerar en digital signatur eller verifieringspayload. När en användare skannar QR‑koden läses den kodade datan (ofta en URL eller token) och valideras, vilket bevisar dokumentets äkthet utan att behöva speciell programvara.

## Varför använda GroupDocs.Signature för Java för att lägga till QR‑koder?
GroupDocs.Signature stöder **50+ in‑ och utdataformat**, kan bearbeta filer med flera hundra sidor utan att ladda hela dokumentet i minnet, och erbjuder ett flytande API som låter dig **programmatically sign Word**‑filer på millisekunder. Biblioteket erbjuder också inbyggd QR‑, Aztec‑, DataMatrix‑ och PDF417‑streckkodsgenerering, vilket gör det till en allt‑i‑ett‑lösning för modern mobil‑först verifiering.

## Förutsättningar

### Nödvändiga bibliotek och beroenden
- **GroupDocs.Signature för Java** version **23.12** eller senare (det enda externa beroendet).

### Krav för miljöinställning
- **JDK 8+** (Java 11 eller 17 rekommenderas för produktion).  
- **IDE** efter eget val (IntelliJ IDEA, Eclipse, VS Code).  
- **Byggverktyg** – Maven eller Gradle (exemplen nedan fungerar med båda).

### Kunskapsförutsättningar
- Grundläggande Java‑syntax och fil‑IO‑hantering.  
- Bekantskap med Maven/Gradle‑beroendedeklarationer (vi visar exakta kodsnuttar).

## Installera GroupDocs.Signature för Java

Välj ditt byggsystem och lägg till beroendet exakt som visas. Platshållarna nedan representerar de ursprungliga kodblocken; behåll dem oförändrade.

**Maven**

```java
```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```
```

**Gradle**

```java
```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```
```

**Direct Download**

Föredrar du manuell hantering? Ladda ner JAR‑filen direkt från [GroupDocs.Signature för Java‑utgåvor](https://releases.groupdocs.com/signature/java/) och lägg till den i ditt projekts classpath.

### Licensanskaffning
- **Free Trial:** Ideal för prototypframtagning; kärnfunktioner är tillgängliga.  
- **Temporary License:** Full‑feature access for short‑term development.  
- **Commercial License:** Required for production deployments.  

**Pro Tip:** Börja med free trial, begär sedan en temporary license innan du går över till produktion. Detta låter dig validera arbetsflödet utan förhandskostnad.

### Grundläggande initiering
`Signature`‑objektet är ingångspunkten för alla signeringsoperationer. Det implementerar `AutoCloseable`, så du kan säkert använda ett try‑with‑resources‑block.

```java
```java
Signature signature = new Signature("path/to/your/document");
```
```

## Implementeringsguide: Signering av Word‑dokument med QR‑koder

Nedan går vi igenom varje steg, lägger till definitionsankare och direkta svar där det behövs.

### Hur initierar jag Signature‑objektet för en Word‑fil?
Läs in källdokumentet med `new Signature("source.docx")` inom ett try‑with‑resources‑block; objektet förbereder filen för modifieringar och frigör automatiskt resurser när blocket avslutas.

```java
```java
String filePath = "YOUR_DOCUMENT_DIRECTORY/SampleDocX.docx";
Signature signature = new Signature(filePath);
```
```

`Signature`‑klassen representerar ett enskilt dokument i minnet och exponerar metoder för att lägga till, söka och verifiera signaturer. Den stöder `.docx`, `.doc` och många andra format.

### Hur kan jag konfigurera QR‑kodsigneringsalternativ?
Skapa en `QrCodeSignOptions`‑instans, ange den kodade texten, streckkodstypen och positioneringen. Följande kodsnutt visar en minimal konfiguration.

```java
```java
QrCodeSignOptions signOptions = new QrCodeSignOptions("JohnSmith");
signOptions.setEncodeType(QrCodeTypes.QR);
signOptions.setLeft(100); // X-axis position in pixels
signOptions.setTop(100);  // Y-axis position in pixels
```
```

`QrCodeSignOptions`‑klassen kapslar in alla inställningar som krävs för att generera och placera en QR‑kodsignatur, inklusive den kodade texten, streckkodstyp, storlek, färger och positionskoordinater i dokumentet.

#### Anpassa utseende
Du kan ytterligare justera storlek, marginal och färger:

```java
```java
QrCodeSignOptions signOptions = new QrCodeSignOptions("https://yourapp.com/verify/doc-12345");
```
```

**Varför det är viktigt:** En 150 px kvadratisk QR‑kod med svart förgrund på vit bakgrund ger >99 % skanningsframgång både på skärm och i utskrift.

### Hur ställer jag in utdataalternativ för det signerade dokumentet?
Definiera målformatet och överskrivningsbeteendet innan du anropar `sign`.

```java
```java
WordProcessingSaveOptions saveOptions = new WordProcessingSaveOptions();
saveOptions.setFileFormat(WordProcessingSaveFileFormat.Odt);
saveOptions.setOverwriteExistingFiles(true);
```
```

`WordProcessingSaveOptions`‑klassen definierar hur det signerade Word‑dokumentet ska sparas, vilket låter dig ange utdataformat (DOCX, ODT, etc.), om befintliga filer ska skrivas över och andra filnivåpreferenser.

Om du behöver ett öppen‑källkodsformat, byt till `OutputType.ODT`:

```java
```java
saveOptions.setFileFormat(WordProcessingSaveFileFormat.Docx);
```
```

### Hur signerar och sparar jag dokumentet med QR‑koden?
`sign`‑metoden applicerar QR‑koden och skriver utdatafilen i ett anrop.

```java
```java
String outputFilePath = "YOUR_OUTPUT_DIRECTORY/SaveSignedOutputType/SampleDocX.odt";
signature.sign(outputFilePath, signOptions, saveOptions);
```
```

`sign`‑metoden för `Signature`‑objektet tar destinationssökvägen, de konfigurerade signeringsalternativen och eventuella sparalternativ, sedan bäddar den in QR‑koden i dokumentet och skriver resultatet till den angivna platsen.

**Vad händer:**  
1. Biblioteket läser källdokumentet.  
2. Genererar QR‑koden baserat på `QrCodeSignOptions`.  
3. Infogar grafiken på de angivna koordinaterna.  
4. Sparar den modifierade filen till den sökväg du angav.

### Hur bör jag hantera fel under signering?
Omge signeringslogiken med ett try‑catch‑block för att fånga saknade filer, ogiltiga sökvägar eller licensproblem.

```java
```java
try {
    signature.sign(outputFilePath, signOptions, saveOptions);
    System.out.println("Document signed successfully!");
} catch (Exception e) {
    System.err.println("Signing failed: " + e.getMessage());
}
```
```

Att fånga `Exception` säkerställer att eventuella körningsproblem som saknade filer, ogiltiga sökvägar eller licensproblem rapporteras på ett smidigt sätt, vilket förhindrar att applikationen kraschar i produktion.

## Vanliga användningsfall och verkliga tillämpningar

### Automatiserad kontraktshantering
En SaaS‑plattform signerar **500+ kontrakt per månad** genom att generera en unik QR‑kod som innehåller kontraktets ID och en verifierings‑URL. Mottagare skannar för att se kontraktets status i portalen, vilket eliminerar manuella e‑postutbyten.

### Utdelning av anställdas certifikat
HR‑avdelningar bäddar in anställdas ID‑nummer och utfärdandedatum i QR‑koder på utbildningscertifikat. Genom att skanna QR‑koden valideras äktheten omedelbart mot en intern databas, vilket minskar bedrägeri med **över 80 %**.

### Automatisering av godkännandeflöde
Varje godkännare har en QR‑kod som lagrar deras anställdnummer, roll och en tidsstämpel. Systemet läser QR‑koden under revision och ger ett manipulering‑evident spår utan extra databasuppslag.

### Signering av fakturor och kvitton
Ekonomiteam lägger till QR‑koder som länkar till en betalningsgateway. När den skannas dirigerar QR‑koden betalaren till en säker betalningssida, vilket minskar behandlingstiden med **30 %** och minskar risken för fakturaförfalskning.

## Bästa praxis för produktionsanvändning

### Säkerhetsaspekter
- **Aldrig bädda in råa lösenord**; använd en token eller referens‑ID som löses upp på servern.  
- **Använd alltid HTTPS** för URL‑er; undvik HTTP för att förhindra man‑in‑the‑middle‑attacker.  
- **Ställ in tokenutgång** (t.ex. JWT med 24‑timmars giltighet) för tidskänsliga dokument.

### Prestandaoptimering
- **Batch‑bearbetning:** Behåll en enda `Signature`‑instans levande och iterera över filer för att undvika upprepad JVM‑uppvärmning.  
- **Minneshantering:** För dokument > 50 MB, bearbeta sekventiellt och frigör `Signature`‑objektet efter varje fil.  
- **Placering är viktig:** Placera QR‑koder längst ner på sidan för att minska layout‑omflöde och förbättra hastigheten.

```java
```java
List<String> documents = getDocumentPaths();
for (String docPath : documents) {
    Signature sig = new Signature(docPath);
    // Configure and sign
    sig.dispose();
}
```
```

### Tips för QR‑kodplacering
- **Utskriftsäkerhet:** Håll QR‑koder minst 0,5 tum från sidans kanter för att undvika att de kapas bort.  
- **Storleksrekommendation:** Minimum 150 × 150 px för pålitlig skanning på tryckt media.  
- **Flera sidor:** Loopa igenom sidor och skapa en ny `QrCodeSignOptions` för varje position.

```java
```java
for (Document doc : documents) {
    Signature sig = new Signature(doc.getPath());
    sig.sign(outputPath, signOptions, saveOptions);
    sig.dispose();
}
```
```

## Avancerade konfigurationsalternativ

### Hur kan jag lägga till flera QR‑koder i ett enda dokument?
Skapa separata `QrCodeSignOptions`‑objekt för varje plats och anropa `sign` upprepade gånger.

```java
```java
// First QR code
QrCodeSignOptions sign1 = new QrCodeSignOptions("Approver 1");
sign1.setLeft(100);
sign1.setTop(100);

// Second QR code
QrCodeSignOptions sign2 = new QrCodeSignOptions("Approver 2");
sign2.setLeft(300);
sign2.setTop(100);

// Apply both
signature.sign(outputPath, sign1, saveOptions);
signature.sign(outputPath, sign2, saveOptions);
```
```

### Vilka andra streckkodstyper stöds?
Utöver QR kan du generera **Aztec**, **DataMatrix** eller **PDF417**‑koder genom att ändra `setEncodeType()`.

### Hur beräknar jag dynamiska positioner baserat på sidstorlek?
Hämta siddimensioner via `Signature.getDocumentInfo()` och beräkna koordinater programatiskt.

```java
```java
// Get document info
DocumentInfo docInfo = signature.getDocumentInfo();
int pageWidth = docInfo.getWidth();
int pageHeight = docInfo.getHeight();

// Center the QR code
int qrSize = 100;
signOptions.setLeft((pageWidth - qrSize) / 2);
signOptions.setTop((pageHeight - qrSize) / 2);
```
```

`Signature.getDocumentInfo()` returnerar ett `DocumentInfo`‑objekt som innehåller metadata såsom siddimensioner, vilket kan användas för att beräkna exakta placeringskoordinater för signaturer baserat på varje sidas faktiska storlek.

## Felsökning av vanliga problem

### QR‑kod visas inte
- Verifiera att `setLeft`/`setTop` ligger inom sidans gränser (A4 ≈ 595 × 842 px vid 72 DPI).  
- Säkerställ att förgrunds‑/bakgrundsfärger har kontrast (svart på vit).  
- Öka bredd/höjd om koden är för liten för att skannas.

### “File not found” när Signature initieras
- Använd absoluta sökvägar under utveckling eller validera relativa sökvägar med `Paths.get(...)`.  
- Bekräfta att källfilen inte är låst av en annan process.

### Utdatafil är korrupt
- Dubbelkolla att `setFileFormat` matchar önskad filändelse.  
- Stäng eventuella strömmar som kan hålla filen öppen innan signering.

### QR‑kod innehåller fel data
- Skriv ut strängen du skickar till `QrCodeSignOptions` före signering för att bekräfta kodning.  
- Undvik icke‑ASCII‑tecken om du inte explicit sätter UTF‑8‑kodning.

### Prestanda är långsam på stora dokument
- Bearbeta dokument i batchar (se kodblock 10).  
- Undvik att placera QR‑koder i komplexa tabeller; de triggar omfattande layout‑omräkningar.

## Vanliga frågor

**Q: Kan jag signera PDF‑filer istället för Word‑dokument?**  
A: Ja. GroupDocs.Signature stöder PDF, Excel, PowerPoint, bilder och många andra format. Ändra bara `setFileFormat` till önskad utdataformat.

**Q: Hur verifierar jag en QR‑kodsignatur efter att den har lagts till?**  
A: Använd bibliotekets `SearchQrCodeSignatures`‑metod för att hitta QR‑koder och validera den inbäddade datan mot din backend‑tjänst.

**Q: Vad är den maximala mängden data jag kan lagra i en QR‑kod?**  
A: Standard‑QR‑koder kan hålla upp till **4 296 alfanumeriska tecken**, men för pålitlig skanning håll payloaden under **500 tecken**. För större payloads lagra ett referens‑ID och hämta detaljer på serversidan.

**Q: Kan jag anpassa QR‑kodens visuella utseende?**  
A: Ja. Du kan sätta storlek, position, förgrunds‑/bakgrundsfärger och till och med lägga till en logotyp‑överlagring. Använd högkontrastfärger för bästa skanningsresultat.

**Q: Hur hanterar jag effektivt signering av stora dokument?**  
A: För dokument med mer än 50 sidor, förvänta dig några sekunder per fil. Använd batch‑bearbetning, återanvänd `Signature`‑instansen och övervaka JVM‑heap‑storleken.

**Q: Kommer QR‑signaturer att överleva konvertering till PDF?**  
A: Absolut. QR‑koden är inbäddad som en grafik, så den förblir intakt vid konvertering mellan format, förutsatt att du behåller tillräcklig upplösning.

**Q: Kan jag signera dokument lagrade i molnlagring som S3?**  
A: Ja. Ladda ner filen till en temporär lokal sökväg, signera den och ladda sedan upp den signerade versionen tillbaka till S3. Biblioteket fungerar endast med lokala filer.

**Q: Vad händer om någon ändrar dokumentet efter signering?**  
A: QR‑grafiken i sig förblir oförändrad, men den upptäcker inte manipulation. Kombinera QR‑koder med hash‑baserad verifiering eller digitala certifikat för robusta integritetskontroller.

**Q: Behöver jag olika licenser för utveckling respektive produktion?**  
A: Utveckling kan använda free trial eller en temporary license. Produktionsdistributioner kräver en commercial license enligt GroupDocs villkor.

**Q: Kan mottagare utan Java skanna dessa QR‑koder?**  
A: Ja. QR‑koder följer en öppen standard; vilken smartphone‑kamera eller QR‑läsarapp som helst kan avkoda dem. Java behövs endast för *att skapa* signaturerna.

## Resurser

- [GroupDocs.Signature för Java‑utgåvor](https://releases.groupdocs.com/signature/java/)
- [GroupDocs.Signature för Java‑dokumentation](https://docs.groupdocs.com/signature/java/)
- [GroupDocs.Signature API‑referens](https://reference.groupdocs.com/signature/java/)
- [Senaste GroupDocs.Signature‑utgåvor](https://releases.groupdocs.com/signature/java/)
- [Köp GroupDocs.Signature](https://purchase.groupdocs.com/buy)
- [GroupDocs Signatures gratis provperiod](https://releases.groupdocs.com/signature/java/)
- [Ansök om tillfällig licens](https://purchase.groupdocs.com/temporary-license/)
- [GroupDocs forum‑support](https://forum.groupdocs.com/c/signature/)

## Slutsats

Du har nu en komplett, produktionsklar färdplan för att **create QR code signature** i Word‑dokument med Java och GroupDocs.Signature. Från grundläggande installation till batch‑bearbetning, från säkerhets‑bästa praxis till avancerade streckkodstyper, allt du behöver är täckt. Börja med en free trial, experimentera med olika payloads och integrera signeringssteget i din befintliga dokument‑genereringspipeline. Lycka till med kodandet och säker signering!

---

**Senast uppdaterad:** 2026-06-26  
**Testat med:** GroupDocs.Signature 23.12 för Java  
**Författare:** GroupDocs  

{{< blocks/products/products-backtop-button >}}

## Relaterade handledningar

- [Java QR Code Signature Library – komplett GroupDocs‑handledning](/signature/java/qr-code-signatures/)
- [Ladda och spara dokument i Java – komplett GroupDocs.Signature‑handledning](/signature/java/document-loading-saving/)
- [Hur man lägger till digitala signaturer i dokument i Java](/signature/java/digital-signatures/groupdocs-signature-java-digital-signing-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}