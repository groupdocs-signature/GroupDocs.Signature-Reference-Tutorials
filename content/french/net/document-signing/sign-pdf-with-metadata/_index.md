---
"description": "Intégrez des signatures de métadonnées à vos documents PDF grâce à GroupDocs.Signature pour .NET. Apprenez à intégrer des informations sur l'auteur, des horodatages et des données personnalisées pour améliorer l'authenticité et la traçabilité des PDF."
"linktitle": "Signer un PDF avec des métadonnées"
"second_title": "API .NET GroupDocs.Signature"
"title": "Ajouter des signatures de métadonnées aux documents PDF en C# .NET"
"url": "/fr/net/document-signing/sign-pdf-with-metadata/"
"weight": 11
type: docs
---
## Introduction

Les documents PDF (Portable Document Format) sont largement utilisés dans tous les secteurs d'activité en raison de leur cohérence et de leur indépendance vis-à-vis des plateformes. Garantir l'authenticité et la traçabilité de ces documents est crucial dans de nombreux environnements professionnels. Un moyen efficace d'y parvenir est d'intégrer des métadonnées directement dans les fichiers PDF.

Dans ce tutoriel complet, nous découvrirons comment signer des documents PDF avec des métadonnées grâce à GroupDocs.Signature pour .NET. Les signatures de métadonnées vous permettent d'intégrer des informations supplémentaires au document, telles que les coordonnées de l'auteur, l'horodatage de création, les identifiants de document et les valeurs personnalisées, sans altérer visiblement l'apparence du document.

## Prérequis

Avant de commencer, assurez-vous d’avoir les éléments suivants en place :

1. [GroupDocs.Signature pour .NET](https://releases.groupdocs.com/signature/net/) - Téléchargez et installez la bibliothèque
2. Environnement de développement - Visual Studio ou tout autre IDE compatible .NET
3. Document PDF - Un exemple de fichier PDF à signer
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

Tout d’abord, définissez le chemin d’accès à votre document PDF et indiquez où vous souhaitez enregistrer la sortie signée :

```csharp
// Spécifiez le chemin d'accès à votre document PDF
string filePath = "sample.pdf";

// Définir le répertoire de sortie et le chemin du fichier
string outputDirectory = "Your Document Directory";
string outputFilePath = Path.Combine(outputDirectory, "SignPdfWithMetadata", "SignedWithMetadata.pdf");

// Assurez-vous que le répertoire de sortie existe
Directory.CreateDirectory(Path.GetDirectoryName(outputFilePath));
```

## Étape 2 : Initialiser l’objet Signature

Créez une instance de la classe Signature avec votre document PDF source :

```csharp
using (Signature signature = new Signature(filePath))
{
    // Le code de signature sera placé ici
}
```

## Étape 3 : Définir les options de métadonnées

Créez et configurez les options de métadonnées, en ajoutant différents types de signatures de métadonnées :

```csharp
// Créer un objet d'options de métadonnées
MetadataSignOptions options = new MetadataSignOptions();

// Ajoutez différents types de métadonnées à l'aide de l'interface fluide
options
    .Add(new PdfMetadataSignature("Author", "Mr.Sherlock Holmes")) // Valeur de chaîne
    .Add(new PdfMetadataSignature("CreatedOn", DateTime.Now))       // Valeur DateTime
    .Add(new PdfMetadataSignature("DocumentId", 123456))            // Valeur entière
    .Add(new PdfMetadataSignature("SignatureId", 123.456D))         // Valeur double
    .Add(new PdfMetadataSignature("Amount", 123.456M))              // Valeur décimale
    .Add(new PdfMetadataSignature("Total", 123.456F));              // Valeur flottante
```

## Étape 4 : Signer le PDF avec des métadonnées

Appliquez les signatures de métadonnées au document PDF et enregistrez le résultat :

```csharp
// Signez le document et enregistrez-le dans le chemin de sortie
SignResult result = signature.Sign(outputFilePath, options);

// Afficher un message de réussite
Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} metadata signature(s).");
Console.WriteLine($"Signed document saved at: {outputFilePath}");
```

## Exemple complet

Voici l'exemple de code complet qui rassemble toutes les étapes :

```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;

namespace SignPdfWithMetadataExample
{
    class Program
    {
        static void Main(string[] args)
        {
            // Spécifier les chemins de fichiers
            string filePath = "sample.pdf";
            string outputFilePath = Path.Combine("Your Document Directory", "SignPdfWithMetadata", "SignedWithMetadata.pdf");
            
            // Assurez-vous que le répertoire de sortie existe
            Directory.CreateDirectory(Path.GetDirectoryName(outputFilePath));

            // Signer le PDF avec des métadonnées
            using (Signature signature = new Signature(filePath))
            {
                // Créer un objet d'options de métadonnées
                MetadataSignOptions options = new MetadataSignOptions();
                
                // Ajouter différents types de signatures de métadonnées
                options
                    .Add(new PdfMetadataSignature("Author", "Mr.Sherlock Holmes")) // Valeur de chaîne
                    .Add(new PdfMetadataSignature("CreatedOn", DateTime.Now))       // Valeur DateTime
                    .Add(new PdfMetadataSignature("DocumentId", 123456))            // Valeur entière
                    .Add(new PdfMetadataSignature("SignatureId", 123.456D))         // Valeur double
                    .Add(new PdfMetadataSignature("Amount", 123.456M))              // Valeur décimale
                    .Add(new PdfMetadataSignature("Total", 123.456F));              // Valeur flottante
                
                // Signer le document et l'enregistrer dans un fichier
                SignResult result = signature.Sign(outputFilePath, options);
                
                // Afficher les résultats
                Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).");
                Console.WriteLine($"File saved at {outputFilePath}.");
            }
        }
    }
}
```

## Opérations avancées sur les métadonnées PDF

### Ajout de métadonnées personnalisées avec prise en charge des espaces de noms

Les documents PDF prennent en charge les métadonnées personnalisées avec la prise en charge de l'espace de noms XML :

```csharp
// Ajouter des métadonnées personnalisées avec un espace de noms
options.Add(new PdfMetadataSignature("CustomProperty", "Custom Value")
{
    NamespaceUri = "http://votre-espace-de-noms.com/schema"
});
```

### Recherche de métadonnées dans les PDF signés

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

### Travailler avec des métadonnées PDF standard

Les documents PDF ont des champs de métadonnées standard qui peuvent être consultés et modifiés :

```csharp
// Définir des champs de métadonnées PDF standard
options
    .Add(new PdfMetadataSignature("Title", "Important Contract"))
    .Add(new PdfMetadataSignature("Subject", "Legal Agreement"))
    .Add(new PdfMetadataSignature("Keywords", "contract, agreement, legal, binding"))
    .Add(new PdfMetadataSignature("Creator", "Legal Department"))
    .Add(new PdfMetadataSignature("Producer", "GroupDocs.Signature"));
```

## Conclusion

Dans ce tutoriel, vous avez appris à signer des documents PDF avec des métadonnées grâce à GroupDocs.Signature pour .NET. L'intégration de métadonnées dans les fichiers PDF constitue un excellent moyen d'améliorer l'authenticité des documents, d'ajouter des informations essentielles et d'optimiser les flux de travail de gestion documentaire.

Les signatures de métadonnées dans les PDF sont particulièrement utiles dans les environnements professionnels où la traçabilité et la vérification de l'authenticité des documents sont essentielles. Les métadonnées intégrées peuvent inclure des informations sur l'origine du document, son auteur, sa date de création, sa version et des propriétés personnalisées pertinentes pour le flux de travail de votre organisation.

En implémentant des signatures de métadonnées avec GroupDocs.Signature, vous pouvez garantir que vos documents PDF conservent leur intégrité et fournissent des informations vérifiables tout au long de leur cycle de vie.

## FAQ

### Puis-je modifier les métadonnées existantes dans un document PDF ?

Oui, vous pouvez modifier les métadonnées existantes dans les documents PDF. Lorsque vous appliquez de nouvelles signatures de métadonnées portant les mêmes noms que les signatures existantes, les valeurs sont mises à jour en conséquence.

### Les signatures de métadonnées dans les documents PDF sont-elles visibles par l’utilisateur final ?

Les signatures de métadonnées ne sont pas visibles dans le contenu du document lui-même. Cependant, elles peuvent être visualisées via le panneau des propriétés du document dans des lecteurs PDF comme Adobe Acrobat ou à l'aide d'outils spécialisés de visualisation des métadonnées.

### Puis-je crypter ou protéger les métadonnées des fichiers PDF ?

GroupDocs.Signature propose des options de sécurisation des documents, notamment le chiffrement. Vous pouvez appliquer un chiffrement au niveau du document pour protéger l'intégralité du PDF, y compris ses métadonnées.

### Existe-t-il une limite à la quantité de métadonnées que je peux ajouter à un PDF ?

Bien que la spécification PDF n'impose aucune limite stricte, l'ajout d'une quantité excessive de métadonnées peut augmenter la taille du fichier. Il est recommandé de n'inclure que les informations pertinentes et nécessaires dans les métadonnées.

### Puis-je valider par programmation si un PDF a été falsifié après avoir ajouté des métadonnées ?

Oui, GroupDocs.Signature fournit des fonctionnalités de vérification qui peuvent aider à détecter si un document a été modifié après la signature, y compris les modifications apportées aux métadonnées.

### Où puis-je trouver plus de ressources et de soutien ?

- [Référence de l'API](https://reference.groupdocs.com/signature/net/)
- [Téléchargements](https://releases.groupdocs.com/signature/net/)
- [Exemples](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
- [Documentation](https://docs.groupdocs.com/signature/net/)
- [Page produit](https://products.groupdocs.com/signature/net/)
- [Blog](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
- [Forum d'assistance](https://forum.groupdocs.com/c/signature/13)
- [Licence temporaire](https://purchase.groupdocs.com/temporary-license/)