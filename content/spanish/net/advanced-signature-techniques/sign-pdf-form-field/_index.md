---
title: Firmar PDF con campo de formulario
linktitle: Firmar PDF con campo de formulario
second_title: API GroupDocs.Signature .NET
description: Aprenda a firmar documentos PDF con campos de formulario usando GroupDocs.Signature para .NET. Garantice la autenticidad y la integridad de los documentos sin esfuerzo.
weight: 10
url: /es/net/advanced-signature-techniques/sign-pdf-form-field/
---

# Firmar PDF con campo de formulario

## Introducción
Las firmas digitales proporcionan una forma segura y legalmente vinculante de firmar documentos electrónicamente, garantizando su autenticidad e integridad. En este tutorial, aprenderemos cómo firmar un documento PDF que contiene campos de formulario usando la biblioteca GroupDocs.Signature para .NET.
## Requisitos previos
Antes de comenzar, asegúrese de tener los siguientes requisitos previos:
1.  GroupDocs.Signature para la biblioteca .NET: descargue e instale la biblioteca desde[aquí](https://releases.groupdocs.com/signature/net/).
2. Entorno de desarrollo: configure un entorno de desarrollo .NET.
3. Documento PDF: tenga un documento PDF con campos de formulario listos para firmar.

## Importar espacios de nombres
Asegúrese de importar los espacios de nombres necesarios a su proyecto:
```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## Paso 1: cargue el documento PDF
Primero, especifique la ruta a su documento PDF:
```csharp
string filePath = "sample.pdf";
```
## Paso 2: definir la ruta de salida
Defina la ruta donde se guardará el documento firmado:
```csharp
string outputFilePath = Path.Combine("Your Document Directory", "SignPdfWithFormField", "SignedWithFormField.pdf");
```
## Paso 3: inicializar el objeto de firma
 Crear una instancia del`Signature` class y pásale la ruta del archivo PDF:
```csharp
using (Signature signature = new Signature(filePath))
{
    // El código de firma irá aquí
}
```
## Paso 4: crear una instancia de la firma del campo del formulario
A continuación, cree una instancia de una firma de campo de formulario de texto con el nombre y valor del campo deseado:
```csharp
FormFieldSignature textSignature = new TextFormFieldSignature("FieldText", "Value1");
```
## Paso 5: configurar las opciones de firma
Cree opciones para firmar según la firma del campo del formulario de texto. Puede especificar la posición y el tamaño de la firma:
```csharp
FormFieldSignOptions options = new FormFieldSignOptions(textSignature)
{
    Top = 150,
    Left = 50,
    Height = 50,
    Width = 200
};
```
## Paso 6: Firme el documento
Firme el documento utilizando las opciones especificadas y guarde el documento firmado en la ruta de salida:
```csharp
SignResult result = signature.Sign(outputFilePath, options);
```

## Conclusión
En este tutorial, aprendimos cómo firmar un documento PDF que contiene campos de formulario usando GroupDocs.Signature para .NET. Las firmas digitales son esenciales para garantizar la autenticidad e integridad de los documentos en diversas industrias.
## Preguntas frecuentes
### ¿Puedo firmar documentos PDF mediante programación usando GroupDocs.Signature para .NET?
Sí, puede firmar documentos PDF mediante programación utilizando GroupDocs.Signature para .NET como se demuestra en este tutorial.
### ¿GroupDocs.Signature para .NET es adecuado para aplicaciones de nivel empresarial?
¡Absolutamente! GroupDocs.Signature para .NET es robusto y escalable, lo que lo hace adecuado para aplicaciones de nivel empresarial.
### ¿GroupDocs.Signature para .NET admite otros formatos de documentos además de PDF?
Sí, GroupDocs.Signature para .NET admite una amplia gama de formatos de documentos, incluidos Word, Excel, PowerPoint y más.
### ¿Puedo personalizar la apariencia de la firma?
Sí, puedes personalizar la apariencia de la firma ajustando varios parámetros como el color, la fuente, el tamaño y la posición.
### ¿Existe una versión de prueba disponible para GroupDocs.Signature para .NET?
 Sí, puede descargar una versión de prueba gratuita de GroupDocs.Signature para .NET desde[aquí](https://releases.groupdocs.com/).