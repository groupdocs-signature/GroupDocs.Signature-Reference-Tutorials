---
"description": "Scopri come verificare i codici QR nei documenti utilizzando GroupDocs.Signature per .NET. Guida completa con esempi di codice e best practice per l'autenticazione dei documenti."
"linktitle": "Verifica il codice QR"
"second_title": "API .NET GroupDocs.Signature"
"title": "Verifica il codice QR nei documenti"
"url": "/it/net/verify-operations/verify-qr-code/"
"weight": 12
type: docs
---
## Introduzione

La sicurezza dei documenti è un aspetto fondamentale delle moderne operazioni aziendali. I codici QR sono diventati un metodo sempre più diffuso per incorporare informazioni nei documenti, la cui autenticità può essere verificata. GroupDocs.Signature per .NET offre una soluzione potente e flessibile per la verifica dei codici QR incorporati nei documenti in vari formati.

Questo tutorial completo ti guiderà attraverso il processo di implementazione della verifica del codice QR nelle tue applicazioni .NET, garantendo che i tuoi documenti mantengano la loro integrità e autenticità.

## Prerequisiti

Prima di implementare la funzionalità di verifica del codice QR, assicurati di disporre dei seguenti prerequisiti:

1. GroupDocs.Signature per .NET: Scarica e installa la libreria da [pagina di download](https://releases.groupdocs.com/signature/net/).
2. Ambiente di sviluppo: Visual Studio o qualsiasi ambiente di sviluppo .NET compatibile.
3. Documento di prova: documento contenente firme con codice QR a scopo di verifica.
4. Conoscenze di base: familiarità con la programmazione C# e i concetti del framework .NET.

## Importa spazi dei nomi

Per iniziare, importare gli spazi dei nomi necessari per accedere alla funzionalità GroupDocs.Signature:

```csharp
using System;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

## Procedura di verifica passo passo del codice QR

Per verificare i codici QR presenti nei tuoi documenti, segui questi passaggi dettagliati:

### Passaggio 1: specificare il percorso del documento

```csharp
// Fornire il percorso al documento contenente le firme con codice QR
string filePath = "sample_multiple_signatures.docx";
```

Assicurati di sostituire il percorso di esempio con il percorso effettivo del tuo documento.

### Passaggio 2: inizializzare l'oggetto firma

```csharp
// Crea un'istanza di Signature passando il percorso del documento
using (Signature signature = new Signature(filePath))
{
    // Il codice di verifica verrà implementato qui
}
```

La classe Signature è il punto di ingresso principale per tutte le operazioni nell'API GroupDocs.Signature.

### Passaggio 3: configura le opzioni di verifica del codice QR

```csharp
// Definisci le opzioni di verifica del codice QR
QrCodeVerifyOptions options = new QrCodeVerifyOptions()
{
    AllPages = true, // Controlla tutte le pagine del documento
    Text = "John",   // Testo da verificare all'interno del codice QR
    MatchType = TextMatchType.Contains // Specificare i criteri di corrispondenza del testo
};
```

Le opzioni di verifica consentono di definire criteri specifici per il processo di verifica:
- `AllPages`: Impostare su true per controllare tutte le pagine del documento (comportamento predefinito)
- `Text`: Il contenuto del testo da abbinare all'interno del codice QR
- `MatchType`: Il metodo per la corrispondenza del testo (Contiene, Esatto, Inizia con, ecc.)

### Fase 4: Eseguire il processo di verifica

```csharp
// Eseguire la verifica
VerificationResult result = signature.Verify(options);
```

In questo modo viene eseguito il processo di verifica in base alle opzioni specificate.

### Fase 5: Risultati della verifica del processo

```csharp
// Controllare il risultato della verifica e procedere di conseguenza
if (result.IsValid)
{
    Console.WriteLine($"Document {filePath} contains valid QR code signature!");
    
    // Visualizza informazioni sulle firme riuscite
    foreach (QrCodeSignature signature in result.Succeeded)
    {
        Console.WriteLine($"Found valid QR Code signature with text: {signature.Text}");
        Console.WriteLine($"QR Code type: {signature.EncodeType.TypeName}");
        Console.WriteLine($"Location: Page {signature.PageNumber}, {signature.Left}x{signature.Top}");
    }
}
else
{
    Console.WriteLine($"Document {filePath} failed verification process.");
    Console.WriteLine($"Number of failed signatures: {result.Failed.Count}");
}
```

Gestire correttamente il risultato della verifica consente all'applicazione di intraprendere azioni appropriate in base all'esito della verifica.

## Esempio completo

Ecco un esempio completo e funzionante che dimostra la verifica tramite codice QR:

```csharp
using System;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;

namespace GroupDocs.Signature.Examples
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
                // Opzioni di verifica della configurazione
                QrCodeVerifyOptions options = new QrCodeVerifyOptions()
                {
                    AllPages = true,
                    Text = "John",
                    MatchType = TextMatchType.Contains
                };
                
                // Verificare le firme dei documenti
                VerificationResult result = signature.Verify(options);
                
                // Risultati della verifica del processo
                if (result.IsValid)
                {
                    Console.WriteLine($"Document {filePath} contains valid QR code signature!");
                    
                    foreach (QrCodeSignature qrSignature in result.Succeeded)
                    {
                        Console.WriteLine($"Found valid QR Code with text: {qrSignature.Text}");
                    }
                }
                else
                {
                    Console.WriteLine($"Document {filePath} failed verification process.");
                }
            }
        }
    }
}
```

## Opzioni di verifica avanzate

GroupDocs.Signature fornisce opzioni aggiuntive per scenari di verifica più complessi:

### Verifica di tipi specifici di codice QR

```csharp
QrCodeVerifyOptions options = new QrCodeVerifyOptions()
{
    EncodeType = QrCodeTypes.QR,  // Verifica solo i codici QR standard
    Text = "Confidential",
    MatchType = TextMatchType.Exact
};
```

### Verifica su pagine specifiche

```csharp
QrCodeVerifyOptions options = new QrCodeVerifyOptions()
{
    AllPages = false,
    PageNumber = 2,  // Verificare solo a pagina 2
    Text = "Approved"
};
```

### Utilizzo di espressioni regolari per la verifica

```csharp
QrCodeVerifyOptions options = new QrCodeVerifyOptions()
{
    Text = "INV-\\d{6}",  // Corrispondenza numeri fattura (ad esempio, INV-123456)
    MatchType = TextMatchType.Regex
};
```

## Best Practice per la verifica del codice QR

1. Convalidare sempre gli input: assicurarsi che i percorsi dei documenti e i criteri di verifica siano validi prima dell'elaborazione.
2. Implementare la gestione degli errori: utilizzare blocchi try-catch per gestire potenziali eccezioni durante la verifica.
3. Considerare le prestazioni: per i documenti di grandi dimensioni, valutare la verifica di pagine specifiche anziché dell'intero documento.
4. Registra i risultati della verifica: conserva i registri dei processi di verifica per scopi di audit.
5. Esegui test con vari formati di documenti: assicurati che la verifica funzioni su tutti i formati di documenti richiesti.

## Conclusione

La verifica dei codici QR nei documenti è un aspetto essenziale per garantirne l'autenticità e l'integrità. GroupDocs.Signature per .NET fornisce un'API completa e intuitiva per implementare la verifica dei codici QR nelle applicazioni .NET.

Seguendo questo tutorial, hai imparato come:
- Configurare e inizializzare il processo di verifica
- Specificare vari criteri di verifica
- Elaborare e interpretare i risultati della verifica
- Implementare opzioni di verifica avanzate

Questa conoscenza ti consente di migliorare la sicurezza e l'affidabilità dei tuoi sistemi di gestione dei documenti.

## Domande frequenti

### GroupDocs.Signature può verificare più codici QR in un singolo documento?
Sì, GroupDocs.Signature può verificare più codici QR all'interno di un singolo documento. I risultati della verifica includeranno tutti i codici QR corrispondenti.

### Quali formati di documento sono supportati per la verifica del codice QR?
GroupDocs.Signature supporta un'ampia gamma di formati di documenti, tra cui PDF, Word (DOC, DOCX), Excel (XLS, XLSX), PowerPoint (PPT, PPTX), immagini e altro ancora.

### Posso verificare i codici QR con una crittografia o una formattazione specifiche?
Sì, GroupDocs.Signature offre opzioni per verificare i codici QR con specifici tipi di codifica e modelli di formattazione del contenuto.

### È possibile verificare i codici QR creati da applicazioni di terze parti?
Sì, GroupDocs.Signature può verificare i codici QR standard generati dalla maggior parte delle applicazioni, a condizione che rispettino i formati standard dei codici QR.

### Come posso gestire i codici QR che contengono dati binari anziché testo?
GroupDocs.Signature fornisce opzioni per verificare i codici QR con dati binari tramite `BinaryData` proprietà delle opzioni di verifica.

### Risorse correlate
* [Riferimento API GroupDocs.Signature](https://reference.groupdocs.com/signature/net/)
* [Download di GroupDocs.Signature](https://releases.groupdocs.com/signature/net/)
* [Esempi di codice su GitHub](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
* [Documentazione](https://docs.groupdocs.com/signature/net/)
* [Pagina del prodotto](https://products.groupdocs.com/signature/net/)
* [Articoli del blog](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
* [Forum di supporto](https://forum.groupdocs.com/c/signature/13)
* [Licenza temporanea](https://purchase.groupdocs.com/temporary-license/)