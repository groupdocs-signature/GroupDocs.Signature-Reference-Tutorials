---
title: Eliminar firma por ID
linktitle: Eliminar firma por ID
second_title: API GroupDocs.Signature .NET
description: Aprenda cómo eliminar una firma por ID en documentos .NET usando la biblioteca GroupDocs.Signature. Guía sencilla paso a paso.
type: docs
weight: 11
url: /es/net/delete-operations/delete-signature-by-id/
---
## Introducción
En este tutorial, exploraremos cómo eliminar una firma por su ID usando GroupDocs.Signature para .NET. GroupDocs.Signature para .NET es una potente biblioteca que permite a los desarrolladores agregar, eliminar o verificar firmas digitales en varios formatos de documentos utilizando aplicaciones .NET.
## Requisitos previos
Antes de comenzar, asegúrese de tener los siguientes requisitos previos:
1.  GroupDocs.Signature para la biblioteca .NET: descargue e instale la biblioteca desde[aquí](https://releases.groupdocs.com/signature/net/).
2. .NET Framework: asegúrese de tener .NET Framework instalado en su sistema.
3. Documento con firma: prepare un documento (p. ej., DOCX, PDF) con una firma que desee eliminar.

## Importar espacios de nombres
```csharp
using System;
using System.IO;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## Paso 1: definir rutas de archivos
Primero, especifique la ruta del archivo para el documento que contiene la firma y la ruta del archivo de salida donde se guardará el documento modificado.
```csharp
string filePath = "sample_multiple_signatures.docx";
string fileName = Path.GetFileName(filePath);
string outputFilePath = Path.Combine("Your Document Directory", "DeleteById", fileName);
```
## Paso 2: copie el documento
 desde el`Delete` método modifica el documento en su lugar, es mejor crear una copia del documento original.
```csharp
File.Copy(filePath, outputFilePath, true);
```
## Paso 3: Eliminar firma por ID
 Inicializar el`Signature` objeto con la ruta del archivo del documento y utilice el`Delete` Método para eliminar la firma por su ID.
```csharp
using (Signature signature = new Signature(outputFilePath))
{
    string id = @"eff64a14-dad9-47b0-88e5-2ee4e3604e71";
    bool result = signature.Delete(id);
    if (result)
    {
        Console.WriteLine($"Signature with Id# '{id}' was deleted from document ['{fileName}'].");
    }
    else
    {
        Helper.WriteError($"Signature was not deleted from the document! Signature with id# '{id}' was not found!");
    }
}
```

## Conclusión
En este tutorial, aprendimos cómo eliminar una firma por su ID usando GroupDocs.Signature para .NET. Esta biblioteca proporciona una manera conveniente de administrar firmas digitales en varios formatos de documentos mediante programación.
## Preguntas frecuentes
### ¿Puedo eliminar varias firmas a la vez?
 Sí, puede eliminar varias firmas recorriendo sus ID y llamando al`Delete` método para cada ID.
### ¿GroupDocs.Signature para .NET es compatible con todos los formatos de documentos?
GroupDocs.Signature para .NET admite una amplia gama de formatos de documentos, incluidos PDF, DOCX, XLSX y más.
### ¿Puedo personalizar la apariencia de la firma?
Sí, puedes personalizar la apariencia de la firma, incluida su posición, tamaño, fuente y color.
### ¿Hay una versión de prueba disponible?
 Sí, puedes descargar una versión de prueba gratuita desde[aquí](https://releases.groupdocs.com/).
### ¿Dónde puedo encontrar ayuda o soporte para GroupDocs.Signature para .NET?
 Puedes visitar el foro de soporte.[aquí](https://forum.groupdocs.com/c/signature/13) para asistencia.