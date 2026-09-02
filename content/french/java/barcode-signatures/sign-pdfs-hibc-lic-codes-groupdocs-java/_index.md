---
categories:
- Document Signing
- Healthcare Integration
date: '2026-05-16'
description: Apprenez à créer un PDF Data Matrix et à ajouter un PDF QR code en utilisant
  GroupDocs.Signature pour Java. Guide étape par étape pour la signature de documents
  de santé.
keywords:
- create data matrix pdf
- add qr code pdf
- HIBC barcode Java
lastmod: '2026-05-16'
linktitle: Guide de signature PDF HIBC Java
schemas:
- author: GroupDocs
  dateModified: '2026-05-16'
  description: Learn how to create data matrix PDF and add QR code PDF using GroupDocs.Signature
    for Java. Step‑by‑step guide for healthcare document signing.
  headline: Create Data Matrix PDF with HIBC Barcode in Java
  type: TechArticle
- description: Learn how to create data matrix PDF and add QR code PDF using GroupDocs.Signature
    for Java. Step‑by‑step guide for healthcare document signing.
  name: Create Data Matrix PDF with HIBC Barcode in Java
  steps:
  - name: '**Import the required classes** – these give you access to the signature
      engine and Data Matrix options.'
    text: '**Import the required classes** – these give you access to the signature
      engine and Data Matrix options.'
  - name: '**Instantiate the `Signature` object** with absolute paths for source and
      destination files.'
    text: '**Instantiate the `Signature` object** with absolute paths for source and
      destination files.'
  - name: '**Configure the Data Matrix options** – set the HIBC string, choose `QrCodeTypes.HIBCLICDataMatrix`,
      and define placement coordinates. `QrCodeTypes` enumerates the supported barcode
      formats for HIBC signatures.'
    text: '**Configure the Data Matrix options** – set the HIBC string, choose `QrCodeTypes.HIBCLICDataMatrix`,
      and define placement coordinates. `QrCodeTypes` enumerates the supported barcode
      formats for HIBC signatures.'
  - name: '**Apply the signature** to the PDF.'
    text: '**Apply the signature** to the PDF.'
  - name: '**Dispose of resources** to free file handles and avoid memory leaks.'
    text: '**Dispose of resources** to free file handles and avoid memory leaks.'
  - name: '**Import QR‑specific classes**'
    text: '**Import QR‑specific classes**'
  - name: '**Create and configure QR options** – note the use of `QrCodeTypes.HIBCLICQR`.'
    text: '**Create and configure QR options** – note the use of `QrCodeTypes.HIBCLICQR`.'
  - name: '**Sign the document**'
    text: '**Sign the document**'
  type: HowTo
- questions:
  - answer: Yes, it also supports DOCX, XLSX, PPTX, PNG, JPEG, and TIFF with the same
      barcode‑signing API.
    question: Can GroupDocs.Signature sign file types other than PDF?
  - answer: Verify that your HIBC string follows the exact HIBCC syntax, use the online
      validator, and ensure you’re using the correct `QrCodeTypes` constant for the
      chosen format.
    question: How do I troubleshoot “Invalid barcode content” errors?
  - answer: QR ≈ 4,296 alphanumeric characters, Aztec ≈ 3,832 numeric / 3,067 alphanumeric,
      Data Matrix ≈ 3,116 numeric / 2,335 alphanumeric. Keep codes under 200 characters
      for optimal scan reliability.
    question: What is the maximum data capacity for each HIBC format?
  - answer: Absolutely. Create separate `QrCodeSignOptions` objects with different
      positions and call `signature.sign()` for each. Just ensure they don’t overlap.
    question: Is it possible to embed multiple barcode types in one PDF?
  - answer: No. After the JAR is on the classpath and the license is activated, all
      operations are performed locally.
    question: Do I need an internet connection for signing at runtime?
  type: FAQPage
tags:
- java
- pdf-signing
- hibc
- healthcare
- barcode
- pharmaceutical
title: Créer un PDF Data Matrix avec le code-barres HIBC en Java
type: docs
url: /fr/java/barcode-signatures/sign-pdfs-hibc-lic-codes-groupdocs-java/
weight: 1
---

# Créer un PDF Data Matrix avec code-barres HIBC en Java

Si vous développez un logiciel de logistique pharmaceutique ou de santé, vous avez probablement rencontré les limites du suivi papier, les signatures perdues et les cauchemars d’audit. **Créer un PDF Data Matrix** qui intègre un code‑barres HIBC LIC résout ces problèmes en vous offrant une trace infalsifiable et lisible par machine qui résiste à l’impression, à la numérisation et aux contrôles réglementaires. Dans ce tutoriel, vous verrez exactement comment **ajouter la prise en charge du PDF de code QR**, ainsi que les formats Aztec et Data Matrix, en utilisant GroupDocs.Signature pour Java.

## Réponses rapides
- **Quelle bibliothèque gère les codes‑barres HIBC en Java ?** GroupDocs.Signature for Java.  
- **Quel format de code‑barres est le plus compact ?** Data Matrix – idéal pour les petites étiquettes.  
- **Puis‑je ajouter à la fois un QR et un Data Matrix au même PDF ?** Oui, il suffit de créer des `QrCodeSignOptions` séparés.  
- **Ai‑je besoin d’une connexion Internet à l’exécution ?** Non, la bibliothèque fonctionne entièrement hors ligne après l’installation.  
- **Quelle version de Java est recommandée ?** Java 11+ pour des performances de niveau production.

## Qu’est‑ce que la signature PDF avec code-barres HIBC ?
La classe `Signature` de GroupDocs.Signature pour Java représente un document PDF et fournit des méthodes pour intégrer des codes‑barres HIBC en tant que signatures numériques. En signant un PDF avec un code‑barres HIBC, vous créez un enregistrement vérifiable et infalsifiable qui peut être scanné à tout moment de la chaîne d’approvisionnement.

## Pourquoi utiliser conjointement Data Matrix et QR ?
GroupDocs.Signature prend en charge **plus de 50 formats d’entrée et de sortie** et peut traiter des PDF de plusieurs centaines de pages sans charger le fichier complet en mémoire. Utiliser Data Matrix pour des étiquettes denses et de petite surface et QR pour des documents plus spacieux vous offre le meilleur équilibre entre lisibilité, capacité de données (jusqu’à 4 296 caractères pour QR) et efficacité de l’espace d’impression.

## Prérequis
- **JDK 11 ou supérieur** (Java 8 fonctionne mais Java 11+ est recommandé pour des performances optimales).  
- **IDE** tel qu’IntelliJ IDEA, Eclipse ou VS Code avec extensions Java.  
- **Maven ou Gradle** pour la gestion des dépendances (exemples ci‑dessous).  
- **PDF d’exemple** (par ex., `sample.pdf`) pour tester l’implémentation.  
- **Licence valide GroupDocs.Signature** (essai gratuit pour le développement, licence payante pour la production).

## Configuration de GroupDocs.Signature pour Java

### Configuration Maven
Ajoutez la dépendance à votre `pom.xml` :

```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

### Configuration Gradle
Pour les projets Gradle, ajoutez ceci à votre `build.gradle` :

```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

### Option de téléchargement direct
Vous pouvez également télécharger le fichier JAR directement depuis [GroupDocs.Signature for Java releases](https://releases.groupdocs.com/signature/java/) et l’ajouter manuellement au classpath de votre projet. Cette approche fonctionne bien dans les environnements à réseau restreint.

### Obtention d’une licence
Demandez un essai gratuit ou une licence temporaire auprès de GroupDocs pour supprimer les filigranes et débloquer toutes les fonctionnalités. Les déploiements en production nécessitent une licence achetée.

### Initialisation de base
La classe `Signature` est le point d’entrée pour toutes les opérations de signature. Elle charge le PDF, applique le code‑barres et écrit le fichier signé.

```java
import com.groupdocs.signature.Signature;

class InitializeSignature {
    public static void main(String[] args) {
        Signature signature = new Signature("sample.pdf");
        // Proceed with signing operations...
    }
}
```

## Comment créer un PDF Data Matrix avec code-barres HIBC ?
Chargez votre PDF source, configurez un objet `QrCodeSignOptions` pour le format Data Matrix, puis appelez `sign()` – c’est tout ce dont vous avez besoin pour intégrer un code‑barres HIBC Data Matrix conforme. Les étapes suivantes vous guident à travers le code exact requis. `QrCodeSignOptions` définit les paramètres d’une signature de code‑barres, tels que le type, le contenu, la taille et la position.

1. **Import the required classes** – these give you access to the signature engine and Data Matrix options.  

```java
import com.groupdocs.signature.Signature;
import com.groupdocs.signature.options.sign.QrCodeSignOptions;
import com.groupdocs.signature.domain.qrcodes.QrCodeTypes;
```

2. **Instantiate the `Signature` object** with absolute paths for source and destination files.  

```java
String sourceFilePath = "YOUR_DOCUMENT_DIRECTORY";
String destinFilePath = "YOUR_OUTPUT_DIRECTORY/SignWithHIBCLICQR.pdf";

final Signature signature = new Signature(sourceFilePath);
```

3. **Configure the Data Matrix options** – set the HIBC string, choose `QrCodeTypes.HIBCLICDataMatrix`, and define placement coordinates. `QrCodeTypes` enumerates the supported barcode formats for HIBC signatures.  

```java
QrCodeSignOptions hibcLic_QR = new QrCodeSignOptions("A123PROD30917/75#422011907#GP293", QrCodeTypes.HIBCLICQR);
hibcLic_QR.setLeft(1); // Set the position from left
hibcLic_QR.setTop(1);   // Set the position from top
hibcLic_QR.setReturnContent(true); // Return content after signing
hibcLic_QR.setReturnContentType(FileType.PNG); // Specify return content type as PNG
```

4. **Apply the signature** to the PDF.  

```java
signature.sign(destinFilePath, hibcLic_QR);
```

5. **Dispose of resources** to free file handles and avoid memory leaks.  

```java
finally {
    if (signature != null) signature.dispose();
}
```

### Exemple complet fonctionnel
Voici le flux complet dans un seul bloc (les espaces réservés représentent le code exact que vous collerez à partir des extraits précédents) :

```java
import com.groupdocs.signature.Signature;
import com.groupdocs.signature.options.sign.QrCodeSignOptions;
import com.groupdocs.signature.domain.qrcodes.QrCodeTypes;

public class HibcQrSigning {
    public static void main(String[] args) {
        String sourceFilePath = "sample.pdf";
        String destinFilePath = "output/SignWithHIBCLICQR.pdf";
        
        Signature signature = null;
        try {
            signature = new Signature(sourceFilePath);
            
            QrCodeSignOptions hibcLic_QR = new QrCodeSignOptions(
                "A123PROD30917/75#422011907#GP293", 
                QrCodeTypes.HIBCLICQR
            );
            hibcLic_QR.setLeft(1);
            hibcLic_QR.setTop(1);
            hibcLic_QR.setReturnContent(true);
            hibcLic_QR.setReturnContentType(FileType.PNG);
            
            signature.sign(destinFilePath, hibcLic_QR);
            System.out.println("PDF signed successfully with HIBC QR code");
            
        } catch (Exception e) {
            System.err.println("Error signing PDF: " + e.getMessage());
            e.printStackTrace();
        } finally {
            if (signature != null) signature.dispose();
        }
    }
}
```

#### Réponse directe (40–70 mots)
Pour **créer un PDF Data Matrix**, instanciez `Signature` avec votre PDF source, définissez `QrCodeSignOptions` sur `QrCodeTypes.HIBCLICDataMatrix` et fournissez une chaîne HIBC correctement formatée, puis appelez `signature.sign(outputPath, options)`. La bibliothèque écrit le PDF signé vers la destination, préservant la mise en page et intégrant le code‑barres comme une signature infalsifiable.

## Comment ajouter un PDF de code QR avec GroupDocs.Signature ?
Chargez le PDF, configurez `QrCodeSignOptions` pour le format QR, puis invoquez `sign()`. Ce modèle en deux lignes fonctionne pour toute taille de PDF et ajuste automatiquement l’image QR pour une lisibilité optimale. `QrCodeSignOptions` configure la signature du code‑barres QR, y compris son contenu et ses propriétés visuelles. Il positionne le code selon les coordonnées que vous définissez, garantissant qu’il ne chevauche pas le contenu existant et reste scannable après impression.

1. **Import QR‑specific classes**  

```java
QrCodeSignOptions hibcLic_AZ = new QrCodeSignOptions("A123PROD30917/75#422011907#GP293", QrCodeTypes.HIBCLICAztec);
hibcLic_AZ.setLeft(1); // Set the position from left
hibcLic_AZ.setTop(200); // Set the position from top
hibcLic_AZ.setReturnContent(true); // Return content after signing
hibcLic_AZ.setReturnContentType(FileType.PNG); // Specify return content type as PNG
```

2. **Create and configure QR options** – note the use of `QrCodeTypes.HIBCLICQR`.  

```java
signature.sign(destinFilePath, hibcLic_AZ);
```

3. **Sign the document**  

```java
QrCodeSignOptions hibcLic_DM = new QrCodeSignOptions("A123PROD30917/75#422011907#GP293", QrCodeTypes.HIBCLICDataMatrix);
hibcLic_DM.setLeft(1); // Set the position from left
hibcLic_DM.setTop(400); // Set the position from top
hibcLic_DM.setReturnContent(true); // Return content after signing
hibcLic_DM.setReturnContentType(FileType.PNG); // Specify return content type as PNG
```

> **Réponse directe :** Utilisez `QrCodeTypes.HIBCLICQR` dans `QrCodeSignOptions`, définissez la chaîne de contenu HIBC, positionnez le code avec `setLeft()` et `setTop()`, puis appelez `signature.sign(outputPath, options)`. Le code‑barres QR est intégré instantanément, prêt à être capturé par smartphone ou scanner.

## Erreurs courantes à éviter

### 1. Oublier de libérer les ressources
**Incorrect :**  
```java
Signature signature = new Signature("sample.pdf");
signature.sign(destinFilePath, options);
// Oops, no dispose() call
```  

**Correction :** Enveloppez l’utilisation de `Signature` dans un bloc try‑with‑resources ou appelez explicitement `close()` dans un bloc finally.

### 2. Utiliser des chaînes de format HIBC incorrectes
**Incorrect :** Utilisation de chaînes génériques comme « 12345 ».  
**Correction :** Respectez la norme HIBCC (par ex., `A123PROD30917/75#422011907#GP293`). Validez avec le [HIBCC online validator](https://www.hibcc.org/).

### 3. Codage en dur des chemins de fichiers
**Incorrect :**  
```java
String sourceFilePath = "C:/Users/John/Documents/test.pdf";
```  

**Correction :** Stockez les chemins dans un fichier de configuration ou une variable d’environnement et lisez‑les à l’exécution.

### 4. Ignorer les conflits de position du code‑barres
Placez les codes‑barres loin du texte ou des signatures existants. Utilisez les coordonnées PDF (l’origine est en bas‑à‑gauche) et testez avec un échantillon imprimé.

### 5. Ne pas tester avec de vrais scanners
Imprimez le PDF signé et scannez‑le avec le matériel exact utilisé dans votre flux de travail. Vérifiez la lisibilité à différentes qualités d’impression.

## Applications pratiques dans le secteur de la santé

| Scénario | Code‑barres recommandé | Pourquoi c’est adapté |
|----------|------------------------|------------------------|
| **Distribution pharmaceutique** | QR Code | Grande capacité de données, largement scanné par les smartphones. |
| **Gestion des stocks** | Data Matrix | Petite empreinte, idéal pour les étiquettes d’étagères denses. |
| **Conformité réglementaire (FDA 21 CFR Part 11)** | QR + Data Matrix | Le double format offre redondance et auditabilité. |
| **Suivi des dispositifs médicaux** | Aztec Code | Taille compacte adaptée aux emballages à espace limité. |

## Considérations de performance et bonnes pratiques

### Modèle de traitement par lots
```java
List<String> filesToSign = getFileList();
for (String filePath : filesToSign) {
    Signature signature = null;
    try {
        signature = new Signature(filePath);
        // Sign and save
    } finally {
        if (signature != null) signature.dispose();
    }
}
```

- Créez une nouvelle instance `Signature` par fichier pour maintenir une faible utilisation de la mémoire.  
- Utilisez un pool de threads fixe (`Executors.newFixedThreadPool(Runtime.getRuntime().availableProcessors() - 1)`) pour le traitement parallèle, mais surveillez la taille du tas car chaque `Signature` charge le PDF complet en mémoire.  

### Maintenir les bibliothèques à jour
Les versions de GroupDocs améliorent la vitesse de traitement jusqu’à **20 %** et ajoutent de nouvelles fonctionnalités de conformité HIBC. Planifiez des vérifications de dépendances chaque trimestre.

### Mise en cache des modèles
Chargez un modèle PDF une fois, clonez‑le pour chaque variante de code‑barres et signez les clones. Cela réduit les I/O et accélère les flux de travail à haut volume.

## Questions fréquemment posées

**Q : GroupDocs.Signature peut‑il signer des types de fichiers autres que PDF ?**  
R : Oui, il prend également en charge DOCX, XLSX, PPTX, PNG, JPEG et TIFF avec la même API de signature de code‑barres.

**Q : Comment dépanner les erreurs « Invalid barcode content » ?**  
R : Vérifiez que votre chaîne HIBC suit exactement la syntaxe HIBCC, utilisez le validateur en ligne, et assurez‑vous d’utiliser la constante `QrCodeTypes` correcte pour le format choisi.

**Q : Quelle est la capacité maximale de données pour chaque format HIBC ?**  
R : QR ≈ 4 296 caractères alphanumériques, Aztec ≈ 3 832 numériques / 3 067 alphanumériques, Data Matrix ≈ 3 116 numériques / 2 335 alphanumériques. Gardez les codes sous 200 caractères pour une fiabilité de lecture optimale.

**Q : Est‑il possible d’intégrer plusieurs types de code‑barres dans un même PDF ?**  
R : Absolument. Créez des objets `QrCodeSignOptions` séparés avec des positions différentes et appelez `signature.sign()` pour chacun. Veillez simplement à ce qu’ils ne se chevauchent pas.

**Q : Ai‑je besoin d’une connexion Internet pour signer à l’exécution ?**  
R : Non. Une fois le JAR présent dans le classpath et la licence activée, toutes les opérations sont effectuées localement.

## Ressources supplémentaires

- [Documentation GroupDocs.Signature pour Java](https://docs.groupdocs.com/signature/java/)  
- [Guide de référence API](https://reference.groupdocs.com/signature/java/)  
- [Téléchargements des dernières versions](https://releases.groupdocs.com/signature/java/)  
- [Acheter une licence](https://purchase.groupdocs.com/buy)  
- [Obtenir un essai gratuit](https://releases.groupdocs.com/signature/java/)  
- [Demander une licence temporaire](https://purchase.groupdocs.com/temporary-license/)  
- [Forum GroupDocs](https://forum.groupdocs.com/c/signature/)

---

**Dernière mise à jour :** 2026-05-16  
**Testé avec :** GroupDocs.Signature 23.12 pour Java  
**Auteur :** GroupDocs  

```java
signature.sign(destinFilePath, hibcLic_DM);
```

## Tutoriels associés

- [Créer une signature de code‑barres PDF en Java – Guide GroupDocs](/signature/java/barcode-signatures/create-sign-pdfs-groupdocs-barcode-java/)
- [Créer une signature de code‑barres en Java – Mettre à jour les codes‑barres PDF](/signature/java/barcode-signatures/java-groupdocs-signature-barcode-initialize-update/)
- [Comment lire un PDF de code QR avec Java et GroupDocs.Signature](/signature/java/barcode-signatures/java-pdf-barcode-search-groupdocs-signature-api/)