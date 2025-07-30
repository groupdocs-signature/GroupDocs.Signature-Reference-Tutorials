---
"description": "Scopri come aggiornare a livello di codice a barre le firme in diversi formati di documento utilizzando GroupDocs.Signature per .NET. Tutorial completo per sviluppatori che creano soluzioni di gestione dei documenti."
"linktitle": "Aggiorna codice a barre"
"second_title": "API .NET GroupDocs.Signature"
"title": "Aggiorna le firme dei codici a barre nei documenti"
"url": "/it/net/update-operations/update-barcode/"
"weight": 10
---

## Introduzione
Le firme con codice a barre sono ampiamente utilizzate nei flussi di lavoro dei documenti digitali per codificare dati strutturati, consentendo un monitoraggio, un'identificazione e una convalida efficienti. GroupDocs.Signature per .NET è una soluzione completa per la firma dei documenti che consente agli sviluppatori di integrare funzionalità di firma avanzate nelle loro applicazioni, inclusa la possibilità di aggiornare le firme con codice a barre esistenti all'interno dei documenti.

Questo tutorial si concentra specificamente sull'aggiornamento delle firme dei codici a barre nei documenti utilizzando GroupDocs.Signature per .NET. Che tu debba modificare la posizione, le dimensioni o i dati codificati di codici a barre esistenti, questa guida ti guiderà attraverso il processo con chiari esempi di codice e spiegazioni.

## Prerequisiti
Prima di implementare gli aggiornamenti della firma del codice a barre con GroupDocs.Signature per .NET, assicurarsi di disporre dei seguenti prerequisiti:

1. Ambiente di sviluppo: un ambiente di sviluppo .NET funzionante, come Visual Studio 2017 o versione successiva.
2. Libreria GroupDocs.Signature: la libreria GroupDocs.Signature per .NET, che puoi scaricare da [pagina di download](https://releases.groupdocs.com/signature/net/).
3. Conoscenza di base di C#: familiarità con i concetti di programmazione C#.
4. Documenti di esempio: Documenti contenenti firme con codice a barre che si desidera aggiornare.

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

Ora, scomponiamo il processo di aggiornamento delle firme dei codici a barre in passaggi gestibili:

## Passaggio 1: impostare i percorsi dei documenti
Per prima cosa, definisci i percorsi del documento sorgente e dove verrà salvato il documento aggiornato:

```csharp
// Percorso al documento sorgente con firme con codice a barre
string filePath = "sample_multiple_signatures.docx";

// Ottieni il nome del file per l'output
string fileName = Path.GetFileName(filePath);

// Definisci la directory di output e il percorso del file
string outputDirectory = Path.Combine("Your Document Directory", "UpdateBarcode");
string outputFilePath = Path.Combine(outputDirectory, fileName);

// Assicurarsi che la directory di output esista
Directory.CreateDirectory(outputDirectory);
```

## Passaggio 2: Copia il documento sorgente
Poiché l'operazione di aggiornamento modifica direttamente il documento, creare una copia del documento originale per conservarlo:

```csharp
// Crea una copia del documento originale
File.Copy(filePath, outputFilePath, true);
```

## Passaggio 3: inizializzare l'istanza della firma
Crea un'istanza di `Signature` classe per lavorare con il documento:

```csharp
// Inizializza l'istanza Signature con il percorso del file di output
using (Signature signature = new Signature(outputFilePath))
{
    // Qui verranno eseguite le operazioni di firma
}
```

## Passaggio 4: configurare le opzioni di ricerca dei codici a barre
Imposta le opzioni di ricerca per trovare le firme con codice a barre esistenti nel documento:

```csharp
// Configurare le opzioni di ricerca per le firme con codice a barre
BarcodeSearchOptions options = new BarcodeSearchOptions()
{
    // Puoi filtrare per contenuto di testo
    Text = "12345",
    MatchType = TextMatchType.Contains
    
    // Rimuovi commento per cercare in tutte le pagine
    // Tutte le pagine = vero
};
```

## Passaggio 5: ricerca delle firme con codice a barre
Utilizzare le opzioni di ricerca configurate per trovare le firme con codice a barre nel documento:

```csharp
// Ricerca firme con codice a barre
List<BarcodeSignature> signatures = signature.Search<BarcodeSignature>(options);
```

## Passaggio 6: Aggiorna le proprietà della firma del codice a barre
Se vengono trovate firme con codice a barre, aggiornarne le proprietà secondo necessità:

```csharp
// Controlla se sono state trovate firme
if (signatures.Count > 0)
{
    // Ottieni la prima firma con codice a barre
    BarcodeSignature barcodeSignature = signatures[0];
    
    // Aggiorna posizione
    barcodeSignature.Left = 100;
    barcodeSignature.Top = 100;
    
    // Aggiorna dimensione
    barcodeSignature.Width = 400;
    barcodeSignature.Height = 100;
    
    // Applica gli aggiornamenti
    bool result = signature.Update(barcodeSignature);
    
    // Controlla il risultato
    if (result)
    {
        Console.WriteLine($"Signature with Barcode '{barcodeSignature.Text}' and encode type '{barcodeSignature.EncodeType.TypeName}' was updated in the document ['{fileName}'].");
    }
    else
    {
        Console.WriteLine($"Signature was not updated in the document! Signature with Barcode '{barcodeSignature.Text}' and encode type '{barcodeSignature.EncodeType.TypeName}' was not found!");
    }
}
else
{
    Console.WriteLine("No barcode signatures found in the document.");
}
```

## Esempio completo
Ecco un esempio completo e funzionale che mostra come aggiornare una firma con codice a barre in un documento:

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;

namespace UpdateBarcodeSignatureExample
{
    class Program
    {
        static void Main(string[] args)
        {
            // Percorso del documento
            string filePath = "sample_multiple_signatures.docx";
            
            // Definisci il percorso di output
            string fileName = Path.GetFileName(filePath);
            string outputDirectory = Path.Combine(Environment.CurrentDirectory, "UpdateBarcode");
            string outputFilePath = Path.Combine(outputDirectory, fileName);
            
            // Assicurarsi che la directory di output esista
            Directory.CreateDirectory(outputDirectory);
            
            // Crea una copia del documento originale
            File.Copy(filePath, outputFilePath, true);
            
            // Inizializza l'istanza della firma
            using (Signature signature = new Signature(outputFilePath))
            {
                // Configura le opzioni di ricerca
                BarcodeSearchOptions options = new BarcodeSearchOptions
                {
                    Text = "12345",
                    MatchType = TextMatchType.Contains
                };
                
                // Ricerca firme con codice a barre
                List<BarcodeSignature> signatures = signature.Search<BarcodeSignature>(options);
                
                // Controlla se sono state trovate firme
                if (signatures.Count > 0)
                {
                    // Ottieni la prima firma
                    BarcodeSignature barcodeSignature = signatures[0];
                    
                    // Aggiorna posizione e dimensione
                    barcodeSignature.Left = 100;
                    barcodeSignature.Top = 100;
                    barcodeSignature.Width = 400;
                    barcodeSignature.Height = 100;
                    
                    // Applica gli aggiornamenti
                    bool result = signature.Update(barcodeSignature);
                    
                    // Controlla il risultato
                    if (result)
                    {
                        Console.WriteLine($"Barcode signature was successfully updated in document '{fileName}'.");
                        Console.WriteLine($"Barcode text: {barcodeSignature.Text}");
                        Console.WriteLine($"Encode type: {barcodeSignature.EncodeType.TypeName}");
                        Console.WriteLine($"New position: {barcodeSignature.Left}x{barcodeSignature.Top}");
                        Console.WriteLine($"New size: {barcodeSignature.Width}x{barcodeSignature.Height}");
                        Console.WriteLine($"Output file path: {outputFilePath}");
                    }
                    else
                    {
                        Console.WriteLine("Failed to update barcode signature!");
                    }
                }
                else
                {
                    Console.WriteLine("No barcode signatures found in the document.");
                }
            }
            
            Console.WriteLine("\nPress any key to exit...");
            Console.ReadKey();
        }
    }
}
```

## Personalizzazione avanzata della firma con codice a barre
GroupDocs.Signature offre opzioni aggiuntive per personalizzare le firme dei codici a barre oltre alla posizione e alle dimensioni di base:

### Regolazione delle proprietà dell'aspetto
Personalizza gli aspetti visivi del codice a barre:

```csharp
// Imposta il colore di primo piano (colore del codice a barre)
barcodeSignature.ForeColor = System.Drawing.Color.Blue;

// Imposta il colore di sfondo
barcodeSignature.BackgroundColor = System.Drawing.Color.LightYellow;

// Regola la trasparenza
barcodeSignature.Opacity = 0.8;
```

### Aggiunta di bordi
Migliora il codice a barre con bordi personalizzati:

```csharp
barcodeSignature.Border.Color = System.Drawing.Color.Red;
barcodeSignature.Border.DashStyle = System.Drawing.Drawing2D.DashStyle.Dash;
barcodeSignature.Border.Weight = 2;
barcodeSignature.Border.Visible = true;
```

### Rotazione del codice a barre
Ruota la firma del codice a barre di un'angolazione specifica:

```csharp
barcodeSignature.Angle = 30; // Ruota di 30 gradi
```

## Conclusione
GroupDocs.Signature per .NET offre una soluzione potente e flessibile per l'aggiornamento delle firme con codice a barre all'interno dei documenti. Seguendo i passaggi descritti in questo tutorial, gli sviluppatori possono implementare in modo efficiente la funzionalità di aggiornamento delle firme con codice a barre nelle loro applicazioni .NET, migliorando le capacità di gestione e automazione dei documenti.

Grazie al suo set completo di funzionalità e all'API intuitiva, GroupDocs.Signature consente agli sviluppatori di creare soluzioni sofisticate per la firma dei documenti che soddisfano i requisiti delle moderne applicazioni aziendali, garantendo al contempo l'integrità e l'accessibilità dei documenti.

## Domande frequenti
### Posso aggiornare più firme con codice a barre all'interno di un singolo documento?
Sì, GroupDocs.Signature consente di aggiornare più firme con codice a barre all'interno dello stesso documento. Dopo aver cercato le firme, è possibile scorrere l'elenco risultante e aggiornare ciascuna firma con codice a barre singolarmente.

### GroupDocs.Signature supporta diversi formati di codici a barre?
Sì, GroupDocs.Signature supporta un'ampia gamma di formati di codici a barre, tra cui codici a barre lineari (Codice 128, Codice 39, EAN, UPC, ecc.) e codici a barre 2D (Codice QR, Data Matrix, PDF417, ecc.).

### È disponibile una versione di prova di GroupDocs.Signature per .NET?
Sì, puoi scaricare una versione di prova gratuita da [Sito web di GroupDocs](https://releases.groupdocs.com/signature/net/) per valutare le caratteristiche della biblioteca prima di effettuare un acquisto.

### Posso convertire un tipo di codice a barre in un altro durante l'aggiornamento?
La conversione diretta tra i diversi tipi di codice a barre non è supportata durante gli aggiornamenti. Tuttavia, è possibile farlo eliminando il codice a barre esistente e aggiungendone uno nuovo con il formato desiderato.

### L'aggiornamento di un codice a barre influisce sulla sua capacità di scansione?
Quando si aggiornano le proprietà del codice a barre, come dimensione e posizione, GroupDocs.Signature mantiene l'integrità della scansione del codice a barre. Tuttavia, dimensioni estremamente ridotte o angoli di rotazione sostanziali potrebbero influire sulle prestazioni di scansione con alcuni lettori.

### Dove posso trovare ulteriore supporto per GroupDocs.Signature per .NET?
Puoi trovare un supporto completo attraverso le seguenti risorse:
- [Documentazione API](https://docs.groupdocs.com/signature/net/)
- [Riferimento API](https://reference.groupdocs.com/signature/net/)
- [Esempi di GitHub](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
- [Forum di supporto](https://forum.groupdocs.com/c/signature/13)
- [Blog](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
- [Supporto gratuito](https://forum.groupdocs.com/c/signature)
- [Licenza temporanea](https://purchase.groupdocs.com/temporary-license/)