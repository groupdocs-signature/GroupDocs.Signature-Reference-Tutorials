---
title: Eliminar la firma del código QR del documento
linktitle: Eliminar la firma del código QR del documento
second_title: API GroupDocs.Signature .NET
description: Aprenda cómo eliminar firmas de códigos QR de documentos usando GroupDocs.Signature para .NET. Siga nuestra guía paso a paso para una gestión eficiente de firmas.
weight: 16
url: /es/net/delete-operations/delete-qr-code-signature/
---

# Eliminar la firma del código QR del documento

## Introducción
En este tutorial, lo guiaremos a través del proceso de eliminar una firma de código QR de un documento usando GroupDocs.Signature para .NET. Siga estas instrucciones paso a paso para eliminar eficazmente las firmas de códigos QR.
## Requisitos previos
Antes de comenzar, asegúrese de tener los siguientes requisitos previos:
-  GroupDocs.Signature para .NET: asegúrese de tener la biblioteca GroupDocs.Signature instalada en su proyecto .NET. Puedes descargarlo desde[aquí](https://releases.groupdocs.com/signature/net/).
- Documento con firma de código QR: prepare un documento que contenga firmas de códigos QR que desee eliminar.
- Conocimientos básicos de C#: familiarícese con los conceptos básicos del lenguaje de programación C#.

## Importando espacios de nombres
Antes de profundizar en el código, importe los espacios de nombres necesarios a su archivo C#:
```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## Paso 1: definir rutas de archivos
```csharp
// La ruta al directorio de documentos.
string filePath = "sample_multiple_signatures.docx";
string fileName = Path.GetFileName(filePath);
// Defina la ruta del archivo de salida para el documento modificado.
string outputFilePath = Path.Combine("Your Document Directory", "DeleteQRCode", fileName);
// Copie el archivo fuente ya que el método Eliminar funciona con el mismo documento.
File.Copy(filePath, outputFilePath, true);
```
## Paso 2: inicializar el objeto de firma
```csharp
using (Signature signature = new Signature(outputFilePath))
{
    // Cree opciones para buscar firmas de códigos QR.
    QrCodeSearchOptions options = new QrCodeSearchOptions();
    // Busque firmas de códigos QR en el documento.
    List<QrCodeSignature> signatures = signature.Search<QrCodeSignature>(options);
```
## Paso 3: Verifique la existencia de la firma del código QR
```csharp
    if (signatures.Count > 0)
    {
        // Obtenga la primera firma del código QR que se encuentra en el documento.
        QrCodeSignature qrCodeSignature = signatures[0];
```
## Paso 4: eliminar la firma del código QR
```csharp
        // Elimina la firma del código QR del documento.
        bool result = signature.Delete(qrCodeSignature);
        if (result)
        {
            Console.WriteLine($"Signature with QR-Code '{qrCodeSignature.Text}' and encode type '{qrCodeSignature.EncodeType.TypeName}' was deleted from document ['{fileName}'].");
        }
        else
        {
            Helper.WriteError($"Signature was not deleted from the document! Signature with Barcode '{qrCodeSignature.Text}' and encode type '{qrCodeSignature.EncodeType.TypeName}' was not found!");
        }
    }
}
```
¡Felicidades! Ha eliminado con éxito la firma del código QR del documento utilizando GroupDocs.Signature para .NET.

## Conclusión
En este tutorial, aprendimos cómo eliminar una firma de código QR de un documento usando GroupDocs.Signature para .NET. Si sigue los pasos proporcionados, podrá administrar y manipular firmas de manera eficiente dentro de sus aplicaciones .NET.
## Preguntas frecuentes
### ¿Puedo eliminar varias firmas de códigos QR de un documento?
Sí, puede modificar el código para recorrer todas las firmas de códigos QR y eliminarlas en consecuencia.
### ¿GroupDocs.Signature admite otros tipos de firmas además de los códigos QR?
Sí, GroupDocs.Signature admite varios tipos de firma, como texto, imagen, código de barras y más.
### ¿GroupDocs.Signature es compatible con todos los formatos de documentos?
GroupDocs.Signature admite una amplia gama de formatos de documentos, incluidos PDF, Microsoft Word, Excel, PowerPoint y más.
### ¿Puedo personalizar las opciones de búsqueda de firmas?
Sí, puede adaptar las opciones de búsqueda según sus requisitos para localizar firmas específicas dentro del documento.
### ¿Existe una versión de prueba disponible para GroupDocs.Signature?
 Sí, puede acceder a una versión de prueba gratuita de GroupDocs.Signature desde[aquí](https://releases.groupdocs.com/).