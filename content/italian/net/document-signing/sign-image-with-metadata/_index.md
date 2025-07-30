---
"description": "Scopri come firmare e incorporare metadati nelle immagini utilizzando GroupDocs.Signature per .NET. Aggiungi informazioni sull'autore, timestamp e dati personalizzati per migliorare l'autenticità e la tracciabilità delle immagini."
"linktitle": "Immagine del segno con metadati"
"second_title": "API .NET GroupDocs.Signature"
"title": "Firma delle immagini con metadati in C# .NET"
"url": "/it/net/document-signing/sign-image-with-metadata/"
"weight": 10
---

## Introduzione

La firma digitale delle immagini con metadati sta diventando sempre più importante per stabilire autenticità, proprietà e tracciabilità. GroupDocs.Signature per .NET offre una soluzione potente e semplice da usare per aggiungere firme con metadati a vari formati di immagine. Questo tutorial vi guiderà attraverso l'intero processo di firma delle immagini con metadati utilizzando C#.

Le firme dei metadati consentono di incorporare informazioni preziose direttamente nei file immagine, come informazioni sull'autore, timestamp di creazione, identificatori univoci e altro ancora. Queste informazioni diventano parte integrante del file immagine stesso, fornendo un metodo affidabile per tracciare e verificare l'autenticità dell'immagine.

## Prerequisiti

Prima di procedere con questo tutorial, assicurati di avere quanto segue:

1. [GroupDocs.Signature per .NET](https://releases.groupdocs.com/signature/net/) - Scarica e installa la libreria
2. Ambiente di sviluppo: Visual Studio o qualsiasi IDE compatibile con supporto .NET
3. File immagine: un file immagine di esempio in un formato supportato (PNG, JPG, TIFF, ecc.)
4. Conoscenza di base della programmazione C# - Familiarità con i concetti di programmazione C#

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

Definisci i percorsi per l'immagine sorgente e dove salvare l'output firmato:

```csharp
// Specificare il percorso del file immagine sorgente
string filePath = "sample.png";

// Definire la directory di output e il nome file per l'immagine firmata
string outputDirectory = "Your Document Directory";
string outputFilePath = Path.Combine(outputDirectory, "SignImageWithMetadata", "SignedWithMetadata.png");

// Assicurarsi che la directory di output esista
Directory.CreateDirectory(Path.GetDirectoryName(outputFilePath));
```

## Passaggio 2: inizializzare l'oggetto firma

Crea un'istanza della classe Signature con il tuo file immagine sorgente:

```csharp
using (Signature signature = new Signature(filePath))
{
    // Il resto del codice andrà qui
}
```

## Passaggio 3: creare e configurare le firme dei metadati

Successivamente, definisci i metadati che desideri incorporare nell'immagine. GroupDocs.Signature supporta vari tipi di dati per i metadati:

```csharp
// Inizializza l'ID dei metadati (specifico per il formato dell'immagine)
ushort imgsMetadataId = 41996;

// Crea oggetto opzioni metadati
MetadataSignOptions options = new MetadataSignOptions();

// Aggiungere vari tipi di firme di metadati
options
    .Add(new ImageMetadataSignature(imgsMetadataId++, "Mr.Sherlock Holmes"))  // Valore stringa
    .Add(new ImageMetadataSignature(imgsMetadataId++, DateTime.Now))          // Valore data/ora
    .Add(new ImageMetadataSignature(imgsMetadataId++, 123456))                // Valore intero
    .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456D))              // Doppio valore
    .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456M))              // Valore decimale
    .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456F));             // Valore float
```

## Passaggio 4: firmare l'immagine con i metadati

Applica le firme dei metadati all'immagine e salva il risultato:

```csharp
// Firma il documento e salvalo nel percorso del file di output
SignResult result = signature.Sign(outputFilePath, options);

// Visualizza messaggio di successo
Console.WriteLine($"\nSource image signed successfully with {result.Succeeded.Count} metadata signature(s).");
Console.WriteLine($"Signed image saved at: {outputFilePath}");
```

## Esempio completo

Ecco l'esempio di codice completo che riunisce tutti i passaggi:

```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;

namespace SignImageWithMetadataExample
{
    class Program
    {
        static void Main(string[] args)
        {
            // Specificare i percorsi dei file
            string filePath = "sample.png";            
            string outputFilePath = Path.Combine("Your Document Directory", "SignImageWithMetadata", "SignedWithMetadata.png");
            
            // Assicurarsi che la directory di output esista
            Directory.CreateDirectory(Path.GetDirectoryName(outputFilePath));

            // Firma l'immagine con i metadati
            using (Signature signature = new Signature(filePath))
            {
                // Inizializza l'ID dei metadati (specifico per il formato dell'immagine)
                ushort imgsMetadataId = 41996;
                
                // Crea opzioni di metadati
                MetadataSignOptions options = new MetadataSignOptions();
                
                // Aggiungere diversi tipi di firme di metadati
                options
                    .Add(new ImageMetadataSignature(imgsMetadataId++, "Mr.Sherlock Holmes")) // Valore stringa
                    .Add(new ImageMetadataSignature(imgsMetadataId++, DateTime.Now))          // Valore data/ora
                    .Add(new ImageMetadataSignature(imgsMetadataId++, 123456))                // Valore intero
                    .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456D))              // Doppio valore
                    .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456M))              // Valore decimale
                    .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456F));             // Valore float
                
                // Firma il documento e salvalo nel file
                SignResult result = signature.Sign(outputFilePath, options);
                
                // Visualizza i risultati
                Console.WriteLine($"\nSource image signed successfully with {result.Succeeded.Count} signature(s).");
                Console.WriteLine($"File saved at {outputFilePath}.");
            }
        }
    }
}
```

## Tecniche avanzate di firma dei metadati

### Lavorare con metadati personalizzati

È anche possibile creare campi di metadati personalizzati con ID specifici:

```csharp
// Crea metadati personalizzati con ID specifico
options.Add(new ImageMetadataSignature(42000, "CustomValue"));
```

### Verifica delle firme dei metadati

Dopo la firma, potresti voler verificare le firme dei metadati:

```csharp
// Crea opzioni di verifica
MetadataSearchOptions searchOptions = new MetadataSearchOptions();

// Cerca firme di metadati
SearchResult result = signature.Search(searchOptions);

// Visualizza le firme trovate
Console.WriteLine($"Found {result.Signatures.Count} metadata signatures:");
foreach(var metadataSignature in result.Signatures)
{
    Console.WriteLine($"- {metadataSignature.Name}: {metadataSignature.Value}");
}
```

## Conclusione

In questo tutorial, hai imparato come firmare le immagini con metadati utilizzando GroupDocs.Signature per .NET. L'incorporazione di metadati nelle immagini offre un modo eccellente per migliorarne l'autenticità, aggiungere informazioni critiche e ottimizzare i flussi di lavoro di gestione dei documenti. Il processo è semplice ma potente, e consente la personalizzazione in base alle tue esigenze specifiche.

I metadati incorporati nel file immagine possono essere utilizzati per vari scopi, come la protezione del copyright, il tracciamento dell'origine dell'immagine, l'aggiunta di informazioni descrittive e la definizione della catena di custodia digitale. Implementando le firme dei metadati, è possibile garantire che le immagini mantengano la loro integrità e autenticità durante tutto il loro ciclo di vita.

## Domande frequenti

### Posso aggiungere metadati alle immagini firmate esistenti?

Sì, è possibile aggiungere metadati aggiuntivi alle immagini che già contengono firme di metadati. I metadati esistenti verranno conservati e i nuovi metadati verranno aggiunti di conseguenza.

### Quali formati di immagine sono supportati per la firma dei metadati?

GroupDocs.Signature per .NET supporta la firma dei metadati per vari formati di immagine, tra cui PNG, JPEG, TIFF, BMP, GIF e altri. Per un elenco completo, fare riferimento a [documentazione ufficiale](https://docs.groupdocs.com/signature/net/).

### È possibile crittografare i metadati nelle immagini?

Sì, GroupDocs.Signature offre opzioni per crittografare i metadati per una maggiore sicurezza. È possibile utilizzare le opzioni di crittografia fornite dalla biblioteca per proteggere le informazioni sensibili sui metadati.

### Posso convalidare programmaticamente l'autenticità delle immagini firmate?

Assolutamente sì. Puoi utilizzare i metodi di verifica in GroupDocs.Signature per convalidare le firme dei metadati e confermare l'autenticità delle immagini firmate.

### Esiste un limite di dimensione del file quando si firmano immagini con metadati?

Non esiste una limitazione specifica per le dimensioni dei file imposta dalla libreria stessa, ma file molto grandi potrebbero richiedere più tempo di elaborazione e memoria. Si consiglia di considerare le risorse di sistema quando si lavora con immagini di grandi dimensioni.

### Come posso ottenere una licenza temporanea per scopi di prova?

Puoi ottenere un [licenza temporanea](https://purchase.groupdocs.com/temporary-license/) per testare GroupDocs.Signature prima di effettuare un acquisto.

### Dove posso trovare ulteriori risorse e supporto?

- [Riferimento API](https://reference.groupdocs.com/signature/net/)
- [Scarica](https://releases.groupdocs.com/signature/net/)
- [Esempi](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
- [Documentazione](https://docs.groupdocs.com/signature/net/)
- [Pagina del prodotto](https://products.groupdocs.com/signature/net/)
- [Blog](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
- [Forum di supporto](https://forum.groupdocs.com/c/signature/13)