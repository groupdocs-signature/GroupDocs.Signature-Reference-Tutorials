---
title: Presentación de letreros con metadatos
linktitle: Presentación de letreros con metadatos
second_title: API GroupDocs.Signature .NET
description: Aprenda a firmar archivos de presentación con metadatos usando GroupDocs.Signature para .NET. Mejore la integridad de los documentos y agregue información valiosa.
weight: 12
url: /es/net/document-signing/sign-presentation-with-metadata/
---
## Introducción
En este tutorial, aprenderemos cómo firmar un archivo de presentación (PPTX) con metadatos usando la biblioteca GroupDocs.Signature para .NET. Firmar presentaciones con metadatos agrega información valiosa al documento, como el nombre del autor, la fecha de creación, el ID del documento, el ID de la firma y varios valores numéricos.
## Requisitos previos
Antes de comenzar, asegúrese de tener lo siguiente:
1.  GroupDocs.Signature para la biblioteca .NET: descargue e instale la biblioteca desde[aquí](https://releases.groupdocs.com/signature/net/).
2. Entorno de desarrollo: asegúrese de tener configurado un entorno de desarrollo .NET.
3. Archivo de presentación: tenga un archivo de presentación de muestra (formato PPTX) listo para firmar.
4. Comprensión básica de C#: será beneficiosa la familiaridad con el lenguaje de programación C#.

## Importar espacios de nombres
Antes de profundizar en el código, importemos los espacios de nombres necesarios:
```csharp
using System;
using System.IO;
    using GroupDocs.Signature;
    using GroupDocs.Signature.Domain;
    using GroupDocs.Signature.Options;
```
## Paso 1: cargar el archivo de presentación
```csharp
string filePath = "sample.pptx";
```
 Reemplazar`"sample.pptx"` con la ruta a su archivo de presentación.
## Paso 2: especificar la ruta del archivo de salida
```csharp
string outputFilePath = Path.Combine("Your Document Directory", "SignPresentationWithMetadata", "SignedWithMetadata.pptx");
```
Especifique el directorio donde desea guardar el archivo de presentación firmado junto con el nombre del archivo.
## Paso 3: inicializar el objeto de firma
```csharp
using (Signature signature = new Signature(filePath))
```
Inicialice un objeto Firma proporcionando la ruta al archivo de presentación.
## Paso 4: Definir las opciones de firma de metadatos
```csharp
MetadataSignOptions options = new MetadataSignOptions();
```
Cree una instancia de MetadataSignOptions para definir opciones de firma de metadatos.
## Paso 5: crear firmas de metadatos
```csharp
PresentationMetadataSignature[] signatures = new PresentationMetadataSignature[]
{
    new PresentationMetadataSignature("Author", "Mr.Scherlock Holmes"),
    new PresentationMetadataSignature("CreatedOn", DateTime.Now),
    new PresentationMetadataSignature("DocumentId", 123456),
    new PresentationMetadataSignature("SignatureId", 123.456D),
    new PresentationMetadataSignature("Amount", 123.456M),
    new PresentationMetadataSignature("Total", 123.456F)
};
```
Cree una matriz de objetos PresentationMetadataSignature, cada uno de los cuales represente una firma de metadatos. Puede agregar varios tipos de metadatos, incluidos cadenas, fecha y hora, enteros, dobles, decimales y flotantes.
## Paso 6: agregar firmas a las opciones
```csharp
options.Signatures.AddRange(signatures);
```
Agregue las firmas de metadatos creadas al objeto MetadataSignOptions.
## Paso 7: firmar el documento
```csharp
SignResult result = signature.Sign(outputFilePath, options);
```
Firme el archivo de presentación con metadatos usando las opciones especificadas y guarde el archivo firmado en la ruta de salida.
## Paso 8: Mostrar resultado
```csharp
Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).\nFile saved at {outputFilePath}.");
```
Muestra un mensaje de éxito junto con la cantidad de firmas aplicadas y la ruta donde se guarda el archivo firmado.

## Conclusión
En este tutorial, aprendimos cómo firmar un archivo de presentación con metadatos usando la biblioteca GroupDocs.Signature para .NET. Agregar firmas de metadatos mejora la integridad del documento y proporciona información valiosa sobre su contenido.

## Preguntas frecuentes
### ¿Puedo firmar otros formatos de documentos además de PPTX con metadatos usando GroupDocs.Signature para .NET?
Sí, GroupDocs.Signature admite varios formatos de documentos, incluidos Word, Excel, PDF y más, para firmar con metadatos.
### ¿GroupDocs.Signature para .NET es compatible con .NET Core?
Sí, la biblioteca es compatible tanto con .NET Framework como con .NET Core.
### ¿Puedo personalizar la apariencia de las firmas de metadatos?
Sí, puede personalizar la apariencia, la posición y otras propiedades de las firmas de metadatos según sus requisitos.
### ¿GroupDocs.Signature para .NET proporciona cifrado para documentos firmados?
Sí, GroupDocs.Signature ofrece opciones de cifrado para proteger los documentos firmados contra el acceso no autorizado.
### ¿Existe una versión de prueba disponible para probar antes de comprar?
 Sí, puede aprovechar una prueba gratuita de GroupDocs.Signature para .NET desde[aquí](https://releases.groupdocs.com/).