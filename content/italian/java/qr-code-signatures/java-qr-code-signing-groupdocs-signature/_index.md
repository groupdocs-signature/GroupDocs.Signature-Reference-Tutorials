---
"date": "2025-05-08"
"description": "Scopri come implementare la firma tramite codice QR Java utilizzando GroupDocs.Signature. Migliora la sicurezza dei documenti, configura le opzioni di firma e applica la crittografia personalizzata nelle tue applicazioni Java."
"title": "Guida alla firma del codice QR Java&#58; proteggi i tuoi documenti con GroupDocs.Signature"
"url": "/it/java/qr-code-signatures/java-qr-code-signing-groupdocs-signature/"
"weight": 1
---

# Implementazione della firma del codice QR Java con GroupDocs.Signature per Java

## Introduzione

Migliora la sicurezza dei tuoi documenti digitali integrando i codici QR nelle tue applicazioni Java. Sfruttando GroupDocs.Signature per Java puoi garantire in modo efficace l'autenticità e la tracciabilità dei documenti. Questa guida ti guiderà nella creazione di firme personalizzate, nella configurazione delle opzioni di firma tramite codici QR e nella protezione dei tuoi documenti con una crittografia avanzata.

**Cosa imparerai:**
- Come creare una classe di firma dati personalizzata utilizzando GroupDocs.Signature
- Configurazione delle opzioni di firma del codice QR nelle applicazioni Java
- Firma di documenti con codici QR e applicazione di crittografia personalizzata

Analizziamo i prerequisiti e iniziamo a integrare questa funzionalità nei tuoi progetti!

## Prerequisiti

Prima di iniziare, assicurati di aver configurato le librerie e le dipendenze necessarie nel tuo ambiente di sviluppo.

### Librerie e versioni richieste

Per implementare GroupDocs.Signature per Java, includere la seguente dipendenza:

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
implementation 'com.groupdocs:groupdocs-signation:23.12'
```

Puoi anche scaricare l'ultima versione direttamente da [GroupDocs.Signature per le versioni Java](https://releases.groupdocs.com/signature/java/).

### Requisiti di configurazione dell'ambiente

- Assicurati di aver installato un Java Development Kit (JDK) funzionante.
- Configura il tuo ambiente di sviluppo integrato (IDE), come IntelliJ IDEA o Eclipse.

### Prerequisiti di conoscenza

- Conoscenza di base della programmazione Java e dei concetti orientati agli oggetti.
- Familiarità con la gestione delle dipendenze tramite Maven o Gradle.

## Impostazione di GroupDocs.Signature per Java

Per iniziare, configura GroupDocs.Signature nel tuo progetto seguendo le istruzioni di installazione sopra riportate per includerlo nella configurazione della build.

### Fasi di acquisizione della licenza

GroupDocs offre diverse opzioni di licenza:
- **Prova gratuita**: Prova tutte le funzionalità senza limitazioni.
- **Licenza temporanea**: Ottenere una licenza per scopi di valutazione.
- **Acquistare**: Acquisire una licenza completa per uso commerciale.

Dopo il download, inizializza GroupDocs.Signature in questo modo:

```java
import com.groupdocs.signature.Signature;

class InitializeGroupDocs {
    public static void main(String[] args) {
        Signature signature = new Signature("path/to/your/document");
        // Ora puoi iniziare a utilizzare l'oggetto firma per lavorare con i documenti.
    }
}
```

## Guida all'implementazione

Suddividiamo il processo di implementazione in sezioni gestibili, concentrandoci sulle caratteristiche principali.

### Classe di firma dati personalizzata

#### Panoramica
Crea una classe personalizzata per memorizzare i dati della firma, come ID, autore, data di firma e altri fattori. In questo modo, avrai tutti i metadati necessari incapsulati nelle tue firme.

#### Implementazione passo dopo passo

**Definire la classe DocumentSignatureData**

```java
import com.groupdocs.signature.domain.extensions.serialization.FormatAttribute;
import java.util.Date;
import java.math.BigDecimal;

class DocumentSignatureData {
    @FormatAttribute(propertyName = "SignID")
    public String ID; // Identificatore univoco per la firma
    
    public String getID() { return ID; }
    public void setID(String value) { ID = value; }
    
    @FormatAttribute(propertyName = "SAuth")
    public final String Author; // Autore del documento
    
    public final String getAuthor() { return Author; }
    public final void setAuthor(String value) { Author = value; }
    
    @FormatAttribute(propertyName = "SDate", propertyFormat = "yyyy-MM-dd")
    public final Date Signed = new Date(); // Data e ora della firma
    
    public final Date getSigned() { return Signed; }
    public final void setSigned(Date value) { Signed = value; }
    
    @FormatAttribute(propertyName = "SDFact", propertyFormat = "N2")
    public final BigDecimal DataFactor = new BigDecimal(0.01); // Fattore dati aggiuntivo per la firma
    
    public final BigDecimal getDataFactor() { return DataFactor; }
    public final void setDataFactor(BigDecimal value) { DataFactor = value; }
}
```

**Spiegazione:**
- **Attributo di formato**: Annota le proprietà per personalizzare la serializzazione.
- **Proprietà**: Acquisisci dettagli essenziali come l'ID univoco, il nome dell'autore, la data della firma e il fattore dati.

### Configurazione delle opzioni di firma del codice QR

#### Panoramica
Configura le opzioni di firma del codice QR per definire come appariranno i tuoi codici QR sui documenti, tra cui dimensioni, allineamento e spaziatura.

#### Implementazione passo dopo passo

**Definisci la classe QrCodeSignOptionsConfig**

```java
import com.groupdocs.signature.domain.enums.HorizontalAlignment;
import com.groupdocs.signature.domain.enums.VerticalAlignment;
import com.groupdocs.signature.domain.qrcodes.QrCodeTypes;
import com.groupdocs.signature.domain.Padding;
import com.groupdocs.signature.options.sign.QrCodeSignOptions;

class QrCodeSignOptionsConfig {
    public static QrCodeSignOptions setupQrCodeSignOptions(DocumentSignatureData documentSignature) {
        QrCodeSignOptions options = new QrCodeSignOptions();
        
        // Serializzare l'oggetto dati personalizzato nel codice QR
        options.setData(documentSignature);
        
        // Specificare il tipo di codice QR
        options.setEncodeType(QrCodeTypes.QR);
        
        // Configurare il padding per l'allineamento
        Padding padding = new Padding();
        padding.setRight(10); // Riempimento destro in pixel
        padding.setBottom(10); // Imbottitura inferiore in pixel
        options.setMargin(padding);
        
        // Definisci la dimensione e la posizione del codice QR
        options.setHeight(100);
        options.setWidth(100);
        options.setVerticalAlignment(VerticalAlignment.Bottom);
        options.setHorizontalAlignment(HorizontalAlignment.Right);
        
        return options;
    }
}
```

**Spiegazione:**
- **Opzioni di firma del codice QR**: Gestisce il modo in cui viene visualizzato il codice QR, comprese le sue dimensioni e la sua posizione.
- **Imbottitura**Regola l'allineamento all'interno del documento.

### Firma dei documenti con codice QR e crittografia personalizzata

#### Panoramica
Combina codici QR e crittografia personalizzata per firmare i documenti in modo sicuro. Questo garantisce l'integrità e la riservatezza dei dati.

#### Implementazione passo dopo passo

**Firma un documento con il codice QR**

```java
import com.groupdocs.signature.Signature;
import com.groupdocs.signature.domain.extensions.encryption.IDataEncryption;
import com.groupdocs.signature.exception.GroupDocsSignatureException;

import java.util.UUID;

class SignDocumentWithQRCode {
    public static void signDocument(String filePath, String outputFilePath) throws Exception {
        try {
            Signature signature = new Signature(filePath);

            // Strategia di crittografia XOR personalizzata
            IDataEncryption encryption = new CustomXOREncryption();

            // Configurare l'oggetto dati della firma del documento personalizzato
            DocumentSignatureData documentSignature = new DocumentSignatureData();
            documentSignature.setID(UUID.randomUUID().toString());
            documentSignature.setAuthor(System.getenv("USERNAME"));
            documentSignature.setSigned(new Date());
            documentSignature.setDataFactor(new BigDecimal("11.22"));

            // Imposta le opzioni del codice QR
            QrCodeSignOptions options = QrCodeSignOptionsConfig.setupQrCodeSignOptions(documentSignature);

            // Applica la crittografia ai dati all'interno del codice QR
            options.setDataEncryption(encryption);

            // Firma e salva il documento
            signature.sign(outputFilePath, options);
        } catch (Exception e) {
            throw new GroupDocsSignatureException(e.getMessage());
        }
    }
}
```

**Spiegazione:**
- **Crittografia XORE personalizzata**: Implementa una strategia di crittografia personalizzata per proteggere i dati del codice QR.
- **UUID**: Genera un identificatore univoco per ogni firma.