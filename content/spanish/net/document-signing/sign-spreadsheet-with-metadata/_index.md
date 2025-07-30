---
"description": "Proteja y mejore sus hojas de cálculo de Excel integrando firmas de metadatos con GroupDocs.Signature para .NET. Añada información de autor, marcas de tiempo y datos personalizados para mejorar la trazabilidad y la autenticidad de los documentos."
"linktitle": "Hoja de cálculo de firmas con metadatos"
"second_title": "API .NET de GroupDocs.Signature"
"title": "Agregar firmas de metadatos a hojas de cálculo de Excel en C# .NET"
"url": "/es/net/document-signing/sign-spreadsheet-with-metadata/"
"weight": 13
---

## Introducción

Las hojas de cálculo de Excel suelen contener datos empresariales críticos, información financiera y cálculos importantes. Garantizar su autenticidad, rastrear su origen y proteger su integridad es crucial en muchos entornos profesionales. Una estrategia eficaz para mejorar la seguridad y la trazabilidad de las hojas de cálculo es integrar firmas de metadatos.

Este completo tutorial le guiará a través del proceso de firmar hojas de cálculo de Excel con metadatos mediante GroupDocs.Signature para .NET. Al añadir firmas de metadatos, puede integrar información valiosa, como datos del autor, marcas de tiempo de creación, identificadores de documentos y otras propiedades personalizadas, directamente en la estructura del archivo de la hoja de cálculo.

## Prerrequisitos

Antes de continuar con este tutorial, asegúrese de tener lo siguiente:

1. [GroupDocs.Signature para .NET](https://releases.groupdocs.com/signature/net/) - Descargar e instalar la biblioteca
2. Entorno de desarrollo: Visual Studio o cualquier otro IDE compatible con .NET
3. Hoja de cálculo de Excel: un archivo de hoja de cálculo de muestra (XLSX, XLS, etc.)
4. Conocimientos básicos de C#: familiaridad con el lenguaje de programación C#

## Importar espacios de nombres

Comience importando los espacios de nombres necesarios para acceder a la funcionalidad de GroupDocs.Signature:

```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

## Paso 1: Configurar rutas de archivos

Define las rutas para tu hoja de cálculo de origen y dónde debe guardarse la salida firmada:

```csharp
// Especifique la ruta a su archivo de Excel
string filePath = "sample.xlsx";

// Define el directorio de salida y el nombre del archivo para la hoja de cálculo firmada
string outputDirectory = "Your Document Directory";
string outputFilePath = Path.Combine(outputDirectory, "SignSpreadsheetWithMetadata", "SignedWithMetadata.xlsx");

// Asegúrese de que exista el directorio de salida
Directory.CreateDirectory(Path.GetDirectoryName(outputFilePath));
```

## Paso 2: Inicializar el objeto de firma

Cree una instancia de la clase Signature con su archivo de hoja de cálculo de origen:

```csharp
using (Signature signature = new Signature(filePath))
{
    // El resto del código irá aquí.
}
```

## Paso 3: Crear y configurar firmas de metadatos

A continuación, defina las opciones de metadatos y cree una matriz de firmas de metadatos de la hoja de cálculo:

```csharp
// Crear un objeto de opciones de metadatos
MetadataSignOptions options = new MetadataSignOptions();

// Cree una matriz de firmas de metadatos de hojas de cálculo con diferentes tipos de datos
SpreadsheetMetadataSignature[] signatures = new SpreadsheetMetadataSignature[]
{
    new SpreadsheetMetadataSignature("Author", "Mr.Sherlock Holmes"), // Valor de cadena
    new SpreadsheetMetadataSignature("CreatedOn", DateTime.Now),      // Valor de fecha y hora
    new SpreadsheetMetadataSignature("DocumentId", 123456),           // Valor entero
    new SpreadsheetMetadataSignature("SignatureId", 123.456D),        // Doble valor
    new SpreadsheetMetadataSignature("Amount", 123.456M),             // Valor decimal
    new SpreadsheetMetadataSignature("Total", 123.456F)               // Valor flotante
};

// Añadir colección de firmas a las opciones
options.Signatures.AddRange(signatures);
```

## Paso 4: Firmar la hoja de cálculo con metadatos

Aplique las firmas de metadatos a la hoja de cálculo y guarde el resultado:

```csharp
// Firme el documento y guárdelo en la ruta del archivo de salida
SignResult result = signature.Sign(outputFilePath, options);

// Mostrar mensaje de éxito
Console.WriteLine($"\nSource spreadsheet signed successfully with {result.Succeeded.Count} metadata signature(s).");
Console.WriteLine($"Signed spreadsheet saved at: {outputFilePath}");
```

## Ejemplo completo

Aquí está el ejemplo de código completo que reúne todos los pasos:

```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;

namespace SignSpreadsheetWithMetadataExample
{
    class Program
    {
        static void Main(string[] args)
        {
            // Especificar rutas de archivos
            string filePath = "sample.xlsx";
            string outputFilePath = Path.Combine("Your Document Directory", "SignSpreadsheetWithMetadata", "SignedWithMetadata.xlsx");
            
            // Asegúrese de que exista el directorio de salida
            Directory.CreateDirectory(Path.GetDirectoryName(outputFilePath));

            // Firmar la hoja de cálculo con metadatos
            using (Signature signature = new Signature(filePath))
            {
                // Crear un objeto de opciones de metadatos
                MetadataSignOptions options = new MetadataSignOptions();
                
                // Cree una matriz de firmas de metadatos de hojas de cálculo con diferentes tipos de datos
                SpreadsheetMetadataSignature[] signatures = new SpreadsheetMetadataSignature[]
                {
                    new SpreadsheetMetadataSignature("Author", "Mr.Sherlock Holmes"), // Valor de cadena
                    new SpreadsheetMetadataSignature("CreatedOn", DateTime.Now),      // Valor de fecha y hora
                    new SpreadsheetMetadataSignature("DocumentId", 123456),           // Valor entero
                    new SpreadsheetMetadataSignature("SignatureId", 123.456D),        // Doble valor
                    new SpreadsheetMetadataSignature("Amount", 123.456M),             // Valor decimal
                    new SpreadsheetMetadataSignature("Total", 123.456F)               // Valor flotante
                };
                
                // Añadir colección de firmas a las opciones
                options.Signatures.AddRange(signatures);
                
                // Firmar el documento y guardarlo en el archivo
                SignResult result = signature.Sign(outputFilePath, options);
                
                // Mostrar resultados
                Console.WriteLine($"\nSource spreadsheet signed successfully with {result.Succeeded.Count} signature(s).");
                Console.WriteLine($"File saved at {outputFilePath}.");
            }
        }
    }
}
```

## Técnicas avanzadas de metadatos de hojas de cálculo

### Trabajar con propiedades de hojas de cálculo personalizadas e integradas

Las hojas de cálculo de Excel tienen propiedades integradas y personalizadas, accesibles a través del cuadro de diálogo de propiedades del archivo. GroupDocs.Signature permite trabajar con ambas:

```csharp
// Agregar propiedades integradas
signatures = new SpreadsheetMetadataSignature[]
{
    new SpreadsheetMetadataSignature("Company", "Sherlock Holmes Consulting"),
    new SpreadsheetMetadataSignature("Category", "Financial"),
    new SpreadsheetMetadataSignature("Keywords", "budget,forecast,analysis"),
    new SpreadsheetMetadataSignature("Comments", "This spreadsheet contains confidential information"),
    new SpreadsheetMetadataSignature("Manager", "John Watson")
};
options.Signatures.AddRange(signatures);

// Agregar propiedades personalizadas
options.Signatures.Add(new SpreadsheetMetadataSignature("Department", "Finance"));
options.Signatures.Add(new SpreadsheetMetadataSignature("SecurityLevel", "Confidential"));
```

### Búsqueda de metadatos en hojas de cálculo firmadas

Después de firmar, es posible que desee verificar o extraer los metadatos:

```csharp
// Crear opciones de búsqueda para metadatos
MetadataSearchOptions searchOptions = new MetadataSearchOptions();

// Búsqueda de firmas de metadatos
SearchResult searchResult = signature.Search(searchOptions);

// Mostrar firmas encontradas
Console.WriteLine($"Found {searchResult.Signatures.Count} metadata signatures:");
foreach (var foundSignature in searchResult.Signatures)
{
    MetadataSignature metadataSignature = foundSignature as MetadataSignature;
    if (metadataSignature != null)
    {
        Console.WriteLine($"- {metadataSignature.Name}: {metadataSignature.Value} ({metadataSignature.Value.GetType().Name})");
    }
}
```

### Actualización de metadatos existentes

Puede actualizar metadatos existentes en hojas de cálculo utilizando los mismos nombres de propiedad:

```csharp
// Actualizar metadatos existentes
options.Signatures.Add(new SpreadsheetMetadataSignature("Author", "Updated Author Name"));
```

## Conclusión

En este completo tutorial, aprendió a firmar hojas de cálculo de Excel con metadatos usando GroupDocs.Signature para .NET. Incrustar metadatos en archivos de hojas de cálculo mejora la trazabilidad de los documentos, proporciona un contexto valioso y ayuda a establecer la autenticidad.

Las firmas de metadatos en hojas de cálculo son especialmente útiles en entornos empresariales donde el origen, la autoría y el seguimiento de versiones de los documentos son importantes. Los metadatos incrustados pueden incluir información sobre el autor, la fecha de creación, los identificadores del documento y las propiedades personalizadas relevantes para las necesidades de su organización.

Al implementar firmas de metadatos con GroupDocs.Signature, puede garantizar que sus hojas de cálculo de Excel mantengan su integridad y proporcionen información verificable durante todo su ciclo de vida.

## Preguntas frecuentes

### ¿Puedo agregar metadatos a hojas de cálculo que ya tienen algunas propiedades definidas?

Sí, puede agregar nuevos metadatos o actualizar los existentes en hojas de cálculo. GroupDocs.Signature gestionará la integración, ya sea agregando nuevas propiedades o actualizando las existentes con los mismos nombres.

### ¿Qué formatos de hojas de cálculo son compatibles con la firma de metadatos?

GroupDocs.Signature para .NET admite la firma de metadatos para varios formatos de hojas de cálculo, como XLSX, XLS, XLSM, ODS y más. Para obtener una lista completa, consulte [documentación oficial](https://docs.groupdocs.com/signature/net/).

### ¿Las firmas de metadatos en las hojas de cálculo son visibles para los usuarios?

Las firmas de metadatos no son visibles en el contenido de la hoja de cálculo. Sin embargo, pueden visualizarse a través del panel de propiedades del documento en Excel u otras aplicaciones compatibles.

### ¿Puedo validar programáticamente si una hoja de cálculo ha sido alterada después de agregar metadatos?

Sí, GroupDocs.Signature proporciona capacidades de verificación que pueden ayudar a detectar si un documento ha sido modificado después de la firma, incluidos los cambios en los metadatos.

### ¿Agregar metadatos afecta la funcionalidad de la hoja de cálculo?

Añadir metadatos tiene un impacto mínimo en el tamaño del archivo y no afecta la funcionalidad de la hoja de cálculo. Es una forma sencilla de mejorar las propiedades del documento sin afectar los cálculos, las fórmulas ni otras funciones de Excel.

### ¿Dónde puedo encontrar más recursos y apoyo?

- [Referencia de API](https://reference.groupdocs.com/signature/net/)
- [Descargas](https://releases.groupdocs.com/signature/net/)
- [Ejemplos](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
- [Documentación](https://docs.groupdocs.com/signature/net/)
- [Página del producto](https://products.groupdocs.com/signature/net/)
- [Blog](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
- [Foro de soporte](https://forum.groupdocs.com/c/signature/13)
- [Licencia temporal](https://purchase.groupdocs.com/temporary-license/)