---
"date": "2025-05-07"
"description": "Découvrez comment signer des images DICOM avec des codes QR grâce à GroupDocs.Signature pour .NET. Ce guide couvre la configuration, la mise en œuvre et la vérification des signatures de codes QR en imagerie médicale."
"title": "Comment signer des images DICOM avec des codes QR à l'aide de GroupDocs.Signature pour .NET ? Un guide complet"
"url": "/fr/net/qr-code-signatures/groupdocs-signature-net-dicom-images-qr-codes/"
"weight": 1
type: docs
---
# Comment signer des images DICOM avec des codes QR à l'aide de GroupDocs.Signature pour .NET : guide complet

Vous cherchez une méthode sécurisée pour authentifier vos fichiers DICOM ? Ce guide détaillé vous explique comment utiliser GroupDocs.Signature pour .NET afin d'intégrer des signatures de codes QR dans des images DICOM. Idéal pour les professionnels de santé, les développeurs et toute personne travaillant avec des documents médicaux numériques, ce tutoriel couvre l'installation et la mise en œuvre.

## Ce que vous apprendrez :
- Configuration de votre environnement de développement avec GroupDocs.Signature pour .NET.
- Instructions étape par étape sur la signature d'images DICOM à l'aide de codes QR.
- Méthodes pour vérifier et rechercher des signatures de codes QR dans les fichiers DICOM.
- Techniques permettant de générer des aperçus de documents signés à des fins de révision.
- Meilleures pratiques pour optimiser les performances et gérer efficacement les ressources.

Commençons par les prérequis !

## Prérequis

Pour utiliser GroupDocs.Signature pour .NET, assurez-vous que votre environnement est prêt. Voici ce dont vous aurez besoin :

### Bibliothèques et versions requises
- **GroupDocs.Signature pour .NET**:Assurez la compatibilité avec votre framework .NET.

### Configuration requise pour l'environnement
- Un environnement de développement sous Windows ou Linux.
- Visual Studio ou un autre IDE compatible .NET installé.

### Prérequis en matière de connaissances
- Compréhension de base de la programmation C#.
- Connaissance des E/S de fichiers dans les applications .NET.

## Configuration de GroupDocs.Signature pour .NET

Installez la bibliothèque GroupDocs.Signature en utilisant votre méthode préférée :

**Utilisation de .NET CLI :**
```bash
dotnet add package GroupDocs.Signature
```

**Gestionnaire de paquets :**
```powershell
Install-Package GroupDocs.Signature
```

**Interface utilisateur du gestionnaire de packages NuGet :**
- Recherchez « GroupDocs.Signature » et installez la dernière version.

### Acquisition de licence

Commencez par un essai gratuit pour explorer les fonctionnalités. Pour une utilisation prolongée, envisagez d'acquérir une licence temporaire ou complète auprès de [Documents de groupe](https://purchase.groupdocs.com/buy).

Une fois installée, initialisez la bibliothèque :

```csharp
using GroupDocs.Signature;
// Initialisez l'objet Signature avec le chemin de votre fichier DICOM.
Signature signature = new Signature("YOUR_DOCUMENT_DIRECTORY\\sample.dicom");
```

## Guide de mise en œuvre

### Signer une image DICOM avec un code QR

#### Aperçu
Ajoutez des signatures de code QR pour garantir l’authenticité et la traçabilité des documents médicaux.

**Étape 1 : Initialiser l'objet Signature**

```csharp
string filePath = "YOUR_DOCUMENT_DIRECTORY\\sample.dicom";
using (Signature signature = new Signature(filePath))
{
    // Procéder aux opérations de signature...
}
```

**Étape 2 : Créer des options de signature de code QR**

Configurez les propriétés telles que le texte, la taille et l’alignement.

```csharp
QrCodeSignOptions options = new QrCodeSignOptions("Patient #36363393. R: No-Issues")
{
    AllPages = true,
    Width = 100,
    Height = 100,
    VerticalAlignment = VerticalAlignment.Bottom,
    HorizontalAlignment = HorizontalAlignment.Right,
    Margin = new Padding() { Right = 5, Left = 5 }
};
```

**Étape 3 : ajouter des métadonnées XMP**

Améliorez le document avec des métadonnées supplémentaires.

```csharp
DicomSaveOptions dicomSaveOptions = new DicomSaveOptions()
{
    XmpEntries = new List<DicomXmpEntry>() { new DicomXmpEntry(DicomXmpType.PatientName, "Patient #4") }
};
```

**Étape 4 : Signer le document**

Exécutez la signature et enregistrez.

```csharp
SignResult signResult = signature.Sign("YOUR_OUTPUT_DIRECTORY\\SignedDicom", options, dicomSaveOptions);
```

### Obtenir des informations sur le document

Récupérez les métadonnées des fichiers DICOM signés pour garantir l’intégrité des données.

**Aperçu:**
Accédez aux informations du document et aux signatures de métadonnées XMP pour vérification.

**Étape 1 : Récupérer les informations du document**

```csharp
using (Signature signature = new Signature("YOUR_DOCUMENT_DIRECTORY\\sample_signed.dicom"))
{
    IDocumentInfo signedDocumentInfo = signature.GetDocumentInfo();
}
```

**Étape 2 : Itérer et imprimer les données XMP**

Afficher les détails des métadonnées.

```csharp
foreach (var item in signedDocumentInfo.MetadataSignatures)
{
    Console.WriteLine(item.ToString());
}
```

### Vérifier les signatures DICOM

Valider l'authenticité des signatures de codes QR dans les images DICOM.

**Aperçu:**
Assurez-vous que les signatures sont correctes et authentiques.

**Étape 1 : Créer un code QR Vérifier les options**

Définissez des options correspondant à un texte spécifique dans les codes QR.

```csharp
QrCodeVerifyOptions options = new QrCodeVerifyOptions()
{
    AllPages = true,
    Text = "Patient #36363393",
    MatchType = TextMatchType.Contains
};
```

**Étape 2 : Vérifier les signatures**

Vérifiez si les signatures répondent aux critères.

```csharp
VerificationResult result = signature.Verify(options);

if (result.IsValid)
{
    Console.WriteLine($"DICOM {filePath} has {result.Succeeded.Count} successfully verified signatures!");
}
```

### Rechercher des signatures dans DICOM

Localisez les signatures de code QR dans les images DICOM signées.

**Aperçu:**
Trouvez efficacement toutes les signatures de codes QR pour gérer l'authenticité des documents.

**Étape 1 : Rechercher des signatures de codes QR**

```csharp
List<QrCodeSignature> signatures = signature.Search<QrCodeSignature>(SignatureType.QrCode);
```

**Étape 2 : Itérer et imprimer les détails de la signature**

Passez en revue les détails de chaque signature trouvée.

```csharp
foreach (var QrCodeSignature in signatures)
{
    Console.WriteLine($"QRCode signature found at page {QrCodeSignature.PageNumber} with type {QrCodeSignature.EncodeType.TypeName} and text {QrCodeSignature.Text}");
}
```

### Générer un aperçu du DICOM signé

Créez des aperçus visuels pour vérification.

**Aperçu:**
Générez des aperçus d'images pour vérifier le contenu sans logiciel spécialisé.

**Étape 1 : Définir les méthodes de flux**

Configurer des méthodes de gestion des flux de fichiers lors de la génération d'aperçus.

```csharp
Stream CreatePageStream(PreviewPageData pageData)
{
    string imageFilePath = Path.Combine("YOUR_OUTPUT_DIRECTORY", "SignDicomImageAdvanced", $"preview-{pageData.PageNumber}.jpg");
    var folder = Path.GetDirectoryName(imageFilePath);
    if (!Directory.Exists(folder))
    {
        Directory.CreateDirectory(folder);
    }
    return new FileStream(imageFilePath, FileMode.Create);
}

void ReleasePageStream(PreviewPageData pageData, Stream pageStream)
{
    pageStream.Dispose();
}
```

**Étape 2 : Générer des aperçus**

Exécutez le processus de génération d’aperçu.

```csharp
using (Signature signature = new Signature("YOUR_DOCUMENT_DIRECTORY\\sample_signed.dicom"))
{
    PreviewOptions previewOption = new PreviewOptions(CreatePageStream, ReleasePageStream)
    {
        PreviewFormat = PreviewOptions.PreviewFormats.PNG,
    };

    signature.GeneratePreview(previewOption);
}
```

## Applications pratiques

1. **Gestion des dossiers médicaux**:Authentifiez les dossiers des patients à l'aide de signatures de code QR pour la conformité.
2. **Pistes d'audit dans les systèmes de santé**:Suivez les modifications des documents et vérifiez leur authenticité avec des codes QR.
3. **Partage sécurisé des données**:Assurez le partage sécurisé des images médicales en intégrant des signatures numériques.
4. **Vérification de la conformité**:Vérifiez régulièrement l’intégrité du fichier DICOM pour répondre aux exigences légales.
5. **Intégration avec les systèmes DSE**:Intégrez de manière transparente les fichiers DICOM signés dans les systèmes de dossiers de santé électroniques (DSE) pour des opérations rationalisées.