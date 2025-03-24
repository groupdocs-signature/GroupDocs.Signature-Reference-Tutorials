---
title: Firma con testo utilizzando GroupDocs.Signature per .NET
linktitle: Firmare con il testo
second_title: API GroupDocs.Signature .NET
description: Scopri come firmare documenti con testo utilizzando GroupDocs.Signature per .NET. Guida dettagliata per l'aggiunta di firme di testo a livello di codice.
weight: 17
url: /it/net/advanced-signature-techniques/sign-with-text/
---
## introduzione
Nell'era digitale, firmare elettronicamente i documenti è diventata una pratica standard, consentendo di risparmiare tempo e risorse. GroupDocs.Signature per .NET offre una soluzione completa per aggiungere firme di testo a vari formati di documenti a livello di codice. In questo tutorial ti guideremo attraverso il processo di firma di un documento con testo utilizzando GroupDocs.Signature per .NET.
## Prerequisiti
Prima di immergerci nel tutorial, assicurati di avere i seguenti prerequisiti:
1.  GroupDocs.Signature per .NET: assicurati di avere la libreria GroupDocs.Signature per .NET installata. Puoi scaricarlo da[Qui](https://releases.groupdocs.com/signature/net/).
2. Ambiente di sviluppo: disporre di un ambiente di lavoro configurato per lo sviluppo .NET.
3. Documento: prepara il documento (ad esempio PDF, Word) che desideri firmare con il testo.

## Importa spazi dei nomi
Innanzitutto, devi importare gli spazi dei nomi necessari nel tuo progetto .NET per utilizzare le funzionalità GroupDocs.Signature.
```csharp
using System;
using System.IO;
using System.Drawing;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

Suddividiamo il processo di firma di un documento con testo in più passaggi:
## Passaggio 1: caricare il documento
Carica il documento che vuoi firmare con il testo.
```csharp
string filePath = "sample.pdf"; // Percorso del documento
string fileName = Path.GetFileName(filePath);
```
## Passaggio 2: imposta il percorso del file di output
Definire il percorso del file di output in cui verrà salvato il documento firmato.
```csharp
string outputFilePath = Path.Combine("Your Document Directory", "SignWithText", fileName);
```
## Passaggio 3: crea opzioni di firma
Configura le opzioni per la firma del testo, inclusi contenuto del testo, posizione, dimensione, colore e carattere.
```csharp
TextSignOptions options = new TextSignOptions("John Smith")
{
    Left = 50, // Imposta la posizione della firma
    Top = 200,
    Width = 100, // Imposta il rettangolo della firma
    Height = 30,
    ForeColor = Color.Red, // Imposta il colore del testo
    Font = new SignatureFont { Size = 14, FamilyName = "Comic Sans MS" } // Imposta carattere
};
```
## Passaggio 4: firma il documento
Utilizzare GroupDocs.Signature per firmare il documento con le opzioni specificate e salvare il documento firmato nel percorso del file di output.
```csharp
using (Signature signature = new Signature(filePath))
{
    SignResult result = signature.Sign(outputFilePath, options); // Firmare il documento
    Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).\nFile saved at {outputFilePath}.");
}
```

## Conclusione
In questo tutorial abbiamo imparato come firmare un documento con testo utilizzando GroupDocs.Signature per .NET. Seguendo questi passaggi, puoi aggiungere in modo efficiente firme di testo ai tuoi documenti a livello di codice, migliorando la sicurezza e l'autenticità.
## Domande frequenti
### Posso personalizzare l'aspetto della firma del testo?
Sì, puoi personalizzare vari parametri come colore, carattere, dimensione e posizione della firma del testo in base alle tue preferenze.
### GroupDocs.Signature è compatibile con più formati di documenti?
Sì, GroupDocs.Signature supporta vari formati di documenti tra cui PDF, Word, Excel, PowerPoint e altri.
### Posso aggiungere più firme di testo a un singolo documento?
Assolutamente, puoi aggiungere più firme di testo a un documento, ciascuna con il proprio set di opzioni di personalizzazione.
### GroupDocs.Signature garantisce l'integrità del documento dopo la firma?
Sì, GroupDocs.Signature utilizza robusti algoritmi crittografici per garantire l'integrità del documento e prevenire manomissioni dopo la firma.
### È disponibile una versione di prova da provare prima dell'acquisto?
 Sì, puoi scaricare una versione di prova gratuita da[Qui](https://releases.groupdocs.com/) per esplorare le funzionalità prima di effettuare un acquisto.