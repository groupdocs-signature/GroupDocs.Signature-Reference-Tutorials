---
title: Elimina firma immagine
linktitle: Elimina firma immagine
second_title: API GroupDocs.Signature .NET
description: Scopri come eliminare le firme delle immagini dai documenti utilizzando GroupDocs.Signature per .NET. Segui la nostra guida passo passo per una gestione efficiente delle firme.
weight: 14
url: /it/net/delete-operations/delete-image-signature/
---
## introduzione
In questo tutorial esploreremo come eliminare le firme di immagini dai documenti utilizzando GroupDocs.Signature per .NET. GroupDocs.Signature è una potente libreria che consente agli sviluppatori di lavorare con firme digitali, timbri e campi modulo all'interno di vari formati di documenti.
## Prerequisiti
Prima di iniziare, assicurati di avere quanto segue:
### 1. GroupDocs.Signature per .NET
 Scarica e installa GroupDocs.Signature per .NET dal file[sito web](https://releases.groupdocs.com/signature/net/). Seguire le istruzioni di installazione fornite nella documentazione.
### 2. .NET Framework
Assicurati di avere .NET Framework installato sul tuo computer.
## Importa spazi dei nomi
Includi gli spazi dei nomi necessari nel tuo progetto:
```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
Analizziamo il processo di eliminazione delle firme delle immagini in più passaggi:
## Passaggio 1: definire i percorsi dei file
Innanzitutto, specifica i percorsi per il documento di input e il documento di output dopo aver eliminato la firma:
```csharp
string filePath = "sample_multiple_signatures.docx";
string fileName = Path.GetFileName(filePath);
string outputFilePath = Path.Combine("Your Document Directory", "DeleteImage", fileName);
```
## Passaggio 2: copia il file sorgente
 Dal momento che`Delete`funziona con lo stesso documento, è essenziale copiare il file sorgente in un'altra posizione:
```csharp
File.Copy(filePath, outputFilePath, true);
```
## Passaggio 3: inizializzare l'oggetto firma
 Crea un'istanza di`Signature` class e specificare il percorso del documento di output:
```csharp
using (Signature signature = new Signature(outputFilePath))
{
    // Il codice va qui
}
```
## Passaggio 4: ricerca delle firme immagine
Definisci le opzioni di ricerca e cerca le firme immagine all'interno del documento:
```csharp
ImageSearchOptions options = new ImageSearchOptions();
List<ImageSignature> signatures = signature.Search<ImageSignature>(options);
```
## Passaggio 5: Elimina la firma dell'immagine
Se vengono trovate firme di immagini, elimina la prima:
```csharp
if (signatures.Count > 0)
{
    ImageSignature imageSignature = signatures[0];
    bool result = signature.Delete(imageSignature);
    if (result)
    {
        Console.WriteLine($"Image signature at location {imageSignature.Left}x{imageSignature.Top} and Size {imageSignature.Size} was deleted from document ['{fileName}'].");
    }
    else
    {
        Helper.WriteError($"Signature was not deleted from the document! Signature at location {imageSignature.Left}x{imageSignature.Top} and Size {imageSignature.Size} was not found!");
    }
}
```
## Conclusione
In questo tutorial, abbiamo imparato come eliminare le firme delle immagini dai documenti utilizzando GroupDocs.Signature per .NET. Seguendo la guida passo passo, gli sviluppatori possono gestire in modo efficiente le firme digitali all'interno delle loro applicazioni.
## Domande frequenti
### Posso eliminare più firme di immagini da un documento?
 Sì, puoi modificare il codice per eliminare più firme di immagini eseguendo l'iterazione su`signatures` elenco.
### GroupDocs.Signature supporta altri formati di documenti oltre a DOCX?
Sì, GroupDocs.Signature supporta un'ampia gamma di formati di documenti, inclusi PDF, PPT, XLS e altri.
### È disponibile una versione di prova per GroupDocs.Signature per .NET?
 Sì, puoi scaricare una versione di prova gratuita da[sito web](https://releases.groupdocs.com/).
### Come posso ottenere supporto per GroupDocs.Signature?
 Puoi visitare il[Forum GroupDocs.Signature](https://forum.groupdocs.com/c/signature/13) per assistenza e supporto.
### Posso acquistare una licenza temporanea per GroupDocs.Signature?
 Sì, puoi acquistare una licenza temporanea da[pagina di acquisto](https://purchase.groupdocs.com/temporary-license/).