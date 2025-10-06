---
"description": "Découvrez comment signer et intégrer des métadonnées dans des images avec GroupDocs.Signature pour .NET. Ajoutez des informations sur l'auteur, des horodatages et des données personnalisées pour améliorer l'authenticité et la traçabilité des images."
"linktitle": "Image de signe avec métadonnées"
"second_title": "API .NET GroupDocs.Signature"
"title": "Signer des images avec des métadonnées en C# .NET"
"url": "/fr/net/document-signing/sign-image-with-metadata/"
"weight": 10
type: docs
---
## Introduction

La signature d'images numériques avec métadonnées devient de plus en plus importante pour établir l'authenticité, la propriété et la traçabilité. GroupDocs.Signature pour .NET offre une solution puissante et simple d'utilisation pour ajouter des signatures de métadonnées à différents formats d'images. Ce tutoriel vous guide tout au long du processus de signature d'images avec métadonnées en C#.

Les signatures de métadonnées vous permettent d'intégrer des informations précieuses directement dans les fichiers image, telles que les informations sur l'auteur, l'horodatage de création, les identifiants uniques, etc. Ces informations sont intégrées au fichier image lui-même, offrant ainsi une méthode fiable pour suivre et vérifier l'authenticité de l'image.

## Prérequis

Avant de poursuivre ce tutoriel, assurez-vous de disposer des éléments suivants :

1. [GroupDocs.Signature pour .NET](https://releases.groupdocs.com/signature/net/) - Téléchargez et installez la bibliothèque
2. Environnement de développement - Visual Studio ou tout autre IDE compatible avec prise en charge .NET
3. Fichier image - Un exemple de fichier image dans un format pris en charge (PNG, JPG, TIFF, etc.)
4. Connaissances de base en programmation C# - Familiarité avec les concepts de programmation C#

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

Définissez les chemins d’accès à votre image source et l’endroit où la sortie signée doit être enregistrée :

```csharp
// Spécifiez le chemin d'accès à votre fichier image source
string filePath = "sample.png";

// Définir le répertoire de sortie et le nom de fichier de l'image signée
string outputDirectory = "Your Document Directory";
string outputFilePath = Path.Combine(outputDirectory, "SignImageWithMetadata", "SignedWithMetadata.png");

// Assurez-vous que le répertoire de sortie existe
Directory.CreateDirectory(Path.GetDirectoryName(outputFilePath));
```

## Étape 2 : Initialiser l’objet Signature

Créez une instance de la classe Signature avec votre fichier image source :

```csharp
using (Signature signature = new Signature(filePath))
{
    // Le reste du code ira ici
}
```

## Étape 3 : Créer et configurer les signatures de métadonnées

Ensuite, définissez les métadonnées à intégrer à l'image. GroupDocs.Signature prend en charge différents types de métadonnées :

```csharp
// Initialiser l'ID de métadonnées (spécifique au format d'image)
ushort imgsMetadataId = 41996;

// Créer un objet d'options de métadonnées
MetadataSignOptions options = new MetadataSignOptions();

// Ajouter différents types de signatures de métadonnées
options
    .Add(new ImageMetadataSignature(imgsMetadataId++, "Mr.Sherlock Holmes"))  // Valeur de chaîne
    .Add(new ImageMetadataSignature(imgsMetadataId++, DateTime.Now))          // Valeur de date et d'heure
    .Add(new ImageMetadataSignature(imgsMetadataId++, 123456))                // Valeur entière
    .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456D))              // Valeur double
    .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456M))              // Valeur décimale
    .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456F));             // Valeur flottante
```

## Étape 4 : Signer l'image avec des métadonnées

Appliquez les signatures de métadonnées à l’image et enregistrez le résultat :

```csharp
// Signez le document et enregistrez-le dans le chemin du fichier de sortie
SignResult result = signature.Sign(outputFilePath, options);

// Afficher un message de réussite
Console.WriteLine($"\nSource image signed successfully with {result.Succeeded.Count} metadata signature(s).");
Console.WriteLine($"Signed image saved at: {outputFilePath}");
```

## Exemple complet

Voici l'exemple de code complet qui rassemble toutes les étapes :

```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;

namespace SignImageWithMetadataExample
{
    class Program
    {
        static void Main(string[] args)
        {
            // Spécifier les chemins de fichiers
            string filePath = "sample.png";            
            string outputFilePath = Path.Combine("Your Document Directory", "SignImageWithMetadata", "SignedWithMetadata.png");
            
            // Assurez-vous que le répertoire de sortie existe
            Directory.CreateDirectory(Path.GetDirectoryName(outputFilePath));

            // Signer l'image avec des métadonnées
            using (Signature signature = new Signature(filePath))
            {
                // Initialiser l'ID de métadonnées (spécifique au format d'image)
                ushort imgsMetadataId = 41996;
                
                // Créer des options de métadonnées
                MetadataSignOptions options = new MetadataSignOptions();
                
                // Ajouter différents types de signatures de métadonnées
                options
                    .Add(new ImageMetadataSignature(imgsMetadataId++, "Mr.Sherlock Holmes")) // Valeur de chaîne
                    .Add(new ImageMetadataSignature(imgsMetadataId++, DateTime.Now))          // Valeur de date et d'heure
                    .Add(new ImageMetadataSignature(imgsMetadataId++, 123456))                // Valeur entière
                    .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456D))              // Valeur double
                    .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456M))              // Valeur décimale
                    .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456F));             // Valeur flottante
                
                // Signer le document et l'enregistrer dans un fichier
                SignResult result = signature.Sign(outputFilePath, options);
                
                // Afficher les résultats
                Console.WriteLine($"\nSource image signed successfully with {result.Succeeded.Count} signature(s).");
                Console.WriteLine($"File saved at {outputFilePath}.");
            }
        }
    }
}
```

## Techniques avancées de signature de métadonnées

### Travailler avec des métadonnées personnalisées

Vous pouvez également créer des champs de métadonnées personnalisés avec des ID spécifiques :

```csharp
// Créer des métadonnées personnalisées avec un ID spécifique
options.Add(new ImageMetadataSignature(42000, "CustomValue"));
```

### Vérification des signatures de métadonnées

Après la signature, vous souhaiterez peut-être vérifier les signatures des métadonnées :

```csharp
// Créer des options de vérification
MetadataSearchOptions searchOptions = new MetadataSearchOptions();

// Rechercher des signatures de métadonnées
SearchResult result = signature.Search(searchOptions);

// Afficher les signatures trouvées
Console.WriteLine($"Found {result.Signatures.Count} metadata signatures:");
foreach(var metadataSignature in result.Signatures)
{
    Console.WriteLine($"- {metadataSignature.Name}: {metadataSignature.Value}");
}
```

## Conclusion

Dans ce tutoriel, vous avez appris à signer des images avec des métadonnées grâce à GroupDocs.Signature pour .NET. L'intégration de métadonnées aux images est un excellent moyen d'améliorer l'authenticité des images, d'ajouter des informations essentielles et d'optimiser les flux de gestion des documents. Ce processus, simple et performant, permet une personnalisation en fonction de vos besoins spécifiques.

Les métadonnées intégrées au fichier image peuvent être utilisées à diverses fins, telles que la protection des droits d'auteur, le suivi de l'origine de l'image, l'ajout d'informations descriptives et l'établissement d'une chaîne de traçabilité numérique. En implémentant des signatures de métadonnées, vous garantissez l'intégrité et l'authenticité de vos images tout au long de leur cycle de vie.

## FAQ

### Puis-je ajouter des métadonnées à des images signées existantes ?

Oui, vous pouvez ajouter des métadonnées supplémentaires aux images contenant déjà des signatures de métadonnées. Les métadonnées existantes seront conservées et de nouvelles métadonnées seront ajoutées en conséquence.

### Quels formats d’image sont pris en charge pour la signature des métadonnées ?

GroupDocs.Signature pour .NET prend en charge la signature des métadonnées pour divers formats d'image, notamment PNG, JPEG, TIFF, BMP, GIF, etc. Pour une liste complète, consultez la [documentation officielle](https://docs.groupdocs.com/signature/net/).

### Est-il possible de crypter les métadonnées des images ?

Oui, GroupDocs.Signature propose des options de chiffrement des métadonnées pour une sécurité renforcée. Vous pouvez utiliser les options de chiffrement fournies par la bibliothèque pour protéger les métadonnées sensibles.

### Puis-je valider par programmation l’authenticité des images signées ?

Absolument. Vous pouvez utiliser les méthodes de vérification de GroupDocs.Signature pour valider les signatures de métadonnées et confirmer l'authenticité des images signées.

### Existe-t-il une limitation de taille de fichier lors de la signature d'images avec des métadonnées ?

La bibliothèque elle-même n'impose aucune limite de taille de fichier spécifique, mais les fichiers très volumineux peuvent nécessiter davantage de temps de traitement et de mémoire. Il est recommandé de prendre en compte les ressources système lorsque vous travaillez avec des images extrêmement volumineuses.

### Comment puis-je obtenir une licence temporaire à des fins de test ?

Vous pouvez obtenir un [permis temporaire](https://purchase.groupdocs.com/temporary-license/) pour tester GroupDocs.Signature avant de faire un achat.

### Où puis-je trouver plus de ressources et de soutien ?

- [Référence de l'API](https://reference.groupdocs.com/signature/net/)
- [Téléchargements](https://releases.groupdocs.com/signature/net/)
- [Exemples](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
- [Documentation](https://docs.groupdocs.com/signature/net/)
- [Page produit](https://products.groupdocs.com/signature/net/)
- [Blog](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
- [Forum d'assistance](https://forum.groupdocs.com/c/signature/13)