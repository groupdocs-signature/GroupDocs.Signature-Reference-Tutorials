---
title: Signature avec plusieurs options
linktitle: Signature avec plusieurs options
second_title: API GroupDocs.Signature .NET
description: Découvrez comment signer des documents avec plusieurs options à l'aide de GroupDocs.Signature pour .NET. Améliorez la sécurité des documents avec du texte, des codes-barres, des codes QR, des données numériques et des images.
type: docs
weight: 14
url: /fr/net/advanced-signature-techniques/sign-with-multiple-options/
---
## Introduction
Dans ce didacticiel, nous allons explorer comment signer un document à l'aide de plusieurs options de signature à l'aide de la bibliothèque GroupDocs.Signature pour .NET. La signature de documents avec diverses options telles que les signatures de texte, de code-barres, de code QR, numérique, d'image et de métadonnées peut offrir une polyvalence et améliorer la sécurité des documents.
## Conditions préalables
Avant de commencer, assurez-vous de disposer des prérequis suivants :
1.  Bibliothèque GroupDocs.Signature pour .NET : téléchargez et installez la bibliothèque GroupDocs.Signature pour .NET à partir de[ici](https://releases.groupdocs.com/signature/net/).
2. Environnement de développement : configurez un environnement de développement avec .NET Framework installé.
3. Document à signer : Préparez le document (par exemple, sample.docx) que vous souhaitez signer.
4. Certificats et images : préparez tous les certificats et images requis pour les signatures numériques et d'images.

## Importer des espaces de noms
Tout d’abord, importez les espaces de noms nécessaires pour utiliser la bibliothèque GroupDocs.Signature dans votre application .NET :
```csharp
using System;
using System.IO;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## Étape 1 : Charger le document
```csharp
string filePath = "sample.docx";
string outputFilePath = Path.Combine("Your Document Directory", "SignWithMultiple", "SignWithMultiple.docx");
using (Signature signature = new Signature(filePath))
{
    // Votre code continue...
}
```
## Étape 2 : définir les options de signature
Définissez plusieurs options de signature de différents types et paramètres, tels que les signatures de texte, de code-barres, de code QR, numérique, d'image et de métadonnées :
```csharp
TextSignOptions textOptions = new TextSignOptions("Text signature")
{
    VerticalAlignment = VerticalAlignment.Top,
    HorizontalAlignment = HorizontalAlignment.Left
};
BarcodeSignOptions barcodeOptions = new BarcodeSignOptions("123456")
{
    EncodeType = BarcodeTypes.Code128,
    Left = 0,
    Top = 150,
    Height = 50,
    Width = 200
};
// Définir d'autres options de signature (par exemple, code QR, numérique, image, métadonnées)...
```
## Étape 3 : Créer une liste d'options de signature
Définissez une liste d'options de signature contenant toutes les options définies précédemment :
```csharp
List<SignOptions> listOptions = new List<SignOptions>();
listOptions.Add(textOptions);
listOptions.Add(barcodeOptions);
// Ajoutez d'autres options de signature à la liste...
```
## Étape 4 : Signez le document
Signez le document avec la liste des options de signature et enregistrez le document signé :
```csharp
SignResult result = signature.Sign(outputFilePath, listOptions);
Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).\nFile saved at {outputFilePath}.");
```

## Conclusion
La signature de documents avec plusieurs options à l'aide de GroupDocs.Signature pour .NET fournit une solution robuste pour améliorer la sécurité et la polyvalence des documents. En suivant les étapes décrites dans ce didacticiel, vous pouvez intégrer de manière transparente différents types de signatures dans vos applications .NET.
## FAQ
### Puis-je utiliser des images personnalisées pour les signatures numériques ?
Oui, vous pouvez spécifier des images personnalisées pour les signatures numériques à l'aide de la bibliothèque GroupDocs.Signature.
### GroupDocs.Signature est-il compatible avec différents formats de documents ?
Oui, GroupDocs.Signature prend en charge divers formats de documents, notamment DOCX, PDF, PPTX, etc.
### Puis-je personnaliser l’apparence des signatures textuelles ?
Absolument, vous pouvez personnaliser l'apparence des signatures de texte, notamment la taille, la couleur et le style de la police.
### GroupDocs.Signature fournit-il le cryptage des signatures numériques ?
Oui, GroupDocs.Signature propose des options de cryptage pour les signatures numériques afin de garantir la sécurité des documents.
### Existe-t-il une version d’essai disponible pour GroupDocs.Signature pour .NET ?
 Oui, vous pouvez télécharger une version d'essai gratuite de GroupDocs.Signature pour .NET à partir de[ici](https://releases.groupdocs.com/).