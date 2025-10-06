---
"description": "Aprenda a actualizar programáticamente firmas de códigos de barras en múltiples formatos de documentos con GroupDocs.Signature para .NET. Tutorial completo para desarrolladores que crean soluciones de gestión documental."
"linktitle": "Actualizar código de barras"
"second_title": "API .NET de GroupDocs.Signature"
"title": "Actualizar firmas de código de barras en documentos"
"url": "/es/net/update-operations/update-barcode/"
"weight": 10
type: docs
---
## Introducción
Las firmas de código de barras se utilizan ampliamente en flujos de trabajo de documentos digitales para codificar datos estructurados, lo que permite un seguimiento, una identificación y una validación eficientes. GroupDocs.Signature para .NET es una solución integral de firma de documentos que permite a los desarrolladores integrar funciones avanzadas de firma en sus aplicaciones, incluyendo la posibilidad de actualizar las firmas de código de barras existentes en los documentos.

Este tutorial se centra específicamente en la actualización de firmas de códigos de barras en documentos con GroupDocs.Signature para .NET. Si necesita modificar la posición, el tamaño o los datos codificados de códigos de barras existentes, esta guía le guiará a través del proceso con ejemplos de código y explicaciones claras.

## Prerrequisitos
Antes de implementar actualizaciones de firmas de código de barras con GroupDocs.Signature para .NET, asegúrese de tener los siguientes requisitos previos:

1. Entorno de desarrollo: un entorno de desarrollo .NET funcional, como Visual Studio 2017 o posterior.
2. Biblioteca GroupDocs.Signature: la biblioteca GroupDocs.Signature para .NET, que puede descargar desde [página de descarga](https://releases.groupdocs.com/signature/net/).
3. Conocimientos básicos de C#: familiaridad con los conceptos de programación de C#.
4. Documentos de muestra: Documentos que contienen firmas de código de barras que desea actualizar.

## Importar espacios de nombres
Comience importando los espacios de nombres necesarios para acceder a la funcionalidad de GroupDocs.Signature:

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

Ahora, desglosemos el proceso de actualización de firmas de códigos de barras en pasos manejables:

## Paso 1: Configurar rutas de documentos
Primero, defina las rutas para su documento de origen y dónde se guardará el documento actualizado:

```csharp
// Ruta al documento fuente con firmas de código de barras
string filePath = "sample_multiple_signatures.docx";

// Obtener el nombre del archivo para la salida
string fileName = Path.GetFileName(filePath);

// Definir el directorio de salida y la ruta del archivo
string outputDirectory = Path.Combine("Your Document Directory", "UpdateBarcode");
string outputFilePath = Path.Combine(outputDirectory, fileName);

// Asegúrese de que exista el directorio de salida
Directory.CreateDirectory(outputDirectory);
```

## Paso 2: Copiar el documento fuente
Dado que la operación de actualización modifica el documento directamente, cree una copia del documento original para conservarlo:

```csharp
// Crear una copia del documento original
File.Copy(filePath, outputFilePath, true);
```

## Paso 3: Inicializar la instancia de firma
Crear una instancia de la `Signature` clase para trabajar con el documento:

```csharp
// Inicialice la instancia de Signature con la ruta del archivo de salida
using (Signature signature = new Signature(outputFilePath))
{
    // Aquí se realizarán las operaciones de firma.
}
```

## Paso 4: Configurar las opciones de búsqueda de código de barras
Configure las opciones de búsqueda para encontrar firmas de código de barras existentes en el documento:

```csharp
// Configurar las opciones de búsqueda para firmas de código de barras
BarcodeSearchOptions options = new BarcodeSearchOptions()
{
    // Puedes filtrar por contenido de texto
    Text = "12345",
    MatchType = TextMatchType.Contains
    
    // Descomentar para buscar en todas las páginas
    // AllPages = verdadero
};
```

## Paso 5: Buscar firmas de códigos de barras
Utilice las opciones de búsqueda configuradas para encontrar firmas de código de barras en el documento:

```csharp
// Búsqueda de firmas de códigos de barras
List<BarcodeSignature> signatures = signature.Search<BarcodeSignature>(options);
```

## Paso 6: Actualizar las propiedades de la firma del código de barras
Si se encuentran firmas de código de barras, actualice sus propiedades según sea necesario:

```csharp
// Comprobar si se encontraron firmas
if (signatures.Count > 0)
{
    // Obtenga la primera firma de código de barras
    BarcodeSignature barcodeSignature = signatures[0];
    
    // Actualizar posición
    barcodeSignature.Left = 100;
    barcodeSignature.Top = 100;
    
    // Actualizar tamaño
    barcodeSignature.Width = 400;
    barcodeSignature.Height = 100;
    
    // Aplicar las actualizaciones
    bool result = signature.Update(barcodeSignature);
    
    // Comprueba el resultado
    if (result)
    {
        Console.WriteLine($"Signature with Barcode '{barcodeSignature.Text}' and encode type '{barcodeSignature.EncodeType.TypeName}' was updated in the document ['{fileName}'].");
    }
    else
    {
        Console.WriteLine($"Signature was not updated in the document! Signature with Barcode '{barcodeSignature.Text}' and encode type '{barcodeSignature.EncodeType.TypeName}' was not found!");
    }
}
else
{
    Console.WriteLine("No barcode signatures found in the document.");
}
```

## Ejemplo completo
A continuación se muestra un ejemplo completo y funcional que demuestra cómo actualizar una firma de código de barras en un documento:

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;

namespace UpdateBarcodeSignatureExample
{
    class Program
    {
        static void Main(string[] args)
        {
            // Ruta del documento
            string filePath = "sample_multiple_signatures.docx";
            
            // Definir ruta de salida
            string fileName = Path.GetFileName(filePath);
            string outputDirectory = Path.Combine(Environment.CurrentDirectory, "UpdateBarcode");
            string outputFilePath = Path.Combine(outputDirectory, fileName);
            
            // Asegúrese de que exista el directorio de salida
            Directory.CreateDirectory(outputDirectory);
            
            // Crear una copia del documento original
            File.Copy(filePath, outputFilePath, true);
            
            // Inicializar instancia de firma
            using (Signature signature = new Signature(outputFilePath))
            {
                // Configurar las opciones de búsqueda
                BarcodeSearchOptions options = new BarcodeSearchOptions
                {
                    Text = "12345",
                    MatchType = TextMatchType.Contains
                };
                
                // Búsqueda de firmas de códigos de barras
                List<BarcodeSignature> signatures = signature.Search<BarcodeSignature>(options);
                
                // Comprobar si se encontraron firmas
                if (signatures.Count > 0)
                {
                    // Obtenga la primera firma
                    BarcodeSignature barcodeSignature = signatures[0];
                    
                    // Actualizar posición y tamaño
                    barcodeSignature.Left = 100;
                    barcodeSignature.Top = 100;
                    barcodeSignature.Width = 400;
                    barcodeSignature.Height = 100;
                    
                    // Aplicar las actualizaciones
                    bool result = signature.Update(barcodeSignature);
                    
                    // Comprobar resultado
                    if (result)
                    {
                        Console.WriteLine($"Barcode signature was successfully updated in document '{fileName}'.");
                        Console.WriteLine($"Barcode text: {barcodeSignature.Text}");
                        Console.WriteLine($"Encode type: {barcodeSignature.EncodeType.TypeName}");
                        Console.WriteLine($"New position: {barcodeSignature.Left}x{barcodeSignature.Top}");
                        Console.WriteLine($"New size: {barcodeSignature.Width}x{barcodeSignature.Height}");
                        Console.WriteLine($"Output file path: {outputFilePath}");
                    }
                    else
                    {
                        Console.WriteLine("Failed to update barcode signature!");
                    }
                }
                else
                {
                    Console.WriteLine("No barcode signatures found in the document.");
                }
            }
            
            Console.WriteLine("\nPress any key to exit...");
            Console.ReadKey();
        }
    }
}
```

## Personalización avanzada de firmas de código de barras
GroupDocs.Signature proporciona opciones adicionales para personalizar las firmas de códigos de barras más allá de la posición y el tamaño básicos:

### Ajuste de las propiedades de apariencia
Personalice los aspectos visuales del código de barras:

```csharp
// Establecer el color de primer plano (color del código de barras)
barcodeSignature.ForeColor = System.Drawing.Color.Blue;

// Establecer el color de fondo
barcodeSignature.BackgroundColor = System.Drawing.Color.LightYellow;

// Ajustar la transparencia
barcodeSignature.Opacity = 0.8;
```

### Añadiendo bordes
Mejore el código de barras con bordes personalizados:

```csharp
barcodeSignature.Border.Color = System.Drawing.Color.Red;
barcodeSignature.Border.DashStyle = System.Drawing.Drawing2D.DashStyle.Dash;
barcodeSignature.Border.Weight = 2;
barcodeSignature.Border.Visible = true;
```

### Girar el código de barras
Gire la firma del código de barras a un ángulo específico:

```csharp
barcodeSignature.Angle = 30; // Girar 30 grados
```

## Conclusión
GroupDocs.Signature para .NET ofrece una solución potente y flexible para actualizar firmas de código de barras en documentos. Siguiendo los pasos descritos en este tutorial, los desarrolladores pueden implementar eficientemente la función de actualización de firmas de código de barras en sus aplicaciones .NET, optimizando así la gestión y automatización de documentos.

Con su completo conjunto de funciones y su API intuitiva, GroupDocs.Signature permite a los desarrolladores crear sofisticadas soluciones de firma de documentos que satisfacen los requisitos de las aplicaciones comerciales modernas y al mismo tiempo garantizan la integridad y la accesibilidad de los documentos.

## Preguntas frecuentes
### ¿Puedo actualizar varias firmas de códigos de barras dentro de un solo documento?
Sí, GroupDocs.Signature permite actualizar varias firmas de código de barras dentro del mismo documento. Tras buscar firmas, se puede iterar por la lista resultante y actualizar cada firma de código de barras individualmente.

### ¿GroupDocs.Signature admite diferentes formatos de códigos de barras?
Sí, GroupDocs.Signature admite una amplia variedad de formatos de códigos de barras, incluidos códigos de barras lineales (Código 128, Código 39, EAN, UPC, etc.) y códigos de barras 2D (Código QR, Data Matrix, PDF417, etc.).

### ¿Hay una versión de prueba disponible para GroupDocs.Signature para .NET?
Sí, puedes descargar una versión de prueba gratuita desde [Sitio web de GroupDocs](https://releases.groupdocs.com/signature/net/) evaluar las características de la biblioteca antes de realizar una compra.

### ¿Puedo convertir un tipo de código de barras a otro al actualizar?
No se permite la conversión directa entre tipos de códigos de barras durante las actualizaciones. Sin embargo, puede lograrlo eliminando el código de barras existente y agregando uno nuevo con el formato deseado.

### ¿Actualizar un código de barras afecta su capacidad de escaneo?
Al actualizar las propiedades del código de barras, como el tamaño y la posición, GroupDocs.Signature mantiene la integridad del escaneo. Sin embargo, tamaños extremadamente pequeños o ángulos de rotación considerables podrían afectar el rendimiento del escaneo con algunos lectores.

### ¿Dónde puedo encontrar soporte adicional para GroupDocs.Signature para .NET?
Puede encontrar apoyo integral a través de los siguientes recursos:
- [Documentación de la API](https://docs.groupdocs.com/signature/net/)
- [Referencia de API](https://reference.groupdocs.com/signature/net/)
- [Ejemplos de GitHub](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
- [Foro de soporte](https://forum.groupdocs.com/c/signature/13)
- [Blog](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
- [Soporte gratuito](https://forum.groupdocs.com/c/signature)
- [Licencia temporal](https://purchase.groupdocs.com/temporary-license/)