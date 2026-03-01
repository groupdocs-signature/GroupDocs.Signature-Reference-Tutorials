---
categories:
- Java Development
- Document Processing
date: '2026-03-01'
description: Aprende a leer archivos PDF con códigos QR usando Java y GroupDocs.Signature.
  Guía paso a paso, ejemplos de código, solución de problemas y casos reales.
keywords: read qr code pdf, Java barcode verification PDF, GroupDocs barcode search
  tutorial, extract barcode data from PDF Java, Java PDF barcode scanner
lastmod: '2026-03-01'
linktitle: Search PDF Barcodes Java
tags:
- barcode-search
- pdf-processing
- groupdocs
- java-tutorial
- document-verification
title: Cómo leer un PDF con código QR usando Java y GroupDocs.Signature
type: docs
url: /es/java/barcode-signatures/java-pdf-barcode-search-groupdocs-signature-api/
weight: 1
---

# Cómo leer PDF con código QR usando Java

## Introducción

¿Alguna vez necesitaste extraer información de códigos de barras de cientos de facturas PDF, etiquetas de envío o documentos de inventario? Escanear manualmente las páginas es tedioso y propenso a errores. Ya sea que estés construyendo un sistema automatizado de procesamiento de documentos o verificando la autenticidad de productos, encontrar códigos de barras de manera eficiente en PDFs puede ser un desafío.

En esta guía, aprenderás a **leer PDF con código QR** de forma eficiente usando la API GroupDocs.Signature. Esta poderosa API convierte lo que podrían ser horas de trabajo manual en solo unas pocas líneas de código. Puedes escanear documentos completos, localizar tipos específicos de códigos de barras (como códigos QR o Code128) y extraer sus datos automáticamente.

**Lo que aprenderás:**
- Configurar GroupDocs.Signature para Java en minutos  
- Buscar firmas de códigos de barras dentro de documentos PDF  
- Configurar opciones de búsqueda para obtener resultados precisos y dirigidos  
- Manejar diferentes tipos de códigos de barras (códigos QR, EAN, Code128, etc.)  
- Solucionar problemas comunes y optimizar el rendimiento  

¡Vamos al grano!

## Respuestas rápidas
- **¿GroupDocs.Signature puede leer códigos QR de PDFs?** Sí, detecta QR, Data Matrix, PDF417 y muchos códigos de barras 1D.  
- **¿Necesito una licencia para uso en producción?** Se requiere una licencia comercial; hay una prueba gratuita disponible para evaluación.  
- **¿Qué versión de Java se necesita?** Java 8+ (se recomienda Java 11+).  
- **¿Cómo limito la búsqueda a páginas específicas?** Usa `BarcodeSearchOptions.setAllPages(false)` y establece `setPageNumber()`.  
- **¿Es la API segura para hilos en procesamiento por lotes?** Sí, cuando creas una instancia `Signature` separada por hilo.

## ¿Por qué buscar códigos de barras en PDFs?

Antes de entrar en lo técnico, aquí tienes por qué esto es importante en aplicaciones del mundo real:

**Escenarios empresariales comunes**
- **Procesamiento de facturas** – Extrae automáticamente números de orden o códigos de seguimiento de facturas de proveedores.  
- **Gestión de inventario** – Escanea catálogos de productos y extrae códigos de barras SKU para actualizar bases de datos.  
- **Envíos y logística** – Verifica códigos de seguimiento de paquetes en manifiestos de envío.  
- **Autenticación de documentos** – Valida documentos firmados verificando códigos de barras de seguridad incrustados.  
- **Registros de salud** – Extrae IDs de pacientes o códigos de prescripción de documentos médicos.  

La API GroupDocs.Signature se encarga del trabajo pesado; no necesitas preocuparte por el procesamiento de imágenes, algoritmos de decodificación de códigos de barras o complejidades de renderizado de PDF. Todo está integrado.

## Requisitos previos

Antes de comenzar este tutorial, asegúrate de tener lo siguiente listo:

### Bibliotecas y dependencias requeridas

Necesitarás incluir la biblioteca GroupDocs.Signature en tu proyecto Java. Así es como se agrega usando Maven o Gradle:

**Maven:**  
```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

**Gradle:**  
```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

**Nota:** Siempre verifica la última versión en [GroupDocs.Signature for Java releases](https://releases.groupdocs.com/signature/java/). Usar la versión más reciente garantiza correcciones de errores y nuevas funcionalidades.

### Configuración del entorno

- **JDK 8 o superior** – GroupDocs.Signature requiere Java 8 como mínimo (se recomienda Java 11+ para mejor rendimiento).  
- **IDE** – Cualquier editor de texto funciona, pero IntelliJ IDEA o Eclipse harán tu vida más fácil con autocompletado y depuración.  
- **Documento PDF** – Ten un PDF de prueba con códigos de barras listo (facturas, etiquetas de envío o catálogos de productos funcionan muy bien).

### Conocimientos previos

Debes estar cómodo con:
- Sintaxis básica de Java y conceptos de programación orientada a objetos  
- Manejo de excepciones con bloques `try‑catch`  
- Trabajo con bibliotecas externas en tu IDE  

Si eres nuevo en bibliotecas Java de terceros, no te preocupes; recorreremos todo paso a paso.

## Configuración de GroupDocs.Signature para Java

Comenzar con GroupDocs.Signature lleva solo unos minutos. Este es el proceso completo de configuración:

### Paso 1: Añadir la dependencia

Usa Maven o Gradle para incluir la biblioteca (ver código arriba). Después de añadir la dependencia, actualiza tu proyecto para descargar los archivos JAR.

### Paso 2: Obtención de la licencia

GroupDocs ofrece varias opciones de licencia:

- **Prueba gratuita** – Perfecta para pruebas. Descárgala desde [GroupDocs releases](https://releases.groupdocs.com/signature/java/).  
- **Licencia temporal** – Obtén 30 días de acceso completo a través de la [Temporary License Page](https://purchase.groupdocs.com/temporary-license/).  
- **Licencia comercial** – Para uso en producción, compra una licencia en [GroupDocs Purchase](https://purchase.groupdocs.com/).  

**Consejo profesional:** Comienza con la prueba gratuita para crear tu prueba de concepto y luego actualiza si la API se ajusta a tus necesidades.

### Paso 3: Inicialización básica

Así es como creas un objeto `Signature` para trabajar con tu PDF:

```java
import com.groupdocs.signature.Signature;

String filePath = "YOUR_DOCUMENT_DIRECTORY/sample_signed.pdf"; // Replace with your PDF path
Signature signature = new Signature(filePath);
```

La clase `Signature` es tu punto de entrada principal. Carga el PDF en memoria y proporciona métodos para buscar, verificar y extraer datos de firmas (incluidos los códigos de barras).

**Importante**: Asegúrate de que la ruta del archivo sea correcta y que el PDF exista. ¿Error típico de principiantes? Usar barras invertidas en Windows sin escaparlas (`C:\\Documents\\file.pdf` y no `C:\Documents\file.pdf`).

## Guía de implementación

Ahora viene la parte divertida: escribamos el código para buscar códigos de barras en tu PDF.

### Búsqueda de firmas de códigos de barras en un documento

Esta sección muestra cómo escanear un PDF y localizar todas las firmas de códigos de barras. Lo dividiremos en pasos digeribles con explicaciones para cada parte.

#### Paso 1: Inicializar el objeto Signature

Comienza cargando tu documento PDF:

```java
import com.groupdocs.signature.Signature;

String filePath = "YOUR_DOCUMENT_DIRECTORY/sample_signed.pdf"; // Replace with actual file path
Signature signature = new Signature(filePath);
```

**Qué está ocurriendo aquí**  
La clase `Signature` abre tu PDF y lo prepara para el procesamiento. Piensa en ello como abrir un archivo en un editor de texto: estás cargando el documento en memoria para trabajar con él.

**Nota del mundo real**  
Si procesas PDFs subidos por usuarios, siempre valida la ruta del archivo y verifica que exista antes de crear el objeto `Signature`. Esto evita errores crípticos más adelante.

#### Paso 2: Crear BarcodeSearchOptions

Configura cómo deseas buscar los códigos de barras:

```java
import com.groupdocs.signature.options.search.BarcodeSearchOptions;

// Configure options for searching barcodes
BarcodeSearchOptions options = new BarcodeSearchOptions();
options.setAllPages(true); // Search every page in the document
```

**Opciones clave de configuración**

- `setAllPages(true)`: Escanea todas las páginas. Establécelo en `false` si solo deseas revisar páginas específicas (configúralo con `setPageNumber()`).  
- **Por qué importa**: Si procesas facturas donde los códigos de barras siempre están en la página 1, buscar en todas las páginas desperdicia recursos. Para manifiestos de envío de varias páginas, necesitarás `setAllPages(true)`.

**Consejo profesional**: También puedes filtrar por tipo de código de barras (más adelante en la sección **Tipos de códigos de barras compatibles**). Esto acelera las búsquedas cuando sabes exactamente qué formato buscas.

#### Paso 3: Ejecutar la búsqueda y manejar los resultados

Ahora ejecuta la búsqueda y procesa los resultados:

```java
import com.groupdocs.signature.domain.signatures.BarcodeSignature;
import java.util.List;

try {
    // Execute the barcode search
    List<BarcodeSignature> signatures = signature.search(BarcodeSignature.class, options);
    
    // Check if any barcodes were found
    if (signatures.isEmpty()) {
        System.out.println("No barcode signatures found in the document.");
    } else {
        System.out.println("Found " + signatures.size() + " barcode signature(s):\n");
        
        // Loop through each barcode and display details
        for (BarcodeSignature barcodeSignature : signatures) {
            System.out.println("----------------------------------------");
            System.out.println("Barcode Type: " + barcodeSignature.getEncodeType().getTypeName());
            System.out.println("Barcode Text: " + barcodeSignature.getText());
            System.out.println("Page Number: " + barcodeSignature.getPageNumber());
            System.out.println("Position: X=" + barcodeSignature.getLeft() + 
                             ", Y=" + barcodeSignature.getTop());
            System.out.println("Size: Width=" + barcodeSignature.getWidth() + 
                             ", Height=" + barcodeSignature.getHeight());
            System.out.println("----------------------------------------\n");
        }
    }
} catch (Exception e) {
    System.err.println("Error searching for barcodes: " + e.getMessage());
    e.printStackTrace();
} finally {
    // Always dispose of the signature object to free resources
    if (signature != null) {
        signature.dispose();
    }
}
```

**Qué ocurre en este código**

1. **Ejecución de la búsqueda** – `signature.search()` escanea el PDF y devuelve una lista de objetos `BarcodeSignature`.  
2. **Comprobación de vacío** – Verifica que realmente se hayan encontrado códigos de barras (evita excepciones de puntero nulo).  
3. **Extracción de datos** – Para cada código de barras, extraemos:  
   - **Tipo** – El formato del código (QR Code, Code128, EAN13, etc.)  
   - **Texto** – Los datos decodificados (número de orden, código de seguimiento, SKU, etc.)  
   - **Ubicación** – Número de página y coordenadas X/Y  
   - **Dimensiones** – Ancho y alto (útil para validación)  
4. **Manejo de errores** – El bloque `try‑catch` evita caídas si algo sale mal (PDF corrupto, archivo faltante, etc.).  
5. **Limpieza de recursos** – El bloque `finally` asegura que el objeto `Signature` se libere correctamente, liberando memoria.

**Aplicación del mundo real**  
Supongamos que procesas etiquetas de envío. Extraerías el valor `getText()` (número de seguimiento) y lo almacenarías en tu base de datos. El número de página te indica a qué etiqueta corresponde cada envío si procesas documentos por lotes.

### Filtrado por tipo de código de barras

Puedes acelerar las búsquedas especificando el tipo de código que buscas:

```java
import com.groupdocs.signature.domain.barcodes.BarcodeTypes;

BarcodeSearchOptions options = new BarcodeSearchOptions();
options.setEncodeType(BarcodeTypes.QR); // Only search for QR codes
options.setAllPages(true);
```

**Cuándo filtrar**  
Si sabes que tus facturas solo contienen códigos Code128, filtrar por tipo reduce el tiempo de procesamiento entre un 30 % y 50 % en documentos grandes.

## Tipos de códigos de barras compatibles

GroupDocs.Signature puede detectar una amplia gama de formatos de códigos de barras. Esto es lo que puedes buscar:

**Códigos de barras 1D (lineales)**
- **Code128** – Común en envíos y empaques  
- **Code39** – Usado en industrias automotriz y de defensa  
- **EAN13/EAN8** – Códigos de productos minoristas (los ves en cada producto)  
- **UPC‑A/UPC‑E** – Estándar norteamericano de retail  
- **Interleaved2of5** – Almacenes y distribución  

**Códigos de barras 2D (matrices)**
- **QR Code** – El más popular—usado para URLs, contraseñas Wi‑Fi, información de pago  
- **Data Matrix** – Formato compacto para artículos pequeños (componentes electrónicos)  
- **PDF417** – Identificaciones gubernamentales, tarjetas de embarque, licencias de conducir  
- **Aztec Code** – Boletos de transporte  

**Filtrado por tipo** (ejemplo mostrado antes) te ayuda a enfocarte en el formato exacto que necesitas.

## Casos de uso del mundo real

Así es como los desarrolladores están usando la búsqueda de códigos de barras en producción:

### 1. Procesamiento automatizado de facturas
**Escenario** – Un departamento de contabilidad recibe más de 500 facturas de proveedores al día en formato PDF.  
**Solución** – Escanear cada PDF en busca de códigos Code39 que contengan números de factura, emparejándolos automáticamente con órdenes de compra en el ERP. Esto elimina la entrada manual de datos y reduce errores.

```java
// Pseudo-code workflow
for (PDF invoice : invoiceBatch) {
    List<BarcodeSignature> barcodes = searchBarcodes(invoice);
    String invoiceNumber = barcodes.get(0).getText();
    updateERPSystem(invoiceNumber, invoice);
}
```

### 2. Actualizaciones de inventario en almacén
**Escenario** – Un almacén recibe envíos con listas de empaque PDF que contienen SKUs como códigos EAN13.  
**Solución** – Extraer todos los códigos de barras de las listas de empaque, actualizar los conteos de inventario automáticamente y marcar discrepancias para revisión.

### 3. Autenticación de documentos
**Escenario** – Documentos legales incluyen códigos QR con firmas criptográficas para verificar autenticidad.  
**Solución** – Buscar códigos QR en contratos firmados, decodificar los datos de la firma y verificarlos contra una autoridad certificadora de confianza. Esto garantiza que los documentos no hayan sido manipulados.

### 4. Gestión de registros de salud
**Escenario** – Los expedientes de pacientes en hospitales contienen informes de laboratorio PDF con códigos Code128 para IDs de muestras.  
**Solución** – Extraer automáticamente los IDs de muestra y enlazar los resultados de laboratorio con los registros de pacientes en el sistema de información hospitalaria (HIS).

## Problemas comunes y soluciones

A continuación se presentan problemas que podrías encontrar y cómo solucionarlos:

### Problema 1: “No se encontraron códigos de barras” (aunque sabes que existen)

**Posibles causas**
- La calidad de la imagen del código de barras es demasiado baja (borrosa, pixelada)  
- El PDF es basado en imágenes pero el código es muy pequeño  
- Estás buscando el tipo de código de barras incorrecto  

**Soluciones**
1. **Verifica la resolución de la imagen** – Los códigos de barras necesitan al menos 200 DPI para una detección fiable. Si escaneas documentos, usa 300 DPI o más.  
2. **Elimina el filtrado por tipo** – Prueba buscar todos los tipos de códigos de barras primero (no establezcas `setEncodeType()`), luego delimita una vez que identifiques lo que hay en el documento.  
3. **Comprueba la calidad del código** – Abre el PDF en Adobe Acrobat y haz zoom. Si el código se ve borroso para ti, también lo será para la API.

### Problema 2: `OutOfMemoryError` con PDFs grandes

**Causa** – Cargar un PDF de 500 páginas con imágenes de alta resolución consume mucha memoria.  

**Solución**
1. **Procesar páginas por lotes** – En lugar de `setAllPages(true)`, procesa 50 páginas a la vez:

```java
for (int startPage = 1; startPage <= totalPages; startPage += 50) {
    BarcodeSearchOptions options = new BarcodeSearchOptions();
    options.setPageNumber(startPage);
    options.setPagesSetup(new PagesSetup());
    options.getPagesSetup().setLastPage(Math.min(startPage + 49, totalPages));
    
    List<BarcodeSignature> batchResults = signature.search(BarcodeSignature.class, options);
    // Process results...
}
```

2. **Aumentar el heap de JVM** – Añade `-Xmx4g` a tu comando Java para asignar 4 GB de memoria (ajusta según tus necesidades).

### Problema 3: Rendimiento lento en documentos multipágina

**Causa** – Buscar en todas las páginas secuencialmente lleva tiempo, especialmente con códigos complejos como PDF417.  

**Soluciones**
1. **Procesamiento paralelo** – Si los códigos siempre están en páginas específicas (p. ej., página 1 de facturas), busca solo esas páginas.  
2. **Cachear resultados** – Si procesas el mismo documento varias veces, almacena en caché los datos de los códigos de barras para evitar volver a escanear.  
3. **Usar SSDs** – La velocidad de I/O importa al cargar PDFs grandes. Los SSD reducen el tiempo de carga en un 60‑70 % comparado con HDDs.

### Problema 4: Falsos positivos (detecta patrones aleatorios como códigos de barras)

**Causa** – Tablas, cuadrículas o patrones de líneas pueden ser identificados erróneamente como códigos de barras.  

**Solución** – Valida los resultados verificando la longitud y el formato del texto decodificado:

```java
for (BarcodeSignature barcode : signatures) {
    String text = barcode.getText();
    
    // Example: Invoice numbers are always 10 digits
    if (text.matches("\\d{10}")) {
        // Valid invoice number
        processBarcode(barcode);
    } else {
        System.out.println("Skipping invalid barcode: " + text);
    }
}
```

## Consejos de rendimiento para documentos grandes

¿Procesas miles de PDFs? Aquí tienes cómo optimizar:

### 1. Estrategia de procesamiento por lotes

En lugar de procesar archivos uno a uno, usa un pool de hilos para manejar varios PDFs simultáneamente:

```java
ExecutorService executor = Executors.newFixedThreadPool(4); // 4 parallel threads

for (String pdfPath : pdfFiles) {
    executor.submit(() -> {
        try (Signature sig = new Signature(pdfPath)) {
            List<BarcodeSignature> results = sig.search(BarcodeSignature.class, options);
            // Process results...
        } catch (Exception e) {
            e.printStackTrace();
        }
    });
}

executor.shutdown();
executor.awaitTermination(1, TimeUnit.HOURS);
```

**Ganancia de rendimiento** – Procesar 1 000 archivos pasa de ~2 horas a ~30 minutos en una máquina quad‑core.

### 2. Reducir el alcance de la búsqueda

Si tu lógica de negocio lo permite, limita el área de búsqueda:

```java
// Only search the top‑right corner where barcodes are typically placed
options.setRectangle(new Rectangle(400, 50, 150, 150)); // X, Y, Width, Height
```

**Ganancia de rendimiento** – 40‑60 % más rápido en documentos donde la ubicación del código de barras es consistente.

### 3. Monitorear el uso de memoria

Para procesos por lotes de larga duración, monitorea el heap y sugiere explícitamente la recolección de basura si es necesario:

```java
Runtime runtime = Runtime.getRuntime();
long usedMemory = runtime.totalMemory() - runtime.freeMemory();

if (usedMemory > (runtime.maxMemory() * 0.8)) {
    System.gc(); // Suggest garbage collection
}
```

## Buenas prácticas

Sigue estas directrices para un código listo para producción:

### 1. Siempre disponer de los objetos Signature

Envuelve tu código en *try‑with‑resources* (Java 7+) para cerrar recursos automáticamente:

```java
try (Signature signature = new Signature(filePath)) {
    // Your search code here...
} // Automatically disposed
```

### 2. Validar archivos de entrada

Antes de procesar, verifica que el archivo exista y sea un PDF válido:

```java
File pdfFile = new File(filePath);
if (!pdfFile.exists() || !pdfFile.canRead()) {
    throw new FileNotFoundException("PDF not found or not readable: " + filePath);
}

// Optional: Verify it's actually a PDF (check magic bytes)
```

### 3. Registrar los resultados de detección de códigos de barras

Para depuración y auditoría, registra lo que encuentras:

```java
Logger logger = Logger.getLogger(BarcodeSearcher.class.getName());

for (BarcodeSignature barcode : signatures) {
    logger.info(String.format("Detected %s barcode '%s' on page %d at (%.2f, %.2f)",
        barcode.getEncodeType().getTypeName(),
        barcode.getText(),
        barcode.getPageNumber(),
        barcode.getLeft(),
        barcode.getTop()));
}
```

### 4. Manejar diferentes formatos de códigos de barras

Diferentes industrias usan diferentes estándares. Haz tu código flexible:

```java
switch (barcode.getEncodeType().getTypeName()) {
    case "QR":
        // QR codes might contain URLs or JSON data
        processQRCode(barcode.getText());
        break;
    case "Code128":
        // Code128 typically contains alphanumeric order/tracking numbers
        processTrackingNumber(barcode.getText());
        break;
    default:
        logger.warning("Unexpected barcode type: " + barcode.getEncodeType());
}
```

### 5. Probar con documentos del mundo real

No te limites a PDFs de muestra perfectos. Usa documentos reales de tu entorno de producción:
- Facturas escaneadas con manchas de café  
- Etiquetas de envío faxadas con ruido  
- Fotos de baja resolución tomadas con móvil y convertidas a PDF  

Esto revela casos límite que no aparecen en demos.

## Preguntas frecuentes

**P: ¿Puedo leer PDFs con código QR sin una licencia?**  
R: Una prueba gratuita te permite leer PDFs con código QR para evaluación, pero se requiere una licencia comercial para despliegues en producción.

**P: ¿La API admite PDFs protegidos con contraseña?**  
R: Sí. Puedes pasar la contraseña al crear el objeto `Signature`: `new Signature(filePath, "password")`.

**P: ¿Cómo mejoro la detección en escaneos de baja resolución?**  
R: Aumenta la DPI del escaneo original (mínimo 200 DPI) y considera filtrar por tipo de código de barras para reducir falsos positivos.

**P: ¿La búsqueda es segura para hilos en procesamiento paralelo?**  
R: Cada hilo debe usar su propia instancia `Signature`. La API es segura para hilos cuando se usa de esta manera.

**P: ¿Con qué versión de GroupDocs.Signature se probó este tutorial?**  
R: El código se validó con GroupDocs.Signature 23.12.

## Conclusión

Acabas de aprender a **leer PDF con código QR** usando Java y la API GroupDocs.Signature. Esto es lo que cubrimos:

✅ **Configuración** – Añadir GroupDocs.Signature al proyecto y opciones de licencia  
✅ **Implementación** – Código completo para buscar, extraer y procesar datos de códigos de barras  
✅ **Tipos de códigos de barras** – Entender qué formatos son compatibles (1D y 2D)  
✅ **Casos de uso reales** – Procesamiento de facturas, gestión de inventario, autenticación de documentos, registros de salud  
✅ **Solución de problemas** – Resolver errores comunes como problemas de memoria y falsos positivos  
✅ **Rendimiento** – Optimizar búsquedas para procesamiento a gran escala  

La API GroupDocs.Signature maneja la complejidad del análisis de PDFs y la detección de códigos de barras, permitiéndote centrarte en la lógica de negocio. Ya sea que automatices el procesamiento de facturas, verifiques etiquetas de envío o extraigas datos de inventario, ahora cuentas con una solución robusta.

---

**Última actualización:** 2026-03-01  
**Probado con:** GroupDocs.Signature 23.12  
**Autor:** GroupDocs