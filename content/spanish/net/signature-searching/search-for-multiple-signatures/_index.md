---
title: Buscar múltiples firmas
linktitle: Buscar múltiples firmas
second_title: API GroupDocs.Signature .NET
description: Aprenda a buscar varias firmas en documentos .NET utilizando GroupDocs.Signature para lograr una seguridad e integridad eficientes en los documentos.
weight: 14
url: /es/net/signature-searching/search-for-multiple-signatures/
---
## Introducción
GroupDocs.Signature para .NET es una potente biblioteca que permite a los desarrolladores agregar, buscar y eliminar varios tipos de firmas en formatos de documentos populares utilizando aplicaciones .NET. En este tutorial, nos centraremos en buscar múltiples firmas dentro de un documento usando GroupDocs.Signature para .NET.
## Requisitos previos
Antes de comenzar, asegúrese de tener los siguientes requisitos previos:
- Visual Studio instalado en su sistema.
- Conocimientos básicos del lenguaje de programación C#.
- Biblioteca GroupDocs.Signature para .NET instalada en su proyecto. Puedes descargarlo desde[aquí](https://releases.groupdocs.com/signature/net/).

## Importar espacios de nombres
Primero, debe importar los espacios de nombres necesarios para acceder a las clases y métodos proporcionados por GroupDocs.Signature para .NET.
```csharp
using System;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## Paso 1: cargue el documento
Cargue el documento donde desea buscar varias firmas. Asegúrese de proporcionar la ruta de archivo correcta.
```csharp
string filePath = "sample_multiple_signatures.docx";
using (Signature signature = new Signature(filePath))
{
    // Tu código va aquí
}
```
## Paso 2: definir las opciones de búsqueda
Defina opciones de búsqueda para varios tipos de firmas, como texto, digital, código de barras, código QR y metadatos. Puede especificar criterios de búsqueda como texto que debe coincidir, tipo de coincidencia y búsqueda en todas las páginas.
```csharp
// Definir opciones de búsqueda
TextSearchOptions textOptions = new TextSearchOptions()
{
    AllPages = true
};
DigitalSearchOptions digitalOptions = new DigitalSearchOptions()
{
    AllPages = true
};
BarcodeSearchOptions barcodeOptions = new BarcodeSearchOptions()
{
    AllPages = true,
    Text = "123456",
    MatchType = TextMatchType.Exact
};
QrCodeSearchOptions qrCodeOptions = new QrCodeSearchOptions()
{
    AllPages = true,
    Text = "John",
    MatchType = TextMatchType.Contains
};
MetadataSearchOptions metadataOptions = new MetadataSearchOptions();
```
## Paso 3: agregar opciones de búsqueda a la lista
Agregue las opciones de búsqueda definidas a una lista.
```csharp
// Agregar opciones a la lista
List<SearchOptions> listOptions = new List<SearchOptions>();
listOptions.Add(textOptions);
listOptions.Add(barcodeOptions);
listOptions.Add(qrCodeOptions);
listOptions.Add(metadataOptions);
listOptions.Add(digitalOptions);
```
## Paso 4: buscar firmas
Busque firmas en el documento utilizando las opciones de búsqueda definidas.
```csharp
// Buscar firmas en el documento.
SearchResult result = signature.Search(listOptions);
if (result.Signatures.Count > 0)
{
    Console.WriteLine($"\nSource document ['{filePath}'] contains following signatures.");
    foreach (var resSignature in result.Signatures)
    {
        Console.WriteLine($"Signature found at page {resSignature.PageNumber} with type {resSignature.SignatureType} and Id#: {resSignature.SignatureId}");
    }
}
else
{
    Helper.WriteError("No one signature was found.");
}
```

## Conclusión
En este tutorial, aprendimos cómo buscar varias firmas dentro de un documento usando GroupDocs.Signature para .NET. Si sigue los pasos proporcionados, podrá localizar de manera eficiente varios tipos de firmas en sus documentos, mejorando la seguridad e integridad de los documentos.
## Preguntas frecuentes
### ¿Puedo buscar firmas en diferentes formatos de documentos?
Sí, GroupDocs.Signature para .NET admite una amplia gama de formatos de documentos, incluidos Word, PDF, Excel y más.
### ¿Es posible personalizar los criterios de búsqueda de firmas?
Por supuesto, puede adaptar los criterios de búsqueda según sus requisitos, como especificar coincidencias de texto exactas o buscar en todas las páginas.
### ¿GroupDocs.Signature para .NET ofrece soporte para firmas digitales?
Sí, puede buscar firmas digitales y otros tipos, como firmas de texto, códigos de barras y códigos QR.
### ¿Puedo integrar fácilmente la funcionalidad de búsqueda de firmas en mis aplicaciones .NET?
Sí, GroupDocs.Signature para .NET proporciona una API sencilla que simplifica el proceso de integración.
### ¿Dónde puedo encontrar soporte o asistencia adicional?
 Puedes visitar el foro GroupDocs.Signature[aquí](https://forum.groupdocs.com/c/signature/13) para cualquier consulta o ayuda.