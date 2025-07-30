---
"date": "2025-05-08"
"description": "Découvrez comment signer des images DICOM en toute sécurité avec GroupDocs.Signature pour Java. Améliorez la sécurité de vos documents en intégrant des codes QR et des métadonnées."
"title": "Signer des images DICOM avec des codes QR et des métadonnées à l'aide de GroupDocs.Signature pour Java"
"url": "/fr/java/image-signatures/sign-dicom-images-groupdocs-signature-java/"
"weight": 1
---

# Comment signer des images DICOM avec des codes QR et des métadonnées à l'aide de GroupDocs.Signature pour Java

## Introduction

Dans un environnement de santé numérique en constante évolution, la gestion sécurisée des données patients est primordiale. Ce tutoriel vous guide dans la mise en œuvre d'une solution robuste utilisant GroupDocs.Signature pour Java pour signer des images DICOM (Digital Imaging and Communications in Medicine) avec des codes QR et des métadonnées. Ces fonctionnalités garantissent l'authenticité, améliorent la traçabilité et garantissent la conformité en intégrant des informations vitales directement dans les images médicales.

### Ce que vous apprendrez :
- Comment intégrer GroupDocs.Signature pour Java dans votre projet.
- Le processus de signature d'images DICOM avec des codes QR.
- Ajout de métadonnées XMP pour améliorer la sécurité des documents.
- Récupération, vérification et recherche de signatures dans les fichiers DICOM.
- Génération d'aperçus d'images DICOM signées.

C'est parti ! Avant de commencer, assurez-vous que vous avez tout le nécessaire pour suivre le cours sans problème.

## Prérequis

Pour implémenter efficacement les fonctionnalités de GroupDocs.Signature, assurez-vous de respecter les conditions préalables suivantes :

### Bibliothèques et dépendances requises
- **GroupDocs.Signature pour Java**:Vous aurez besoin de la version 23.12 ou ultérieure de cette bibliothèque.

### Configuration requise pour l'environnement
- **Kit de développement Java (JDK)**: Assurez-vous que JDK est installé sur votre système.
- **IDE**:Utilisez un environnement de développement intégré comme IntelliJ IDEA ou Eclipse.

### Prérequis en matière de connaissances
Une compréhension de base de :
- Programmation Java et principes orientés objet.
- Outils de build Maven ou Gradle pour la gestion des dépendances.

## Configuration de GroupDocs.Signature pour Java

Pour commencer à utiliser GroupDocs.Signature, vous devez l'ajouter comme dépendance à votre projet. Voici comment procéder avec différents outils de build :

### Maven
Ajoutez l'extrait suivant à votre `pom.xml` déposer:
```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

### Gradle
Incluez ceci dans votre `build.gradle` déposer:
```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

### Téléchargement direct
Alternativement, vous pouvez télécharger la dernière version à partir de [Versions de GroupDocs.Signature pour Java](https://releases.groupdocs.com/signature/java/).

#### Étapes d'acquisition de licence
1. **Essai gratuit**:Testez les fonctionnalités avec un essai gratuit à durée limitée.
2. **Licence temporaire**Obtenez une licence temporaire pour explorer toutes les fonctionnalités.
3. **Achat**: Achetez un abonnement si vous avez besoin d’un accès à long terme.

#### Initialisation et configuration de base

Pour initialiser GroupDocs.Signature, créez une instance du `Signature` classe:
```java
import com.groupdocs.signature.Signature;

// Initialisez l'objet de signature avec le chemin d'accès à votre fichier DICOM
Signature signature = new Signature(filePath);
```

## Guide de mise en œuvre

### Signature d'une image DICOM avec un code QR et des métadonnées

#### Aperçu
Cette fonctionnalité vous permet de signer des images DICOM avec un code QR et d'ajouter des métadonnées XMP, améliorant ainsi la sécurité des documents.

#### Étape 1 : Configurer les options de signature du code QR
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
Ici, nous configurons l'apparence et la position du code QR sur l'image DICOM.

#### Étape 2 : ajouter des métadonnées XMP
```java
import com.groupdocs.signature.options.saveoptions.imagessaveoptions.DicomSaveOptions;
import com.groupdocs.signature.options.saveoptions.imagessaveoptions.DicomXmpEntry;
import com.groupdocs.signature.options.saveoptions.imagessaveoptions.DicomXmpType;

DicomSaveOptions dicomSaveOptions = new DicomSaveOptions();
List<DicomXmpEntry> xmpEntries = new ArrayList<>();
xmpEntries.add(new DicomXmpEntry(DicomXmpType.PatientName, "Patient #4"));
dicomSaveOptions.setXmpEntries(xmpEntries);
```
Cet extrait ajoute des métadonnées au fichier DICOM, intégrant des informations supplémentaires sur le patient.

#### Étape 3 : Signer le document
```java
String outputFilePath = YOUR_OUTPUT_DIRECTORY + "/SignDicomImageAdvanced/" + fileName;
signature.sign(outputFilePath, options, dicomSaveOptions);
```
Le `sign` La méthode écrit le code QR et les métadonnées dans votre fichier DICOM, en l'enregistrant à l'emplacement spécifié.

### Récupération des informations d'image DICOM signées

#### Aperçu
Extraire les métadonnées XMP d'une image DICOM signée à des fins de vérification ou d'audit.
```java
import com.groupdocs.signature.domain.IDocumentInfo;
import com.groupdocs.signature.domain.signatures.MetadataSignature;

IDocumentInfo documentInfo = signature.getDocumentInfo();
for (MetadataSignature item : documentInfo.getMetadataSignatures()) {
    System.out.println(item.toString());
}
```
Ce code récupère et imprime toutes les signatures de métadonnées associées au fichier DICOM.

### Vérification du DICOM signé

#### Aperçu
Vérifiez qu’une signature de code QR est présente dans l’image DICOM signée pour confirmer son authenticité.
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
Cette étape de vérification garantit que le code QR correspond aux critères attendus, confirmant ainsi l’intégrité du document.

### Recherche de signatures dans un DICOM signé

#### Aperçu
Localisez toutes les signatures de code QR dans une image DICOM signée pour les examiner ou les auditer.
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
Cette fonctionnalité est utile pour numériser toutes les signatures de code QR dans le document, offrant une visibilité complète.

### Génération d'un aperçu du DICOM signé

#### Aperçu
Créez des aperçus pour chaque page d'une image DICOM signée, permettant une inspection visuelle rapide sans ouvrir l'intégralité du fichier.
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
Cet extrait génère des aperçus d'images pour chaque page, ce qui peut être utile pour une vérification ou un partage rapide.

## Applications pratiques

GroupDocs.Signature pour Java propose plusieurs applications concrètes :
- **Imagerie médicale**: Signez et gérez en toute sécurité les images DICOM des patients avec des codes QR et des métadonnées.
- **Gestion des documents juridiques**:Améliorer l'authenticité et la conformité des documents dans les procédures judiciaires.
- **Services financiers**: Mettre en œuvre des signatures électroniques sécurisées sur des documents financiers sensibles.