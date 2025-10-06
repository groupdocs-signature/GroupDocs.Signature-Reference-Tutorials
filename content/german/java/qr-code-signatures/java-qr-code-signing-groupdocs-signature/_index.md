---
"date": "2025-05-08"
"description": "Erfahren Sie, wie Sie Java-QR-Code-Signaturen mit GroupDocs.Signature implementieren. Verbessern Sie die Dokumentensicherheit, konfigurieren Sie Signaturoptionen und wenden Sie benutzerdefinierte Verschlüsselung in Ihren Java-Anwendungen an."
"title": "Java QR Code Signing Guide&#58; Sichern Sie Ihre Dokumente mit GroupDocs.Signature"
"url": "/de/java/qr-code-signatures/java-qr-code-signing-groupdocs-signature/"
"weight": 1
type: docs
---
# Implementierung der Java QR-Code-Signierung mit GroupDocs.Signature für Java

## Einführung

Verbessern Sie die Sicherheit Ihrer digitalen Dokumente durch die Einbettung von QR-Codes in Ihre Java-Anwendungen. Mit GroupDocs.Signature für Java gewährleisten Sie die Authentizität und Rückverfolgbarkeit von Dokumenten. Diese Anleitung führt Sie durch die Erstellung benutzerdefinierter Datensignaturen, die Konfiguration von QR-Code-Signaturoptionen und die Sicherung Ihrer Dokumente mit robuster Verschlüsselung.

**Was Sie lernen werden:**
- So erstellen Sie eine benutzerdefinierte Datensignaturklasse mit GroupDocs.Signature
- Konfigurieren von QR-Code-Signaturoptionen in Java-Anwendungen
- Dokumente mit QR-Codes signieren und benutzerdefinierte Verschlüsselung anwenden

Lassen Sie uns die Voraussetzungen näher betrachten und mit der Integration dieser Funktionalität in Ihre Projekte beginnen!

## Voraussetzungen

Bevor wir beginnen, stellen Sie sicher, dass Sie die erforderlichen Bibliotheken und Abhängigkeiten in Ihrer Entwicklungsumgebung eingerichtet haben.

### Erforderliche Bibliotheken und Versionen

Um GroupDocs.Signature für Java zu implementieren, schließen Sie die folgende Abhängigkeit ein:

**Maven**
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

Sie können die neueste Version auch direkt von herunterladen [GroupDocs.Signature für Java-Versionen](https://releases.groupdocs.com/signature/java/).

### Anforderungen für die Umgebungseinrichtung

- Stellen Sie sicher, dass Sie ein funktionierendes Java Development Kit (JDK) installiert haben.
- Richten Sie Ihre integrierte Entwicklungsumgebung (IDE) ein, beispielsweise IntelliJ IDEA oder Eclipse.

### Erforderliche Kenntnisse

- Grundlegende Kenntnisse der Java-Programmierung und objektorientierter Konzepte.
- Vertrautheit mit der Handhabung von Abhängigkeiten mit Maven oder Gradle.

## Einrichten von GroupDocs.Signature für Java

Richten Sie zunächst GroupDocs.Signature in Ihrem Projekt ein, indem Sie die obigen Installationsanweisungen befolgen, um es in Ihre Build-Konfiguration aufzunehmen.

### Schritte zum Lizenzerwerb

GroupDocs bietet verschiedene Lizenzierungsoptionen:
- **Kostenlose Testversion**: Testen Sie alle Funktionen ohne Einschränkungen.
- **Temporäre Lizenz**: Erwerben Sie eine Lizenz zu Evaluierungszwecken.
- **Kaufen**: Erwerben Sie eine Volllizenz für die kommerzielle Nutzung.

Initialisieren Sie GroupDocs.Signature nach dem Herunterladen wie folgt:

```java
import com.groupdocs.signature.Signature;

class InitializeGroupDocs {
    public static void main(String[] args) {
        Signature signature = new Signature("path/to/your/document");
        // Sie können jetzt mit der Verwendung des Signaturobjekts zum Arbeiten mit Dokumenten beginnen.
    }
}
```

## Implementierungshandbuch

Lassen Sie uns den Implementierungsprozess in überschaubare Abschnitte unterteilen und uns auf die wichtigsten Funktionen konzentrieren.

### Benutzerdefinierte Datensignaturklasse

#### Überblick
Erstellen Sie eine benutzerdefinierte Klasse zum Speichern von Signaturdaten wie ID, Autor, Signaturdatum und weiteren Faktoren. So stellen Sie sicher, dass alle erforderlichen Metadaten in Ihren Signaturen enthalten sind.

#### Schrittweise Implementierung

**Definieren der DocumentSignatureData-Klasse**

```java
import com.groupdocs.signature.domain.extensions.serialization.FormatAttribute;
import java.util.Date;
import java.math.BigDecimal;

class DocumentSignatureData {
    @FormatAttribute(propertyName = "SignID")
    public String ID; // Eindeutige Kennung für die Signatur
    
    public String getID() { return ID; }
    public void setID(String value) { ID = value; }
    
    @FormatAttribute(propertyName = "SAuth")
    public final String Author; // Autor des Dokuments
    
    public final String getAuthor() { return Author; }
    public final void setAuthor(String value) { Author = value; }
    
    @FormatAttribute(propertyName = "SDate", propertyFormat = "yyyy-MM-dd")
    public final Date Signed = new Date(); // Datum und Uhrzeit der Unterzeichnung
    
    public final Date getSigned() { return Signed; }
    public final void setSigned(Date value) { Signed = value; }
    
    @FormatAttribute(propertyName = "SDFact", propertyFormat = "N2")
    public final BigDecimal DataFactor = new BigDecimal(0.01); // Zusätzlicher Datenfaktor für die Signatur
    
    public final BigDecimal getDataFactor() { return DataFactor; }
    public final void setDataFactor(BigDecimal value) { DataFactor = value; }
}
```

**Erläuterung:**
- **FormatAttribute**: Kommentiert Eigenschaften, um die Serialisierung anzupassen.
- **Eigenschaften**: Erfassen Sie wichtige Details wie die eindeutige ID, den Namen des Autors, das Datum der Signatur und den Datenfaktor.

### Konfiguration der QR-Code-Zeichenoptionen

#### Überblick
Konfigurieren Sie die QR-Code-Zeichenoptionen, um festzulegen, wie Ihre QR-Codes auf Dokumenten angezeigt werden, einschließlich Größe, Ausrichtung und Auffüllung.

#### Schrittweise Implementierung

**Definieren Sie die QrCodeSignOptionsConfig-Klasse**

```java
import com.groupdocs.signature.domain.enums.HorizontalAlignment;
import com.groupdocs.signature.domain.enums.VerticalAlignment;
import com.groupdocs.signature.domain.qrcodes.QrCodeTypes;
import com.groupdocs.signature.domain.Padding;
import com.groupdocs.signature.options.sign.QrCodeSignOptions;

class QrCodeSignOptionsConfig {
    public static QrCodeSignOptions setupQrCodeSignOptions(DocumentSignatureData documentSignature) {
        QrCodeSignOptions options = new QrCodeSignOptions();
        
        // Serialisieren Sie das benutzerdefinierte Datenobjekt in einen QR-Code
        options.setData(documentSignature);
        
        // QR-Code-Typ angeben
        options.setEncodeType(QrCodeTypes.QR);
        
        // Konfigurieren Sie die Polsterung für die Ausrichtung
        Padding padding = new Padding();
        padding.setRight(10); // Rechte Polsterung in Pixeln
        padding.setBottom(10); // Untere Polsterung in Pixeln
        options.setMargin(padding);
        
        // Größe und Position des QR-Codes festlegen
        options.setHeight(100);
        options.setWidth(100);
        options.setVerticalAlignment(VerticalAlignment.Bottom);
        options.setHorizontalAlignment(HorizontalAlignment.Right);
        
        return options;
    }
}
```

**Erläuterung:**
- **QrCodeSignOptions**: Verwaltet die Anzeige des QR-Codes, einschließlich seiner Größe und Position.
- **Polsterung**Passt die Ausrichtung innerhalb des Dokuments an.

### Dokumentensignierung mit QR-Code und benutzerdefinierter Verschlüsselung

#### Überblick
Kombinieren Sie QR-Codes und benutzerdefinierte Verschlüsselung, um Dokumente sicher zu signieren. Dies gewährleistet Datenintegrität und Vertraulichkeit.

#### Schrittweise Implementierung

**Unterschreiben Sie ein Dokument mit einem QR-Code**

```java
import com.groupdocs.signature.Signature;
import com.groupdocs.signature.domain.extensions.encryption.IDataEncryption;
import com.groupdocs.signature.exception.GroupDocsSignatureException;

import java.util.UUID;

class SignDocumentWithQRCode {
    public static void signDocument(String filePath, String outputFilePath) throws Exception {
        try {
            Signature signature = new Signature(filePath);

            // Benutzerdefinierte XOR-Verschlüsselungsstrategie
            IDataEncryption encryption = new CustomXOREncryption();

            // Konfigurieren des benutzerdefinierten Dokumentsignaturdatenobjekts
            DocumentSignatureData documentSignature = new DocumentSignatureData();
            documentSignature.setID(UUID.randomUUID().toString());
            documentSignature.setAuthor(System.getenv("USERNAME"));
            documentSignature.setSigned(new Date());
            documentSignature.setDataFactor(new BigDecimal("11.22"));

            // QR-Code-Optionen einrichten
            QrCodeSignOptions options = QrCodeSignOptionsConfig.setupQrCodeSignOptions(documentSignature);

            // Verschlüsseln Sie die Daten im QR-Code
            options.setDataEncryption(encryption);

            // Unterschreiben und speichern Sie das Dokument
            signature.sign(outputFilePath, options);
        } catch (Exception e) {
            throw new GroupDocsSignatureException(e.getMessage());
        }
    }
}
```

**Erläuterung:**
- **Benutzerdefinierte XORE-Verschlüsselung**: Implementiert eine benutzerdefinierte Verschlüsselungsstrategie zum Sichern von QR-Code-Daten.
- **UUID**: Generiert eine eindeutige Kennung für jede Signatur.