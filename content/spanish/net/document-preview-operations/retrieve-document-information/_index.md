---
title: Recuperar información del documento
linktitle: Recuperar información del documento
second_title: API GroupDocs.Signature .NET
description: Mejore la gestión de documentos en .NET con GroupDocs.Signature. Recuperar información del documento paso a paso. Soporta varios formatos.
weight: 11
url: /es/net/document-preview-operations/retrieve-document-information/
---
## Introducción
En el ámbito de la documentación digital, garantizar la autenticidad y la integridad es primordial. GroupDocs.Signature para .NET proporciona una solución sólida para administrar firmas de documentos dentro del entorno .NET. En este tutorial, profundizamos en el proceso de recuperación de información de documentos utilizando GroupDocs.Signature para .NET, desglosando cada paso para una comprensión integral.
## Requisitos previos
Antes de sumergirse en el tutorial, asegúrese de cumplir con los siguientes requisitos previos:
1.  Instalación: Instale GroupDocs.Signature para .NET descargándolo desde[aquí](https://releases.groupdocs.com/signature/net/).
2. Entorno .NET: tener conocimientos prácticos del marco .NET.
3. Documento: prepare un documento de muestra (por ejemplo, "sample_multiple_signatures.docx") para fines de prueba.

## Importando espacios de nombres
Antes de continuar con el proceso de recuperación de la firma del documento, importe los espacios de nombres necesarios:
```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
```

## Paso 1: Establecer la ruta del archivo del documento:
Defina la ruta del archivo para el documento del que desea recuperar información.
```csharp
string filePath = "sample_multiple_signatures.docx";
```
## Paso 2: Crear una instancia del objeto de firma:
 Crear una instancia del`Signature` clase pasando la ruta del archivo del documento.
```csharp
using (Signature signature = new Signature(filePath))
{

}
```
## Paso 3: recuperar la información del documento:
 Utilice el`GetDocumentInfo()` método para obtener información completa sobre el documento.
```csharp
IDocumentInfo documentInfo = signature.GetDocumentInfo();
```
## Paso 4: Mostrar propiedades del documento:
Genere varias propiedades del documento, como formato, extensión, tamaño, recuento de páginas, etc.
```csharp
Console.WriteLine($"Document properties {Path.GetFileName(filePath)}:");
Console.WriteLine($" - format : {documentInfo.FileType.FileFormat}");
Console.WriteLine($" - extension : {documentInfo.FileType.Extension}");
Console.WriteLine($" - size : {documentInfo.Size}");
Console.WriteLine($" - page count : {documentInfo.PageCount}");
Console.WriteLine($" - Form Fields count : {documentInfo.FormFields.Count}");
Console.WriteLine($" - Text signatures count : {documentInfo.TextSignatures.Count}");
Console.WriteLine($" - Image signatures count : {documentInfo.ImageSignatures.Count}");
Console.WriteLine($" - Digital signatures count : {documentInfo.DigitalSignatures.Count}");
Console.WriteLine($" - Barcode signatures count : {documentInfo.BarcodeSignatures.Count}");
Console.WriteLine($" - QrCode signatures count : {documentInfo.QrCodeSignatures.Count}");
Console.WriteLine($" - FormField signatures count : {documentInfo.FormFieldSignatures.Count}");
foreach (PageInfo pageInfo in documentInfo.Pages)
{
   Console.WriteLine($" - page-{pageInfo.PageNumber} Width {pageInfo.Width}, Height {pageInfo.Height}");
}
```


## Conclusión
GroupDocs.Signature para .NET ofrece un potente conjunto de herramientas para gestionar firmas de documentos sin problemas dentro del marco .NET. Si sigue los pasos descritos en esta guía, podrá recuperar de manera eficiente información completa sobre sus documentos, lo que facilitará capacidades mejoradas de administración de documentos.

## Preguntas frecuentes
### ¿Puede GroupDocs.Signature para .NET manejar múltiples formatos de documentos?
Sí, GroupDocs.Signature admite una amplia gama de formatos de documentos, incluidos, entre otros, DOCX, PDF, PNG y JPEG.
### ¿Existe una versión de prueba disponible para GroupDocs.Signature para .NET?
 Sí, puedes acceder a la versión de prueba desde[aquí](https://releases.groupdocs.com/).
### ¿GroupDocs.Signature para .NET proporciona soporte para firmas digitales?
Por supuesto, GroupDocs.Signature ofrece un sólido soporte para firmas digitales, lo que garantiza la autenticidad e integridad de los documentos.
### ¿Dónde puedo encontrar documentación adicional y soporte para GroupDocs.Signature para .NET?
 Puede consultar la documentación completa.[aquí](https://tutorials.groupdocs.com/signature/net/) y para obtener ayuda, visite el foro de GroupDocs.[aquí](https://forum.groupdocs.com/c/signature/13).
### ¿Se pueden obtener licencias temporales de GroupDocs.Signature para .NET?
 Sí, hay licencias temporales disponibles para su compra.[aquí](https://purchase.groupdocs.com/temporary-license/).