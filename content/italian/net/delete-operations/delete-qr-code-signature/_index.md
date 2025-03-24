---
title: Elimina la firma del codice QR dal documento
linktitle: Elimina la firma del codice QR dal documento
second_title: API GroupDocs.Signature .NET
description: Scopri come eliminare le firme dei codici QR dai documenti utilizzando GroupDocs.Signature per .NET. Segui la nostra guida passo passo per una gestione efficiente delle firme.
weight: 16
url: /it/net/delete-operations/delete-qr-code-signature/
---
## introduzione
In questo tutorial ti guideremo attraverso il processo di rimozione di una firma con codice QR da un documento utilizzando GroupDocs.Signature per .NET. Segui queste istruzioni dettagliate per eliminare in modo efficace le firme dei codici QR.
## Prerequisiti
Prima di iniziare, assicurati di possedere i seguenti prerequisiti:
-  GroupDocs.Signature per .NET: assicurati di avere la libreria GroupDocs.Signature installata nel tuo progetto .NET. Puoi scaricarlo da[Qui](https://releases.groupdocs.com/signature/net/).
- Documento con firma del codice QR: prepara un documento contenente le firme del codice QR che desideri eliminare.
- Conoscenza di base di C#: familiarizza con le nozioni di base del linguaggio di programmazione C#.

## Importazione di spazi dei nomi
Prima di immergerti nel codice, importa gli spazi dei nomi necessari nel tuo file C#:
```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## Passaggio 1: definire i percorsi dei file
```csharp
// Il percorso della directory dei documenti.
string filePath = "sample_multiple_signatures.docx";
string fileName = Path.GetFileName(filePath);
// Definire il percorso del file di output per il documento modificato.
string outputFilePath = Path.Combine("Your Document Directory", "DeleteQRCode", fileName);
// Copia il file sorgente poiché il metodo Elimina funziona con lo stesso documento.
File.Copy(filePath, outputFilePath, true);
```
## Passaggio 2: inizializzare l'oggetto firma
```csharp
using (Signature signature = new Signature(outputFilePath))
{
    // Crea opzioni per la ricerca delle firme dei codici QR.
    QrCodeSearchOptions options = new QrCodeSearchOptions();
    // Cerca le firme del codice QR nel documento.
    List<QrCodeSignature> signatures = signature.Search<QrCodeSignature>(options);
```
## Passaggio 3: verificare l'esistenza della firma del codice QR
```csharp
    if (signatures.Count > 0)
    {
        // Ottieni la prima firma del codice QR trovata nel documento.
        QrCodeSignature qrCodeSignature = signatures[0];
```
## Passaggio 4: elimina la firma del codice QR
```csharp
        // Elimina la firma del codice QR dal documento.
        bool result = signature.Delete(qrCodeSignature);
        if (result)
        {
            Console.WriteLine($"Signature with QR-Code '{qrCodeSignature.Text}' and encode type '{qrCodeSignature.EncodeType.TypeName}' was deleted from document ['{fileName}'].");
        }
        else
        {
            Helper.WriteError($"Signature was not deleted from the document! Signature with Barcode '{qrCodeSignature.Text}' and encode type '{qrCodeSignature.EncodeType.TypeName}' was not found!");
        }
    }
}
```
Congratulazioni! Hai rimosso correttamente la firma del codice QR dal documento utilizzando GroupDocs.Signature per .NET.

## Conclusione
In questo tutorial, abbiamo imparato come eliminare una firma con codice QR da un documento utilizzando GroupDocs.Signature per .NET. Seguendo i passaggi forniti, puoi gestire e manipolare in modo efficiente le firme all'interno delle tue applicazioni .NET.
## Domande frequenti
### Posso eliminare più firme di codici QR da un documento?
Sì, puoi modificare il codice per scorrere tutte le firme dei codici QR ed eliminarle di conseguenza.
### GroupDocs.Signature supporta altri tipi di firme oltre ai codici QR?
Sì, GroupDocs.Signature supporta vari tipi di firma come testo, immagine, codice a barre e altro.
### GroupDocs.Signature è compatibile con tutti i formati di documenti?
GroupDocs.Signature supporta un'ampia gamma di formati di documenti tra cui PDF, Microsoft Word, Excel, PowerPoint e altri.
### Posso personalizzare le opzioni di ricerca per le firme?
Sì, puoi personalizzare le opzioni di ricerca in base alle tue esigenze per individuare firme specifiche all'interno del documento.
### È disponibile una versione di prova per GroupDocs.Signature?
 Sì, puoi accedere a una versione di prova gratuita di GroupDocs.Signature da[Qui](https://releases.groupdocs.com/).