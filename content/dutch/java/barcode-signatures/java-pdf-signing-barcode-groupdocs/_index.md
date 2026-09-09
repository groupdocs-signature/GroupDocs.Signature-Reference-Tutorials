---
categories:
- Java PDF Processing
date: '2026-07-20'
description: Leer hoe je een barcode-handtekening in PDF-documenten maakt met Java
  en GroupDocs.Signature. Stapsgewijze tutorial met codevoorbeelden en best practices.
keywords:
- create barcode signature
- how to add barcode
- generate code128 barcode
- add barcode pdf
- tamper evident barcode
lastmod: '2026-07-20'
linktitle: Barcode-handtekening maken in Java
og_description: Maak een barcode-handtekening in PDF met Java en GroupDocs.Signature.
  Leer stap voor stap hoe je Code128-barcodes toevoegt, positioneert en documenten
  beveiligt.
og_image_alt: 'Developer guide: Create barcode signature in PDF using Java and GroupDocs'
og_title: Barcode-handtekening maken in PDF met Java – Volledige gids
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
title: Hoe een barcode-handtekening in PDF te maken met Java
type: docs
url: /nl/java/barcode-signatures/java-pdf-signing-barcode-groupdocs/
weight: 1
---

# Hoe een barcodehandtekening maken in PDF met Java

In deze tutorial leer je hoe je **een barcodehandtekening** maakt in PDF‑bestanden met Java en GroupDocs.Signature. Barcodehandtekeningen bevatten machine‑leesbare identifiers die zowel tamper‑evident als gemakkelijk te scannen zijn — perfect voor contracten, certificaten, facturen en elk document dat betrouwbare verificatie nodig heeft.

## Snelle antwoorden
- **Wat is een barcodehandtekening?** Een barcode ingebed in een PDF die gestructureerde gegevens opslaat en kan worden gelezen door scanners of software.  
- **Welke barcode‑type wordt aanbevolen?** Code128, omdat het alfanumerieke gegevens compact verwerkt.  
- **Heb ik een licentie nodig?** Een gratis proefversie werkt voor testen; een volledige licentie is vereist voor productie.  
- **Kan ik de barcode op elke paginagrootte plaatsen?** Ja — gebruik op percentages gebaseerde positionering voor automatische schaalvergroting.  
- **Is de barcode vector‑gebaseerd?** Ja, het voegt slechts enkele kilobytes toe aan de PDF en blijft scherp bij elke resolutie.  

## Wat is een barcodehandtekening?
Een barcodehandtekening is een vector‑gebaseerde barcode die direct in een PDF‑pagina wordt ingebed, en zowel fungeert als visueel element als cryptografische handtekening die later kan worden gevalideerd. Het slaat gestructureerde gegevens op, zoals ID’s of tijdstempels, en waarborgt de integriteit van het document terwijl het een machine‑leesbare referentie biedt.

## Waarom barcodehandtekeningen belangrijk zijn voor jouw PDF’s
Barcodehandtekeningen geven PDF’s een compact, machine‑leesbaar identifier dat direct kan worden gescand, waardoor handmatige gegevensinvoer wordt geëlimineerd en fouten worden verminderd. Omdat ze zijn ingebed als vectorafbeeldingen, blijven ze scherp bij elke resolutie en voegen ze slechts enkele kilobytes toe aan het bestand. Deze combinatie van leesbaarheid, tamper‑evidence en minimale grootte maakt ze ideaal voor contracten, facturen, certificaten en elk document dat betrouwbare verificatie vereist.

Hier is een uitdaging die je waarschijnlijk bent tegengekomen: je moet unieke identifiers aan PDF’s toevoegen die zowel machine‑leesbaar als tamper‑evident zijn. Misschien werk je aan een documentbeheersysteem, verwerk je certificaten, of behandel je contracten die later moeten worden geverifieerd.

Dat is waar barcodehandtekeningen van pas komen. In tegenstelling tot eenvoudige tekststempels kun je met barcodes gestructureerde gegevens embedden die scanners (en jouw software) direct kunnen lezen. Bovendien, wanneer je ze combineert met PDF‑ondertekening via GroupDocs.Signature voor Java, krijg je een krachtige manier om documenten te volgen en te verifiëren zonder complexe database‑lookups.

In deze gids leer je precies hoe je barcodehandtekeningen implementeert in je Java‑PDF’s — van basisinstelling tot productie‑klare code met flexibele positionering. Of je nu een factuursysteem, certificaategenerator of contractbeheersplatform bouwt, je hebt aan het einde alles wat je nodig hebt.

**Wat je onder de knie krijgt:**
- GroupDocs.Signature voor Java in enkele minuten opzetten  
- Code128 barcodehandtekeningen maken (en waarom dit vaak de beste keuze is)  
- Barcodes positioneren met op percentages gebaseerde lay‑outs die op elke PDF‑grootte werken  
- Veelvoorkomende valkuilen vermijden die ontwikkelaars tegenkomen  
- Je implementatie correct testen  

## Hoe een barcodehandtekening maken in Java
Een barcodehandtekening maken in Java omvat het laden van de doel‑PDF, het configureren van de barcode‑opties zoals data, type, grootte en positie, en vervolgens het toepassen van de handtekening om een nieuw document te genereren. GroupDocs.Signature verzorgt het renderen en de cryptografische binding, zodat je alleen de gewenste parameters hoeft te leveren en de bestands‑paden moet beheren.

## Voorvereisten en checklist voor de omgeving

Voordat je begint, controleer of je de volgende zaken klaar hebt staan:

- **Java Development Kit (JDK) 8 of nieuwer** – vereist voor alle GroupDocs Java‑bibliotheken.  
- **Maven of Gradle** – om de GroupDocs.Signature‑dependency te beheren.  
- **Een IDE** zoals IntelliJ IDEA, Eclipse of VS Code met Java‑extensies.  
- **GroupDocs.Signature voor Java** (versie 23.12 of nieuwer wordt aanbevolen).  
- **Basiskennis van Java** – je moet vertrouwd zijn met het maken van klassen, het afhandelen van uitzonderingen en werken met bestands‑I/O.

## GroupDocs.Signature in je project instellen

De bibliotheek in je project krijgen is eenvoudig. Kies je build‑tool:

**Voor Maven‑gebruikers**, voeg deze dependency toe aan je `pom.xml`:

```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

**Gradle gebruiken?** Voeg deze regel toe aan je `build.gradle`:

```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

**Handmatige installatie verkiezen?** Download de JAR rechtstreeks van [GroupDocs.Signature for Java releases](https://releases.groupdocs.com/signature/java/) en voeg deze toe aan je classpath.

### Je licentie regelen

Voordat je volledig productie gaat, moet je de licentie regelen:

- **Gratis proefversie:** Perfect voor testen — haal deze van de GroupDocs‑website om de kernfuncties te verkennen.  
- **Tijdelijke licentie:** Meer tijd nodig om te evalueren? Vraag een tijdelijke licentie van 30 dagen aan.  
- **Volledige licentie:** Klaar voor productie? Schaf een licentie aan voor onbeperkt gebruik.  

Hier is een snelle sanity‑check om te bevestigen dat alles werkt:

```java
Signature signature = new Signature("sample.pdf");
System.out.println("Signature object created successfully.");
```

Als dit zonder fouten draait, ben je klaar om verder te gaan!

## Hoe een barcodehandtekening maken in Java

Nu het leuke gedeelte — laten we een PDF ondertekenen met een barcode. We splitsen dit op in hapklare stappen zodat je precies begrijpt wat er op elk moment gebeurt.

### Stap 1: Het Signature‑object initialiseren

**Definitie‑anker:** De `Signature`‑klasse is het toegangspunt van GroupDocs voor het laden, wijzigen en opslaan van PDF‑documenten.

Eerst moet je GroupDocs vertellen welke PDF je wilt bewerken:

```java
Signature signature = new Signature("input.pdf");
```

**Wat er gebeurt:** Het `Signature`‑object laadt je PDF in het geheugen en maakt het klaar voor wijzigingen. Zorg ervoor dat je bestands‑pad correct is — een veelvoorkomende valkuil is het gebruiken van backslashes op Windows zonder ze te escapen (gebruik `\\` of gewoon forward slashes, die werken platform‑onafhankelijk).

### Stap 2: Je barcode‑opties configureren (Hoe een barcode toe te voegen)

**Definitie‑anker:** `BarcodeSignOptions` bevat alle instellingen die nodig zijn om een barcode in een PDF te renderen.

Maak nu de barcodehandtekening met jouw data:

```java
BarcodeSignOptions options = new BarcodeSignOptions("12345678");
options.setEncodeType(BarcodeEncodeType.Code128);
```

- `"12345678"` is je barcode‑data — dit kan een order‑ID, certificaatnummer of elke gewenste identifier zijn.  
- `Code128` is het coderings‑type (meer over de juiste keuze hieronder).  

**Pro‑tip:** Code128 kan zowel cijfers als letters verwerken, waardoor het veelzijdig is voor de meeste scenario’s. Als je alleen cijfers nodig hebt, kan `Code39` eenvoudiger zijn, maar Code128 biedt meer flexibiliteit.

### Stap 3: Je barcode positioneren (Hoe een PDF met barcode te ondertekenen)

**Definitie‑anker:** `SignatureOptions` biedt lay‑out‑eigenschappen zoals paginanummer, grootte en uitlijning.

Hier komt GroupDocs echt van pas — positionering op basis van percentages betekent dat je barcode er goed uitziet op elke PDF‑grootte:

```java
options.setLeft(10);   // 10% from the left edge
options.setTop(90);    // 90% from the bottom edge (near the footer)
options.setWidth(30);  // 30% of page width
options.setHeight(10); // 10% of page height
options.setPageNumber(1);
```

**Waarom percentages belangrijk zijn:** Stel je voor dat je zowel A4‑documenten als legal‑formaat formulieren ondertekent. Met percentage‑positionering schaalt je barcode automatisch proportioneel op beide. Het gebruik van vaste pixelwaarden zou je barcode te klein maken op grote documenten of te groot op kleine documenten.

**Praktisch voorbeeld:** Op een A4‑pagina (595 × 842 punten) is een barcode van 30 % breed ongeveer 180 punten breed. Op een legal‑pagina (612 × 1008 punten) wordt deze ongeveer 184 punten breed — automatisch proportioneel.

### Stap 4: Ondertekenen en het document opslaan (Hoe een barcode‑pdf toe te voegen)

Tijd om de handtekening daadwerkelijk toe te passen en je werk op te slaan:

```java
signature.sign(outputPath, options);
```

**Belangrijk:** De output‑map moet bestaan voordat je deze code uitvoert. GroupDocs maakt geen geneste mappen voor je aan, dus maak ze eerst aan of behandel dit in je code:

```java
new File("output").mkdirs();
```

**Wat als er iets misgaat?** Plaats dit in een try‑catch‑blok:

```java
try {
    signature.sign("signed.pdf", options);
} catch (Exception e) {
    e.printStackTrace();
}
```

## De juiste barcode‑type kiezen voor jouw behoeften (generate code128 barcode)

GroupDocs ondersteunt meerdere barcode‑formaten, en de juiste keuze maakt verschil. Hier een praktische vergelijking:

**Code128 (Onze standaardkeuze):**
- **Beste voor:** Gemengde alfanumerieke data (ID’s zoals "INV2024-001")  
- **Capaciteit:** Tot 128 ASCII‑tekens  
- **Waarom het wint:** Compact, breed ondersteund, verwerkt zowel letters als cijfers  
- **Gebruik wanneer:** Je flexibiliteit nodig hebt en niet weet welk type data je gaat coderen  

**Code39:**
- **Beste voor:** Eenvoudige alfanumerieke codes  
- **Capaciteit:** 43 tekens (A‑Z, 0‑9 en enkele symbolen)  
- **Waarom overwegen:** Oudere scanners ondersteunen het vaak beter  
- **Gebruik wanneer:** Je werkt met legacy‑systemen of eenvoud belangrijker is dan datadichtheid  

**QR‑code:**
- **Beste voor:** Grote hoeveelheden data (URL’s, JSON‑payloads)  
- **Capaciteit:** Tot 3 KB data  
- **Waarom krachtig:** Kan complexe datastructuren opslaan, foutcorrectie ingebouwd  
- **Gebruik wanneer:** Je gestructureerde data of URL’s moet embedden  

**EAN/UPC:**
- **Beste voor:** Productidentificatie  
- **Capaciteit:** Vaste numerieke codes (8‑13 cijfers)  
- **Gebruik wanneer:** Je werkt met retail‑ of voorraad‑systemen  

**Snelle beslissingsgids:**  
- Letters en cijfers nodig? → Code128  
- Alleen cijfers, houd het simpel? → Code39  
- Veel data of URL’s? → QR‑code  
- Retail/productcodes? → EAN/UPC  

## Veelvoorkomende valkuilen en hoe ze te vermijden (tamper evident barcode)

Hier zijn de problemen waar ontwikkelaars het vaakst tegenaan lopen (zodat jij ze niet tegenkomt):

### Probleem 1: Barcode‑positionering ziet er verkeerd uit

**Symptoom:** Je barcode verschijnt op onverwachte plekken of wordt afgesneden.

**Veelvoorkomende oorzaken:**  
- Pixelwaarden gebruiken op verschillende paginagroottes  
- Vergeten dat PDF‑coördinaten beginnen links‑onder, niet links‑boven  
- Marges die inhoud buiten het zichtbare gebied duwen  

**Oplossing:** Gebruik altijd percentage‑gebaseerde positionering voor consistentie:

```java
options.setLeft(5);
options.setTop(95);
options.setWidth(40);
options.setHeight(12);
```

### Probleem 2: Barcode‑tekst is onleesbaar

**Symptoom:** De gecodeerde tekst wordt weergegeven maar scanners kunnen het niet lezen.

**Oorzaken:**  
- Barcode te klein voor de hoeveelheid data  
- Verkeerd coderings‑type voor je data  
- Lage contrast tussen strepen en achtergrond  

**Oplossing:** Pas de barcode‑grootte aan op basis van de datalengte. Voor Code128 met 10‑15 tekens, mik op minimaal 8‑10 % paginabreedte.

### Probleem 3: Bestands‑pad‑uitzonderingen

**Symptoom:** `FileNotFoundException` of soortgelijke fouten.

**Oorzaken:**  
- Hard‑gecodeerde Windows‑paden met enkele backslashes  
- Output‑map bestaat niet  
- Bestands‑toegangsrechten  

**Oplossing:** Gebruik forward slashes (ze werken overal) en maak mappen eerst aan:

```java
Path output = Paths.get("output/signed.pdf");
Files.createDirectories(output.getParent());
```

### Probleem 4: Geheugenproblemen bij grote PDF’s

**Symptoom:** Out‑of‑memory‑fouten bij het verwerken van grote documenten.

**Oplossing:** Sluit het `Signature`‑object wanneer je klaar bent om bronnen vrij te geven:

```java
signature.close();
```

## Je barcode‑implementatie testen

Voordat je live gaat, zorg dat je barcodes daadwerkelijk werken. Hier een praktische test‑checklist:

### 1. Visuele inspectie
Open je ondertekende PDF en controleer:
- Is de barcode zichtbaar en correct gepositioneerd?  
- Ziet hij er scherp uit (niet wazig of gepixeld)?  
- Is er voldoende witruimte eromheen?

### 2. Scan‑test
Gebruik een barcode‑scanner‑app op je telefoon (bijv. “Barcode Scanner” of “QR & Barcode Reader”) om te verifiëren:
- De scanner kan je barcode lezen  
- De gedecodeerde data komt overeen met wat je hebt gecodeerd  
- Het werkt vanuit verschillende hoeken en afstanden

### 3. Cross‑platform test
Open je PDF op verschillende apparaten:
- Windows (Adobe Reader, Chrome)  
- Mac (Preview, Chrome)  
- Mobiele apparaten (iOS, Android)  

Zorg dat de barcode overal correct wordt weergegeven.

### 4. Geautomatiseerde testcode
Hier is een eenvoudige test die je kunt uitvoeren:

```java
Signature testSignature = new Signature("signed.pdf");
List<BarcodeSignature> signatures = testSignature.search(BarcodeSignature.class);
if (signatures.size() > 0) {
    System.out.println("Barcode found: " + signatures.get(0).getText());
}
```

## Praktijkvoorbeelden voor barcodehandtekeningen

Laten we kijken waar deze techniek echt schittert in productie‑omgevingen:

### 1. Certificaatgeneratie en -verificatie
**Scenario:** Je bouwt een trainingsplatform dat voltooiingscertificaten uitgeeft.  
**Implementatie:** Genereer een uniek certificaat‑ID (bijv. “CERT‑2024‑00123”) en embed dit als een Code128‑barcode in de rechter‑onderhoek. Het scannen van de barcode laat je API de certificaatdetails direct ophalen, waardoor handmatige invoer overbodig wordt.

### 2. Factuursortering
**Scenario:** Je bedrijf verwerkt duizenden facturen per maand.  
**Implementatie:** Voeg factuurnummer en vervaldatum toe als QR‑code op een plek waar scan‑apparatuur deze gemakkelijk kan lezen. Geautomatiseerde sorteersystemen kunnen facturen zonder menselijke tussenkomst routeren, waardoor de verwerkingstijd van uren naar minuten wordt verkort.

### 3. Juridisch contractbeheer
**Scenario:** Een advocatenkantoor moet contractversies en amendementen bijhouden.  
**Implementatie:** Elke contractversie krijgt een unieke barcode‑identifier die contract‑ID, versienummer en ondertekeningsdatum bevat. Scannen tijdens audits haalt automatisch de volledige versiegeschiedenis op.

### 4. Beveiliging van medische dossiers
**Scenario:** Een ziekenhuis wil ongeautoriseerde toegang tot dossiers voorkomen.  
**Implementatie:** Embed patiënt‑ID en tijdstempel van creatie in een barcode. Alleen geauthenticeerde apparaten kunnen decoderen en toegang krijgen tot het volledige dossier, en elke scan genereert een audit‑log voor compliance.

## Tips voor prestatie‑optimalisatie (java document security)

Wanneer je veel PDF’s ondertekent, is performance cruciaal. Hier enkele tips om alles soepel te laten verlopen:

### Batch‑verwerkingstrategie
In plaats van één document tegelijk te ondertekenen, verwerk ze in batches:

```java
for (String filePath : pdfList) {
    Signature batchSignature = new Signature(filePath);
    batchSignature.sign(outputPath, options);
    batchSignature.close();
}
```

**Waarom dit helpt:** Het hergebruiken van het opties‑object en het correct sluiten van bronnen voorkomt geheugenlekken.

### Geheugenbeheer voor grote PDF’s
Voor PDF’s groter dan 50 MB:
- Verwerk ze sequentieel in plaats van meerdere tegelijk te laden.  
- Gebruik try‑with‑resources om opruimen te garanderen.  
- Houd de heap‑grootte in de gaten en pas JVM‑parameters aan indien nodig: `-Xmx2g`.

### Veelgebruikte barcodes cachen
Als je veel documenten met dezelfde barcode ondertekent, cache dan de `BarcodeSignOptions`‑instantie:

```java
BarcodeSignOptions cachedOptions = new BarcodeSignOptions("STATIC_ID");
cachedOptions.setEncodeType(BarcodeEncodeType.Code128);
```

## Wanneer barcodehandtekeningen gebruiken (en wanneer niet)

**Ideale scenario’s:**
- Je hebt machine‑leesbare document‑identifiers nodig.  
- Documenten worden automatisch gescand of verwerkt.  
- Je wilt tamper‑evidente tracking zonder digitale certificaten.  
- Integratie met bestaande barcode‑infrastructuur is vereist.  

**Minder geschikt wanneer:**
- Je juridisch bindende digitale handtekeningen nodig hebt (gebruik digitale certificaten).  
- Documenten alleen door mensen worden bekeken (een eenvoudige tekst‑watermark volstaat).  
- Je werkt met extreem kleine documenten waarbij een barcode de pagina domineert.  
- Veiligheidseisen encryptie vereisen — barcodes zijn zichtbaar en door iedereen scanbaar.  

**Kun je benaderingen combineren?** Absoluut! Veel systemen gebruiken zowel barcodehandtekeningen voor tracking als digitale handtekeningen voor juridische geldigheid.

## Veelgestelde vragen

**V: Kan ik verschillende barcode‑types in dezelfde PDF gebruiken?**  
A: Ja! Roep `signature.sign()` meerdere keren aan met verschillende `BarcodeSignOptions` voor elk barcode‑type. Zorg er alleen voor dat ze elkaar niet overlappen.

**V: Hoe ga ik om met barcodes die speciale tekens bevatten?**  
A: Code128 ondersteunt de meeste ASCII‑tekens. Voor Unicode of complexe data, schakel over naar QR‑codes — die UTF‑8‑codering ondersteunen.

**V: Wat is de maximale hoeveelheid data die ik in een Code128‑barcode kan opslaan?**  
A: Technisch tot 128 tekens, maar de leesbaarheid neemt sterk af boven 30‑40 tekens. Voor grotere payloads gebruik je QR‑codes.

**V: Verhoogt het toevoegen van barcodes de PDF‑bestandsgrootte merkbaar?**  
A: Niet echt — barcodes zijn vectorafbeeldingen en voegen meestal slechts 5‑20 KB per barcode toe, afhankelijk van grootte en complexiteit.

**V: Kan ik barcodes roteren of verticaal plaatsen?**  
A: Ja! Gebruik `options.setRotationAngle(90)` om je barcode te draaien, handig voor plaatsing in de marge.

**V: Hoe laat ik barcodes op elke pagina van een meer‑pagina PDF verschijnen?**  
A: Loop door de pagina’s en pas de handtekening op elke pagina toe. Bekijk de `PagesSetup`‑klasse in de GroupDocs‑documentatie om te bepalen welke pagina’s ondertekend moeten worden.

**V: Wat als mijn barcode‑scanner de gegenereerde barcode niet kan lezen?**  
A: Controleer eerst of de scanner het gekozen barcode‑type ondersteunt. Vergroot vervolgens de barcode‑grootte — de meeste leesproblemen komen door te kleine strepen. Streef naar minimaal 1 inch (2,54 cm) breedte voor betrouwbare scans.

## Aanvullende bronnen

**Documentatie:**  
- [GroupDocs.Signature for Java Docs](https://docs.groupdocs.com/signature/java/)  
- [API Reference Guide](https://reference.groupdocs.com/signature/java/)  

**Downloads en licenties:**  
- [Download Latest Version](https://releases.groupdocs.com/signature/java/)  
- [Free Trial Access](https://releases.groupdocs.com/signature/java/)  
- [Get Temporary License](https://purchase.groupdocs.com/temporary-license/)  
- [Purchase Full License](https://purchase.groupdocs.com/buy)  

**Community en support:**  
- [Support Forum](https://forum.groupdocs.com/c/signature/) - Actieve community met GroupDocs‑engineers  

---

**Laatst bijgewerkt:** 2026-07-20  
**Getest met:** GroupDocs.Signature 23.12 (Java)  
**Auteur:** GroupDocs

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

## Gerelateerde tutorials

- [Java Barcode Signature Tutorial - Add, Verify & Manage Barcodes in PDFs](/signature/java/barcode-signatures/)
- [Create Barcode Signature in Java – Update PDF Barcodes](/signature/java/barcode-signatures/java-groupdocs-signature-barcode-initialize-update/)
- [How to read QR code PDF using Java and GroupDocs.Signature](/signature/java/barcode-signatures/java-pdf-barcode-search-groupdocs-signature-api/)