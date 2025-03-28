---
title: Supprimer la signature par ID
linktitle: Supprimer la signature par ID
second_title: API GroupDocs.Signature .NET
description: Découvrez comment supprimer une signature par ID dans des documents .NET à l'aide de la bibliothèque GroupDocs.Signature. Guide facile étape par étape.
weight: 11
url: /fr/net/delete-operations/delete-signature-by-id/
---

# Supprimer la signature par ID

## Introduction
Dans ce didacticiel, nous allons explorer comment supprimer une signature par son ID à l'aide de GroupDocs.Signature pour .NET. GroupDocs.Signature for .NET est une bibliothèque puissante qui permet aux développeurs d'ajouter, de supprimer ou de vérifier des signatures numériques dans divers formats de documents à l'aide d'applications .NET.
## Conditions préalables
Avant de commencer, assurez-vous d'avoir les prérequis suivants :
1.  GroupDocs.Signature pour la bibliothèque .NET : téléchargez et installez la bibliothèque à partir de[ici](https://releases.groupdocs.com/signature/net/).
2. .NET Framework : assurez-vous que .NET Framework est installé sur votre système.
3. Document avec signature : préparez un document (par exemple, DOCX, PDF) avec une signature que vous souhaitez supprimer.

## Importer des espaces de noms
```csharp
using System;
using System.IO;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## Étape 1 : Définir les chemins de fichiers
Tout d'abord, spécifiez le chemin du fichier du document contenant la signature et le chemin du fichier de sortie où le document modifié sera enregistré.
```csharp
string filePath = "sample_multiple_signatures.docx";
string fileName = Path.GetFileName(filePath);
string outputFilePath = Path.Combine("Your Document Directory", "DeleteById", fileName);
```
## Étape 2 : Copiez le document
 Depuis le`Delete` méthode modifie le document en place, il est préférable de créer une copie du document original.
```csharp
File.Copy(filePath, outputFilePath, true);
```
## Étape 3 : Supprimer la signature par identifiant
 Initialisez le`Signature` objet avec le chemin du fichier du document et utilisez le`Delete` méthode pour supprimer la signature par son ID.
```csharp
using (Signature signature = new Signature(outputFilePath))
{
    string id = @"eff64a14-dad9-47b0-88e5-2ee4e3604e71";
    bool result = signature.Delete(id);
    if (result)
    {
        Console.WriteLine($"Signature with Id# '{id}' was deleted from document ['{fileName}'].");
    }
    else
    {
        Helper.WriteError($"Signature was not deleted from the document! Signature with id# '{id}' was not found!");
    }
}
```

## Conclusion
Dans ce didacticiel, nous avons appris comment supprimer une signature par son ID à l'aide de GroupDocs.Signature pour .NET. Cette bibliothèque offre un moyen pratique de gérer par programmation les signatures numériques dans divers formats de documents.
## FAQ
### Puis-je supprimer plusieurs signatures à la fois ?
 Oui, vous pouvez supprimer plusieurs signatures en parcourant leurs identifiants et en appelant le`Delete` méthode pour chaque ID.
### GroupDocs.Signature pour .NET est-il compatible avec tous les formats de documents ?
GroupDocs.Signature pour .NET prend en charge un large éventail de formats de documents, notamment PDF, DOCX, XLSX, etc.
### Puis-je personnaliser l’apparence de la signature ?
Oui, vous pouvez personnaliser l’apparence de la signature, notamment sa position, sa taille, sa police et sa couleur.
### Existe-t-il une version d'essai disponible ?
 Oui, vous pouvez télécharger une version d'essai gratuite à partir de[ici](https://releases.groupdocs.com/).
### Où puis-je trouver de l’aide ou du support pour GroupDocs.Signature pour .NET ?
 Vous pouvez visiter le forum d'assistance[ici](https://forum.groupdocs.com/c/signature/13) à l'aide.