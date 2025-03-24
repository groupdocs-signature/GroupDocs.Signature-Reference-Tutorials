---
title: Firmar con texto usando GroupDocs.Signature para .NET
linktitle: Firmar con texto
second_title: API GroupDocs.Signature .NET
description: Aprenda a firmar documentos con texto usando GroupDocs.Signature para .NET. Guía paso a paso para agregar firmas de texto mediante programación.
weight: 17
url: /es/net/advanced-signature-techniques/sign-with-text/
---
## Introducción
En la era digital, firmar documentos electrónicamente se ha convertido en una práctica habitual, ahorrando tiempo y recursos. GroupDocs.Signature para .NET ofrece una solución integral para agregar firmas de texto a varios formatos de documentos mediante programación. En este tutorial, lo guiaremos a través del proceso de firmar un documento con texto usando GroupDocs.Signature para .NET.
## Requisitos previos
Antes de sumergirnos en el tutorial, asegúrese de tener los siguientes requisitos previos:
1.  GroupDocs.Signature para .NET: asegúrese de tener instalada la biblioteca GroupDocs.Signature para .NET. Puedes descargarlo desde[aquí](https://releases.groupdocs.com/signature/net/).
2. Entorno de desarrollo: Tener un entorno de trabajo configurado para el desarrollo .NET.
3. Documento: prepare el documento (p. ej., PDF, Word) que desea firmar con texto.

## Importar espacios de nombres
Primero, debe importar los espacios de nombres necesarios a su proyecto .NET para utilizar las funcionalidades de GroupDocs.Signature.
```csharp
using System;
using System.IO;
using System.Drawing;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

Dividamos el proceso de firmar un documento con texto en varios pasos:
## Paso 1: cargar el documento
Cargue el documento que desea firmar con texto.
```csharp
string filePath = "sample.pdf"; // Ruta al documento
string fileName = Path.GetFileName(filePath);
```
## Paso 2: establecer la ruta del archivo de salida
Defina la ruta del archivo de salida donde se guardará el documento firmado.
```csharp
string outputFilePath = Path.Combine("Your Document Directory", "SignWithText", fileName);
```
## Paso 3: crear opciones de firma
Configure las opciones para la firma de texto, incluido el contenido, la posición, el tamaño, el color y la fuente del texto.
```csharp
TextSignOptions options = new TextSignOptions("John Smith")
{
    Left = 50, // Establecer posición de firma
    Top = 200,
    Width = 100, // Establecer rectángulo de firma
    Height = 30,
    ForeColor = Color.Red, // Establecer color de texto
    Font = new SignatureFont { Size = 14, FamilyName = "Comic Sans MS" } // Establecer fuente
};
```
## Paso 4: firmar el documento
Utilice GroupDocs.Signature para firmar el documento con las opciones especificadas y guardar el documento firmado en la ruta del archivo de salida.
```csharp
using (Signature signature = new Signature(filePath))
{
    SignResult result = signature.Sign(outputFilePath, options); // Firmar documento
    Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).\nFile saved at {outputFilePath}.");
}
```

## Conclusión
En este tutorial, aprendimos cómo firmar un documento con texto usando GroupDocs.Signature para .NET. Si sigue estos pasos, podrá agregar firmas de texto a sus documentos de manera eficiente mediante programación, mejorando la seguridad y la autenticidad.
## Preguntas frecuentes
### ¿Puedo personalizar la apariencia de la firma de texto?
Sí, puedes personalizar varios parámetros como el color, la fuente, el tamaño y la posición de la firma del texto según tus preferencias.
### ¿GroupDocs.Signature es compatible con múltiples formatos de documentos?
Sí, GroupDocs.Signature admite varios formatos de documentos, incluidos PDF, Word, Excel, PowerPoint y más.
### ¿Puedo agregar varias firmas de texto a un solo documento?
Por supuesto, puedes agregar varias firmas de texto a un documento, cada una con su propio conjunto de opciones de personalización.
### ¿GroupDocs.Signature garantiza la integridad del documento después de la firma?
Sí, GroupDocs.Signature emplea algoritmos criptográficos sólidos para garantizar la integridad del documento y evitar la manipulación después de la firma.
### ¿Existe una versión de prueba disponible para probar antes de comprar?
 Sí, puedes descargar una versión de prueba gratuita desde[aquí](https://releases.groupdocs.com/) para explorar las funciones antes de realizar una compra.