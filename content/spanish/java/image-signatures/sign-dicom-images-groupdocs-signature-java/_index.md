---
"date": "2025-05-08"
"description": "Aprenda a firmar imágenes DICOM de forma segura con GroupDocs.Signature para Java. Mejore la seguridad de sus documentos integrando códigos QR y metadatos."
"title": "Firmar imágenes DICOM con códigos QR y metadatos usando GroupDocs.Signature para Java"
"url": "/es/java/image-signatures/sign-dicom-images-groupdocs-signature-java/"
"weight": 1
---

# Cómo firmar imágenes DICOM con códigos QR y metadatos usando GroupDocs.Signature para Java

## Introducción

En el cambiante panorama de la atención médica digital, la gestión segura de los datos de los pacientes es fundamental. Este tutorial le guía en la implementación de una solución robusta con GroupDocs.Signature para Java para firmar imágenes DICOM (Imagen Digital y Comunicaciones en Medicina) con códigos QR y metadatos. Estas funciones garantizan la autenticidad, mejoran la trazabilidad y mantienen el cumplimiento normativo al integrar información vital directamente en las imágenes médicas.

### Lo que aprenderás:
- Cómo integrar GroupDocs.Signature para Java en su proyecto.
- El proceso de firmar imágenes DICOM con códigos QR.
- Agregar metadatos XMP para mejorar la seguridad de los documentos.
- Recuperación, verificación y búsqueda de firmas dentro de archivos DICOM.
- Generación de vistas previas de imágenes DICOM firmadas.

¡Comencemos! Antes de empezar, asegurémonos de que tengas todo lo necesario para seguir el tutorial sin problemas.

## Prerrequisitos

Para implementar las funciones de GroupDocs.Signature de manera efectiva, asegúrese de cumplir los siguientes requisitos previos:

### Bibliotecas y dependencias requeridas
- **GroupDocs.Signature para Java**Necesitará la versión 23.12 o posterior de esta biblioteca.

### Requisitos de configuración del entorno
- **Kit de desarrollo de Java (JDK)**:Asegúrese de que JDK esté instalado en su sistema.
- **IDE**:Utilice un entorno de desarrollo integrado como IntelliJ IDEA o Eclipse.

### Requisitos previos de conocimiento
Una comprensión básica de:
- Programación Java y principios orientados a objetos.
- Herramientas de compilación Maven o Gradle para la gestión de dependencias.

## Configuración de GroupDocs.Signature para Java

Para empezar a usar GroupDocs.Signature, debes añadirlo como dependencia a tu proyecto. Puedes hacerlo con diferentes herramientas de compilación a continuación:

### Experto
Añade el siguiente fragmento a tu `pom.xml` archivo:
```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

### Gradle
Incluye esto en tu `build.gradle` archivo:
```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

### Descarga directa
Alternativamente, puede descargar la última versión desde [Versiones de GroupDocs.Signature para Java](https://releases.groupdocs.com/signature/java/).

#### Pasos para la adquisición de la licencia
1. **Prueba gratuita**Pruebe las funciones con una prueba gratuita por tiempo limitado.
2. **Licencia temporal**:Obtenga una licencia temporal para explorar todas las capacidades.
3. **Compra**:Compre una suscripción si necesita acceso a largo plazo.

#### Inicialización y configuración básicas

Para inicializar GroupDocs.Signature, cree una instancia de `Signature` clase:
```java
import com.groupdocs.signature.Signature;

// Inicialice el objeto de firma con la ruta a su archivo DICOM
Signature signature = new Signature(filePath);
```

## Guía de implementación

### Firmar una imagen DICOM con código QR y metadatos

#### Descripción general
Esta función le permite firmar imágenes DICOM con un código QR y agregar metadatos XMP, mejorando la seguridad del documento.

#### Paso 1: Configurar las opciones de señalización del código QR
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
Aquí, configuramos la apariencia y la posición del código QR en la imagen DICOM.

#### Paso 2: Agregar metadatos XMP
```java
import com.groupdocs.signature.options.saveoptions.imagessaveoptions.DicomSaveOptions;
import com.groupdocs.signature.options.saveoptions.imagessaveoptions.DicomXmpEntry;
import com.groupdocs.signature.options.saveoptions.imagessaveoptions.DicomXmpType;

DicomSaveOptions dicomSaveOptions = new DicomSaveOptions();
List<DicomXmpEntry> xmpEntries = new ArrayList<>();
xmpEntries.add(new DicomXmpEntry(DicomXmpType.PatientName, "Patient #4"));
dicomSaveOptions.setXmpEntries(xmpEntries);
```
Este fragmento agrega metadatos al archivo DICOM e incorpora información adicional del paciente.

#### Paso 3: Firmar el documento
```java
String outputFilePath = YOUR_OUTPUT_DIRECTORY + "/SignDicomImageAdvanced/" + fileName;
signature.sign(outputFilePath, options, dicomSaveOptions);
```
El `sign` El método escribe el código QR y los metadatos en su archivo DICOM y lo guarda en la ubicación especificada.

### Recuperación de información de imagen DICOM firmada

#### Descripción general
Extraiga metadatos XMP de una imagen DICOM firmada para fines de verificación o auditoría.
```java
import com.groupdocs.signature.domain.IDocumentInfo;
import com.groupdocs.signature.domain.signatures.MetadataSignature;

IDocumentInfo documentInfo = signature.getDocumentInfo();
for (MetadataSignature item : documentInfo.getMetadataSignatures()) {
    System.out.println(item.toString());
}
```
Este código recupera e imprime todas las firmas de metadatos asociadas con el archivo DICOM.

### Verificación de DICOM firmado

#### Descripción general
Verifique que haya una firma de código QR en la imagen DICOM firmada para confirmar su autenticidad.
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
Este paso de verificación garantiza que el código QR coincida con los criterios esperados, confirmando la integridad del documento.

### Búsqueda de firmas en DICOM firmado

#### Descripción general
Localice todas las firmas de código QR dentro de una imagen DICOM firmada para revisarlas o auditarlas.
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
Esta función es útil para escanear todas las firmas de código QR dentro del documento, proporcionando una visibilidad integral.

### Generación de una vista previa de DICOM firmado

#### Descripción general
Cree vistas previas de cada página de una imagen DICOM firmada, lo que permite una inspección visual rápida sin abrir el archivo completo.
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
Este fragmento genera vistas previas de imágenes para cada página, lo que puede resultar útil para una verificación rápida o para compartir.

## Aplicaciones prácticas

GroupDocs.Signature para Java ofrece varias aplicaciones del mundo real:
- **Imágenes médicas**:Firme y gestione de forma segura imágenes DICOM de pacientes con códigos QR y metadatos.
- **Gestión de documentos legales**: Mejorar la autenticidad y el cumplimiento de los documentos en los procedimientos legales.
- **Servicios financieros**:Implementar firmas electrónicas seguras en documentos financieros sensibles.