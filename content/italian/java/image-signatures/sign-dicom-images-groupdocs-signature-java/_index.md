---
"date": "2025-05-08"
"description": "Scopri come firmare in modo sicuro le immagini DICOM utilizzando GroupDocs.Signature per Java. Migliora la sicurezza dei documenti incorporando codici QR e metadati."
"title": "Firma immagini DICOM con codici QR e metadati utilizzando GroupDocs.Signature per Java"
"url": "/it/java/image-signatures/sign-dicom-images-groupdocs-signature-java/"
"weight": 1
type: docs
---
# Come firmare immagini DICOM con codici QR e metadati utilizzando GroupDocs.Signature per Java

## Introduzione

Nel panorama sanitario digitale in rapida evoluzione, la gestione sicura dei dati dei pazienti è fondamentale. Questo tutorial vi guiderà nell'implementazione di una soluzione affidabile che utilizza GroupDocs.Signature per Java per firmare immagini DICOM (Digital Imaging and Communications in Medicine) con codici QR e metadati. Queste funzionalità garantiscono l'autenticità, migliorano la tracciabilità e mantengono la conformità incorporando informazioni vitali direttamente nelle immagini mediche.

### Cosa imparerai:
- Come integrare GroupDocs.Signature per Java nel tuo progetto.
- Il processo di firma delle immagini DICOM con codici QR.
- Aggiunta di metadati XMP per migliorare la sicurezza dei documenti.
- Recupero, verifica e ricerca di firme nei file DICOM.
- Generazione di anteprime di immagini DICOM firmate.

Cominciamo! Prima di iniziare, assicuriamoci che tu abbia tutto il necessario per seguire il tutorial senza intoppi.

## Prerequisiti

Per implementare efficacemente le funzionalità di GroupDocs.Signature, assicurati di soddisfare i seguenti prerequisiti:

### Librerie e dipendenze richieste
- **GroupDocs.Signature per Java**: Avrai bisogno della versione 23.12 o successiva di questa libreria.

### Requisiti di configurazione dell'ambiente
- **Kit di sviluppo Java (JDK)**: Assicurati che JDK sia installato sul tuo sistema.
- **IDE**: Utilizzare un ambiente di sviluppo integrato come IntelliJ IDEA o Eclipse.

### Prerequisiti di conoscenza
Una conoscenza di base di:
- Programmazione Java e principi orientati agli oggetti.
- Strumenti di compilazione Maven o Gradle per la gestione delle dipendenze.

## Impostazione di GroupDocs.Signature per Java

Per iniziare a utilizzare GroupDocs.Signature, è necessario aggiungerlo come dipendenza al progetto. Ecco come farlo utilizzando diversi strumenti di compilazione:

### Esperto
Aggiungi il seguente frammento al tuo `pom.xml` file:
```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

### Gradle
Includi questo nel tuo `build.gradle` file:
```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

### Download diretto
In alternativa, puoi scaricare l'ultima versione da [GroupDocs.Signature per le versioni Java](https://releases.groupdocs.com/signature/java/).

#### Fasi di acquisizione della licenza
1. **Prova gratuita**: Prova le funzionalità con una prova gratuita a tempo limitato.
2. **Licenza temporanea**Ottieni una licenza temporanea per esplorare tutte le funzionalità.
3. **Acquistare**: Acquista un abbonamento se hai bisogno di un accesso a lungo termine.

#### Inizializzazione e configurazione di base

Per inizializzare GroupDocs.Signature, creare un'istanza di `Signature` classe:
```java
import com.groupdocs.signature.Signature;

// Inizializza l'oggetto firma con il percorso del tuo file DICOM
Signature signature = new Signature(filePath);
```

## Guida all'implementazione

### Firma di un'immagine DICOM con codice QR e metadati

#### Panoramica
Questa funzione consente di firmare le immagini DICOM con un codice QR e di aggiungere metadati XMP, migliorando la sicurezza dei documenti.

#### Passaggio 1: imposta le opzioni di firma del codice QR
```java
import com.groupdocs.signature.domain.Padding;
import com.groupdocs.signature.domain.enums.HorizontalAlignment;
import com.groupdocs.signature.domain.enums.VerticalAlignment;
import com.groupdocs.signature.domain.signatures.QrCodeSignOptions;

Padding padding = new Padding();
padding.setRight(5);
padding.setLeft(5);

QrCodeSignOptions options = new QrCodeSignOptions("Patient #36363393. R: No-Issues");
options.setAllPages(true);
options.setWidth(100);
options.setHeight(100);
options.setVerticalAlignment(VerticalAlignment.Bottom);
options.setHorizontalAlignment(HorizontalAlignment.Right);
options.setMargin(padding);
```
Qui configuriamo l'aspetto e la posizione del codice QR sull'immagine DICOM.

#### Passaggio 2: aggiungere metadati XMP
```java
import com.groupdocs.signature.options.saveoptions.imagessaveoptions.DicomSaveOptions;
import com.groupdocs.signature.options.saveoptions.imagessaveoptions.DicomXmpEntry;
import com.groupdocs.signature.options.saveoptions.imagessaveoptions.DicomXmpType;

DicomSaveOptions dicomSaveOptions = new DicomSaveOptions();
List<DicomXmpEntry> xmpEntries = new ArrayList<>();
xmpEntries.add(new DicomXmpEntry(DicomXmpType.PatientName, "Patient #4"));
dicomSaveOptions.setXmpEntries(xmpEntries);
```
Questo frammento aggiunge metadati al file DICOM, incorporando ulteriori informazioni sul paziente.

#### Fase 3: Firmare il documento
```java
String outputFilePath = YOUR_OUTPUT_DIRECTORY + "/SignDicomImageAdvanced/" + fileName;
signature.sign(outputFilePath, options, dicomSaveOptions);
```
IL `sign` Il metodo scrive il codice QR e i metadati nel file DICOM, salvandolo nella posizione specificata.

### Recupero delle informazioni sull'immagine DICOM firmata

#### Panoramica
Estrarre i metadati XMP da un'immagine DICOM firmata a scopo di verifica o audit.
```java
import com.groupdocs.signature.domain.IDocumentInfo;
import com.groupdocs.signature.domain.signatures.MetadataSignature;

IDocumentInfo documentInfo = signature.getDocumentInfo();
for (MetadataSignature item : documentInfo.getMetadataSignatures()) {
    System.out.println(item.toString());
}
```
Questo codice recupera e stampa tutte le firme dei metadati associate al file DICOM.

### Verifica DICOM firmato

#### Panoramica
Verificare che nell'immagine DICOM firmata sia presente una firma tramite codice QR per confermarne l'autenticità.
```java
import com.groupdocs.signature.domain.VerificationResult;
import com.groupdocs.signature.options.verify.QrCodeVerifyOptions;
import com.groupdocs.signature.domain.enums.TextMatchType;

QrCodeVerifyOptions verifyOptions = new QrCodeVerifyOptions();
verifyOptions.setAllPages(true);
verifyOptions.setText("Patient #36363393");
verifyOptions.setMatchType(TextMatchType.Contains);

VerificationResult result = signature.verify(verifyOptions);
if (result.isValid()) {
    System.out.println(filePath + " has successfully verified signatures!");
} else {
    System.out.println(filePath + " failed verification process.");
}
```
Questa fase di verifica garantisce che il codice QR corrisponda ai criteri previsti, confermando l'integrità del documento.

### Ricerca di firme in DICOM firmato

#### Panoramica
Individua tutte le firme del codice QR all'interno di un'immagine DICOM firmata per esaminarle o verificarle.
```java
import com.groupdocs.signature.domain.signatures.QrCodeSignature;
import java.util.List;

List<QrCodeSignature> signatures = signature.search(QrCodeSignature.class);
for (QrCodeSignature qrCodeSignature : signatures) {
    System.out.println("QRCode signature found at page " +
        qrCodeSignature.getPageNumber() + ": " +
        qrCodeSignature.getEncodeType().getTypeName() + ": " +
        qrCodeSignature.getText());
}
```
Questa funzione è utile per scansionare tutte le firme con codice QR presenti nel documento, garantendo una visibilità completa.

### Generazione dell'anteprima del DICOM firmato

#### Panoramica
Crea anteprime per ogni pagina di un'immagine DICOM firmata, consentendo una rapida ispezione visiva senza dover aprire l'intero file.
```java
import com.groupdocs.signature.options.PreviewOptions;
import java.io.File;
import java.io.FileOutputStream;
import java.nio.file.Paths;

PreviewOptions previewOption = new PreviewOptions(pageNumber -> {
    try {
        String pageFilePath = YOUR_OUTPUT_DIRECTORY + "/SignDicomImageAdvanced/image-" + pageNumber + ".jpg";
        return new FileOutputStream(Paths.get(pageFilePath).toFile());
    } catch (Exception e) {
        throw new RuntimeException(e.getMessage());
    }
});

signature.generatePreview(previewOption);
```
Questo frammento genera anteprime delle immagini per ogni pagina, utili per una rapida verifica o condivisione.

## Applicazioni pratiche

GroupDocs.Signature per Java offre numerose applicazioni concrete:
- **Imaging medico**: Firma e gestisci in modo sicuro le immagini DICOM dei pazienti con codici QR e metadati.
- **Gestione dei documenti legali**: Migliorare l'autenticità e la conformità dei documenti nei procedimenti legali.
- **Servizi finanziari**: Implementare firme elettroniche sicure sui documenti finanziari sensibili.