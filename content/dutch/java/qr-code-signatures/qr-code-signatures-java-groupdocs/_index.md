---
"date": "2025-05-08"
"description": "Leer hoe u de beveiliging van documenten kunt verbeteren door QR-codehandtekeningen in Java te implementeren en te verifiëren met GroupDocs.Signature. Volg deze stapsgewijze handleiding voor een veilig ondertekeningsproces."
"title": "Beveilig uw documenten&#58; implementeer QR-codehandtekeningen in Java met GroupDocs.Signature"
"url": "/nl/java/qr-code-signatures/qr-code-signatures-java-groupdocs/"
"weight": 1
---

# Beveilig uw documenten: implementeer QR-codehandtekeningen in Java met GroupDocs.Signature

In het huidige digitale landschap is het cruciaal om de beveiliging van documenten zoals contracten, facturen of gevoelige persoonlijke informatie te waarborgen. Een innovatieve aanpak om de documentbeveiliging te verbeteren en verificatieprocessen te vereenvoudigen, is het gebruik van QR-codehandtekeningen. Deze tutorial begeleidt u bij het implementeren en verifiëren van QR-codehandtekeningen voor uw documenten in Java met behulp van GroupDocs.Signature.

## Wat je zult leren
- Hoe documenten ondertekenen met QR-codes
- Ondertekende documenten verifiëren met QR-codes
- Zoeken naar bestaande QR-codehandtekeningen in een document
- QR-codehandtekeningen uit uw documenten bijwerken en verwijderen

Laten we uw omgeving instellen en aan de slag gaan!

### Vereisten
Voordat u begint, moet u ervoor zorgen dat u aan de volgende vereisten voldoet:

#### Vereiste bibliotheken en afhankelijkheden
Je hebt GroupDocs.Signature voor Java nodig. Je kunt het via Maven of Gradle toevoegen of direct downloaden.

**Maven**
```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

**Gradle**
```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

**Direct downloaden**
Download de nieuwste versie van [GroupDocs.Signature voor Java-releases](https://releases.groupdocs.com/signature/java/).

#### Vereisten voor omgevingsinstellingen
- Zorg ervoor dat u Java Development Kit (JDK) 8 of hoger hebt geïnstalleerd.
- Gebruik een IDE zoals IntelliJ IDEA, Eclipse of NetBeans.

#### Kennisvereisten
Een basiskennis van Java-programmering en documentverwerking is nuttig.

## GroupDocs.Signature instellen voor Java
Volg deze stappen om GroupDocs.Signature in uw project te gebruiken:
1. **Installatie**: Kies tussen Maven, Gradle of directe download, afhankelijk van uw instellingen.
2. **Licentieverwerving**:
   - Begin met een gratis proefperiode die beschikbaar is op de [GroupDocs-website](https://releases.groupdocs.com/signature/java/).
   - Overweeg om een tijdelijke licentie te verkrijgen voor uitgebreide tests en ontwikkeling van [hier](https://purchase.groupdocs.com/temporary-license/).
3. **Basisinitialisatie**: 
    Hier leest u hoe u GroupDocs.Signature initialiseert:

    ```java
    Signature signature = new Signature("YOUR_DOCUMENT_PATH");
    ```

Hiermee bent u voorbereid op het implementeren van QR-codehandtekeningen.

## Implementatiegids

### Document ondertekenen met QR-codehandtekening
#### Overzicht
Het ondertekenen van een document met een QR-code omvat het invoegen van een unieke code die uw digitale handtekening vertegenwoordigt. Dit proces beveiligt het document en maakt het mogelijk om de authenticiteit ervan later eenvoudig te verifiëren.

##### Stap 1: Stel uw ondertekeningsopties in
```java
import com.groupdocs.signature.Signature;
import com.groupdocs.signature.domain.enums.HorizontalAlignment;
import com.groupdocs.signature.domain.enums.VerticalAlignment;
import com.groupdocs.signature.options.sign.QrCodeSignOptions;

Signature signature = new Signature("YOUR_DOCUMENT_PATH");
QrCodeSignOptions signOptions = new QrCodeSignOptions("John Smith", com.groupdocs.signature.domain.qrcodes.QrCodeTypes.QR);

signOptions.setVerticalAlignment(VerticalAlignment.Top);
signOptions.setHorizontalAlignment(HorizontalAlignment.Center);
signOptions.setWidth(100);
signOptions.setHeight(40);
```
**Uitleg**: `QrCodeSignOptions` is geconfigureerd om een QR-code te maken met specifieke tekst en uitlijning. Pas de breedte en hoogte indien nodig aan.

##### Stap 2: Pas het uiterlijk van de handtekening aan
```java
import java.awt.Color;

signOptions.setForeColor(Color.RED); // QR-codekleur instellen
com.groupdocs.signature.domain.SignatureFont signatureFont = new com.groupdocs.signature.domain.SignatureFont();
signatureFont.setSize(12);
signatureFont.setFamilyName("Comic Sans MS");
signOptions.setFont(signatureFont);
```
**Uitleg**:Door het lettertype en de kleur aan te passen, wordt de visuele identificatie verbeterd.

##### Stap 3: Onderteken het document
```java
import java.util.ArrayList;
import java.util.List;

List<String> signatureIds = new ArrayList<>();
List<com.groupdocs.signature.domain.BaseSignature> signedSignatures = signature.sign("YOUR_OUTPUT_PATH", signOptions).getSucceeded();

for (com.groupdocs.signature.domain.BaseSignature temp : signedSignatures) {
    signatureIds.add(temp.getSignatureId());
}
```
**Uitleg**: Met deze stap wordt het document ondertekend en worden de handtekening-ID's opgeslagen voor toekomstig gebruik.

### Document verifiëren met QR-codehandtekening
#### Overzicht
Verificatie zorgt ervoor dat een document rechtmatig is ondertekend. Zo verifieert u een QR-codehandtekening in een document.

##### Stap 1: Verificatieopties instellen
```java
import com.groupdocs.signature.Signature;
import com.groupdocs.signature.options.verify.QrCodeVerifyOptions;

Signature signature2 = new Signature("YOUR_OUTPUT_PATH");
QrCodeVerifyOptions verifyOptions = new QrCodeVerifyOptions();

verifyOptions.setEncodeType(QrCodeTypes.QR);
verifyOptions.setText("John Smith"); // Tekst ter verificatie
verifyOptions.setAllPages(false); 
verifyOptions.setPageNumber(1);
```
**Uitleg**Met de verificatieopties kunt u aangeven naar welk type QR-code en welke tekst u wilt zoeken. Zo weet u zeker dat de handtekening aan uw verwachtingen voldoet.

##### Stap 2: Verificatie uitvoeren
```java
boolean isValid = signature2.verify(verifyOptions).isValid();
System.out.println("Is Signature Valid? " + isValid);
```
**Uitleg**: Hiermee wordt gecontroleerd of het document een geldige QR-code bevat die aan uw criteria voldoet.

### Zoek document voor QR-code handtekening
#### Overzicht
Soms is het nodig om bestaande handtekeningen in een document te vinden. Hier leest u hoe u ze kunt zoeken met GroupDocs.Signature.

##### Stap 1: Zoekopties configureren
```java
import com.groupdocs.signature.domain.signatures.QrCodeSignature;
import com.groupdocs.signature.options.search.QrCodeSearchOptions;

Signature signature2 = new Signature("YOUR_OUTPUT_PATH");
QrCodeSearchOptions searchOptions = new QrCodeSearchOptions();
searchOptions.setAllPages(true);
```
**Uitleg**: Hiermee wordt de tool zo ingesteld dat alle pagina's worden gescand op QR-codehandtekeningen.

##### Stap 2: Zoekopdracht uitvoeren
```java
List<QrCodeSignature> signatures = signature2.search(QrCodeSignature.class, searchOptions);

for (QrCodeSignature qrSignature : signatures) {
    System.out.println("Found Signature ID: " + qrSignature.getSignatureId());
}
```
**Uitleg**: Hiermee worden alle QR-codehandtekeningen in het document opgehaald.

### Document QR-code handtekening bijwerken
#### Overzicht
Het bijwerken van een handtekening houdt in dat je de eigenschappen ervan wijzigt, zoals de positie of grootte. Zo doe je dat:

##### Stap 1: Handtekeningen voorbereiden voor update
```java
import com.groupdocs.signature.domain.signatures.QrCodeSignature;
import java.io.ByteArrayOutputStream;

Signature signature2 = new Signature("YOUR_OUTPUT_PATH");
List<QrCodeSignature> signaturesToUpdate = new ArrayList<>();

// Ervan uitgaande dat 'handtekeningen' een lijst is van QrCodeSignature-objecten die zijn verkregen door te zoeken
for (QrCodeSignature qrSignature : signatures) {
    qrSignature.setLeft(qrSignature.getLeft() + 100);
    qrSignature.setTop(qrSignature.getTop() + 100);
    qrSignature.setWidth(200);
    qrSignature.setHeight(50);
    signaturesToUpdate.add(qrSignature);
}
```
**Uitleg**: Hiermee past u de positie en de grootte van elke handtekening aan.

##### Stap 2: Het document bijwerken
```java
ByteArrayOutputStream outputStream = new ByteArrayOutputStream();
signature2.update(outputStream, signaturesToUpdate);
```
**Uitleg**: Het document is bijgewerkt met de gewijzigde QR-codehandtekeningen.

### Document QR-code handtekening verwijderen via ID
#### Overzicht
Het verwijderen van een handtekening kan nodig zijn als deze niet langer nodig is of per ongeluk is toegevoegd. Hier leest u hoe u deze kunt verwijderen met behulp van de unieke ID.

##### Stap 1: Identificeer de handtekeningen die u wilt verwijderen
```java
import com.groupdocs.signature.domain.SignatureCollection;
import java.util.Arrays;

SignatureCollection signaturesToDelete = signature2.search(QrCodeSignature.class);
Arrays.stream(signaturesToDelete).forEach(signature -> {
    if (signature.getSignatureId().equals("YOUR_SIGNATURE_ID")) {
        signature.delete();
    }
});
```
**Uitleg**: Hiermee wordt de QR-codehandtekening gevonden en verwijderd op basis van de unieke ID.

## Conclusie
Deze handleiding heeft u begeleid bij het beveiligen van documenten met behulp van QR-codehandtekeningen in Java met GroupDocs.Signature. Door deze stappen te volgen, kunt u ervoor zorgen dat uw documenten veilig worden ondertekend en hun authenticiteit eenvoudig verifiëren.