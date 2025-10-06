---
"description": "Integra le firme dei metadati nei documenti PDF utilizzando GroupDocs.Signature per .NET. Impara a incorporare informazioni sull'autore, timestamp e dati personalizzati per migliorare l'autenticità e la tracciabilità dei PDF."
"linktitle": "Firma PDF con metadati"
"second_title": "API .NET GroupDocs.Signature"
"title": "Aggiungere firme di metadati ai documenti PDF in C# .NET"
"url": "/it/net/document-signing/sign-pdf-with-metadata/"
"weight": 11
type: docs
---
## Introduzione

documenti PDF (Portable Document Format) sono ampiamente utilizzati in diversi settori grazie alla loro coerenza e indipendenza dalla piattaforma. Garantire l'autenticità e la tracciabilità di questi documenti è fondamentale in molti ambienti professionali. Un modo efficace per raggiungere questo obiettivo è incorporare metadati nei file PDF stessi.

In questo tutorial completo, esploreremo come firmare documenti PDF con metadati utilizzando GroupDocs.Signature per .NET. Le firme con metadati consentono di incorporare informazioni aggiuntive nel documento, come dettagli sull'autore, timestamp di creazione, identificatori del documento e valori personalizzati, senza alterarne visibilmente l'aspetto.

## Prerequisiti

Prima di iniziare, assicurati di avere a disposizione quanto segue:

1. [GroupDocs.Signature per .NET](https://releases.groupdocs.com/signature/net/) - Scarica e installa la libreria
2. Ambiente di sviluppo: Visual Studio o qualsiasi altro IDE compatibile con .NET
3. Documento PDF - Un file PDF di esempio per la firma
4. Conoscenza di base di C# - Familiarità con il linguaggio di programmazione C#

## Importa spazi dei nomi

Per iniziare, importare gli spazi dei nomi necessari per accedere alla funzionalità GroupDocs.Signature:

```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

## Passaggio 1: impostare i percorsi dei file

Per prima cosa, definisci il percorso del tuo documento PDF e specifica dove vuoi salvare l'output firmato:

```csharp
// Specifica il percorso del tuo documento PDF
string filePath = "sample.pdf";

// Definisci la directory di output e il percorso del file
string outputDirectory = "Your Document Directory";
string outputFilePath = Path.Combine(outputDirectory, "SignPdfWithMetadata", "SignedWithMetadata.pdf");

// Assicurarsi che la directory di output esista
Directory.CreateDirectory(Path.GetDirectoryName(outputFilePath));
```

## Passaggio 2: inizializzare l'oggetto firma

Crea un'istanza della classe Signature con il tuo documento PDF sorgente:

```csharp
using (Signature signature = new Signature(filePath))
{
    // Il codice per la firma andrà qui
}
```

## Passaggio 3: definire le opzioni dei metadati

Crea e configura le opzioni dei metadati, aggiungendo vari tipi di firme dei metadati:

```csharp
// Crea oggetto opzioni metadati
MetadataSignOptions options = new MetadataSignOptions();

// Aggiungi vari tipi di metadati utilizzando l'interfaccia fluida
options
    .Add(new PdfMetadataSignature("Author", "Mr.Sherlock Holmes")) // Valore stringa
    .Add(new PdfMetadataSignature("CreatedOn", DateTime.Now))       // Valore DateTime
    .Add(new PdfMetadataSignature("DocumentId", 123456))            // Valore intero
    .Add(new PdfMetadataSignature("SignatureId", 123.456D))         // Doppio valore
    .Add(new PdfMetadataSignature("Amount", 123.456M))              // Valore decimale
    .Add(new PdfMetadataSignature("Total", 123.456F));              // Valore float
```

## Passaggio 4: firmare il PDF con i metadati

Applica le firme dei metadati al documento PDF e salva il risultato:

```csharp
// Firma il documento e salvalo nel percorso di output
SignResult result = signature.Sign(outputFilePath, options);

// Visualizza messaggio di successo
Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} metadata signature(s).");
Console.WriteLine($"Signed document saved at: {outputFilePath}");
```

## Esempio completo

Ecco l'esempio di codice completo che riunisce tutti i passaggi:

```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;

namespace SignPdfWithMetadataExample
{
    class Program
    {
        static void Main(string[] args)
        {
            // Specificare i percorsi dei file
            string filePath = "sample.pdf";
            string outputFilePath = Path.Combine("Your Document Directory", "SignPdfWithMetadata", "SignedWithMetadata.pdf");
            
            // Assicurarsi che la directory di output esista
            Directory.CreateDirectory(Path.GetDirectoryName(outputFilePath));

            // Firma il PDF con i metadati
            using (Signature signature = new Signature(filePath))
            {
                // Crea oggetto opzioni metadati
                MetadataSignOptions options = new MetadataSignOptions();
                
                // Aggiungere diversi tipi di firme di metadati
                options
                    .Add(new PdfMetadataSignature("Author", "Mr.Sherlock Holmes")) // Valore stringa
                    .Add(new PdfMetadataSignature("CreatedOn", DateTime.Now))       // Valore DateTime
                    .Add(new PdfMetadataSignature("DocumentId", 123456))            // Valore intero
                    .Add(new PdfMetadataSignature("SignatureId", 123.456D))         // Doppio valore
                    .Add(new PdfMetadataSignature("Amount", 123.456M))              // Valore decimale
                    .Add(new PdfMetadataSignature("Total", 123.456F));              // Valore float
                
                // Firma il documento e salvalo nel file
                SignResult result = signature.Sign(outputFilePath, options);
                
                // Visualizza i risultati
                Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).");
                Console.WriteLine($"File saved at {outputFilePath}.");
            }
        }
    }
}
```

## Operazioni avanzate sui metadati PDF

### Aggiunta di metadati personalizzati con supporto dello spazio dei nomi

I documenti PDF supportano metadati personalizzati con supporto dello spazio dei nomi XML:

```csharp
// Aggiungi metadati personalizzati con namespace
options.Add(new PdfMetadataSignature("CustomProperty", "Custom Value")
{
    NamespaceUri = "http://your-namespace.com/schema"
});
```

### Ricerca di metadati nei PDF firmati

Dopo la firma, potresti voler verificare o estrarre i metadati:

```csharp
// Creare opzioni di ricerca per i metadati
MetadataSearchOptions searchOptions = new MetadataSearchOptions();

// Cerca firme di metadati
SearchResult searchResult = signature.Search(searchOptions);

// Visualizza le firme trovate
Console.WriteLine($"Found {searchResult.Signatures.Count} metadata signatures:");
foreach (var foundSignature in searchResult.Signatures)
{
    MetadataSignature metadataSignature = foundSignature as MetadataSignature;
    if (metadataSignature != null)
    {
        Console.WriteLine($"- {metadataSignature.Name}: {metadataSignature.Value} ({metadataSignature.Value.GetType().Name})");
    }
}
```

### Lavorare con i metadati PDF standard

I documenti PDF dispongono di campi di metadati standard a cui è possibile accedere e che possono essere modificati:

```csharp
// Imposta i campi standard dei metadati PDF
options
    .Add(new PdfMetadataSignature("Title", "Important Contract"))
    .Add(new PdfMetadataSignature("Subject", "Legal Agreement"))
    .Add(new PdfMetadataSignature("Keywords", "contract, agreement, legal, binding"))
    .Add(new PdfMetadataSignature("Creator", "Legal Department"))
    .Add(new PdfMetadataSignature("Producer", "GroupDocs.Signature"));
```

## Conclusione

In questo tutorial, hai imparato come firmare documenti PDF con metadati utilizzando GroupDocs.Signature per .NET. L'incorporazione di metadati nei file PDF è un ottimo modo per migliorare l'autenticità dei documenti, aggiungere informazioni critiche e ottimizzare i flussi di lavoro di gestione dei documenti.

Le firme basate sui metadati nei PDF sono particolarmente utili negli ambienti aziendali in cui la tracciabilità e la verifica dell'autenticità dei documenti sono essenziali. I metadati incorporati possono includere informazioni sull'origine del documento, l'autore, l'ora di creazione, la versione e le proprietà personalizzate rilevanti per il flusso di lavoro della vostra organizzazione.

Implementando le firme dei metadati con GroupDocs.Signature, puoi garantire che i tuoi documenti PDF mantengano la loro integrità e forniscano informazioni verificabili durante tutto il loro ciclo di vita.

## Domande frequenti

### Posso modificare i metadati esistenti in un documento PDF?

Sì, è possibile modificare i metadati esistenti nei documenti PDF. Quando si applicano nuove firme di metadati con gli stessi nomi di quelle esistenti, i valori verranno aggiornati di conseguenza.

### Le firme dei metadati nei documenti PDF sono visibili all'utente finale?

Le firme dei metadati non sono visibili nel contenuto del documento stesso. Tuttavia, possono essere visualizzate tramite il pannello delle proprietà del documento in lettori PDF come Adobe Acrobat o utilizzando strumenti specializzati per la visualizzazione dei metadati.

### Posso crittografare o proteggere i metadati nei PDF?

GroupDocs.Signature offre opzioni per la protezione dei documenti, inclusa la crittografia. È possibile applicare la crittografia a livello di documento per proteggere l'intero PDF, inclusi i relativi metadati.

### Esiste un limite alla quantità di metadati che posso aggiungere a un PDF?

Sebbene non vi siano limiti rigorosi imposti dalle specifiche PDF, l'aggiunta di quantità eccessive di metadati può aumentare le dimensioni del file. Si consiglia di includere nei metadati solo le informazioni pertinenti e necessarie.

### Posso convalidare a livello di programmazione se un PDF è stato manomesso dopo aver aggiunto metadati?

Sì, GroupDocs.Signature offre funzionalità di verifica che possono aiutare a rilevare se un documento è stato modificato dopo la firma, comprese le modifiche ai metadati.

### Dove posso trovare ulteriori risorse e supporto?

- [Riferimento API](https://reference.groupdocs.com/signature/net/)
- [Scarica](https://releases.groupdocs.com/signature/net/)
- [Esempi](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
- [Documentazione](https://docs.groupdocs.com/signature/net/)
- [Pagina del prodotto](https://products.groupdocs.com/signature/net/)
- [Blog](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
- [Forum di supporto](https://forum.groupdocs.com/c/signature/13)
- [Licenza temporanea](https://purchase.groupdocs.com/temporary-license/)