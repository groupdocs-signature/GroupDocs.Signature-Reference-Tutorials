---
"date": "2025-05-08"
"description": "Erfahren Sie, wie Sie die Dokumentensicherheit durch die Implementierung und Überprüfung von QR-Code-Signaturen in Java mit GroupDocs.Signature verbessern. Folgen Sie dieser Schritt-für-Schritt-Anleitung für einen sicheren Signaturprozess."
"title": "Sichern Sie Ihre Dokumente&#58; Implementieren Sie QR-Code-Signaturen in Java mit GroupDocs.Signature"
"url": "/de/java/qr-code-signatures/qr-code-signatures-java-groupdocs/"
"weight": 1
type: docs
---
# Sichern Sie Ihre Dokumente: Implementieren Sie QR-Code-Signaturen in Java mit GroupDocs.Signature

In der heutigen digitalen Landschaft ist die Sicherheit von Dokumenten wie Verträgen, Rechnungen oder sensiblen persönlichen Daten entscheidend. Ein innovativer Ansatz zur Verbesserung der Dokumentensicherheit und Vereinfachung von Verifizierungsprozessen ist die Verwendung von QR-Code-Signaturen. Dieses Tutorial führt Sie durch die Implementierung und Verifizierung von QR-Code-Signaturen für Ihre Dokumente in Java mit GroupDocs.Signature.

## Was Sie lernen werden
- So unterschreiben Sie Dokumente mit QR-Codes
- Unterschriebene Dokumente mit QR-Codes verifizieren
- Suche nach vorhandenen QR-Code-Signaturen innerhalb eines Dokuments
- Aktualisieren und Löschen von QR-Code-Signaturen aus Ihren Dokumenten

Lassen Sie uns Ihre Umgebung einrichten und loslegen!

### Voraussetzungen
Stellen Sie vor dem Beginn sicher, dass Sie die folgenden Voraussetzungen erfüllen:

#### Erforderliche Bibliotheken und Abhängigkeiten
Sie benötigen GroupDocs.Signature für Java. Sie können es über Maven oder Gradle einbinden oder direkt herunterladen.

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
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

**Direkter Download**
Laden Sie die neueste Version herunter von [GroupDocs.Signature für Java-Versionen](https://releases.groupdocs.com/signature/java/).

#### Anforderungen für die Umgebungseinrichtung
- Stellen Sie sicher, dass Sie Java Development Kit (JDK) 8 oder höher installiert haben.
- Verwenden Sie eine IDE wie IntelliJ IDEA, Eclipse oder NetBeans.

#### Erforderliche Kenntnisse
Grundkenntnisse in Java-Programmierung und Dokumentenverarbeitung sind von Vorteil.

## Einrichten von GroupDocs.Signature für Java
Um GroupDocs.Signature in Ihrem Projekt zu verwenden, führen Sie die folgenden Schritte aus:
1. **Installation**: Wählen Sie je nach Ihrer Konfiguration zwischen Maven, Gradle oder direktem Download.
2. **Lizenzerwerb**:
   - Beginnen Sie mit einer kostenlosen Testversion, die auf der [GroupDocs-Website](https://releases.groupdocs.com/signature/java/).
   - Erwägen Sie den Erwerb einer temporären Lizenz für erweiterte Tests und Entwicklung von [Hier](https://purchase.groupdocs.com/temporary-license/).
3. **Grundlegende Initialisierung**: 
    So initialisieren Sie GroupDocs.Signature:

    ```java
    Signature signature = new Signature("YOUR_DOCUMENT_PATH");
    ```

Dies bereitet Sie auf die Implementierung von QR-Code-Signaturen vor.

## Implementierungshandbuch

### Dokument mit QR-Code-Signatur unterzeichnen
#### Überblick
Beim Signieren eines Dokuments mit einem QR-Code wird ein eindeutiger Code eingebettet, der Ihre digitale Signatur darstellt. Dieser Vorgang sichert das Dokument und ermöglicht später eine einfache Überprüfung seiner Authentizität.

##### Schritt 1: Richten Sie Ihre Signaturoptionen ein
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
**Erläuterung**: `QrCodeSignOptions` ist so konfiguriert, dass ein QR-Code mit spezifischem Text und Ausrichtung erstellt wird. Passen Sie Breite und Höhe nach Bedarf an.

##### Schritt 2: Anpassen des Signatur-Erscheinungsbilds
```java
import java.awt.Color;

signOptions.setForeColor(Color.RED); // QR-Code-Farbe festlegen
com.groupdocs.signature.domain.SignatureFont signatureFont = new com.groupdocs.signature.domain.SignatureFont();
signatureFont.setSize(12);
signatureFont.setFamilyName("Comic Sans MS");
signOptions.setFont(signatureFont);
```
**Erläuterung**: Durch Anpassen der Schriftart und Farbe wird die visuelle Identifizierung verbessert.

##### Schritt 3: Unterschreiben Sie das Dokument
```java
import java.util.ArrayList;
import java.util.List;

List<String> signatureIds = new ArrayList<>();
List<com.groupdocs.signature.domain.BaseSignature> signedSignatures = signature.sign("YOUR_OUTPUT_PATH", signOptions).getSucceeded();

for (com.groupdocs.signature.domain.BaseSignature temp : signedSignatures) {
    signatureIds.add(temp.getSignatureId());
}
```
**Erläuterung**: In diesem Schritt wird das Dokument signiert und die Signatur-IDs zur späteren Bezugnahme gespeichert.

### Dokument mit QR-Code-Signatur verifizieren
#### Überblick
Durch die Verifizierung wird sichergestellt, dass ein Dokument ordnungsgemäß signiert wurde. So können Sie eine QR-Code-Signatur in einem Dokument verifizieren.

##### Schritt 1: Verifizierungsoptionen einrichten
```java
import com.groupdocs.signature.Signature;
import com.groupdocs.signature.options.verify.QrCodeVerifyOptions;

Signature signature2 = new Signature("YOUR_OUTPUT_PATH");
QrCodeVerifyOptions verifyOptions = new QrCodeVerifyOptions();

verifyOptions.setEncodeType(QrCodeTypes.QR);
verifyOptions.setText("John Smith"); // Zu bestätigender Text
verifyOptions.setAllPages(false); 
verifyOptions.setPageNumber(1);
```
**Erläuterung**Die Überprüfungsoptionen geben an, nach welchem QR-Code-Typ und Text gesucht werden soll, um sicherzustellen, dass die Signatur Ihren Erwartungen entspricht.

##### Schritt 2: Überprüfung durchführen
```java
boolean isValid = signature2.verify(verifyOptions).isValid();
System.out.println("Is Signature Valid? " + isValid);
```
**Erläuterung**: Hiermit wird geprüft, ob das Dokument einen gültigen QR-Code enthält, der Ihren Kriterien entspricht.

### Dokument nach QR-Code-Signatur durchsuchen
#### Überblick
Manchmal ist es notwendig, vorhandene Signaturen in einem Dokument zu finden. So können Sie mit GroupDocs.Signature danach suchen.

##### Schritt 1: Suchoptionen konfigurieren
```java
import com.groupdocs.signature.domain.signatures.QrCodeSignature;
import com.groupdocs.signature.options.search.QrCodeSearchOptions;

Signature signature2 = new Signature("YOUR_OUTPUT_PATH");
QrCodeSearchOptions searchOptions = new QrCodeSearchOptions();
searchOptions.setAllPages(true);
```
**Erläuterung**: Dadurch wird das Tool so eingerichtet, dass alle Seiten nach QR-Code-Signaturen gescannt werden.

##### Schritt 2: Suche ausführen
```java
List<QrCodeSignature> signatures = signature2.search(QrCodeSignature.class, searchOptions);

for (QrCodeSignature qrSignature : signatures) {
    System.out.println("Found Signature ID: " + qrSignature.getSignatureId());
}
```
**Erläuterung**: Dadurch werden alle im Dokument gefundenen QR-Code-Signaturen abgerufen.

### QR-Code-Signatur des Dokuments aktualisieren
#### Überblick
Beim Aktualisieren einer Signatur werden ihre Eigenschaften wie Position oder Größe geändert. So geht's:

##### Schritt 1: Signaturen für die Aktualisierung vorbereiten
```java
import com.groupdocs.signature.domain.signatures.QrCodeSignature;
import java.io.ByteArrayOutputStream;

Signature signature2 = new Signature("YOUR_OUTPUT_PATH");
List<QrCodeSignature> signaturesToUpdate = new ArrayList<>();

// Angenommen, 'Signaturen' ist eine Liste von QrCodeSignature-Objekten, die durch die Suche erhalten wurden
for (QrCodeSignature qrSignature : signatures) {
    qrSignature.setLeft(qrSignature.getLeft() + 100);
    qrSignature.setTop(qrSignature.getTop() + 100);
    qrSignature.setWidth(200);
    qrSignature.setHeight(50);
    signaturesToUpdate.add(qrSignature);
}
```
**Erläuterung**: Dadurch werden die Position und Größe jeder Signatur angepasst.

##### Schritt 2: Aktualisieren Sie das Dokument
```java
ByteArrayOutputStream outputStream = new ByteArrayOutputStream();
signature2.update(outputStream, signaturesToUpdate);
```
**Erläuterung**: Das Dokument wird mit den geänderten QR-Code-Signaturen aktualisiert.

### Dokument löschen QR-Code Signatur per ID
#### Überblick
Das Löschen einer Signatur kann erforderlich sein, wenn sie nicht mehr benötigt wird oder irrtümlich hinzugefügt wurde. So entfernen Sie sie mithilfe ihrer eindeutigen ID.

##### Schritt 1: Zu löschende Signaturen identifizieren
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
**Erläuterung**: Dadurch wird die QR-Code-Signatur anhand ihrer eindeutigen ID gesucht und gelöscht.

## Abschluss
Diese Anleitung führt Sie durch die Sicherung von Dokumenten mithilfe von QR-Code-Signaturen in Java mit GroupDocs.Signature. Mit diesen Schritten können Sie sicherstellen, dass Ihre Dokumente sicher signiert sind und ihre Authentizität einfach überprüfen.