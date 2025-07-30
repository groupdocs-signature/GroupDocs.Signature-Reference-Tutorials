---
"description": "Découvrez comment vérifier les codes QR dans les documents avec GroupDocs.Signature pour .NET. Guide complet avec exemples de code et bonnes pratiques pour l'authentification des documents."
"linktitle": "Vérifier le code QR"
"second_title": "API .NET GroupDocs.Signature"
"title": "Vérifier le code QR dans les documents"
"url": "/fr/net/verify-operations/verify-qr-code/"
"weight": 12
---

## Introduction

La sécurité des documents est un aspect essentiel des opérations commerciales modernes. Les codes QR sont devenus une méthode de plus en plus répandue pour intégrer des informations dans des documents dont l'authenticité peut être vérifiée. GroupDocs.Signature pour .NET offre une solution puissante et flexible pour vérifier les codes QR intégrés dans des documents de différents formats.

Ce didacticiel complet vous guidera tout au long du processus de mise en œuvre de la vérification du code QR dans vos applications .NET, garantissant que vos documents conservent leur intégrité et leur authenticité.

## Prérequis

Avant d’implémenter la fonctionnalité de vérification du code QR, assurez-vous de disposer des prérequis suivants :

1. GroupDocs.Signature pour .NET : téléchargez et installez la bibliothèque à partir du [page de téléchargement](https://releases.groupdocs.com/signature/net/).
2. Environnement de développement : Visual Studio ou tout environnement de développement .NET compatible.
3. Document de test : un document contenant des signatures de code QR à des fins de vérification.
4. Connaissances de base : Familiarité avec la programmation C# et les concepts du framework .NET.

## Importer des espaces de noms

Commencez par importer les espaces de noms requis pour accéder à la fonctionnalité GroupDocs.Signature :

```csharp
using System;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

## Processus de vérification du code QR étape par étape

Suivez ces étapes détaillées pour vérifier les codes QR dans vos documents :

### Étape 1 : Spécifier le chemin du document

```csharp
// Indiquez le chemin d'accès au document contenant les signatures de code QR
string filePath = "sample_multiple_signatures.docx";
```

Assurez-vous de remplacer le chemin d’exemple par le chemin réel vers votre document.

### Étape 2 : Initialiser l’objet Signature

```csharp
// Créer une instance de signature en transmettant le chemin du document
using (Signature signature = new Signature(filePath))
{
    // Le code de vérification sera implémenté ici
}
```

La classe Signature est le point d’entrée principal pour toutes les opérations de l’API GroupDocs.Signature.

### Étape 3 : Configurer les options de vérification du code QR

```csharp
// Définir les options de vérification du code QR
QrCodeVerifyOptions options = new QrCodeVerifyOptions()
{
    AllPages = true, // Vérifiez toutes les pages du document
    Text = "John",   // Texte à vérifier dans le code QR
    MatchType = TextMatchType.Contains // Spécifiez les critères de correspondance du texte
};
```

Les options de vérification vous permettent de définir des critères spécifiques pour le processus de vérification :
- `AllPages`: Définir sur vrai pour vérifier toutes les pages du document (comportement par défaut)
- `Text`: Le contenu du texte à faire correspondre dans le code QR
- `MatchType`: La méthode de correspondance de texte (Contient, Exact, Commence par, etc.)

### Étape 4 : Exécuter le processus de vérification

```csharp
// Effectuer la vérification
VerificationResult result = signature.Verify(options);
```

Cela exécute le processus de vérification en fonction des options que vous avez spécifiées.

### Étape 5 : Résultats de la vérification du processus

```csharp
// Vérifiez le résultat de la vérification et procédez en conséquence
if (result.IsValid)
{
    Console.WriteLine($"Document {filePath} contains valid QR code signature!");
    
    // Afficher des informations sur les signatures réussies
    foreach (QrCodeSignature signature in result.Succeeded)
    {
        Console.WriteLine($"Found valid QR Code signature with text: {signature.Text}");
        Console.WriteLine($"QR Code type: {signature.EncodeType.TypeName}");
        Console.WriteLine($"Location: Page {signature.PageNumber}, {signature.Left}x{signature.Top}");
    }
}
else
{
    Console.WriteLine($"Document {filePath} failed verification process.");
    Console.WriteLine($"Number of failed signatures: {result.Failed.Count}");
}
```

Une gestion appropriée du résultat de la vérification permet à votre application de prendre les mesures appropriées en fonction du résultat de la vérification.

## Exemple complet

Voici un exemple complet et fonctionnel qui illustre la vérification du code QR :

```csharp
using System;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;

namespace GroupDocs.Signature.Examples
{
    class Program
    {
        static void Main(string[] args)
        {
            // Chemin du document
            string filePath = "sample_multiple_signatures.docx";
            
            // Initialiser l'instance de signature
            using (Signature signature = new Signature(filePath))
            {
                // Options de vérification de la configuration
                QrCodeVerifyOptions options = new QrCodeVerifyOptions()
                {
                    AllPages = true,
                    Text = "John",
                    MatchType = TextMatchType.Contains
                };
                
                // Vérifier les signatures des documents
                VerificationResult result = signature.Verify(options);
                
                // Résultats de la vérification du processus
                if (result.IsValid)
                {
                    Console.WriteLine($"Document {filePath} contains valid QR code signature!");
                    
                    foreach (QrCodeSignature qrSignature in result.Succeeded)
                    {
                        Console.WriteLine($"Found valid QR Code with text: {qrSignature.Text}");
                    }
                }
                else
                {
                    Console.WriteLine($"Document {filePath} failed verification process.");
                }
            }
        }
    }
}
```

## Options de vérification avancées

GroupDocs.Signature fournit des options supplémentaires pour des scénarios de vérification plus complexes :

### Vérification de types de codes QR spécifiques

```csharp
QrCodeVerifyOptions options = new QrCodeVerifyOptions()
{
    EncodeType = QrCodeTypes.QR,  // Vérifiez uniquement les codes QR standard
    Text = "Confidential",
    MatchType = TextMatchType.Exact
};
```

### Vérification sur des pages spécifiques

```csharp
QrCodeVerifyOptions options = new QrCodeVerifyOptions()
{
    AllPages = false,
    PageNumber = 2,  // Vérifier uniquement sur la page 2
    Text = "Approved"
};
```

### Utilisation d'expressions régulières pour la vérification

```csharp
QrCodeVerifyOptions options = new QrCodeVerifyOptions()
{
    Text = "INV-\\d{6}",  // Faire correspondre les numéros de facture (par exemple, INV-123456)
    MatchType = TextMatchType.Regex
};
```

## Meilleures pratiques pour la vérification des codes QR

1. Validez toujours les entrées : assurez-vous que les chemins d’accès aux documents et les critères de vérification sont valides avant le traitement.
2. Implémenter la gestion des erreurs : utilisez des blocs try-catch pour gérer les exceptions potentielles lors de la vérification.
3. Tenez compte des performances : pour les documents volumineux, pensez à vérifier des pages spécifiques plutôt que le document entier.
4. Résultats de la vérification des journaux : conservez les journaux des processus de vérification à des fins d’audit.
5. Testez avec différents formats de documents : assurez-vous que votre vérification fonctionne sur tous les formats de documents requis.

## Conclusion

La vérification des codes QR dans les documents est essentielle pour garantir leur authenticité et leur intégrité. GroupDocs.Signature pour .NET fournit une API complète et conviviale pour implémenter la vérification des codes QR dans vos applications .NET.

En suivant ce tutoriel, vous avez appris à :
- Configurer et initialiser le processus de vérification
- Spécifier différents critères de vérification
- Traiter et interpréter les résultats de la vérification
- Mettre en œuvre des options de vérification avancées

Ces connaissances vous permettent d’améliorer la sécurité et la fiabilité de vos systèmes de gestion de documents.

## FAQ

### GroupDocs.Signature peut-il vérifier plusieurs codes QR dans un seul document ?
Oui, GroupDocs.Signature peut vérifier plusieurs codes QR dans un même document. Les résultats de la vérification incluront tous les codes QR correspondants.

### Quels formats de documents sont pris en charge pour la vérification par code QR ?
GroupDocs.Signature prend en charge une large gamme de formats de documents, notamment PDF, Word (DOC, DOCX), Excel (XLS, XLSX), PowerPoint (PPT, PPTX), images, etc.

### Puis-je vérifier les codes QR avec un cryptage ou un formatage spécifique ?
Oui, GroupDocs.Signature fournit des options pour vérifier les codes QR avec des types d’encodage et des modèles de formatage de contenu spécifiques.

### Est-il possible de vérifier les codes QR créés par des applications tierces ?
Oui, GroupDocs.Signature peut vérifier les codes QR standard générés par la plupart des applications, à condition qu'ils suivent les formats de code QR standard.

### Comment gérer les codes QR qui contiennent des données binaires au lieu de texte ?
GroupDocs.Signature fournit des options pour vérifier les codes QR avec des données binaires via le `BinaryData` propriété des options de vérification.

### Ressources connexes
* [Référence de l'API GroupDocs.Signature](https://reference.groupdocs.com/signature/net/)
* [Téléchargements de GroupDocs.Signature](https://releases.groupdocs.com/signature/net/)
* [Exemples de code sur GitHub](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
* [Documentation](https://docs.groupdocs.com/signature/net/)
* [Page produit](https://products.groupdocs.com/signature/net/)
* [Articles de blog](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
* [Forum d'assistance](https://forum.groupdocs.com/c/signature/13)
* [Licence temporaire](https://purchase.groupdocs.com/temporary-license/)