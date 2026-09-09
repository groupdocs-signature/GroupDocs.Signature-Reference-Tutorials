---
categories:
- Java PDF Processing
date: '2026-07-20'
description: Aprenda cómo crear una firma de barcode en documentos PDF usando Java
  y GroupDocs.Signature. Tutorial paso a paso con ejemplos de código y mejores prácticas.
keywords:
- create barcode signature
- how to add barcode
- generate code128 barcode
- add barcode pdf
- tamper evident barcode
lastmod: '2026-07-20'
linktitle: Crear firma de barcode Java
og_description: Crear firma de barcode en PDF usando Java con GroupDocs.Signature.
  Aprenda paso a paso cómo agregar códigos de barras Code128, posicionarlos y asegurar
  documentos.
og_image_alt: 'Developer guide: Create barcode signature in PDF using Java and GroupDocs'
og_title: Crear firma de barcode en PDF usando Java – Guía completa
schemas:
- author: GroupDocs
  dateModified: '2026-07-20'
  description: Learn how to create barcode signature in PDF documents using Java and
    GroupDocs.Signature. Step-by-step tutorial with code examples and best practices.
  headline: How to Create Barcode Signature in PDF using Java
  type: TechArticle
- description: Learn how to create barcode signature in PDF documents using Java and
    GroupDocs.Signature. Step-by-step tutorial with code examples and best practices.
  name: How to Create Barcode Signature in PDF using Java
  steps:
  - name: Initialize the Signature object
    text: '**Definition anchor:** The `Signature` class is GroupDocs.Signature''s
      entry point for loading, modifying, and saving PDF documents. First, you need
      to tell GroupDocs which PDF you''re working with: **What''s happening here:**
      The `Signature` object loads your PDF into memory and prepares it for modifi'
  - name: Configure your barcode options (How to add barcode)
    text: '**Definition anchor:** `BarcodeSignOptions` encapsulates all settings required
      to render a barcode inside a PDF. Now let''s create the barcode signature with
      your data: - `"12345678"` is your barcode data — this could be an order ID,
      certificate number, or any identifier you need. - `Code128` is the '
  - name: Position your barcode (How to sign PDF with barcode)
    text: '**Definition anchor:** `SignatureOptions` provides layout properties such
      as page number, size, and alignment. Here''s where GroupDocs really shines —
      percentage‑based positioning means your barcode looks good on any PDF size:
      **Why percentages matter:** Imagine you''re signing both A4 documents and l'
  - name: Sign and save your document (How to add barcode pdf)
    text: 'Time to actually apply the signature and save your work: **Important note:**
      The output directory must exist before you run this code. GroupDocs won''t create
      nested directories for you, so create them first or handle that in your code:
      **What if something goes wrong?** Wrap this in a try‑catch block'
  type: HowTo
- questions:
  - answer: Yes! Call `signature.sign()` multiple times with different `BarcodeSignOptions`
      for each barcode type. Just ensure they don’t overlap.
    question: Can I use different barcode types in the same PDF?
  - answer: Code128 handles most ASCII characters fine. For Unicode or complex data,
      switch to QR codes—they support UTF‑8 encoding.
    question: How do I handle barcodes that contain special characters?
  - answer: Technically up to 128 characters, but readability drops significantly
      above 30‑40 characters. For larger payloads, use QR codes.
    question: What's the maximum data I can store in a Code128 barcode?
  - answer: Not noticeably—barcodes are vector graphics, typically adding only 5‑20
      KB per barcode depending on size and complexity.
    question: Will adding barcodes significantly increase my PDF file size?
  - answer: Yes! Use `options.setRotationAngle(90)` to rotate your barcode, which
      is handy for margin placement.
    question: Can I rotate barcodes or place them vertically?
  type: FAQPage
tags:
- pdf-signing
- barcode-signature
- document-security
- groupdocs
- java
- pdf
title: Cómo crear una firma de barcode en PDF usando Java
type: docs
url: /es/java/barcode-signatures/java-pdf-signing-barcode-groupdocs/
weight: 1
---

# Cómo crear una firma de código de barras en PDF usando Java

En este tutorial, aprenderás cómo **crear una firma de código de barras** en archivos PDF usando Java y GroupDocs.Signature. Las firmas de código de barras incrustan identificadores legibles por máquina que son tanto a prueba de manipulaciones como fáciles de escanear —perfectas para contratos, certificados, facturas y cualquier documento que necesite una verificación fiable.

## Respuestas rápidas
- **¿Qué es una firma de código de barras?** Un código de barras incrustado en un PDF que almacena datos estructurados y puede ser leído por escáneres o software.  
- **¿Qué tipo de código de barras se recomienda?** Code128, porque maneja datos alfanuméricos de forma compacta.  
- **¿Necesito una licencia?** Una prueba gratuita funciona para pruebas; se requiere una licencia completa para producción.  
- **¿Puedo posicionar el código de barras en cualquier tamaño de página?** Sí—utiliza posicionamiento basado en porcentajes para escalado automático.  
- **¿El código de barras es vectorial?** Sí, solo añade unos pocos kilobytes al PDF y permanece nítido a cualquier resolución.  

## ¿Qué es una firma de código de barras?
Una firma de código de barras es un código de barras vectorial incrustado directamente en una página PDF, actuando tanto como un elemento visual como una firma criptográfica que puede validarse posteriormente. Almacena datos estructurados, como identificadores o marcas de tiempo, y garantiza la integridad del documento mientras proporciona una referencia legible por máquina.

## Por qué las firmas de código de barras son importantes para tus PDFs
Las firmas de código de barras proporcionan a los PDFs un identificador compacto y legible por máquina que puede escanearse al instante, eliminando la entrada manual de datos y reduciendo errores. Como están incrustados como gráficos vectoriales, permanecen nítidos a cualquier resolución y añaden solo unos pocos kilobytes al archivo. Esta combinación de legibilidad, evidencia de manipulación y tamaño mínimo los hace ideales para contratos, facturas, certificados y cualquier documento que requiera una verificación fiable.

Aquí hay un desafío que probablemente hayas enfrentado: necesitas añadir identificadores únicos a los PDFs que sean tanto legibles por máquina como a prueba de manipulaciones. Tal vez estés trabajando en un sistema de gestión documental, procesando certificados o manejando contratos que necesiten verificación más adelante.

Ahí es donde las firmas de código de barras resultan útiles. A diferencia de los sellos de texto simples, los códigos de barras te permiten incrustar datos estructurados que los escáneres (y tu software) pueden leer al instante. Además, cuando los combinas con la firma de PDF mediante GroupDocs.Signature para Java, obtienes una forma poderosa de rastrear y verificar documentos sin añadir búsquedas complejas en bases de datos.

En esta guía, aprenderás exactamente cómo implementar firmas de código de barras en tus PDFs Java — desde la configuración básica hasta código listo para producción con posicionamiento flexible. Ya sea que estés construyendo un sistema de facturación, un generador de certificados o una plataforma de gestión de contratos, tendrás todo lo que necesitas al final.

**Lo que dominarás:**
- Configurar GroupDocs.Signature para Java en minutos  
- Crear firmas de código de barras Code128 (y por qué a menudo son la mejor opción)  
- Posicionar códigos de barras usando diseños basados en porcentajes que funcionan en cualquier tamaño de PDF  
- Evitar errores comunes que tropiezan a los desarrolladores  
- Probar tu implementación correctamente  

## Cómo crear una firma de código de barras en Java
Crear una firma de código de barras en Java implica cargar el PDF objetivo, configurar las opciones del código de barras como datos, tipo, tamaño y posición, y luego aplicar la firma para generar un nuevo documento. GroupDocs.Signature se encarga del renderizado y del enlace criptográfico, por lo que solo necesitas proporcionar los parámetros deseados y gestionar las rutas de archivo.

## Requisitos previos y lista de verificación del entorno
Antes de sumergirte, verifica que tienes los siguientes elementos listos:

- **Java Development Kit (JDK) 8 o superior** – requerido para todas las bibliotecas Java de GroupDocs.  
- **Maven o Gradle** – para gestionar la dependencia de GroupDocs.Signature.  
- **Un IDE** como IntelliJ IDEA, Eclipse o VS Code con extensiones Java.  
- **GroupDocs.Signature para Java** (se recomienda la versión 23.12 o superior).  
- **Conocimientos básicos de Java** – deberías estar cómodo creando clases, manejando excepciones y trabajando con E/S de archivos.  

## Configuración de GroupDocs.Signature en tu proyecto
Obtener la biblioteca en tu proyecto es sencillo. Elige tu herramienta de compilación:

**Para usuarios de Maven**, agrega esta dependencia a tu `pom.xml`:

```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

**¿Usas Gradle?** Añade esta línea a tu `build.gradle`:

```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

**¿Prefieres configuración manual?** Descarga el JAR directamente de [lanzamientos de GroupDocs.Signature para Java](https://releases.groupdocs.com/signature/java/) y añádelo a tu classpath.

### Obtención de tu licencia
Antes de pasar a producción completa, querrás gestionar la licencia:

- **Prueba gratuita:** Perfecta para pruebas — obténla desde el sitio web de GroupDocs para explorar las funciones principales.  
- **Licencia temporal:** ¿Necesitas más tiempo para evaluar? Solicita una licencia temporal de 30 días.  
- **Licencia completa:** ¿Listo para producción? Compra una licencia para uso ilimitado.  

Aquí tienes una rápida comprobación de sanidad para asegurarte de que todo funciona:

```java
Signature signature = new Signature("sample.pdf");
System.out.println("Signature object created successfully.");
```

¡Si eso se ejecuta sin errores, estás listo!

## Cómo crear una firma de código de barras en Java
Ahora viene la parte divertida — firmemos un PDF con un código de barras. Dividiremos esto en pasos pequeños para que comprendas exactamente lo que ocurre en cada etapa.

### Paso 1: Inicializar el objeto Signature
**Definición:** La clase `Signature` es el punto de entrada de GroupDocs.Signature para cargar, modificar y guardar documentos PDF.

Primero, necesitas indicar a GroupDocs qué PDF estás utilizando:

```java
Signature signature = new Signature("input.pdf");
```

**Qué está sucediendo:** El objeto `Signature` carga tu PDF en memoria y lo prepara para modificaciones. Asegúrate de que la ruta del archivo sea correcta — un error común es usar barras invertidas en Windows sin escaparlas (usa `\\` o simplemente barras normales, que funcionan multiplataforma).

### Paso 2: Configurar tus opciones de código de barras (Cómo añadir código de barras)
**Definición:** `BarcodeSignOptions` encapsula todas las configuraciones necesarias para renderizar un código de barras dentro de un PDF.

Ahora creemos la firma de código de barras con tus datos:

```java
BarcodeSignOptions options = new BarcodeSignOptions("12345678");
options.setEncodeType(BarcodeEncodeType.Code128);
```

- `"12345678"` es tu dato de código de barras — puede ser un ID de pedido, número de certificado o cualquier identificador que necesites.  
- `Code128` es el tipo de codificación (más sobre cómo elegir el tipo correcto a continuación).  

**Consejo profesional:** Code128 puede manejar tanto números como letras, lo que lo hace versátil para la mayoría de los casos. Si solo necesitas números, `Code39` podría ser más simple, pero Code128 te brinda más flexibilidad.

### Paso 3: Posicionar tu código de barras (Cómo firmar PDF con código de barras)
**Definición:** `SignatureOptions` proporciona propiedades de diseño como número de página, tamaño y alineación.

Aquí es donde GroupDocs realmente brilla — el posicionamiento basado en porcentajes hace que tu código de barras se vea bien en cualquier tamaño de PDF:

```java
options.setLeft(10);   // 10% from the left edge
options.setTop(90);    // 90% from the bottom edge (near the footer)
options.setWidth(30);  // 30% of page width
options.setHeight(10); // 10% of page height
options.setPageNumber(1);
```

**Por qué importan los porcentajes:** Imagina que firmas documentos A4 y formularios de tamaño legal. Con el posicionamiento porcentual, tu código de barras se escala automáticamente para verse consistente en ambos. Usar valores de píxeles fijos haría que tu código de barras sea demasiado pequeño en documentos grandes o demasiado grande en documentos pequeños.

**Ejemplo del mundo real:** En una página A4 (595 × 842 puntos), un código de barras de ancho del 30 % será ~180 puntos de ancho. En una página legal (612 × 1008 puntos), será ~184 puntos de ancho — automáticamente proporcional.

### Paso 4: Firmar y guardar tu documento (Cómo añadir código de barras al PDF)
Es hora de aplicar realmente la firma y guardar tu trabajo:

```java
signature.sign(outputPath, options);
```

**Nota importante:** El directorio de salida debe existir antes de ejecutar este código. GroupDocs no creará directorios anidados por ti, así que créalos primero o maneja eso en tu código:

```java
new File("output").mkdirs();
```

**¿Qué pasa si algo sale mal?** Envuelve esto en un bloque try‑catch:

```java
try {
    signature.sign("signed.pdf", options);
} catch (Exception e) {
    e.printStackTrace();
}
```

## Elegir el tipo de código de barras adecuado para tus necesidades (generar código de barras code128)
GroupDocs admite varios formatos de código de barras, y elegir el correcto es importante. Aquí hay una comparación práctica:

**Code128 (Nuestra elección predeterminada):**
- **Mejor para:** Datos alfanuméricos mixtos (IDs como "INV2024-001")  
- **Capacidad:** Hasta 128 caracteres ASCII  
- **Por qué gana:** Compacto, ampliamente soportado, maneja tanto letras como números  
- **Usar cuando:** Necesitas flexibilidad y no sabes qué tipo de datos codificarás  

**Code39:**
- **Mejor para:** Códigos alfanuméricos simples  
- **Capacidad:** 43 caracteres (A‑Z, 0‑9 y algunos símbolos)  
- **Por qué considerarlo:** Los escáneres más antiguos a menudo lo soportan mejor  
- **Usar cuando:** Trabajas con sistemas heredados o cuando la simplicidad importa más que la densidad de datos  

**QR Code:**
- **Mejor para:** Grandes cantidades de datos (URLs, payloads JSON)  
- **Capacidad:** Hasta 3 KB de datos  
- **Por qué es potente:** Puede almacenar estructuras de datos complejas, corrección de errores incorporada  
- **Usar cuando:** Necesitas incrustar datos estructurados o URLs  

**EAN/UPC:**
- **Mejor para:** Identificación de productos  
- **Capacidad:** Códigos numéricos de longitud fija (8‑13 dígitos)  
- **Usar cuando:** Trabajas con sistemas de venta minorista o inventario  

**Guía rápida de decisión:**
- ¿Necesitas letras y números? → Code128  
- ¿Solo números, mantenerlo simple? → Code39  
- ¿Muchos datos o URLs? → QR Code  
- ¿Códigos de venta minorista/producto? → EAN/UPC  

## Errores comunes y cómo evitarlos (código de barras a prueba de manipulaciones)
Aquí están los problemas que los desarrolladores encuentran con mayor frecuencia (para que no tengas que hacerlo):

### Problema 1: El posicionamiento del código de barras se ve incorrecto
**Síntoma:** Tu código de barras aparece en ubicaciones inesperadas o se corta.  
**Causas comunes:**
- Uso de valores de píxeles en diferentes tamaños de página  
- Olvidar que las coordenadas PDF comienzan desde la esquina inferior izquierda, no superior izquierda  
- Márgenes que empujan el contenido fuera del área visible  

**Solución:** Siempre usa posicionamiento basado en porcentajes para consistencia:

```java
options.setLeft(5);
options.setTop(95);
options.setWidth(40);
options.setHeight(12);
```

### Problema 2: El texto del código de barras es ilegible
**Síntoma:** El texto codificado se muestra pero los escáneres no pueden leerlo.  
**Causas:**
- Código de barras demasiado pequeño para la cantidad de datos  
- Tipo de codificación incorrecto para tus datos  
- Bajo contraste entre barras y fondo  

**Solución:** Ajusta el tamaño de tu código de barras a la longitud de tus datos. Para Code128 con 10‑15 caracteres, apunta a al menos el 8‑10 % del ancho de la página.

### Problema 3: Excepciones de ruta de archivo
**Síntoma:** `FileNotFoundException` u otros errores similares.  
**Causas:**
- Rutas de Windows codificadas con barras invertidas simples  
- El directorio de salida no existe  
- Problemas de permisos de archivo  

**Solución:** Usa barras normales (funcionan en todas partes) y crea los directorios primero:

```java
Path output = Paths.get("output/signed.pdf");
Files.createDirectories(output.getParent());
```

### Problema 4: Problemas de memoria con PDFs grandes
**Síntoma:** Errores de falta de memoria al procesar documentos grandes.  
**Solución:** Cierra el objeto `Signature` cuando termines para liberar recursos:

```java
signature.close();
```

## Probando tu implementación de código de barras
Antes de desplegar, asegúrate de que tus códigos de barras realmente funcionen. Aquí tienes una lista práctica de verificación:

### 1. Prueba de inspección visual
Abre tu PDF firmado y verifica:
- ¿El código de barras es visible y está correctamente posicionado?  
- ¿Se ve nítido (no borroso o pixelado)?  
- ¿Hay suficiente espacio blanco alrededor?

### 2. Prueba de escaneo
Usa una aplicación escáner de códigos de barras en tu teléfono (como “Barcode Scanner” o “QR & Barcode Reader”) para verificar:
- El escáner puede leer tu código de barras  
- Los datos decodificados coinciden con lo que codificaste  
- Funciona desde diferentes ángulos y distancias

### 3. Prueba multiplataforma
Abre tu PDF en diferentes dispositivos:
- Windows (Adobe Reader, Chrome)  
- Mac (Preview, Chrome)  
- Dispositivos móviles (iOS, Android)  

Asegúrate de que el código de barras se renderice correctamente en todas partes.

### 4. Código de prueba automatizada
Aquí tienes una prueba simple que puedes ejecutar:

```java
Signature testSignature = new Signature("signed.pdf");
List<BarcodeSignature> signatures = testSignature.search(BarcodeSignature.class);
if (signatures.size() > 0) {
    System.out.println("Barcode found: " + signatures.get(0).getText());
}
```

## Casos de uso reales para firmas de código de barras
Veamos dónde esta técnica realmente brilla en sistemas de producción:

### 1. Generación y verificación de certificados
**Escenario:** Estás construyendo una plataforma de capacitación que emite certificados de finalización.  
**Implementación:** Genera un ID de certificado único (p.ej., “CERT‑2024‑00123”) e incrústalo como un código de barras Code128 en la esquina inferior derecha. Escanear el código de barras permite que tu API recupere los detalles del certificado al instante, eliminando la entrada manual de datos.

### 2. Sistemas de seguimiento de facturas
**Escenario:** Tu empresa procesa miles de facturas mensualmente.  
**Implementación:** Añade el número de factura y la fecha de vencimiento como un código QR posicionado donde el equipo de escaneo pueda leerlo fácilmente. Los sistemas de clasificación automatizados pueden dirigir las facturas sin intervención humana, reduciendo el tiempo de procesamiento de horas a minutos.

### 3. Gestión de contratos legales
**Escenario:** Un bufete de abogados necesita rastrear versiones y enmiendas de contratos.  
**Implementación:** Cada versión del contrato obtiene un identificador de código de barras único que incluye ID del contrato, número de versión y fecha de firma. Escanear durante auditorías recupera automáticamente el historial completo de versiones.

### 4. Seguridad de registros médicos
**Escenario:** Un hospital quiere prevenir el acceso no autorizado a los registros.  
**Implementación:** Incrusta el ID del paciente y la marca de tiempo de creación del registro en un código de barras. Solo los dispositivos autenticados pueden decodificar y acceder al registro completo, y cada escaneo crea un registro de auditoría para cumplimiento.

## Consejos de optimización de rendimiento (seguridad de documentos Java)
Cuando firmas muchos PDFs, el rendimiento importa. Aquí tienes algunos consejos para mantener todo funcionando sin problemas:

### Estrategia de procesamiento por lotes
En lugar de firmar un documento a la vez, procesa por lotes:

```java
for (String filePath : pdfList) {
    Signature batchSignature = new Signature(filePath);
    batchSignature.sign(outputPath, options);
    batchSignature.close();
}
```

**Por qué ayuda esto:** Reutilizar el objeto de opciones y cerrar adecuadamente los recursos previene fugas de memoria.

### Gestión de memoria para PDFs grandes
- Para PDFs mayores de 50 MB:
  - Procésalos secuencialmente en lugar de cargar varios a la vez.  
  - Usa try‑with‑resources para asegurar la limpieza.  
  - Monitorea el tamaño del heap y ajusta los parámetros JVM si es necesario: `-Xmx2g`.

### Caché de códigos de barras de uso frecuente
Si firmas muchos documentos con el mismo código de barras, almacena en caché la instancia `BarcodeSignOptions`:

```java
BarcodeSignOptions cachedOptions = new BarcodeSignOptions("STATIC_ID");
cachedOptions.setEncodeType(BarcodeEncodeType.Code128);
```

## Cuándo usar firmas de código de barras (y cuándo no)
**Escenarios perfectos:**
- Necesitas identificadores de documentos legibles por máquina.  
- Los documentos serán escaneados o procesados automáticamente.  
- Quieres seguimiento a prueba de manipulaciones sin certificados digitales.  
- Se requiere integración con la infraestructura de códigos de barras existente.  

**No es ideal cuando:**
- Necesitas firmas digitales legalmente vinculantes (usa certificados digitales en su lugar).  
- Los documentos solo serán vistos por humanos (una simple marca de agua de texto puede ser suficiente).  
- Trabajas con documentos extremadamente pequeños donde un código de barras dominaría la página.  
- Los requisitos de seguridad exigen encriptación—los códigos de barras son visibles y escaneables por cualquiera.  

**¿Puedes combinar enfoques?** ¡Absolutamente! Muchos sistemas usan tanto firmas de código de barras para seguimiento como firmas digitales para validez legal.

## Preguntas frecuentes
**P: ¿Puedo usar diferentes tipos de código de barras en el mismo PDF?**  
R: ¡Sí! Llama a `signature.sign()` varias veces con diferentes `BarcodeSignOptions` para cada tipo de código de barras. Solo asegúrate de que no se superpongan.

**P: ¿Cómo manejo códigos de barras que contienen caracteres especiales?**  
R: Code128 maneja la mayoría de los caracteres ASCII sin problemas. Para Unicode o datos complejos, cambia a códigos QR—soportan codificación UTF‑8.

**P: ¿Cuál es el máximo de datos que puedo almacenar en un código de barras Code128?**  
R: Técnicamente hasta 128 caracteres, pero la legibilidad disminuye significativamente por encima de 30‑40 caracteres. Para cargas mayores, usa códigos QR.

**P: ¿Añadir códigos de barras aumentará significativamente el tamaño de mi archivo PDF?**  
R: No de forma notable—los códigos de barras son gráficos vectoriales, típicamente añaden solo 5‑20 KB por código de barras según el tamaño y la complejidad.

**P: ¿Puedo rotar los códigos de barras o colocarlos verticalmente?**  
R: ¡Sí! Usa `options.setRotationAngle(90)` para rotar tu código de barras, lo cual es útil para colocarlo en el margen.

**P: ¿Cómo hago que los códigos de barras aparezcan en cada página de un PDF de varias páginas?**  
R: Itera a través de las páginas y aplica la firma a cada una. Revisa la clase `PagesSetup` en la documentación de GroupDocs para controlar qué páginas se firman.

**P: ¿Qué pasa si mi escáner de códigos de barras no puede leer el código generado?**  
R: Primero, verifica que el escáner soporte el tipo de código de barras elegido. Luego aumenta el tamaño del código—la mayoría de los problemas de escaneo provienen de barras demasiado pequeñas. Apunta a al menos 1 pulgada (2.54 cm) de ancho para lecturas fiables.

## Recursos adicionales
**Documentación:**  
- [Documentación de GroupDocs.Signature para Java](https://docs.groupdocs.com/signature/java/)  
- [Guía de referencia API](https://reference.groupdocs.com/signature/java/)  

**Descargas y licencias:**  
- [Descargar última versión](https://releases.groupdocs.com/signature/java/)  
- [Acceso a prueba gratuita](https://releases.groupdocs.com/signature/java/)  
- [Obtener licencia temporal](https://purchase.groupdocs.com/temporary-license/)  
- [Comprar licencia completa](https://purchase.groupdocs.com/buy)  

**Comunidad y soporte:**  
- [Foro de soporte](https://forum.groupdocs.com/c/signature/) - Comunidad activa con ingenieros de GroupDocs  

**Última actualización:** 2026-07-20  
**Probado con:** GroupDocs.Signature 23.12 (Java)  
**Autor:** GroupDocs

```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

```java
import com.groupdocs.signature.Signature;

public class QuickTest {
    public static void main(String[] args) {
        try {
            Signature signature = new Signature("test-document.pdf");
            System.out.println("GroupDocs.Signature is ready to go!");
        } catch (Exception e) {
            System.err.println("Setup issue: " + e.getMessage());
        }
    }
}
```

```java
String filePath = "YOUR_DOCUMENT_DIRECTORY/sample.pdf";
Signature signature = new Signature(filePath);
```

```java
import com.groupdocs.signature.options.sign.BarcodeSignOptions;
import com.groupdocs.signature.domain.barcodes.BarcodeTypes;

BarcodeSignOptions options = new BarcodeSignOptions("12345678");
options.setEncodeType(BarcodeTypes.Code128);
```

```java
import com.groupdocs.signature.domain.enums.MeasureType;
import com.groupdocs.signature.domain.Padding;

// Use percentages instead of fixed pixels
options.setLocationMeasureType(MeasureType.Percents);
options.setLeft(5);  // 5% from the left edge
options.setTop(5);   // 5% from the top

// Size it proportionally too
options.setSizeMeasureType(MeasureType.Percents);
options.setWidth(10);  // 10% of page width
options.setHeight(5);  // 5% of page height

// Add some breathing room with margins
Padding margins = new Padding();
margins.setLeft(1);
margins.setTop(1);
margins.setRight(1);
options.setMargin(margins);
```

```java
String outputFilePath = "YOUR_OUTPUT_DIRECTORY/SignWithPercents/sample_signed.pdf";
signature.sign(outputFilePath, options);
```

```java
Path outputPath = Paths.get(outputFilePath);
Files.createDirectories(outputPath.getParent());
signature.sign(outputFilePath, options);
```

```java
try {
    signature.sign(outputFilePath, options);
    System.out.println("PDF signed successfully at: " + outputFilePath);
} catch (Exception e) {
    System.err.println("Signing failed: " + e.getMessage());
    e.printStackTrace();
}
```

```java
options.setLocationMeasureType(MeasureType.Percents);
options.setLeft(5);  // 5% from left works on any page width
```

```java
options.setWidth(10);  // Give it room to breathe
options.setHeight(5);  // Maintain proper aspect ratio
```

```java
String filePath = "documents/sample.pdf";  // Works on Windows, Mac, Linux
Files.createDirectories(Paths.get("output/signed"));
```

```java
try (Signature signature = new Signature(filePath)) {
    signature.sign(outputFilePath, options);
} // Automatically closes and releases memory
```

```java
import org.junit.Test;
import static org.junit.Assert.*;

public class BarcodeSignatureTest {
    
    @Test
    public void testBarcodeSigning() {
        String testPdf = "test-data/sample.pdf";
        String output = "test-output/signed.pdf";
        
        try (Signature signature = new Signature(testPdf)) {
            BarcodeSignOptions options = new BarcodeSignOptions("TEST123");
            options.setEncodeType(BarcodeTypes.Code128);
            
            signature.sign(output, options);
            
            // Verify output file exists
            assertTrue(new File(output).exists());
            
            // Verify file size increased (signature was added)
            long originalSize = new File(testPdf).length();
            long signedSize = new File(output).length();
            assertTrue(signedSize > originalSize);
            
        } catch (Exception e) {
            fail("Signing should not throw exception: " + e.getMessage());
        }
    }
}
```

```java
List<String> pdfFiles = Arrays.asList("doc1.pdf", "doc2.pdf", "doc3.pdf");

for (String pdfFile : pdfFiles) {
    try (Signature signature = new Signature(pdfFile)) {
        BarcodeSignOptions options = createBarcodeOptions(); // Reuse options
        signature.sign(getOutputPath(pdfFile), options);
    }
}
```

```java
// Create options once, reuse many times
BarcodeSignOptions templateOptions = createStandardBarcodeOptions();

// For each document, clone and customize
BarcodeSignOptions documentOptions = templateOptions.clone();
documentOptions.setText(uniqueDocumentId);
```

## Tutoriales relacionados
- [Tutorial de firma de código de barras Java - Añadir, verificar y gestionar códigos de barras en PDFs](/signature/java/barcode-signatures/)
- [Crear firma de código de barras en Java – Actualizar códigos de barras PDF](/signature/java/barcode-signatures/java-groupdocs-signature-barcode-initialize-update/)
- [Cómo leer PDF con código QR usando Java y GroupDocs.Signature](/signature/java/barcode-signatures/java-pdf-barcode-search-groupdocs-signature-api/)