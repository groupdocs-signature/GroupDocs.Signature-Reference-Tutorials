---
"description": "Maîtrisez la recherche de signatures numériques dans vos documents avec GroupDocs.Signature pour .NET. Améliorez la sécurité et la vérification de vos documents grâce à notre guide détaillé étape par étape."
"linktitle": "Rechercher des signatures numériques"
"second_title": "API .NET GroupDocs.Signature"
"title": "Rechercher des signatures numériques dans les documents"
"url": "/fr/net/signature-searching/search-for-digital-signatures/"
"weight": 11
type: docs
---
## Introduction

Dans le paysage numérique actuel, garantir l'authenticité et l'intégrité des documents est essentiel pour les entreprises et les organisations. Les signatures numériques offrent un mécanisme fiable pour vérifier l'authenticité des documents et détecter les modifications non autorisées. GroupDocs.Signature pour .NET offre une solution complète pour travailler avec des signatures numériques dans différents formats de documents, permettant aux développeurs d'intégrer facilement la fonctionnalité de signature à leurs applications .NET.

Ce didacticiel vous guidera tout au long du processus de recherche de signatures numériques dans des documents à l'aide de GroupDocs.Signature pour .NET, en fournissant des explications détaillées et des exemples de code pratiques.

## Prérequis

Avant de plonger dans les détails de mise en œuvre, assurez-vous de disposer des prérequis suivants :

1. GroupDocs.Signature pour .NET : téléchargez et installez la bibliothèque depuis [ici](https://releases.groupdocs.com/signature/net/).
   
2. Environnement de développement : configurez un environnement de développement .NET avec Visual Studio ou votre IDE préféré.
   
3. Exemples de documents : Préparez des exemples de documents contenant des signatures numériques à des fins de test.

4. Connaissances de base : Familiarité avec le langage de programmation C# et les fondamentaux du framework .NET.

## Importer des espaces de noms

Commencez par importer les espaces de noms requis pour accéder aux fonctionnalités fournies par GroupDocs.Signature pour .NET :

```csharp
using System;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

Décomposons maintenant le processus de recherche de signatures numériques en étapes claires et gérables :

## Étape 1 : Initialiser l'objet Signature

Commencez par créer une instance du `Signature` classe, en passant le chemin vers votre document :

```csharp
string filePath = "sample_multiple_signatures.docx";
using (Signature signature = new Signature(filePath))
{
    // Le code de recherche de signatures numériques sera ajouté ici
}
```

## Étape 2 : Rechercher des signatures numériques

Ensuite, utilisez le `Search` méthode avec le `SignatureType.Digital` paramètre pour rechercher des signatures numériques dans le document :

```csharp
// Rechercher des signatures numériques dans le document
List<DigitalSignature> signatures = signature.Search<DigitalSignature>(SignatureType.Digital);
```

## Étape 3 : Traiter et afficher les résultats

Enfin, traitez les résultats de la recherche et affichez les informations pertinentes sur les signatures numériques trouvées :

```csharp
Console.WriteLine($"\nSource document ['{filePath}'] contains the following digital signatures:");
foreach (var digitalSignature in signatures)
{
    Console.WriteLine($"Digital signature found from {digitalSignature.SignTime} with validation status: {digitalSignature.IsValid}");
    Console.WriteLine($"Certificate: Subject: {digitalSignature.Certificate?.SubjectName}");
    Console.WriteLine($"Certificate: Issuer: {digitalSignature.Certificate?.IssuerName}");
    Console.WriteLine($"Certificate: Serial Number: {digitalSignature.Certificate?.SerialNumber}");
    Console.WriteLine();
}
```

## Exemple complet

Voici un exemple complet et fonctionnel qui montre comment rechercher des signatures numériques dans un document :

```csharp
using System;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;

namespace SearchDigitalSignatures
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
                // Rechercher des signatures numériques dans le document
                List<DigitalSignature> signatures = signature.Search<DigitalSignature>(SignatureType.Digital);
                
                // Afficher les résultats de la recherche
                Console.WriteLine($"\nSource document ['{filePath}'] contains the following digital signatures:");
                
                if (signatures.Count > 0)
                {
                    foreach (var digitalSignature in signatures)
                    {
                        Console.WriteLine($"Digital signature found from {digitalSignature.SignTime} with validation status: {digitalSignature.IsValid}");
                        Console.WriteLine($"Certificate: Subject: {digitalSignature.Certificate?.SubjectName}");
                        Console.WriteLine($"Certificate: Issuer: {digitalSignature.Certificate?.IssuerName}");
                        Console.WriteLine($"Certificate: Serial Number: {digitalSignature.Certificate?.SerialNumber}");
                        Console.WriteLine();
                    }
                }
                else
                {
                    Console.WriteLine("No digital signatures found in the document.");
                }
            }
        }
    }
}
```

## Options de recherche avancées

Pour des recherches plus ciblées, vous pouvez utiliser `DigitalSearchOptions` pour personnaliser les critères de recherche :

```csharp
// Créer des options de recherche numérique
DigitalSearchOptions options = new DigitalSearchOptions()
{
    // Rechercher uniquement sur des pages spécifiques (par exemple, pages 1 et 2)
    PageNumber = 1,
    PagesSetup = new PagesSetup() { Pages = new List<int> { 1, 2 } },
    
    // Filtrer par commentaires dans les signatures numériques
    Comments = "Approved",
    
    // Définir la date et la plage horaire pour la recherche
    SignDateTimeFrom = new DateTime(2022, 1, 1),
    SignDateTimeTo = DateTime.Now
};

// Rechercher avec des options spécifiques
List<DigitalSignature> signatures = signature.Search<DigitalSignature>(options);
```

## Travailler avec les informations du certificat

Les signatures numériques contiennent des informations de certificat précieuses auxquelles vous pouvez accéder et valider :

```csharp
foreach (var digitalSignature in signatures)
{
    if (digitalSignature.Certificate != null)
    {
        // Accéder aux propriétés du certificat
        Console.WriteLine($"Certificate Valid From: {digitalSignature.Certificate.NotBefore}");
        Console.WriteLine($"Certificate Valid To: {digitalSignature.Certificate.NotAfter}");
        
        // Vérifiez si le certificat est dans une plage de dates valide
        bool isDateValid = DateTime.Now >= digitalSignature.Certificate.NotBefore && 
                          DateTime.Now <= digitalSignature.Certificate.NotAfter;
        
        Console.WriteLine($"Certificate Date Validity: {isDateValid}");
        
        // Accéder aux détails de l'émetteur du certificat
        Console.WriteLine($"Certificate Issuer: {digitalSignature.Certificate.IssuerName}");
    }
}
```

## Conclusion

GroupDocs.Signature pour .NET offre une solution puissante et flexible pour la recherche et la validation de signatures numériques dans les documents. Dans ce tutoriel, nous avons exploré étape par étape le processus d'implémentation de la fonctionnalité de recherche de signatures numériques dans les applications .NET, vous fournissant ainsi les connaissances nécessaires pour améliorer la sécurité et la vérification de l'intégrité des documents.

En tirant parti de GroupDocs.Signature, vous pouvez créer des systèmes de gestion de documents robustes qui garantissent l'authenticité et l'intégrité de vos documents numériques, favorisant ainsi la confiance et la conformité dans vos processus métier.

## FAQ

### GroupDocs.Signature peut-il vérifier la validité des signatures numériques ?

Oui, GroupDocs.Signature valide automatiquement les signatures numériques pendant le processus de recherche et fournit le statut de validation via le `IsValid` propriété de la `DigitalSignature` classe.

### Quels formats de documents prennent en charge la recherche de signature numérique ?

GroupDocs.Signature prend en charge la recherche de signatures numériques dans divers formats, notamment PDF, documents Microsoft Office (Word, Excel, PowerPoint), formats OpenOffice, etc.

### Puis-je rechercher des signatures numériques dans des documents protégés par mot de passe ?

Oui, vous pouvez rechercher des signatures numériques dans des documents protégés par mot de passe en fournissant le mot de passe lors de l'initialisation du `Signature` objet:

```csharp
LoadOptions loadOptions = new LoadOptions() { Password = "your_password" };
using (Signature signature = new Signature(filePath, loadOptions))
{
    // Rechercher des signatures numériques
}
```

### Comment puis-je vérifier si une signature numérique a été créée par une personne spécifique ?

Vous pouvez examiner le nom du sujet du certificat et d’autres propriétés pour vérifier l’identité du signataire :

```csharp
foreach (var signature in signatures)
{
    if (signature.Certificate?.SubjectName?.Contains("John Doe") == true)
    {
        Console.WriteLine("Found signature by John Doe");
    }
}
```

### Puis-je extraire la clé publique d’un certificat de signature numérique ?

Oui, vous pouvez accéder aux informations de la clé publique via les propriétés du certificat :

```csharp
if (signature.Certificate != null)
{
    // Accéder aux informations de clé publique
    Console.WriteLine($"Public Key: {signature.Certificate.GetPublicKeyString()}");
}
```

## Voir aussi

* [Référence de l'API](https://reference.groupdocs.com/signature/net/)
* [Exemples de code](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
* [Documentation du produit](https://docs.groupdocs.com/signature/net/)
* [Page produit](https://products.groupdocs.com/signature/net/)
* [Télécharger la dernière version](https://releases.groupdocs.com/signature/net/)
* [Articles de blog](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
* [Forum d'assistance](https://forum.groupdocs.com/c/signature/13)
* [Licence temporaire](https://purchase.groupdocs.com/temporary-license/)