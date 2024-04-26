---
title: Firma di documenti con codice QR utilizzando GroupDocs.Signature
linktitle: Firmare con il codice QR
second_title: API GroupDocs.Signature .NET
description: Scopri come aggiungere firme di codici QR ai tuoi documenti con GroupDocs.Signature per .NET. Migliora la sicurezza e l'autenticazione senza sforzo.
type: docs
weight: 15
url: /it/net/advanced-signature-techniques/sign-with-qr-code/
---
## introduzione
In questo tutorial, esamineremo il processo di firma dei documenti con un codice QR utilizzando GroupDocs.Signature per .NET. GroupDocs.Signature per .NET è una potente API che consente agli sviluppatori di aggiungere vari tipi di firme ai documenti digitali in modo programmatico. La firma di documenti con codici QR può fornire un ulteriore livello di sicurezza e autenticazione ai tuoi documenti.
## Prerequisiti
Prima di iniziare, assicurati di avere installati i seguenti prerequisiti:
1.  GroupDocs.Signature per .NET: è possibile scaricare la libreria dal file[sito web](https://releases.groupdocs.com/signature/net/).
2. Ambiente di sviluppo: assicurati di avere un ambiente di sviluppo .NET configurato sul tuo computer.
3. Documento di esempio: prepara un documento di esempio (ad esempio PDF) che desideri firmare con un codice QR.

## Importazione degli spazi dei nomi necessari
Prima di immergerci nel codice, importiamo gli spazi dei nomi necessari:
```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

## Passaggio 1: definire i percorsi dei file
```csharp
string filePath = "sample.pdf";
string fileName = Path.GetFileName(filePath);
string outputFilePath = Path.Combine("Your Document Directory", "SignWithQRCode", fileName);
```
 Assicurarsi di sostituire`"Your Document Directory"` con il percorso della directory in cui si desidera salvare il documento firmato.
## Passaggio 2: inizializzare l'oggetto firma
```csharp
using (Signature signature = new Signature(filePath))
{
    //Il codice per la firma va qui
}
```
 Inizializzare a`Signature` oggetto con il percorso del documento che vuoi firmare.
## Passaggio 3: crea QRCodeSignOptions
```csharp
QrCodeSignOptions options = new QrCodeSignOptions("JohnSmith")
{
    EncodeType = QrCodeTypes.QR,
    Left = 50,
    Top = 150,
    Width = 200,
    Height = 200
};
```
 Creare un`QrCodeSignOptions` oggetto con le impostazioni desiderate per la firma del codice QR. Puoi personalizzare parametri come il testo da codificare, la posizione e le dimensioni del codice QR.
## Passaggio 4: firma il documento
```csharp
SignResult result = signature.Sign(outputFilePath, options);
```
 Usa il`Sign` metodo del`Signature` oggetto di firmare il documento con le opzioni specificate. Questo metodo restituisce a`SignResult` oggetto contenente informazioni sul processo di firma.
## Passaggio 5: Visualizza il risultato
```csharp
Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).\nFile saved at {outputFilePath}.");
```
Visualizza un messaggio che indica il successo del processo di firma e la posizione in cui viene salvato il documento firmato.

## Conclusione
In questo tutorial abbiamo imparato come firmare documenti con un codice QR utilizzando GroupDocs.Signature per .NET. Seguendo questi semplici passaggi, puoi aggiungere firme di codici QR ai tuoi documenti digitali, migliorando la sicurezza e l'autenticazione.

## Domande frequenti
### Posso personalizzare l'aspetto del codice QR?
Sì, puoi personalizzare vari parametri come dimensione, posizione e tipo di codifica del codice QR in base alle tue esigenze.
### Quali formati di documento sono supportati per la firma con i codici QR?
GroupDocs.Signature per .NET supporta un'ampia gamma di formati di documenti, tra cui PDF, Word, Excel, PowerPoint e altri.
### È possibile firmare più documenti in un processo batch?
Assolutamente, puoi utilizzare GroupDocs.Signature for .NET per firmare più documenti contemporaneamente, semplificando il tuo flusso di lavoro.
### Posso verificare l'autenticità di un documento firmato con un codice QR?
Sì, GroupDocs.Signature per .NET fornisce meccanismi di verifica per garantire l'integrità e l'autenticità dei documenti firmati.
### È disponibile una versione di prova per testare la funzionalità prima dell'acquisto?
 Sì, puoi scaricare una versione di prova gratuita da[sito web](https://releases.groupdocs.com/) per valutare le caratteristiche e le capacità di GroupDocs.Signature per .NET.