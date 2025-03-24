---
title: Vérifier le code QR
linktitle: Vérifier le code QR
second_title: API GroupDocs.Signature .NET
description: Découvrez comment vérifier les codes QR dans les documents à l'aide de GroupDocs.Signature pour .NET. Tutoriel complet avec guide étape par étape.
weight: 12
url: /fr/net/verify-operations/verify-qr-code/
---
## Introduction
Dans le domaine de la gestion et de l’authentification des documents, garantir l’intégrité et la validité des signatures est primordial. GroupDocs.Signature pour .NET fournit une solution complète pour vérifier les codes QR intégrés dans les documents. Dans ce didacticiel, nous aborderons le processus étape par étape de vérification des codes QR à l'aide de GroupDocs.Signature pour .NET.
## Conditions préalables
Avant de vous lancer dans le processus de vérification, assurez-vous que les conditions préalables suivantes sont remplies :
1.  Installation de GroupDocs.Signature pour .NET : Téléchargez et installez GroupDocs.Signature pour .NET à partir du[lien de téléchargement](https://releases.groupdocs.com/signature/net/).
2. Accès à un document contenant des codes QR : préparez un exemple de document contenant des codes QR pour vérification. 

## Importer des espaces de noms
Tout d'abord, vous devez importer les espaces de noms nécessaires pour utiliser les fonctionnalités fournies par GroupDocs.Signature pour .NET. Suivez ces étapes:

```csharp
using System;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```


Maintenant, décomposons le processus de vérification des codes QR intégrés dans un document à l'aide de GroupDocs.Signature pour .NET :
## Étape 1 : Spécifier le chemin du document
```csharp
string filePath = "sample_multiple_signatures.docx";
```
 Assurez-vous de remplacer`"sample_multiple_signatures.docx"` avec le chemin d'accès à votre document.
## Étape 2 : initialiser l'objet de signature
```csharp
using (Signature signature = new Signature(filePath))
{
    //Le code de vérification va ici
}
```
 Initialiser un`Signature` objet en fournissant le chemin d’accès au document.
## Étape 3 : Spécifier les options de vérification
```csharp
QrCodeVerifyOptions options = new QrCodeVerifyOptions()
{
    AllPages = true, // cette valeur est définie par défaut
    Text = "John",
    MatchType = TextMatchType.Contains
};
```
 Définir des options de vérification telles que`AllPages` pour vérifier toutes les pages,`Text` pour spécifier le texte à faire correspondre dans le code QR, et`MatchType` pour définir les critères de correspondance.
## Étape 4 : Vérifier les signatures des documents
```csharp
VerificationResult result = signature.Verify(options);
```
 Invoquer le`Verify` méthode du`Signature` objet, en passant les options de vérification.
## Étape 5 : Gérer les résultats de la vérification
```csharp
if (result.IsValid)
{
    // Signature valide trouvée
}
else
{
    // Signature invalide trouvée
}
```
En fonction du résultat de la vérification, gérez les scénarios de réussite ou d’échec en conséquence.

## Conclusion
Dans ce didacticiel, nous avons exploré le processus de vérification des codes QR dans les documents à l'aide de GroupDocs.Signature pour .NET. En suivant ces étapes, vous pouvez intégrer de manière transparente la fonctionnalité de vérification du code QR dans vos applications .NET, garantissant ainsi l'intégrité et l'authenticité des documents.
## FAQ
### GroupDocs.Signature for .NET peut-il vérifier les codes QR dans différents formats de documents ?
Oui, GroupDocs.Signature pour .NET prend en charge un large éventail de formats de documents, notamment DOCX, PDF, etc. pour la vérification du code QR.
### Existe-t-il un essai gratuit disponible pour GroupDocs.Signature pour .NET ?
 Oui, vous pouvez bénéficier d'un essai gratuit auprès du[page des versions](https://releases.groupdocs.com/).
### Quelles options de support sont disponibles pour les utilisateurs de GroupDocs.Signature pour .NET ?
 Les utilisateurs peuvent accéder à l'assistance via le[forum](https://forum.groupdocs.com/c/signature/13) pour GroupDocs.Signature.
### Puis-je acheter une licence temporaire pour GroupDocs.Signature pour .NET ?
 Oui, des licences temporaires sont disponibles à l'achat auprès du[Page d'achat de GroupDocs](https://purchase.groupdocs.com/temporary-license/).
### Existe-t-il une documentation complète disponible pour GroupDocs.Signature pour .NET ?
 Tout à fait, vous pouvez vous référer à la documentation détaillée fournie[ici](https://tutorials.groupdocs.com/signature/net/) pour des conseils complets sur l’utilisation des fonctionnalités de GroupDocs.Signature pour .NET.