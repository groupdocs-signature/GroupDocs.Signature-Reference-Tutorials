---
categories:
- Java PDF Processing
date: '2026-07-20'
description: Apprenez à créer une signature barcode dans des documents PDF en utilisant
  Java et GroupDocs.Signature. Tutoriel étape par étape avec des exemples de code
  et les meilleures pratiques.
keywords:
- create barcode signature
- how to add barcode
- generate code128 barcode
- add barcode pdf
- tamper evident barcode
lastmod: '2026-07-20'
linktitle: Créer une signature barcode en Java
og_description: Créez une signature barcode dans un PDF avec Java et GroupDocs.Signature.
  Apprenez étape par étape comment ajouter des codes-barres Code128, les positionner
  et sécuriser les documents.
og_image_alt: 'Developer guide: Create barcode signature in PDF using Java and GroupDocs'
og_title: Créer une signature barcode dans un PDF avec Java – Guide complet
schemas:
- author: GroupDocs
  dateModified: '2026-07-20'
  description: Learn how to create barcode signature in PDF documents using Java and
    GroupDocs.Signature. Step-by-step tutorial with code examples and best practices.
  headline: How to Create Barcode Signature in PDF using Java
  type: TechArticle
- description: Learn how to create barcode signature in PDF documents using Java and
    GroupDocs.Signature. Step-by-step tutorial with code examples and best practices.
  name: How to Create Barcode Signature in PDF using Java
  steps:
  - name: Initialize the Signature object
    text: '**Definition anchor:** The `Signature` class is GroupDocs.Signature''s
      entry point for loading, modifying, and saving PDF documents. First, you need
      to tell GroupDocs which PDF you''re working with: **What''s happening here:**
      The `Signature` object loads your PDF into memory and prepares it for modifi'
  - name: Configure your barcode options (How to add barcode)
    text: '**Definition anchor:** `BarcodeSignOptions` encapsulates all settings required
      to render a barcode inside a PDF. Now let''s create the barcode signature with
      your data: - `"12345678"` is your barcode data — this could be an order ID,
      certificate number, or any identifier you need. - `Code128` is the '
  - name: Position your barcode (How to sign PDF with barcode)
    text: '**Definition anchor:** `SignatureOptions` provides layout properties such
      as page number, size, and alignment. Here''s where GroupDocs really shines —
      percentage‑based positioning means your barcode looks good on any PDF size:
      **Why percentages matter:** Imagine you''re signing both A4 documents and l'
  - name: Sign and save your document (How to add barcode pdf)
    text: 'Time to actually apply the signature and save your work: **Important note:**
      The output directory must exist before you run this code. GroupDocs won''t create
      nested directories for you, so create them first or handle that in your code:
      **What if something goes wrong?** Wrap this in a try‑catch block'
  type: HowTo
- questions:
  - answer: Yes! Call `signature.sign()` multiple times with different `BarcodeSignOptions`
      for each barcode type. Just ensure they don’t overlap.
    question: Can I use different barcode types in the same PDF?
  - answer: Code128 handles most ASCII characters fine. For Unicode or complex data,
      switch to QR codes—they support UTF‑8 encoding.
    question: How do I handle barcodes that contain special characters?
  - answer: Technically up to 128 characters, but readability drops significantly
      above 30‑40 characters. For larger payloads, use QR codes.
    question: What's the maximum data I can store in a Code128 barcode?
  - answer: Not noticeably—barcodes are vector graphics, typically adding only 5‑20
      KB per barcode depending on size and complexity.
    question: Will adding barcodes significantly increase my PDF file size?
  - answer: Yes! Use `options.setRotationAngle(90)` to rotate your barcode, which
      is handy for margin placement.
    question: Can I rotate barcodes or place them vertically?
  type: FAQPage
tags:
- pdf-signing
- barcode-signature
- document-security
- groupdocs
- java
- pdf
title: Comment créer une signature barcode dans un PDF avec Java
type: docs
url: /fr/java/barcode-signatures/java-pdf-signing-barcode-groupdocs/
weight: 1
---

# Comment créer une signature de code‑barres dans un PDF avec Java

Dans ce tutoriel, vous apprendrez comment **créer une signature de code‑barres** dans des fichiers PDF en utilisant Java et GroupDocs.Signature. Les signatures de code‑barres intègrent des identifiants lisibles par machine qui sont à la fois à l'épreuve de la falsification et faciles à scanner — parfaits pour les contrats, certificats, factures et tout document nécessitant une vérification fiable.

## Réponses rapides
- **Qu'est‑ce qu'une signature de code‑barres ?** Un code‑barres intégré dans un PDF qui stocke des données structurées et peut être lu par des scanners ou des logiciels.  
- **Quel type de code‑barres est recommandé ?** Code128, car il gère les données alphanumériques de manière compacte.  
- **Ai‑je besoin d'une licence ?** Un essai gratuit suffit pour les tests — une licence complète est requise pour la production.  
- **Puis‑je positionner le code‑barres sur n'importe quelle taille de page ?** Oui — utilisez le positionnement basé sur les pourcentages pour un redimensionnement automatique.  
- **Le code‑barres est‑il vectoriel ?** Oui, il n'ajoute que quelques kilo‑octets au PDF et reste net à n'importe quelle résolution.  

## Qu'est‑ce qu'une signature de code‑barres ?
Une signature de code‑barres est un code‑barres vectoriel intégré directement dans une page PDF, agissant à la fois comme élément visuel et comme signature cryptographique pouvant être validée ultérieurement. Elle stocke des données structurées, telles que des identifiants ou des horodatages, et assure l'intégrité du document tout en fournissant une référence lisible par machine.

## Pourquoi les signatures de code‑barres sont importantes pour vos PDF
Les signatures de code‑barres offrent aux PDF un identifiant compact et lisible par machine qui peut être scanné instantanément, éliminant la saisie manuelle de données et réduisant les erreurs. Comme elles sont intégrées sous forme de graphiques vectoriels, elles restent nettes à n'importe quelle résolution et n'ajoutent que quelques kilo‑octets au fichier. Cette combinaison de lisibilité, de résistance à la falsification et de taille minimale les rend idéales pour les contrats, factures, certificats et tout document nécessitant une vérification fiable.

Voici un défi que vous avez probablement rencontré : vous devez ajouter des identifiants uniques aux PDF qui soient à la fois lisibles par machine et à l'épreuve de la falsification. Peut‑être travaillez‑vous sur un système de gestion de documents, le traitement de certificats, ou la gestion de contrats nécessitant une vérification ultérieure.

C'est là que les signatures de code‑barres sont utiles. Contrairement aux tampons de texte simples, les codes‑barres vous permettent d'intégrer des données structurées que les scanners (et votre logiciel) peuvent lire instantanément. De plus, lorsque vous les combinez avec la signature PDF via GroupDocs.Signature pour Java, vous obtenez un moyen puissant de suivre et de vérifier les documents sans ajouter de recherches complexes dans une base de données.

Dans ce guide, vous apprendrez exactement comment implémenter des signatures de code‑barres dans vos PDF Java — de la configuration de base au code prêt pour la production avec un positionnement flexible. Que vous construisiez un système de facturation, un générateur de certificats ou une plateforme de gestion de contrats, vous disposerez de tout ce dont vous avez besoin à la fin.

**Ce que vous maîtriserez :**
- Configurer GroupDocs.Signature pour Java en quelques minutes  
- Créer des signatures de code‑barres Code128 (et pourquoi elles sont souvent votre meilleur choix)  
- Positionner les codes‑barres en utilisant des mises en page basées sur les pourcentages qui fonctionnent sur n'importe quelle taille de PDF  
- Éviter les pièges courants qui font trébucher les développeurs  
- Tester correctement votre implémentation  

## Comment créer une signature de code‑barres en Java
Créer une signature de code‑barres en Java implique de charger le PDF cible, de configurer les options du code‑barres telles que les données, le type, la taille et la position, puis d'appliquer la signature pour générer un nouveau document. GroupDocs.Signature gère le rendu et la liaison cryptographique, vous n'avez donc qu'à fournir les paramètres souhaités et à gérer les chemins de fichiers.

## Prérequis et checklist de l'environnement
Avant de commencer, vérifiez que vous avez les éléments suivants prêts :
- **Java Development Kit (JDK) 8 ou plus récent** – requis pour toutes les bibliothèques GroupDocs Java.  
- **Maven ou Gradle** – pour gérer la dépendance GroupDocs.Signature.  
- **Un IDE** tel qu'IntelliJ IDEA, Eclipse ou VS Code avec les extensions Java.  
- **GroupDocs.Signature pour Java** (la version 23.12 ou plus récente est recommandée).  
- **Connaissances de base en Java** – vous devez être à l'aise avec la création de classes, la gestion des exceptions et la manipulation des I/O de fichiers.  

## Configurer GroupDocs.Signature dans votre projet
Intégrer la bibliothèque dans votre projet est simple. Choisissez votre outil de construction :

**Pour les utilisateurs Maven**, ajoutez cette dépendance à votre `pom.xml` :
```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

**Utilisez Gradle ?** Ajoutez cette ligne à votre `build.gradle` :
```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

**Préférez une configuration manuelle ?** Téléchargez le JAR directement depuis [GroupDocs.Signature for Java releases](https://releases.groupdocs.com/signature/java/) et ajoutez‑le à votre classpath.

### Obtenir votre licence
Avant de passer en production complète, vous devrez gérer la licence :
- **Essai gratuit :** Parfait pour les tests — obtenez‑le sur le site GroupDocs pour explorer les fonctionnalités principales.  
- **Licence temporaire :** Besoin de plus de temps pour évaluer ? Demandez une licence temporaire de 30 jours.  
- **Licence complète :** Prêt pour la production ? Achetez une licence pour une utilisation illimitée.  

Voici une vérification rapide pour s'assurer que tout fonctionne :
```java
Signature signature = new Signature("sample.pdf");
System.out.println("Signature object created successfully.");
```

Si cela s'exécute sans erreur, vous êtes prêt !

## Comment créer une signature de code‑barres en Java
Passons maintenant à la partie amusante — signons un PDF avec un code‑barres. Nous décomposerons cela en étapes faciles afin que vous compreniez exactement ce qui se passe à chaque étape.

### Étape 1 : Initialiser l'objet Signature
**Ancre de définition :** La classe `Signature` est le point d'entrée de GroupDocs.Signature pour charger, modifier et enregistrer des documents PDF.  
Tout d'abord, vous devez indiquer à GroupDocs quel PDF vous utilisez :
```java
Signature signature = new Signature("input.pdf");
```

**Ce qui se passe ici :** L'objet `Signature` charge votre PDF en mémoire et le prépare pour les modifications. Assurez‑vous que le chemin du fichier est correct — une erreur fréquente consiste à utiliser des antislashs sous Windows sans les échapper (utilisez `\\` ou simplement des barres obliques, qui fonctionnent sur toutes les plateformes).

### Étape 2 : Configurer vos options de code‑barres (Comment ajouter un code‑barres)
**Ancre de définition :** `BarcodeSignOptions` encapsule tous les paramètres nécessaires pour rendre un code‑barres dans un PDF.  
Créons maintenant la signature de code‑barres avec vos données :
```java
BarcodeSignOptions options = new BarcodeSignOptions("12345678");
options.setEncodeType(BarcodeEncodeType.Code128);
```

- `"12345678"` est la donnée de votre code‑barres — cela peut être un ID de commande, un numéro de certificat ou tout autre identifiant dont vous avez besoin.  
- `Code128` est le type d'encodage (plus d'informations sur le choix du bon type ci‑dessous).  

**Astuce :** Code128 peut gérer à la fois les chiffres et les lettres, ce qui le rend polyvalent pour la plupart des cas d'utilisation. Si vous avez seulement besoin de chiffres, `Code39` peut être plus simple, mais Code128 vous offre plus de flexibilité.

### Étape 3 : Positionner votre code‑barres (Comment signer un PDF avec un code‑barres)
**Ancre de définition :** `SignatureOptions` fournit des propriétés de mise en page telles que le numéro de page, la taille et l'alignement.  
C'est ici que GroupDocs brille vraiment — le positionnement basé sur les pourcentages signifie que votre code‑barres s'affiche correctement sur n'importe quelle taille de PDF :
```java
options.setLeft(10);   // 10% from the left edge
options.setTop(90);    // 90% from the bottom edge (near the footer)
options.setWidth(30);  // 30% of page width
options.setHeight(10); // 10% of page height
options.setPageNumber(1);
```

**Pourquoi les pourcentages sont importants :** Imaginez que vous signez à la fois des documents A4 et des formulaires au format légal. Avec le positionnement en pourcentage, votre code‑barres s'ajuste automatiquement pour rester cohérent sur les deux. Utiliser des valeurs fixes en pixels rendrait votre code‑barres trop petit sur les grands documents ou trop grand sur les petits.

**Exemple réel :** Sur une page A4 (595 × 842 points), un code‑barres de 30 % de largeur fera environ 180 points de large. Sur une page légal (612 × 1008 points), il fera environ 184 points de large — proportionnel automatiquement.

### Étape 4 : Signer et enregistrer votre document (Comment ajouter un code‑barres PDF)
Il est temps d'appliquer réellement la signature et d'enregistrer votre travail :
```java
signature.sign(outputPath, options);
```

**Note importante :** Le répertoire de sortie doit exister avant d'exécuter ce code. GroupDocs ne créera pas de répertoires imbriqués pour vous, créez‑les donc d'abord ou gérez cela dans votre code :
```java
new File("output").mkdirs();
```

**Et si quelque chose tourne mal ?** Enveloppez cela dans un bloc try‑catch :
```java
try {
    signature.sign("signed.pdf", options);
} catch (Exception e) {
    e.printStackTrace();
}
```

## Choisir le bon type de code‑barres pour vos besoins (générer un code128)
GroupDocs prend en charge plusieurs formats de code‑barres, et choisir le bon est important. Voici une comparaison pratique :

**Code128 (Notre choix par défaut) :**
- **Idéal pour :** Données alphanumériques mixtes (ID comme « INV2024-001 »)  
- **Capacité :** Jusqu'à 128 caractères ASCII  
- **Pourquoi c'est le meilleur :** Compact, largement supporté, gère à la fois les lettres et les chiffres  
- **À utiliser quand :** Vous avez besoin de flexibilité et ne savez pas quel type de données vous allez encoder  

**Code39 :**
- **Idéal pour :** Codes alphanumériques simples  
- **Capacité :** 43 caractères (A‑Z, 0‑9 et quelques symboles)  
- **Pourquoi le considérer :** Les scanners plus anciens le supportent souvent mieux  
- **À utiliser quand :** Vous travaillez avec des systèmes hérités ou lorsque la simplicité prime sur la densité des données  

**QR Code :**
- **Idéal pour :** Grandes quantités de données (URL, charges JSON)  
- **Capacité :** Jusqu'à 3 KB de données  
- **Pourquoi c'est puissant :** Peut stocker des structures de données complexes, correction d'erreurs intégrée  
- **À utiliser quand :** Vous devez intégrer des données structurées ou des URL  

**EAN/UPC :**
- **Idéal pour :** Identification de produit  
- **Capacité :** Codes numériques à longueur fixe (8‑13 chiffres)  
- **À utiliser quand :** Vous travaillez avec des systèmes de vente au détail ou d'inventaire  

Guide de décision rapide :
- Besoin de lettres et de chiffres ? → Code128  
- Seulement des chiffres, rester simple ? → Code39  
- Beaucoup de données ou URL ? → QR Code  
- Codes de vente au détail/produits ? → EAN/UPC  

## Pièges courants et comment les éviter (code‑barres à l'épreuve de la falsification)
Voici les problèmes que les développeurs rencontrent le plus souvent (pour que vous n'ayez pas à les affronter) :

### Problème 1 : Le positionnement du code‑barres est incorrect
**Symptôme :** Votre code‑barres apparaît à des emplacements inattendus ou est coupé.  
**Causes courantes :**
- Utilisation de valeurs en pixels sur différentes tailles de page  
- Oublier que les coordonnées PDF commencent en bas à gauche, pas en haut à gauche  
- Marges poussant le contenu hors de la zone visible  

**Solution :** Utilisez toujours le positionnement basé sur les pourcentages pour la cohérence :
```java
options.setLeft(5);
options.setTop(95);
options.setWidth(40);
options.setHeight(12);
```

### Problème 2 : Le texte du code‑barres est illisible
**Symptôme :** Le texte encodé s'affiche mais les scanners ne peuvent pas le lire.  
**Causes :**
- Code‑barres trop petit pour la quantité de données  
- Type d'encodage incorrect pour vos données  
- Contraste faible entre les barres et le fond  

**Solution :** Adaptez la taille de votre code‑barres à la longueur de vos données. Pour Code128 avec 10‑15 caractères, visez au moins 8‑10 % de la largeur de la page.

### Problème 3 : Exceptions de chemin de fichier
**Symptôme :** `FileNotFoundException` ou erreurs similaires.  
**Causes :**
- Chemins Windows codés en dur avec des antislashs simples  
- Le répertoire de sortie n'existe pas  
- Problèmes de permissions de fichier  

**Solution :** Utilisez des barres obliques (elles fonctionnent partout) et créez d'abord les répertoires :
```java
Path output = Paths.get("output/signed.pdf");
Files.createDirectories(output.getParent());
```

### Problème 4 : Problèmes de mémoire avec de gros PDF
**Symptôme :** Erreurs de mémoire insuffisante lors du traitement de gros documents.  
**Solution :** Fermez l'objet `Signature` lorsque vous avez terminé pour libérer les ressources :
```java
signature.close();
```

## Tester votre implémentation de code‑barres
Avant de déployer, assurez‑vous que vos codes‑barres fonctionnent réellement. Voici une checklist de test pratique :

### 1. Test d'inspection visuelle
Ouvrez votre PDF signé et vérifiez :
- Le code‑barres est‑il visible et correctement positionné ?  
- A‑t‑il l'air net (pas flou ou pixellisé) ?  
- Y a‑t‑il suffisamment d'espace blanc autour ?

### 2. Test de numérisation
Utilisez une application de scanner de code‑barres sur votre téléphone (comme « Barcode Scanner » ou « QR & Barcode Reader ») pour vérifier :
- Le scanner peut lire votre code‑barres  
- Les données décodées correspondent à ce que vous avez encodé  
- Il fonctionne sous différents angles et distances

### 3. Test multiplateforme
Ouvrez votre PDF sur différents appareils :
- Windows (Adobe Reader, Chrome)  
- Mac (Preview, Chrome)  
- Appareils mobiles (iOS, Android)  

Assurez‑vous que le code‑barres s'affiche correctement partout.

### 4. Code de test automatisé
Voici un test simple que vous pouvez exécuter :
```java
Signature testSignature = new Signature("signed.pdf");
List<BarcodeSignature> signatures = testSignature.search(BarcodeSignature.class);
if (signatures.size() > 0) {
    System.out.println("Barcode found: " + signatures.get(0).getText());
}
```

## Cas d'utilisation réels pour les signatures de code‑barres
Examinons où cette technique brille réellement dans les systèmes de production :

### 1. Génération et vérification de certificats
**Scénario :** Vous créez une plateforme de formation qui délivre des certificats de fin de formation.  
**Implémentation :** Générez un ID de certificat unique (par ex. « CERT‑2024‑00123 ») et intégrez‑le comme code‑barres Code128 dans le coin inférieur droit. Scanner le code‑barres permet à votre API de récupérer instantanément les détails du certificat, éliminant la saisie manuelle de données.

### 2. Systèmes de suivi des factures
**Scénario :** Votre entreprise traite des milliers de factures chaque mois.  
**Implémentation :** Ajoutez le numéro de facture et la date d'échéance sous forme de QR code positionné où l'équipement de numérisation peut le lire facilement. Les systèmes de tri automatisés peuvent acheminer les factures sans intervention humaine, réduisant le temps de traitement de heures à minutes.

### 3. Gestion juridique des contrats
**Scénario :** Un cabinet d'avocats doit suivre les versions et les amendements des contrats.  
**Implémentation :** Chaque version de contrat reçoit un identifiant de code‑barres unique incluant l'ID du contrat, le numéro de version et la date de signature. Le scan lors des audits récupère automatiquement l'historique complet des versions.

### 4. Sécurité des dossiers médicaux
**Scénario :** Un hôpital veut empêcher l'accès non autorisé aux dossiers.  
**Implémentation :** Intégrez l'ID du patient et le horodatage de création du dossier dans un code‑barres. Seuls les appareils authentifiés peuvent décoder et accéder au dossier complet, et chaque scan crée un journal d'audit pour la conformité.

## Conseils d'optimisation des performances (sécurité des documents Java)
Lorsque vous signez de nombreux PDF, les performances sont importantes. Voici quelques conseils pour que tout fonctionne sans accroc :

### Stratégie de traitement par lots
Au lieu de signer un document à la fois, traitez‑les par lots :
```java
for (String filePath : pdfList) {
    Signature batchSignature = new Signature(filePath);
    batchSignature.sign(outputPath, options);
    batchSignature.close();
}
```

**Pourquoi cela aide :** Réutiliser l'objet d'options et fermer correctement les ressources évite les fuites de mémoire.

### Gestion de la mémoire pour les gros PDF
Pour les PDF de plus de 50 Mo :
- Traitez‑les séquentiellement plutôt que de charger plusieurs à la fois.  
- Utilisez try‑with‑resources pour garantir le nettoyage.  
- Surveillez la taille du tas et ajustez les paramètres JVM si nécessaire : `-Xmx2g`.

### Mise en cache des codes‑barres fréquemment utilisés
Si vous signez de nombreux documents avec le même code‑barres, mettez en cache l'instance `BarcodeSignOptions` :
```java
BarcodeSignOptions cachedOptions = new BarcodeSignOptions("STATIC_ID");
cachedOptions.setEncodeType(BarcodeEncodeType.Code128);
```

## Quand utiliser les signatures de code‑barres (et quand ne pas le faire)

**Scénarios parfaits :**
- Vous avez besoin d'identifiants de documents lisibles par machine.  
- Les documents seront scannés ou traités automatiquement.  
- Vous souhaitez un suivi à l'épreuve de la falsification sans certificats numériques.  
- Une intégration avec l'infrastructure de code‑barres existante est requise.  

**Pas idéal lorsque :**
- Vous avez besoin de signatures numériques juridiquement contraignantes (utilisez des certificats numériques à la place).  
- Les documents ne seront visualisés que par des humains (un simple filigrane texte peut suffire).  
- Vous travaillez avec des documents extrêmement petits où un code‑barres dominerait la page.  
- Les exigences de sécurité imposent le chiffrement — les codes‑barres sont visibles et scannables par tous.  

**Pouvez‑vous combiner les approches ?** Absolument ! De nombreux systèmes utilisent à la fois des signatures de code‑barres pour le suivi et des signatures numériques pour la validité juridique.

## Questions fréquentes
**Q : Puis‑je utiliser différents types de code‑barres dans le même PDF ?**  
**R :** Oui ! Appelez `signature.sign()` plusieurs fois avec différents `BarcodeSignOptions` pour chaque type de code‑barres. Assurez‑vous simplement qu'ils ne se chevauchent pas.

**Q : Comment gérer les code‑barres contenant des caractères spéciaux ?**  
**R :** Code128 gère correctement la plupart des caractères ASCII. Pour l'Unicode ou des données complexes, passez aux QR codes — ils supportent l'encodage UTF‑8.

**Q : Quelle est la quantité maximale de données que je peux stocker dans un code‑barres Code128 ?**  
**R :** Techniquement jusqu'à 128 caractères, mais la lisibilité chute nettement au‑delà de 30‑40 caractères. Pour des charges plus importantes, utilisez des QR codes.

**Q : L'ajout de code‑barres augmentera‑t‑il de façon significative la taille de mon fichier PDF ?**  
**R :** Pas de façon notable — les code‑barres sont des graphiques vectoriels, ajoutant généralement seulement 5‑20 KB par code‑barres selon la taille et la complexité.

**Q : Puis‑je faire pivoter les code‑barres ou les placer verticalement ?**  
**R :** Oui ! Utilisez `options.setRotationAngle(90)` pour faire pivoter votre code‑barres, ce qui est pratique pour le placer en marge.

**Q : Comment faire apparaître les code‑barres sur chaque page d'un PDF multipage ?**  
**R :** Parcourez les pages et appliquez la signature à chacune. Consultez la classe `PagesSetup` dans la documentation GroupDocs pour contrôler quelles pages sont signées.

**Q : Que faire si mon scanner de code‑barres ne peut pas lire le code‑barres généré ?**  
**R :** D'abord, vérifiez que le scanner supporte le type de code‑barres choisi. Ensuite, augmentez la taille du code‑barres — la plupart des problèmes de numérisation proviennent de barres trop petites. Visez au moins 1 pouce (2,54 cm) de largeur pour des lectures fiables.

## Ressources supplémentaires
**Documentation :**
- [GroupDocs.Signature for Java Docs](https://docs.groupdocs.com/signature/java/)  
- [API Reference Guide](https://reference.groupdocs.com/signature/java/)  

**Téléchargements et licences :**
- [Download Latest Version](https://releases.groupdocs.com/signature/java/)  
- [Free Trial Access](https://releases.groupdocs.com/signature/java/)  
- [Get Temporary License](https://purchase.groupdocs.com/temporary-license/)  
- [Purchase Full License](https://purchase.groupdocs.com/buy)  

**Communauté et support :**
- [Support Forum](https://forum.groupdocs.com/c/signature/) - Communauté active avec les ingénieurs GroupDocs  

---

**Dernière mise à jour :** 2026-07-20  
**Testé avec :** GroupDocs.Signature 23.12 (Java)  
**Auteur :** GroupDocs  

```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

```java
import com.groupdocs.signature.Signature;

public class QuickTest {
    public static void main(String[] args) {
        try {
            Signature signature = new Signature("test-document.pdf");
            System.out.println("GroupDocs.Signature is ready to go!");
        } catch (Exception e) {
            System.err.println("Setup issue: " + e.getMessage());
        }
    }
}
```

```java
String filePath = "YOUR_DOCUMENT_DIRECTORY/sample.pdf";
Signature signature = new Signature(filePath);
```

```java
import com.groupdocs.signature.options.sign.BarcodeSignOptions;
import com.groupdocs.signature.domain.barcodes.BarcodeTypes;

BarcodeSignOptions options = new BarcodeSignOptions("12345678");
options.setEncodeType(BarcodeTypes.Code128);
```

```java
import com.groupdocs.signature.domain.enums.MeasureType;
import com.groupdocs.signature.domain.Padding;

// Use percentages instead of fixed pixels
options.setLocationMeasureType(MeasureType.Percents);
options.setLeft(5);  // 5% from the left edge
options.setTop(5);   // 5% from the top

// Size it proportionally too
options.setSizeMeasureType(MeasureType.Percents);
options.setWidth(10);  // 10% of page width
options.setHeight(5);  // 5% of page height

// Add some breathing room with margins
Padding margins = new Padding();
margins.setLeft(1);
margins.setTop(1);
margins.setRight(1);
options.setMargin(margins);
```

```java
String outputFilePath = "YOUR_OUTPUT_DIRECTORY/SignWithPercents/sample_signed.pdf";
signature.sign(outputFilePath, options);
```

```java
Path outputPath = Paths.get(outputFilePath);
Files.createDirectories(outputPath.getParent());
signature.sign(outputFilePath, options);
```

```java
try {
    signature.sign(outputFilePath, options);
    System.out.println("PDF signed successfully at: " + outputFilePath);
} catch (Exception e) {
    System.err.println("Signing failed: " + e.getMessage());
    e.printStackTrace();
}
```

```java
options.setLocationMeasureType(MeasureType.Percents);
options.setLeft(5);  // 5% from left works on any page width
```

```java
options.setWidth(10);  // Give it room to breathe
options.setHeight(5);  // Maintain proper aspect ratio
```

```java
String filePath = "documents/sample.pdf";  // Works on Windows, Mac, Linux
Files.createDirectories(Paths.get("output/signed"));
```

```java
try (Signature signature = new Signature(filePath)) {
    signature.sign(outputFilePath, options);
} // Automatically closes and releases memory
```

```java
import org.junit.Test;
import static org.junit.Assert.*;

public class BarcodeSignatureTest {
    
    @Test
    public void testBarcodeSigning() {
        String testPdf = "test-data/sample.pdf";
        String output = "test-output/signed.pdf";
        
        try (Signature signature = new Signature(testPdf)) {
            BarcodeSignOptions options = new BarcodeSignOptions("TEST123");
            options.setEncodeType(BarcodeTypes.Code128);
            
            signature.sign(output, options);
            
            // Verify output file exists
            assertTrue(new File(output).exists());
            
            // Verify file size increased (signature was added)
            long originalSize = new File(testPdf).length();
            long signedSize = new File(output).length();
            assertTrue(signedSize > originalSize);
            
        } catch (Exception e) {
            fail("Signing should not throw exception: " + e.getMessage());
        }
    }
}
```

```java
List<String> pdfFiles = Arrays.asList("doc1.pdf", "doc2.pdf", "doc3.pdf");

for (String pdfFile : pdfFiles) {
    try (Signature signature = new Signature(pdfFile)) {
        BarcodeSignOptions options = createBarcodeOptions(); // Reuse options
        signature.sign(getOutputPath(pdfFile), options);
    }
}
```

```java
// Create options once, reuse many times
BarcodeSignOptions templateOptions = createStandardBarcodeOptions();

// For each document, clone and customize
BarcodeSignOptions documentOptions = templateOptions.clone();
documentOptions.setText(uniqueDocumentId);
```

## Tutoriels associés

- [Tutoriel Java sur la signature de code‑barres - Ajouter, vérifier et gérer les codes‑barres dans les PDF](/signature/java/barcode-signatures/)  
- [Créer une signature de code‑barres en Java – Mettre à jour les codes‑barres PDF](/signature/java/barcode-signatures/java-groupdocs-signature-barcode-initialize-update/)  
- [Comment lire un PDF QR code avec Java et GroupDocs.Signature](/signature/java/barcode-signatures/java-pdf-barcode-search-groupdocs-signature-api/)