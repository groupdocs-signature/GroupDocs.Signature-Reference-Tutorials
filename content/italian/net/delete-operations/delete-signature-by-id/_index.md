---
title: Elimina firma per ID
linktitle: Elimina firma per ID
second_title: API GroupDocs.Signature .NET
description: Scopri come eliminare una firma in base all'ID nei documenti .NET utilizzando la libreria GroupDocs.Signature. Facile guida passo passo.
weight: 11
url: /it/net/delete-operations/delete-signature-by-id/
---

# Elimina firma per ID

## introduzione
In questo tutorial esploreremo come eliminare una firma in base al relativo ID utilizzando GroupDocs.Signature per .NET. GroupDocs.Signature per .NET è una potente libreria che consente agli sviluppatori di aggiungere, rimuovere o verificare firme digitali in vari formati di documenti utilizzando applicazioni .NET.
## Prerequisiti
Prima di iniziare, assicurati di avere i seguenti prerequisiti:
1.  GroupDocs.Signature per .NET Library: scarica e installa la libreria da[Qui](https://releases.groupdocs.com/signature/net/).
2. .NET Framework: assicurati di avere .NET Framework installato sul tuo sistema.
3. Documento con firma: prepara un documento (ad esempio DOCX, PDF) con una firma che desideri eliminare.

## Importa spazi dei nomi
```csharp
using System;
using System.IO;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## Passaggio 1: definire i percorsi dei file
Innanzitutto, specificare il percorso del file per il documento contenente la firma e il percorso del file di output in cui verrà salvato il documento modificato.
```csharp
string filePath = "sample_multiple_signatures.docx";
string fileName = Path.GetFileName(filePath);
string outputFilePath = Path.Combine("Your Document Directory", "DeleteById", fileName);
```
## Passaggio 2: copiare il documento
 Dal momento che`Delete` Il metodo modifica il documento sul posto, è meglio creare una copia del documento originale.
```csharp
File.Copy(filePath, outputFilePath, true);
```
## Passaggio 3: elimina la firma per ID
 Inizializza il`Signature` oggetto con il percorso del file del documento e utilizzare il file`Delete` metodo per rimuovere la firma tramite il suo ID.
```csharp
using (Signature signature = new Signature(outputFilePath))
{
    string id = @"eff64a14-dad9-47b0-88e5-2ee4e3604e71";
    bool result = signature.Delete(id);
    if (result)
    {
        Console.WriteLine($"Signature with Id# '{id}' was deleted from document ['{fileName}'].");
    }
    else
    {
        Helper.WriteError($"Signature was not deleted from the document! Signature with id# '{id}' was not found!");
    }
}
```

## Conclusione
In questo tutorial abbiamo imparato come eliminare una firma in base al suo ID utilizzando GroupDocs.Signature per .NET. Questa libreria fornisce un modo conveniente per gestire le firme digitali in vari formati di documenti a livello di codice.
## Domande frequenti
### Posso eliminare più firme contemporaneamente?
 Sì, puoi eliminare più firme scorrendo i loro ID e chiamando il file`Delete` metodo per ciascun ID.
### GroupDocs.Signature per .NET è compatibile con tutti i formati di documenti?
GroupDocs.Signature per .NET supporta un'ampia gamma di formati di documenti, inclusi PDF, DOCX, XLSX e altri.
### Posso personalizzare l'aspetto della firma?
Sì, puoi personalizzare l'aspetto della firma, inclusa la posizione, la dimensione, il carattere e il colore.
### È disponibile una versione di prova?
 Sì, puoi scaricare una versione di prova gratuita da[Qui](https://releases.groupdocs.com/).
### Dove posso trovare aiuto o supporto per GroupDocs.Signature per .NET?
 Puoi visitare il forum di supporto[Qui](https://forum.groupdocs.com/c/signature/13) per assistenza.