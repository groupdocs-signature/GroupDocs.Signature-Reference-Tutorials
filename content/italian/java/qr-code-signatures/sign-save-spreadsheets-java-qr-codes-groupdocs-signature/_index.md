---
"date": "2025-05-08"
"description": "Scopri come firmare fogli di calcolo Excel con codici QR e salvarli in diversi formati utilizzando GroupDocs.Signature per Java. Proteggi i tuoi documenti in modo efficiente."
"title": "Firma e salva fogli di calcolo Excel con codici QR in Java utilizzando GroupDocs.Signature"
"url": "/it/java/qr-code-signatures/sign-save-spreadsheets-java-qr-codes-groupdocs-signature/"
"weight": 1
type: docs
---
# Firma e salva fogli di calcolo Excel con codici QR in Java utilizzando GroupDocs.Signature

## Introduzione

Nell'era digitale odierna, garantire l'autenticità dei documenti è più importante che mai. Che si tratti di contratti, accordi o fogli di calcolo finanziari, firmare i documenti in modo sicuro può far risparmiare tempo e prevenire le frodi. **GroupDocs.Signature per Java** è una potente libreria che semplifica l'inserimento di firme elettroniche in vari formati di documento. Questo tutorial ti guiderà nell'utilizzo di GroupDocs.Signature per firmare fogli di calcolo Excel con codici QR e salvarli in diversi formati.

### Cosa imparerai:
- Come firmare fogli di calcolo utilizzando firme con codice QR.
- Salva i documenti firmati in più formati di output come PDF, XLSX, ecc.
- Ottimizza le prestazioni della tua applicazione Java quando si tratta di firme di documenti.

Al termine di questo tutorial, avrai una solida conoscenza dell'integrazione e dell'utilizzo di GroupDocs.Signature per la firma delle attività nelle tue applicazioni Java. Approfondiamo la configurazione degli strumenti necessari prima di iniziare a implementare queste funzionalità!

## Prerequisiti

Prima di procedere con questa guida, assicurati di avere quanto segue:
- **Kit di sviluppo Java (JDK)** installato sul tuo computer.
- Conoscenza di base della programmazione Java e familiarità con i sistemi di compilazione Maven o Gradle.
- Un IDE come IntelliJ IDEA, Eclipse o NetBeans.

Inoltre, dovrai configurare GroupDocs.Signature per Java nel tuo progetto. La procedura di configurazione è semplice e può essere eseguita utilizzando dipendenze Maven o Gradle, come mostrato di seguito:

## Impostazione di GroupDocs.Signature per Java

Per iniziare, aggiungi la dipendenza GroupDocs.Signature al file di build del tuo progetto.

### Esperto
```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

### Gradle
```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

In alternativa, puoi scaricare la libreria direttamente da [GroupDocs.Signature per le versioni Java](https://releases.groupdocs.com/signature/java/).

#### Acquisizione della licenza
Per sfruttare appieno le funzionalità di GroupDocs.Signature:
- **Prova gratuita**: Inizia con una prova gratuita per esplorare le funzionalità di base.
- **Licenza temporanea**: Ottieni una licenza temporanea per l'accesso completo durante la valutazione.
- **Acquistare**: Per un utilizzo a lungo termine, si consiglia di acquistare una licenza commerciale.

### Inizializzazione e configurazione di base
Inizializzare il `Signature` classe passando il percorso del file del documento come mostrato di seguito:
```java
import com.groupdocs.signature.Signature;

// Inizializza con il percorso del tuo documento
Signature signature = new Signature("YOUR_DOCUMENT_DIRECTORY/SampleSpreadsheet.xlsx");
```

## Guida all'implementazione
In questa sezione, illustreremo i passaggi per firmare un foglio di calcolo e salvarlo utilizzando GroupDocs.Signature.

### Firmare un foglio di calcolo con il codice QR
#### Panoramica
Questa funzionalità consente di aggiungere firme con codice QR ai fogli di calcolo Excel. È particolarmente utile per aggiungere identificatori elettronici sicuri e facilmente scansionabili.
##### Passaggio 1: definire i percorsi dei file
Iniziamo definendo i percorsi per i file di input e di output:
```java
String filePath = "YOUR_DOCUMENT_DIRECTORY/SampleSpreadsheet.xlsx";
String outputFilePath = "YOUR_OUTPUT_DIRECTORY/signedDocument.pdf";
```
##### Passaggio 2: inizializzare l'oggetto firma
Crea un `Signature` oggetto con il percorso del file del tuo documento.
```java
Signature signature = new Signature(filePath);
```
##### Passaggio 3: creare opzioni di firma del codice QR
Configura le opzioni di firma del codice QR. Specifica proprietà come testo, tipo e posizione del codice QR:
```java
import com.groupdocs.signature.options.sign.QrCodeSignOptions;
import com.groupdocs.signature.domain.qrcodes.QrCodeTypes;

QrCodeSignOptions signOptions = new QrCodeSignOptions("JohnSmith");
signOptions.setEncodeType(QrCodeTypes.QR);
signOptions.setLeft(100); // Coordinata X
signOptions.setTop(100);  // Coordinata Y
```
##### Passaggio 4: Configurare le opzioni di salvataggio
Specificare come si desidera salvare il documento firmato, incluso il formato:
```java
import com.groupdocs.signature.options.saveoptions.SpreadsheetSaveOptions;
import com.groupdocs.signature.domain.enums.SpreadsheetSaveFileFormat;

SpreadsheetSaveOptions saveOptions = new SpreadsheetSaveOptions();
saveOptions.setFileFormat(SpreadsheetSaveFileFormat.Pdf);
saveOptions.setOverwriteExistingFiles(true);
```
##### Passaggio 5: firmare e salvare il documento
Infine, utilizzare il `sign` metodo per applicare la firma con codice QR e salvare il documento:
```java
try {
    signature.sign(outputFilePath, signOptions, saveOptions);
} catch (Exception e) {
    e.printStackTrace();
}
```
### Salvataggio di un documento in diversi formati di file di output
#### Panoramica
GroupDocs.Signature consente di salvare i documenti firmati in vari formati, quali PDF, XLSX e DOCX.
##### Passaggio 1: definire il percorso di output
Specificare il percorso e il formato del file di output desiderati:
```java
String outputPath = "YOUR_OUTPUT_DIRECTORY/signedDocument.pdf"; // Cambiare il formato secondo necessità
```
##### Passaggio 2: imposta le opzioni di salvataggio
Configurare `SpreadsheetSaveOptions` per definire come si desidera salvare il documento:
```java
SpreadsheetSaveOptions saveOptions = new SpreadsheetSaveOptions();
saveOptions.setFileFormat(SpreadsheetSaveFileFormat.Pdf); // Può essere modificato per formati diversi
saveOptions.setOverwriteExistingFiles(true);
```
##### Fase 3: Implementare l'operazione di firma
Utilizzare queste opzioni in un'operazione di firma. Assicurarsi che `signature` l'oggetto è inizializzato correttamente:
```java
// Esempio di utilizzo (supponendo che esista un oggetto firma)
signature.sign(outputPath, signOptions, saveOptions);
```
## Applicazioni pratiche
Ecco alcuni scenari reali in cui questa funzionalità può rivelarsi utile:
- **Documenti legali**: Firma i contratti in modo sicuro con i codici QR per una facile verifica.
- **Rapporti finanziari**: Aggiungi firme ai fogli di calcolo contenenti dati finanziari sensibili.
- **Gestione dell'inventario**: Utilizza i codici QR sui fogli di inventario per semplificare il monitoraggio e l'autenticazione.

## Considerazioni sulle prestazioni
Quando si lavora con la firma di documenti, tenere presente i seguenti suggerimenti:
- Ottimizza la gestione della memoria Java profilando l'utilizzo delle risorse durante le operazioni di firma.
- GroupDocs.Signature è ottimizzato per le prestazioni, ma assicurati di eseguirlo in un ambiente adatto per gestire in modo efficiente documenti di grandi dimensioni.

## Conclusione
questo punto, dovresti avere familiarità con GroupDocs.Signature per firmare e salvare fogli di calcolo Excel con codici QR. Questo potente strumento può migliorare notevolmente la sicurezza e l'autenticità dei tuoi documenti digitali. Come passaggio successivo, esplora funzionalità aggiuntive come firme testuali o firme con timbro per proteggere ulteriormente i tuoi documenti.

**Invito all'azione**: Prova a implementare queste soluzioni nei tuoi progetti oggi stesso!

## Sezione FAQ
1. **Quali formati supporta GroupDocs.Signature?**
   - Supporta PDF, XLSX, DOCX e altri.
2. **Come posso risolvere i problemi relativi alla firma?**
   - Controllare i messaggi di eccezione per eventuali indizi; assicurarsi che tutti i percorsi dei file siano corretti.
3. **È possibile firmare più pagine di un documento?**
   - Sì, specifica i numeri di pagina nelle opzioni di firma.
4. **GroupDocs.Signature può essere utilizzato nelle applicazioni web?**
   - Certamente, è molto adatto per le applicazioni Java lato server.
5. **Come posso ottenere supporto se necessario?**
   - Utilizzare il [Forum di supporto GroupDocs](https://forum.groupdocs.com/c/signature) per assistenza.

## Risorse
- **Documentazione**: Guide complete e riferimenti API possono essere trovati su [Documentazione GroupDocs](https://docs.groupdocs.com/signature/java/).
- **Riferimento API**: Informazioni dettagliate sono disponibili sul [Pagina di riferimento API](https://reference.groupdocs.com/signature/java/).
- **Scaricamento**: Accedi all'ultima versione su [Versioni di GroupDocs](https://releases.groupdocs.com/signature/java/).
- **Acquisto e licenza**: Scopri di più sulle opzioni di licenza su [Acquisto GroupDocs](https://purchase.groupdocs.com/buy) e ottieni una prova gratuita tramite [Prova gratuita di GroupDocs](http://www.groupdocs.com/pricing)