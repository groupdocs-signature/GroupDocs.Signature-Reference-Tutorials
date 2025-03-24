---
title: Firma l'immagine con i metadati
linktitle: Firma l'immagine con i metadati
second_title: API GroupDocs.Signature .NET
description: Scopri come firmare immagini con metadati in .NET utilizzando GroupDocs.Signature. Soluzione di firma dei metadati semplice, efficiente e personalizzabile.
weight: 10
url: /it/net/document-signing/sign-image-with-metadata/
---
## introduzione
GroupDocs.Signature per .NET consente agli sviluppatori di firmare immagini con metadati in modo efficiente. Questo tutorial ti guida attraverso il processo passo dopo passo.
## Prerequisiti
Prima di iniziare, assicurati di avere quanto segue:
1. GroupDocs.Signature per .NET: installa il pacchetto GroupDocs.Signature nel tuo progetto .NET. Puoi scaricarlo da[Qui](https://releases.groupdocs.com/signature/net/).   
2. File immagine: prepara il file immagine che desideri firmare con i metadati.

## Importa spazi dei nomi
Assicurati di importare gli spazi dei nomi necessari nel codice C#:
```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## Passaggio 1: caricare il file immagine
Innanzitutto, specifica il percorso del file immagine e la directory di output per l'immagine firmata con metadati:
```csharp
string filePath = "sample.png";            
string outputFilePath = Path.Combine("Your Document Directory", "SignImageWithMetadata", "SignedWithMetadata.png");
```
## Passaggio 2: crea firme di metadati
Successivamente, crea diverse firme di metadati e aggiungile alla raccolta di firme delle opzioni:
```csharp
using (Signature signature = new Signature(filePath))
{
    ushort imgsMetadataId = 41996;
    MetadataSignOptions options = new MetadataSignOptions();
    options
        .Add(new ImageMetadataSignature(imgsMetadataId++, "Mr.Scherlock Holmes")) // Valore stringa
        .Add(new ImageMetadataSignature(imgsMetadataId++, DateTime.Now))          // Valore data/ora
        .Add(new ImageMetadataSignature(imgsMetadataId++, 123456))                // Valore intero
        .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456D))              // Doppio valore
        .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456M))              // Valore decimale
        .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456F));             // Valore flottante
    
    // firmare il documento da archiviare
    SignResult result = signature.Sign(outputFilePath, options);
    Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).\nFile saved at {outputFilePath}.");
}
```

## Conclusione
In questo tutorial hai imparato come firmare un'immagine con metadati utilizzando GroupDocs.Signature per .NET. Seguendo questi passaggi è possibile incorporare facilmente le firme dei metadati nelle applicazioni .NET.

## Domande frequenti
### Posso firmare più immagini con metadati utilizzando GroupDocs.Signature per .NET?
Sì, puoi firmare più immagini con metadati scorrendo ogni file immagine e applicando le firme dei metadati.
### È disponibile una versione di prova per GroupDocs.Signature per .NET?
 Sì, puoi scaricare la versione di prova da[Qui](https://releases.groupdocs.com/).
### GroupDocs.Signature per .NET supporta altri formati di file oltre alle immagini?
Sì, GroupDocs.Signature supporta vari formati di file, tra cui PDF, Word, Excel e altri.
### Posso personalizzare l'aspetto della firma dei metadati?
Sì, puoi personalizzare l'aspetto della firma dei metadati, come dimensione, colore e posizione del carattere.
### Dove posso ottenere supporto per GroupDocs.Signature per .NET?
 Puoi ottenere supporto dal forum GroupDocs.Signature[Qui](https://forum.groupdocs.com/c/signature/13).