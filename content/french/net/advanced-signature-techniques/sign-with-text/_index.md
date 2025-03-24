---
title: Signature avec du texte à l'aide de GroupDocs.Signature pour .NET
linktitle: Signer avec du texte
second_title: API GroupDocs.Signature .NET
description: Découvrez comment signer des documents avec du texte à l'aide de GroupDocs.Signature pour .NET. Guide étape par étape pour ajouter des signatures de texte par programmation.
weight: 17
url: /fr/net/advanced-signature-techniques/sign-with-text/
---
## Introduction
À l’ère du numérique, la signature électronique de documents est devenue une pratique courante, permettant d’économiser du temps et des ressources. GroupDocs.Signature pour .NET offre une solution complète pour ajouter par programme des signatures de texte à divers formats de documents. Dans ce didacticiel, nous vous guiderons tout au long du processus de signature d'un document contenant du texte à l'aide de GroupDocs.Signature pour .NET.
## Conditions préalables
Avant de plonger dans le didacticiel, assurez-vous de disposer des prérequis suivants :
1.  GroupDocs.Signature pour .NET : assurez-vous que la bibliothèque GroupDocs.Signature pour .NET est installée. Vous pouvez le télécharger depuis[ici](https://releases.groupdocs.com/signature/net/).
2. Environnement de développement : disposez d'un environnement de travail configuré pour le développement .NET.
3. Document : Préparez le document (par exemple, PDF, Word) que vous souhaitez signer avec du texte.

## Importer des espaces de noms
Tout d’abord, vous devez importer les espaces de noms nécessaires dans votre projet .NET pour utiliser les fonctionnalités GroupDocs.Signature.
```csharp
using System;
using System.IO;
using System.Drawing;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

Décomposons le processus de signature d'un document avec du texte en plusieurs étapes :
## Étape 1 : Charger le document
Chargez le document que vous souhaitez signer avec du texte.
```csharp
string filePath = "sample.pdf"; // Chemin d'accès au document
string fileName = Path.GetFileName(filePath);
```
## Étape 2 : Définir le chemin du fichier de sortie
Définissez le chemin du fichier de sortie où le document signé sera enregistré.
```csharp
string outputFilePath = Path.Combine("Your Document Directory", "SignWithText", fileName);
```
## Étape 3 : Créer des options de signature
Configurez les options de signature de texte, notamment le contenu du texte, la position, la taille, la couleur et la police.
```csharp
TextSignOptions options = new TextSignOptions("John Smith")
{
    Left = 50, // Définir la position de la signature
    Top = 200,
    Width = 100, // Définir le rectangle de signature
    Height = 30,
    ForeColor = Color.Red, // Définir la couleur du texte
    Font = new SignatureFont { Size = 14, FamilyName = "Comic Sans MS" } // Définir la police
};
```
## Étape 4 : Signer le document
Utilisez GroupDocs.Signature pour signer le document avec les options spécifiées et enregistrez le document signé dans le chemin du fichier de sortie.
```csharp
using (Signature signature = new Signature(filePath))
{
    SignResult result = signature.Sign(outputFilePath, options); // Signer le document
    Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).\nFile saved at {outputFilePath}.");
}
```

## Conclusion
Dans ce didacticiel, nous avons appris à signer un document avec du texte à l'aide de GroupDocs.Signature pour .NET. En suivant ces étapes, vous pouvez ajouter efficacement des signatures textuelles à vos documents par programmation, améliorant ainsi la sécurité et l'authenticité.
## FAQ
### Puis-je personnaliser l’apparence de la signature textuelle ?
Oui, vous pouvez personnaliser divers paramètres tels que la couleur, la police, la taille et la position de la signature textuelle selon vos préférences.
### GroupDocs.Signature est-il compatible avec plusieurs formats de documents ?
Oui, GroupDocs.Signature prend en charge divers formats de documents, notamment PDF, Word, Excel, PowerPoint, etc.
### Puis-je ajouter plusieurs signatures textuelles à un seul document ?
Absolument, vous pouvez ajouter plusieurs signatures textuelles à un document, chacune avec son propre ensemble d'options de personnalisation.
### GroupDocs.Signature garantit-il l’intégrité du document après la signature ?
Oui, GroupDocs.Signature utilise des algorithmes cryptographiques robustes pour garantir l'intégrité des documents et empêcher toute falsification après la signature.
### Existe-t-il une version d'essai disponible pour tester avant d'acheter ?
 Oui, vous pouvez télécharger une version d'essai gratuite à partir de[ici](https://releases.groupdocs.com/) pour explorer les fonctionnalités avant de faire un achat.