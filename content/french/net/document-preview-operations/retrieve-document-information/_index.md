---
title: Récupérer les informations du document
linktitle: Récupérer les informations du document
second_title: API GroupDocs.Signature .NET
description: Améliorez la gestion des documents dans .NET avec GroupDocs.Signature. Récupérez les informations du document étape par étape. Prend en charge différents formats.
weight: 11
url: /fr/net/document-preview-operations/retrieve-document-information/
---

# Récupérer les informations du document

## Introduction
Dans le domaine de la documentation numérique, garantir l’authenticité et l’intégrité est primordial. GroupDocs.Signature for .NET fournit une solution robuste pour gérer les signatures de documents dans l'environnement .NET. Dans ce didacticiel, nous approfondissons le processus de récupération des informations sur les documents à l'aide de GroupDocs.Signature pour .NET, en décomposant chaque étape pour une compréhension globale.
## Conditions préalables
Avant de plonger dans le didacticiel, assurez-vous que les conditions préalables suivantes sont remplies :
1.  Installation : installez GroupDocs.Signature pour .NET en le téléchargeant depuis[ici](https://releases.groupdocs.com/signature/net/).
2. Environnement .NET : Avoir une connaissance pratique du framework .NET.
3. Document : Préparez un exemple de document (par exemple, "sample_multiple_signatures.docx") à des fins de test.

## Importation d'espaces de noms
Avant de poursuivre le processus de récupération des signatures du document, importez les espaces de noms nécessaires :
```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
```

## Étape 1 : Définir le chemin du fichier du document :
Définissez le chemin du fichier du document à partir duquel vous souhaitez récupérer des informations.
```csharp
string filePath = "sample_multiple_signatures.docx";
```
## Étape 2 : Instancier l'objet de signature :
 Créez une instance du`Signature` classe en passant le chemin du fichier du document.
```csharp
using (Signature signature = new Signature(filePath))
{

}
```
## Étape 3 : Récupérer les informations du document :
 Utiliser le`GetDocumentInfo()` méthode pour récupérer des informations complètes sur le document.
```csharp
IDocumentInfo documentInfo = signature.GetDocumentInfo();
```
## Étape 4 : Afficher les propriétés du document :
Affichez diverses propriétés du document telles que le format, l'extension, la taille, le nombre de pages, etc.
```csharp
Console.WriteLine($"Document properties {Path.GetFileName(filePath)}:");
Console.WriteLine($" - format : {documentInfo.FileType.FileFormat}");
Console.WriteLine($" - extension : {documentInfo.FileType.Extension}");
Console.WriteLine($" - size : {documentInfo.Size}");
Console.WriteLine($" - page count : {documentInfo.PageCount}");
Console.WriteLine($" - Form Fields count : {documentInfo.FormFields.Count}");
Console.WriteLine($" - Text signatures count : {documentInfo.TextSignatures.Count}");
Console.WriteLine($" - Image signatures count : {documentInfo.ImageSignatures.Count}");
Console.WriteLine($" - Digital signatures count : {documentInfo.DigitalSignatures.Count}");
Console.WriteLine($" - Barcode signatures count : {documentInfo.BarcodeSignatures.Count}");
Console.WriteLine($" - QrCode signatures count : {documentInfo.QrCodeSignatures.Count}");
Console.WriteLine($" - FormField signatures count : {documentInfo.FormFieldSignatures.Count}");
foreach (PageInfo pageInfo in documentInfo.Pages)
{
   Console.WriteLine($" - page-{pageInfo.PageNumber} Width {pageInfo.Width}, Height {pageInfo.Height}");
}
```


## Conclusion
GroupDocs.Signature for .NET offre une suite puissante d'outils pour gérer les signatures de documents de manière transparente au sein du framework .NET. En suivant les étapes décrites dans ce guide, vous pouvez récupérer efficacement des informations complètes sur vos documents, facilitant ainsi des capacités améliorées de gestion de documents.

## FAQ
### GroupDocs.Signature pour .NET peut-il gérer plusieurs formats de documents ?
Oui, GroupDocs.Signature prend en charge un large éventail de formats de documents, notamment, mais sans s'y limiter, DOCX, PDF, PNG et JPEG.
### Existe-t-il une version d’essai disponible pour GroupDocs.Signature pour .NET ?
 Oui, vous pouvez accéder à la version d'essai à partir de[ici](https://releases.groupdocs.com/).
### GroupDocs.Signature pour .NET prend-il en charge les signatures numériques ?
Absolument, GroupDocs.Signature offre une prise en charge robuste des signatures numériques, garantissant l'authenticité et l'intégrité des documents.
### Où puis-je trouver une documentation supplémentaire et une assistance pour GroupDocs.Signature pour .NET ?
 Vous pouvez vous référer à la documentation complète[ici](https://tutorials.groupdocs.com/signature/net/) , et pour obtenir de l'aide, visitez le forum GroupDocs[ici](https://forum.groupdocs.com/c/signature/13).
### Des licences temporaires peuvent-elles être obtenues pour GroupDocs.Signature pour .NET ?
 Oui, des licences temporaires sont disponibles à l'achat[ici](https://purchase.groupdocs.com/temporary-license/).