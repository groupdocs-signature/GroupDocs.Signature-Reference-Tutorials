---
"description": "Scopri come cercare in modo efficiente i codici QR nei documenti utilizzando GroupDocs.Signature per .NET con questa guida completa passo dopo passo ed esempi di codice."
"linktitle": "Cerca codici QR"
"second_title": "API .NET GroupDocs.Signature"
"title": "Cerca firme con codice QR nei documenti"
"url": "/it/net/signature-searching/search-for-qr-codes/"
"weight": 15
type: docs
---
## Introduzione

Nell'attuale ecosistema dei documenti digitali, le firme con codice QR sono diventate uno strumento prezioso per incorporare informazioni, autenticare e migliorare la sicurezza dei documenti. GroupDocs.Signature per .NET offre agli sviluppatori una potente API per cercare ed estrarre codici QR da vari formati di documento, consentendo funzionalità avanzate di analisi e verifica dei documenti nelle applicazioni .NET.

Questo tutorial completo ti guiderà attraverso il processo di implementazione della funzionalità di ricerca tramite codice QR utilizzando GroupDocs.Signature per .NET, fornendo spiegazioni chiare, istruzioni dettagliate ed esempi di codice pratici che potrai integrare nelle tue applicazioni.

## Prerequisiti

Prima di iniziare a cercare la firma tramite codice QR, assicurati di disporre dei seguenti prerequisiti:

1. GroupDocs.Signature per .NET SDK: scarica e installa l'SDK da [pagina di download](https://releases.groupdocs.com/signature/net/).

2. Ambiente di sviluppo: configurare un ambiente di sviluppo .NET, come Visual Studio, con installato .NET Framework o .NET Core.

3. Conoscenze di base: familiarità con la programmazione C# e con i concetti di sviluppo .NET.

4. Documenti campione: preparare documenti di prova contenenti codici QR per la verifica e il test.

## Importa spazi dei nomi

Per iniziare, importare gli spazi dei nomi necessari per accedere alla funzionalità GroupDocs.Signature:

```csharp
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
using System;
using System.Collections.Generic;
```

Ora, scomponiamo il processo di ricerca dei codici QR in passaggi chiari e facili da seguire:

## Passaggio 1: definire il percorso del documento

Per prima cosa, specifica il percorso del documento contenente i codici QR che vuoi cercare:

```csharp
string filePath = "sample_multiple_signatures.docx";
```

## Passaggio 2: inizializzare l'oggetto firma

Crea un'istanza di `Signature` classe passando il percorso del documento:

```csharp
using (Signature signature = new Signature(filePath))
{
    // Il codice di ricerca del codice QR verrà aggiunto qui
}
```

## Passaggio 3: Cerca le firme del codice QR

Utilizzare il `Search` metodo con il tipo di firma appropriato per trovare i codici QR nel documento:

```csharp
// Cerca le firme del codice QR all'interno del documento
List<QrCodeSignature> signatures = signature.Search<QrCodeSignature>(SignatureType.QrCode);
```

## Fase 4: Elaborazione e visualizzazione dei risultati

Scorri le firme dei codici QR trovati e accedi alle loro proprietà:

```csharp
// Visualizza informazioni sui codici QR trovati
Console.WriteLine($"\nSource document contains {signatures.Count} QR code signature(s):");

foreach (var qrCodeSignature in signatures)
{
    Console.WriteLine($"QR Code found at page {qrCodeSignature.PageNumber} with type {qrCodeSignature.EncodeType.TypeName}");
    Console.WriteLine($"Content: {qrCodeSignature.Text}");
    Console.WriteLine($"Location: X={qrCodeSignature.Left}, Y={qrCodeSignature.Top}, Width={qrCodeSignature.Width}, Height={qrCodeSignature.Height}");
    Console.WriteLine();
}
```

## Esempio completo

Ecco un esempio pratico e completo che illustra il processo completo di ricerca dei codici QR in un documento:

```csharp
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
using System;
using System.Collections.Generic;

namespace QrCodeSignatureSearch
{
    class Program
    {
        static void Main(string[] args)
        {
            // Percorso del documento: aggiorna con il percorso del tuo file
            string filePath = "sample_multiple_signatures.docx";
            
            // Inizializza l'istanza della firma
            using (Signature signature = new Signature(filePath))
            {
                try
                {
                    // Cerca le firme del codice QR nel documento
                    List<QrCodeSignature> signatures = signature.Search<QrCodeSignature>(SignatureType.QrCode);
                    
                    // Visualizza i risultati della ricerca
                    Console.WriteLine($"\nSource document ['{filePath}'] contains {signatures.Count} QR code signature(s):");
                    
                    foreach (var qrCodeSignature in signatures)
                    {
                        Console.WriteLine($"QR Code found at page {qrCodeSignature.PageNumber} with type {qrCodeSignature.EncodeType.TypeName}");
                        Console.WriteLine($"Content: {qrCodeSignature.Text}");
                        Console.WriteLine($"Location: X={qrCodeSignature.Left}, Y={qrCodeSignature.Top}, Width={qrCodeSignature.Width}, Height={qrCodeSignature.Height}");
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

## Tecniche avanzate di ricerca tramite codice QR

### Ricerca con criteri specifici

Per ricerche più mirate, puoi utilizzare `QrCodeSearchOptions` per personalizzare i criteri di ricerca:

```csharp
// Crea opzioni di ricerca del codice QR con criteri specifici
QrCodeSearchOptions options = new QrCodeSearchOptions
{
    // Cerca solo su pagine specifiche
    AllPages = false,
    PageNumber = 1,
    PagesSetup = new PagesSetup { Pages = new List<int> { 1, 3, 5 } },
    
    // Filtra per contenuto del codice QR
    Text = "Invoice",
    MatchType = TextMatchType.Contains,
    
    // Filtra per tipi specifici di codice QR
    EncodeType = QrCodeTypes.QR,
    
    // Definisci un'area specifica in cui effettuare la ricerca
    Rectangle = new Rectangle(100, 100, 400, 400)
};

// Cerca con opzioni specifiche
List<QrCodeSignature> filteredSignatures = signature.Search<QrCodeSignature>(options);
```

### Elaborazione dei dati del codice QR

È possibile implementare un'elaborazione personalizzata per i dati del codice QR in base ai requisiti della propria applicazione:

```csharp
foreach (var qrCode in signatures)
{
    // Estrarre ed elaborare i dati del codice QR in base al contenuto
    string qrContent = qrCode.Text;
    
    if (qrContent.StartsWith("URL:"))
    {
        // Elaborare i dati URL
        string url = qrContent.Substring(4);
        Console.WriteLine($"Found URL in QR code: {url}");
    }
    else if (qrContent.StartsWith("CONTACT:"))
    {
        // Elaborare le informazioni di contatto
        string contact = qrContent.Substring(8);
        Console.WriteLine($"Found contact information in QR code: {contact}");
    }
    else if (qrContent.StartsWith("INVOICE:"))
    {
        // Elaborare le informazioni sulla fattura
        string invoiceData = qrContent.Substring(8);
        Console.WriteLine($"Found invoice information in QR code: {invoiceData}");
        
        // Analizzare e convalidare i dati della fattura
        if (ValidateInvoiceData(invoiceData))
        {
            Console.WriteLine("Invoice data is valid!");
        }
        else
        {
            Console.WriteLine("Warning: Invalid invoice data detected!");
        }
    }
}

// Esempio di metodo di convalida
static bool ValidateInvoiceData(string data)
{
    // Implementa la tua logica di convalida
    return !string.IsNullOrEmpty(data) && data.Contains("ID") && data.Contains("Amount");
}
```

### Implementazione della verifica di sicurezza

I codici QR vengono spesso utilizzati per scopi di autenticazione. Ecco come implementare una verifica di sicurezza di base:

```csharp
// Controlla se il documento contiene un codice QR di autenticazione valido
bool hasValidAuthQrCode = false;

foreach (var qrCode in signatures)
{
    if (qrCode.Text.StartsWith("AUTH:"))
    {
        string authCode = qrCode.Text.Substring(5);
        
        // Verificare il codice di autenticazione (ad esempio, rispetto a un database o a un elenco predefinito)
        if (VerifyAuthCode(authCode))
        {
            hasValidAuthQrCode = true;
            Console.WriteLine("Document contains valid authentication QR code!");
            break;
        }
    }
}

if (!hasValidAuthQrCode)
{
    Console.WriteLine("Warning: Document does not contain a valid authentication QR code!");
}

// Esempio di metodo di verifica
static bool VerifyAuthCode(string code)
{
    // Implementa la tua logica di verifica
    // Potrebbe trattarsi di una ricerca nel database, di una chiamata API o di un confronto con valori predefiniti
    return code == "A7B82C3D" || code == "X9Y8Z7W6";
}
```

### Estrazione di immagini di codici QR

È possibile estrarre le immagini dei codici QR dai documenti per elaborarle ulteriormente o visualizzarle:

```csharp
// Salva le immagini del codice QR sul disco
foreach (var qrCode in signatures)
{
    if (qrCode.Content != null)
    {
        // Crea un nome file univoco in base al numero di pagina e alla posizione
        string outputPath = $"QrCode_P{qrCode.PageNumber}_X{qrCode.Left}_Y{qrCode.Top}.png";
        
        // Salva i dati dell'immagine
        File.WriteAllBytes(outputPath, qrCode.Content);
        Console.WriteLine($"Saved QR code image to {outputPath}");
    }
}
```

## Conclusione

In questa guida completa, abbiamo esplorato come cercare firme con codice QR nei documenti utilizzando GroupDocs.Signature per .NET. Dalla ricerca di base alle tecniche avanzate, ora hai le conoscenze necessarie per implementare una gestione affidabile dei codici QR nelle tue applicazioni .NET. L'API GroupDocs.Signature fornisce un framework potente e flessibile per lavorare con vari tipi di firme, inclusi i codici QR, in diversi formati di documento.

Sfruttando queste funzionalità, puoi migliorare i processi di verifica dei documenti, implementare sistemi di autenticazione ed estrarre informazioni preziose incorporate nei codici QR, il tutto all'interno delle tue applicazioni .NET.

## Domande frequenti

### Quali formati di codice QR sono supportati da GroupDocs.Signature?

GroupDocs.Signature supporta vari formati di codici QR, tra cui il codice QR standard, il micro codice QR e altri standard comuni. Il formato specifico è accessibile tramite `EncodeType` proprietà del `QrCodeSignature` oggetto.

### Posso cercare codici QR nei documenti protetti da password?

Sì, GroupDocs.Signature supporta la ricerca di codici QR nei documenti protetti da password fornendo la password durante l'inizializzazione `Signature` oggetto:

```csharp
LoadOptions loadOptions = new LoadOptions { Password = "your_password" };
using (Signature signature = new Signature(filePath, loadOptions))
{
    // Cerca i codici QR
}
```

### Come posso filtrare i codici QR in base al loro contenuto?

Puoi filtrare i codici QR in base al loro contenuto utilizzando `Text` E `MatchType` proprietà di `QrCodeSearchOptions`:

```csharp
QrCodeSearchOptions options = new QrCodeSearchOptions
{
    Text = "Invoice",
    MatchType = TextMatchType.Contains // Altre opzioni: Esatto, Inizia con, Termina con
};
```

### GroupDocs.Signature può rilevare codici QR danneggiati o parzialmente visibili?

GroupDocs.Signature ha una certa capacità di rilevare codici QR parzialmente visibili, ma i codici QR gravemente danneggiati potrebbero non essere riconosciuti. La precisione del rilevamento dipende dalla qualità e dalla visibilità del codice QR nel documento.

### Quali formati di documento sono supportati per la ricerca tramite codice QR?

GroupDocs.Signature supporta la ricerca tramite codice QR in vari formati di documenti, tra cui PDF, documenti Microsoft Office (Word, Excel, PowerPoint), immagini (JPEG, PNG, TIFF) e molti altri.

## Vedi anche

* [Riferimento API](https://reference.groupdocs.com/signature/net/)
* [Esempi di codice su GitHub](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
* [Documentazione del prodotto](https://docs.groupdocs.com/signature/net/)
* [Pagina del prodotto](https://products.groupdocs.com/signature/net/)
* [Scarica l'ultima versione](https://releases.groupdocs.com/signature/net/)
* [Articoli del blog](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
* [Forum di supporto gratuito](https://forum.groupdocs.com/c/signature/13)
* [Licenza temporanea](https://purchase.groupdocs.com/temporary-license/)