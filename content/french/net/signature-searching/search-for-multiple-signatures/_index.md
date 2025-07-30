---
"description": "Découvrez comment rechercher plusieurs types de signatures dans des documents avec GroupDocs.Signature pour .NET. Guide complet avec exemples de code pour une sécurité renforcée des documents."
"linktitle": "Recherche de signatures multiples"
"second_title": "API .NET GroupDocs.Signature"
"title": "Rechercher plusieurs types de signature dans les documents"
"url": "/fr/net/signature-searching/search-for-multiple-signatures/"
"weight": 14
---

## Introduction

Dans les systèmes modernes de gestion de documents, la capacité à rechercher et valider plusieurs types de signatures au sein d'un même document est de plus en plus importante. Les organisations utilisent souvent différents types de signatures, tels que les signatures numériques, les signatures textuelles, les codes-barres, les codes QR, etc., pour renforcer la sécurité des documents et simplifier les processus de vérification. GroupDocs.Signature pour .NET offre un framework puissant permettant aux développeurs de mettre en œuvre une fonctionnalité complète de recherche de signatures dans différents formats de documents.

Ce didacticiel vous guidera tout au long du processus de recherche de plusieurs types de signatures dans des documents à l'aide de GroupDocs.Signature pour .NET, en offrant des explications détaillées et des exemples de code pratiques.

## Prérequis

Avant de vous lancer dans la mise en œuvre de la fonctionnalité de recherche de signatures multiples, assurez-vous de disposer des prérequis suivants :

1. Environnement de développement : Visual Studio ou tout autre environnement de développement .NET préféré installé sur votre système.
  
2. GroupDocs.Signature pour .NET : téléchargez et installez la bibliothèque GroupDocs.Signature pour .NET à partir de [ici](https://releases.groupdocs.com/signature/net/).

3. Connaissances de base en C# : Familiarité avec le langage de programmation C# et les concepts du framework .NET.

4. Exemples de documents : Préparez des documents de test contenant différents types de signatures à des fins de test.

## Importer des espaces de noms

Commencez par importer les espaces de noms nécessaires pour accéder à la fonctionnalité GroupDocs.Signature :

```csharp
using System;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

Décomposons maintenant le processus de recherche de plusieurs types de signatures en étapes claires et gérables :

## Étape 1 : Charger le document

Tout d’abord, chargez le document contenant les signatures que vous souhaitez rechercher :

```csharp
string filePath = "sample_multiple_signatures.docx";
using (Signature signature = new Signature(filePath))
{
    // Le code de recherche multi-signature sera ajouté ici
}
```

## Étape 2 : Définir les options de recherche pour différents types de signature

Créez des options de recherche pour chaque type de signature que vous souhaitez rechercher :

```csharp
// Définir les options de recherche pour les signatures de texte
TextSearchOptions textOptions = new TextSearchOptions
{
    AllPages = true,  // Rechercher sur toutes les pages
    Text = "Signature",  // Facultatif : texte à rechercher
    MatchType = TextMatchType.Contains  // Critères de correspondance
};

// Définir les options de recherche pour les signatures numériques
DigitalSearchOptions digitalOptions = new DigitalSearchOptions
{
    AllPages = true
};

// Définir les options de recherche pour les signatures de codes-barres
BarcodeSearchOptions barcodeOptions = new BarcodeSearchOptions
{
    AllPages = true,
    Text = "123456",  // Facultatif : texte du code-barres à faire correspondre
    MatchType = TextMatchType.Exact  // Critères de correspondance
};

// Définir les options de recherche pour les signatures de code QR
QrCodeSearchOptions qrCodeOptions = new QrCodeSearchOptions
{
    AllPages = true,
    Text = "John",  // Facultatif : texte du code QR à faire correspondre
    MatchType = TextMatchType.Contains  // Critères de correspondance
};

// Définir les options de recherche pour les signatures de métadonnées
MetadataSearchOptions metadataOptions = new MetadataSearchOptions();
```

## Étape 3 : Ajouter des options à une collection

Ajoutez toutes les options de recherche à une collection :

```csharp
// Créer une liste pour contenir toutes les options de recherche
List<SearchOptions> searchOptions = new List<SearchOptions>
{
    textOptions,
    digitalOptions,
    barcodeOptions,
    qrCodeOptions,
    metadataOptions
};
```

## Étape 4 : Effectuer la recherche et traiter les résultats

Exécutez la recherche en utilisant les options de recherche combinées et traitez les résultats :

```csharp
// Rechercher tous les types de signature à l'aide des options définies
SearchResult result = signature.Search(searchOptions);

// Vérifiez si des signatures ont été trouvées
if (result.Signatures.Count > 0)
{
    Console.WriteLine($"\nSource document ['{filePath}'] contains {result.Signatures.Count} signature(s):");
    
    // Parcourir les signatures trouvées
    foreach (var foundSignature in result.Signatures)
    {
        Console.WriteLine($"Signature found: Type: {foundSignature.SignatureType}, Page: {foundSignature.PageNumber}, ID: {foundSignature.SignatureId}");
        
        // Types de signatures spécifiques au processus
        if (foundSignature is TextSignature textSignature)
        {
            Console.WriteLine($"Text: '{textSignature.Text}'");
        }
        else if (foundSignature is BarcodeSignature barcodeSignature)
        {
            Console.WriteLine($"Barcode Type: {barcodeSignature.EncodeType.TypeName}, Text: '{barcodeSignature.Text}'");
        }
        else if (foundSignature is QrCodeSignature qrCodeSignature)
        {
            Console.WriteLine($"QR Code Type: {qrCodeSignature.EncodeType.TypeName}, Text: '{qrCodeSignature.Text}'");
        }
        else if (foundSignature is DigitalSignature digitalSignature)
        {
            Console.WriteLine($"Certificate: {digitalSignature.Certificate?.SubjectName}, Valid: {digitalSignature.IsValid}");
        }
        else if (foundSignature is MetadataSignature metadataSignature)
        {
            Console.WriteLine($"Metadata: Name: {metadataSignature.Name}, Value: {metadataSignature.Value}");
        }
    }
}
else
{
    Console.WriteLine("No signatures were found in the document.");
}
```

## Exemple complet

Voici un exemple complet et fonctionnel qui illustre la recherche de plusieurs types de signatures dans un document :

```csharp
using System;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;

namespace MultiSignatureSearch
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
                try
                {
                    // Définir les options de recherche pour les signatures de texte
                    TextSearchOptions textOptions = new TextSearchOptions
                    {
                        AllPages = true,
                        MatchType = TextMatchType.Contains
                    };

                    // Définir les options de recherche pour les signatures numériques
                    DigitalSearchOptions digitalOptions = new DigitalSearchOptions
                    {
                        AllPages = true
                    };

                    // Définir les options de recherche pour les signatures de codes-barres
                    BarcodeSearchOptions barcodeOptions = new BarcodeSearchOptions
                    {
                        AllPages = true
                    };

                    // Définir les options de recherche pour les signatures de code QR
                    QrCodeSearchOptions qrCodeOptions = new QrCodeSearchOptions
                    {
                        AllPages = true
                    };

                    // Définir les options de recherche pour les signatures de métadonnées
                    MetadataSearchOptions metadataOptions = new MetadataSearchOptions();

                    // Créer une liste pour contenir toutes les options de recherche
                    List<SearchOptions> searchOptions = new List<SearchOptions>
                    {
                        textOptions,
                        digitalOptions,
                        barcodeOptions,
                        qrCodeOptions,
                        metadataOptions
                    };

                    // Rechercher tous les types de signature
                    SearchResult result = signature.Search(searchOptions);

                    // Vérifiez si des signatures ont été trouvées
                    if (result.Signatures.Count > 0)
                    {
                        Console.WriteLine($"\nSource document ['{filePath}'] contains {result.Signatures.Count} signature(s):");
                        
                        // Résultats du processus par type de signature
                        foreach (var foundSignature in result.Signatures)
                        {
                            Console.WriteLine($"Signature found: Type: {foundSignature.SignatureType}, Page: {foundSignature.PageNumber}");
                            
                            // Types de signatures spécifiques au processus
                            switch (foundSignature.SignatureType)
                            {
                                case SignatureType.Text:
                                    var textSignature = foundSignature as TextSignature;
                                    Console.WriteLine($"Text: '{textSignature.Text}'");
                                    break;
                                    
                                case SignatureType.Barcode:
                                    var barcodeSignature = foundSignature as BarcodeSignature;
                                    Console.WriteLine($"Barcode Type: {barcodeSignature.EncodeType.TypeName}, Text: '{barcodeSignature.Text}'");
                                    break;
                                    
                                case SignatureType.QrCode:
                                    var qrCodeSignature = foundSignature as QrCodeSignature;
                                    Console.WriteLine($"QR Code Type: {qrCodeSignature.EncodeType.TypeName}, Text: '{qrCodeSignature.Text}'");
                                    break;
                                    
                                case SignatureType.Digital:
                                    var digitalSignature = foundSignature as DigitalSignature;
                                    Console.WriteLine($"Certificate: {digitalSignature.Certificate?.SubjectName}, Valid: {digitalSignature.IsValid}");
                                    break;
                                    
                                case SignatureType.Metadata:
                                    var metadataSignature = foundSignature as MetadataSignature;
                                    Console.WriteLine($"Metadata: Name: {metadataSignature.Name}, Value: {metadataSignature.Value}");
                                    break;
                            }
                            
                            Console.WriteLine(); // Ajouter un saut de ligne entre les signatures
                        }
                    }
                    else
                    {
                        Console.WriteLine("No signatures were found in the document.");
                    }
                }
                catch (Exception ex)
                {
                    Console.WriteLine($"Error occurred: {ex.Message}");
                }
            }
            
            Console.WriteLine("Press any key to exit...");
            Console.ReadKey();
        }
    }
}
```

## Techniques avancées de recherche multi-signatures

### Filtrage des résultats de recherche

Vous pouvez mettre en œuvre un filtrage avancé pour affiner les résultats de recherche :

```csharp
// Filtrer les résultats par numéro de page
var signaturesOnFirstPage = result.Signatures.FindAll(s => s.PageNumber == 1);

// Filtrer les résultats par type de signature
var digitalSignatures = result.Signatures.FindAll(s => s.SignatureType == SignatureType.Digital);
var qrCodeSignatures = result.Signatures.FindAll(s => s.SignatureType == SignatureType.QrCode);

// Filtrer les signatures de texte contenant un contenu spécifique
var approvalSignatures = result.Signatures
    .FindAll(s => s is TextSignature && ((TextSignature)s).Text.Contains("Approved"));
```

### Validation de plusieurs signatures

Implémenter une logique de validation pour différents types de signature :

```csharp
bool ValidateAllSignatures(SearchResult result)
{
    bool isDocumentValid = true;
    
    // Vérifiez si le document possède une signature numérique valide
    bool hasValidDigitalSignature = result.Signatures
        .Any(s => s is DigitalSignature && ((DigitalSignature)s).IsValid);
    
    if (!hasValidDigitalSignature)
    {
        Console.WriteLine("Warning: Document does not contain a valid digital signature");
        isDocumentValid = false;
    }
    
    // Vérifiez si le document possède le code QR requis
    bool hasRequiredQRCode = result.Signatures
        .Any(s => s is QrCodeSignature && ((QrCodeSignature)s).Text.Contains("Auth-Code"));
    
    if (!hasRequiredQRCode)
    {
        Console.WriteLine("Warning: Document does not contain the required authentication QR code");
        isDocumentValid = false;
    }
    
    return isDocumentValid;
}
```

### Recherche avec traitement personnalisé

Vous pouvez définir une logique de traitement personnalisée pour les opérations de recherche :

```csharp
// Créez des options de recherche avec un traitement personnalisé
TextSearchOptions textOptions = new TextSearchOptions
{
    AllPages = true,
    
    // Définir un traitement personnalisé à l'aide d'un délégué
    ProcessCompleted = (signature) =>
    {
        // Logique de validation personnalisée - accepter uniquement les signatures sur les pages spécifiées
        TextSignature textSignature = signature as TextSignature;
        return textSignature != null && (textSignature.PageNumber == 1 || textSignature.PageNumber == 2);
    }
};
```

## Conclusion

Dans ce guide complet, nous avons découvert comment rechercher plusieurs types de signatures dans des documents à l'aide de GroupDocs.Signature pour .NET. De la configuration des options de recherche pour différents types de signatures au traitement et à la validation des résultats, vous disposez désormais des connaissances nécessaires pour implémenter une fonctionnalité de recherche de signatures performante dans vos applications .NET.

La possibilité de rechercher simultanément plusieurs types de signatures améliore les processus de vérification des documents, renforce les mesures de sécurité et simplifie les processus de validation. GroupDocs.Signature offre un cadre puissant et flexible pour travailler avec différents types de signatures dans différents formats de documents, ce qui en fait un excellent choix pour les applications de traitement de documents.

## FAQ

### Puis-je rechercher des signatures dans des documents protégés par mot de passe ?

Oui, GroupDocs.Signature prend en charge la recherche de signatures dans les documents protégés par mot de passe. Vous pouvez fournir le mot de passe lors de l'initialisation du fichier. `Signature` objet:

```csharp
LoadOptions loadOptions = new LoadOptions { Password = "your_password" };
using (Signature signature = new Signature(filePath, loadOptions))
{
    // Recherche de signatures
}
```

### Quels formats de documents sont pris en charge pour la recherche de signature ?

GroupDocs.Signature prend en charge une large gamme de formats de documents, notamment les documents PDF, Microsoft Office (Word, Excel, PowerPoint), les formats OpenOffice, les images, etc.

### Puis-je limiter la recherche à des pages spécifiques d’un document ?

Oui, chaque type d'option de recherche possède des propriétés qui vous permettent de spécifier les pages à rechercher :

```csharp
TextSearchOptions options = new TextSearchOptions
{
    AllPages = false,  // Ne pas rechercher toutes les pages
    PageNumber = 1,    // Rechercher uniquement sur la page 1
    
    // Ou spécifiez plusieurs pages
    PagesSetup = new PagesSetup { Pages = new List<int> { 1, 3, 5 } }
};
```

### Comment puis-je optimiser les performances lors de la recherche dans des documents volumineux ?

Pour les documents volumineux, vous pouvez optimiser les performances en :

1. Limiter la recherche à des pages ou plages de pages spécifiques
2. Utiliser des critères de recherche plus spécifiques pour réduire le nombre de correspondances potentielles
3. Implémentation de la pagination dans l'affichage de vos résultats
4. Rechercher un type de signature à la fois si vous n'avez pas besoin de résultats simultanés

### Puis-je étendre GroupDocs.Signature pour prendre en charge les types de signature personnalisés ?

Bien que GroupDocs.Signature fournisse une prise en charge intégrée des types de signature courants, vous pouvez étendre ses fonctionnalités en :

1. Création de classes d'options de recherche personnalisées dérivées de `SearchOptions`
2. Implémentation d'une logique de traitement personnalisée à l'aide de `ProcessCompleted` déléguer
3. Développer des classes wrapper qui combinent plusieurs recherches de signatures avec une logique métier avancée

## Voir aussi

* [Référence de l'API](https://reference.groupdocs.com/signature/net/)
* [Exemples de code sur GitHub](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
* [Documentation du produit](https://docs.groupdocs.com/signature/net/)
* [Page produit](https://products.groupdocs.com/signature/net/)
* [Télécharger la dernière version](https://releases.groupdocs.com/signature/net/)
* [Articles de blog](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
* [Forum d'assistance gratuit](https://forum.groupdocs.com/c/signature/13)
* [Licence temporaire](https://purchase.groupdocs.com/temporary-license/)