---
title: Cerca firme multiple
linktitle: Cerca firme multiple
second_title: API GroupDocs.Signature .NET
description: Scopri come cercare più firme nei documenti .NET utilizzando GroupDocs.Signature per un'efficiente sicurezza e integrità dei documenti.
weight: 14
url: /it/net/signature-searching/search-for-multiple-signatures/
---

# Cerca firme multiple

## introduzione
GroupDocs.Signature per .NET è una potente libreria che consente agli sviluppatori di aggiungere, cercare e rimuovere vari tipi di firme nei formati di documenti più diffusi utilizzando le applicazioni .NET. In questo tutorial ci concentreremo sulla ricerca di più firme all'interno di un documento utilizzando GroupDocs.Signature per .NET.
## Prerequisiti
Prima di iniziare, assicurati di avere i seguenti prerequisiti:
- Visual Studio installato nel sistema.
- Conoscenza base del linguaggio di programmazione C#.
- Libreria GroupDocs.Signature per .NET installata nel tuo progetto. Puoi scaricarlo da[Qui](https://releases.groupdocs.com/signature/net/).

## Importa spazi dei nomi
Innanzitutto, è necessario importare gli spazi dei nomi necessari per accedere alle classi e ai metodi forniti da GroupDocs.Signature per .NET.
```csharp
using System;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## Passaggio 1: caricare il documento
Carica il documento in cui desideri cercare più firme. Assicurati di fornire il percorso file corretto.
```csharp
string filePath = "sample_multiple_signatures.docx";
using (Signature signature = new Signature(filePath))
{
    // Il tuo codice va qui
}
```
## Passaggio 2: definire le opzioni di ricerca
Definisci le opzioni di ricerca per vari tipi di firme come testo, digitale, codice a barre, codice QR e metadati. Puoi specificare criteri di ricerca come il testo da abbinare, il tipo di corrispondenza e la ricerca in tutte le pagine.
```csharp
// Definire le opzioni di ricerca
TextSearchOptions textOptions = new TextSearchOptions()
{
    AllPages = true
};
DigitalSearchOptions digitalOptions = new DigitalSearchOptions()
{
    AllPages = true
};
BarcodeSearchOptions barcodeOptions = new BarcodeSearchOptions()
{
    AllPages = true,
    Text = "123456",
    MatchType = TextMatchType.Exact
};
QrCodeSearchOptions qrCodeOptions = new QrCodeSearchOptions()
{
    AllPages = true,
    Text = "John",
    MatchType = TextMatchType.Contains
};
MetadataSearchOptions metadataOptions = new MetadataSearchOptions();
```
## Passaggio 3: aggiungi opzioni di ricerca all'elenco
Aggiunge le opzioni di ricerca definite a un elenco.
```csharp
// Aggiungi opzioni all'elenco
List<SearchOptions> listOptions = new List<SearchOptions>();
listOptions.Add(textOptions);
listOptions.Add(barcodeOptions);
listOptions.Add(qrCodeOptions);
listOptions.Add(metadataOptions);
listOptions.Add(digitalOptions);
```
## Passaggio 4: ricerca delle firme
Cerca le firme nel documento utilizzando le opzioni di ricerca definite.
```csharp
// Cerca firme nel documento
SearchResult result = signature.Search(listOptions);
if (result.Signatures.Count > 0)
{
    Console.WriteLine($"\nSource document ['{filePath}'] contains following signatures.");
    foreach (var resSignature in result.Signatures)
    {
        Console.WriteLine($"Signature found at page {resSignature.PageNumber} with type {resSignature.SignatureType} and Id#: {resSignature.SignatureId}");
    }
}
else
{
    Helper.WriteError("No one signature was found.");
}
```

## Conclusione
In questo tutorial abbiamo imparato come cercare più firme all'interno di un documento utilizzando GroupDocs.Signature per .NET. Seguendo i passaggi forniti, puoi individuare in modo efficiente vari tipi di firme nei tuoi documenti, migliorando la sicurezza e l'integrità dei documenti.
## Domande frequenti
### Posso cercare firme in diversi formati di documenti?
Sì, GroupDocs.Signature per .NET supporta un'ampia gamma di formati di documenti tra cui Word, PDF, Excel e altri.
### È possibile personalizzare i criteri di ricerca per le firme?
Assolutamente, puoi personalizzare i criteri di ricerca in base alle tue esigenze, ad esempio specificando corrispondenze di testo esatte o cercando in tutte le pagine.
### GroupDocs.Signature per .NET offre supporto per le firme digitali?
Sì, puoi cercare firme digitali e altri tipi come firme di testo, codici a barre e codici QR.
### Posso integrare facilmente la funzionalità di ricerca delle firme nelle mie applicazioni .NET?
Sì, GroupDocs.Signature per .NET fornisce un'API semplice che semplifica il processo di integrazione.
### Dove posso trovare ulteriore supporto o assistenza?
 È possibile visitare il forum GroupDocs.Signature[Qui](https://forum.groupdocs.com/c/signature/13) per qualsiasi domanda o assistenza.