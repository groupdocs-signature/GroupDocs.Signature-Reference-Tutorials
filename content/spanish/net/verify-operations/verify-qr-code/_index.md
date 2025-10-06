---
"description": "Aprenda a verificar códigos QR en documentos con GroupDocs.Signature para .NET. Guía completa con ejemplos de código y prácticas recomendadas para la autenticación de documentos."
"linktitle": "Verificar código QR"
"second_title": "API .NET de GroupDocs.Signature"
"title": "Verificar el código QR en los documentos"
"url": "/es/net/verify-operations/verify-qr-code/"
"weight": 12
type: docs
---
## Introducción

La seguridad de los documentos es un aspecto fundamental de las operaciones comerciales modernas. Los códigos QR se han convertido en un método cada vez más popular para incrustar información en documentos cuya autenticidad puede verificarse. GroupDocs.Signature para .NET ofrece una solución potente y flexible para verificar códigos QR incrustados en documentos en diversos formatos.

Este completo tutorial lo guiará a través del proceso de implementación de la verificación de código QR en sus aplicaciones .NET, garantizando que sus documentos mantengan su integridad y autenticidad.

## Prerrequisitos

Antes de implementar la funcionalidad de verificación del código QR, asegúrese de tener los siguientes requisitos previos:

1. GroupDocs.Signature para .NET: Descargue e instale la biblioteca desde el [página de descarga](https://releases.groupdocs.com/signature/net/).
2. Entorno de desarrollo: Visual Studio o cualquier entorno de desarrollo .NET compatible.
3. Documento de prueba: un documento que contiene firmas de código QR para fines de verificación.
4. Conocimientos básicos: Familiaridad con la programación en C# y conceptos del marco .NET.

## Importar espacios de nombres

Comience importando los espacios de nombres necesarios para acceder a la funcionalidad GroupDocs.Signature:

```csharp
using System;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

## Proceso de verificación de código QR paso a paso

Siga estos pasos detallados para verificar los códigos QR dentro de sus documentos:

### Paso 1: Especifique la ruta del documento

```csharp
// Proporcionar la ruta al documento que contiene las firmas del código QR
string filePath = "sample_multiple_signatures.docx";
```

Asegúrese de reemplazar la ruta de ejemplo con la ruta real a su documento.

### Paso 2: Inicializar el objeto de firma

```csharp
// Cree una instancia de Signature pasando la ruta del documento
using (Signature signature = new Signature(filePath))
{
    // El código de verificación se implementará aquí
}
```

La clase Signature es el punto de entrada principal para todas las operaciones en la API GroupDocs.Signature.

### Paso 3: Configurar las opciones de verificación del código QR

```csharp
// Definir las opciones de verificación del código QR
QrCodeVerifyOptions options = new QrCodeVerifyOptions()
{
    AllPages = true, // Revisar todas las páginas del documento
    Text = "John",   // Texto para verificar dentro del código QR
    MatchType = TextMatchType.Contains // Especifique los criterios de coincidencia de texto
};
```

Las opciones de verificación le permiten definir criterios específicos para el proceso de verificación:
- `AllPages`:Establezca en verdadero para comprobar todas las páginas del documento (comportamiento predeterminado)
- `Text`:El contenido del texto que debe coincidir con el código QR
- `MatchType`:El método para la coincidencia de texto (Contiene, Exacto, Comienza con, etc.)

### Paso 4: Ejecutar el proceso de verificación

```csharp
// Realizar verificación
VerificationResult result = signature.Verify(options);
```

Esto ejecuta el proceso de verificación según las opciones que haya especificado.

### Paso 5: Resultados de la verificación del proceso

```csharp
// Verifique el resultado de la verificación y procese según corresponda
if (result.IsValid)
{
    Console.WriteLine($"Document {filePath} contains valid QR code signature!");
    
    // Mostrar información sobre firmas exitosas
    foreach (QrCodeSignature signature in result.Succeeded)
    {
        Console.WriteLine($"Found valid QR Code signature with text: {signature.Text}");
        Console.WriteLine($"QR Code type: {signature.EncodeType.TypeName}");
        Console.WriteLine($"Location: Page {signature.PageNumber}, {signature.Left}x{signature.Top}");
    }
}
else
{
    Console.WriteLine($"Document {filePath} failed verification process.");
    Console.WriteLine($"Number of failed signatures: {result.Failed.Count}");
}
```

El manejo adecuado del resultado de la verificación permite que su aplicación tome las acciones apropiadas en función del resultado de la verificación.

## Ejemplo completo

A continuación se muestra un ejemplo completo y funcional que demuestra la verificación del código QR:

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
            
            // Inicializar instancia de firma
            using (Signature signature = new Signature(filePath))
            {
                // Configurar opciones de verificación
                QrCodeVerifyOptions options = new QrCodeVerifyOptions()
                {
                    AllPages = true,
                    Text = "John",
                    MatchType = TextMatchType.Contains
                };
                
                // Verificar firmas de documentos
                VerificationResult result = signature.Verify(options);
                
                // Resultados de la verificación del proceso
                if (result.IsValid)
                {
                    Console.WriteLine($"Document {filePath} contains valid QR code signature!");
                    
                    foreach (QrCodeSignature qrSignature in result.Succeeded)
                    {
                        Console.WriteLine($"Found valid QR Code with text: {qrSignature.Text}");
                    }
                }
                else
                {
                    Console.WriteLine($"Document {filePath} failed verification process.");
                }
            }
        }
    }
}
```

## Opciones de verificación avanzadas

GroupDocs.Signature proporciona opciones adicionales para escenarios de verificación más complejos:

### Verificación de tipos específicos de códigos QR

```csharp
QrCodeVerifyOptions options = new QrCodeVerifyOptions()
{
    EncodeType = QrCodeTypes.QR,  // Verificar únicamente códigos QR estándar
    Text = "Confidential",
    MatchType = TextMatchType.Exact
};
```

### Verificación en páginas específicas

```csharp
QrCodeVerifyOptions options = new QrCodeVerifyOptions()
{
    AllPages = false,
    PageNumber = 2,  // Verificar solo en la página 2
    Text = "Approved"
};
```

### Uso de expresiones regulares para la verificación

```csharp
QrCodeVerifyOptions options = new QrCodeVerifyOptions()
{
    Text = "INV-\\d{6}",  // Coincidir con los números de factura (por ejemplo, INV-123456)
    MatchType = TextMatchType.Regex
};
```

## Mejores prácticas para la verificación de códigos QR

1. Valide siempre las entradas: asegúrese de que las rutas de los documentos y los criterios de verificación sean válidos antes de procesarlos.
2. Implementar el manejo de errores: utilice bloques try-catch para manejar posibles excepciones durante la verificación.
3. Tenga en cuenta el rendimiento: para documentos grandes, considere verificar páginas específicas en lugar de todo el documento.
4. Resultados de la verificación de registros: mantener registros de los procesos de verificación para fines de auditoría.
5. Pruebe con varios formatos de documentos: asegúrese de que su verificación funcione en todos los formatos de documentos requeridos.

## Conclusión

Verificar códigos QR en documentos es esencial para garantizar su autenticidad e integridad. GroupDocs.Signature para .NET ofrece una API completa e intuitiva para implementar la verificación de códigos QR en sus aplicaciones .NET.

Siguiendo este tutorial, aprenderá a:
- Configurar e inicializar el proceso de verificación
- Especificar varios criterios de verificación
- Procesar e interpretar los resultados de la verificación
- Implementar opciones de verificación avanzadas

Este conocimiento le permitirá mejorar la seguridad y confiabilidad de sus sistemas de gestión de documentos.

## Preguntas frecuentes

### ¿Puede GroupDocs.Signature verificar múltiples códigos QR en un solo documento?
Sí, GroupDocs.Signature puede verificar varios códigos QR en un mismo documento. Los resultados de la verificación incluirán todos los códigos QR coincidentes.

### ¿Qué formatos de documentos son compatibles con la verificación del código QR?
GroupDocs.Signature admite una amplia gama de formatos de documentos, incluidos PDF, Word (DOC, DOCX), Excel (XLS, XLSX), PowerPoint (PPT, PPTX), imágenes y más.

### ¿Puedo verificar códigos QR con encriptación o formato específico?
Sí, GroupDocs.Signature ofrece opciones para verificar códigos QR con tipos de codificación y patrones de formato de contenido específicos.

### ¿Es posible verificar códigos QR creados por aplicaciones de terceros?
Sí, GroupDocs.Signature puede verificar códigos QR estándar generados por la mayoría de las aplicaciones, siempre que sigan los formatos de código QR estándar.

### ¿Cómo manejo los códigos QR que contienen datos binarios en lugar de texto?
GroupDocs.Signature proporciona opciones para verificar códigos QR con datos binarios a través de `BinaryData` propiedad de las opciones de verificación.

### Recursos relacionados
* [Referencia de la API de GroupDocs.Signature](https://reference.groupdocs.com/signature/net/)
* [Descargas de GroupDocs.Signature](https://releases.groupdocs.com/signature/net/)
* [Ejemplos de código en GitHub](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
* [Documentación](https://docs.groupdocs.com/signature/net/)
* [Página del producto](https://products.groupdocs.com/signature/net/)
* [Artículos del blog](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
* [Foro de soporte](https://forum.groupdocs.com/c/signature/13)
* [Licencia temporal](https://purchase.groupdocs.com/temporary-license/)