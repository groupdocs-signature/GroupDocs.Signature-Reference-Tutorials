---
"description": "Aprenda a buscar de manera eficiente códigos QR en documentos usando GroupDocs.Signature para .NET con esta completa guía paso a paso y ejemplos de código."
"linktitle": "Buscar códigos QR"
"second_title": "API .NET de GroupDocs.Signature"
"title": "Buscar firmas de código QR en documentos"
"url": "/es/net/signature-searching/search-for-qr-codes/"
"weight": 15
---

## Introducción

En el ecosistema actual de documentos digitales, las firmas de código QR se han convertido en una herramienta invaluable para integrar información, autenticar y mejorar la seguridad de los documentos. GroupDocs.Signature para .NET ofrece a los desarrolladores una potente API para buscar y extraer códigos QR de diversos formatos de documentos, lo que permite funciones avanzadas de análisis y verificación de documentos en aplicaciones .NET.

Este completo tutorial lo guiará a través del proceso de implementación de la funcionalidad de búsqueda de códigos QR utilizando GroupDocs.Signature para .NET, brindando explicaciones claras, instrucciones paso a paso y ejemplos de código prácticos que puede integrar en sus propias aplicaciones.

## Prerrequisitos

Antes de sumergirse en la búsqueda de firmas de códigos QR, asegúrese de tener los siguientes requisitos previos:

1. GroupDocs.Signature para .NET SDK: Descargue e instale el SDK desde [página de descarga](https://releases.groupdocs.com/signature/net/).

2. Entorno de desarrollo: configure un entorno de desarrollo .NET, como Visual Studio, con .NET Framework o .NET Core instalado.

3. Conocimientos básicos: Familiaridad con la programación en C# y conceptos de desarrollo .NET.

4. Documentos de muestra: Prepare documentos de prueba que contengan códigos QR para verificación y prueba.

## Importar espacios de nombres

Comience importando los espacios de nombres necesarios para acceder a la funcionalidad de GroupDocs.Signature:

```csharp
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
using System;
using System.Collections.Generic;
```

Ahora, desglosemos el proceso de búsqueda de códigos QR en pasos claros y fáciles de seguir:

## Paso 1: Definir la ruta del documento

Primero, especifique la ruta al documento que contiene los códigos QR que desea buscar:

```csharp
string filePath = "sample_multiple_signatures.docx";
```

## Paso 2: Inicializar el objeto de firma

Crear una instancia de la `Signature` clase pasando la ruta del documento:

```csharp
using (Signature signature = new Signature(filePath))
{
    // El código de búsqueda del código QR se agregará aquí
}
```

## Paso 3: Buscar firmas de códigos QR

Utilice el `Search` Método con el tipo de firma apropiado para encontrar códigos QR en el documento:

```csharp
// Buscar firmas de código QR dentro del documento
List<QrCodeSignature> signatures = signature.Search<QrCodeSignature>(SignatureType.QrCode);
```

## Paso 4: Procesar y mostrar resultados

Itere a través de las firmas de códigos QR encontradas y acceda a sus propiedades:

```csharp
// Mostrar información sobre los códigos QR encontrados
Console.WriteLine($"\nSource document contains {signatures.Count} QR code signature(s):");

foreach (var qrCodeSignature in signatures)
{
    Console.WriteLine($"QR Code found at page {qrCodeSignature.PageNumber} with type {qrCodeSignature.EncodeType.TypeName}");
    Console.WriteLine($"Content: {qrCodeSignature.Text}");
    Console.WriteLine($"Location: X={qrCodeSignature.Left}, Y={qrCodeSignature.Top}, Width={qrCodeSignature.Width}, Height={qrCodeSignature.Height}");
    Console.WriteLine();
}
```

## Ejemplo completo

A continuación se muestra un ejemplo práctico completo que demuestra el proceso completo de búsqueda de códigos QR en un documento:

```csharp
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
using System;
using System.Collections.Generic;

namespace QrCodeSignatureSearch
{
    class Program
    {
        static void Main(string[] args)
        {
            // Ruta del documento: actualice con la ruta de su archivo
            string filePath = "sample_multiple_signatures.docx";
            
            // Inicializar instancia de firma
            using (Signature signature = new Signature(filePath))
            {
                try
                {
                    // Buscar firmas de código QR en el documento
                    List<QrCodeSignature> signatures = signature.Search<QrCodeSignature>(SignatureType.QrCode);
                    
                    // Mostrar resultados de búsqueda
                    Console.WriteLine($"\nSource document ['{filePath}'] contains {signatures.Count} QR code signature(s):");
                    
                    foreach (var qrCodeSignature in signatures)
                    {
                        Console.WriteLine($"QR Code found at page {qrCodeSignature.PageNumber} with type {qrCodeSignature.EncodeType.TypeName}");
                        Console.WriteLine($"Content: {qrCodeSignature.Text}");
                        Console.WriteLine($"Location: X={qrCodeSignature.Left}, Y={qrCodeSignature.Top}, Width={qrCodeSignature.Width}, Height={qrCodeSignature.Height}");
                        Console.WriteLine();
                    }
                }
                catch (Exception ex)
                {
                    Console.WriteLine($"Error occurred: {ex.Message}");
                }
            }
            
            Console.WriteLine("Press any key to exit...");
            Console.ReadKey();
        }
    }
}
```

## Técnicas avanzadas de búsqueda de códigos QR

### Búsqueda con criterios específicos

Para búsquedas más específicas, puede utilizar `QrCodeSearchOptions` Para personalizar sus criterios de búsqueda:

```csharp
// Cree opciones de búsqueda de códigos QR con criterios específicos
QrCodeSearchOptions options = new QrCodeSearchOptions
{
    // Buscar sólo en páginas específicas
    AllPages = false,
    PageNumber = 1,
    PagesSetup = new PagesSetup { Pages = new List<int> { 1, 3, 5 } },
    
    // Filtrar por contenido de código QR
    Text = "Invoice",
    MatchType = TextMatchType.Contains,
    
    // Filtrar por tipos de códigos QR específicos
    EncodeType = QrCodeTypes.QR,
    
    // Define un área específica para buscar dentro
    Rectangle = new Rectangle(100, 100, 400, 400)
};

// Buscar con opciones específicas
List<QrCodeSignature> filteredSignatures = signature.Search<QrCodeSignature>(options);
```

### Procesamiento de datos de códigos QR

Puede implementar un procesamiento personalizado para los datos del código QR según los requisitos de su aplicación:

```csharp
foreach (var qrCode in signatures)
{
    // Extraer y procesar datos de códigos QR según el contenido
    string qrContent = qrCode.Text;
    
    if (qrContent.StartsWith("URL:"))
    {
        // Procesar datos de URL
        string url = qrContent.Substring(4);
        Console.WriteLine($"Found URL in QR code: {url}");
    }
    else if (qrContent.StartsWith("CONTACT:"))
    {
        // Procesar información de contacto
        string contact = qrContent.Substring(8);
        Console.WriteLine($"Found contact information in QR code: {contact}");
    }
    else if (qrContent.StartsWith("INVOICE:"))
    {
        // Procesar información de la factura
        string invoiceData = qrContent.Substring(8);
        Console.WriteLine($"Found invoice information in QR code: {invoiceData}");
        
        // Analizar y validar datos de facturas
        if (ValidateInvoiceData(invoiceData))
        {
            Console.WriteLine("Invoice data is valid!");
        }
        else
        {
            Console.WriteLine("Warning: Invalid invoice data detected!");
        }
    }
}

// Ejemplo de método de validación
static bool ValidateInvoiceData(string data)
{
    // Implemente su lógica de validación
    return !string.IsNullOrEmpty(data) && data.Contains("ID") && data.Contains("Amount");
}
```

### Implementación de la verificación de seguridad

Los códigos QR se utilizan a menudo con fines de autenticación. A continuación, se explica cómo implementar una verificación de seguridad básica:

```csharp
// Compruebe si el documento contiene un código QR de autenticación válido
bool hasValidAuthQrCode = false;

foreach (var qrCode in signatures)
{
    if (qrCode.Text.StartsWith("AUTH:"))
    {
        string authCode = qrCode.Text.Substring(5);
        
        // Verificar el código de autenticación (por ejemplo, contra una base de datos o una lista predefinida)
        if (VerifyAuthCode(authCode))
        {
            hasValidAuthQrCode = true;
            Console.WriteLine("Document contains valid authentication QR code!");
            break;
        }
    }
}

if (!hasValidAuthQrCode)
{
    Console.WriteLine("Warning: Document does not contain a valid authentication QR code!");
}

// Ejemplo de método de verificación
static bool VerifyAuthCode(string code)
{
    // Implemente su lógica de verificación
    // Esto podría ser una búsqueda en una base de datos, una llamada a una API o una comparación con valores predefinidos.
    return code == "A7B82C3D" || code == "X9Y8Z7W6";
}
```

### Extracción de imágenes de códigos QR

Puede extraer imágenes de códigos QR de documentos para su posterior procesamiento o visualización:

```csharp
// Guardar imágenes de códigos QR en el disco
foreach (var qrCode in signatures)
{
    if (qrCode.Content != null)
    {
        // Crea un nombre de archivo único basado en el número de página y la posición
        string outputPath = $"QrCode_P{qrCode.PageNumber}_X{qrCode.Left}_Y{qrCode.Top}.png";
        
        // Guardar los datos de la imagen
        File.WriteAllBytes(outputPath, qrCode.Content);
        Console.WriteLine($"Saved QR code image to {outputPath}");
    }
}
```

## Conclusión

En esta guía completa, hemos explorado cómo buscar firmas de códigos QR en documentos con GroupDocs.Signature para .NET. Desde búsquedas básicas hasta técnicas avanzadas, ahora cuenta con los conocimientos necesarios para implementar un manejo robusto de códigos QR en sus aplicaciones .NET. La API de GroupDocs.Signature proporciona un marco potente y flexible para trabajar con diversos tipos de firmas, incluidos códigos QR, en diferentes formatos de documento.

Al aprovechar estas capacidades, puede mejorar los procesos de verificación de documentos, implementar sistemas de autenticación y extraer información valiosa integrada en códigos QR, todo dentro de sus aplicaciones .NET.

## Preguntas frecuentes

### ¿Qué formatos de código QR admite GroupDocs.Signature?

GroupDocs.Signature admite varios formatos de códigos QR, incluyendo códigos QR estándar, microcódigos QR y otros estándares comunes. Se puede acceder al formato específico a través de `EncodeType` propiedad de la `QrCodeSignature` objeto.

### ¿Puedo buscar códigos QR en documentos protegidos con contraseña?

Sí, GroupDocs.Signature admite la búsqueda de códigos QR en documentos protegidos con contraseña proporcionando la contraseña al inicializar el documento. `Signature` objeto:

```csharp
LoadOptions loadOptions = new LoadOptions { Password = "your_password" };
using (Signature signature = new Signature(filePath, loadOptions))
{
    // Buscar códigos QR
}
```

### ¿Cómo puedo filtrar códigos QR según su contenido?

Puede filtrar códigos QR según su contenido utilizando el `Text` y `MatchType` propiedades de `QrCodeSearchOptions`:

```csharp
QrCodeSearchOptions options = new QrCodeSearchOptions
{
    Text = "Invoice",
    MatchType = TextMatchType.Contains // Otras opciones: Exacto, Empieza con, Termina con
};
```

### ¿Puede GroupDocs.Signature detectar códigos QR dañados o parcialmente visibles?

GroupDocs.Signature tiene cierta capacidad para detectar códigos QR parcialmente visibles, pero es posible que no reconozca códigos QR muy dañados. La precisión de la detección depende de la calidad y la visibilidad del código QR en el documento.

### ¿Qué formatos de documentos son compatibles con la búsqueda de códigos QR?

GroupDocs.Signature admite la búsqueda de códigos QR en varios formatos de documentos, incluidos PDF, documentos de Microsoft Office (Word, Excel, PowerPoint), imágenes (JPEG, PNG, TIFF) y muchos otros.

## Ver también

* [Referencia de API](https://reference.groupdocs.com/signature/net/)
* [Ejemplos de código en GitHub](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
* [Documentación del producto](https://docs.groupdocs.com/signature/net/)
* [Página del producto](https://products.groupdocs.com/signature/net/)
* [Descargar la última versión](https://releases.groupdocs.com/signature/net/)
* [Artículos del blog](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
* [Foro de soporte gratuito](https://forum.groupdocs.com/c/signature/13)
* [Licencia temporal](https://purchase.groupdocs.com/temporary-license/)