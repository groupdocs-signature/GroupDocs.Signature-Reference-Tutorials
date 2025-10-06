---
"date": "2025-05-08"
"description": "Scopri come proteggere i PDF utilizzando la crittografia tramite codice QR e le firme digitali con GroupDocs.Signature per Java. Migliora efficacemente la sicurezza dei tuoi documenti."
"title": "Implementare la firma PDF sicura con crittografia del codice QR in Java utilizzando GroupDocs.Signature"
"url": "/it/java/qr-code-signatures/secure-pdf-signing-qr-code-groupdocs-java/"
"weight": 1
type: docs
---
# Come implementare la firma PDF sicura con crittografia del codice QR in Java utilizzando GroupDocs.Signature

Nell'era digitale odierna, proteggere le informazioni sensibili contenute nei documenti è fondamentale. L'aumento delle minacce informatiche ha reso la crittografia dei dati una componente essenziale della gestione dei documenti. Questo tutorial vi guiderà nell'implementazione della firma PDF sicura utilizzando la crittografia tramite codice QR con GroupDocs.Signature per Java. Al termine di questo articolo, sarete in grado di integrare solide funzionalità di sicurezza nelle vostre applicazioni.

## Cosa imparerai:
- Comprensione della crittografia simmetrica dei dati in Java
- Creazione di una classe di firma personalizzata
- Configurazione delle firme QR-code con dati personalizzati e allineamento
- Integrazione di GroupDocs.Signature per la firma sicura dei PDF

Pronti a tuffarcisi? Iniziamo!

## Prerequisiti
Prima di iniziare, assicurati di avere quanto segue:
- **Kit di sviluppo Java (JDK):** Versione 8 o successiva.
- **Maven o Gradle:** Per la gestione delle dipendenze. Scegli in base alla configurazione del tuo progetto.
- **Conoscenza della programmazione Java:** Conoscenza di base della programmazione orientata agli oggetti in Java.

## Impostazione di GroupDocs.Signature per Java
Per iniziare a utilizzare GroupDocs.Signature, è necessario aggiungerlo come dipendenza al progetto. Questa libreria offre potenti strumenti per la gestione delle firme digitali e la crittografia dei documenti.

### Configurazione Maven
Aggiungi la seguente dipendenza al tuo `pom.xml` file:
```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

### Configurazione Gradle
Per gli utenti Gradle, includi questo nel tuo `build.gradle` file:
```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

### Download diretto
In alternativa, scarica l'ultima versione da [GroupDocs.Signature per le versioni Java](https://releases.groupdocs.com/signature/java/).

### Acquisizione della licenza
Puoi iniziare con una prova gratuita di GroupDocs.Signature per valutarne le funzionalità. Per un utilizzo prolungato, valuta l'acquisto di una licenza o la richiesta di una licenza temporanea tramite il sito web.

## Guida all'implementazione
Questa guida è suddivisa in sezioni chiave che riguardano la crittografia dei dati, la creazione di firme personalizzate e la configurazione della firma tramite codice QR.

### Crittografia dei dati con algoritmo simmetrico
La crittografia dei dati garantisce la sicurezza durante la trasmissione e l'archiviazione. Ecco come impostare la crittografia simmetrica utilizzando GroupDocs.Signature:

#### Impostazione della crittografia simmetrica
1. **Importa i pacchetti necessari:**
   ```java
   import com.groupdocs.signature.domain.extensions.encryption.IDataEncryption;
   import com.groupdocs.signature.domain.extensions.encryption.SymmetricAlgorithmType;
   import com.groupdocs.signature.domain.extensions.encryption.SymmetricEncryption;
   ```
2. **Inizializzare l'oggetto di crittografia:**
   Utilizzare una chiave sicura e un sale per la crittografia. Sostituisci `"YOUR_SECURE_KEY"` con le tue chiavi.
   ```java
   String key = "YOUR_SECURE_KEY";
   String salt = "YOUR_SECURE_SALT";

   IDataEncryption encryption = new SymmetricEncryption(
       SymmetricAlgorithmType.Rijndael, 
       key, 
       salt
   );
   ```
   - **Tipo di algoritmo simmetrico.Rijndael:** Specifica il tipo di algoritmo simmetrico da utilizzare.
   - **Chiave e sale:** Assicurati che siano univoci e sicuri per la tua applicazione.

### Classe di firma dati personalizzata
La creazione di una classe personalizzata consente di gestire efficacemente le proprietà della firma. Ecco come:

#### Definire il `DocumentSignatureData` Classe
```java
class DocumentSignatureData {
    private String ID;
    private String Author;
    private Date Signed = new Date();
    private BigDecimal DataFactor = new BigDecimal(0.01);

    public String getID() { return ID; }
    public void setID(String value) { ID = value; }

    public final String getAuthor() { return Author; }
    public final void setAuthor(String value) { Author = value; }

    public final Date getSigned() { return Signed; }
    public final void setSigned(Date value) { Signed = value; }

    public final BigDecimal getDataFactor() { return DataFactor; }
    public final void setDataFactor(BigDecimal value) { DataFactor = value; }
}
```
- **ID, Autore, Firma:** Questi campi memorizzano i metadati della firma.
- **Fattore dati:** Contiene un valore numerico rilevante per la logica della tua applicazione.

### Opzioni di firma tramite codice QR
I codici QR offrono un modo compatto per incorporare informazioni. Configurali con dati personalizzati e crittografia:

#### Impostazione delle firme tramite codice QR
1. **Inizializzare `Signature` Oggetto:**
   ```java
   import com.groupdocs.signature.Signature;
   
   Signature signature = new Signature("YOUR_DOCUMENT_DIRECTORY");
   ```
2. **Configura le opzioni del codice QR:**
   ```java
   import com.groupdocs.signature.domain.qrcodes.QrCodeTypes;
   import com.groupdocs.signature.options.sign.QrCodeSignOptions;
   import java.util.UUID;

   DocumentSignatureData documentSignature = new DocumentSignatureData();
   documentSignature.setID(UUID.randomUUID().toString());
   documentSignature.setAuthor(System.getenv("USERNAME"));
   documentSignature.setDataFactor(new BigDecimal("11.22"));

   QrCodeSignOptions options = new QrCodeSignOptions();
   options.setData(documentSignature);
   options.setEncodeType(QrCodeTypes.QR);
   options.setDataEncryption(encryption); // Utilizzare l'oggetto di crittografia
   options.setHeight(100);
   options.setWidth(100);
   options.setVerticalAlignment(com.groupdocs.signature.domain.enums.VerticalAlignment.Bottom);
   options.setHorizontalAlignment(com.groupdocs.signature.domain.enums.HorizontalAlignment.Right);

   import com.groupdocs.signature.domain.Padding;
   Padding padding = new Padding();
   padding.setRight(10);
   padding.setBottom(10);
   options.setMargin(padding);
   ```
   - **Tipo di codifica:** Specifica il formato del codice QR.
   - **Allineamento e margine:** Personalizza il modo in cui il codice QR appare sul documento.

### Esempio di utilizzo
Per firmare un documento con le opzioni configurate:
```java
signature.sign("YOUR_OUTPUT_DIRECTORY/QRCodeEncryptedObject.pdf\