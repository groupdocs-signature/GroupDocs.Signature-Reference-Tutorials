---
title: Vérifier la signature numérique
linktitle: Vérifier la signature numérique
second_title: API GroupDocs.Signature .NET
description: Vérifiez facilement les signatures numériques dans .NET à l’aide de GroupDocs.Signature. Garantissez l’authenticité et l’intégrité des documents sans effort.
type: docs
weight: 11
url: /fr/net/verify-operations/verify-digital/
---
## Introduction
Dans le domaine des documents numériques, garantir l’authenticité et l’intégrité est primordial. Les signatures numériques sont l'équivalent numérique des signatures manuscrites, offrant un moyen sécurisé de vérifier l'origine et l'intégrité des documents électroniques. GroupDocs.Signature for .NET offre une boîte à outils puissante pour travailler avec des signatures numériques dans les applications .NET, facilitant ainsi la vérification des signatures numériques.
## Conditions préalables
Avant de vous lancer dans le processus de vérification à l'aide de GroupDocs.Signature pour .NET, assurez-vous que les conditions préalables suivantes sont en place :
### 1. Installez GroupDocs.Signature pour .NET
 Pour commencer, téléchargez et installez GroupDocs.Signature pour .NET. Vous pouvez trouver le lien de téléchargement[ici](https://releases.groupdocs.com/signature/net/).
### 2. Obtenir le fichier de signature numérique
Vous aurez besoin d'un fichier de signature numérique (par exemple, YourSignature.pfx) à des fins de vérification. Assurez-vous d'avoir accès à ce fichier et à son mot de passe associé.

## Importer des espaces de noms
Dans votre projet .NET, importez les espaces de noms nécessaires pour utiliser la fonctionnalité GroupDocs.Signature.

```csharp
using System;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## 1. Spécifiez le chemin du document
```csharp
string filePath = "sample_multiple_signatures.docx";
```
Spécifiez le chemin d'accès au document que vous souhaitez vérifier.
## 2. Initialiser l'objet de signature
```csharp
using (Signature signature = new Signature(filePath))
```
Créez un nouvel objet Signature en passant le chemin du document comme paramètre.
## 3. Définir les options de vérification
```csharp
DigitalVerifyOptions options = new DigitalVerifyOptions("YourSignature.pfx")
{
    Contact = "Mr.Smith",
    Password = "1234567890"
};
```
Créez un objet DigitalVerifyOptions, en spécifiant le chemin d'accès au fichier de signature numérique (par exemple, YourSignature.pfx), ainsi que toutes les options supplémentaires telles que les informations de contact et le mot de passe.
## 4. Vérifiez les signatures
```csharp
VerificationResult result = signature.Verify(options);
```
Invoquez la méthode Verify sur l'objet Signature, en transmettant les options de vérification.
## 5. Gérer le résultat de la vérification
```csharp
if (result.IsValid)
{
    // Signatures valides trouvées
    foreach (DigitalSignature item in result.Succeeded)
    {
        Console.WriteLine($"\nValid signature is found.");
    }
}
else
{
    // Échec de la vérification
    Helper.WriteError($"\nDocument {filePath} failed verification process.");
}
```
Vérifiez si le résultat de la vérification est valide. Si valide, parcourez la liste des signatures réussies. Sinon, gérez l’échec de la vérification.

## Conclusion
En conclusion, GroupDocs.Signature pour .NET simplifie le processus de vérification des signatures numériques dans les applications .NET. En suivant le guide étape par étape décrit ci-dessus et en tirant parti des puissantes fonctionnalités de GroupDocs.Signature, vous pouvez garantir l'authenticité et l'intégrité de vos documents numériques en toute confiance.
## FAQ
### GroupDocs.Signature peut-il vérifier plusieurs signatures dans un seul document ?
Oui, GroupDocs.Signature prend en charge la vérification de plusieurs signatures dans un seul document, offrant ainsi des capacités de validation complètes.
### GroupDocs.Signature est-il compatible avec différents types de fichiers de signature numérique ?
GroupDocs.Signature prend en charge divers formats de fichiers de signature numérique, notamment PFX, P12 et autres, garantissant la flexibilité des processus de vérification.
### Puis-je personnaliser les options de vérification telles que les informations de contact pendant le processus de vérification ?
Oui, GroupDocs.Signature permet de personnaliser les options de vérification, permettant aux utilisateurs de spécifier des informations de contact, des mots de passe et d'autres paramètres selon leurs besoins.
### GroupDocs.Signature offre-t-il un support pour le dépannage et une assistance ?
Oui, GroupDocs.Signature fournit une assistance dédiée via son forum, où les utilisateurs peuvent demander de l'aide, partager des informations et résoudre efficacement les problèmes.
### Existe-t-il une version d’essai disponible pour GroupDocs.Signature ?
Oui, les utilisateurs intéressés peuvent accéder à une version d'essai gratuite de GroupDocs.Signature pour explorer ses fonctionnalités avant de prendre une décision d'achat.