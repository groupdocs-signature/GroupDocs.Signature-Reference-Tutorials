---
title: Elimina la firma digitale dal documento
linktitle: Elimina la firma digitale dal documento
second_title: API GroupDocs.Signature .NET
description: Scopri come eliminare le firme digitali dai documenti utilizzando GroupDocs.Signature per .NET. Segui la nostra guida passo passo per una gestione efficiente.
weight: 13
url: /it/net/delete-operations/delete-digital-signature/
---
## introduzione
Nel mondo dei documenti digitali, garantire l’autenticità e la sicurezza è fondamentale. Le firme digitali svolgono un ruolo cruciale nella verifica dell'integrità dei documenti elettronici. GroupDocs.Signature per .NET offre potenti strumenti per gestire in modo efficiente le firme digitali all'interno delle applicazioni .NET.
## Prerequisiti
Prima di iniziare a utilizzare GroupDocs.Signature per .NET per eliminare le firme digitali dai documenti, assicurati di disporre di quanto segue:
1. Visual Studio: installa l'IDE di Visual Studio sul tuo sistema.
2.  GroupDocs.Signature per .NET: scaricare e installare GroupDocs.Signature per .NET dal[pagina di download](https://releases.groupdocs.com/signature/net/).
3. Documento di esempio: preparare un documento di esempio contenente le firme digitali per il test.

## Importa spazi dei nomi
Per iniziare, assicurati di importare gli spazi dei nomi necessari nel tuo progetto .NET:
```csharp
using System;
using System.IO;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
```
## Passaggio 1: definire i percorsi dei file
Inizia definendo i percorsi dei file per il documento di origine e il documento di output:
```csharp
string filePath = "sample.pdf"_SIGNED_DIGITAL;
string fileName = Path.GetFileName(filePath);
string outputFilePath = Path.Combine("Your Document Directory", "DeleteDigital", fileName);
```
## Passaggio 2: copia il documento di origine
 Dal momento che`Delete` funziona con lo stesso documento, è necessario copiare il file sorgente in una nuova posizione:
```csharp
File.Copy(filePath, outputFilePath, true);
```
## Passaggio 3: inizializzare l'oggetto firma
 Inizializzare a`Signature` oggetto con il percorso del file di output:
```csharp
using (Signature signature = new Signature(outputFilePath))
{
    // Il tuo codice va qui
}
```
## Passaggio 4: ricerca delle firme digitali
Cerca le firme digitali elettroniche all'interno del documento:
```csharp
List<DigitalSignature> signatures = signature.Search<DigitalSignature>(SignatureType.Digital);
```
## Passaggio 5: Elimina la firma digitale
Se vengono trovate firme digitali, elimina la prima firma trovata:
```csharp
if (signatures.Count > 0)
{
    DigitalSignature digitalSignature = signatures[0];
    bool result = signature.Delete(digitalSignature);
    if (result)
    {
        Console.WriteLine($"Digital signature #{digitalSignature.Thumbprint} from {digitalSignature.SignTime.ToShortDateString()} was deleted from document ['{fileName}'].");
    }
    else
    {
        Helper.WriteError($"Signature was not deleted from the document! Signature# {digitalSignature.Thumbprint} was not found!");
    }
}
```

## Conclusione
La gestione delle firme digitali nelle applicazioni .NET diventa semplice con GroupDocs.Signature. Seguendo i semplici passaggi sopra descritti, puoi eliminare senza problemi le firme digitali dai tuoi documenti, garantendo l'integrità e la sicurezza dei dati.
## Domande frequenti
### Posso eliminare più firme digitali da un singolo documento?
Sì, puoi modificare il codice per scorrere tutte le firme digitali trovate ed eliminarle di conseguenza.
### GroupDocs.Signature supporta altri tipi di firme oltre a quelle digitali?
Sì, GroupDocs.Signature supporta vari tipi di firme, comprese le firme elettroniche, digitali e scritte a mano.
### GroupDocs.Signature è adatto alla gestione dei documenti a livello aziendale?
Assolutamente sì, GroupDocs.Signature è progettato per soddisfare le esigenze sia dei singoli sviluppatori che delle applicazioni di livello aziendale, offrendo funzionalità robuste e scalabilità.
### Posso personalizzare il processo di eliminazione delle firme digitali?
Sì, GroupDocs.Signature fornisce un'ampia gamma di opzioni e impostazioni per personalizzare il processo di eliminazione della firma in base alle tue esigenze specifiche.
### È disponibile una versione di prova per testare GroupDocs.Signature?
 Sì, puoi scaricare una versione di prova gratuita da[pagina delle uscite](https://releases.groupdocs.com/).