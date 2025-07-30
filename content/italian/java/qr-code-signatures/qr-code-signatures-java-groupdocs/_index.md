---
"date": "2025-05-08"
"description": "Scopri come migliorare la sicurezza dei documenti implementando e verificando le firme tramite codice QR in Java con GroupDocs.Signature. Segui questa guida passo passo per un processo di firma sicuro."
"title": "Proteggi i tuoi documenti&#58; implementa le firme con codice QR in Java utilizzando GroupDocs.Signature"
"url": "/it/java/qr-code-signatures/qr-code-signatures-java-groupdocs/"
"weight": 1
---

# Proteggi i tuoi documenti: implementa le firme con codice QR in Java utilizzando GroupDocs.Signature

Nell'attuale panorama digitale, garantire la sicurezza di documenti come contratti, fatture o informazioni personali sensibili è fondamentale. Un approccio innovativo per migliorare la sicurezza dei documenti e semplificare i processi di verifica è l'utilizzo di firme basate su codici QR. Questo tutorial vi guiderà nell'implementazione e nella verifica delle firme basate su codici QR per i vostri documenti in Java utilizzando GroupDocs.Signature.

## Cosa imparerai
- Come firmare i documenti utilizzando i codici QR
- Verifica dei documenti firmati con i codici QR
- Ricerca di firme QR Code esistenti all'interno di un documento
- Aggiornamento ed eliminazione delle firme QR Code dai tuoi documenti

Configuriamo il tuo ambiente e iniziamo!

### Prerequisiti
Prima di iniziare, assicurati di avere i seguenti prerequisiti:

#### Librerie e dipendenze richieste
Avrai bisogno di GroupDocs.Signature per Java. Puoi includerlo tramite Maven o Gradle, oppure scaricarlo direttamente.

**Esperto**
```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

**Gradle**
```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

**Download diretto**
Scarica l'ultima versione da [GroupDocs.Signature per le versioni Java](https://releases.groupdocs.com/signature/java/).

#### Requisiti di configurazione dell'ambiente
- Assicurati di aver installato Java Development Kit (JDK) 8 o versione successiva.
- Utilizzare un IDE come IntelliJ IDEA, Eclipse o NetBeans.

#### Prerequisiti di conoscenza
È utile una conoscenza di base della programmazione Java e dell'elaborazione dei documenti.

## Impostazione di GroupDocs.Signature per Java
Per utilizzare GroupDocs.Signature nel tuo progetto, segui questi passaggi:
1. **Installazione**: Scegli tra Maven, Gradle o download diretto in base alla tua configurazione.
2. **Acquisizione della licenza**:
   - Inizia con una prova gratuita disponibile su [Sito web di GroupDocs](https://releases.groupdocs.com/signature/java/).
   - Valutare l'ottenimento di una licenza temporanea per test e sviluppo estesi da [Qui](https://purchase.groupdocs.com/temporary-license/).
3. **Inizializzazione di base**: 
    Ecco come inizializzare GroupDocs.Signature:

    ```java
    Signature signature = new Signature("YOUR_DOCUMENT_PATH");
    ```

Questo ti prepara all'implementazione delle firme tramite codice QR.

## Guida all'implementazione

### Firma il documento con la firma tramite codice QR
#### Panoramica
Firmare un documento utilizzando un QR Code implica l'inserimento di un codice univoco che rappresenta la tua firma digitale. Questo processo protegge il documento e consente di verificarne facilmente l'autenticità in un secondo momento.

##### Passaggio 1: imposta le opzioni di firma
```java
import com.groupdocs.signature.Signature;
import com.groupdocs.signature.domain.enums.HorizontalAlignment;
import com.groupdocs.signature.domain.enums.VerticalAlignment;
import com.groupdocs.signature.options.sign.QrCodeSignOptions;

Signature signature = new Signature("YOUR_DOCUMENT_PATH");
QrCodeSignOptions signOptions = new QrCodeSignOptions("John Smith", com.groupdocs.signature.domain.qrcodes.QrCodeTypes.QR);

signOptions.setVerticalAlignment(VerticalAlignment.Top);
signOptions.setHorizontalAlignment(HorizontalAlignment.Center);
signOptions.setWidth(100);
signOptions.setHeight(40);
```
**Spiegazione**: `QrCodeSignOptions` è configurato per creare un codice QR con testo e allineamento specifici. Regola larghezza e altezza secondo necessità.

##### Passaggio 2: personalizza l'aspetto della firma
```java
import java.awt.Color;

signOptions.setForeColor(Color.RED); // Imposta il colore del codice QR
com.groupdocs.signature.domain.SignatureFont signatureFont = new com.groupdocs.signature.domain.SignatureFont();
signatureFont.setSize(12);
signatureFont.setFamilyName("Comic Sans MS");
signOptions.setFont(signatureFont);
```
**Spiegazione**: La personalizzazione del carattere e del colore migliora l'identificazione visiva.

##### Fase 3: Firmare il documento
```java
import java.util.ArrayList;
import java.util.List;

List<String> signatureIds = new ArrayList<>();
List<com.groupdocs.signature.domain.BaseSignature> signedSignatures = signature.sign("YOUR_OUTPUT_PATH", signOptions).getSucceeded();

for (com.groupdocs.signature.domain.BaseSignature temp : signedSignatures) {
    signatureIds.add(temp.getSignatureId());
}
```
**Spiegazione**: In questo passaggio il documento viene firmato e gli ID della firma vengono memorizzati per riferimento futuro.

### Verifica il documento con la firma tramite codice QR
#### Panoramica
La verifica garantisce che un documento sia stato firmato legittimamente. Ecco come verificare una firma tramite QR Code in un documento.

##### Passaggio 1: imposta le opzioni di verifica
```java
import com.groupdocs.signature.Signature;
import com.groupdocs.signature.options.verify.QrCodeVerifyOptions;

Signature signature2 = new Signature("YOUR_OUTPUT_PATH");
QrCodeVerifyOptions verifyOptions = new QrCodeVerifyOptions();

verifyOptions.setEncodeType(QrCodeTypes.QR);
verifyOptions.setText("John Smith"); // Testo da verificare
verifyOptions.setAllPages(false); 
verifyOptions.setPageNumber(1);
```
**Spiegazione**Le opzioni di verifica specificano quale tipo di codice QR e testo cercare, assicurando che la firma corrisponda alle tue aspettative.

##### Passaggio 2: eseguire la verifica
```java
boolean isValid = signature2.verify(verifyOptions).isValid();
System.out.println("Is Signature Valid? " + isValid);
```
**Spiegazione**: Controlla se il documento contiene un codice QR valido che corrisponde ai tuoi criteri.

### Cerca documento per firma con codice QR
#### Panoramica
A volte è necessario individuare le firme esistenti all'interno di un documento. Ecco come cercarle utilizzando GroupDocs.Signature.

##### Passaggio 1: configurare le opzioni di ricerca
```java
import com.groupdocs.signature.domain.signatures.QrCodeSignature;
import com.groupdocs.signature.options.search.QrCodeSearchOptions;

Signature signature2 = new Signature("YOUR_OUTPUT_PATH");
QrCodeSearchOptions searchOptions = new QrCodeSearchOptions();
searchOptions.setAllPages(true);
```
**Spiegazione**: In questo modo lo strumento viene impostato per scansionare tutte le pagine alla ricerca di firme tramite codice QR.

##### Passaggio 2: eseguire la ricerca
```java
List<QrCodeSignature> signatures = signature2.search(QrCodeSignature.class, searchOptions);

for (QrCodeSignature qrSignature : signatures) {
    System.out.println("Found Signature ID: " + qrSignature.getSignatureId());
}
```
**Spiegazione**: Recupera tutte le firme QR Code presenti nel documento.

### Aggiorna la firma del codice QR del documento
#### Panoramica
Aggiornare una firma significa modificarne le proprietà, come la posizione o le dimensioni. Ecco come fare:

##### Fase 1: preparare le firme per l'aggiornamento
```java
import com.groupdocs.signature.domain.signatures.QrCodeSignature;
import java.io.ByteArrayOutputStream;

Signature signature2 = new Signature("YOUR_OUTPUT_PATH");
List<QrCodeSignature> signaturesToUpdate = new ArrayList<>();

// Supponendo che "firme" sia un elenco di oggetti QrCodeSignature ottenuti dalla ricerca
for (QrCodeSignature qrSignature : signatures) {
    qrSignature.setLeft(qrSignature.getLeft() + 100);
    qrSignature.setTop(qrSignature.getTop() + 100);
    qrSignature.setWidth(200);
    qrSignature.setHeight(50);
    signaturesToUpdate.add(qrSignature);
}
```
**Spiegazione**: Regola la posizione e la dimensione di ogni firma.

##### Passaggio 2: aggiorna il documento
```java
ByteArrayOutputStream outputStream = new ByteArrayOutputStream();
signature2.update(outputStream, signaturesToUpdate);
```
**Spiegazione**: Il documento viene aggiornato con le firme del codice QR modificate.

### Elimina la firma del codice QR del documento tramite ID
#### Panoramica
Potrebbe essere necessario eliminare una firma se non è più necessaria o è stata aggiunta per errore. Ecco come rimuoverla utilizzando il suo ID univoco.

##### Passaggio 1: identificare le firme da eliminare
```java
import com.groupdocs.signature.domain.SignatureCollection;
import java.util.Arrays;

SignatureCollection signaturesToDelete = signature2.search(QrCodeSignature.class);
Arrays.stream(signaturesToDelete).forEach(signature -> {
    if (signature.getSignatureId().equals("YOUR_SIGNATURE_ID")) {
        signature.delete();
    }
});
```
**Spiegazione**: Trova ed elimina la firma del codice QR in base al suo ID univoco.

## Conclusione
Questa guida ti ha illustrato come proteggere i documenti utilizzando firme con codice QR in Java con GroupDocs.Signature. Seguendo questi passaggi, puoi garantire che i tuoi documenti siano firmati in modo sicuro e verificarne facilmente l'autenticità.