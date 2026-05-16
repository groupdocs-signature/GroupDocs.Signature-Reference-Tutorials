---
categories:
- Document Signing
- Healthcare Integration
date: '2026-05-16'
description: Leer hoe u een data matrix PDF maakt en een QR‑code PDF toevoegt met
  GroupDocs.Signature voor Java. Stapsgewijze handleiding voor het ondertekenen van
  zorgdocumenten.
keywords:
- create data matrix pdf
- add qr code pdf
- HIBC barcode Java
lastmod: '2026-05-16'
linktitle: HIBC PDF-ondertekeningsgids voor Java
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
title: Maak Data Matrix PDF met HIBC-barcode in Java
type: docs
url: /nl/java/barcode-signatures/sign-pdfs-hibc-lic-codes-groupdocs-java/
weight: 1
---

# Maak Data Matrix PDF met HIBC Barcode in Java

Als je farmaceutische of gezondheidslogistieke software bouwt, ben je waarschijnlijk tegen het probleem van papieren tracking, verloren handtekeningen en audit‑nachtmerries aangelopen. **Een Data Matrix PDF maken** die een HIBC LIC‑barcode bevat, lost die problemen op door je een sabotage‑bewijs, machinaal‑leesbare spoor te geven dat bestand is tegen afdrukken, scannen en regelgevende beoordeling. In deze tutorial zie je precies hoe je **QR‑code‑PDF**‑ondersteuning kunt **toevoegen**, evenals Aztec‑ en Data Matrix‑formaten, met behulp van GroupDocs.Signature voor Java.

## Snelle Antwoorden
- **Welke bibliotheek verwerkt HIBC‑barcodes in Java?** GroupDocs.Signature for Java.  
- **Welk barcode‑formaat is het meest compact?** Data Matrix – ideaal voor kleine labels.  
- **Kan ik zowel QR als Data Matrix aan dezelfde PDF toevoegen?** Ja, maak gewoon aparte `QrCodeSignOptions`.  
- **Heb ik een internetverbinding nodig tijdens runtime?** Nee, de bibliotheek werkt volledig offline na installatie.  
- **Welke Java‑versie wordt aanbevolen?** Java 11+ voor productie‑prestaties.

## Wat is HIBC‑barcode PDF‑ondertekening?
De `Signature`‑klasse in GroupDocs.Signature voor Java vertegenwoordigt een PDF‑document en biedt methoden om HIBC‑barcodes in te sluiten als digitale handtekeningen. Door een PDF te ondertekenen met een HIBC‑barcode maak je een verifieerbaar, sabotage‑bewijs record dat op elk punt in de toeleveringsketen kan worden gescand.

## Waarom Data Matrix en QR‑codes samen gebruiken?
GroupDocs.Signature ondersteunt **meer dan 50 invoer‑ en uitvoerformaten** en kan PDF‑bestanden van honderden pagina's verwerken zonder het volledige bestand in het geheugen te laden. Het gebruik van Data Matrix voor dichte, kleine labels en QR voor ruimere documenten geeft je de beste balans tussen leesbaarheid, gegevenscapaciteit (tot 4.296 tekens voor QR) en efficiëntie van de afdrukruimte.

## Vereisten
- **JDK 11 of hoger** (Java 8 werkt, maar Java 11+ wordt aanbevolen voor optimale prestaties).  
- **IDE** zoals IntelliJ IDEA, Eclipse of VS Code met Java‑extensies.  
- **Maven of Gradle** voor afhankelijkheidsbeheer (voorbeelden hieronder).  
- **Voorbeeld‑PDF** (bijv. `sample.pdf`) om de implementatie te testen.  
- **Geldige GroupDocs.Signature‑licentie** (gratis proefversie voor ontwikkeling, betaalde licentie voor productie).

## GroupDocs.Signature voor Java instellen

### Maven‑configuratie
Add the dependency to your `pom.xml`:

```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

### Gradle‑configuratie
For Gradle projects, add this to your `build.gradle`:

```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

### Directe downloadoptie
Je kunt het JAR‑bestand ook rechtstreeks downloaden van [GroupDocs.Signature for Java releases](https://releases.groupdocs.com/signature/java/) en handmatig toevoegen aan de classpath van je project. Deze aanpak werkt goed in netwerken met beperkte toegang.

### Een licentie verkrijgen
Vraag een gratis proefversie of tijdelijke licentie aan bij GroupDocs om watermerken te verwijderen en alle functies te ontgrendelen. Voor productie‑implementaties is een aangeschafte licentie vereist.

### Basisinitialisatie
De `Signature`‑klasse is het toegangspunt voor alle ondertekeningsbewerkingen. Hij laadt de PDF, past de barcode toe en schrijft het ondertekende bestand.

```java
import com.groupdocs.signature.Signature;

class InitializeSignature {
    public static void main(String[] args) {
        Signature signature = new Signature("sample.pdf");
        // Proceed with signing operations...
    }
}
```

## Hoe maak je een Data Matrix PDF met HIBC‑barcode?
Laad je bron‑PDF, configureer een `QrCodeSignOptions`‑object voor het Data Matrix‑formaat, en roep `sign()` aan – dat is alles wat je nodig hebt om een conforme HIBC Data Matrix‑barcode in te sluiten. De volgende stappen leiden je door de exacte benodigde code. `QrCodeSignOptions` definieert de instellingen voor een barcode‑handtekening, zoals type, inhoud, grootte en positie.

1. **Importeer de vereiste klassen** – deze geven je toegang tot de ondertekeningsengine en Data Matrix‑opties.  

```java
import com.groupdocs.signature.Signature;
import com.groupdocs.signature.options.sign.QrCodeSignOptions;
import com.groupdocs.signature.domain.qrcodes.QrCodeTypes;
```

2. **Instantieer het `Signature`‑object** met absolute paden voor bron‑ en bestemmingsbestanden.  

```java
String sourceFilePath = "YOUR_DOCUMENT_DIRECTORY";
String destinFilePath = "YOUR_OUTPUT_DIRECTORY/SignWithHIBCLICQR.pdf";

final Signature signature = new Signature(sourceFilePath);
```

3. **Configureer de Data Matrix‑opties** – stel de HIBC‑string in, kies `QrCodeTypes.HIBCLICDataMatrix`, en definieer de plaatsingscoördinaten. `QrCodeTypes` somt de ondersteunde barcode‑formaten voor HIBC‑handtekeningen op.  

```java
QrCodeSignOptions hibcLic_QR = new QrCodeSignOptions("A123PROD30917/75#422011907#GP293", QrCodeTypes.HIBCLICQR);
hibcLic_QR.setLeft(1); // Set the position from left
hibcLic_QR.setTop(1);   // Set the position from top
hibcLic_QR.setReturnContent(true); // Return content after signing
hibcLic_QR.setReturnContentType(FileType.PNG); // Specify return content type as PNG
```

4. **Pas de handtekening toe** op de PDF.  

```java
signature.sign(destinFilePath, hibcLic_QR);
```

5. **Maak de bronnen vrij** om bestands‑handles vrij te geven en geheugenlekken te voorkomen.  

```java
finally {
    if (signature != null) signature.dispose();
}
```

### Volledig werkend voorbeeld
Hier is de volledige stroom in één blok (de placeholders vertegenwoordigen de exacte code die je uit de eerdere fragmenten plakt):

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

#### Direct antwoord (40–70 woorden)
Om **een Data Matrix PDF te maken**, instantieer je `Signature` met je bron‑PDF, stel je `QrCodeSignOptions` in op `QrCodeTypes.HIBCLICDataMatrix` en geef je een correct geformatteerde HIBC‑string op, vervolgens roep je `signature.sign(outputPath, options)` aan. De bibliotheek schrijft de ondertekende PDF naar de bestemming, behoudt de lay‑out en voegt de barcode toe als een sabotage‑bewijs handtekening.

## Hoe QR‑code PDF toevoegen met GroupDocs.Signature?
Laad de PDF, configureer `QrCodeSignOptions` voor het QR‑formaat, en roep `sign()` aan. Dit tweeregel‑patroon werkt voor elke PDF‑grootte en schaalt de QR‑afbeelding automatisch voor optimale leesbaarheid. `QrCodeSignOptions` configureert de QR‑barcode‑handtekening, inclusief inhoud en visuele eigenschappen. Het positioneert de code op basis van de door jou ingestelde coördinaten, zodat deze niet overlapt met bestaande inhoud en scanbaar blijft na het afdrukken.

1. **Importeer QR‑specifieke klassen**  

```java
QrCodeSignOptions hibcLic_AZ = new QrCodeSignOptions("A123PROD30917/75#422011907#GP293", QrCodeTypes.HIBCLICAztec);
hibcLic_AZ.setLeft(1); // Set the position from left
hibcLic_AZ.setTop(200); // Set the position from top
hibcLic_AZ.setReturnContent(true); // Return content after signing
hibcLic_AZ.setReturnContentType(FileType.PNG); // Specify return content type as PNG
```

2. **Maak en configureer QR‑opties** – let op het gebruik van `QrCodeTypes.HIBCLICQR`.  

```java
signature.sign(destinFilePath, hibcLic_AZ);
```

3. **Onderteken het document**  

```java
QrCodeSignOptions hibcLic_DM = new QrCodeSignOptions("A123PROD30917/75#422011907#GP293", QrCodeTypes.HIBCLICDataMatrix);
hibcLic_DM.setLeft(1); // Set the position from left
hibcLic_DM.setTop(400); // Set the position from top
hibcLic_DM.setReturnContent(true); // Return content after signing
hibcLic_DM.setReturnContentType(FileType.PNG); // Specify return content type as PNG
```

> **Direct antwoord:** Gebruik `QrCodeTypes.HIBCLICQR` in `QrCodeSignOptions`, stel de HIBC‑inhoudsstring in, positioneer de code met `setLeft()` en `setTop()`, en roep vervolgens `signature.sign(outputPath, options)` aan. De QR‑barcode wordt direct ingebed, klaar voor smartphone‑ of scanner‑vastlegging.

## Veelvoorkomende fouten om te vermijden

### 1. Het vergeten van resource‑afvoer
**Wrong:**  
```java
Signature signature = new Signature("sample.pdf");
signature.sign(destinFilePath, options);
// Oops, no dispose() call
```  

**Fix:** Plaats het gebruik van `Signature` in een try‑with‑resources‑blok of roep expliciet `close()` aan in een finally‑clausule.

### 2. Onjuiste HIBC‑formaatstrings gebruiken
**Wrong:** Het gebruiken van generieke strings zoals “12345”.  
**Fix:** Volg de HIBCC‑standaard (bijv. `A123PROD30917/75#422011907#GP293`). Valideer met de [HIBCC online validator](https://www.hibcc.org/).

### 3. Hard‑coded bestands‑paden
**Wrong:**  
```java
String sourceFilePath = "C:/Users/John/Documents/test.pdf";
```  

**Fix:** Sla paden op in een configuratiebestand of omgevingsvariabele en lees ze tijdens runtime.

### 4. Barcode‑positieconflicten negeren
Plaats barcodes weg van bestaande tekst of handtekeningen. Gebruik PDF‑coördinaten (origine is linksonder) en test met een afgedrukt monster.

### 5. Niet testen met echte scanners
Print de ondertekende PDF en scan deze met de exacte hardware die in je workflow wordt gebruikt. Verifieer de leesbaarheid bij verschillende afdrukkwaliteiten.

## Praktische toepassingen in de gezondheidszorg

| Scenario | Aanbevolen barcode | Waarom het past |
|----------|--------------------|-----------------|
| **Farmaceutische distributie** | QR‑code | Hoge gegevenscapaciteit, breed gescand door smartphones. |
| **Voorraadbeheer** | Data Matrix | Kleine voetafdruk, ideaal voor dichte schap‑labels. |
| **Regelgevende naleving (FDA 21 CFR Part 11)** | QR + Data Matrix | Dual‑formaat biedt redundantie en auditbaarheid. |
| **Tracking van medische apparaten** | Aztec Code | Compact formaat werkt op verpakking met beperkte ruimte. |

## Prestatie‑overwegingen en best practices

### Batch‑verwerkingspatroon
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

- Maak per bestand een nieuwe `Signature`‑instantie om het geheugenverbruik laag te houden.  
- Gebruik een vaste thread‑pool (`Executors.newFixedThreadPool(Runtime.getRuntime().availableProcessors() - 1)`) voor parallelle verwerking, maar houd de heap‑grootte in de gaten omdat elke `Signature` de volledige PDF in het geheugen houdt.  

### Houd bibliotheken up‑to‑date
GroupDocs‑releases verbeteren de verwerkingssnelheid tot **20 %** en voegen nieuwe HIBC‑compliance‑functies toe. Plan elk kwartaal een controle van afhankelijkheden.

### Sjablonen cachen
Laad een PDF‑sjabloon één keer, kloon het voor elke barcode‑variant, en onderteken de klonen. Dit vermindert I/O en versnelt workflows met hoog volume.

## Veelgestelde vragen

**Q: Kan GroupDocs.Signature bestandstypen ondertekenen anders dan PDF?**  
A: Ja, het ondersteunt ook DOCX, XLSX, PPTX, PNG, JPEG en TIFF met dezelfde barcode‑ondertekenings‑API.

**Q: Hoe los ik “Invalid barcode content”‑fouten op?**  
A: Controleer of je HIBC‑string exact de HIBCC‑syntaxis volgt, gebruik de online validator, en zorg dat je de juiste `QrCodeTypes`‑constante voor het gekozen formaat gebruikt.

**Q: Wat is de maximale gegevenscapaciteit voor elk HIBC‑formaat?**  
A: QR ≈ 4.296 alfanumerieke tekens, Aztec ≈ 3.832 numeriek / 3.067 alfanumeriek, Data Matrix ≈ 3.116 numeriek / 2.335 alfanumeriek. Houd codes onder de 200 tekens voor optimale scanbetrouwbaarheid.

**Q: Is het mogelijk om meerdere barcode‑typen in één PDF in te sluiten?**  
A: Absoluut. Maak aparte `QrCodeSignOptions`‑objecten met verschillende posities en roep `signature.sign()` voor elk aan. Zorg er alleen voor dat ze niet overlappen.

**Q: Heb ik een internetverbinding nodig voor ondertekenen tijdens runtime?**  
A: Nee. Nadat het JAR‑bestand in de classpath staat en de licentie geactiveerd is, worden alle bewerkingen lokaal uitgevoerd.

## Aanvullende bronnen

- [GroupDocs.Signature voor Java Documentatie](https://docs.groupdocs.com/signature/java/)  
- [API‑referentiegids](https://reference.groupdocs.com/signature/java/)  
- [Laatste release‑downloads](https://releases.groupdocs.com/signature/java/)  
- [Licentie aanschaffen](https://purchase.groupdocs.com/buy)  
- [Gratis proefversie krijgen](https://releases.groupdocs.com/signature/java/)  
- [Tijdelijke licentie aanvragen](https://purchase.groupdocs.com/temporary-license/)  
- [GroupDocs‑forum](https://forum.groupdocs.com/c/signature/)

---

**Laatst bijgewerkt:** 2026-05-16  
**Getest met:** GroupDocs.Signature 23.12 voor Java  
**Auteur:** GroupDocs  

```java
signature.sign(destinFilePath, hibcLic_DM);
```

## Gerelateerde tutorials

- [Barcode‑handtekening PDF maken in Java – GroupDocs‑gids](/signature/java/barcode-signatures/create-sign-pdfs-groupdocs-barcode-java/)
- [Barcode‑handtekening maken in Java – PDF‑barcodes bijwerken](/signature/java/barcode-signatures/java-groupdocs-signature-barcode-initialize-update/)
- [Hoe QR‑code PDF lezen met Java en GroupDocs.Signature](/signature/java/barcode-signatures/java-pdf-barcode-search-groupdocs-signature-api/)