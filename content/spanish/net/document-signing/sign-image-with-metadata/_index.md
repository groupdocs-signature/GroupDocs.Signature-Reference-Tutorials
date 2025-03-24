---
title: Firmar imagen con metadatos
linktitle: Firmar imagen con metadatos
second_title: API GroupDocs.Signature .NET
description: Aprenda a firmar imágenes con metadatos en .NET usando GroupDocs.Signature. Solución de firma de metadatos fácil, eficiente y personalizable.
weight: 10
url: /es/net/document-signing/sign-image-with-metadata/
---
## Introducción
GroupDocs.Signature para .NET permite a los desarrolladores firmar imágenes con metadatos de manera eficiente. Este tutorial le guiará a través del proceso paso a paso.
## Requisitos previos
Antes de comenzar, asegúrese de tener lo siguiente:
1. GroupDocs.Signature para .NET: instale el paquete GroupDocs.Signature en su proyecto .NET. Puedes descargarlo desde[aquí](https://releases.groupdocs.com/signature/net/).   
2. Archivo de imagen: prepare el archivo de imagen que desea firmar con metadatos.

## Importar espacios de nombres
Asegúrese de importar los espacios de nombres necesarios en su código C#:
```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## Paso 1: cargar el archivo de imagen
Primero, especifique la ruta a su archivo de imagen y el directorio de salida de la imagen firmada con metadatos:
```csharp
string filePath = "sample.png";            
string outputFilePath = Path.Combine("Your Document Directory", "SignImageWithMetadata", "SignedWithMetadata.png");
```
## Paso 2: crear firmas de metadatos
A continuación, cree diferentes firmas de metadatos y agréguelas a la colección de firmas de opciones:
```csharp
using (Signature signature = new Signature(filePath))
{
    ushort imgsMetadataId = 41996;
    MetadataSignOptions options = new MetadataSignOptions();
    options
        .Add(new ImageMetadataSignature(imgsMetadataId++, "Mr.Scherlock Holmes")) // Valor de cadena
        .Add(new ImageMetadataSignature(imgsMetadataId++, DateTime.Now))          // Valor de fecha y hora
        .Add(new ImageMetadataSignature(imgsMetadataId++, 123456))                // Valor entero
        .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456D))              // valor doble
        .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456M))              // valor decimal
        .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456F));             // Valor flotante
    
    // firmar documento para presentar
    SignResult result = signature.Sign(outputFilePath, options);
    Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).\nFile saved at {outputFilePath}.");
}
```

## Conclusión
En este tutorial, aprendió cómo firmar una imagen con metadatos usando GroupDocs.Signature para .NET. Si sigue estos pasos, podrá incorporar fácilmente firmas de metadatos en sus aplicaciones .NET.

## Preguntas frecuentes
### ¿Puedo firmar varias imágenes con metadatos usando GroupDocs.Signature para .NET?
Sí, puede firmar varias imágenes con metadatos iterando a través de cada archivo de imagen y aplicando las firmas de metadatos.
### ¿Existe una versión de prueba disponible para GroupDocs.Signature para .NET?
 Sí, puedes descargar la versión de prueba desde[aquí](https://releases.groupdocs.com/).
### ¿GroupDocs.Signature para .NET admite otros formatos de archivo además de las imágenes?
Sí, GroupDocs.Signature admite varios formatos de archivo, incluidos PDF, Word, Excel y más.
### ¿Puedo personalizar la apariencia de la firma de metadatos?
Sí, puede personalizar la apariencia de la firma de metadatos, como el tamaño, el color y la posición de la fuente.
### ¿Dónde puedo obtener soporte para GroupDocs.Signature para .NET?
 Puede obtener soporte en el foro GroupDocs.Signature[aquí](https://forum.groupdocs.com/c/signature/13).