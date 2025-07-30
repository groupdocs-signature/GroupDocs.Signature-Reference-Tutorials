---
"description": "Proteggi e migliora i fogli di calcolo Excel incorporando firme di metadati utilizzando GroupDocs.Signature per .NET. Aggiungi informazioni sull'autore, timestamp e dati personalizzati per migliorare la tracciabilità e l'autenticità dei documenti."
"linktitle": "Firma il foglio di calcolo con i metadati"
"second_title": "API .NET GroupDocs.Signature"
"title": "Aggiungere firme di metadati ai fogli di calcolo Excel in C# .NET"
"url": "/it/net/document-signing/sign-spreadsheet-with-metadata/"
"weight": 13
---

## Introduzione

I fogli di calcolo Excel contengono spesso dati aziendali critici, informazioni finanziarie e calcoli importanti. Garantirne l'autenticità, tracciarne l'origine e proteggerne l'integrità è fondamentale in molti ambienti professionali. Un approccio efficace per migliorare la sicurezza e la tracciabilità dei fogli di calcolo è l'integrazione di firme di metadati.

Questo tutorial completo ti guiderà attraverso il processo di firma di fogli di calcolo Excel con metadati utilizzando GroupDocs.Signature per .NET. Aggiungendo firme con metadati, puoi incorporare informazioni preziose come dettagli dell'autore, timestamp di creazione, identificatori di documento e altre proprietà personalizzate direttamente nella struttura del file del foglio di calcolo.

## Prerequisiti

Prima di procedere con questo tutorial, assicurati di avere quanto segue:

1. [GroupDocs.Signature per .NET](https://releases.groupdocs.com/signature/net/) - Scarica e installa la libreria
2. Ambiente di sviluppo: Visual Studio o qualsiasi altro IDE compatibile con .NET
3. Foglio di calcolo Excel: un file di foglio di calcolo di esempio (XLSX, XLS, ecc.)
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

Definisci i percorsi per il foglio di calcolo di origine e dove salvare l'output firmato:

```csharp
// Specificare il percorso del file Excel
string filePath = "sample.xlsx";

// Definire la directory di output e il nome del file per il foglio di calcolo firmato
string outputDirectory = "Your Document Directory";
string outputFilePath = Path.Combine(outputDirectory, "SignSpreadsheetWithMetadata", "SignedWithMetadata.xlsx");

// Assicurarsi che la directory di output esista
Directory.CreateDirectory(Path.GetDirectoryName(outputFilePath));
```

## Passaggio 2: inizializzare l'oggetto firma

Crea un'istanza della classe Signature con il file del foglio di calcolo di origine:

```csharp
using (Signature signature = new Signature(filePath))
{
    // Il resto del codice andrà qui
}
```

## Passaggio 3: creare e configurare le firme dei metadati

Successivamente, definisci le opzioni dei metadati e crea una matrice di firme dei metadati del foglio di calcolo:

```csharp
// Crea oggetto opzioni metadati
MetadataSignOptions options = new MetadataSignOptions();

// Crea una serie di firme di metadati di fogli di calcolo con diversi tipi di dati
SpreadsheetMetadataSignature[] signatures = new SpreadsheetMetadataSignature[]
{
    new SpreadsheetMetadataSignature("Author", "Mr.Sherlock Holmes"), // Valore stringa
    new SpreadsheetMetadataSignature("CreatedOn", DateTime.Now),      // Valore DateTime
    new SpreadsheetMetadataSignature("DocumentId", 123456),           // Valore intero
    new SpreadsheetMetadataSignature("SignatureId", 123.456D),        // Doppio valore
    new SpreadsheetMetadataSignature("Amount", 123.456M),             // Valore decimale
    new SpreadsheetMetadataSignature("Total", 123.456F)               // Valore float
};

// Aggiungi la raccolta firme alle opzioni
options.Signatures.AddRange(signatures);
```

## Passaggio 4: firmare il foglio di calcolo con i metadati

Applica le firme dei metadati al foglio di calcolo e salva il risultato:

```csharp
// Firma il documento e salvalo nel percorso del file di output
SignResult result = signature.Sign(outputFilePath, options);

// Visualizza messaggio di successo
Console.WriteLine($"\nSource spreadsheet signed successfully with {result.Succeeded.Count} metadata signature(s).");
Console.WriteLine($"Signed spreadsheet saved at: {outputFilePath}");
```

## Esempio completo

Ecco l'esempio di codice completo che riunisce tutti i passaggi:

```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;

namespace SignSpreadsheetWithMetadataExample
{
    class Program
    {
        static void Main(string[] args)
        {
            // Specificare i percorsi dei file
            string filePath = "sample.xlsx";
            string outputFilePath = Path.Combine("Your Document Directory", "SignSpreadsheetWithMetadata", "SignedWithMetadata.xlsx");
            
            // Assicurarsi che la directory di output esista
            Directory.CreateDirectory(Path.GetDirectoryName(outputFilePath));

            // Firma il foglio di calcolo con i metadati
            using (Signature signature = new Signature(filePath))
            {
                // Crea oggetto opzioni metadati
                MetadataSignOptions options = new MetadataSignOptions();
                
                // Crea una serie di firme di metadati di fogli di calcolo con diversi tipi di dati
                SpreadsheetMetadataSignature[] signatures = new SpreadsheetMetadataSignature[]
                {
                    new SpreadsheetMetadataSignature("Author", "Mr.Sherlock Holmes"), // Valore stringa
                    new SpreadsheetMetadataSignature("CreatedOn", DateTime.Now),      // Valore DateTime
                    new SpreadsheetMetadataSignature("DocumentId", 123456),           // Valore intero
                    new SpreadsheetMetadataSignature("SignatureId", 123.456D),        // Doppio valore
                    new SpreadsheetMetadataSignature("Amount", 123.456M),             // Valore decimale
                    new SpreadsheetMetadataSignature("Total", 123.456F)               // Valore float
                };
                
                // Aggiungi la raccolta firme alle opzioni
                options.Signatures.AddRange(signatures);
                
                // Firma il documento e salvalo nel file
                SignResult result = signature.Sign(outputFilePath, options);
                
                // Visualizza i risultati
                Console.WriteLine($"\nSource spreadsheet signed successfully with {result.Succeeded.Count} signature(s).");
                Console.WriteLine($"File saved at {outputFilePath}.");
            }
        }
    }
}
```

## Tecniche avanzate di metadati per fogli di calcolo

### Utilizzo delle proprietà personalizzate e integrate dei fogli di calcolo

fogli di calcolo Excel dispongono di proprietà sia integrate che personalizzate, accessibili tramite la finestra di dialogo delle proprietà del file. GroupDocs.Signature consente di lavorare con entrambe:

```csharp
// Aggiungi proprietà integrate
signatures = new SpreadsheetMetadataSignature[]
{
    new SpreadsheetMetadataSignature("Company", "Sherlock Holmes Consulting"),
    new SpreadsheetMetadataSignature("Category", "Financial"),
    new SpreadsheetMetadataSignature("Keywords", "budget,forecast,analysis"),
    new SpreadsheetMetadataSignature("Comments", "This spreadsheet contains confidential information"),
    new SpreadsheetMetadataSignature("Manager", "John Watson")
};
options.Signatures.AddRange(signatures);

// Aggiungi proprietà personalizzate
options.Signatures.Add(new SpreadsheetMetadataSignature("Department", "Finance"));
options.Signatures.Add(new SpreadsheetMetadataSignature("SecurityLevel", "Confidential"));
```

### Ricerca di metadati nei fogli di calcolo firmati

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

### Aggiornamento dei metadati esistenti

È possibile aggiornare i metadati esistenti nei fogli di calcolo utilizzando gli stessi nomi di proprietà:

```csharp
// Aggiorna i metadati esistenti
options.Signatures.Add(new SpreadsheetMetadataSignature("Author", "Updated Author Name"));
```

## Conclusione

In questo tutorial completo, hai imparato come firmare fogli di calcolo Excel con metadati utilizzando GroupDocs.Signature per .NET. L'incorporazione di metadati nei file di foglio di calcolo migliora la tracciabilità dei documenti, fornisce un contesto prezioso e contribuisce a stabilirne l'autenticità.

Le firme dei metadati nei fogli di calcolo sono particolarmente utili negli ambienti aziendali in cui l'origine, la paternità e il monitoraggio delle versioni dei documenti sono importanti. I metadati incorporati possono includere informazioni sull'autore, l'ora di creazione, gli identificatori dei documenti e proprietà personalizzate pertinenti alle esigenze della tua organizzazione.

Implementando le firme dei metadati con GroupDocs.Signature, puoi garantire che i tuoi fogli di calcolo Excel mantengano la loro integrità e forniscano informazioni verificabili durante tutto il loro ciclo di vita.

## Domande frequenti

### Posso aggiungere metadati ai fogli di calcolo in cui sono già definite alcune proprietà?

Sì, è possibile aggiungere nuovi metadati o aggiornare quelli esistenti nei fogli di calcolo. GroupDocs.Signature gestirà l'integrazione, aggiungendo nuove proprietà o aggiornando quelle esistenti con gli stessi nomi.

### Quali formati di foglio di calcolo sono supportati per la firma dei metadati?

GroupDocs.Signature per .NET supporta la firma dei metadati per vari formati di fogli di calcolo, tra cui XLSX, XLS, XLSM, ODS e altri. Per un elenco completo, fare riferimento a [documentazione ufficiale](https://docs.groupdocs.com/signature/net/).

### Le firme dei metadati nei fogli di calcolo sono visibili agli utenti?

Le firme dei metadati non sono visibili nel contenuto del foglio di calcolo stesso. Tuttavia, possono essere visualizzate tramite il pannello delle proprietà del documento in Excel o altre applicazioni compatibili.

### Posso convalidare a livello di programmazione se un foglio di calcolo è stato manomesso dopo aver aggiunto metadati?

Sì, GroupDocs.Signature offre funzionalità di verifica che possono aiutare a rilevare se un documento è stato modificato dopo la firma, comprese le modifiche ai metadati.

### L'aggiunta di metadati influisce sulla funzionalità del foglio di calcolo?

L'aggiunta di metadati ha un impatto minimo sulle dimensioni del file e non influisce sulla funzionalità del foglio di calcolo. È un modo semplice per migliorare le proprietà del documento senza influire su calcoli, formule o altre funzionalità di Excel.

### Dove posso trovare ulteriori risorse e supporto?

- [Riferimento API](https://reference.groupdocs.com/signature/net/)
- [Scarica](https://releases.groupdocs.com/signature/net/)
- [Esempi](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
- [Documentazione](https://docs.groupdocs.com/signature/net/)
- [Pagina del prodotto](https://products.groupdocs.com/signature/net/)
- [Blog](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
- [Forum di supporto](https://forum.groupdocs.com/c/signature/13)
- [Licenza temporanea](https://purchase.groupdocs.com/temporary-license/)