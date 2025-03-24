---
title: Supprimer la signature du code QR du document
linktitle: Supprimer la signature du code QR du document
second_title: API GroupDocs.Signature .NET
description: Découvrez comment supprimer les signatures de code QR des documents à l'aide de GroupDocs.Signature pour .NET. Suivez notre guide étape par étape pour une gestion efficace des signatures.
weight: 16
url: /fr/net/delete-operations/delete-qr-code-signature/
---
## Introduction
Dans ce didacticiel, nous vous guiderons tout au long du processus de suppression d'une signature de code QR d'un document à l'aide de GroupDocs.Signature pour .NET. Suivez ces instructions étape par étape pour supprimer efficacement les signatures de code QR.
## Conditions préalables
Avant de commencer, assurez-vous de disposer des conditions préalables suivantes :
-  GroupDocs.Signature pour .NET : assurez-vous que la bibliothèque GroupDocs.Signature est installée dans votre projet .NET. Vous pouvez le télécharger depuis[ici](https://releases.groupdocs.com/signature/net/).
- Document avec signature de code QR : préparez un document contenant les signatures de code QR que vous souhaitez supprimer.
- Connaissance de base de C# : Familiarisez-vous avec les bases du langage de programmation C#.

## Importation d'espaces de noms
Avant de plonger dans le code, importez les espaces de noms nécessaires dans votre fichier C# :
```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## Étape 1 : Définir les chemins de fichiers
```csharp
// Le chemin d'accès au répertoire des documents.
string filePath = "sample_multiple_signatures.docx";
string fileName = Path.GetFileName(filePath);
// Définissez le chemin du fichier de sortie pour le document modifié.
string outputFilePath = Path.Combine("Your Document Directory", "DeleteQRCode", fileName);
// Copiez le fichier source puisque la méthode Supprimer fonctionne avec le même document.
File.Copy(filePath, outputFilePath, true);
```
## Étape 2 : initialiser l'objet de signature
```csharp
using (Signature signature = new Signature(outputFilePath))
{
    // Créez des options pour rechercher les signatures de code QR.
    QrCodeSearchOptions options = new QrCodeSearchOptions();
    // Recherchez les signatures de code QR dans le document.
    List<QrCodeSignature> signatures = signature.Search<QrCodeSignature>(options);
```
## Étape 3 : Vérifier l'existence de la signature du code QR
```csharp
    if (signatures.Count > 0)
    {
        // Obtenez la première signature de code QR trouvée dans le document.
        QrCodeSignature qrCodeSignature = signatures[0];
```
## Étape 4 : Supprimer la signature du code QR
```csharp
        // Supprimez la signature du code QR du document.
        bool result = signature.Delete(qrCodeSignature);
        if (result)
        {
            Console.WriteLine($"Signature with QR-Code '{qrCodeSignature.Text}' and encode type '{qrCodeSignature.EncodeType.TypeName}' was deleted from document ['{fileName}'].");
        }
        else
        {
            Helper.WriteError($"Signature was not deleted from the document! Signature with Barcode '{qrCodeSignature.Text}' and encode type '{qrCodeSignature.EncodeType.TypeName}' was not found!");
        }
    }
}
```
Toutes nos félicitations! Vous avez réussi à supprimer la signature du code QR du document à l'aide de GroupDocs.Signature pour .NET.

## Conclusion
Dans ce didacticiel, nous avons appris à supprimer une signature de code QR d'un document à l'aide de GroupDocs.Signature pour .NET. En suivant les étapes fournies, vous pouvez gérer et manipuler efficacement les signatures au sein de vos applications .NET.
## FAQ
### Puis-je supprimer plusieurs signatures de code QR d’un document ?
Oui, vous pouvez modifier le code pour parcourir toutes les signatures de code QR et les supprimer en conséquence.
### GroupDocs.Signature prend-il en charge d'autres types de signatures en plus des codes QR ?
Oui, GroupDocs.Signature prend en charge différents types de signature tels que le texte, l'image, le code-barres, etc.
### GroupDocs.Signature est-il compatible avec tous les formats de documents ?
GroupDocs.Signature prend en charge un large éventail de formats de documents, notamment PDF, Microsoft Word, Excel, PowerPoint, etc.
### Puis-je personnaliser les options de recherche de signatures ?
Oui, vous pouvez adapter les options de recherche en fonction de vos besoins pour localiser des signatures spécifiques dans le document.
### Existe-t-il une version d’essai disponible pour GroupDocs.Signature ?
 Oui, vous pouvez accéder à une version d'essai gratuite de GroupDocs.Signature à partir de[ici](https://releases.groupdocs.com/).