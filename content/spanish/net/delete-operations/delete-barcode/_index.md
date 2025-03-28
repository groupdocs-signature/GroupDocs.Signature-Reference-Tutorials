---
title: Eliminar código de barras del documento
linktitle: Eliminar código de barras del documento
second_title: API GroupDocs.Signature .NET
description: Aprenda cómo eliminar el código de barras de un documento usando GroupDocs.Signature para .NET. Guía paso a paso con ejemplos de código.
weight: 10
url: /es/net/delete-operations/delete-barcode/
---

# Eliminar código de barras del documento

## Introducción
GroupDocs.Signature para .NET es una potente biblioteca que permite a los desarrolladores trabajar sin problemas con firmas digitales, sellos y códigos de barras dentro de aplicaciones .NET. En este tutorial, lo guiaremos a través del proceso de eliminar un código de barras de un documento usando GroupDocs.Signature para .NET.
## Requisitos previos
Antes de comenzar, asegúrese de tener los siguientes requisitos previos:
- Conocimientos básicos del lenguaje de programación C#.
- Visual Studio instalado en su sistema.
-  Biblioteca GroupDocs.Signature para .NET instalada. Puedes descargarlo desde[aquí](https://releases.groupdocs.com/signature/net/).
- Un documento de muestra con un código de barras que desea eliminar.

## Importar espacios de nombres
Primero, asegúrese de importar los espacios de nombres necesarios en su código C#:
```csharp
using System;
using System.IO;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

Dividamos el proceso de eliminar un código de barras de un documento en pasos simples:
## Paso 1: definir rutas de archivos
```csharp
string filePath = "sample_multiple_signatures.docx";
string fileName = Path.GetFileName(filePath);
string outputFilePath = Path.Combine("Your Document Directory", "DeleteBarcode", fileName);
```
 Asegúrese de reemplazar`"sample_multiple_signatures.docx"` con la ruta a su documento que contiene el código de barras.
## Paso 2: copie el archivo fuente
```csharp
File.Copy(filePath, outputFilePath, true);
```
Este paso asegura que estamos trabajando con una copia del documento original para preservar el archivo original.
## Paso 3: Inicializar GroupDocs.Signature
```csharp
using (Signature signature = new Signature(outputFilePath))
{
    // Tu código va aquí
}
```
Inicialice el objeto Firma pasando la ruta a la copia del documento creada en el paso anterior.
## Paso 4: busque firmas de códigos de barras
```csharp
BarcodeSearchOptions options = new BarcodeSearchOptions();
List<BarcodeSignature> signatures = signature.Search<BarcodeSignature>(options);
```
Cree una instancia de BarcodeSearchOptions y utilícela para buscar firmas de códigos de barras dentro del documento.
## Paso 5: eliminar la firma del código de barras
```csharp
if (signatures.Count > 0)
{
    BarcodeSignature barcodeSignature = signatures[0];
    bool result = signature.Delete(barcodeSignature);
    if (result)
    {
        Console.WriteLine($"Signature with Barcode '{barcodeSignature.Text}' and encode type '{barcodeSignature.EncodeType.TypeName}' was deleted from document ['{fileName}'].");
    }
    else
    {
        Helper.WriteError($"Signature was not deleted from the document! Signature with Barcode '{barcodeSignature.Text}' and encode type '{barcodeSignature.EncodeType.TypeName}' was not found!");
    }
}
```
Compruebe si se encuentran firmas de códigos de barras en el documento. Si la encuentra, elimine la primera firma de código de barras encontrada.

## Conclusión
En este tutorial, aprendimos cómo eliminar un código de barras de un documento usando GroupDocs.Signature para .NET. Si sigue la guía paso a paso, podrá integrar perfectamente la funcionalidad de eliminación de códigos de barras en sus aplicaciones .NET.
## Preguntas frecuentes
### ¿Puedo eliminar varias firmas de códigos de barras de un documento?
Sí, puede modificar el código para eliminar varias firmas de códigos de barras iterando sobre la lista de firmas.
### ¿GroupDocs.Signature para .NET admite otros tipos de firmas?
Sí, GroupDocs.Signature para .NET admite varios tipos de firmas, incluidas firmas digitales, sellos y firmas de texto.
### ¿Puedo personalizar las opciones de búsqueda de firmas de códigos de barras?
Sí, puede personalizar las opciones de búsqueda según sus requisitos, como especificar tipos de códigos de barras o áreas de búsqueda dentro del documento.
### ¿GroupDocs.Signature para .NET es compatible con diferentes formatos de documentos?
Sí, GroupDocs.Signature para .NET admite una amplia gama de formatos de documentos, incluidos Word, Excel, PDF y más.
### ¿Dónde puedo encontrar soporte o recursos adicionales para GroupDocs.Signature para .NET?
 Puedes visitar el foro GroupDocs.Signature[aquí](https://forum.groupdocs.com/c/signature/13) para cualquier consulta o ayuda sobre la biblioteca.