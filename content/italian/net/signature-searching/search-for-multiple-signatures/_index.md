---
"description": "Scopri come cercare più tipi di firma nei documenti utilizzando GroupDocs.Signature per .NET. Guida completa con esempi di codice per una maggiore sicurezza dei documenti."
"linktitle": "Cerca firme multiple"
"second_title": "API .NET GroupDocs.Signature"
"title": "Cerca più tipi di firma nei documenti"
"url": "/it/net/signature-searching/search-for-multiple-signatures/"
"weight": 14
---

## Introduzione

Nei moderni sistemi di gestione documentale, la possibilità di cercare e convalidare più tipi di firma all'interno di un singolo documento è sempre più importante. Le organizzazioni spesso utilizzano diversi tipi di firma, come firme digitali, firme testuali, codici a barre, codici QR e altro ancora, per migliorare la sicurezza dei documenti e semplificare i processi di verifica. GroupDocs.Signature per .NET fornisce un potente framework che consente agli sviluppatori di implementare funzionalità complete di ricerca delle firme in diversi formati di documento.

Questo tutorial ti guiderà attraverso il processo di ricerca di più tipi di firma all'interno dei documenti utilizzando GroupDocs.Signature per .NET, offrendo spiegazioni dettagliate ed esempi di codice pratici.

## Prerequisiti

Prima di procedere all'implementazione della funzionalità di ricerca di più firme, assicurati di disporre dei seguenti prerequisiti:

1. Ambiente di sviluppo: Visual Studio o qualsiasi altro ambiente di sviluppo .NET preferito installato sul sistema.
  
2. GroupDocs.Signature per .NET: Scarica e installa la libreria GroupDocs.Signature per .NET da [Qui](https://releases.groupdocs.com/signature/net/).

3. Conoscenza di base di C#: familiarità con il linguaggio di programmazione C# e i concetti del framework .NET.

4. Documenti campione: preparare documenti di prova contenenti vari tipi di firme a scopo di verifica.

## Importa spazi dei nomi

Per iniziare, importare gli spazi dei nomi necessari per accedere alla funzionalità GroupDocs.Signature:

```csharp
using System;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

Ora, scomponiamo il processo di ricerca di più tipi di firma in passaggi chiari e gestibili:

## Passaggio 1: caricare il documento

Per prima cosa, carica il documento contenente le firme che vuoi cercare:

```csharp
string filePath = "sample_multiple_signatures.docx";
using (Signature signature = new Signature(filePath))
{
    // Qui verrà aggiunto il codice di ricerca multi-firma
}
```

## Passaggio 2: definire le opzioni di ricerca per diversi tipi di firma

Crea opzioni di ricerca per ogni tipo di firma che desideri ricercare:

```csharp
// Definisci le opzioni di ricerca per le firme di testo
TextSearchOptions textOptions = new TextSearchOptions
{
    AllPages = true,  // Cerca in tutte le pagine
    Text = "Signature",  // Facoltativo: testo da trovare
    MatchType = TextMatchType.Contains  // Criteri di corrispondenza
};

// Definisci le opzioni di ricerca per le firme digitali
DigitalSearchOptions digitalOptions = new DigitalSearchOptions
{
    AllPages = true
};

// Definisci le opzioni di ricerca per le firme con codice a barre
BarcodeSearchOptions barcodeOptions = new BarcodeSearchOptions
{
    AllPages = true,
    Text = "123456",  // Facoltativo: testo del codice a barre da abbinare
    MatchType = TextMatchType.Exact  // Criteri di corrispondenza
};

// Definisci le opzioni di ricerca per le firme dei codici QR
QrCodeSearchOptions qrCodeOptions = new QrCodeSearchOptions
{
    AllPages = true,
    Text = "John",  // Facoltativo: testo del codice QR da abbinare
    MatchType = TextMatchType.Contains  // Criteri di corrispondenza
};

// Definisci le opzioni di ricerca per le firme dei metadati
MetadataSearchOptions metadataOptions = new MetadataSearchOptions();
```

## Passaggio 3: aggiungere opzioni a una raccolta

Aggiungi tutte le opzioni di ricerca a una raccolta:

```csharp
// Crea un elenco per contenere tutte le opzioni di ricerca
List<SearchOptions> searchOptions = new List<SearchOptions>
{
    textOptions,
    digitalOptions,
    barcodeOptions,
    qrCodeOptions,
    metadataOptions
};
```

## Fase 4: Eseguire la ricerca ed elaborare i risultati

Eseguire la ricerca utilizzando le opzioni di ricerca combinate ed elaborare i risultati:

```csharp
// Cerca tutti i tipi di firma utilizzando le opzioni definite
SearchResult result = signature.Search(searchOptions);

// Controlla se sono state trovate firme
if (result.Signatures.Count > 0)
{
    Console.WriteLine($"\nSource document ['{filePath}'] contains {result.Signatures.Count} signature(s):");
    
    // Scorrere le firme trovate
    foreach (var foundSignature in result.Signatures)
    {
        Console.WriteLine($"Signature found: Type: {foundSignature.SignatureType}, Page: {foundSignature.PageNumber}, ID: {foundSignature.SignatureId}");
        
        // Tipi di firma specifici del processo
        if (foundSignature is TextSignature textSignature)
        {
            Console.WriteLine($"Text: '{textSignature.Text}'");
        }
        else if (foundSignature is BarcodeSignature barcodeSignature)
        {
            Console.WriteLine($"Barcode Type: {barcodeSignature.EncodeType.TypeName}, Text: '{barcodeSignature.Text}'");
        }
        else if (foundSignature is QrCodeSignature qrCodeSignature)
        {
            Console.WriteLine($"QR Code Type: {qrCodeSignature.EncodeType.TypeName}, Text: '{qrCodeSignature.Text}'");
        }
        else if (foundSignature is DigitalSignature digitalSignature)
        {
            Console.WriteLine($"Certificate: {digitalSignature.Certificate?.SubjectName}, Valid: {digitalSignature.IsValid}");
        }
        else if (foundSignature is MetadataSignature metadataSignature)
        {
            Console.WriteLine($"Metadata: Name: {metadataSignature.Name}, Value: {metadataSignature.Value}");
        }
    }
}
else
{
    Console.WriteLine("No signatures were found in the document.");
}
```

## Esempio completo

Ecco un esempio completo e funzionante che dimostra come cercare più tipi di firma in un documento:

```csharp
using System;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;

namespace MultiSignatureSearch
{
    class Program
    {
        static void Main(string[] args)
        {
            // Percorso del documento
            string filePath = "sample_multiple_signatures.docx";
            
            // Inizializza l'istanza della firma
            using (Signature signature = new Signature(filePath))
            {
                try
                {
                    // Definisci le opzioni di ricerca per le firme di testo
                    TextSearchOptions textOptions = new TextSearchOptions
                    {
                        AllPages = true,
                        MatchType = TextMatchType.Contains
                    };

                    // Definisci le opzioni di ricerca per le firme digitali
                    DigitalSearchOptions digitalOptions = new DigitalSearchOptions
                    {
                        AllPages = true
                    };

                    // Definisci le opzioni di ricerca per le firme con codice a barre
                    BarcodeSearchOptions barcodeOptions = new BarcodeSearchOptions
                    {
                        AllPages = true
                    };

                    // Definisci le opzioni di ricerca per le firme dei codici QR
                    QrCodeSearchOptions qrCodeOptions = new QrCodeSearchOptions
                    {
                        AllPages = true
                    };

                    // Definisci le opzioni di ricerca per le firme dei metadati
                    MetadataSearchOptions metadataOptions = new MetadataSearchOptions();

                    // Crea un elenco per contenere tutte le opzioni di ricerca
                    List<SearchOptions> searchOptions = new List<SearchOptions>
                    {
                        textOptions,
                        digitalOptions,
                        barcodeOptions,
                        qrCodeOptions,
                        metadataOptions
                    };

                    // Cerca tutti i tipi di firma
                    SearchResult result = signature.Search(searchOptions);

                    // Controlla se sono state trovate firme
                    if (result.Signatures.Count > 0)
                    {
                        Console.WriteLine($"\nSource document ['{filePath}'] contains {result.Signatures.Count} signature(s):");
                        
                        // Risultati del processo per tipo di firma
                        foreach (var foundSignature in result.Signatures)
                        {
                            Console.WriteLine($"Signature found: Type: {foundSignature.SignatureType}, Page: {foundSignature.PageNumber}");
                            
                            // Tipi di firma specifici del processo
                            switch (foundSignature.SignatureType)
                            {
                                case SignatureType.Text:
                                    var textSignature = foundSignature as TextSignature;
                                    Console.WriteLine($"Text: '{textSignature.Text}'");
                                    break;
                                    
                                case SignatureType.Barcode:
                                    var barcodeSignature = foundSignature as BarcodeSignature;
                                    Console.WriteLine($"Barcode Type: {barcodeSignature.EncodeType.TypeName}, Text: '{barcodeSignature.Text}'");
                                    break;
                                    
                                case SignatureType.QrCode:
                                    var qrCodeSignature = foundSignature as QrCodeSignature;
                                    Console.WriteLine($"QR Code Type: {qrCodeSignature.EncodeType.TypeName}, Text: '{qrCodeSignature.Text}'");
                                    break;
                                    
                                case SignatureType.Digital:
                                    var digitalSignature = foundSignature as DigitalSignature;
                                    Console.WriteLine($"Certificate: {digitalSignature.Certificate?.SubjectName}, Valid: {digitalSignature.IsValid}");
                                    break;
                                    
                                case SignatureType.Metadata:
                                    var metadataSignature = foundSignature as MetadataSignature;
                                    Console.WriteLine($"Metadata: Name: {metadataSignature.Name}, Value: {metadataSignature.Value}");
                                    break;
                            }
                            
                            Console.WriteLine(); // Aggiungi un'interruzione di riga tra le firme
                        }
                    }
                    else
                    {
                        Console.WriteLine("No signatures were found in the document.");
                    }
                }
                catch (Exception ex)
                {
                    Console.WriteLine($"Error occurred: {ex.Message}");
                }
            }
            
            Console.WriteLine("Press any key to exit...");
            Console.ReadKey();
        }
    }
}
```

## Tecniche avanzate di ricerca multi-firma

### Filtraggio dei risultati della ricerca

È possibile implementare un filtro avanzato per restringere i risultati della ricerca:

```csharp
// Filtra i risultati per numero di pagina
var signaturesOnFirstPage = result.Signatures.FindAll(s => s.PageNumber == 1);

// Filtra i risultati per tipo di firma
var digitalSignatures = result.Signatures.FindAll(s => s.SignatureType == SignatureType.Digital);
var qrCodeSignatures = result.Signatures.FindAll(s => s.SignatureType == SignatureType.QrCode);

// Filtra le firme di testo contenenti contenuti specifici
var approvalSignatures = result.Signatures
    .FindAll(s => s is TextSignature && ((TextSignature)s).Text.Contains("Approved"));
```

### Convalida di più firme

Implementare la logica di convalida per diversi tipi di firma:

```csharp
bool ValidateAllSignatures(SearchResult result)
{
    bool isDocumentValid = true;
    
    // Verificare se il documento ha una firma digitale valida
    bool hasValidDigitalSignature = result.Signatures
        .Any(s => s is DigitalSignature && ((DigitalSignature)s).IsValid);
    
    if (!hasValidDigitalSignature)
    {
        Console.WriteLine("Warning: Document does not contain a valid digital signature");
        isDocumentValid = false;
    }
    
    // Controlla se il documento ha il codice QR richiesto
    bool hasRequiredQRCode = result.Signatures
        .Any(s => s is QrCodeSignature && ((QrCodeSignature)s).Text.Contains("Auth-Code"));
    
    if (!hasRequiredQRCode)
    {
        Console.WriteLine("Warning: Document does not contain the required authentication QR code");
        isDocumentValid = false;
    }
    
    return isDocumentValid;
}
```

### Ricerca con elaborazione personalizzata

È possibile definire una logica di elaborazione personalizzata per le operazioni di ricerca:

```csharp
// Crea opzioni di ricerca con elaborazione personalizzata
TextSearchOptions textOptions = new TextSearchOptions
{
    AllPages = true,
    
    // Definisci l'elaborazione personalizzata utilizzando un delegato
    ProcessCompleted = (signature) =>
    {
        // Logica di convalida personalizzata: accetta solo le firme sulle pagine specificate
        TextSignature textSignature = signature as TextSignature;
        return textSignature != null && (textSignature.PageNumber == 1 || textSignature.PageNumber == 2);
    }
};
```

## Conclusione

In questa guida completa, abbiamo esplorato come cercare più tipi di firma all'interno dei documenti utilizzando GroupDocs.Signature per .NET. Dalla configurazione delle opzioni di ricerca per diversi tipi di firma all'elaborazione e alla convalida dei risultati, ora hai le conoscenze necessarie per implementare una solida funzionalità di ricerca delle firme nelle tue applicazioni .NET.

La possibilità di cercare più tipi di firma contemporaneamente migliora i processi di verifica dei documenti, rafforza le misure di sicurezza e semplifica i flussi di lavoro di convalida dei documenti. GroupDocs.Signature offre un framework potente e flessibile per lavorare con diversi tipi di firma in diversi formati di documento, rendendolo una scelta eccellente per le applicazioni di elaborazione dei documenti.

## Domande frequenti

### Posso cercare firme nei documenti protetti da password?

Sì, GroupDocs.Signature supporta la ricerca di firme nei documenti protetti da password. È possibile specificare la password durante l'inizializzazione. `Signature` oggetto:

```csharp
LoadOptions loadOptions = new LoadOptions { Password = "your_password" };
using (Signature signature = new Signature(filePath, loadOptions))
{
    // Cerca firme
}
```

### Quali formati di documento sono supportati per la ricerca delle firme?

GroupDocs.Signature supporta un'ampia gamma di formati di documenti, tra cui PDF, documenti Microsoft Office (Word, Excel, PowerPoint), formati OpenOffice, immagini e altro ancora.

### Posso limitare la ricerca a pagine specifiche di un documento?

Sì, ogni tipo di opzione di ricerca ha delle proprietà che consentono di specificare in quali pagine effettuare la ricerca:

```csharp
TextSearchOptions options = new TextSearchOptions
{
    AllPages = false,  // Non cercare in tutte le pagine
    PageNumber = 1,    // Cerca solo nella pagina 1
    
    // Oppure specifica più pagine
    PagesSetup = new PagesSetup { Pages = new List<int> { 1, 3, 5 } }
};
```

### Come posso ottimizzare le prestazioni durante la ricerca in documenti di grandi dimensioni?

Per i documenti di grandi dimensioni, è possibile ottimizzare le prestazioni:

1. Limitare la ricerca a pagine o intervalli di pagine specifici
2. Utilizzo di criteri di ricerca più specifici per ridurre il numero di potenziali corrispondenze
3. Implementazione della paginazione nella visualizzazione dei risultati
4. Cercare un tipo di firma alla volta se non sono necessari risultati simultanei

### Posso estendere GroupDocs.Signature per supportare tipi di firma personalizzati?

Sebbene GroupDocs.Signature fornisca supporto integrato per i tipi di firma più comuni, è possibile estenderne le funzionalità:

1. Creazione di classi di opzioni di ricerca personalizzate derivate da `SearchOptions`
2. Implementazione della logica di elaborazione personalizzata utilizzando `ProcessCompleted` delegare
3. Sviluppo di classi wrapper che combinano più ricerche di firme con logica aziendale avanzata

## Vedi anche

* [Riferimento API](https://reference.groupdocs.com/signature/net/)
* [Esempi di codice su GitHub](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
* [Documentazione del prodotto](https://docs.groupdocs.com/signature/net/)
* [Pagina del prodotto](https://products.groupdocs.com/signature/net/)
* [Scarica l'ultima versione](https://releases.groupdocs.com/signature/net/)
* [Articoli del blog](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
* [Forum di supporto gratuito](https://forum.groupdocs.com/c/signature/13)
* [Licenza temporanea](https://purchase.groupdocs.com/temporary-license/)