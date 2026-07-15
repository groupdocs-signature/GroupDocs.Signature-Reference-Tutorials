---
date: '2026-07-15'
description: Apprenez comment ajouter Barcode PDF Java en utilisant GroupDocs.Signature
  – guide étape par étape pour signer, vérifier, rechercher, mettre à jour et supprimer
  les signatures de barcode dans les documents Java.
keywords:
- add barcode pdf java
- groupdocs barcode signature
- java document signing
lastmod: '2026-07-15'
linktitle: Guide Barcode Signature Java
og_description: Apprenez comment ajouter Barcode PDF Java en utilisant GroupDocs.Signature
  – guide étape par étape pour signer, vérifier, rechercher, mettre à jour et supprimer
  les signatures de barcode dans les documents Java.
og_image_alt: Guide showing how to add barcode PDF Java using GroupDocs.Signature
og_title: Ajouter Barcode PDF Java – Signer et vérifier avec GroupDocs
schemas:
- author: GroupDocs
  dateModified: '2026-07-15'
  description: Learn how to add barcode PDF Java using GroupDocs.Signature – step‑by‑step
    guide to sign, verify, search, update and delete barcode signatures in Java documents.
  headline: Add Barcode PDF Java – Sign & Verify with GroupDocs
  type: TechArticle
- description: Learn how to add barcode PDF Java using GroupDocs.Signature – step‑by‑step
    guide to sign, verify, search, update and delete barcode signatures in Java documents.
  name: Add Barcode PDF Java – Sign & Verify with GroupDocs
  steps:
  - name: Case mismatch (e.g., “John Smith” vs. “john smith”).
    text: Case mismatch (e.g., “John Smith” vs. “john smith”).
  - name: Extra whitespace in the encoded text.
    text: Extra whitespace in the encoded text.
  - name: Wrong barcode type specified in the verification options.
    text: Wrong barcode type specified in the verification options.
  - name: Searching the wrong page number.
    text: Searching the wrong page number.
  - name: '**Reuse Signature Instances** – Create a single `Signature` object per
      document and reuse it for multiple operations.'
    text: '**Reuse Signature Instances** – Create a single `Signature` object per
      document and reuse it for multiple operations.'
  - name: '**Search Specific Pages Only** – Limit the page range to where barcodes
      are expected.'
    text: '**Search Specific Pages Only** – Limit the page range to where barcodes
      are expected.'
  - name: '**Choose the Simplest Barcode Type** – Simpler barcodes generate faster;
      only use QR or Data Matrix when you truly need the extra capacity.'
    text: '**Choose the Simplest Barcode Type** – Simpler barcodes generate faster;
      only use QR or Data Matrix when you truly need the extra capacity.'
  - name: '**Never Encode Sensitive Personal Data** – Barcodes are easily readable;
      avoid PII such as SSNs or passwords.'
    text: '**Never Encode Sensitive Personal Data** – Barcodes are easily readable;
      avoid PII such as SSNs or passwords.'
  - name: '**Validate Server‑Side** – Never trust client‑side verification alone;
      always re‑verify on a trusted backend.'
    text: '**Validate Server‑Side** – Never trust client‑side verification alone;
      always re‑verify on a trusted backend.'
  - name: '**Add Timestamps** – Include a timestamp in the barcode payload to prevent
      replay attacks.'
    text: '**Add Timestamps** – Include a timestamp in the barcode payload to prevent
      replay attacks.'
  type: HowTo
- questions:
  - answer: Yes – the library is fully compatible with JDK 8, 11, and 17.
    question: Can I use GroupDocs.Signature with Java 17?
  - answer: When you use Code128 or QR with sufficient size and contrast, the barcode
      remains scannable after printing and scanning.
    question: Does the barcode survive a print‑scan cycle?
  - answer: There is no hard limit; however, for optimal performance keep the total
      count below **200** per document.
    question: How many barcodes can a single document contain?
  - answer: A temporary license removes evaluation watermarks; a full license is mandatory
      for any production deployment.
    question: Is a license required for development builds?
  - answer: Yes – provide the password when creating the `Signature` object; the API
      will unlock the file internally.
    question: Can I sign password‑protected PDFs?
  type: FAQPage
tags:
- barcode signature
- groupdocs
- java
- pdf
- document signing
title: Ajouter Barcode PDF Java – Signer et vérifier avec GroupDocs
type: docs
url: /fr/java/digital-signatures/java-document-signature-groupdocs-signature-barcode/
weight: 1
---

# Ajouter un code‑barres PDF Java – Signer et vérifier avec GroupDocs

Si vous avez besoin d’une méthode rapide et visuelle pour marquer les documents dans les flux de travail internes, ajouter un code‑barres à un PDF en Java est une solution idéale. Avec **GroupDocs.Signature**, vous pouvez intégrer, vérifier, rechercher, mettre à jour et supprimer des signatures de code‑barres sans la surcharge des signatures numériques complètes basées sur PKI. Ce tutoriel vous guide à travers chaque étape, de la configuration de l’environnement aux meilleures pratiques prêtes pour la production.

## Réponses rapides
- **Quelle bibliothèque ajoute un code‑barres aux PDF en Java ?** GroupDocs.Signature for Java.  
- **Puis‑je signer des PDF, Word et images ?** Oui – l’API prend en charge plus de 30 formats.  
- **Ai‑je besoin d’une licence pour le développement ?** Une licence temporaire de 30 jours est gratuite ; une licence complète est requise pour la production.  
- **Combien de lignes de code pour signer un PDF ?** Juste deux lignes : créez un objet `Signature` et appelez `sign`.  
- **La vérification du code‑barres est‑elle sensible à la casse ?** Oui – le texte doit correspondre exactement, y compris la casse et les espaces.

## Qu’est‑ce que add barcode pdf java ?
`add barcode pdf java` désigne le processus d’utilisation du code Java pour intégrer un code‑barres (tel que Code128, QR ou Data Matrix) dans un fichier PDF. Cette technique fournit une étiquette lisible par machine qui peut être scannée ou vérifiée programmatiquement, permettant un suivi rapide des documents dans les systèmes internes.

## Pourquoi utiliser des signatures de code‑barres plutôt que des signatures numériques complètes ?
Les signatures de code‑barres sont **30‑50 % plus rapides** à générer et à vérifier que les signatures numériques basées sur PKI, et elles fonctionnent de manière fiable après un cycle impression‑numérisation. Elles ne nécessitent aucune gestion de certificats, ce qui les rend idéales pour des flux de travail internes à haut volume où la preuve cryptographique n’est pas obligatoire.

## Prérequis
- **Java Development Kit (JDK) 8+** – Java 11 ou 17 est recommandé pour de meilleures performances.  
- **IDE** – IntelliJ IDEA ou Eclipse (les exemples utilisent la syntaxe IntelliJ).  
- **Outil de construction** – Maven ou Gradle pour la gestion des dépendances.  

### Ajouter GroupDocs.Signature à votre projet
La façon la plus simple de commencer est d’ajouter la bibliothèque via votre outil de construction. Voici comment :

**Utilisateurs Maven** – Ajoutez ceci à votre `pom.xml` :

```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

**Utilisateurs Gradle** – Ajoutez ceci à votre `build.gradle` :

```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

**Téléchargement direct du JAR** – Si vous préférez une configuration manuelle, récupérez le JAR depuis [versions GroupDocs.Signature](https://releases.groupdocs.com/signature/java/) et ajoutez‑le à votre classpath.

### Obtenir votre licence
GroupDocs.Signature n’est pas gratuit pour une utilisation en production, mais vous avez des options flexibles :
- **Essai gratuit** – Téléchargez depuis la [page de téléchargement GroupDocs](https://releases.groupdocs.com/signature/java/) pour tester les fonctionnalités (des filigranes d’évaluation sont ajoutés).  
- **Licence temporaire** – Obtenez 30 jours d’accès complet via la [page de licence temporaire de GroupDocs](https://purchase.groupdocs.com/temporary-license/) – idéal pour les preuves de concept.  
- **Licence complète** – Pour les déploiements en production, consultez les [options d’achat GroupDocs](https://purchase.groupdocs.com/buy).  

**Astuce :** Commencez avec la licence temporaire pour le développement ; elle supprime les filigranes une fois que vous passez à une clé permanente.

### Vérification rapide de l’environnement
Une fois la dépendance ajoutée, exécutez un test de fumée simple :

```java
import com.groupdocs.signature.Signature;

public class SignatureTest {
    public static void main(String[] args) {
        try {
            Signature signature = new Signature("test.pdf");
            System.out.println("GroupDocs.Signature initialized successfully!");
            signature.dispose();
        } catch (Exception e) {
            System.err.println("Setup issue: " + e.getMessage());
        }
    }
}
```

Si le programme s’exécute sans erreur, votre environnement est prêt. En cas de problème, vérifiez la version du JDK et la version exacte de la bibliothèque que vous avez ajoutée.

## Quand utiliser les signatures de code‑barres
Les signatures de code‑barres excellent dans des scénarios spécifiques :
- **Flux de travail internes de documents** – Suivez les factures, bons de commande ou mémos à travers les chaînes d’approbation.  
- **Traitement à haut volume** – Signez des milliers de documents rapidement ; la génération de code‑barres est jusqu’à **2 fois plus rapide** que la signature numérique complète.  
- **Ponts impression‑numérisation** – Les code‑barres survivent au cycle impression‑numérisation, les rendant idéaux pour les processus hybrides papier‑numérique.  
- **Intégration de systèmes hérités** – Les scanners de code‑barres existants peuvent lire les étiquettes sans logiciel supplémentaire.  
- **Pistes d’audit** – Intégrez des ID de transaction ou des horodatages que les auditeurs peuvent vérifier instantanément.  

Évitez les signatures de code‑barres pour les contrats légaux, les documents à haute sécurité ou les échanges avec des partenaires externes où des signatures numériques basées sur PKI sont requises.

## Configurer GroupDocs.Signature pour Java
### Définition de la classe principale
La classe `Signature` est le point d’entrée pour toutes les opérations de signature, vérification, recherche, mise à jour et suppression dans GroupDocs.Signature.

```java
import com.groupdocs.signature.Signature;
```

### Initialisation de base
Créez un objet `Signature` qui pointe vers le fichier cible :

```java
Signature signature = new Signature("path/to/your/document.pdf");
```

**Notes importantes**
- Les chemins peuvent être absolus ou relatifs ; utilisez `System.getProperty("user.home")` pour une compatibilité multiplateforme.  
- GroupDocs prend en charge **plus de 30 formats d’entrée et de sortie**, dont PDF, DOCX, XLSX, PPTX et PNG.  
- Libérez toujours les ressources avec `signature.dispose()` ou un bloc try‑with‑resources :

```java
try (Signature signature = new Signature("path/to/your/document.pdf")) {
    // Your signing operations here
} catch (Exception e) {
    System.err.println("Error working with document: " + e.getMessage());
}
```

Vous êtes maintenant prêt à ajouter des code‑barres.

## Comment ajouter un code‑barres à un PDF en Java ?
Chargez le PDF source avec `new Signature("input.pdf")`, configurez un objet `BarcodeSignature` (par exemple Code128 avec le texte « John Smith »), et appelez `sign` pour produire le fichier signé – le tout en trois lignes de code concises. Cette approche vous permet d’intégrer une étiquette lisible par machine tout en conservant la mise en page du document original, et elle fonctionne pour tout format supporté, pas seulement les PDF.

### Implémentation étape par étape
#### 1. Définir les chemins de fichiers
Définissez les emplacements des fichiers source et de sortie :

```java
String filePath = "YOUR_DOCUMENT_DIRECTORY/sample.docx";
String outputFilePath = "YOUR_OUTPUT_DIRECTORY/signed_sample.docx";
```

#### 2. Créer le gestionnaire de signature
Initialisez le gestionnaire avec le document source :

```java
Signature signature = new Signature(filePath);
```

#### 3. Configurer les options du code‑barres
Un objet `BarcodeSignature` définit les propriétés visuelles et de données du code‑barres à intégrer. Définissez le type de code‑barres, le texte encodé, la position, la taille, la couleur et la police lisible optionnelle :

```java
BarcodeSignOptions signOptions = new BarcodeSignOptions("John Smith", BarcodeTypes.Code128);
signOptions.setVerticalAlignment(VerticalAlignment.Top);
signOptions.setHorizontalAlignment(HorizontalAlignment.Center);
signOptions.setWidth(100);
signOptions.setHeight(40);
signOptions.setMargin(new java.awt.Rectangle(20, 20, 0, 0));
signOptions.setForeColor(Color.RED);

SignatureFont signatureFont = new SignatureFont();
signatureFont.setSize(12);
signatureFont.setFamilyName("Comic Sans MS");
signOptions.setFont(signatureFont);
```

> **Astuce :** Si la chaîne encodée dépasse 20 caractères, augmentez la largeur du code‑barres pour éviter les erreurs de lecture.

#### 4. Appliquer la signature
Exécutez l’opération de signature et générez le fichier de sortie :

```java
signature.sign(outputFilePath, signOptions);
```

#### 5. Exemple réel
Dans un système d’approbation de factures, vous pourriez intégrer l’ID employé de l’approbateur et un horodatage :

```java
String invoiceId = "INV-2025-0042";
String approver = "john.smith@company.com";
String timestamp = LocalDateTime.now().toString();

// Combine into barcode data
String barcodeData = invoiceId + "|" + approver + "|" + timestamp;

BarcodeSignOptions signOptions = new BarcodeSignOptions(barcodeData, BarcodeTypes.QR);
signOptions.setVerticalAlignment(VerticalAlignment.Bottom);
signOptions.setHorizontalAlignment(HorizontalAlignment.Right);

signature.sign(outputFilePath, signOptions);
```

Le PDF résultant porte désormais un code‑barres scannable qui encode toutes les métadonnées d’approbation nécessaires.

## Comment vérifier une signature de code‑barres dans un document Java ?
La méthode `Signature.verify` vérifie un document à la recherche de signatures de code‑barres correspondantes selon les options fournies, renvoyant un booléen indiquant si le code‑barres attendu est présent. La vérification est utile pour les flux de travail automatisés où vous devez confirmer qu’un document a été traité par la bonne partie avant d’autres actions.

### Étapes de vérification
#### 1. Charger le document signé

```java
Signature signature = new Signature("YOUR_OUTPUT_DIRECTORY/signed_sample.docx");
```

#### 2. Définir les critères de vérification
Définissez le texte exact, le format du code‑barres et le numéro de page attendus :

```java
BarcodeVerifyOptions verifyOptions = new BarcodeVerifyOptions();
verifyOptions.setAllPages(false); // Only check the first page
verifyOptions.setPageNumber(1);
verifyOptions.setEncodeType(BarcodeTypes.Code128);
verifyOptions.setText("John Smith");
```

#### 3. Exécuter la vérification
Exécutez la vérification et gérez le résultat :

```java
boolean isValid = signature.verify(verifyOptions) != null;

if (isValid) {
    System.out.println("Document signature verified successfully!");
} else {
    System.out.println("Warning: Signature verification failed!");
}
```

> **Modèle courant :** Pour simplement confirmer qu’un *quelconque* code‑barres d’un type donné existe, omettez le filtre `setText` :

```java
BarcodeVerifyOptions flexibleOptions = new BarcodeVerifyOptions();
flexibleOptions.setAllPages(true);
flexibleOptions.setEncodeType(BarcodeTypes.Code128);
// No setText() call = accept any text with this barcode type

boolean hasAnySignature = signature.verify(flexibleOptions) != null;
```

> Ou vérifiez uniquement le format du code‑barres sans vous soucier du contenu :

```java
BarcodeVerifyOptions formatOnly = new BarcodeVerifyOptions();
formatOnly.setEncodeType(BarcodeTypes.QR);
// Confirms a QR code exists, regardless of content
```

> **Avertissement :** La vérification est sensible à la casse et aux espaces ; toujours tronquer et normaliser les données avant de signer.

## Comment rechercher des signatures de code‑barres dans un document ?
La méthode `Signature.search` parcourt un document à la recherche de signatures de code‑barres correspondant aux `BarcodeSearchOptions` fournies, renvoyant une collection incluant l’emplacement, le numéro de page et la valeur encodée de chaque code‑barres. Cette capacité permet l’extraction massive de métadonnées sans ouvrir chaque fichier manuellement.

### Flux de recherche
#### 1. Initialiser la recherche

```java
Signature signature = new Signature("YOUR_OUTPUT_DIRECTORY/signed_sample.docx");
```

#### 2. Configurer les paramètres de recherche
Spécifiez la plage de pages, le type de code‑barres ou les filtres de texte :

```java
BarcodeSearchOptions searchOptions = new BarcodeSearchOptions();
searchOptions.setAllPages(true); // Search the entire document
```

Optionnellement, restreignez la recherche pour améliorer les performances :

```java
BarcodeSearchOptions narrowSearch = new BarcodeSearchOptions();
narrowSearch.setAllPages(false);
narrowSearch.setPageNumber(1); // Only search page 1
narrowSearch.setEncodeType(BarcodeTypes.Code128); // Only find Code128 barcodes
```

#### 3. Exécuter la recherche

```java
java.util.List<BarcodeSignature> signatures = signature.search(BarcodeSignature.class, searchOptions);

System.out.println("Found " + signatures.size() + " barcode signature(s)");

for (BarcodeSignature bcSignature : signatures) {
    System.out.println("Barcode Type: " + bcSignature.getEncodeType().getTypeName());
    System.out.println("Text: " + bcSignature.getText());
    System.out.println("Position: (" + bcSignature.getLeft() + ", " + bcSignature.getTop() + ")");
    System.out.println("Size: " + bcSignature.getWidth() + "x" + bcSignature.getHeight());
    System.out.println("---");
}
```

#### 4. Exemple d’extraction de données
Extrayez les données d’approbation de chaque code‑barres d’un lot de factures :

```java
List<BarcodeSignature> foundSignatures = signature.search(BarcodeSignature.class, searchOptions);

for (BarcodeSignature sig : foundSignatures) {
    String barcodeData = sig.getText();
    
    // Parse your custom format (remember our invoice example?)
    String[] parts = barcodeData.split("\\|");
    if (parts.length == 3) {
        String invoiceId = parts[0];
        String approver = parts[1];
        String timestamp = parts[2];
        
        System.out.println("Invoice " + invoiceId + " approved by " + approver + " at " + timestamp);
    }
}
```

> **Conseil de performance :** Pour les documents de plus de 100 pages, limitez toujours la recherche aux pages contenant réellement des code‑barres ; cela peut réduire le temps d’exécution jusqu’à **70 %**.

## Comment mettre à jour une signature de code‑barres existante ?
La méthode `Signature.update` modifie les attributs visuels d’une signature de code‑barres existante — comme la position, la taille ou la couleur — tout en préservant les données encodées d’origine. Cela est pratique lorsque des changements de mise en page sont nécessaires après que le document a déjà été signé.

### Procédure de mise à jour
#### 1. Trouver les signatures à mettre à jour

```java
Signature signature = new Signature("YOUR_OUTPUT_DIRECTORY/signed_sample.docx");

BarcodeSearchOptions searchOptions = new BarcodeSearchOptions();
searchOptions.setAllPages(true);

List<BarcodeSignature> signatures = signature.search(BarcodeSignature.class, searchOptions);
```

#### 2. Modifier les propriétés souhaitées

```java
List<BarcodeSignature> signaturesToUpdate = new ArrayList<>();

if (!signatures.isEmpty()) {
    BarcodeSignature bcSignature = signatures.get(0); // Update the first found signature
    
    // Move it 100px right and 100px down
    bcSignature.setLeft(bcSignature.getLeft() + 100);
    bcSignature.setTop(bcSignature.getTop() + 100);
    
    // Make it bigger
    bcSignature.setWidth(200);
    bcSignature.setHeight(50);
    
    signaturesToUpdate.add(bcSignature);
}
```

Vous pouvez changer plusieurs attributs à la fois :

```java
bcSignature.setLeft(50);
bcSignature.setTop(50);
bcSignature.setWidth(150);
bcSignature.setHeight(45);
// Note: You can't change the encoded text or barcode type with update
// For that, you'd need to delete and re-sign
```

#### 3. Enregistrer les modifications

```java
ByteArrayOutputStream outputStream = new ByteArrayOutputStream();
signature.update(outputStream, signaturesToUpdate);

// If you want to save to a file instead:
// signature.update("path/to/updated_document.docx", signaturesToUpdate);
```

#### 4. Scénario réel
Repositionnez toutes les signatures pour éviter qu’elles ne chevauchent un nouveau logo d’entreprise ajouté :

```java
List<BarcodeSignature> allSignatures = signature.search(BarcodeSignature.class, searchOptions);
List<BarcodeSignature> toUpdate = new ArrayList<>();

for (BarcodeSignature sig : allSignatures) {
    // Move all signatures down by 50px to clear space for new logo
    if (sig.getTop() < 100) {
        sig.setTop(sig.getTop() + 50);
        toUpdate.add(sig);
    }
}

if (!toUpdate.isEmpty()) {
    signature.update(outputStream, toUpdate);
    System.out.println("Repositioned " + toUpdate.size() + " signature(s)");
}
```

> **Limitation :** Modifier le texte encodé nécessite la suppression et l’insertion d’une nouvelle signature.

## Comment supprimer des signatures de code‑barres d’un document ?
La méthode `Signature.delete` supprime définitivement les signatures de code‑barres sélectionnées d’un document, effaçant à la fois l’élément visuel et ses données encodées. Utilisez cette opération lors du nettoyage de signatures de test ou lorsqu’un code‑barres n’est plus pertinent.

### Étapes de suppression
#### 1. Localiser les signatures

```java
Signature signature = new Signature("YOUR_OUTPUT_DIRECTORY/signed_sample.docx");

BarcodeSearchOptions searchOptions = new BarcodeSearchOptions();
searchOptions.setAllPages(true);

List<BarcodeSignature> signatures = signature.search(BarcodeSignature.class, searchOptions);
```

#### 2. Supprimer les signatures sélectionnées

```java
List<BarcodeSignature> signaturesToDelete = new ArrayList<>();

// Delete all Code128 signatures (for example)
for (BarcodeSignature sig : signatures) {
    if (sig.getEncodeType().equals(BarcodeTypes.Code128)) {
        signaturesToDelete.add(sig);
    }
}

if (!signaturesToDelete.isEmpty()) {
    boolean result = signature.delete(signaturesToDelete);
    
    if (result) {
        System.out.println("Successfully deleted " + signaturesToDelete.size() + " signature(s)");
    } else {
        System.err.println("Failed to delete signatures");
    }
}
```

#### 3. Exemple de suppression conditionnelle
Supprimez uniquement les code‑barres plus anciens qu’un horodatage spécifique (en supposant que l’horodatage fait partie du texte encodé) :

```java
LocalDateTime cutoffDate = LocalDateTime.now().minusDays(30);
List<BarcodeSignature> outdatedSignatures = new ArrayList<>();

for (BarcodeSignature sig : signatures) {
    try {
        String text = sig.getText();
        // Assuming format like "data|timestamp"
        String[] parts = text.split("\\|");
        if (parts.length > 1) {
            LocalDateTime sigDate = LocalDateTime.parse(parts[1]);
            if (sigDate.isBefore(cutoffDate)) {
                outdatedSignatures.add(sig);
            }
        }
    } catch (Exception e) {
        // Skip signatures that don't match our format
        continue;
    }
}

if (!outdatedSignatures.isEmpty()) {
    signature.delete(outdatedSignatures);
    System.out.println("Removed " + outdatedSignatures.size() + " outdated signature(s)");
}
```

> **Attention :** La suppression ne peut pas être annulée ; travaillez toujours sur une copie des fichiers de production lors des tests.

#### 4. Modèle de suppression par lot
Nettoyez les signatures de test avant une version :

```java
// Remove all signatures containing "TEST" in their text
List<BarcodeSignature> testSignatures = signatures.stream()
    .filter(sig -> sig.getText().toUpperCase().contains("TEST"))
    .collect(Collectors.toList());

if (!testSignatures.isEmpty()) {
    signature.delete(testSignatures);
    System.out.println("Cleaned up " + testSignatures.size() + " test signature(s)");
}
```

## Types de code‑barres : guide pratique
Choisir le bon code‑barres impacte la fiabilité de la lecture, la capacité de données et la compatibilité avec les imprimantes.

### Code128 (choix le plus courant)
- **Quand l’utiliser :** Données alphanumériques, haute densité, documents imprimés.  
- **Avantages :** Compact, fonctionne avec les scanners standards, s’imprime clairement à petite taille.  
- **Inconvénients :** Limité à l’ASCII, moins résistant aux erreurs que les codes 2‑D.

```java
BarcodeSignOptions code128 = new BarcodeSignOptions("INV-2025-042", BarcodeTypes.Code128);
```

### QR Code (idéal pour le mobile)
- **Quand l’utiliser :** Scan mobile, gros volumes de données (URL, JSON, etc.), documents susceptibles d’être endommagés.  
- **Avantages :** Jusqu’à 4 000 caractères, correction d’erreurs intégrée, compatible smartphone.  
- **Inconvénients :** Empreinte visuelle plus grande, nécessite une résolution plus élevée pour les petites tailles.

```java
String jsonData = "{\"invoice\":\"INV-042\",\"amount\":1500.00,\"approver\":\"john@company.com\"}";
BarcodeSignOptions qrCode = new BarcodeSignOptions(jsonData, BarcodeTypes.QR);
```

### Code39 (ancien fiable)
- **Quand l’utiliser :** Environnements de scanners hérités, besoin de texte lisible par l’homme.  
- **Avantages :** Large support hérité, format simple, pas de somme de contrôle requise.  
- **Inconvénients :** Faible densité de données, jeu de caractères limité, occupe plus d’espace.

### Data Matrix (puissant et compact)
- **Quand l’utiliser :** Espace extrêmement limité, marquage d’objets minuscules, données à haute densité.  
- **Avantages :** Très compact, forte correction d’erreurs, fonctionne sur des surfaces courbes.  
- **Inconvénients :** Nécessite une impression de haute qualité, support de scanner moins répandu.

#### Comparaison rapide
| Type de code‑barres | Capacité de données | Idéal pour | Taille typique |
|---------------------|---------------------|------------|----------------|
| Code128             | ~100 caractères     | Étiquetage à usage général | Petit |
| QR Code             | ~4 000 caractères   | Scan mobile, données riches | Moyen |
| Code39              | ~43 caractères      | Matériel hérité | Grand |
| Data Matrix         | ~3 000 caractères   | Espaces minuscules, tags industriels | Très petit |

**Recommandation :** Commencez avec **Code128** pour des ID simples. Passez à **QR** lorsque vous devez intégrer des URL ou des charges utiles plus importantes. Utilisez **Code39** uniquement pour les intégrations héritées.

## Problèmes courants & solutions
### Problème : « Code‑barres introuvable lors de la vérification »
**Symptômes :** La vérification renvoie `false` même si le code‑barres est visible.  
**Causes typiques**
1. Différence de casse (par ex., « John Smith » vs. « john smith »).  
2. Espaces supplémentaires dans le texte encodé.  
3. Type de code‑barres incorrect spécifié dans les options de vérification.  
4. Recherche du mauvais numéro de page.  

**Solution :** Normalisez le texte avant la signature et la vérification, et assurez‑vous que `setEncodeType` correspond au type original.

```java
// Always normalize your data
String signatureText = originalText.trim().toLowerCase();

// When signing:
BarcodeSignOptions signOptions = new BarcodeSignOptions(signatureText, BarcodeTypes.Code128);

// When verifying:
BarcodeVerifyOptions verifyOptions = new BarcodeVerifyOptions();
verifyOptions.setText(signatureText); // Use the same normalized text
verifyOptions.setEncodeType(BarcodeTypes.Code128);
```

### Problème : « Le code‑barres apparaît flou ou illisible »
**Symptômes :** Les code‑barres imprimés ne peuvent pas être scannés.  
**Causes**
- Dimensions du code‑barres trop petites pour les données encodées.  
- Paramètres d’imprimante à basse résolution.  
- Contraste insuffisant entre la couleur du code‑barres et le fond.  

**Solution :** Augmentez la largeur/hauteur du code‑barres, utilisez des couleurs à fort contraste (noir sur blanc) et réglez le DPI de l’imprimante à au moins 300 dpi.

```java
// Increase size for longer strings
int dataLength = barcodeText.length();
int minWidth = Math.max(100, dataLength * 10); // 10px per character minimum

BarcodeSignOptions signOptions = new BarcodeSignOptions(barcodeText, BarcodeTypes.Code128);
signOptions.setWidth(minWidth);
signOptions.setHeight(60); // Taller = easier to scan

// Use high-contrast colors
signOptions.setForeColor(Color.BLACK); // Black on white is most reliable
signOptions.setBackColor(Color.WHITE);
```

### Problème : « OutOfMemoryError avec de gros documents »
**Symptômes :** L’application plante lors du traitement de PDF contenant des centaines de pages.  
**Cause :** La bibliothèque charge l’ensemble du document en mémoire.  
**Solution :** Activez le mode flux et traitez les pages de façon incrémentale.

```java
// Process pages in batches instead of all at once
BarcodeSearchOptions searchOptions = new BarcodeSearchOptions();
searchOptions.setAllPages(false);

List<BarcodeSignature> allSignatures = new ArrayList<>();

for (int page = 1; page <= totalPages; page++) {
    searchOptions.setPageNumber(page);
    List<BarcodeSignature> pageSignatures = signature.search(BarcodeSignature.class, searchOptions);
    allSignatures.addAll(pageSignatures);
    
    // Process and clear as you go
    if (page % 10 == 0) {
        System.gc(); // Suggest garbage collection every 10 pages
    }
}
```

### Problème : « Position de la signature incohérente selon le type de document »
**Symptômes :** Les code‑barres apparaissent à des emplacements différents lors de la signature de PDF vs. documents Word.  
**Cause :** Le PDF utilise une origine en bas à gauche, tandis que Word utilise une origine en haut à gauche.  
**Solution :** Détectez le type de document et appliquez la transformation de coordonnées appropriée.

```java
// Use relative positioning instead of absolute
signOptions.setVerticalAlignment(VerticalAlignment.Bottom);
signOptions.setHorizontalAlignment(HorizontalAlignment.Right);

// Then use margins for fine-tuning
Padding margin = new Padding();
margin.setRight(50); // 50px from right edge
margin.setBottom(50); // 50px from bottom
signOptions.setMargin(margin);

// This works consistently across PDF, DOCX, XLSX, etc.
```

### Problème : « Les signatures mises à jour perdent le formatage »
**Symptômes :** Après l’appel à `update`, la couleur ou la police du code‑barres change de façon inattendue.  
**Cause :** Toutes les propriétés visuelles ne sont pas conservées lors d’une opération de mise à jour.  
**Solution :** Réappliquez les paramètres visuels après l’appel à `update`.

```java
// When updating, explicitly set all visual properties
bcSignature.setLeft(newLeft);
bcSignature.setTop(newTop);
bcSignature.setWidth(originalWidth); // Don't forget these!
bcSignature.setHeight(originalHeight);
// Note: Color and font can't be updated - you'd need to delete and re-sign
```

## Bonnes pratiques pour la production
### Optimisation des performances
1. **Réutiliser les instances Signature** – Créez un seul objet `Signature` par document et réutilisez‑le pour plusieurs opérations.

```java
// Bad - Creates new instance each time
public void processDocument(String path) {
    Signature sig1 = new Signature(path);
    sig1.search(/* ... */);
    
    Signature sig2 = new Signature(path); // Unnecessary reload
    sig2.verify(/* ... */);
}

// Good - Reuse the same instance
public void processDocument(String path) {
    try (Signature signature = new Signature(path)) {
        signature.search(/* ... */);
        signature.verify(/* ... */);
        signature.update(/* ... */);
    }
}
```

2. **Rechercher uniquement les pages spécifiques** – Limitez la plage de pages à celles où les code‑barres sont attendus.

```java
// Slow for 100+ page documents
BarcodeSearchOptions slowSearch = new BarcodeSearchOptions();
slowSearch.setAllPages(true);

// Fast - only check where signatures actually are
BarcodeSearchOptions fastSearch = new BarcodeSearchOptions();
fastSearch.setAllPages(false);
fastSearch.setPageNumber(1); // Only check cover page
```

3. **Choisir le type de code‑barres le plus simple** – Les code‑barres plus simples se génèrent plus rapidement ; n’utilisez QR ou Data Matrix que lorsque vous avez réellement besoin de la capacité supplémentaire.

```java
// Overkill for simple IDs
BarcodeSignOptions slow = new BarcodeSignOptions("12345", BarcodeTypes.QR);

// Faster and more appropriate
BarcodeSignOptions fast = new BarcodeSignOptions("12345", BarcodeTypes.Code128);
```

### Considérations de sécurité
1. **Ne jamais encoder de données personnelles sensibles** – Les code‑barres sont facilement lisibles ; évitez les informations personnelles identifiables (PII) telles que les numéros de sécurité sociale ou les mots de passe.

```java
// Bad - exposes sensitive data
String barcodeData = "SSN:123-45-6789|Password:hunter2";

// Good - use reference IDs
String barcodeData = "USER-REF-7721X"; // Look up sensitive data server-side
```

2. **Valider côté serveur** – Ne faites jamais confiance uniquement à la vérification côté client ; re‑vérifiez toujours sur un backend de confiance.

```java
// Client scans barcode and extracts "APPROVED-BY-ADMIN"
// Always verify server-side:
public boolean verifyApproval(String documentId, String scannedData) {
    // Load document from secure storage
    Signature signature = new Signature(getSecureDocument(documentId));
    
    BarcodeVerifyOptions verifyOptions = new BarcodeVerifyOptions();
    verifyOptions.setText(scannedData);
    
    boolean isValid = signature.verify(verifyOptions) != null;
    
    // Also check against your database
    boolean isInDatabase = checkApprovalDatabase(documentId, scannedData);
    
    return isValid && isInDatabase;
}
```

3. **Ajouter des horodatages** – Incluez un horodatage dans la charge du code‑barres pour prévenir les attaques de rejeu.

```java
import java.time.LocalDateTime;
import java.time.temporal.ChronoUnit;

String timestamp = LocalDateTime.now().truncatedTo(ChronoUnit.SECONDS).toString();
String barcodeData = "APPROVAL|" + userId + "|" + timestamp;

// When verifying, check the timestamp isn't too old
public boolean isSignatureRecent(String barcodeData, int maxAgeHours) {
    String[] parts = barcodeData.split("\\|");
    if (parts.length < 3) return false;
    
    LocalDateTime signatureTime = LocalDateTime.parse(parts[2]);
    LocalDateTime now = LocalDateTime.now();
    
    long hoursSince = ChronoUnit.HOURS.between(signatureTime, now);
    return hoursSince <= maxAgeHours;
}
```

### Modèles de gestion des erreurs
- **Utilisez toujours try‑with‑resources** pour garantir que les objets `Signature` sont libérés.

```java
try (Signature signature = new Signature(documentPath)) {
    // Your operations here
    signature.sign(outputPath, signOptions);
} catch (Exception e) {
    logger.error("Failed to sign document: " + documentPath, e);
    throw new DocumentSigningException("Could not process document", e);
}
```

- **Validez l’accès aux fichiers** avant d’essayer de signer.

```java
public void signDocument(String inputPath, String outputPath) {
    File inputFile = new File(inputPath);
    
    if (!inputFile.exists()) {
        throw new IllegalArgumentException("Input file not found: " + inputPath);
    }
    
    if (!inputFile.canRead()) {
        throw new SecurityException("Cannot read input file: " + inputPath);
    }
    
    File outputDir = new File(outputPath).getParentFile();
    if (outputDir != null && !outputDir.exists()) {
        outputDir.mkdirs();
    }
    
    try (Signature signature = new Signature(inputPath)) {
        signature.sign(outputPath, signOptions);
    }
}
```

- **Synchronisez l’accès** si plusieurs threads peuvent travailler sur le même fichier.

```java
import java.util.concurrent.locks.ReentrantLock;
import java.util.concurrent.ConcurrentHashMap;

public class SignatureManager {
    private final ConcurrentHashMap<String, ReentrantLock> documentLocks = new ConcurrentHashMap<>();
    
    public void signDocument(String documentPath, BarcodeSignOptions options) {
        ReentrantLock lock = documentLocks.computeIfAbsent(documentPath, k -> new ReentrantLock());
        
        lock.lock();
        try (Signature signature = new Signature(documentPath)) {
            signature.sign(documentPath + ".signed", options);
        } finally {
            lock.unlock();
        }
    }
}
```

### Tester votre implémentation
**Modèle de test unitaire**

```java
import org.junit.jupiter.api.Test;
import org.junit.jupiter.api.io.TempDir;
import static org.junit.jupiter.api.Assertions.*;

public class BarcodeSignatureTest {
    
    @TempDir
    Path tempDir;
    
    @Test
    public void testSignAndVerify() throws Exception {
        // Setup
        String testDoc = "test-document.pdf";
        String outputDoc = tempDir.resolve("signed-test.pdf").toString();
        String testData = "TEST-USER-12345";
        
        // Sign
        try (Signature signature = new Signature(testDoc)) {
            BarcodeSignOptions signOptions = new BarcodeSignOptions(testData, BarcodeTypes.Code128);
            signature.sign(outputDoc, signOptions);
        }
        
        // Verify
        try (Signature signature = new Signature(outputDoc)) {
            BarcodeVerifyOptions verifyOptions = new BarcodeVerifyOptions();
            verifyOptions.setText(testData);
            verifyOptions.setEncodeType(BarcodeTypes.Code128);
            
            boolean isValid = signature.verify(verifyOptions) != null;
            assertTrue(isValid, "Signature should be valid");
        }
    }
    
    @Test
    public void testSearchFindsSignature() throws Exception {
        String signedDoc = "signed-document.pdf";
        
        try (Signature signature = new Signature(signedDoc)) {
            BarcodeSearchOptions searchOptions = new BarcodeSearchOptions();
            searchOptions.setAllPages(true);
            
            List<BarcodeSignature> signatures = signature.search(BarcodeSignature.class, searchOptions);
            
            assertFalse(signatures.isEmpty(), "Should find at least one signature");
            assertEquals("TEST-USER-12345", signatures.get(0).getText());
        }
    }
}
```

**Checklist d’intégration**
- ✅ Tester tous les formats supportés (PDF, DOCX, XLSX, PPTX, PNG).  
- ✅ Vérifier que les code‑barres survivent à un cycle impression‑numérisation.  
- ✅ Effectuer un test de charge avec des chaînes de données de longueur maximale.  
- ✅ Confirmer le positionnement sur les tailles de page A4, Letter et personnalisées.  
- ✅ Exécuter des signatures concurrentes sur plusieurs documents.  
- ✅ Surveiller l’utilisation de la mémoire pour les documents > 500 pages.  
- ✅ S’assurer que les scanners de code‑barres lisent correctement la sortie.

### Journalisation et surveillance
Ajoutez des journaux pertinents autour de chaque opération :

```java
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

public class DocumentSigningService {
    private static final Logger logger = LoggerFactory.getLogger(DocumentSigningService.class);
    
    public void signDocument(String docPath, String barcodeData) {
        logger.info("Starting signature process for document: {}", docPath);
        logger.debug("Barcode data length: {} characters", barcodeData.length());
        
        try (Signature signature = new Signature(docPath)) {
            BarcodeSignOptions options = new BarcodeSignOptions(barcodeData, BarcodeTypes.Code128);
            
            long startTime = System.currentTimeMillis();
            signature.sign(docPath + ".signed", options);
            long duration = System.currentTimeMillis() - startTime;
            
            logger.info("Successfully signed document in {}ms", duration);
        } catch (Exception e) {
            logger.error("Failed to sign document: {}", docPath, e);
            throw new RuntimeException("Signature operation failed", e);
        }
    }
}
```

Suivez les métriques clés comme le temps de traitement, la consommation mémoire et les taux d’erreur :

```java
// Track success/failure rates
metricsService.incrementCounter("signature.sign.success");
metricsService.incrementCounter("signature.verify.failure");

// Track performance
metricsService.recordTimer("signature.sign.duration", duration);

// Track document sizes
metricsService.recordHistogram("signature.document.pages", pageCount);
```

## Astuces pro tirées de l’utilisation réelle
**Stratégie de traitement par lots**
Lors du traitement de centaines de fichiers, traitez‑les par lots et indiquez la progression :

```java
public void signBatch(List<String> documents, String barcodePrefix) {
    int total = documents.size();
    int completed = 0;
    int failed = 0;
    
    for (String docPath : documents) {
        try {
            String barcodeData = barcodePrefix + "-" + UUID.randomUUID().toString();
            signDocument(docPath, barcodeData);
            completed++;
            
            if (completed % 10 == 0) {
                logger.info("Progress: {}/{} documents signed", completed, total);
            }
        } catch (Exception e) {
            failed++;
            logger.warn("Failed to sign: {}", docPath, e);
        }
    }
    
    logger.info("Batch complete: {} succeeded, {} failed", completed, failed);
}
```

**Externaliser la configuration**
Stockez les paramètres du code‑barres (type, taille, couleur) dans un fichier de propriétés pour un réglage facile sans recompilation :

```java
public class BarcodeConfig {
    private int defaultWidth = 100;
    private int defaultHeight = 40;
    private String defaultBarcodeType = "Code128";
    private String defaultColor = "BLACK";
    
    // Load from properties file or environment variables
    public BarcodeConfig() {
        this.defaultWidth = Integer.parseInt(
            System.getProperty("barcode.width", "100")
        );
        // ... load other properties
    }
    
    public BarcodeSignOptions createDefaultOptions(String text) {
        BarcodeSignOptions options = new BarcodeSignOptions(text, getBarcodeType());
        options.setWidth(defaultWidth);
        options.setHeight(defaultHeight);
        options.setForeColor(getColor());
        return options;
    }
}
```

**Standardiser la charge du code‑barres**
Utilisez un format délimité comme `EMPID|TIMESTAMP|DOCID` pour rendre l’analyse simple et cohérente :

```java
public class BarcodeDataBuilder {
    private String userId;
    private String action;
    private LocalDateTime timestamp;
    private String documentId;
    
    public BarcodeDataBuilder setUserId(String userId) {
        this.userId = userId;
        return this;
    }
    
    public BarcodeDataBuilder setAction(String action) {
        this.action = action;
        return this;
    }
    
    public BarcodeDataBuilder setDocumentId(String documentId) {
        this.documentId = documentId;
        return this;
    }
    
    public String build() {
        this.timestamp = LocalDateTime.now();
        
        // Format: VERSION|USER|ACTION|DOC_ID|TIMESTAMP|CHECKSUM
        String data = String.join("|",
            "v1",
            userId,
            action,
            documentId,
            timestamp.toString()
        );
        
        // Add simple checksum
        int checksum = data.hashCode();
        return data + "|" + checksum;
    }
    
    public static ParsedBarcodeData parse(String barcodeData) {
        String[] parts = barcodeData.split("\\|");
        if (parts.length != 6 || !parts[0].equals("v1")) {
            throw new IllegalArgumentException("Invalid barcode format");
        }
        
        return new ParsedBarcodeData(parts[1], parts[2], parts[3], 
                                     LocalDateTime.parse(parts[4]));
    }
}

// Usage:
String barcodeData = new BarcodeDataBuilder()
    .setUserId("john.smith")
    .setAction("APPROVED")
    .setDocumentId("INV-2025-042")
    .build();
```

**Détecter automatiquement le type de document**
Ajustez les dimensions du code‑barres selon que la cible est un PDF, Word ou une image :

```java
public BarcodeSignOptions getOptimalOptions(String documentPath, String text) {
    String extension = documentPath.substring(documentPath.lastIndexOf(".") + 1).toLowerCase();
    
    BarcodeSignOptions options = new BarcodeSignOptions(text, BarcodeTypes.Code128);
    
    switch (extension) {
        case "pdf":
            // PDFs can handle larger, detailed barcodes
            options.setWidth(150);
            options.setHeight(50);
            break;
        case "docx":
        case "doc":
            // Word docs need compact signatures that don't disrupt flow
            options.setWidth(100);
            options.setHeight(35);
            options.setVerticalAlignment(VerticalAlignment.Bottom);
            break;
        case "xlsx":
        case "xls":
            // Excel needs signatures that don't obscure data
            options.setWidth(80);
            options.setHeight(30);
            options.setHorizontalAlignment(HorizontalAlignment.Right);
            break;
        default:
            // Safe defaults
            options.setWidth(100);
            options.setHeight(40);
    }
    
    return options;
}
```

## Ressources supplémentaires
- [Documentation GroupDocs.Signature](https://docs.groupdocs.com/signature/java/) – Guide complet de l’API et exemples d’utilisation.  
- [Forum de support GroupDocs](https://forum.groupdocs.com/c/signature/13) – Aide communautaire et dépannage.  
- [Référence API](https://apireference.groupdocs.com/signature/java) – Signatures de méthodes détaillées et descriptions des paramètres.

## Questions fréquemment posées
**Q : Puis‑je utiliser GroupDocs.Signature avec Java 17 ?**  
R : Oui – la bibliothèque est entièrement compatible avec JDK 8, 11 et 17.  

**Q : Le code‑barres survit‑il à un cycle impression‑numérisation ?**  
R : Lorsque vous utilisez Code128 ou QR avec une taille et un contraste suffisants, le code‑barres reste scannable après impression et numérisation.  

**Q : Combien de code‑barres un document unique peut‑il contenir ?**  
R : Il n’y a pas de limite stricte ; toutefois, pour des performances optimales, maintenez le nombre total en dessous de **200** par document.  

**Q : Une licence est‑elle requise pour les builds de développement ?**  
R : Une licence temporaire supprime les filigranes d’évaluation ; une licence complète est obligatoire pour tout déploiement en production.  

**Q : Puis‑je signer des PDF protégés par mot de passe ?**  
R : Oui – fournissez le mot de passe lors de la création de l’objet `Signature` ; l’API déverrouillera le fichier en interne.  

**Dernière mise à jour :** 2026-07-15  
**Testé avec :** GroupDocs.Signature 23.9 pour Java  
**Auteur :** GroupDocs  

{< /blocks/products/pf/tutorial-page-section >}
{< /blocks/products/pf/main-container >}
{< /blocks/products/pf/main-wrap-class >}
{< blocks/products/products-backtop-button >}

## Tutoriels associés

- [Comment vérifier les signatures de code‑barres en Java avec GroupDocs.Signature](/signature/java/search-verification/groupdocs-signature-java-document-verification/)
- [Comment rechercher des signatures numériques dans des documents Java avec GroupDocs](/signature/java/search-verification/groupdocs-signature-java-digital-search-tutorial/)
- [Tutoriel de signature de code‑barres Java – Ajouter, vérifier et gérer les code‑barres dans les PDF](/signature/java/barcode-signatures/)