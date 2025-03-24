---
title: Supprimer plusieurs signatures du document
linktitle: Supprimer plusieurs signatures du document
second_title: API GroupDocs.Signature .NET
description: Supprimez sans effort plusieurs signatures de documents à l’aide de GroupDocs.Signature pour .NET. Rationalisez votre flux de gestion de documents.
weight: 15
url: /fr/net/delete-operations/delete-multiple-signatures/
---

# Supprimer plusieurs signatures du document

## Introduction
Dans le monde numérique, la gestion documentaire implique souvent la gestion de diverses signatures. La suppression programmée de plusieurs signatures d'un document peut rationaliser les flux de travail et améliorer l'efficacité. Avec GroupDocs.Signature pour .NET, cette tâche devient transparente et simple. Ce didacticiel vous guidera étape par étape tout au long du processus de suppression de plusieurs signatures d'un document.
## Conditions préalables
Avant de plonger dans le didacticiel, assurez-vous d'avoir les prérequis suivants :
- Compréhension de base du langage de programmation C#.
- Bibliothèque GroupDocs.Signature pour .NET installée.
- Exemple de document avec plusieurs signatures pour les tests.

## Importer des espaces de noms
Commencez par importer les espaces de noms nécessaires pour accéder aux fonctionnalités de GroupDocs.Signature pour .NET :
```csharp
using System;
using System.IO;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## Étape 1 : Définir le chemin du document et le nom du fichier
Définissez le chemin du fichier du document contenant plusieurs signatures. Assurez-vous d'avoir le chemin et le nom de fichier appropriés :
```csharp
string filePath = "sample_multiple_signatures.docx";
string fileName = Path.GetFileName(filePath);
```
## Étape 2 : Copiez le document pour traitement
Pour éviter de modifier le document original, créez une copie à traiter :
```csharp
string outputFilePath = Path.Combine("Your Document Directory", "DeleteMultiple", fileName);
File.Copy(filePath, outputFilePath, true);
```
## Étape 3 : initialiser l'objet de signature
Instanciez un objet Signature à l'aide du chemin du fichier de sortie :
```csharp
using (Signature signature = new Signature(outputFilePath))
{
    // Le code de traitement des signatures va ici
}
```
## Étape 4 : Définir les options de recherche
Définissez diverses options de recherche pour identifier les signatures dans le document. Les options incluent la recherche de texte, la recherche d'images, la recherche de codes-barres et la recherche de code QR :
```csharp
TextSearchOptions textSearchOptions = new TextSearchOptions();
ImageSearchOptions imageSearchOptions = new ImageSearchOptions();
BarcodeSearchOptions barcodeOptions = new BarcodeSearchOptions();
QrCodeSearchOptions qrCodeOptions = new QrCodeSearchOptions();
// Ajouter des options à la liste
List<SearchOptions> listOptions = new List<SearchOptions>();
listOptions.Add(textSearchOptions);
listOptions.Add(imageSearchOptions);
listOptions.Add(barcodeOptions);
listOptions.Add(qrCodeOptions);
```
## Étape 5 : Rechercher des signatures
Exécutez une opération de recherche pour trouver toutes les signatures dans le document en fonction des options de recherche définies :
```csharp
SearchResult result = signature.Search(listOptions);
```
## Étape 6 : Supprimer les signatures
Si des signatures sont trouvées, procédez à leur suppression :
```csharp
if (result.Signatures.Count > 0)
{
    // Tentative de supprimer toutes les signatures
    DeleteResult deleteResult = signature.Delete(result.Signatures);
    //Vérifiez si la suppression a réussi
    if(deleteResult.Succeeded.Count == result.Signatures.Count)
    {
        Console.WriteLine("\nAll signatures were successfully deleted!");                        
    }
    else
    {
        Console.WriteLine($"Successfully deleted signatures : {deleteResult.Succeeded.Count}");
        Helper.WriteError($"Not deleted signatures : {deleteResult.Failed.Count}");
    }
    // Afficher des informations sur les signatures supprimées
    Console.WriteLine("\nList of deleted signatures:");
    int number = 1;
    foreach(BaseSignature temp in deleteResult.Succeeded)
    {
        Console.WriteLine($"Signature #{number++}: Type: {temp.SignatureType} Id:{temp.SignatureId}, Location: {temp.Left}x{temp.Top}. Size: {temp.Width}x{temp.Height}");
    }
}
else
{
    Helper.WriteError("No one signature was found.");
}
```

## Conclusion
La suppression programmée de plusieurs signatures d'un document est une tâche cruciale dans la gestion des documents. Avec GroupDocs.Signature pour .NET, ce processus devient efficace et fiable. En suivant les étapes décrites dans ce didacticiel, vous pouvez facilement intégrer la fonctionnalité de suppression de signature dans vos applications .NET.
## FAQ
### GroupDocs.Signature pour .NET peut-il gérer différents formats de documents ?
Oui, GroupDocs.Signature pour .NET prend en charge un large éventail de formats de documents, notamment DOCX, PDF, PPTX, XLSX, etc.
### Est-il possible de personnaliser les options de recherche pour la détection de signature ?
Absolument, vous pouvez personnaliser les options de recherche telles que la recherche de texte, la recherche d'images, la recherche de codes-barres et la recherche de codes QR pour répondre à vos besoins spécifiques.
### GroupDocs.Signature pour .NET fournit-il des mécanismes de gestion des erreurs ?
Oui, la bibliothèque offre de solides capacités de gestion des erreurs pour garantir une exécution fluide des tâches de traitement des documents.
### Puis-je intégrer GroupDocs.Signature pour .NET avec d’autres bibliothèques tierces ?
Certes, GroupDocs.Signature pour .NET est conçu pour s'intégrer de manière transparente à d'autres bibliothèques .NET, offrant ainsi flexibilité et extensibilité.
### Où puis-je trouver une assistance et des ressources supplémentaires pour GroupDocs.Signature pour .NET ?
 Vous pouvez visiter les GroupDocs[forum](https://forum.groupdocs.com/c/signature/13) dédié aux discussions liées à la signature et demander l’aide de la communauté et des experts.