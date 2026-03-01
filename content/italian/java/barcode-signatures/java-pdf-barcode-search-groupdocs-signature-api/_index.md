---
categories:
- Java Development
- Document Processing
date: '2026-03-01'
description: Scopri come leggere i file PDF con codici QR usando Java e GroupDocs.Signature.
  Guida passo passo, esempi di codice, risoluzione dei problemi e scenari reali.
keywords: read qr code pdf, Java barcode verification PDF, GroupDocs barcode search
  tutorial, extract barcode data from PDF Java, Java PDF barcode scanner
lastmod: '2026-03-01'
linktitle: Search PDF Barcodes Java
tags:
- barcode-search
- pdf-processing
- groupdocs
- java-tutorial
- document-verification
title: Come leggere un PDF con codice QR usando Java e GroupDocs.Signature
type: docs
url: /it/java/barcode-signatures/java-pdf-barcode-search-groupdocs-signature-api/
weight: 1
---

# Come leggere PDF con codice QR usando Java

## Introduzione

Hai mai dovuto estrarre informazioni di codici a barre da centinaia di fatture PDF, etichette di spedizione o documenti di inventario? Scansionare manualmente le pagine è noioso e soggetto a errori. Che tu stia costruendo un sistema automatizzato di elaborazione documenti o verificando l'autenticità di un prodotto, trovare i codici a barre in modo efficiente nei PDF può essere una sfida.

In questa guida imparerai a **leggere PDF con codice QR** in modo efficiente usando l'API GroupDocs.Signature. Questa potente API trasforma quello che potrebbe richiedere ore di lavoro manuale in poche righe di codice. Puoi scansionare interi documenti, individuare tipi specifici di codici a barre (come QR o Code128) ed estrarre automaticamente i loro dati.

**Cosa imparerai:**
- Configurare GroupDocs.Signature per Java in pochi minuti  
- Cercare firme di codici a barre all'interno di documenti PDF  
- Configurare le opzioni di ricerca per risultati precisi e mirati  
- Gestire diversi tipi di codici a barre (QR, EAN, Code128, ecc.)  
- Risolvere problemi comuni e ottimizzare le prestazioni  

Iniziamo!

## Risposte rapide
- **GroupDocs.Signature può leggere i codici QR dai PDF?** Sì, rileva QR, Data Matrix, PDF417 e molti codici a barre 1D.  
- **È necessaria una licenza per l'uso in produzione?** È richiesta una licenza commerciale; è disponibile una prova gratuita per la valutazione.  
- **Quale versione di Java è richiesta?** Java 8+ (Java 11+ consigliato).  
- **Come limitare la ricerca a pagine specifiche?** Usa `BarcodeSearchOptions.setAllPages(false)` e imposta `setPageNumber()`.  
- **L'API è thread‑safe per l'elaborazione batch?** Sì, quando crei un'istanza `Signature` separata per ogni thread.

## Perché cercare codici a barre nei PDF?

Prima di entrare nel tecnico, ecco perché è importante nelle applicazioni reali:

**Scenari aziendali comuni**
- **Elaborazione fatture** – Estrarre automaticamente numeri d'ordine o codici di tracciamento dalle fatture dei fornitori.  
- **Gestione inventario** – Scansionare cataloghi di prodotti ed estrarre i codici SKU per aggiornare il database.  
- **Spedizioni e logistica** – Verificare i codici di tracciamento dei pacchi nei manifesti di spedizione.  
- **Autenticazione documenti** – Convalidare documenti firmati controllando i codici a barre di sicurezza incorporati.  
- **Cartelle cliniche** – Estrarre ID paziente o codici di prescrizione da documenti medici.  

L'API GroupDocs.Signature si occupa del lavoro pesante: non devi preoccuparti di elaborazione immagini, algoritmi di decodifica dei codici a barre o complessità di rendering PDF. È tutto integrato.

## Prerequisiti

Prima di iniziare questo tutorial, assicurati di avere tutto il necessario:

### Librerie e dipendenze richieste

Devi includere la libreria GroupDocs.Signature nel tuo progetto Java. Ecco come aggiungerla usando Maven o Gradle:

**Maven:**
```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

**Gradle:**
```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

**Nota:** Controlla sempre l'ultima versione su [GroupDocs.Signature for Java releases](https://releases.groupdocs.com/signature/java/). Usare la versione più recente garantisce correzioni di bug e nuove funzionalità.

### Configurazione dell'ambiente

- **JDK 8 o superiore** – GroupDocs.Signature richiede almeno Java 8 (Java 11+ consigliato per migliori prestazioni).  
- **IDE** – Qualsiasi editor di testo funziona, ma IntelliJ IDEA o Eclipse renderanno il lavoro più semplice con autocomplete e debug.  
- **Documento PDF** – Preparati un PDF di test con codici a barre (fatture, etichette di spedizione o cataloghi di prodotti vanno benissimo).

### Conoscenze pregresse

Dovresti sentirti a tuo agio con:
- Sintassi Java di base e concetti di programmazione orientata agli oggetti  
- Gestione delle eccezioni con blocchi `try‑catch`  
- Utilizzo di librerie esterne nel tuo IDE  

Se sei nuovo alle librerie Java di terze parti, non preoccuparti: ti guideremo passo passo.

## Configurare GroupDocs.Signature per Java

Iniziare con GroupDocs.Signature richiede solo pochi minuti. Ecco il processo completo:

### Passo 1: Aggiungere la dipendenza

Usa Maven o Gradle per includere la libreria (vedi il codice sopra). Dopo aver aggiunto la dipendenza, aggiorna il progetto per scaricare i file JAR.

### Passo 2: Acquisizione della licenza

GroupDocs offre diverse opzioni di licenza:

- **Prova gratuita** – Perfetta per i test. Scarica da [GroupDocs releases](https://releases.groupdocs.com/signature/java/).  
- **Licenza temporanea** – Ottieni 30 giorni di accesso completo tramite la [Temporary License Page](https://purchase.groupdocs.com/temporary-license/).  
- **Licenza commerciale** – Per l'uso in produzione, acquista una licenza su [GroupDocs Purchase](https://purchase.groupdocs.com/).  

**Suggerimento professionale:** Inizia con la prova gratuita per costruire il tuo proof‑of‑concept, poi passa a una licenza a pagamento se l'API soddisfa le tue esigenze.

### Passo 3: Inizializzazione di base

Ecco come creare un oggetto `Signature` per lavorare con il tuo PDF:

```java
import com.groupdocs.signature.Signature;

String filePath = "YOUR_DOCUMENT_DIRECTORY/sample_signed.pdf"; // Replace with your PDF path
Signature signature = new Signature(filePath);
```

La classe `Signature` è il punto di ingresso principale. Carica il PDF in memoria e fornisce metodi per cercare, verificare ed estrarre dati di firma (inclusi i codici a barre).

**Importante**: Assicurati che il percorso del file sia corretto e che il PDF esista. Errore comune? Usare le backslash su Windows senza escape (`C:\\Documents\\file.pdf` e non `C:\Documents\file.pdf`).

## Guida all'implementazione

Ora la parte divertente: scriviamo il codice per cercare i codici a barre nel tuo PDF.

### Ricerca di firme di codici a barre in un documento

Questa sezione mostra come scansionare un PDF e individuare tutte le firme di codici a barre. Suddivideremo il processo in passaggi comprensibili con spiegazioni per ciascuna parte.

#### Passo 1: Inizializzare l'oggetto Signature

Carica il tuo documento PDF:

```java
import com.groupdocs.signature.Signature;

String filePath = "YOUR_DOCUMENT_DIRECTORY/sample_signed.pdf"; // Replace with actual file path
Signature signature = new Signature(filePath);
```

**Cosa succede qui**  
La classe `Signature` apre il PDF e lo prepara per l'elaborazione. È come aprire un file in un editor di testo: il documento viene caricato in memoria così da poterci lavorare sopra.

**Nota pratica**  
Se elabori PDF caricati dagli utenti, valida sempre il percorso del file e verifica che il file esista prima di creare l'oggetto `Signature`. Questo evita errori criptici in seguito.

#### Passo 2: Creare BarcodeSearchOptions

Configura come vuoi cercare i codici a barre:

```java
import com.groupdocs.signature.options.search.BarcodeSearchOptions;

// Configure options for searching barcodes
BarcodeSearchOptions options = new BarcodeSearchOptions();
options.setAllPages(true); // Search every page in the document
```

**Opzioni di configurazione chiave**

- `setAllPages(true)`: Scansiona tutte le pagine. Imposta a `false` se vuoi controllare solo pagine specifiche (configura con `setPageNumber()`).  
- **Perché è importante**: Se elabori fatture dove i codici a barre sono sempre a pagina 1, cercare in tutte le pagine spreca risorse. Per manifesti di spedizione multi‑pagina, servirà `setAllPages(true)`.

**Suggerimento professionale**: Puoi anche filtrare per tipo di codice a barre (vedi la sezione **Tipi di codice a barre supportati** più avanti). Questo velocizza le ricerche quando sai esattamente quale formato cercare.

#### Passo 3: Eseguire la ricerca e gestire i risultati

Ora esegui la ricerca e processa i risultati:

```java
import com.groupdocs.signature.domain.signatures.BarcodeSignature;
import java.util.List;

try {
    // Execute the barcode search
    List<BarcodeSignature> signatures = signature.search(BarcodeSignature.class, options);
    
    // Check if any barcodes were found
    if (signatures.isEmpty()) {
        System.out.println("No barcode signatures found in the document.");
    } else {
        System.out.println("Found " + signatures.size() + " barcode signature(s):\n");
        
        // Loop through each barcode and display details
        for (BarcodeSignature barcodeSignature : signatures) {
            System.out.println("----------------------------------------");
            System.out.println("Barcode Type: " + barcodeSignature.getEncodeType().getTypeName());
            System.out.println("Barcode Text: " + barcodeSignature.getText());
            System.out.println("Page Number: " + barcodeSignature.getPageNumber());
            System.out.println("Position: X=" + barcodeSignature.getLeft() + 
                             ", Y=" + barcodeSignature.getTop());
            System.out.println("Size: Width=" + barcodeSignature.getWidth() + 
                             ", Height=" + barcodeSignature.getHeight());
            System.out.println("----------------------------------------\n");
        }
    }
} catch (Exception e) {
    System.err.println("Error searching for barcodes: " + e.getMessage());
    e.printStackTrace();
} finally {
    // Always dispose of the signature object to free resources
    if (signature != null) {
        signature.dispose();
    }
}
```

**Cosa succede in questo codice**

1. **Esecuzione della ricerca** – `signature.search()` scansiona il PDF e restituisce una lista di oggetti `BarcodeSignature`.  
2. **Controllo vuoto** – Verifica che siano stati effettivamente trovati codici a barre (evita NullPointerException).  
3. **Estrazione dati** – Per ogni codice a barre estraiamo:  
   - **Tipo** – Il formato del codice (QR Code, Code128, EAN13, ecc.)  
   - **Testo** – I dati decodificati (numero d'ordine, codice di tracciamento, SKU, ecc.)  
   - **Posizione** – Numero di pagina e coordinate X/Y  
   - **Dimensioni** – Larghezza e altezza (utile per la validazione)  
4. **Gestione errori** – Il blocco `try‑catch` previene crash se qualcosa va storto (PDF corrotto, file mancante, ecc.).  
5. **Pulizia delle risorse** – Il blocco `finally` garantisce che l'oggetto `Signature` venga correttamente eliminato, liberando memoria.

**Applicazione pratica**  
Supponiamo di elaborare etichette di spedizione. Estrarresti il valore `getText()` (numero di tracciamento) e lo salveresti nel tuo database. Il numero di pagina ti indica a quale etichetta corrisponde ogni spedizione se elabori documenti batch.

### Filtrare per tipo di codice a barre

Puoi velocizzare le ricerche specificando il tipo di codice a barre che ti interessa:

```java
import com.groupdocs.signature.domain.barcodes.BarcodeTypes;

BarcodeSearchOptions options = new BarcodeSearchOptions();
options.setEncodeType(BarcodeTypes.QR); // Only search for QR codes
options.setAllPages(true);
```

**Quando filtrare**  
Se sai che le tue fatture contengono solo codici Code128, filtrare per tipo riduce il tempo di elaborazione del 30‑50 % su documenti di grandi dimensioni.

## Tipi di codice a barre supportati

GroupDocs.Signature può rilevare un'ampia gamma di formati di codici a barre. Ecco cosa puoi cercare:

**Codici a barre 1D (Lineari)**
- **Code128** – Comune in spedizioni e imballaggi  
- **Code39** – Usato nei settori automotive e difesa  
- **EAN13/EAN8** – Codici prodotto al dettaglio (li vedi su ogni prodotto)  
- **UPC‑A/UPC‑E** – Standard nordamericano per il retail  
- **Interleaved2of5** – Magazzini e distribuzione  

**Codici a barre 2D (Matrice)**
- **QR Code** – Il più popolare—usato per URL, password Wi‑Fi, informazioni di pagamento  
- **Data Matrix** – Formato compatto per piccoli oggetti (componenti elettronici)  
- **PDF417** – ID governativi, carte d'imbarco, patenti di guida  
- **Aztec Code** – Biglietti di trasporto  

**Filtrare per tipo** (esempio mostrato prima) ti aiuta a concentrarti sul formato esatto di cui hai bisogno.

## Casi d'uso reali

Ecco come gli sviluppatori stanno usando la ricerca di codici a barre in produzione:

### 1. Elaborazione automatica delle fatture
**Scenario** – Un dipartimento contabile riceve più di 500 fatture fornitori al giorno in PDF.  
**Soluzione** – Scansionare ogni PDF per codici Code39 contenenti i numeri di fattura, abbinandoli automaticamente agli ordini di acquisto nel sistema ERP. Questo elimina l'inserimento manuale dei dati e riduce gli errori.

```java
// Pseudo-code workflow
for (PDF invoice : invoiceBatch) {
    List<BarcodeSignature> barcodes = searchBarcodes(invoice);
    String invoiceNumber = barcodes.get(0).getText();
    updateERPSystem(invoiceNumber, invoice);
}
```

### 2. Aggiornamenti inventario in magazzino
**Scenario** – Un magazzino riceve spedizioni con liste di imballaggio PDF contenenti SKU in codici EAN13.  
**Soluzione** – Estrarre tutti i codici dalle liste, aggiornare automaticamente i conteggi di inventario e segnalare le discrepanze per la revisione.

### 3. Autenticazione dei documenti
**Scenario** – Documenti legali includono QR code con firme crittografiche per la verifica dell'autenticità.  
**Soluzione** – Cercare i QR code nei contratti firmati, decodificare i dati della firma e verificarli rispetto a un'autorità di certificazione affidabile. Questo garantisce che i documenti non siano stati manomessi.

### 4. Gestione delle cartelle cliniche
**Scenario** – I fascicoli paziente negli ospedali contengono PDF di referti di laboratorio con codici Code128 per gli ID dei campioni.  
**Soluzione** – Estrarre automaticamente gli ID dei campioni e collegare i risultati di laboratorio ai record dei pazienti nel sistema informativo ospedaliero (HIS).

## Problemi comuni e soluzioni

Ecco i problemi che potresti incontrare e come risolverli:

### Problema 1: “Nessun codice a barre trovato” (anche se sai che ci sono)

**Possibili cause**
- Qualità dell'immagine del codice troppo bassa (sfocata, pixelata)  
- Il PDF è basato su immagini ma il codice è troppo piccolo  
- Stai cercando il tipo di codice sbagliato  

**Soluzioni**
1. **Controlla la risoluzione dell'immagine** – I codici a barre necessitano di almeno 200 DPI per una rilevazione affidabile. Se scansioni documenti, usa 300 DPI o più.  
2. **Rimuovi il filtro per tipo** – Prova a cercare tutti i tipi di codice a barre prima (non impostare `setEncodeType()`), poi restringi una volta identificato il contenuto del documento.  
3. **Verifica la qualità del codice** – Apri il PDF in Adobe Acrobat e ingrandisci. Se il codice appare sfocato a te, sarà difficile anche per l'API.

### Problema 2: `OutOfMemoryError` con PDF di grandi dimensioni

**Causa** – Caricare un PDF di 500 pagine con immagini ad alta risoluzione consuma molta memoria.  

**Soluzione**
1. **Elaborare le pagine a lotti** – Invece di `setAllPages(true)`, elabora 50 pagine alla volta:

```java
for (int startPage = 1; startPage <= totalPages; startPage += 50) {
    BarcodeSearchOptions options = new BarcodeSearchOptions();
    options.setPageNumber(startPage);
    options.setPagesSetup(new PagesSetup());
    options.getPagesSetup().setLastPage(Math.min(startPage + 49, totalPages));
    
    List<BarcodeSignature> batchResults = signature.search(BarcodeSignature.class, options);
    // Process results...
}
```

2. **Aumentare l'heap JVM** – Aggiungi `-Xmx4g` al comando Java per allocare 4 GB di memoria (adatta in base alle tue esigenze).

### Problema 3: Prestazioni lente su documenti multipagina

**Causa** – Cercare tutte le pagine in sequenza richiede tempo, soprattutto con codici complessi come PDF417.  

**Soluzioni**
1. **Elaborazione parallela** – Se i codici sono sempre su pagine specifiche (es. pagina 1 delle fatture), cerca solo quelle pagine.  
2. **Cache dei risultati** – Se elabori più volte lo stesso documento, memorizza nella cache i dati dei codici a barre per evitare una nuova scansione.  
3. **Usa SSD** – La velocità di I/O influisce quando si caricano PDF di grandi dimensioni. Gli SSD riducono i tempi di caricamento del 60‑70 % rispetto agli HDD.

### Problema 4: Falsi positivi (rilevamento di pattern casuali come codici a barre)

**Causa** – Tabelle, griglie o linee possono essere interpretate erroneamente come codici a barre.  

**Soluzione** – Convalida i risultati controllando la lunghezza e il formato del testo decodificato:

```java
for (BarcodeSignature barcode : signatures) {
    String text = barcode.getText();
    
    // Example: Invoice numbers are always 10 digits
    if (text.matches("\\d{10}")) {
        // Valid invoice number
        processBarcode(barcode);
    } else {
        System.out.println("Skipping invalid barcode: " + text);
    }
}
```

## Suggerimenti di performance per documenti di grandi dimensioni

Elabori migliaia di PDF? Ecco come ottimizzare:

### 1. Strategia di elaborazione batch

Invece di processare i file uno alla volta, usa un pool di thread per gestire più PDF contemporaneamente:

```java
ExecutorService executor = Executors.newFixedThreadPool(4); // 4 parallel threads

for (String pdfPath : pdfFiles) {
    executor.submit(() -> {
        try (Signature sig = new Signature(pdfPath)) {
            List<BarcodeSignature> results = sig.search(BarcodeSignature.class, options);
            // Process results...
        } catch (Exception e) {
            e.printStackTrace();
        }
    });
}

executor.shutdown();
executor.awaitTermination(1, TimeUnit.HOURS);
```

**Guadagno di performance** – Elaborare 1 000 file scende da ~2 ore a ~30 minuti su una macchina quad‑core.

### 2. Ridurre l'ambito di ricerca

Se la tua logica aziendale lo consente, limita l'area di ricerca:

```java
// Only search the top‑right corner where barcodes are typically placed
options.setRectangle(new Rectangle(400, 50, 150, 150)); // X, Y, Width, Height
```

**Guadagno di performance** – 40‑60 % più veloce su documenti dove le posizioni dei codici a barre sono costanti.

### 3. Monitorare l'uso della memoria

Per processi batch di lunga durata, monitora l'heap e suggerisci esplicitamente la garbage collection se necessario:

```java
Runtime runtime = Runtime.getRuntime();
long usedMemory = runtime.totalMemory() - runtime.freeMemory();

if (usedMemory > (runtime.maxMemory() * 0.8)) {
    System.gc(); // Suggest garbage collection
}
```

## Best practice

Segui queste linee guida per un codice pronto per la produzione:

### 1. Disporre sempre degli oggetti Signature

Avvolgi il tuo codice in try‑with‑resources (Java 7+) per chiudere automaticamente le risorse:

```java
try (Signature signature = new Signature(filePath)) {
    // Your search code here...
} // Automatically disposed
```

### 2. Validare i file di input

Prima dell'elaborazione, verifica che il file esista ed è un PDF valido:

```java
File pdfFile = new File(filePath);
if (!pdfFile.exists() || !pdfFile.canRead()) {
    throw new FileNotFoundException("PDF not found or not readable: " + filePath);
}

// Optional: Verify it's actually a PDF (check magic bytes)
```

### 3. Registrare i risultati della rilevazione dei codici a barre

Per debug e audit, registra ciò che trovi:

```java
Logger logger = Logger.getLogger(BarcodeSearcher.class.getName());

for (BarcodeSignature barcode : signatures) {
    logger.info(String.format("Detected %s barcode '%s' on page %d at (%.2f, %.2f)",
        barcode.getEncodeType().getTypeName(),
        barcode.getText(),
        barcode.getPageNumber(),
        barcode.getLeft(),
        barcode.getTop()));
}
```

### 4. Gestire diversi formati di codice a barre

Diversi settori usano standard diversi. Rendi il tuo codice flessibile:

```java
switch (barcode.getEncodeType().getTypeName()) {
    case "QR":
        // QR codes might contain URLs or JSON data
        processQRCode(barcode.getText());
        break;
    case "Code128":
        // Code128 typically contains alphanumeric order/tracking numbers
        processTrackingNumber(barcode.getText());
        break;
    default:
        logger.warning("Unexpected barcode type: " + barcode.getEncodeType());
}
```

### 5. Testare con documenti reali

Non limitarti a PDF di esempio perfetti. Usa documenti reali del tuo ambiente di produzione:
- Fatture scansionate con macchie di caffè  
- Etichette di spedizione faxate con rumore  
- Foto a bassa risoluzione da smartphone convertite in PDF  

Questo rivela casi limite che non emergono nelle demo.

## Domande frequenti

**D: Posso leggere PDF con codice QR senza licenza?**  
R: Una prova gratuita ti consente di leggere PDF con codice QR per la valutazione, ma è necessaria una licenza commerciale per le distribuzioni in produzione.

**D: L'API supporta PDF protetti da password?**  
R: Sì. Puoi passare la password quando crei l'oggetto `Signature`: `new Signature(filePath, "password")`.

**D: Come migliorare la rilevazione su scansioni a bassa risoluzione?**  
R: Aumenta la DPI della scansione di origine (minimo 200 DPI) e considera il filtraggio per tipo di codice a barre per ridurre i falsi positivi.

**D: La ricerca è thread‑safe per l'elaborazione parallela?**  
R: Ogni thread deve utilizzare la propria istanza `Signature`. L'API è thread‑safe se usata in questo modo.

**D: Quale versione di GroupDocs.Signature è stata testata con questo tutorial?**  
R: Il codice è stato validato con GroupDocs.Signature 23.12.

## Conclusione

Hai appena imparato a **leggere PDF con codice QR** usando Java e l'API GroupDocs.Signature. Ecco cosa abbiamo coperto:

✅ **Setup** – Aggiungere GroupDocs.Signature al progetto e le opzioni di licenza  
✅ **Implementazione** – Codice completo per cercare, estrarre e processare dati di codici a barre  
✅ **Tipi di codice a barre** – Comprendere i formati supportati (1D e 2D)  
✅ **Casi d'uso reali** – Elaborazione fatture, gestione inventario, autenticazione documenti, cartelle cliniche  
✅ **Risoluzione problemi** – Come affrontare errori di memoria e falsi positivi  
✅ **Performance** – Ottimizzare le ricerche per l'elaborazione su larga scala  

L'API GroupDocs.Signature gestisce la complessità di parsing PDF e rilevazione dei codici a barre, permettendoti di concentrarti sulla logica di business. Che tu stia automatizzando l'elaborazione delle fatture, verificando le etichette di spedizione o estraendo dati di inventario, ora disponi di una soluzione robusta.

---

**Ultimo aggiornamento:** 2026-03-01  
**Testato con:** GroupDocs.Signature 23.12  
**Autore:** GroupDocs