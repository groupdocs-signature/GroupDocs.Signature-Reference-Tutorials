---
"date": "2025-05-07"
"description": "Scopri come firmare immagini DICOM con codici QR utilizzando GroupDocs.Signature per .NET. Questa guida illustra la configurazione, l'implementazione e la verifica delle firme tramite codici QR nell'imaging medico."
"title": "Come firmare le immagini DICOM con i codici QR utilizzando GroupDocs.Signature per .NET&#58; una guida completa"
"url": "/it/net/qr-code-signatures/groupdocs-signature-net-dicom-images-qr-codes/"
"weight": 1
type: docs
---
# Come firmare le immagini DICOM con i codici QR utilizzando GroupDocs.Signature per .NET: una guida completa

Cerchi un metodo sicuro per autenticare i tuoi file DICOM? Questa guida dettagliata ti mostrerà come utilizzare GroupDocs.Signature per .NET per integrare firme con codice QR nelle immagini DICOM. Ideale per professionisti sanitari, sviluppatori e chiunque lavori con documenti medici digitali, questo tutorial copre l'intera configurazione e l'implementazione.

## Cosa imparerai:
- Configurazione dell'ambiente di sviluppo con GroupDocs.Signature per .NET.
- Istruzioni dettagliate sulla firma delle immagini DICOM tramite codici QR.
- Metodi per verificare e cercare le firme dei codici QR nei file DICOM.
- Tecniche per generare anteprime di documenti firmati a scopo di revisione.
- Le migliori pratiche per ottimizzare le prestazioni e gestire efficacemente le risorse.

Cominciamo con i prerequisiti!

## Prerequisiti

Per utilizzare GroupDocs.Signature per .NET, assicurati che il tuo ambiente sia pronto. Ecco cosa ti servirà:

### Librerie e versioni richieste
- **GroupDocs.Signature per .NET**Garantisci la compatibilità con il tuo framework .NET.

### Requisiti di configurazione dell'ambiente
- Un ambiente di sviluppo su Windows o Linux.
- Visual Studio o un altro IDE compatibile con .NET installato.

### Prerequisiti di conoscenza
- Conoscenza di base della programmazione C#.
- Familiarità con l'I/O dei file nelle applicazioni .NET.

## Impostazione di GroupDocs.Signature per .NET

Installa la libreria GroupDocs.Signature utilizzando il metodo che preferisci:

**Utilizzo di .NET CLI:**
```bash
dotnet add package GroupDocs.Signature
```

**Gestore pacchetti:**
```powershell
Install-Package GroupDocs.Signature
```

**Interfaccia utente del gestore pacchetti NuGet:**
- Cerca "GroupDocs.Signature" e installa la versione più recente.

### Acquisizione della licenza

Inizia con una prova gratuita per esplorare le funzionalità. Per un utilizzo prolungato, valuta l'acquisto di una licenza temporanea o completa da [Documenti di gruppo](https://purchase.groupdocs.com/buy).

Una volta installata, inizializzare la libreria:

```csharp
using GroupDocs.Signature;
// Inizializza l'oggetto Signature con il percorso del file DICOM.
Signature signature = new Signature("YOUR_DOCUMENT_DIRECTORY\\sample.dicom");
```

## Guida all'implementazione

### Firma l'immagine DICOM con il codice QR

#### Panoramica
Aggiungi firme con codice QR per garantire l'autenticità e la tracciabilità dei documenti medici.

**Passaggio 1: inizializzare l'oggetto firma**

```csharp
string filePath = "YOUR_DOCUMENT_DIRECTORY\\sample.dicom";
using (Signature signature = new Signature(filePath))
{
    // Procedere con le operazioni di firma...
}
```

**Passaggio 2: creare opzioni di firma del codice QR**

Configura proprietà come testo, dimensione e allineamento.

```csharp
QrCodeSignOptions options = new QrCodeSignOptions("Patient #36363393. R: No-Issues")
{
    AllPages = true,
    Width = 100,
    Height = 100,
    VerticalAlignment = VerticalAlignment.Bottom,
    HorizontalAlignment = HorizontalAlignment.Right,
    Margin = new Padding() { Right = 5, Left = 5 }
};
```

**Passaggio 3: aggiungere metadati XMP**

Arricchisci il documento con metadati aggiuntivi.

```csharp
DicomSaveOptions dicomSaveOptions = new DicomSaveOptions()
{
    XmpEntries = new List<DicomXmpEntry>() { new DicomXmpEntry(DicomXmpType.PatientName, "Patient #4") }
};
```

**Fase 4: Firmare il documento**

Eseguire la firma e salvare.

```csharp
SignResult signResult = signature.Sign("YOUR_OUTPUT_DIRECTORY\\SignedDicom", options, dicomSaveOptions);
```

### Ottieni informazioni sul documento

Recupera i metadati dai file DICOM firmati per garantire l'integrità dei dati.

**Panoramica:**
Accedi alle informazioni del documento e alle firme dei metadati XMP per la verifica.

**Passaggio 1: Recupera le informazioni sul documento**

```csharp
using (Signature signature = new Signature("YOUR_DOCUMENT_DIRECTORY\\sample_signed.dicom"))
{
    IDocumentInfo signedDocumentInfo = signature.GetDocumentInfo();
}
```

**Passaggio 2: iterare e stampare i dati XMP**

Visualizza i dettagli dei metadati.

```csharp
foreach (var item in signedDocumentInfo.MetadataSignatures)
{
    Console.WriteLine(item.ToString());
}
```

### Verifica le firme DICOM

Convalida l'autenticità delle firme dei codici QR nelle immagini DICOM.

**Panoramica:**
Assicurarsi che le firme siano corrette e autentiche.

**Passaggio 1: creare le opzioni di verifica del codice QR**

Imposta le opzioni corrispondenti al testo specifico nei codici QR.

```csharp
QrCodeVerifyOptions options = new QrCodeVerifyOptions()
{
    AllPages = true,
    Text = "Patient #36363393",
    MatchType = TextMatchType.Contains
};
```

**Passaggio 2: verifica delle firme**

Verificare se le firme soddisfano i criteri.

```csharp
VerificationResult result = signature.Verify(options);

if (result.IsValid)
{
    Console.WriteLine($"DICOM {filePath} has {result.Succeeded.Count} successfully verified signatures!");
}
```

### Ricerca di firme in DICOM

Individuare le firme dei codici QR all'interno delle immagini DICOM firmate.

**Panoramica:**
Trova in modo efficiente tutte le firme dei codici QR per gestire l'autenticità dei documenti.

**Passaggio 1: Cerca le firme del codice QR**

```csharp
List<QrCodeSignature> signatures = signature.Search<QrCodeSignature>(SignatureType.QrCode);
```

**Passaggio 2: ripetere e stampare i dettagli della firma**

Esamina i dettagli di ogni firma trovata.

```csharp
foreach (var QrCodeSignature in signatures)
{
    Console.WriteLine($"QRCode signature found at page {QrCodeSignature.PageNumber} with type {QrCodeSignature.EncodeType.TypeName} and text {QrCodeSignature.Text}");
}
```

### Genera anteprima del DICOM firmato

Crea anteprime visive per la verifica.

**Panoramica:**
Genera anteprime delle immagini per verificare il contenuto senza software specializzati.

**Passaggio 1: definire i metodi di flusso**

Impostare metodi per la gestione del flusso di file durante la generazione dell'anteprima.

```csharp
Stream CreatePageStream(PreviewPageData pageData)
{
    string imageFilePath = Path.Combine("YOUR_OUTPUT_DIRECTORY", "SignDicomImageAdvanced", $"preview-{pageData.PageNumber}.jpg");
    var folder = Path.GetDirectoryName(imageFilePath);
    if (!Directory.Exists(folder))
    {
        Directory.CreateDirectory(folder);
    }
    return new FileStream(imageFilePath, FileMode.Create);
}

void ReleasePageStream(PreviewPageData pageData, Stream pageStream)
{
    pageStream.Dispose();
}
```

**Passaggio 2: Genera anteprime**

Eseguire il processo di generazione dell'anteprima.

```csharp
using (Signature signature = new Signature("YOUR_DOCUMENT_DIRECTORY\\sample_signed.dicom"))
{
    PreviewOptions previewOption = new PreviewOptions(CreatePageStream, ReleasePageStream)
    {
        PreviewFormat = PreviewOptions.PreviewFormats.PNG,
    };

    signature.GeneratePreview(previewOption);
}
```

## Applicazioni pratiche

1. **Gestione delle cartelle cliniche**: Autenticare le cartelle cliniche dei pazienti utilizzando firme con codice QR per la conformità.
2. **Piste di controllo nei sistemi sanitari**: Tieni traccia delle modifiche ai documenti e verificane l'autenticità con i codici QR.
3. **Condivisione sicura dei dati**: Garantire la condivisione sicura delle immagini mediche incorporando firme digitali.
4. **Verifica della conformità**: Verificare regolarmente l'integrità dei file DICOM per soddisfare i requisiti legali.
5. **Integrazione con i sistemi EHR**: Integra senza problemi i file DICOM firmati nei sistemi di cartelle cliniche elettroniche (EHR) per semplificare le operazioni.