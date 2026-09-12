---
categories:
- Java Development
- Document Management
date: '2026-08-25'
description: Leer hoe u barcode kunt toevoegen aan PDF‑documenten in Java met GroupDocs.Signature.
  Deze stapsgewijze handleiding laat zien hoe u GS1DotCode-barcodes toevoegt, afbeeldingen
  extraheert en veelvoorkomende valkuilen vermijdt.
keywords:
- how to add barcode
- groupdocs signature java
- pdf document barcode
lastmod: '2026-08-25'
linktitle: Barcode toevoegen aan PDF Java
og_description: Leer hoe u barcode kunt toevoegen aan PDF in Java met GroupDocs.Signature.
  Stapsgewijze tutorial, code‑voorbeelden en oplossingsrichtlijnen voor GS1DotCode-barcodes.
og_image_alt: Guide showing Java code to embed GS1DotCode barcode into a PDF using
  GroupDocs.Signature
og_title: Hoe een barcode toe te voegen aan PDF in Java – Complete gids
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
title: Hoe een barcode toe te voegen aan PDF in Java
type: docs
url: /nl/java/digital-signatures/master-java-document-signing-groupdocs-signature/
weight: 1
---

# Hoe barcode toe te voegen aan PDF in Java

## Introductie

Heb je ooit geworsteld met de authenticiteit van documenten in je Java‑applicatie? Je bent niet de enige. Of je nu een voorraadbeheersysteem bouwt, contracten beheert, of supply‑chain‑documenten verwerkt, de kans is groot dat je een betrouwbare manier nodig hebt om PDF‑bestanden automatisch te ondertekenen en te verifiëren.

Traditionele digitale handtekeningen zijn uitstekend, maar soms heb je iets meer gespecialiseerd nodig—zoals barcode‑handtekeningen die naadloos werken met scansystemen en geautomatiseerde workflows. Daar komen GS1DotCode‑barcodes van pas.

**Wat je leert:**
- Hoe PDF‑documenten te ondertekenen met GS1DotCode‑barcodes in Java
- Hoe barcode‑handtekeningafbeeldingen te extraheren en op te slaan
- Wanneer (en waarom) barcode‑handtekeningen te gebruiken in plaats van traditionele methoden
- Veelvoorkomende valkuilen en hoe deze te vermijden

Aan het einde van deze gids heb je een kant‑en‑klare oplossing die je in elk Java‑project kunt integreren.

## Snelle antwoorden
- **Welke bibliotheek voegt barcodes toe aan PDF's in Java?** GroupDocs.Signature for Java.  
- **Welk barcode‑formaat wordt ondersteund?** GS1DotCode, een compacte 2‑D‑dotmatrix.  
- **Heb ik een betaalde licentie nodig?** Een gratis proefversie werkt voor testen; productie vereist een commerciële licentie.  
- **Kan ik de barcode als afbeelding extraheren?** Ja, met de `BarcodeSignature`‑API.  
- **Welke Java‑versie is vereist?** JDK 8 of hoger.

## Wat is hoe barcode toe te voegen?
*Hoe barcode toe te voegen* verwijst naar het proces waarbij je programmatisch een machine‑leesbare barcode‑grafiek in een PDF‑bestand embedt, zodat de barcode deel uitmaakt van de content‑stream van het document. Dit omvat het genereren van de barcode‑afbeelding, het positioneren op een pagina en het opslaan van de gewijzigde PDF, waarbij de barcode doorzoekbaar en afdrukbaar blijft.

## Waarom kiezen voor GS1DotCode barcodes?
GS1DotCode is ontworpen voor situaties waarin ruimte schaars is. In tegenstelling tot lineaire barcodes die horizontaal uitrekken, creëert DotCode een 2‑D‑matrix van stippen die veel informatie in een klein gebied verpakt. Dit maakt het perfect voor:

- **Kleine productetiketten** waarbij elke millimeter telt  
- **Hogesnelheids‑afdrukken** op productielijnen (het formaat is daarvoor geoptimaliseerd)  
- **Supply‑chain tracking** waar je complexe datastructuren moet coderen  

Het formaat kan tot **3.116 tekens** in een compact gebied verwerken en leest betrouwbaar zelfs bij hoge snelheden of bij gedeeltelijke schade. Werk je in retail of logistiek, dan gebruiken je partners waarschijnlijk al GS1‑standaarden—dus spreek je dezelfde taal.

> **Pro tip:** Gebruik GS1DotCode wanneer je meer dan 20 tekens moet embedden op een label kleiner dan 1 inch × 1 inch.

## Vereisten

Voordat je begint met coderen, controleer of je omgeving aan de volgende eisen voldoet.

### Vereiste bibliotheken en afhankelijkheden
- **GroupDocs.Signature for Java** 23.12 of later (ondersteunt **30+** documentformaten)  
- Maven of Gradle voor afhankelijkheidsbeheer

### Omgevingsconfiguratie
- **JDK 8** of nieuwer geïnstalleerd en geconfigureerd in je `PATH`  
- Een IDE zoals IntelliJ IDEA, Eclipse of NetBeans  
- Een voorbeeld‑PDF‑bestand om mee te experimenteren (elke niet‑beveiligde PDF volstaat)

### Kennisvereisten
- Basis Java‑syntaxis (variabelen, methoden, objecten)  
- Vertrouwdheid met Maven‑ of Gradle‑afhankelijkheidsdeclaratie  
- Begrip van bestands‑I/O in Java (bijv. `FileInputStream`)

Als een van deze items ontbreekt, pauzeer dan en installeer ze nu; de latere stappen gaan ervan uit dat ze aanwezig zijn.

## Instellen van GroupDocs.Signature voor Java

### Maven
Als je Maven gebruikt, voeg dan de volgende afhankelijkheid toe aan je `pom.xml`:

```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

Maven downloadt de bibliotheek en alle vereiste transitieve afhankelijkheden automatisch.

### Gradle
Voor Gradle‑gebruikers, voeg deze regel toe aan je `build.gradle`‑bestand:

```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

Gradle lost het pakket op dezelfde hands‑off manier op.

### Directe download
Als je liever handmatig beheert, download de JAR‑bestanden van de officiële release‑pagina: [GroupDocs.Signature voor Java releases](https://releases.groupdocs.com/signature/java/). Plaats de JAR‑bestanden op de classpath van je project.

**Pro tip:** Maven of Gradle vereenvoudigt toekomstige upgrades—verhoog simpelweg het versienummer.

### Licentie‑acquisitie
GroupDocs biedt drie licentie‑opties:

- **Gratis proefversie** – geen creditcard, watermerken toegepast op de output  
- **Tijdelijke licentie** – 30‑daagse volledige‑functies evaluatie  
- **Commerciële licentie** – verwijdert proefbeperkingen en verleent productierechten  

Na het verkrijgen van een licentiebestand, plaats het in de resources‑map van je project en laad het voordat een `Signature`‑object wordt aangemaakt.

`License.setLicense` laadt het GroupDocs‑licentiebestand, waardoor volledige functionaliteit beschikbaar is zonder proefbeperkingen.

Voer het volgende fragment uit om te verifiëren dat de bibliotheek correct wordt geladen:

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

Zie je “Initialization successful!” dan is de installatie voltooid. Zo niet, controleer dan het classpath en het licentiepad.

## Implementatiegids

We behandelen twee kernfuncties: (1) een PDF ondertekenen met een GS1DotCode barcode en (2) die barcode extraheren als afbeeldingsbestand.

### Functie 1: document ondertekenen met GS1DotCode barcode

#### Hoe een PDF ondertekenen met een GS1DotCode barcode in Java?

Laad de doel‑PDF met `new Signature("source.pdf")`, configureer een `BarcodeSignOptions`‑object met GS1‑geformatteerde data, en roep `sign()` aan om een nieuwe PDF te produceren die de barcode embedt. Deze bewerking schrijft de barcode direct in de PDF‑content‑stream, waardoor deze behouden blijft bij afdrukken en herscannen.

Het proces bestaat uit drie beknopte stappen: maak een `Signature`‑instantie, stel `BarcodeSignOptions` in, en roep `sign()` aan. De code hieronder toont elke stap.

##### 1. initialiseer het handtekeningobject
De `Signature`‑klasse is het toegangspunt voor alle documentverwerkingsbewerkingen in GroupDocs.Signature.

```java
import com.groupdocs.signature.Signature;

String sourceFilePath = "YOUR_DOCUMENT_DIRECTORY/document.pdf";
final Signature signature = new Signature(sourceFilePath);
```

> **Waarom dit belangrijk is:** Het `Signature`‑object abstraheert bestands‑handling, streamt grote PDF's efficiënt zonder het volledige bestand in het geheugen te laden.

##### 2. configureer barcode‑opties
`BarcodeSignOptions` laat je het barcode‑type, de gecodeerde data, positie en afmetingen specificeren.

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

> **Belangrijke punten:**  
> - De gecodeerde string volgt GS1 Application Identifiers (AIs) zoals `(01)` voor GTIN, `(15)` voor vervaldatum, enz.  
> - `setLeft()` en `setTop()` gebruiken punten (72 pts = 1 in).  
> - De minimaal aanbevolen grootte voor betrouwbare scanning is **108 pt × 108 pt** (1,5 in × 1,5 in).

##### 3. onderteken het document
Voeg de geconfigureerde opties toe aan een lijst (je kunt meerdere handtekeningtypen combineren) en roep `sign()` aan.

```java
import java.util.ArrayList;
import java.util.List;

List<com.groupdocs.signature.options.sign.SignOptions> listOptions = new ArrayList<>();
listOptions.add(gs1DotCodeOptions);
signature.sign("YOUR_OUTPUT_DIRECTORY/signed_document_with_gs1dotcode.pdf", listOptions);
```

> **Prestatie‑opmerking:** Het hergebruiken van één `Signature`‑instantie voor batch‑bewerkingen vermindert de overhead van objectcreatie en verbetert de doorvoersnelheid.

### Functie 2: barcode‑handtekeninginhoud opslaan naar bestand

#### Hoe een barcode‑afbeelding uit een ondertekende PDF te extraheren in Java?

`BarcodeSignature` vertegenwoordigt een barcode‑handtekeningobject dat uit een ondertekend document is gehaald, en biedt toegang tot zowel de data als de afbeeldingsinhoud.

Maak een `BarcodeSignature`‑instantie (of haal er één op via `search()`), lees de Base64‑gecodeerde afbeeldingsdata via `getContent()`, decodeer deze en schrijf de bytes naar een PNG‑bestand. Zo krijg je een zelfstandige afbeelding die je in een UI kunt tonen of naar een labelprinter kunt sturen.

##### 1. simuleer barcode‑handtekeningcreatie
In echte scenario's haal je de `BarcodeSignature` uit een zoekresultaat; hier maken we het handmatig aan voor illustratie.

```java
import com.groupdocs.signature.domain.signatures.BarcodeSignature;
import java.io.FileOutputStream;

String base64String = "SampleBase64EncodedData";
BarcodeSignature barcodeSignature = new BarcodeSignature(base64String);
```

##### 2. sla de inhoud op naar een bestand
Decodeer de Base64‑string en schrijf de resulterende bytes naar schijf met een try‑with‑resources‑blok.

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

> **Gotcha:** `getContent()` kan `null` retourneren als de handtekening zonder afbeelding is aangemaakt. Controleer altijd op `null` vóór het schrijven.

## Veelvoorkomende problemen en oplossingen

### Probleem: barcode wordt niet gescand
**Symptomen:** De barcode ziet er goed uit in de PDF‑viewer, maar scanners geven fouten.

**Oplossingen:**
- Vergroot de barcode tot minimaal **108 pt × 108 pt**.  
- Zorg dat de printerresolutie **≥ 300 dpi** is.  
- Controleer of de GS1‑datastring de juiste AI‑syntaxis volgt; een ontbrekende haakje breekt de scanner.

### Probleem: OutOfMemoryError bij grote PDF's
**Symptomen:** Het verwerken van documenten groter dan **50 MB** veroorzaakt heap‑space‑fouten.

**Oplossingen:**
- Start de JVM met een grotere heap, bijv. `-Xmx2g`.  
- Verwerk documenten in kleinere batches.  
- Vernietig `Signature`‑objecten expliciet: `signature.dispose()` na elk bestand.

### Probleem: barcode ziet er wazig uit
**Symptomen:** De gerenderde barcode is gepixeld in de output‑PDF.

**Oplossingen:**
- Gebruik grotere afmetingen; de bibliotheek rendert vector‑graphics wanneer mogelijk, maar verkleinen na generatie veroorzaakt artefacten.  
- Vermijd raster‑naar‑vector‑conversies; laat GroupDocs direct renderen vanuit de vector‑definitie.

### Probleem: licentie‑uitzonderingen
**Symptomen:** Fouten zoals “License not found” of “Trial limitations exceeded”.

**Oplossingen:**
- Plaats het licentiebestand in de classpath‑root (`src/main/resources`).  
- Roep `License.setLicense("GroupDocs.Signature.lic")` **vóór** enige `Signature`‑instantiatie aan.  
- Controleer bij tijdelijke licenties de vervaldatum (30 dagen vanaf uitgifte).

## Wanneer deze aanpak te gebruiken

### Goede gebruikssituaties
- **Supply‑chain tracking** – embed product‑ID’s, batch‑nummers en vervaldatums direct op verzenddocumenten.  
- **Geautomatiseerde label‑afdruk** – genereer barcodes on‑the‑fly voor elke PDF‑factuur.  
- **Gereguleerde industrieën** – GS1‑standaarden zijn verplicht in veel retail‑ en zorgomgevingen.  

### Wanneer alternatieven te overwegen
- Als je alleen cryptografische integriteit nodig hebt, is een standaard PKI‑digitale handtekening geschikter.  
- Voor eenvoudige visuele annotaties volstaat een tekst‑handtekening of afbeelding‑stempel.  
- Wanneer de bestandsgrootte kritisch is, vermijd het toevoegen van hoge‑resolutie barcode‑afbeeldingen; gebruik in plaats daarvan QR‑codes die bij vergelijkbare datadichtheid kleiner kunnen zijn.

## Beveiligingsbest practices

### Gegevensvalidatie
Sanitiseer alle door gebruikers geleverde data voordat je deze in een barcode codeert. Misvormde GS1‑strings kunnen downstream‑scan‑fouten veroorzaken of, in het slechtste geval, buffer‑overflows in legacy scanner‑firmware triggeren.

### Toegangscontrole
Implementeer role‑based access control (RBAC) zodat alleen geautoriseerde gebruikers de onderteken‑API kunnen aanroepen. Bewaar het licentiebestand veilig en beperk bestands‑systeem‑rechten.

### Auditlogboek
Log elke onderteken‑operatie met details zoals gebruikers‑ID, tijdstempel, bron‑bestandspad en de exacte GS1‑payload. Voorbeeld‑logfragment:

```java
// Simple logging example (use a proper logging framework in production)
System.out.println("Document signed by: " + userId + " at " + new Date());
System.out.println("Barcode data: " + barcodeData);
```

### Detectie van manipulatie
Combineer een barcode‑handtekening met een cryptografische digitale handtekening. De barcode levert machine‑leesbare data, terwijl de digitale handtekening integriteit en non‑repudiatie garandeert.

## Praktische toepassingen

### 1. supply‑chain beheer
Elke pakbon krijgt een GS1DotCode‑barcode die de GTIN, batch en bestemming van de zending codeert. Scanners bij elk controlepunt werken de ERP‑systemen automatisch bij, waardoor handmatige invoerfouten met **98 %** afnemen.

### 2. voorraadbeheer
Bij ontvangst van goederen wordt de ontvangen PDF ondertekend met een barcode die het inkooporder‑nummer en de aantallen bevat. Magazijnpersoneel scant de barcode en de voorraaddatabase wordt realtime bijgewerkt.

### 3. retail point‑of‑sale
Facturen met een barcode stellen kassamedewerkers in staat retouren te verwerken door de factuur te scannen in plaats van handmatig het transactie‑ID in te voeren, waardoor de gemiddelde afhandelingstijd met **30 seconden** per retour daalt.

### 4. gezondheidszorgdocumentatie
Voorschriften ondertekend met een GS1DotCode‑barcode bevatten patiënt‑ID, medicatiecode en doseringsinstructies. Apotheken scannen de barcode, waardoor transcriptiefouten die leiden tot bijwerkingen worden geëlimineerd.

## Prestatie‑overwegingen

### Geheugenbeheer
GroupDocs.Signature streamt PDF‑data, maar je moet nog steeds bronnen snel sluiten:

```java
try (Signature signature = new Signature(sourceFilePath)) {
    // Do your signing operations here
} // Signature automatically disposed here
```

Het gebruik van try‑with‑resources garandeert dat het `Signature`‑object bestands‑handles vrijgeeft, zelfs bij een uitzondering.

### Batchverwerkingstips
- Hergebruik dezelfde `BarcodeSignOptions`‑instantie wanneer de payload identiek is voor veel documenten.  
- Paralleliseer ondertekening met `ExecutorService` voor CPU‑intensieve workloads; een typische 8‑core server kan **≈ 150 PDF's per minuut** ondertekenen wanneer elk bestand onder 5 MB is.  
- Beperk externe licentie‑validatie‑calls om rate‑limit throttling te vermijden.

### Bestandsformaatoptimalisatie
- Geef de voorkeur aan PDF/A‑1b voor archivering; het comprimeert streams en verkleint de bestandsgrootte tot **40 %**.  
- Houd barcode‑afmetingen zo klein mogelijk; een 1,5 in × 1,5 in barcode voegt ongeveer **15 KB** toe aan een 2 MB PDF.

## Conclusie

Je beschikt nu over een volledige, productie‑klare workflow om GS1DotCode‑barcode‑handtekeningen toe te voegen aan PDF‑bestanden in Java, die barcodes als afbeeldingen te extraheren, en het proces te integreren in grotere document‑beheerpijplijnen. Onthoud:

1. Valideer GS1‑payloads vóór codering.  
2. Kies barcode‑afmetingen die scankwaliteit balanceren met lay‑out‑beperkingen.  
3. Combineer barcode‑handtekeningen met cryptografische handtekeningen voor volledige beveiligingsdekking.  

Volgende stappen: verken andere handtekeningtypen die GroupDocs.Signature biedt—QR‑codes, tekststempels en digitale certificaten—die allemaal een consistente API‑structuur delen.

---

## Veelgestelde vragen

**Q: Wat is GS1DotCode en waarom verschilt het van QR‑codes?**  
A: GS1DotCode is een compacte 2‑D‑dotmatrix die tot **3.116 tekens** opslaat in een kleinere voetafdruk dan QR‑codes, waardoor het ideaal is voor kleine etiketten en hogesnelheids‑afdrukken.

**Q: Kan ik een gratis proefversie gebruiken voor productie‑implementaties?**  
A: De gratis proefversie is beperkt tot evaluatie en voegt een watermerk toe aan output‑bestanden. Voor productie‑gebruik is een aangekochte of tijdelijke 30‑daagse licentie vereist.

**Q: Hoe positioneer ik de barcode op een specifieke pagina?**  
A: Stel `setPageNumber(pageIndex)` in op het `BarcodeSignOptions`‑object en pas `setLeft()` en `setTop()` aan voor precieze plaatsing.

**Q: Ondersteunt GroupDocs.Signature wachtwoord‑beveiligde PDF's?**  
A: Ja. Geef het wachtwoord mee bij het construeren van het `Signature`‑object: `new Signature("file.pdf", "password")`.

**Q: Hoe kan ik verifiëren dat een barcode‑handtekening correct is toegevoegd?**  
`Signature.search()` zoekt een document naar handtekeningen en retourneert een collectie van overeenkomstige handtekeningobjecten. Gebruik `Signature.search()` met `BarcodeSearchOptions`. De geretourneerde `BarcodeSignature`‑objecten bevatten de gecodeerde data en afbeeldingsinhoud voor verificatie.

**Q: Wat is de minimale barcode‑grootte voor betrouwbare scanning?**  
A: Streef naar minimaal **108 pt × 108 pt** (1,5 in × 1,5 in). Grotere formaten verbeteren leesbaarheid, vooral op printers met lage resolutie.

**Q: Kan ik meerdere PDF's gelijktijdig ondertekenen?**  
A: Ja. Maak een thread‑pool en instantiate een apart `Signature`‑object per thread; de bibliotheek is thread‑safe zolang elke thread met zijn eigen document werkt.

**Q: Is er een limiet aan het aantal barcodes dat ik in één PDF kan embedden?**  
A: Geen harde limiet, maar elke barcode voegt ongeveer **15 KB** data toe. Voor PDF's groter dan **100 MB** is batch‑verwerking aan te raden om het geheugenbeheer te optimaliseren.

**Q: Werkt de bibliotheek op niet‑Windows platformen?**  
A: GroupDocs.Signature for Java is platform‑agnostisch en draait op elk OS met een compatibele JRE, inclusief Linux en macOS.

**Last Updated:** 2026-08-25  
**Tested With:** GroupDocs.Signature 23.12 for Java  
**Author:** GroupDocs

## Gerelateerde tutorials

- [Hoe barcode‑handtekeningen te verifiëren in Java met GroupDocs.Signature](/signature/java/barcode-signatures/verify-barcode-signatures-groupdocs-signature-java/)  
- [Barcode‑handtekening Java – PDF‑barcodes bijwerken](/signature/java/barcode-signatures/java-groupdocs-signature-barcode-initialize-update/)  
- [QR‑code toevoegen aan PDF Java – Complete gids met GroupDocs.Signature](/signature/java/qr-code-signatures/qr-code-signatures-java-groupdocs/)