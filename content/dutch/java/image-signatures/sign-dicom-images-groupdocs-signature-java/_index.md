---
"date": "2025-05-08"
"description": "Leer hoe u DICOM-afbeeldingen veilig kunt ondertekenen met GroupDocs.Signature voor Java. Verbeter de beveiliging van uw documenten door QR-codes en metadata in te sluiten."
"title": "Onderteken DICOM-afbeeldingen met QR-codes en metagegevens met GroupDocs.Signature voor Java"
"url": "/nl/java/image-signatures/sign-dicom-images-groupdocs-signature-java/"
"weight": 1
type: docs
---
# DICOM-afbeeldingen ondertekenen met QR-codes en metagegevens met GroupDocs.Signature voor Java

## Invoering

In het snel veranderende digitale zorglandschap is het veilig beheren van patiëntgegevens van cruciaal belang. Deze tutorial begeleidt u bij de implementatie van een robuuste oplossing met GroupDocs.Signature voor Java om DICOM-beelden (Digital Imaging and Communications in Medicine) te ondertekenen met QR-codes en metadata. Deze functies garanderen authenticiteit, verbeteren de traceerbaarheid en zorgen voor naleving door essentiële informatie rechtstreeks in medische beelden te integreren.

### Wat je leert:
- Hoe u GroupDocs.Signature voor Java in uw project integreert.
- Het proces van het ondertekenen van DICOM-afbeeldingen met QR-codes.
- XMP-metagegevens toevoegen om de beveiliging van documenten te verbeteren.
- Ophalen, verifiëren en zoeken naar handtekeningen in DICOM-bestanden.
- Previews van ondertekende DICOM-afbeeldingen genereren.

Laten we beginnen! Voordat we beginnen, zorgen we ervoor dat je alles hebt wat je nodig hebt om de cursus soepel te kunnen volgen.

## Vereisten

Om de functies van GroupDocs.Signature effectief te implementeren, moet u aan de volgende vereisten voldoen:

### Vereiste bibliotheken en afhankelijkheden
- **GroupDocs.Signature voor Java**: U hebt versie 23.12 of hoger van deze bibliotheek nodig.

### Vereisten voor omgevingsinstellingen
- **Java-ontwikkelingskit (JDK)**: Zorg ervoor dat JDK op uw systeem is geïnstalleerd.
- **IDE**: Gebruik een geïntegreerde ontwikkelomgeving zoals IntelliJ IDEA of Eclipse.

### Kennisvereisten
Basiskennis van:
- Java-programmering en objectgeoriënteerde principes.
- Maven- of Gradle-buildtools voor afhankelijkheidsbeheer.

## GroupDocs.Signature instellen voor Java

Om aan de slag te gaan met GroupDocs.Signature, moet je het als afhankelijkheid aan je project toevoegen. Zo doe je dat met verschillende buildtools:

### Maven
Voeg het volgende fragment toe aan uw `pom.xml` bestand:
```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

### Gradle
Neem dit op in uw `build.gradle` bestand:
```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

### Direct downloaden
U kunt de nieuwste versie ook downloaden van [GroupDocs.Signature voor Java-releases](https://releases.groupdocs.com/signature/java/).

#### Stappen voor het verkrijgen van een licentie
1. **Gratis proefperiode**: Test de functies met een gratis proefperiode van beperkte duur.
2. **Tijdelijke licentie**Schaf een tijdelijke licentie aan om alle mogelijkheden te verkennen.
3. **Aankoop**: Koop een abonnement als u langdurig toegang nodig hebt.

#### Basisinitialisatie en -installatie

Om GroupDocs.Signature te initialiseren, maakt u een exemplaar van de `Signature` klas:
```java
import com.groupdocs.signature.Signature;

// Initialiseer het handtekeningobject met het pad naar uw DICOM-bestand
Signature signature = new Signature(filePath);
```

## Implementatiegids

### Een DICOM-afbeelding ondertekenen met een QR-code en metagegevens

#### Overzicht
Met deze functie kunt u DICOM-afbeeldingen ondertekenen met een QR-code en XMP-metagegevens toevoegen, waardoor de beveiliging van uw documenten wordt verbeterd.

#### Stap 1: QR-code-ondertekeningsopties instellen
```java
import com.groupdocs.signature.domain.Padding;
import com.groupdocs.signature.domain.enums.HorizontalAlignment;
import com.groupdocs.signature.domain.enums.VerticalAlignment;
import com.groupdocs.signature.domain.signatures.QrCodeSignOptions;

Padding padding = new Padding();
padding.setRight(5);
padding.setLeft(5);

QrCodeSignOptions options = new QrCodeSignOptions("Patient #36363393. R: No-Issues");
options.setAllPages(true);
options.setWidth(100);
options.setHeight(100);
options.setVerticalAlignment(VerticalAlignment.Bottom);
options.setHorizontalAlignment(HorizontalAlignment.Right);
options.setMargin(padding);
```
Hier configureren we het uiterlijk en de positie van de QR-code op de DICOM-afbeelding.

#### Stap 2: XMP-metagegevens toevoegen
```java
import com.groupdocs.signature.options.saveoptions.imagessaveoptions.DicomSaveOptions;
import com.groupdocs.signature.options.saveoptions.imagessaveoptions.DicomXmpEntry;
import com.groupdocs.signature.options.saveoptions.imagessaveoptions.DicomXmpType;

DicomSaveOptions dicomSaveOptions = new DicomSaveOptions();
List<DicomXmpEntry> xmpEntries = new ArrayList<>();
xmpEntries.add(new DicomXmpEntry(DicomXmpType.PatientName, "Patient #4"));
dicomSaveOptions.setXmpEntries(xmpEntries);
```
Met dit fragment worden metagegevens aan het DICOM-bestand toegevoegd, waarin aanvullende patiëntinformatie is opgenomen.

#### Stap 3: Onderteken het document
```java
String outputFilePath = YOUR_OUTPUT_DIRECTORY + "/SignDicomImageAdvanced/" + fileName;
signature.sign(outputFilePath, options, dicomSaveOptions);
```
De `sign` schrijft de QR-code en metagegevens naar uw DICOM-bestand en slaat deze op de opgegeven locatie op.

### Ophalen van ondertekende DICOM-afbeeldingsinformatie

#### Overzicht
Extraheer XMP-metagegevens uit een ondertekende DICOM-image voor verificatie- of auditdoeleinden.
```java
import com.groupdocs.signature.domain.IDocumentInfo;
import com.groupdocs.signature.domain.signatures.MetadataSignature;

IDocumentInfo documentInfo = signature.getDocumentInfo();
for (MetadataSignature item : documentInfo.getMetadataSignatures()) {
    System.out.println(item.toString());
}
```
Met deze code worden alle metadatahandtekeningen die aan het DICOM-bestand zijn gekoppeld, opgehaald en afgedrukt.

### Verifiëren van ondertekende DICOM

#### Overzicht
Controleer of er een QR-codehandtekening aanwezig is in de ondertekende DICOM-afbeelding om de authenticiteit ervan te bevestigen.
```java
import com.groupdocs.signature.domain.VerificationResult;
import com.groupdocs.signature.options.verify.QrCodeVerifyOptions;
import com.groupdocs.signature.domain.enums.TextMatchType;

QrCodeVerifyOptions verifyOptions = new QrCodeVerifyOptions();
verifyOptions.setAllPages(true);
verifyOptions.setText("Patient #36363393");
verifyOptions.setMatchType(TextMatchType.Contains);

VerificationResult result = signature.verify(verifyOptions);
if (result.isValid()) {
    System.out.println(filePath + " has successfully verified signatures!");
} else {
    System.out.println(filePath + " failed verification process.");
}
```
Met deze verificatiestap wordt gecontroleerd of de QR-code aan de verwachte criteria voldoet en wordt de integriteit van het document bevestigd.

### Zoeken naar handtekeningen in ondertekende DICOM

#### Overzicht
Zoek alle QR-codehandtekeningen in een ondertekende DICOM-afbeelding om ze te bekijken of te controleren.
```java
import com.groupdocs.signature.domain.signatures.QrCodeSignature;
import java.util.List;

List<QrCodeSignature> signatures = signature.search(QrCodeSignature.class);
for (QrCodeSignature qrCodeSignature : signatures) {
    System.out.println("QRCode signature found at page " +
        qrCodeSignature.getPageNumber() + ": " +
        qrCodeSignature.getEncodeType().getTypeName() + ": " +
        qrCodeSignature.getText());
}
```
Deze functie is handig voor het scannen van alle QR-codehandtekeningen in het document, waardoor u een volledig overzicht krijgt.

### Voorbeeld van ondertekende DICOM genereren

#### Overzicht
Maak voorvertoningen voor elke pagina van een ondertekende DICOM-afbeelding, zodat u deze snel visueel kunt inspecteren zonder dat u het hele bestand hoeft te openen.
```java
import com.groupdocs.signature.options.PreviewOptions;
import java.io.File;
import java.io.FileOutputStream;
import java.nio.file.Paths;

PreviewOptions previewOption = new PreviewOptions(pageNumber -> {
    try {
        String pageFilePath = YOUR_OUTPUT_DIRECTORY + "/SignDicomImageAdvanced/image-" + pageNumber + ".jpg";
        return new FileOutputStream(Paths.get(pageFilePath).toFile());
    } catch (Exception e) {
        throw new RuntimeException(e.getMessage());
    }
});

signature.generatePreview(previewOption);
```
Met dit fragment worden voor elke pagina voorbeeldafbeeldingen gegenereerd. Dit kan handig zijn voor snelle verificatie of om te delen.

## Praktische toepassingen

GroupDocs.Signature voor Java biedt verschillende praktische toepassingen:
- **Medische beeldvorming**: Onderteken en beheer DICOM-beelden van patiënten veilig met QR-codes en metagegevens.
- **Juridisch documentbeheer**: Verbeter de authenticiteit van documenten en de naleving van regelgeving in gerechtelijke procedures.
- **Financiële diensten**: Implementeer veilige elektronische handtekeningen op gevoelige financiële documenten.