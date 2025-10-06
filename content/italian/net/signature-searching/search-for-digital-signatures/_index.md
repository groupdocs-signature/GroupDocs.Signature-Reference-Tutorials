---
"description": "Padroneggia la ricerca di firme digitali nei documenti con GroupDocs.Signature per .NET. Migliora la sicurezza e la verifica dei documenti con la nostra guida dettagliata passo dopo passo."
"linktitle": "Ricerca di firme digitali"
"second_title": "API .NET GroupDocs.Signature"
"title": "Ricerca di firme digitali nei documenti"
"url": "/it/net/signature-searching/search-for-digital-signatures/"
"weight": 11
type: docs
---
## Introduzione

Nell'attuale panorama digitale, garantire l'autenticità e l'integrità dei documenti è fondamentale per aziende e organizzazioni. Le firme digitali forniscono un meccanismo affidabile per verificare l'autenticità dei documenti e rilevare modifiche non autorizzate. GroupDocs.Signature per .NET offre una soluzione completa per lavorare con firme digitali in vari formati di documento, consentendo agli sviluppatori di integrare perfettamente la funzionalità di firma nelle loro applicazioni .NET.

Questo tutorial ti guiderà attraverso il processo di ricerca di firme digitali nei documenti utilizzando GroupDocs.Signature per .NET, fornendo spiegazioni dettagliate ed esempi di codice pratici.

## Prerequisiti

Prima di addentrarci nei dettagli dell'implementazione, assicurati di disporre dei seguenti prerequisiti:

1. GroupDocs.Signature per .NET: Scarica e installa la libreria da [Qui](https://releases.groupdocs.com/signature/net/).
   
2. Ambiente di sviluppo: configura un ambiente di sviluppo .NET con Visual Studio o il tuo IDE preferito.
   
3. Documenti campione: preparare documenti campione contenenti firme digitali a scopo di test.

4. Conoscenze di base: familiarità con il linguaggio di programmazione C# e con i fondamenti del framework .NET.

## Importa spazi dei nomi

Per iniziare, importare gli spazi dei nomi necessari per accedere alle funzionalità fornite da GroupDocs.Signature per .NET:

```csharp
using System;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

Ora, scomponiamo il processo di ricerca delle firme digitali in passaggi chiari e gestibili:

## Passaggio 1: inizializzare l'oggetto firma

Inizia creando un'istanza di `Signature` classe, passando il percorso al tuo documento:

```csharp
string filePath = "sample_multiple_signatures.docx";
using (Signature signature = new Signature(filePath))
{
    // Qui verrà aggiunto il codice per la ricerca delle firme digitali
}
```

## Passaggio 2: ricerca delle firme digitali

Quindi, utilizzare il `Search` metodo con il `SignatureType.Digital` parametro per cercare firme digitali nel documento:

```csharp
// Cerca firme digitali nel documento
List<DigitalSignature> signatures = signature.Search<DigitalSignature>(SignatureType.Digital);
```

## Fase 3: Elaborazione e visualizzazione dei risultati

Infine, elabora i risultati della ricerca e visualizza le informazioni rilevanti sulle firme digitali trovate:

```csharp
Console.WriteLine($"\nSource document ['{filePath}'] contains the following digital signatures:");
foreach (var digitalSignature in signatures)
{
    Console.WriteLine($"Digital signature found from {digitalSignature.SignTime} with validation status: {digitalSignature.IsValid}");
    Console.WriteLine($"Certificate: Subject: {digitalSignature.Certificate?.SubjectName}");
    Console.WriteLine($"Certificate: Issuer: {digitalSignature.Certificate?.IssuerName}");
    Console.WriteLine($"Certificate: Serial Number: {digitalSignature.Certificate?.SerialNumber}");
    Console.WriteLine();
}
```

## Esempio completo

Ecco un esempio completo e funzionante che mostra come cercare firme digitali in un documento:

```csharp
using System;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;

namespace SearchDigitalSignatures
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
                // Cerca firme digitali nel documento
                List<DigitalSignature> signatures = signature.Search<DigitalSignature>(SignatureType.Digital);
                
                // Visualizza i risultati della ricerca
                Console.WriteLine($"\nSource document ['{filePath}'] contains the following digital signatures:");
                
                if (signatures.Count > 0)
                {
                    foreach (var digitalSignature in signatures)
                    {
                        Console.WriteLine($"Digital signature found from {digitalSignature.SignTime} with validation status: {digitalSignature.IsValid}");
                        Console.WriteLine($"Certificate: Subject: {digitalSignature.Certificate?.SubjectName}");
                        Console.WriteLine($"Certificate: Issuer: {digitalSignature.Certificate?.IssuerName}");
                        Console.WriteLine($"Certificate: Serial Number: {digitalSignature.Certificate?.SerialNumber}");
                        Console.WriteLine();
                    }
                }
                else
                {
                    Console.WriteLine("No digital signatures found in the document.");
                }
            }
        }
    }
}
```

## Opzioni di ricerca avanzate

Per ricerche più mirate, puoi utilizzare `DigitalSearchOptions` per personalizzare i criteri di ricerca:

```csharp
// Creare opzioni di ricerca digitale
DigitalSearchOptions options = new DigitalSearchOptions()
{
    // Cerca solo su pagine specifiche (ad esempio, pagine 1 e 2)
    PageNumber = 1,
    PagesSetup = new PagesSetup() { Pages = new List<int> { 1, 2 } },
    
    // Filtra per commenti nelle firme digitali
    Comments = "Approved",
    
    // Imposta l'intervallo di data e ora per la ricerca
    SignDateTimeFrom = new DateTime(2022, 1, 1),
    SignDateTimeTo = DateTime.Now
};

// Cerca con opzioni specifiche
List<DigitalSignature> signatures = signature.Search<DigitalSignature>(options);
```

## Lavorare con le informazioni del certificato

Le firme digitali contengono preziose informazioni sul certificato a cui puoi accedere e che puoi convalidare:

```csharp
foreach (var digitalSignature in signatures)
{
    if (digitalSignature.Certificate != null)
    {
        // Proprietà del certificato di accesso
        Console.WriteLine($"Certificate Valid From: {digitalSignature.Certificate.NotBefore}");
        Console.WriteLine($"Certificate Valid To: {digitalSignature.Certificate.NotAfter}");
        
        // Controlla se il certificato rientra in un intervallo di date valido
        bool isDateValid = DateTime.Now >= digitalSignature.Certificate.NotBefore && 
                          DateTime.Now <= digitalSignature.Certificate.NotAfter;
        
        Console.WriteLine($"Certificate Date Validity: {isDateValid}");
        
        // Accedi ai dettagli dell'emittente del certificato
        Console.WriteLine($"Certificate Issuer: {digitalSignature.Certificate.IssuerName}");
    }
}
```

## Conclusione

GroupDocs.Signature per .NET offre una soluzione potente e flessibile per la ricerca e la convalida delle firme digitali all'interno dei documenti. In questo tutorial, abbiamo esplorato il processo passo passo per implementare la funzionalità di ricerca delle firme digitali nelle applicazioni .NET, fornendovi le conoscenze necessarie per migliorare la sicurezza e la verifica dell'integrità dei documenti.

Sfruttando GroupDocs.Signature, puoi creare sistemi di gestione dei documenti affidabili che garantiscono l'autenticità e l'integrità dei tuoi documenti digitali, promuovendo la fiducia e la conformità nei tuoi processi aziendali.

## Domande frequenti

### GroupDocs.Signature può verificare la validità delle firme digitali?

Sì, GroupDocs.Signature convalida automaticamente le firme digitali durante il processo di ricerca e fornisce lo stato di convalida tramite `IsValid` proprietà del `DigitalSignature` classe.

### Quali formati di documento supportano la ricerca tramite firma digitale?

GroupDocs.Signature supporta la ricerca di firme digitali in vari formati, tra cui PDF, documenti Microsoft Office (Word, Excel, PowerPoint), formati OpenOffice e altro ancora.

### Posso cercare firme digitali nei documenti protetti da password?

Sì, è possibile cercare firme digitali nei documenti protetti da password fornendo la password durante l'inizializzazione `Signature` oggetto:

```csharp
LoadOptions loadOptions = new LoadOptions() { Password = "your_password" };
using (Signature signature = new Signature(filePath, loadOptions))
{
    // Ricerca firme digitali
}
```

### Come posso verificare se una firma digitale è stata creata da una persona specifica?

È possibile esaminare il nome dell'oggetto del certificato e altre proprietà per verificare l'identità del firmatario:

```csharp
foreach (var signature in signatures)
{
    if (signature.Certificate?.SubjectName?.Contains("John Doe") == true)
    {
        Console.WriteLine("Found signature by John Doe");
    }
}
```

### Posso estrarre la chiave pubblica da un certificato di firma digitale?

Sì, puoi accedere alle informazioni sulla chiave pubblica tramite le proprietà del certificato:

```csharp
if (signature.Certificate != null)
{
    // Accedi alle informazioni sulla chiave pubblica
    Console.WriteLine($"Public Key: {signature.Certificate.GetPublicKeyString()}");
}
```

## Vedi anche

* [Riferimento API](https://reference.groupdocs.com/signature/net/)
* [Esempi di codice](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
* [Documentazione del prodotto](https://docs.groupdocs.com/signature/net/)
* [Pagina del prodotto](https://products.groupdocs.com/signature/net/)
* [Scarica l'ultima versione](https://releases.groupdocs.com/signature/net/)
* [Articoli del blog](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
* [Forum di supporto](https://forum.groupdocs.com/c/signature/13)
* [Licenza temporanea](https://purchase.groupdocs.com/temporary-license/)