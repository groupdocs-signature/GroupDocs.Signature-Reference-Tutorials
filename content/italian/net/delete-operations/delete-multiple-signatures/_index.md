---
title: Elimina più firme dal documento
linktitle: Elimina più firme dal documento
second_title: API GroupDocs.Signature .NET
description: Elimina facilmente più firme dai documenti utilizzando GroupDocs.Signature per .NET. Semplifica il flusso di lavoro della gestione dei documenti.
weight: 15
url: /it/net/delete-operations/delete-multiple-signatures/
---

# Elimina più firme dal documento

## introduzione
Nel mondo digitale, la gestione dei documenti spesso implica la gestione di varie firme. L'eliminazione di più firme da un documento a livello di codice può semplificare i flussi di lavoro e migliorare l'efficienza. Con GroupDocs.Signature per .NET, questa attività diventa semplice e immediata. Questo tutorial ti guiderà passo dopo passo attraverso il processo di eliminazione di più firme da un documento.
## Prerequisiti
Prima di immergerti nel tutorial, assicurati di possedere i seguenti prerequisiti:
- Conoscenza base del linguaggio di programmazione C#.
- GroupDocs.Signature installato per la libreria .NET.
- Documento di esempio con firme multiple per test.

## Importa spazi dei nomi
Inizia importando gli spazi dei nomi necessari per accedere alla funzionalità di GroupDocs.Signature per .NET:
```csharp
using System;
using System.IO;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## Passaggio 1: definire il percorso del documento e il nome del file
Imposta il percorso del file del documento contenente più firme. Assicurati di avere il percorso e il nome file appropriati:
```csharp
string filePath = "sample_multiple_signatures.docx";
string fileName = Path.GetFileName(filePath);
```
## Passaggio 2: copiare il documento per l'elaborazione
Per evitare di modificare il documento originale, crea una copia per l'elaborazione:
```csharp
string outputFilePath = Path.Combine("Your Document Directory", "DeleteMultiple", fileName);
File.Copy(filePath, outputFilePath, true);
```
## Passaggio 3: inizializzare l'oggetto firma
Crea un'istanza di un oggetto Signature utilizzando il percorso del file di output:
```csharp
using (Signature signature = new Signature(outputFilePath))
{
    // Il codice di elaborazione della firma va qui
}
```
## Passaggio 4: definire le opzioni di ricerca
Definire varie opzioni di ricerca per identificare le firme all'interno del documento. Le opzioni includono ricerca di testo, ricerca di immagini, ricerca di codici a barre e ricerca di codici QR:
```csharp
TextSearchOptions textSearchOptions = new TextSearchOptions();
ImageSearchOptions imageSearchOptions = new ImageSearchOptions();
BarcodeSearchOptions barcodeOptions = new BarcodeSearchOptions();
QrCodeSearchOptions qrCodeOptions = new QrCodeSearchOptions();
// Aggiungi opzioni all'elenco
List<SearchOptions> listOptions = new List<SearchOptions>();
listOptions.Add(textSearchOptions);
listOptions.Add(imageSearchOptions);
listOptions.Add(barcodeOptions);
listOptions.Add(qrCodeOptions);
```
## Passaggio 5: ricerca delle firme
Esegui un'operazione di ricerca per trovare tutte le firme all'interno del documento in base alle opzioni di ricerca definite:
```csharp
SearchResult result = signature.Search(listOptions);
```
## Passaggio 6: eliminare le firme
Se vengono trovate firme, procedere alla loro eliminazione:
```csharp
if (result.Signatures.Count > 0)
{
    // Tentare di eliminare tutte le firme
    DeleteResult deleteResult = signature.Delete(result.Signatures);
    //Controlla se la cancellazione è andata a buon fine
    if(deleteResult.Succeeded.Count == result.Signatures.Count)
    {
        Console.WriteLine("\nAll signatures were successfully deleted!");                        
    }
    else
    {
        Console.WriteLine($"Successfully deleted signatures : {deleteResult.Succeeded.Count}");
        Helper.WriteError($"Not deleted signatures : {deleteResult.Failed.Count}");
    }
    // Visualizza informazioni sulle firme cancellate
    Console.WriteLine("\nList of deleted signatures:");
    int number = 1;
    foreach(BaseSignature temp in deleteResult.Succeeded)
    {
        Console.WriteLine($"Signature #{number++}: Type: {temp.SignatureType} Id:{temp.SignatureId}, Location: {temp.Left}x{temp.Top}. Size: {temp.Width}x{temp.Height}");
    }
}
else
{
    Helper.WriteError("No one signature was found.");
}
```

## Conclusione
L'eliminazione di più firme da un documento a livello di codice è un'attività cruciale nella gestione dei documenti. Con GroupDocs.Signature per .NET, questo processo diventa efficiente e affidabile. Seguendo i passaggi descritti in questo tutorial, puoi integrare facilmente la funzionalità di eliminazione delle firme nelle tue applicazioni .NET.
## Domande frequenti
### GroupDocs.Signature per .NET può gestire vari formati di documenti?
Sì, GroupDocs.Signature per .NET supporta un'ampia gamma di formati di documenti, inclusi DOCX, PDF, PPTX, XLSX e altri.
### È possibile personalizzare le opzioni di ricerca per il rilevamento della firma?
Assolutamente, puoi personalizzare le opzioni di ricerca come ricerca di testo, ricerca di immagini, ricerca di codici a barre e ricerca di codici QR per soddisfare le tue esigenze specifiche.
### GroupDocs.Signature per .NET fornisce meccanismi di gestione degli errori?
Sì, la libreria offre solide funzionalità di gestione degli errori per garantire un'esecuzione fluida delle attività di elaborazione dei documenti.
### Posso integrare GroupDocs.Signature for .NET con altre librerie di terze parti?
Certamente, GroupDocs.Signature per .NET è progettato per integrarsi perfettamente con altre librerie .NET, fornendo flessibilità ed estensibilità.
### Dove posso trovare ulteriore supporto e risorse per GroupDocs.Signature per .NET?
 Puoi visitare i GroupDocs[Forum](https://forum.groupdocs.com/c/signature/13) dedicarsi alle discussioni relative alla firma e chiedere assistenza alla comunità e agli esperti.