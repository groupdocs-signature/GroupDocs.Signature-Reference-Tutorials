---
title: Eliminar firma digital del documento
linktitle: Eliminar firma digital del documento
second_title: API GroupDocs.Signature .NET
description: Aprenda cómo eliminar firmas digitales de documentos usando GroupDocs.Signature para .NET. Siga nuestra guía paso a paso para una gestión eficiente.
weight: 13
url: /es/net/delete-operations/delete-digital-signature/
---

# Eliminar firma digital del documento

## Introducción
En el mundo de los documentos digitales, garantizar la autenticidad y la seguridad es primordial. Las firmas digitales desempeñan un papel crucial en la verificación de la integridad de los documentos electrónicos. GroupDocs.Signature para .NET ofrece potentes herramientas para gestionar firmas digitales dentro de aplicaciones .NET de manera eficiente.
## Requisitos previos
Antes de sumergirse en el uso de GroupDocs.Signature para .NET para eliminar firmas digitales de documentos, asegúrese de tener lo siguiente:
1. Visual Studio: instale Visual Studio IDE en su sistema.
2.  GroupDocs.Signature para .NET: descargue e instale GroupDocs.Signature para .NET desde[pagina de descarga](https://releases.groupdocs.com/signature/net/).
3. Documento de muestra: prepare un documento de muestra que contenga firmas digitales para realizar pruebas.

## Importar espacios de nombres
Para comenzar, asegúrese de importar los espacios de nombres necesarios en su proyecto .NET:
```csharp
using System;
using System.IO;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
```
## Paso 1: definir rutas de archivos
Comience definiendo las rutas de archivo para el documento de origen y el documento de salida:
```csharp
string filePath = "sample.pdf"_SIGNED_DIGITAL;
string fileName = Path.GetFileName(filePath);
string outputFilePath = Path.Combine("Your Document Directory", "DeleteDigital", fileName);
```
## Paso 2: copie el documento fuente
 desde el`Delete` El método funciona con el mismo documento, es necesario copiar el archivo fuente a una nueva ubicación:
```csharp
File.Copy(filePath, outputFilePath, true);
```
## Paso 3: inicializar el objeto de firma
 Inicializar un`Signature` objeto con la ruta del archivo de salida:
```csharp
using (Signature signature = new Signature(outputFilePath))
{
    // Tu código va aquí
}
```
## Paso 4: busque firmas digitales
Busque firmas digitales electrónicas dentro del documento:
```csharp
List<DigitalSignature> signatures = signature.Search<DigitalSignature>(SignatureType.Digital);
```
## Paso 5: eliminar la firma digital
Si se encuentran firmas digitales, elimine la primera firma encontrada:
```csharp
if (signatures.Count > 0)
{
    DigitalSignature digitalSignature = signatures[0];
    bool result = signature.Delete(digitalSignature);
    if (result)
    {
        Console.WriteLine($"Digital signature #{digitalSignature.Thumbprint} from {digitalSignature.SignTime.ToShortDateString()} was deleted from document ['{fileName}'].");
    }
    else
    {
        Helper.WriteError($"Signature was not deleted from the document! Signature# {digitalSignature.Thumbprint} was not found!");
    }
}
```

## Conclusión
Administrar firmas digitales en aplicaciones .NET se vuelve muy sencillo con GroupDocs.Signature. Si sigue los sencillos pasos descritos anteriormente, puede eliminar sin problemas las firmas digitales de sus documentos, garantizando la integridad y seguridad de los datos.
## Preguntas frecuentes
### ¿Puedo eliminar varias firmas digitales de un solo documento?
Sí, puede modificar el código para recorrer todas las firmas digitales encontradas y eliminarlas en consecuencia.
### ¿GroupDocs.Signature admite otros tipos de firmas además de las digitales?
Sí, GroupDocs.Signature admite varios tipos de firmas, incluidas firmas electrónicas, digitales y manuscritas.
### ¿GroupDocs.Signature es adecuado para la gestión de documentos a nivel empresarial?
Por supuesto, GroupDocs.Signature está diseñado para satisfacer las necesidades tanto de los desarrolladores individuales como de las aplicaciones de nivel empresarial, ofreciendo funciones sólidas y escalabilidad.
### ¿Puedo personalizar el proceso de eliminación de firmas digitales?
Sí, GroupDocs.Signature ofrece una amplia gama de opciones y configuraciones para personalizar el proceso de eliminación de firmas según sus requisitos específicos.
### ¿Existe una versión de prueba disponible para probar GroupDocs.Signature?
 Sí, puedes descargar una versión de prueba gratuita desde[página de lanzamientos](https://releases.groupdocs.com/).