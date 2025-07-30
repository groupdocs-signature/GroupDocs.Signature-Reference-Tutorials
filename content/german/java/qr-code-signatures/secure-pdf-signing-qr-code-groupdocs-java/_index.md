---
"date": "2025-05-08"
"description": "Erfahren Sie, wie Sie PDFs mit QR-Code-Verschlüsselung und digitalen Signaturen mit GroupDocs.Signature für Java sichern. Verbessern Sie effektiv die Sicherheit Ihrer Dokumente."
"title": "Implementieren Sie sichere PDF-Signaturen mit QR-Code-Verschlüsselung in Java mithilfe von GroupDocs.Signature"
"url": "/de/java/qr-code-signatures/secure-pdf-signing-qr-code-groupdocs-java/"
"weight": 1
---

# So implementieren Sie sichere PDF-Signaturen mit QR-Code-Verschlüsselung in Java mithilfe von GroupDocs.Signature

Im digitalen Zeitalter ist die Sicherung sensibler Informationen in Dokumenten von größter Bedeutung. Die zunehmende Cyber-Bedrohungslage hat die Datenverschlüsselung zu einem wesentlichen Bestandteil des Dokumentenmanagements gemacht. Dieses Tutorial führt Sie durch die Implementierung sicherer PDF-Signaturen mit QR-Code-Verschlüsselung und GroupDocs.Signature für Java. Am Ende dieses Artikels sind Sie in der Lage, robuste Sicherheitsfunktionen in Ihre Anwendungen zu integrieren.

## Was Sie lernen werden:
- Symmetrische Datenverschlüsselung in Java verstehen
- Erstellen einer benutzerdefinierten Signaturklasse
- Konfigurieren von QR-Code-Signaturen mit benutzerdefinierten Daten und Ausrichtung
- Integration von GroupDocs.Signature für sichere PDF-Signatur

Bereit zum Eintauchen? Dann legen wir los!

## Voraussetzungen
Bevor wir beginnen, stellen Sie sicher, dass Sie über Folgendes verfügen:
- **Java Development Kit (JDK):** Version 8 oder höher.
- **Maven oder Gradle:** Für die Abhängigkeitsverwaltung. Wählen Sie basierend auf Ihrem Projekt-Setup.
- **Kenntnisse in der Java-Programmierung:** Grundlegende Kenntnisse der objektorientierten Programmierung in Java.

## Einrichten von GroupDocs.Signature für Java
Um GroupDocs.Signature zu verwenden, müssen Sie es als Abhängigkeit zu Ihrem Projekt hinzufügen. Diese Bibliothek bietet leistungsstarke Tools zur Verwaltung digitaler Signaturen und Dokumentverschlüsselung.

### Maven-Setup
Fügen Sie die folgende Abhängigkeit zu Ihrem `pom.xml` Datei:
```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

### Gradle-Setup
Für Gradle-Benutzer: Fügen Sie dies in Ihre `build.gradle` Datei:
```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

### Direkter Download
Alternativ können Sie die neueste Version von herunterladen. [GroupDocs.Signature für Java-Versionen](https://releases.groupdocs.com/signature/java/).

### Lizenzerwerb
Sie können GroupDocs.Signature kostenlos testen und dessen Funktionen testen. Für eine längere Nutzung können Sie eine Lizenz erwerben oder eine temporäre Lizenz über die Website beantragen.

## Implementierungshandbuch
Dieses Handbuch ist in Hauptabschnitte unterteilt, die die Datenverschlüsselung, die Erstellung benutzerdefinierter Signaturen und die Konfiguration von QR-Code-Signaturen behandeln.

### Datenverschlüsselung mit symmetrischem Algorithmus
Durch die Verschlüsselung Ihrer Daten wird sichergestellt, dass diese während der Übertragung und Speicherung sicher bleiben. So richten Sie die symmetrische Verschlüsselung mit GroupDocs.Signature ein:

#### Einrichten der symmetrischen Verschlüsselung
1. **Importieren Sie die erforderlichen Pakete:**
   ```java
   import com.groupdocs.signature.domain.extensions.encryption.IDataEncryption;
   import com.groupdocs.signature.domain.extensions.encryption.SymmetricAlgorithmType;
   import com.groupdocs.signature.domain.extensions.encryption.SymmetricEncryption;
   ```
2. **Initialisieren Sie das Verschlüsselungsobjekt:**
   Verwenden Sie einen sicheren Schlüssel und Salt zur Verschlüsselung. Ersetzen `"YOUR_SECURE_KEY"` mit Ihren eigenen Schlüsseln.
   ```java
   String key = "YOUR_SECURE_KEY";
   String salt = "YOUR_SECURE_SALT";

   IDataEncryption encryption = new SymmetricEncryption(
       SymmetricAlgorithmType.Rijndael, 
       key, 
       salt
   );
   ```
   - **SymmetricAlgorithmType.Rijndael:** Dies gibt den Typ des zu verwendenden symmetrischen Algorithmus an.
   - **Schlüssel und Salt:** Stellen Sie sicher, dass diese für Ihre Anwendung eindeutig und sicher sind.

### Benutzerdefinierte Datensignaturklasse
Durch das Erstellen einer benutzerdefinierten Klasse können Sie Signatureigenschaften effektiv verwalten. So geht's:

#### Definieren der `DocumentSignatureData` Klasse
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
- **ID, Autor, Unterschrift:** In diesen Feldern werden die Metadaten der Signatur gespeichert.
- **Datenfaktor:** Enthält einen numerischen Wert, der für die Logik Ihrer Anwendung relevant ist.

### QR-Code-Signaturoptionen
QR-Codes bieten eine kompakte Möglichkeit, Informationen einzubetten. Konfigurieren Sie sie mit benutzerdefinierten Daten und Verschlüsselung:

#### Einrichten von QR-Code-Signaturen
1. **Initialisieren `Signature` Objekt:**
   ```java
   import com.groupdocs.signature.Signature;
   
   Signature signature = new Signature("YOUR_DOCUMENT_DIRECTORY");
   ```
2. **QR-Code-Optionen konfigurieren:**
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
   options.setDataEncryption(encryption); // Verwenden des Verschlüsselungsobjekts
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
   - **Kodierungstyp:** Gibt das QR-Codeformat an.
   - **Ausrichtung und Rand:** Passen Sie an, wie der QR-Code auf dem Dokument angezeigt wird.

### Beispielverwendung
So signieren Sie ein Dokument mit Ihren konfigurierten Optionen:
```java
signature.sign("YOUR_OUTPUT_DIRECTORY/QRCodeEncryptedObject.pdf\