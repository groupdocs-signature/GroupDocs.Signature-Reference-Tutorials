---
title: Firmar documentos con código QR usando GroupDocs.Signature
linktitle: Firmar con código QR
second_title: API GroupDocs.Signature .NET
description: Aprenda a agregar firmas de códigos QR a sus documentos con GroupDocs.Signature para .NET. Mejore la seguridad y la autenticación sin esfuerzo.
weight: 15
url: /es/net/advanced-signature-techniques/sign-with-qr-code/
---

# Firmar documentos con código QR usando GroupDocs.Signature

## Introducción
En este tutorial, recorreremos el proceso de firma de documentos con un código QR utilizando GroupDocs.Signature para .NET. GroupDocs.Signature para .NET es una potente API que permite a los desarrolladores agregar varios tipos de firmas a documentos digitales mediante programación. Firmar documentos con códigos QR puede proporcionar una capa adicional de seguridad y autenticación a sus documentos.
## Requisitos previos
Antes de comenzar, asegúrese de tener instalados los siguientes requisitos previos:
1.  GroupDocs.Signature para .NET: puede descargar la biblioteca desde[sitio web](https://releases.groupdocs.com/signature/net/).
2. Entorno de desarrollo: asegúrese de tener un entorno de desarrollo .NET configurado en su máquina.
3. Documento de muestra: prepare un documento de muestra (por ejemplo, PDF) que desee firmar con un código QR.

## Importación de espacios de nombres necesarios
Antes de profundizar en el código, importemos los espacios de nombres necesarios:
```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

## Paso 1: definir rutas de archivos
```csharp
string filePath = "sample.pdf";
string fileName = Path.GetFileName(filePath);
string outputFilePath = Path.Combine("Your Document Directory", "SignWithQRCode", fileName);
```
 Asegúrese de reemplazar`"Your Document Directory"` con la ruta al directorio donde desea guardar el documento firmado.
## Paso 2: inicializar el objeto de firma
```csharp
using (Signature signature = new Signature(filePath))
{
    //El código para firmar va aquí.
}
```
 Inicializar un`Signature` objeto con la ruta al documento que desea firmar.
## Paso 3: crear QRCodeSignOptions
```csharp
QrCodeSignOptions options = new QrCodeSignOptions("JohnSmith")
{
    EncodeType = QrCodeTypes.QR,
    Left = 50,
    Top = 150,
    Width = 200,
    Height = 200
};
```
 Crear un`QrCodeSignOptions` objeto con la configuración deseada para la firma del código QR. Puedes personalizar parámetros como el texto a codificar, la posición y las dimensiones del código QR.
## Paso 4: Firme el documento
```csharp
SignResult result = signature.Sign(outputFilePath, options);
```
 Utilizar el`Sign` método de la`Signature` objeto para firmar el documento con las opciones especificadas. Este método devuelve un`SignResult` objeto que contiene información sobre el proceso de firma.
## Paso 5: Mostrar resultado
```csharp
Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).\nFile saved at {outputFilePath}.");
```
Muestra un mensaje indicando el éxito del proceso de firma y la ubicación donde se guarda el documento firmado.

## Conclusión
En este tutorial, aprendimos cómo firmar documentos con un código QR usando GroupDocs.Signature para .NET. Siguiendo estos sencillos pasos, puede agregar firmas de códigos QR a sus documentos digitales, mejorando la seguridad y la autenticación.

## Preguntas frecuentes
### ¿Puedo personalizar la apariencia del código QR?
Sí, puede personalizar varios parámetros, como el tamaño, la posición y el tipo de codificación del código QR, según sus requisitos.
### ¿Qué formatos de documentos se admiten para firmar con códigos QR?
GroupDocs.Signature para .NET admite una amplia gama de formatos de documentos, incluidos PDF, Word, Excel, PowerPoint y más.
### ¿Es posible firmar varios documentos en un proceso por lotes?
Por supuesto, puedes utilizar GroupDocs.Signature para .NET para firmar varios documentos simultáneamente, agilizando tu flujo de trabajo.
### ¿Puedo verificar la autenticidad de un documento firmado con un código QR?
Sí, GroupDocs.Signature para .NET proporciona mecanismos de verificación para garantizar la integridad y autenticidad de los documentos firmados.
### ¿Existe una versión de prueba disponible para probar la funcionalidad antes de comprar?
 Sí, puedes descargar una versión de prueba gratuita desde[sitio web](https://releases.groupdocs.com/) para evaluar las características y capacidades de GroupDocs.Signature para .NET.