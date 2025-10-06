---
"date": "2025-05-08"
"description": "Lär dig hur du signerar DICOM-bilder säkert med GroupDocs.Signature för Java. Förbättra dokumentsäkerheten genom att bädda in QR-koder och metadata."
"title": "Signera DICOM-bilder med QR-koder och metadata med GroupDocs.Signature för Java"
"url": "/sv/java/image-signatures/sign-dicom-images-groupdocs-signature-java/"
"weight": 1
type: docs
---
# Hur man signerar DICOM-bilder med QR-koder och metadata med GroupDocs.Signature för Java

## Introduktion

I det snabbt föränderliga digitala hälsovårdslandskapet är det av yttersta vikt att hantera patientdata på ett säkert sätt. Den här handledningen guidar dig genom att implementera en robust lösning med GroupDocs.Signature för Java för att signera DICOM-bilder (Digital Imaging and Communications in Medicine) med QR-koder och metadata. Dessa funktioner säkerställer autenticitet, förbättrar spårbarheten och upprätthåller efterlevnad genom att bädda in viktig information direkt i medicinska bilder.

### Vad du kommer att lära dig:
- Hur man integrerar GroupDocs.Signature för Java i sitt projekt.
- Processen att signera DICOM-bilder med QR-koder.
- Lägger till XMP-metadata för att förbättra dokumentsäkerheten.
- Hämta, verifiera och söka efter signaturer i DICOM-filer.
- Genererar förhandsgranskningar av signerade DICOM-bilder.

Nu kör vi! Innan vi börjar, låt oss se till att du har allt som behövs för att följa med smidigt.

## Förkunskapskrav

För att implementera GroupDocs.Signature-funktionerna effektivt, se till att du uppfyller följande krav:

### Obligatoriska bibliotek och beroenden
- **GroupDocs.Signature för Java**Du behöver version 23.12 eller senare av det här biblioteket.

### Krav för miljöinstallation
- **Java-utvecklingspaket (JDK)**Se till att JDK är installerat på ditt system.
- **ID**Använd en integrerad utvecklingsmiljö som IntelliJ IDEA eller Eclipse.

### Kunskapsförkunskaper
En grundläggande förståelse för:
- Java-programmering och objektorienterade principer.
- Maven- eller Gradle-byggverktyg för beroendehantering.

## Konfigurera GroupDocs.Signature för Java

För att komma igång med GroupDocs.Signature måste du lägga till det som ett beroende i ditt projekt. Så här kan du göra detta med olika byggverktyg:

### Maven
Lägg till följande utdrag till din `pom.xml` fil:
```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

### Gradle
Inkludera detta i din `build.gradle` fil:
```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

### Direkt nedladdning
Alternativt kan du ladda ner den senaste versionen från [GroupDocs.Signature för Java-utgåvor](https://releases.groupdocs.com/signature/java/).

#### Steg för att förvärva licens
1. **Gratis provperiod**Testa funktionerna med en tidsbegränsad gratis provperiod.
2. **Tillfällig licens**Skaffa en tillfällig licens för att utforska alla funktioner.
3. **Köpa**Köp en prenumeration om du behöver långsiktig åtkomst.

#### Grundläggande initialisering och installation

För att initiera GroupDocs.Signature, skapa en instans av `Signature` klass:
```java
import com.groupdocs.signature.Signature;

// Initiera signaturobjektet med sökvägen till din DICOM-fil
Signature signature = new Signature(filePath);
```

## Implementeringsguide

### Signera en DICOM-bild med QR-kod och metadata

#### Översikt
Den här funktionen låter dig signera DICOM-bilder med en QR-kod och lägga till XMP-metadata, vilket förbättrar dokumentsäkerheten.

#### Steg 1: Konfigurera alternativ för QR-kodsignering
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
Här konfigurerar vi QR-kodens utseende och position på DICOM-bilden.

#### Steg 2: Lägg till XMP-metadata
```java
import com.groupdocs.signature.options.saveoptions.imagessaveoptions.DicomSaveOptions;
import com.groupdocs.signature.options.saveoptions.imagessaveoptions.DicomXmpEntry;
import com.groupdocs.signature.options.saveoptions.imagessaveoptions.DicomXmpType;

DicomSaveOptions dicomSaveOptions = new DicomSaveOptions();
List<DicomXmpEntry> xmpEntries = new ArrayList<>();
xmpEntries.add(new DicomXmpEntry(DicomXmpType.PatientName, "Patient #4"));
dicomSaveOptions.setXmpEntries(xmpEntries);
```
Det här kodavsnittet lägger till metadata i DICOM-filen och bäddar in ytterligare patientinformation.

#### Steg 3: Signera dokumentet
```java
String outputFilePath = YOUR_OUTPUT_DIRECTORY + "/SignDicomImageAdvanced/" + fileName;
signature.sign(outputFilePath, options, dicomSaveOptions);
```
De `sign` Metoden skriver QR-koden och metadata till din DICOM-fil och sparar den på den angivna platsen.

### Hämtar signerad DICOM-bildinformation

#### Översikt
Extrahera XMP-metadata från en signerad DICOM-bild för verifiering eller granskning.
```java
import com.groupdocs.signature.domain.IDocumentInfo;
import com.groupdocs.signature.domain.signatures.MetadataSignature;

IDocumentInfo documentInfo = signature.getDocumentInfo();
for (MetadataSignature item : documentInfo.getMetadataSignatures()) {
    System.out.println(item.toString());
}
```
Den här koden hämtar och skriver ut alla metadatasignaturer som är associerade med DICOM-filen.

### Verifierar signerad DICOM

#### Översikt
Kontrollera att en QR-kodsignatur finns i den signerade DICOM-bilden för att bekräfta dess äkthet.
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
Detta verifieringssteg säkerställer att QR-koden matchar förväntade kriterier och bekräftar dokumentets integritet.

### Söka efter signaturer i signerad DICOM

#### Översikt
Leta reda på alla QR-kodsignaturer i en signerad DICOM-bild för att granska eller granska dem.
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
Den här funktionen är användbar för att skanna alla QR-kodsignaturer i dokumentet, vilket ger omfattande överblick.

### Genererar förhandsgranskning av signerad DICOM

#### Översikt
Skapa förhandsgranskningar för varje sida av en signerad DICOM-bild, vilket möjliggör snabb visuell inspektion utan att öppna hela filen.
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
Det här utdraget genererar förhandsgranskningar av bilder för varje sida, vilket kan vara användbart för snabb verifiering eller delning.

## Praktiska tillämpningar

GroupDocs.Signature för Java erbjuder flera verkliga tillämpningar:
- **Medicinsk avbildning**Signera och hantera patient-DICOM-bilder säkert med QR-koder och metadata.
- **Hantering av juridiska dokument**Förbättra dokumentäkthet och efterlevnad i rättsliga förfaranden.
- **Finansiella tjänster**Implementera säkra elektroniska signaturer på känsliga finansiella dokument.