---
title: Firma con più opzioni
linktitle: Firma con più opzioni
second_title: API GroupDocs.Signature .NET
description: Scopri come firmare documenti con più opzioni utilizzando GroupDocs.Signature per .NET. Migliora la sicurezza dei documenti con testo, codice a barre, codice QR, digitale e immagine.
type: docs
weight: 14
url: /it/net/advanced-signature-techniques/sign-with-multiple-options/
---
## introduzione
In questo tutorial esploreremo come firmare un documento utilizzando più opzioni di firma utilizzando la libreria GroupDocs.Signature per .NET. La firma di documenti con varie opzioni come testo, codice a barre, codice QR, firme digitali, immagini e metadati può fornire versatilità e migliorare la sicurezza dei documenti.
## Prerequisiti
Prima di iniziare, assicurati di possedere i seguenti prerequisiti:
1.  Libreria GroupDocs.Signature per .NET: scaricare e installare la libreria GroupDocs.Signature per .NET da[Qui](https://releases.groupdocs.com/signature/net/).
2. Ambiente di sviluppo: configurare un ambiente di sviluppo con .NET Framework installato.
3. Documento da firmare: prepara il documento (ad esempio, sample.docx) che desideri firmare.
4. Certificati e immagini: prepara tutti i certificati e le immagini richiesti per le firme digitali e di immagine.

## Importa spazi dei nomi
Innanzitutto, importa gli spazi dei nomi necessari per utilizzare la libreria GroupDocs.Signature nella tua applicazione .NET:
```csharp
using System;
using System.IO;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## Passaggio 1: caricare il documento
```csharp
string filePath = "sample.docx";
string outputFilePath = Path.Combine("Your Document Directory", "SignWithMultiple", "SignWithMultiple.docx");
using (Signature signature = new Signature(filePath))
{
    // Il tuo codice continua...
}
```
## Passaggio 2: definire le opzioni di firma
Definire diverse opzioni di firma di diversi tipi e impostazioni, come testo, codice a barre, codice QR, firme digitali, di immagini e di metadati:
```csharp
TextSignOptions textOptions = new TextSignOptions("Text signature")
{
    VerticalAlignment = VerticalAlignment.Top,
    HorizontalAlignment = HorizontalAlignment.Left
};
BarcodeSignOptions barcodeOptions = new BarcodeSignOptions("123456")
{
    EncodeType = BarcodeTypes.Code128,
    Left = 0,
    Top = 150,
    Height = 50,
    Width = 200
};
// Definire altre opzioni di firma (ad esempio, codice QR, digitale, immagine, metadati)...
```
## Passaggio 3: crea un elenco di opzioni di firma
Definire un elenco di opzioni di firma contenente tutte le opzioni definite in precedenza:
```csharp
List<SignOptions> listOptions = new List<SignOptions>();
listOptions.Add(textOptions);
listOptions.Add(barcodeOptions);
// Aggiungi altre opzioni di firma all'elenco...
```
## Passaggio 4: firma il documento
Firma il documento con l'elenco delle opzioni di firma e salva il documento firmato:
```csharp
SignResult result = signature.Sign(outputFilePath, listOptions);
Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).\nFile saved at {outputFilePath}.");
```

## Conclusione
La firma di documenti con più opzioni utilizzando GroupDocs.Signature per .NET fornisce una soluzione solida per migliorare la sicurezza e la versatilità dei documenti. Seguendo i passaggi descritti in questa esercitazione, puoi integrare facilmente vari tipi di firma nelle tue applicazioni .NET.
## Domande frequenti
### Posso utilizzare immagini personalizzate per le firme digitali?
Sì, puoi specificare immagini personalizzate per le firme digitali utilizzando la libreria GroupDocs.Signature.
### GroupDocs.Signature è compatibile con diversi formati di documenti?
Sì, GroupDocs.Signature supporta vari formati di documenti, inclusi DOCX, PDF, PPTX e altri.
### Posso personalizzare l'aspetto delle firme di testo?
Assolutamente, puoi personalizzare l'aspetto delle firme di testo, inclusi la dimensione, il colore e lo stile del carattere.
### GroupDocs.Signature fornisce la crittografia per le firme digitali?
Sì, GroupDocs.Signature offre opzioni di crittografia per le firme digitali per garantire la sicurezza dei documenti.
### È disponibile una versione di prova per GroupDocs.Signature per .NET?
 Sì, puoi scaricare una versione di prova gratuita di GroupDocs.Signature per .NET da[Qui](https://releases.groupdocs.com/).