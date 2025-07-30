---
"description": "Domine la verificación de firmas de texto en aplicaciones .NET con GroupDocs.Signature. Guía de implementación paso a paso con ejemplos de código completos y prácticas recomendadas."
"linktitle": "Verificar texto"
"second_title": "API .NET de GroupDocs.Signature"
"title": "Verificar firmas de texto en documentos"
"url": "/es/net/verify-operations/verify-text/"
"weight": 13
---

## Introducción

Las firmas de texto, aunque suelen ser más sencillas que las firmas digitales o electrónicas, desempeñan un papel crucial en la gestión y verificación de documentos. Ya sean marcas de agua, texto de pie de página o patrones de contenido específicos, validar la presencia e integridad de las firmas de texto es un aspecto importante de los procesos de verificación de documentos.

GroupDocs.Signature para .NET ofrece una potente API para verificar firmas de texto en documentos en una amplia gama de formatos. Este completo tutorial le guiará en la implementación de la función de verificación de texto en sus aplicaciones .NET, garantizando así la integridad y autenticidad de sus documentos.

## Prerrequisitos

Antes de implementar la funcionalidad de verificación de texto, asegúrese de tener los siguientes requisitos previos:

1. GroupDocs.Signature para .NET: Descargue e instale la biblioteca desde el [página de descarga](https://releases.groupdocs.com/signature/net/).
2. Entorno de desarrollo .NET: Visual Studio o cualquier entorno de desarrollo .NET compatible.
3. Conocimientos básicos: Familiaridad con la programación en C# y conceptos del marco .NET.
4. Documento de prueba: un documento que contiene firmas de texto para fines de verificación.

## Importar espacios de nombres requeridos

Comience importando los espacios de nombres necesarios para acceder a la funcionalidad GroupDocs.Signature:

```csharp
using System;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

Dividamos el proceso de verificación de texto en pasos claros y manejables:

## Paso 1: Especifique la ruta del documento

```csharp
// Ruta al documento que contiene las firmas de texto
string filePath = "sample_multiple_signatures.docx";
```

Asegúrese de reemplazar la ruta de ejemplo con la ruta real a su documento que contiene las firmas de texto.

## Paso 2: Inicializar el objeto de firma

```csharp
// Cree una instancia de la clase Signature pasando la ruta del documento
using (Signature signature = new Signature(filePath))
{
    // El código de verificación se implementará aquí
}
```

La clase Signature es el punto de entrada principal para todas las operaciones en la API GroupDocs.Signature.

## Paso 3: Configurar las opciones de verificación de texto

```csharp
// Definir opciones de verificación de texto
TextVerifyOptions options = new TextVerifyOptions()
{
    AllPages = true,                               // Revisar todas las páginas del documento
    SignatureImplementation = TextSignatureImplementation.Native,
    Text = "signature",                            // Texto a verificar
    MatchType = TextMatchType.Contains             // Especificar criterios de coincidencia
};
```

Las opciones de verificación le permiten definir criterios específicos para el proceso de verificación:
- `AllPages`:Establecer como verdadero para comprobar todas las páginas del documento
- `SignatureImplementation`:Especifique cómo se implementa el texto (nativo o pegatina)
- `Text`:El contenido del texto que debe coincidir dentro del documento
- `MatchType`:El método para la coincidencia de texto (Contiene, Exacto, Comienza con, etc.)

## Paso 4: Ejecutar el proceso de verificación

```csharp
// Realizar verificación
VerificationResult result = signature.Verify(options);
```

Esto ejecuta el proceso de verificación según las opciones que haya especificado.

## Paso 5: Resultados de la verificación del proceso

```csharp
// Verifique el resultado de la verificación y procese según corresponda
if (result.IsValid)
{
    Console.WriteLine($"Document {filePath} contains valid text signatures!");
    
    // Mostrar información sobre firmas exitosas
    foreach (TextSignature textSignature in result.Succeeded)
    {
        Console.WriteLine($"\nFound valid text signature:");
        Console.WriteLine($"Text: {textSignature.Text}");
        Console.WriteLine($"Location: Page {textSignature.PageNumber}, {textSignature.Left}x{textSignature.Top}");
    }
}
else
{
    Console.WriteLine($"Document {filePath} failed verification process.");
    Console.WriteLine($"Number of failed signatures: {result.Failed.Count}");
}
```

Este código verifica si la verificación fue exitosa y proporciona información detallada sobre las firmas de texto que se verificaron.

## Ejemplo completo

A continuación se muestra un ejemplo completo que demuestra la verificación de la firma de texto:

```csharp
using System;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;

namespace GroupDocs.Signature.Examples
{
    class Program
    {
        static void Main(string[] args)
        {
            // Ruta del documento
            string filePath = "sample_multiple_signatures.docx";
            
            try
            {
                // Inicializar instancia de firma
                using (Signature signature = new Signature(filePath))
                {
                    // Configurar opciones de verificación
                    TextVerifyOptions options = new TextVerifyOptions()
                    {
                        AllPages = true,
                        SignatureImplementation = TextSignatureImplementation.Native,
                        Text = "signature",
                        MatchType = TextMatchType.Contains
                    };
                    
                    // Verificar firmas de documentos
                    VerificationResult result = signature.Verify(options);
                    
                    // Resultados de la verificación del proceso
                    if(result.IsValid)
                    {
                        Console.WriteLine($"\nDocument {filePath} was verified successfully!");
                        foreach (TextSignature item in result.Succeeded)
                        {
                            Console.WriteLine($"\nValid signature is found with text: {item.Text}");
                            Console.WriteLine($"Location: Page {item.PageNumber}, position {item.Left}x{item.Top}");
                        }
                    }
                    else
                    {
                        Console.WriteLine($"\nDocument {filePath} failed verification process.");
                    }
                }
            }
            catch (Exception ex)
            {
                Console.WriteLine($"Error: {ex.Message}");
            }
        }
    }
}
```

## Escenarios de verificación avanzada

GroupDocs.Signature proporciona opciones adicionales para escenarios de verificación más complejos:

### Uso de expresiones regulares para la verificación

Para una coincidencia de patrones más flexible, puede utilizar expresiones regulares:

```csharp
TextVerifyOptions options = new TextVerifyOptions()
{
    Text = "Invoice\\s+#\\d{5,6}",  // Coincidir con patrones como "Factura n.° 12345"
    MatchType = TextMatchType.Regex
};
```

### Verificación de texto en áreas específicas del documento

Puede restringir la verificación a áreas específicas del documento:

```csharp
TextVerifyOptions options = new TextVerifyOptions()
{
    AllPages = false,
    PageNumber = 1,  // Verificar solo en la primera página
    
    // Define el área a buscar (coordenadas en puntos)
    PagesSetup = new PagesSetup() 
    { 
        FirstPage = true,
        LastPage = false,
        OddPages = false,
        EvenPages = false 
    },
    
    // Área del rectángulo en milímetros
    Rectangle = new Rectangle(10, 10, 100, 30),
    
    Text = "Confidential"
};
```

### Verificación simultánea de múltiples patrones de texto

Puede crear múltiples opciones de verificación para comprobar diferentes patrones de texto:

```csharp
// Crear una lista de opciones de verificación
List<VerifyOptions> listOptions = new List<VerifyOptions>();

// Agregar la primera verificación de texto
listOptions.Add(new TextVerifyOptions()
{
    Text = "Confidential",
    MatchType = TextMatchType.Exact
});

// Agregar segunda verificación de texto
listOptions.Add(new TextVerifyOptions()
{
    Text = "Do not copy",
    MatchType = TextMatchType.Contains
});

// Verificar con múltiples opciones
VerificationResult result = signature.Verify(listOptions);
```

### Verificación de texto con apariencia específica

También puede verificar texto con características de formato específicas:

```csharp
TextVerifyOptions options = new TextVerifyOptions()
{
    Text = "APPROVED",
    MatchType = TextMatchType.Exact,
    
    // Verificar propiedades de apariencia específicas
    ForegroundColorRGB = System.Drawing.Color.Green,
    Font = new SignatureFont() { FontFamily = "Arial", FontSize = 12, Bold = true }
};
```

## Mejores prácticas para la verificación de texto

1. Elija los tipos de coincidencia adecuados: seleccione el tipo de coincidencia correcto (Contiene, Exacto, Expresión regular) según sus requisitos de verificación.
2. Optimizar el rendimiento: para documentos grandes, considere verificar páginas específicas en lugar de todo el documento.
3. Manejo de errores: implemente un manejo de errores adecuado para gestionar escenarios inesperados con elegancia.
4. Tenga en cuenta la distinción entre mayúsculas y minúsculas: tenga en cuenta la distinción entre mayúsculas y minúsculas al hacer coincidir texto, especialmente en verificaciones críticas.
5. Prueba exhaustiva: prueba la verificación con varios formatos de documentos y patrones de texto para garantizar la compatibilidad.

## Solución de problemas comunes

### Texto no detectado
- Compruebe si el formato o la codificación del texto están afectando la detección
- Asegúrese de que el texto esté realmente presente en el documento como texto normal (no como imagen)
- Pruebe diferentes criterios de coincidencia (Contiene en lugar de Exacto)

### Problemas de rendimiento
- Optimice la verificación dirigiéndose a páginas o áreas específicas
- Utilice patrones de texto más específicos para reducir los falsos positivos

### Fallos de verificación
- Comprueba si los espacios, caracteres especiales o el formato afectan la coincidencia
- Verifique que el texto no sea parte de una imagen escaneada (que requiere OCR)
- Asegúrese de que el documento no haya sido modificado desde que se agregó el texto

## Conclusión

La verificación de texto es un enfoque versátil y práctico para la autenticación de documentos, que puede utilizarse de forma independiente o en combinación con otros métodos de verificación. GroupDocs.Signature para .NET ofrece una API completa y fácil de usar para implementar una robusta funcionalidad de verificación de texto en sus aplicaciones .NET.

Siguiendo esta guía paso a paso, aprenderá a:
- Configurar e inicializar el proceso de verificación de texto
- Especificar varios criterios de verificación
- Procesar e interpretar los resultados de la verificación
- Implementar escenarios de verificación avanzados

Estas capacidades le permiten construir sistemas de procesamiento de documentos seguros y confiables que pueden verificar la autenticidad del texto en varios formatos de documentos.

## Preguntas frecuentes

### ¿Puede GroupDocs.Signature verificar texto en documentos escaneados?
GroupDocs.Signature está diseñado principalmente para la verificación digital de texto. Para documentos escaneados, primero deberá utilizar la tecnología OCR (Reconocimiento Óptico de Caracteres) para convertir las imágenes escaneadas a texto.

### ¿Qué formatos de documentos son compatibles con la verificación de texto?
GroupDocs.Signature admite una amplia gama de formatos de documentos, incluidos PDF, documentos de Word (DOC, DOCX), hojas de cálculo de Excel (XLS, XLSX), presentaciones de PowerPoint (PPT, PPTX), imágenes y más.

### ¿Puedo verificar el texto formateado (negrita, cursiva, fuentes específicas)?
Sí, GroupDocs.Signature ofrece opciones para verificar texto con características de formato específicas, incluida la familia de fuentes, el tamaño, el estilo (negrita, cursiva) y el color.

### ¿Es posible verificar texto en documentos protegidos con contraseña?
Sí, GroupDocs.Signature proporciona opciones para especificar contraseñas de documentos al abrir documentos protegidos para verificación.

### ¿Puedo verificar las marcas de agua y el texto de fondo?
Sí, GroupDocs.Signature puede verificar varios tipos de firmas de texto, incluidas marcas de agua y texto de fondo, dependiendo de cómo se implementaron en el documento.

### Recursos relacionados
* [Referencia de la API de GroupDocs.Signature](https://reference.groupdocs.com/signature/net/)
* [Descargas de GroupDocs.Signature](https://releases.groupdocs.com/signature/net/)
* [Ejemplos de código en GitHub](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
* [Documentación](https://docs.groupdocs.com/signature/net/)
* [Página del producto](https://products.groupdocs.com/signature/net/)
* [Artículos del blog](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
* [Foro de soporte](https://forum.groupdocs.com/c/signature/13)
* [Licencia temporal](https://purchase.groupdocs.com/temporary-license/)