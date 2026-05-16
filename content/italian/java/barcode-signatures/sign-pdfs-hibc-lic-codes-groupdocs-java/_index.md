---
categories:
- Document Signing
- Healthcare Integration
date: '2026-05-16'
description: Scopri come creare PDF Data Matrix e aggiungere PDF QR code usando GroupDocs.Signature
  per Java. Guida passo‑passo per la firma di documenti sanitari.
keywords:
- create data matrix pdf
- add qr code pdf
- HIBC barcode Java
lastmod: '2026-05-16'
linktitle: Guida Java per la firma PDF HIBC
schemas:
- author: GroupDocs
  dateModified: '2026-05-16'
  description: Learn how to create data matrix PDF and add QR code PDF using GroupDocs.Signature
    for Java. Step‑by‑step guide for healthcare document signing.
  headline: Create Data Matrix PDF with HIBC Barcode in Java
  type: TechArticle
- description: Learn how to create data matrix PDF and add QR code PDF using GroupDocs.Signature
    for Java. Step‑by‑step guide for healthcare document signing.
  name: Create Data Matrix PDF with HIBC Barcode in Java
  steps:
  - name: '**Import the required classes** – these give you access to the signature
      engine and Data Matrix options.'
    text: '**Import the required classes** – these give you access to the signature
      engine and Data Matrix options.'
  - name: '**Instantiate the `Signature` object** with absolute paths for source and
      destination files.'
    text: '**Instantiate the `Signature` object** with absolute paths for source and
      destination files.'
  - name: '**Configure the Data Matrix options** – set the HIBC string, choose `QrCodeTypes.HIBCLICDataMatrix`,
      and define placement coordinates. `QrCodeTypes` enumerates the supported barcode
      formats for HIBC signatures.'
    text: '**Configure the Data Matrix options** – set the HIBC string, choose `QrCodeTypes.HIBCLICDataMatrix`,
      and define placement coordinates. `QrCodeTypes` enumerates the supported barcode
      formats for HIBC signatures.'
  - name: '**Apply the signature** to the PDF.'
    text: '**Apply the signature** to the PDF.'
  - name: '**Dispose of resources** to free file handles and avoid memory leaks.'
    text: '**Dispose of resources** to free file handles and avoid memory leaks.'
  - name: '**Import QR‑specific classes**'
    text: '**Import QR‑specific classes**'
  - name: '**Create and configure QR options** – note the use of `QrCodeTypes.HIBCLICQR`.'
    text: '**Create and configure QR options** – note the use of `QrCodeTypes.HIBCLICQR`.'
  - name: '**Sign the document**'
    text: '**Sign the document**'
  type: HowTo
- questions:
  - answer: Yes, it also supports DOCX, XLSX, PPTX, PNG, JPEG, and TIFF with the same
      barcode‑signing API.
    question: Can GroupDocs.Signature sign file types other than PDF?
  - answer: Verify that your HIBC string follows the exact HIBCC syntax, use the online
      validator, and ensure you’re using the correct `QrCodeTypes` constant for the
      chosen format.
    question: How do I troubleshoot “Invalid barcode content” errors?
  - answer: QR ≈ 4,296 alphanumeric characters, Aztec ≈ 3,832 numeric / 3,067 alphanumeric,
      Data Matrix ≈ 3,116 numeric / 2,335 alphanumeric. Keep codes under 200 characters
      for optimal scan reliability.
    question: What is the maximum data capacity for each HIBC format?
  - answer: Absolutely. Create separate `QrCodeSignOptions` objects with different
      positions and call `signature.sign()` for each. Just ensure they don’t overlap.
    question: Is it possible to embed multiple barcode types in one PDF?
  - answer: No. After the JAR is on the classpath and the license is activated, all
      operations are performed locally.
    question: Do I need an internet connection for signing at runtime?
  type: FAQPage
tags:
- java
- pdf-signing
- hibc
- healthcare
- barcode
- pharmaceutical
title: Crea PDF Data Matrix con codice a barre HIBC in Java
type: docs
url: /it/java/barcode-signatures/sign-pdfs-hibc-lic-codes-groupdocs-java/
weight: 1
---

# Crea PDF Data Matrix con codice a barre HIBC in Java

Se stai sviluppando software per la logistica farmaceutica o sanitaria, probabilmente ti sei imbattuto nel problema del tracciamento basato su carta, firme perse e incubi di audit. **Creare un PDF Data Matrix** che incorpora un codice a barre HIBC LIC risolve questi problemi fornendoti una traccia a prova di manomissione, leggibile da macchine, che resiste alla stampa, alla scansione e alla revisione normativa. In questo tutorial vedrai esattamente come **aggiungere il supporto PDF per QR code**, oltre ai formati Aztec e Data Matrix, utilizzando GroupDocs.Signature for Java.

## Risposte rapide
- **Quale libreria gestisce i codici a barre HIBC in Java?** GroupDocs.Signature for Java.  
- **Quale formato di codice a barre è più compatto?** Data Matrix – ideale per etichette piccole.  
- **Posso aggiungere sia QR che Data Matrix allo stesso PDF?** Sì, basta creare separati `QrCodeSignOptions`.  
- **È necessaria una connessione internet durante l'esecuzione?** No, la libreria funziona completamente offline dopo l'installazione.  
- **Quale versione di Java è consigliata?** Java 11+ per prestazioni di livello produzione.

## Cos'è la firma PDF con codice a barre HIBC?
La classe `Signature` in GroupDocs.Signature for Java rappresenta un documento PDF e fornisce metodi per incorporare codici a barre HIBC come firme digitali. Firmando un PDF con un codice a barre HIBC crei un record verificabile, a prova di manomissione, che può essere scansionato in qualsiasi punto della catena di approvvigionamento.

## Perché usare Data Matrix e QR code insieme?
GroupDocs.Signature supporta **oltre 50 formati di input e output** e può elaborare PDF di centinaia di pagine senza caricare l'intero file in memoria. Utilizzare Data Matrix per etichette dense e di piccola area e QR per documenti più ampi ti offre il miglior equilibrio tra leggibilità, capacità di dati (fino a 4.296 caratteri per QR) ed efficienza dello spazio di stampa.

## Prerequisiti
- **JDK 11 o superiore** (Java 8 funziona ma Java 11+ è consigliato per prestazioni ottimali).  
- **IDE** come IntelliJ IDEA, Eclipse o VS Code con estensioni Java.  
- **Maven o Gradle** per la gestione delle dipendenze (esempi sotto).  
- **PDF di esempio** (ad es., `sample.pdf`) per testare l'implementazione.  
- **Licenza valida di GroupDocs.Signature** (prova gratuita per lo sviluppo, licenza a pagamento per la produzione).

## Configurazione di GroupDocs.Signature per Java

### Configurazione Maven
Aggiungi la dipendenza al tuo `pom.xml`:

```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

### Configurazione Gradle
Per i progetti Gradle, aggiungi questo al tuo `build.gradle`:

```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

### Opzione di download diretto
Puoi anche scaricare il file JAR direttamente da [GroupDocs.Signature for Java releases](https://releases.groupdocs.com/signature/java/) e aggiungerlo manualmente al classpath del tuo progetto. Questo approccio funziona bene in ambienti con rete limitata.

### Ottenere una licenza
Richiedi una prova gratuita o una licenza temporanea da GroupDocs per rimuovere le filigrane e sbloccare tutte le funzionalità. Le distribuzioni in produzione richiedono una licenza acquistata.

### Inizializzazione di base
La classe `Signature` è il punto di ingresso per tutte le operazioni di firma. Carica il PDF, applica il codice a barre e scrive il file firmato.

```java
import com.groupdocs.signature.Signature;

class InitializeSignature {
    public static void main(String[] args) {
        Signature signature = new Signature("sample.pdf");
        // Proceed with signing operations...
    }
}
```

## Come creare un PDF Data Matrix con codice a barre HIBC?
Carica il tuo PDF di origine, configura un oggetto `QrCodeSignOptions` per il formato Data Matrix e chiama `sign()` – è tutto ciò di cui hai bisogno per incorporare un codice a barre HIBC Data Matrix conforme. I passaggi seguenti ti guidano attraverso il codice esatto necessario. `QrCodeSignOptions` definisce le impostazioni per una firma di codice a barre, come tipo, contenuto, dimensione e posizione.

1. **Importa le classi necessarie** – queste ti danno accesso al motore di firma e alle opzioni Data Matrix.  

```java
import com.groupdocs.signature.Signature;
import com.groupdocs.signature.options.sign.QrCodeSignOptions;
import com.groupdocs.signature.domain.qrcodes.QrCodeTypes;
```

2. **Istanzia l'oggetto `Signature`** con percorsi assoluti per i file di origine e destinazione.  

```java
String sourceFilePath = "YOUR_DOCUMENT_DIRECTORY";
String destinFilePath = "YOUR_OUTPUT_DIRECTORY/SignWithHIBCLICQR.pdf";

final Signature signature = new Signature(sourceFilePath);
```

3. **Configura le opzioni Data Matrix** – imposta la stringa HIBC, scegli `QrCodeTypes.HIBCLICDataMatrix` e definisci le coordinate di posizionamento. `QrCodeTypes` enumera i formati di codice a barre supportati per le firme HIBC.  

```java
QrCodeSignOptions hibcLic_QR = new QrCodeSignOptions("A123PROD30917/75#422011907#GP293", QrCodeTypes.HIBCLICQR);
hibcLic_QR.setLeft(1); // Set the position from left
hibcLic_QR.setTop(1);   // Set the position from top
hibcLic_QR.setReturnContent(true); // Return content after signing
hibcLic_QR.setReturnContentType(FileType.PNG); // Specify return content type as PNG
```

4. **Applica la firma** al PDF.  

```java
signature.sign(destinFilePath, hibcLic_QR);
```

5. **Rilascia le risorse** per liberare i handle dei file ed evitare perdite di memoria.  

```java
finally {
    if (signature != null) signature.dispose();
}
```

### Esempio completo funzionante
Ecco il flusso completo in un unico blocco (i segnaposto rappresentano il codice esatto che incollerai dagli snippet precedenti):

```java
import com.groupdocs.signature.Signature;
import com.groupdocs.signature.options.sign.QrCodeSignOptions;
import com.groupdocs.signature.domain.qrcodes.QrCodeTypes;

public class HibcQrSigning {
    public static void main(String[] args) {
        String sourceFilePath = "sample.pdf";
        String destinFilePath = "output/SignWithHIBCLICQR.pdf";
        
        Signature signature = null;
        try {
            signature = new Signature(sourceFilePath);
            
            QrCodeSignOptions hibcLic_QR = new QrCodeSignOptions(
                "A123PROD30917/75#422011907#GP293", 
                QrCodeTypes.HIBCLICQR
            );
            hibcLic_QR.setLeft(1);
            hibcLic_QR.setTop(1);
            hibcLic_QR.setReturnContent(true);
            hibcLic_QR.setReturnContentType(FileType.PNG);
            
            signature.sign(destinFilePath, hibcLic_QR);
            System.out.println("PDF signed successfully with HIBC QR code");
            
        } catch (Exception e) {
            System.err.println("Error signing PDF: " + e.getMessage());
            e.printStackTrace();
        } finally {
            if (signature != null) signature.dispose();
        }
    }
}
```

#### Risposta diretta (40–70 parole)
Per **creare un PDF Data Matrix**, istanzia `Signature` con il tuo PDF di origine, imposta `QrCodeSignOptions` su `QrCodeTypes.HIBCLICDataMatrix` e fornisci una stringa HIBC formattata correttamente, quindi chiama `signature.sign(outputPath, options)`. La libreria scrive il PDF firmato nella destinazione, preservando il layout e incorporando il codice a barre come firma a prova di manomissione.

## Come aggiungere un PDF con QR code usando GroupDocs.Signature?
Carica il PDF, configura `QrCodeSignOptions` per il formato QR e invoca `sign()`. Questo modello a due righe funziona per qualsiasi dimensione di PDF e scala automaticamente l'immagine QR per una leggibilità ottimale. `QrCodeSignOptions` configura la firma del codice a barre QR, includendo il suo contenuto e le proprietà visive. Posiziona il codice in base alle coordinate impostate, garantendo che non si sovrapponga al contenuto esistente e rimanga scansionabile dopo la stampa.

1. **Importa le classi specifiche per QR**  

```java
QrCodeSignOptions hibcLic_AZ = new QrCodeSignOptions("A123PROD30917/75#422011907#GP293", QrCodeTypes.HIBCLICAztec);
hibcLic_AZ.setLeft(1); // Set the position from left
hibcLic_AZ.setTop(200); // Set the position from top
hibcLic_AZ.setReturnContent(true); // Return content after signing
hibcLic_AZ.setReturnContentType(FileType.PNG); // Specify return content type as PNG
```

2. **Crea e configura le opzioni QR** – nota l'uso di `QrCodeTypes.HIBCLICQR`.  

```java
signature.sign(destinFilePath, hibcLic_AZ);
```

3. **Firma il documento**  

```java
QrCodeSignOptions hibcLic_DM = new QrCodeSignOptions("A123PROD30917/75#422011907#GP293", QrCodeTypes.HIBCLICDataMatrix);
hibcLic_DM.setLeft(1); // Set the position from left
hibcLic_DM.setTop(400); // Set the position from top
hibcLic_DM.setReturnContent(true); // Return content after signing
hibcLic_DM.setReturnContentType(FileType.PNG); // Specify return content type as PNG
```

> **Risposta diretta:** Usa `QrCodeTypes.HIBCLICQR` in `QrCodeSignOptions`, imposta la stringa di contenuto HIBC, posiziona il codice con `setLeft()` e `setTop()`, quindi chiama `signature.sign(outputPath, options)`. Il codice a barre QR viene incorporato istantaneamente, pronto per la cattura da smartphone o scanner.

## Errori comuni da evitare

### 1. Dimenticare il rilascio delle risorse
**Sbagliato:**  
```java
Signature signature = new Signature("sample.pdf");
signature.sign(destinFilePath, options);
// Oops, no dispose() call
```  

**Correzione:** Avvolgi l'uso di `Signature` in un blocco try‑with‑resources o chiama esplicitamente `close()` in un blocco finally.

### 2. Usare stringhe di formato HIBC errate
**Sbagliato:** Usare stringhe generiche come “12345”.  
**Correzione:** Segui lo standard HIBCC (ad esempio `A123PROD30917/75#422011907#GP293`). Valida con il [validatore online HIBCC](https://www.hibcc.org/).

### 3. Codificare percorsi di file in modo statico
**Sbagliato:**  
```java
String sourceFilePath = "C:/Users/John/Documents/test.pdf";
```  

**Correzione:** Memorizza i percorsi in un file di configurazione o in una variabile d'ambiente e leggili a runtime.

### 4. Ignorare i conflitti di posizione del codice a barre
Posiziona i codici a barre lontano dal testo o dalle firme esistenti. Usa le coordinate PDF (l'origine è in basso a sinistra) e testa con un campione stampato.

### 5. Non testare con scanner reali
Stampa il PDF firmato e scansiona con l'hardware esatto usato nel tuo flusso di lavoro. Verifica la leggibilità a diverse qualità di stampa.

## Applicazioni pratiche in ambito sanitario

| Scenario | Codice a barre consigliato | Perché è adatto |
|----------|----------------------------|-----------------|
| **Distribuzione farmaceutica** | QR Code | Elevata capacità di dati, ampiamente scansionato da smartphone. |
| **Gestione dell'inventario** | Data Matrix | Piccola impronta, ideale per etichette di scaffale dense. |
| **Conformità normativa (FDA 21 CFR Part 11)** | QR + Data Matrix | Il doppio formato fornisce ridondanza e auditabilità. |
| **Tracciamento dispositivi medici** | Aztec Code | Dimensioni compatte funzionano su imballaggi con spazio limitato. |

## Considerazioni sulle prestazioni e migliori pratiche

### Modello di elaborazione batch
```java
List<String> filesToSign = getFileList();
for (String filePath : filesToSign) {
    Signature signature = null;
    try {
        signature = new Signature(filePath);
        // Sign and save
    } finally {
        if (signature != null) signature.dispose();
    }
}
```

- Crea una nuova istanza `Signature` per file per mantenere basso l'uso della memoria.  
- Usa un pool di thread fisso (`Executors.newFixedThreadPool(Runtime.getRuntime().availableProcessors() - 1)`) per l'elaborazione parallela, ma monitora la dimensione dell'heap poiché ogni `Signature` mantiene l'intero PDF in memoria.  

### Mantieni le librerie aggiornate
Le versioni di GroupDocs migliorano la velocità di elaborazione fino al **20 %** e aggiungono nuove funzionalità di conformità HIBC. Pianifica controlli delle dipendenze trimestrali.

### Cache dei modelli
Carica un modello PDF una volta, clonaloo per ogni variante di codice a barre e firma i cloni. Questo riduce I/O e velocizza i flussi di lavoro ad alto volume.

## Domande frequenti

**Q:** GroupDocs.Signature può firmare tipi di file diversi da PDF?  
**A:** Sì, supporta anche DOCX, XLSX, PPTX, PNG, JPEG e TIFF con la stessa API di firma dei codici a barre.

**Q:** Come risolvere gli errori “Invalid barcode content”?  
**A:** Verifica che la tua stringa HIBC segua esattamente la sintassi HIBCC, usa il validatore online e assicurati di utilizzare la costante `QrCodeTypes` corretta per il formato scelto.

**Q:** Qual è la capacità massima di dati per ciascun formato HIBC?  
**A:** QR ≈ 4.296 caratteri alfanumerici, Aztec ≈ 3.832 numerici / 3.067 alfanumerici, Data Matrix ≈ 3.116 numerici / 2.335 alfanumerici. Mantieni i codici sotto i 200 caratteri per una affidabilità di scansione ottimale.

**Q:** È possibile incorporare più tipi di codice a barre in un unico PDF?  
**A:** Assolutamente. Crea oggetti `QrCodeSignOptions` separati con posizioni diverse e chiama `signature.sign()` per ciascuno. Basta assicurarsi che non si sovrappongano.

**Q:** È necessaria una connessione internet per la firma a runtime?  
**A:** No. Dopo che il JAR è nel classpath e la licenza è attivata, tutte le operazioni vengono eseguite localmente.

## Risorse aggiuntive

- [Documentazione GroupDocs.Signature per Java](https://docs.groupdocs.com/signature/java/)  
- [Guida di riferimento API](https://reference.groupdocs.com/signature/java/)  
- [Download ultime versioni](https://releases.groupdocs.com/signature/java/)  
- [Acquista licenza](https://purchase.groupdocs.com/buy)  
- [Ottieni prova gratuita](https://releases.groupdocs.com/signature/java/)  
- [Richiedi licenza temporanea](https://purchase.groupdocs.com/temporary-license/)  
- [Forum GroupDocs](https://forum.groupdocs.com/c/signature/)

---

**Ultimo aggiornamento:** 2026-05-16  
**Testato con:** GroupDocs.Signature 23.12 per Java  
**Autore:** GroupDocs  

```java
signature.sign(destinFilePath, hibcLic_DM);
```

## Tutorial correlati

- [Crea firma PDF con codice a barre in Java – Guida GroupDocs](/signature/java/barcode-signatures/create-sign-pdfs-groupdocs-barcode-java/)
- [Crea firma codice a barre in Java – Aggiorna codici a barre PDF](/signature/java/barcode-signatures/java-groupdocs-signature-barcode-initialize-update/)
- [Come leggere PDF con QR code usando Java e GroupDocs.Signature](/signature/java/barcode-signatures/java-pdf-barcode-search-groupdocs-signature-api/)