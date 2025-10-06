---
"description": "Implementa una solida verifica dei codici a barre nelle applicazioni .NET con GroupDocs.Signature. Esempi di codice completi e best practice per garantire l'autenticità dei documenti."
"linktitle": "Verifica codice a barre"
"second_title": "API .NET GroupDocs.Signature"
"title": "Verifica le firme dei codici a barre nei documenti"
"url": "/it/net/verify-operations/verify-barcode/"
"weight": 10
type: docs
---
## Introduzione

codici a barre sono diventati parte integrante dei moderni sistemi di gestione documentale, consentendo un rapido accesso alle informazioni codificate e fungendo anche da misura di sicurezza. GroupDocs.Signature per .NET fornisce una potente API per la verifica delle firme con codice a barre all'interno dei documenti, garantendone l'autenticità e l'integrità.

Questo tutorial completo esplora il processo di implementazione della verifica dei codici a barre nelle applicazioni .NET utilizzando GroupDocs.Signature. Che si lavori con documenti aziendali, certificati, contratti o qualsiasi tipo di documento che utilizzi codici a barre per l'autenticazione, questa guida ti aiuterà a implementare funzionalità di verifica affidabili.

## Prerequisiti

Prima di implementare la funzionalità di verifica del codice a barre, assicurati di disporre dei seguenti prerequisiti:

1. GroupDocs.Signature per .NET: Scarica e installa la libreria da [pagina di download](https://releases.groupdocs.com/signature/net/).
2. Ambiente di sviluppo .NET: Visual Studio o qualsiasi ambiente di sviluppo .NET compatibile.
3. Conoscenze di base: familiarità con la programmazione C# e i concetti del framework .NET.
4. Documento di prova: documento contenente firme con codice a barre a scopo di verifica.

## Importa gli spazi dei nomi richiesti

Per iniziare, importare gli spazi dei nomi necessari per accedere alla funzionalità GroupDocs.Signature:

```csharp
using System;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

Scomponiamo il processo di verifica del codice a barre in passaggi chiari e gestibili:

## Passaggio 1: specificare il percorso del documento

```csharp
// Percorso del documento contenente le firme con codice a barre
string filePath = "sample_multiple_signatures.docx";
```

Assicurati di sostituire il percorso di esempio con il percorso effettivo del documento contenente le firme con codice a barre.

## Passaggio 2: inizializzare l'oggetto firma

```csharp
// Crea un'istanza della classe Signature passando il percorso del documento
using (Signature signature = new Signature(filePath))
{
    // Il codice di verifica verrà implementato qui
}
```

La classe Signature è il punto di ingresso principale per tutte le operazioni nell'API GroupDocs.Signature.

## Passaggio 3: configurare le opzioni di verifica del codice a barre

```csharp
// Definisci le opzioni di verifica del codice a barre
BarcodeVerifyOptions options = new BarcodeVerifyOptions()
{
    AllPages = true,           // Controlla tutte le pagine del documento
    Text = "12345",            // Testo da abbinare al codice a barre
    MatchType = TextMatchType.Contains // Specificare i criteri di corrispondenza del testo
};
```

Le opzioni di verifica consentono di definire criteri specifici per il processo di verifica:
- `AllPages`: Imposta su true per controllare tutte le pagine del documento
- `Text`: Il contenuto del testo da abbinare al codice a barre
- `MatchType`: Il metodo per la corrispondenza del testo (Contiene, Esatto, Inizia con, Termina con)

## Fase 4: Eseguire il processo di verifica

```csharp
// Eseguire la verifica
VerificationResult result = signature.Verify(options);
```

In questo modo viene eseguito il processo di verifica in base alle opzioni specificate.

## Fase 5: Risultati della verifica del processo

```csharp
// Controllare il risultato della verifica e procedere di conseguenza
if (result.IsValid)
{
    Console.WriteLine($"Document {filePath} contains valid barcode signatures!");
    
    // Visualizza informazioni sulle firme riuscite
    foreach (BarcodeSignature barcodeSignature in result.Succeeded)
    {
        Console.WriteLine($"\nFound valid barcode signature:");
        Console.WriteLine($"Text: {barcodeSignature.Text}");
        Console.WriteLine($"Type: {barcodeSignature.EncodeType.TypeName}");
        Console.WriteLine($"Location: Page {barcodeSignature.PageNumber}, {barcodeSignature.Left}x{barcodeSignature.Top}");
    }
}
else
{
    Console.WriteLine($"Document {filePath} failed verification process.");
    Console.WriteLine($"Number of failed signatures: {result.Failed.Count}");
}
```

Questo codice controlla se la verifica è andata a buon fine e fornisce informazioni dettagliate sulle firme dei codici a barre verificate.

## Esempio completo

Ecco un esempio completo e funzionante che dimostra la verifica tramite codice a barre:

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
            
            try
            {
                // Inizializza l'istanza della firma
                using (Signature signature = new Signature(filePath))
                {
                    // Opzioni di verifica della configurazione
                    BarcodeVerifyOptions options = new BarcodeVerifyOptions()
                    {
                        AllPages = true,
                        Text = "12345",
                        MatchType = TextMatchType.Contains
                    };
                    
                    // Verificare le firme dei documenti
                    VerificationResult result = signature.Verify(options);
                    
                    // Risultati della verifica del processo
                    if (result.IsValid)
                    {
                        Console.WriteLine($"Document {filePath} contains valid barcode signatures!");
                        
                        foreach (BarcodeSignature item in result.Succeeded)
                        {
                            Console.WriteLine($"\nValid signature found with text: {item.Text}");
                            Console.WriteLine($"Barcode type: {item.EncodeType.TypeName}");
                            Console.WriteLine($"Page: {item.PageNumber}");
                        }
                    }
                    else
                    {
                        Console.WriteLine($"\nDocument {filePath} failed verification process.");
                    }
                }
            }
            catch (Exception ex)
            {
                Console.WriteLine($"Error: {ex.Message}");
            }
        }
    }
}
```

## Scenari di verifica avanzati

GroupDocs.Signature fornisce opzioni aggiuntive per scenari di verifica più complessi:

### Verifica di tipi specifici di codici a barre

Se conosci il tipo specifico di codice a barre che stai cercando, puoi limitare la verifica a quel tipo:

```csharp
BarcodeVerifyOptions options = new BarcodeVerifyOptions()
{
    EncodeType = BarcodeTypes.Code128,  // Verificare solo i codici a barre Code128
    Text = "PROD-12345",
    MatchType = TextMatchType.Exact
};
```

### Verifica dei codici a barre su pagine specifiche

Per i documenti composti da più pagine, è possibile limitare la verifica a pagine specifiche:

```csharp
BarcodeVerifyOptions options = new BarcodeVerifyOptions()
{
    AllPages = false,
    PageNumber = 2,  // Verificare solo a pagina 2
    Text = "INV-2023"
};
```

### Utilizzo di espressioni regolari per la verifica

Per una corrispondenza di pattern più flessibile, è possibile utilizzare le espressioni regolari:

```csharp
BarcodeVerifyOptions options = new BarcodeVerifyOptions()
{
    Text = "INV-\\d{4}-\\d{2}",  // Abbina i numeri di fattura come INV-2023-01
    MatchType = TextMatchType.Regex
};
```

### Verifica simultanea di più tipi di codici a barre

È possibile creare più opzioni di verifica per verificare diversi tipi di codici a barre:

```csharp
// Crea un elenco di opzioni di verifica
List<VerifyOptions> listOptions = new List<VerifyOptions>();

// Aggiungi la verifica del codice QR
listOptions.Add(new BarcodeVerifyOptions()
{
    EncodeType = BarcodeTypes.QR,
    Text = "Security"
});

// Aggiungi la verifica Code128
listOptions.Add(new BarcodeVerifyOptions()
{
    EncodeType = BarcodeTypes.Code128,
    Text = "12345"
});

// Verifica con più opzioni
VerificationResult result = signature.Verify(listOptions);
```

## Best Practice per la verifica dei codici a barre

1. Gestione degli errori: implementare sempre una corretta gestione degli errori per gestire con eleganza gli scenari imprevisti.
2. Ottimizzazione delle prestazioni: per i documenti di grandi dimensioni, valutare la possibilità di verificare pagine specifiche anziché l'intero documento.
3. Registrazione: implementare la registrazione per tenere traccia dei tentativi di verifica e dei risultati a fini di audit.
4. Considerazioni sulla sicurezza: conservare i criteri di verifica in modo sicuro, soprattutto se fanno parte della propria infrastruttura di sicurezza.
5. Test: verifica dei test con vari formati di documenti e tipi di codici a barre per garantire la compatibilità.

## Risoluzione dei problemi comuni

### Codice a barre non rilevato
- Assicurarsi che il codice a barre sia chiaramente visibile nel documento
- Verificare se il tipo di codice a barre è supportato da GroupDocs.Signature
- Verificare che il codice a barre non sia distorto o danneggiato

### Errori di verifica
- Confermare che i criteri di verifica (testo, tipo di codice a barre) siano corretti
- Controlla se MatchType è appropriato per il tuo caso d'uso
- Verificare che il documento non sia stato modificato da quando è stato applicato il codice a barre

### Problemi di prestazioni
- Ottimizza la verifica prendendo di mira pagine specifiche in cui sono previsti codici a barre
- Limitare la verifica a tipi specifici di codici a barre se noti in anticipo

## Conclusione

La verifica dei codici a barre è uno strumento essenziale per garantire l'autenticità e l'integrità dei documenti nei moderni sistemi di gestione documentale. GroupDocs.Signature per .NET fornisce un'API completa e di facile utilizzo per implementare solide funzionalità di verifica dei codici a barre nelle applicazioni .NET.

Seguendo questa guida passo passo, hai imparato come:
- Configurare e inizializzare il processo di verifica
- Specificare vari criteri di verifica
- Elaborare e interpretare i risultati della verifica
- Implementare scenari di verifica avanzati

Queste funzionalità consentono di creare sistemi di elaborazione dei documenti sicuri e affidabili, in grado di verificare l'autenticità dei codici a barre in vari formati di documento.

## Domande frequenti

### Quali formati di documento sono supportati per la verifica del codice a barre?
GroupDocs.Signature supporta un'ampia gamma di formati di documenti, tra cui PDF, documenti Word (DOC, DOCX), fogli di calcolo Excel (XLS, XLSX), presentazioni PowerPoint (PPT, PPTX), immagini e altro ancora.

### GroupDocs.Signature può verificare più codici a barre in un singolo documento?
Sì, GroupDocs.Signature può verificare più codici a barre all'interno di un singolo documento. I risultati della verifica includeranno tutti i codici a barre corrispondenti.

### Quali tipi di codici a barre sono supportati per la verifica?
GroupDocs.Signature supporta numerosi tipi di codici a barre, tra cui Code39, Code128, EAN13, EAN8, QR Code, DataMatrix, PDF417 e molti altri.

### Posso verificare i codici a barre nei documenti protetti da password?
Sì, GroupDocs.Signature fornisce opzioni per specificare le password dei documenti quando si aprono documenti protetti per la verifica.

### È possibile verificare i codici a barre che contengono dati binari anziché testo?
Sì, GroupDocs.Signature fornisce opzioni per la verifica dei codici a barre con dati binari tramite `BinaryData` proprietà delle opzioni di verifica.

### Risorse correlate
* [Riferimento API GroupDocs.Signature](https://reference.groupdocs.com/signature/net/)
* [Download di GroupDocs.Signature](https://releases.groupdocs.com/signature/net/)
* [Esempi di codice su GitHub](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
* [Documentazione](https://docs.groupdocs.com/signature/net/)
* [Pagina del prodotto](https://products.groupdocs.com/signature/net/)
* [Articoli del blog](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
* [Forum di supporto](https://forum.groupdocs.com/c/signature/13)
* [Licenza temporanea](https://purchase.groupdocs.com/temporary-license/)