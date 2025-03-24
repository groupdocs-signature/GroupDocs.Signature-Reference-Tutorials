---
title: Firma PDF con metadati
linktitle: Firma PDF con metadati
second_title: API GroupDocs.Signature .NET
description: Scopri come firmare documenti PDF con metadati utilizzando GroupDocs.Signature per .NET. Migliora facilmente la tracciabilità e l'autenticità dei documenti.
weight: 11
url: /it/net/document-signing/sign-pdf-with-metadata/
---

# Firma PDF con metadati

## introduzione
In questo tutorial impareremo come firmare un documento PDF con metadati utilizzando GroupDocs.Signature per .NET. L'aggiunta di metadati a un PDF può fornire ulteriori informazioni sul documento, come paternità, data di creazione, ID documento e altro.
## Prerequisiti
Prima di iniziare, assicurati di avere quanto segue:
1.  GroupDocs.Signature per .NET: puoi scaricarlo da[Qui](https://releases.groupdocs.com/signature/net/).
2. Un documento PDF: tieni pronto un file PDF di esempio per la firma.
3. Conoscenza di base della programmazione C#: per comprendere gli esempi di codice è necessaria la familiarità con la sintassi C#.
## Importa spazi dei nomi
Innanzitutto, assicurati di importare gli spazi dei nomi necessari per accedere alle classi e ai metodi richiesti:
```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## Passaggio 1: caricare il documento PDF
Carica il documento PDF che vuoi firmare:
```csharp
string filePath = "sample.pdf";
```
## Passaggio 2: specificare il percorso del file di output
Definire il percorso del file di output in cui verrà salvato il PDF firmato con metadati:
```csharp
string outputFilePath = Path.Combine("Your Document Directory", "SignPdfWithMetadata", "SignedWithMetadata.pdf");
```
## Passaggio 3: crea un'istanza di firma
Inizializza un'istanza di firma fornendo il percorso del documento PDF:
```csharp
using (Signature signature = new Signature(filePath))
{
    // Il codice relativo alla firma andrà qui
}
```
## Passaggio 4: definire le opzioni dei metadati
Crea MetadataSignOptions e aggiungi campi di metadati con i rispettivi valori:
```csharp
MetadataSignOptions options = new MetadataSignOptions();
options
    .Add(new PdfMetadataSignature("Author", "Mr.Sherlock Holmes")) // Valore stringa
    .Add(new PdfMetadataSignature("CreatedOn", DateTime.Now))       // Valori DateTime
    .Add(new PdfMetadataSignature("DocumentId", 123456))            // Valore intero
    .Add(new PdfMetadataSignature("SignatureId", 123.456D))         // Doppio valore
    .Add(new PdfMetadataSignature("Amount", 123.456M))              // Valore decimale
    .Add(new PdfMetadataSignature("Total", 123.456F));              // Valore flottante
```
## Passaggio 5: firma il documento
Firma il documento PDF con le opzioni di metadati specificate e salva il documento firmato:
```csharp
SignResult result = signature.Sign(outputFilePath, options);
Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).\nFile saved at {outputFilePath}.");
```

## Conclusione
In questo tutorial, abbiamo spiegato come firmare un documento PDF con metadati utilizzando GroupDocs.Signature per .NET. Seguendo la guida passo passo, puoi aggiungere facilmente informazioni sui metadati come paternità, data di creazione e altro ancora ai tuoi file PDF, migliorandone l'utilità e la tracciabilità.
## Domande frequenti
### Posso aggiungere campi di metadati personalizzati ai miei documenti PDF?
Sì, puoi aggiungere campi di metadati personalizzati specificando il nome del campo e il valore corrispondente utilizzando GroupDocs.Signature per .NET.
### GroupDocs.Signature per .NET è compatibile con tutte le versioni di .NET Framework?
GroupDocs.Signature per .NET è compatibile con varie versioni di .NET Framework, garantendo flessibilità e facilità di integrazione.
### GroupDocs.Signature supporta la firma di altri formati di documenti oltre al PDF?
Sì, GroupDocs.Signature supporta un'ampia gamma di formati di documenti, tra cui Word, Excel, PowerPoint e altri.
### Posso firmare più documenti in blocco utilizzando GroupDocs.Signature per .NET?
Sì, puoi firmare più documenti in blocco scorrendo un elenco di file e applicando il processo di firma a livello di codice.
### Il supporto tecnico è disponibile per gli utenti di GroupDocs.Signature?
 Sì, GroupDocs fornisce supporto tecnico dedicato attraverso i suoi forum. È possibile accedere al forum di supporto[Qui](https://forum.groupdocs.com/c/signature/13).