---
categories:
- Document Signing
- Healthcare Integration
date: '2026-05-16'
description: Lär dig hur du skapar data matrix PDF och lägger till QR‑kod PDF med
  GroupDocs.Signature för Java. Steg‑för‑steg‑guide för signering av hälsodokument.
keywords:
- create data matrix pdf
- add qr code pdf
- HIBC barcode Java
lastmod: '2026-05-16'
linktitle: HIBC PDF Signeringsguide för Java
schemas:
- author: GroupDocs
  dateModified: '2026-05-16'
  description: Learn how to create data matrix PDF and add QR code PDF using GroupDocs.Signature
    for Java. Step‑by‑step guide for healthcare document signing.
  headline: Create Data Matrix PDF with HIBC Barcode in Java
  type: TechArticle
- description: Learn how to create data matrix PDF and add QR code PDF using GroupDocs.Signature
    for Java. Step‑by‑step guide for healthcare document signing.
  name: Create Data Matrix PDF with HIBC Barcode in Java
  steps:
  - name: '**Import the required classes** – these give you access to the signature
      engine and Data Matrix options.'
    text: '**Import the required classes** – these give you access to the signature
      engine and Data Matrix options.'
  - name: '**Instantiate the `Signature` object** with absolute paths for source and
      destination files.'
    text: '**Instantiate the `Signature` object** with absolute paths for source and
      destination files.'
  - name: '**Configure the Data Matrix options** – set the HIBC string, choose `QrCodeTypes.HIBCLICDataMatrix`,
      and define placement coordinates. `QrCodeTypes` enumerates the supported barcode
      formats for HIBC signatures.'
    text: '**Configure the Data Matrix options** – set the HIBC string, choose `QrCodeTypes.HIBCLICDataMatrix`,
      and define placement coordinates. `QrCodeTypes` enumerates the supported barcode
      formats for HIBC signatures.'
  - name: '**Apply the signature** to the PDF.'
    text: '**Apply the signature** to the PDF.'
  - name: '**Dispose of resources** to free file handles and avoid memory leaks.'
    text: '**Dispose of resources** to free file handles and avoid memory leaks.'
  - name: '**Import QR‑specific classes**'
    text: '**Import QR‑specific classes**'
  - name: '**Create and configure QR options** – note the use of `QrCodeTypes.HIBCLICQR`.'
    text: '**Create and configure QR options** – note the use of `QrCodeTypes.HIBCLICQR`.'
  - name: '**Sign the document**'
    text: '**Sign the document**'
  type: HowTo
- questions:
  - answer: Yes, it also supports DOCX, XLSX, PPTX, PNG, JPEG, and TIFF with the same
      barcode‑signing API.
    question: Can GroupDocs.Signature sign file types other than PDF?
  - answer: Verify that your HIBC string follows the exact HIBCC syntax, use the online
      validator, and ensure you’re using the correct `QrCodeTypes` constant for the
      chosen format.
    question: How do I troubleshoot “Invalid barcode content” errors?
  - answer: QR ≈ 4,296 alphanumeric characters, Aztec ≈ 3,832 numeric / 3,067 alphanumeric,
      Data Matrix ≈ 3,116 numeric / 2,335 alphanumeric. Keep codes under 200 characters
      for optimal scan reliability.
    question: What is the maximum data capacity for each HIBC format?
  - answer: Absolutely. Create separate `QrCodeSignOptions` objects with different
      positions and call `signature.sign()` for each. Just ensure they don’t overlap.
    question: Is it possible to embed multiple barcode types in one PDF?
  - answer: No. After the JAR is on the classpath and the license is activated, all
      operations are performed locally.
    question: Do I need an internet connection for signing at runtime?
  type: FAQPage
tags:
- java
- pdf-signing
- hibc
- healthcare
- barcode
- pharmaceutical
title: Skapa Data Matrix PDF med HIBC-streckkod i Java
type: docs
url: /sv/java/barcode-signatures/sign-pdfs-hibc-lic-codes-groupdocs-java/
weight: 1
---

# Skapa Data Matrix PDF med HIBC‑streckkod i Java

Om du bygger programvara för farmaceutisk eller hälso‑logistik, har du förmodligen stött på problemet med pappersbaserad spårning, förlorade signaturer och revisionsmardrömmar. **Skapa en Data Matrix PDF** som bäddar in en HIBC‑LIC‑streckkod löser dessa problem genom att ge dig ett manipulering‑synligt, maskin‑läsbart spår som överlever utskrift, skanning och regulatorisk granskning. I den här handledningen kommer du att se exakt hur du **lägger till QR‑kod PDF**‑stöd, samt Aztec‑ och Data Matrix‑format, med hjälp av GroupDocs.Signature för Java.

## Snabba svar
- **Vilket bibliotek hanterar HIBC‑streckkoder i Java?** GroupDocs.Signature for Java.  
- **Vilket streckkodformat är mest kompakt?** Data Matrix – idealiskt för små etiketter.  
- **Kan jag lägga till både QR och Data Matrix i samma PDF?** Ja, skapa bara separata `QrCodeSignOptions`.  
- **Behöver jag en internetanslutning vid körning?** Nej, biblioteket fungerar helt offline efter installation.  
- **Vilken Java‑version rekommenderas?** Java 11+ för produktionsklass prestanda.

## Vad är HIBC‑streckkod PDF‑signering?
`Signature`‑klassen i GroupDocs.Signature för Java representerar ett PDF‑dokument och tillhandahåller metoder för att bädda in HIBC‑streckkoder som digitala signaturer. Genom att signera en PDF med en HIBC‑streckkod skapar du en verifierbar, manipulering‑synlig post som kan skannas när som helst i leveranskedjan.

## Varför använda Data Matrix och QR‑koder tillsammans?
GroupDocs.Signature stöder **50+ in‑ och utdataformat** och kan bearbeta PDF‑filer med flera hundra sidor utan att ladda in hela filen i minnet. Att använda Data Matrix för täta, småytade etiketter och QR för mer rymliga dokument ger dig den bästa balansen mellan läsbarhet, datakapacitet (upp till 4 296 tecken för QR) och utskrifts‑yteseffektivitet.

## Förutsättningar
- **JDK 11 eller högre** (Java 8 fungerar men Java 11+ rekommenderas för optimal prestanda).  
- **IDE** såsom IntelliJ IDEA, Eclipse eller VS Code med Java‑tillägg.  
- **Maven eller Gradle** för beroendehantering (exempel nedan).  
- **Exempel‑PDF** (t.ex. `sample.pdf`) för att testa implementationen.  
- **Giltig GroupDocs.Signature‑licens** (gratis prov för utveckling, betald licens för produktion).

## Konfigurera GroupDocs.Signature för Java

### Maven‑konfiguration
Lägg till beroendet i din `pom.xml`:

```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

### Gradle‑konfiguration
För Gradle‑projekt, lägg till detta i din `build.gradle`:

```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

### Direktnedladdningsalternativ
Du kan också ladda ner JAR‑filen direkt från [GroupDocs.Signature for Java releases](https://releases.groupdocs.com/signature/java/) och lägga till den i ditt projekts classpath manuellt. Detta tillvägagångssätt fungerar bra i nätverk med begränsad åtkomst.

### Skaffa en licens
Begär en gratis provperiod eller tillfällig licens från GroupDocs för att ta bort vattenmärken och låsa upp alla funktioner. Produktionsutplaceringar kräver en köpt licens.

### Grundläggande initiering
`Signature`‑klassen är startpunkten för alla signeringsoperationer. Den laddar PDF‑filen, applicerar streckkoden och skriver den signerade filen.

```java
import com.groupdocs.signature.Signature;

class InitializeSignature {
    public static void main(String[] args) {
        Signature signature = new Signature("sample.pdf");
        // Proceed with signing operations...
    }
}
```

## Hur skapar man en Data Matrix PDF med HIBC‑streckkod?
Läs in din käll‑PDF, konfigurera ett `QrCodeSignOptions`‑objekt för Data Matrix‑formatet och anropa `sign()` – det är allt du behöver för att bädda in en kompatibel HIBC Data Matrix‑streckkod. Följande steg guidar dig genom den exakta koden som krävs. `QrCodeSignOptions` definierar inställningarna för en streckkodssignatur, såsom typ, innehåll, storlek och position.

1. **Importera de nödvändiga klasserna** – dessa ger dig åtkomst till signaturmotorn och Data Matrix‑alternativen.  

```java
import com.groupdocs.signature.Signature;
import com.groupdocs.signature.options.sign.QrCodeSignOptions;
import com.groupdocs.signature.domain.qrcodes.QrCodeTypes;
```

2. **Instansiera `Signature`‑objektet** med absoluta sökvägar för käll‑ och destinationsfiler.  

```java
String sourceFilePath = "YOUR_DOCUMENT_DIRECTORY";
String destinFilePath = "YOUR_OUTPUT_DIRECTORY/SignWithHIBCLICQR.pdf";

final Signature signature = new Signature(sourceFilePath);
```

3. **Konfigurera Data Matrix‑alternativen** – ange HIBC‑strängen, välj `QrCodeTypes.HIBCLICDataMatrix` och definiera placeringskoordinater. `QrCodeTypes` enumererar de stödjade streckkodformaten för HIBC‑signaturer.  

```java
QrCodeSignOptions hibcLic_QR = new QrCodeSignOptions("A123PROD30917/75#422011907#GP293", QrCodeTypes.HIBCLICQR);
hibcLic_QR.setLeft(1); // Set the position from left
hibcLic_QR.setTop(1);   // Set the position from top
hibcLic_QR.setReturnContent(true); // Return content after signing
hibcLic_QR.setReturnContentType(FileType.PNG); // Specify return content type as PNG
```

4. **Applicera signaturen** på PDF‑filen.  

```java
signature.sign(destinFilePath, hibcLic_QR);
```

5. **Frigör resurser** för att släppa filhandtag och undvika minnesläckor.  

```java
finally {
    if (signature != null) signature.dispose();
}
```

### Fullständigt fungerande exempel
Här är hela flödet i ett enda block (platshållarna representerar den exakta koden du klistrar in från de tidigare snippetarna):

```java
import com.groupdocs.signature.Signature;
import com.groupdocs.signature.options.sign.QrCodeSignOptions;
import com.groupdocs.signature.domain.qrcodes.QrCodeTypes;

public class HibcQrSigning {
    public static void main(String[] args) {
        String sourceFilePath = "sample.pdf";
        String destinFilePath = "output/SignWithHIBCLICQR.pdf";
        
        Signature signature = null;
        try {
            signature = new Signature(sourceFilePath);
            
            QrCodeSignOptions hibcLic_QR = new QrCodeSignOptions(
                "A123PROD30917/75#422011907#GP293", 
                QrCodeTypes.HIBCLICQR
            );
            hibcLic_QR.setLeft(1);
            hibcLic_QR.setTop(1);
            hibcLic_QR.setReturnContent(true);
            hibcLic_QR.setReturnContentType(FileType.PNG);
            
            signature.sign(destinFilePath, hibcLic_QR);
            System.out.println("PDF signed successfully with HIBC QR code");
            
        } catch (Exception e) {
            System.err.println("Error signing PDF: " + e.getMessage());
            e.printStackTrace();
        } finally {
            if (signature != null) signature.dispose();
        }
    }
}
```

#### Direkt svar (40–70 ord)
För att **skapa en Data Matrix PDF**, instansiera `Signature` med din käll‑PDF, sätt `QrCodeSignOptions` till `QrCodeTypes.HIBCLICDataMatrix` och ange en korrekt formaterad HIBC‑sträng, sedan anropa `signature.sign(outputPath, options)`. Biblioteket skriver den signerade PDF‑filen till destinationen, bevarar layouten och bäddar in streckkoden som en manipulering‑synlig signatur.

## Hur lägger man till QR‑kod PDF med GroupDocs.Signature?
Läs in PDF‑filen, konfigurera `QrCodeSignOptions` för QR‑formatet och anropa `sign()`. Detta två‑radsmönster fungerar för alla PDF‑storlekar och skalar automatiskt QR‑bilden för optimal läsbarhet. `QrCodeSignOptions` konfigurerar QR‑streckkodssignaturen, inklusive dess innehåll och visuella egenskaper. Den placerar koden baserat på de koordinater du anger, vilket säkerställer att den inte överlappar befintligt innehåll och förblir skannbar efter utskrift.

1. **Importera QR‑specifika klasser**  

```java
QrCodeSignOptions hibcLic_AZ = new QrCodeSignOptions("A123PROD30917/75#422011907#GP293", QrCodeTypes.HIBCLICAztec);
hibcLic_AZ.setLeft(1); // Set the position from left
hibcLic_AZ.setTop(200); // Set the position from top
hibcLic_AZ.setReturnContent(true); // Return content after signing
hibcLic_AZ.setReturnContentType(FileType.PNG); // Specify return content type as PNG
```

2. **Skapa och konfigurera QR‑alternativ** – observera användningen av `QrCodeTypes.HIBCLICQR`.  

```java
signature.sign(destinFilePath, hibcLic_AZ);
```

3. **Signera dokumentet**  

```java
QrCodeSignOptions hibcLic_DM = new QrCodeSignOptions("A123PROD30917/75#422011907#GP293", QrCodeTypes.HIBCLICDataMatrix);
hibcLic_DM.setLeft(1); // Set the position from left
hibcLic_DM.setTop(400); // Set the position from top
hibcLic_DM.setReturnContent(true); // Return content after signing
hibcLic_DM.setReturnContentType(FileType.PNG); // Specify return content type as PNG
```

> **Direkt svar:** Använd `QrCodeTypes.HIBCLICQR` i `QrCodeSignOptions`, ange HIBC‑innehållssträngen, positionera koden med `setLeft()` och `setTop()`, och anropa sedan `signature.sign(outputPath, options)`. QR‑streckkoden bäddas in omedelbart, klar för smartphone‑ eller skanner‑avläsning.

## Vanliga misstag att undvika

### 1. Glömma att frigöra resurser
**Fel:**  
```java
Signature signature = new Signature("sample.pdf");
signature.sign(destinFilePath, options);
// Oops, no dispose() call
```  

**Lösning:** Wrappa `Signature`‑användningen i ett try‑with‑resources‑block eller anropa explicit `close()` i ett finally‑avsnitt.

### 2. Använda felaktiga HIBC‑formatsträngar
**Fel:** Använda generiska strängar som “12345”.  
**Lösning:** Följ HIBCC‑standarden (t.ex. `A123PROD30917/75#422011907#GP293`). Validera med [HIBCC online validator](https://www.hibcc.org/).

### 3. Hårdkoda filsökvägar
**Fel:**  

```java
String sourceFilePath = "C:/Users/John/Documents/test.pdf";
```  

**Lösning:** Spara sökvägar i en konfigurationsfil eller miljövariabel och läs dem vid körning.

### 4. Ignorera streckkodens positionskonflikter
Placera streckkoder bort från befintlig text eller signaturer. Använd PDF‑koordinater (ursprunget är nedre vänstra) och testa med ett utskrivet prov.

### 5. Inte testa med riktiga skannrar
Skriv ut den signerade PDF‑filen och skanna den med exakt den hårdvara som används i ditt arbetsflöde. Verifiera läsbarhet vid olika utskriftskvaliteter.

## Praktiska tillämpningar inom hälso‑vård

| Scenario | Rekommenderad streckkod | Varför det passar |
|----------|------------------------|-------------------|
| **Farmaceutisk distribution** | QR‑kod | Hög datakapacitet, ofta skannad av smartphones. |
| **Lagerhantering** | Data Matrix | Litet fotavtryck, idealiskt för täta hylletiketter. |
| **Regulatorisk efterlevnad (FDA 21 CFR Part 11)** | QR + Data Matrix | Dubbelformat ger redundans och spårbarhet. |
| **Spårning av medicintekniska produkter** | Aztec‑kod | Kompakt storlek fungerar på förpackningar med begränsat utrymme. |

## Prestandaöverväganden och bästa praxis

### Batch‑bearbetningsmönster
```java
List<String> filesToSign = getFileList();
for (String filePath : filesToSign) {
    Signature signature = null;
    try {
        signature = new Signature(filePath);
        // Sign and save
    } finally {
        if (signature != null) signature.dispose();
    }
}
```

- Skapa en ny `Signature`‑instans per fil för att hålla minnesanvändningen låg.  
- Använd en fast trådpool (`Executors.newFixedThreadPool(Runtime.getRuntime().availableProcessors() - 1)`) för parallell bearbetning, men övervaka heap‑storleken eftersom varje `Signature` håller hela PDF‑filen i minnet.  

### Håll bibliotek uppdaterade
GroupDocs‑utgåvor förbättrar bearbetningshastigheten med upp till **20 %** och lägger till nya HIBC‑efterlevnadsfunktioner. Schemalägg kvartalsvisa beroendekontroller.

### Cacha mallar
Läs in en PDF‑mall en gång, klona den för varje streckkodsvariant och signera klonerna. Detta minskar I/O och snabbar upp arbetsflöden med hög volym.

## Vanliga frågor

**Q: Kan GroupDocs.Signature signera filtyper förutom PDF?**  
A: Ja, det stödjer även DOCX, XLSX, PPTX, PNG, JPEG och TIFF med samma streckkod‑signerings‑API.

**Q: Hur felsöker jag felmeddelandet “Invalid barcode content”?**  
A: Verifiera att din HIBC‑sträng följer exakt HIBCC‑syntax, använd online‑valideraren och säkerställ att du använder rätt `QrCodeTypes`‑konstant för det valda formatet.

**Q: Vad är den maximala datakapaciteten för varje HIBC‑format?**  
A: QR ≈ 4 296 alfanumeriska tecken, Aztec ≈ 3 832 numeriska / 3 067 alfanumeriska, Data Matrix ≈ 3 116 numeriska / 2 335 alfanumeriska. Håll koder under 200 tecken för optimal skanningspålitlighet.

**Q: Är det möjligt att bädda in flera streckkodstyper i en PDF?**  
A: Absolut. Skapa separata `QrCodeSignOptions`‑objekt med olika positioner och anropa `signature.sign()` för varje. Se bara till att de inte överlappar.

**Q: Behöver jag en internetanslutning för signering vid körning?**  
A: Nej. Efter att JAR‑filen är i classpath och licensen är aktiverad utförs alla operationer lokalt.

## Ytterligare resurser

- [GroupDocs.Signature för Java‑dokumentation](https://docs.groupdocs.com/signature/java/)  
- [API‑referensguide](https://reference.groupdocs.com/signature/java/)  
- [Senaste release‑nedladdningar](https://releases.groupdocs.com/signature/java/)  
- [Köp licens](https://purchase.groupdocs.com/buy)  
- [Få gratis provperiod](https://releases.groupdocs.com/signature/java/)  
- [Begär tillfällig licens](https://purchase.groupdocs.com/temporary-license/)  
- [GroupDocs‑forum](https://forum.groupdocs.com/c/signature/)

---

**Senast uppdaterad:** 2026-05-16  
**Testad med:** GroupDocs.Signature 23.12 för Java  
**Författare:** GroupDocs  

```java
signature.sign(destinFilePath, hibcLic_DM);
```

## Relaterade handledningar

- [Skapa streckkodssignatur PDF i Java – GroupDocs‑guide](/signature/java/barcode-signatures/create-sign-pdfs-groupdocs-barcode-java/)
- [Skapa streckkodssignatur i Java – Uppdatera PDF‑streckkoder](/signature/java/barcode-signatures/java-groupdocs-signature-barcode-initialize-update/)
- [Hur man läser QR‑kod PDF med Java och GroupDocs.Signature](/signature/java/barcode-signatures/java-pdf-barcode-search-groupdocs-signature-api/)