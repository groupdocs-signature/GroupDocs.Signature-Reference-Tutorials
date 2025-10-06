---
"description": "Implementa la verifica sicura della firma digitale nelle applicazioni .NET con GroupDocs.Signature. Guida dettagliata con esempi di codice completi per l'autenticazione dei documenti."
"linktitle": "Verifica la firma digitale"
"second_title": "API .NET GroupDocs.Signature"
"title": "Verificare le firme digitali nei documenti"
"url": "/it/net/verify-operations/verify-digital/"
"weight": 11
type: docs
---
## Introduzione

Le firme digitali svolgono un ruolo cruciale nel garantire l'autenticità, l'integrità e la non ripudiabilità dei documenti nei moderni processi aziendali. A differenza delle tradizionali firme autografe, le firme digitali utilizzano tecniche crittografiche per verificare l'identità del firmatario e garantire che il documento non sia stato alterato dopo la firma.

GroupDocs.Signature per .NET offre un toolkit completo che consente agli sviluppatori di implementare una solida verifica delle firme digitali nelle loro applicazioni .NET. Questo tutorial dettagliato vi guiderà attraverso il processo di verifica delle firme digitali all'interno dei documenti utilizzando GroupDocs.Signature per .NET.

## Prerequisiti

Prima di implementare la funzionalità di verifica della firma digitale, accertarsi di disporre dei seguenti prerequisiti:

1. GroupDocs.Signature per .NET: Scarica e installa la libreria da [GroupDocs.Signature per le versioni .NET](https://releases.groupdocs.com/signature/net/).
2. Ambiente di sviluppo .NET: Visual Studio o qualsiasi ambiente di sviluppo .NET compatibile.
3. Certificato digitale: un file di certificato digitale (ad esempio, .pfx) utilizzato per firmare il documento o un certificato appartenente alla catena attendibile.
4. Documento per la verifica: documento contenente firme digitali che necessitano di verifica.

## Importa gli spazi dei nomi richiesti

Per iniziare, importare gli spazi dei nomi necessari per accedere alla funzionalità GroupDocs.Signature:

```csharp
using System;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

Analizziamo il processo di verifica delle firme digitali in passaggi chiari e gestibili:

## Passaggio 1: specificare il percorso del documento

```csharp
// Percorso del documento contenente le firme digitali
string filePath = "sample_multiple_signatures.docx";
```

Sostituisci il percorso di esempio con il percorso effettivo del documento contenente le firme digitali.

## Passaggio 2: inizializzare l'oggetto firma

```csharp
// Crea un'istanza della classe Signature passando il percorso del documento
using (Signature signature = new Signature(filePath))
{
    // Il codice di verifica verrà implementato qui
}
```

La classe Signature è il punto di ingresso principale per tutte le operazioni nell'API GroupDocs.Signature.

## Passaggio 3: configurare le opzioni di verifica digitale

```csharp
// Opzioni di verifica della configurazione
DigitalVerifyOptions options = new DigitalVerifyOptions("YourSignature.pfx")
{
    Contact = "Mr.Smith",     // Contatto del firmatario previsto
    Password = "1234567890",  // Password del certificato, se richiesta
    AllPages = true           // Controlla tutte le pagine per le firme
};
```

Le opzioni di verifica consentono di specificare:
- Il percorso del file del certificato digitale
- Informazioni di contatto previste per il firmatario
- Password per il certificato se è protetto da password
- Intervallo di pagine da verificare (tutte le pagine per impostazione predefinita)

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
    Console.WriteLine($"Document {filePath} contains valid digital signatures!");
    
    // Visualizza i dettagli delle firme valide
    foreach (DigitalSignature digitalSignature in result.Succeeded)
    {
        Console.WriteLine($"\nValid signature found:");
        Console.WriteLine($"Signer: {digitalSignature.Subject}");
        Console.WriteLine($"Issuer: {digitalSignature.Issuer}");
        Console.WriteLine($"Valid From: {digitalSignature.ValidFrom}");
        Console.WriteLine($"Valid To: {digitalSignature.ValidTo}");
    }
}
else
{
    Console.WriteLine($"Document {filePath} failed verification process.");
    
    // Visualizzare informazioni sulle firme non riuscite, se necessario
    foreach (DigitalSignature failedSignature in result.Failed)
    {
        Console.WriteLine($"Failed signature reason: {failedSignature.Comments}");
    }
}
```

Questo codice controlla se la verifica è andata a buon fine e fornisce informazioni dettagliate sulle firme verificate.

## Esempio completo

Ecco un esempio completo e funzionante che dimostra la verifica della firma digitale:

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
                    DigitalVerifyOptions options = new DigitalVerifyOptions("YourSignature.pfx")
                    {
                        Contact = "Mr.Smith",
                        Password = "1234567890"
                    };
                    
                    // Verificare le firme dei documenti
                    VerificationResult result = signature.Verify(options);
                    
                    // Risultati della verifica del processo
                    if (result.IsValid)
                    {
                        Console.WriteLine($"Document {filePath} contains valid digital signatures!");
                        
                        foreach (DigitalSignature item in result.Succeeded)
                        {
                            Console.WriteLine($"\nValid signature found.");
                            Console.WriteLine($"Subject: {item.Subject}");
                            Console.WriteLine($"Comments: {item.Comments}");
                            Console.WriteLine($"Sign Time: {item.SignTime}");
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

### Verifica di più firme digitali

```csharp
// Crea un elenco di opzioni di verifica
List<VerifyOptions> listOptions = new List<VerifyOptions>();

// Aggiungi le prime opzioni di verifica del certificato
listOptions.Add(new DigitalVerifyOptions("Certificate1.pfx")
{
    Contact = "John Smith"
});

// Aggiungi opzioni di verifica del secondo certificato
listOptions.Add(new DigitalVerifyOptions("Certificate2.pfx")
{
    Contact = "Jane Doe"
});

// Verifica con più opzioni
VerificationResult result = signature.Verify(listOptions);
```

### Verifica delle firme su pagine specifiche

```csharp
// Verificare le firme digitali solo sulla prima pagina
DigitalVerifyOptions options = new DigitalVerifyOptions("YourSignature.pfx")
{
    AllPages = false,
    PageNumber = 1
};
```

### Utilizzo della convalida del timestamp e dell'autorità di certificazione

```csharp
DigitalVerifyOptions options = new DigitalVerifyOptions("YourSignature.pfx")
{
    ValidateTimeStampOnly = true,   // Convalida solo il timestamp
    CertificateAuth = CertificateAuthType.Standard  // Convalida il certificato del firmatario
};
```

## Migliori pratiche per la verifica della firma digitale

1. Gestione corretta dei certificati: archiviare i file dei certificati in modo sicuro e gestire le password in modo appropriato.
2. Convalida del certificato: implementare la convalida della catena di certificati per garantire la validità del certificato stesso.
3. Gestione degli errori: implementare una gestione degli errori solida per gestire in modo efficiente gli errori di verifica.
4. Registrazione: registra i tentativi di verifica e i risultati per scopi di audit e conformità.
5. Aggiornamenti regolari dei certificati: assicurati che i certificati vengano aggiornati prima della scadenza.

## Risoluzione dei problemi comuni

### Certificato non valido
- Verificare che il percorso del file del certificato sia corretto
- Assicurarsi che la password del certificato sia corretta
- Controlla se il certificato è scaduto

### Firma non trovata
- Confermare che il documento contenga effettivamente firme digitali
- Verifica di controllare le pagine corrette

### Errori di verifica
- Verificare se il documento è stato modificato dopo la firma
- Verificare che il certificato del firmatario sia nella catena di certificati attendibili

## Conclusione

GroupDocs.Signature per .NET offre una soluzione potente e flessibile per la verifica delle firme digitali nei documenti. Seguendo questa guida dettagliata, è possibile implementare una solida verifica delle firme digitali nelle applicazioni .NET, garantendo l'autenticità e l'integrità dei documenti.

La verifica della firma digitale è una componente fondamentale per flussi di lavoro documentali sicuri negli ambienti aziendali moderni. Con GroupDocs.Signature, è possibile implementare questa funzionalità in modo sicuro e con il minimo sforzo, sfruttando l'API completa per gestire diversi scenari di verifica.

## Domande frequenti

### GroupDocs.Signature può verificare le firme nei documenti PDF firmati con Adobe Acrobat?
Sì, GroupDocs.Signature può verificare le firme digitali standard nei documenti PDF creati da Adobe Acrobat e altri software PDF compatibili.

### GroupDocs.Signature supporta la verifica dei timestamp dei documenti?
Sì, l'API fornisce opzioni per verificare i timestamp dei documenti come parte del processo di verifica della firma digitale.

### Posso verificare le firme su pagine specifiche di un documento composto da più pagine?
Sì, puoi configurare le opzioni di verifica per controllare le firme su pagine specifiche anziché sull'intero documento.

### GroupDocs.Signature supporta la verifica di più firme all'interno di un singolo documento?
Sì, GroupDocs.Signature può verificare più firme digitali all'interno di un singolo documento e fornire risultati dettagliati per ciascuna firma.

### È possibile verificare le firme create con certificati di diverse autorità di certificazione?
Sì, GroupDocs.Signature supporta la verifica delle firme create con certificati provenienti da diverse autorità di certificazione, purché si trovino nella catena di certificati attendibili.

### Risorse correlate
* [Riferimento API GroupDocs.Signature](https://reference.groupdocs.com/signature/net/)
* [Download di GroupDocs.Signature](https://releases.groupdocs.com/signature/net/)
* [Esempi di codice su GitHub](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
* [Documentazione](https://docs.groupdocs.com/signature/net/)
* [Pagina del prodotto](https://products.groupdocs.com/signature/net/)
* [Articoli del blog](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
* [Forum di supporto](https://forum.groupdocs.com/c/signature/13)
* [Licenza temporanea](https://purchase.groupdocs.com/temporary-license/)