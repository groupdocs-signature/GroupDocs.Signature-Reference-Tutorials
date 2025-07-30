---
"date": "2025-05-08"
"description": "Aprenda a mejorar la seguridad de sus documentos implementando y verificando firmas de código QR en Java con GroupDocs.Signature. Siga esta guía paso a paso para un proceso de firma seguro."
"title": "Proteja sus documentos&#58; Implemente firmas de código QR en Java con GroupDocs.Signature"
"url": "/es/java/qr-code-signatures/qr-code-signatures-java-groupdocs/"
"weight": 1
---

# Proteja sus documentos: Implemente firmas de código QR en Java con GroupDocs.Signature

En el panorama digital actual, garantizar la seguridad de documentos como contratos, facturas o información personal confidencial es crucial. Un enfoque innovador para mejorar la seguridad de los documentos y simplificar los procesos de verificación es el uso de firmas de código QR. Este tutorial le guiará en la implementación y verificación de firmas de código QR para sus documentos en Java con GroupDocs.Signature.

## Lo que aprenderás
- Cómo firmar documentos usando códigos QR
- Verificación de documentos firmados con códigos QR
- Búsqueda de firmas de código QR existentes dentro de un documento
- Actualización y eliminación de firmas de código QR de sus documentos

¡Configuremos tu entorno y comencemos!

### Prerrequisitos
Antes de comenzar, asegúrese de tener los siguientes requisitos previos:

#### Bibliotecas y dependencias requeridas
Necesitarás GroupDocs.Signature para Java. Puedes incluirlo mediante Maven o Gradle, o descargarlo directamente.

**Experto**
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

**Descarga directa**
Descargue la última versión desde [Versiones de GroupDocs.Signature para Java](https://releases.groupdocs.com/signature/java/).

#### Requisitos de configuración del entorno
- Asegúrese de tener instalado Java Development Kit (JDK) 8 o superior.
- Utilice un IDE como IntelliJ IDEA, Eclipse o NetBeans.

#### Requisitos previos de conocimiento
Es beneficioso tener conocimientos básicos de programación Java y procesamiento de documentos.

## Configuración de GroupDocs.Signature para Java
Para utilizar GroupDocs.Signature en su proyecto, siga estos pasos:
1. **Instalación**:Elija entre Maven, Gradle o descarga directa según su configuración.
2. **Adquisición de licencias**:
   - Comience con una prueba gratuita disponible en [Sitio web de GroupDocs](https://releases.groupdocs.com/signature/java/).
   - Considere obtener una licencia temporal para realizar pruebas y desarrollos extendidos de [aquí](https://purchase.groupdocs.com/temporary-license/).
3. **Inicialización básica**: 
    A continuación se explica cómo inicializar GroupDocs.Signature:

    ```java
    Signature signature = new Signature("YOUR_DOCUMENT_PATH");
    ```

Esto lo prepara para implementar firmas de código QR.

## Guía de implementación

### Firmar documento con firma de código QR
#### Descripción general
Firmar un documento con un código QR implica insertar un código único que representa su firma digital. Este proceso protege el documento y facilita la verificación posterior de su autenticidad.

##### Paso 1: Configure sus opciones de firma
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
**Explicación**: `QrCodeSignOptions` Está configurado para crear un código QR con texto y alineación específicos. Ajuste el ancho y la altura según sea necesario.

##### Paso 2: Personalizar la apariencia de la firma
```java
import java.awt.Color;

signOptions.setForeColor(Color.RED); // Establecer el color del código QR
com.groupdocs.signature.domain.SignatureFont signatureFont = new com.groupdocs.signature.domain.SignatureFont();
signatureFont.setSize(12);
signatureFont.setFamilyName("Comic Sans MS");
signOptions.setFont(signatureFont);
```
**Explicación**:Personalizar la fuente y el color mejora la identificación visual.

##### Paso 3: Firmar el documento
```java
import java.util.ArrayList;
import java.util.List;

List<String> signatureIds = new ArrayList<>();
List<com.groupdocs.signature.domain.BaseSignature> signedSignatures = signature.sign("YOUR_OUTPUT_PATH", signOptions).getSucceeded();

for (com.groupdocs.signature.domain.BaseSignature temp : signedSignatures) {
    signatureIds.add(temp.getSignatureId());
}
```
**Explicación**:Este paso firma el documento y almacena los ID de firma para referencia futura.

### Verificar documento con firma de código QR
#### Descripción general
La verificación garantiza que un documento se haya firmado legítimamente. Aquí te explicamos cómo verificar una firma con código QR en un documento.

##### Paso 1: Configurar las opciones de verificación
```java
import com.groupdocs.signature.Signature;
import com.groupdocs.signature.options.verify.QrCodeVerifyOptions;

Signature signature2 = new Signature("YOUR_OUTPUT_PATH");
QrCodeVerifyOptions verifyOptions = new QrCodeVerifyOptions();

verifyOptions.setEncodeType(QrCodeTypes.QR);
verifyOptions.setText("John Smith"); // Texto para verificar
verifyOptions.setAllPages(false); 
verifyOptions.setPageNumber(1);
```
**Explicación**:Las opciones de verificación especifican qué tipo de código QR y texto buscar, garantizando que la firma coincida con sus expectativas.

##### Paso 2: Realizar la verificación
```java
boolean isValid = signature2.verify(verifyOptions).isValid();
System.out.println("Is Signature Valid? " + isValid);
```
**Explicación**:Esto verifica si el documento contiene un código QR válido que coincida con sus criterios.

### Buscar documento para la firma del código QR
#### Descripción general
A veces es necesario localizar firmas existentes en un documento. Aquí te explicamos cómo buscarlas con GroupDocs.Signature.

##### Paso 1: Configurar las opciones de búsqueda
```java
import com.groupdocs.signature.domain.signatures.QrCodeSignature;
import com.groupdocs.signature.options.search.QrCodeSearchOptions;

Signature signature2 = new Signature("YOUR_OUTPUT_PATH");
QrCodeSearchOptions searchOptions = new QrCodeSearchOptions();
searchOptions.setAllPages(true);
```
**Explicación**:Esto configura la herramienta para escanear todas las páginas en busca de firmas de código QR.

##### Paso 2: Ejecutar búsqueda
```java
List<QrCodeSignature> signatures = signature2.search(QrCodeSignature.class, searchOptions);

for (QrCodeSignature qrSignature : signatures) {
    System.out.println("Found Signature ID: " + qrSignature.getSignatureId());
}
```
**Explicación**:Esto recupera todas las firmas de código QR encontradas en el documento.

### Actualizar la firma del código QR del documento
#### Descripción general
Actualizar una firma implica cambiar sus propiedades, como la posición o el tamaño. A continuación, se explica cómo hacerlo:

##### Paso 1: Preparar las firmas para la actualización
```java
import com.groupdocs.signature.domain.signatures.QrCodeSignature;
import java.io.ByteArrayOutputStream;

Signature signature2 = new Signature("YOUR_OUTPUT_PATH");
List<QrCodeSignature> signaturesToUpdate = new ArrayList<>();

// Suponiendo que 'firmas' es una lista de objetos QrCodeSignature obtenidos a partir de la búsqueda
for (QrCodeSignature qrSignature : signatures) {
    qrSignature.setLeft(qrSignature.getLeft() + 100);
    qrSignature.setTop(qrSignature.getTop() + 100);
    qrSignature.setWidth(200);
    qrSignature.setHeight(50);
    signaturesToUpdate.add(qrSignature);
}
```
**Explicación**:Esto ajusta la posición y el tamaño de cada firma.

##### Paso 2: Actualizar el documento
```java
ByteArrayOutputStream outputStream = new ByteArrayOutputStream();
signature2.update(outputStream, signaturesToUpdate);
```
**Explicación**:El documento se actualiza con las firmas de código QR modificadas.

### Eliminar la firma del código QR del documento por ID
#### Descripción general
Puede ser necesario eliminar una firma si ya no es necesaria o se agregó por error. Aquí te explicamos cómo eliminarla usando su ID único.

##### Paso 1: Identificar las firmas que se eliminarán
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
**Explicación**:Esto busca y elimina la firma del código QR por su ID único.

## Conclusión
Esta guía le ha guiado a través de la protección de documentos mediante firmas de código QR en Java con GroupDocs.Signature. Siguiendo estos pasos, podrá garantizar la firma segura de sus documentos y verificar su autenticidad fácilmente.