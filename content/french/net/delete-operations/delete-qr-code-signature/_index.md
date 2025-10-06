---
"description": "Découvrez comment supprimer facilement les signatures de code QR de vos documents à l'aide de GroupDocs.Signature pour .NET avec notre guide de développement étape par étape."
"linktitle": "Supprimer la signature du code QR du document"
"second_title": "API .NET GroupDocs.Signature"
"title": "Comment supprimer les signatures de code QR des documents dans .NET"
"url": "/fr/net/delete-operations/delete-qr-code-signature/"
"weight": 16
type: docs
---
# Comment supprimer les signatures de code QR de vos documents

## Introduction

Avez-vous déjà eu besoin de supprimer la signature d'un code QR d'un document par programmation ? Que vous souhaitiez nettoyer des informations obsolètes ou préparer des documents pour une redistribution, savoir gérer efficacement les signatures de documents est une compétence essentielle pour les développeurs .NET.

Dans ce guide convivial, nous vous expliquerons précisément comment supprimer les signatures de codes QR de vos documents à l'aide de GroupDocs.Signature pour .NET. Cette puissante bibliothèque simplifie la gestion des signatures et vous permet de vous concentrer sur la création d'applications performantes plutôt que sur la manipulation de documents.

## Ce dont vous aurez besoin avant de commencer

Avant de plonger dans le code, assurons-nous que tout est prêt :

- GroupDocs.Signature pour .NET : la bibliothèque doit être installée dans votre projet. Vous pouvez la télécharger directement depuis [la page des versions de GroupDocs](https://releases.groupdocs.com/signature/net/).
- Un document avec des codes QR : Pour vous entraîner, préparez un document contenant au moins une signature de code QR que vous souhaitez supprimer.
- Connaissances de base en C# : vous devez être à l’aise avec les fondamentaux de C# pour suivre nos exemples.

Une fois ces conditions préalables remplies, vous êtes prêt à commencer à supprimer ces codes QR !

## Configurer votre projet avec les bons espaces de noms

Tout d’abord, importons les espaces de noms nécessaires pour que notre code fonctionne correctement :

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

Ces importations nous donnent accès à toutes les fonctionnalités dont nous avons besoin de la bibliothèque GroupDocs.Signature, ainsi qu'à certaines classes .NET essentielles pour la gestion des fichiers.

## Étape 1 : Où sont vos fichiers ? Configuration des chemins d'accès aux documents

Commençons par définir où se trouvent nos documents et où nous voulons enregistrer la version modifiée :

```csharp
// Le chemin vers le répertoire des documents.
string filePath = "sample_multiple_signatures.docx";
string fileName = Path.GetFileName(filePath);

// Définissez le chemin du fichier de sortie pour le document modifié.
string outputFilePath = Path.Combine("Your Document Directory", "DeleteQRCode", fileName);

// Copiez le fichier source puisque la méthode Delete fonctionne avec le même document.
File.Copy(filePath, outputFilePath, true);
```

Notez que nous créons une copie de notre document original. Ceci est important car la suppression de la signature modifiera directement le fichier, et nous souhaitons toujours préserver nos documents originaux.

## Étape 2 : Création d'un objet de signature avec lequel travailler

Nous allons maintenant créer un objet Signature qui se connecte à notre document :

```csharp
using (Signature signature = new Signature(outputFilePath))
{
    // Créez des options pour rechercher des signatures de code QR.
    QrCodeSearchOptions options = new QrCodeSearchOptions();
    
    // Recherchez des signatures de code QR dans le document.
    List<QrCodeSignature> signatures = signature.Search<QrCodeSignature>(options);
```

Ce code initialise l'objet Signature avec notre document, puis recherche les signatures de codes QR présentes. La recherche renvoie la liste de toutes les signatures de codes QR trouvées.

## Étape 3 : Existe-t-il des codes QR à supprimer ?

Avant de tenter de supprimer quoi que ce soit, nous devons vérifier s'il y a réellement des codes QR présents :

```csharp
    if (signatures.Count > 0)
    {
        // Obtenez la première signature de code QR trouvée dans le document.
        QrCodeSignature qrCodeSignature = signatures[0];
```

Cette vérification simple garantit que nous ne traitons que si le document contient au moins une signature de code QR. Dans cet exemple, nous ciblons le premier code QR trouvé, mais vous pouvez facilement modifier ce paramètre pour gérer plusieurs signatures si nécessaire.

## Étape 4 : Suppression du code QR de votre document

Passons maintenant à l’événement principal : la suppression du code QR :

```csharp
        // Supprimez la signature du code QR du document.
        bool result = signature.Delete(qrCodeSignature);
        
        if (result)
        {
            Console.WriteLine($"Signature with QR-Code '{qrCodeSignature.Text}' and encode type '{qrCodeSignature.EncodeType.TypeName}' was deleted from document ['{fileName}'].");
        }
        else
        {
            Console.WriteLine($"Signature was not deleted from the document! Signature with QR-Code '{qrCodeSignature.Text}' and encode type '{qrCodeSignature.EncodeType.TypeName}' was not found!");
        }
    }
}
```

Le code supprime la signature et fournit un retour d'information sur la réussite de l'opération. Ce retour est essentiel pour le débogage et la confirmation du bon fonctionnement de votre code.

## Qu’avons-nous accompli ?

Félicitations ! Vous venez d'apprendre à supprimer les signatures de codes QR de vos documents avec GroupDocs.Signature pour .NET. Cette compétence ouvre de nombreuses possibilités pour la gestion documentaire de vos applications.

Avec seulement quelques lignes de code, vous pouvez désormais nettoyer par programmation des documents en supprimant les signatures de code QR obsolètes ou inutiles, garantissant ainsi que vos documents ne contiennent toujours que les informations pertinentes.

## Questions courantes que vous pourriez avoir

### Puis-je supprimer plusieurs codes QR à la fois ?

Absolument ! Au lieu de supprimer simplement la première signature trouvée, vous pouvez parcourir la liste complète des signatures et supprimer chacune d'elles comme suit :

```csharp
foreach(var qrSignature in signatures)
{
    signature.Delete(qrSignature);
}
```

### Quels autres types de signatures puis-je gérer avec GroupDocs.Signature ?

GroupDocs.Signature est incroyablement polyvalent, prenant en charge différents types de signatures, notamment :
- Signatures de texte
- Signatures d'images
- Signatures de codes-barres
- Signatures numériques
- Et bien d'autres encore !

### Cela fonctionnera-t-il avec tous mes formats de documents ?

Vous serez heureux d'apprendre que GroupDocs.Signature fonctionne avec une large gamme de formats de documents, notamment :
- Documents PDF
- documents Microsoft Word
- feuilles de calcul Excel
- Présentations PowerPoint
- Et bien d'autres

### Puis-je rechercher des codes QR spécifiques plutôt que de les supprimer tous ?

Oui! Le `QrCodeSearchOptions` La classe propose diverses propriétés pour filtrer votre recherche. Vous pouvez, par exemple, rechercher des codes QR contenant un texte spécifique ou codés selon un format particulier.

### Existe-t-il un moyen d'essayer GroupDocs.Signature avant d'acheter ?

Oui, vous pouvez télécharger une version d'essai gratuite à partir de [le site Web GroupDocs](https://releases.groupdocs.com/) pour le tester avec vos cas d'utilisation spécifiques avant de vous engager.