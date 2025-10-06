---
"description": "Découvrez comment rechercher efficacement des codes QR dans des documents à l'aide de GroupDocs.Signature pour .NET avec ce guide complet étape par étape et des exemples de code."
"linktitle": "Rechercher des codes QR"
"second_title": "API .NET GroupDocs.Signature"
"title": "Rechercher des signatures de code QR dans les documents"
"url": "/fr/net/signature-searching/search-for-qr-codes/"
"weight": 15
type: docs
---
## Introduction

Dans l'écosystème actuel des documents numériques, les signatures par code QR sont devenues un outil précieux pour l'intégration d'informations, l'authentification et la sécurisation des documents. GroupDocs.Signature pour .NET offre aux développeurs une API puissante pour rechercher et extraire des codes QR de divers formats de documents, offrant ainsi des fonctionnalités avancées d'analyse et de vérification de documents dans les applications .NET.

Ce didacticiel complet vous guidera tout au long du processus de mise en œuvre de la fonctionnalité de recherche de code QR à l'aide de GroupDocs.Signature pour .NET, en fournissant des explications claires, des instructions étape par étape et des exemples de code pratiques que vous pouvez intégrer dans vos propres applications.

## Prérequis

Avant de vous lancer dans la recherche de signature de code QR, assurez-vous de disposer des prérequis suivants :

1. GroupDocs.Signature pour .NET SDK : téléchargez et installez le SDK à partir du [page de téléchargement](https://releases.groupdocs.com/signature/net/).

2. Environnement de développement : configurez un environnement de développement .NET, tel que Visual Studio, avec .NET Framework ou .NET Core installé.

3. Connaissances de base : Familiarité avec la programmation C# et les concepts de développement .NET.

4. Exemples de documents : Préparez des documents de test contenant des codes QR pour vérification et test.

## Importer des espaces de noms

Commencez par importer les espaces de noms nécessaires pour accéder à la fonctionnalité GroupDocs.Signature :

```csharp
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
using System;
using System.Collections.Generic;
```

Décomposons maintenant le processus de recherche de codes QR en étapes claires et faciles à suivre :

## Étape 1 : Définir le chemin du document

Tout d’abord, spécifiez le chemin d’accès au document contenant les codes QR que vous souhaitez rechercher :

```csharp
string filePath = "sample_multiple_signatures.docx";
```

## Étape 2 : Initialiser l’objet Signature

Créer une instance de `Signature` classe en passant le chemin du document :

```csharp
using (Signature signature = new Signature(filePath))
{
    // Le code de recherche du code QR sera ajouté ici
}
```

## Étape 3 : Rechercher des signatures de codes QR

Utilisez le `Search` méthode avec le type de signature approprié pour trouver les codes QR dans le document :

```csharp
// Rechercher des signatures de code QR dans le document
List<QrCodeSignature> signatures = signature.Search<QrCodeSignature>(SignatureType.QrCode);
```

## Étape 4 : Traiter et afficher les résultats

Parcourez les signatures de codes QR trouvées et accédez à leurs propriétés :

```csharp
// Afficher des informations sur les codes QR trouvés
Console.WriteLine($"\nSource document contains {signatures.Count} QR code signature(s):");

foreach (var qrCodeSignature in signatures)
{
    Console.WriteLine($"QR Code found at page {qrCodeSignature.PageNumber} with type {qrCodeSignature.EncodeType.TypeName}");
    Console.WriteLine($"Content: {qrCodeSignature.Text}");
    Console.WriteLine($"Location: X={qrCodeSignature.Left}, Y={qrCodeSignature.Top}, Width={qrCodeSignature.Width}, Height={qrCodeSignature.Height}");
    Console.WriteLine();
}
```

## Exemple complet

Voici un exemple de travail complet qui démontre le processus complet de recherche de codes QR dans un document :

```csharp
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
using System;
using System.Collections.Generic;

namespace QrCodeSignatureSearch
{
    class Program
    {
        static void Main(string[] args)
        {
            // Chemin du document - mettre à jour avec le chemin de votre fichier
            string filePath = "sample_multiple_signatures.docx";
            
            // Initialiser l'instance de signature
            using (Signature signature = new Signature(filePath))
            {
                try
                {
                    // Rechercher des signatures de code QR dans le document
                    List<QrCodeSignature> signatures = signature.Search<QrCodeSignature>(SignatureType.QrCode);
                    
                    // Afficher les résultats de la recherche
                    Console.WriteLine($"\nSource document ['{filePath}'] contains {signatures.Count} QR code signature(s):");
                    
                    foreach (var qrCodeSignature in signatures)
                    {
                        Console.WriteLine($"QR Code found at page {qrCodeSignature.PageNumber} with type {qrCodeSignature.EncodeType.TypeName}");
                        Console.WriteLine($"Content: {qrCodeSignature.Text}");
                        Console.WriteLine($"Location: X={qrCodeSignature.Left}, Y={qrCodeSignature.Top}, Width={qrCodeSignature.Width}, Height={qrCodeSignature.Height}");
                        Console.WriteLine();
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

## Techniques avancées de recherche de codes QR

### Recherche avec des critères spécifiques

Pour des recherches plus ciblées, vous pouvez utiliser `QrCodeSearchOptions` pour personnaliser vos critères de recherche :

```csharp
// Créez des options de recherche de code QR avec des critères spécifiques
QrCodeSearchOptions options = new QrCodeSearchOptions
{
    // Rechercher uniquement sur des pages spécifiques
    AllPages = false,
    PageNumber = 1,
    PagesSetup = new PagesSetup { Pages = new List<int> { 1, 3, 5 } },
    
    // Filtrer par contenu de code QR
    Text = "Invoice",
    MatchType = TextMatchType.Contains,
    
    // Filtrer par types de codes QR spécifiques
    EncodeType = QrCodeTypes.QR,
    
    // Définir une zone spécifique dans laquelle effectuer la recherche
    Rectangle = new Rectangle(100, 100, 400, 400)
};

// Rechercher avec des options spécifiques
List<QrCodeSignature> filteredSignatures = signature.Search<QrCodeSignature>(options);
```

### Traitement des données du code QR

Vous pouvez implémenter un traitement personnalisé pour les données de code QR en fonction des exigences de votre application :

```csharp
foreach (var qrCode in signatures)
{
    // Extraire et traiter les données du code QR en fonction du contenu
    string qrContent = qrCode.Text;
    
    if (qrContent.StartsWith("URL:"))
    {
        // Traiter les données URL
        string url = qrContent.Substring(4);
        Console.WriteLine($"Found URL in QR code: {url}");
    }
    else if (qrContent.StartsWith("CONTACT:"))
    {
        // Informations de contact du processus
        string contact = qrContent.Substring(8);
        Console.WriteLine($"Found contact information in QR code: {contact}");
    }
    else if (qrContent.StartsWith("INVOICE:"))
    {
        // Traiter les informations de facturation
        string invoiceData = qrContent.Substring(8);
        Console.WriteLine($"Found invoice information in QR code: {invoiceData}");
        
        // Analyser et valider les données de facturation
        if (ValidateInvoiceData(invoiceData))
        {
            Console.WriteLine("Invoice data is valid!");
        }
        else
        {
            Console.WriteLine("Warning: Invalid invoice data detected!");
        }
    }
}

// Exemple de méthode de validation
static bool ValidateInvoiceData(string data)
{
    // Implémentez votre logique de validation
    return !string.IsNullOrEmpty(data) && data.Contains("ID") && data.Contains("Amount");
}
```

### Mise en œuvre de la vérification de sécurité

Les codes QR sont souvent utilisés à des fins d'authentification. Voici comment mettre en œuvre une vérification de sécurité de base :

```csharp
// Vérifiez si le document contient un code QR d'authentification valide
bool hasValidAuthQrCode = false;

foreach (var qrCode in signatures)
{
    if (qrCode.Text.StartsWith("AUTH:"))
    {
        string authCode = qrCode.Text.Substring(5);
        
        // Vérifier le code d'authentification (par exemple, par rapport à une base de données ou à une liste prédéfinie)
        if (VerifyAuthCode(authCode))
        {
            hasValidAuthQrCode = true;
            Console.WriteLine("Document contains valid authentication QR code!");
            break;
        }
    }
}

if (!hasValidAuthQrCode)
{
    Console.WriteLine("Warning: Document does not contain a valid authentication QR code!");
}

// Exemple de méthode de vérification
static bool VerifyAuthCode(string code)
{
    // Implémentez votre logique de vérification
    // Il peut s'agir d'une recherche dans une base de données, d'un appel d'API ou d'une comparaison avec des valeurs prédéfinies.
    return code == "A7B82C3D" || code == "X9Y8Z7W6";
}
```

### Extraction d'images de codes QR

Vous pouvez extraire des images de code QR à partir de documents pour un traitement ultérieur ou un affichage :

```csharp
// Enregistrer les images du code QR sur le disque
foreach (var qrCode in signatures)
{
    if (qrCode.Content != null)
    {
        // Créez un nom de fichier unique basé sur le numéro de page et la position
        string outputPath = $"QrCode_P{qrCode.PageNumber}_X{qrCode.Left}_Y{qrCode.Top}.png";
        
        // Enregistrer les données de l'image
        File.WriteAllBytes(outputPath, qrCode.Content);
        Console.WriteLine($"Saved QR code image to {outputPath}");
    }
}
```

## Conclusion

Dans ce guide complet, nous avons découvert comment rechercher des signatures de codes QR dans des documents à l'aide de GroupDocs.Signature pour .NET. De la recherche basique aux techniques avancées, vous disposez désormais des connaissances nécessaires pour implémenter une gestion robuste des codes QR dans vos applications .NET. L'API GroupDocs.Signature offre un cadre puissant et flexible pour travailler avec différents types de signatures, dont les codes QR, dans différents formats de documents.

En exploitant ces fonctionnalités, vous pouvez améliorer les processus de vérification des documents, mettre en œuvre des systèmes d’authentification et extraire des informations précieuses intégrées dans les codes QR, le tout dans vos applications .NET.

## FAQ

### Quels formats de code QR sont pris en charge par GroupDocs.Signature ?

GroupDocs.Signature prend en charge différents formats de codes QR, notamment les codes QR standard, les micro-codes QR et d'autres normes courantes. Le format spécifique est accessible via le `EncodeType` propriété de la `QrCodeSignature` objet.

### Puis-je rechercher des codes QR dans des documents protégés par mot de passe ?

Oui, GroupDocs.Signature prend en charge la recherche de codes QR dans les documents protégés par mot de passe en fournissant le mot de passe lors de l'initialisation du `Signature` objet:

```csharp
LoadOptions loadOptions = new LoadOptions { Password = "your_password" };
using (Signature signature = new Signature(filePath, loadOptions))
{
    // Rechercher des codes QR
}
```

### Comment puis-je filtrer les codes QR en fonction de leur contenu ?

Vous pouvez filtrer les codes QR en fonction de leur contenu à l'aide de l' `Text` et `MatchType` propriétés de `QrCodeSearchOptions`:

```csharp
QrCodeSearchOptions options = new QrCodeSearchOptions
{
    Text = "Invoice",
    MatchType = TextMatchType.Contains // Autres options : Exact, Commence par, Se termine par
};
```

### GroupDocs.Signature peut-il détecter les codes QR endommagés ou partiellement visibles ?

GroupDocs.Signature est capable de détecter les codes QR partiellement visibles, mais les codes QR fortement endommagés peuvent ne pas être reconnus. La précision de la détection dépend de la qualité et de la visibilité du code QR dans le document.

### Quels formats de documents sont pris en charge pour la recherche par code QR ?

GroupDocs.Signature prend en charge la recherche de codes QR dans divers formats de documents, notamment PDF, documents Microsoft Office (Word, Excel, PowerPoint), images (JPEG, PNG, TIFF) et bien d'autres.

## Voir aussi

* [Référence de l'API](https://reference.groupdocs.com/signature/net/)
* [Exemples de code sur GitHub](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
* [Documentation du produit](https://docs.groupdocs.com/signature/net/)
* [Page produit](https://products.groupdocs.com/signature/net/)
* [Télécharger la dernière version](https://releases.groupdocs.com/signature/net/)
* [Articles de blog](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
* [Forum d'assistance gratuit](https://forum.groupdocs.com/c/signature/13)
* [Licence temporaire](https://purchase.groupdocs.com/temporary-license/)