---
"description": "Aprenda a buscar varios tipos de firmas en documentos con GroupDocs.Signature para .NET. Guía completa con ejemplos de código para mejorar la seguridad de los documentos."
"linktitle": "Buscar múltiples firmas"
"second_title": "API .NET de GroupDocs.Signature"
"title": "Buscar múltiples tipos de firmas en documentos"
"url": "/es/net/signature-searching/search-for-multiple-signatures/"
"weight": 14
---

## Introducción

En los sistemas modernos de gestión documental, la capacidad de buscar y validar múltiples tipos de firmas dentro de un mismo documento es cada vez más importante. Las organizaciones suelen emplear diversos tipos de firmas (como firmas digitales, firmas de texto, códigos de barras, códigos QR, etc.) para mejorar la seguridad de los documentos y agilizar los procesos de verificación. GroupDocs.Signature para .NET ofrece un potente marco que permite a los desarrolladores implementar una completa funcionalidad de búsqueda de firmas en diversos formatos de documentos.

Este tutorial lo guiará a través del proceso de búsqueda de múltiples tipos de firmas dentro de documentos utilizando GroupDocs.Signature para .NET, ofreciendo explicaciones detalladas y ejemplos de código prácticos.

## Prerrequisitos

Antes de comenzar a implementar la funcionalidad de búsqueda de múltiples firmas, asegúrese de tener los siguientes requisitos previos:

1. Entorno de desarrollo: Visual Studio o cualquier entorno de desarrollo .NET preferido instalado en su sistema.
  
2. GroupDocs.Signature para .NET: Descargue e instale la biblioteca GroupDocs.Signature para .NET desde [aquí](https://releases.groupdocs.com/signature/net/).

3. Conocimientos básicos de C#: familiaridad con el lenguaje de programación C# y conceptos del marco .NET.

4. Documentos de muestra: Prepare documentos de prueba que contengan varios tipos de firmas para fines de prueba.

## Importar espacios de nombres

Comience importando los espacios de nombres necesarios para acceder a la funcionalidad de GroupDocs.Signature:

```csharp
using System;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

Ahora, desglosemos el proceso de búsqueda de múltiples tipos de firmas en pasos claros y manejables:

## Paso 1: Cargar el documento

Primero, cargue el documento que contiene las firmas que desea buscar:

```csharp
string filePath = "sample_multiple_signatures.docx";
using (Signature signature = new Signature(filePath))
{
    // Aquí se añadirá el código de búsqueda de múltiples firmas
}
```

## Paso 2: Definir opciones de búsqueda para diferentes tipos de firmas

Crea opciones de búsqueda para cada tipo de firma que quieras buscar:

```csharp
// Definir opciones de búsqueda para firmas de texto
TextSearchOptions textOptions = new TextSearchOptions
{
    AllPages = true,  // Buscar en todas las páginas
    Text = "Signature",  // Opcional: texto a buscar
    MatchType = TextMatchType.Contains  // Criterios de coincidencia
};

// Definir opciones de búsqueda para firmas digitales
DigitalSearchOptions digitalOptions = new DigitalSearchOptions
{
    AllPages = true
};

// Definir opciones de búsqueda para firmas de código de barras
BarcodeSearchOptions barcodeOptions = new BarcodeSearchOptions
{
    AllPages = true,
    Text = "123456",  // Opcional: texto del código de barras para que coincida
    MatchType = TextMatchType.Exact  // Criterios de coincidencia
};

// Definir opciones de búsqueda para firmas de códigos QR
QrCodeSearchOptions qrCodeOptions = new QrCodeSearchOptions
{
    AllPages = true,
    Text = "John",  // Opcional: Texto del código QR para que coincida
    MatchType = TextMatchType.Contains  // Criterios de coincidencia
};

// Definir opciones de búsqueda para firmas de metadatos
MetadataSearchOptions metadataOptions = new MetadataSearchOptions();
```

## Paso 3: Agregar opciones a una colección

Añade todas las opciones de búsqueda a una colección:

```csharp
// Crea una lista para guardar todas las opciones de búsqueda
List<SearchOptions> searchOptions = new List<SearchOptions>
{
    textOptions,
    digitalOptions,
    barcodeOptions,
    qrCodeOptions,
    metadataOptions
};
```

## Paso 4: Realizar la búsqueda y procesar los resultados

Ejecute la búsqueda utilizando las opciones de búsqueda combinadas y procese los resultados:

```csharp
// Busque todos los tipos de firma utilizando las opciones definidas
SearchResult result = signature.Search(searchOptions);

// Comprobar si se encontraron firmas
if (result.Signatures.Count > 0)
{
    Console.WriteLine($"\nSource document ['{filePath}'] contains {result.Signatures.Count} signature(s):");
    
    // Iterar a través de las firmas encontradas
    foreach (var foundSignature in result.Signatures)
    {
        Console.WriteLine($"Signature found: Type: {foundSignature.SignatureType}, Page: {foundSignature.PageNumber}, ID: {foundSignature.SignatureId}");
        
        // Procesar tipos de firma específicos
        if (foundSignature is TextSignature textSignature)
        {
            Console.WriteLine($"Text: '{textSignature.Text}'");
        }
        else if (foundSignature is BarcodeSignature barcodeSignature)
        {
            Console.WriteLine($"Barcode Type: {barcodeSignature.EncodeType.TypeName}, Text: '{barcodeSignature.Text}'");
        }
        else if (foundSignature is QrCodeSignature qrCodeSignature)
        {
            Console.WriteLine($"QR Code Type: {qrCodeSignature.EncodeType.TypeName}, Text: '{qrCodeSignature.Text}'");
        }
        else if (foundSignature is DigitalSignature digitalSignature)
        {
            Console.WriteLine($"Certificate: {digitalSignature.Certificate?.SubjectName}, Valid: {digitalSignature.IsValid}");
        }
        else if (foundSignature is MetadataSignature metadataSignature)
        {
            Console.WriteLine($"Metadata: Name: {metadataSignature.Name}, Value: {metadataSignature.Value}");
        }
    }
}
else
{
    Console.WriteLine("No signatures were found in the document.");
}
```

## Ejemplo completo

A continuación se muestra un ejemplo completo y funcional que demuestra cómo buscar múltiples tipos de firmas en un documento:

```csharp
using System;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;

namespace MultiSignatureSearch
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
                try
                {
                    // Definir opciones de búsqueda para firmas de texto
                    TextSearchOptions textOptions = new TextSearchOptions
                    {
                        AllPages = true,
                        MatchType = TextMatchType.Contains
                    };

                    // Definir opciones de búsqueda para firmas digitales
                    DigitalSearchOptions digitalOptions = new DigitalSearchOptions
                    {
                        AllPages = true
                    };

                    // Definir opciones de búsqueda para firmas de código de barras
                    BarcodeSearchOptions barcodeOptions = new BarcodeSearchOptions
                    {
                        AllPages = true
                    };

                    // Definir opciones de búsqueda para firmas de códigos QR
                    QrCodeSearchOptions qrCodeOptions = new QrCodeSearchOptions
                    {
                        AllPages = true
                    };

                    // Definir opciones de búsqueda para firmas de metadatos
                    MetadataSearchOptions metadataOptions = new MetadataSearchOptions();

                    // Crea una lista para guardar todas las opciones de búsqueda
                    List<SearchOptions> searchOptions = new List<SearchOptions>
                    {
                        textOptions,
                        digitalOptions,
                        barcodeOptions,
                        qrCodeOptions,
                        metadataOptions
                    };

                    // Buscar todos los tipos de firmas
                    SearchResult result = signature.Search(searchOptions);

                    // Comprobar si se encontraron firmas
                    if (result.Signatures.Count > 0)
                    {
                        Console.WriteLine($"\nSource document ['{filePath}'] contains {result.Signatures.Count} signature(s):");
                        
                        // Resultados del proceso por tipo de firma
                        foreach (var foundSignature in result.Signatures)
                        {
                            Console.WriteLine($"Signature found: Type: {foundSignature.SignatureType}, Page: {foundSignature.PageNumber}");
                            
                            // Procesar tipos de firma específicos
                            switch (foundSignature.SignatureType)
                            {
                                case SignatureType.Text:
                                    var textSignature = foundSignature as TextSignature;
                                    Console.WriteLine($"Text: '{textSignature.Text}'");
                                    break;
                                    
                                case SignatureType.Barcode:
                                    var barcodeSignature = foundSignature as BarcodeSignature;
                                    Console.WriteLine($"Barcode Type: {barcodeSignature.EncodeType.TypeName}, Text: '{barcodeSignature.Text}'");
                                    break;
                                    
                                case SignatureType.QrCode:
                                    var qrCodeSignature = foundSignature as QrCodeSignature;
                                    Console.WriteLine($"QR Code Type: {qrCodeSignature.EncodeType.TypeName}, Text: '{qrCodeSignature.Text}'");
                                    break;
                                    
                                case SignatureType.Digital:
                                    var digitalSignature = foundSignature as DigitalSignature;
                                    Console.WriteLine($"Certificate: {digitalSignature.Certificate?.SubjectName}, Valid: {digitalSignature.IsValid}");
                                    break;
                                    
                                case SignatureType.Metadata:
                                    var metadataSignature = foundSignature as MetadataSignature;
                                    Console.WriteLine($"Metadata: Name: {metadataSignature.Name}, Value: {metadataSignature.Value}");
                                    break;
                            }
                            
                            Console.WriteLine(); // Agregar salto de línea entre firmas
                        }
                    }
                    else
                    {
                        Console.WriteLine("No signatures were found in the document.");
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

## Técnicas avanzadas de búsqueda de múltiples firmas

### Filtrar resultados de búsqueda

Puede implementar un filtrado avanzado para limitar los resultados de búsqueda:

```csharp
// Filtrar resultados por número de página
var signaturesOnFirstPage = result.Signatures.FindAll(s => s.PageNumber == 1);

// Filtrar resultados por tipo de firma
var digitalSignatures = result.Signatures.FindAll(s => s.SignatureType == SignatureType.Digital);
var qrCodeSignatures = result.Signatures.FindAll(s => s.SignatureType == SignatureType.QrCode);

// Filtrar firmas de texto que contienen contenido específico
var approvalSignatures = result.Signatures
    .FindAll(s => s is TextSignature && ((TextSignature)s).Text.Contains("Approved"));
```

### Validación de múltiples firmas

Implementar lógica de validación para diferentes tipos de firmas:

```csharp
bool ValidateAllSignatures(SearchResult result)
{
    bool isDocumentValid = true;
    
    // Comprobar si el documento tiene una firma digital válida
    bool hasValidDigitalSignature = result.Signatures
        .Any(s => s is DigitalSignature && ((DigitalSignature)s).IsValid);
    
    if (!hasValidDigitalSignature)
    {
        Console.WriteLine("Warning: Document does not contain a valid digital signature");
        isDocumentValid = false;
    }
    
    // Verificar si el documento tiene el código QR requerido
    bool hasRequiredQRCode = result.Signatures
        .Any(s => s is QrCodeSignature && ((QrCodeSignature)s).Text.Contains("Auth-Code"));
    
    if (!hasRequiredQRCode)
    {
        Console.WriteLine("Warning: Document does not contain the required authentication QR code");
        isDocumentValid = false;
    }
    
    return isDocumentValid;
}
```

### Búsqueda con procesamiento personalizado

Puede definir una lógica de procesamiento personalizada para las operaciones de búsqueda:

```csharp
// Cree opciones de búsqueda con procesamiento personalizado
TextSearchOptions textOptions = new TextSearchOptions
{
    AllPages = true,
    
    // Definir el procesamiento personalizado utilizando un delegado
    ProcessCompleted = (signature) =>
    {
        // Lógica de validación personalizada: acepta solo firmas en páginas específicas
        TextSignature textSignature = signature as TextSignature;
        return textSignature != null && (textSignature.PageNumber == 1 || textSignature.PageNumber == 2);
    }
};
```

## Conclusión

En esta guía completa, hemos explorado cómo buscar múltiples tipos de firmas en documentos con GroupDocs.Signature para .NET. Desde la configuración de opciones de búsqueda para diferentes tipos de firma hasta el procesamiento y la validación de los resultados, ahora cuenta con los conocimientos necesarios para implementar una sólida función de búsqueda de firmas en sus aplicaciones .NET.

La capacidad de buscar múltiples tipos de firma simultáneamente optimiza los procesos de verificación de documentos, refuerza las medidas de seguridad y agiliza los flujos de trabajo de validación. GroupDocs.Signature ofrece un marco potente y flexible para trabajar con diversos tipos de firma en diferentes formatos de documento, lo que lo convierte en una excelente opción para aplicaciones de procesamiento de documentos.

## Preguntas frecuentes

### ¿Puedo buscar firmas en documentos protegidos con contraseña?

Sí, GroupDocs.Signature permite la búsqueda de firmas en documentos protegidos con contraseña. Puede proporcionar la contraseña al inicializar el documento. `Signature` objeto:

```csharp
LoadOptions loadOptions = new LoadOptions { Password = "your_password" };
using (Signature signature = new Signature(filePath, loadOptions))
{
    // Búsqueda de firmas
}
```

### ¿Qué formatos de documentos son compatibles con la búsqueda de firmas?

GroupDocs.Signature admite una amplia gama de formatos de documentos, incluidos PDF, documentos de Microsoft Office (Word, Excel, PowerPoint), formatos OpenOffice, imágenes y más.

### ¿Puedo limitar la búsqueda a páginas específicas de un documento?

Sí, cada tipo de opción de búsqueda tiene propiedades que le permiten especificar qué páginas buscar:

```csharp
TextSearchOptions options = new TextSearchOptions
{
    AllPages = false,  // No busques en todas las páginas
    PageNumber = 1,    // Buscar sólo en la página 1
    
    // O especifique varias páginas
    PagesSetup = new PagesSetup { Pages = new List<int> { 1, 3, 5 } }
};
```

### ¿Cómo puedo optimizar el rendimiento al buscar en documentos grandes?

Para documentos grandes, puede optimizar el rendimiento mediante lo siguiente:

1. Limitar la búsqueda a páginas o rangos de páginas específicos
2. Utilizar criterios de búsqueda más específicos para reducir el número de coincidencias potenciales
3. Implementar la paginación en la visualización de resultados
4. Busque un tipo de firma a la vez si no necesita resultados simultáneos

### ¿Puedo ampliar GroupDocs.Signature para admitir tipos de firma personalizados?

Si bien GroupDocs.Signature proporciona soporte integrado para tipos de firma comunes, puede ampliar su funcionalidad mediante lo siguiente:

1. Creación de clases de opciones de búsqueda personalizadas derivadas de `SearchOptions`
2. Implementación de lógica de procesamiento personalizada utilizando el `ProcessCompleted` delegar
3. Desarrollo de clases contenedoras que combinan múltiples búsquedas de firmas con lógica empresarial avanzada

## Ver también

* [Referencia de API](https://reference.groupdocs.com/signature/net/)
* [Ejemplos de código en GitHub](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
* [Documentación del producto](https://docs.groupdocs.com/signature/net/)
* [Página del producto](https://products.groupdocs.com/signature/net/)
* [Descargar la última versión](https://releases.groupdocs.com/signature/net/)
* [Artículos del blog](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
* [Foro de soporte gratuito](https://forum.groupdocs.com/c/signature/13)
* [Licencia temporal](https://purchase.groupdocs.com/temporary-license/)