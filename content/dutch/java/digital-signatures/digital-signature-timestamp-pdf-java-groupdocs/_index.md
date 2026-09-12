---
date: '2026-09-05'
description: Leer hoe u PDF kunt ondertekenen met Java met behulp van GroupDocs.Signature,
  een digital signature en timestamp kunt toevoegen. Stapsgewijze handleiding met
  code‑voorbeelden en best practices.
keywords:
- how to sign pdf
- add digital signature pdf
- digital signature pdf java
- sign pdf java
- groupdocs signature java
lastmod: '2026-09-05'
linktitle: Digital signature toevoegen aan PDF met Java
og_description: Leer hoe u PDF kunt ondertekenen met Java met behulp van GroupDocs.Signature,
  een digital signature en een vertrouwde timestamp kunt toevoegen in een paar regels
  code. Volg stapsgewijze instructies, best practices en tips voor probleemoplossing.
og_image_alt: Guide showing Java code to add digital signature and timestamp to PDF
  with GroupDocs.Signature
og_title: Hoe PDF te ondertekenen met Java met GroupDocs.Signature
schemas:
- author: GroupDocs
  dateModified: '2026-09-05'
  description: Learn how to sign PDF with Java using GroupDocs.Signature, add digital
    signature and timestamp. Step-by-step guide with code examples and best practices.
  headline: How to sign PDF with Java and timestamp
  type: TechArticle
- description: Learn how to sign PDF with Java using GroupDocs.Signature, add digital
    signature and timestamp. Step-by-step guide with code examples and best practices.
  name: How to sign PDF with Java and timestamp
  steps:
  - name: import required classes
    text: The following imports give you access to signature configuration, positioning,
      and timestamp functionality.
  - name: define your file paths
    text: Set up paths for the input PDF, the certificate (PFX), and the output location.
      Keep the certificate file secure; it contains your private key.
  - name: initialize the Signature object
    text: '`Signature` is the entry point for all signing actions. Creating it loads
      the PDF into memory and prepares the API for further operations.'
  - name: configure signature properties and timestamp
    text: '`DigitalSignature` is the cryptographic seal that will be embedded in the
      PDF. You can also attach a timestamp from a trusted authority. * **ContactInfo**
      – e.g., `john.doe@company.com` * **Location** – e.g., `New York Office` * **Reason**
      – e.g., `Contract Approval` We use FreeTSA (a free timestamp'
  - name: configure digital sign options
    text: '`SignOptions` aggregates the certificate, visual appearance, and placement
      settings for the digital signature.'
  - name: sign and save the document
    text: '`SignResult` provides the outcome of the signing operation, including success
      status and any warnings.'
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
- pdf signing
- digital signatures
- java security
- groupdocs
- java pdf signature
title: Hoe PDF te ondertekenen met Java en timestamp
---

# Hoe PDF te ondertekenen met Java en tijdstempel

Wanneer u een contract, factuur of een ander kritisch document moet beschermen tegen manipulatie, wordt **hoe PDF te ondertekenen** op een veilige manier een topprioriteit. In deze gids ontdekt u hoe u een digitale handtekening en een vertrouwde tijdstempel aan een PDF kunt toevoegen met GroupDocs.Signature voor Java. De aanpak werkt offline, schaalt tot bestanden van 500 MB en vereist slechts een paar regels code.

## Snelle antwoorden
- **Welke bibliotheek vereenvoudigt het ondertekenen van PDF in Java?** GroupDocs.Signature for Java.  
- **Heb ik een internetverbinding nodig?** Alleen voor de tijdstempelautoriteit; het cryptografische ondertekenen gebeurt lokaal.  
- **Kan ik een zelfondertekend certificaat gebruiken voor testen?** Ja, genereer er één met `keytool`.  
- **Is er een grootte‑limiet?** De bibliotheek kan PDF‑s bestanden tot 500 MB ondertekenen zonder het hele bestand in het geheugen te laden.  
- **Hoeveel formaten ondersteunt GroupDocs?** Meer dan 50 invoer‑ en uitvoerformaten, waaronder DOCX, XLSX, PPTX, HTML en afbeeldingen.

## Hoe PDF te ondertekenen met Java?

Laad de PDF, configureer een `DigitalSignature` met uw certificaat, voeg eventueel een tijdstempel toe van een RFC 3161‑conforme TSA, en roep `sign()` aan. Het `Signature`‑object schrijft het ondertekende bestand naar schijf en retourneert een `SignResult` die aangeeft of de bewerking geslaagd is en eventuele waarschuwingen vermeldt. Deze end‑to‑end workflow vereist slechts een paar regels Java‑code en handelt hashing, certificaatvalidatie en tijdstempel‑ophaling automatisch af.

## Waarom digitale handtekeningen belangrijk zijn (en waarom u tijdstempels nodig heeft)

Een digitale handtekening garandeert **authenticiteit** (wie heeft ondertekend) en **integriteit** (het document is niet gewijzigd). Het toevoegen van een tijdstempel bewijst dat de handtekening op een specifiek moment bestond, waardoor u beschermd bent zelfs als het ondertekeningscertificaat later verloopt of wordt ingetrokken. Samen bieden ze non‑repudiatie — cruciaal voor juridische, financiële en regelgevende werkstromen.

## GroupDocs.Signature voor Java instellen

### Integratiemethoden

Kies de build‑tool die u prefereert:

**Voor Maven‑gebruikers**  
Voeg de afhankelijkheid toe aan uw `pom.xml`:

De volgende Maven‑coördinaten halen de nieuwste stabiele release van GroupDocs.Signature voor Java.

```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

**Voor Gradle‑gebruikers**  
Voeg de regel toe aan uw `build.gradle`:

Gradle zal de bibliotheek ophalen van Maven Central.

```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

**Direct downloaden (als u dat prefereert)**  
Ga naar [GroupDocs.Signature for Java releases](https://releases.groupdocs.com/signature/java/) en download het JAR‑bestand. Voeg het handmatig toe aan de classpath van uw project. Zie de [GroupDocs.Signature Documentation](https://docs.groupdocs.com/signature/java/) voor een volledige API‑referentie. Voor de meest recente build, zie de [Latest Version & Releases](https://releases.groupdocs.com/signature/java/).

*Pro tip:* Maven of Gradle automatiseert versie‑upgrades en transitieve afhankelijkheden, waardoor u tijd bespaart wanneer nieuwe beveiligingspatches worden uitgebracht.

### Uw licentie regelen

GroupDocs biedt drie licentie‑opties:

1. **Gratis proefversie** – evalueer alle functies zonder watermerk. [Download Trial Version](https://releases.groupdocs.com/signature/java/)  
2. **Tijdelijke licentie** – 30‑daagse volledige toegangssleutel voor ontwikkeling.  
3. **Commerciële licentie** – productie‑klaar, onbeperkt gebruik. [Buy License](https://purchase.groupdocs.com/buy)

Als u vragen heeft, is de community actief op het [GroupDocs Forum](https://forum.groupdocs.com/c/signature/).

### Basisinitialisatie

`Signature` is het top‑level object van GroupDocs.Signature dat een enkel PDF‑bestand in het geheugen vertegenwoordigt. Nadat u een instantie maakt, verlopen alle lees‑/schrijf‑bewerkingen via dit object.

```java
import com.groupdocs.signature.Signature;

String filePath = "YOUR_DOCUMENT_DIRECTORY/sample.pdf";
final Signature signature = new Signature(filePath);
```

## Hoe digitale handtekening toe te voegen aan PDF Java: stap‑voor‑stap

Het proces is lineair: importeer klassen, stel bestands‑paden in, maak een `Signature`‑object, configureer een `DigitalSignature` met optionele tijdstempel, definieer `SignOptions`, en onderteken en sla vervolgens op.

### Stap 1: vereiste klassen importeren

De volgende imports geven u toegang tot handtekeningconfiguratie, positionering en tijdstempel‑functionaliteit.

```java
import com.groupdocs.signature.Signature;
import com.groupdocs.signature.domain.enums.HorizontalAlignment;
import com.groupdocs.signature.domain.enums.VerticalAlignment;
import com.groupdocs.signature.domain.signatures.PdfDigitalSignature;
import com.groupdocs.signature.domain.structs.TimeStamp;
import com.groupdocs.signature.options.sign.DigitalSignOptions;
```

### Stap 2: definieer uw bestands‑paden

Stel paden in voor de invoer‑PDF, het certificaat (PFX) en de uitvoerlocatie. Houd het certificaatbestand veilig; het bevat uw privésleutel.

```java
String filePath = "YOUR_DOCUMENT_DIRECTORY/sample.pdf";
String certificatePath = "YOUR_DOCUMENT_DIRECTORY/certificate.pfx";
String outputFilePath = "YOUR_OUTPUT_DIRECTORY/digitallySignedTimeStamp.pdf";
```

### Stap 3: initialiseert het Signature‑object

`Signature` is het toegangspunt voor alle ondertekeningsacties. Het aanmaken laadt de PDF in het geheugen en bereidt de API voor verdere bewerkingen voor.

```java
final Signature signature = new Signature(filePath);
```

### Stap 4: configureer handtekening‑eigenschappen en tijdstempel

`DigitalSignature` is het cryptografische zegel dat in de PDF wordt ingebed. U kunt ook een tijdstempel van een vertrouwde autoriteit toevoegen.

```java
PdfDigitalSignature pdfDigitalSignature = new PdfDigitalSignature();
pdfDigitalSignature.setContactInfo("Contact Information");
pdfDigitalSignature.setLocation("Location Info");
pdfDigitalSignature.setReason("Signing Reason");

// Configure the TimeStamp with URL, User Id, and Password
TimeStamp timeStamp = new TimeStamp("https://freetsa.org/tsr", "User Id", "Password");
pdfDigitalSignature.setTimeStamp(timeStamp);
```

* **ContactInfo** – bijv. `john.doe@company.com`  
* **Location** – bijv. `New York Office`  
* **Reason** – bijv. `Contract Approval`  

We gebruiken FreeTSA (een gratis tijdstempel‑autoriteit) voor demonstratie. In productie kiest u een commerciële TSA voor gegarandeerde uptime en juridische status.

### Stap 5: configureer digitale ondertekeningsopties

`SignOptions` bundelt het certificaat, de visuele weergave en de plaatsingsinstellingen voor de digitale handtekening.

```java
DigitalSignOptions options = new DigitalSignOptions(certificatePath);
options.setPassword("YourCertificatePassword"); // Certificate password
options.setSignature(pdfDigitalSignature); // Attach the PdfDigitalSignature object

// Specify signature alignment (where it appears on the page)
options.setVerticalAlignment(VerticalAlignment.Bottom);
options.setHorizontalAlignment(HorizontalAlignment.Right);
```

### Stap 6: onderteken en sla het document op

`SignResult` geeft het resultaat van de ondertekeningsbewerking, inclusief successtatus en eventuele waarschuwingen.

```java
try {
    SignResult signResult = signature.sign(outputFilePath, options);
    System.out.println("Document signed successfully!");
    System.out.println("Output: " + outputFilePath);
} catch (Exception e) {
    throw new RuntimeException("Error during signing process: " + e.getMessage());
}
```

## Veelvoorkomende valkuilen om te vermijden

### 1. certificaatproblemen
**Probleem:** “Invalid certificate” fouten.  
**Oplossing:** Controleer het wachtwoord met `keytool -list -v -keystore your.pfx`.

```bash
keytool -list -v -keystore certificate.pfx -storetype PKCS12
```

### 2. tijdstempelservice‑time‑outs
**Probleem:** Netwerk‑time‑outs bij het benaderen van de TSA.  
**Oplossing:** Test de connectiviteit (`curl -I https://freetsa.org/tsr`), voeg retry‑logica toe, of configureer een fallback‑TSA.

```java
new File(outputFilePath).getParentFile().mkdirs();
```

### 3. bestands‑toegangsproblemen
**Probleem:** “Access denied” bij het opslaan.  
**Oplossing:** Zorg ervoor dat de uitvoermap bestaat en dat de applicatie schrijfrechten heeft.

```bash
keytool -genkeypair -alias mykey -keyalg RSA -keysize 2048 -storetype PKCS12 -keystore certificate.pfx -validity 365
```

### 4. geheugenproblemen met grote PDF‑s
**Probleem:** `OutOfMemoryError` voor grote bestanden.  
**Oplossing:** Verhoog de JVM‑heap (`-Xmx4g`) of verwerk bestanden in batches.

### 5. verkeerde handtekeningplaatsing
**Probleem:** Handtekening overlapt bestaande inhoud.  
**Oplossing:** Test eerst de uitlijningsinstellingen; voor pixel‑perfecte plaatsing, gebruik coördinaat‑gebaseerde opties.

## Tips voor certificaatbeheer

### Een certificaat verkrijgen voor ontwikkeling
Genereer een zelfondertekend certificaat met Java’s `keytool` voor testdoeleinden.

```java
   String certPassword = System.getenv("CERT_PASSWORD");
   ```

### Beste praktijken voor certificaten
1. **Nooit wachtwoorden hard‑coderen** – gebruik omgevingsvariabelen.  
2. **Roteer certificaten** voordat ze verlopen.  
3. **Bewaar privésleutels** in veilige hardware (HSM) voor high‑security applicaties.  
4. **Maak back‑ups van certificaten** op een beveiligde locatie.  
5. **Valideer certificaten** vóór het ondertekenen om verlopen of ingetrokken certificaten te detecteren.

## Beveiligings‑beste praktijken

### 1. bescherm privésleutels
Bewaar certificaten buiten de projectdirectory, gebruik omgevingsspecifieke configuraties, en overweeg HSM‑s voor enterprise‑implementaties.

### 2. valideer invoer‑PDF‑s
Controleer op corruptie, bestaande handtekeningen, grootte‑limieten en inhouds‑compliance vóór het ondertekenen.

### 3. implementeer audit‑logging
Log elke ondertekeningsactie met tijdstempel, gebruiker, documentnaam en status.

```java
try {
    SignResult result = signature.sign(outputFilePath, options);
    logger.info("Document signed: " + filePath + " by " + signerEmail);
} catch (Exception e) {
    logger.error("Signing failed: " + filePath + " - " + e.getMessage());
    // Handle appropriately
}
```

### 4. gebruik vertrouwde tijdstempel‑autoriteiten
Vertrouw nooit op de lokale systeemtijd; vraag altijd een tijdstempel aan bij een RFC 3161‑conforme TSA.

### 5. implementeer foutafhandeling
Vang uitzonderingen op zonder gevoelige details bloot te stellen.

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

## Praktijkvoorbeelden en toepassingen

1. **Contractbeheersystemen** – medewerkers ondertekenen NDA’s en overeenkomsten elektronisch; tijdstempels bewijzen precies wanneer elk contract is geaccepteerd.  
2. **Financiële documentverwerking** – batch‑onderteken facturen en inkooporders, waardoor een onveranderlijk audit‑pad voor toezichthouders ontstaat.  
3. **Onderwijs‑credential verificatie** – universiteiten geven manipulatie‑veilige transcripties uit die direct gevalideerd kunnen worden via een QR‑code link.  
4. **Software‑licentiebeheer** – genereer licentiecertificaten met een digitale handtekening en tijdstempel om vervalsing te voorkomen.  
5. **Regelgevende compliance (FDA 21 CFR Part 11, etc.)** – medische apparaatbedrijven ondertekenen SOP’s en validatierapporten; tijdstempels voldoen aan non‑repudiatie‑eisen.

## Prestatie‑overwegingen en optimalisatie

### Geheugenbeheer
Verwerk grote PDF‑s in batches, sluit `Signature`‑objecten snel, en vergroot de heap‑grootte wanneer nodig.

### Netwerkoptimalisatie voor tijdstempels
Pool HTTP‑verbindingen, implementeer exponentiële backoff‑retries, en cache tijdstempels voor snelle opeenvolgende ondertekeningen.

### Beste praktijken voor batch‑verwerking
```java
// Pseudo‑code: process a list of PDFs in parallel, limiting to 5 concurrent TSA calls
```  
*Vermijd het spawnen van te veel threads; 5‑10 gelijktijdige ondertekeningen balanceren doorvoersnelheid en TSA‑belasting.*

### Schijf‑I/O optimalisatie
Gebruik SSD‑s voor tijdelijke bestanden, minimaliseer lees‑/schrijfcycli, en maak tijdelijke artefacten schoon na elke ondertekeningsrun.

## Probleemoplossingsgids

### Fout: “Invalid certificate password”
**Oplossing:** Controleer het wachtwoord met `keytool -list -keystore your.pfx`.

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

### Fout: “Timestamp authority not responding”
**Oplossing:** Test de TSA‑URL, controleer firewall‑regels, en voeg fallback‑TSA‑logica toe.

```bash
keytool -list -v -keystore certificate.pfx -storetype PKCS12
```

### Fout: “PDF is already signed”
**Oplossing:** Detecteer eerst bestaande handtekeningen; voeg een tegen‑handtekening toe of onderteken een verse kopie.

### Fout: “Access denied” bij het opslaan
**Oplossing:** Zorg dat de uitvoermap bestaat, de app schrijfrechten heeft, en dat geen ander proces het bestand vergrendelt.

```java
TimeStamp timeStamp;
try {
    timeStamp = new TimeStamp("https://freetsa.org/tsr", "", "");
} catch (Exception e) {
    // Fallback to alternative TSA
    timeStamp = new TimeStamp("https://alternate-tsa.com/tsr", "", "");
}
```

### Fout: OutOfMemoryError
**Oplossing:** Verhoog de JVM‑heap, verwerk PDF‑s in kleinere batches, of schakel over op streaming‑API‑s voor zeer grote bestanden.

## Conclusie en volgende stappen

U weet nu **hoe PDF‑s te ondertekenen** met Java, een vertrouwde tijdstempel toe te voegen, en veelvoorkomende valkuilen te vermijden. Vervolgens kunt u:

1. Meerdere handtekeningvelden toevoegen voor multi‑partij overeenkomsten.  
2. Handtekeningen programmatisch verifiëren met GroupDocs.Signature.  
3. Het visuele uiterlijk van handtekeningen aanpassen (afbeeldingen, tekst, positionering).  
4. Een robuuste batch‑ondertekeningsservice bouwen met queueing en monitoring.

## Veelgestelde vragen

**Q: Wat is het verschil tussen een digitale handtekening en een elektronische handtekening?**  
A: Een digitale handtekening gebruikt cryptografische algoritmen om identiteit te verifiëren en manipulatie te detecteren, terwijl een elektronische handtekening zo simpel kan zijn als een getypte naam.

**Q: Heb ik internetconnectiviteit nodig om PDF‑s te ondertekenen?**  
A: Alleen voor de tijdstempelservice; het cryptografisch ondertekenen zelf gebeurt lokaal.

**Q: Kunnen ondertekende PDF‑s later bewerkt worden?**  
A: Elke wijziging breekt de handtekening, en PDF‑viewers tonen een waarschuwing dat het document is aangepast.

**Q: Hoe verifieer ik een ondertekende PDF?**  
A: De meeste PDF‑readers verifiëren automatisch; programmatisch kunt u de verificatie‑API van GroupDocs.Signature gebruiken om status, ondertekenaar‑details en tijdstempel‑geldigheid te controleren.

**Q: Wat gebeurt er als mijn certificaat verloopt nadat ik documenten heb ondertekend?**  
A: De ingebedde tijdstempel bewijst dat de handtekening is gemaakt terwijl het certificaat nog geldig was, waardoor de juridische status behouden blijft.

**Q: Kan ik dit gebruiken met cloudopslag (S3, Azure Blob, enz.)?**  
A: Ja—download de PDF naar een tijdelijke locatie, onderteken deze, en upload vervolgens de ondertekende versie terug naar de cloud.

**Q: Zijn er limieten voor bestandsgrootte?**  
A: De bibliotheek verwerkt PDF‑s tot 500 MB zonder het volledige bestand in het geheugen te laden; grotere bestanden kunnen streaming vereisen.

**Q: Hoeveel kost GroupDocs.Signature voor commercieel gebruik?**  
A: De prijs varieert per implementatietype; neem contact op met de salesafdeling van GroupDocs voor de laatste tarieven. Gratis proefversies en tijdelijke licenties zijn beschikbaar voor evaluatie.

**Q: Werkt dit op Linux‑servers?**  
A: Absoluut. GroupDocs.Signature voor Java is platform‑onafhankelijk en draait op elk OS met een JRE.

**Laatst bijgewerkt:** 2026-09-05  
**Getest met:** GroupDocs.Signature 23.9 for Java  
**Auteur:** GroupDocs

## Gerelateerde tutorials

- [Hoe digitale certificaten te verifiëren in Java - Complete gids met code‑voorbeelden](/signature/java/digital-signatures/java-certificate-verification-groupdocs-signature/)
- [Hoe PDF programmatisch te ondertekenen in Java met GroupDocs.Signature](/signature/java/digital-signatures/sign-pdfs-groupdocs-signature-java/)
- [Afbeeldingshandtekening toevoegen aan PDF Java met GroupDocs](/signature/java/image-signatures/sign-pdf-image-signature-groupdocs-java/)

```java
File outputFile = new File(outputFilePath);
outputFile.getParentFile().mkdirs(); // Create directories if needed

if (!outputFile.canWrite() && outputFile.exists()) {
    throw new IOException("Cannot write to " + outputFilePath);
}
```