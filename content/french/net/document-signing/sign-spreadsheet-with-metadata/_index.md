---
"description": "Protégez et optimisez vos feuilles de calcul Excel en intégrant des signatures de métadonnées avec GroupDocs.Signature pour .NET. Ajoutez des informations sur l'auteur, des horodatages et des données personnalisées pour améliorer la traçabilité et l'authenticité des documents."
"linktitle": "Feuille de calcul de signature avec métadonnées"
"second_title": "API .NET GroupDocs.Signature"
"title": "Ajouter des signatures de métadonnées aux feuilles de calcul Excel en C# .NET"
"url": "/fr/net/document-signing/sign-spreadsheet-with-metadata/"
"weight": 13
type: docs
---
## Introduction

Les feuilles de calcul Excel contiennent souvent des données commerciales critiques, des informations financières et des calculs importants. Garantir leur authenticité, retracer leur origine et protéger leur intégrité est crucial dans de nombreux environnements professionnels. Une approche efficace pour renforcer la sécurité et la traçabilité des feuilles de calcul consiste à intégrer des signatures de métadonnées.

Ce tutoriel complet vous guidera dans la signature de feuilles de calcul Excel avec des métadonnées à l'aide de GroupDocs.Signature pour .NET. En ajoutant des signatures de métadonnées, vous pouvez intégrer des informations précieuses telles que les détails de l'auteur, les horodatages de création, les identifiants de document et d'autres propriétés personnalisées directement dans la structure du fichier de la feuille de calcul.

## Prérequis

Avant de poursuivre ce tutoriel, assurez-vous de disposer des éléments suivants :

1. [GroupDocs.Signature pour .NET](https://releases.groupdocs.com/signature/net/) - Téléchargez et installez la bibliothèque
2. Environnement de développement - Visual Studio ou tout autre IDE compatible .NET
3. Feuille de calcul Excel - Un exemple de fichier de feuille de calcul (XLSX, XLS, etc.)
4. Connaissances de base en C# - Familiarité avec le langage de programmation C#

## Importer des espaces de noms

Commencez par importer les espaces de noms nécessaires pour accéder à la fonctionnalité GroupDocs.Signature :

```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

## Étape 1 : Configurer les chemins d’accès aux fichiers

Définissez les chemins d'accès à votre feuille de calcul source et l'endroit où la sortie signée doit être enregistrée :

```csharp
// Spécifiez le chemin d'accès à votre fichier Excel
string filePath = "sample.xlsx";

// Définir le répertoire de sortie et le nom de fichier de la feuille de calcul signée
string outputDirectory = "Your Document Directory";
string outputFilePath = Path.Combine(outputDirectory, "SignSpreadsheetWithMetadata", "SignedWithMetadata.xlsx");

// Assurez-vous que le répertoire de sortie existe
Directory.CreateDirectory(Path.GetDirectoryName(outputFilePath));
```

## Étape 2 : Initialiser l’objet Signature

Créez une instance de la classe Signature avec votre fichier de feuille de calcul source :

```csharp
using (Signature signature = new Signature(filePath))
{
    // Le reste du code ira ici
}
```

## Étape 3 : Créer et configurer les signatures de métadonnées

Ensuite, définissez les options de métadonnées et créez un tableau de signatures de métadonnées de feuille de calcul :

```csharp
// Créer un objet d'options de métadonnées
MetadataSignOptions options = new MetadataSignOptions();

// Créer un tableau de signatures de métadonnées de feuille de calcul avec différents types de données
SpreadsheetMetadataSignature[] signatures = new SpreadsheetMetadataSignature[]
{
    new SpreadsheetMetadataSignature("Author", "Mr.Sherlock Holmes"), // Valeur de chaîne
    new SpreadsheetMetadataSignature("CreatedOn", DateTime.Now),      // Valeur DateTime
    new SpreadsheetMetadataSignature("DocumentId", 123456),           // Valeur entière
    new SpreadsheetMetadataSignature("SignatureId", 123.456D),        // Valeur double
    new SpreadsheetMetadataSignature("Amount", 123.456M),             // Valeur décimale
    new SpreadsheetMetadataSignature("Total", 123.456F)               // Valeur flottante
};

// Ajouter une collection de signatures aux options
options.Signatures.AddRange(signatures);
```

## Étape 4 : Signer la feuille de calcul avec les métadonnées

Appliquez les signatures de métadonnées à la feuille de calcul et enregistrez le résultat :

```csharp
// Signez le document et enregistrez-le dans le chemin du fichier de sortie
SignResult result = signature.Sign(outputFilePath, options);

// Afficher un message de réussite
Console.WriteLine($"\nSource spreadsheet signed successfully with {result.Succeeded.Count} metadata signature(s).");
Console.WriteLine($"Signed spreadsheet saved at: {outputFilePath}");
```

## Exemple complet

Voici l'exemple de code complet qui rassemble toutes les étapes :

```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;

namespace SignSpreadsheetWithMetadataExample
{
    class Program
    {
        static void Main(string[] args)
        {
            // Spécifier les chemins de fichiers
            string filePath = "sample.xlsx";
            string outputFilePath = Path.Combine("Your Document Directory", "SignSpreadsheetWithMetadata", "SignedWithMetadata.xlsx");
            
            // Assurez-vous que le répertoire de sortie existe
            Directory.CreateDirectory(Path.GetDirectoryName(outputFilePath));

            // Signer la feuille de calcul avec des métadonnées
            using (Signature signature = new Signature(filePath))
            {
                // Créer un objet d'options de métadonnées
                MetadataSignOptions options = new MetadataSignOptions();
                
                // Créer un tableau de signatures de métadonnées de feuille de calcul avec différents types de données
                SpreadsheetMetadataSignature[] signatures = new SpreadsheetMetadataSignature[]
                {
                    new SpreadsheetMetadataSignature("Author", "Mr.Sherlock Holmes"), // Valeur de chaîne
                    new SpreadsheetMetadataSignature("CreatedOn", DateTime.Now),      // Valeur DateTime
                    new SpreadsheetMetadataSignature("DocumentId", 123456),           // Valeur entière
                    new SpreadsheetMetadataSignature("SignatureId", 123.456D),        // Valeur double
                    new SpreadsheetMetadataSignature("Amount", 123.456M),             // Valeur décimale
                    new SpreadsheetMetadataSignature("Total", 123.456F)               // Valeur flottante
                };
                
                // Ajouter une collection de signatures aux options
                options.Signatures.AddRange(signatures);
                
                // Signer le document et l'enregistrer dans un fichier
                SignResult result = signature.Sign(outputFilePath, options);
                
                // Afficher les résultats
                Console.WriteLine($"\nSource spreadsheet signed successfully with {result.Succeeded.Count} signature(s).");
                Console.WriteLine($"File saved at {outputFilePath}.");
            }
        }
    }
}
```

## Techniques avancées de métadonnées de feuille de calcul

### Travailler avec des propriétés de feuille de calcul personnalisées et intégrées

Les feuilles de calcul Excel disposent de propriétés intégrées et personnalisées, accessibles via la boîte de dialogue des propriétés du fichier. GroupDocs.Signature vous permet de travailler avec :

```csharp
// Ajouter des propriétés intégrées
signatures = new SpreadsheetMetadataSignature[]
{
    new SpreadsheetMetadataSignature("Company", "Sherlock Holmes Consulting"),
    new SpreadsheetMetadataSignature("Category", "Financial"),
    new SpreadsheetMetadataSignature("Keywords", "budget,forecast,analysis"),
    new SpreadsheetMetadataSignature("Comments", "This spreadsheet contains confidential information"),
    new SpreadsheetMetadataSignature("Manager", "John Watson")
};
options.Signatures.AddRange(signatures);

// Ajouter des propriétés personnalisées
options.Signatures.Add(new SpreadsheetMetadataSignature("Department", "Finance"));
options.Signatures.Add(new SpreadsheetMetadataSignature("SecurityLevel", "Confidential"));
```

### Recherche de métadonnées dans des feuilles de calcul signées

Après la signature, vous souhaiterez peut-être vérifier ou extraire les métadonnées :

```csharp
// Créer des options de recherche pour les métadonnées
MetadataSearchOptions searchOptions = new MetadataSearchOptions();

// Rechercher des signatures de métadonnées
SearchResult searchResult = signature.Search(searchOptions);

// Afficher les signatures trouvées
Console.WriteLine($"Found {searchResult.Signatures.Count} metadata signatures:");
foreach (var foundSignature in searchResult.Signatures)
{
    MetadataSignature metadataSignature = foundSignature as MetadataSignature;
    if (metadataSignature != null)
    {
        Console.WriteLine($"- {metadataSignature.Name}: {metadataSignature.Value} ({metadataSignature.Value.GetType().Name})");
    }
}
```

### Mise à jour des métadonnées existantes

Vous pouvez mettre à jour les métadonnées existantes dans les feuilles de calcul en utilisant les mêmes noms de propriété :

```csharp
// Mettre à jour les métadonnées existantes
options.Signatures.Add(new SpreadsheetMetadataSignature("Author", "Updated Author Name"));
```

## Conclusion

Dans ce tutoriel complet, vous avez appris à signer des feuilles de calcul Excel avec des métadonnées à l'aide de GroupDocs.Signature pour .NET. L'intégration de métadonnées dans les feuilles de calcul améliore la traçabilité des documents, fournit un contexte précieux et contribue à établir l'authenticité.

Les signatures de métadonnées dans les feuilles de calcul sont particulièrement utiles dans les environnements professionnels où l'origine, la paternité et le suivi des versions des documents sont importants. Les métadonnées intégrées peuvent inclure des informations sur l'auteur, la date de création, les identifiants des documents et des propriétés personnalisées adaptées aux besoins de votre organisation.

En implémentant des signatures de métadonnées avec GroupDocs.Signature, vous pouvez garantir que vos feuilles de calcul Excel conservent leur intégrité et fournissent des informations vérifiables tout au long de leur cycle de vie.

## FAQ

### Puis-je ajouter des métadonnées à des feuilles de calcul dont certaines propriétés sont déjà définies ?

Oui, vous pouvez ajouter de nouvelles métadonnées ou mettre à jour celles existantes dans les feuilles de calcul. GroupDocs.Signature se charge de l'intégration, soit en ajoutant de nouvelles propriétés, soit en mettant à jour celles existantes portant les mêmes noms.

### Quels formats de feuille de calcul sont pris en charge pour la signature des métadonnées ?

GroupDocs.Signature pour .NET prend en charge la signature des métadonnées pour divers formats de feuilles de calcul, notamment XLSX, XLS, XLSM, ODS, etc. Pour une liste complète, consultez la [documentation officielle](https://docs.groupdocs.com/signature/net/).

### Les signatures de métadonnées dans les feuilles de calcul sont-elles visibles par les utilisateurs ?

Les signatures de métadonnées ne sont pas visibles dans le contenu de la feuille de calcul. Cependant, elles peuvent être consultées via le panneau des propriétés du document dans Excel ou d'autres applications compatibles.

### Puis-je valider par programmation si une feuille de calcul a été falsifiée après avoir ajouté des métadonnées ?

Oui, GroupDocs.Signature fournit des fonctionnalités de vérification qui peuvent aider à détecter si un document a été modifié après la signature, y compris les modifications apportées aux métadonnées.

### L’ajout de métadonnées affecte-t-il la fonctionnalité de la feuille de calcul ?

L'ajout de métadonnées a un impact minimal sur la taille du fichier et n'a aucune incidence sur les fonctionnalités du tableur. C'est une méthode simple pour améliorer les propriétés d'un document sans affecter les calculs, les formules ou les autres fonctionnalités d'Excel.

### Où puis-je trouver plus de ressources et de soutien ?

- [Référence de l'API](https://reference.groupdocs.com/signature/net/)
- [Téléchargements](https://releases.groupdocs.com/signature/net/)
- [Exemples](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
- [Documentation](https://docs.groupdocs.com/signature/net/)
- [Page produit](https://products.groupdocs.com/signature/net/)
- [Blog](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
- [Forum d'assistance](https://forum.groupdocs.com/c/signature/13)
- [Licence temporaire](https://purchase.groupdocs.com/temporary-license/)