---
title: Firma la presentazione con metadati
linktitle: Firma la presentazione con metadati
second_title: API GroupDocs.Signature .NET
description: Scopri come firmare file di presentazione con metadati utilizzando GroupDocs.Signature per .NET. Migliora l'integrità del documento e aggiungi informazioni preziose.
type: docs
weight: 12
url: /it/net/document-signing/sign-presentation-with-metadata/
---
## introduzione
In questo tutorial impareremo come firmare un file di presentazione (PPTX) con metadati utilizzando la libreria GroupDocs.Signature per .NET. Firmare le presentazioni con metadati aggiunge informazioni preziose al documento, come il nome dell'autore, la data di creazione, l'ID del documento, l'ID della firma e vari valori numerici.
## Prerequisiti
Prima di iniziare, assicurati di avere quanto segue:
1.  GroupDocs.Signature per .NET Library: scarica e installa la libreria da[Qui](https://releases.groupdocs.com/signature/net/).
2. Ambiente di sviluppo: assicurati di avere un ambiente di sviluppo .NET configurato.
3. File di presentazione: tenere pronto un file di presentazione di esempio (formato PPTX) per la firma.
4. Comprensione di base di C#: la familiarità con il linguaggio di programmazione C# sarà utile.

## Importa spazi dei nomi
Prima di immergerci nel codice, importiamo gli spazi dei nomi necessari:
```csharp
using System;
using System.IO;
    using GroupDocs.Signature;
    using GroupDocs.Signature.Domain;
    using GroupDocs.Signature.Options;
```
## Passaggio 1: caricare il file di presentazione
```csharp
string filePath = "sample.pptx";
```
 Sostituire`"sample.pptx"` con il percorso del file di presentazione.
## Passaggio 2: specificare il percorso del file di output
```csharp
string outputFilePath = Path.Combine("Your Document Directory", "SignPresentationWithMetadata", "SignedWithMetadata.pptx");
```
Specifica la directory in cui desideri salvare il file di presentazione firmato insieme al nome del file.
## Passaggio 3: inizializzare l'oggetto firma
```csharp
using (Signature signature = new Signature(filePath))
```
Inizializza un oggetto Signature fornendo il percorso del file di presentazione.
## Passaggio 4: definire le opzioni di firma dei metadati
```csharp
MetadataSignOptions options = new MetadataSignOptions();
```
Crea un'istanza di MetadataSignOptions per definire le opzioni di firma dei metadati.
## Passaggio 5: crea firme di metadati
```csharp
PresentationMetadataSignature[] signatures = new PresentationMetadataSignature[]
{
    new PresentationMetadataSignature("Author", "Mr.Scherlock Holmes"),
    new PresentationMetadataSignature("CreatedOn", DateTime.Now),
    new PresentationMetadataSignature("DocumentId", 123456),
    new PresentationMetadataSignature("SignatureId", 123.456D),
    new PresentationMetadataSignature("Amount", 123.456M),
    new PresentationMetadataSignature("Total", 123.456F)
};
```
Crea una serie di oggetti PresentationMetadataSignature, ciascuno dei quali rappresenta una firma dei metadati. Puoi aggiungere vari tipi di metadati, tra cui stringa, DateTime, intero, doppio, decimale e float.
## Passaggio 6: aggiungi firme alle opzioni
```csharp
options.Signatures.AddRange(signatures);
```
Aggiungi le firme dei metadati create all'oggetto MetadataSignOptions.
## Passaggio 7: firma il documento
```csharp
SignResult result = signature.Sign(outputFilePath, options);
```
Firma il file di presentazione con metadati utilizzando le opzioni specificate e salva il file firmato nel percorso di output.
## Passaggio 8: Visualizza risultato
```csharp
Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).\nFile saved at {outputFilePath}.");
```
Visualizza un messaggio di successo insieme al numero di firme applicate e al percorso in cui viene salvato il file firmato.

## Conclusione
In questo tutorial abbiamo imparato come firmare un file di presentazione con metadati utilizzando la libreria GroupDocs.Signature per .NET. L'aggiunta di firme di metadati migliora l'integrità del documento e fornisce informazioni preziose sul suo contenuto.

## Domande frequenti
### Posso firmare altri formati di documenti oltre a PPTX con metadati utilizzando GroupDocs.Signature per .NET?
Sì, GroupDocs.Signature supporta vari formati di documenti, tra cui Word, Excel, PDF e altri, per la firma con metadati.
### GroupDocs.Signature per .NET è compatibile con .NET Core?
Sì, la libreria è compatibile sia con .NET Framework che con .NET Core.
### Posso personalizzare l'aspetto delle firme dei metadati?
Sì, puoi personalizzare l'aspetto, la posizione e altre proprietà delle firme dei metadati in base alle tue esigenze.
### GroupDocs.Signature per .NET fornisce la crittografia per i documenti firmati?
Sì, GroupDocs.Signature offre opzioni di crittografia per proteggere i documenti firmati da accessi non autorizzati.
### È disponibile una versione di prova da provare prima dell'acquisto?
 Sì, puoi usufruire di una prova gratuita di GroupDocs.Signature per .NET da[Qui](https://releases.groupdocs.com/).