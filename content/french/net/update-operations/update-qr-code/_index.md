---
"description": "Découvrez comment mettre à jour dynamiquement les signatures de codes QR dans différents formats de documents avec GroupDocs.Signature pour .NET. Guide complet du développeur pour les solutions modernes de gestion de documents."
"linktitle": "Mettre à jour le code QR"
"second_title": "API .NET GroupDocs.Signature"
"title": "Mettre à jour les signatures de code QR dans les documents"
"url": "/fr/net/update-operations/update-qr-code/"
"weight": 12
type: docs
---
## Introduction
Dans un environnement commercial axé sur le numérique, les codes QR sont devenus un élément essentiel des systèmes de gestion documentaire et d'authentification. Ils offrent un moyen pratique d'encoder et d'accéder à des informations, des simples URL aux données structurées complexes. GroupDocs.Signature pour .NET offre une boîte à outils complète permettant aux développeurs d'intégrer des fonctionnalités avancées de signature électronique à leurs applications, notamment la possibilité de mettre à jour les signatures de codes QR existantes dans les documents.

Ce tutoriel se concentre spécifiquement sur la mise à jour des signatures de codes QR dans les documents avec GroupDocs.Signature pour .NET. Que vous ayez besoin de modifier la position, la taille ou les données codées de codes QR existants, ce guide vous guidera pas à pas à travers des exemples de code clairs et des explications.

## Prérequis
Avant de vous lancer dans les mises à jour de signature de code QR avec GroupDocs.Signature pour .NET, assurez-vous de disposer des conditions préalables suivantes :

1. Environnement de développement : un environnement de développement .NET fonctionnel, tel que Visual Studio 2017 ou version ultérieure.
2. Bibliothèque GroupDocs.Signature : téléchargez et installez la bibliothèque GroupDocs.Signature pour .NET à partir du [page de téléchargement](https://releases.groupdocs.com/signature/net/).
3. Licence (facultatif) : Pour une utilisation en production, vous aurez besoin d'une licence valide. À des fins de test, vous pouvez utiliser une licence. [permis temporaire](https://purchase.groupdocs.com/temporary-license/).
4. Exemple de document : un document contenant des signatures de code QR que vous souhaitez mettre à jour.
5. Connaissances de base en C# : Familiarité avec les concepts de programmation C#.

## Importer des espaces de noms
Commencez par importer les espaces de noms nécessaires pour accéder à la fonctionnalité GroupDocs.Signature :

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

Décomposons le processus de mise à jour des signatures de codes QR en étapes claires et gérables :

## Étape 1 : Configurer les chemins d’accès aux documents
Tout d’abord, définissez les chemins d’accès à votre document source et l’endroit où le document mis à jour sera enregistré :

```csharp
// Chemin vers le document source avec signatures de code QR
string filePath = "sample_multiple_signatures.docx";

// Obtenir le nom du fichier de sortie
string fileName = Path.GetFileName(filePath);

// Définir le répertoire de sortie et le chemin du fichier
string outputDirectory = Path.Combine("Your Document Directory", "UpdateQRCode");
string outputFilePath = Path.Combine(outputDirectory, fileName);

// Assurez-vous que le répertoire de sortie existe
Directory.CreateDirectory(outputDirectory);
```

## Étape 2 : Copier le document source
Étant donné que l'opération de mise à jour modifie directement le document, créez une copie du document original pour le conserver :

```csharp
// Créer une copie du document original
File.Copy(filePath, outputFilePath, true);
```

## Étape 3 : Initialiser l’instance de signature
Créer une instance de `Signature` classe pour travailler avec le document :

```csharp
// Initialiser l'instance Signature avec le chemin du fichier de sortie
using (Signature signature = new Signature(outputFilePath))
{
    // Les opérations de signature seront effectuées ici
}
```

## Étape 4 : Configurer les options de recherche par code QR
Configurez les options de recherche pour trouver les signatures de code QR existantes dans le document :

```csharp
// Configurer les options de recherche pour les signatures de code QR
QrCodeSearchOptions options = new QrCodeSearchOptions();

// Vous pouvez personnaliser les options de recherche si nécessaire
// options.AllPages = true; // Rechercher sur toutes les pages
// options.PageNumber = 1; // Rechercher sur une page spécifique
// options.EncodeType = QrCodeTypes.QR; // Rechercher un type de code QR spécifique
```

## Étape 5 : Rechercher des signatures de codes QR
Utilisez les options de recherche configurées pour trouver les signatures de code QR dans le document :

```csharp
// Rechercher des signatures de codes QR
List<QrCodeSignature> signatures = signature.Search<QrCodeSignature>(options);
```

## Étape 6 : Mettre à jour les propriétés de la signature du code QR
Si des signatures de code QR sont trouvées, mettez à jour leurs propriétés si nécessaire :

```csharp
// Vérifiez si des signatures ont été trouvées
if (signatures.Count > 0)
{
    // Obtenez la première signature de code QR
    QrCodeSignature qrCodeSignature = signatures[0];
    
    // Mettre à jour la position
    qrCodeSignature.Left = 200;
    qrCodeSignature.Top = 250;
    
    // Mettre à jour la taille
    qrCodeSignature.Width = 200;
    qrCodeSignature.Height = 200;
    
    // Vous pouvez également mettre à jour les données du code QR si nécessaire
    // qrCodeSignature.Text = "Données du code QR mises à jour";
    
    // Appliquer les mises à jour
    bool result = signature.Update(qrCodeSignature);
    
    // Vérifiez le résultat
    if (result)
    {
        Console.WriteLine($"QR Code signature was successfully updated in the document '{fileName}'.");
        Console.WriteLine($"New position: {qrCodeSignature.Left}x{qrCodeSignature.Top}");
        Console.WriteLine($"New size: {qrCodeSignature.Width}x{qrCodeSignature.Height}");
    }
    else
    {
        Console.WriteLine($"Failed to update QR Code signature in the document!");
    }
}
else
{
    Console.WriteLine("No QR Code signatures found in the document.");
}
```

## Exemple complet
Voici un exemple complet et fonctionnel qui montre comment mettre à jour une signature de code QR dans un document :

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;

namespace UpdateQRCodeSignatureExample
{
    class Program
    {
        static void Main(string[] args)
        {
            // Chemin du document
            string filePath = "sample_multiple_signatures.docx";
            
            // Définir le chemin de sortie
            string fileName = Path.GetFileName(filePath);
            string outputDirectory = Path.Combine(Environment.CurrentDirectory, "UpdateQRCode");
            string outputFilePath = Path.Combine(outputDirectory, fileName);
            
            // Assurez-vous que le répertoire de sortie existe
            Directory.CreateDirectory(outputDirectory);
            
            // Créer une copie du document original
            File.Copy(filePath, outputFilePath, true);
            
            // Initialiser l'instance de signature
            using (Signature signature = new Signature(outputFilePath))
            {
                // Configurer les options de recherche
                QrCodeSearchOptions options = new QrCodeSearchOptions();
                
                // Rechercher des signatures de codes QR
                List<QrCodeSignature> signatures = signature.Search<QrCodeSignature>(options);
                
                // Vérifiez si des signatures ont été trouvées
                if (signatures.Count > 0)
                {
                    // Obtenez la première signature
                    QrCodeSignature qrCodeSignature = signatures[0];
                    
                    // Mettre à jour la position et la taille
                    qrCodeSignature.Left = 200;
                    qrCodeSignature.Top = 250;
                    qrCodeSignature.Width = 200;
                    qrCodeSignature.Height = 200;
                    
                    // Appliquer les mises à jour
                    bool result = signature.Update(qrCodeSignature);
                    
                    // Vérifier le résultat
                    if (result)
                    {
                        Console.WriteLine($"QR Code signature was successfully updated in document '{fileName}'.");
                        Console.WriteLine($"New position: {qrCodeSignature.Left}x{qrCodeSignature.Top}");
                        Console.WriteLine($"New size: {qrCodeSignature.Width}x{qrCodeSignature.Height}");
                        Console.WriteLine($"Output file path: {outputFilePath}");
                    }
                    else
                    {
                        Console.WriteLine("Failed to update QR Code signature!");
                    }
                }
                else
                {
                    Console.WriteLine("No QR Code signatures found in the document.");
                }
            }
            
            Console.WriteLine("\nPress any key to exit...");
            Console.ReadKey();
        }
    }
}
```

## Personnalisation avancée de la signature du code QR
GroupDocs.Signature fournit des options supplémentaires pour personnaliser les signatures de code QR au-delà de la position et de la taille de base :

### Mise à jour des données codées
Vous pouvez mettre à jour les données réelles encodées dans le code QR :

```csharp
// Mettre à jour les données codées
qrCodeSignature.Text = "https://www.updated-website.com";
```

### Réglage des propriétés d'apparence
Personnaliser les aspects visuels du code QR :

```csharp
// Définir la couleur de premier plan (couleur du code QR)
qrCodeSignature.ForeColor = System.Drawing.Color.Blue;

// Définir la couleur d'arrière-plan
qrCodeSignature.BackgroundColor = System.Drawing.Color.LightYellow;

// Ajuster la transparence
qrCodeSignature.Opacity = 0.8;
```

### Ajout de bordures
Améliorez le code QR avec des bordures personnalisées :

```csharp
qrCodeSignature.Border.Color = System.Drawing.Color.Red;
qrCodeSignature.Border.DashStyle = System.Drawing.Drawing2D.DashStyle.Dash;
qrCodeSignature.Border.Weight = 2;
qrCodeSignature.Border.Visible = true;
```

### Rotation du code QR
Faites pivoter la signature du code QR selon un angle spécifique :

```csharp
qrCodeSignature.Angle = 30; // Rotation de 30 degrés
```

## Travailler avec différents formats de documents
GroupDocs.Signature prend en charge la mise à jour des signatures de code QR dans divers formats de documents :

- Documents PDF
- Documents Microsoft Word (DOC, DOCX)
- Feuilles de calcul Microsoft Excel (XLS, XLSX)
- Présentations Microsoft PowerPoint (PPT, PPTX)
- Formats OpenDocument
- Formats d'image

Le même code peut être utilisé dans ces formats avec des ajustements minimes.

## Conclusion
GroupDocs.Signature pour .NET offre une solution puissante et flexible pour mettre à jour les signatures de codes QR dans les documents. En suivant les étapes décrites dans ce tutoriel, les développeurs peuvent implémenter efficacement la fonctionnalité de mise à jour des signatures de codes QR dans leurs applications .NET, améliorant ainsi la gestion des documents et les capacités d'authentification.

Grâce à son ensemble complet de fonctionnalités et à son API intuitive, GroupDocs.Signature permet aux développeurs de créer des solutions de signature de documents sophistiquées qui répondent aux exigences des applications commerciales modernes tout en garantissant l'intégrité et l'accessibilité des documents.

## FAQ
### Puis-je mettre à jour plusieurs signatures de code QR dans un seul document ?
Oui, GroupDocs.Signature vous permet de mettre à jour plusieurs signatures de code QR au sein d'un même document. Après avoir recherché des signatures, vous pouvez parcourir la liste obtenue et mettre à jour chaque signature de code QR individuellement.

### GroupDocs.Signature prend-il en charge différents types de codes QR ?
Oui, GroupDocs.Signature prend en charge différents types de codes QR, notamment les codes QR standard, les micro-QR et autres. Vous pouvez spécifier le type de code QR à l'aide du bouton `EncodeType` propriété.

### Existe-t-il une version d'essai disponible pour GroupDocs.Signature pour .NET ?
Oui, vous pouvez télécharger une version d'essai gratuite à partir du [Site Web GroupDocs](https://releases.groupdocs.com/signature/net/) pour évaluer les fonctionnalités de la bibliothèque avant de procéder à un achat.

### Puis-je modifier par programmation le niveau de correction d'erreur du code QR ?
Oui, vous pouvez modifier le niveau de correction d'erreur lors de l'ajout de nouveaux codes QR, mais la mise à jour de cette propriété pour les codes QR existants peut ne pas être prise en charge dans tous les formats de document.

### Où puis-je trouver une assistance supplémentaire pour GroupDocs.Signature pour .NET ?
Vous pouvez trouver un soutien complet grâce aux ressources suivantes :
- [Documentation de l'API](https://docs.groupdocs.com/signature/net/)
- [Référence de l'API](https://reference.groupdocs.com/signature/net/)
- [Exemples GitHub](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
- [Forum d'assistance](https://forum.groupdocs.com/c/signature/13)
- [Blog](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)