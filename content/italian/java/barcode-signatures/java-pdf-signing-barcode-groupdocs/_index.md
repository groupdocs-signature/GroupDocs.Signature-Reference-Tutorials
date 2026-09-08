---
categories:
- Java PDF Processing
date: '2026-07-20'
description: Scopri come creare una firma barcode in documenti PDF usando Java e GroupDocs.Signature.
  Tutorial passo-passo con esempi di codice e migliori pratiche.
keywords:
- create barcode signature
- how to add barcode
- generate code128 barcode
- add barcode pdf
- tamper evident barcode
lastmod: '2026-07-20'
linktitle: Crea firma barcode Java
og_description: Crea firma barcode in PDF usando Java con GroupDocs.Signature. Scopri
  passo-passo come aggiungere codici a barre Code128, posizionarli e proteggere i
  documenti.
og_image_alt: 'Developer guide: Create barcode signature in PDF using Java and GroupDocs'
og_title: Crea firma barcode in PDF usando Java – Guida completa
schemas:
- author: GroupDocs
  dateModified: '2026-07-20'
  description: Learn how to create barcode signature in PDF documents using Java and
    GroupDocs.Signature. Step-by-step tutorial with code examples and best practices.
  headline: How to Create Barcode Signature in PDF using Java
  type: TechArticle
- description: Learn how to create barcode signature in PDF documents using Java and
    GroupDocs.Signature. Step-by-step tutorial with code examples and best practices.
  name: How to Create Barcode Signature in PDF using Java
  steps:
  - name: Initialize the Signature object
    text: '**Definition anchor:** The `Signature` class is GroupDocs.Signature''s
      entry point for loading, modifying, and saving PDF documents. First, you need
      to tell GroupDocs which PDF you''re working with: **What''s happening here:**
      The `Signature` object loads your PDF into memory and prepares it for modifi'
  - name: Configure your barcode options (How to add barcode)
    text: '**Definition anchor:** `BarcodeSignOptions` encapsulates all settings required
      to render a barcode inside a PDF. Now let''s create the barcode signature with
      your data: - `"12345678"` is your barcode data — this could be an order ID,
      certificate number, or any identifier you need. - `Code128` is the '
  - name: Position your barcode (How to sign PDF with barcode)
    text: '**Definition anchor:** `SignatureOptions` provides layout properties such
      as page number, size, and alignment. Here''s where GroupDocs really shines —
      percentage‑based positioning means your barcode looks good on any PDF size:
      **Why percentages matter:** Imagine you''re signing both A4 documents and l'
  - name: Sign and save your document (How to add barcode pdf)
    text: 'Time to actually apply the signature and save your work: **Important note:**
      The output directory must exist before you run this code. GroupDocs won''t create
      nested directories for you, so create them first or handle that in your code:
      **What if something goes wrong?** Wrap this in a try‑catch block'
  type: HowTo
- questions:
  - answer: Yes! Call `signature.sign()` multiple times with different `BarcodeSignOptions`
      for each barcode type. Just ensure they don’t overlap.
    question: Can I use different barcode types in the same PDF?
  - answer: Code128 handles most ASCII characters fine. For Unicode or complex data,
      switch to QR codes—they support UTF‑8 encoding.
    question: How do I handle barcodes that contain special characters?
  - answer: Technically up to 128 characters, but readability drops significantly
      above 30‑40 characters. For larger payloads, use QR codes.
    question: What's the maximum data I can store in a Code128 barcode?
  - answer: Not noticeably—barcodes are vector graphics, typically adding only 5‑20
      KB per barcode depending on size and complexity.
    question: Will adding barcodes significantly increase my PDF file size?
  - answer: Yes! Use `options.setRotationAngle(90)` to rotate your barcode, which
      is handy for margin placement.
    question: Can I rotate barcodes or place them vertically?
  type: FAQPage
tags:
- pdf-signing
- barcode-signature
- document-security
- groupdocs
- java
- pdf
title: Come creare una firma barcode in PDF usando Java
type: docs
url: /it/java/barcode-signatures/java-pdf-signing-barcode-groupdocs/
weight: 1
---

# Come creare una firma barcode in PDF usando Java

In questo tutorial, imparerai come **creare una firma barcode** nei file PDF usando Java e GroupDocs.Signature. Le firme barcode incorporano identificatori leggibili da macchine che sono sia a prova di manomissione sia facili da scansionare—perfette per contratti, certificati, fatture e qualsiasi documento che richieda una verifica affidabile.

## Risposte rapide
- **Cos'è una firma barcode?** Un barcode incorporato in un PDF che memorizza dati strutturati e può essere letto da scanner o software.  
- **Quale tipo di barcode è consigliato?** Code128, perché gestisce dati alfanumerici in modo compatto.  
- **Ho bisogno di una licenza?** Una prova gratuita funziona per i test; è necessaria una licenza completa per la produzione.  
- **Posso posizionare il barcode su qualsiasi dimensione di pagina?** Sì—usa il posizionamento basato su percentuale per il ridimensionamento automatico.  
- **Il barcode è basato su vettori?** Sì, aggiunge solo pochi kilobyte al PDF e rimane nitido a qualsiasi risoluzione.  

## Cos'è una firma barcode?
Una firma barcode è un barcode basato su vettori incorporato direttamente in una pagina PDF, che funge sia da elemento visivo sia da firma crittografica verificabile in seguito. Memorizza dati strutturati, come ID o timestamp, garantendo l'integrità del documento e fornendo un riferimento leggibile da macchine.

## Perché le firme barcode sono importanti per i tuoi PDF
Le firme barcode forniscono ai PDF un identificatore compatto e leggibile da macchine che può essere scansionato istantaneamente, eliminando l'inserimento manuale dei dati e riducendo gli errori. Poiché sono incorporate come grafica vettoriale, rimangono nitide a qualsiasi risoluzione e aggiungono solo pochi kilobyte al file. Questa combinazione di leggibilità, prova di manomissione e dimensione minima le rende ideali per contratti, fatture, certificati e qualsiasi documento che richieda una verifica affidabile.

Ecco una sfida che probabilmente hai già affrontato: devi aggiungere identificatori unici ai PDF che siano sia leggibili da macchine sia a prova di manomissione. Forse stai lavorando su un sistema di gestione documentale, elaborando certificati o gestendo contratti che necessitano di verifica in futuro.

È qui che le firme barcode risultano utili. A differenza dei semplici timbri di testo, i barcode ti permettono di incorporare dati strutturati che scanner (e il tuo software) possono leggere immediatamente. Inoltre, combinandoli con la firma PDF tramite GroupDocs.Signature per Java, ottieni un modo potente per tracciare e verificare i documenti senza aggiungere ricerche complesse nel database.

In questa guida, imparerai esattamente come implementare le firme barcode nei tuoi PDF Java — dalla configurazione di base al codice pronto per la produzione con posizionamento flessibile. Che tu stia costruendo un sistema di fatturazione, un generatore di certificati o una piattaforma di gestione contratti, avrai tutto il necessario al termine.

**Cosa imparerai:**
- Configurare GroupDocs.Signature per Java in pochi minuti  
- Creare firme barcode Code128 (e perché sono spesso la scelta migliore)  
- Posizionare i barcode usando layout basati su percentuale che funzionano su qualsiasi dimensione di PDF  
- Evitare gli errori comuni che ostacolano gli sviluppatori  
- Testare correttamente la tua implementazione  

## Come creare una firma barcode in Java
Creare una firma barcode in Java comporta il caricamento del PDF di destinazione, la configurazione delle opzioni del barcode (dati, tipo, dimensione e posizione) e l'applicazione della firma per generare un nuovo documento. GroupDocs.Signature gestisce il rendering e il legame crittografico, quindi devi solo fornire i parametri desiderati e gestire i percorsi dei file.

## Prerequisiti e checklist dell'ambiente

Prima di immergerti, verifica di avere i seguenti elementi pronti:

- **Java Development Kit (JDK) 8 o superiore** – richiesto per tutte le librerie Java di GroupDocs.  
- **Maven o Gradle** – per gestire la dipendenza GroupDocs.Signature.  
- **Un IDE** come IntelliJ IDEA, Eclipse o VS Code con estensioni Java.  
- **GroupDocs.Signature per Java** (si consiglia la versione 23.12 o più recente).  
- **Conoscenza di base di Java** – dovresti sentirti a tuo agio nella creazione di classi, nella gestione delle eccezioni e nella manipolazione di file I/O.

## Configurare GroupDocs.Signature nel tuo progetto

Ottenere la libreria nel tuo progetto è semplice. Scegli il tuo strumento di build:

**Per gli utenti Maven**, aggiungi questa dipendenza al tuo `pom.xml`:

```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

**Usi Gradle?** Aggiungi questa riga al tuo `build.gradle`:

```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

**Preferisci l'installazione manuale?** Scarica il JAR direttamente da [GroupDocs.Signature for Java releases](https://releases.groupdocs.com/signature/java/) e aggiungilo al tuo classpath.

### Ottenere la licenza

Prima di passare alla produzione, dovrai gestire la licenza:

- **Prova gratuita:** Perfetta per i test — ottienila dal sito GroupDocs per esplorare le funzionalità principali.  
- **Licenza temporanea:** Hai bisogno di più tempo per valutare? Richiedi una licenza temporanea di 30 giorni.  
- **Licenza completa:** Pronto per la produzione? Acquista una licenza per utilizzo illimitato.  

Ecco un rapido controllo di sanità per assicurarti che tutto funzioni:

```java
Signature signature = new Signature("sample.pdf");
System.out.println("Signature object created successfully.");
```

Se questo viene eseguito senza errori, sei pronto!

## Come creare una firma barcode in Java

Ora arriva la parte divertente — firmiamo un PDF con un barcode. Divideremo il processo in passaggi piccoli così capirai esattamente cosa succede in ogni fase.

### Passo 1: Inizializzare l'oggetto Signature

**Definition anchor:** La classe `Signature` è il punto di ingresso di GroupDocs.Signature per caricare, modificare e salvare documenti PDF.

Per prima cosa, devi indicare a GroupDocs quale PDF stai utilizzando:

```java
Signature signature = new Signature("input.pdf");
```

**What's happening here:** L'oggetto `Signature` carica il tuo PDF in memoria e lo prepara per le modifiche. Assicurati che il percorso del file sia corretto — un errore comune è usare le barre rovesciate su Windows senza escape (usa `\\` o semplicemente le barre forward, che funzionano su tutte le piattaforme).

### Passo 2: Configurare le opzioni del barcode (Come aggiungere il barcode)

**Definition anchor:** `BarcodeSignOptions` incapsula tutte le impostazioni necessarie per renderizzare un barcode all'interno di un PDF.

Ora creiamo la firma barcode con i tuoi dati:

```java
BarcodeSignOptions options = new BarcodeSignOptions("12345678");
options.setEncodeType(BarcodeEncodeType.Code128);
```

- `"12345678"` è il tuo dato barcode — può essere un ID ordine, numero di certificato o qualsiasi identificatore necessario.  
- `Code128` è il tipo di codifica (vedi più sotto per scegliere il tipo corretto).

**Pro tip:** Code128 può gestire sia numeri sia lettere, rendendolo versatile per la maggior parte dei casi d'uso. Se ti servono solo numeri, `Code39` potrebbe essere più semplice, ma Code128 ti offre maggiore flessibilità.

### Passo 3: Posizionare il barcode (Come firmare il PDF con il barcode)

**Definition anchor:** `SignatureOptions` fornisce proprietà di layout come numero di pagina, dimensione e allineamento.

Ecco dove GroupDocs brilla davvero — il posizionamento basato su percentuale significa che il tuo barcode appare bene su qualsiasi dimensione di PDF:

```java
options.setLeft(10);   // 10% from the left edge
options.setTop(90);    // 90% from the bottom edge (near the footer)
options.setWidth(30);  // 30% of page width
options.setHeight(10); // 10% of page height
options.setPageNumber(1);
```

**Why percentages matter:** Immagina di firmare sia documenti A4 sia moduli formato legal. Con il posizionamento percentuale, il barcode si scala automaticamente per apparire coerente su entrambi. L'uso di valori fissi in pixel renderebbe il barcode troppo piccolo su documenti grandi o troppo grande su quelli piccoli.

**Real‑world example:** Su una pagina A4 (595 × 842 punti), un barcode largo il 30 % sarà circa 180 punti. Su una pagina legal (612 × 1008 punti), sarà circa 184 punti — automaticamente proporzionale.

### Passo 4: Firmare e salvare il documento (Come aggiungere il barcode al PDF)

È il momento di applicare la firma e salvare il lavoro:

```java
signature.sign(outputPath, options);
```

**Important note:** La directory di output deve esistere prima di eseguire questo codice. GroupDocs non crea directory nidificate per te, quindi creale prima o gestiscile nel tuo codice:

```java
new File("output").mkdirs();
```

**What if something goes wrong?** Avvolgi il tutto in un blocco try‑catch:

```java
try {
    signature.sign("signed.pdf", options);
} catch (Exception e) {
    e.printStackTrace();
}
```

## Scegliere il tipo di barcode giusto per le tue esigenze (generare barcode code128)

GroupDocs supporta più formati di barcode, e scegliere quello giusto è importante. Ecco un confronto pratico:

**Code128 (La nostra scelta predefinita):**
- **Ideale per:** Dati alfanumerici misti (ID come "INV2024-001")  
- **Capacità:** Fino a 128 caratteri ASCII  
- **Perché è la migliore:** Compatto, ampiamente supportato, gestisce sia lettere che numeri  
- **Usalo quando:** Hai bisogno di flessibilità e non sai che tipo di dati codificherai  

**Code39:**
- **Ideale per:** Codici alfanumerici semplici  
- **Capacità:** 43 caratteri (A‑Z, 0‑9 e alcuni simboli)  
- **Perché considerarlo:** Gli scanner più vecchi lo supportano meglio  
- **Usalo quando:** Lavori con sistemi legacy o la semplicità è più importante della densità dei dati  

**QR Code:**
- **Ideale per:** Grandi quantità di dati (URL, payload JSON)  
- **Capacità:** Fino a 3 KB di dati  
- **Perché è potente:** Può memorizzare strutture dati complesse, correzione d'errore integrata  
- **Usalo quando:** Devi incorporare dati strutturati o URL  

**EAN/UPC:**
- **Ideale per:** Identificazione di prodotti  
- **Capacità:** Codici numerici a lunghezza fissa (8‑13 cifre)  
- **Usalo quando:** Lavori con sistemi di retail o inventario  

**Guida rapida alla decisione:**  
- Hai bisogno di lettere e numeri? → Code128  
- Solo numeri, mantieni semplice? → Code39  
- Molti dati o URL? → QR Code  
- Codici retail/prodotto? → EAN/UPC  

## Problemi comuni e come evitarli (barcode a prova di manomissione)

Ecco i problemi più frequenti che gli sviluppatori incontrano (così non dovrai farlo tu):

### Problema 1: Il posizionamento del barcode è errato

**Symptom:** Il tuo barcode appare in posizioni inattese o viene tagliato.

**Common causes:**  
- Uso di valori in pixel su pagine di dimensioni diverse  
- Dimenticare che le coordinate PDF partono dall'angolo in basso‑sinistra, non dall'alto‑sinistra  
- Margini che spingono il contenuto fuori dall'area visibile  

**Solution:** Usa sempre il posizionamento basato su percentuale per coerenza:

```java
options.setLeft(5);
options.setTop(95);
options.setWidth(40);
options.setHeight(12);
```

### Problema 2: Il testo del barcode è illeggibile

**Symptom:** Il testo codificato è visibile ma gli scanner non riescono a leggerlo.

**Causes:**  
- Barcode troppo piccolo per la quantità di dati  
- Tipo di codifica errato per i tuoi dati  
- Basso contrasto tra barre e sfondo  

**Solution:** Adatta la dimensione del barcode alla lunghezza dei dati. Per Code128 con 10‑15 caratteri, punta a almeno l'8‑10 % della larghezza della pagina.

### Problema 3: Eccezioni relative ai percorsi dei file

**Symptom:** `FileNotFoundException` o errori simili.

**Causes:**  
- Percorsi Windows hard‑coded con singole barre rovesciate  
- Directory di output inesistente  
- Problemi di permessi sui file  

**Solution:** Usa barre forward (funzionano ovunque) e crea le directory prima:

```java
Path output = Paths.get("output/signed.pdf");
Files.createDirectories(output.getParent());
```

### Problema 4: Problemi di memoria con PDF di grandi dimensioni

**Symptom:** Errori di out of memory durante l'elaborazione di documenti voluminosi.

**Solution:** Chiudi l'oggetto `Signature` quando hai finito per liberare le risorse:

```java
signature.close();
```

## Testare la tua implementazione barcode

Prima di distribuire, assicurati che i barcode funzionino davvero. Ecco una checklist pratica di test:

### 1. Test di ispezione visiva
Apri il PDF firmato e verifica:
- Il barcode è visibile e correttamente posizionato?  
- È nitido (non sfocato o pixelato)?  
- C'è spazio bianco sufficiente attorno?

### 2. Test di scansione
Usa un'app di scanner barcode sul telefono (come “Barcode Scanner” o “QR & Barcode Reader”) per verificare:
- Lo scanner legge il tuo barcode  
- I dati decodificati corrispondono a quelli codificati  
- Funziona da angolazioni e distanze diverse

### 3. Test cross‑platform
Apri il PDF su dispositivi diversi:
- Windows (Adobe Reader, Chrome)  
- Mac (Preview, Chrome)  
- Dispositivi mobili (iOS, Android)  

Assicurati che il barcode venga renderizzato correttamente ovunque.

### 4. Codice di test automatizzato
Ecco un semplice test che puoi eseguire:

```java
Signature testSignature = new Signature("signed.pdf");
List<BarcodeSignature> signatures = testSignature.search(BarcodeSignature.class);
if (signatures.size() > 0) {
    System.out.println("Barcode found: " + signatures.get(0).getText());
}
```

## Casi d'uso reali per le firme barcode

Esaminiamo dove questa tecnica brilla davvero nei sistemi di produzione:

### 1. Generazione e verifica di certificati
**Scenario:** Stai costruendo una piattaforma di formazione che rilascia certificati di completamento.  
**Implementazione:** Genera un ID certificato unico (es. “CERT‑2024‑00123”) e incorporalo come barcode Code128 nell'angolo in basso a destra. La scansione del barcode permette alla tua API di recuperare i dettagli del certificato istantaneamente, eliminando l'inserimento manuale dei dati.  

### 2. Sistemi di tracciamento fatture
**Scenario:** La tua azienda elabora migliaia di fatture mensili.  
**Implementazione:** Aggiungi numero fattura e data di scadenza come QR code posizionato dove le apparecchiature di scansione possono leggerlo facilmente. I sistemi di smistamento automatico possono instradare le fatture senza intervento umano, riducendo il tempo di elaborazione da ore a minuti.  

### 3. Gestione contratti legali
**Scenario:** Uno studio legale deve tracciare versioni e modifiche dei contratti.  
**Implementazione:** Ogni versione del contratto ottiene un identificatore barcode unico che include ID contratto, numero di versione e data di firma. La scansione durante gli audit richiama automaticamente la cronologia completa della versione.  

### 4. Sicurezza delle cartelle cliniche
**Scenario:** Un ospedale vuole prevenire accessi non autorizzati alle cartelle cliniche.  
**Implementazione:** Incorpora ID paziente e timestamp di creazione del record in un barcode. Solo dispositivi autenticati possono decodificare e accedere al record completo, e ogni scansione genera un log di audit per la conformità.  

## Suggerimenti per l'ottimizzazione delle prestazioni (sicurezza documenti Java)

Quando firmi molti PDF, le prestazioni contano. Ecco alcuni consigli per mantenere tutto fluido:

### Strategia di elaborazione batch
Invece di firmare un documento alla volta, elabora in batch:

```java
for (String filePath : pdfList) {
    Signature batchSignature = new Signature(filePath);
    batchSignature.sign(outputPath, options);
    batchSignature.close();
}
```

**Why this helps:** Riutilizzare l'oggetto delle opzioni e chiudere correttamente le risorse evita perdite di memoria.

### Gestione della memoria per PDF di grandi dimensioni
Per PDF superiori a 50 MB:
- Elaborali sequenzialmente anziché caricarne più di uno contemporaneamente.  
- Usa try‑with‑resources per garantire la pulizia.  
- Monitora la dimensione dell'heap e regola i parametri JVM se necessario: `-Xmx2g`.

### Cache di barcode usati frequentemente
Se firmi molti documenti con lo stesso barcode, metti in cache l'istanza `BarcodeSignOptions`:

```java
BarcodeSignOptions cachedOptions = new BarcodeSignOptions("STATIC_ID");
cachedOptions.setEncodeType(BarcodeEncodeType.Code128);
```

## Quando usare le firme barcode (e quando no)

**Scenari perfetti:**
- Hai bisogno di identificatori leggibili da macchine.  
- I documenti saranno scansionati o elaborati automaticamente.  
- Vuoi tracciamento a prova di manomissione senza certificati digitali.  
- È necessaria integrazione con infrastrutture barcode esistenti.  

**Non ideale quando:**
- Hai bisogno di firme digitali legalmente vincolanti (usa certificati digitali).  
- I documenti saranno visualizzati solo da esseri umani (un semplice watermark di testo può bastare).  
- Lavori con documenti estremamente piccoli dove un barcode occuperebbe troppo spazio.  
- I requisiti di sicurezza impongono crittografia—i barcode sono visibili e scansionabili da chiunque.  

**Puoi combinare gli approcci?** Assolutamente! Molti sistemi usano sia le firme barcode per il tracciamento sia le firme digitali per la validità legale.

## Domande frequenti

**Q: Posso usare diversi tipi di barcode nello stesso PDF?**  
A: Sì! Chiama `signature.sign()` più volte con diversi `BarcodeSignOptions` per ogni tipo di barcode. Assicurati solo che non si sovrappongano.

**Q: Come gestisco i barcode che contengono caratteri speciali?**  
A: Code128 gestisce la maggior parte dei caratteri ASCII. Per Unicode o dati complessi, passa ai QR code—supportano la codifica UTF‑8.

**Q: Qual è la quantità massima di dati che posso memorizzare in un barcode Code128?**  
A: Tecnicamente fino a 128 caratteri, ma la leggibilità diminuisce notevolmente oltre i 30‑40 caratteri. Per payload più grandi, usa i QR code.

**Q: L'aggiunta di barcode aumenterà notevolmente le dimensioni del mio PDF?**  
A: No, non in modo significativo—i barcode sono grafica vettoriale, tipicamente aggiungono solo 5‑20 KB per barcode a seconda di dimensione e complessità.

**Q: Posso ruotare i barcode o posizionarli verticalmente?**  
A: Sì! Usa `options.setRotationAngle(90)` per ruotare il barcode, utile per il posizionamento sui margini.

**Q: Come faccio a far apparire i barcode su ogni pagina di un PDF multi‑pagina?**  
A: Itera sulle pagine e applica la firma a ciascuna. Consulta la classe `PagesSetup` nella documentazione GroupDocs per controllare quali pagine firmare.

**Q: Cosa succede se lo scanner barcode non legge il barcode generato?**  
A: Prima verifica che lo scanner supporti il tipo di barcode scelto. Poi aumenta la dimensione del barcode—la maggior parte dei problemi di scansione deriva da barre troppo piccole. Punta a una larghezza di almeno 1 pollice (2,54 cm) per letture affidabili.

## Risorse aggiuntive

**Documentazione:**  
- [GroupDocs.Signature for Java Docs](https://docs.groupdocs.com/signature/java/)  
- [API Reference Guide](https://reference.groupdocs.com/signature/java/)  

**Download e licenze:**  
- [Download Latest Version](https://releases.groupdocs.com/signature/java/)  
- [Free Trial Access](https://releases.groupdocs.com/signature/java/)  
- [Get Temporary License](https://purchase.groupdocs.com/temporary-license/)  
- [Purchase Full License](https://purchase.groupdocs.com/buy)  

**Community e supporto:**  
- [Support Forum](https://forum.groupdocs.com/c/signature/) - Community attiva con ingegneri GroupDocs  

---

**Last Updated:** 2026-07-20  
**Tested With:** GroupDocs.Signature 23.12 (Java)  
**Author:** GroupDocs

```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

```java
import com.groupdocs.signature.Signature;

public class QuickTest {
    public static void main(String[] args) {
        try {
            Signature signature = new Signature("test-document.pdf");
            System.out.println("GroupDocs.Signature is ready to go!");
        } catch (Exception e) {
            System.err.println("Setup issue: " + e.getMessage());
        }
    }
}
```

```java
String filePath = "YOUR_DOCUMENT_DIRECTORY/sample.pdf";
Signature signature = new Signature(filePath);
```

```java
import com.groupdocs.signature.options.sign.BarcodeSignOptions;
import com.groupdocs.signature.domain.barcodes.BarcodeTypes;

BarcodeSignOptions options = new BarcodeSignOptions("12345678");
options.setEncodeType(BarcodeTypes.Code128);
```

```java
import com.groupdocs.signature.domain.enums.MeasureType;
import com.groupdocs.signature.domain.Padding;

// Use percentages instead of fixed pixels
options.setLocationMeasureType(MeasureType.Percents);
options.setLeft(5);  // 5% from the left edge
options.setTop(5);   // 5% from the top

// Size it proportionally too
options.setSizeMeasureType(MeasureType.Percents);
options.setWidth(10);  // 10% of page width
options.setHeight(5);  // 5% of page height

// Add some breathing room with margins
Padding margins = new Padding();
margins.setLeft(1);
margins.setTop(1);
margins.setRight(1);
options.setMargin(margins);
```

```java
String outputFilePath = "YOUR_OUTPUT_DIRECTORY/SignWithPercents/sample_signed.pdf";
signature.sign(outputFilePath, options);
```

```java
Path outputPath = Paths.get(outputFilePath);
Files.createDirectories(outputPath.getParent());
signature.sign(outputFilePath, options);
```

```java
try {
    signature.sign(outputFilePath, options);
    System.out.println("PDF signed successfully at: " + outputFilePath);
} catch (Exception e) {
    System.err.println("Signing failed: " + e.getMessage());
    e.printStackTrace();
}
```

```java
options.setLocationMeasureType(MeasureType.Percents);
options.setLeft(5);  // 5% from left works on any page width
```

```java
options.setWidth(10);  // Give it room to breathe
options.setHeight(5);  // Maintain proper aspect ratio
```

```java
String filePath = "documents/sample.pdf";  // Works on Windows, Mac, Linux
Files.createDirectories(Paths.get("output/signed"));
```

```java
try (Signature signature = new Signature(filePath)) {
    signature.sign(outputFilePath, options);
} // Automatically closes and releases memory
```

```java
import org.junit.Test;
import static org.junit.Assert.*;

public class BarcodeSignatureTest {
    
    @Test
    public void testBarcodeSigning() {
        String testPdf = "test-data/sample.pdf";
        String output = "test-output/signed.pdf";
        
        try (Signature signature = new Signature(testPdf)) {
            BarcodeSignOptions options = new BarcodeSignOptions("TEST123");
            options.setEncodeType(BarcodeTypes.Code128);
            
            signature.sign(output, options);
            
            // Verify output file exists
            assertTrue(new File(output).exists());
            
            // Verify file size increased (signature was added)
            long originalSize = new File(testPdf).length();
            long signedSize = new File(output).length();
            assertTrue(signedSize > originalSize);
            
        } catch (Exception e) {
            fail("Signing should not throw exception: " + e.getMessage());
        }
    }
}
```

```java
List<String> pdfFiles = Arrays.asList("doc1.pdf", "doc2.pdf", "doc3.pdf");

for (String pdfFile : pdfFiles) {
    try (Signature signature = new Signature(pdfFile)) {
        BarcodeSignOptions options = createBarcodeOptions(); // Reuse options
        signature.sign(getOutputPath(pdfFile), options);
    }
}
```

```java
// Create options once, reuse many times
BarcodeSignOptions templateOptions = createStandardBarcodeOptions();

// For each document, clone and customize
BarcodeSignOptions documentOptions = templateOptions.clone();
documentOptions.setText(uniqueDocumentId);
```

## Tutorial correlati

- [Java Barcode Signature Tutorial - Add, Verify & Manage Barcodes in PDFs](/signature/java/barcode-signatures/)
- [Create Barcode Signature in Java – Update PDF Barcodes](/signature/java/barcode-signatures/java-groupdocs-signature-barcode-initialize-update/)
- [How to read QR code PDF using Java and GroupDocs.Signature](/signature/java/barcode-signatures/java-pdf-barcode-search-groupdocs-signature-api/)