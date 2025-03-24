---
title: Signature avec Stamp à l'aide de GroupDocs.Signature
linktitle: Signature avec tampon
second_title: API GroupDocs.Signature .NET
description: Découvrez comment ajouter facilement des signatures de tampon à vos documents .NET avec GroupDocs.Signature pour .NET. Améliorez la sécurité des documents.
weight: 16
url: /fr/net/advanced-signature-techniques/sign-with-stamp/
---

# Signature avec Stamp à l'aide de GroupDocs.Signature

## Introduction
Dans ce didacticiel, nous vous guiderons tout au long du processus de signature d'un document avec un tampon à l'aide de GroupDocs.Signature pour .NET. En suivant ces instructions étape par étape, vous pourrez facilement ajouter une signature tampon à vos documents.
## Conditions préalables
Avant de commencer, assurez-vous de disposer des prérequis suivants :
1.  GroupDocs.Signature pour .NET SDK : téléchargez et installez le SDK à partir du[site web](https://releases.groupdocs.com/signature/net/).
2. Environnement de développement : assurez-vous de disposer d'un environnement de développement approprié configuré pour le développement .NET.
3. Document à signer : Préparez le document (par exemple, PDF) que vous souhaitez signer avec un tampon.

## Importation d'espaces de noms
Commencez par importer les espaces de noms nécessaires dans votre projet :
```csharp
using System;
using System.IO;
using System.Drawing;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## Étape 1 : Charger le document
```csharp
string filePath = "sample.pdf";
using (Signature signature = new Signature(filePath))
{
    // Votre code va ici
}
```
## Étape 2 : Définir les options de signe de tampon
```csharp
StampSignOptions options = new StampSignOptions()
{
    Left = 50,
    Top = 150,                    
    Width = 200,
    Height = 200
};
```
## Étape 3 : Configurer l'apparence du tampon
```csharp
StampLine outerLine = new StampLine();
outerLine.Text = " * European Union ";
outerLine.TextRepeatType = StampTextRepeatType.FullTextRepeat;
outerLine.Font.Size = 12;
outerLine.Height = 22;
outerLine.TextBottomIntent = 6;
outerLine.TextColor = Color.WhiteSmoke;
outerLine.BackgroundColor = Color.DarkSlateBlue;
options.OuterLines.Add(outerLine);
StampLine innerLine = new StampLine();
innerLine.Text = "John Smith";
innerLine.TextColor = Color.MediumVioletRed;
innerLine.Font.Size = 20;
innerLine.Font.Bold = true;
innerLine.Height = 40;
options.InnerLines.Add(innerLine);
```
## Étape 4 : Signez le document
```csharp
string outputFilePath = Path.Combine("Your Document Directory", "SignWithStamp", fileName);
SignResult result = signature.Sign(outputFilePath, options);
Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).\nFile saved at {outputFilePath}.");
```

## Conclusion
L'ajout de signatures de tampon à vos documents à l'aide de GroupDocs.Signature pour .NET est un processus simple, comme le démontre ce didacticiel. Avec les étapes fournies, vous pouvez facilement améliorer la sécurité et l'authenticité de vos documents.
## FAQ
### Puis-je personnaliser l’apparence de la signature du tampon ?
Oui, vous pouvez personnaliser divers aspects tels que le texte, la police, la couleur et le positionnement de la signature du tampon en fonction de vos besoins.
### GroupDocs.Signature prend-il en charge la signature de plusieurs formats de documents ?
Oui, GroupDocs.Signature prend en charge un large éventail de formats de documents, notamment PDF, Microsoft Word, Excel, PowerPoint, etc.
### Existe-t-il une version d’essai disponible pour GroupDocs.Signature ?
 Oui, vous pouvez accéder à la version d'essai gratuite à partir du[site web](https://releases.groupdocs.com/).
### Puis-je ajouter plusieurs signatures à un seul document ?
Absolument, GroupDocs.Signature vous permet d'ajouter plusieurs signatures, notamment des tampons, du texte, des images et des signatures numériques, à un seul document.
### Où puis-je trouver de l'aide si je rencontre des problèmes lors de la mise en œuvre ?
 Vous pouvez trouver du support et de l'assistance sur le forum de la communauté GroupDocs.Signature.[ici](https://forum.groupdocs.com/c/signature/13).