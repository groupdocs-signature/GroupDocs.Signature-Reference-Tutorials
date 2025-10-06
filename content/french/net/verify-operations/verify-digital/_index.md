---
"description": "Implémentez la vérification sécurisée des signatures numériques dans les applications .NET avec GroupDocs.Signature. Guide étape par étape avec des exemples de code complets pour l'authentification de documents."
"linktitle": "Vérifier la signature numérique"
"second_title": "API .NET GroupDocs.Signature"
"title": "Vérifier les signatures numériques dans les documents"
"url": "/fr/net/verify-operations/verify-digital/"
"weight": 11
type: docs
---
## Introduction

Les signatures numériques jouent un rôle crucial pour garantir l'authenticité, l'intégrité et la non-répudiation des documents dans les processus commerciaux modernes. Contrairement aux signatures manuscrites traditionnelles, les signatures numériques utilisent des techniques cryptographiques pour vérifier l'identité du signataire et garantir que le document n'a pas été modifié depuis sa signature.

GroupDocs.Signature pour .NET fournit une boîte à outils complète permettant aux développeurs d'implémenter une vérification robuste des signatures numériques dans leurs applications .NET. Ce tutoriel détaillé vous guidera tout au long du processus de vérification des signatures numériques dans les documents avec GroupDocs.Signature pour .NET.

## Prérequis

Avant de mettre en œuvre la fonctionnalité de vérification de signature numérique, assurez-vous de disposer des conditions préalables suivantes :

1. GroupDocs.Signature pour .NET : téléchargez et installez la bibliothèque depuis [GroupDocs.Signature pour les versions .NET](https://releases.groupdocs.com/signature/net/).
2. Environnement de développement .NET : Visual Studio ou tout environnement de développement .NET compatible.
3. Certificat numérique : un fichier de certificat numérique (par exemple, .pfx) qui a été utilisé pour signer le document ou un certificat appartenant à la chaîne de confiance.
4. Document à vérifier : un document contenant des signatures numériques qui nécessitent une vérification.

## Importer les espaces de noms requis

Commencez par importer les espaces de noms nécessaires pour accéder à la fonctionnalité GroupDocs.Signature :

```csharp
using System;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

Décomposons le processus de vérification des signatures numériques en étapes claires et gérables :

## Étape 1 : Spécifier le chemin du document

```csharp
// Chemin d'accès au document contenant les signatures numériques
string filePath = "sample_multiple_signatures.docx";
```

Remplacez le chemin d’exemple par le chemin réel vers votre document contenant les signatures numériques.

## Étape 2 : Initialiser l’objet Signature

```csharp
// Créer une instance de la classe Signature en passant le chemin du document
using (Signature signature = new Signature(filePath))
{
    // Le code de vérification sera implémenté ici
}
```

La classe Signature est le point d’entrée principal pour toutes les opérations de l’API GroupDocs.Signature.

## Étape 3 : Configurer les options de vérification numérique

```csharp
// Options de vérification de la configuration
DigitalVerifyOptions options = new DigitalVerifyOptions("YourSignature.pfx")
{
    Contact = "Mr.Smith",     // Contact attendu du signataire
    Password = "1234567890",  // Mot de passe du certificat si nécessaire
    AllPages = true           // Vérifiez toutes les pages pour les signatures
};
```

Les options de vérification vous permettent de spécifier :
- Le chemin du fichier de certificat numérique
- Coordonnées attendues du signataire
- Mot de passe du certificat s'il est protégé par mot de passe
- Plage de pages à vérifier (toutes les pages par défaut)

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
    Console.WriteLine($"Document {filePath} contains valid digital signatures!");
    
    // Afficher les détails des signatures valides
    foreach (DigitalSignature digitalSignature in result.Succeeded)
    {
        Console.WriteLine($"\nValid signature found:");
        Console.WriteLine($"Signer: {digitalSignature.Subject}");
        Console.WriteLine($"Issuer: {digitalSignature.Issuer}");
        Console.WriteLine($"Valid From: {digitalSignature.ValidFrom}");
        Console.WriteLine($"Valid To: {digitalSignature.ValidTo}");
    }
}
else
{
    Console.WriteLine($"Document {filePath} failed verification process.");
    
    // Afficher des informations sur les signatures échouées si nécessaire
    foreach (DigitalSignature failedSignature in result.Failed)
    {
        Console.WriteLine($"Failed signature reason: {failedSignature.Comments}");
    }
}
```

Ce code vérifie si la vérification a réussi et fournit des informations détaillées sur les signatures qui ont été vérifiées.

## Exemple complet

Voici un exemple fonctionnel complet qui illustre la vérification de la signature numérique :

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
                    DigitalVerifyOptions options = new DigitalVerifyOptions("YourSignature.pfx")
                    {
                        Contact = "Mr.Smith",
                        Password = "1234567890"
                    };
                    
                    // Vérifier les signatures des documents
                    VerificationResult result = signature.Verify(options);
                    
                    // Résultats de la vérification du processus
                    if (result.IsValid)
                    {
                        Console.WriteLine($"Document {filePath} contains valid digital signatures!");
                        
                        foreach (DigitalSignature item in result.Succeeded)
                        {
                            Console.WriteLine($"\nValid signature found.");
                            Console.WriteLine($"Subject: {item.Subject}");
                            Console.WriteLine($"Comments: {item.Comments}");
                            Console.WriteLine($"Sign Time: {item.SignTime}");
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

### Vérification de plusieurs signatures numériques

```csharp
// Créer une liste d'options de vérification
List<VerifyOptions> listOptions = new List<VerifyOptions>();

// Ajouter les premières options de vérification du certificat
listOptions.Add(new DigitalVerifyOptions("Certificate1.pfx")
{
    Contact = "John Smith"
});

// Ajouter des options de vérification du deuxième certificat
listOptions.Add(new DigitalVerifyOptions("Certificate2.pfx")
{
    Contact = "Jane Doe"
});

// Vérifier avec plusieurs options
VerificationResult result = signature.Verify(listOptions);
```

### Vérification des signatures sur des pages spécifiques

```csharp
// Vérifiez les signatures numériques uniquement sur la première page
DigitalVerifyOptions options = new DigitalVerifyOptions("YourSignature.pfx")
{
    AllPages = false,
    PageNumber = 1
};
```

### Utilisation de l'horodatage et de la validation de l'autorité de certification

```csharp
DigitalVerifyOptions options = new DigitalVerifyOptions("YourSignature.pfx")
{
    ValidateTimeStampOnly = true,   // Valider uniquement l'horodatage
    CertificateAuth = CertificateAuthType.Standard  // Valide le certificat du signataire
};
```

## Meilleures pratiques pour la vérification de la signature numérique

1. Gestion appropriée des certificats : stockez les fichiers de certificats en toute sécurité et gérez les mots de passe de manière appropriée.
2. Validation du certificat : implémentez la validation de la chaîne de certificats pour garantir que le certificat lui-même est valide.
3. Gestion des erreurs : implémentez une gestion des erreurs robuste pour gérer les échecs de vérification avec élégance.
4. Journalisation : enregistrez les tentatives de vérification et les résultats à des fins d'audit et de conformité.
5. Mises à jour régulières des certificats : assurez-vous que les certificats sont mis à jour avant leur expiration.

## Dépannage des problèmes courants

### Certificat invalide
- Vérifiez que le chemin du fichier de certificat est correct
- Assurez-vous que le mot de passe du certificat est correct
- Vérifiez si le certificat a expiré

### Signature non trouvée
- Confirmer que le document contient effectivement des signatures numériques
- Vérifiez que vous consultez les bonnes pages

### Échecs de vérification
- Vérifiez si le document a été modifié après la signature
- Vérifiez que le certificat du signataire se trouve dans la chaîne de certificats de confiance

## Conclusion

GroupDocs.Signature pour .NET offre une solution puissante et flexible pour vérifier les signatures numériques dans les documents. En suivant ce guide étape par étape, vous pourrez implémenter une vérification robuste des signatures numériques dans vos applications .NET, garantissant ainsi l'authenticité et l'intégrité des documents.

La vérification des signatures numériques est un élément essentiel des flux de travail sécurisés dans les environnements professionnels modernes. Avec GroupDocs.Signature, vous pouvez implémenter cette fonctionnalité en toute confiance et avec un minimum d'efforts, en tirant parti de l'API complète pour gérer divers scénarios de vérification.

## FAQ

### GroupDocs.Signature peut-il vérifier les signatures dans les documents PDF signés à l'aide d'Adobe Acrobat ?
Oui, GroupDocs.Signature peut vérifier les signatures numériques standard dans les documents PDF créés par Adobe Acrobat et d'autres logiciels PDF compatibles.

### GroupDocs.Signature prend-il en charge la vérification des horodatages des documents ?
Oui, l’API fournit des options pour vérifier les horodatages des documents dans le cadre du processus de vérification de la signature numérique.

### Puis-je vérifier les signatures sur des pages spécifiques d’un document de plusieurs pages ?
Oui, vous pouvez configurer les options de vérification pour vérifier les signatures sur des pages spécifiques plutôt que sur l’ensemble du document.

### GroupDocs.Signature prend-il en charge la vérification de plusieurs signatures dans un même document ?
Oui, GroupDocs.Signature peut vérifier plusieurs signatures numériques dans un seul document et fournir des résultats détaillés pour chaque signature.

### Est-il possible de vérifier les signatures créées avec des certificats provenant de différentes autorités de certification ?
Oui, GroupDocs.Signature prend en charge la vérification des signatures créées avec des certificats provenant de différentes autorités de certification, à condition qu'elles se trouvent dans la chaîne de certificats de confiance.

### Ressources connexes
* [Référence de l'API GroupDocs.Signature](https://reference.groupdocs.com/signature/net/)
* [Téléchargements de GroupDocs.Signature](https://releases.groupdocs.com/signature/net/)
* [Exemples de code sur GitHub](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
* [Documentation](https://docs.groupdocs.com/signature/net/)
* [Page produit](https://products.groupdocs.com/signature/net/)
* [Articles de blog](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
* [Forum d'assistance](https://forum.groupdocs.com/c/signature/13)
* [Licence temporaire](https://purchase.groupdocs.com/temporary-license/)