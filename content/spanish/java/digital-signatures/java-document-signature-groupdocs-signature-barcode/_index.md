---
date: '2026-07-15'
description: Aprende cómo agregar barcode PDF Java usando GroupDocs.Signature – guía
  paso a paso para firmar, verificar, buscar, actualizar y eliminar firmas de barcode
  en documentos Java.
keywords:
- add barcode pdf java
- groupdocs barcode signature
- java document signing
lastmod: '2026-07-15'
linktitle: Guía de Barcode Signature Java
og_description: Aprende cómo agregar barcode PDF Java usando GroupDocs.Signature –
  guía paso a paso para firmar, verificar, buscar, actualizar y eliminar firmas de
  barcode en documentos Java.
og_image_alt: Guide showing how to add barcode PDF Java using GroupDocs.Signature
og_title: Agregar Barcode PDF Java – Firmar y Verificar con GroupDocs
schemas:
- author: GroupDocs
  dateModified: '2026-07-15'
  description: Learn how to add barcode PDF Java using GroupDocs.Signature – step‑by‑step
    guide to sign, verify, search, update and delete barcode signatures in Java documents.
  headline: Add Barcode PDF Java – Sign & Verify with GroupDocs
  type: TechArticle
- description: Learn how to add barcode PDF Java using GroupDocs.Signature – step‑by‑step
    guide to sign, verify, search, update and delete barcode signatures in Java documents.
  name: Add Barcode PDF Java – Sign & Verify with GroupDocs
  steps:
  - name: Case mismatch (e.g., “John Smith” vs. “john smith”).
    text: Case mismatch (e.g., “John Smith” vs. “john smith”).
  - name: Extra whitespace in the encoded text.
    text: Extra whitespace in the encoded text.
  - name: Wrong barcode type specified in the verification options.
    text: Wrong barcode type specified in the verification options.
  - name: Searching the wrong page number.
    text: Searching the wrong page number.
  - name: '**Reuse Signature Instances** – Create a single `Signature` object per
      document and reuse it for multiple operations.'
    text: '**Reuse Signature Instances** – Create a single `Signature` object per
      document and reuse it for multiple operations.'
  - name: '**Search Specific Pages Only** – Limit the page range to where barcodes
      are expected.'
    text: '**Search Specific Pages Only** – Limit the page range to where barcodes
      are expected.'
  - name: '**Choose the Simplest Barcode Type** – Simpler barcodes generate faster;
      only use QR or Data Matrix when you truly need the extra capacity.'
    text: '**Choose the Simplest Barcode Type** – Simpler barcodes generate faster;
      only use QR or Data Matrix when you truly need the extra capacity.'
  - name: '**Never Encode Sensitive Personal Data** – Barcodes are easily readable;
      avoid PII such as SSNs or passwords.'
    text: '**Never Encode Sensitive Personal Data** – Barcodes are easily readable;
      avoid PII such as SSNs or passwords.'
  - name: '**Validate Server‑Side** – Never trust client‑side verification alone;
      always re‑verify on a trusted backend.'
    text: '**Validate Server‑Side** – Never trust client‑side verification alone;
      always re‑verify on a trusted backend.'
  - name: '**Add Timestamps** – Include a timestamp in the barcode payload to prevent
      replay attacks.'
    text: '**Add Timestamps** – Include a timestamp in the barcode payload to prevent
      replay attacks.'
  type: HowTo
- questions:
  - answer: Yes – the library is fully compatible with JDK 8, 11, and 17.
    question: Can I use GroupDocs.Signature with Java 17?
  - answer: When you use Code128 or QR with sufficient size and contrast, the barcode
      remains scannable after printing and scanning.
    question: Does the barcode survive a print‑scan cycle?
  - answer: There is no hard limit; however, for optimal performance keep the total
      count below **200** per document.
    question: How many barcodes can a single document contain?
  - answer: A temporary license removes evaluation watermarks; a full license is mandatory
      for any production deployment.
    question: Is a license required for development builds?
  - answer: Yes – provide the password when creating the `Signature` object; the API
      will unlock the file internally.
    question: Can I sign password‑protected PDFs?
  type: FAQPage
tags:
- barcode signature
- groupdocs
- java
- pdf
- document signing
title: Agregar Barcode PDF Java – Firmar y Verificar con GroupDocs
type: docs
url: /es/java/digital-signatures/java-document-signature-groupdocs-signature-barcode/
weight: 1
---

# Agregar código de barras PDF Java – Firmar y Verificar con GroupDocs

Si necesita una forma rápida y visual de etiquetar documentos para flujos de trabajo internos, agregar un código de barras a un PDF en Java es una solución perfecta. Con **GroupDocs.Signature**, puede incrustar, verificar, buscar, actualizar y eliminar firmas de código de barras sin la sobrecarga de firmas digitales basadas en PKI completas. Este tutorial lo guía paso a paso, desde la configuración del entorno hasta las mejores prácticas listas para producción.

## Respuestas rápidas
- **¿Qué biblioteca agrega códigos de barras a PDFs en Java?** GroupDocs.Signature for Java.  
- **¿Puedo firmar PDF, Word e imágenes?** Sí – la API admite más de 30 formatos.  
- **¿Necesito una licencia para desarrollo?** Una licencia temporal de 30 días es gratuita; se requiere una licencia completa para producción.  
- **¿Cuántas líneas de código se necesitan para firmar un PDF?** Solo dos líneas: crear un objeto `Signature` y llamar a `sign`.  
- **¿La verificación del código de barras distingue mayúsculas y minúsculas?** Sí – el texto debe coincidir exactamente, incluyendo mayúsculas, minúsculas y espacios.

## ¿Qué es add barcode pdf java?
`add barcode pdf java` se refiere al proceso de usar código Java para incrustar un código de barras (como Code128, QR o Data Matrix) en un archivo PDF. Esta técnica proporciona una etiqueta legible por máquina que puede escanearse o verificarse programáticamente, permitiendo un seguimiento rápido de documentos en sistemas internos.

## ¿Por qué usar firmas de código de barras en lugar de firmas digitales completas?
Las firmas de código de barras son **30‑50 % más rápidas** de generar y verificar que las firmas digitales basadas en PKI, y funcionan de manera fiable después de un ciclo de impresión‑escaneo. Además, no requieren gestión de certificados, lo que las hace ideales para flujos de trabajo internos de alto volumen donde la prueba criptográfica no es obligatoria.

## Requisitos previos
- **Java Development Kit (JDK) 8+** – Se recomienda Java 11 o 17 para mejor rendimiento.  
- **IDE** – IntelliJ IDEA o Eclipse (los ejemplos usan sintaxis de IntelliJ).  
- **Herramienta de compilación** – Maven o Gradle para la gestión de dependencias.  

### Agregando GroupDocs.Signature a su proyecto
La forma más fácil de comenzar es agregar la biblioteca a través de su herramienta de compilación. Así es como se hace:

**Usuarios de Maven** – Agregue esto a su `pom.xml`:

```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

**Usuarios de Gradle** – Agregue esto a su `build.gradle`:

```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

**Descarga directa de JAR** – Si prefiere una configuración manual, obtenga el JAR de [GroupDocs.Signature releases](https://releases.groupdocs.com/signature/java/) y agréguelo a su classpath.

### Obtención de su licencia
GroupDocs.Signature no es gratuito para uso en producción, pero tiene opciones flexibles:
- **Prueba gratuita** – Descargue desde la [página de descargas de GroupDocs](https://releases.groupdocs.com/signature/java/) para probar las funciones (se añaden marcas de agua de evaluación).  
- **Licencia temporal** – Obtenga 30 días de acceso completo a través de la [página de licencia temporal de GroupDocs](https://purchase.groupdocs.com/temporary-license/) – perfecta para pruebas de concepto.  
- **Licencia completa** – Para implementaciones en producción, consulte las [opciones de compra de GroupDocs](https://purchase.groupdocs.com/buy).  

**Consejo profesional:** Comience con la licencia temporal para desarrollo; elimina las marcas de agua una vez que cambie a una clave permanente.

### Verificación rápida del entorno
Una vez que haya agregado la dependencia, ejecute una prueba rápida:

```java
import com.groupdocs.signature.Signature;

public class SignatureTest {
    public static void main(String[] args) {
        try {
            Signature signature = new Signature("test.pdf");
            System.out.println("GroupDocs.Signature initialized successfully!");
            signature.dispose();
        } catch (Exception e) {
            System.err.println("Setup issue: " + e.getMessage());
        }
    }
}
```

Si el programa se ejecuta sin errores, su entorno está listo. Si encuentra problemas, verifique la versión del JDK y la versión exacta de la biblioteca que agregó.

## Cuándo usar firmas de código de barras
Las firmas de código de barras destacan en escenarios específicos:
- **Flujos de trabajo internos de documentos** – Rastrear facturas, órdenes de compra o memorandos a través de cadenas de aprobación.  
- **Procesamiento de alto volumen** – Firmar miles de documentos rápidamente; la generación de códigos de barras es hasta **2× más rápida** que la firma digital completa.  
- **Puentes de impresión‑escaneo** – Los códigos de barras sobreviven al ciclo de impresión‑escaneo, lo que los hace ideales para procesos híbridos papel‑digital.  
- **Integración con sistemas heredados** – Los escáneres de códigos de barras existentes pueden leer las etiquetas sin software adicional.  
- **Rastros de auditoría** – Incruste IDs de transacción o marcas de tiempo que los auditores pueden verificar al instante.  

Evite las firmas de código de barras para contratos legales, documentos de alta seguridad o intercambios con socios externos donde se requieran firmas digitales basadas en PKI.

## Configuración de GroupDocs.Signature para Java
### Definición de la clase principal
La clase `Signature` es el punto de entrada para todas las operaciones de firma, verificación, búsqueda, actualización y eliminación en GroupDocs.Signature.

```java
import com.groupdocs.signature.Signature;
```

### Inicialización básica
Cree un objeto `Signature` que apunte al archivo objetivo:

```java
Signature signature = new Signature("path/to/your/document.pdf");
```

**Notas importantes**
- Las rutas pueden ser absolutas o relativas; use `System.getProperty("user.home")` para compatibilidad multiplataforma.  
- GroupDocs admite **más de 30 formatos de entrada y salida**, incluidos PDF, DOCX, XLSX, PPTX y PNG.  
- Siempre libere los recursos con `signature.dispose()` o un bloque try‑with‑resources:

```java
try (Signature signature = new Signature("path/to/your/document.pdf")) {
    // Your signing operations here
} catch (Exception e) {
    System.err.println("Error working with document: " + e.getMessage());
}
```

Ahora está listo para agregar códigos de barras.

## ¿Cómo agregar un código de barras a un PDF en Java?
Cargue el PDF de origen con `new Signature("input.pdf")`, configure un objeto `BarcodeSignature` (p. ej., Code128 con el texto “John Smith”) y llame a `sign` para generar el archivo firmado, todo en tres líneas concisas de código. Este enfoque le permite incrustar una etiqueta legible por máquina mientras mantiene intacto el diseño original del documento, y funciona para cualquier formato compatible, no solo PDFs.

### Implementación paso a paso
#### 1. Definir rutas de archivos
Establezca las ubicaciones para los archivos de origen y salida:

```java
String filePath = "YOUR_DOCUMENT_DIRECTORY/sample.docx";
String outputFilePath = "YOUR_OUTPUT_DIRECTORY/signed_sample.docx";
```

#### 2. Crear el manejador de firma
Inicialice el manejador con el documento de origen:

```java
Signature signature = new Signature(filePath);
```

#### 3. Configurar opciones del código de barras
Un objeto `BarcodeSignature` define las propiedades visuales y de datos del código de barras que se incrustará. Establezca el tipo de código de barras, el texto codificado, la posición, el tamaño, el color y la fuente legible opcional:

```java
BarcodeSignOptions signOptions = new BarcodeSignOptions("John Smith", BarcodeTypes.Code128);
signOptions.setVerticalAlignment(VerticalAlignment.Top);
signOptions.setHorizontalAlignment(HorizontalAlignment.Center);
signOptions.setWidth(100);
signOptions.setHeight(40);
signOptions.setMargin(new java.awt.Rectangle(20, 20, 0, 0));
signOptions.setForeColor(Color.RED);

SignatureFont signatureFont = new SignatureFont();
signatureFont.setSize(12);
signatureFont.setFamilyName("Comic Sans MS");
signOptions.setFont(signatureFont);
```

> **Consejo profesional:** Si la cadena codificada supera los 20 caracteres, aumente el ancho del código de barras para evitar errores de escaneo.

#### 4. Aplicar la firma
Ejecute la operación de firma y genere el archivo de salida:

```java
signature.sign(outputFilePath, signOptions);
```

#### 5. Ejemplo del mundo real
En un sistema de aprobación de facturas podría incrustar el ID de empleado del aprobador y una marca de tiempo:

```java
String invoiceId = "INV-2025-0042";
String approver = "john.smith@company.com";
String timestamp = LocalDateTime.now().toString();

// Combine into barcode data
String barcodeData = invoiceId + "|" + approver + "|" + timestamp;

BarcodeSignOptions signOptions = new BarcodeSignOptions(barcodeData, BarcodeTypes.QR);
signOptions.setVerticalAlignment(VerticalAlignment.Bottom);
signOptions.setHorizontalAlignment(HorizontalAlignment.Right);

signature.sign(outputFilePath, signOptions);
```

El PDF resultante ahora lleva un código de barras escaneable que codifica todos los metadatos de aprobación necesarios.

## ¿Cómo verificar una firma de código de barras en un documento Java?
El método `Signature.verify` verifica un documento en busca de firmas de código de barras coincidentes según las opciones proporcionadas, devolviendo un booleano que indica si el código de barras esperado está presente. La verificación es útil para flujos de trabajo automatizados donde necesita confirmar que un documento ha sido procesado por la parte correcta antes de acciones posteriores.

### Pasos de verificación
#### 1. Cargar el documento firmado

```java
Signature signature = new Signature("YOUR_OUTPUT_DIRECTORY/signed_sample.docx");
```

#### 2. Establecer criterios de verificación
Defina el texto exacto, el formato del código de barras y el número de página que espera:

```java
BarcodeVerifyOptions verifyOptions = new BarcodeVerifyOptions();
verifyOptions.setAllPages(false); // Only check the first page
verifyOptions.setPageNumber(1);
verifyOptions.setEncodeType(BarcodeTypes.Code128);
verifyOptions.setText("John Smith");
```

#### 3. Ejecutar la verificación
Ejecute la comprobación y maneje el resultado:

```java
boolean isValid = signature.verify(verifyOptions) != null;

if (isValid) {
    System.out.println("Document signature verified successfully!");
} else {
    System.out.println("Warning: Signature verification failed!");
}
```

**Patrón común:** Para confirmar simplemente que *cualquier* código de barras de un tipo dado exista, omita el filtro `setText`:

```java
BarcodeVerifyOptions flexibleOptions = new BarcodeVerifyOptions();
flexibleOptions.setAllPages(true);
flexibleOptions.setEncodeType(BarcodeTypes.Code128);
// No setText() call = accept any text with this barcode type

boolean hasAnySignature = signature.verify(flexibleOptions) != null;
```

O verifique solo el formato del código de barras sin preocuparse por el contenido:

```java
BarcodeVerifyOptions formatOnly = new BarcodeVerifyOptions();
formatOnly.setEncodeType(BarcodeTypes.QR);
// Confirms a QR code exists, regardless of content
```

> **Advertencia:** La verificación distingue mayúsculas/minúsculas y espacios; siempre recorte y normalice los datos antes de firmar.

## ¿Cómo buscar firmas de código de barras dentro de un documento?
El método `Signature.search` escanea un documento en busca de firmas de código de barras que coincidan con los `BarcodeSearchOptions` suministrados, devolviendo una colección que incluye la ubicación de cada código de barras, el número de página y el valor codificado. Esta capacidad permite la extracción masiva de metadatos sin abrir cada archivo manualmente.

### Flujo de trabajo de búsqueda
#### 1. Inicializar búsqueda

```java
Signature signature = new Signature("YOUR_OUTPUT_DIRECTORY/signed_sample.docx");
```

#### 2. Configurar parámetros de búsqueda
Especifique el rango de páginas, el tipo de código de barras o filtros de texto:

```java
BarcodeSearchOptions searchOptions = new BarcodeSearchOptions();
searchOptions.setAllPages(true); // Search the entire document
```

Opcionalmente, reduzca la búsqueda para mejorar el rendimiento:

```java
BarcodeSearchOptions narrowSearch = new BarcodeSearchOptions();
narrowSearch.setAllPages(false);
narrowSearch.setPageNumber(1); // Only search page 1
narrowSearch.setEncodeType(BarcodeTypes.Code128); // Only find Code128 barcodes
```

#### 3. Ejecutar búsqueda

```java
java.util.List<BarcodeSignature> signatures = signature.search(BarcodeSignature.class, searchOptions);

System.out.println("Found " + signatures.size() + " barcode signature(s)");

for (BarcodeSignature bcSignature : signatures) {
    System.out.println("Barcode Type: " + bcSignature.getEncodeType().getTypeName());
    System.out.println("Text: " + bcSignature.getText());
    System.out.println("Position: (" + bcSignature.getLeft() + ", " + bcSignature.getTop() + ")");
    System.out.println("Size: " + bcSignature.getWidth() + "x" + bcSignature.getHeight());
    System.out.println("---");
}
```

#### 4. Ejemplo de extracción de datos
Extraiga datos de aprobación de cada código de barras en un lote de facturas:

```java
List<BarcodeSignature> foundSignatures = signature.search(BarcodeSignature.class, searchOptions);

for (BarcodeSignature sig : foundSignatures) {
    String barcodeData = sig.getText();
    
    // Parse your custom format (remember our invoice example?)
    String[] parts = barcodeData.split("\\|");
    if (parts.length == 3) {
        String invoiceId = parts[0];
        String approver = parts[1];
        String timestamp = parts[2];
        
        System.out.println("Invoice " + invoiceId + " approved by " + approver + " at " + timestamp);
    }
}
```

> **Consejo de rendimiento:** Para documentos de más de 100 páginas, siempre limite la búsqueda a las páginas que realmente contienen códigos de barras; esto puede reducir el tiempo de ejecución hasta en **70 %**.

## ¿Cómo actualizar una firma de código de barras existente?
El método `Signature.update` modifica los atributos visuales de una firma de código de barras existente —como posición, tamaño o color— mientras preserva los datos codificados originales. Esto es útil cuando se requieren cambios de diseño después de que el documento ya ha sido firmado.

### Procedimiento de actualización
#### 1. Encontrar firmas para actualizar

```java
Signature signature = new Signature("YOUR_OUTPUT_DIRECTORY/signed_sample.docx");

BarcodeSearchOptions searchOptions = new BarcodeSearchOptions();
searchOptions.setAllPages(true);

List<BarcodeSignature> signatures = signature.search(BarcodeSignature.class, searchOptions);
```

#### 2. Modificar propiedades deseadas

```java
List<BarcodeSignature> signaturesToUpdate = new ArrayList<>();

if (!signatures.isEmpty()) {
    BarcodeSignature bcSignature = signatures.get(0); // Update the first found signature
    
    // Move it 100px right and 100px down
    bcSignature.setLeft(bcSignature.getLeft() + 100);
    bcSignature.setTop(bcSignature.getTop() + 100);
    
    // Make it bigger
    bcSignature.setWidth(200);
    bcSignature.setHeight(50);
    
    signaturesToUpdate.add(bcSignature);
}
```

Puede cambiar varios atributos a la vez:

```java
bcSignature.setLeft(50);
bcSignature.setTop(50);
bcSignature.setWidth(150);
bcSignature.setHeight(45);
// Note: You can't change the encoded text or barcode type with update
// For that, you'd need to delete and re-sign
```

#### 3. Guardar cambios

```java
ByteArrayOutputStream outputStream = new ByteArrayOutputStream();
signature.update(outputStream, signaturesToUpdate);

// If you want to save to a file instead:
// signature.update("path/to/updated_document.docx", signaturesToUpdate);
```

#### 4. Escenario del mundo real
Reposicione todas las firmas para evitar superponerse a un logotipo de empresa recién agregado:

```java
List<BarcodeSignature> allSignatures = signature.search(BarcodeSignature.class, searchOptions);
List<BarcodeSignature> toUpdate = new ArrayList<>();

for (BarcodeSignature sig : allSignatures) {
    // Move all signatures down by 50px to clear space for new logo
    if (sig.getTop() < 100) {
        sig.setTop(sig.getTop() + 50);
        toUpdate.add(sig);
    }
}

if (!toUpdate.isEmpty()) {
    signature.update(outputStream, toUpdate);
    System.out.println("Repositioned " + toUpdate.size() + " signature(s)");
}
```

> **Limitación:** Cambiar el texto codificado requiere eliminar e insertar una nueva firma.

## ¿Cómo eliminar firmas de código de barras de un documento?
El método `Signature.delete` elimina permanentemente las firmas de código de barras seleccionadas de un documento, borrando tanto el elemento visual como sus datos codificados. Use esta operación al limpiar firmas de prueba o cuando un código de barras ya no sea relevante.

### Pasos de eliminación
#### 1. Localizar firmas

```java
Signature signature = new Signature("YOUR_OUTPUT_DIRECTORY/signed_sample.docx");

BarcodeSearchOptions searchOptions = new BarcodeSearchOptions();
searchOptions.setAllPages(true);

List<BarcodeSignature> signatures = signature.search(BarcodeSignature.class, searchOptions);
```

#### 2. Eliminar firmas seleccionadas

```java
List<BarcodeSignature> signaturesToDelete = new ArrayList<>();

// Delete all Code128 signatures (for example)
for (BarcodeSignature sig : signatures) {
    if (sig.getEncodeType().equals(BarcodeTypes.Code128)) {
        signaturesToDelete.add(sig);
    }
}

if (!signaturesToDelete.isEmpty()) {
    boolean result = signature.delete(signaturesToDelete);
    
    if (result) {
        System.out.println("Successfully deleted " + signaturesToDelete.size() + " signature(s)");
    } else {
        System.err.println("Failed to delete signatures");
    }
}
```

#### 3. Ejemplo de eliminación condicional
Eliminar solo los códigos de barras más antiguos que una marca de tiempo específica (asumiendo que la marca de tiempo forma parte del texto codificado):

```java
LocalDateTime cutoffDate = LocalDateTime.now().minusDays(30);
List<BarcodeSignature> outdatedSignatures = new ArrayList<>();

for (BarcodeSignature sig : signatures) {
    try {
        String text = sig.getText();
        // Assuming format like "data|timestamp"
        String[] parts = text.split("\\|");
        if (parts.length > 1) {
            LocalDateTime sigDate = LocalDateTime.parse(parts[1]);
            if (sigDate.isBefore(cutoffDate)) {
                outdatedSignatures.add(sig);
            }
        }
    } catch (Exception e) {
        // Skip signatures that don't match our format
        continue;
    }
}

if (!outdatedSignatures.isEmpty()) {
    signature.delete(outdatedSignatures);
    System.out.println("Removed " + outdatedSignatures.size() + " outdated signature(s)");
}
```

> **Precaución:** La eliminación no se puede deshacer; siempre opere sobre una copia de los archivos de producción durante las pruebas.

#### 4. Patrón de eliminación por lotes
Limpie las firmas de prueba antes de una versión:

```java
// Remove all signatures containing "TEST" in their text
List<BarcodeSignature> testSignatures = signatures.stream()
    .filter(sig -> sig.getText().toUpperCase().contains("TEST"))
    .collect(Collectors.toList());

if (!testSignatures.isEmpty()) {
    signature.delete(testSignatures);
    System.out.println("Cleaned up " + testSignatures.size() + " test signature(s)");
}
```

## Tipos de códigos de barras: Guía práctica
Elegir el código de barras adecuado impacta la fiabilidad del escaneo, la capacidad de datos y la compatibilidad de la impresora.

### Code128 (Elección más común)
- **Cuándo usar:** Datos alfanuméricos, alta densidad, documentos impresos.  
- **Ventajas:** Compacto, funciona con escáneres estándar, se imprime claramente en tamaños pequeños.  
- **Desventajas:** Limitado a ASCII, menos resistente a errores que los códigos 2‑D.  

Ejemplo:

```java
BarcodeSignOptions code128 = new BarcodeSignOptions("INV-2025-042", BarcodeTypes.Code128);
```

### Código QR (Mejor para móviles)
- **Cuándo usar:** Escaneo móvil, grandes cargas de datos (URL, JSON, etc.), documentos que pueden dañarse.  
- **Ventajas:** Hasta 4 000 caracteres, corrección de errores incorporada, amigable para smartphones.  
- **Desventajas:** Mayor huella visual, requiere mayor resolución para tamaños pequeños.  

Ejemplo:

```java
String jsonData = "{\"invoice\":\"INV-042\",\"amount\":1500.00,\"approver\":\"john@company.com\"}";
BarcodeSignOptions qrCode = new BarcodeSignOptions(jsonData, BarcodeTypes.QR);
```

### Code39 (Clásico confiable)
- **Cuándo usar:** Entornos de escáneres heredados, necesidad de texto legible por humanos.  
- **Ventajas:** Amplio soporte heredado, formato simple, no requiere checksum.  
- **Desventajas:** Baja densidad de datos, conjunto de caracteres limitado, ocupa más espacio.

### Data Matrix (Potente y compacto)
- **Cuándo usar:** Espacio extremadamente limitado, marcaje de objetos diminutos, datos de alta densidad.  
- **Ventajas:** Muy compacto, fuerte corrección de errores, funciona en superficies curvas.  
- **Desventajas:** Requiere impresión de alta calidad, soporte de escáner menos común.

#### Comparación rápida
| Tipo de código de barras | Capacidad de datos | Mejor para | Tamaño típico |
|--------------------------|--------------------|------------|---------------|
| Code128                  | ~100 caracteres    | Etiquetado de propósito general | Pequeño |
| QR Code                  | ~4 000 caracteres  | Escaneo móvil, datos ricos | Mediano |
| Code39                   | ~43 caracteres     | Hardware heredado | Grande |
| Data Matrix              | ~3 000 caracteres  | Espacios diminutos, etiquetas industriales | Muy pequeño |

**Recomendación:** Comience con **Code128** para IDs simples. Cambie a **QR** cuando necesite incrustar URL o cargas útiles más grandes. Use **Code39** solo para integraciones heredadas.

## Problemas comunes y soluciones
### Problema: “Código de barras no encontrado durante la verificación”
**Síntomas:** La verificación devuelve `false` aunque el código de barras sea visible.

**Causas típicas**
1. Diferencia de mayúsculas/minúsculas (p. ej., “John Smith” vs. “john smith”).  
2. Espacios en blanco extra en el texto codificado.  
3. Tipo de código de barras incorrecto especificado en las opciones de verificación.  
4. Búsqueda en el número de página incorrecto.

**Solución:** Normalice el texto antes de firmar y verificar, y asegúrese de que `setEncodeType` coincida con el tipo original.

```java
// Always normalize your data
String signatureText = originalText.trim().toLowerCase();

// When signing:
BarcodeSignOptions signOptions = new BarcodeSignOptions(signatureText, BarcodeTypes.Code128);

// When verifying:
BarcodeVerifyOptions verifyOptions = new BarcodeVerifyOptions();
verifyOptions.setText(signatureText); // Use the same normalized text
verifyOptions.setEncodeType(BarcodeTypes.Code128);
```

### Problema: “El código de barras aparece borroso o ilegible”
**Síntomas:** Los códigos de barras impresos no pueden escanearse.

**Causas**
- Dimensiones del código de barras demasiado pequeñas para los datos codificados.  
- Configuraciones de impresora de baja resolución.  
- Contraste insuficiente entre el color del código de barras y el fondo.

**Solución:** Aumente el ancho/alto del código de barras, use colores de alto contraste (negro sobre blanco) y configure la DPI de la impresora a al menos 300 dpi.

```java
// Increase size for longer strings
int dataLength = barcodeText.length();
int minWidth = Math.max(100, dataLength * 10); // 10px per character minimum

BarcodeSignOptions signOptions = new BarcodeSignOptions(barcodeText, BarcodeTypes.Code128);
signOptions.setWidth(minWidth);
signOptions.setHeight(60); // Taller = easier to scan

// Use high-contrast colors
signOptions.setForeColor(Color.BLACK); // Black on white is most reliable
signOptions.setBackColor(Color.WHITE);
```

### Problema: “OutOfMemoryError con documentos grandes”
**Síntomas:** La aplicación se bloquea al procesar PDFs con cientos de páginas.

**Causa:** La biblioteca carga todo el documento en memoria.

**Solución:** Habilite el modo de transmisión y procese las páginas de forma incremental.

```java
// Process pages in batches instead of all at once
BarcodeSearchOptions searchOptions = new BarcodeSearchOptions();
searchOptions.setAllPages(false);

List<BarcodeSignature> allSignatures = new ArrayList<>();

for (int page = 1; page <= totalPages; page++) {
    searchOptions.setPageNumber(page);
    List<BarcodeSignature> pageSignatures = signature.search(BarcodeSignature.class, searchOptions);
    allSignatures.addAll(pageSignatures);
    
    // Process and clear as you go
    if (page % 10 == 0) {
        System.gc(); // Suggest garbage collection every 10 pages
    }
}
```

### Problema: “Posición de la firma inconsistente entre tipos de documento”
**Síntomas:** Los códigos de barras aparecen en diferentes ubicaciones al firmar PDFs vs. documentos Word.

**Causa:** PDF usa un origen inferior‑izquierdo, mientras que Word usa un origen superior‑izquierdo.

**Solución:** Detecte el tipo de documento y aplique la transformación de coordenadas adecuada.

```java
// Use relative positioning instead of absolute
signOptions.setVerticalAlignment(VerticalAlignment.Bottom);
signOptions.setHorizontalAlignment(HorizontalAlignment.Right);

// Then use margins for fine-tuning
Padding margin = new Padding();
margin.setRight(50); // 50px from right edge
margin.setBottom(50); // 50px from bottom
signOptions.setMargin(margin);

// This works consistently across PDF, DOCX, XLSX, etc.
```

### Problema: “Las firmas actualizadas pierden formato”
**Síntomas:** Después de llamar a `update`, el color o la fuente del código de barras cambian inesperadamente.

**Causa:** No todas las propiedades visuales se conservan durante una operación de actualización.

**Solución:** Vuelva a aplicar cualquier configuración visual después de la llamada a `update`.

```java
// When updating, explicitly set all visual properties
bcSignature.setLeft(newLeft);
bcSignature.setTop(newTop);
bcSignature.setWidth(originalWidth); // Don't forget these!
bcSignature.setHeight(originalHeight);
// Note: Color and font can't be updated - you'd need to delete and re-sign
```

## Mejores prácticas para producción
### Optimización del rendimiento
1. **Reutilizar instancias de Signature** – Crear un solo objeto `Signature` por documento y reutilizarlo para múltiples operaciones.

```java
// Bad - Creates new instance each time
public void processDocument(String path) {
    Signature sig1 = new Signature(path);
    sig1.search(/* ... */);
    
    Signature sig2 = new Signature(path); // Unnecessary reload
    sig2.verify(/* ... */);
}

// Good - Reuse the same instance
public void processDocument(String path) {
    try (Signature signature = new Signature(path)) {
        signature.search(/* ... */);
        signature.verify(/* ... */);
        signature.update(/* ... */);
    }
}
```

2. **Buscar solo páginas específicas** – Limite el rango de páginas a donde se esperan los códigos de barras.

```java
// Slow for 100+ page documents
BarcodeSearchOptions slowSearch = new BarcodeSearchOptions();
slowSearch.setAllPages(true);

// Fast - only check where signatures actually are
BarcodeSearchOptions fastSearch = new BarcodeSearchOptions();
fastSearch.setAllPages(false);
fastSearch.setPageNumber(1); // Only check cover page
```

3. **Elegir el tipo de código de barras más simple** – Los códigos de barras más simples se generan más rápido; use QR o Data Matrix solo cuando realmente necesite la capacidad extra.

```java
// Overkill for simple IDs
BarcodeSignOptions slow = new BarcodeSignOptions("12345", BarcodeTypes.QR);

// Faster and more appropriate
BarcodeSignOptions fast = new BarcodeSignOptions("12345", BarcodeTypes.Code128);
```

### Consideraciones de seguridad
1. **Nunca codifique datos personales sensibles** – Los códigos de barras son fácilmente legibles; evite PII como SSN o contraseñas.  

```java
// Bad - exposes sensitive data
String barcodeData = "SSN:123-45-6789|Password:hunter2";

// Good - use reference IDs
String barcodeData = "USER-REF-7721X"; // Look up sensitive data server-side
```

2. **Validar del lado del servidor** – Nunca confíe solo en la verificación del lado del cliente; siempre vuelva a verificar en un backend confiable.  

```java
// Client scans barcode and extracts "APPROVED-BY-ADMIN"
// Always verify server-side:
public boolean verifyApproval(String documentId, String scannedData) {
    // Load document from secure storage
    Signature signature = new Signature(getSecureDocument(documentId));
    
    BarcodeVerifyOptions verifyOptions = new BarcodeVerifyOptions();
    verifyOptions.setText(scannedData);
    
    boolean isValid = signature.verify(verifyOptions) != null;
    
    // Also check against your database
    boolean isInDatabase = checkApprovalDatabase(documentId, scannedData);
    
    return isValid && isInDatabase;
}
```

3. **Agregar marcas de tiempo** – Incluya una marca de tiempo en la carga útil del código de barras para prevenir ataques de reproducción.  

```java
import java.time.LocalDateTime;
import java.time.temporal.ChronoUnit;

String timestamp = LocalDateTime.now().truncatedTo(ChronoUnit.SECONDS).toString();
String barcodeData = "APPROVAL|" + userId + "|" + timestamp;

// When verifying, check the timestamp isn't too old
public boolean isSignatureRecent(String barcodeData, int maxAgeHours) {
    String[] parts = barcodeData.split("\\|");
    if (parts.length < 3) return false;
    
    LocalDateTime signatureTime = LocalDateTime.parse(parts[2]);
    LocalDateTime now = LocalDateTime.now();
    
    long hoursSince = ChronoUnit.HOURS.between(signatureTime, now);
    return hoursSince <= maxAgeHours;
}
```

### Patrones de manejo de errores
- **Siempre use try‑with‑resources** para asegurar que los objetos `Signature` se liberen.

```java
try (Signature signature = new Signature(documentPath)) {
    // Your operations here
    signature.sign(outputPath, signOptions);
} catch (Exception e) {
    logger.error("Failed to sign document: " + documentPath, e);
    throw new DocumentSigningException("Could not process document", e);
}
```

- **Validar acceso a archivos** antes de intentar firmar.

```java
public void signDocument(String inputPath, String outputPath) {
    File inputFile = new File(inputPath);
    
    if (!inputFile.exists()) {
        throw new IllegalArgumentException("Input file not found: " + inputPath);
    }
    
    if (!inputFile.canRead()) {
        throw new SecurityException("Cannot read input file: " + inputPath);
    }
    
    File outputDir = new File(outputPath).getParentFile();
    if (outputDir != null && !outputDir.exists()) {
        outputDir.mkdirs();
    }
    
    try (Signature signature = new Signature(inputPath)) {
        signature.sign(outputPath, signOptions);
    }
}
```

- **Sincronizar acceso** si varios hilos pueden trabajar en el mismo archivo.

```java
import java.util.concurrent.locks.ReentrantLock;
import java.util.concurrent.ConcurrentHashMap;

public class SignatureManager {
    private final ConcurrentHashMap<String, ReentrantLock> documentLocks = new ConcurrentHashMap<>();
    
    public void signDocument(String documentPath, BarcodeSignOptions options) {
        ReentrantLock lock = documentLocks.computeIfAbsent(documentPath, k -> new ReentrantLock());
        
        lock.lock();
        try (Signature signature = new Signature(documentPath)) {
            signature.sign(documentPath + ".signed", options);
        } finally {
            lock.unlock();
        }
    }
}
```

### Pruebas de su implementación
**Plantilla de prueba unitaria**

```java
import org.junit.jupiter.api.Test;
import org.junit.jupiter.api.io.TempDir;
import static org.junit.jupiter.api.Assertions.*;

public class BarcodeSignatureTest {
    
    @TempDir
    Path tempDir;
    
    @Test
    public void testSignAndVerify() throws Exception {
        // Setup
        String testDoc = "test-document.pdf";
        String outputDoc = tempDir.resolve("signed-test.pdf").toString();
        String testData = "TEST-USER-12345";
        
        // Sign
        try (Signature signature = new Signature(testDoc)) {
            BarcodeSignOptions signOptions = new BarcodeSignOptions(testData, BarcodeTypes.Code128);
            signature.sign(outputDoc, signOptions);
        }
        
        // Verify
        try (Signature signature = new Signature(outputDoc)) {
            BarcodeVerifyOptions verifyOptions = new BarcodeVerifyOptions();
            verifyOptions.setText(testData);
            verifyOptions.setEncodeType(BarcodeTypes.Code128);
            
            boolean isValid = signature.verify(verifyOptions) != null;
            assertTrue(isValid, "Signature should be valid");
        }
    }
    
    @Test
    public void testSearchFindsSignature() throws Exception {
        String signedDoc = "signed-document.pdf";
        
        try (Signature signature = new Signature(signedDoc)) {
            BarcodeSearchOptions searchOptions = new BarcodeSearchOptions();
            searchOptions.setAllPages(true);
            
            List<BarcodeSignature> signatures = signature.search(BarcodeSignature.class, searchOptions);
            
            assertFalse(signatures.isEmpty(), "Should find at least one signature");
            assertEquals("TEST-USER-12345", signatures.get(0).getText());
        }
    }
}
```

**Lista de verificación de integración**
- ✅ Probar todos los formatos compatibles (PDF, DOCX, XLSX, PPTX, PNG).  
- ✅ Verificar que los códigos de barras sobrevivan a un ciclo de impresión‑escaneo.  
- ✅ Realizar pruebas de estrés con cadenas de datos de longitud máxima.  
- ✅ Confirmar la posición en tamaños de página A4, Letter y personalizados.  
- ✅ Ejecutar firmas concurrentes en varios documentos.  
- ✅ Monitorear el uso de memoria para documentos > 500 páginas.  
- ✅ Asegurar que los escáneres de códigos de barras lean la salida de forma fiable.

### Registro y monitoreo
Agregue registros significativos alrededor de cada operación:

```java
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

public class DocumentSigningService {
    private static final Logger logger = LoggerFactory.getLogger(DocumentSigningService.class);
    
    public void signDocument(String docPath, String barcodeData) {
        logger.info("Starting signature process for document: {}", docPath);
        logger.debug("Barcode data length: {} characters", barcodeData.length());
        
        try (Signature signature = new Signature(docPath)) {
            BarcodeSignOptions options = new BarcodeSignOptions(barcodeData, BarcodeTypes.Code128);
            
            long startTime = System.currentTimeMillis();
            signature.sign(docPath + ".signed", options);
            long duration = System.currentTimeMillis() - startTime;
            
            logger.info("Successfully signed document in {}ms", duration);
        } catch (Exception e) {
            logger.error("Failed to sign document: {}", docPath, e);
            throw new RuntimeException("Signature operation failed", e);
        }
    }
}
```

Rastrear métricas clave como tiempo de procesamiento, consumo de memoria y tasas de error:

```java
// Track success/failure rates
metricsService.incrementCounter("signature.sign.success");
metricsService.incrementCounter("signature.verify.failure");

// Track performance
metricsService.recordTimer("signature.sign.duration", duration);

// Track document sizes
metricsService.recordHistogram("signature.document.pages", pageCount);
```

## Consejos profesionales de uso real
**Estrategia de procesamiento por lotes**
Al manejar cientos de archivos, procese en lotes y reporte el progreso:

```java
public void signBatch(List<String> documents, String barcodePrefix) {
    int total = documents.size();
    int completed = 0;
    int failed = 0;
    
    for (String docPath : documents) {
        try {
            String barcodeData = barcodePrefix + "-" + UUID.randomUUID().toString();
            signDocument(docPath, barcodeData);
            completed++;
            
            if (completed % 10 == 0) {
                logger.info("Progress: {}/{} documents signed", completed, total);
            }
        } catch (Exception e) {
            failed++;
            logger.warn("Failed to sign: {}", docPath, e);
        }
    }
    
    logger.info("Batch complete: {} succeeded, {} failed", completed, failed);
}
```

**Externalizar configuración**
Almacene la configuración del código de barras (tipo, tamaño, color) en un archivo de propiedades para ajustar fácilmente sin recompilar:

```java
public class BarcodeConfig {
    private int defaultWidth = 100;
    private int defaultHeight = 40;
    private String defaultBarcodeType = "Code128";
    private String defaultColor = "BLACK";
    
    // Load from properties file or environment variables
    public BarcodeConfig() {
        this.defaultWidth = Integer.parseInt(
            System.getProperty("barcode.width", "100")
        );
        // ... load other properties
    }
    
    public BarcodeSignOptions createDefaultOptions(String text) {
        BarcodeSignOptions options = new BarcodeSignOptions(text, getBarcodeType());
        options.setWidth(defaultWidth);
        options.setHeight(defaultHeight);
        options.setForeColor(getColor());
        return options;
    }
}
```

**Estandarizar la carga útil del código de barras**
Utilice un formato delimitado como `EMPID|TIMESTAMP|DOCID` para que el análisis sea simple y consistente:

```java
public class BarcodeDataBuilder {
    private String userId;
    private String action;
    private LocalDateTime timestamp;
    private String documentId;
    
    public BarcodeDataBuilder setUserId(String userId) {
        this.userId = userId;
        return this;
    }
    
    public BarcodeDataBuilder setAction(String action) {
        this.action = action;
        return this;
    }
    
    public BarcodeDataBuilder setDocumentId(String documentId) {
        this.documentId = documentId;
        return this;
    }
    
    public String build() {
        this.timestamp = LocalDateTime.now();
        
        // Format: VERSION|USER|ACTION|DOC_ID|TIMESTAMP|CHECKSUM
        String data = String.join("|",
            "v1",
            userId,
            action,
            documentId,
            timestamp.toString()
        );
        
        // Add simple checksum
        int checksum = data.hashCode();
        return data + "|" + checksum;
    }
    
    public static ParsedBarcodeData parse(String barcodeData) {
        String[] parts = barcodeData.split("\\|");
        if (parts.length != 6 || !parts[0].equals("v1")) {
            throw new IllegalArgumentException("Invalid barcode format");
        }
        
        return new ParsedBarcodeData(parts[1], parts[2], parts[3], 
                                     LocalDateTime.parse(parts[4]));
    }
}

// Usage:
String barcodeData = new BarcodeDataBuilder()
    .setUserId("john.smith")
    .setAction("APPROVED")
    .setDocumentId("INV-2025-042")
    .build();
```

**Detectar tipo de documento automáticamente**
Ajuste las dimensiones del código de barras según si el objetivo es PDF, Word o una imagen:

```java
public BarcodeSignOptions getOptimalOptions(String documentPath, String text) {
    String extension = documentPath.substring(documentPath.lastIndexOf(".") + 1).toLowerCase();
    
    BarcodeSignOptions options = new BarcodeSignOptions(text, BarcodeTypes.Code128);
    
    switch (extension) {
        case "pdf":
            // PDFs can handle larger, detailed barcodes
            options.setWidth(150);
            options.setHeight(50);
            break;
        case "docx":
        case "doc":
            // Word docs need compact signatures that don't disrupt flow
            options.setWidth(100);
            options.setHeight(35);
            options.setVerticalAlignment(VerticalAlignment.Bottom);
            break;
        case "xlsx":
        case "xls":
            // Excel needs signatures that don't obscure data
            options.setWidth(80);
            options.setHeight(30);
            options.setHorizontalAlignment(HorizontalAlignment.Right);
            break;
        default:
            // Safe defaults
            options.setWidth(100);
            options.setHeight(40);
    }
    
    return options;
}
```

## Recursos adicionales
- [GroupDocs.Signature documentation](https://docs.groupdocs.com/signature/java/) – Guía completa de la API y ejemplos de uso.  
- [GroupDocs support forum](https://forum.groupdocs.com/c/signature/13) – Ayuda de la comunidad y solución de problemas.  
- [API reference](https://apireference.groupdocs.com/signature/java) – Descripciones detalladas de firmas de métodos y parámetros.

## Preguntas frecuentes
**P: ¿Puedo usar GroupDocs.Signature con Java 17?**  
A: Sí – la biblioteca es totalmente compatible con JDK 8, 11 y 17.

**P: ¿El código de barras sobrevive a un ciclo de impresión‑escaneo?**  
A: Cuando usa Code128 o QR con tamaño y contraste suficientes, el código de barras sigue siendo escaneable después de imprimir y escanear.

**P: ¿Cuántos códigos de barras puede contener un solo documento?**  
A: No hay un límite estricto; sin embargo, para un rendimiento óptimo mantenga el recuento total por debajo de **200** por documento.

**P: ¿Se requiere una licencia para compilaciones de desarrollo?**  
A: Una licencia temporal elimina las marcas de agua de evaluación; una licencia completa es obligatoria para cualquier despliegue en producción.

**P: ¿Puedo firmar PDFs protegidos con contraseña?**  
A: Sí – proporcione la contraseña al crear el objeto `Signature`; la API desbloqueará el archivo internamente.

**Última actualización:** 2026-07-15  
**Probado con:** GroupDocs.Signature 23.9 para Java  
**Autor:** GroupDocs  

{< /blocks/products/pf/tutorial-page-section >}
{< /blocks/products/pf/main-container >}
{< /blocks/products/pf/main-wrap-class >}
{< blocks/products/products-backtop-button >}

## Tutoriales relacionados
- [Cómo verificar firmas de códigos de barras en Java con GroupDocs.Signature](/signature/java/search-verification/groupdocs-signature-java-document-verification/)
- [Cómo buscar firmas digitales en documentos Java con GroupDocs](/signature/java/search-verification/groupdocs-signature-java-digital-search-tutorial/)
- [Tutorial de firma de códigos de barras Java - Agregar, verificar y gestionar códigos de barras en PDFs](/signature/java/barcode-signatures/)