---
"description": "Scopri come cercare in modo efficiente le firme di testo nei documenti utilizzando GroupDocs.Signature per .NET con la nostra guida completa passo passo e gli esempi di codice."
"linktitle": "Cerca firme di testo"
"second_title": "API .NET GroupDocs.Signature"
"title": "Cerca firme di testo nei documenti"
"url": "/it/net/signature-searching/search-for-text-signatures/"
"weight": 16
---

## Introduzione

Le firme testuali sono un metodo comune per indicare la paternità, l'approvazione o la verifica di un documento. Nella gestione dei documenti digitali, la possibilità di cercare ed estrarre le firme testuali a livello di codice è fondamentale per la convalida dei documenti, l'automazione del flusso di lavoro e la verifica della conformità. GroupDocs.Signature per .NET offre una soluzione completa per implementare la funzionalità di ricerca delle firme testuali nelle applicazioni .NET, supportando vari formati di documento e funzionalità di ricerca avanzate.

Questo tutorial ti guiderà attraverso il processo di ricerca di firme di testo nei documenti utilizzando GroupDocs.Signature per .NET, fornendo spiegazioni dettagliate, istruzioni passo passo ed esempi di codice pratici.

## Prerequisiti

Prima di iniziare a cercare firme testuali, assicurati di disporre dei seguenti prerequisiti:

1. GroupDocs.Signature per la libreria .NET: scarica e installa la libreria da [pagina delle versioni](https://releases.groupdocs.com/signature/net/).

2. Ambiente di sviluppo: impostare un ambiente di sviluppo adatto, come Visual Studio o qualsiasi IDE compatibile con supporto .NET.

3. Documenti campione: preparare documenti di prova contenenti firme di testo per la verifica e il test.

4. Conoscenza di base di C#: familiarità con il linguaggio di programmazione C# e i concetti del framework .NET.

## Importa spazi dei nomi

Per iniziare, importare gli spazi dei nomi necessari per accedere alla funzionalità GroupDocs.Signature:

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

Ora, scomponiamo il processo di ricerca delle firme testuali in passaggi chiari e gestibili:

## Passaggio 1: caricare il documento

Per prima cosa, definisci il percorso del documento e inizializza un `Signature` oggetto:

```csharp
string filePath = "sample_multiple_signatures.docx";
string fileName = Path.GetFileName(filePath);

using (Signature signature = new Signature(filePath))
{
    // Il codice di ricerca della firma del testo verrà aggiunto qui
}
```

## Passaggio 2: configura le opzioni di ricerca

Crea e configura `TextSearchOptions` per specificare come devono essere ricercate le firme di testo:

```csharp
// Configurare le opzioni di ricerca di testo
TextSearchOptions options = new TextSearchOptions
{
    // Cerca in tutte le pagine
    AllPages = true,
    
    // Facoltativo: specificare il testo da abbinare
    // Testo = "Approvato",
    
    // Facoltativo: specificare il tipo di corrispondenza
    // MatchType = TextMatchType.Contiene
};
```

## Passaggio 3: eseguire la ricerca della firma del testo

Eseguire l'operazione di ricerca utilizzando le opzioni configurate:

```csharp
// Cerca firme di testo
List<TextSignature> signatures = signature.Search<TextSignature>(options);
```

## Fase 4: Elaborazione e visualizzazione dei risultati

Scorri le firme di testo trovate e visualizza i loro dettagli:

```csharp
// Visualizza i risultati della ricerca
Console.WriteLine($"\nSource document '{fileName}' contains {signatures.Count} text signature(s):");

foreach (TextSignature textSignature in signatures)
{
    Console.WriteLine($"Text signature found at page {textSignature.PageNumber} with text '{textSignature.Text}'");
    Console.WriteLine($"Location: X={textSignature.Left}, Y={textSignature.Top}, Width={textSignature.Width}, Height={textSignature.Height}");
    Console.WriteLine($"Signature type: {textSignature.SignatureImplementation}");
    Console.WriteLine();
}
```

## Esempio completo

Ecco un esempio completo e funzionante che mostra come cercare firme di testo in un documento:

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;

namespace TextSignatureSearch
{
    class Program
    {
        static void Main(string[] args)
        {
            // Percorso del documento: aggiorna con il percorso del tuo file
            string filePath = "sample_multiple_signatures.docx";
            string fileName = Path.GetFileName(filePath);
            
            // Inizializza l'istanza della firma
            using (Signature signature = new Signature(filePath))
            {
                try
                {
                    // Configurare le opzioni di ricerca di testo
                    TextSearchOptions options = new TextSearchOptions
                    {
                        // Cerca in tutte le pagine
                        AllPages = true
                    };
                    
                    // Cerca firme di testo
                    List<TextSignature> signatures = signature.Search<TextSignature>(options);
                    
                    // Visualizza i risultati della ricerca
                    Console.WriteLine($"\nSource document '{fileName}' contains {signatures.Count} text signature(s):");
                    
                    foreach (TextSignature textSignature in signatures)
                    {
                        Console.WriteLine($"Text signature found at page {textSignature.PageNumber} with text '{textSignature.Text}'");
                        Console.WriteLine($"Location: X={textSignature.Left}, Y={textSignature.Top}, Width={textSignature.Width}, Height={textSignature.Height}");
                        Console.WriteLine($"Signature type: {textSignature.SignatureImplementation}");
                        Console.WriteLine();
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

## Tecniche avanzate di ricerca della firma del testo

### Ricerca con criteri di testo specifici

Per ricerche più mirate, puoi personalizzare il `TextSearchOptions` per filtrare in base a contenuti di testo specifici:

```csharp
// Crea opzioni di ricerca con criteri di testo specifici
TextSearchOptions options = new TextSearchOptions
{
    // Cerca in tutte le pagine
    AllPages = true,
    
    // Cerca un testo specifico
    Text = "Approved",
    
    // Specificare il tipo di corrispondenza (Contiene, Esatto, Inizia con, Termina con)
    MatchType = TextMatchType.Contains,
    
    // Ricerca con distinzione tra maiuscole e minuscole
    MatchCase = true
};
```

### Ricerca in aree specifiche del documento

È possibile limitare la ricerca ad aree specifiche del documento:

```csharp
// Crea opzioni di ricerca per un'area specifica del documento
TextSearchOptions options = new TextSearchOptions
{
    // Cerca solo su pagine specifiche
    AllPages = false,
    PageNumber = 1,
    
    // Oppure specifica più pagine
    PagesSetup = new PagesSetup { Pages = new List<int> { 1, 3, 5 } },
    
    // Definisci un'area specifica in cui effettuare la ricerca
    Rectangle = new Rectangle(100, 100, 400, 200)
};
```

### Filtraggio avanzato del testo

Implementare una logica di filtraggio personalizzata per requisiti di ricerca più complessi:

```csharp
// Crea opzioni di ricerca con elaborazione personalizzata
TextSearchOptions options = new TextSearchOptions
{
    AllPages = true,
    
    // Definisci l'elaborazione personalizzata utilizzando un delegato
    ProcessCompleted = (TextSignature signature) =>
    {
        // Logica di convalida personalizzata
        bool isValid = signature.Text.Length > 5 && 
                      (signature.Text.Contains("Approved") || signature.Text.Contains("Verified"));
        
        return isValid;
    }
};
```

### Ricerca di diversi stili di testo

Utilizzare le proprietà del carattere e dello stile per filtrare le firme di testo:

```csharp
// Crea opzioni di ricerca mirate all'aspetto specifico del testo
TextSearchOptions options = new TextSearchOptions
{
    // Filtra per nome del font
    FontName = "Arial",
    
    // Filtra per intervallo di dimensioni del carattere
    MinFontSize = 10,
    MaxFontSize = 14,
    
    // Filtra per colore del carattere
    ForeColor = System.Drawing.Color.Blue
};
```

### Estrazione dei metadati della firma

Estrarre ed elaborare i metadati associati alle firme di testo:

```csharp
foreach (TextSignature signature in signatures)
{
    // Accedi ai metadati della firma
    if (signature.Metadata != null && signature.Metadata.Count > 0)
    {
        Console.WriteLine("Signature Metadata:");
        
        foreach (var item in signature.Metadata)
        {
            Console.WriteLine($"  {item.Key}: {item.Value}");
        }
    }
    
    // Controllare le date di creazione e modifica della firma
    if (signature.CreatedOn.HasValue)
    {
        Console.WriteLine($"Created on: {signature.CreatedOn.Value}");
    }
    
    if (signature.ModifiedOn.HasValue)
    {
        Console.WriteLine($"Modified on: {signature.ModifiedOn.Value}");
    }
}
```

## Conclusione

In questa guida completa, abbiamo esplorato come cercare firme testuali nei documenti utilizzando GroupDocs.Signature per .NET. Dalle operazioni di ricerca di base alle tecniche avanzate, ora hai le conoscenze necessarie per implementare solide funzionalità di firma testuale nelle tue applicazioni .NET.

GroupDocs.Signature fornisce un framework potente e flessibile per lavorare con le firme di testo, consentendo di creare sistemi sofisticati di verifica dei documenti, soluzioni di flusso di lavoro automatizzate e strumenti di convalida della conformità.

## Domande frequenti

### Posso cercare firme testuali in documenti protetti da password?

Sì, GroupDocs.Signature supporta la ricerca di firme testuali nei documenti protetti da password. È possibile specificare la password durante l'inizializzazione. `Signature` oggetto:

```csharp
LoadOptions loadOptions = new LoadOptions { Password = "your_password" };
using (Signature signature = new Signature(filePath, loadOptions))
{
    // Cerca firme di testo
}
```

### Quali formati di documento sono supportati per la ricerca di firme testuali?

GroupDocs.Signature supporta un'ampia gamma di formati di documenti, tra cui PDF, documenti Microsoft Office (Word, Excel, PowerPoint), formati OpenOffice, immagini e altro ancora.

### Posso cercare firme di testo con formattazioni specifiche, come grassetto o corsivo?

Sì, puoi cercare firme di testo con formattazione specifica utilizzando `FontBold` E `FontItalic` proprietà in `TextSearchOptions`:

```csharp
TextSearchOptions options = new TextSearchOptions
{
    FontBold = true,
    FontItalic = true
};
```

### Come posso migliorare le prestazioni di ricerca per documenti di grandi dimensioni?

Per i documenti di grandi dimensioni, puoi ottimizzare le prestazioni di ricerca:

1. Limitare la ricerca a pagine specifiche anziché cercare nell'intero documento
2. Utilizzo di criteri di ricerca più specifici per ridurre il numero di corrispondenze
3. Specificare un'area di ricerca utilizzando `Rectangle` proprietà se sai dove si trovano in genere le firme
4. Implementazione della paginazione nella tua applicazione per elaborare i risultati della ricerca in batch

### Posso verificare se una firma testuale è stata aggiunta elettronicamente o fa parte del contenuto del documento originale?

GroupDocs.Signature può distinguere tra diversi tipi di elementi di testo nei documenti. `SignatureImplementation` proprietà di `TextSignature` Indica se il testo è una firma formale o il normale contenuto di un documento. Tuttavia, la determinazione definitiva può dipendere da come il testo è stato originariamente aggiunto al documento.

## Vedi anche

* [Riferimento API](https://reference.groupdocs.com/signature/net/)
* [Esempi di codice su GitHub](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
* [Documentazione del prodotto](https://docs.groupdocs.com/signature/net/)
* [Pagina del prodotto](https://products.groupdocs.com/signature/net/)
* [Scarica l'ultima versione](https://releases.groupdocs.com/signature/net/)
* [Articoli del blog](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
* [Forum di supporto gratuito](https://forum.groupdocs.com/c/signature/13)
* [Licenza temporanea](https://purchase.groupdocs.com/temporary-license/)