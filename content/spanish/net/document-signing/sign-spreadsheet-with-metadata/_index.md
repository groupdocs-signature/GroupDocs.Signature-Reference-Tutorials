---
title: Firmar hoja de cálculo con metadatos
linktitle: Firmar hoja de cálculo con metadatos
second_title: API GroupDocs.Signature .NET
description: Aprenda a firmar hojas de cálculo con metadatos usando Groupdocs.Signature para .NET. Mejore la integridad y verificación de los documentos con firmas de metadatos.
weight: 13
url: /es/net/document-signing/sign-spreadsheet-with-metadata/
---

# Firmar hoja de cálculo con metadatos

## Introducción
En este tutorial, recorreremos el proceso de firmar una hoja de cálculo con metadatos usando Groupdocs.Signature para .NET. La firma de metadatos le permite incorporar información adicional en sus documentos, proporcionando contexto o verificación. Al final de esta guía, podrá aplicar firmas de metadatos a sus hojas de cálculo sin esfuerzo.
## Requisitos previos
Antes de comenzar, asegúrese de tener los siguientes requisitos previos:
1.  Groupdocs.Signature para .NET: instale la biblioteca Groupdocs.Signature para .NET. Puedes descargarlo desde[aquí](https://releases.groupdocs.com/signature/net/).
2. Entorno .NET: asegúrese de tener un entorno .NET configurado en su sistema.
3. Documento de hoja de cálculo: tenga listo un documento de hoja de cálculo de muestra que desee firmar con metadatos.
## Importar espacios de nombres
Antes de implementar el código, importe los espacios de nombres necesarios para acceder a las clases y métodos requeridos:
```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
Ahora, dividamos el código de ejemplo en varios pasos para una comprensión más clara:
## Paso 1: cargue el documento de hoja de cálculo
```csharp
string filePath = "sample.xlsx";
string outputFilePath = Path.Combine("Your Document Directory", "SignSpreadsheetWithMetadata", "SignedWithMetadata.xlsx");
using (Signature signature = new Signature(filePath))
{
```
## Paso 2: Definir las opciones de firma de metadatos
```csharp
	// Crear opción de metadatos con texto de metadatos predefinido.
	MetadataSignOptions options = new MetadataSignOptions();
```
## Paso 3: crear firmas de metadatos
```csharp
	// Cree algunas firmas de metadatos de hojas de cálculo
	SpreadsheetMetadataSignature[] signatures = new SpreadsheetMetadataSignature[]
	{
		new SpreadsheetMetadataSignature("Author", "Mr.Scherlock Holmes"), // Valor de cadena
		new SpreadsheetMetadataSignature("CreatedOn", DateTime.Now), // Valores de fecha y hora
		new SpreadsheetMetadataSignature("DocumentId", 123456), // Valor entero
		new SpreadsheetMetadataSignature("SignatureId", 123.456D), // valor doble
		new SpreadsheetMetadataSignature("Amount", 123.456M), // valor decimal
		new SpreadsheetMetadataSignature("Total", 123.456F) // Valor flotante
	};
	options.Signatures.AddRange(signatures);
```
## Paso 4: Firme el documento
```csharp
	// firmar documento para presentar
	SignResult result = signature.Sign(outputFilePath, options);
	Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).\nFile saved at {outputFilePath}.");
}
```
## Conclusión
¡Felicidades! Ha aprendido a firmar una hoja de cálculo con metadatos usando Groupdocs.Signature para .NET. La firma de metadatos mejora la integridad del documento y proporciona información adicional con fines de verificación. Comience a aplicar firmas de metadatos a sus hojas de cálculo hoy y garantice la autenticidad y el contexto de sus documentos.
## Preguntas frecuentes
### ¿Qué es la firma de metadatos?
La firma de metadatos implica incorporar información adicional, como el nombre del autor, la fecha de creación o el ID del documento, en un documento con fines de verificación.
### ¿Puedo personalizar las firmas de metadatos?
Sí, puede personalizar las firmas de metadatos según sus requisitos, incluidos texto, fechas, números enteros, dobles, decimales y flotantes.
### ¿Groupdocs.Signature para .NET es compatible con otros formatos de documentos?
Sí, Groupdocs.Signature para .NET admite varios formatos de documentos, incluidas hojas de cálculo, presentaciones, archivos PDF y más.
### ¿Cómo puedo verificar las firmas de metadatos?
Puede verificar las firmas de metadatos utilizando Groupdocs.Signature u otro software compatible que admita la extracción de metadatos.
### ¿Puedo aplicar firmas de metadatos mediante programación?
Sí, puede aplicar firmas de metadatos mediante programación utilizando la biblioteca Groupdocs.Signature para .NET dentro de sus aplicaciones .NET.