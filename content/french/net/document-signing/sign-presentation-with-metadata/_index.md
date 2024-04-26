---
title: Signer une présentation avec des métadonnées
linktitle: Signer une présentation avec des métadonnées
second_title: API GroupDocs.Signature .NET
description: Découvrez comment signer des fichiers de présentation avec des métadonnées à l'aide de GroupDocs.Signature pour .NET. Améliorez l’intégrité des documents et ajoutez des informations précieuses.
type: docs
weight: 12
url: /fr/net/document-signing/sign-presentation-with-metadata/
---
## Introduction
Dans ce didacticiel, nous apprendrons comment signer un fichier de présentation (PPTX) avec des métadonnées à l'aide de la bibliothèque GroupDocs.Signature pour .NET. La signature de présentations avec des métadonnées ajoute des informations précieuses au document, telles que le nom de l'auteur, la date de création, l'ID du document, l'ID de la signature et diverses valeurs numériques.
## Conditions préalables
Avant de commencer, assurez-vous d'avoir les éléments suivants :
1.  GroupDocs.Signature pour la bibliothèque .NET : téléchargez et installez la bibliothèque à partir de[ici](https://releases.groupdocs.com/signature/net/).
2. Environnement de développement : assurez-vous d'avoir configuré un environnement de développement .NET.
3. Fichier de présentation : préparez un exemple de fichier de présentation (format PPTX) à signer.
4. Compréhension de base de C# : Une connaissance du langage de programmation C# sera bénéfique.

## Importer des espaces de noms
Avant de plonger dans le code, importons les espaces de noms nécessaires :
```csharp
using System;
using System.IO;
    using GroupDocs.Signature;
    using GroupDocs.Signature.Domain;
    using GroupDocs.Signature.Options;
```
## Étape 1 : Charger le fichier de présentation
```csharp
string filePath = "sample.pptx";
```
 Remplacer`"sample.pptx"` avec le chemin d'accès à votre fichier de présentation.
## Étape 2 : Spécifier le chemin du fichier de sortie
```csharp
string outputFilePath = Path.Combine("Your Document Directory", "SignPresentationWithMetadata", "SignedWithMetadata.pptx");
```
Spécifiez le répertoire dans lequel vous souhaitez enregistrer le fichier de présentation signé ainsi que le nom du fichier.
## Étape 3 : initialiser l'objet de signature
```csharp
using (Signature signature = new Signature(filePath))
```
Initialisez un objet Signature en fournissant le chemin d'accès au fichier de présentation.
## Étape 4 : Définir les options de signature des métadonnées
```csharp
MetadataSignOptions options = new MetadataSignOptions();
```
Créez une instance de MetadataSignOptions pour définir les options de signature de métadonnées.
## Étape 5 : Créer des signatures de métadonnées
```csharp
PresentationMetadataSignature[] signatures = new PresentationMetadataSignature[]
{
    new PresentationMetadataSignature("Author", "Mr.Scherlock Holmes"),
    new PresentationMetadataSignature("CreatedOn", DateTime.Now),
    new PresentationMetadataSignature("DocumentId", 123456),
    new PresentationMetadataSignature("SignatureId", 123.456D),
    new PresentationMetadataSignature("Amount", 123.456M),
    new PresentationMetadataSignature("Total", 123.456F)
};
```
Créez un tableau d’objets PresentationMetadataSignature, chacun représentant une signature de métadonnées. Vous pouvez ajouter différents types de métadonnées, notamment chaîne, DateTime, entier, double, décimal et flottant.
## Étape 6 : ajouter des signatures aux options
```csharp
options.Signatures.AddRange(signatures);
```
Ajoutez les signatures de métadonnées créées à l'objet MetadataSignOptions.
## Étape 7 : signer le document
```csharp
SignResult result = signature.Sign(outputFilePath, options);
```
Signez le fichier de présentation avec les métadonnées à l'aide des options spécifiées et enregistrez le fichier signé dans le chemin de sortie.
## Étape 8 : Afficher le résultat
```csharp
Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).\nFile saved at {outputFilePath}.");
```
Affichez un message de réussite ainsi que le nombre de signatures appliquées et le chemin où le fichier signé est enregistré.

## Conclusion
Dans ce didacticiel, nous avons appris à signer un fichier de présentation avec des métadonnées à l'aide de la bibliothèque GroupDocs.Signature pour .NET. L'ajout de signatures de métadonnées améliore l'intégrité du document et fournit des informations précieuses sur son contenu.

## FAQ
### Puis-je signer d'autres formats de document que PPTX avec des métadonnées à l'aide de GroupDocs.Signature pour .NET ?
Oui, GroupDocs.Signature prend en charge divers formats de documents, notamment Word, Excel, PDF, etc., pour la signature avec des métadonnées.
### GroupDocs.Signature pour .NET est-il compatible avec .NET Core ?
Oui, la bibliothèque est compatible avec .NET Framework et .NET Core.
### Puis-je personnaliser l’apparence des signatures de métadonnées ?
Oui, vous pouvez personnaliser l'apparence, la position et d'autres propriétés des signatures de métadonnées en fonction de vos besoins.
### GroupDocs.Signature pour .NET fournit-il le cryptage des documents signés ?
Oui, GroupDocs.Signature propose des options de cryptage pour sécuriser les documents signés contre tout accès non autorisé.
### Existe-t-il une version d'essai disponible pour tester avant d'acheter ?
 Oui, vous pouvez bénéficier d'un essai gratuit de GroupDocs.Signature pour .NET à partir de[ici](https://releases.groupdocs.com/).