---
title: Firmar con múltiples opciones
linktitle: Firmar con múltiples opciones
second_title: API GroupDocs.Signature .NET
description: Aprenda a firmar documentos con múltiples opciones usando GroupDocs.Signature para .NET. Mejore la seguridad de los documentos con texto, códigos de barras, códigos QR, digitales e imágenes.
type: docs
weight: 14
url: /es/net/advanced-signature-techniques/sign-with-multiple-options/
---
## Introducción
En este tutorial, exploraremos cómo firmar un documento usando múltiples opciones de firma usando la biblioteca GroupDocs.Signature para .NET. La firma de documentos con varias opciones, como texto, código de barras, código QR, firmas digitales, de imagen y de metadatos, puede brindar versatilidad y mejorar la seguridad de los documentos.
## Requisitos previos
Antes de comenzar, asegúrese de tener los siguientes requisitos previos:
1.  Biblioteca GroupDocs.Signature para .NET: descargue e instale la biblioteca GroupDocs.Signature para .NET desde[aquí](https://releases.groupdocs.com/signature/net/).
2. Entorno de desarrollo: configure un entorno de desarrollo con .NET Framework instalado.
3. Documento para firmar: prepare el documento (p. ej., muestra.docx) que desea firmar.
4. Certificados e imágenes: prepare los certificados e imágenes necesarios para firmas digitales y de imagen.

## Importar espacios de nombres
Primero, importe los espacios de nombres necesarios para usar la biblioteca GroupDocs.Signature en su aplicación .NET:
```csharp
using System;
using System.IO;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## Paso 1: cargue el documento
```csharp
string filePath = "sample.docx";
string outputFilePath = Path.Combine("Your Document Directory", "SignWithMultiple", "SignWithMultiple.docx");
using (Signature signature = new Signature(filePath))
{
    // Tu código continúa...
}
```
## Paso 2: definir las opciones de firma
Defina varias opciones de firma de diferentes tipos y configuraciones, como firmas de texto, código de barras, código QR, digital, de imagen y de metadatos:
```csharp
TextSignOptions textOptions = new TextSignOptions("Text signature")
{
    VerticalAlignment = VerticalAlignment.Top,
    HorizontalAlignment = HorizontalAlignment.Left
};
BarcodeSignOptions barcodeOptions = new BarcodeSignOptions("123456")
{
    EncodeType = BarcodeTypes.Code128,
    Left = 0,
    Top = 150,
    Height = 50,
    Width = 200
};
// Definir otras opciones de firma (p. ej., código QR, digital, imagen, metadatos)...
```
## Paso 3: cree una lista de opciones de firma
Defina una lista de opciones de firma que contenga todas las opciones definidas previamente:
```csharp
List<SignOptions> listOptions = new List<SignOptions>();
listOptions.Add(textOptions);
listOptions.Add(barcodeOptions);
// Agregue otras opciones de firma a la lista...
```
## Paso 4: Firme el documento
Firme el documento con la lista de opciones de firma y guarde el documento firmado:
```csharp
SignResult result = signature.Sign(outputFilePath, listOptions);
Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).\nFile saved at {outputFilePath}.");
```

## Conclusión
La firma de documentos con múltiples opciones utilizando GroupDocs.Signature para .NET proporciona una solución sólida para mejorar la seguridad y versatilidad de los documentos. Si sigue los pasos descritos en este tutorial, podrá integrar sin problemas varios tipos de firmas en sus aplicaciones .NET.
## Preguntas frecuentes
### ¿Puedo utilizar imágenes personalizadas para firmas digitales?
Sí, puede especificar imágenes personalizadas para firmas digitales utilizando la biblioteca GroupDocs.Signature.
### ¿GroupDocs.Signature es compatible con diferentes formatos de documentos?
Sí, GroupDocs.Signature admite varios formatos de documentos, incluidos DOCX, PDF, PPTX y más.
### ¿Puedo personalizar la apariencia de las firmas de texto?
Por supuesto, puedes personalizar la apariencia de las firmas de texto, incluido el tamaño, el color y el estilo de la fuente.
### ¿GroupDocs.Signature proporciona cifrado para firmas digitales?
Sí, GroupDocs.Signature ofrece opciones de cifrado para firmas digitales para garantizar la seguridad de los documentos.
### ¿Existe una versión de prueba disponible para GroupDocs.Signature para .NET?
 Sí, puede descargar una versión de prueba gratuita de GroupDocs.Signature para .NET desde[aquí](https://releases.groupdocs.com/).