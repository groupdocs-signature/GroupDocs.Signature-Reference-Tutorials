---
title: Supprimer la signature numérique du document
linktitle: Supprimer la signature numérique du document
second_title: API GroupDocs.Signature .NET
description: Découvrez comment supprimer les signatures numériques des documents à l'aide de GroupDocs.Signature pour .NET. Suivez notre guide étape par étape pour une gestion efficace.
weight: 13
url: /fr/net/delete-operations/delete-digital-signature/
---

# Supprimer la signature numérique du document

## Introduction
Dans le monde des documents numériques, garantir l’authenticité et la sécurité est primordial. Les signatures numériques jouent un rôle crucial dans la vérification de l'intégrité des documents électroniques. GroupDocs.Signature for .NET offre des outils puissants pour gérer efficacement les signatures numériques au sein des applications .NET.
## Conditions préalables
Avant de vous lancer dans l'utilisation de GroupDocs.Signature pour .NET pour supprimer les signatures numériques des documents, assurez-vous de disposer des éléments suivants :
1. Visual Studio : installez Visual Studio IDE sur votre système.
2.  GroupDocs.Signature pour .NET : téléchargez et installez GroupDocs.Signature pour .NET à partir du[page de téléchargement](https://releases.groupdocs.com/signature/net/).
3. Exemple de document : préparez un exemple de document contenant des signatures numériques pour les tests.

## Importer des espaces de noms
Pour commencer, assurez-vous d'importer les espaces de noms nécessaires dans votre projet .NET :
```csharp
using System;
using System.IO;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
```
## Étape 1 : Définir les chemins de fichiers
Commencez par définir les chemins de fichiers du document source et du document de sortie :
```csharp
string filePath = "sample.pdf"_SIGNED_DIGITAL;
string fileName = Path.GetFileName(filePath);
string outputFilePath = Path.Combine("Your Document Directory", "DeleteDigital", fileName);
```
## Étape 2 : Copiez le document source
 Depuis le`Delete` fonctionne avec le même document, il est nécessaire de copier le fichier source vers un nouvel emplacement :
```csharp
File.Copy(filePath, outputFilePath, true);
```
## Étape 3 : initialiser l'objet de signature
 Initialiser un`Signature` objet avec le chemin du fichier de sortie :
```csharp
using (Signature signature = new Signature(outputFilePath))
{
    // Votre code va ici
}
```
## Étape 4 : Rechercher des signatures numériques
Rechercher des signatures numériques électroniques dans le document :
```csharp
List<DigitalSignature> signatures = signature.Search<DigitalSignature>(SignatureType.Digital);
```
## Étape 5 : Supprimer la signature numérique
Si des signatures numériques sont trouvées, supprimez la première signature trouvée :
```csharp
if (signatures.Count > 0)
{
    DigitalSignature digitalSignature = signatures[0];
    bool result = signature.Delete(digitalSignature);
    if (result)
    {
        Console.WriteLine($"Digital signature #{digitalSignature.Thumbprint} from {digitalSignature.SignTime.ToShortDateString()} was deleted from document ['{fileName}'].");
    }
    else
    {
        Helper.WriteError($"Signature was not deleted from the document! Signature# {digitalSignature.Thumbprint} was not found!");
    }
}
```

## Conclusion
La gestion des signatures numériques dans les applications .NET devient un jeu d'enfant avec GroupDocs.Signature. En suivant les étapes simples décrites ci-dessus, vous pouvez supprimer en toute transparence les signatures numériques de vos documents, garantissant ainsi l'intégrité et la sécurité des données.
## FAQ
### Puis-je supprimer plusieurs signatures numériques d’un même document ?
Oui, vous pouvez modifier le code pour parcourir toutes les signatures numériques trouvées et les supprimer en conséquence.
### GroupDocs.Signature prend-il en charge d'autres types de signatures que numériques ?
Oui, GroupDocs.Signature prend en charge différents types de signatures, notamment les signatures électroniques, numériques et manuscrites.
### GroupDocs.Signature est-il adapté à la gestion de documents au niveau de l’entreprise ?
Absolument, GroupDocs.Signature est conçu pour répondre aux besoins des développeurs individuels et des applications d'entreprise, offrant des fonctionnalités robustes et une évolutivité.
### Puis-je personnaliser le processus de suppression des signatures numériques ?
Oui, GroupDocs.Signature fournit un large éventail d'options et de paramètres pour personnaliser le processus de suppression de signature en fonction de vos besoins spécifiques.
### Existe-t-il une version d’essai disponible pour tester GroupDocs.Signature ?
 Oui, vous pouvez télécharger une version d'essai gratuite à partir du[page des versions](https://releases.groupdocs.com/).