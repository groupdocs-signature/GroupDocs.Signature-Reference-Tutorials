---
title: Signer un PDF avec des métadonnées
linktitle: Signer un PDF avec des métadonnées
second_title: API GroupDocs.Signature .NET
description: Découvrez comment signer des documents PDF avec des métadonnées à l'aide de GroupDocs.Signature pour .NET. Améliorez facilement la traçabilité et l’authenticité des documents.
type: docs
weight: 11
url: /fr/net/document-signing/sign-pdf-with-metadata/
---
## Introduction
Dans ce didacticiel, nous apprendrons comment signer un document PDF avec des métadonnées à l'aide de GroupDocs.Signature pour .NET. L'ajout de métadonnées à un PDF peut fournir des informations supplémentaires sur le document, telles que la paternité, la date de création, l'ID du document, etc.
## Conditions préalables
Avant de commencer, assurez-vous d'avoir les éléments suivants :
1.  GroupDocs.Signature pour .NET : vous pouvez le télécharger depuis[ici](https://releases.groupdocs.com/signature/net/).
2. Un document PDF : préparez un exemple de fichier PDF à signer.
3. Connaissance de base de la programmation C# : Une connaissance de la syntaxe C# est requise pour comprendre les exemples de code.
## Importer des espaces de noms
Tout d’abord, assurez-vous d’importer les espaces de noms nécessaires pour accéder aux classes et méthodes requises :
```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## Étape 1 : Charger le document PDF
Chargez le document PDF que vous souhaitez signer :
```csharp
string filePath = "sample.pdf";
```
## Étape 2 : Spécifier le chemin du fichier de sortie
Définissez le chemin du fichier de sortie où le PDF signé avec les métadonnées sera enregistré :
```csharp
string outputFilePath = Path.Combine("Your Document Directory", "SignPdfWithMetadata", "SignedWithMetadata.pdf");
```
## Étape 3 : Créer une instance de signature
Initialisez une instance de Signature en fournissant le chemin d'accès au document PDF :
```csharp
using (Signature signature = new Signature(filePath))
{
    // Le code lié à la signature ira ici
}
```
## Étape 4 : Définir les options de métadonnées
Créez MetadataSignOptions et ajoutez des champs de métadonnées avec leurs valeurs respectives :
```csharp
MetadataSignOptions options = new MetadataSignOptions();
options
    .Add(new PdfMetadataSignature("Author", "Mr.Sherlock Holmes")) // Valeur de chaîne
    .Add(new PdfMetadataSignature("CreatedOn", DateTime.Now))       // Valeurs DateHeure
    .Add(new PdfMetadataSignature("DocumentId", 123456))            // Valeur entière
    .Add(new PdfMetadataSignature("SignatureId", 123.456D))         // Valeur double
    .Add(new PdfMetadataSignature("Amount", 123.456M))              // Valeur décimale
    .Add(new PdfMetadataSignature("Total", 123.456F));              // Valeur flottante
```
## Étape 5 : Signez le document
Signez le document PDF avec les options de métadonnées spécifiées et enregistrez le document signé :
```csharp
SignResult result = signature.Sign(outputFilePath, options);
Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).\nFile saved at {outputFilePath}.");
```

## Conclusion
Dans ce didacticiel, nous avons expliqué comment signer un document PDF avec des métadonnées à l'aide de GroupDocs.Signature pour .NET. En suivant le guide étape par étape, vous pouvez facilement ajouter des informations de métadonnées telles que la paternité, la date de création, etc. à vos fichiers PDF, améliorant ainsi leur utilité et leur traçabilité.
## FAQ
### Puis-je ajouter des champs de métadonnées personnalisés à mes documents PDF ?
Oui, vous pouvez ajouter des champs de métadonnées personnalisés en spécifiant le nom du champ et sa valeur correspondante à l'aide de GroupDocs.Signature pour .NET.
### GroupDocs.Signature pour .NET est-il compatible avec toutes les versions de .NET Framework ?
GroupDocs.Signature pour .NET est compatible avec différentes versions de .NET Framework, garantissant flexibilité et facilité d'intégration.
### GroupDocs.Signature prend-il en charge la signature d'autres formats de documents que le PDF ?
Oui, GroupDocs.Signature prend en charge un large éventail de formats de documents, notamment Word, Excel, PowerPoint, etc.
### Puis-je signer plusieurs documents en masse à l’aide de GroupDocs.Signature pour .NET ?
Oui, vous pouvez signer plusieurs documents en masse en parcourant une liste de fichiers et en appliquant le processus de signature par programme.
### Le support technique est-il disponible pour les utilisateurs de GroupDocs.Signature ?
 Oui, GroupDocs fournit un support technique dédié via ses forums. Vous pouvez accéder au forum d'assistance[ici](https://forum.groupdocs.com/c/signature/13).