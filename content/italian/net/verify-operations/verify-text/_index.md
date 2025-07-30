---
"description": "Padroneggia la verifica della firma testuale nelle applicazioni .NET con GroupDocs.Signature. Guida all'implementazione dettagliata con esempi di codice completi e best practice."
"linktitle": "Verifica testo"
"second_title": "API .NET GroupDocs.Signature"
"title": "Verifica le firme di testo nei documenti"
"url": "/it/net/verify-operations/verify-text/"
"weight": 13
---

## Introduzione

Le firme testuali, sebbene spesso più semplici delle firme digitali o elettroniche, svolgono un ruolo cruciale nella gestione e nella verifica dei documenti. Che si tratti di filigrane, testo a piè di pagina o specifici pattern di contenuto, convalidare la presenza e l'integrità delle firme testuali è un aspetto importante dei processi di verifica dei documenti.

GroupDocs.Signature per .NET fornisce una potente API per la verifica delle firme testuali all'interno di documenti in un'ampia gamma di formati. Questo tutorial completo ti guiderà nell'implementazione della funzionalità di verifica del testo nelle tue applicazioni .NET, garantendo che i tuoi documenti mantengano la loro integrità e autenticità.

## Prerequisiti

Prima di implementare la funzionalità di verifica del testo, assicurati di disporre dei seguenti prerequisiti:

1. GroupDocs.Signature per .NET: Scarica e installa la libreria da [pagina di download](https://releases.groupdocs.com/signature/net/).
2. Ambiente di sviluppo .NET: Visual Studio o qualsiasi ambiente di sviluppo .NET compatibile.
3. Conoscenze di base: familiarità con la programmazione C# e i concetti del framework .NET.
4. Documento di prova: documento contenente firme di testo a scopo di verifica.

## Importa gli spazi dei nomi richiesti

Per iniziare, importare gli spazi dei nomi necessari per accedere alla funzionalità GroupDocs.Signature:

```csharp
using System;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

Analizziamo il processo di verifica del testo in passaggi chiari e gestibili:

## Passaggio 1: specificare il percorso del documento

```csharp
// Percorso del documento contenente le firme di testo
string filePath = "sample_multiple_signatures.docx";
```

Assicurati di sostituire il percorso di esempio con il percorso effettivo del documento contenente le firme di testo.

## Passaggio 2: inizializzare l'oggetto firma

```csharp
// Crea un'istanza della classe Signature passando il percorso del documento
using (Signature signature = new Signature(filePath))
{
    // Il codice di verifica verrà implementato qui
}
```

La classe Signature è il punto di ingresso principale per tutte le operazioni nell'API GroupDocs.Signature.

## Passaggio 3: configurare le opzioni di verifica del testo

```csharp
// Definisci le opzioni di verifica del testo
TextVerifyOptions options = new TextVerifyOptions()
{
    AllPages = true,                               // Controlla tutte le pagine del documento
    SignatureImplementation = TextSignatureImplementation.Native,
    Text = "signature",                            // Testo da verificare
    MatchType = TextMatchType.Contains             // Specificare i criteri di corrispondenza
};
```

Le opzioni di verifica consentono di definire criteri specifici per il processo di verifica:
- `AllPages`: Imposta su true per controllare tutte le pagine del documento
- `SignatureImplementation`: Specifica come viene implementato il testo (Nativo o Adesivo)
- `Text`: Il contenuto del testo da abbinare all'interno del documento
- `MatchType`: Il metodo per la corrispondenza del testo (Contiene, Esatto, Inizia con, ecc.)

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
    Console.WriteLine($"Document {filePath} contains valid text signatures!");
    
    // Visualizza informazioni sulle firme riuscite
    foreach (TextSignature textSignature in result.Succeeded)
    {
        Console.WriteLine($"\nFound valid text signature:");
        Console.WriteLine($"Text: {textSignature.Text}");
        Console.WriteLine($"Location: Page {textSignature.PageNumber}, {textSignature.Left}x{textSignature.Top}");
    }
}
else
{
    Console.WriteLine($"Document {filePath} failed verification process.");
    Console.WriteLine($"Number of failed signatures: {result.Failed.Count}");
}
```

Questo codice controlla se la verifica è andata a buon fine e fornisce informazioni dettagliate sulle firme di testo verificate.

## Esempio completo

Ecco un esempio completo e funzionante che dimostra la verifica della firma del testo:

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
                    TextVerifyOptions options = new TextVerifyOptions()
                    {
                        AllPages = true,
                        SignatureImplementation = TextSignatureImplementation.Native,
                        Text = "signature",
                        MatchType = TextMatchType.Contains
                    };
                    
                    // Verificare le firme dei documenti
                    VerificationResult result = signature.Verify(options);
                    
                    // Risultati della verifica del processo
                    if(result.IsValid)
                    {
                        Console.WriteLine($"\nDocument {filePath} was verified successfully!");
                        foreach (TextSignature item in result.Succeeded)
                        {
                            Console.WriteLine($"\nValid signature is found with text: {item.Text}");
                            Console.WriteLine($"Location: Page {item.PageNumber}, position {item.Left}x{item.Top}");
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

### Utilizzo di espressioni regolari per la verifica

Per una corrispondenza di pattern più flessibile, è possibile utilizzare le espressioni regolari:

```csharp
TextVerifyOptions options = new TextVerifyOptions()
{
    Text = "Invoice\\s+#\\d{5,6}",  // Abbina modelli come "Fattura n. 12345"
    MatchType = TextMatchType.Regex
};
```

### Verifica del testo in aree specifiche del documento

È possibile limitare la verifica ad aree specifiche del documento:

```csharp
TextVerifyOptions options = new TextVerifyOptions()
{
    AllPages = false,
    PageNumber = 1,  // Verifica solo sulla prima pagina
    
    // Definisci l'area in cui effettuare la ricerca (coordinate in punti)
    PagesSetup = new PagesSetup() 
    { 
        FirstPage = true,
        LastPage = false,
        OddPages = false,
        EvenPages = false 
    },
    
    // Area del rettangolo in millimetri
    Rectangle = new Rectangle(10, 10, 100, 30),
    
    Text = "Confidential"
};
```

### Verifica simultanea di più modelli di testo

È possibile creare più opzioni di verifica per verificare diversi modelli di testo:

```csharp
// Crea un elenco di opzioni di verifica
List<VerifyOptions> listOptions = new List<VerifyOptions>();

// Aggiungi la prima verifica del testo
listOptions.Add(new TextVerifyOptions()
{
    Text = "Confidential",
    MatchType = TextMatchType.Exact
});

// Aggiungi una seconda verifica del testo
listOptions.Add(new TextVerifyOptions()
{
    Text = "Do not copy",
    MatchType = TextMatchType.Contains
});

// Verifica con più opzioni
VerificationResult result = signature.Verify(listOptions);
```

### Verifica del testo con aspetto specifico

È anche possibile verificare il testo con caratteristiche di formattazione specifiche:

```csharp
TextVerifyOptions options = new TextVerifyOptions()
{
    Text = "APPROVED",
    MatchType = TextMatchType.Exact,
    
    // Verificare le proprietà specifiche dell'aspetto
    ForegroundColorRGB = System.Drawing.Color.Green,
    Font = new SignatureFont() { FontFamily = "Arial", FontSize = 12, Bold = true }
};
```

## Buone pratiche per la verifica del testo

1. Scegli i tipi di corrispondenza appropriati: seleziona il tipo di corrispondenza corretto (Contiene, Esatto, Regex) in base ai tuoi requisiti di verifica.
2. Ottimizzazione delle prestazioni: per i documenti di grandi dimensioni, valutare la possibilità di verificare pagine specifiche anziché l'intero documento.
3. Gestione degli errori: implementare una corretta gestione degli errori per gestire con eleganza gli scenari imprevisti.
4. Tieni presente la distinzione tra maiuscole e minuscole: tieni presente la distinzione tra maiuscole e minuscole nella corrispondenza del testo, soprattutto per le verifiche critiche.
5. Test approfonditi: testare la verifica con vari formati di documenti e modelli di testo per garantire la compatibilità.

## Risoluzione dei problemi comuni

### Testo non rilevato
- Verificare se la formattazione o la codifica del testo influiscono sul rilevamento
- Assicurati che il testo sia effettivamente presente nel documento come testo normale (non come immagine)
- Prova diversi criteri di corrispondenza (Contiene invece di Esatto)

### Problemi di prestazioni
- Ottimizza la verifica prendendo di mira pagine o aree specifiche
- Utilizzare modelli di testo più specifici per ridurre i falsi positivi

### Errori di verifica
- Controlla se spazi, caratteri speciali o formattazione influenzano la corrispondenza
- Verificare che il testo non faccia parte di un'immagine scansionata (che richiede l'OCR)
- Assicurati che il documento non sia stato modificato da quando è stato aggiunto il testo

## Conclusione

La verifica testuale è un approccio versatile e pratico all'autenticazione dei documenti, che può essere utilizzato da solo o in combinazione con altri metodi di verifica. GroupDocs.Signature per .NET fornisce un'API completa e di facile utilizzo per implementare funzionalità di verifica testuale affidabili nelle applicazioni .NET.

Seguendo questa guida passo passo, hai imparato come:
- Configurare e inizializzare il processo di verifica del testo
- Specificare vari criteri di verifica
- Elaborare e interpretare i risultati della verifica
- Implementare scenari di verifica avanzati

Queste funzionalità consentono di creare sistemi di elaborazione dei documenti sicuri e affidabili, in grado di verificare l'autenticità del testo in vari formati di documento.

## Domande frequenti

### GroupDocs.Signature può verificare il testo nei documenti scansionati?
GroupDocs.Signature è progettato principalmente per la verifica di testo digitale. Per i documenti scansionati, è necessario utilizzare prima la tecnologia OCR (riconoscimento ottico dei caratteri) per convertire le immagini scansionate in testo.

### Quali formati di documento sono supportati per la verifica del testo?
GroupDocs.Signature supporta un'ampia gamma di formati di documenti, tra cui PDF, documenti Word (DOC, DOCX), fogli di calcolo Excel (XLS, XLSX), presentazioni PowerPoint (PPT, PPTX), immagini e altro ancora.

### Posso verificare il testo formattato (grassetto, corsivo, caratteri specifici)?
Sì, GroupDocs.Signature fornisce opzioni per verificare il testo con caratteristiche di formattazione specifiche, tra cui tipo di carattere, dimensione, stile (grassetto, corsivo) e colore.

### È possibile verificare il testo nei documenti protetti da password?
Sì, GroupDocs.Signature fornisce opzioni per specificare le password dei documenti quando si aprono documenti protetti per la verifica.

### Posso verificare le filigrane e il testo di sfondo?
Sì, GroupDocs.Signature può verificare vari tipi di firme di testo, tra cui filigrane e testo di sfondo, a seconda di come sono state implementate nel documento.

### Risorse correlate
* [Riferimento API GroupDocs.Signature](https://reference.groupdocs.com/signature/net/)
* [Download di GroupDocs.Signature](https://releases.groupdocs.com/signature/net/)
* [Esempi di codice su GitHub](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
* [Documentazione](https://docs.groupdocs.com/signature/net/)
* [Pagina del prodotto](https://products.groupdocs.com/signature/net/)
* [Articoli del blog](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
* [Forum di supporto](https://forum.groupdocs.com/c/signature/13)
* [Licenza temporanea](https://purchase.groupdocs.com/temporary-license/)