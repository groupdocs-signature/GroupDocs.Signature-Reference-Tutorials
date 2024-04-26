---
title: Elimina il codice a barre dal documento
linktitle: Elimina il codice a barre dal documento
second_title: API GroupDocs.Signature .NET
description: Scopri come eliminare il codice a barre da un documento utilizzando GroupDocs.Signature per .NET. Guida passo passo con esempi di codice.
type: docs
weight: 10
url: /it/net/delete-operations/delete-barcode/
---
## introduzione
GroupDocs.Signature per .NET è una potente libreria che consente agli sviluppatori di lavorare senza problemi con firme digitali, timbri e codici a barre all'interno delle applicazioni .NET. In questo tutorial ti guideremo attraverso il processo di eliminazione di un codice a barre da un documento utilizzando GroupDocs.Signature per .NET.
## Prerequisiti
Prima di iniziare, assicurati di possedere i seguenti prerequisiti:
- Conoscenza base del linguaggio di programmazione C#.
- Visual Studio installato nel sistema.
-  Libreria GroupDocs.Signature per .NET installata. Puoi scaricarlo da[Qui](https://releases.groupdocs.com/signature/net/).
- Un documento di esempio con un codice a barre che desideri eliminare.

## Importa spazi dei nomi
Innanzitutto, assicurati di importare gli spazi dei nomi necessari nel tuo codice C#:
```csharp
using System;
using System.IO;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

Analizziamo il processo di eliminazione di un codice a barre da un documento in semplici passaggi:
## Passaggio 1: definire i percorsi dei file
```csharp
string filePath = "sample_multiple_signatures.docx";
string fileName = Path.GetFileName(filePath);
string outputFilePath = Path.Combine("Your Document Directory", "DeleteBarcode", fileName);
```
 Assicurarsi di sostituire`"sample_multiple_signatures.docx"` con il percorso del documento contenente il codice a barre.
## Passaggio 2: copia il file sorgente
```csharp
File.Copy(filePath, outputFilePath, true);
```
Questo passaggio garantisce che stiamo lavorando con una copia del documento originale per preservare il file originale.
## Passaggio 3: inizializzare GroupDocs.Signature
```csharp
using (Signature signature = new Signature(outputFilePath))
{
    // Il tuo codice va qui
}
```
Inizializza l'oggetto Signature passando il percorso alla copia del documento creata nel passaggio precedente.
## Passaggio 4: ricerca delle firme dei codici a barre
```csharp
BarcodeSearchOptions options = new BarcodeSearchOptions();
List<BarcodeSignature> signatures = signature.Search<BarcodeSignature>(options);
```
Crea un'istanza di BarcodeSearchOptions e utilizzala per cercare firme di codici a barre all'interno del documento.
## Passaggio 5: eliminare la firma del codice a barre
```csharp
if (signatures.Count > 0)
{
    BarcodeSignature barcodeSignature = signatures[0];
    bool result = signature.Delete(barcodeSignature);
    if (result)
    {
        Console.WriteLine($"Signature with Barcode '{barcodeSignature.Text}' and encode type '{barcodeSignature.EncodeType.TypeName}' was deleted from document ['{fileName}'].");
    }
    else
    {
        Helper.WriteError($"Signature was not deleted from the document! Signature with Barcode '{barcodeSignature.Text}' and encode type '{barcodeSignature.EncodeType.TypeName}' was not found!");
    }
}
```
Controlla se nel documento sono presenti firme con codici a barre. Se trovata, elimina la prima firma del codice a barre trovata.

## Conclusione
In questo tutorial, abbiamo imparato come eliminare un codice a barre da un documento utilizzando GroupDocs.Signature per .NET. Seguendo la guida passo passo, puoi integrare perfettamente la funzionalità di eliminazione dei codici a barre nelle tue applicazioni .NET.
## Domande frequenti
### Posso eliminare più firme con codice a barre da un documento?
Sì, puoi modificare il codice per eliminare più firme di codici a barre scorrendo l'elenco delle firme.
### GroupDocs.Signature per .NET supporta altri tipi di firme?
Sì, GroupDocs.Signature per .NET supporta vari tipi di firme, tra cui firme digitali, timbri e firme di testo.
### Posso personalizzare le opzioni di ricerca per le firme con codice a barre?
Sì, puoi personalizzare le opzioni di ricerca in base alle tue esigenze, ad esempio specificando i tipi di codici a barre o le aree di ricerca all'interno del documento.
### GroupDocs.Signature per .NET è compatibile con diversi formati di documenti?
Sì, GroupDocs.Signature per .NET supporta un'ampia gamma di formati di documenti, tra cui Word, Excel, PDF e altri.
### Dove posso trovare ulteriore supporto o risorse per GroupDocs.Signature per .NET?
 È possibile visitare il forum GroupDocs.Signature[Qui](https://forum.groupdocs.com/c/signature/13) per qualsiasi domanda o assistenza riguardante la biblioteca.