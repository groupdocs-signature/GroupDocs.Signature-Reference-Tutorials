---
categories:
- Java Development
date: '2026-06-11'
description: Leer hoe je PDF ondertekent met Java met behulp van GroupDocs.Signature,
  voeg digital signature en timestamp toe. Stapsgewijze handleiding met codevoorbeelden
  en best practices.
keywords:
- how to sign pdf
- add digital signature pdf
- timestamp pdf signature
- java pdf signature library
- groupdocs signature java
lastmod: '2026-06-11'
linktitle: Digital Signature toevoegen aan PDF Java
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
title: 'Hoe PDF ondertekenen met Java: Digital Signature en Timestamp toevoegen'
type: docs
url: /nl/java/digital-signatures/digital-signature-timestamp-pdf-java-groupdocs/
weight: 1
---

# Hoe PDF te ondertekenen met Java en Tijdstempel

Heb je ooit een belangrijk document verzonden en je zorgen gemaakt of iemand het later zou kunnen wijzigen? Je bent niet alleen. Of je nu een enterprise document management systeem bouwt, een contractondertekeningsplatform creëert, of gewoon je PDF‑bestanden programmatisch moet beveiligen, **how to sign PDF** met een vertrouwde tijdstempel is het antwoord. Het toevoegen van een digitale handtekening bewijst niet alleen wie het bestand heeft ondertekend, maar creëert ook een onveranderlijk record van *exact* wanneer de ondertekening plaatsvond.

## Snelle Antwoorden
- **Welke bibliotheek vereenvoudigt PDF-ondertekening in Java?** GroupDocs.Signature for Java.  
- **Heb ik een internetverbinding nodig?** Alleen voor de tijdstempelautoriteit; de ondertekening zelf is offline.  
- **Kan ik een zelfondertekend certificaat gebruiken voor testen?** Ja, genereer er één met `keytool`.  
- **Is er een grootte‑limiet?** De bibliotheek kan PDF’s tot 500 MB ondertekenen zonder het hele bestand in het geheugen te laden.  
- **Hoeveel formaten ondersteunt GroupDocs?** Meer dan 50 invoer‑ en uitvoerformaten, waaronder DOCX, XLSX, PPTX, HTML en afbeeldingen.

## Waarom Digitale Handtekeningen Belangrijk Zijn (En Waarom Je Tijdstempels Nodig Hebt)

Laad je PDF, pas een cryptografische zegel toe en voeg een vertrouwde tijdstempel toe — dit twee‑stappenproces garandeert authenticatie, integriteit en niet‑ontkenning. De tijdstempel bewijst dat de handtekening op een specifiek moment bestond, zelfs als het ondertekeningscertificaat later verloopt of wordt ingetrokken.

## Hoe PDF te ondertekenen met Java?

Laad je PDF met `new Signature("input.pdf")`, configureer een `DigitalSignature`‑object, voeg een tijdstempel van een vertrouwde autoriteit toe, en roep `sign()` aan — de volledige bewerking wordt voltooid in een paar regels code. GroupDocs.Signature verwerkt automatisch certificaatparsing, hash‑berekening en tijdstempel‑ophaling, zodat je je kunt concentreren op de bedrijfslogica in plaats van cryptografie.

## GroupDocs.Signature voor Java Instellen

### Integratiemethoden

Kies de build‑tool die je gebruikt:

**Voor Maven‑gebruikers:**  
Add this dependency to your `pom.xml`:
```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

**Voor Gradle‑gebruikers:**  
Add this to your `build.gradle`:
```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

**Directe Download (Als Je Liever Wilt):**  
Ga naar [GroupDocs.Signature for Java releases](https://releases.groupdocs.com/signature/java/) en download het JAR‑bestand. Voeg het handmatig toe aan de classpath van je project. Zie de [GroupDocs.Signature Documentation](https://docs.groupdocs.com/signature/java/) voor een gedetailleerde API‑referentie. Voor de meest recente build, zie de [Latest Version & Releases](https://releases.groupdocs.com/signature/java/).

Pro tip: Gebruik Maven of Gradle indien mogelijk — het maakt afhankelijkheidsbeheer en updates veel eenvoudiger op de lange termijn.

### Je Licentie Regelen

GroupDocs biedt hier een paar opties, afhankelijk van waar je in je project staat:

1. **Free Trial** – Perfect voor evaluatie. [Download Trial Version](https://releases.groupdocs.com/signature/java/) and test drive all features.  
2. **Temporary License** – Volledige toegang nodig voor ontwikkeling zonder het trial‑watermerk? Verkrijg een tijdelijke licentie van 30 dagen.  
3. **Commercial License** – Voor productiegebruik, [Buy License](https://purchase.groupdocs.com/buy). De prijzen variëren afhankelijk van het type implementatie.

Hulp nodig? Bezoek het [GroupDocs Forum](https://forum.groupdocs.com/c/signature/).

### Basisinitialisatie

De `Signature`‑klasse is het top‑level object van GroupDocs.Signature dat een enkel PDF‑bestand in het geheugen vertegenwoordigt. Na instantiering verlopen alle lees‑ en schrijf‑operaties via dit object.

```java
import com.groupdocs.signature.Signature;

String filePath = "YOUR_DOCUMENT_DIRECTORY/sample.pdf";
final Signature signature = new Signature(filePath);
```

Eenvoudig, toch? Je wijst het simpelweg op je PDF‑bestand, en je bent klaar om te gaan. Het `Signature`‑object is je belangrijkste interface voor alle ondertekeningsoperaties.

## Hoe Digitale Handtekening Toevoegen aan PDF Java: Stap‑voor‑Stap

Laad je PDF, configureer handtekeningdetails, voeg een tijdstempel toe, en sla het ondertekende document op — alles in een duidelijke, lineaire stroom.

### Stap 1: Vereiste Klassen Importeren

De volgende imports geven je toegang tot handtekeningconfiguratie, positionering en tijdstempel‑functionaliteit.

```java
import com.groupdocs.signature.Signature;
import com.groupdocs.signature.domain.enums.HorizontalAlignment;
import com.groupdocs.signature.domain.enums.VerticalAlignment;
import com.groupdocs.signature.domain.signatures.PdfDigitalSignature;
import com.groupdocs.signature.domain.structs.TimeStamp;
import com.groupdocs.signature.options.sign.DigitalSignOptions;
```

### Stap 2: Definieer Je Bestandspaden

Stel paden in voor je invoer‑PDF, certificaat, en waar je de ondertekende PDF wilt opslaan. Houd het certificaatbestand veilig; het bevat je privésleutel.

```java
String filePath = "YOUR_DOCUMENT_DIRECTORY/sample.pdf";
String certificatePath = "YOUR_DOCUMENT_DIRECTORY/certificate.pfx";
String outputFilePath = "YOUR_OUTPUT_DIRECTORY/digitallySignedTimeStamp.pdf";
```

### Stap 3: Initialiseer het Signature‑Object

Maak een `Signature`‑instantie die naar de PDF wijst die je wilt ondertekenen. Dit laadt de PDF in het geheugen en maakt deze klaar voor ondertekening.

```java
final Signature signature = new Signature(filePath);
```

### Stap 4: Handtekeningeigenschappen en Tijdstempel Configureren

De `DigitalSignature`‑klasse vertegenwoordigt de cryptografische zegel die in de PDF wordt ingebed. Je kunt ook een tijdstempel van een vertrouwde autoriteit toevoegen.

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

We gebruiken FreeTSA (een gratis tijdstempel‑autoriteit) voor demonstratie. In productie kies je een commerciële TSA voor gegarandeerde uptime en juridische geldigheid.

### Stap 5: Digitale Handtekeningopties Configureren

De `SignOptions`‑klasse verbindt het certificaat, de handtekeningeigenschappen en de visuele plaatsing. Alignement‑enums bepalen waar de handtekening verschijnt.

```java
DigitalSignOptions options = new DigitalSignOptions(certificatePath);
options.setPassword("YourCertificatePassword"); // Certificate password
options.setSignature(pdfDigitalSignature); // Attach the PdfDigitalSignature object

// Specify signature alignment (where it appears on the page)
options.setVerticalAlignment(VerticalAlignment.Bottom);
options.setHorizontalAlignment(HorizontalAlignment.Right);
```

### Stap 6: Onderteken en Sla het Document Op

Voer het ondertekeningsproces uit en schrijf de ondertekende PDF naar schijf. Het geretourneerde `SignResult`‑object vertelt je of de bewerking geslaagd is en geeft eventuele waarschuwingen weer.

```java
try {
    SignResult signResult = signature.sign(outputFilePath, options);
    System.out.println("Document signed successfully!");
    System.out.println("Output: " + outputFilePath);
} catch (Exception e) {
    throw new RuntimeException("Error during signing process: " + e.getMessage());
}
```

## Veelvoorkomende Valkuilen om te Vermijden

### 1. Certificaatproblemen

**Problem:** “Invalid certificate” fouten.  
**Fix:** Verifieer het wachtwoord met `keytool -list -v -keystore your.pfx`.

```bash
keytool -list -v -keystore certificate.pfx -storetype PKCS12
```

### 2. Tijdstempelservice Time‑outs

**Problem:** Netwerktime‑outs bij het contacteren van de TSA.  
**Fix:** Test de connectiviteit (`curl -I https://freetsa.org/tsr`), voeg retry‑logica toe, of configureer een fallback‑TSA.

```java
new File(outputFilePath).getParentFile().mkdirs();
```

### 3. Bestandsmachtigingsproblemen

**Problem:** “Access denied” tijdens het opslaan.  
**Fix:** Zorg ervoor dat de uitvoermap bestaat en de applicatie schrijfrechten heeft.

```bash
keytool -genkeypair -alias mykey -keyalg RSA -keysize 2048 -storetype PKCS12 -keystore certificate.pfx -validity 365
```

### 4. Geheugenproblemen met Grote PDF’s

**Problem:** `OutOfMemoryError` voor grote bestanden.  
**Fix:** Verhoog de JVM‑heap (`-Xmx4g`) of verwerk bestanden in batches.

### 5. Verkeerde Handtekeningplaatsing

**Problem:** Handtekening overlapt bestaande inhoud.  
**Fix:** Test eerst de uitlijningsinstellingen; voor pixel‑perfecte plaatsing, gebruik coördinaat‑gebaseerde opties.

## Tips voor Certificaatbeheer

### Een Certificaat Krijgen voor Ontwikkeling

Genereer een zelfondertekend certificaat met Java’s `keytool` voor testdoeleinden.

```java
   String certPassword = System.getenv("CERT_PASSWORD");
   ```

### Beste Praktijken voor Certificaten

1. **Never hard‑code passwords** – gebruik omgevingsvariabelen.  
2. **Rotate certificates** vóór ze verlopen.  
3. **Store private keys** in veilige hardware (HSM) voor high‑security apps.  
4. **Back up certificates** op een beveiligde locatie.  
5. **Validate certificates** vóór ondertekening om verlopen of ingetrokken certificaten te detecteren.

## Beveiligingsbeste Praktijken

### 1. Bescherm Privésleutels

Bewaar certificaten buiten de projectmap, gebruik omgeving‑specifieke configuraties, en overweeg HSM’s voor enterprise‑implementaties.

### 2. Valideer Invoer‑PDF’s

Controleer op corruptie, bestaande handtekeningen, grootte‑limieten en inhouds‑conformiteit vóór ondertekening.

### 3. Implementeer Audit‑Logging

Log elke ondertekeningsoperatie met tijdstempel, gebruiker, documentnaam en status.

```java
try {
    SignResult result = signature.sign(outputFilePath, options);
    logger.info("Document signed: " + filePath + " by " + signerEmail);
} catch (Exception e) {
    logger.error("Signing failed: " + filePath + " - " + e.getMessage());
    // Handle appropriately
}
```

### 4. Gebruik Vertrouwde Tijdstempelautoriteiten

Vertrouw nooit op de lokale systeemtijd; vraag altijd een tijdstempel aan bij een RFC 3161‑compliant TSA.

### 5. Implementeer Foutafhandeling

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

## Praktijkvoorbeelden en Toepassingen

### 1. Contractmanagementsystemen

Werknemers ondertekenen NDA’s en overeenkomsten elektronisch; tijdstempels bewijzen exact wanneer elk contract is geaccepteerd.

### 2. Financiële Documentverwerking

Batch‑onderteken facturen en inkooporders, waardoor een onveranderlijk audit‑pad voor toezichthouders ontstaat.

### 3. Verificatie van Onderwijscredentialen

Universiteiten geven manipulatie‑veilige transcripties uit die direct gevalideerd kunnen worden via een QR‑code‑link.

### 4. Softwarelicentiebeheer

Genereer licentiecertificaten met een digitale handtekening en tijdstempel om vervalsing te voorkomen.

### 5. Regelgevende Naleving (FDA 21 CFR Part 11, enz.)

Medische apparaatbedrijven ondertekenen SOP’s en validatierapporten; tijdstempels voldoen aan de eisen voor niet‑ontkenning.

## Prestatieoverwegingen en Optimalisatie

### Geheugenbeheer

Verwerk grote PDF’s in batches, sluit `Signature`‑objecten tijdig, en vergroot de heap‑grootte indien nodig.

### Netwerkoptimalisatie voor Tijdstempels

Pool HTTP‑verbindingen, implementeer exponentiële backoff‑retries, en cache tijdstempels voor snelle opeenvolgende ondertekeningen.

### Batchverwerking Beste Praktijken

```java
// Pseudo‑code: process a list of PDFs in parallel, limiting to 5 concurrent TSA calls
```
*Vermijd het starten van te veel threads; 5‑10 gelijktijdige ondertekeningen balanceren doorvoer en TSA‑belasting.*

### Schijf‑I/O‑optimalisatie

Gebruik SSD’s voor tijdelijke bestanden, minimaliseer lees‑/schrijfcycli, en ruim tijdelijke artefacten op na elke ondertekeningsrun.

## Probleemoplossingsgids

### Fout: “Invalid Certificate Password”

**Solution:** Verifieer het wachtwoord met `keytool -list -keystore your.pfx`.

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

### Fout: “Timestamp Authority Not Responding”

**Solution:** Test de TSA‑URL, controleer firewall‑regels, en voeg fallback‑TSA‑logica toe.

```bash
keytool -list -v -keystore certificate.pfx -storetype PKCS12
```

### Fout: “PDF is Already Signed”

**Solution:** Detecteer eerst bestaande handtekeningen; voeg een tegenhandtekening toe of onderteken een verse kopie.

### Fout: “Access Denied” Bij Opslaan

**Solution:** Zorg dat de uitvoermap bestaat, de app schrijfrechten heeft, en geen ander proces het bestand vergrendelt.

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

**Solution:** Verhoog de JVM‑heap, verwerk PDF’s in kleinere batches, of schakel over naar streaming‑API’s voor zeer grote bestanden.

## Conclusie en Volgende Stappen

Je hebt geleerd **how to sign PDF** bestanden met Java, een vertrouwde tijdstempel toe te voegen, en veelvoorkomende valkuilen te behandelen. Volgende, verken:

1. Meerdere handtekeningvelden toevoegen voor multi‑party overeenkomsten.  
2. Handtekeningen programmatisch verifiëren met GroupDocs.Signature.  
3. Handtekeningweergave aanpassen (afbeeldingen, tekst, positionering).  
4. Een robuuste batch‑ondertekeningsservice bouwen met wachtrijen en monitoring.

## Veelgestelde Vragen

**Q: Wat is het verschil tussen een digitale handtekening en een elektronische handtekening?**  
A: Een digitale handtekening gebruikt cryptografische algoritmen om identiteit te verifiëren en manipulatie te detecteren, terwijl een elektronische handtekening zo simpel kan zijn als een getypte naam.

**Q: Heb ik internetconnectiviteit nodig om PDF’s te ondertekenen?**  
A: Alleen voor de tijdstempelservice; de cryptografische ondertekening zelf draait lokaal.

**Q: Kunnen ondertekende PDF’s later worden bewerkt?**  
A: Elke wijziging breekt de handtekening, en PDF‑viewers tonen een waarschuwing dat het document is aangepast.

**Q: Hoe verifieer ik een ondertekende PDF?**  
A: De meeste PDF‑readers verifiëren automatisch; programmatisch kun je de verificatie‑API van GroupDocs.Signature gebruiken om status, ondertekenaargegevens en tijdstempelgeldigheid te controleren.

**Q: Wat gebeurt er als mijn certificaat verloopt nadat ik documenten heb ondertekend?**  
A: De ingebedde tijdstempel bewijst dat de handtekening is gemaakt terwijl het certificaat nog geldig was, waardoor de juridische status behouden blijft.

**Q: Kan ik dit gebruiken met cloudopslag (S3, Azure Blob, enz.)?**  
A: Ja — download de PDF naar een tijdelijke locatie, onderteken deze, en upload vervolgens de ondertekende versie terug naar de cloud.

**Q: Zijn er limieten voor de bestandsgrootte?**  
A: De bibliotheek verwerkt PDF’s tot 500 MB zonder het hele bestand in het geheugen te laden; grotere bestanden kunnen streaming vereisen.

**Q: Hoeveel kost GroupDocs.Signature voor commercieel gebruik?**  
A: De prijzen variëren per implementatietype; neem contact op met de verkoop van GroupDocs voor de laatste tarieven. Gratis proefversies en tijdelijke licenties zijn beschikbaar voor evaluatie.

**Q: Werkt dit op Linux‑servers?**  
A: Absoluut. GroupDocs.Signature voor Java is platform‑onafhankelijk en draait op elk OS met een JRE.

**Laatst Bijgewerkt:** 2026-06-11  
**Getest Met:** GroupDocs.Signature 23.9 for Java  
**Auteur:** GroupDocs

```java
File outputFile = new File(outputFilePath);
outputFile.getParentFile().mkdirs(); // Create directories if needed

if (!outputFile.canWrite() && outputFile.exists()) {
    throw new IOException("Cannot write to " + outputFilePath);
}
```

## Gerelateerde Tutorials

- [Hoe Digitale Certificaten in Java te Verifiëren - Complete Gids met Codevoorbeelden](/signature/java/digital-signatures/java-certificate-verification-groupdocs-signature/)
- [Hoe PDF Programmatically in Java te Ondertekenen met GroupDocs.Signature](/signature/java/digital-signatures/sign-pdfs-groupdocs-signature-java/)
- [Afbeelding Handtekening Toevoegen aan PDF Java met GroupDocs](/signature/java/image-signatures/sign-pdf-image-signature-groupdocs-java/)