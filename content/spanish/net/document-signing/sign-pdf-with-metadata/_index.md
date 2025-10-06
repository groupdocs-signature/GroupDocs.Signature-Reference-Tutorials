---
"description": "Integre firmas de metadatos en documentos PDF con GroupDocs.Signature para .NET. Aprenda a integrar información de autor, marcas de tiempo y datos personalizados para mejorar la autenticidad y la trazabilidad de los PDF."
"linktitle": "Firmar PDF con metadatos"
"second_title": "API .NET de GroupDocs.Signature"
"title": "Agregar firmas de metadatos a documentos PDF en C# .NET"
"url": "/es/net/document-signing/sign-pdf-with-metadata/"
"weight": 11
type: docs
---
## Introducción

Los documentos PDF (formato de documento portátil) se utilizan ampliamente en diversas industrias debido a su consistencia e independencia de plataforma. Garantizar la autenticidad y la trazabilidad de estos documentos es crucial en muchos entornos profesionales. Una forma eficaz de lograrlo es integrar metadatos en los propios archivos PDF.

En este completo tutorial, exploraremos cómo firmar documentos PDF con metadatos usando GroupDocs.Signature para .NET. Las firmas de metadatos permiten incrustar información adicional en el documento, como datos del autor, marcas de tiempo de creación, identificadores del documento y valores personalizados, sin alterar visiblemente su apariencia.

## Prerrequisitos

Antes de comenzar, asegúrese de tener lo siguiente en su lugar:

1. [GroupDocs.Signature para .NET](https://releases.groupdocs.com/signature/net/) - Descargar e instalar la biblioteca
2. Entorno de desarrollo: Visual Studio o cualquier otro IDE compatible con .NET
3. Documento PDF: un archivo PDF de muestra para firmar
4. Conocimientos básicos de C#: familiaridad con el lenguaje de programación C#

## Importar espacios de nombres

Comience importando los espacios de nombres necesarios para acceder a la funcionalidad GroupDocs.Signature:

```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

## Paso 1: Configurar rutas de archivos

Primero, defina la ruta a su documento PDF y especifique dónde desea guardar la salida firmada:

```csharp
// Especifique la ruta a su documento PDF
string filePath = "sample.pdf";

// Definir el directorio de salida y la ruta del archivo
string outputDirectory = "Your Document Directory";
string outputFilePath = Path.Combine(outputDirectory, "SignPdfWithMetadata", "SignedWithMetadata.pdf");

// Asegúrese de que exista el directorio de salida
Directory.CreateDirectory(Path.GetDirectoryName(outputFilePath));
```

## Paso 2: Inicializar el objeto de firma

Cree una instancia de la clase Signature con su documento PDF de origen:

```csharp
using (Signature signature = new Signature(filePath))
{
    // El código para firmar irá aquí
}
```

## Paso 3: Definir las opciones de metadatos

Cree y configure las opciones de metadatos, agregando varios tipos de firmas de metadatos:

```csharp
// Crear un objeto de opciones de metadatos
MetadataSignOptions options = new MetadataSignOptions();

// Agregue varios tipos de metadatos utilizando la interfaz fluida
options
    .Add(new PdfMetadataSignature("Author", "Mr.Sherlock Holmes")) // Valor de cadena
    .Add(new PdfMetadataSignature("CreatedOn", DateTime.Now))       // Valor de fecha y hora
    .Add(new PdfMetadataSignature("DocumentId", 123456))            // Valor entero
    .Add(new PdfMetadataSignature("SignatureId", 123.456D))         // Doble valor
    .Add(new PdfMetadataSignature("Amount", 123.456M))              // Valor decimal
    .Add(new PdfMetadataSignature("Total", 123.456F));              // Valor flotante
```

## Paso 4: Firma el PDF con metadatos

Aplique las firmas de metadatos al documento PDF y guarde el resultado:

```csharp
// Firme el documento y guárdelo en la ruta de salida
SignResult result = signature.Sign(outputFilePath, options);

// Mostrar mensaje de éxito
Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} metadata signature(s).");
Console.WriteLine($"Signed document saved at: {outputFilePath}");
```

## Ejemplo completo

Aquí está el ejemplo de código completo que reúne todos los pasos:

```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;

namespace SignPdfWithMetadataExample
{
    class Program
    {
        static void Main(string[] args)
        {
            // Especificar rutas de archivos
            string filePath = "sample.pdf";
            string outputFilePath = Path.Combine("Your Document Directory", "SignPdfWithMetadata", "SignedWithMetadata.pdf");
            
            // Asegúrese de que exista el directorio de salida
            Directory.CreateDirectory(Path.GetDirectoryName(outputFilePath));

            // Firmar el PDF con metadatos
            using (Signature signature = new Signature(filePath))
            {
                // Crear un objeto de opciones de metadatos
                MetadataSignOptions options = new MetadataSignOptions();
                
                // Agregar diferentes tipos de firmas de metadatos
                options
                    .Add(new PdfMetadataSignature("Author", "Mr.Sherlock Holmes")) // Valor de cadena
                    .Add(new PdfMetadataSignature("CreatedOn", DateTime.Now))       // Valor de fecha y hora
                    .Add(new PdfMetadataSignature("DocumentId", 123456))            // Valor entero
                    .Add(new PdfMetadataSignature("SignatureId", 123.456D))         // Doble valor
                    .Add(new PdfMetadataSignature("Amount", 123.456M))              // Valor decimal
                    .Add(new PdfMetadataSignature("Total", 123.456F));              // Valor flotante
                
                // Firmar el documento y guardarlo en el archivo
                SignResult result = signature.Sign(outputFilePath, options);
                
                // Mostrar resultados
                Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).");
                Console.WriteLine($"File saved at {outputFilePath}.");
            }
        }
    }
}
```

## Operaciones avanzadas de metadatos de PDF

### Agregar metadatos personalizados con compatibilidad con espacios de nombres

Los documentos PDF admiten metadatos personalizados con compatibilidad con espacios de nombres XML:

```csharp
// Agregar metadatos personalizados con espacio de nombres
options.Add(new PdfMetadataSignature("CustomProperty", "Custom Value")
{
    NamespaceUri = "http://"tu-espaciodenombres.com/esquema"
});
```

### Búsqueda de metadatos en archivos PDF firmados

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

### Trabajar con metadatos PDF estándar

Los documentos PDF tienen campos de metadatos estándar a los que se puede acceder y modificar:

```csharp
// Establecer campos de metadatos PDF estándar
options
    .Add(new PdfMetadataSignature("Title", "Important Contract"))
    .Add(new PdfMetadataSignature("Subject", "Legal Agreement"))
    .Add(new PdfMetadataSignature("Keywords", "contract, agreement, legal, binding"))
    .Add(new PdfMetadataSignature("Creator", "Legal Department"))
    .Add(new PdfMetadataSignature("Producer", "GroupDocs.Signature"));
```

## Conclusión

En este tutorial, aprendió a firmar documentos PDF con metadatos usando GroupDocs.Signature para .NET. Incrustar metadatos en archivos PDF es una excelente manera de mejorar la autenticidad de los documentos, añadir información importante y optimizar los flujos de trabajo de gestión documental.

Las firmas de metadatos en archivos PDF son especialmente valiosas en entornos empresariales donde la trazabilidad y la verificación de la autenticidad de los documentos son esenciales. Los metadatos incrustados pueden incluir información sobre el origen, el autor, la fecha de creación, la versión y las propiedades personalizadas del documento relevantes para el flujo de trabajo de su organización.

Al implementar firmas de metadatos con GroupDocs.Signature, puede garantizar que sus documentos PDF mantengan su integridad y proporcionen información verificable durante todo su ciclo de vida.

## Preguntas frecuentes

### ¿Puedo modificar los metadatos existentes en un documento PDF?

Sí, puede modificar los metadatos existentes en documentos PDF. Al aplicar nuevas firmas de metadatos con los mismos nombres que las existentes, los valores se actualizarán según corresponda.

### ¿Las firmas de metadatos en los documentos PDF son visibles para el usuario final?

Las firmas de metadatos no son visibles en el contenido del documento. Sin embargo, pueden visualizarse a través del panel de propiedades del documento en lectores de PDF como Adobe Acrobat o con herramientas especializadas para la visualización de metadatos.

### ¿Puedo cifrar o proteger los metadatos de los archivos PDF?

GroupDocs.Signature ofrece opciones para proteger documentos, incluyendo el cifrado. Puede aplicar cifrado a nivel de documento para proteger todo el PDF, incluidos sus metadatos.

### ¿Existe un límite en la cantidad de metadatos que puedo agregar a un PDF?

Aunque la especificación PDF no impone un límite estricto, añadir una cantidad excesiva de metadatos puede aumentar el tamaño del archivo. Se recomienda incluir únicamente la información relevante y necesaria en los metadatos.

### ¿Puedo validar programáticamente si un PDF ha sido alterado después de agregar metadatos?

Sí, GroupDocs.Signature proporciona capacidades de verificación que pueden ayudar a detectar si un documento ha sido modificado después de la firma, incluidos los cambios en los metadatos.

### ¿Dónde puedo encontrar más recursos y apoyo?

- [Referencia de API](https://reference.groupdocs.com/signature/net/)
- [Descargas](https://releases.groupdocs.com/signature/net/)
- [Ejemplos](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
- [Documentación](https://docs.groupdocs.com/signature/net/)
- [Página del producto](https://products.groupdocs.com/signature/net/)
- [Blog](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
- [Foro de soporte](https://forum.groupdocs.com/c/signature/13)
- [Licencia temporal](https://purchase.groupdocs.com/temporary-license/)