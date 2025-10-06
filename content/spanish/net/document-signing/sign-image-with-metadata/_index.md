---
"description": "Aprenda a firmar e incrustar metadatos en imágenes con GroupDocs.Signature para .NET. Agregue información del autor, marcas de tiempo y datos personalizados para mejorar la autenticidad y la trazabilidad de las imágenes."
"linktitle": "Firmar imagen con metadatos"
"second_title": "API .NET de GroupDocs.Signature"
"title": "Firmar imágenes con metadatos en C# .NET"
"url": "/es/net/document-signing/sign-image-with-metadata/"
"weight": 10
type: docs
---
## Introducción

La firma digital de imágenes con metadatos es cada vez más importante para establecer la autenticidad, la propiedad y la trazabilidad. GroupDocs.Signature para .NET ofrece una solución potente y fácil de usar para añadir firmas de metadatos a diversos formatos de imagen. Este tutorial le guía a través del proceso completo de firma de imágenes con metadatos usando C#.

Las firmas de metadatos permiten incrustar información valiosa directamente en los archivos de imagen, como información del autor, marcas de tiempo de creación, identificadores únicos y más. Esta información se integra en el archivo de imagen, lo que proporciona un método fiable para rastrear y verificar la autenticidad de la imagen.

## Prerrequisitos

Antes de continuar con este tutorial, asegúrese de tener lo siguiente:

1. [GroupDocs.Signature para .NET](https://releases.groupdocs.com/signature/net/) - Descargar e instalar la biblioteca
2. Entorno de desarrollo: Visual Studio o cualquier IDE compatible con soporte .NET
3. Archivo de imagen: un archivo de imagen de muestra en un formato compatible (PNG, JPG, TIFF, etc.)
4. Conocimientos básicos de programación en C#: familiaridad con los conceptos de programación en C#

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

Define las rutas para tu imagen de origen y dónde debe guardarse la salida firmada:

```csharp
// Especifique la ruta a su archivo de imagen de origen
string filePath = "sample.png";

// Define el directorio de salida y el nombre del archivo para la imagen firmada
string outputDirectory = "Your Document Directory";
string outputFilePath = Path.Combine(outputDirectory, "SignImageWithMetadata", "SignedWithMetadata.png");

// Asegúrese de que exista el directorio de salida
Directory.CreateDirectory(Path.GetDirectoryName(outputFilePath));
```

## Paso 2: Inicializar el objeto de firma

Crea una instancia de la clase Signature con tu archivo de imagen de origen:

```csharp
using (Signature signature = new Signature(filePath))
{
    // El resto del código irá aquí.
}
```

## Paso 3: Crear y configurar firmas de metadatos

A continuación, defina los metadatos que desea incrustar en la imagen. GroupDocs.Signature admite varios tipos de datos para metadatos:

```csharp
// Inicializar el ID de metadatos (específico del formato de imagen)
ushort imgsMetadataId = 41996;

// Crear un objeto de opciones de metadatos
MetadataSignOptions options = new MetadataSignOptions();

// Añadir varios tipos de firmas de metadatos
options
    .Add(new ImageMetadataSignature(imgsMetadataId++, "Mr.Sherlock Holmes"))  // Valor de cadena
    .Add(new ImageMetadataSignature(imgsMetadataId++, DateTime.Now))          // Valor de fecha y hora
    .Add(new ImageMetadataSignature(imgsMetadataId++, 123456))                // Valor entero
    .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456D))              // Doble valor
    .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456M))              // Valor decimal
    .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456F));             // Valor flotante
```

## Paso 4: Firmar la imagen con metadatos

Aplique las firmas de metadatos a la imagen y guarde el resultado:

```csharp
// Firme el documento y guárdelo en la ruta del archivo de salida
SignResult result = signature.Sign(outputFilePath, options);

// Mostrar mensaje de éxito
Console.WriteLine($"\nSource image signed successfully with {result.Succeeded.Count} metadata signature(s).");
Console.WriteLine($"Signed image saved at: {outputFilePath}");
```

## Ejemplo completo

Aquí está el ejemplo de código completo que reúne todos los pasos:

```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;

namespace SignImageWithMetadataExample
{
    class Program
    {
        static void Main(string[] args)
        {
            // Especificar rutas de archivos
            string filePath = "sample.png";            
            string outputFilePath = Path.Combine("Your Document Directory", "SignImageWithMetadata", "SignedWithMetadata.png");
            
            // Asegúrese de que exista el directorio de salida
            Directory.CreateDirectory(Path.GetDirectoryName(outputFilePath));

            // Firmar la imagen con metadatos
            using (Signature signature = new Signature(filePath))
            {
                // Inicializar el ID de metadatos (específico del formato de imagen)
                ushort imgsMetadataId = 41996;
                
                // Crear opciones de metadatos
                MetadataSignOptions options = new MetadataSignOptions();
                
                // Agregar diferentes tipos de firmas de metadatos
                options
                    .Add(new ImageMetadataSignature(imgsMetadataId++, "Mr.Sherlock Holmes")) // Valor de cadena
                    .Add(new ImageMetadataSignature(imgsMetadataId++, DateTime.Now))          // Valor de fecha y hora
                    .Add(new ImageMetadataSignature(imgsMetadataId++, 123456))                // Valor entero
                    .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456D))              // Doble valor
                    .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456M))              // Valor decimal
                    .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456F));             // Valor flotante
                
                // Firmar el documento y guardarlo en el archivo
                SignResult result = signature.Sign(outputFilePath, options);
                
                // Mostrar resultados
                Console.WriteLine($"\nSource image signed successfully with {result.Succeeded.Count} signature(s).");
                Console.WriteLine($"File saved at {outputFilePath}.");
            }
        }
    }
}
```

## Técnicas avanzadas de firma de metadatos

### Trabajar con metadatos personalizados

También puedes crear campos de metadatos personalizados con identificaciones específicas:

```csharp
// Crear metadatos personalizados con una identificación específica
options.Add(new ImageMetadataSignature(42000, "CustomValue"));
```

### Verificación de firmas de metadatos

Después de firmar, es posible que desee verificar las firmas de metadatos:

```csharp
// Crear opciones de verificación
MetadataSearchOptions searchOptions = new MetadataSearchOptions();

// Búsqueda de firmas de metadatos
SearchResult result = signature.Search(searchOptions);

// Mostrar firmas encontradas
Console.WriteLine($"Found {result.Signatures.Count} metadata signatures:");
foreach(var metadataSignature in result.Signatures)
{
    Console.WriteLine($"- {metadataSignature.Name}: {metadataSignature.Value}");
}
```

## Conclusión

En este tutorial, aprendió a firmar imágenes con metadatos usando GroupDocs.Signature para .NET. Incrustar metadatos en imágenes es una excelente manera de mejorar su autenticidad, añadir información crítica y optimizar los flujos de trabajo de gestión documental. El proceso es sencillo pero eficaz, y permite la personalización según sus necesidades específicas.

Los metadatos incrustados en el archivo de imagen pueden utilizarse para diversos fines, como la protección de derechos de autor, el rastreo del origen de la imagen, la adición de información descriptiva y el establecimiento de la cadena de custodia digital. Al implementar firmas de metadatos, puede garantizar que sus imágenes mantengan su integridad y autenticidad durante todo su ciclo de vida.

## Preguntas frecuentes

### ¿Puedo agregar metadatos a imágenes firmadas existentes?

Sí, puedes añadir metadatos adicionales a las imágenes que ya contienen firmas de metadatos. Los metadatos existentes se conservarán y se añadirán los nuevos según corresponda.

### ¿Qué formatos de imagen son compatibles con la firma de metadatos?

GroupDocs.Signature para .NET admite la firma de metadatos para varios formatos de imagen, como PNG, JPEG, TIFF, BMP, GIF y más. Para obtener una lista completa, consulte [documentación oficial](https://docs.groupdocs.com/signature/net/).

### ¿Es posible cifrar los metadatos de las imágenes?

Sí, GroupDocs.Signature ofrece opciones para cifrar metadatos y mejorar la seguridad. Puede usar las opciones de cifrado de la biblioteca para proteger la información confidencial de los metadatos.

### ¿Puedo validar programáticamente la autenticidad de las imágenes firmadas?

Por supuesto. Puedes usar los métodos de verificación de GroupDocs.Signature para validar las firmas de metadatos y confirmar la autenticidad de las imágenes firmadas.

### ¿Existe una limitación en el tamaño de archivo al firmar imágenes con metadatos?

La biblioteca no impone un límite de tamaño de archivo específico, pero los archivos muy grandes podrían requerir más tiempo de procesamiento y memoria. Se recomienda considerar los recursos del sistema al trabajar con imágenes extremadamente grandes.

### ¿Cómo puedo obtener una licencia temporal para fines de prueba?

Puedes obtener una [licencia temporal](https://purchase.groupdocs.com/temporary-license/) para probar GroupDocs.Signature antes de realizar una compra.

### ¿Dónde puedo encontrar más recursos y apoyo?

- [Referencia de API](https://reference.groupdocs.com/signature/net/)
- [Descargas](https://releases.groupdocs.com/signature/net/)
- [Ejemplos](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
- [Documentación](https://docs.groupdocs.com/signature/net/)
- [Página del producto](https://products.groupdocs.com/signature/net/)
- [Blog](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
- [Foro de soporte](https://forum.groupdocs.com/c/signature/13)