---
title: Signature de documents avec code QR à l'aide de GroupDocs.Signature
linktitle: Signature avec QR Code
second_title: API GroupDocs.Signature .NET
description: Découvrez comment ajouter des signatures de code QR à vos documents avec GroupDocs.Signature pour .NET. Améliorez la sécurité et l’authentification sans effort.
weight: 15
url: /fr/net/advanced-signature-techniques/sign-with-qr-code/
---

# Signature de documents avec code QR à l'aide de GroupDocs.Signature

## Introduction
Dans ce didacticiel, nous allons parcourir le processus de signature de documents avec un code QR à l'aide de GroupDocs.Signature pour .NET. GroupDocs.Signature for .NET est une API puissante qui permet aux développeurs d'ajouter par programme différents types de signatures aux documents numériques. La signature de documents avec des codes QR peut fournir une couche supplémentaire de sécurité et d'authentification à vos documents.
## Conditions préalables
Avant de commencer, assurez-vous que les prérequis suivants sont installés :
1.  GroupDocs.Signature pour .NET : vous pouvez télécharger la bibliothèque à partir du[site web](https://releases.groupdocs.com/signature/net/).
2. Environnement de développement : assurez-vous d'avoir un environnement de développement .NET configuré sur votre ordinateur.
3. Exemple de document : préparez un exemple de document (par exemple, PDF) que vous souhaitez signer avec un code QR.

## Importation des espaces de noms nécessaires
Avant de plonger dans le code, importons les espaces de noms nécessaires :
```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

## Étape 1 : Définir les chemins de fichiers
```csharp
string filePath = "sample.pdf";
string fileName = Path.GetFileName(filePath);
string outputFilePath = Path.Combine("Your Document Directory", "SignWithQRCode", fileName);
```
 Assurez-vous de remplacer`"Your Document Directory"` avec le chemin d'accès au répertoire dans lequel vous souhaitez enregistrer le document signé.
## Étape 2 : initialiser l'objet de signature
```csharp
using (Signature signature = new Signature(filePath))
{
    //Le code pour signer va ici
}
```
 Initialiser un`Signature` objet avec le chemin d’accès au document que vous souhaitez signer.
## Étape 3 : Créer des options QRCodeSign
```csharp
QrCodeSignOptions options = new QrCodeSignOptions("JohnSmith")
{
    EncodeType = QrCodeTypes.QR,
    Left = 50,
    Top = 150,
    Width = 200,
    Height = 200
};
```
 Créer un`QrCodeSignOptions` objet avec les paramètres souhaités pour la signature du code QR. Vous pouvez personnaliser des paramètres tels que le texte à encoder, la position et les dimensions du code QR.
## Étape 4 : Signez le document
```csharp
SignResult result = signature.Sign(outputFilePath, options);
```
 Utilisez le`Sign` méthode du`Signature` objet pour signer le document avec les options spécifiées. Cette méthode renvoie un`SignResult` objet contenant des informations sur le processus de signature.
## Étape 5 : Afficher le résultat
```csharp
Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).\nFile saved at {outputFilePath}.");
```
Afficher un message indiquant le succès du processus de signature et l'emplacement où le document signé est enregistré.

## Conclusion
Dans ce didacticiel, nous avons appris à signer des documents avec un code QR à l'aide de GroupDocs.Signature pour .NET. En suivant ces étapes simples, vous pouvez ajouter des signatures de code QR à vos documents numériques, améliorant ainsi la sécurité et l'authentification.

## FAQ
### Puis-je personnaliser l'apparence du code QR ?
Oui, vous pouvez personnaliser divers paramètres tels que la taille, la position et le type d'encodage du code QR en fonction de vos besoins.
### Quels formats de documents sont pris en charge pour la signature avec des codes QR ?
GroupDocs.Signature pour .NET prend en charge un large éventail de formats de documents, notamment PDF, Word, Excel, PowerPoint, etc.
### Est-il possible de signer plusieurs documents dans un processus par lots ?
Absolument, vous pouvez utiliser GroupDocs.Signature pour .NET pour signer plusieurs documents simultanément, rationalisant ainsi votre flux de travail.
### Puis-je vérifier l'authenticité d'un document signé avec un code QR ?
Oui, GroupDocs.Signature pour .NET fournit des mécanismes de vérification pour garantir l'intégrité et l'authenticité des documents signés.
### Existe-t-il une version d'essai disponible pour tester la fonctionnalité avant d'acheter ?
 Oui, vous pouvez télécharger une version d'essai gratuite à partir du[site web](https://releases.groupdocs.com/) pour évaluer les fonctionnalités et les capacités de GroupDocs.Signature pour .NET.