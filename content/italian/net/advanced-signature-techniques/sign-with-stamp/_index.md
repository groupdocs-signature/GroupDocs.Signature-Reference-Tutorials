---
title: Firma con Stamp utilizzando GroupDocs.Signature
linktitle: Firma con timbro
second_title: API GroupDocs.Signature .NET
description: Scopri come aggiungere facilmente timbri ai tuoi documenti .NET con GroupDocs.Signature per .NET. Migliora la sicurezza dei documenti.
type: docs
weight: 16
url: /it/net/advanced-signature-techniques/sign-with-stamp/
---
## introduzione
In questo tutorial ti guideremo attraverso il processo di firma di un documento con un timbro utilizzando GroupDocs.Signature per .NET. Seguendo queste istruzioni passo passo, sarai in grado di aggiungere facilmente un timbro firma ai tuoi documenti.
## Prerequisiti
Prima di iniziare, assicurati di possedere i seguenti prerequisiti:
1.  GroupDocs.Signature per .NET SDK: scarica e installa l'SDK da[sito web](https://releases.groupdocs.com/signature/net/).
2. Ambiente di sviluppo: assicurati di disporre di un ambiente di sviluppo adatto configurato per lo sviluppo .NET.
3. Documento da firmare: prepara il documento (ad esempio PDF) che desideri firmare con un timbro.

## Importazione di spazi dei nomi
Inizia importando gli spazi dei nomi necessari nel tuo progetto:
```csharp
using System;
using System.IO;
using System.Drawing;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## Passaggio 1: caricare il documento
```csharp
string filePath = "sample.pdf";
using (Signature signature = new Signature(filePath))
{
    // Il tuo codice va qui
}
```
## Passaggio 2: impostare le opzioni del segno del timbro
```csharp
StampSignOptions options = new StampSignOptions()
{
    Left = 50,
    Top = 150,                    
    Width = 200,
    Height = 200
};
```
## Passaggio 3: configurare l'aspetto del timbro
```csharp
StampLine outerLine = new StampLine();
outerLine.Text = " * European Union ";
outerLine.TextRepeatType = StampTextRepeatType.FullTextRepeat;
outerLine.Font.Size = 12;
outerLine.Height = 22;
outerLine.TextBottomIntent = 6;
outerLine.TextColor = Color.WhiteSmoke;
outerLine.BackgroundColor = Color.DarkSlateBlue;
options.OuterLines.Add(outerLine);
StampLine innerLine = new StampLine();
innerLine.Text = "John Smith";
innerLine.TextColor = Color.MediumVioletRed;
innerLine.Font.Size = 20;
innerLine.Font.Bold = true;
innerLine.Height = 40;
options.InnerLines.Add(innerLine);
```
## Passaggio 4: firma il documento
```csharp
string outputFilePath = Path.Combine("Your Document Directory", "SignWithStamp", fileName);
SignResult result = signature.Sign(outputFilePath, options);
Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).\nFile saved at {outputFilePath}.");
```

## Conclusione
Aggiungere firme ai tuoi documenti utilizzando GroupDocs.Signature per .NET è un processo semplice, come dimostrato in questo tutorial. Con i passaggi forniti, puoi facilmente migliorare la sicurezza e l'autenticità dei tuoi documenti.
## Domande frequenti
### Posso personalizzare l'aspetto della firma del timbro?
Sì, puoi personalizzare vari aspetti come testo, carattere, colore e posizionamento della firma del timbro in base alle tue esigenze.
### GroupDocs.Signature supporta la firma di più formati di documenti?
Sì, GroupDocs.Signature supporta un'ampia gamma di formati di documenti tra cui PDF, Microsoft Word, Excel, PowerPoint e altri.
### È disponibile una versione di prova per GroupDocs.Signature?
 Sì, puoi accedere alla versione di prova gratuita da[sito web](https://releases.groupdocs.com/).
### Posso aggiungere più firme a un singolo documento?
Assolutamente sì, GroupDocs.Signature ti consente di aggiungere più firme, inclusi timbri, testo, immagini e firme digitali, a un singolo documento.
### Dove posso trovare supporto se riscontro problemi durante l'implementazione?
 Puoi trovare supporto e assistenza nel forum della community GroupDocs.Signature[Qui](https://forum.groupdocs.com/c/signature/13).