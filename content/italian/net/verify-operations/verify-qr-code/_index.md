---
title: Verifica il codice QR
linktitle: Verifica il codice QR
second_title: API GroupDocs.Signature .NET
description: Scopri come verificare i codici QR all'interno dei documenti utilizzando GroupDocs.Signature per .NET. Tutorial completo con guida passo passo.
weight: 12
url: /it/net/verify-operations/verify-qr-code/
---
## introduzione
Nell'ambito della gestione e dell'autenticazione dei documenti, garantire l'integrità e la validità delle firme è fondamentale. GroupDocs.Signature per .NET fornisce una soluzione completa per la verifica dei codici QR incorporati nei documenti. In questo tutorial, approfondiremo il processo passo passo di verifica dei codici QR utilizzando GroupDocs.Signature per .NET.
## Prerequisiti
Prima di immergerti nel processo di verifica, assicurati di disporre dei seguenti prerequisiti:
1.  Installazione di GroupDocs.Signature per .NET: scaricare e installare GroupDocs.Signature per .NET dal[Link per scaricare](https://releases.groupdocs.com/signature/net/).
2. Accesso a un documento contenente codici QR: preparare un documento di esempio che contiene codici QR per la verifica. 

## Importa spazi dei nomi
Innanzitutto, devi importare gli spazi dei nomi necessari per utilizzare le funzionalità fornite da GroupDocs.Signature per .NET. Segui questi passi:

```csharp
using System;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```


Ora analizziamo il processo di verifica dei codici QR incorporati in un documento utilizzando GroupDocs.Signature per .NET:
## Passaggio 1: specificare il percorso del documento
```csharp
string filePath = "sample_multiple_signatures.docx";
```
 Assicurarsi di sostituire`"sample_multiple_signatures.docx"` con il percorso del documento.
## Passaggio 2: inizializzare l'oggetto firma
```csharp
using (Signature signature = new Signature(filePath))
{
    //Il codice di verifica va qui
}
```
 Inizializzare a`Signature` oggetto fornendo il percorso del documento.
## Passaggio 3: specificare le opzioni di verifica
```csharp
QrCodeVerifyOptions options = new QrCodeVerifyOptions()
{
    AllPages = true, // questo valore è impostato per impostazione predefinita
    Text = "John",
    MatchType = TextMatchType.Contains
};
```
 Definire opzioni di verifica come`AllPages` per verificare tutte le pagine,`Text` specificare il testo da abbinare all'interno del codice QR, e`MatchType` definire i criteri di abbinamento.
## Passaggio 4: verifica le firme dei documenti
```csharp
VerificationResult result = signature.Verify(options);
```
 Invocare il`Verify` metodo del`Signature` oggetto, passando le opzioni di verifica.
## Passaggio 5: gestire i risultati della verifica
```csharp
if (result.IsValid)
{
    // Trovata firma valida
}
else
{
    // Trovata firma non valida
}
```
In base al risultato della verifica, gestisci di conseguenza gli scenari di successo o fallimento.

## Conclusione
In questo tutorial abbiamo esplorato il processo di verifica dei codici QR all'interno dei documenti utilizzando GroupDocs.Signature per .NET. Seguendo questi passaggi, puoi integrare perfettamente la funzionalità di verifica del codice QR nelle tue applicazioni .NET, garantendo l'integrità e l'autenticità del documento.
## Domande frequenti
### GroupDocs.Signature per .NET può verificare i codici QR su diversi formati di documenti?
Sì, GroupDocs.Signature per .NET supporta un'ampia gamma di formati di documenti tra cui DOCX, PDF e altri per la verifica del codice QR.
### È disponibile una prova gratuita per GroupDocs.Signature per .NET?
 Sì, puoi usufruire di una prova gratuita da[pagina delle uscite](https://releases.groupdocs.com/).
### Quali opzioni di supporto sono disponibili per gli utenti GroupDocs.Signature per .NET?
 Gli utenti possono accedere al supporto tramite[Forum](https://forum.groupdocs.com/c/signature/13) per GroupDocs.Signature.
### Posso acquistare una licenza temporanea per GroupDocs.Signature per .NET?
 Sì, è possibile acquistare licenze temporanee da[Pagina di acquisto di GroupDocs](https://purchase.groupdocs.com/temporary-license/).
### È disponibile un'ampia documentazione per GroupDocs.Signature per .NET?
 Assolutamente sì, potete fare riferimento alla documentazione dettagliata fornita[Qui](https://tutorials.groupdocs.com/signature/net/) per una guida completa sull'utilizzo delle funzionalità di GroupDocs.Signature per .NET.