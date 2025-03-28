---
title: Rechercher plusieurs signatures
linktitle: Rechercher plusieurs signatures
second_title: API GroupDocs.Signature .NET
description: Découvrez comment rechercher plusieurs signatures dans des documents .NET à l'aide de GroupDocs.Signature pour une sécurité et une intégrité efficaces des documents.
weight: 14
url: /fr/net/signature-searching/search-for-multiple-signatures/
---

# Rechercher plusieurs signatures

## Introduction
GroupDocs.Signature for .NET est une bibliothèque puissante qui permet aux développeurs d'ajouter, de rechercher et de supprimer divers types de signatures dans des formats de documents courants à l'aide d'applications .NET. Dans ce didacticiel, nous nous concentrerons sur la recherche de plusieurs signatures dans un document à l'aide de GroupDocs.Signature pour .NET.
## Conditions préalables
Avant de commencer, assurez-vous d'avoir les prérequis suivants :
- Visual Studio installé sur votre système.
- Compréhension de base du langage de programmation C#.
- Bibliothèque GroupDocs.Signature pour .NET installée dans votre projet. Vous pouvez le télécharger depuis[ici](https://releases.groupdocs.com/signature/net/).

## Importer des espaces de noms
Tout d’abord, vous devez importer les espaces de noms nécessaires pour accéder aux classes et méthodes fournies par GroupDocs.Signature pour .NET.
```csharp
using System;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## Étape 1 : Charger le document
Chargez le document dans lequel vous souhaitez rechercher plusieurs signatures. Assurez-vous de fournir le chemin d'accès correct au fichier.
```csharp
string filePath = "sample_multiple_signatures.docx";
using (Signature signature = new Signature(filePath))
{
    // Votre code va ici
}
```
## Étape 2 : Définir les options de recherche
Définissez des options de recherche pour différents types de signatures telles que le texte, les signatures numériques, les codes-barres, les codes QR et les métadonnées. Vous pouvez spécifier des critères de recherche tels que le texte à rechercher, le type de correspondance et la recherche sur toutes les pages.
```csharp
// Définir les options de recherche
TextSearchOptions textOptions = new TextSearchOptions()
{
    AllPages = true
};
DigitalSearchOptions digitalOptions = new DigitalSearchOptions()
{
    AllPages = true
};
BarcodeSearchOptions barcodeOptions = new BarcodeSearchOptions()
{
    AllPages = true,
    Text = "123456",
    MatchType = TextMatchType.Exact
};
QrCodeSearchOptions qrCodeOptions = new QrCodeSearchOptions()
{
    AllPages = true,
    Text = "John",
    MatchType = TextMatchType.Contains
};
MetadataSearchOptions metadataOptions = new MetadataSearchOptions();
```
## Étape 3 : Ajouter des options de recherche à la liste
Ajoutez les options de recherche définies à une liste.
```csharp
// Ajouter des options à la liste
List<SearchOptions> listOptions = new List<SearchOptions>();
listOptions.Add(textOptions);
listOptions.Add(barcodeOptions);
listOptions.Add(qrCodeOptions);
listOptions.Add(metadataOptions);
listOptions.Add(digitalOptions);
```
## Étape 4 : Rechercher des signatures
Recherchez des signatures dans le document à l'aide des options de recherche définies.
```csharp
// Rechercher des signatures dans un document
SearchResult result = signature.Search(listOptions);
if (result.Signatures.Count > 0)
{
    Console.WriteLine($"\nSource document ['{filePath}'] contains following signatures.");
    foreach (var resSignature in result.Signatures)
    {
        Console.WriteLine($"Signature found at page {resSignature.PageNumber} with type {resSignature.SignatureType} and Id#: {resSignature.SignatureId}");
    }
}
else
{
    Helper.WriteError("No one signature was found.");
}
```

## Conclusion
Dans ce didacticiel, nous avons appris à rechercher plusieurs signatures dans un document à l'aide de GroupDocs.Signature pour .NET. En suivant les étapes fournies, vous pouvez localiser efficacement différents types de signatures dans vos documents, améliorant ainsi la sécurité et l'intégrité des documents.
## FAQ
### Puis-je rechercher des signatures dans différents formats de documents ?
Oui, GroupDocs.Signature pour .NET prend en charge un large éventail de formats de documents, notamment Word, PDF, Excel, etc.
### Est-il possible de personnaliser les critères de recherche des signatures ?
Absolument, vous pouvez adapter les critères de recherche en fonction de vos besoins, par exemple en spécifiant des correspondances de texte exactes ou en effectuant une recherche sur toutes les pages.
### GroupDocs.Signature for .NET offre-t-il la prise en charge des signatures numériques ?
Oui, vous pouvez rechercher des signatures numériques ainsi que d'autres types tels que des signatures de texte, de codes-barres et de codes QR.
### Puis-je intégrer facilement la fonctionnalité de recherche de signatures dans mes applications .NET ?
Oui, GroupDocs.Signature pour .NET fournit une API simple qui simplifie le processus d'intégration.
### Où puis-je trouver un soutien ou une assistance supplémentaire ?
 Vous pouvez visiter le forum GroupDocs.Signature[ici](https://forum.groupdocs.com/c/signature/13) pour toute question ou assistance.