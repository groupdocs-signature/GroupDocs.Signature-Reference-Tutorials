---
"date": "2025-05-08"
"description": "Découvrez comment renforcer la sécurité de vos documents en implémentant et en vérifiant les signatures de codes QR en Java avec GroupDocs.Signature. Suivez ce guide étape par étape pour un processus de signature sécurisé."
"title": "Sécurisez vos documents &#58; implémentez des signatures de code QR en Java avec GroupDocs.Signature"
"url": "/fr/java/qr-code-signatures/qr-code-signatures-java-groupdocs/"
"weight": 1
---

# Sécurisez vos documents : implémentez des signatures de code QR en Java avec GroupDocs.Signature

Dans le paysage numérique actuel, garantir la sécurité des documents tels que les contrats, les factures ou les informations personnelles sensibles est crucial. Une approche innovante pour renforcer la sécurité des documents et simplifier les processus de vérification consiste à utiliser des signatures par code QR. Ce tutoriel vous guidera dans l'implémentation et la vérification des signatures par code QR pour vos documents en Java avec GroupDocs.Signature.

## Ce que vous apprendrez
- Comment signer des documents à l'aide de codes QR
- Vérification des documents signés avec des codes QR
- Recherche de signatures de code QR existantes dans un document
- Mise à jour et suppression des signatures de codes QR de vos documents

Configurons votre environnement et commençons !

### Prérequis
Avant de commencer, assurez-vous d’avoir les prérequis suivants :

#### Bibliothèques et dépendances requises
Vous aurez besoin de GroupDocs.Signature pour Java. Vous pouvez l'inclure via Maven ou Gradle, ou le télécharger directement.

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

**Téléchargement direct**
Téléchargez la dernière version depuis [Versions de GroupDocs.Signature pour Java](https://releases.groupdocs.com/signature/java/).

#### Configuration requise pour l'environnement
- Assurez-vous que Java Development Kit (JDK) 8 ou supérieur est installé.
- Utilisez un IDE comme IntelliJ IDEA, Eclipse ou NetBeans.

#### Prérequis en matière de connaissances
Une compréhension de base de la programmation Java et du traitement de documents est bénéfique.

## Configuration de GroupDocs.Signature pour Java
Pour utiliser GroupDocs.Signature dans votre projet, suivez ces étapes :
1. **Installation**: Choisissez entre Maven, Gradle ou le téléchargement direct en fonction de votre configuration.
2. **Acquisition de licence**:
   - Commencez par un essai gratuit disponible sur le [Site Web GroupDocs](https://releases.groupdocs.com/signature/java/).
   - Envisagez d'obtenir une licence temporaire pour des tests et un développement prolongés auprès de [ici](https://purchase.groupdocs.com/temporary-license/).
3. **Initialisation de base**: 
    Voici comment initialiser GroupDocs.Signature :

    ```java
    Signature signature = new Signature("YOUR_DOCUMENT_PATH");
    ```

Cela vous prépare à la mise en œuvre des signatures de code QR.

## Guide de mise en œuvre

### Signer un document avec une signature par code QR
#### Aperçu
Signer un document avec un QR Code implique l'insertion d'un code unique représentant votre signature numérique. Ce procédé sécurise le document et permet de vérifier facilement son authenticité ultérieurement.

##### Étape 1 : Configurez vos options de signature
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
**Explication**: `QrCodeSignOptions` est configuré pour créer un code QR avec un texte et un alignement spécifiques. Ajustez la largeur et la hauteur selon vos besoins.

##### Étape 2 : Personnaliser l’apparence de la signature
```java
import java.awt.Color;

signOptions.setForeColor(Color.RED); // Définir la couleur du code QR
com.groupdocs.signature.domain.SignatureFont signatureFont = new com.groupdocs.signature.domain.SignatureFont();
signatureFont.setSize(12);
signatureFont.setFamilyName("Comic Sans MS");
signOptions.setFont(signatureFont);
```
**Explication**: La personnalisation de la police et de la couleur améliore l’identification visuelle.

##### Étape 3 : Signer le document
```java
import java.util.ArrayList;
import java.util.List;

List<String> signatureIds = new ArrayList<>();
List<com.groupdocs.signature.domain.BaseSignature> signedSignatures = signature.sign("YOUR_OUTPUT_PATH", signOptions).getSucceeded();

for (com.groupdocs.signature.domain.BaseSignature temp : signedSignatures) {
    signatureIds.add(temp.getSignatureId());
}
```
**Explication**:Cette étape signe le document et stocke les identifiants de signature pour référence ultérieure.

### Vérifier le document avec la signature du code QR
#### Aperçu
La vérification garantit qu'un document a été signé légalement. Voici comment vérifier une signature par QR Code dans un document.

##### Étape 1 : Configurer les options de vérification
```java
import com.groupdocs.signature.Signature;
import com.groupdocs.signature.options.verify.QrCodeVerifyOptions;

Signature signature2 = new Signature("YOUR_OUTPUT_PATH");
QrCodeVerifyOptions verifyOptions = new QrCodeVerifyOptions();

verifyOptions.setEncodeType(QrCodeTypes.QR);
verifyOptions.setText("John Smith"); // Texte à vérifier
verifyOptions.setAllPages(false); 
verifyOptions.setPageNumber(1);
```
**Explication**:Les options de vérification spécifient le type de code QR et le texte à rechercher, garantissant que la signature correspond à vos attentes.

##### Étape 2 : Effectuer la vérification
```java
boolean isValid = signature2.verify(verifyOptions).isValid();
System.out.println("Is Signature Valid? " + isValid);
```
**Explication**: Cela vérifie si le document contient un code QR valide correspondant à vos critères.

### Rechercher un document pour une signature de code QR
#### Aperçu
Il est parfois nécessaire de localiser des signatures existantes dans un document. Voici comment les rechercher avec GroupDocs.Signature.

##### Étape 1 : Configurer les options de recherche
```java
import com.groupdocs.signature.domain.signatures.QrCodeSignature;
import com.groupdocs.signature.options.search.QrCodeSearchOptions;

Signature signature2 = new Signature("YOUR_OUTPUT_PATH");
QrCodeSearchOptions searchOptions = new QrCodeSearchOptions();
searchOptions.setAllPages(true);
```
**Explication**:Cela configure l'outil pour analyser toutes les pages à la recherche de signatures de code QR.

##### Étape 2 : Exécuter la recherche
```java
List<QrCodeSignature> signatures = signature2.search(QrCodeSignature.class, searchOptions);

for (QrCodeSignature qrSignature : signatures) {
    System.out.println("Found Signature ID: " + qrSignature.getSignatureId());
}
```
**Explication**: Cela récupère toutes les signatures de code QR trouvées dans le document.

### Mettre à jour la signature du code QR du document
#### Aperçu
Mettre à jour une signature implique de modifier ses propriétés, comme sa position ou sa taille. Voici comment procéder :

##### Étape 1 : préparer les signatures pour la mise à jour
```java
import com.groupdocs.signature.domain.signatures.QrCodeSignature;
import java.io.ByteArrayOutputStream;

Signature signature2 = new Signature("YOUR_OUTPUT_PATH");
List<QrCodeSignature> signaturesToUpdate = new ArrayList<>();

// En supposant que « signatures » est une liste d'objets QrCodeSignature obtenus à partir d'une recherche
for (QrCodeSignature qrSignature : signatures) {
    qrSignature.setLeft(qrSignature.getLeft() + 100);
    qrSignature.setTop(qrSignature.getTop() + 100);
    qrSignature.setWidth(200);
    qrSignature.setHeight(50);
    signaturesToUpdate.add(qrSignature);
}
```
**Explication**:Cela ajuste la position et la taille de chaque signature.

##### Étape 2 : Mettre à jour le document
```java
ByteArrayOutputStream outputStream = new ByteArrayOutputStream();
signature2.update(outputStream, signaturesToUpdate);
```
**Explication**:Le document est mis à jour avec les signatures de code QR modifiées.

### Supprimer la signature du code QR du document par identifiant
#### Aperçu
Il peut être nécessaire de supprimer une signature si elle n'est plus nécessaire ou si elle a été ajoutée par erreur. Voici comment la supprimer grâce à son identifiant unique.

##### Étape 1 : Identifier les signatures à supprimer
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
**Explication**: Cela recherche et supprime la signature du code QR par son identifiant unique.

## Conclusion
Ce guide vous explique comment sécuriser vos documents à l'aide de signatures par code QR en Java avec GroupDocs.Signature. En suivant ces étapes, vous pouvez garantir la sécurité de vos documents et vérifier leur authenticité facilement.