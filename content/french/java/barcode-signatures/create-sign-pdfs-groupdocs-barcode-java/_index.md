---
categories:
- Java PDF Processing
date: '2026-01-08'
description: Apprenez à créer une signature de code‑barres PDF en Java de manière
  programmatique. Ce guide étape par étape utilisant GroupDocs.Signature montre comment
  générer efficacement un PDF avec code‑barres.
keywords: add barcode to PDF Java, generate barcode in PDF programmatically, Java
  PDF barcode library, sign PDF with barcode Java, create barcode signature PDF
lastmod: '2026-01-08'
linktitle: Add Barcode to PDF Java
tags:
- barcode-generation
- pdf-signing
- document-automation
- groupdocs
title: Créer une signature de code‑barres PDF en Java – Guide GroupDocs
type: docs
url: /fr/java/barcode-signatures/create-sign-pdfs-groupdocs-barcode-java/
weight: 1
---

# Comment ajouter un code‑barres aux documents PDF Java

## Introduction

Vous avez déjà eu besoin de suivre automatiquement des factures, de vérifier l’authenticité d’un contrat ou de gérer des documents d’inventaire à grande échelle ? **Créer une signature de code‑barres PDF** en Java de façon programmatique résout ces problèmes—et si vous travaillez en Java, vous avez plusieurs options solides.

Ajouter des codes‑barres aux PDF manuellement ne passe pas à l’échelle. Que vous traitiez 10 factures ou 10 000, vous avez besoin d’une méthode fiable pour **créer des PDF avec signature de code‑barres**. C’est là qu’une bonne bibliothèque Java de codes‑barres PDF devient indispensable.

Dans ce guide, je vous montre comment ajouter un code‑barres à des fichiers PDF Java en utilisant GroupDocs.Signature—une bibliothèque qui gère le travail lourd tout en vous offrant un contrôle fin sur le positionnement, la taille et les types de codes‑barres. À la fin, vous saurez comment signer un PDF avec du code Java de code‑barres, gérer les cas limites et éviter les pièges courants qui bloquent les développeurs.

**Ce que vous allez apprendre :**
- Pourquoi les codes‑barres dans les PDF sont importants pour votre flux de travail
- Configurer GroupDocs.Signature pour Java (de la bonne façon)
- Créer et positionner des signatures de code‑barres avec précision
- Gérer les erreurs et optimiser les performances
- Applications concrètes dans différents secteurs

## Réponses rapides
- **Quelle bibliothèque dois‑je utiliser ?** GroupDocs.Signature pour Java  
- **Comment créer un PDF avec signature de code‑barres ?** Utilisez `BarcodeSignOptions` avec `Signature.sign()`  
- **Quel type de code‑barres est le meilleur dans la plupart des cas ?** Code128  
- **Puis‑je ajouter plusieurs codes‑barres à un même PDF ?** Oui, appelez `sign()` plusieurs fois ou passez une liste  
- **Ai‑je besoin d’une licence pour la production ?** Oui, une licence GroupDocs valide supprime les filigranes  

## Pourquoi ajouter des codes‑barres aux PDF ?

Avant de plonger dans le code, parlons de l’importance de cette fonctionnalité. Les codes‑barres dans les PDF ne sont pas seulement esthétiques — ils résolvent de vrais problèmes métier :

**Vérification de documents** : Les codes‑barres peuvent encoder des identifiants uniques rendant la falsification quasi impossible. Lorsqu’on scanne le code‑barres, votre système peut vérifier instantanément la légitimité du document.

**Automatisation des flux** : Au lieu de saisir manuellement des IDs ou des numéros de suivi, votre personnel (ou vos clients) peut scanner un code‑barres. Cela réduit les erreurs humaines d’environ 95 % comparé à la saisie manuelle.

**Intégration avec les systèmes existants** : La plupart des ERP, systèmes d’inventaire et de gestion documentaire comprennent déjà le “code‑barres”. Les ajouter à vos PDF signifie une intégration fluide sans développer d’API personnalisées.

**Exigences de conformité** : De nombreux secteurs (santé, logistique, juridique) exigent la traçabilité des documents. Les codes‑barres offrent une piste d’audit qui satisfait les exigences réglementaires.

L’avantage clé d’ajouter des codes‑barres de façon programmatique ? **Cohérence et échelle**. Vous définissez les règles une fois, et chaque document reçoit le même traitement—que vous traitiez 5 fichiers ou 50 000.

## Prérequis

Avant de commencer à coder, assurez‑vous que les points suivants sont couverts :

### Logiciels et bibliothèques requis
- **JDK 8 ou supérieur** installé sur votre machine (JDK 11+ recommandé pour de meilleures performances)  
- Un IDE tel qu’IntelliJ IDEA, Eclipse ou VS Code avec les extensions Java  
- **GroupDocs.Signature pour Java version 23.12** (nous vous montrons comment l’ajouter ci‑dessous)

### Connaissances de base requises
- Maîtrise des fondamentaux Java (classes, objets, gestion de fichiers)  
- Compréhension de la structure d’un document PDF (utile mais pas indispensable)  
- Familiarité avec la gestion des dépendances (Maven ou Gradle)

**Astuce** : Si vous débutez avec GroupDocs, commencez par leur essai gratuit. Vous avez 30 jours pour expérimenter sans licence—idéal pour un proof‑of‑concept.

## Configuration de GroupDocs.Signature pour Java

Intégrer GroupDocs.Signature à votre projet est simple. Choisissez le système de gestion de dépendances qui correspond à votre configuration :

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
Vous préférez ne pas utiliser d’outil de construction ? Téléchargez le JAR directement depuis la [page des releases GroupDocs.Signature pour Java](https://releases.groupdocs.com/signature/java/) et ajoutez‑le manuellement au classpath de votre projet.

### Configuration de la licence

Voici le chemin de licence le plus couramment suivi par les développeurs :

1. **Commencer avec l’essai gratuit** – Aucun carte bancaire, aucun engagement. Parfait pour les tests.  
2. **Obtenir une licence temporaire** – Si 30 jours ne suffisent pas, demandez une licence temporaire pour prolonger le développement.  
3. **Acheter pour la production** – Une fois prêt à déployer, achetez une licence adaptée à votre volume d’utilisation.

**Important** : L’essai gratuit ajoute des filigranes aux documents de sortie. Pour un travail destiné aux clients, vous aurez besoin d’au moins une licence temporaire.

### Code d’initialisation

Une fois les dépendances en place, initialisez l’objet Signature comme suit :

```java
import com.groupdocs.signature.Signature;

// Initialize Signature object with your document path
Signature signature = new Signature("YOUR_DOCUMENT_DIRECTORY/sample.pdf");
```

**Ce qui se passe** : la classe `Signature` est votre point d’entrée principal. Vous lui passez un chemin de fichier, et elle charge le PDF en mémoire pour le traitement. Simple, non ?

**Erreur fréquente à éviter** : n’oubliez pas de fermer l’objet Signature lorsque vous avez terminé (ou utilisez try‑with‑resources). Le laisser ouvert peut entraîner des fuites de mémoire dans les applications de longue durée.

## Choisir le bon type de code‑barres

Tous les codes‑barres ne se valent pas. Le type que vous choisissez dépend de ce que vous devez encoder et de l’endroit où le code‑barres sera scanné.

### Types de codes‑barres populaires pris en charge

**Code128** (exemple utilisé) : Idéal pour encoder des données alphanumériques. Couramment utilisé sur les étiquettes d’expédition et les emballages. Supporte lettres, chiffres et quelques caractères spéciaux.

**QR Codes** : Parfait lorsque vous devez stocker plus de données (URL, JSON, etc.). Peut contenir jusqu’à 4 000 caractères et reste lisible même partiellement endommagé.

**Code39** : Plus simple que le Code128 mais moins efficace en termes d’espace. Bon pour le suivi interne où la simplicité prime sur la densité de données.

**EAN/UPC** : Standard industriel pour les produits de détail. Si vous générez des factures devant correspondre aux systèmes de vente au détail, c’est le choix à faire.

**Quand utiliser lequel ?**
- Besoin de plus de 50 caractères ? → QR Code  
- Identification produit standard ? → EAN/UPC  
- Suivi général de documents ? → Code128  
- Compatibilité maximale avec les scanners hérités ? → Code39  

**Astuce** : Code128 est le choix par défaut le plus sûr pour la gestion documentaire. Il équilibre lisibilité, capacité de données et compatibilité scanner.

## Guide d’implémentation : création de signatures de code‑barres

Passons à la partie pratique — créons et ajoutons des codes‑barres à vos PDF. Je décompose le processus en étapes gérables afin que vous puissiez suivre (ou sauter les parties qui ne vous intéressent pas).

### Étape 1 : configuration des chemins de documents

Première chose — indiquez à Java où se trouve votre PDF et où enregistrer la version signée :

```java
String filePath = "YOUR_DOCUMENT_DIRECTORY/sample.pdf";
String fileName = new File(filePath).getName();
```

**Ce qui se passe** : vous définissez le chemin du fichier d’entrée et extrayez simplement le nom de fichier. Cela garde vos sorties organisées (particulièrement utile en traitement par lots).

**Conseil réel** : en production, ces chemins proviennent généralement de fichiers de configuration ou de variables d’environnement—not pas de chaînes codées en dur. Pensez à `System.getenv()` ou à un fichier *.properties* pour plus de flexibilité.

### Étape 2 : configuration de la sortie et des options de code‑barres

Ensuite, définissez où le document signé sera enregistré et quel code‑barres créer :

```java
// Define output file path
String outputFilePath = "YOUR_OUTPUT_DIRECTORY/SignWithMillimeters/" + fileName;

BarcodeSignOptions options = new BarcodeSignOptions("12345678");
options.setEncodeType(BarcodeTypes.Code128);
```

**Décomposition** :
- `outputFilePath` : emplacement du PDF final. Remarquez la sous‑structure de dossiers ? Cela aide à organiser les différentes méthodes de signature.  
- `BarcodeSignOptions("12345678")` : les données encodées dans le code‑barres. Cela peut être un numéro de facture, un ID de suivi, un hash de document—ce que vous voulez.  
- `setEncodeType(BarcodeTypes.Code128)` : indique à GroupDocs le format de code‑barres à utiliser.

**Question fréquente** : « Puis‑je utiliser des caractères spéciaux dans les données du code‑barres ? » Avec Code128, oui — lettres, chiffres et la plupart des ponctuations sont acceptés. Les QR codes sont encore plus souples.

### Étape 3 : positionnement précis du code‑barres

Voici la partie intéressante. Vous pouvez positionner les codes‑barres avec une précision au millimètre :

```java
// Set position and size in millimeters
options.setLocationMeasureType(MeasureType.Millimeters);
options.setLeft(40);  // X-coordinate from left edge
options.setTop(50);   // Y-coordinate from top edge

options.setSizeMeasureType(MeasureType.Millimeters);
options.setWidth(20);  // Width of the barcode
options.setHeight(10); // Height of the barcode
```

**Pourquoi les millimètres ?** : lors de l’impression, les millimètres offrent une taille cohérente quel que soit le format de papier ou la résolution. (Vous pouvez aussi utiliser des pixels ou des pourcentages si cela convient mieux à votre cas.)

**Stratégies de positionnement** :
- **Coin supérieur droit** (comme les étiquettes d’expédition) : `setLeft(150)`, `setTop(10)`  
- **Centre inférieur** (comme les billets) : calculez le centre à partir de la largeur de la page  
- **À côté d’un contenu existant** : mesurez la mise en page du PDF et positionnez en conséquence

**Astuce** : testez le positionnement sur quelques PDF d’exemple avant de lancer le traitement par lots. Des mises en page différentes peuvent nécessiter de légers ajustements.

### Étape 4 : ajout de marges pour le rendu

Les marges évitent que le code‑barres ne se retrouve trop près d’autres éléments :

```java
// Define margin settings
Padding padding = new Padding();
padding.setLeft(5);   // Left margin in mm
padding.setTop(5);    // Top margin in mm
padding.setRight(5);  // Right margin in mm
padding.setBottom(5); // Bottom margin in mm
options.setMargin(padding);
```

**Ce que cela fait** : crée une zone tampon de 5 mm autour du code‑barres. Cet espace améliore la lisibilité et donne un aspect plus professionnel.

**Quand augmenter les marges** : si vous placez le code‑barres près du bord de la page, passez à 10 mm. Les imprimantes ont souvent du mal à reproduire du contenu trop proche des bords.

### Étape 5 : signature et sauvegarde du document

Le moment tant attendu — ajouter réellement le code‑barres :

```java
// Sign and save the document
SignResult signResult = signature.sign(outputFilePath, options);
```

**Ce qui se passe en coulisses** : GroupDocs ouvre votre PDF, génère le code‑barres selon vos options, l’insère à la position indiquée, puis enregistre le fichier modifié. Le PDF original reste intact.

**Valeur de retour** : l’objet `SignResult` contient le statut de succès/échec et des métadonnées sur ce qui a été signé. Vous pouvez l’inspecter pour vérifier le bon déroulement.

### Étape 6 : gestion des erreurs de façon robuste

Des problèmes peuvent survenir (chemins erronés, PDF corrompu, permissions insuffisantes). Gérez les exceptions correctement :

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

**Erreurs courantes** :
- `FileNotFoundException` : le chemin du PDF d’entrée est incorrect  
- `GroupDocsSignatureException` : données de code‑barres invalides ou version PDF non prise en charge  
- `OutOfMemoryError` : traitement de trop nombreux PDF volumineux simultanément

## Comment créer un PDF avec signature de code‑barres en Java

Si vous préférez une checklist concise, la voici :

1. **Ajouter la dépendance GroupDocs.Signature** (Maven, Gradle ou JAR manuel).  
2. **Initialiser `Signature`** avec le chemin du PDF source.  
3. **Configurer `BarcodeSignOptions`** — définir les données, le type, la taille et la position.  
4. **Optionnel : définir les marges** pour améliorer la lisibilité.  
5. **Appeler `signature.sign(outputPath, options)`** pour intégrer le code‑barres.  
6. **Gérer les exceptions** et fermer les ressources.

En suivant ces six étapes, vous pourrez **créer des PDF avec signature de code‑barres** de façon fiable dans n’importe quelle application Java.

## Problèmes courants & solutions

Abordons les difficultés que rencontrent réellement les développeurs (parce que la documentation ne couvre pas toujours tout) :

### Problème 1 : le code‑barres ne se scanne pas correctement

**Symptômes** : le scanner ne lit pas le code‑barres ou renvoie des données erronées.

**Solutions** :
- Augmentez la taille du code‑barres (minimum 15 mm de largeur pour la plupart des scanners)  
- Vérifiez que les données n’incluent pas de caractères non supportés pour le type choisi  
- Assurez‑vous d’un bon contraste entre le code‑barres et le fond  
- Testez avec plusieurs applications de scanner—certaines sont plus performantes que d’autres

### Problème 2 : le positionnement du code‑barres varie d’un document à l’autre

**Symptômes** : le même code produit des positions différentes selon les PDF.

**Solutions** :
- Les PDF de tailles différentes nécessitent des calculs de position, pas de valeurs fixes  
- Vérifiez la rotation éventuelle des PDF sources (cela décale les coordonnées)  
- Utilisez un positionnement basé sur les pourcentages pour plus de cohérence  
- Normalisez les PDF d’entrée à une taille de page standard lorsque c’est possible

### Problème 3 : dégradation des performances avec de gros lots

**Symptômes** : les 100 premiers PDF sont rapides, puis le traitement ralentit.

**Solutions** :
- Fermez rapidement les objets `Signature` (ou utilisez try‑with‑resources)  
- Traitez en lots plus petits avec nettoyage de la mémoire entre chaque lot  
- Envisagez le traitement parallèle pour les opérations CPU‑intensives  
- Surveillez l’utilisation du heap — vous pourriez devoir ajuster les paramètres JVM

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

**Symptômes** : les PDF signés sont beaucoup plus gros que les originaux.

**Solutions** :
- GroupDocs ne compresse pas automatiquement — prévoir une compression séparée si besoin  
- Évitez d’ajouter des images de code‑barres haute résolution quand les vecteurs suffisent  
- Vérifiez que vous n’incorporez pas accidentellement des polices ou des métadonnées superflues

**Quand contacter le support** : si vous avez appliqué ces solutions et que le problème persiste, le [forum GroupDocs](https://forum.groupdocs.com/c/signature/) dispose d’une équipe réactive.

## Cas d’utilisation réels

Voici comment différents secteurs exploitent cette fonctionnalité :

### Secteur juridique : gestion de contrats
Les cabinets d’avocats apposent des codes‑barres sur les contrats pour les relier aux systèmes de gestion de dossiers. Lorsqu’un contrat arrive par courrier, le personnel le scanne et le système récupère instantanément tout l’historique du dossier. Cela réduit le temps de traitement de minutes à quelques secondes.

**Astuce d’implémentation** : encodez un hash du document dans le code‑barres afin de vérifier que le support physique n’a pas été altéré.

### Santé : dossiers patients
Les hôpitaux ajoutent des codes‑barres aux résumés de sortie et aux ordonnances PDF. À l’arrivée du patient, le personnel scanne le code‑barres pour remplir automatiquement le dossier avec l’historique des visites.

**Note conformité** : assurez‑vous que votre implémentation respecte les exigences HIPAA concernant le codage des données.

### Logistique : étiquettes d’expédition
Les plateformes e‑commerce génèrent automatiquement des codes‑barres de suivi sur les bordereaux d’emballage. Les équipes d’entrepôt les scannent pour mettre à jour le statut d’expédition sans saisie manuelle.

**Considération de performance** : ces systèmes traitent souvent des milliers de documents par heure—le traitement par lots et l’exécution parallèle sont essentiels.

### Finance : traitement de factures
Les services comptables ajoutent des codes‑barres aux factures contenant les conditions de paiement et les identifiants fournisseurs. Lors de la réception, le scan oriente automatiquement la facture vers le bon workflow d’approbation.

**Astuce** : combinez les codes‑barres avec l’OCR pour une automatisation maximale — le code‑barres fournit les métadonnées, l’OCR extrait les lignes de facturation.

## Bonnes pratiques de performance

Lorsque vous traitez des documents à grande échelle, ces optimisations font réellement la différence :

### Gestion de la mémoire
- **Utilisez try‑with‑resources** : garantit la fermeture correcte des objets `Signature`.  
- **Traitez par lots** : ne chargez pas 10 000 PDF en mémoire simultanément.  
- **Surveillez l’utilisation du heap** : définissez des paramètres JVM appropriés (`-Xmx`, `-Xms`).

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

**Attention** : le traitement parallèle consomme plus de mémoire. Surveillez et ajustez en conséquence.

### Mise en cache des objets Signature
Si vous traitez régulièrement des documents similaires, réutilisez la configuration :

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

## Questions fréquentes

**Q : Comment créer un PDF avec signature de code‑barres en Java pour différents types de codes‑barres ?**  
R : Modifiez le paramètre de `setEncodeType()`. Pour les QR codes, utilisez `BarcodeTypes.QR`. Pour EAN‑13, `BarcodeTypes.EAN13`. GroupDocs prend en charge plus de 60 types de codes‑barres prêts à l’emploi.

**Q : Puis‑je ajouter plusieurs codes‑barres au même PDF ?**  
R : Absolument. Appelez `signature.sign()` plusieurs fois avec des `BarcodeSignOptions` différents, ou passez une liste d’options de signature en un seul appel.

**Q : Comment ajouter un code‑barres à un PDF existant sans perdre le contenu ?**  
R : GroupDocs est non destructif par défaut — il ajoute les codes‑barres comme une nouvelle couche sans modifier le contenu existant. Votre texte, images et mise en forme restent intacts.

**Q : Quelle est la quantité maximale de données que je peux encoder dans un code‑barres ?**  
R : Cela dépend du type. Code128 gère confortablement environ 128 caractères. Les QR codes peuvent stocker jusqu’à 4 000 caractères. Si vous avez besoin de plus, envisagez d’encoder une URL pointant vers vos données.

**Q : Ai‑je besoin d’une licence pour la production ?**  
R : Oui. L’essai gratuit ajoute des filigranes. Pour les déploiements en production, choisissez une licence temporaire (pour les tests prolongés) ou une licence achetée. Consultez la [page de tarification GroupDocs](https://purchase.groupdocs.com/buy) pour les options actuelles.

**Q : Comment gérer les exceptions lors du traitement par lots ?**  
R : Encapsulez chaque opération de fichier dans son propre bloc try‑catch afin qu’un PDF échoué n’arrête pas tout le lot. Loggez les erreurs avec le nom du fichier pour pouvoir les retraiter plus tard.

**Q : GroupDocs peut‑il générer des codes‑barres 2D comme Data Matrix ?**  
R : Oui ! Utilisez `BarcodeTypes.DataMatrix`. Les codes Data Matrix sont populaires en fabrication car ils restent lisibles même partiellement endommagés ou à des angles inhabituels.

**Q : Quels versions de PDF sont prises en charge par GroupDocs ?**  
R : GroupDocs.Signature gère les PDF de la version 1.3 à 2.0 (couvre 99 % des PDF rencontrés). Si vous avez des PDF très anciens, pensez à les convertir d’abord.

## Conclusion

Vous savez maintenant comment **ajouter un code‑barres aux documents PDF Java** de façon programmatique avec GroupDocs.Signature. Nous avons couvert tout, de la configuration de base à la gestion d’erreurs en production et à l’optimisation des performances.

**Points clés**
- Les codes‑barres résolvent de vrais problèmes de flux (automatisation, vérification, traçabilité)  
- GroupDocs vous donne un contrôle précis sur le positionnement et les types de codes‑barres  
- Une bonne gestion des erreurs et des ressources évite les maux de tête en production  
- L’optimisation des performances devient cruciale lorsqu’on traite des volumes importants  

**Prochaines étapes** : commencez par un petit proof‑of‑concept avec l’essai gratuit. Testez différents types de codes‑barres avec vos documents réels. Une fois validé, passez au traitement par lots puis au déploiement en production.

Des questions ou des problèmes ? Publiez‑les sur le [forum de support GroupDocs](https://forum.groupdocs.com/c/signature/) — la communauté est réactive et les temps de réponse sont bons.

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

**Dernière mise à jour :** 2026-01-08  
**Testé avec :** GroupDocs.Signature 23.12 pour Java  
**Auteur :** GroupDocs