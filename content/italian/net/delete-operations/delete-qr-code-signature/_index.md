---
"description": "Scopri come eliminare facilmente le firme con codice QR dai tuoi documenti utilizzando GroupDocs.Signature per .NET con la nostra guida passo passo per sviluppatori."
"linktitle": "Elimina la firma del codice QR dal documento"
"second_title": "API .NET GroupDocs.Signature"
"title": "Come rimuovere le firme dei codici QR dai documenti in .NET"
"url": "/it/net/delete-operations/delete-qr-code-signature/"
"weight": 16
---

# Come eliminare le firme con codice QR dai tuoi documenti

## Introduzione

Hai mai avuto bisogno di rimuovere una firma tramite codice QR da un documento a livello di codice? Che si tratti di ripulire informazioni obsolete o di preparare documenti per la ridistribuzione, saper gestire efficacemente le firme dei documenti è una competenza fondamentale per gli sviluppatori .NET.

In questa guida intuitiva, ti spiegheremo nel dettaglio come eliminare le firme con codice QR dai documenti utilizzando GroupDocs.Signature per .NET. Questa potente libreria semplifica la gestione delle firme, consentendoti di concentrarti sulla creazione di applicazioni efficaci anziché sulle problematiche di manipolazione dei documenti.

## Cosa ti servirà prima di iniziare

Prima di immergerci nel codice, assicuriamoci che tutto sia pronto:

- GroupDocs.Signature per .NET: la libreria deve essere installata nel progetto. Puoi scaricarla direttamente da [la pagina delle versioni di GroupDocs](https://releases.groupdocs.com/signature/net/).
- Un documento con codici QR: per esercitarti, prepara un documento che contenga almeno una firma con codice QR che vuoi rimuovere.
- Conoscenza di base di C#: per seguire i nostri esempi è necessario avere familiarità con i fondamenti di C#.

Una volta soddisfatti questi prerequisiti, sei pronto per iniziare a rimuovere i codici QR!

## Impostare il progetto con gli spazi dei nomi corretti

Per prima cosa, importiamo gli spazi dei nomi necessari per far funzionare correttamente il nostro codice:

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

Queste importazioni ci danno accesso a tutte le funzionalità di cui abbiamo bisogno dalla libreria GroupDocs.Signature, nonché ad alcune classi .NET essenziali per la gestione dei file.

## Fase 1: Dove sono i tuoi file? Impostazione dei percorsi dei documenti

Iniziamo definendo dove si trovano i nostri documenti e dove vogliamo salvare la versione modificata:

```csharp
// Il percorso alla directory dei documenti.
string filePath = "sample_multiple_signatures.docx";
string fileName = Path.GetFileName(filePath);

// Definire il percorso del file di output per il documento modificato.
string outputFilePath = Path.Combine("Your Document Directory", "DeleteQRCode", fileName);

// Copiare il file sorgente poiché il metodo Delete funziona con lo stesso Documento.
File.Copy(filePath, outputFilePath, true);
```

Si noti che stiamo creando una copia del documento originale. Questo è importante perché il processo di eliminazione della firma modificherà direttamente il file e vogliamo sempre preservare i documenti originali.

## Passaggio 2: creazione di un oggetto firma con cui lavorare

Ora creeremo un oggetto Signature che si connetterà al nostro documento:

```csharp
using (Signature signature = new Signature(outputFilePath))
{
    // Crea opzioni per la ricerca delle firme dei codici QR.
    QrCodeSearchOptions options = new QrCodeSearchOptions();
    
    // Cerca le firme con codice QR nel documento.
    List<QrCodeSignature> signatures = signature.Search<QrCodeSignature>(options);
```

Questo codice inizializza l'oggetto Signature con il nostro documento e poi cerca tutte le firme QR code presenti in esso. La ricerca restituisce un elenco di tutte le firme QR code trovate.

## Passaggio 3: Ci sono codici QR da eliminare?

Prima di tentare di eliminare qualsiasi cosa, dovremmo verificare se sono effettivamente presenti codici QR:

```csharp
    if (signatures.Count > 0)
    {
        // Ottieni la prima firma con codice QR trovata nel documento.
        QrCodeSignature qrCodeSignature = signatures[0];
```

Questo semplice controllo garantisce che si proceda solo se nel documento è presente almeno una firma con codice QR. In questo esempio, ci stiamo concentrando sul primo codice QR trovato, ma è possibile modificarlo facilmente per gestire più firme, se necessario.

## Passaggio 4: rimozione del codice QR dal documento

Ora passiamo all'evento principale: l'eliminazione effettiva del codice QR:

```csharp
        // Elimina la firma con codice QR dal documento.
        bool result = signature.Delete(qrCodeSignature);
        
        if (result)
        {
            Console.WriteLine($"Signature with QR-Code '{qrCodeSignature.Text}' and encode type '{qrCodeSignature.EncodeType.TypeName}' was deleted from document ['{fileName}'].");
        }
        else
        {
            Console.WriteLine($"Signature was not deleted from the document! Signature with QR-Code '{qrCodeSignature.Text}' and encode type '{qrCodeSignature.EncodeType.TypeName}' was not found!");
        }
    }
}
```

Il codice elimina la firma e fornisce un feedback sull'esito positivo dell'operazione. Questo feedback è fondamentale per il debug e per confermare che il codice funzioni come previsto.

## Cosa abbiamo realizzato?

Congratulazioni! Hai appena imparato come rimuovere le firme con codice QR dai documenti utilizzando GroupDocs.Signature per .NET. Questa competenza apre numerose possibilità per la gestione dei documenti nelle tue applicazioni.

Con solo poche righe di codice, ora puoi ripulire i documenti a livello di programmazione rimuovendo le firme dei codici QR obsolete o non necessarie, assicurandoti che i tuoi documenti contengano sempre solo le informazioni rilevanti.

## Domande frequenti che potresti avere

### Posso eliminare più codici QR contemporaneamente?

Assolutamente! Invece di eliminare semplicemente la prima firma trovata, potresti scorrere l'intero elenco delle firme ed eliminarle una per una in questo modo:

```csharp
foreach(var qrSignature in signatures)
{
    signature.Delete(qrSignature);
}
```

### Quali altri tipi di firme posso gestire con GroupDocs.Signature?

GroupDocs.Signature è incredibilmente versatile e supporta vari tipi di firma, tra cui:
- Firme di testo
- Firme delle immagini
- Firme con codice a barre
- Firme digitali
- E molti altri ancora!

### Funzionerà con tutti i miei formati di documenti?

Sarai lieto di sapere che GroupDocs.Signature funziona con un'ampia gamma di formati di documenti, tra cui:
- documenti PDF
- Documenti di Microsoft Word
- fogli di calcolo Excel
- Presentazioni PowerPoint
- molti altri

### Posso cercare codici QR specifici anziché eliminarli tutti?

Sì! Il `QrCodeSearchOptions` La classe offre diverse proprietà per filtrare la ricerca. Ad esempio, è possibile cercare codici QR contenenti testo specifico o codificati con formati particolari.

### Esiste un modo per provare GroupDocs.Signature prima di acquistarlo?

Sì, puoi scaricare una versione di prova gratuita da [il sito web GroupDocs](https://releases.groupdocs.com/) per testarlo con i tuoi casi d'uso specifici prima di prendere un impegno.