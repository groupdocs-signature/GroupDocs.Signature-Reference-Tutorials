---
title: Signer une image avec des métadonnées
linktitle: Signer une image avec des métadonnées
second_title: API GroupDocs.Signature .NET
description: Découvrez comment signer des images avec des métadonnées dans .NET à l'aide de GroupDocs.Signature. Solution de signature de métadonnées simple, efficace et personnalisable.
weight: 10
url: /fr/net/document-signing/sign-image-with-metadata/
---
## Introduction
GroupDocs.Signature pour .NET permet aux développeurs de signer efficacement des images avec des métadonnées. Ce tutoriel vous guide pas à pas tout au long du processus.
## Conditions préalables
Avant de commencer, assurez-vous d'avoir les éléments suivants :
1. GroupDocs.Signature pour .NET : installez le package GroupDocs.Signature dans votre projet .NET. Vous pouvez le télécharger depuis[ici](https://releases.groupdocs.com/signature/net/).   
2. Fichier image : préparez le fichier image que vous souhaitez signer avec des métadonnées.

## Importer des espaces de noms
Assurez-vous d'importer les espaces de noms nécessaires dans votre code C# :
```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## Étape 1 : Charger le fichier image
Tout d'abord, spécifiez le chemin d'accès à votre fichier image et le répertoire de sortie de l'image signée avec les métadonnées :
```csharp
string filePath = "sample.png";            
string outputFilePath = Path.Combine("Your Document Directory", "SignImageWithMetadata", "SignedWithMetadata.png");
```
## Étape 2 : Créer des signatures de métadonnées
Ensuite, créez différentes signatures de métadonnées et ajoutez-les à la collection de signatures d'options :
```csharp
using (Signature signature = new Signature(filePath))
{
    ushort imgsMetadataId = 41996;
    MetadataSignOptions options = new MetadataSignOptions();
    options
        .Add(new ImageMetadataSignature(imgsMetadataId++, "Mr.Scherlock Holmes")) // Valeur de chaîne
        .Add(new ImageMetadataSignature(imgsMetadataId++, DateTime.Now))          // Valeur de l'heure et de la date
        .Add(new ImageMetadataSignature(imgsMetadataId++, 123456))                // Valeur entière
        .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456D))              // Valeur double
        .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456M))              // Valeur décimale
        .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456F));             // Valeur flottante
    
    // signer le document à déposer
    SignResult result = signature.Sign(outputFilePath, options);
    Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).\nFile saved at {outputFilePath}.");
}
```

## Conclusion
Dans ce didacticiel, vous avez appris à signer une image avec des métadonnées à l'aide de GroupDocs.Signature pour .NET. En suivant ces étapes, vous pouvez facilement incorporer des signatures de métadonnées dans vos applications .NET.

## FAQ
### Puis-je signer plusieurs images avec des métadonnées à l’aide de GroupDocs.Signature pour .NET ?
Oui, vous pouvez signer plusieurs images avec des métadonnées en parcourant chaque fichier image et en appliquant les signatures de métadonnées.
### Existe-t-il une version d’essai disponible pour GroupDocs.Signature pour .NET ?
 Oui, vous pouvez télécharger la version d'essai à partir de[ici](https://releases.groupdocs.com/).
### GroupDocs.Signature pour .NET prend-il en charge d’autres formats de fichiers que les images ?
Oui, GroupDocs.Signature prend en charge divers formats de fichiers, notamment PDF, Word, Excel, etc.
### Puis-je personnaliser l’apparence de la signature des métadonnées ?
Oui, vous pouvez personnaliser l'apparence de la signature des métadonnées, comme la taille, la couleur et la position de la police.
### Où puis-je obtenir de l’assistance pour GroupDocs.Signature pour .NET ?
 Vous pouvez obtenir de l'aide sur le forum GroupDocs.Signature[ici](https://forum.groupdocs.com/c/signature/13).