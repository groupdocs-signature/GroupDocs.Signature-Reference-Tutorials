---
categories:
- Document Signing
- Healthcare Integration
date: '2026-05-16'
description: Aprenda cómo crear PDF de Data Matrix y agregar PDF de código QR usando
  GroupDocs.Signature para Java. Guía paso a paso para la firma de documentos de atención
  médica.
keywords:
- create data matrix pdf
- add qr code pdf
- HIBC barcode Java
lastmod: '2026-05-16'
linktitle: Guía de firma de PDF HIBC en Java
schemas:
- author: GroupDocs
  dateModified: '2026-05-16'
  description: Learn how to create data matrix PDF and add QR code PDF using GroupDocs.Signature
    for Java. Step‑by‑step guide for healthcare document signing.
  headline: Create Data Matrix PDF with HIBC Barcode in Java
  type: TechArticle
- description: Learn how to create data matrix PDF and add QR code PDF using GroupDocs.Signature
    for Java. Step‑by‑step guide for healthcare document signing.
  name: Create Data Matrix PDF with HIBC Barcode in Java
  steps:
  - name: '**Import the required classes** – these give you access to the signature
      engine and Data Matrix options.'
    text: '**Import the required classes** – these give you access to the signature
      engine and Data Matrix options.'
  - name: '**Instantiate the `Signature` object** with absolute paths for source and
      destination files.'
    text: '**Instantiate the `Signature` object** with absolute paths for source and
      destination files.'
  - name: '**Configure the Data Matrix options** – set the HIBC string, choose `QrCodeTypes.HIBCLICDataMatrix`,
      and define placement coordinates. `QrCodeTypes` enumerates the supported barcode
      formats for HIBC signatures.'
    text: '**Configure the Data Matrix options** – set the HIBC string, choose `QrCodeTypes.HIBCLICDataMatrix`,
      and define placement coordinates. `QrCodeTypes` enumerates the supported barcode
      formats for HIBC signatures.'
  - name: '**Apply the signature** to the PDF.'
    text: '**Apply the signature** to the PDF.'
  - name: '**Dispose of resources** to free file handles and avoid memory leaks.'
    text: '**Dispose of resources** to free file handles and avoid memory leaks.'
  - name: '**Import QR‑specific classes**'
    text: '**Import QR‑specific classes**'
  - name: '**Create and configure QR options** – note the use of `QrCodeTypes.HIBCLICQR`.'
    text: '**Create and configure QR options** – note the use of `QrCodeTypes.HIBCLICQR`.'
  - name: '**Sign the document**'
    text: '**Sign the document**'
  type: HowTo
- questions:
  - answer: Yes, it also supports DOCX, XLSX, PPTX, PNG, JPEG, and TIFF with the same
      barcode‑signing API.
    question: Can GroupDocs.Signature sign file types other than PDF?
  - answer: Verify that your HIBC string follows the exact HIBCC syntax, use the online
      validator, and ensure you’re using the correct `QrCodeTypes` constant for the
      chosen format.
    question: How do I troubleshoot “Invalid barcode content” errors?
  - answer: QR ≈ 4,296 alphanumeric characters, Aztec ≈ 3,832 numeric / 3,067 alphanumeric,
      Data Matrix ≈ 3,116 numeric / 2,335 alphanumeric. Keep codes under 200 characters
      for optimal scan reliability.
    question: What is the maximum data capacity for each HIBC format?
  - answer: Absolutely. Create separate `QrCodeSignOptions` objects with different
      positions and call `signature.sign()` for each. Just ensure they don’t overlap.
    question: Is it possible to embed multiple barcode types in one PDF?
  - answer: No. After the JAR is on the classpath and the license is activated, all
      operations are performed locally.
    question: Do I need an internet connection for signing at runtime?
  type: FAQPage
tags:
- java
- pdf-signing
- hibc
- healthcare
- barcode
- pharmaceutical
title: Crear PDF de Data Matrix con código de barras HIBC en Java
type: docs
url: /es/java/barcode-signatures/sign-pdfs-hibc-lic-codes-groupdocs-java/
weight: 1
---

# Crear PDF Data Matrix con código de barras HIBC en Java

Si estás desarrollando software de logística farmacéutica o de atención médica, probablemente te hayas topado con el muro del seguimiento basado en papel, firmas perdidas y pesadillas de auditoría. **Crear un PDF Data Matrix** que incorpore un código de barras HIBC LIC resuelve esos problemas al proporcionarte una pista a prueba de manipulaciones y legible por máquinas que sobrevive a la impresión, escaneo y revisión regulatoria. En este tutorial verás exactamente cómo **añadir soporte de PDF con código QR**, así como los formatos Aztec y Data Matrix, usando GroupDocs.Signature para Java.

## Respuestas rápidas
- **¿Qué biblioteca maneja códigos de barras HIBC en Java?** GroupDocs.Signature for Java.  
- **¿Qué formato de código de barras es el más compacto?** Data Matrix – ideal para etiquetas pequeñas.  
- **¿Puedo agregar tanto QR como Data Matrix al mismo PDF?** Sí, solo crea `QrCodeSignOptions` separados.  
- **¿Necesito una conexión a internet en tiempo de ejecución?** No, la biblioteca funciona completamente sin conexión después de la instalación.  
- **¿Qué versión de Java se recomienda?** Java 11+ para rendimiento de nivel de producción.

## ¿Qué es la firma de PDF con código de barras HIBC?
La clase `Signature` en GroupDocs.Signature para Java representa un documento PDF y proporciona métodos para incrustar códigos de barras HIBC como firmas digitales. Al firmar un PDF con un código de barras HIBC creas un registro verificable y a prueba de manipulaciones que puede escanearse en cualquier punto de la cadena de suministro.

## ¿Por qué usar Data Matrix y códigos QR juntos?
GroupDocs.Signature admite **más de 50 formatos de entrada y salida** y puede procesar PDFs de cientos de páginas sin cargar todo el archivo en memoria. Usar Data Matrix para etiquetas densas y de área pequeña y QR para documentos más espaciosos te brinda el mejor equilibrio entre legibilidad, capacidad de datos (hasta 4 296 caracteres para QR) y eficiencia del espacio de impresión.

## Requisitos previos
- **JDK 11 o superior** (Java 8 funciona pero se recomienda Java 11+ para un rendimiento óptimo).  
- **IDE** como IntelliJ IDEA, Eclipse o VS Code con extensiones Java.  
- **Maven o Gradle** para la gestión de dependencias (ejemplos a continuación).  
- **PDF de ejemplo** (p. ej., `sample.pdf`) para probar la implementación.  
- **Licencia válida de GroupDocs.Signature** (prueba gratuita para desarrollo, licencia de pago para producción).

## Configuración de GroupDocs.Signature para Java

### Configuración de Maven
Add the dependency to your `pom.xml`:

```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

### Configuración de Gradle
For Gradle projects, add this to your `build.gradle`:

```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

### Opción de descarga directa
También puedes descargar el archivo JAR directamente desde [GroupDocs.Signature for Java releases](https://releases.groupdocs.com/signature/java/) y añadirlo manualmente al classpath de tu proyecto. Este enfoque funciona bien en entornos con red restringida.

### Obtención de una licencia
Solicita una prueba gratuita o una licencia temporal a GroupDocs para eliminar marcas de agua y desbloquear todas las funciones. Las implementaciones en producción requieren una licencia comprada.

### Inicialización básica
La clase `Signature` es el punto de entrada para todas las operaciones de firma. Carga el PDF, aplica el código de barras y escribe el archivo firmado.

```java
import com.groupdocs.signature.Signature;

class InitializeSignature {
    public static void main(String[] args) {
        Signature signature = new Signature("sample.pdf");
        // Proceed with signing operations...
    }
}
```

## ¿Cómo crear un PDF Data Matrix con código de barras HIBC?
Carga tu PDF de origen, configura un objeto `QrCodeSignOptions` para el formato Data Matrix y llama a `sign()` – eso es todo lo que necesitas para incrustar un código de barras HIBC Data Matrix compatible. Los pasos siguientes te guiarán a través del código exacto requerido. `QrCodeSignOptions` define la configuración de una firma de código de barras, como tipo, contenido, tamaño y posición.

1. **Importar las clases requeridas** – estas te dan acceso al motor de firma y a las opciones de Data Matrix.  

```java
import com.groupdocs.signature.Signature;
import com.groupdocs.signature.options.sign.QrCodeSignOptions;
import com.groupdocs.signature.domain.qrcodes.QrCodeTypes;
```

2. **Instanciar el objeto `Signature`** con rutas absolutas para los archivos de origen y destino.  

```java
String sourceFilePath = "YOUR_DOCUMENT_DIRECTORY";
String destinFilePath = "YOUR_OUTPUT_DIRECTORY/SignWithHIBCLICQR.pdf";

final Signature signature = new Signature(sourceFilePath);
```

3. **Configurar las opciones de Data Matrix** – establecer la cadena HIBC, elegir `QrCodeTypes.HIBCLICDataMatrix` y definir las coordenadas de ubicación. `QrCodeTypes` enumera los formatos de código de barras compatibles para firmas HIBC.  

```java
QrCodeSignOptions hibcLic_QR = new QrCodeSignOptions("A123PROD30917/75#422011907#GP293", QrCodeTypes.HIBCLICQR);
hibcLic_QR.setLeft(1); // Set the position from left
hibcLic_QR.setTop(1);   // Set the position from top
hibcLic_QR.setReturnContent(true); // Return content after signing
hibcLic_QR.setReturnContentType(FileType.PNG); // Specify return content type as PNG
```

4. **Aplicar la firma** al PDF.  

```java
signature.sign(destinFilePath, hibcLic_QR);
```

5. **Liberar los recursos** para liberar los manejadores de archivo y evitar fugas de memoria.  

```java
finally {
    if (signature != null) signature.dispose();
}
```

### Ejemplo completo en funcionamiento
Aquí está el flujo completo en un solo bloque (los marcadores de posición representan el código exacto que pegarás de los fragmentos anteriores):

```java
import com.groupdocs.signature.Signature;
import com.groupdocs.signature.options.sign.QrCodeSignOptions;
import com.groupdocs.signature.domain.qrcodes.QrCodeTypes;

public class HibcQrSigning {
    public static void main(String[] args) {
        String sourceFilePath = "sample.pdf";
        String destinFilePath = "output/SignWithHIBCLICQR.pdf";
        
        Signature signature = null;
        try {
            signature = new Signature(sourceFilePath);
            
            QrCodeSignOptions hibcLic_QR = new QrCodeSignOptions(
                "A123PROD30917/75#422011907#GP293", 
                QrCodeTypes.HIBCLICQR
            );
            hibcLic_QR.setLeft(1);
            hibcLic_QR.setTop(1);
            hibcLic_QR.setReturnContent(true);
            hibcLic_QR.setReturnContentType(FileType.PNG);
            
            signature.sign(destinFilePath, hibcLic_QR);
            System.out.println("PDF signed successfully with HIBC QR code");
            
        } catch (Exception e) {
            System.err.println("Error signing PDF: " + e.getMessage());
            e.printStackTrace();
        } finally {
            if (signature != null) signature.dispose();
        }
    }
}
```

#### Respuesta directa (40–70 palabras)
Para **crear un PDF Data Matrix**, instancia `Signature` con tu PDF de origen, configura `QrCodeSignOptions` a `QrCodeTypes.HIBCLICDataMatrix` y proporciona una cadena HIBC correctamente formateada, luego llama a `signature.sign(outputPath, options)`. La biblioteca escribe el PDF firmado en el destino, preservando el diseño e incrustando el código de barras como una firma a prueba de manipulaciones.

## ¿Cómo agregar PDF con código QR usando GroupDocs.Signature?
Carga el PDF, configura `QrCodeSignOptions` para el formato QR y llama a `sign()`. Este patrón de dos líneas funciona para cualquier tamaño de PDF y escala automáticamente la imagen QR para una legibilidad óptima. `QrCodeSignOptions` configura la firma del código de barras QR, incluyendo su contenido y propiedades visuales. Posiciona el código según las coordenadas que establezcas, asegurando que no se superponga al contenido existente y que siga siendo escaneable después de imprimir.

1. **Importar clases específicas de QR**  

```java
QrCodeSignOptions hibcLic_AZ = new QrCodeSignOptions("A123PROD30917/75#422011907#GP293", QrCodeTypes.HIBCLICAztec);
hibcLic_AZ.setLeft(1); // Set the position from left
hibcLic_AZ.setTop(200); // Set the position from top
hibcLic_AZ.setReturnContent(true); // Return content after signing
hibcLic_AZ.setReturnContentType(FileType.PNG); // Specify return content type as PNG
```

2. **Crear y configurar opciones QR** – observa el uso de `QrCodeTypes.HIBCLICQR`.  

```java
signature.sign(destinFilePath, hibcLic_AZ);
```

3. **Firmar el documento**  

```java
QrCodeSignOptions hibcLic_DM = new QrCodeSignOptions("A123PROD30917/75#422011907#GP293", QrCodeTypes.HIBCLICDataMatrix);
hibcLic_DM.setLeft(1); // Set the position from left
hibcLic_DM.setTop(400); // Set the position from top
hibcLic_DM.setReturnContent(true); // Return content after signing
hibcLic_DM.setReturnContentType(FileType.PNG); // Specify return content type as PNG
```

> **Respuesta directa:** Usa `QrCodeTypes.HIBCLICQR` en `QrCodeSignOptions`, establece la cadena de contenido HIBC, posiciona el código con `setLeft()` y `setTop()`, luego llama a `signature.sign(outputPath, options)`. El código de barras QR se incrusta instantáneamente, listo para captura con smartphone o escáner.

## Errores comunes a evitar

### 1. Olvidar liberar recursos
**Incorrecto:**  
```java
Signature signature = new Signature("sample.pdf");
signature.sign(destinFilePath, options);
// Oops, no dispose() call
```  

**Corrección:** Envuelve el uso de `Signature` en un bloque try‑with‑resources o llama explícitamente a `close()` en una cláusula finally.

### 2. Usar cadenas de formato HIBC incorrectas
**Incorrecto:** Usar cadenas genéricas como “12345”.  
**Corrección:** Sigue el estándar HIBCC (p. ej., `A123PROD30917/75#422011907#GP293`). Valida con el [validador en línea de HIBCC](https://www.hibcc.org/).

### 3. Codificar rutas de archivo de forma rígida
**Incorrecto:**  
```java
String sourceFilePath = "C:/Users/John/Documents/test.pdf";
```  

**Corrección:** Almacena las rutas en un archivo de configuración o variable de entorno y léelas en tiempo de ejecución.

### 4. Ignorar conflictos de posición del código de barras
Coloca los códigos de barras lejos del texto o firmas existentes. Usa coordenadas PDF (el origen es la esquina inferior izquierda) y prueba con una muestra impresa.

### 5. No probar con escáneres reales
Imprime el PDF firmado y escanéalo con el hardware exacto usado en tu flujo de trabajo. Verifica la legibilidad en diferentes calidades de impresión.

## Aplicaciones prácticas en el sector salud

| Escenario | Código de barras recomendado | Por qué es adecuado |
|----------|------------------------------|---------------------|
| **Distribución farmacéutica** | QR Code | Alta capacidad de datos, escaneado ampliamente por smartphones. |
| **Gestión de inventario** | Data Matrix | Pequeña huella, ideal para etiquetas densas en estanterías. |
| **Cumplimiento regulatorio (FDA 21 CFR Part 11)** | QR + Data Matrix | Formato dual proporciona redundancia y auditabilidad. |
| **Seguimiento de dispositivos médicos** | Aztec Code | Tamaño compacto funciona en empaques con espacio limitado. |

## Consideraciones de rendimiento y mejores prácticas

### Patrón de procesamiento por lotes
```java
List<String> filesToSign = getFileList();
for (String filePath : filesToSign) {
    Signature signature = null;
    try {
        signature = new Signature(filePath);
        // Sign and save
    } finally {
        if (signature != null) signature.dispose();
    }
}
```

- Crear una nueva instancia de `Signature` por archivo para mantener bajo el uso de memoria.  
- Utilizar un pool de hilos fijo (`Executors.newFixedThreadPool(Runtime.getRuntime().availableProcessors() - 1)`) para procesamiento en paralelo, pero monitorear el tamaño del heap porque cada `Signature` mantiene el PDF completo en memoria.  

### Mantener las bibliotecas actualizadas
Las versiones de GroupDocs mejoran la velocidad de procesamiento hasta en **20 %** y añaden nuevas funciones de cumplimiento HIBC. Programa revisiones de dependencias trimestrales.

### Caché de plantillas
Carga una plantilla PDF una vez, clónala para cada variante de código de barras y firma los clones. Esto reduce I/O y acelera los flujos de trabajo de alto volumen.

## Preguntas frecuentes

**Q: ¿Puede GroupDocs.Signature firmar tipos de archivo distintos a PDF?**  
A: Sí, también admite DOCX, XLSX, PPTX, PNG, JPEG y TIFF con la misma API de firma de códigos de barras.

**Q: ¿Cómo solucionar errores de “Contenido de código de barras inválido”?**  
A: Verifica que tu cadena HIBC siga la sintaxis exacta de HIBCC, usa el validador en línea y asegura que estés usando la constante `QrCodeTypes` correcta para el formato elegido.

**Q: ¿Cuál es la capacidad máxima de datos para cada formato HIBC?**  
A: QR ≈ 4 296 caracteres alfanuméricos, Aztec ≈ 3 832 numéricos / 3 067 alfanuméricos, Data Matrix ≈ 3 116 numéricos / 2 335 alfanuméricos. Mantén los códigos por debajo de 200 caracteres para una fiabilidad de escaneo óptima.

**Q: ¿Es posible incrustar varios tipos de códigos de barras en un solo PDF?**  
A: Absolutamente. Crea objetos `QrCodeSignOptions` separados con diferentes posiciones y llama a `signature.sign()` para cada uno. Solo asegúrate de que no se superpongan.

**Q: ¿Necesito una conexión a internet para firmar en tiempo de ejecución?**  
A: No. Después de que el JAR esté en el classpath y la licencia esté activada, todas las operaciones se realizan localmente.

## Recursos adicionales

- [Documentación de GroupDocs.Signature para Java](https://docs.groupdocs.com/signature/java/)  
- [Guía de referencia API](https://reference.groupdocs.com/signature/java/)  
- [Descargas de la última versión](https://releases.groupdocs.com/signature/java/)  
- [Comprar licencia](https://purchase.groupdocs.com/buy)  
- [Obtener prueba gratuita](https://releases.groupdocs.com/signature/java/)  
- [Solicitar licencia temporal](https://purchase.groupdocs.com/temporary-license/)  
- [Foro de GroupDocs](https://forum.groupdocs.com/c/signature/)

---

**Última actualización:** 2026-05-16  
**Probado con:** GroupDocs.Signature 23.12 para Java  
**Autor:** GroupDocs  

```java
signature.sign(destinFilePath, hibcLic_DM);
```

## Tutoriales relacionados

- [Crear firma de código de barras PDF en Java – Guía de GroupDocs](/signature/java/barcode-signatures/create-sign-pdfs-groupdocs-barcode-java/)
- [Crear firma de código de barras en Java – Actualizar códigos de barras PDF](/signature/java/barcode-signatures/java-groupdocs-signature-barcode-initialize-update/)
- [Cómo leer PDF con código QR usando Java y GroupDocs.Signature](/signature/java/barcode-signatures/java-pdf-barcode-search-groupdocs-signature-api/)