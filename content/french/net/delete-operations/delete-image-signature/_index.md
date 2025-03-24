---
title: Supprimer la signature de l'image
linktitle: Supprimer la signature de l'image
second_title: API GroupDocs.Signature .NET
description: Découvrez comment supprimer des signatures d'image de documents à l'aide de GroupDocs.Signature pour .NET. Suivez notre guide étape par étape pour une gestion efficace des signatures.
weight: 14
url: /fr/net/delete-operations/delete-image-signature/
---
## Introduction
Dans ce didacticiel, nous verrons comment supprimer des signatures d'image de documents à l'aide de GroupDocs.Signature pour .NET. GroupDocs.Signature est une bibliothèque puissante qui permet aux développeurs de travailler avec des signatures numériques, des tampons et des champs de formulaire dans différents formats de documents.
## Conditions préalables
Avant de commencer, assurez-vous d'avoir les éléments suivants :
### 1. GroupDocs.Signature pour .NET
 Téléchargez et installez GroupDocs.Signature pour .NET à partir du[site web](https://releases.groupdocs.com/signature/net/). Suivez les instructions d'installation fournies dans la documentation.
### 2. Cadre .NET
Assurez-vous que le .NET Framework est installé sur votre ordinateur.
## Importer des espaces de noms
Incluez les espaces de noms nécessaires dans votre projet :
```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
Décomposons le processus de suppression des signatures d'image en plusieurs étapes :
## Étape 1 : Définir les chemins de fichiers
Tout d'abord, spécifiez les chemins du document d'entrée et du document de sortie après avoir supprimé la signature :
```csharp
string filePath = "sample_multiple_signatures.docx";
string fileName = Path.GetFileName(filePath);
string outputFilePath = Path.Combine("Your Document Directory", "DeleteImage", fileName);
```
## Étape 2 : Copiez le fichier source
 Depuis le`Delete`fonctionne avec le même document, il est essentiel de copier le fichier source vers un autre emplacement :
```csharp
File.Copy(filePath, outputFilePath, true);
```
## Étape 3 : initialiser l'objet de signature
 Créez une instance du`Signature` class et spécifiez le chemin d'accès au document de sortie :
```csharp
using (Signature signature = new Signature(outputFilePath))
{
    // Le code va ici
}
```
## Étape 4 : Rechercher des signatures d'image
Définissez les options de recherche et recherchez des signatures d'images dans le document :
```csharp
ImageSearchOptions options = new ImageSearchOptions();
List<ImageSignature> signatures = signature.Search<ImageSignature>(options);
```
## Étape 5 : Supprimer la signature de l'image
Si des signatures d'images sont trouvées, supprimez la première :
```csharp
if (signatures.Count > 0)
{
    ImageSignature imageSignature = signatures[0];
    bool result = signature.Delete(imageSignature);
    if (result)
    {
        Console.WriteLine($"Image signature at location {imageSignature.Left}x{imageSignature.Top} and Size {imageSignature.Size} was deleted from document ['{fileName}'].");
    }
    else
    {
        Helper.WriteError($"Signature was not deleted from the document! Signature at location {imageSignature.Left}x{imageSignature.Top} and Size {imageSignature.Size} was not found!");
    }
}
```
## Conclusion
Dans ce didacticiel, nous avons appris à supprimer les signatures d'image des documents à l'aide de GroupDocs.Signature pour .NET. En suivant le guide étape par étape, les développeurs peuvent gérer efficacement les signatures numériques au sein de leurs applications.
## FAQ
### Puis-je supprimer plusieurs signatures d’image d’un document ?
 Oui, vous pouvez modifier le code pour supprimer plusieurs signatures d'image en itérant sur le`signatures` liste.
### GroupDocs.Signature prend-il en charge d'autres formats de documents que DOCX ?
Oui, GroupDocs.Signature prend en charge un large éventail de formats de documents, notamment PDF, PPT, XLS, etc.
### Existe-t-il une version d’essai disponible pour GroupDocs.Signature pour .NET ?
 Oui, vous pouvez télécharger une version d'essai gratuite à partir du[site web](https://releases.groupdocs.com/).
### Comment puis-je obtenir de l’aide pour GroupDocs.Signature ?
 Vous pouvez visiter le[Forum GroupDocs.Signature](https://forum.groupdocs.com/c/signature/13) pour obtenir de l'aide et du soutien.
### Puis-je acheter une licence temporaire pour GroupDocs.Signature ?
 Oui, vous pouvez acheter une licence temporaire auprès du[page d'achat](https://purchase.groupdocs.com/temporary-license/).