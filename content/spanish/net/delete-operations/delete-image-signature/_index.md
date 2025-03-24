---
title: Eliminar firma de imagen
linktitle: Eliminar firma de imagen
second_title: API GroupDocs.Signature .NET
description: Aprenda cómo eliminar firmas de imágenes de documentos usando GroupDocs.Signature para .NET. Siga nuestra guía paso a paso para una gestión eficiente de firmas.
weight: 14
url: /es/net/delete-operations/delete-image-signature/
---

# Eliminar firma de imagen

## Introducción
En este tutorial, exploraremos cómo eliminar firmas de imágenes de documentos usando GroupDocs.Signature para .NET. GroupDocs.Signature es una poderosa biblioteca que permite a los desarrolladores trabajar con firmas digitales, sellos y campos de formulario dentro de varios formatos de documentos.
## Requisitos previos
Antes de comenzar, asegúrese de tener lo siguiente:
### 1. GroupDocs.Signature para .NET
 Descargue e instale GroupDocs.Signature para .NET desde[sitio web](https://releases.groupdocs.com/signature/net/). Siga las instrucciones de instalación proporcionadas en la documentación.
### 2. Marco .NET
Asegúrese de tener .NET Framework instalado en su máquina.
## Importar espacios de nombres
Incluya los espacios de nombres necesarios en su proyecto:
```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
Dividamos el proceso de eliminación de firmas de imágenes en varios pasos:
## Paso 1: definir rutas de archivos
Primero, especifique las rutas para el documento de entrada y el documento de salida después de eliminar la firma:
```csharp
string filePath = "sample_multiple_signatures.docx";
string fileName = Path.GetFileName(filePath);
string outputFilePath = Path.Combine("Your Document Directory", "DeleteImage", fileName);
```
## Paso 2: copie el archivo fuente
 desde el`Delete`método funciona con el mismo documento, es esencial copiar el archivo fuente a otra ubicación:
```csharp
File.Copy(filePath, outputFilePath, true);
```
## Paso 3: inicializar el objeto de firma
 Crear una instancia del`Signature` clase y especifique la ruta al documento de salida:
```csharp
using (Signature signature = new Signature(outputFilePath))
{
    // El código va aquí.
}
```
## Paso 4: busque firmas de imágenes
Defina opciones de búsqueda y busque firmas de imágenes dentro del documento:
```csharp
ImageSearchOptions options = new ImageSearchOptions();
List<ImageSignature> signatures = signature.Search<ImageSignature>(options);
```
## Paso 5: eliminar la firma de la imagen
Si se encuentran firmas de imágenes, elimine la primera:
```csharp
if (signatures.Count > 0)
{
    ImageSignature imageSignature = signatures[0];
    bool result = signature.Delete(imageSignature);
    if (result)
    {
        Console.WriteLine($"Image signature at location {imageSignature.Left}x{imageSignature.Top} and Size {imageSignature.Size} was deleted from document ['{fileName}'].");
    }
    else
    {
        Helper.WriteError($"Signature was not deleted from the document! Signature at location {imageSignature.Left}x{imageSignature.Top} and Size {imageSignature.Size} was not found!");
    }
}
```
## Conclusión
En este tutorial, aprendimos cómo eliminar firmas de imágenes de documentos usando GroupDocs.Signature para .NET. Siguiendo la guía paso a paso, los desarrolladores pueden gestionar de manera eficiente las firmas digitales dentro de sus aplicaciones.
## Preguntas frecuentes
### ¿Puedo eliminar varias firmas de imágenes de un documento?
 Sí, puede modificar el código para eliminar varias firmas de imágenes iterando sobre el`signatures` lista.
### ¿GroupDocs.Signature admite otros formatos de documentos además de DOCX?
Sí, GroupDocs.Signature admite una amplia gama de formatos de documentos, incluidos PDF, PPT, XLS y más.
### ¿Existe una versión de prueba disponible para GroupDocs.Signature para .NET?
 Sí, puedes descargar una versión de prueba gratuita desde[sitio web](https://releases.groupdocs.com/).
### ¿Cómo puedo obtener soporte para GroupDocs.Signature?
 Puedes visitar el[Foro GroupDocs.Signature](https://forum.groupdocs.com/c/signature/13) para asistencia y apoyo.
### ¿Puedo comprar una licencia temporal para GroupDocs.Signature?
 Sí, puede comprar una licencia temporal en el[pagina de compra](https://purchase.groupdocs.com/temporary-license/).