---
"description": "Maîtrisez la vérification des signatures de texte dans les applications .NET avec GroupDocs.Signature. Guide d'implémentation étape par étape avec des exemples de code complets et les meilleures pratiques."
"linktitle": "Vérifier le texte"
"second_title": "API .NET GroupDocs.Signature"
"title": "Vérifier les signatures de texte dans les documents"
"url": "/fr/net/verify-operations/verify-text/"
"weight": 13
---

## Introduction

Les signatures textuelles, bien que souvent plus simples que les signatures numériques ou électroniques, jouent un rôle crucial dans la gestion et la vérification des documents. Qu'il s'agisse de filigranes, de texte de pied de page ou de modèles de contenu spécifiques, la validation de la présence et de l'intégrité des signatures textuelles est un aspect important des processus de vérification des documents.

GroupDocs.Signature pour .NET fournit une API puissante pour vérifier les signatures textuelles dans des documents de différents formats. Ce tutoriel complet vous guidera dans l'implémentation de la fonctionnalité de vérification textuelle dans vos applications .NET, garantissant ainsi l'intégrité et l'authenticité de vos documents.

## Prérequis

Avant d'implémenter la fonctionnalité de vérification de texte, assurez-vous de disposer des conditions préalables suivantes :

1. GroupDocs.Signature pour .NET : téléchargez et installez la bibliothèque à partir du [page de téléchargement](https://releases.groupdocs.com/signature/net/).
2. Environnement de développement .NET : Visual Studio ou tout environnement de développement .NET compatible.
3. Connaissances de base : Familiarité avec la programmation C# et les concepts du framework .NET.
4. Document de test : un document contenant des signatures textuelles à des fins de vérification.

## Importer les espaces de noms requis

Commencez par importer les espaces de noms nécessaires pour accéder à la fonctionnalité GroupDocs.Signature :

```csharp
using System;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

Décomposons le processus de vérification de texte en étapes claires et gérables :

## Étape 1 : Spécifier le chemin du document

```csharp
// Chemin d'accès au document contenant les signatures de texte
string filePath = "sample_multiple_signatures.docx";
```

Assurez-vous de remplacer le chemin d'exemple par le chemin réel vers votre document contenant les signatures de texte.

## Étape 2 : Initialiser l’objet Signature

```csharp
// Créer une instance de la classe Signature en passant le chemin du document
using (Signature signature = new Signature(filePath))
{
    // Le code de vérification sera implémenté ici
}
```

La classe Signature est le point d’entrée principal pour toutes les opérations de l’API GroupDocs.Signature.

## Étape 3 : Configurer les options de vérification du texte

```csharp
// Définir les options de vérification du texte
TextVerifyOptions options = new TextVerifyOptions()
{
    AllPages = true,                               // Vérifiez toutes les pages du document
    SignatureImplementation = TextSignatureImplementation.Native,
    Text = "signature",                            // Texte à vérifier
    MatchType = TextMatchType.Contains             // Spécifier les critères de correspondance
};
```

Les options de vérification vous permettent de définir des critères spécifiques pour le processus de vérification :
- `AllPages`: Définir sur vrai pour vérifier toutes les pages du document
- `SignatureImplementation`: Spécifiez comment le texte est implémenté (natif ou autocollant)
- `Text`: Le contenu du texte à faire correspondre dans le document
- `MatchType`: La méthode de correspondance de texte (Contient, Exact, Commence par, etc.)

## Étape 4 : Exécuter le processus de vérification

```csharp
// Effectuer la vérification
VerificationResult result = signature.Verify(options);
```

Cela exécute le processus de vérification en fonction des options que vous avez spécifiées.

## Étape 5 : Résultats de la vérification du processus

```csharp
// Vérifiez le résultat de la vérification et procédez en conséquence
if (result.IsValid)
{
    Console.WriteLine($"Document {filePath} contains valid text signatures!");
    
    // Afficher des informations sur les signatures réussies
    foreach (TextSignature textSignature in result.Succeeded)
    {
        Console.WriteLine($"\nFound valid text signature:");
        Console.WriteLine($"Text: {textSignature.Text}");
        Console.WriteLine($"Location: Page {textSignature.PageNumber}, {textSignature.Left}x{textSignature.Top}");
    }
}
else
{
    Console.WriteLine($"Document {filePath} failed verification process.");
    Console.WriteLine($"Number of failed signatures: {result.Failed.Count}");
}
```

Ce code vérifie si la vérification a réussi et fournit des informations détaillées sur les signatures de texte qui ont été vérifiées.

## Exemple complet

Voici un exemple fonctionnel complet qui illustre la vérification de la signature de texte :

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
            
            try
            {
                // Initialiser l'instance de signature
                using (Signature signature = new Signature(filePath))
                {
                    // Options de vérification de la configuration
                    TextVerifyOptions options = new TextVerifyOptions()
                    {
                        AllPages = true,
                        SignatureImplementation = TextSignatureImplementation.Native,
                        Text = "signature",
                        MatchType = TextMatchType.Contains
                    };
                    
                    // Vérifier les signatures des documents
                    VerificationResult result = signature.Verify(options);
                    
                    // Résultats de la vérification du processus
                    if(result.IsValid)
                    {
                        Console.WriteLine($"\nDocument {filePath} was verified successfully!");
                        foreach (TextSignature item in result.Succeeded)
                        {
                            Console.WriteLine($"\nValid signature is found with text: {item.Text}");
                            Console.WriteLine($"Location: Page {item.PageNumber}, position {item.Left}x{item.Top}");
                        }
                    }
                    else
                    {
                        Console.WriteLine($"\nDocument {filePath} failed verification process.");
                    }
                }
            }
            catch (Exception ex)
            {
                Console.WriteLine($"Error: {ex.Message}");
            }
        }
    }
}
```

## Scénarios de vérification avancés

GroupDocs.Signature fournit des options supplémentaires pour des scénarios de vérification plus complexes :

### Utilisation d'expressions régulières pour la vérification

Pour une correspondance de modèles plus flexible, vous pouvez utiliser des expressions régulières :

```csharp
TextVerifyOptions options = new TextVerifyOptions()
{
    Text = "Invoice\\s+#\\d{5,6}",  // Associer des modèles tels que « Facture n° 12345 »
    MatchType = TextMatchType.Regex
};
```

### Vérification du texte dans des zones spécifiques du document

Vous pouvez restreindre la vérification à des zones spécifiques du document :

```csharp
TextVerifyOptions options = new TextVerifyOptions()
{
    AllPages = false,
    PageNumber = 1,  // Vérifier uniquement sur la première page
    
    // Définir la zone de recherche (coordonnées en points)
    PagesSetup = new PagesSetup() 
    { 
        FirstPage = true,
        LastPage = false,
        OddPages = false,
        EvenPages = false 
    },
    
    // Aire du rectangle en millimètres
    Rectangle = new Rectangle(10, 10, 100, 30),
    
    Text = "Confidential"
};
```

### Vérification simultanée de plusieurs modèles de texte

Vous pouvez créer plusieurs options de vérification pour vérifier différents modèles de texte :

```csharp
// Créer une liste d'options de vérification
List<VerifyOptions> listOptions = new List<VerifyOptions>();

// Ajouter la première vérification du texte
listOptions.Add(new TextVerifyOptions()
{
    Text = "Confidential",
    MatchType = TextMatchType.Exact
});

// Ajouter une deuxième vérification de texte
listOptions.Add(new TextVerifyOptions()
{
    Text = "Do not copy",
    MatchType = TextMatchType.Contains
});

// Vérifier avec plusieurs options
VerificationResult result = signature.Verify(listOptions);
```

### Vérification du texte avec une apparence spécifique

Vous pouvez également vérifier le texte avec des caractéristiques de formatage spécifiques :

```csharp
TextVerifyOptions options = new TextVerifyOptions()
{
    Text = "APPROVED",
    MatchType = TextMatchType.Exact,
    
    // Vérifier les propriétés d'apparence spécifiques
    ForegroundColorRGB = System.Drawing.Color.Green,
    Font = new SignatureFont() { FontFamily = "Arial", FontSize = 12, Bold = true }
};
```

## Meilleures pratiques pour la vérification de texte

1. Choisissez les types de correspondance appropriés : sélectionnez le type de correspondance approprié (Contient, Exact, Regex) en fonction de vos exigences de vérification.
2. Optimiser les performances : pour les documents volumineux, pensez à vérifier des pages spécifiques plutôt que le document entier.
3. Gestion des erreurs : implémentez une gestion des erreurs appropriée pour gérer les scénarios inattendus avec élégance.
4. Tenez compte de la sensibilité à la casse : soyez attentif à la sensibilité à la casse dans la correspondance de texte, en particulier pour les vérifications critiques.
5. Testez minutieusement : testez la vérification avec différents formats de documents et modèles de texte pour garantir la compatibilité.

## Dépannage des problèmes courants

### Texte non détecté
- Vérifiez si le formatage ou l'encodage du texte affecte la détection
- Assurez-vous que le texte est réellement présent dans le document sous forme de texte normal (et non d'image)
- Essayez différents critères de correspondance (Contient au lieu d'Exact)

### Problèmes de performances
- Optimisez la vérification en ciblant des pages ou des zones spécifiques
- Utilisez des modèles de texte plus spécifiques pour réduire les faux positifs

### Échecs de vérification
- Vérifiez si les espaces, les caractères spéciaux ou le formatage affectent la correspondance
- Vérifiez que le texte ne fait pas partie d'une image numérisée (ce qui nécessite l'OCR)
- Assurez-vous que le document n'a pas été modifié depuis l'ajout du texte

## Conclusion

La vérification de texte est une approche polyvalente et pratique de l'authentification de documents, utilisable seule ou en combinaison avec d'autres méthodes de vérification. GroupDocs.Signature pour .NET fournit une API complète et facile à utiliser pour implémenter une fonctionnalité de vérification de texte robuste dans vos applications .NET.

En suivant ce guide étape par étape, vous avez appris à :
- Configurer et initialiser le processus de vérification de texte
- Spécifier différents critères de vérification
- Traiter et interpréter les résultats de la vérification
- Mettre en œuvre des scénarios de vérification avancés

Ces fonctionnalités vous permettent de créer des systèmes de traitement de documents sécurisés et fiables, capables de vérifier l’authenticité du texte dans différents formats de documents.

## FAQ

### GroupDocs.Signature peut-il vérifier le texte des documents numérisés ?
GroupDocs.Signature est principalement conçu pour la vérification de textes numériques. Pour les documents numérisés, vous devrez d'abord utiliser la technologie OCR (reconnaissance optique de caractères) pour convertir les images numérisées en texte.

### Quels formats de documents sont pris en charge pour la vérification de texte ?
GroupDocs.Signature prend en charge une large gamme de formats de documents, notamment les documents PDF, Word (DOC, DOCX), les feuilles de calcul Excel (XLS, XLSX), les présentations PowerPoint (PPT, PPTX), les images, etc.

### Puis-je vérifier le texte formaté (gras, italique, polices spécifiques) ?
Oui, GroupDocs.Signature fournit des options pour vérifier le texte avec des caractéristiques de formatage spécifiques, notamment la famille de polices, la taille, le style (gras, italique) et la couleur.

### Est-il possible de vérifier le texte dans des documents protégés par mot de passe ?
Oui, GroupDocs.Signature fournit des options permettant de spécifier les mots de passe des documents lors de l’ouverture de documents protégés pour vérification.

### Puis-je vérifier les filigranes et le texte d’arrière-plan ?
Oui, GroupDocs.Signature peut vérifier différents types de signatures de texte, y compris les filigranes et le texte d'arrière-plan, selon la manière dont ils ont été implémentés dans le document.

### Ressources connexes
* [Référence de l'API GroupDocs.Signature](https://reference.groupdocs.com/signature/net/)
* [Téléchargements de GroupDocs.Signature](https://releases.groupdocs.com/signature/net/)
* [Exemples de code sur GitHub](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
* [Documentation](https://docs.groupdocs.com/signature/net/)
* [Page produit](https://products.groupdocs.com/signature/net/)
* [Articles de blog](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
* [Forum d'assistance](https://forum.groupdocs.com/c/signature/13)
* [Licence temporaire](https://purchase.groupdocs.com/temporary-license/)