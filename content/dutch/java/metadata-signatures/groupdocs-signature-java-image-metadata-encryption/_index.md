---
"date": "2025-05-08"
"description": "Leer hoe u metadata van afbeeldingen kunt beveiligen met behulp van encryptie met GroupDocs.Signature voor Java. Garandeer de integriteit en authenticiteit van uw gegevens met stapsgewijze instructies."
"title": "Implementeer het ondertekenen en versleutelen van afbeeldingsmetagegevens in Java met GroupDocs.Signature"
"url": "/nl/java/metadata-signatures/groupdocs-signature-java-image-metadata-encryption/"
"weight": 1
type: docs
---
# Implementeer het ondertekenen van afbeeldingsmetagegevens met encryptie in Java met behulp van GroupDocs.Signature

## Invoering

In het huidige digitale landschap is het beveiligen van gevoelige informatie in documentmetadata van het grootste belang. Of het nu gaat om vertrouwelijke zakelijke contracten of persoonlijke identificatiefoto's, het behouden van de integriteit en authenticiteit van beeldmetadata helpt ongeautoriseerde toegang en manipulatie te voorkomen. **GroupDocs.Signature voor Java** biedt een robuuste oplossing voor het veilig ondertekenen en versleutelen van beeldmetadata.

Deze tutorial begeleidt je bij het implementeren van het ondertekenen van afbeeldingsmetadata met encryptie in Java met behulp van de krachtige functies van GroupDocs.Signature. Door deze stappen te volgen, integreer je deze functionaliteit effectief in je Java-applicaties.

**Wat je leert:**
- Documentmetagegevens ondertekenen met GroupDocs.Signature voor Java
- Implementatie van aangepaste objecthandtekeningen met encryptie
- Het opzetten van een veilige omgeving met behulp van symmetrische sleutelversleuteling

## Vereisten

Voordat u begint, moet u ervoor zorgen dat aan de volgende voorwaarden is voldaan:

### Vereiste bibliotheken en afhankelijkheden:
- **GroupDocs.Signature voor Java**: Zorg ervoor dat u versie 23.12 of hoger hebt.

### Vereisten voor omgevingsinstelling:
- Installeer Java Development Kit (JDK) op uw computer.
- Gebruik een Integrated Development Environment (IDE) zoals IntelliJ IDEA, Eclipse of NetBeans.

### Kennisvereisten:
- Basiskennis van Java-programmering.
- Kennis van Maven of Gradle voor afhankelijkheidsbeheer.

## GroupDocs.Signature instellen voor Java

Om GroupDocs.Signature in uw project te gebruiken, neemt u de volgende benodigde afhankelijkheden op:

### Maven gebruiken
Voeg dit toe aan je `pom.xml` bestand:
```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

### Gradle gebruiken
Neem dit op in uw `build.gradle` bestand:
```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

### Direct downloaden
U kunt ook de nieuwste versie downloaden van [GroupDocs.Signature voor Java-releases](https://releases.groupdocs.com/signature/java/).

#### Stappen voor het verkrijgen van een licentie
- **Gratis proefperiode**: Begin met een proefperiode om de functies te ontdekken.
- **Tijdelijke licentie**: Vraag indien nodig een uitgebreide test aan.
- **Aankoop**: Koop een licentie voor productiegebruik van [Groepsdocumenten](https://purchase.groupdocs.com/buy).

## Basisinitialisatie en -installatie

Hier ziet u hoe u GroupDocs.Signature in uw Java-toepassing kunt initialiseren:

```java
import com.groupdocs.signature.Signature;

public class InitializeSignature {
    public static void main(String[] args) {
        // Pad naar het document
        String filePath = "path/to/your/document.jpg";
        
        // Een nieuw exemplaar van Signature maken
        Signature signature = new Signature(filePath);

        System.out.println("GroupDocs.Signature initialized successfully.");
    }
}
```

## Implementatiegids

### Functie: Metadata-handtekening met aangepast object

#### Overzicht
Met deze functie kunt u metagegevens van afbeeldingen ondertekenen met een aangepast object en deze versleutelen voor extra beveiliging. Zo weet u zeker dat alleen geautoriseerde partijen toegang hebben tot de metagegevens en deze kunnen wijzigen.

#### Stapsgewijze implementatie

##### 1. Definieer uw documenthandtekeninggegevensklasse
Maak een klasse om uw metagegevens in op te slaan:

```java
import java.math.BigDecimal;
import java.util.Date;

class DocumentSignatureData {
    private String ID;
    private String Author;
    private Date Signed = new Date();
    private BigDecimal DataFactor = new BigDecimal(0.01);

    public String getID() { return ID; }
    public void setID(String value) { ID = value; }

    @FormatAttribute(propertyName = "SignID")
    public final String getAuthor() { return Author; }
    public final void setAuthor(String value) { Author = value; }

    @FormatAttribute(propertyName = "SAuth")
    public final Date getSigned() { return Signed; }
    public final void setSigned(Date value) { Signed = value; }

    @FormatAttribute(propertyName = "SDate", propertyFormat = "yyyy-MM-dd")
    public final BigDecimal getDataFactor() { return DataFactor; }
    public final void setDataFactor(BigDecimal value) { DataFactor = value; }
}
```

##### 2. Implementeer de handtekeninglogica
Hier leest u hoe u metagegevens kunt ondertekenen met behulp van encryptie:

```java
import com.groupdocs.signature.Signature;
import com.groupdocs.signature.domain.extensions.encryption.IDataEncryption;
import com.groupdocs.signature.domain.extensions.encryption.SymmetricAlgorithmType;
import com.groupdocs.signature.domain.extensions.encryption.SymmetricEncryption;
import com.groupdocs.signature.domain.signatures.metadata.ImageMetadataSignature;
import com.groupdocs.signature.exception.GroupDocsSignatureException;
import com.groupdocs.signature.options.sign.MetadataSignOptions;

import java.io.File;
import java.nio.file.Paths;
import java.util.UUID;

public class SignMetadataWithCustomObject {
    // Initialiseer bestandspaden met tijdelijke aanduidingen
    String filePath = "YOUR_DOCUMENT_DIRECTORY/SampleImage.jpg";
    String outputFilePath = new File("YOUR_OUTPUT_DIRECTORY", 
                                       "SignedImageWithCustomMetadata/SampleImage_signed.jpg").getPath();

    public void run() throws Exception {
        Signature signature = new Signature(filePath);

        // Stel sleutel en wachtwoordzin in voor encryptie
        String key = "1234567890";
        String salt = "1234567890";
        IDataEncryption encryption = new SymmetricEncryption(
            SymmetricAlgorithmType.Rijndael, key, salt);

        MetadataSignOptions options = new MetadataSignOptions();
        DocumentSignatureData documentSignature = new DocumentSignatureData();
        
        // Aangepaste metagegevenseigenschappen instellen
        documentSignature.setID(UUID.randomUUID().toString());
        documentSignature.setAuthor(System.getenv("USERNAME"));
        documentSignature.setSigned(new Date());
        documentSignature.setDataFactor(new BigDecimal("11.22"));

        ImageMetadataSignature mdDocument = new ImageMetadataSignature(41996, documentSignature);
        mdDocument.setDataEncryption(encryption);

        // Metadatahandtekeningen toevoegen aan opties
        options.getSignatures().add(mdDocument);

        signature.sign(outputFilePath, options);
    }
}
```

#### Belangrijkste configuratieopties
- **Symmetrische encryptie**: Maakt gebruik van het Rijndael-algoritme voor encryptie.
- **Metagegevens SignOptions**: Hiermee configureert u het ondertekeningsproces en geeft u op welke metagegevens u wilt ondertekenen.

##### Tips voor probleemoplossing
- Zorg ervoor dat de bestandspaden correct en toegankelijk zijn.
- Controleer of de omgevingsvariabele `USERNAME` is correct ingesteld.
- Controleer of de versie van de GroupDocs.Signature-bibliotheek overeenkomt met uw codeafhankelijkheden.

### Functie: Metadata-handtekening met encryptie

#### Overzicht
Deze functie richt zich op het versleutelen van metadatahandtekeningen om gevoelige informatie in afbeeldingsbestanden te beschermen.

#### Stapsgewijze implementatie
##### 1. Implementeer de encryptielogica
Hier leest u hoe u metagegevens kunt ondertekenen met behulp van encryptie:
```java
import com.groupdocs.signature.Signature;
import com.groupdocs.signature.domain.extensions.encryption.IDataEncryption;
import com.groupdocs.signature.domain.extensions.encryption.SymmetricAlgorithmType;
import com.groupdocs.signature.domain.extensions.encryption.SymmetricEncryption;
import com.groupdocs.signature.exception.GroupDocsSignatureException;
import com.groupdocs.signature.options.sign.MetadataSignOptions;

import java.io.File;
import java.nio.file.Paths;
import java.util.UUID;

public class SignMetadataWithEncryption {
    // Initialiseer bestandspaden met tijdelijke aanduidingen
    String filePath = "YOUR_DOCUMENT_DIRECTORY/SampleImage.jpg";
    String outputFilePath = new File("YOUR_OUTPUT_DIRECTORY", 
                                       "SignedImageWithEncryption/SampleImage_signed.jpg").getPath();

    public void run() throws Exception {
        Signature signature = new Signature(filePath);

        // Stel sleutel en wachtwoordzin in voor encryptie
        String key = "1234567890";
        String salt = "1234567890";
        IDataEncryption encryption = new SymmetricEncryption(
            SymmetricAlgorithmType.Rijndael, key, salt);

        MetadataSignOptions options = new MetadataSignOptions();
        DocumentSignatureData documentSignature = new DocumentSignatureData();
        
        // Aangepaste metagegevenseigenschappen instellen
        documentSignature.setID(UUID.randomUUID().toString());
        documentSignature.setAuthor(System.getenv("USERNAME"));
        documentSignature.setSigned(new Date());
        documentSignature.setDataFactor(new BigDecimal("11.22"));

        ImageMetadataSignature mdDocument = new ImageMetadataSignature(41996, documentSignature);
        mdDocument.setDataEncryption(encryption);

        // Metadatahandtekeningen toevoegen aan opties
        options.getSignatures().add(mdDocument);

        signature.sign(outputFilePath, options);
    }
}
```