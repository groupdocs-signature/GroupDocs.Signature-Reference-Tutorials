---
categories:
- Java PDF Processing
date: '2026-03-22'
description: Apprenez à ajouter un code‑barres aux fichiers PDF en Java avec GroupDocs.Signature.
  Ce tutoriel étape par étape montre comment générer des PDF contenant des codes‑barres
  de manière efficace et fiable.
keywords: add barcode to PDF Java, generate barcode in PDF programmatically, Java
  PDF barcode library, sign PDF with barcode Java, create barcode signature PDF
lastmod: '2026-03-22'
linktitle: Add Barcode to PDF Java
tags:
- barcode-generation
- pdf-signing
- document-automation
- groupdocs
title: Comment ajouter un code‑barres à un PDF en Java – Guide GroupDocs
type: docs
url: /fr/java/barcode-signatures/create-sign-pdfs-groupdocs-barcode-java/
weight: 1
---

# Comment ajouter un code‑barres à un PDF en Java

## Introduction

Vous avez déjà eu besoin de suivre automatiquement des factures, de vérifier l’authenticité d’un contrat ou de gérer des documents d’inventaire à grande échelle ? **Apprendre à ajouter un code‑barres** aux fichiers PDF de façon programmatique résout ces problèmes—et si vous travaillez en Java, vous disposez d’une option solide, éprouvée au combat.

Ajouter des codes‑barres manuellement ne passe pas à l’échelle. Que vous traitiez dix factures ou dix mille, vous avez besoin d’une méthode fiable pour **ajouter un code‑barres à un PDF**. C’est là qu’une bonne bibliothèque Java de codes‑barres PDF devient indispensable.

Dans ce guide, je vous montre comment ajouter un code‑barres à des fichiers PDF Java en utilisant GroupDocs.Signature—une bibliothèque qui gère le travail lourd tout en vous offrant un contrôle fin sur le positionnement, la taille et les types de codes‑barres. À la fin, vous saurez comment signer un PDF avec du code Java de code‑barres, gérer les cas limites et éviter les pièges courants qui bloquent les développeurs.

**Ce que vous allez apprendre :**
- Pourquoi les codes‑barres dans les PDF sont importants pour votre flux de travail  
- Configurer GroupDocs.Signature pour Java (de la bonne façon)  
- Créer et positionner des signatures de code‑barres avec précision  
- Gérer les erreurs et optimiser les performances  
- Applications concrètes dans différents secteurs  

## Réponses rapides
- **Quelle bibliothèque dois‑je utiliser ?** GroupDocs.Signature pour Java  
- **Comment créer une signature de code‑barres PDF ?** Utilisez `BarcodeSignOptions` avec `Signature.sign()`  
- **Quel type de code‑barres est le meilleur dans la plupart des cas ?** Code128  
- **Puis‑je ajouter plusieurs codes‑barres à un même PDF ?** Oui, appelez `sign()` plusieurs fois ou passez une liste  
- **Ai‑je besoin d’une licence pour la production ?** Oui, une licence GroupDocs valide supprime les filigranes  

## Pourquoi ajouter des codes‑barres aux PDF ?

Avant de plonger dans le code, parlons de l’importance de cette opération. Les codes‑barres dans les PDF ne servent pas seulement à donner un aspect professionnel—ils résolvent de vrais problèmes métier :

**Vérification de documents** – Les codes‑barres peuvent encoder des identifiants uniques qui rendent la contrefaçon quasi impossible. Lorsqu’on scanne le code‑barres, votre système peut immédiatement vérifier la légitimité du document.

**Automatisation des flux de travail** – Au lieu de saisir manuellement les ID de documents ou les numéros de suivi, votre personnel (ou vos clients) peut scanner un code‑barres. Cela réduit les erreurs humaines d’environ 95 % comparé à la saisie manuelle.

**Intégration avec les systèmes existants** – La plupart des ERP, systèmes d’inventaire et de gestion de documents comprennent déjà le “code‑barres”. Les ajouter à vos PDF signifie une intégration fluide sans devoir créer des API personnalisées.

**Exigences de conformité** – De nombreux secteurs (santé, logistique, juridique) exigent la traçabilité des documents. Les codes‑barres offrent une piste d’audit qui satisfait les exigences réglementaires.

L’avantage clé d’ajouter des codes‑barres de façon programmatique ? **Cohérence et échelle**. Vous définissez les règles une fois, et chaque document reçoit le même traitement—que vous traitiez cinq fichiers ou cinquante mille.

## Prérequis

Avant de commencer à coder, assurez‑vous d’avoir ces bases couvertes :

### Logiciels et bibliothèques requis
- **JDK 8 ou supérieur** installé sur votre machine (JDK 11+ recommandé pour de meilleures performances)  
- Un IDE comme IntelliJ IDEA, Eclipse ou VS Code avec les extensions Java  
- **GroupDocs.Signature pour Java version 23.12** (nous vous montrerons comment l’ajouter ci‑dessous)

### Connaissances de base requises
- À l’aise avec les fondamentaux de Java (classes, objets, gestion de fichiers)  
- Compréhension de la structure d’un document PDF (utile mais pas indispensable)  
- Familiarité avec la gestion des dépendances (Maven ou Gradle)

**Astuce pro** : Si vous débutez avec GroupDocs, commencez par leur essai gratuit. Vous avez 30 jours pour expérimenter sans engagement—parfait pour un proof‑of‑concept.

## Configuration de GroupDocs.Signature pour Java

Intégrer GroupDocs.Signature à votre projet est simple. Choisissez le système de gestion des dépendances qui correspond à votre configuration :

### Configuration Maven
Ajoutez ceci à votre fichier `pom.xml` :

```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

### Configuration Gradle
Pour les utilisateurs de Gradle, ajoutez cette ligne à votre `build.gradle` :

```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

### Option de téléchargement direct
Vous préférez ne pas utiliser d’outils de construction ? Téléchargez le JAR directement depuis la [page des releases GroupDocs.Signature pour Java](https://releases.groupdocs.com/signature/java/) et ajoutez‑le manuellement à votre classpath.

### Configuration de la licence

Voici le chemin de licence le plus couramment suivi par les développeurs :

1. **Commencer avec l’essai gratuit** – Sans carte de crédit, sans engagement. Idéal pour les tests.  
2. **Obtenir une licence temporaire** – Si 30 jours ne suffisent pas, demandez une licence temporaire pour prolonger le développement.  
3. **Acheter pour la production** – Une fois prêt à déployer, achetez une licence adaptée à votre volume d’utilisation.

**Important** : L’essai gratuit ajoute des filigranes aux documents de sortie. Pour un travail destiné aux clients, vous aurez besoin d’au moins une licence temporaire.

### Code d’initialisation

Une fois les dépendances en place, initialisez l’objet `Signature` ainsi :

```java
import com.groupdocs.signature.Signature;

// Initialize Signature object with your document path
Signature signature = new Signature("YOUR_DOCUMENT_DIRECTORY/sample.pdf");
```

**Ce qui se passe** : La classe `Signature` est votre point d’entrée principal. Vous lui passez un chemin de fichier, et elle charge le PDF en mémoire pour le traitement. Simple, non ?

**Erreur fréquente à éviter** : N’oubliez pas de fermer l’objet `Signature` lorsque vous avez terminé (ou utilisez try‑with‑resources). Le laisser ouvert peut provoquer des fuites de mémoire dans les applications à long terme.

## Choisir le bon type de code‑barres

Tous les codes‑barres ne se valent pas. Le type que vous choisissez dépend de ce que vous devez encoder et de l’endroit où le code sera scanné.

### Types de codes‑barres populaires pris en charge

- **Code128** – Idéal pour les données alphanumériques ; courant sur les étiquettes d’expédition.  
- **QR Codes** – Parfait quand vous devez stocker plus de données (URL, JSON, jusqu’à 4 000 caractères).  
- **Code39** – Plus simple que Code128 mais moins efficace en espace ; bon pour le suivi interne.  
- **EAN/UPC** – Standard industriel pour les produits de détail.  

**Quand utiliser lequel ?**  
- Besoin d’encoder plus de 50 caractères ? → QR Code  
- Identification produit standard ? → EAN/UPC  
- Suivi de documents générique ? → Code128  
- Compatibilité maximale avec les scanners anciens ? → Code39  

**Astuce pro** : Code128 est le choix par défaut le plus sûr pour la gestion de documents. Il équilibre lisibilité, capacité de données et compatibilité scanner.

## Guide d’implémentation : création de signatures de code‑barres

Passons à la partie pratique—créons et ajoutons réellement des codes‑barres à vos PDF. Je décompose cela en étapes gérables afin que vous puissiez suivre (ou sauter les parties dont vous n’avez pas besoin).

### Étape 1 : configuration des chemins de documents

Première chose — indiquez à Java où se trouve votre PDF et où enregistrer la version signée :

```java
String filePath = "YOUR_DOCUMENT_DIRECTORY/sample.pdf";
String fileName = new File(filePath).getName();
```

**Ce qui se passe** : Vous définissez le chemin du fichier d’entrée et extrayez simplement le nom de fichier. Cela garde vos sorties organisées (particulièrement utile lors du traitement par lots de plusieurs fichiers).

**Conseil réel** : En production, ces chemins proviennent généralement de fichiers de configuration ou de variables d’environnement—not de chaînes codées en dur. Envisagez `System.getenv()` ou un fichier `.properties` pour plus de flexibilité.

### Étape 2 : configuration de la sortie et des options de code‑barres

Ensuite, définissez où le document signé sera enregistré et quel code‑barres créer :

```java
// Define output file path
String outputFilePath = "YOUR_OUTPUT_DIRECTORY/SignWithMillimeters/" + fileName;

BarcodeSignOptions options = new BarcodeSignOptions("12345678");
options.setEncodeType(BarcodeTypes.Code128);
```

**Décomposition** :  
- `outputFilePath` — L’endroit où votre PDF final sera sauvegardé. Remarquez la structure de sous‑dossier ? Cela aide à organiser les différentes méthodes de signature.  
- `BarcodeSignOptions("12345678")` — Les données encodées dans votre code‑barres. Cela peut être un numéro de facture, un ID de suivi, un hash de document—tout ce dont vous avez besoin.  
- `setEncodeType(BarcodeTypes.Code128)` — Indique à GroupDocs le format de code‑barres à utiliser.

**Question fréquente** : « Puis‑je utiliser des caractères spéciaux dans les données du code‑barres ? » Avec Code128, oui —vous pouvez inclure lettres, chiffres et la plupart des ponctuations. Les QR codes sont encore plus flexibles.

### Étape 3 : positionnement précis du code‑barres

Voici la partie intéressante. Vous pouvez positionner les codes‑barres avec une précision au millimètre :

```java
// Set position and size in millimeters
options.setLocationMeasureType(MeasureType.Millimeters);
options.setLeft(40);  // X‑coordinate from left edge
options.setTop(50);   // Y‑coordinate from top edge

options.setSizeMeasureType(MeasureType.Millimeters);
options.setWidth(20);  // Width of the barcode
options.setHeight(10); // Height of the barcode
```

**Pourquoi les millimètres comptent** : Lors de l’impression, les millimètres offrent une taille cohérente quel que soit le format de papier ou la résolution. (Vous pouvez aussi utiliser des pixels ou des pourcentages si cela convient mieux à votre cas d’utilisation.)

**Stratégie de positionnement** :  
- **Coin supérieur droit** (type étiquette d’expédition) : `setLeft(150)`, `setTop(10)`  
- **Centre inférieur** (type billet) : calculez le centre en fonction de la largeur de la page  
- **À côté d’un contenu existant** : mesurez la mise en page du PDF et positionnez en conséquence  

**Astuce pro** : Testez votre positionnement sur quelques PDF d’exemple avant de lancer le traitement par lots. Des mises en page différentes peuvent nécessiter de légers ajustements.

### Étape 4 : ajout de marges pour le rendu

Les marges évitent que le code‑barres ne foule le reste du contenu :

```java
// Define margin settings
Padding padding = new Padding();
padding.setLeft(5);   // Left margin in mm
padding.setTop(5);    // Top margin in mm
padding.setRight(5);  // Right margin in mm
padding.setBottom(5); // Bottom margin in mm
options.setMargin(padding);
```

**Ce que cela fait** : Crée une zone tampon de 5 mm autour du code‑barres. Cet espace de respiration améliore la lisibilité et donne un aspect plus professionnel.

**Quand augmenter les marges** : Si vous placez le code‑barres près du bord d’une page, passez à 10 mm. Les imprimantes ont souvent du mal avec du contenu trop proche des bords.

### Étape 5 : signature et sauvegarde du document

Le moment de vérité—ajouter réellement le code‑barres :

```java
// Sign and save the document
SignResult signResult = signature.sign(outputFilePath, options);
```

**Ce qui se passe en coulisses** : GroupDocs ouvre votre PDF, rend le code‑barres selon vos options, l’insère à la position spécifiée, puis enregistre le fichier modifié. Le PDF original reste intact.

**Valeur de retour** : L’objet `SignResult` contient le statut de succès/échec et des métadonnées sur ce qui a été signé. Vous pouvez l’inspecter pour vérifier que tout a fonctionné.

### Étape 6 : gestion des erreurs de façon élégante

Des problèmes peuvent survenir (chemins incorrects, PDF corrompu, permissions insuffisantes). Gérez les erreurs correctement :

```java
try {
    Signature signature = new Signature(filePath);
    SignResult signResult = signature.sign(outputFilePath, options);
    
    System.out.println("Barcode added successfully!");
    System.out.println("Output saved to: " + outputFilePath);
    
} catch (Exception e) {
    System.err.println("Error signing document: " + e.getMessage());
    throw new GroupDocsSignatureException(e.getMessage());
}
```

**Bonnes pratiques de gestion d’exceptions** :  
- Enregistrez la stack trace complète pour le débogage (pas seulement le message)  
- Fournissez des messages d’erreur compréhensibles pour l’utilisateur (évitez le jargon technique)  
- Nettoyez les ressources même en cas d’erreur (utilisez try‑with‑resources)  
- Envisagez une logique de retry pour les échecs transitoires (problèmes réseau, fichiers verrouillés)

**Erreurs courantes que vous rencontrerez** :  
- `FileNotFoundException` — le chemin du PDF d’entrée est erroné  
- `GroupDocsSignatureException` — données du code‑barres invalides ou version PDF non prise en charge  
- `OutOfMemoryError` — traitement de trop nombreux PDF volumineux simultanément  

## Comment créer une signature de code‑barres PDF en Java

Si vous préférez une checklist concise, la voici :

1. **Ajouter la dépendance GroupDocs.Signature** (Maven, Gradle ou JAR manuel).  
2. **Initialiser `Signature`** avec le chemin du PDF source.  
3. **Configurer `BarcodeSignOptions`** — définir les données, le type, la taille et la localisation.  
4. **Optionnellement définir des marges** pour améliorer la lisibilité.  
5. **Appeler `signature.sign(outputPath, options)`** pour intégrer le code‑barres.  
6. **Gérer les exceptions** et fermer les ressources.

Suivre ces six étapes vous permettra d’**ajouter un code‑barres à des documents PDF Java** de façon fiable dans n’importe quelle application Java.

## Problèmes courants & solutions

Abordons les difficultés que rencontrent réellement les développeurs (parce que la documentation le fait rarement) :

### Problème 1 : le code‑barres ne se scanne pas correctement

**Symptômes** : Le scanner ne lit pas le code‑barres ou renvoie des données erronées.  

**Solutions** :  
- Augmentez la taille du code‑barres (minimum 15 mm de largeur pour la plupart des scanners)  
- Vérifiez que les données n’incluent pas de caractères non supportés pour ce type  
- Assurez un contraste suffisant entre le code‑barres et le fond  
- Testez avec plusieurs applications de scanner—certaines sont meilleures que d’autres  

### Problème 2 : le positionnement du code‑barres varie d’un document à l’autre

**Symptômes** : Le même code produit des résultats différents selon les PDF de tailles différentes.  

**Solutions** :  
- Les PDF de tailles différentes nécessitent des calculs de position, pas des valeurs codées en dur  
- Vérifiez si les PDF sources ont une rotation appliquée (cela décale les coordonnées)  
- Utilisez un positionnement basé sur les pourcentages pour plus de cohérence  
- Normalisez, si possible, tous les PDF d’entrée à une taille de page standard  

### Problème 3 : dégradation des performances avec de gros lots

**Symptômes** : Les 100 premiers PDF sont traités rapidement, puis le processus ralentit.  

**Solutions** :  
- Fermez rapidement les objets `Signature` (ou utilisez try‑with‑resources)  
- Traitez en lots plus petits avec nettoyage de la mémoire entre les lots  
- Envisagez le traitement parallèle pour les opérations CPU‑intensives  
- Surveillez l’utilisation du heap —vous pourriez devoir ajuster la JVM  

```java
// Good: Process in chunks
List<String> allFiles = getAllPdfFiles();
int batchSize = 100;

for (int i = 0; i < allFiles.size(); i += batchSize) {
    List<String> batch = allFiles.subList(i, Math.min(i + batchSize, allFiles.size()));
    processBatch(batch);
    System.gc(); // Suggest garbage collection between batches
}
```

### Problème 4 : augmentation excessive de la taille du fichier de sortie

**Symptômes** : Les PDF signés sont beaucoup plus lourds que les originaux.  

**Solutions** :  
- GroupDocs ne compresse pas automatiquement—gérez la compression séparément si besoin  
- Évitez d’ajouter des images de code‑barres haute résolution lorsque les vecteurs suffisent  
- Vérifiez que vous n’incorporez pas accidentellement des polices ou des métadonnées supplémentaires  

**Quand contacter le support** : Si vous avez essayé ces solutions et que le problème persiste, le [forum GroupDocs](https://forum.groupdocs.com/c/signature/) propose un support réactif.

## Cas d’utilisation réels

Voici comment différents secteurs exploitent concrètement cette fonctionnalité :

### Secteur juridique : gestion de contrats
Les cabinets d’avocats ajoutent des codes‑barres aux contrats pour les lier aux systèmes de gestion de dossiers. Scanner le code‑barres récupère instantanément l’historique complet du dossier, réduisant le temps de traitement de minutes à secondes.

**Astuce d’implémentation** : Encodez un hash du document dans le code‑barres afin de vérifier que le document physique n’a pas été altéré.

### Santé : dossiers patients
Les hôpitaux joignent des codes‑barres aux résumés de sortie et aux ordonnances PDF. Lors de l’arrivée du patient, le personnel scanne le code‑barres pour remplir automatiquement le dossier avec l’historique des visites précédentes.

**Note de conformité** : Assurez‑vous que votre implémentation de code‑barres respecte les exigences HIPAA pour le codage des données.

### Logistique : étiquettes d’expédition
Les plateformes e‑commerce ajoutent automatiquement des codes‑barres de suivi aux bordereaux d’emballage. Le personnel d’entrepôt scanne pour mettre à jour le statut d’expédition sans saisie manuelle.

**Considération de performance** : Ces systèmes traitent souvent des milliers de documents par heure—le traitement par lots et l’exécution parallèle sont cruciaux.

### Finance : traitement des factures
Les services comptables ajoutent des codes‑barres aux factures contenant les conditions de paiement et les ID fournisseurs. Le scan les dirige automatiquement vers le bon workflow d’approbation.

**Astuce pro** : Combinez les codes‑barres avec l’OCR pour une automatisation maximale—scannez le code‑barres pour les métadonnées, utilisez l’OCR pour les lignes de facturation.

## Meilleures pratiques de performance

Lorsque vous traitez des documents à grande échelle, ces optimisations font réellement la différence :

### Gestion de la mémoire
- **Utilisez try‑with‑resources** : garantit la fermeture correcte des objets `Signature`.  
- **Traitez par lots** : ne chargez pas 10 000 PDF en mémoire d’un coup.  
- **Surveillez l’utilisation du heap** : définissez les paramètres JVM appropriés (`-Xmx`, `-Xms`).

### Stratégies de traitement par lots
```java
List<String> files = getAllPdfFiles();
files.parallelStream().forEach(file -> {
    try {
        addBarcodeToFile(file);
    } catch (Exception e) {
        // Handle per‑file errors
    }
});
```

**Attention** : Le traitement parallèle consomme plus de mémoire. Surveillez et ajustez en conséquence.

### Mise en cache des objets de signature
Si vous traitez régulièrement des documents similaires, pensez à réutiliser la configuration :

```java
// Create options once
BarcodeSignOptions templateOptions = createStandardOptions();

// Reuse for multiple files
for (String file : files) {
    BarcodeSignOptions options = templateOptions.clone();
    // Customize per file if needed
    processFile(file, options);
}
```

## Foire aux questions

**Q : Comment créer une signature de code‑barres PDF en Java pour différents types de code‑barres ?**  
R : Modifiez le paramètre de `setEncodeType()`. Pour les QR codes, utilisez `BarcodeTypes.QR`. Pour EAN‑13, utilisez `BarcodeTypes.EAN13`. GroupDocs supporte plus de 60 types de codes‑barres prêts à l’emploi.

**Q : Puis‑je ajouter plusieurs codes‑barres au même PDF ?**  
R : Absolument. Appelez `signature.sign()` plusieurs fois avec différents `BarcodeSignOptions`, ou passez une liste d’options de signature en un seul appel.

**Q : Comment ajouter un code‑barres à un PDF existant sans perdre le contenu ?**  
R : GroupDocs est non destructif par défaut —il ajoute les codes‑barres comme une nouvelle couche sans modifier le contenu existant. Votre texte, images et mise en forme restent intacts.

**Q : Quelle est la quantité maximale de données que je peux encoder dans un code‑barres ?**  
R : Cela dépend du type. Code128 gère confortablement environ 128 caractères. Les QR codes peuvent stocker jusqu’à 4 000 caractères. Si vous avez besoin de plus, envisagez d’encoder une URL pointant vers vos données.

**Q : Ai‑je besoin d’une licence pour la production ?**  
R : Oui. L’essai gratuit ajoute des filigranes. Pour les déploiements en production, vous aurez besoin d’une licence temporaire (pour les tests prolongés) ou d’une licence achetée. Consultez la [page de tarification GroupDocs](https://purchase.groupdocs.com/buy) pour les options actuelles.

**Q : Comment gérer les exceptions lors du traitement par lots ?**  
R : Enveloppez chaque opération de fichier dans son propre bloc try‑catch afin qu’un PDF échoué ne fasse pas planter tout le lot. Loggez les erreurs avec le nom du fichier pour pouvoir retraiter les échecs plus tard.

**Q : GroupDocs peut‑il générer des codes‑barres 2D comme Data Matrix ?**  
R : Oui ! Utilisez `BarcodeTypes.DataMatrix`. Les Data Matrix sont populaires en fabrication car ils restent lisibles même partiellement endommagés ou à des angles inhabituels.

**Q : Quelles versions de PDF GroupDocs supporte‑t‑il ?**  
R : GroupDocs.Signature gère les PDF de la version 1.3 à 2.0 (couvre 99 % des PDF rencontrés). Si vous avez des PDF très anciens, envisagez de les convertir d’abord.

## Conclusion

Vous savez maintenant comment **ajouter un code‑barres à des documents PDF Java** de façon programmatique avec GroupDocs.Signature. Nous avons couvert tout, de la configuration de base à la gestion des erreurs prête pour la production, en passant par l’optimisation des performances.

**Points clés**  
- Les codes‑barres résolvent de vrais problèmes de flux de travail (automatisation, vérification, traçabilité)  
- GroupDocs vous donne un contrôle précis sur le positionnement et les types de codes‑barres  
- Une bonne gestion des erreurs et des ressources évite les maux de tête en production  
- L’optimisation des performances est indispensable lorsqu’on traite des volumes importants  

**Prochaines étapes** : Commencez par un petit proof‑of‑concept avec l’essai gratuit. Testez différents types de codes‑barres avec vos documents réels. Une fois validé, passez au traitement par lots, puis au déploiement en production.

Des questions ou des problèmes ? Publiez‑les sur le [forum de support GroupDocs](https://forum.groupdocs.com/c/signature/)—la communauté est réactive et les temps de réponse sont bons.

## Ressources

### Documentation & téléchargements
- [Documentation GroupDocs.Signature pour Java](https://docs.groupdocs.com/signature/java/)  
- [Référence API complète](https://reference.groupdocs.com/signature/java/)  
- [Télécharger la dernière version](https://releases.groupdocs.com/signature/java/)

### Licences & support
- [Acheter une licence](https://purchase.groupdocs.com/buy)  
- [Commencer l’essai gratuit](https://releases.groupdocs.com/signature/java/)  
- [Demander une licence temporaire](https://purchase.groupdocs.com/temporary-license/)  
- [Forum de support communautaire](https://forum.groupdocs.com/c/signature/)

---

**Dernière mise à jour :** 2026-03-22  
**Testé avec :** GroupDocs.Signature 23.12 pour Java  
**Auteur :** GroupDocs