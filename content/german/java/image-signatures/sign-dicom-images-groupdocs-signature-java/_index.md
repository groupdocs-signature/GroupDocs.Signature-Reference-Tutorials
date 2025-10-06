---
"date": "2025-05-08"
"description": "Erfahren Sie, wie Sie DICOM-Bilder mit GroupDocs.Signature für Java sicher signieren. Verbessern Sie die Dokumentensicherheit durch die Einbettung von QR-Codes und Metadaten."
"title": "Signieren Sie DICOM-Bilder mit QR-Codes und Metadaten mithilfe von GroupDocs.Signature für Java"
"url": "/de/java/image-signatures/sign-dicom-images-groupdocs-signature-java/"
"weight": 1
type: docs
---
# So signieren Sie DICOM-Bilder mit QR-Codes und Metadaten mithilfe von GroupDocs.Signature für Java

## Einführung

In der sich schnell entwickelnden digitalen Gesundheitslandschaft ist die sichere Verwaltung von Patientendaten von größter Bedeutung. Dieses Tutorial führt Sie durch die Implementierung einer robusten Lösung mit GroupDocs.Signature für Java, um DICOM-Bilder (Digital Imaging and Communications in Medicine) mit QR-Codes und Metadaten zu signieren. Diese Funktionen gewährleisten Authentizität, verbessern die Rückverfolgbarkeit und gewährleisten die Compliance durch die Einbettung wichtiger Informationen direkt in medizinische Bilder.

### Was Sie lernen werden:
- So integrieren Sie GroupDocs.Signature für Java in Ihr Projekt.
- Der Vorgang des Signierens von DICOM-Bildern mit QR-Codes.
- Hinzufügen von XMP-Metadaten zur Verbesserung der Dokumentsicherheit.
- Abrufen, Überprüfen und Suchen von Signaturen in DICOM-Dateien.
- Erstellen einer Vorschau signierter DICOM-Bilder.

Lassen Sie uns eintauchen! Bevor wir beginnen, stellen wir sicher, dass Sie alles haben, was Sie brauchen, um nahtlos mitzumachen.

## Voraussetzungen

Um die GroupDocs.Signature-Funktionen effektiv zu implementieren, stellen Sie sicher, dass Sie die folgenden Voraussetzungen erfüllen:

### Erforderliche Bibliotheken und Abhängigkeiten
- **GroupDocs.Signature für Java**: Sie benötigen Version 23.12 oder höher dieser Bibliothek.

### Anforderungen für die Umgebungseinrichtung
- **Java Development Kit (JDK)**: Stellen Sie sicher, dass JDK auf Ihrem System installiert ist.
- **IDE**: Verwenden Sie eine integrierte Entwicklungsumgebung wie IntelliJ IDEA oder Eclipse.

### Erforderliche Kenntnisse
Ein grundlegendes Verständnis von:
- Java-Programmierung und objektorientierte Prinzipien.
- Maven- oder Gradle-Build-Tools für die Abhängigkeitsverwaltung.

## Einrichten von GroupDocs.Signature für Java

Um mit GroupDocs.Signature zu beginnen, müssen Sie es als Abhängigkeit in Ihr Projekt einfügen. So können Sie dies mit verschiedenen Build-Tools tun:

### Maven
Fügen Sie den folgenden Ausschnitt zu Ihrem `pom.xml` Datei:
```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

### Gradle
Nehmen Sie dies in Ihre `build.gradle` Datei:
```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

### Direkter Download
Alternativ können Sie die neueste Version herunterladen von [GroupDocs.Signature für Java-Versionen](https://releases.groupdocs.com/signature/java/).

#### Schritte zum Lizenzerwerb
1. **Kostenlose Testversion**: Testen Sie die Funktionen mit einer zeitlich begrenzten kostenlosen Testversion.
2. **Temporäre Lizenz**Erwerben Sie eine temporäre Lizenz, um alle Funktionen zu erkunden.
3. **Kaufen**: Kaufen Sie ein Abonnement, wenn Sie langfristigen Zugriff benötigen.

#### Grundlegende Initialisierung und Einrichtung

Um GroupDocs.Signature zu initialisieren, erstellen Sie eine Instanz des `Signature` Klasse:
```java
import com.groupdocs.signature.Signature;

// Initialisieren Sie das Signaturobjekt mit dem Pfad zu Ihrer DICOM-Datei
Signature signature = new Signature(filePath);
```

## Implementierungshandbuch

### Signieren eines DICOM-Bildes mit QR-Code und Metadaten

#### Überblick
Mit dieser Funktion können Sie DICOM-Bilder mit einem QR-Code signieren und XMP-Metadaten hinzufügen, wodurch die Dokumentensicherheit verbessert wird.

#### Schritt 1: QR-Code-Signaturoptionen einrichten
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
Hier konfigurieren wir das Erscheinungsbild und die Position des QR-Codes auf dem DICOM-Bild.

#### Schritt 2: XMP-Metadaten hinzufügen
```java
import com.groupdocs.signature.options.saveoptions.imagessaveoptions.DicomSaveOptions;
import com.groupdocs.signature.options.saveoptions.imagessaveoptions.DicomXmpEntry;
import com.groupdocs.signature.options.saveoptions.imagessaveoptions.DicomXmpType;

DicomSaveOptions dicomSaveOptions = new DicomSaveOptions();
List<DicomXmpEntry> xmpEntries = new ArrayList<>();
xmpEntries.add(new DicomXmpEntry(DicomXmpType.PatientName, "Patient #4"));
dicomSaveOptions.setXmpEntries(xmpEntries);
```
Dieses Snippet fügt der DICOM-Datei Metadaten hinzu und bettet zusätzliche Patienteninformationen ein.

#### Schritt 3: Unterschreiben Sie das Dokument
```java
String outputFilePath = YOUR_OUTPUT_DIRECTORY + "/SignDicomImageAdvanced/" + fileName;
signature.sign(outputFilePath, options, dicomSaveOptions);
```
Der `sign` Die Methode schreibt den QR-Code und die Metadaten in Ihre DICOM-Datei und speichert sie am angegebenen Speicherort.

### Abrufen signierter DICOM-Bildinformationen

#### Überblick
Extrahieren Sie XMP-Metadaten aus einem signierten DICOM-Bild zu Verifizierungs- oder Prüfzwecken.
```java
import com.groupdocs.signature.domain.IDocumentInfo;
import com.groupdocs.signature.domain.signatures.MetadataSignature;

IDocumentInfo documentInfo = signature.getDocumentInfo();
for (MetadataSignature item : documentInfo.getMetadataSignatures()) {
    System.out.println(item.toString());
}
```
Dieser Code ruft alle mit der DICOM-Datei verknüpften Metadatensignaturen ab und druckt sie.

### Überprüfen signierter DICOM-Dateien

#### Überblick
Überprüfen Sie, ob im signierten DICOM-Bild eine QR-Code-Signatur vorhanden ist, um dessen Authentizität zu bestätigen.
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
Dieser Überprüfungsschritt stellt sicher, dass der QR-Code den erwarteten Kriterien entspricht und bestätigt die Dokumentintegrität.

### Suchen nach Signaturen in signiertem DICOM

#### Überblick
Suchen Sie alle QR-Code-Signaturen in einem signierten DICOM-Bild, um sie zu überprüfen oder zu auditieren.
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
Diese Funktion ist nützlich, um alle QR-Code-Signaturen im Dokument zu scannen und so eine umfassende Sichtbarkeit zu gewährleisten.

### Vorschau des signierten DICOM generieren

#### Überblick
Erstellen Sie Vorschauen für jede Seite eines signierten DICOM-Bildes, um eine schnelle visuelle Überprüfung zu ermöglichen, ohne die gesamte Datei öffnen zu müssen.
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
Dieses Snippet generiert Bildvorschauen für jede Seite, was für eine schnelle Überprüfung oder Freigabe nützlich sein kann.

## Praktische Anwendungen

GroupDocs.Signature für Java bietet mehrere praktische Anwendungen:
- **Medizinische Bildgebung**: Signieren und verwalten Sie DICOM-Bilder von Patienten sicher mit QR-Codes und Metadaten.
- **Verwaltung juristischer Dokumente**: Verbessern Sie die Authentizität und Compliance von Dokumenten in Gerichtsverfahren.
- **Finanzdienstleistungen**: Implementieren Sie sichere elektronische Signaturen für vertrauliche Finanzdokumente.