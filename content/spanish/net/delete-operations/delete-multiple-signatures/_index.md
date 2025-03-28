---
title: Eliminar varias firmas del documento
linktitle: Eliminar varias firmas del documento
second_title: API GroupDocs.Signature .NET
description: Elimine sin esfuerzo varias firmas de documentos utilizando GroupDocs.Signature para .NET. Optimice su flujo de trabajo de gestión de documentos.
weight: 15
url: /es/net/delete-operations/delete-multiple-signatures/
---

# Eliminar varias firmas del documento

## Introducción
En el mundo digital, la gestión documental suele implicar la manipulación de varias firmas. Eliminar varias firmas de un documento mediante programación puede optimizar los flujos de trabajo y mejorar la eficiencia. Con GroupDocs.Signature para .NET, esta tarea se vuelve sencilla y sencilla. Este tutorial lo guiará paso a paso a través del proceso de eliminar múltiples firmas de un documento.
## Requisitos previos
Antes de sumergirse en el tutorial, asegúrese de tener los siguientes requisitos previos:
- Conocimientos básicos del lenguaje de programación C#.
- Se instaló la biblioteca GroupDocs.Signature para .NET.
- Documento de muestra con múltiples firmas para pruebas.

## Importar espacios de nombres
Comience importando los espacios de nombres necesarios para acceder a la funcionalidad de GroupDocs.Signature para .NET:
```csharp
using System;
using System.IO;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## Paso 1: definir la ruta del documento y el nombre del archivo
Establezca la ruta del archivo del documento que contiene varias firmas. Asegúrese de tener la ruta de archivo y el nombre de archivo adecuados:
```csharp
string filePath = "sample_multiple_signatures.docx";
string fileName = Path.GetFileName(filePath);
```
## Paso 2: Copie el documento para su procesamiento
Para evitar modificar el documento original, cree una copia para su procesamiento:
```csharp
string outputFilePath = Path.Combine("Your Document Directory", "DeleteMultiple", fileName);
File.Copy(filePath, outputFilePath, true);
```
## Paso 3: inicializar el objeto de firma
Cree una instancia de un objeto Firma utilizando la ruta del archivo de salida:
```csharp
using (Signature signature = new Signature(outputFilePath))
{
    // El código de procesamiento de firma va aquí
}
```
## Paso 4: definir las opciones de búsqueda
Defina varias opciones de búsqueda para identificar firmas dentro del documento. Las opciones incluyen búsqueda de texto, búsqueda de imágenes, búsqueda de códigos de barras y búsqueda de códigos QR:
```csharp
TextSearchOptions textSearchOptions = new TextSearchOptions();
ImageSearchOptions imageSearchOptions = new ImageSearchOptions();
BarcodeSearchOptions barcodeOptions = new BarcodeSearchOptions();
QrCodeSearchOptions qrCodeOptions = new QrCodeSearchOptions();
// Agregar opciones a la lista
List<SearchOptions> listOptions = new List<SearchOptions>();
listOptions.Add(textSearchOptions);
listOptions.Add(imageSearchOptions);
listOptions.Add(barcodeOptions);
listOptions.Add(qrCodeOptions);
```
## Paso 5: buscar firmas
Ejecute una operación de búsqueda para encontrar todas las firmas dentro del documento según las opciones de búsqueda definidas:
```csharp
SearchResult result = signature.Search(listOptions);
```
## Paso 6: eliminar firmas
Si se encuentran firmas, proceda a eliminarlas:
```csharp
if (result.Signatures.Count > 0)
{
    // Intenta eliminar todas las firmas
    DeleteResult deleteResult = signature.Delete(result.Signatures);
    //Compruebe si la eliminación fue exitosa
    if(deleteResult.Succeeded.Count == result.Signatures.Count)
    {
        Console.WriteLine("\nAll signatures were successfully deleted!");                        
    }
    else
    {
        Console.WriteLine($"Successfully deleted signatures : {deleteResult.Succeeded.Count}");
        Helper.WriteError($"Not deleted signatures : {deleteResult.Failed.Count}");
    }
    // Mostrar información sobre firmas eliminadas
    Console.WriteLine("\nList of deleted signatures:");
    int number = 1;
    foreach(BaseSignature temp in deleteResult.Succeeded)
    {
        Console.WriteLine($"Signature #{number++}: Type: {temp.SignatureType} Id:{temp.SignatureId}, Location: {temp.Left}x{temp.Top}. Size: {temp.Width}x{temp.Height}");
    }
}
else
{
    Helper.WriteError("No one signature was found.");
}
```

## Conclusión
Eliminar varias firmas de un documento mediante programación es una tarea crucial en la gestión de documentos. Con GroupDocs.Signature para .NET, este proceso se vuelve eficiente y confiable. Si sigue los pasos descritos en este tutorial, podrá integrar fácilmente la funcionalidad de eliminación de firmas en sus aplicaciones .NET.
## Preguntas frecuentes
### ¿Puede GroupDocs.Signature para .NET manejar varios formatos de documentos?
Sí, GroupDocs.Signature para .NET admite una amplia gama de formatos de documentos, incluidos DOCX, PDF, PPTX, XLSX y más.
### ¿Es posible personalizar las opciones de búsqueda para la detección de firmas?
Por supuesto, puede personalizar las opciones de búsqueda, como la búsqueda de texto, la búsqueda de imágenes, la búsqueda de códigos de barras y la búsqueda de códigos QR, para satisfacer sus necesidades específicas.
### ¿GroupDocs.Signature para .NET proporciona mecanismos de manejo de errores?
Sí, la biblioteca ofrece sólidas capacidades de manejo de errores para garantizar una ejecución fluida de las tareas de procesamiento de documentos.
### ¿Puedo integrar GroupDocs.Signature para .NET con otras bibliotecas de terceros?
Ciertamente, GroupDocs.Signature para .NET está diseñado para integrarse perfectamente con otras bibliotecas .NET, brindando flexibilidad y extensibilidad.
### ¿Dónde puedo encontrar soporte y recursos adicionales para GroupDocs.Signature para .NET?
 Puedes visitar GroupDocs[foro](https://forum.groupdocs.com/c/signature/13) dedicado a debates relacionados con firmas y buscar ayuda de la comunidad y expertos.