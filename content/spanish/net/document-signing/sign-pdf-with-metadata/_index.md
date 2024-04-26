---
title: Firmar PDF con metadatos
linktitle: Firmar PDF con metadatos
second_title: API GroupDocs.Signature .NET
description: Aprenda a firmar documentos PDF con metadatos usando GroupDocs.Signature para .NET. Mejore la trazabilidad y autenticidad de los documentos fácilmente.
type: docs
weight: 11
url: /es/net/document-signing/sign-pdf-with-metadata/
---
## Introducción
En este tutorial, aprenderemos cómo firmar un documento PDF con metadatos usando GroupDocs.Signature para .NET. Agregar metadatos a un PDF puede proporcionar información adicional sobre el documento, como la autoría, la fecha de creación, el ID del documento y más.
## Requisitos previos
Antes de comenzar, asegúrese de tener lo siguiente:
1.  GroupDocs.Signature para .NET: puede descargarlo desde[aquí](https://releases.groupdocs.com/signature/net/).
2. Un documento PDF: tenga un archivo PDF de muestra listo para firmar.
3. Conocimientos básicos de programación en C#: se requiere familiaridad con la sintaxis de C# para comprender los ejemplos de código.
## Importar espacios de nombres
Primero, asegúrese de importar los espacios de nombres necesarios para acceder a las clases y métodos requeridos:
```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## Paso 1: cargue el documento PDF
Cargue el documento PDF que desea firmar:
```csharp
string filePath = "sample.pdf";
```
## Paso 2: especificar la ruta del archivo de salida
Defina la ruta del archivo de salida donde se guardará el PDF firmado con metadatos:
```csharp
string outputFilePath = Path.Combine("Your Document Directory", "SignPdfWithMetadata", "SignedWithMetadata.pdf");
```
## Paso 3: crear una instancia de firma
Inicialice una instancia de Firma proporcionando la ruta al documento PDF:
```csharp
using (Signature signature = new Signature(filePath))
{
    // El código relacionado con la firma irá aquí
}
```
## Paso 4: definir opciones de metadatos
Cree MetadataSignOptions y agregue campos de metadatos con sus respectivos valores:
```csharp
MetadataSignOptions options = new MetadataSignOptions();
options
    .Add(new PdfMetadataSignature("Author", "Mr.Sherlock Holmes")) // Valor de cadena
    .Add(new PdfMetadataSignature("CreatedOn", DateTime.Now))       // Valores de fecha y hora
    .Add(new PdfMetadataSignature("DocumentId", 123456))            // Valor entero
    .Add(new PdfMetadataSignature("SignatureId", 123.456D))         // valor doble
    .Add(new PdfMetadataSignature("Amount", 123.456M))              // valor decimal
    .Add(new PdfMetadataSignature("Total", 123.456F));              // Valor flotante
```
## Paso 5: Firme el documento
Firme el documento PDF con las opciones de metadatos especificadas y guarde el documento firmado:
```csharp
SignResult result = signature.Sign(outputFilePath, options);
Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).\nFile saved at {outputFilePath}.");
```

## Conclusión
En este tutorial, cubrimos cómo firmar un documento PDF con metadatos usando GroupDocs.Signature para .NET. Si sigue la guía paso a paso, puede agregar fácilmente información de metadatos, como la autoría, la fecha de creación y más, a sus archivos PDF, mejorando su utilidad y trazabilidad.
## Preguntas frecuentes
### ¿Puedo agregar campos de metadatos personalizados a mis documentos PDF?
Sí, puede agregar campos de metadatos personalizados especificando el nombre del campo y su valor correspondiente usando GroupDocs.Signature para .NET.
### ¿GroupDocs.Signature para .NET es compatible con todas las versiones de .NET Framework?
GroupDocs.Signature para .NET es compatible con varias versiones de .NET Framework, lo que garantiza flexibilidad y facilidad de integración.
### ¿GroupDocs.Signature admite la firma de otros formatos de documentos además de PDF?
Sí, GroupDocs.Signature admite una amplia gama de formatos de documentos, incluidos Word, Excel, PowerPoint y más.
### ¿Puedo firmar varios documentos de forma masiva utilizando GroupDocs.Signature para .NET?
Sí, puede firmar varios documentos de forma masiva recorriendo una lista de archivos y aplicando el proceso de firma mediante programación.
### ¿Hay soporte técnico disponible para los usuarios de GroupDocs.Signature?
 Sí, GroupDocs brinda soporte técnico dedicado a través de sus foros. Puedes acceder al foro de soporte.[aquí](https://forum.groupdocs.com/c/signature/13).